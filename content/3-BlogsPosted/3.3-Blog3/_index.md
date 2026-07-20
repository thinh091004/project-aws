---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
## Real-time Quiz System Infrastructure: 100% Serverless & Event-Driven on AWS
Hello everyone, I'd like to share the architectural design for a Real-time Quiz/Assessment Application – a real-time quiz application built entirely on a Serverless & Event-Driven model on the AWS platform.
For Quiz Apps, the key is the ability to handle traffic spikes when thousands of people simultaneously submit or receive questions, along with the requirement for extremely low latency.
Below is an overview of the main subsystems in the system architecture (details in the attached diagram) CORE COMPONENTS IN THE SYSTEM:

### Edge & Auth Security Layer
* CloudFront + WAF: Protects the system frontend, prevents DDoS attacks, and filters malicious requests.
* S3 Static Hosting & Cognito: Static web interface hosting, combined with Amazon Cognito for managing user authentication and authorization (JWT Token).

### Dual-API Layer
* REST API Gateway + Lambda REST: Handles synchronous RESTful data query tasks (retrieving question sets, viewing exam history, etc.).

* WebSocket API Gateway + Lambda WebSocket: Handles countdown timers, pushes questions in bulk, and updates leaderboards in real time to clients.

## Core Processing & Data Storage Layer
* Private Subnet Compute: AWS Lambda clusters are securely placed in a private subnet to handle business logic, automatically obtaining security credentials from AWS Secrets Manager.

* RDS Proxy + Amazon RDS: RDS Proxy manages the Connection Pool, effectively resolving the DB connection exhaustion issue when thousands of Lambda functions are initialized simultaneously.

* Amazon DynamoDB: High-speed storage (millisecond latency) for dynamic data such as WebSocket Connection IDs and session status.

* S3 Media Storage: Separate storage for multimedia files (images, audio) of the questions.

### Asynchronous Processing & Monitoring Layer

* SQS + Lambda Worker: Traffic smoothing when multiple users submit their answers simultaneously. SQS queues the exams, and Lambda Workers consume the data sequentially for grading, preventing interface crashes.

* Dead Letter Queue (DLQ): Stores error handling messages to ensure users never lose their exam submissions. * CloudWatch + SNS: Monitors all infrastructure metrics in real-time and sends instant alerts via SNS to the Admin when issues are detected.

Thank you for reading.

## ARCHITECTURE ILLUSTRATION
![AWS Systems Manager Architecture](/images/3-BlogPosted/Blog3.PNG)
### Post on AWS Study Group: Blog post link:
https://aws.amazon.com/vi/blogs/compute/building-a-serverless-multiplayer-game-that-scales/