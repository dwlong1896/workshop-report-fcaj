---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
### Mục tiêu tuần 3:

* Nắm dịch vụ lưu trữ Amazon S3, quản lý Object cơ bản hos,t website tĩnh.
* Triển khai, bảo mật và kết nối cơ sở dữ liệu quan hệ với Amazon RDS.
* Thiết lập hệ thống giám sát tài nguyên và cảnh báo tự động thông qua Amazon CloudWatch.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                                                                                               | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Lưu trữ trang web tĩnh với Amazon S3 <br>&emsp; + Tìm hiểu S3 Bucket, Object và cơ chế phân quyền truy cập <br> - **Thực hành:** <br>&emsp; + Tạo Bucket, thiết lập Block Public Access <br>&emsp; + Upload và quản lý các file tĩnh cơ bản                                                                  | 15/06/2025   | 15/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Lưu trữ trang web tĩnh với Amazon S3 <br>&emsp; + Cơ chế phục vụ web tĩnh trực tiếp từ S3 Bucket <br> - **Thực hành:** <br>&emsp; + Bật tính năng Static Website Hosting <br>&emsp; + Cấu hình Bucket Policy <br>&emsp; + Triển khai một giao diện web tĩnh          | 16/06/2025   | 16/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Tạo cơ sở dữ liệu trên Amazon RDS  <br>&emsp; + Tìm hiểu các loại DB Engines (MySQL, PostgreSQL...) <br> - **Thực hành:** <br>&emsp; + Khởi tạo RDS instance nằm trong Private Subnet <br>&emsp; + Cấu hình Security Group chỉ cho phép kết nối từ máy chủ ứng dụng                                       | 17/06/2025   | 17/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tạo cơ sở dữ liệu trên Amazon RDS <br>&emsp; + Tìm hiểu Endpoint và cơ chế Backup tự động của RDS <br> - **Thực hành:** <br>&emsp; + Thiết lập kết nối an toàn từ ứng dụng backend đang chạy trên EC2 xuống RDS <br>&emsp; + Thực hiện thao tác truy vấn dữ liệu test                | 18/06/2025   | 18/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Tạo hệ thống giám sát với Amazon CloudWatch <br>&emsp; + Khái niệm Metrics, Logs và Alarms trên AWS <br> - **Thực hành:** <br>&emsp; + Đọc và theo dõi biểu đồ CPU, RAM của EC2 và RDS <br>&emsp; + Tạo Alarm tự động gửi email cảnh báo khi CPU của máy chủ vượt ngưỡng 80%                                        | 19/06/2025   | 19/06/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 3:

* Hiểu cơ bản dịch vụ lưu trữ đối tượng Amazon S3:
  * Biết cách cấu hình và phân quyền truy cập an toàn cho các file tài nguyên tĩnh.
  * Phân phối ứng dụng Frontend trực tiếp từ S3 ra Internet với chi phí thấp, vận hành mượt mà.

* Quản trị và vận hành an toàn cơ sở dữ liệu trên Cloud với Amazon RDS:
  * Khởi tạo cơ sở dữ liệu quan hệ và bảo vệ bằng cách đặt sâu trong mạng nội bộ (Private Subnet).
  * Hiểu rõ khái niệm Endpoint; kết nối thành công luồng dữ liệu từ Backend xuống Database, hoàn thiện kiến trúc ứng dụng web đa tầng cơ bản.

* Tự động hóa quá trình giám sát hệ thống bằng Amazon CloudWatch:
  * Biết cách tra cứu log và đọc các chỉ số (Metrics) để đánh giá trực quan sức khỏe của toàn bộ hạ tầng.
  * Thiết lập thành công hệ thống cảnh báo tự động, đảm bảo luôn nhận được thông báo kịp thời nếu tài nguyên máy chủ bị quá tải.