---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
# AWS Cost Anomaly Detection: Người gác cổng giúp bạn không bị dính hóa đơn AWS bất ngờ

Chắc hẳn ai học AWS cũng từng nghe câu chuyện: bật một GPU instance để train model qua đêm, xong quên tắt; hoặc auto scaling group tự phình to trong lúc load test rồi không ai nhớ scale lại; đến cuối tháng mở AWS Billing lên, cost tăng bất thường. Đây chính là cost anomaly — chi phí phát sinh bất thường.

Hôm nay mình giới thiệu AWS Cost Anomaly Detection (CAD) — một công cụ hoàn toàn miễn phí trong AWS Billing and Cost Management, dùng machine learning để tự học "nhịp chi tiêu" bình thường của bạn và báo động ngay khi có gì đó bất thường, thay vì để bạn tự phát hiện qua hóa đơn cuối tháng.

### 1. CAD khác gì so với việc tự đặt ngưỡng cảnh báo (AWS Budgets)?

Nhiều bạn mới dùng AWS thường nhầm CAD với AWS Budgets — nhưng hai công cụ này giải quyết hai bài toán khác nhau:
{{< figure
  src="/images/3.3.2.jpg"
  alt="AWS Budgets"
  class="image-70"
  caption="Hình 1. AWS Budgets sử dụng các ngưỡng cố định, trong khi Cost Anomaly Detection sử dụng máy học để phát hiện các mô hình chi tiêu bất thường."
>}}
* AWS Budgets: bạn tự đặt một ngưỡng cố định. Đơn giản, nhưng ngưỡng cố định không phản ánh được việc chi tiêu của bạn vốn dao động tự nhiên theo thời gian (ví dụ: cuối tuần train model nhiều hơn ngày thường).
* Cost Anomaly Detection: không dùng ngưỡng cố định, mà xây dựng một baseline (đường cơ sở chi tiêu bình thường) từ dữ liệu lịch sử bằng machine learning, rồi so sánh chi tiêu thực tế với mức dự đoán cho từng khung thời gian. Nhờ vậy, CAD hiểu được rằng chi phí EC2 của bạn vốn tăng đều vào mỗi sáng thứ Hai vì batch job chạy định kỳ — và sẽ không báo động cho việc đó. Nhưng nếu đột nhiên có một pattern data-transfer lạ trên S3 khiến bill tăng gấp 3 lúc 2 giờ sáng thứ Bảy, CAD sẽ phát hiện ngay.

Nói cách khác: Budgets phù hợp làm "lưới an toàn" cứng khi bạn mới có tài khoản, còn CAD phát huy tác dụng tốt nhất khi bạn đã có ít nhất vài tuần dữ liệu chi tiêu để model học được nhịp điệu bình thường của bạn — cả hai nên dùng song song, không thay thế nhau.

### 2. Cơ chế hoạt động

Pipeline của CAD gồm các bước:

1. Thu thập dữ liệu: CAD lấy dữ liệu billing và usage chi tiết trên toàn bộ account/service đang giám sát.
2. Phân tích lịch sử: mô hình machine learning học từ vài tuần đến vài tháng dữ liệu chi tiêu quá khứ để xây baseline hành vi.
3. Phát hiện bất thường: mô hình liên tục dự đoán mức chi tiêu kỳ vọng cho khung thời gian tiếp theo (thường là theo ngày) và so sánh với chi tiêu thực tế.
4. Cảnh báo & phân tích nguyên nhân gốc (root cause): nếu độ lệch vượt ngưỡng bạn đặt, CAD gửi cảnh báo kèm gợi ý service/tài nguyên nào đang gây ra bất thường.

Một cải tiến đáng chú ý AWS công bố cuối 2025: thuật toán chuyển sang so sánh theo cửa sổ trượt 24 giờ (rolling 24-hour window) thay vì so theo ngày lịch cố định — giúp phát hiện nhanh hơn (không phải chờ hết ngày mới so sánh được) và chính xác hơn (so đúng khung giờ tương ứng, tránh nhầm lẫn giữa pattern buổi sáng và buổi tối).

### 3. Bốn loại Monitor — chọn đúng "góc nhìn" chi phí
{{< figure
  src="/images/3.3.1.jpg"
  alt="Cost Monitor"
  class="image-70"
  caption="Hình 2. Tạo công cụ giám sát chi phí trong AWS Billing and Cost Management."
>}} 
Khi tạo Cost Monitor, bạn chọn 1 trong 4 chiều để giám sát:

* AWS Services: theo dõi bất thường theo từng service riêng lẻ (EC2, S3, RDS...) — phù hợp nhất cho tài khoản cá nhân/học tập vì đơn giản, không cần cấu trúc tổ chức phức tạp.
* Linked Account: theo dõi chi tiêu qua nhiều account con trong một AWS Organization — hữu ích khi công ty có nhiều team, mỗi team một account riêng.
* Cost Allocation Tag: theo dõi theo tag bạn tự gắn (ví dụ Environment=Production, Project=X) — giúp biết chính xác dự án/nhóm nào đang phát sinh bất thường thay vì chỉ biết "EC2 tăng" chung chung.
* Cost Category: nhóm chi phí theo cấu trúc nghiệp vụ tự định nghĩa (kết hợp account, tag, service...).

Một điểm hay: kể từ khi AWS mở rộng AWS managed monitors cho cả 4 loại trên (trước đó managed monitor chỉ có ở AWS Services), bạn có thể tạo một monitor "tự động bao phủ" toàn bộ account/tag mới phát sinh sau này mà không cần tạo lại thủ công — rất hợp khi tổ chức của bạn liên tục thêm account hoặc dự án mới.

Lưu ý về giới hạn: mỗi account tối đa 1 AWS Service Monitor + 500 custom monitor (tổng tối đa 501 monitor), và có thể gắn tất cả vào cùng một alert subscription.

### 4. Thiết lập cảnh báo
{{< figure
  src="/images/3.3.3.jpg"
  alt="Cấu hình"
  class="image-70"
  caption="Hình 3. Cấu hình Alert Subscription để nhận cảnh báo chi phí bất thường."
>}} 
Sau khi tạo monitor, bạn cấu hình Alert Subscription gồm:
* Kênh nhận cảnh báo: email hoặc SNS (từ SNS có thể forward tiếp qua AWS Chatbot vào Slack).
* Ngưỡng kích hoạt: theo số tiền tuyệt đối, theo phần trăm chênh lệch so với dự đoán, hoặc kết hợp cả hai (ví dụ: "chỉ báo khi mức tăng vượt 40% VÀ vượt 100 USD" — cách kết hợp này giúp giảm cảnh báo giả cho các dao động nhỏ nhưng vẫn bắt được các đợt tăng thực sự đáng kể).
* Tần suất: theo thời gian thực (immediate), tổng hợp theo ngày, hoặc theo tuần.

Riêng với tài khoản Cost Explorer mới, AWS đã tự động bật sẵn một AWS Services Monitor kèm alert email hàng ngày mặc định, nên nhiều khi bạn đã có CAD chạy ngầm mà không để ý.

### 5. Những giới hạn cần biết — CAD không phải "lá chắn" hoàn hảo

Để dùng đúng kỳ vọng, có vài điểm CAD không làm được:
* Không ngăn chặn chi tiêu chủ động — CAD chỉ phát hiện và cảnh báo sau khi chi phí đã phát sinh, không tự động dừng hay giới hạn tài nguyên như một "cầu dao" thực sự.
* Có độ trễ — dữ liệu billing cần thời gian xử lý, nên thường có độ trễ vài giờ đến khoảng 1 ngày; một đợt chi tiêu bất thường vào tối thứ Bảy có thể chỉ được báo vào sáng thứ Hai.
* Monitor mới cần thời gian "làm quen" — một monitor mới tạo có thể mất tới 24 giờ mới bắt đầu hoạt động, và với một service hoàn toàn mới trong account, CAD cần khoảng 10 ngày dữ liệu lịch sử trước khi có thể phát hiện bất thường cho service đó.
* Không tính unit economics — CAD không tự quy đổi chi phí về "chi phí trên mỗi khách hàng/feature", nên nếu cần phân tích ở mức đó, bạn vẫn cần thêm công cụ FinOps chuyên sâu hoặc tự xây dashboard riêng.

### 6. Vài khuyến nghị thực tế cho tài khoản cá nhân/học tập

* Bắt đầu với AWS Services Monitor (mặc định, đơn giản, không cần cấu trúc tag phức tạp).
* Đặt ngưỡng cảnh báo kết hợp cả số tiền tuyệt đối lẫn phần trăm, và đừng đặt ngưỡng tiền quá thấp (vài USD) cho tài khoản học tập — vì baseline chi tiêu vốn đã rất nhỏ, ngưỡng thấp dễ gây báo động giả liên tục.
* Trong lúc mới tạo tài khoản (chưa đủ dữ liệu lịch sử để CAD học), hãy dùng thêm AWS Budgets với ngưỡng cứng làm lưới an toàn tạm thời — ví dụ chặn ở mức 5-10 USD — song song với CAD.
* Nếu học/làm việc trong một AWS Organization có nhiều account (như môi trường lab của trường hoặc công ty), nên tạo thêm Cost Allocation Tag Monitor theo tag `Project` hoặc `Team` để khi có cảnh báo, biết ngay dự án nào đang gây bất thường thay vì phải dò cả account.

### 7. Kết luận

CAD không thay thế được ý thức tắt tài nguyên sau khi dùng xong, nhưng nó là một lớp phòng vệ tự động, miễn phí, đáng bật lên ngay từ ngày đầu tạo tài khoản AWS — đặc biệt hữu ích với các bạn đang thực tập hoặc làm đồ án hay phải bật các instance GPU/big data tốn kém trong thời gian ngắn. Chi phí lớn nhất trong quá trình học AWS thường không đến từ việc thiếu kiến thức, mà từ việc quên tắt một thứ gì đó — và đây chính là công cụ được sinh ra để bắt lỗi quên đó sớm nhất có thể.

**Lưu ý về độ tin cậy:** cơ chế thuật toán, các loại monitor và giới hạn nêu trên mình tổng hợp từ tài liệu chính thức AWS (docs.aws.amazon.com, trang What's New) và một số bài phân tích kỹ thuật từ các nền tảng FinOps bên thứ ba. Vì AWS cập nhật thuật toán CAD khá thường xuyên (đã có ít nhất 2 lần cải tiến độ chính xác/độ trễ chỉ trong năm 2025), một số chi tiết vận hành có thể đã thay đổi — nên kiểm tra lại User Guide chính thức trước khi dựa hoàn toàn vào công cụ này cho tài khoản production.

Cảm ơn mọi người đã đọc! Bạn nào từng bị "dính" hóa đơn bất ngờ vì quên tắt tài nguyên rồi thì chia sẻ thêm kinh nghiệm nhé, chắc ai học AWS cũng có ít nhất một câu chuyện như vậy.

### Tài liệu tham khảo

* https://docs.aws.amazon.com/cost-management/latest/userguide/getting-started-ad.html
* https://aws.amazon.com/aws-cost-management/aws-cost-anomaly-detection/faqs
* https://aws.amazon.com/about-aws/whats-new/2025/11/aws-cost-anomaly-detection-accelerates-anomaly
* https://aws.amazon.com/about-aws/whats-new/2025/07/aws-cost-anomaly-detection-improves-accuracy-model-enhancements
* https://aws.amazon.com/blogs/aws-cloud-financial-management/extending-aws-managed-monitors-in-cost-anomaly-detection/

Link bài viết: https://www.facebook.com/groups/awsstudygroupfcj/permalink/2228079044623722/?rdid=UfKIY40XQuTCrdo9