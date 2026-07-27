---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
### Mục tiêu tuần 4:

* Nắm vững quy trình Database Migration từ hệ thống on-premise lên AWS RDS.
* Sử dụng AWS DMS và SCT để convert schema và replicate data với thời gian downtime ít nhất.
* Thực hành migrate virtual machine từ môi trường on-premise lên Amazon EC2 theo mô hình Lift-and-Shift.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                                        | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Database Migration với AWS DMS & SCT <br>&emsp; + Tìm hiểu kiến trúc của AWS Database Migration Service  <br> - **Thực hành:** <br>&emsp; + Khởi tạo Replication Instance <br>&emsp; + Cấu hình Source và Target Endpoint                        | 22/06/2025   | 22/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Database Migration với AWS DMS & SCT <br>&emsp; + Tìm hiểu công cụ Schema Conversion Tool <br> - **Thực hành:** <br>&emsp; + Cài đặt AWS SCT <br>&emsp; + Đánh giá và convert schema từ source database sang target RDS                         | 23/06/2025   | 23/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Database Migration với AWS DMS & SCT <br>&emsp; + Luồng thực thi Migration Task <br> - **Thực hành:** <br>&emsp; + Chạy Migration Task để replicate data <br>&emsp; + Kiểm tra data integrity sau khi đồng bộ lên RDS                                 | 24/06/2025   | 24/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Migrate virtual servers với AWS VM Import/Export <br>&emsp; + Tìm hiểu quy trình import/export virtual machine (VMware, VirtualBox...) <br> - **Thực hành:** <br>&emsp; + Chuẩn bị VM image với định dạng hỗ trợ (OVA, VMDK) <br>&emsp; + Cấu hình IAM Role cho tính năng Import | 25/06/2025   | 25/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Migrate virtual servers với AWS VM Import/Export <br>&emsp; + Mô hình triển khai Lift-and-Shift <br> - **Thực hành:** <br>&emsp; + Thực thi lệnh import VM thành một Amazon Machine Image (AMI) <br>&emsp; + Khởi chạy EC2 Instance từ AMI vừa tạo      | 26/06/2025   | 26/06/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 4:

* Migrate database thành công với AWS DMS và SCT:
  * Biết cách sử dụng SCT để đánh giá mức độ tương thích và tự động convert schema sang target database.
  * Thiết lập thành công luồng data replication liên tục bằng DMS, giúp migrate dữ liệu lớn lên Cloud mà hệ thống on-premise vẫn hoạt động bình thường.

* Migrate hạ tầng máy chủ lên Cloud với AWS VM Import/Export:
  * Nắm được phương pháp Lift-and-Shift.
  * Đóng gói và import thành công một virtual machine nội bộ thành một AMI, sau đó vận hành ổn định trên môi trường Amazon EC2.