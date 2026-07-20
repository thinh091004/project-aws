---
title: "Tuần 9"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
menuTitle: "Tuần 9"
linkTitle: "Tuần 9"
---
### Mục tiêu tuần 9:
* Tăng cường phân quyền chi tiết (RBAC) dựa trên Cognito Groups (Admin/User) và xử lý tự động làm mới Token (Refresh Token).
* Hoàn thiện giao diện Dashboard Chấm điểm trên Frontend và xây dựng kịch bản Postman Test tự động chạy theo chuỗi nghiệp vụ.

#### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Bảo mật API:** Phân quyền nâng cao (RBAC) qua Cognito Groups (phân biệt quyền Sinh viên nộp bài / Giảng viên xem bảng điểm) <br>- Xử lý tự động gia hạn Session bằng Refresh Token | 15/06/2026 | 15/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - **Frontend - API:** Tích hợp giao diện Dashboard hiển thị lịch sử chấm điểm, biểu đồ điểm số và phản hồi chi tiết từ API <br>- Xử lý các lỗi HTTP 403 Forbidden trên UI khi người dùng không đủ quyền | 16/06/2026 | 16/06/2026 | Tài liệu dự án |
| 4 | - **Chấm điểm cơ bản:** Tối ưu hóa thuật toán chấm điểm: xử lý các trường hợp biên (Edge cases), tính điểm cho nhiều dạng bài nộp và lưu lịch sử làm bài | 17/06/2026 | 17/06/2026 | Tài liệu dự án |
| 5 | - **Postman Test:** Viết script kiểm thử tự động đa bước (Multi-step test flow): [Đăng nhập lấy Token] -> [Nộp bài] -> [Gọi API Chấm điểm] -> [Kiểm tra Bảng điểm] | 18/06/2026 | 18/06/2026 | <https://www.postman.com/> |
| 6 | - **Tích hợp:** Kiểm thử toàn diện sự đồng bộ giữa phân quyền Cognito, giao diện Dashboard Frontend và kết quả tính toán của Engine Chấm điểm <br>- Viết báo cáo Worklog Tuần 9 | 19/06/2026 | 19/06/2026 | Tài liệu dự án |

#### Kết quả đạt được tuần 9:
* Hoàn thiện cơ chế phân quyền RBAC chặt chẽ với Cognito Groups và xử lý mượt mà việc làm mới Session bằng Refresh Token.
* Frontend hiển thị Dashboard Chấm điểm trực quan, hiển thị lịch sử nộp bài và thông báo lỗi phân quyền thân thiện.
* Engine Chấm điểm xử lý mượt mà các dạng bài tập khác nhau và đảm bảo tính toàn vẹn của lịch sử làm bài.
* Xây dựng thành công kịch bản Postman Automated Test Suite chạy liên hoàn tự động từ bước Xác thực đến bước Kiểm tra Bảng điểm.

