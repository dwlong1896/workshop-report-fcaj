---
title: "Event 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Bài thu hoạch “FCAJ x Agentic AI Build Week”

### Mục Đích Của Sự Kiện

- Chia sẻ thông tin và kinh nghiệm từ cuộc thi Hackathon
- Giới thiệu sản phẩm của các team tham gia Hackathon


### Danh Sách Diễn Giả

- **Mr. Nguyen Gia Hung** - Head of Solutions Architect tại VietNam
- **Mr. Joseph Marazota** - Head of technology of Asia
- **Các team tham gia Hackathon**: OneTeam,  

### Nội Dung Nổi Bật

#### Chatbot đặt hàng KFC qua hội thoại
- Chatbot đặt hàng đa kênh qua Zalo và WhatsApp, khách đặt món ngay trong khung chat
- KDùng Bedrock **AgentCore**, **Tiny Fish** scrape dữ liệu menu từ website KFC lưu vào DynamoDB; có bước xác nhận đơn trước khi chốt để tránh lặp lại lỗi kiểu McDonald's.
- Chi phí tương đối rẻ, độ trễ đầu-cuối chỉ 3-4 giây.
#### Signal C – Phân tích chiến lược đối thủ 
- Multi-agent thu thập tín hiệu rời rạc (báo cáo tài chính, tin tức...) để tổng hợp thông tin chiến lược đối thủ và ước tính ROI.
- Kiến trúc supervisor-agent điều phối các sub-agent, có cơ chế tự chấm điểm & retry trước khi cần người review.
- Vấn đề: chi phí tăng mạnh do phụ thuộc dịch vụ bên thứ 3.
#### BL Team – Sinh kiến trúc AWS từ ngôn ngữ tự nhiên
- Giải quyết áp lực deadline gấp của Solution Architect: nhập yêu cầu AI sẽ vẽ kiến trúc, chỉnh sửa, xuất bảng giá, deploy tự động.
- Có cơ chế chặn dịch vụ không được phép ngay từ đầu ra; thách thức là đảm bảo output nhất quán.
#### 3K – Giám sát đám đông bằng camera AI 
- Dùng YOLO + ByteTrack phát hiện, đếm người theo từng khu vực, cảnh báo khi quá tải và gợi ý điều phối
- Bài học tối ưu chi phí khi chọn model AI.
#### Six Pillar – Hỗ trợ điều tra chống rửa tiền cho ngân hàng
- Giải quyết vấn đề 90-95% cảnh báo là báo động giả, rút ngắn thời gian xử lý case từ ~3 giờ xuống còn vài phút.
- Kiến trúc 3 lớp: Fast Detection, Deep Investigation, Case Management 
### Những Gì Học Được
 
#### Xác định rõ phạm vi 
- Không ôm đồm tính năng
- Hướng tới MVP vừa đủ để chứng minh ý tưởng trong thời gian giới hạn.
#### Ưu tiên thực thi hơn lý thuyết
- Sản phẩm phải chạy được, nên deploy thật.
#### Teamwork 
- Tranh luận vào vấn đề, không công kích cá nhân
- phân vai rõ ràng theo thế mạnh từng người.
#### Tìm đúng Pain Point thực tế
- Công nghệ xịn vô nghĩa nếu không giải quyết đúng vấn đề nghiệp vụ của khách hàng và thị trường.
#### Kiểm soát chi phí và hallucination
- Tối ưu chi phí ngay từ đầu
- Dùng double-check, guardrails để giảm ảo giác AI
- Luôn giữ con người trong vòng lặp quyết định.
### Ứng Dụng Vào Công Việc
- Thiết kế hệ thống theo mô hình supervisor-agent điều phối các sub-agent chuyên biệt thay vì một agent ôm hết việc.
- Dùng kiến trúc lọc trước và xử lý sâu sau để tối ưu chi phí AI ở quy mô lớn.
- Luôn thiết kế điểm dừng cho con người can thiệp với các quyết định rủi ro cao.
### Trải nghiệm trong event
 
#### Không khí hackathon
- Các anh chị mang tới một không khí làm việc xuyên đêm, nhiều khoảnh khắc hài hước nhưng vẫn giữ tinh thần lạc quan. 
- Tinh thần không bỏ quộc dù có nhiều khó khăn, thành viên đến từ nhiều nền tảng, phải trình bày trước nhóm giám khảo trong thời gian ngắn.
#### Bài học rút ra
- Qua đó em học được việc chuẩn bị tâm lý vững vàng quan trọng không kém kỹ năng kỹ thuật; mạnh dạn tham gia dù chưa có kinh nghiệm; networking cũng là giá trị lớn của hackathon.


#### Một số hình ảnh khi tham gia sự kiện
* Thêm các hình ảnh của các bạn tại đây
> Sự kiện giúp em hiểu thêm về cuộc thi hackathon, nó không chỉ là cuộc thi công nghệ mà là hành trình trải nghiệm toàn diện: áp lực, mệt mỏi, tranh luận nhóm, niềm vui khi sản phẩm chạy được và tự hào khi trình bày trước giám khảo. Giá trị lớn nhất không chỉ nằm ở giải thưởng mà còn nằm ở bài học thực chiến về làm sản phẩm, làm việc nhóm và tư duy giải quyết vấn đề thực tế.
