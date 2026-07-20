---
title: "Week 9 Worklog"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---
### Week 9 Objectives:
* Enforce Role-Based Access Control (RBAC) via Cognito Groups and handle automatic Refresh Token cycles.
* Build a comprehensive Frontend Scoring Dashboard and construct multi-step automated Postman test workflows.

#### Tasks to be deployed this week:
| Day | Tasks | Start Date | End Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - **API Security:** Implement granular RBAC via Cognito Groups (Student submission permissions vs Instructor gradebook access) <br>- Handle automatic Session renewal via Refresh Tokens | 15/06/2026 | 15/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Tue | - **Frontend - API:** Develop Dashboard UI components displaying score history, grade charts, and API response details <br>- Handle HTTP 403 Forbidden UI errors | 16/06/2026 | 16/06/2026 | Project Documentation |
| Wed | - **Basic Scoring:** Optimize scoring algorithms to handle edge cases, multi-attempt submissions, and detailed audit history logging | 17/06/2026 | 17/06/2026 | Project Documentation |
| Thu | - **Postman Test:** Write multi-step automated integration scripts: [Login & Fetch Token] -> [Submit Payload] -> [Invoke Scoring API] -> [Verify Gradebook] | 18/06/2026 | 18/06/2026 | <https://www.postman.com/> |
| Fri | - **Integration:** Perform full end-to-end synchronization tests across Cognito RBAC, Frontend Dashboards, and Scoring Engine calculation outputs <br>- Write Week 9 report | 19/06/2026 | 19/06/2026 | Project Documentation |

#### Week 9 Achieved Results:
* Implemented strict RBAC mechanisms with Cognito Groups and seamless background token refreshes.
* Built an interactive Frontend Scoring Dashboard displaying history charts and user-friendly authorization error handling.
* Enhanced Scoring Engine algorithms to support edge case validations and history logging.
* Developed multi-step automated Postman integration flows verifying full application lifecycles.
