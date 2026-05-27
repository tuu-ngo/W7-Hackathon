# W7 Evidence Pack Outline — BudgetBot / AI Money Coach

> **File path:** `docs/W7_evidence.md`
> **Project:** BudgetBot — AI Money Coach
> **Domain:** FinTech
> **Region:** `ap-southeast-1` Singapore
> **Hard cap:** `$100 / group`
> **Optional capability:** `[Advanced Cost Insights / Full Observability / Advanced Security]`

---

# 0. Evidence Screenshot Checklist

## Required screenshots

* `docs/screenshots/00-preflight-mfa-enabled.png`
* `docs/screenshots/01-budget-alert-80-confirmed.png`
* `docs/screenshots/02-cost-anomaly-enabled.png`
* `docs/screenshots/03-bedrock-model-access.png`
* `docs/screenshots/04-resource-tags-example.png`
* `docs/screenshots/05-live-url-home.png`
* `docs/screenshots/06-upload-success.png`
* `docs/screenshots/07-ai-classification-result.png`
* `docs/screenshots/08-dashboard-summary.png`
* `docs/screenshots/09-chat-answer.png`
* `docs/screenshots/10-s3-upload-object.png`
* `docs/screenshots/11-rds-private-subnet.png`
* `docs/screenshots/12-rds-transactions-after-reload.png`
* `docs/screenshots/13-rds-proxy-status.png`
* `docs/screenshots/14-lambda-cloudwatch-log-bedrock.png`
* `docs/screenshots/15-iam-lambda-role-policy.png`
* `docs/screenshots/16-security-group-rds-inbound.png`
* `docs/screenshots/17-vpc-endpoints.png`
* `docs/screenshots/18-cloudwatch-dashboard.png`
* `docs/screenshots/19-cloudwatch-alarm-ok.png`
* `docs/screenshots/20-log-insights-query-result.png`
* `docs/screenshots/21-cost-day1-eod.png`
* `docs/screenshots/22-cost-day2-eod.png`
* `docs/screenshots/23-cost-friday-predemo.png`
* `docs/screenshots/24-cost-anomaly-monitor.png`
* `docs/screenshots/25-sns-budget-email-alert.png`
* `docs/screenshots/26-review-queue-low-confidence.png`
* `docs/screenshots/27-teardown-before.png`
* `docs/screenshots/28-teardown-after.png`

---

# 1. Cover Page

## Fill in

* Group number: 2
* Team members: 
| Name                    | Student ID  |
| ----------------------- | ----------- |
| Ngo Huu Tai             | XB-DN26-008 |
| Mai Phuoc Khoa          | XB-DN26-033 |
| Nguyen Tien Hoang Thinh | XB-DN26-047 |
| Dang Thi Ngoc Thao      | XB-DN26-055 |
| Nguyen Phu Trieu        | XB-DN26-070 |
| Nguyen Hung Thinh       | XB-DN26-077 |
| Huynh Ba Huan           | XB-DN26-106 |
| Nguyen Van Tuan Anh     | XB-DN26-112 |
| Le Hoang Viet           | XB-DN26-134 |
| Hoang Cong Tri Dung     | XB-DN26-148 |

* Project name
* Domain
* AWS region
* Live public URL
* API base URL
* GitHub repository
* Demo video link/path
* Slides path
* Final total cost
* Optional capability chosen

## Screenshots needed

* `docs/screenshots/05-live-url-home.png`
* `docs/screenshots/23-cost-friday-predemo.png`

---

# 2. Domain and Use Case

## Main headings

* Domain selected: FinTech — AI Money Coach
* Problem statement
* Target users
* Core user stories
* Real-world parallel
* Dataset provenance
* Data privacy note

## Screenshots needed

* `docs/screenshots/06-upload-success.png`
* `docs/screenshots/08-dashboard-summary.png`
* `docs/screenshots/09-chat-answer.png`

---

# 3. Final Architecture

## Main headings

* Final deployed architecture diagram
* Upload and classification flow
* Chat flow
* Budget alert flow
* Resource inventory
* 7 mandatory capabilities mapping

## Screenshots / images needed

* `docs/architecture/final-architecture.png`
* `docs/architecture/data-flow-upload.png`
* `docs/architecture/data-flow-chat.png`
* `docs/screenshots/05-live-url-home.png`
* `docs/screenshots/10-s3-upload-object.png`
* `docs/screenshots/11-rds-private-subnet.png`
* `docs/screenshots/12-rds-transactions-after-reload.png`
* `docs/screenshots/13-rds-proxy-status.png`
* `docs/screenshots/17-vpc-endpoints.png`

---

# 4. Mandatory Capabilities Evidence

## Main headings

* Capability 1: User Interface / Public HTTPS Entry
* Capability 2: Application Compute
* Capability 3: AI / ML Feature
* Capability 4: Data Persistence
* Capability 5: Object Storage
* Capability 6: Network Foundation
* Capability 7: Identity and Access

## Screenshots needed

* `docs/screenshots/05-live-url-home.png`
* `docs/screenshots/api-gateway-routes.png`
* `docs/screenshots/lambda-functions.png`
* `docs/screenshots/14-lambda-cloudwatch-log-bedrock.png`
* `docs/screenshots/12-rds-transactions-after-reload.png`
* `docs/screenshots/10-s3-upload-object.png`
* `docs/screenshots/11-rds-private-subnet.png`
* `docs/screenshots/16-security-group-rds-inbound.png`
* `docs/screenshots/15-iam-lambda-role-policy.png`

---

# 5. Service Decisions and Trade-offs

## Main headings

* Frontend hosting decision
* API entry decision
* Compute decision
* AI model decision
* Database decision
* Storage decision
* Async processing decision
* Network decision
* Cost decision
* 2–3 key trade-offs

## Screenshots needed

* `docs/screenshots/05-live-url-home.png`
* `docs/screenshots/api-gateway-routes.png`
* `docs/screenshots/lambda-functions.png`
* `docs/screenshots/14-lambda-cloudwatch-log-bedrock.png`
* `docs/screenshots/12-rds-transactions-after-reload.png`
* `docs/screenshots/10-s3-upload-object.png`
* `docs/screenshots/sqs-trigger.png`
* `docs/screenshots/17-vpc-endpoints.png`
* `docs/screenshots/23-cost-friday-predemo.png`

---

# 6. AI Classification Evidence

## Main headings

* Bedrock model used
* Prompting strategy
* Categories used
* Confidence score design
* Low-confidence review queue
* Classification evaluation
* Known failure cases

## Screenshots / files needed

* `docs/screenshots/07-ai-classification-result.png`
* `docs/screenshots/14-lambda-cloudwatch-log-bedrock.png`
* `docs/screenshots/26-review-queue-low-confidence.png`
* `docs/evaluation/classification_eval.csv`
* `docs/screenshots/classification-eval-summary.png`

---

# 7. Data Persistence Evidence

## Main headings

* RDS schema summary
* Transactions table
* Import batches table
* Review queue table
* Chat history table, if implemented
* Persistence across sessions
* Duplicate handling strategy

## Screenshots needed

* `docs/screenshots/12-rds-transactions-after-reload.png`
* `docs/screenshots/rds-table-transactions.png`
* `docs/screenshots/rds-table-import-batches.png`
* `docs/screenshots/rds-table-review-queue.png`
* `docs/screenshots/upload-duplicate-skip.png`
* `docs/screenshots/upload-incremental-import.png`
* `docs/screenshots/db-natural-key-occurrence.png`

---

# 8. Object Storage Evidence

## Main headings

* S3 upload bucket
* Raw statement storage
* Bucket prefix strategy
* Block Public Access
* Encryption
* Lifecycle / cleanup note

## Screenshots needed

* `docs/screenshots/10-s3-upload-object.png`
* `docs/screenshots/s3-block-public-access.png`
* `docs/screenshots/s3-encryption.png`
* `docs/screenshots/s3-bucket-policy.png`
* `docs/screenshots/s3-upload-prefix.png`

---

# 9. Network and Security Evidence

## Main headings

* VPC design
* Private subnets
* RDS private access
* Security groups
* VPC endpoints
* No NAT Gateway decision
* IAM least-privilege
* Secrets handling

## Screenshots needed

* `docs/screenshots/11-rds-private-subnet.png`
* `docs/screenshots/16-security-group-rds-inbound.png`
* `docs/screenshots/lambda-vpc-config.png`
* `docs/screenshots/17-vpc-endpoints.png`
* `docs/screenshots/vpc-endpoint-sns.png`
* `docs/screenshots/vpc-endpoint-secrets.png`
* `docs/screenshots/no-nat-gateway.png`
* `docs/screenshots/15-iam-lambda-role-policy.png`
* `docs/screenshots/iam-parsing-role.png`
* `docs/screenshots/iam-chat-role.png`
* `docs/screenshots/iam-budget-role.png`

---

# 10. Monitoring and Observability

## Main headings

* CloudWatch dashboard
* Lambda metrics
* API Gateway metrics
* SQS metrics
* RDS metrics
* Custom application metric
* CloudWatch alarm
* Log Insights query

## Screenshots needed

* `docs/screenshots/18-cloudwatch-dashboard.png`
* `docs/screenshots/19-cloudwatch-alarm-ok.png`
* `docs/screenshots/20-log-insights-query-result.png`
* `docs/screenshots/lambda-metrics.png`
* `docs/screenshots/api-gateway-metrics.png`
* `docs/screenshots/sqs-queue-depth.png`
* `docs/screenshots/rds-cpu-connections.png`
* `docs/screenshots/custom-metric-transactions-classified.png`

---

# 11. Cost Discipline

## Main headings

* Cost safety setup
* Budget alert
* Cost Anomaly Detection
* Cost screenshots
* Top 3 cost drivers
* Cost-per-feature analysis
* Cost risks avoided
* Final spend vs $100 hard cap
* Bonus path H check, if applicable

## Screenshots needed

* `docs/screenshots/01-budget-alert-80-confirmed.png`
* `docs/screenshots/02-cost-anomaly-enabled.png`
* `docs/screenshots/21-cost-day1-eod.png`
* `docs/screenshots/22-cost-day2-eod.png`
* `docs/screenshots/23-cost-friday-predemo.png`
* `docs/screenshots/24-cost-anomaly-monitor.png`
* `docs/screenshots/04-resource-tags-example.png`
* `docs/screenshots/no-nat-gateway.png`
* `docs/screenshots/17-vpc-endpoints.png`

---

# 12. Optional Capability Evidence

## Choose only one section to fill deeply

## 12.1 Option A — Advanced Cost Insights

### Main headings

* 3 Cost Explorer screenshots
* Top 3 cost drivers
* Cost-per-feature analysis
* Cost Anomaly Detection
* Cost optimization decisions

### Screenshots needed

* `docs/screenshots/21-cost-day1-eod.png`
* `docs/screenshots/22-cost-day2-eod.png`
* `docs/screenshots/23-cost-friday-predemo.png`
* `docs/screenshots/24-cost-anomaly-monitor.png`
* `docs/screenshots/01-budget-alert-80-confirmed.png`

## 12.2 Option B — Full Observability

### Main headings

* Dashboard
* Custom metric
* Alarm in OK/ALARM state
* Log Insights query
* Observability result during demo

### Screenshots needed

* `docs/screenshots/18-cloudwatch-dashboard.png`
* `docs/screenshots/19-cloudwatch-alarm-ok.png`
* `docs/screenshots/20-log-insights-query-result.png`
* `docs/screenshots/custom-metric-transactions-classified.png`

## 12.3 Option C — Advanced Security

### Main headings

* Security area selected
* Implementation
* Measurement
* Evidence
* Trade-off

### Screenshots needed

* `docs/screenshots/s3-encryption.png`
* `docs/screenshots/kms-key-rotation.png`
* `docs/screenshots/secrets-manager-secret.png`
* `docs/screenshots/cloudtrail-enabled.png`
* `docs/screenshots/config-rule-result.png`
* `docs/screenshots/vpc-flow-logs.png`
* `docs/screenshots/16-security-group-rds-inbound.png`

---

# 13. Measurement and Decisions

## Main headings

* Decision 1: AI model and classification strategy
* Decision 2: RDS PostgreSQL vs DynamoDB
* Decision 3: Async upload with S3 + SQS + Parsing Lambda
* Decision 4: No NAT Gateway, VPC Endpoints instead
* Decision 5: Duplicate handling with natural_key + occurrence_no

## Evidence files / screenshots needed

* `docs/evaluation/classification_eval.csv`
* `docs/screenshots/14-lambda-cloudwatch-log-bedrock.png`
* `docs/screenshots/26-review-queue-low-confidence.png`
* `docs/screenshots/12-rds-transactions-after-reload.png`
* `docs/screenshots/rds-query-summary.png`
* `docs/screenshots/sqs-trigger.png`
* `docs/screenshots/17-vpc-endpoints.png`
* `docs/screenshots/no-nat-gateway.png`
* `docs/screenshots/upload-duplicate-skip.png`
* `docs/screenshots/upload-incremental-import.png`

---

# 14. Demo Evidence

## Main headings

* Demo script summary
* Demo video
* Live demo flow
* Backup plan if live demo fails
* Test account / test user
* Sample data used

## Screenshots / files needed

* `docs/demo.mp4`
* `docs/demo-script.md`
* `docs/screenshots/05-live-url-home.png`
* `docs/screenshots/06-upload-success.png`
* `docs/screenshots/08-dashboard-summary.png`
* `docs/screenshots/09-chat-answer.png`

---

# 15. Lessons Learned

## Main headings

* What went well
* What failed or surprised us
* What we would do differently
* Real-world comparison
* Main architecture lesson
* Main cost lesson
* Main AI lesson

## Screenshots needed

* Optional. Use screenshots from previous sections if needed.

---

# 16. Known Limitations

## Main headings

* CSV has no transaction ID or timestamp
* Synthetic dataset only
* PDF parsing not fully supported, if applicable
* Classifier can misclassify ambiguous merchants
* Auth may be simplified for hackathon
* Budget alert is basic email only

## Screenshots needed

* `docs/screenshots/26-review-queue-low-confidence.png`
* `docs/screenshots/upload-duplicate-skip.png`
* `docs/screenshots/upload-incremental-import.png`

---

# 17. Teardown Plan and Confirmation

## Main headings

* Teardown owner table
* Teardown order
* Resources to delete
* Commands used, if any
* Post-teardown screenshots
* Final confirmation

## Screenshots needed

* `docs/screenshots/27-teardown-before.png`
* `docs/screenshots/28-teardown-after.png`
* `docs/screenshots/cost-after-teardown.png`
* `docs/screenshots/stack-delete-complete.png`, if using IaC

---

# 18. Final Submission Checklist

## Required artifacts

* Live public HTTPS URL
* GitHub repository
* README setup guide
* Final architecture diagram
* Evidence Pack
* Demo video
* Slides PDF
* Cost screenshots
* Teardown confirmation

## Files to verify

* `README.md`
* `docs/W7_evidence.md`
* `docs/slides.pdf`
* `docs/demo.mp4` or video link
* `docs/architecture/final-architecture.png`
* `docs/teardown_confirmation.md`
