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
* Nắm được quy trình xây dựng, huấn luyện và triển khai mô hình Machine Learning với Amazon SageMaker.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                                                          | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Xây dựng Data Lake trên AWS <br>&emsp; + Tìm hiểu kiến trúc Data Lake và sự khác biệt với Data Warehouse <br> - **Thực hành:** <br>&emsp; + Thiết lập Amazon S3 làm storage layer trung tâm lưu trữ raw data <br>&emsp; + Phân vùng dữ liệu     | 03/08/2025   | 03/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Xây dựng Data Lake trên AWS <br>&emsp; + Tìm hiểu AWS Glue và Data Catalog <br> - **Thực hành:** <br>&emsp; + Chạy AWS Glue Crawler để tự động khám phá schema dữ liệu <br>&emsp; + Truy vấn dữ liệu thô trực tiếp trên S3 bằng Amazon Athena                           | 04/08/2025   | 04/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Làm quen với Amazon QuickSight <br>&emsp; + Giới thiệu dịch vụ Business Intelligence trên Cloud <br> - **Thực hành:** <br>&emsp; + Kết nối QuickSight với Data source (Athena, S3 hoặc RDS) <br>&emsp; + Thiết kế dashboard trực quan hóa dữ liệu với các chart cơ bản | 05/08/2025   | 05/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Làm quen với Amazon SageMaker   <br>&emsp; + Tổng quan Machine Learning lifecycle trên AWS <br> - **Thực hành:** <br>&emsp; + Khởi tạo SageMaker Notebook instance <br>&emsp; + Load và tiền xử lý dataset mẫu bằng Python/Pandas                       | 06/08/2025   | 06/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Làm quen với Amazon SageMaker   <br>&emsp; + Train và Deploy model <br> - **Thực hành:** <br>&emsp; + Lựa chọn thuật toán built-in để train mô hình <br>&emsp; + Deploy model thành API Endpoint để dự đoán theo thời gian thực                          | 07/08/2025   | 07/08/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 10:

* Xây dựng thành công Data Lake trên hạ tầng AWS:
  * Thiết lập kho lưu trữ tập trung có khả năng tiếp nhận khối lượng dữ liệu lớn
  * Khai thác và truy vấn dữ liệu thô nhanh chóng bằng SQL.

* Làm chủ công cụ trực quan hóa Amazon QuickSight:
  * Xây dựng thành công các dashboard báo cáo real-time.
 

* Hoàn thiện quy trình Machine Learning với Amazon SageMaker:
  * Nắm được vòng đời của một dự án AI trên đám mây.