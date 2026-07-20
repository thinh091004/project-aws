---
title: "API Gateway - HTTP API"
date: 2024-01-01
weight: 8
pre: " <b> 5.8. </b> "
---

## Setting up Amazon API Gateway HTTP API

Amazon API Gateway HTTP API is used in the SyncQuiz project to build backend APIs serving the React frontend. The HTTP API offers low latency, optimized costs, and is ideal for connecting to AWS Lambda for functionalities such as quiz management, room creation, retrieving user info, and system data processing.

### Step 1: Access Amazon API Gateway

Open the AWS Management Console and access the API Gateway service. On the APIs page, you can view the list of APIs created in your AWS account. To create a new API, click Create API.

![Access API Gateway](/images/5-Workshop/5.8-APIGateway-HTTP/api1.jpg)

### Step 2: Select HTTP API Type

On the Choose an API type page, locate HTTP API and click Build. HTTP APIs are suitable for simple REST APIs, offering low latency and easy integration with Lambda backends.

![Select HTTP API Type](/images/5-Workshop/5.8-APIGateway-HTTP/api2.jpg)

### Step 3: Configure API Information

In the Configure API section, enter the API name as webquiz-dev-http-api. Under IP address type, select IPv4. At this step, you do not need to add integrations immediately, as integrations and routes can be configured after the API is created.

![Configure HTTP API](/images/5-Workshop/5.8-APIGateway-HTTP/api3.jpg)

### Step 4: Skip Initial Routes Configuration

In the Configure routes step, you can skip creating initial routes if you do not have specific Lambda integrations set up yet. Routes will be added later depending on backend features like creating quizzes, getting quizzes, creating rooms, or processing results.

![Configure Routes](/images/5-Workshop/5.8-APIGateway-HTTP/api4.jpg)

### Step 5: Configure Stage

In the Define stages step, enter the stage name as dev and enable Auto-deploy. The dev stage is used for the development environment. When Auto-deploy is enabled, changes in the API will be deployed automatically to this stage.

![Configure Stage dev](/images/5-Workshop/5.8-APIGateway-HTTP/api5.jpg)

### Step 6: Review and Create API

In the Review and create step, verify the API information, Routes, and Stages. If the details are correct, click Create to create the HTTP API.

![Review and Create HTTP API](/images/5-Workshop/5.8-APIGateway-HTTP/api6.jpg)

### Step 7: Verify HTTP API After Creation

After successful creation, API Gateway will display the Routes page of the newly created API. Here, you can continue to create routes, configure authorization, add integrations with Lambda, and deploy the API.

![HTTP API Created Successfully](/images/5-Workshop/5.8-APIGateway-HTTP/api7.jpg)

---

### 2. Configure CORS

To allow frontend requests from different domains or local hosts:

1. Inside your HTTP API detail menu on the left, select **CORS** and click **Configure**.

![Access and configure CORS](/images/workshop/5.8-apigateway/cors1.jpg)

2. Add the following CORS settings:
   * **Access-Control-Allow-Origin:** Enter `*`.
   * **Access-Control-Allow-Headers:** Enter `Content-Type, Authorization`.
   * **Access-Control-Allow-Methods:** Enter `GET, POST, PUT, DELETE, OPTIONS`.
   * **Access-Control-Max-Age:** Enter `300`.

![Enter CORS configuration settings](/images/workshop/5.8-apigateway/cors2.jpg)

3. Click **Save** to complete the configuration.

![CORS configuration saved successfully](/images/workshop/5.8-apigateway/cors3.jpg)

---

### 3. Create Cognito JWT Authorizer

1. Select **Authorization** on the left menu.
2. Under the **Manage authorizers** tab, click **Create**.
3. Configure the Authorizer:
   * **Authorizer type:** Select **JWT**.
   * **Name:** Enter CognitoAuthorizer.
   * **Identity source:** Enter `$request.header.Authorization`.
   * **Issuer URL:** Enter `https://cognito-idp.us-east-1.amazonaws.com/YOUR_USER_POOL_ID` (replace `YOUR_USER_POOL_ID` with the actual User Pool ID from Step 3).
   * **Audience:** Enter the **App Client ID** (copied from Step 3).
   * Click **Create**.

---

### 4. Create Integrations

Connect the HTTP API Gateway to the backend Lambda functions:

1. Select **Integrations** on the left menu.
2. Click **Create** for two integrations:
   * **Integration 1 (Quiz CRUD):**
     * **Integration target:** Select **Lambda function**.
     * **Lambda function:** Select webquiz-dev-quiz-crud.
     * Click **Create**.
   * **Integration 2 (Room Management):**
     * Click **Create**.
     * **Integration target:** Select **Lambda function**.
     * **Lambda function:** Select webquiz-dev-room-management.
     * Click **Create**.

---

### 5. Create Routes & Attach Permissions

Now, map the API paths, attach their integrations, and configure authorization:

1. Select **Routes** on the left menu.
2. Create and configure the following 5 routes:

| Route | Method | Path | Integration Target | Authorizer Type |
| :--- | :--- | :--- | :--- | :--- |
| **Route 1** | `ANY` | `/quizzes` | webquiz-dev-quiz-crud | CognitoAuthorizer |
| **Route 2** | `ANY` | `/quizzes/{proxy+}` | webquiz-dev-quiz-crud | CognitoAuthorizer |
| **Route 3** | `POST` | `/rooms` | webquiz-dev-room-management | CognitoAuthorizer |
| **Route 4** | `GET` | `/rooms/{pin}` | webquiz-dev-room-management | **None** (Public) |
| **Route 5** | `POST` | `/rooms/{pin}/join` | webquiz-dev-room-management | **None** (Public) |

*How to configure a route:*
1. Click **Create** and enter the **Method** and **Path**.
2. Click on the route you just created → Click **Attach integration** and select the correct target function.
3. Click **Attach authorizer** (if applicable) and select CognitoAuthorizer.

---

### 6. Record the REST Endpoint URL

1. Go to **Stages** on the left menu.
2. Click on the stage named **`dev`**.
3. Copy and save the **Invoke URL**:
   ```
   https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/dev
   ```
   *(You will need this REST endpoint URL for frontend configuration).*

## Expected Outcomes

After completing the steps:
- The HTTP API webquiz-dev-http-api has been successfully created.
- The Stage dev has been configured with Auto-deploy.
- The API Gateway is ready to add routes and integrations.
- The system has the foundation to allow the React frontend to call the backend via the HTTP API.
- Lambda functions can be integrated into the API Gateway in the subsequent steps.

## Role in the SyncQuiz Project

In the SyncQuiz project, the HTTP API acts as the gateway between the React frontend and the serverless backend. When users interact with the system, the frontend sends requests to API Gateway. API Gateway then forwards the request to the corresponding Lambda function to handle business logic such as creating a quiz, fetching a quiz list, creating a game room, or saving results.
