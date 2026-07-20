---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---


## Hạ tầng Hệ thống Quiz Trắc Nghiệm Real-time 100% Serverless & Event-Driven trên AWS
Chào mọi người, mình xin chia sẻ thiết kế kiến trúc cho dự án Real-time Quiz / Assessment Application – ứng dụng thi trắc nghiệm thời gian thực được xây dựng hoàn toàn theo mô hình Serverless & Event-Driven trên nền tảng AWS.
Đối với dạng bài toán Quiz App, điểm then chốt nằm ở khả năng chịu tải đột biến (Traffic Spike) khi hàng ngàn người tham gia cùng bấm nộp bài hoặc nhận câu hỏi đồng loạt, kèm theo yêu cầu độ trễ cực thấp (Low Latency).
Dưới đây là tổng quan các phân hệ chính trong kiến trúc hệ thống (chi tiết theo sơ đồ đính kèm) CÁC THÀNH PHẦN CỐT LÕI TRONG HỆ THỐNG:
### Tầng Phân Phối & Bảo Mật Lớp Biên (Edge & Auth)
* CloudFront + WAF: Bảo vệ mặt tiền hệ thống, chống DDoS và lọc các request độc hại.
* S3 Static Hosting & Cognito: Hosting giao diện Web tĩnh, kết hợp Amazon Cognito để quản lý xác thực và phân quyền người dùng (JWT Token).
### Tầng Cổng API Kép (Dual-API Layer)
* REST API Gateway + Lambda REST: Xử lý các tác vụ truy vấn dữ liệu đồng bộ chuẩn RESTful (lấy danh sách bộ đề, xem lịch sử thi...).
* WebSocket API Gateway + Lambda WebSocket: Đảm nhiệm việc đếm ngược thời gian, đẩy câu hỏi đồng loạt và cập nhật bảng xếp hạng (Leaderboard) thời gian thực tới Client.
### Tầng Xử Lý Lõi & Lưu Trữ Dữ Liệu (Compute & Storage)
* Private Subnet Compute: Cụm AWS Lambda đặt an toàn trong Private Subnet để xử lý logic nghiệp vụ, tự động lấy credential bảo mật từ AWS Secrets Manager.
* RDS Proxy + Amazon RDS: RDS Proxy đóng vai trò quản lý Connection Pool, giải quyết triệt để sự cố cạn kiệt kết nối DB khi hàng ngàn Lambda function khởi tạo cùng lúc.
* Amazon DynamoDB: Lưu trữ tốc độ cao (độ trễ mili-giây) cho các dữ liệu linh hoạt như Connection ID của WebSocket và trạng thái phiên làm bài.
* S3 Media Storage: Lưu trữ riêng biệt các file đa phương tiện (hình ảnh, âm thanh) của câu hỏi.
### Tầng Xử Lý Bất Đồng Bộ & Cảnh Báo (Async Processing & Monitoring)
* SQS + Lambda Worker: Làm phẳng đỉnh lưu lượng (Traffic Smoothing) khi người dùng bấm nộp bài cùng lúc. SQS sẽ xếp hàng các bài thi và Lambda Worker sẽ tiêu thụ tuần tự để chấm điểm, tránh gây treo giao diện.
* Dead Letter Queue (DLQ): Lưu giữ các tin nhắn xử lý lỗi để đảm bảo không bao giờ làm mất bài thi của người dùng.* * CloudWatch + SNS: Giám sát toàn bộ chỉ số hạ tầng real-time và gửi cảnh báo tức thì qua SNS về cho Admin khi phát hiện sự cố.
Cám ơn mọi người đã đọc.

### Bài viết trên AWS Study Group: Đường link bài Blog: 
https://aws.amazon.com/vi/blogs/compute/building-a-serverless-multiplayer-game-that-scales/