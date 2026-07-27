---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
### Mục tiêu tuần 5:

* Nắm vững khái niệm containerization, biết cách đóng gói và deploy ứng dụng bằng Docker.
* Nắm vững tư duy Infrastructure as Code (IaC) để tự động hóa việc quản trị và khởi tạo hạ tầng.
* Sử dụng AWS CloudFormation để deploy đồng loạt các tài nguyên AWS (Network, Compute, Database) thông qua template.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                                             | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Deploy Applications với Docker (Phần 1) <br>&emsp; + Tìm hiểu khái niệm Containerization, Docker Engine, Image, Dockerfile <br> - **Thực hành:** <br>&emsp; + Cài đặt Docker engine <br>&emsp; + Kéo (pull) và chạy thử các base image cơ bản                         | 29/06/2025   | 29/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Deploy Applications với Docker (Phần 2) <br>&emsp; + Quy trình build và run container <br> - **Thực hành:** <br>&emsp; + Viết Dockerfile đóng gói ứng dụng (VD: backend PHP/Spring Boot hoặc frontend ReactJS) <br>&emsp; + Build image và deploy container trên EC2 | 30/06/2025   | 30/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Initialize Infrastructure as Code với AWS CloudFormation (Phần 1) <br>&emsp; + Tìm hiểu tư duy IaC <br>&emsp; + Cấu trúc của CloudFormation Template (JSON/YAML) <br> - **Thực hành:** <br>&emsp; + Viết template cơ bản định nghĩa Parameters và Resources           | 01/07/2025   | 01/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Initialize IaC với AWS CloudFormation (Phần 2) <br>&emsp; + Khai báo network resources <br> - **Thực hành:** <br>&emsp; + Viết template để tự động deploy Custom VPC, Subnet, Internet Gateway và Security Group                                                    | 02/07/2025   | 02/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Initialize IaC với AWS CloudFormation (Phần 3) <br>&emsp; + Triển khai toàn bộ hệ thống <br> - **Thực hành:** <br>&emsp; + Khởi tạo một Stack hoàn chỉnh tự động deploy EC2 instance và RDS database thông qua script                                               | 03/07/2025   | 03/07/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 5:

* Đóng gói ứng dụng thành công bằng Docker:
  * Hiểu rõ lợi ích của containerization trong việc cô lập môi trường chạy code, đảm bảo tính đồng nhất giữa môi trường dev và production.
  * Tự viết được Dockerfile đóng gói các ứng dụng thực tế (như Spring Boot, PHP, hoặc ReactJS) thành các Docker Image độc lập, loại bỏ triệt để lỗi xung đột môi trường khi deploy.

* Tự động hóa hạ tầng đám mây với AWS CloudFormation (IaC):
  * Chuyển đổi tư duy từ việc thao tác thủ công (click tay) trên AWS Console sang quản lý hạ tầng bằng code (Template).
  * Khởi tạo thành công một CloudFormation Stack hoàn chỉnh, có khả năng dựng lại toàn bộ kiến trúc mạng (VPC) và máy chủ (EC2, RDS) một cách nhất quán chỉ bằng một thao tác chạy script tự động.