---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---
### Mục tiêu tuần 8:

* Quản lý định danh, xác thực và phân quyền người dùng với Amazon Cognito.
* Nắm các mô hình giao tiếp bất đồng bộ (asynchronous) để decouple các microservices.
* Xây dựng kiến trúc xử lý đơn hàng (processing orders) có khả năng chịu tải cao bằng Amazon SQS và SNS.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                                                                    | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Serverless – Authentication với Amazon Cognito <br>&emsp; + Tìm hiểu khái niệm User Pool và Identity Pool <br> - **Thực hành:** <br>&emsp; + Khởi tạo User Pool để quản lý danh sách user <br>&emsp; + Cấu hình các policy cho password và MFA      | 20/07/2025   | 20/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Serverless – Authentication với Amazon Cognito <br>&emsp; + Tích hợp Cognito vào ứng dụng thực tế <br> - **Thực hành:** <br>&emsp; + Giả lập frontend gọi API đăng ký, đăng nhập <br>&emsp; + Xử lý và xác thực JWT token trả về từ Cognito                         | 21/07/2025   | 21/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Serverless – Message Queuing với Amazon SQS <br>&emsp; + Tìm hiểu Message Queue và lợi ích của việc decoupling <br> - **Thực hành:** <br>&emsp; + Tạo Standard Queue và FIFO Queue <br>&emsp; + Viết script gửi, nhận và xóa message trong Queue                 | 22/07/2025   | 22/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Serverless – Pub/Sub Messaging với Amazon SNS <br>&emsp; + Kiến trúc Publish/Subscribe <br> - **Thực hành:** <br>&emsp; + Tạo SNS Topic <br>&emsp; + Cấu hình Subscribe để tự động gửi Email notification khi có event mới publish vào Topic                                               | 23/07/2025   | 23/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Serverless – Processing orders với SQS và SNS <br>&emsp; + Mô hình Fanout architecture <br> - **Thực hành:** <br>&emsp; + Kết hợp SNS và SQS: Cấu hình SNS Topic đẩy message đồng loạt tới nhiều SQS Queues <br>&emsp; + Mô phỏng luồng backend tạo đơn hàng, thanh toán và gửi thông báo | 24/07/2025   | 24/07/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 8:

* Quản lý Authentication với Amazon Cognito:
  * Xây dựng thành công luồng sign-up/sign-in hoàn chỉnh
  * Biết cách sử dụng JWT token để authorize các request gọi xuống API backend.

* Giải quyết bài toán nghẽn cổ chai bằng Amazon SQS:
  * Hiểu và áp dụng được cơ chế Message Queue để buffer các request.
  * Đảm bảo hệ thống không bị crash hoặc drop data khi có lượng truy cập tăng đột biến, tăng tính chịu lỗi.

* Triển khai kiến trúc Fanout Event-driven với Amazon SNS & SQS:
  * Nắm vững mô hình Pub/Sub để broadcast thông tin cho nhiều services khác nhau cùng lúc.
