---
title: "Week 7 Worklog"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---
### Week 7 Objectives:
* Provision security infrastructure using Amazon Cognito and integrate Login/Register authentication flows on Frontend.
* Set up Cognito Authorizers on API Gateway, finalize scoring database schemas, and construct initial Postman Collections.

#### Tasks to be deployed this week:
| Day | Tasks | Start Date | End Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - **API Security:** Initialize Amazon Cognito User Pool & App Client; define user attributes (Email, Role, Full Name) <br>- **Postman:** Set up Postman Environment variables (Base URL, Cognito Client ID) for Auth API testing | 01/06/2026 | 01/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Tue | - **API Security:** Set up Cognito Authorizer on API Gateway to validate Token authenticity <br>- **Postman:** Write test scripts for Login/Register APIs and auto-save `id_token` and `access_token` to environment variables | 02/06/2026 | 02/06/2026 | <https://www.postman.com/> |
| Wed | - **Frontend - API:** Configure CORS (Origins, Headers) on API Gateway for Frontend domain access <br>- Integrate AWS Amplify/Cognito SDK into Frontend to build Login pages and fetch Cognito Tokens to Client | 03/06/2026 | 03/06/2026 | Project Documentation |
| Thu | - **Basic Scoring:** Analyze business logic, design scoring algorithms, and define output DB schemas (DynamoDB/RDS) <br>- **Postman:** Create negative test cases sending unauthenticated requests to verify HTTP 401 Unauthorized errors | 04/06/2026 | 04/06/2026 | Project Documentation |
| Fri | - **Integration:** Conduct end-to-end testing for Auth flow: Frontend Login -> Retrieve Token -> API Test Call -> Postman Validation <br>- Write Week 7 report | 05/06/2026 | 05/06/2026 | Project Documentation |

#### Week 7 Achieved Results:
* Successfully provisioned Amazon Cognito User Pool and attached Cognito Authorizers to protect API Gateway endpoints.
* Completed Frontend Login/Register UI components and established successful token retrieval mechanisms on the client.
* Finalized database schemas and logical evaluation criteria for the basic scoring engine.
* Built initial Postman Test Collections with automated Cognito Token capture scripts.