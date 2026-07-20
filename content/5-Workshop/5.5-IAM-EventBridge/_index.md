---
title: "IAM Permissions & EventBridge"
date: 2024-01-01
weight: 5
pre: " <b> 5.5. </b> "
---

## IAM Role and Amazon EventBridge Configuration

In this section, the SyncQuiz system configures the IAM Role for AWS Lambda and creates the EventBridge Event Bus to handle internal event processing. The IAM Role grants Lambda permissions to write logs to CloudWatch and can be extended to access other services as needed. EventBridge is used to route system events, such as game starting, game ending, or result saving events.

### Step 1: Access the IAM Dashboard

Open the AWS Management Console and access the Identity and Access Management service. On the IAM Dashboard, you can see an overview of IAM resources like users, roles, policies, and security recommendations.

![Access IAM Dashboard](/images/5-Workshop/5.5-IAM-EventBridge/iam1.jpg)

### Step 2: Open the Roles List

In the left menu, select Roles to view the list of existing IAM Roles. This is where you manage roles used by Lambda, API Gateway, RDS, CloudWatch, or other AWS services.

![Open IAM Roles List](/images/5-Workshop/5.5-IAM-EventBridge/iam2.jpg)

### Step 3: Create an IAM Role for Lambda

Click Create role. Under Trusted entity type, select AWS service. Under Use case, select Lambda to allow Lambda functions to use this role when executing.

![Create IAM Role for Lambda](/images/5-Workshop/5.5-IAM-EventBridge/iam3.jpg)

### Step 4: Attach the AWSLambdaBasicExecutionRole Policy

In the Add permissions step, search for the policy AWSLambdaBasicExecutionRole and select it. This policy allows Lambda to write logs to Amazon CloudWatch Logs, helping track errors and function execution.

![Attach AWSLambdaBasicExecutionRole](/images/5-Workshop/5.5-IAM-EventBridge/iam4.jpg)

### Step 5: Name the IAM Role

In the Name, review, and create step, enter the role name as webquiz-dev-lambda-role. The role name should clearly reflect the environment and purpose for easier management during development.

![Name the IAM Role](/images/5-Workshop/5.5-IAM-EventBridge/iam5.jpg)

### Step 6: Verify the Created IAM Role

After successfully creating the role, open webquiz-dev-lambda-role to verify the attached permissions. This role currently has AWSLambdaBasicExecutionRole attached, and you can add a custom inline policy if Lambda needs to access other services like DynamoDB or EventBridge.

![Verify IAM Role](/images/5-Workshop/5.5-IAM-EventBridge/iam6.jpg)

### Step 6.1: Attach Custom Inline Policy

To grant this role permission to access your specific DynamoDB tables, write events to EventBridge, and manage WebSocket connections, you must attach a custom inline policy:

1. Find and click on the newly created role webquiz-dev-lambda-role.
2. Under the **Permissions** tab, click **Add permissions** → Select **Create inline policy**.
3. Select the **JSON** tab and paste the following policy:
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
4. Click **Next**.
5. **Policy name:** Enter webquiz-dev-lambda-policy.
6. Click **Create policy** to complete the process.

![Attach Custom Inline Policy](/images/5-Workshop/5.5-IAM-EventBridge/policy1.png)

---

### Step 7: Access Amazon EventBridge

Open the Amazon EventBridge service and select the Event buses section. An Event bus receives and routes events from your application or AWS services.

![Access Amazon EventBridge](/images/5-Workshop/5.5-IAM-EventBridge/iam7.jpg)

### Step 8: Create a Custom Event Bus

Under Custom event bus, select Create event bus to create a separate event bus for the SyncQuiz system. Creating a dedicated event bus helps isolate application events from the default event bus.

![Create Custom Event Bus](/images/5-Workshop/5.5-IAM-EventBridge/iam8.jpg)

### Step 9: Enter the Event Bus Name

On the Create event bus page, enter the event bus name as webquiz-dev-game-events. This event bus will be used to route events related to games, quiz rooms, and results in the system.

![Enter Event Bus Name](/images/5-Workshop/5.5-IAM-EventBridge/iam9.jpg)

### Step 10: Complete Event Bus Creation

Keep the default options if no advanced configuration is required, then select Create to generate the event bus. Once created successfully, the system can use this event bus to send and process asynchronous events.

![Complete Event Bus Creation](/images/5-Workshop/5.5-IAM-EventBridge/iam10.jpg)

## Expected Outcomes

After completing the steps:
- The IAM Role for Lambda has been successfully created.
- Lambda has permissions to write logs to CloudWatch via AWSLambdaBasicExecutionRole.
- The webquiz-dev-lambda-role is ready to be attached to Lambda functions in the project.
- The custom Event Bus webquiz-dev-game-events has been created in Amazon EventBridge.
- The system has the foundation to handle internal events and support asynchronous workflows.

## Role in the SyncQuiz Project

In the SyncQuiz project, the IAM Role is used to grant secure access permissions to Lambda instead of using AWS account credentials directly. EventBridge handles event routing in the system, allowing backend components such as Lambdas that process game logic, save results, or update state to run asynchronously, decoupled, and in a highly scalable manner.
