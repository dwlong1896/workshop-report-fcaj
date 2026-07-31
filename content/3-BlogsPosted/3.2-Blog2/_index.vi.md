---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Amazon Aurora DSQL: Database SQL phân tán active-active, bỏ hẳn cơ chế khóa truyền thống

Nếu từng phải chọn database cho một hệ thống cần chạy ở nhiều region cùng lúc, chắc bạn đã quen với bài toán kinh điển: muốn tốc độ và khả năng scale kiểu serverless thì chọn DynamoDB, nhưng phải học lại tư duy thiết kế (single-table design) và mất hẳn SQL; còn muốn giữ SQL quen thuộc thì chọn RDS/Aurora, nhưng triển khai active-active nhiều region với strong consistency (đảm bảo mọi region đọc/ghi đều thấy dữ liệu mới nhất, không có độ trễ đồng bộ) lại cực kỳ khó làm đúng.

Amazon Aurora DSQL là câu trả lời của AWS cho khoảng trống này — một database SQL serverless, phân tán, hỗ trợ active-active multi-region với strong consistency, nhưng đi kèm một vài đánh đổi kiến trúc mà theo mình bất kỳ ai định dùng cũng nên hiểu rõ trước khi bắt tay vào code.
{{< figure
  src="/images/3.2.1.jpg"
  alt="Tổng quan kiến trúc"
  class="image-70"
  caption="Hình 1. Tổng quan kiến trúc Amazon Aurora DSQL với mô hình active-active multi-region và kiến trúc serverless."
>}} 

### 1. Aurora DSQL là gì?

Nói ngắn gọn: đây là database tương thích PostgreSQL, nhưng tách hoàn toàn phần compute và storage ra kiến trúc phân tán "shared-nothing".

Vài con số đáng chú ý:
* SLA 99,99% cho cluster 1 region, 99,999% cho cluster nhiều region.
* Không cần provision instance, không cần patch, scale tới 0 khi idle — đúng nghĩa serverless.
* Tính phí theo DPU (Distributed Processing Unit) — đơn vị đo công xử lý phân tán, tương tự khái niệm "capacity unit" bạn đã quen ở Aurora Serverless v2, nhưng đo cho hạ tầng phân tán nhiều thành phần hơn — cộng với phí lưu trữ 0,33 USD/GB-tháng. Mỗi tháng có 100.000 DPU + 1GB storage miễn phí vĩnh viễn (không giới hạn 12 tháng như free tier thông thường), đủ cho môi trường dev hoặc app cá nhân traffic thấp.
{{< figure
  src="/images/3.2.2.jpg"
  alt="Kiến trúc shared-nothing"
  class="image-70"
  caption="Hình 2. Kiến trúc shared-nothing của Aurora DSQL, trong đó compute và storage được tách biệt để hỗ trợ khả năng mở rộng và tính sẵn sàng cao."
>}} 

### 2. Điểm khác biệt cốt lõi: OCC thay vì lock truyền thống

Đây là phần quan trọng nhất, vì nó ảnh hưởng trực tiếp tới cách bạn viết code.

PostgreSQL thông thường dùng MVCC (Multi-Version Concurrency Control) kết hợp row-level locking — khi hai transaction cùng sửa một dòng dữ liệu, transaction đến sau phải chờ (block) cho tới khi transaction trước commit hoặc rollback.

Aurora DSQL dùng OCC (Optimistic Concurrency Control — kiểm soát tương tranh theo hướng lạc quan): transaction cứ chạy thoải mái, không cần xin khóa trước; xung đột chỉ được kiểm tra tại thời điểm commit. Nếu hai transaction cùng sửa một dữ liệu, transaction commit trước sẽ thắng, transaction còn lại nhận lỗi serialization error (mã lỗi PostgreSQL chuẩn SQLSTATE 40001, hoặc mã riêng của DSQL như `OC000`/`OC001`) thay vì bị "treo" chờ.

Lợi ích: không bao giờ có deadlock, transaction không bị chặn bởi transaction khác đang chạy chậm. Nhưng cái giá phải trả: ứng dụng của bạn bắt buộc phải tự viết logic retry cho những transaction bị lỗi serialization — đây không phải bug, mà là hành vi được thiết kế sẵn. Nếu bạn có endpoint nào đó cập nhật liên tục cùng một dòng dữ liệu (ví dụ: đếm số lượng tồn kho của một sản phẩm đang hot, hay số dư của một tài khoản giao dịch tần suất cao), tỷ lệ retry sẽ tăng mạnh và throughput thực tế giảm — đây là điểm nghẽn đặc trưng của mọi hệ OCC, không riêng gì DSQL.

Ngoài ra, vì cơ chế lock-free, Aurora DSQL hiện chỉ hỗ trợ snapshot isolation (tương đương mức REPEATABLE READ của PostgreSQL) — không hỗ trợ đầy đủ các isolation level khác như SERIALIZABLE mà một số ứng dụng PostgreSQL cũ có thể đang dựa vào.

### 3. DDL cũng phải chạy bất đồng bộ

Một hệ quả thú vị khác của kiến trúc OCC: DDL (Data Definition Language — các câu lệnh thay đổi cấu trúc như tạo bảng, tạo index) không thể là thao tác khóa trong một hệ phân tán hoàn toàn optimistic. Vì vậy, thay vì CREATE INDEX như PostgreSQL thông thường (chỉ chạy ngay được khi bảng chưa có dữ liệu), Aurora DSQL yêu cầu CREATE INDEX ASYNC — chạy như một background task, không chặn việc đọc/ghi bảng trong lúc index đang được xây dựng.

### 4. Vậy Aurora DSQL còn thiếu gì so với PostgreSQL "xịn"?

Theo tài liệu chính thức và một số kỹ sư đã thử nghiệm thực tế, một số điểm hạn chế đáng lưu ý:
* Không hỗ trợ đầy đủ explicit locking (`SELECT ... FOR UPDATE` và tương tự) theo kiểu PostgreSQL truyền thống, vì mâu thuẫn triết lý với OCC.
* Một số tính năng như sequence, trigger, hàm PL/pgSQL phức tạp còn hạn chế hoặc chưa tương thích hoàn toàn.
* Chỉ có snapshot isolation như đã nói ở trên.

Vì những lý do này, nhiều kỹ sư đã thử nghiệm DSQL đều đưa ra khuyến nghị khá thống nhất: không nên dùng để "lift-and-shift" một ứng dụng PostgreSQL cũ đang chạy production mà không sửa code, vì rủi ro gặp transaction fail do serialization error hoặc thiếu tính năng là khá cao. Ngược lại, với một ứng dụng thiết kế mới từ đầu theo hướng serverless, DSQL là lựa chọn rất đáng cân nhắc.

### 5. Khi nào nên dùng, khi nào không?

Phù hợp:
* Ứng dụng mới, kiến trúc serverless, muốn giữ SQL thay vì học lại NoSQL single-table design.
* Cần active-active multi-region với strong consistency mà không muốn tự xây dựng cơ chế đồng bộ.
* Pattern ghi dữ liệu tương đối phân tán đều (không dồn update liên tục vào cùng một vài dòng/khóa).

Cân nhắc lựa chọn khác (Aurora PostgreSQL, RDS, hoặc DynamoDB) khi:
* Đang migrate một ứng dụng PostgreSQL cũ có nhiều transaction phức tạp, dùng explicit lock, trigger, hoặc cần isolation level khác snapshot.
* Workload có các "hot key" bị update liên tục tần suất cao (bộ đếm, số dư tài khoản giao dịch nhanh) — OCC sẽ khiến tỷ lệ retry tăng cao trong trường hợp này.
{{< figure
  src="/images/3.2.3.jpg"
  alt="Kiến trúc shared-nothing"
  class="image-70"
  caption="Hình 3. So sánh Aurora DSQL với Aurora PostgreSQL và DynamoDB theo kiến trúc, khả năng mở rộng và trường hợp sử dụng."
>}} 
### 6. Kết luận

Aurora DSQL không cố "giả vờ" là PostgreSQL 100% tương thích — AWS đánh đổi một số tính năng và hành vi quen thuộc để đổi lấy kiến trúc serverless thật sự và khả năng active-active multi-region mà trước đây gần như chỉ có các sản phẩm như Google Spanner hay CockroachDB làm được. Với các bạn đang làm đồ án hoặc dự án cá nhân cần thử nghiệm kiến trúc phân tán mà không muốn tốn tiền dựng cluster riêng, free tier vĩnh viễn của DSQL (100.000 DPU + 1GB storage/tháng) là một sân chơi khá tốt để thực hành.

Lưu ý về độ tin cậy: các thông tin về kiến trúc, giới hạn tính năng và giá trong bài mình tổng hợp từ tài liệu chính thức AWS và một số bài viết kỹ thuật của kỹ sư đã trực tiếp thử nghiệm DSQL. Vì đây là dịch vụ còn khá mới (hơn 1 năm kể từ GA) và AWS vẫn đang bổ sung tính năng/mở rộng region đều đặn, một số giới hạn (ví dụ danh sách tính năng PostgreSQL chưa hỗ trợ) có thể đã thay đổi — nên kiểm tra lại trang "PostgreSQL compatibility" chính thức trước khi quyết định dùng cho dự án thật.

Cảm ơn mọi người đã đọc! Bạn nào đã thử viết retry logic cho OCC trong Aurora DSQL rồi thì rất mong nghe thêm kinh nghiệm thực tế, đặc biệt là cách xử lý sao cho code không bị rối vì phải retry ở nhiều tầng.

### Tài liệu tham khảo

* https://aws.amazon.com/about-aws/whats-new/2025/05/amazon-aurora-dsql-generally-available
* https://docs.aws.amazon.com/aurora-dsql/latest/userguide/working-with-concurrency-control.html
* https://docs.aws.amazon.com/aurora-dsql/latest/userguide/working-with.html
* https://docs.aws.amazon.com/aurora-dsql/latest/userguide/working-with-postgresql-compatibility-unsupported-features.html
* https://aws.amazon.com/rds/aurora/dsql/pricing/
