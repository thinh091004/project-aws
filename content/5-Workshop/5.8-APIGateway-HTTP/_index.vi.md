---
title: "API Gateway - HTTP API"
date: 2024-01-01
weight: 8
pre: " <b> 5.8. </b> "
---

## Thiết lập Amazon API Gateway HTTP API

Amazon API Gateway HTTP API được sử dụng trong dự án SyncQuiz để xây dựng các API backend phục vụ frontend React. HTTP API có độ trễ thấp, chi phí tối ưu và phù hợp để kết nối với AWS Lambda cho các chức năng như quản lý quiz, tạo phòng, lấy thông tin người dùng và xử lý dữ liệu hệ thống.

### Bước 1: Truy cập Amazon API Gateway

Mở AWS Management Console và truy cập dịch vụ API Gateway. Tại trang APIs, có thể xem danh sách các API đã tạo trong tài khoản AWS. Để tạo API mới, chọn Create API.

![Truy cập API Gateway](/images/5-Workshop/5.8-APIGateway-HTTP/api1.jpg)

### Bước 2: Chọn loại HTTP API

Ở trang Choose an API type, chọn HTTP API và bấm Build. HTTP API phù hợp cho các REST API đơn giản, có độ trễ thấp và dễ tích hợp với Lambda backend.

![Chọn HTTP API](/images/5-Workshop/5.8-APIGateway-HTTP/api2.jpg)

### Bước 3: Cấu hình thông tin API

Trong phần Configure API, nhập tên API là webquiz-dev-http-api. Ở phần IP address type, chọn IPv4. Ở bước này có thể chưa cần thêm integration ngay, vì integration và routes có thể cấu hình sau khi API được tạo.

![Cấu hình HTTP API](/images/5-Workshop/5.8-APIGateway-HTTP/api3.jpg)

### Bước 4: Bỏ qua cấu hình Routes ban đầu

Ở bước Configure routes, có thể bỏ qua việc tạo route ban đầu nếu chưa có Lambda integration cụ thể. Routes sẽ được thêm sau tùy theo chức năng backend như tạo quiz, lấy quiz, tạo phòng hoặc xử lý kết quả.

![Cấu hình Routes](/images/5-Workshop/5.8-APIGateway-HTTP/api4.jpg)

### Bước 5: Cấu hình Stage

Ở bước Define stages, nhập stage name là dev và bật Auto-deploy. Stage dev được dùng cho môi trường phát triển. Khi Auto-deploy được bật, các thay đổi trong API sẽ được triển khai tự động lên stage này.

![Cấu hình Stage dev](/images/5-Workshop/5.8-APIGateway-HTTP/api5.jpg)

### Bước 6: Kiểm tra và tạo API

Ở bước Review and create, kiểm tra lại thông tin API, Routes và Stages. Nếu thông tin đúng, chọn Create để tạo HTTP API.

![Kiểm tra và tạo HTTP API](/images/5-Workshop/5.8-APIGateway-HTTP/api6.jpg)

### Bước 7: Kiểm tra HTTP API sau khi tạo

Sau khi tạo thành công, API Gateway sẽ hiển thị trang Routes của API vừa tạo. Tại đây có thể tiếp tục tạo routes, cấu hình authorization, thêm integrations với Lambda và deploy API.

![HTTP API được tạo thành công](/images/5-Workshop/5.8-APIGateway-HTTP/api7.jpg)

---

### 2. Cấu hình CORS

Để cho phép frontend gọi các request API từ các domain khác hoặc từ localhost:

1. Trong menu bên trái của API vừa tạo, chọn **CORS** và nhấp chọn **Configure**.

![Truy cập và cấu hình CORS](/images/workshop/5.8-apigateway/cors1.jpg)

2. Nhập các thông số cấu hình CORS như sau:
   * **Access-Control-Allow-Origin:** Nhập `*`.
   * **Access-Control-Allow-Headers:** Nhập `Content-Type, Authorization`.
   * **Access-Control-Allow-Methods:** Nhập `GET, POST, PUT, DELETE, OPTIONS`.
   * **Access-Control-Max-Age:** Nhập `300`.

![Nhập thông số cấu hình CORS](/images/workshop/5.8-apigateway/cors2.jpg)

3. Nhấp chọn **Save** để hoàn tất cấu hình.

![Lưu cấu hình CORS thành công](/images/workshop/5.8-apigateway/cors3.jpg)

---

### 3. Tạo bộ xác thực Cognito JWT Authorizer

1. Chọn **Authorization** ở menu bên trái.
2. Chọn tab **Manage authorizers**, nhấp chọn **Create**.
3. Thiết lập thông số Authorizer:
   * **Authorizer type:** Chọn **JWT**.
   * **Name:** Nhập CognitoAuthorizer.
   * **Identity source:** Nhập `$request.header.Authorization`.
   * **Issuer URL:** Nhập `https://cognito-idp.us-east-1.amazonaws.com/YOUR_USER_POOL_ID` (Thay thế `YOUR_USER_POOL_ID` bằng User Pool ID thực tế đã lưu ở phần Cognito).
   * **Audience:** Nhập **App Client ID** đã lưu ở phần Cognito.
   * Nhấp chọn **Create**.

---

### 4. Tạo các Tích hợp (Integrations)

Kết nối API Gateway với các hàm Lambda xử lý nghiệp vụ backend:

1. Chọn **Integrations** ở menu bên trái.
2. Nhấp chọn **Create** cho 2 integration sau:
   * **Integration 1 (Quiz CRUD):**
     * **Integration target:** Chọn **Lambda function**.
     * **Lambda function:** Chọn webquiz-dev-quiz-crud.
     * Nhấp chọn **Create**.
   * **Integration 2 (Room Management):**
     * Nhấp chọn **Create**.
     * **Integration target:** Chọn **Lambda function**.
     * **Lambda function:** Chọn webquiz-dev-room-management.
     * Nhấp chọn **Create**.

---

### 5. Tạo Định tuyến (Routes) & Gán Phân Quyền

Liên kết các route đường dẫn của API, tích hợp Lambda và gắn quyền xác thực tương ứng:

1. Chọn **Routes** ở menu bên trái.
2. Khởi tạo và thiết lập 5 route theo bảng dưới đây:

| STT | Phương thức (Method) | Đường dẫn (Path) | Tích hợp Target (Integration) | Bộ xác thực (Authorizer) |
| :--- | :--- | :--- | :--- | :--- |
| **Route 1** | `ANY` | `/quizzes` | webquiz-dev-quiz-crud | CognitoAuthorizer |
| **Route 2** | `ANY` | `/quizzes/{proxy+}` | webquiz-dev-quiz-crud | CognitoAuthorizer |
| **Route 3** | `POST` | `/rooms` | webquiz-dev-room-management | CognitoAuthorizer |
| **Route 4** | `GET` | `/rooms/{pin}` | webquiz-dev-room-management | **None** (Công khai) |
| **Route 5** | `POST` | `/rooms/{pin}/join` | webquiz-dev-room-management | **None** (Công khai) |

*Các bước cấu hình cho từng Route:*
1. Nhấp chọn **Create**, nhập **Method** và **Path** tương ứng.
2. Click vào route vừa tạo → Chọn **Attach integration** và gán hàm Lambda tương ứng.
3. Chọn **Attach authorizer** (nếu bảng yêu cầu) và gán CognitoAuthorizer.

---

### 6. Lưu lại Endpoint REST API

1. Chọn mục **Stages** trên menu bên trái.
2. Click chọn stage tên là **`dev`**.
3. Sao chép và lưu trữ URL tại phần **Invoke URL**:
   ```
   https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/dev
   ```
   *(Bạn sẽ cần dùng link REST endpoint này để cấu hình cho client frontend sau này).*

## Kết quả đạt được

Sau khi hoàn thành các bước trên:
- HTTP API webquiz-dev-http-api đã được tạo thành công.
- Stage dev đã được cấu hình với Auto-deploy.
- API Gateway đã sẵn sàng để thêm routes và integrations.
- Hệ thống có nền tảng để frontend React gọi backend thông qua HTTP API.
- Các Lambda function có thể được tích hợp vào API Gateway ở các bước tiếp theo.

## Vai trò trong dự án SyncQuiz

Trong dự án SyncQuiz, HTTP API đóng vai trò là cổng giao tiếp giữa frontend React và backend serverless. Khi người dùng thao tác trên hệ thống, frontend sẽ gửi request đến API Gateway. API Gateway sau đó chuyển request đến Lambda function tương ứng để xử lý nghiệp vụ như tạo quiz, lấy danh sách quiz, tạo phòng chơi hoặc lưu kết quả.
