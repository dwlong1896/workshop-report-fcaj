---
title: "Event 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Bài thu hoạch “Chung kết cuộc thi Cloud Architect và Meeting”

### Mục Đích Của Sự Kiện

- Chung kết cuộc thi Cloud Architect
- Tăng cường bảo mật các ứng dụng web với AWS Security Agent
- Giới thiệu về Service Level Agreement (SLA) và Monitoring
- Giới thiệu Lộ trình chinh phục chứng chỉ AWS Cloud Practitioner một cách hiệu quả

### Danh Sách Diễn Giả

- **Thinh Nguyen** - DevOps/DevSecOps/Cloud Engineer, Styl Solutions First Cloud AI Journey
- **Ngo Le Tan Huy** - Admin First Cloud AI Journey
- **Nguyen Huynh Son** - Admin First Cloud AI Journey

### Nội Dung Nổi Bật
#### Chung kết cuộc thi Cloud Architect
- Cuộc tranh tài giữa 2 đội KAKAT và Ngũ đại hiệp diễn ra vô cùng gay cấn
- Những câu hỏi hóc búa xoay quanh kiến trúc hệ thống, bảo mật, và các dịch vụ AWS


#### Tăng cường bảo mật các ứng dụng web với AWS Security Agent
##### Giới thiệu về Frontier Agent

- Tự động suy luận, sử dụng Amazon Bedrock để lập kế hoạch và thực hiện tác vụ mà không cần con người can thiệp.
- Vòng đời đầy đủ bao gồm đánh giá thiết kế, bảo mật mã nguồn và kiểm thử xâm nhập.
- Thực hiện khai thác thực tế để kiểm chứng lỗ hổng thay vì chỉ dự đoán.

##### Các chức năng chính của Frontier Agent

- Design Review: Phân tích tài liệu kiến trúc trước khi viết code, hỗ trợ các chuẩn như PCI DSS, NIST CSF, AWS Well-Architected.
- Code Review: Tích hợp trực tiếp vào PR trên GitHub/GitLab, tự động đề xuất bản vá.
- Automated Pentesting: Mô phỏng các chuỗi khai thác đa bước, xác thực như người dùng thật và cung cấp biểu đồ tấn công chi tiết.

##### Các hạn chế kĩ thuật
- Chặn xác thực: Agent không thể vượt qua các lớp bảo mật phức tạp như MFA, sinh trắc học hoặc mTLS.
- Lỗi logic: Khó phát hiện các gian lận dựa trên logic kinh doanh phức tạp.
- Kiểm soát chi phí: Các ứng dụng phức tạp có thể tiêu tốn giờ thực hiện rất nhanh, đòi hỏi phải giám sát chặt chẽ.

#### Giới thiệu về Service Level Agreement (SLA) và Monitoring

##### Nền tảng về SLA và quản lý rủi ro
- SLA là cam kết về mức chất lượng dịch vụ giữa nhà cung cấp và khách hàng.
- SLA không đảm bảo toàn bộ trải nghiệm người dùng, chỉ là một phần của quản lý rủi ro.
- Quản lý rủi ro gồm nhận diện, giám sát, phản ứng và cải tiến liên tục.

##### Tư duy về tháp giám sát
- Tháp giám sát theo dõi từ hạ tầng đến trải nghiệm người dùng.
- Chỉ giám sát hạ tầng là chưa đủ để phát hiện mọi vấn đề.
- Giám sát tầng trên giúp phát hiện sớm ảnh hưởng đến người dùng và kinh doanh.

##### Minh họa thực tế qua demo
- Hạ tầng có thể báo bình thường dù dịch vụ phụ thuộc gặp lỗi.
- Health check có thể thành công nhưng người dùng vẫn không đăng nhập được.
- Chỉ số hạ tầng không phản ánh đầy đủ trải nghiệm thực tế của người dùng.

##### Quy trình cảnh báo và phản ứng
- Giám sát hiệu quả phải phát hiện sự cố trước khi khách hàng phản ánh.
- CloudWatch chuyển đổi chỉ số thành cảnh báo gửi qua Email hoặc Slack.


#### Giới thiệu Lộ trình chinh phục chứng chỉ AWS Cloud Practitioner

##### Tổng quan và cấu trúc kỳ thi AWS Cloud Practitioner (CLF-C02)
- 65 câu hỏi trong 90 phút 
- Điểm đạt 700/1000
- Thời hạn 3 năm
- Cloud Concepts (24%), Security and Compliance (30%) - Cloud Technology and Services (34%), Billing, Pricing, and Support (12%)

##### Các dịch vụ AWS cốt lõi về công nghệ và hạ tầng 
- Bao gồm Compute (EC2, Lambda), Storage (S3, EBS), và Networking (VPC, Route 53)

##### Chiến lược ôn tập và mẹo làm bài thi hiệu quả
- Sử dụng phương pháp loại trừ 
- Gắn từ khóa vào các trường hợp sử dụng (use case)

### Những Gì Học Được

#### Kiến thức và Tư duy Bảo mật Tự động
- Hiểu được sự ưu việt của việc ứng dụng AI (như Amazon Bedrock thông qua Frontier Agent) vào quy trình bảo mật (DevSecOps).
- Nắm bắt được khả năng tự động hóa trong việc đánh giá thiết kế, review code và pentest mà không cần nhiều sự can thiệp của con người.

#### Quản lý rủi ro và Tư duy Giám sát hệ thống (Monitoring)
- Nhận thức được rằng SLA chỉ là một phần của cam kết dịch vụ, và việc giám sát hệ thống cần tập trung vào trải nghiệm thực tế của người dùng thay vì chỉ nhìn vào các chỉ số hạ tầng (CPU, RAM).
- Hiểu cách thức hoạt động của tháp giám sát và sự cần thiết của việc cấu hình các cảnh báo (Alert) sớm thông qua CloudWatch để chủ động phản ứng trước khi khách hàng phàn nàn.

#### Lộ trình và Chiến lược học tập AWS
- Nắm vững cấu trúc bài thi, trọng số các phần trong kỳ thi AWS Cloud Practitioner (CLF-C02).
- Bỏ túi được các chiến lược làm bài hiệu quả như phương pháp loại trừ và gắn từ khóa (keyword) với các use case cụ thể của từng dịch vụ AWS cốt lõi (EC2, S3, VPC...).

### Trải nghiệm trong event

Tham gia sự kiện **“Chung kết cuộc thi Cloud Architect và Meeting”** là một trải nghiệm rất bổ ích, giúp tôi có cái nhìn toàn diện về bảo mật, giám sát hệ thống và đặc biệt là định hướng chứng chỉ AWS. Một số trải nghiệm nổi bật:

#### Không khí sôi động và đầy kịch tính của vòng chung kết
- Cuộc tranh tài giữa 2 đội KAKAT và Ngũ đại hiệp không chỉ mang lại sự hứng khởi mà còn là cơ hội tuyệt vời để mình lắng nghe cách các anh chị đi trước giải quyết các bài toán hóc búa về kiến trúc hệ thống và bảo mật trên AWS.

#### Mở rộng tầm nhìn về bảo mật ứng dụng với AI
- Lần đầu tiên được nghe chi tiết về việc sử dụng Agent (Frontier Agent) để tự động hóa toàn bộ vòng đời bảo mật. Mặc dù vẫn còn những hạn chế kỹ thuật như chặn xác thực MFA hay lỗi logic phức tạp, nhưng tiềm năng của AI trong an toàn thông tin là cực kỳ lớn.

#### Thay đổi tư duy về giám sát (Monitoring)
- Phần demo về SLA và Monitoring thực sự chạm đến những vấn đề thực tế: một hệ thống có thể báo an toàn nhưng người dùng vẫn không thể sử dụng. Điều này giúp mình nhận ra tầm quan trọng của việc giám sát từ góc độ người dùng.

#### Được tiếp thêm động lực học tập
- Việc lắng nghe chia sẻ về lộ trình thi AWS Cloud Practitioner giúp mình vạch ra được kế hoạch học tập rõ ràng hơn, giảm bớt sự mơ hồ và có thêm động lực để sớm chinh phục chứng chỉ này.

#### Bài học rút ra
- Cần có tư duy Security by Design và luôn đặt trải nghiệm người dùng làm trọng tâm khi xây dựng, giám sát bất kỳ hệ thống nào.
- Việc thi chứng chỉ không chỉ là để có bằng cấp, mà quan trọng hơn là học được cách tư duy và nắm vững các use case thực tế của hệ thống đám mây.

#### Một số hình ảnh khi tham gia sự kiện
![Chung kết cuộc thi Cloud Architect](/images/event1a.jpg)
![Meeting First Cloud AI Journey](/images/event1b.jpg)
> Tổng thể, sự kiện không chỉ cung cấp kiến thức kỹ thuật sâu sắc mà còn truyền cảm hứng mạnh mẽ, giúp tôi định hình rõ ràng hơn tư duy thiết kế kiến trúc cũng như con đường phát triển chuyên môn trên nền tảng đám mây AWS.
