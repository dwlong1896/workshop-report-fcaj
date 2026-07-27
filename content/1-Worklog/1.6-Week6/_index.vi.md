---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---
### Mục tiêu tuần 6:

* Quản trị và truy cập an toàn vào máy chủ EC2 mà không cần quản lý SSH Key hay mở port public.
* Đảm bảo an toàn dữ liệu bằng cách thiết lập chiến lược backup tự động cho toàn hệ thống.
* Nắm vững các mô hình pricing để tối ưu hóa chi phí vận hành (Cost Optimization) trên AWS.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                                                          | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Working với AWS Systems Manager – Session Manager (Phần 1) <br>&emsp; + Tìm hiểu kiến trúc Systems Manager và SSM Agent <br> - **Thực hành:** <br>&emsp; + Cấu hình IAM Role cho phép EC2 giao tiếp với Systems Manager <br>&emsp; + Kiểm tra SSM Agent trên EC2 instance        | 06/07/2025   | 06/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Working với AWS Systems Manager – Session Manager (Phần 2) <br>&emsp; + Các best practices về security khi access server <br> - **Thực hành:** <br>&emsp; + Truy cập shell của EC2 trực tiếp trên web console qua Session Manager <br>&emsp; + Đóng port 22 trên Security Group | 07/07/2025   | 07/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Implement system backup plan với AWS Backup (Phần 1) <br>&emsp; + Tìm hiểu cơ chế quản lý backup tập trung trên AWS <br> - **Thực hành:** <br>&emsp; + Tạo Backup Vault để lưu trữ an toàn các bản sao lưu <br>&emsp; + Cấu hình Backup Plan định nghĩa lịch trình tự động       | 08/07/2025   | 08/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Implement system backup plan với AWS Backup (Phần 2) <br>&emsp; + Quản lý lifecycle của các recovery point <br> - **Thực hành:** <br>&emsp; + Assign các resource (EC2, RDS) vào Backup Plan <br>&emsp; + Thực hành quy trình Restore dữ liệu từ một bản backup                 | 09/07/2025   | 09/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Optimize cost với Savings Plans và Reserved Instances <br>&emsp; + Tìm hiểu các mô hình pricing (On-Demand, Reserved, Savings Plans) <br> - **Thực hành:** <br>&emsp; + Phân tích usage và so sánh cost giữa các mô hình <br>&emsp; + Lên kế hoạch right-sizing cho EC2 và RDS | 10/07/2025   | 10/07/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 6:

* Quản trị server bảo mật với AWS Systems Manager:
  * Loại bỏ hoàn toàn rủi ro lộ SSH Key và các lỗ hổng bảo mật tiềm ẩn từ việc mở port 22 ra internet.
  * Access thành công vào command line của EC2 instance một cách an toàn trực tiếp từ trình duyệt web thông qua Session Manager, giúp đơn giản hóa quá trình vận hành.

* Đảm bảo data protection với AWS Backup:
  * Thiết lập thành công cơ chế backup tự động (automated backup) tập trung cho nhiều loại resource khác nhau (như EC2, RDS) dựa trên policy đã định nghĩa.
  * Hiểu và thực hành thành thạo quy trình restore, đảm bảo khả năng disaster recovery (khôi phục sau thảm họa) nhanh chóng và giữ tính toàn vẹn của dữ liệu khi hệ thống gặp sự cố.

* Tối ưu hóa chi phí (Cost Optimization):
  * Nắm vững các strategy tối ưu chi phí thông qua việc cam kết sử dụng với Savings Plans và Reserved Instances.
  * Biết cách lựa chọn commitment plan phù hợp để giảm thiểu từ 40-70% cost cho các workload dài hạn và ổn định, so với mức giá On-Demand mặc định.