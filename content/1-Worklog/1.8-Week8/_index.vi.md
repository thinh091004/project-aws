---
title: "Tuần 8"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
menuTitle: "Tuần 8"
linkTitle: "Tuần 8"
---
### Mục tiêu tuần 8:
* Bắt buộc truyền Cognito Token trong Header của tất cả các truy vấn từ Frontend đến API Gateway.
* Xây dựng hàm xử lý logic Chấm điểm cơ bản (AWS Lambda) và viết bộ kiểm thử tự động với Postman.

#### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Bảo mật API:** Cấu hình API Gateway giải mã (decode) Cognito JWT Token trong Header `Authorization: Bearer <token>` để trích xuất thông tin User ID | 08/06/2026 | 08/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - **Frontend - API:** Cấu hình Interceptor (Axios/Fetch) trên Frontend để tự động đính kèm Cognito Token vào Header của mọi HTTP Request gửi tới API Gateway | 09/06/2026 | 09/06/2026 | Tài liệu dự án |
| 4 | - **Chấm điểm cơ bản:** Viết AWS Lambda Function xử lý logic Chấm điểm cơ bản (nhận input bài nộp -> tính điểm -> lưu kết quả vào DB) | 10/06/2026 | 10/06/2026 | Tài liệu dự án |
| 5 | - **Postman Test:** Xây dựng kịch bản kiểm thử API Chấm điểm: Validate Status Code 200, Response Schema và kiểm tra độ chính xác của kết quả điểm số | 11/06/2026 | 11/06/2026 | <https://www.postman.com/> |
| 6 | - **Tích hợp:** Nối API Chấm điểm với giao diện nộp bài Frontend; chạy kiểm thử liên hoàn từ UI -> API Gateway -> Lambda -> DB <br>- Viết báo cáo Worklog Tuần 8 | 12/06/2026 | 12/06/2026 | Tài liệu dự án |

#### Kết quả đạt được tuần 8:
* Chuẩn hóa luồng gửi request an toàn từ Frontend đến API Gateway với Header `Authorization: Bearer <token>`.
* Triển khai thành công AWS Lambda Engine tính toán và xử lý kết quả Chấm điểm tự động.
* Frontend đã nộp được dữ liệu bài tập lên API và nhận về kết quả điểm số theo thời gian thực.
* Viết thành công các kịch bản Postman Test tự động bắt lỗi cấu hình Header và kiểm tra cấu trúc dữ liệu API Chấm điểm.