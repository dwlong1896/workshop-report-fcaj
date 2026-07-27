---
title: "Worklog Tuần 10"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---
### Mục tiêu tuần 10:

* Thiết kế và xây dựng kho dữ liệu tập trung (Data Lake) quy mô lớn trên Amazon S3.
* Trực quan hóa dữ liệu, xây dựng các báo cáo phân tích thông minh (BI) với Amazon QuickSight.
* Nắm vững quy trình xây dựng, huấn luyện và triển khai mô hình Machine Learning thực tế với Amazon SageMaker.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                                                          | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Building Data Lake on AWS (Phần 1) <br>&emsp; + Tìm hiểu kiến trúc Data Lake và sự khác biệt với Data Warehouse <br> - **Thực hành:** <br>&emsp; + Thiết lập Amazon S3 làm storage layer trung tâm lưu trữ raw data <br>&emsp; + Phân vùng dữ liệu (Partitioning) hiệu quả     | 03/08/2025   | 03/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Building Data Lake on AWS (Phần 2) <br>&emsp; + Tìm hiểu AWS Glue và Data Catalog <br> - **Thực hành:** <br>&emsp; + Chạy AWS Glue Crawler để tự động khám phá schema dữ liệu <br>&emsp; + Truy vấn dữ liệu thô trực tiếp trên S3 bằng Amazon Athena                           | 04/08/2025   | 04/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Get started với Amazon QuickSight <br>&emsp; + Giới thiệu dịch vụ Business Intelligence (BI) trên Cloud <br> - **Thực hành:** <br>&emsp; + Kết nối QuickSight với Data source (Athena, S3 hoặc RDS) <br>&emsp; + Thiết kế dashboard trực quan hóa dữ liệu với các chart cơ bản | 05/08/2025   | 05/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Get started với Amazon SageMaker (Phần 1) <br>&emsp; + Tổng quan Machine Learning lifecycle trên AWS <br> - **Thực hành:** <br>&emsp; + Khởi tạo SageMaker Notebook instance <br>&emsp; + Load và tiền xử lý (preprocess) dataset mẫu bằng Python/Pandas                       | 06/08/2025   | 06/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Get started với Amazon SageMaker (Phần 2) <br>&emsp; + Train và Deploy model <br> - **Thực hành:** <br>&emsp; + Lựa chọn thuật toán built-in để train mô hình <br>&emsp; + Deploy model thành API Endpoint để dự đoán (inference) theo thời gian thực                          | 07/08/2025   | 07/08/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 10:

* Xây dựng thành công Data Lake trên hạ tầng AWS:
  * Biết cách thiết lập kho lưu trữ tập trung có khả năng tiếp nhận khối lượng dữ liệu khổng lồ (ví dụ: các luồng dữ liệu time-series liên tục đổ về từ thiết bị cảm biến giám sát).
  * Khai thác và truy vấn dữ liệu thô nhanh chóng bằng SQL (Athena) mà không cần phải transform hay load vào database truyền thống.

* Làm chủ công cụ trực quan hóa Amazon QuickSight:
  * Tự tay xây dựng thành công các dashboard báo cáo sinh động và real-time.
  * Có khả năng nhúng (embed) các biểu đồ này vào các giao diện frontend (như ứng dụng ReactJS) để tạo ra các AIoT dashboard quản lý môi trường, theo dõi và điều khiển thông số tưới tiêu trực quan cho người dùng cuối.

* Hoàn thiện quy trình Machine Learning với Amazon SageMaker:
  * Nắm vững toàn bộ vòng đời của một dự án AI trên đám mây từ khâu xử lý data, training đến deployment.
  * Xuất bản thành công model AI dưới dạng một API Endpoint độc lập, giúp các hệ thống backend (viết bằng Spring Boot hoặc PHP) dễ dàng gọi đến để thực hiện các dự đoán thông minh, khép lại trọn vẹn lộ trình 10 tuần thực học AWS từ hạ tầng cơ bản đến ứng dụng dữ liệu cấp cao.