---
title: "Week 8 Worklog"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---
### Week 8 Objectives:
* Mandate Cognito Token propagation within Request Headers from Frontend to API Gateway.
* Develop basic scoring engine handlers using AWS Lambda and construct automated Postman assertion scripts.

#### Tasks to be deployed this week:
| Day | Tasks | Start Date | End Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - **API Security:** Configure API Gateway to decode Cognito JWT Tokens in `Authorization: Bearer <token>` headers to extract User ID context | 08/06/2026 | 08/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Tue | - **Frontend - API:** Configure Axios/Fetch Interceptors on Frontend to automatically inject Cognito Tokens into every outgoing API Gateway request header | 09/06/2026 | 09/06/2026 | Project Documentation |
| Wed | - **Basic Scoring:** Develop AWS Lambda Functions to execute core scoring logic (receive submission payload -> calculate grade -> persist result in DB) | 10/06/2026 | 10/06/2026 | Project Documentation |
| Thu | - **Postman Test:** Construct assertion scripts for Scoring APIs: Validate Status Code 200, Response Body Schemas, and grading accuracy | 11/06/2026 | 11/06/2026 | <https://www.postman.com/> |
| Fri | - **Integration:** Connect Scoring APIs to Frontend submission forms; execute full integration tests from UI -> API Gateway -> Lambda -> DB <br>- Write Week 8 report | 12/06/2026 | 12/06/2026 | Project Documentation |

#### Week 8 Achieved Results:
* Standardized secure header transmission from Frontend to API Gateway using `Authorization: Bearer <token>`.
* Successfully deployed AWS Lambda scoring engine to process automated assessment evaluations.
* Connected Frontend forms to submit user assignments and receive real-time score evaluations.
* Created automated Postman tests to validate header configuration errors and payload schemas for Scoring APIs.
