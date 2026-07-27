---
title: "Worklog Tuần 9"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---
### Mục tiêu tuần 9:

* Áp dụng nguyên tắc thiết kế module hóa (modularity) để chuyển đổi ứng dụng từ Monolith sang Microservices.
* Triển khai và vận hành Container theo mô hình Serverless thông qua AWS Fargate.
* Làm quen với nền tảng Container Orchestration quy mô lớn (Kubernetes) thông qua Amazon EKS.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                                          | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | ----------------------------------------- |
| 2   | - Monolith sang Microservices với Docker và AWS Fargate  <br>&emsp; + Tìm hiểu kiến trúc Amazon ECS và Fargate <br> - **Thực hành:** <br>&emsp; + Tạo ECS Cluster <br>&emsp; + Viết Task Definition để định nghĩa resource (CPU, RAM) cho Docker container | 27/07/2025   | 27/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Monolith sang Microservices với Docker và AWS Fargate <br>&emsp; + Load Balancing cho Container <br> - **Thực hành:** <br>&emsp; + Deploy ECS Service chạy trên Fargate <br>&emsp; + Tích hợp Application Load Balancer để phân phối traffic            | 28/07/2025   | 28/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Làm quen với Amazon EKS <br>&emsp; + Tìm hiểu kiến trúc Kubernetes (K8s) <br>&emsp; + Khái niệm Control Plane, Worker Node, Pod <br> - **Thực hành:** <br>&emsp; + Cài đặt và cấu hình CLI tool                         | 29/07/2025   | 29/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Làm quen với Amazon EKS <br>&emsp; + Khởi tạo hạ tầng Kubernetes trên AWS <br> - **Thực hành:** <br>&emsp; + Dùng `eksctl` để provision một EKS Cluster <br>&emsp; + Khởi tạo Managed Node Group để cấp phát compute capacity                      | 30/07/2025   | 30/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Làm quen với Amazon EKS <br>&emsp; + Deploy ứng dụng lên Kubernetes <br> - **Thực hành:** <br>&emsp; + Viết manifest YAML (Deployment, Service) <br>&emsp; + Apply manifest để chạy các Pod chứa ứng dụng và expose ra public internet             | 31/07/2025   | 31/07/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 9:

* Chuyển đổi kiến trúc Microservices:
  * Áp dụng tính module hóa để tách biệt các lớp của ứng dụng.
  * Đóng gói và chạy các service backend và frontend vào các container độc lập
* Vận hành Serverless Container với AWS Fargate:
  * Chạy Docker container trên production mà không cần cấp phát.
  * Tích hợp Load Balancer để tự động điều hướng traffic vào các container.

* Nắm vững nền tảng Kubernetes trên AWS (EKS):
  * Hiểu cách thức hoạt động của nền tảng orchestration chuẩn enterprise.
  * Khởi tạo thành công cluster, quản lý các Node và sử dụng declarative code (file YAML) để deploy, quản lý vòng đời của các Pod ứng dụng.