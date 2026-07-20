---
title: "Week 12 Worklog"
date: 2026-07-06
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### WEEK 12: POST-DEPLOYMENT MONITORING, INFRASTRUCTURE MAINTENANCE, PERFORMANCE EVALUATION & LESSONS LEARNED

#### Week 12 Objectives:
* Monitor and ensure the runtime stability of the WebQuiz application in the post-handover production state.
* Evaluate resource utilization metrics across Lambda, API Gateway, and DynamoDB to enforce cost-control optimizations.
* Consolidate overall internship breakthroughs, document key engineering takeaways (Lessons Learned), and officially archive the project.

#### Tasks to be deployed this week:
| Day | Tasks | Start Date | End Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - **System Monitoring:** Leverage Amazon CloudWatch and AWS X-Ray to track real-world traffic metrics post-handover <br>- Inspect error traces and latency spikes across endpoints if any arise | 06/07/2026 | 06/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Tue | - **Infrastructure Optimization:** Re-evaluate standard data ingestion sizes and read/write capacities on Amazon DynamoDB <br>- Trim CloudWatch Log Group retention policies from indefinite to short-term cycles to block hidden bills | 07/07/2026 | 07/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Wed | - **Codebase Maintenance:** Refactor and optimize targeted Lambda handlers based on the feedback and technical notes collected during last week's sign-off demo <br>- Push patched source code versions to backup repositories | 08/07/2026 | 08/07/2026 | Project Documentation |
| Thu | - **Lessons Learned:** Compile a final engineering post-mortem / lessons learned report, documenting architectural bottlenecks faced and their respective resolutions for future project baselines | 09/07/2026 | 09/07/2026 | Internal Documentation |
| Fri | - **Project Archiving:** Revoke all temporary IAM Access Keys and clean up local workstation build caches <br>- Officially sign off on the 12-week internship worklog and collect final performance evaluations | 10/07/2026 | 10/07/2026 | Project Documentation |

#### Week 12 Achieved Results:
* Maintained flawless operational stability for the serverless WebQuiz platform on AWS with zero post-handover defects.
* Successfully reduced cloud resource bills by hardening log retention parameters and fine-tuning DynamoDB table modes.
* Finalized a high-value engineering lessons learned directory highlighting WebSocket channel scaling and event-driven patterns.
* Safely decommissioned legacy credentials and IAM access routes, leaving the production cloud environment fully secure.
