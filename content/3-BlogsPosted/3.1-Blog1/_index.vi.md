---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Amazon S3 Vectors: Khi S3 học cách lưu trữ và tìm kiếm vector

Nếu bạn từng build một ứng dụng RAG (Retrieval-Augmented Generation — kỹ thuật cho LLM "tra cứu" tài liệu ngoài rồi mới trả lời, thay vì chỉ dựa vào kiến thức đã học sẵn) hay một hệ thống semantic search, chắc hẳn bạn đã phải chọn nơi lưu vector embedding — bản biểu diễn số học của văn bản/ảnh/audio sao cho những nội dung có ý nghĩa gần nhau thì nằm gần nhau trong không gian vector. Ví dụ: embedding của câu "con mèo đang ngủ" sẽ nằm gần embedding của "chú mèo con nằm nghỉ" hơn là gần "báo cáo tài chính quý 3".
{{< figure
  src="/images/3.1.2.jpg"
  alt="Không gian vector SE"
  class="image-70"
  caption="Hình 1. Minh họa không gian vector của Sentence Embeddings."
>}} 
Vấn đề là: hầu hết vector database chuyên dụng (Pinecone, Milvus, hay cluster OpenSearch tự vận hành) được thiết kế để phục vụ query tốc độ cao, nên chúng giữ toàn bộ index trong bộ nhớ hoặc trên compute cluster luôn chạy — rất tốn kém khi bạn có hàng trăm triệu đến hàng tỷ vector nhưng phần lớn dữ liệu đó không được query thường xuyên (ví dụ: embedding của toàn bộ tài liệu nội bộ công ty, hay ảnh y tế lưu trữ nhiều năm).

Amazon S3 Vectors (GA từ tháng 12/2025) sinh ra để giải quyết đúng bài toán này: biến S3 — vốn nổi tiếng rẻ và bền — thành nơi lưu trữ vector gốc, không cần dựng thêm cluster riêng.

### 1. S3 Vectors là gì?

S3 Vectors thêm một loại bucket hoàn toàn mới vào S3 — vector bucket — bên cạnh general purpose bucket, directory bucket và table bucket quen thuộc. Ba khái niệm cốt lõi:

* Vector bucket: loại bucket chuyên biệt để lưu và query vector.
* Vector index: bên trong vector bucket, bạn tổ chức dữ liệu thành các index (tương tự "table" trong database) — mỗi lần similarity search sẽ chạy trên một index cụ thể.
* Vector: chính là embedding, kèm theo metadata (key-value, ví dụ: năm xuất bản, tác giả, danh mục) để lọc kết quả sau này.

Điểm đáng chú ý về mặt kỹ thuật: ghi dữ liệu vào S3 Vectors là strongly consistent (đọc ngay lập tức thấy dữ liệu vừa ghi, không có độ trễ đồng bộ như một số hệ phân tán khác), và S3 tự động tối ưu lại cách lưu trữ vector theo thời gian để giữ chi phí thấp kể cả khi dataset phình to.

Về quy mô, một index hỗ trợ tới 2 tỷ vector, một bucket có thể chứa tới 10.000 index. Độ trễ query dao động từ dưới 1 giây (query không thường xuyên) đến khoảng 100ms (query tần suất cao hơn).
{{< figure
  src="/images/3.1.4.jpg"
  alt="Lưu trữ và truy vấn dữ liệu"
  class="image-70"
  caption="Hình 2. Quy trình lưu trữ và truy vấn dữ liệu trong Amazon S3 Vectors."
>}} 
### 2. Cơ chế tính phí — hiểu để không bị bất ngờ trên bill

Đây là phần mình thấy nhiều bạn mới dùng dễ hiểu nhầm nhất, vì S3 Vectors tính phí theo 3 đầu mục riêng biệt, khác hẳn với S3 thông thường:

a) Storage (lưu trữ)
Kích thước một vector = vector data + metadata + key. Ví dụ một vector 1024 chiều (dimension — số lượng giá trị số học biểu diễn embedding đó, mô hình embedding phổ biến như Titan hay Cohere thường ra 1024 hoặc 1536 chiều): mỗi chiều tốn 4 byte → 1024 × 4 byte = 4KB dữ liệu vector thô, cộng thêm metadata và key mới ra tổng dung lượng tính phí.

b) PUT (ghi dữ liệu)
Tính theo GB dữ liệu logic được ghi. Bạn có thể gửi nhiều vector trong một request PUT để tối ưu chi phí — giống nguyên tắc "batch" quen thuộc khi làm việc với DynamoDB hay SQS.

c) Query (truy vấn)
Đây là phần có 3 lớp phí cộng lại: phí cố định mỗi query, phí theo dung lượng dữ liệu được xử lý (tính theo $/TB, và cách tính này tỷ lệ với kích thước cả index, nên index càng lớn thì mỗi query "quét" càng nhiều dữ liệu — nhưng bù lại đơn giá mỗi TB giảm dần khi index vượt mốc 100 nghìn và 10 triệu vector), và phí theo dữ liệu trả về (512KB đầu tiên mỗi query được miễn phí).

Ví dụ cụ thể theo tài liệu giá chính thức: một hệ thống RAG có 10 triệu vector (mỗi vector ~6.17KB gồm vector data + metadata + key), chia thành 40 index cho 40 khách hàng, cập nhật lại dữ liệu mỗi 6 tháng, chạy 1 triệu query/tháng (trả về 100 kết quả/query) — tổng chi phí ước tính rơi vào khoảng 11 USD/tháng cho cả lưu trữ, ghi và truy vấn ở khu vực US East (N. Virginia). Con số này giúp hình dung: chi phí chủ yếu đến từ khối lượng query, không phải từ việc lưu trữ — nên nếu ứng dụng của bạn ít query nhưng lưu nhiều, S3 Vectors sẽ rất rẻ; ngược lại nếu bạn query liên tục với tần suất cao, chi phí sẽ tăng nhanh và có thể một vector database chuyên dụng (trả phí theo compute cố định) lại kinh tế hơn.

### 3. Tích hợp sẵn với hệ sinh thái AWS

Thay vì phải tự viết pipeline đồng bộ, S3 Vectors đã tích hợp sẵn với:

* Amazon Bedrock Knowledge Bases: chọn thẳng một vector index của S3 Vectors làm vector store khi tạo Knowledge Base cho RAG, không cần dựng thêm hạ tầng.
* Amazon OpenSearch Service: dùng S3 Vectors làm lớp lưu trữ chi phí thấp, rồi export snapshot sang OpenSearch Serverless khi cần QPS (số query mỗi giây) cao và độ trễ thấp cho phần dữ liệu "nóng".
* Bảo mật quản lý qua IAM như các resource S3 khác, nhưng nằm trong namespace `s3vectors` riêng, nên bạn viết policy riêng cho vector bucket mà không ảnh hưởng tới policy S3 thông thường đang có. Ngoài ra Block Public Access luôn được bật mặc định và không thể tắt.

{{< figure
  src="/images/3.1.3.jpg"
  alt="Kiến trúc hoạt động"
  class="image-70"
  caption="Hình 3. Kiến trúc hoạt động của Amazon S3 Vectors."
>}}
{{< figure
  src="/images/3.1.1.jpg"
  alt="Kiến trúc hệ thống RAG"
  class="image-70"
  caption="Hình 4. Kiến trúc hệ thống RAG sử dụng Amazon Bedrock Knowledge Bases."
>}}

### 4. Use case thực tế

Theo tài liệu AWS, các use case điển hình cho similarity search bằng S3 Vectors gồm:

* Tìm ảnh y tế tương tự nhau trong hàng triệu ảnh để hỗ trợ chẩn đoán.
* Phát hiện nội dung vi phạm bản quyền trong kho media lớn.
* Loại bỏ ảnh trùng lặp hoặc gần trùng trong bộ dữ liệu ảnh khổng lồ.
* Tìm cảnh cụ thể trong video dài (video understanding).
* Semantic search trong tài liệu nội bộ doanh nghiệp — tìm theo ý nghĩa thay vì từ khóa chính xác.
* Gợi ý sản phẩm/nội dung tương tự (personalization).

### 5. Vậy khi nào nên dùng S3 Vectors, khi nào không?

Nên dùng khi:
* Dataset lớn (hàng chục triệu đến hàng tỷ vector) nhưng phần lớn được query không thường xuyên — ví dụ dữ liệu lưu trữ lâu dài, tài liệu archive, log lịch sử.
* Bạn muốn tránh vận hành một cluster vector database riêng (patching, scaling, high availability) chỉ để phục vụ vài query mỗi phút.
* Đang dùng Bedrock Knowledge Bases và muốn giảm chi phí vector store cho RAG.

Cân nhắc dùng vector database chuyên dụng (OpenSearch, Milvus, Pinecone...) khi:
* Ứng dụng cần QPS rất cao, độ trễ vài chục mili-giây ổn định (ví dụ: gợi ý sản phẩm real-time trên trang thương mại điện tử có traffic lớn).
* Cần các tính năng tìm kiếm nâng cao như hybrid search (kết hợp full-text + vector), aggregation, faceted search phức tạp — đây là điểm AWS cũng khuyến nghị nên dùng OpenSearch.

Một kiến trúc thực tế nhiều team đang áp dụng: lưu toàn bộ vector trong S3 Vectors làm "nguồn sự thật" chi phí thấp, rồi chỉ export phần dữ liệu đang "hot" (được truy vấn nhiều) sang OpenSearch Serverless để phục vụ tốc độ cao — kết hợp cả hai thay vì chọn một.

### 6. Kết luận

S3 Vectors không nhắm tới việc thay thế hoàn toàn các vector database chuyên dụng, mà lấp vào khoảng trống: lưu trữ vector ở quy mô lớn với chi phí gần với chi phí lưu trữ object thông thường, thay vì chi phí của một cluster compute luôn bật. Với các bạn đang làm đồ án hoặc dự án liên quan đến RAG/semantic search mà ngân sách hạn chế, đây là lựa chọn đáng thử trước khi nhảy thẳng vào một vector database trả phí theo compute.

**Lưu ý về độ tin cậy:** các con số kỹ thuật (giới hạn số vector/index, độ trễ, công thức tính phí) mình lấy trực tiếp từ tài liệu và trang giá chính thức của AWS tại thời điểm viết bài. Vì đây là dịch vụ khá mới (GA chưa lâu), một số giới hạn/mức giá có thể được AWS điều chỉnh theo thời gian — nên kiểm tra lại trang tài liệu/giá chính thức trước khi đưa vào tính toán ngân sách thật.

Cảm ơn mọi người đã đọc! Bạn nào đã thử S3 Vectors cho project cá nhân rồi thì rất mong nghe thêm trải nghiệm thực tế, nhất là về độ trễ query khi index lớn dần.

### Tài liệu tham khảo

* https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-vectors.html
* https://aws.amazon.com/s3/pricing/
* https://aws.amazon.com/about-aws/whats-new/2025/12/amazon-s3-vectors-generally-available/
* https://aws.amazon.com/s3/features/vectors

...Hình ảnh...

Link bài viết: https://www.facebook.com/groups/awsstudygroupfcj/permalink/2225204894911137/?rdid=cg8lX8UFeXdY4OIr#

...Hướng dẫn...