---
title: "Tuần 4"
date: 2026-05-11
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
menuTitle: "Tuần 4"
linkTitle: "Tuần 4"
---
### Mục tiêu tuần 4:

* Làm chủ giải pháp mở rộng hạ tầng tự động sử dụng Amazon EC2 Auto Scaling và bộ cân bằng tải Elastic Load Balancing (ELB).
* Triển khai hệ thống giám sát tập trung, xây dựng bảng theo dõi chỉ số và cài đặt cảnh báo tự động với Amazon CloudWatch.
* Nắm vững kỹ năng định tuyến tên miền toàn cầu với Amazon Route 53 và thành thạo sử dụng AWS CLI để quản trị hạ tầng nhanh chóng.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Nghiên cứu kiến trúc sẵn sàng cao và cơ chế tự động co giãn trên đám mây AWS <br> - **Thực hành:** Tạo Launch Template, cấu hình bộ cân bằng tải Application Load Balancer (ALB) và thiết lập nhóm EC2 Auto Scaling Group | 11/05/2026   | 11/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Tìm hiểu các chỉ số giám sát (Metrics) và cơ chế thu thập dữ liệu của Amazon CloudWatch <br> - **Thực hành:** Tạo Dashboard giám sát tùy chỉnh và thiết lập CloudWatch Alarms gửi thông báo qua SNS (Email) | 12/05/2026   | 12/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Nghiên cứu hệ thống quản lý tên miền và các chính sách định tuyến của Amazon Route 53 <br> - **Thực hành:** Cấu hình các bản ghi DNS (A, CNAME) để trỏ tên miền về S3 static web hoặc Load Balancer | 13/05/2026   | 13/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Khám phá cấu trúc câu lệnh và cơ chế xác thực dòng lệnh thông qua AWS Command Line Interface (CLI) <br> - **Thực hành:** Thực hiện các tác vụ quản trị, khởi tạo và xóa tài nguyên trực tiếp từ Terminal bằng lệnh AWS CLI | 14/05/2026   | 14/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Chạy kịch bản giả lập ép tải (Stress Test) để kiểm tra độ nhạy của hệ thống Auto Scaling và tính chuẩn xác của cảnh báo CloudWatch <br> - Thu thập dữ liệu hiệu năng + Viết báo cáo Tuần 4 | 15/05/2026   | 15/05/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 4:

* Xây dựng và vận hành thành công hệ thống hạ tầng có khả năng tự co giãn (Elasticity), tự động thêm/bớt máy chủ dựa trên lưu lượng truy cập thực tế của người dùng.

* Thiết lập hoàn chỉnh trang quản trị giám sát tập trung sử dụng Amazon CloudWatch để theo dõi sát sao tình trạng sức khỏe hệ thống.

* Cấu hình thành công cơ chế gửi cảnh báo tự động qua Email (qua dịch vụ Amazon SNS) mỗi khi máy chủ gặp sự cố quá tải hoặc chạm ngưỡng tài nguyên tới hạn.

* Làm chủ kỹ thuật quản lý tên miền và định tuyến lưu lượng mạng thông minh về các tài nguyên AWS bằng Amazon Route 53.

* Thành thạo kỹ năng sử dụng Terminal, viết lệnh và chạy script để tương tác với tài nguyên đám mây nhanh chóng qua bộ công cụ AWS CLI.

* Đã kiểm thử và chứng minh được tính chịu tải, khả năng phản ứng linh hoạt của cụm Auto Scaling thông qua bài thực hành giả lập ép tải (Stress Test) thực tế.

