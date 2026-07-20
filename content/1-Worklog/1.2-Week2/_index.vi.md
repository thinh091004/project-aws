---
title: "Tuần 2"
date: 2026-04-27
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
menuTitle: "Tuần 2"
linkTitle: "Tuần 2"
---
### Mục tiêu tuần 2:

* Hiểu các khái niệm cốt lõi của Amazon EC2 và quản lý truy cập thực thể máy chủ an toàn.
* Làm quen với môi trường phát triển tích hợp dựa trên nền tảng điện toán đám mây bằng AWS Cloud9.
* Thành thạo quản lý lưu trữ đối tượng Amazon S3 và triển khai lưu trữ website tĩnh.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tìm hiểu kiến thức cơ bản về máy chủ ảo với Amazon Elastic Compute Cloud (EC2): Instance types, AMI, và EBS <br> - **Thực hành:** Khởi tạo một EC2 instance và cấu hình Security Groups cơ bản | 27/04/2026   | 27/04/2026      | <https://cloudjourney.awsstudygroup.com/> |                         
| 3   | - Nghiên cứu quản lý quyền ứng dụng bằng cách sử dụng IAM Roles cho EC2 để tránh dùng access key cố định <br> - **Thực hành:** Tạo một IAM Role và gắn nó vào một EC2 instance để truy cập an toàn | 28/04/2026   | 28/04/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Khám phá các môi trường phát triển tích hợp (IDE) trên nền tảng đám mây <br> - **Thực hành:** Khởi tạo môi trường AWS Cloud9, cấu hình các công cụ phát triển và chạy lệnh trên cloud      | 29/04/2026   | 29/04/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Nghiên cứu các khái niệm về Amazon S3 (Simple Storage Service): Buckets, Objects, và các lớp lưu trữ (Storage Classes) tối ưu chi phí <br> - **Thực hành:** Tạo một S3 Bucket, tải lên và quản lý dữ liệu đối tượng an toàn | 30/04/2026   | 30/04/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Cấu hình "Static website hosting" trên Amazon S3 và điều chỉnh Bucket Policies để cho phép truy cập công khai <br> - Kiểm tra tích hợp an toàn giữa EC2 và S3 + Viết báo cáo Tuần 2 | 01/05/2026   | 01/05/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 2:

* Nắm vững các thành phần kiến trúc cốt lõi của EC2 bao gồm việc lựa chọn AMI, các loại Instance, và lưu trữ khối EBS.

* Giảm thiểu tối đa các rủi ro bảo mật thành công nhờ áp dụng IAM Roles cho các EC2 instance thay vì nhúng mã cứng các AWS Access Key dài hạn.

* Thiết lập và sử dụng thành thạo AWS Cloud9 như một môi trường phát triển chính được lưu trữ trên đám mây.

* Thành thạo các kiến thức cơ bản về lưu trữ đối tượng Amazon S3, bao gồm cấu hình vòng đời của bucket và các kiểm soát bảo mật.

* Triển khai và lưu trữ thành công một website tĩnh hoạt động trên Amazon S3 với cấu hình truy cập công khai chính xác thông qua Bucket Policies.

* Đạt được các kỹ năng thực tế trong việc tích hợp và điều phối giao tiếp tài nguyên an toàn giữa các dịch vụ tính toán (EC2) và lưu trữ (S3).

### Kết quả đạt được tuần 2:

* Nắm vững Amazon EC2 như dịch vụ máy chủ ảo, bao gồm loại instance, AMI và các tùy chọn cấu hình chính.

* Tạo và cấu hình thành công EC2 instance cơ bản, kết nối SSH và khám phá cài đặt mạng và lưu trữ.

* Tìm hiểu Amazon VPC và các thành phần cốt lõi: subnet, route table, internet gateway và security group, hiểu cách chúng cô lập và quản lý mạng đám mây.

* Nghiên cứu AWS Lambda và mô hình serverless, tìm hiểu cách Lambda loại bỏ nhu cầu quản lý hạ tầng máy chủ.

* Tạo Lambda function đơn giản và kiểm thử trên AWS Console.

* So sánh EC2 và Lambda, hiểu được các trường hợp sử dụng phù hợp cho từng dịch vụ compute.