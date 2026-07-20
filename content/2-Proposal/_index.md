---
title: "Proposal"
date: 2026-04-20
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# PROJECT PROPOSAL

## Project Name: SyncQuiz - Real-time Quiz System

---

## 1. Executive Summary

SyncQuiz is a real-time quiz platform that allows hosts to create quizzes, open live rooms, invite players using a room PIN, and run synchronized quiz sessions in real time. Players can join from their devices, submit answers instantly, receive score updates, and view the final leaderboard after the game ends.

The project is designed using a serverless architecture on AWS to reduce infrastructure management, improve scalability, and optimize cost. Core services include Amazon Cognito for authentication, Amazon DynamoDB for data storage, AWS Lambda for backend logic, Amazon API Gateway for HTTP and WebSocket communication, Amazon EventBridge for event-driven processing, Amazon S3 and CloudFront for frontend hosting, and Amazon CloudWatch for monitoring.

The main goal of SyncQuiz is to provide a lightweight, scalable, and cost-efficient platform for interactive learning, classroom activities, online training, workshops, and team engagement sessions.

---

## 2. Problem Statement

### 2.1 What’s the Problem?

Traditional quiz systems often lack real-time interaction and synchronization between the host and participants. In many cases, users have to refresh pages manually, wait for delayed updates, or rely on third-party tools that may be expensive or difficult to customize.

The main problems include:

* Lack of real-time communication between host and players.
* Difficulty managing live quiz rooms and participant states.
* Delayed score calculation and leaderboard updates.
* Limited scalability when many players join at the same time.
* High infrastructure cost if using always-on servers.
* Complicated deployment and maintenance for small teams or student projects.
* Weak monitoring, making it hard to detect errors during live quiz sessions.

### 2.2 The Solution

SyncQuiz solves these problems by using a serverless, event-driven AWS architecture. The frontend is hosted on Amazon S3 and delivered through CloudFront. Users authenticate through Amazon Cognito. Quiz, room, player, connection, game state, and result data are stored in DynamoDB.

The system uses API Gateway HTTP API for normal REST operations such as creating quizzes, creating rooms, and joining rooms. For real-time gameplay, API Gateway WebSocket API is used to maintain live communication between host and players. AWS Lambda handles backend logic such as quiz CRUD, room management, WebSocket connection handling, answer submission, score calculation, and result saving.

EventBridge is used to trigger asynchronous tasks such as calculating scores when a player submits an answer and saving final results when the game ends.

### 2.3 Benefits and Return on Investment

SyncQuiz provides several benefits:

* Real-time gameplay experience for both host and players.
* Serverless architecture reduces operational effort.
* Pay-as-you-go pricing helps minimize cost during low traffic.
* DynamoDB on-demand capacity supports flexible workloads.
* WebSocket API enables instant communication without page refresh.
* EventBridge improves system modularity and separates business logic.
* CloudWatch monitoring helps detect errors, throttling, and performance issues.
* The system can be extended later for classrooms, events, online courses, and corporate training.

Expected return on investment includes lower hosting costs, faster development, easier scaling, and better user engagement compared to traditional server-based quiz platforms.

---

## 3. Solution Architecture

SyncQuiz follows a serverless architecture. The frontend is deployed to Amazon S3 and distributed globally using Amazon CloudFront. Users access the web application through CloudFront. Authentication is handled by Amazon Cognito.

The backend is divided into multiple Lambda functions. HTTP API is used for quiz and room operations, while WebSocket API is used for live game communication. DynamoDB stores all application data, including users, quizzes, questions, rooms, active connections, game state, and final results. EventBridge connects gameplay events to background processing functions such as score calculation and result saving.

### 3.1 AWS Services Used

The project uses the following AWS services:

* **Amazon Cognito**: Handles user authentication and user pool management.
* **Amazon DynamoDB**: Stores users, quizzes, questions, rooms, WebSocket connections, game state, and game results.
* **AWS Lambda**: Runs backend logic without managing servers.
* **Amazon API Gateway - HTTP API**: Provides REST endpoints for quiz and room management.
* **Amazon API Gateway - WebSocket API**: Provides real-time communication between host and players.
* **Amazon EventBridge**: Handles event-driven workflows such as answer submission and game ending.
* **Amazon S3**: Hosts the static frontend application.
* **Amazon CloudFront**: Delivers the frontend globally with HTTPS and caching.
* **AWS IAM**: Manages permissions for Lambda, DynamoDB, EventBridge, and WebSocket management.
* **Amazon CloudWatch**: Provides logs, metrics, alarms, and dashboards for monitoring.
* **AWS WAF**: Optional service for additional web security in production.

### 3.2 Component Design

The system is divided into the following components:

* **Frontend Component**
  A web interface where hosts can create quizzes, start rooms, manage game flow, and view results. Players can join using a room PIN, answer questions, and view score updates.

* **Authentication Component**
  Amazon Cognito manages user sign-up, sign-in, JWT tokens, and protected access for host features such as quiz creation and room creation.

* **Quiz Management Component**
  Lambda function handles quiz CRUD operations, including creating quizzes, listing quizzes, viewing quiz details, updating quizzes, and adding questions.

* **Room Management Component**
  Lambda function handles room creation, room lookup, and player joining. Each room has a unique PIN and stores status such as waiting, playing, or finished.

* **Real-time WebSocket Component**
  WebSocket API handles live actions such as connecting, disconnecting, starting the game, moving to the next question, submitting answers, and ending the game.

* **Score Calculation Component**
  When a player submits an answer, EventBridge triggers a Lambda function to calculate score based on correctness, remaining time, and answer streak.

* **Result Saving Component**
  When the game ends, EventBridge triggers a Lambda function to save final player results and rankings into DynamoDB.

* **Monitoring Component**
  CloudWatch tracks Lambda errors, API activity, WebSocket messages, DynamoDB throttling, and overall application performance.

---

## 4. Technical Implementation

The technical implementation of SyncQuiz includes the following steps:

1. **Set up Cognito Authentication**
   * Create a Cognito User Pool.
   * Configure email-based sign-in.
   * Create an application client for the web frontend.
   * Use JWT tokens to protect host APIs.

2. **Create DynamoDB Tables**
   * webquiz-dev-users for user data.
   * webquiz-dev-quizzes for quiz metadata.
   * webquiz-dev-questions for quiz questions.
   * webquiz-dev-rooms for live room information.
   * webquiz-dev-connections for active WebSocket connections.
   * webquiz-dev-game-state for live game state, players, answers, and scores.
   * webquiz-dev-game-results for final results.

3. **Configure IAM Role and Policies**
   * Create Lambda execution role.
   * Attach CloudWatch logging permission.
   * Add custom policy for DynamoDB, EventBridge, and WebSocket connection management.

4. **Develop Lambda Functions**
   * webquiz-dev-quiz-crud: Handles quiz and question operations.
   * webquiz-dev-room-management: Handles room creation and player joining.
   * webquiz-dev-ws-connect: Stores WebSocket connection information.
   * webquiz-dev-ws-disconnect: Removes disconnected clients.
   * webquiz-dev-ws-message: Processes real-time game messages.
   * webquiz-dev-score-calculator: Calculates score after answer submission.
   * webquiz-dev-game-results-saver: Saves final game results.

5. **Create API Gateway HTTP API**
   * Configure routes for quiz and room operations.
   * Attach Lambda integrations.
   * Configure Cognito JWT Authorizer for protected routes.
   * Enable CORS for frontend communication.

6. **Create API Gateway WebSocket API**
   * Configure $connect, $disconnect, and $default routes.
   * Connect routes to corresponding Lambda functions.
   * Use WebSocket actions such as START_GAME, NEXT_QUESTION, SUBMIT_ANSWER, and END_GAME.

7. **Configure EventBridge**
   * Create custom event bus.
   * Create rule for AnswerSubmitted event to trigger score calculation.
   * Create rule for GameEnded event to trigger final result saving.

8. **Deploy Frontend**
   * Upload frontend build files to Amazon S3.
   * Configure CloudFront distribution.
   * Use Origin Access Control to secure S3 access.
   * Configure custom error responses for single-page application routing.

9. **Set up Monitoring**
   * Create CloudWatch alarms for Lambda errors.
   * Create alarms for DynamoDB throttling.
   * Build CloudWatch dashboard for Lambda, API Gateway, WebSocket, and DynamoDB metrics.

10. **Testing**
    * Test quiz creation using HTTP API.
    * Test room creation and joining.
    * Test WebSocket connection using tools such as wscat.
    * Test answer submission, score update, game ending, and leaderboard display.

---

## 5. Timeline & Milestones

| Week | Milestone | Main Tasks |
| --- | --- | --- |
| Week 1 | Project Planning & AWS Setup | Define project scope, review architecture, create AWS account, configure AWS CLI, prepare IAM access. |
| Week 2 | Authentication & Database Design | Set up Cognito User Pool, design DynamoDB tables, create users, quizzes, questions, rooms, connections, game state, and results tables. |
| Week 3 | Backend Foundation | Create IAM role, configure Lambda permissions, implement quiz CRUD and room management Lambda functions. |
| Week 4 | HTTP API Development | Create API Gateway HTTP API, configure routes, attach Lambda integrations, add Cognito JWT Authorizer, test quiz and room APIs. |
| Week 5 | WebSocket Real-time System | Create WebSocket API, implement connect/disconnect/message handlers, test host and player live communication. |
| Week 6 | Event-driven Game Logic | Configure EventBridge, implement answer submission workflow, score calculator, result saver, and leaderboard logic. |
| Week 7 | Frontend Deployment | Build frontend application, deploy to S3, configure CloudFront, connect frontend with HTTP and WebSocket APIs. |
| Week 8 | Monitoring, Testing & Optimization | Create CloudWatch alarms and dashboard, perform end-to-end testing, optimize cost, fix bugs, finalize documentation. |

---

## 6. Budget Estimation

The operating cost of SyncQuiz is estimated based on a serverless architecture and static frontend hosting on AWS. The React frontend is deployed to Amazon S3 and delivered through Amazon CloudFront. The backend uses AWS Lambda, Amazon API Gateway, Amazon Cognito, Amazon DynamoDB, Amazon EventBridge, and Amazon CloudWatch.

The following table provides a monthly cost estimation for a development or workshop environment with low to moderate traffic.

| No. | AWS Service | Configuration / Usage Assumption | Estimated Cost / Month |
|---|---|---|---|
| 1 | AWS Lambda | Around 1 million requests/month, 256MB memory, average execution time of 1 second | ~ $5.00 |
| 2 | Amazon DynamoDB | On-demand mode for storing quizzes, game rooms, players, and results | ~ $10.00 |
| 3 | Amazon API Gateway | HTTP API for backend services and WebSocket API for real-time quiz features | ~ $5.00 |
| 4 | Amazon Cognito | User registration, login, authentication, and session management | ~ $0.00 - $5.00 |
| 5 | Amazon S3 | Hosting static files of the production React frontend build | ~ $0.50 |
| 6 | Amazon CloudFront | CDN distribution and caching for the static frontend website | ~ $5.00 |
| 7 | Amazon EventBridge | Internal event routing and asynchronous workflow support | ~ $1.00 |
| 8 | Amazon CloudWatch | Logs, metrics, dashboards, and system monitoring | ~ $3.00 |
| Total | Estimated monthly cost | Development/workshop environment | ~ $29.50 - $34.50 |

### 6.1 Infrastructure Costs

With a serverless architecture, the infrastructure cost of SyncQuiz depends directly on the number of users, quizzes created, real-time game rooms, and API requests. In a development or workshop environment, the system can benefit from the AWS Free Tier for several services such as Lambda, S3, CloudFront, DynamoDB, and Cognito.

To optimize infrastructure costs, the system applies the following approaches:

- Use AWS Lambda to avoid maintaining always-on servers.
- Use DynamoDB On-demand mode to pay based on actual request usage.
- Host the React frontend on Amazon S3 instead of using a dedicated web server.
- Deliver static content through CloudFront to reduce direct requests to S3.
- Monitor logs and metrics with CloudWatch while limiting log retention when needed.
- Use CloudFront caching to reduce origin requests.
- Configure AWS Budgets alerts to prevent unexpected cloud spending.

Overall, the initial operating cost of SyncQuiz remains relatively low because the system does not require a server running 24/7. As the number of users grows, the cost can scale according to actual usage.

---

## 7. Risk Assessment

### 7.1 Risk Matrix

| Risk | Probability | Impact | Level |
| --- | --- | --- | --- |
| WebSocket disconnection during live quiz | Medium | High | High |
| DynamoDB throttling during many simultaneous players | Medium | Medium | Medium |
| Lambda timeout during broadcast to many connections | Medium | High | High |
| Incorrect score calculation logic | Low | High | Medium |
| Cognito configuration error blocks host login | Medium | Medium | Medium |
| API Gateway route or authorizer misconfiguration | Medium | Medium | Medium |
| CloudFront/S3 deployment issue causes frontend access error | Low | Medium | Low |
| CloudWatch cost increases due to excessive logs | Medium | Low | Low |
| Security risk from overly broad IAM permissions | Medium | High | High |

### 7.2 Mitigation Strategies

* Use DynamoDB TTL to automatically remove expired rooms, connections, and game states.
* Clean up disconnected WebSocket clients when API Gateway returns stale connection errors.
* Keep Lambda functions small and focused by separating quiz, room, WebSocket, scoring, and result logic.
* Use EventBridge to separate real-time message handling from asynchronous score calculation.
* Apply least privilege permissions in IAM policies.
* Use Cognito JWT Authorizer for protected host routes.
* Configure CloudWatch alarms for Lambda errors and DynamoDB throttling.
* Test WebSocket flows carefully before live demo or production usage.
* Use CloudFront with Origin Access Control to protect the S3 frontend bucket.
* Keep dev and production environments separated using naming conventions such as dev and prod.

### 7.3 Contingency Plans

* If WebSocket communication fails, users can reconnect using the room PIN and player ID.
* If DynamoDB throttling occurs, review access patterns and optimize indexes or switch to provisioned capacity with auto scaling.
* If Lambda broadcast becomes slow, split broadcasting into smaller batches or use an asynchronous queue-based approach.
* If score calculation fails, store submitted answers first and reprocess them later.
* If Cognito login fails, temporarily test public API endpoints while fixing authorizer configuration.
* If frontend deployment fails on CloudFront, access the latest S3 build internally for debugging.
* If AWS cost increases unexpectedly, review Cost Explorer, reduce log retention, and remove unused resources.

---

## 8. Expected Outcomes

At the end of the project, SyncQuiz is expected to deliver a working real-time quiz platform with the following outcomes:

* Hosts can create and manage quizzes.
* Hosts can create live quiz rooms with room PINs.
* Players can join rooms without authentication.
* Host and players can communicate in real time through WebSocket.
* Players can submit answers instantly.
* Scores are calculated automatically after each answer.
* Leaderboard is updated and final results are saved.
* Frontend is deployed securely through S3 and CloudFront.
* System metrics and errors are monitored through CloudWatch.
* Infrastructure cost remains low through serverless AWS services.

### 8.1 Technical Improvements

The project provides several technical improvements:

* Improved scalability through serverless Lambda and DynamoDB.
* Lower operational overhead because no server management is required.
* Real-time communication using API Gateway WebSocket API.
* Event-driven processing using EventBridge.
* Better security with Cognito authentication and IAM role-based permissions.
* Better frontend delivery using CloudFront CDN.
* Improved observability with CloudWatch metrics, logs, alarms, and dashboards.
* Better data lifecycle management using DynamoDB TTL.
* Modular backend design that separates quiz, room, WebSocket, scoring, and result logic.

### 8.2 Long-term Value

SyncQuiz has strong long-term value because it can be expanded beyond the initial real-time quiz system. Future improvements may include:

* Admin dashboard for managing quizzes and reports.
* Support for multiple quiz modes such as practice mode, competition mode, and exam mode.
* Analytics for player performance and question accuracy.
* Team-based quiz mode.
* Integration with school or training platforms.
* Multi-language support.
* Mobile-friendly interface.
* Production deployment with custom domain, AWS WAF, and stricter security policies.
* CI/CD pipeline for automated deployment.
* Advanced leaderboard and achievement system.

In the long term, SyncQuiz can become a reusable real-time learning and engagement platform for classrooms, workshops, online training, and internal company events.
