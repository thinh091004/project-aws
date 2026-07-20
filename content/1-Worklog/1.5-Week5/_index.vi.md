---
title: "Tuần 5"
date: 2026-05-18
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
menuTitle: "Tuần 5"
linkTitle: "Tuần 5"
---
### Mục tiêu tuần 5:

* Tối ưu hóa hiệu năng hệ thống bằng cách triển khai bộ nhớ đệm trong bộ nhớ (In-memory caching) với Amazon ElastiCache.
* Nâng cao kiến thức mạng chuyên sâu trên nền t mây thông qua các bài thực hành workshop kiến trúc thực tế.
* Tăng tốc truyền tải nội dung toàn cầu và tiếp cận giải pháp tính toán tại biên mạng bằng Amazon CloudFront và Lambda@Edge.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Nghiên cứu giải pháp lưu trữ bộ nhớ đệm (Caching) để tăng tốc truy vấn dữ liệu hiệu năng cao <br> - **Thực hành:** Khởi tạo một cụm Amazon ElastiCache (Redis/Memcached) nhằm giảm tải đọc trực tiếp cho RDS | 18/05/2026   | 18/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Nghiên cứu sâu về các mô hình thiết kế mạng nâng cao và giao tiếp liên VPC <br> - **Thực hành:** Tham gia "Workshop về mạng trên AWS" để cấu hình kết nối mở rộng (VPC Peering, định tuyến nâng cao) | 19/05/2026   | 19/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Tìm hiểu mạng lưới phân phối nội dung (CDN) và cơ chế hoạt động của bộ nhớ đệm tại biên mạng <br> - **Thực hành:** Khởi tạo Amazon CloudFront Distribution, cấu hình S3 Bucket hoặc Load Balancer làm nguồn gốc (Origin) | 20/05/2026   | 20/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Khám phá năng lực tính toán tại biên mạng nhằm chạy các đoạn mã xử lý gần với vị trí người dùng nhất <br> - **Thực hành:** Nghiên cứu tích hợp CloudFront và Lambda@Edge để tùy biến các yêu cầu HTTP tại Edge Location | 21/05/2026   | 21/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Đo lường và đánh giá các chỉ số độ trễ phản hồi của hệ thống (Latency, TTFB) trước và sau khi có Caching và CDN <br> - Thu thập dữ liệu tối ưu + Viết báo cáo Tuần 5 | 22/05/2026   | 22/05/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 5:

* Thiết lập thành công tầng đệm dữ liệu tốc độ cao với Amazon ElastiCache, giảm thiểu tối đa áp lực truy vấn đọc trực tiếp lên hệ thống cơ sở dữ liệu quan hệ RDS.

* Làm chủ các kỹ năng định tuyến mạng phức tạp và kết nối liên thông các vùng mạng nhờ hoàn thành bài thực hành Network Workshop chuyên sâu.

* Triển khai hoàn chỉnh mạng lưới phân phối nội dung với Amazon CloudFront, giúp tăng tốc tối đa tốc độ tải trang và giảm độ trễ trải nghiệm cho người dùng cuối.

* Tiếp thu tư duy kiến trúc mới về tính toán không máy chủ tại biên mạng (Serverless Edge Computing) thông qua mô hình hoạt động của Lambda@Edge.

* Chứng minh được hiệu quả tối ưu hóa hạ tầng bằng các số liệu thực tế thông qua việc đo lường thời gian phản hồi hệ thống trước và sau khi cải tiến.


