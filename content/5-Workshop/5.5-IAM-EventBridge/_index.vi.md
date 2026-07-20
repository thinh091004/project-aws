---
title: "Quyền IAM & EventBridge"
date: 2024-01-01
weight: 5
pre: " <b> 5.5. </b> "
---

## Cấu hình IAM Role và Amazon EventBridge

Trong phần này, hệ thống SyncQuiz cấu hình IAM Role cho AWS Lambda và tạo EventBridge Event Bus để phục vụ xử lý sự kiện nội bộ. IAM Role giúp Lambda có quyền ghi log lên CloudWatch và có thể mở rộng thêm quyền truy cập các dịch vụ khác khi cần. EventBridge được sử dụng để định tuyến các sự kiện phát sinh trong hệ thống, ví dụ như sự kiện bắt đầu game, kết thúc game hoặc lưu kết quả.

### Bước 1: Truy cập IAM Dashboard

Mở AWS Management Console và truy cập dịch vụ Identity and Access Management. Tại IAM Dashboard, có thể xem tổng quan tài nguyên IAM như users, roles, policies và các khuyến nghị bảo mật.

![Truy cập IAM Dashboard](/images/5-Workshop/5.5-IAM-EventBridge/iam1.jpg)

### Bước 2: Mở danh sách Roles

Trong menu bên trái, chọn Roles để xem danh sách các IAM Role hiện có. Đây là nơi quản lý các role được sử dụng bởi Lambda, API Gateway, RDS, CloudWatch hoặc các dịch vụ AWS khác.

![Mở danh sách IAM Roles](/images/5-Workshop/5.5-IAM-EventBridge/iam2.jpg)

### Bước 3: Tạo IAM Role cho Lambda

Chọn Create role. Ở phần Trusted entity type, chọn AWS service. Trong phần Use case, chọn Lambda để cho phép Lambda function sử dụng role này khi thực thi.

![Tạo IAM Role cho Lambda](/images/5-Workshop/5.5-IAM-EventBridge/iam3.jpg)

### Bước 4: Gán quyền AWSLambdaBasicExecutionRole

Ở bước Add permissions, tìm kiếm policy AWSLambdaBasicExecutionRole và chọn policy này. Policy này cho phép Lambda ghi log vào Amazon CloudWatch Logs, giúp theo dõi lỗi và quá trình thực thi function.

![Gán quyền AWSLambdaBasicExecutionRole](/images/5-Workshop/5.5-IAM-EventBridge/iam4.jpg)

### Bước 5: Đặt tên cho IAM Role

Ở bước Name, review, and create, nhập tên role là webquiz-dev-lambda-role. Tên role nên thể hiện rõ môi trường và mục đích sử dụng để dễ quản lý trong quá trình phát triển.

![Đặt tên IAM Role](/images/5-Workshop/5.5-IAM-EventBridge/iam5.jpg)

### Bước 6: Kiểm tra IAM Role sau khi tạo

Sau khi tạo role thành công, mở role webquiz-dev-lambda-role để kiểm tra các permission đã gắn. Role này có AWSLambdaBasicExecutionRole và có thể thêm inline policy riêng nếu Lambda cần truy cập các dịch vụ khác như DynamoDB hoặc EventBridge.

![Kiểm tra IAM Role](/images/5-Workshop/5.5-IAM-EventBridge/iam6.jpg)

### Bước 6.1: Thiết lập Chính sách Phân quyền Custom (Inline Policy)

Để cấp quyền cho Lambda tương tác với DynamoDB, EventBridge và WebSocket API, cần gắn thêm một inline policy cho role vừa tạo:

1. Tìm kiếm và nhấp chọn role vừa tạo: webquiz-dev-lambda-role.
2. Tại tab **Permissions**, nhấp chọn **Add permissions** → Chọn **Create inline policy**.
3. Chọn tab **JSON** và dán chính sách phân quyền sau:
   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "DynamoDBAccess",
               "Effect": "Allow",
               "Action": [
                   "dynamodb:GetItem",
                   "dynamodb:PutItem",
                   "dynamodb:UpdateItem",
                   "dynamodb:DeleteItem",
                   "dynamodb:Query",
                   "dynamodb:Scan",
                   "dynamodb:BatchGetItem",
                   "dynamodb:BatchWriteItem"
               ],
               "Resource": [
                   "arn:aws:dynamodb:us-east-1:*:table/webquiz-dev-*",
                   "arn:aws:dynamodb:us-east-1:*:table/webquiz-dev-*/index/*"
               ]
           },
           {
               "Sid": "EventBridgeAccess",
               "Effect": "Allow",
               "Action": [
                   "events:PutEvents"
               ],
               "Resource": "arn:aws:events:us-east-1:*:event-bus/webquiz-dev-game-events"
           },
           {
               "Sid": "WebSocketManagement",
               "Effect": "Allow",
               "Action": [
                   "execute-api:ManageConnections"
               ],
               "Resource": "arn:aws:execute-api:us-east-1:*:*/dev/*"
           }
       ]
   }
   ```
4. Nhấn **Next**.
5. **Policy name:** Nhập webquiz-dev-lambda-policy.
6. Nhấn **Create policy** để hoàn tất.

![Thiết lập Chính sách Phân quyền Custom](/images/5-Workshop/5.5-IAM-EventBridge/policy1.png)

---

### Bước 7: Truy cập Amazon EventBridge

Mở dịch vụ Amazon EventBridge và chọn mục Event buses. Event bus là nơi nhận và định tuyến các sự kiện từ ứng dụng hoặc các dịch vụ AWS.

![Truy cập Amazon EventBridge](/images/5-Workshop/5.5-IAM-EventBridge/iam7.jpg)

### Bước 8: Tạo Custom Event Bus

Trong phần Custom event bus, chọn Create event bus để tạo event bus riêng cho hệ thống SyncQuiz. Việc tạo event bus riêng giúp tách biệt sự kiện của ứng dụng với default event bus.

![Tạo Custom Event Bus](/images/5-Workshop/5.5-IAM-EventBridge/iam8.jpg)

### Bước 9: Nhập tên Event Bus

Ở trang Create event bus, nhập tên event bus là webquiz-dev-game-events. Event bus này được dùng để định tuyến các sự kiện liên quan đến game, quiz room và kết quả trong hệ thống.

![Nhập tên Event Bus](/images/5-Workshop/5.5-IAM-EventBridge/iam9.jpg)

### Bước 10: Hoàn tất tạo Event Bus

Giữ các tùy chọn mặc định nếu chưa cần cấu hình nâng cao, sau đó chọn Create để tạo event bus. Sau khi tạo thành công, hệ thống có thể sử dụng event bus này để gửi và xử lý các sự kiện bất đồng bộ.

![Hoàn tất tạo Event Bus](/images/5-Workshop/5.5-IAM-EventBridge/iam10.jpg)

## Kết quả đạt được

Sau khi hoàn thành các bước trên:
- IAM Role cho Lambda đã được tạo thành công.
- Lambda có quyền ghi log lên CloudWatch thông qua AWSLambdaBasicExecutionRole.
- Role webquiz-dev-lambda-role có thể được gắn vào các Lambda function trong dự án.
- Custom Event Bus webquiz-dev-game-events đã được tạo trong Amazon EventBridge.
- Hệ thống có nền tảng để xử lý sự kiện nội bộ và mở rộng luồng xử lý bất đồng bộ.

## Vai trò trong dự án SyncQuiz

Trong dự án SyncQuiz, IAM Role được sử dụng để cấp quyền an toàn cho Lambda thay vì dùng trực tiếp thông tin tài khoản AWS. EventBridge hỗ trợ định tuyến sự kiện trong hệ thống, giúp các thành phần như Lambda xử lý logic game, lưu kết quả hoặc cập nhật trạng thái có thể hoạt động theo hướng tách biệt và dễ mở rộng hơn.
