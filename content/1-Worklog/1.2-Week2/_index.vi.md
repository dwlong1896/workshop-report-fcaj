---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---



### Mục tiêu tuần 2:

* Nắm vững kiến trúc mạng cơ bản trên AWS và triển khai được Virtual Private Cloud (VPC).
* Hiểu cách chia Subnet, định tuyến giao thông mạng với Route Table và Internet Gateway.
* Khởi tạo, quản lý và kết nối từ xa vào máy chủ ảo Amazon EC2.
* Triển khai thành công môi trường chạy ứng dụng thực tế trên EC2.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Triển khai hạ tầng mạng với Amazon VPC <br>&emsp; + Tìm hiểu kiến trúc mạng trên Cloud, khái niệm VPC, CIDR block <br>&emsp; + Phân biệt Public Subnet và Private Subnet <br> - **Thực hành:** <br>&emsp; + Tạo một Custom VPC <br>&emsp; + Chia các Subnet | 08/06/2025   | 08/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Quản lý định tuyến và luồng truy cập mạng <br>&emsp; + Tìm hiểu Internet Gateway, Route Table và NAT Gateway <br> - **Thực hành:** <br>&emsp; + Gắn Internet Gateway vào VPC <br>&emsp; + Cấu hình Route Table                                             | 09/06/2025   | 09/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Bảo mật hạ tầng mạng & Giới thiệu máy chủ ảo <br>&emsp; + Khái niệm Security Group và NACL <br>&emsp; + Tìm hiểu Amazon EC2 (Instance types, AMI) <br> - **Thực hành:** <br>&emsp; + Tạo Security Group, mở các port cần thiết (22, 80, 443)              | 10/06/2025   | 10/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Getting Started and Deploying Applications on Amazon EC2 <br>&emsp; + Các phương thức kết nối máy chủ (SSH, RDP) <br> - **Thực hành:** <br>&emsp; + Khởi tạo EC2 Instance (Linux/Ubuntu) nằm trong Public Subnet <br>&emsp; + Kết nối an toàn qua SSH    | 11/06/2025   | 11/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Deploying Applications on Amazon EC2 <br>&emsp; + Quản lý dịch vụ và cài đặt môi trường trên Linux <br> - **Thực hành:** <br>&emsp; + Cài đặt Web Server (Apache/Nginx) <br>&emsp; + Triển khai ứng dụng backend cơ bản lên EC2                            | 12/06/2025   | 12/06/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 2:

* Xây dựng thành công hệ thống mạng đám mây riêng ảo (VPC) từ con số không:
  * Nắm được cách thiết lập dải IP và chia nhỏ thành các mạng con (Subnet).
  * Cấu hình thành công Route Table và Internet Gateway để ra/vào Internet.

* Làm chủ các lớp bảo mật mạng trên AWS:
  * Hiểu và thiết lập được Security Group đóng vai trò như một tường lửa, kiểm soát chặt chẽ các cổng (port).

* Khởi tạo và vận hành thành thạo máy chủ ảo Amazon EC2:
  * Biết cách chọn cấu hình phần cứng (Instance type) và hệ điều hành (AMI).
  * Sử dụng Key Pair để kết nối từ xa (SSH) bảo mật vào máy chủ Linux.

* Triển khai ứng dụng thực tế thành công:
  * Thao tác được với các lệnh Linux cơ bản để cài đặt Web Server.
  * Tự tay cấu hình môi trường và đưa được một ứng dụng backend lên chạy thực tế.