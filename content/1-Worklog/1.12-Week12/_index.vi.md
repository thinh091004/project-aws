---
title: "Tuần 12"
date: 2026-07-06
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
menuTitle: "Tuần 12"
linkTitle: "Tuần 12"
---

### TUẦN 12: THEO DÕI SAU TRIỂN KHAI, BẢO TRÌ HẠ TẦNG, ĐÁNH GIÁ HIỆU NĂNG & TỔNG KẾT KINH NGHIỆM (POST-DEPLOYMENT & LESSONS LEARNED)

#### Mục tiêu tuần 12:
* Theo dõi và giám sát độ ổn định của hệ thống WebQuiz trên môi trường Production sau khi bàn giao.
* Đánh giá lại các chỉ số tiêu thụ tài nguyên của Lambda, API Gateway và DynamoDB để tối ưu hóa chi phí.
* Tổng kết toàn bộ hành trình thực tập, đúc kết các bài học kinh nghiệm (Lessons Learned) và hoàn tất thủ tục đóng log dự án.

#### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Giám sát hệ thống:** Sử dụng Amazon CloudWatch và X-Ray để theo dõi các số liệu thực tế (Real-world metrics) sau khi hệ thống vận hành <br>- Kiểm tra log lỗi (Error logs) hoặc các request bị chậm (Latency spikes) nếu có | 06/07/2026 | 06/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - **Tối ưu hóa hạ tầng:** Đánh giá lại dung lượng lưu trữ và tần suất đọc ghi trên DynamoDB <br>- Điều chỉnh lại thời gian giữ log (Log Retention Policy) của CloudWatch từ vô hạn xuống ngắn hạn để tránh phát sinh chi phí ẩn | 07/07/2026 | 07/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **Bảo trì mã nguồn:** Sửa đổi và tối ưu hóa lại một số hàm Lambda dựa trên các góp ý và nhận xét từ buổi Demo nghiệm thu ở tuần trước <br>- Cập nhật phiên bản code an toàn lên kho lưu trữ dự phòng | 08/07/2026 | 08/07/2026 | Tài liệu dự án |
| 5 | - **Tổng kết kinh nghiệm:** Viết tài liệu tổng kết kỹ thuật (Post-mortem / Lessons Learned Report), ghi nhận các lỗi kiến trúc đã gặp và cách khắc phục để làm tài liệu tham khảo cho các dự án sau | 09/07/2026 | 09/07/2026 | Tài liệu nội bộ |
| 6 | - **Đóng log dự án:** Thu hồi hoàn toàn các IAM Access Keys tạm thời, dọn dẹp môi trường máy trạm cục bộ <br>- Chính thức đóng log Worklog chuỗi 12 tuần thực tập và nhận đánh giá từ đơn vị | 10/07/2026 | 10/07/2026 | Tài liệu dự án |

#### Kết quả đạt được tuần 12:
* Đảm bảo hệ thống WebQuiz Serverless vận hành ổn định trên đám mây, không phát sinh lỗi nghiêm trọng sau bàn giao.
* Tối ưu hóa chi phí hạ tầng AWS thành công thông qua việc siết chặt chính sách lưu trữ log và tinh chỉnh DynamoDB.
* Hoàn thiện bộ tài liệu đúc kết kinh nghiệm (Lessons Learned) quý giá về việc xử lý kết nối WebSocket và kiến trúc hướng sự kiện.
* Vô hiệu hóa an toàn các khóa bảo mật (Access Keys) cũ, đảm bảo an toàn tuyệt đối cho tài khoản AWS sau khi dự án kết thúc.
