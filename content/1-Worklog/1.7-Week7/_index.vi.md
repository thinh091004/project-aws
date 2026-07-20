---
title: "Tuần 7"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
menuTitle: "Tuần 7"
linkTitle: "Tuần 7"
---
### Mục tiêu tuần 7:
* Khởi tạo hạ tầng xác thực với Amazon Cognito và tích hợp luồng Đăng nhập/Đăng ký trên Frontend.
* Thiết lập Cognito Authorizer trên API Gateway, chốt sơ đồ DB cho tính năng Chấm điểm và tạo Postman Collection ban đầu.

#### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Bảo mật API:** Khởi tạo Amazon Cognito User Pool & App Client; định nghĩa các thuộc tính người dùng (Email, Role, Full Name) <br>- **Postman:** Khai báo Postman Environment (Base URL, Cognito Client ID) để chuẩn bị kiểm thử các API Auth | 01/06/2026 | 01/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - **Bảo mật API:** Thiết lập Cognito Authorizer trên API Gateway để kiểm tra tính hợp lệ của Token <br>- **Postman:** Viết kịch bản test API Đăng nhập/Đăng ký và tự động bắt `id_token`, `access_token` lưu vào biến môi trường | 02/06/2026 | 02/06/2026 | <https://www.postman.com/> |
| 4 | - **Frontend - API:** Cấu hình CORS (Origins, Headers) trên API Gateway cho phép Frontend kết nối <br>- Tích hợp AWS Amplify/Cognito SDK vào Frontend để dựng trang Đăng nhập và lấy Cognito Token về Client | 03/06/2026 | 03/06/2026 | Tài liệu dự án |
| 5 | - **Chấm điểm cơ bản:** Phân tích quy trình nghiệp vụ, thiết kế thuật toán chấm điểm và định nghĩa bảng lưu trữ kết quả (DynamoDB/RDS) <br>- **Postman:** Tạo kịch bản test gửi request không chứa Token để xác nhận API trả lỗi HTTP 401 Unauthorized | 04/06/2026 | 04/06/2026 | Tài liệu dự án |
| 6 | - **Tích hợp:** Kiểm thử liên hoàn luồng Auth: Frontend Đăng nhập -> Lấy Token -> Gọi API thử nghiệm -> Postman xác minh tính đúng đắn <br>- Viết báo cáo Worklog Tuần 7 | 05/06/2026 | 05/06/2026 | Tài liệu dự án |

#### Kết quả đạt được tuần 7:
* Khởi tạo thành công Amazon Cognito User Pool và đính kèm Cognito Authorizer bảo vệ API Gateway Endpoints.
* Dựng hoàn thiện giao diện Đăng nhập/Đăng ký trên Frontend, kết nối lấy Cognito Token thành công về Client.
* Chốt sơ đồ cơ sở dữ liệu và bộ tiêu chí logic cho tính năng Chấm điểm cơ bản.
* Xây dựng bộ Postman Collection ban đầu, tự động hóa việc bắt và lưu Cognito Token sau khi xác thực.


