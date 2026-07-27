---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---
### Mục tiêu tuần 7:

* Nắm vững kiến trúc Microservices, biết cách thiết kế và phân tách một hệ thống Monolith thành các dịch vụ độc lập.
* Làm quen với kiến trúc Serverless, xây dựng luồng xử lý tự động với AWS Lambda, Amazon S3 và DynamoDB.
* Ứng dụng AWS Step Functions để orchestrate (điều phối) các business workflow phức tạp.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                                                                                         | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Create a Microservice <br>&emsp; + Tìm hiểu sự khác biệt giữa Monolithic và Microservices architecture <br> - **Thực hành:** <br>&emsp; + Thiết kế phương án tách một monolith application (ví dụ một backend lớn viết bằng Spring Boot hoặc PHP) thành các bounded contexts độc lập                            | 13/07/2025   | 13/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Serverless – Lambda & DynamoDB <br>&emsp; + Tìm hiểu Serverless compute (AWS Lambda) và NoSQL database (DynamoDB) <br> - **Thực hành:** <br>&emsp; + Khởi tạo table cơ bản trên DynamoDB <br>&emsp; + Viết một Lambda function (Hello World) đầu tiên                                                         | 14/07/2025   | 14/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Serverless – Lambda interacting với S3 <br>&emsp; + Tìm hiểu cơ chế Event-driven architecture <br> - **Thực hành:** <br>&emsp; + Cấu hình Event Trigger: Tự động kích hoạt Lambda function mỗi khi có file tĩnh được upload lên S3 bucket (có thể là file assets từ một frontend ReactJS hoặc file tài liệu) | 15/07/2025   | 15/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tích hợp luồng Serverless hoàn chỉnh <br>&emsp; + Cách các serverless services giao tiếp bảo mật với nhau <br> - **Thực hành:** <br>&emsp; + Lập trình Lambda function để đọc metadata của file từ S3 event và thực thi lệnh write (ghi) record vào DynamoDB                                                  | 16/07/2025   | 16/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Getting Started với AWS Step Functions <br>&emsp; + Tìm hiểu State Machine và các orchestration step (Task, Choice, Parallel) <br> - **Thực hành:** <br>&emsp; + Tạo một workflow điều phối tuần tự nhiều Lambda functions để xử lý một logic nghiệp vụ phức tạp mà không bị timeout                          | 17/07/2025   | 17/07/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 7:

* Hình thành tư duy thiết kế hệ thống Microservices:
  * Hiểu rõ ưu nhược điểm và cách chia nhỏ một hệ thống lớn (monolith) thành các services nhỏ, dễ dàng scale và maintain độc lập.

* Chuyển dịch sang kiến trúc Serverless (Không máy chủ):
  * Vận hành thành công các đoạn code backend thực thi logic (Lambda) mà không cần phải provision hay quản trị bất kỳ máy chủ EC2 nào.
  * Tích hợp mượt mà cơ sở dữ liệu phi quan hệ (DynamoDB) với khả năng read/write ở tốc độ mili-giây.

* Xây dựng thành công Event-Driven workflow:
  * Tự động hóa hoàn toàn luồng xử lý dữ liệu: Hệ thống có khả năng detect ngay khi có file mới xuất hiện trên S3 để trigger code, sau đó tự động update data vào DynamoDB mà không cần sự can thiệp thủ công.

* Orchestrate workflow với Step Functions:
  * Biết cách kết nối và trực quan hóa các services rời rạc thành một business process liền mạch.
  * Quản lý hoàn hảo các transaction dài và tích hợp retry mechanism (cơ chế tự thử lại) khi có lỗi xảy ra ở bất kỳ node nào trong hệ thống.