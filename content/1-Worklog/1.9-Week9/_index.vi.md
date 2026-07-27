---
title: "Worklog Tuần 9"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---
### Mục tiêu tuần 9:

* Áp dụng nguyên tắc thiết kế module hóa (modularity) để chuyển đổi hoàn toàn ứng dụng từ Monolith sang Microservices.
* Triển khai và vận hành Container theo mô hình Serverless thông qua AWS Fargate.
* Làm quen với nền tảng Container Orchestration quy mô lớn (Kubernetes) thông qua Amazon EKS.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                                          | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | ----------------------------------------- |
| 2   | - Monolith to Microservices với Docker và AWS Fargate (Phần 1) <br>&emsp; + Tìm hiểu kiến trúc Amazon ECS và Fargate <br> - **Thực hành:** <br>&emsp; + Tạo ECS Cluster <br>&emsp; + Viết Task Definition để định nghĩa resource (CPU, RAM) cho Docker container | 27/07/2025   | 27/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Monolith to Microservices với Docker và AWS Fargate (Phần 2) <br>&emsp; + Load Balancing cho Container <br> - **Thực hành:** <br>&emsp; + Deploy ECS Service chạy trên Fargate <br>&emsp; + Tích hợp Application Load Balancer để phân phối traffic            | 28/07/2025   | 28/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Get started với Amazon EKS (Phần 1) <br>&emsp; + Tìm hiểu kiến trúc Kubernetes (K8s) <br>&emsp; + Khái niệm Control Plane, Worker Node, Pod <br> - **Thực hành:** <br>&emsp; + Cài đặt và cấu hình CLI tool (`kubectl` và `eksctl`)                          | 29/07/2025   | 29/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Get started với Amazon EKS (Phần 2) <br>&emsp; + Khởi tạo hạ tầng Kubernetes trên AWS <br> - **Thực hành:** <br>&emsp; + Dùng `eksctl` để provision một EKS Cluster <br>&emsp; + Khởi tạo Managed Node Group để cấp phát compute capacity                      | 30/07/2025   | 30/07/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Get started với Amazon EKS (Phần 3) <br>&emsp; + Deploy ứng dụng lên Kubernetes <br> - **Thực hành:** <br>&emsp; + Viết manifest YAML (Deployment, Service) <br>&emsp; + Apply manifest để chạy các Pod chứa ứng dụng và expose ra public internet             | 31/07/2025   | 31/07/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 9:

* Chuyển đổi kiến trúc Microservices chuyên nghiệp:
  * Phá vỡ cấu trúc nguyên khối, áp dụng tốt tính module hóa để tách biệt các lớp của ứng dụng.
  * Đóng gói và chạy các service backend (như các API Spring Boot/PHP) và frontend (ReactJS) vào các container độc lập, dễ dàng update mà không ảnh hưởng toàn hệ thống.

* Vận hành Serverless Container với AWS Fargate:
  * Trải nghiệm việc chạy Docker container trên production mà hoàn toàn không cần cấp phát, vá lỗi OS hay quản trị máy chủ vật lý bên dưới.
  * Tích hợp thành công Load Balancer để tự động điều hướng traffic vào các container đang chạy.

* Nắm vững nền tảng Kubernetes trên AWS (EKS):
  * Hiểu rõ cách thức hoạt động của nền tảng orchestration hàng đầu chuẩn enterprise hiện nay.
  * Tự tay khởi tạo thành công cluster, quản lý các Node và biết cách sử dụng declarative code (file YAML) để deploy, quản lý vòng đời của các Pod ứng dụng.