---
title: "Xác thực Cognito"
date: 2024-01-01
weight: 3
pre: " <b> 5.3. </b> "
---

## Hướng dẫn cấu hình Amazon Cognito

Amazon Cognito được sử dụng trong dự án SyncQuiz để quản lý đăng ký, đăng nhập và xác thực người dùng. Dịch vụ này giúp hệ thống có thể tạo User Pool, cấu hình App Client, xác thực bằng email và cung cấp token cho frontend khi người dùng đăng nhập thành công.

### Bước 1: Truy cập dịch vụ Amazon Cognito

Mô tả:
Truy cập AWS Management Console, tìm kiếm dịch vụ Amazon Cognito. Đây là dịch vụ dùng để quản lý danh tính người dùng và kiểm soát truy cập cho ứng dụng.

Chèn hình:
![Truy cập Amazon Cognito](/images/5.3-Cognito/cog1.jpg)

### Bước 2: Chọn chức năng thêm đăng nhập và đăng ký cho ứng dụng

Mô tả:
Tại trang Amazon Cognito, chọn chức năng Add login and signup experiences to your app. Chức năng này dùng để tạo hệ thống xác thực người dùng cho ứng dụng web.

Chèn hình:
![Chọn Add login and signup experiences](/images/5.3-Cognito/cog2.jpg)

### Bước 3: Chọn loại ứng dụng Single-page application

Mô tả:
Trong phần Define your application, chọn Single-page application (SPA) vì frontend của SyncQuiz được xây dựng bằng React. Loại ứng dụng này phù hợp với các website frontend chạy trên trình duyệt.

Chèn hình:
![Chọn Single-page application](/images/5.3-Cognito/cog3.jpg)

### Bước 4: Đặt tên cho ứng dụng

Mô tả:
Nhập tên ứng dụng vào ô Name your application. Trong ví dụ này, tên app client được đặt là webquiz-dev-web-client để phục vụ môi trường phát triển của hệ thống WebQuiz/SyncQuiz.

Chèn hình:
![Đặt tên ứng dụng Cognito](/images/5.3-Cognito/cog4.jpg)

### Bước 5: Chọn phương thức đăng nhập bằng email

Mô tả:
Trong phần Options for login credentials, chọn E-mail. Với lựa chọn này, người dùng có thể đăng ký và đăng nhập bằng địa chỉ email.

Chèn hình:
![Chọn đăng nhập bằng email](/images/5.3-Cognito/cog5.jpg)

### Bước 6: Nhập Return URL cho ứng dụng

Mô tả:
Ở phần Add a return URL, nhập đường dẫn callback của frontend. Đây là URL mà Cognito sẽ chuyển hướng người dùng về sau khi đăng nhập thành công.

Ví dụ môi trường local:
http://localhost:3000/callback

Nếu deploy production, thay bằng domain thật của CloudFront hoặc website đã triển khai.

Chèn hình:
![Nhập Return URL](/images/5.3-Cognito/cog6.jpg)

### Bước 7: Tạo User Directory

Mô tả:
Sau khi hoàn tất các thông tin cần thiết, chọn Create a user directory để Cognito tạo User Pool và App Client cho ứng dụng.

Chèn hình:
![Tạo User Directory](/images/5.3-Cognito/cog7.jpg)

### Bước 8: Kiểm tra User Pool đã được tạo

Mô tả:
Sau khi tạo thành công, quay lại danh sách User groups để kiểm tra User Pool vừa tạo. User Pool này sẽ được dùng để quản lý tài khoản người dùng trong hệ thống.

Chèn hình:
![Kiểm tra User Pool](/images/5.3-Cognito/cog8.jpg)

### Bước 9: Truy cập Authentication Methods

Mô tả:
Trong User Pool, vào mục Authentication, sau đó chọn Authentication methods. Tại đây có thể kiểm tra và cấu hình các phương thức xác thực như email, SMS và chính sách đăng nhập.

Chèn hình:
![Authentication Methods](/images/5.3-Cognito/cog9.jpg)

### Bước 10: Cấu hình Password Policy

Mô tả:
Chọn chỉnh sửa Password Policy để thiết lập chính sách mật khẩu. Trong ví dụ này, mật khẩu tối thiểu 8 ký tự và yêu cầu có số, ký tự đặc biệt, chữ hoa và chữ thường.

Chèn hình:
![Cấu hình Password Policy](/images/5.3-Cognito/cog10.jpg)

### Bước 11: Kiểm tra cấu hình Register

Mô tả:
Chuyển sang mục Register để kiểm tra cấu hình xác minh tài khoản người dùng. Mục này quyết định cách Cognito xác thực email hoặc số điện thoại khi người dùng đăng ký.

Chèn hình:
![Kiểm tra Register](/images/5.3-Cognito/cog11.jpg)

### Bước 12: Chỉnh sửa cấu hình xác minh tài khoản

Mô tả:
Chọn To modify để thay đổi cấu hình xác minh tài khoản người dùng. Bước này dùng để đảm bảo người dùng cần xác minh email trước khi có thể sử dụng tài khoản.

Chèn hình:
![Chỉnh sửa cấu hình Register](/images/5.3-Cognito/cog12.jpg)

### Bước 13: Cấu hình gửi email xác minh

Mô tả:
Trong phần Attribute verification and user account confirmation, chọn cho phép Cognito tự động gửi thông báo xác minh. Sau đó chọn Send an email, verify the email address để Cognito gửi email xác nhận cho người dùng.

Chèn hình:
![Cấu hình gửi email xác minh](/images/5.3-Cognito/cog13.jpg)

### Bước 14: Lưu thay đổi cấu hình xác minh

Mô tả:
Sau khi chọn phương thức xác minh bằng email, bấm Save changes để lưu cấu hình. Từ thời điểm này, người dùng đăng ký tài khoản sẽ cần xác minh email.

Chèn hình:
![Lưu cấu hình xác minh email](/images/5.3-Cognito/cog14.jpg)

### Bước 15: Kiểm tra Application Client

Mô tả:
Vào mục Applications, chọn Application clients để kiểm tra app client đã được tạo. App Client này sẽ cung cấp Client ID cho frontend React khi tích hợp đăng nhập bằng Cognito.

Chèn hình:
![Kiểm tra Application Client](/images/5.3-Cognito/cog15.jpg)

### Bước 16: Hoàn tất cấu hình Cognito

Mô tả:
Sau khi cấu hình User Pool, App Client, email login, return URL, password policy và email verification, hệ thống Cognito đã sẵn sàng để tích hợp với frontend của SyncQuiz.

Chèn hình:
![Hoàn tất cấu hình Cognito](/images/5.3-Cognito/cog16.jpg)

## Kết quả đạt được

Sau khi hoàn thành các bước trên:
- User Pool đã được tạo thành công.
- Ứng dụng SPA đã được cấu hình cho frontend React.
- Người dùng có thể đăng ký và đăng nhập bằng email.
- Return URL đã được cấu hình để Cognito chuyển hướng sau khi đăng nhập.
- Password Policy được thiết lập để tăng tính bảo mật.
- Email verification được bật để xác minh tài khoản người dùng.
- App Client đã sẵn sàng để tích hợp với frontend SyncQuiz.

## Vai trò của Cognito trong dự án SyncQuiz

Trong dự án SyncQuiz, Amazon Cognito đóng vai trò là dịch vụ xác thực người dùng. Khi người dùng đăng ký hoặc đăng nhập, Cognito sẽ xử lý thông tin tài khoản, xác minh email và cấp token xác thực. Frontend React có thể sử dụng token này để gọi các API được bảo vệ, giúp hệ thống đảm bảo chỉ người dùng hợp lệ mới có thể tạo quiz, tham gia phòng hoặc quản lý thông tin cá nhân.
