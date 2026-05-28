# W7 Capstone — Evidence Pack

> **Project:** BudgetBot — AI Money Coach
> **Group:** G2
> **Domain:** B — FinTech ("AI Money Coach")
> **Region:** `ap-southeast-1` (Singapore)
> **Hard cap:** $100 / group
> **Optional capability chosen:** `<#8 Full Observability | #9 Advanced Cost Insights | #10 Advanced Security>`
> **Bonus path(s) attempted (if any):** `<A–H or "none">`

> **How to use this file:** Fill every `<...>` placeholder. Delete the `> NOTE:` helper lines before submitting. Take screenshots DURING the build (timestamps prove credibility — see Common Mistake #6). 2 strong §6.5 decision blocks beat 6 weak ones.

---

## 1. Cover


| Field                             | Value                                                     |
| --------------------------------- | --------------------------------------------------------- |
| Group number                      | G2                                                        |
| Project name                      | BudgetBot — AI Money Coach                                |
| Domain                            | FinTech                                                   |
| AWS region                        | `ap-southeast-1`                                          |
| **Live public URL (HTTPS)**       | `<https://xxxx.cloudfront.net>`                           |
| API base URL                      | https://nvtank.dev                                        |
| GitHub repository                 | https://github.com/tuu-ngo/BudgetBot-AWS                  |
| Demo video                        | `docs/demo.mp4` or `<YouTube unlisted link>`              |
| Slides                            | `docs/slides.pdf`                                         |
| Optional capability               | #8 and #10                                                |
| **Total spend (Friday pre-demo)** | `$<X.XX>`                                                 |
| Test account                      | `username: <demo>` / `password: <demo123>`                |


### Team Members


| Name                    | Student ID  | Owned capabilities (Wed) |
| ----------------------- | ----------- | ------------------------ |
| Ngo Huu Tai             | XB-DN26-008 | Userstory Analyze, AWS Architecture Design, Backend Lambda Development, Database Integration, CICD pipeline(demo), Cost Optimization, Team Leadership, Documentation     |
| Mai Phuoc Khoa          | XB-DN26-033 | Frontend Development , MFA account Setup, Budget Setup, Anomality Cost Setup, Tag Attach                  |
| Nguyen Tien Hoang Thinh | XB-DN26-047 | `<...>`                  |
| Dang Thi Ngoc Thao      | XB-DN26-055 | `<...>`                  |
| Nguyen Phu Trieu        | XB-DN26-070 | `<...>`                  |
| Nguyen Hung Thinh       | XB-DN26-077 | `<...>`                  |
| Huynh Ba Huan           | XB-DN26-106 | `<...>`                  |
| Nguyen Van Tuan Anh     | XB-DN26-112 | `<...>`                  |
| Le Hoang Viet           | XB-DN26-134 | `<...>`                  |
| Hoang Cong Tri Dung     | XB-DN26-148 | `<...>`                  |



**Landing Page Via HTTPS**

![Landing page](image.png)


**Pre-demo Cost**

![Pre-demo cost](image-2.png)


---

## 2. Domain + Use Case + Market

- **Domain:** FinTech — "AI Money Coach"
- **Core AI flow:** Upload bank statement (PDF/CSV) → AI categorizes transactions → spending insights → show list of categorized transactions → answer budget questions.
- **Problem statement (2–3 sentences):** Many individuals and small business owners do not clearly know where their money goes each month because bank statements are difficult to read and analyze manually. Manually categorizing transactions is time-consuming, repetitive, and error-prone, especially when users need to track spending across food, transport, subscriptions, bills, and business expenses. This project solves that problem by using AI to automatically analyze bank statements and provide clear financial insights.
- **Target users:** Individuals managing personal budgets, students tracking monthly expenses, freelancers, and small business owners who need to understand their spending patterns and control their budget more effectively.
- **Core user stories:**
-  Upload bank statement:
As a user, I can upload a 3-month bank statement in PDF or CSV format, so that the system can extract my transactions and generate a categorized spending breakdown such as Food, Transport, Subscriptions, Bills, Shopping, and Unclassified.
- Ask budget questions:
As a user, I can ask questions such as “How much did I spend on food last month?”, so that the AI can return a specific answer with total amount, transaction dates, merchants, and related line items.
- Receive budget recommendation:
As a user, I can receive budget recommendations based on my spending pattern, so that I can set a monthly savings target and reduce unnecessary expenses.
- Track category spending:
As a user, I can view spending by category, so that I can quickly identify which areas take the largest part of my monthly budget.
- Set budget limits:
As a user, I can set a monthly spending cap for a category, so that the system can alert me when my spending is close to or above the limit.


- **Why AI / why this matters:** AI is important because transaction descriptions in bank statements are often inconsistent, unclear, or difficult for users to classify manually. AI can automatically recognize spending patterns, classify merchants into categories, summarize financial behavior, and answer natural-language questions about the user’s budget. This makes personal finance management faster, easier, and more accessible for users who do not want to manually review every transaction.


- **Named real-world parallel:** Similar real-world products include Cake AI by VPBank, YNAB, Money Lover, Spendee, Monzo spending insights, and Revolut spending analytics. These platforms help users understand their spending behavior, categorize expenses, and make better financial decisions.


- **Dataset provenance:** The project uses synthetic bank statements and anonymized sample transaction data for development and testing. The dataset is designed to simulate realistic bank statement records, including transaction date, transaction ID, merchant or brand name, transaction description, category, and amount. No real user financial data is required for the demo unless it is anonymized before upload.

- **Data privacy note:** Financial data is treated as sensitive information. Uploaded statements are scoped per user, and each user can only access their own uploaded transactions. Sensitive data should be protected through secure storage, encrypted communication, environment-based database credentials, and restricted backend access. For production, uploaded files and extracted transaction data should be encrypted at rest and in transit, and personally identifiable financial information should be minimized or anonymized where possible.

**Screenshots:** `docs/screenshots/06-upload-success.png`,

**Upload AI processing**
![upload AI](image-1.png)


**Upload successfully with budget alarm trigger after upload**
![upload success](image-3.png)

**Dashboard Summary**
![dashboard](image-4.png)
![dashboard2](image-5.png)

**Transactions List with Filter**
![transactions](image-6.png)

**AI Chat Answers**
![ai chat](image-7.png)

 `docs/screenshots/08-dashboard-summary.png`, `docs/screenshots/09-chat-answer.png`

---

## 3. Architecture

### 3.1 Final deployed diagram

Final architecture

> NOTE: diagram MUST reflect what is actually deployed, not the Wednesday draft.

### 3.2 Service decision table (7 mandatory capabilities)


| #   | Capability               | Service chosen                                | Why this service (1 line)                  | Alternative rejected + why                                                   |
| --- | ------------------------ | --------------------------------------------- | ------------------------------------------ | ---------------------------------------------------------------------------- |
| 1   | User-Facing Entry (edge) | `<CloudFront + S3 / API Gateway>`             | `<...>`                                    | `<...>`                                                                      |
| 2   | Application Compute      | `<Lambda>`                                    | `<...>`                                    | `<...>`                                                                      |
| 3   | AI / ML Feature          | `<Bedrock InvokeModel — Claude Haiku>`        | `<...>`                                    | `<KB+Agent — rejected because one-shot classification, no retrieval needed>` |
| 4   | Data Persistence         | `<RDS PostgreSQL db.t3.micro / DynamoDB>`     | `<SQL aggregation for spending summaries>` | `<DynamoDB — no multi-attr aggregation w/o scan>`                            |
| 5   | Object Storage           | `<S3 upload bucket>`                          | `<...>`                                    | `<...>`                                                                      |
| 6   | Network Foundation       | `<VPC + private subnets + SG>`                | `<...>`                                    | `<...>`                                                                      |
| 7   | Identity & Access        | `<IAM roles + hardcoded test user / Cognito>` | `<...>`                                    | `<...>`                                                                      |


### 3.3 Three trade-off justifications

1. `<Trade-off 1 — e.g. Single-AZ RDS over Multi-AZ: saved ~$1.73, accepted no failover for 48h demo.>`
2. `<Trade-off 2>`
3. `<Trade-off 3>`

**Screenshots:** `docs/screenshots/05-live-url-home.png`, `docs/screenshots/10-s3-upload-object.png`, `docs/screenshots/11-rds-private-subnet.png`, `docs/screenshots/17-vpc-endpoints.png`

---

## 4. Mandatory Capabilities — Trainer Verification Evidence

> NOTE: One subsection per capability. Each must be demonstrable live from a phone hotspot.

### #1 — Public URL (HTTPS)

- URL: `<...>` — loads, no SSL errors.
- Screenshot: `docs/screenshots/05-live-url-home.png`

### #2 — Application Compute (backend processes a request)

- Flow: `<API Gateway → Lambda → response>`
- Screenshot: `docs/screenshots/api-gateway-routes.png`, `docs/screenshots/lambda-functions.png`

### #3 — AI / ML Feature (real Bedrock invocation)

- Model: `<Claude Haiku>` | Result visible in UI (not hardcoded).
- Screenshot: `docs/screenshots/07-ai-classification-result.png`, `docs/screenshots/14-lambda-cloudwatch-log-bedrock.png`

### #4 — Data Persistence (write Thu → read Fri)

- `<Describe the test record written Thursday, re-read in fresh Friday session.>`
- Screenshot: `docs/screenshots/12-rds-transactions-after-reload.png`

### #5 — Object Storage (S3, Block Public Access ON)

- Bucket: `<name>` | Versioning: `<on>` | Block Public Access: `<on>`
- Screenshot: `docs/screenshots/10-s3-upload-object.png`, `docs/screenshots/s3-block-public-access.png`

### #6 — Network Foundation (DB private, SG scoped)

- DB in private subnet; SG inbound references compute SG, NOT `0.0.0.0/0`.
- Screenshot: `docs/screenshots/11-rds-private-subnet.png`, `docs/screenshots/16-security-group-rds-inbound.png`

### #7 — IAM least-privilege (named actions, no `*`)

- Lambda execution role: `<role name>` — named actions on specific ARNs.
- Screenshot: `docs/screenshots/15-iam-lambda-role-policy.png`

---

## 5. Security

- **IAM role list** (every compute role + scope):


| Role                     | Attached to        | Allowed actions (named, no wildcard)                      |
| ------------------------ | ------------------ | --------------------------------------------------------- |
| `<budgetbot-api-role>`   | `<API Lambda>`     | `<bedrock:InvokeModel, rds-db:connect, s3:GetObject ...>` |
| `<budgetbot-parse-role>` | `<Parsing Lambda>` | `<...>`                                                   |


- **KMS key ARN (if CMK used):** `<arn:aws:kms:...>`
- **MFA on root:** `<confirmed — screenshot>`
- **Secrets handling:** `<Secrets Manager / Parameter Store — DB creds, no keys in code>`

**Screenshots:** `docs/screenshots/00-preflight-mfa-enabled.png`, `docs/screenshots/15-iam-lambda-role-policy.png`, `docs/screenshots/16-security-group-rds-inbound.png`

---

## 6. Monitoring

- **CloudWatch dashboard:** `<widgets included>`
- **Alarm config:** `<metric, threshold, current state — must be OK or ALARM, not INSUFFICIENT_DATA>`
- **Log Insights query (saved):**

```
fields @timestamp, @message
| filter @message like /ERROR/
| sort @timestamp desc
| limit 50
```

**Screenshots:** `docs/screenshots/18-cloudwatch-dashboard.png`, `docs/screenshots/19-cloudwatch-alarm-ok.png`, `docs/screenshots/20-log-insights-query-result.png`

---

## 6.5 Measurement & Decisions ★ (REQUIRED — anti-đối phó)

> NOTE: Minimum 2 blocks. Vague text = 0 for the block. Need: 2+ alternatives, a real NUMBER, an evidence link, a named trade-off. Pick decisions that MATTERED (model choice, DB choice, chunking, threshold) — NOT "Python vs Node".

### DECISION 1 — `<AI model + classification strategy>`

```
DECISION: <e.g. Bedrock Claude Haiku for transaction classification, few-shot prompt with 8 examples>

ALTERNATIVES CONSIDERED:
- <Claude Sonnet> — eliminated because: <~15x cost ($3/$15 vs $0.25/$1.25 per 1M tok); accuracy gain only +<X>% on our 30 labeled rows>
- <Bedrock zero-shot> — eliminated because: <<Y>% accuracy on cryptic codes (e.g. "FT0024...") vs <Z>% few-shot>

MEASUREMENT:
- Classification accuracy = <NN>% on <30> labeled rows — measured via confusion matrix
- Cost per 1000 classifications = $<0.XX> — measured from token counts in CloudWatch logs

EVIDENCE:
- docs/evaluation/classification_eval.csv
- docs/screenshots/14-lambda-cloudwatch-log-bedrock.png

TRADE-OFF ACCEPTED:
- <Few-shot prompt grows context → +<N> input tokens/call (~$<0.XX>/1K extra); accepted for accuracy.>
```

### DECISION 2 — `<RDS PostgreSQL vs DynamoDB>`

```
DECISION: <RDS PostgreSQL db.t3.micro single-AZ for transaction storage>

ALTERNATIVES CONSIDERED:
- <DynamoDB> — eliminated because: <spending summary needs GROUP BY category + SUM; DynamoDB requires full Scan, <X>ms vs <Y>ms SQL>
- <Aurora Serverless> — eliminated because: <min ACU cost > db.t3.micro for 48h; ~$<X> vs $<Y>>

MEASUREMENT:
- Summary query latency = <NN> ms on <2000> rows — measured in <psql / Lambda log>
- DB cost over 48h = $<X.XX> — measured from Cost Explorer

EVIDENCE:
- docs/screenshots/rds-query-summary.png
- docs/screenshots/12-rds-transactions-after-reload.png

TRADE-OFF ACCEPTED:
- <Single-AZ = no failover; accepted for 48h hackathon (saved $<X>).>
```

> NOTE: Add DECISION 3+ optionally (e.g. async S3+SQS parsing, No-NAT/VPC endpoints, duplicate handling). 2 strong > 6 weak.

---

## 7. Cost Discipline

### Pre-flight safety

- MFA on root — `docs/screenshots/00-preflight-mfa-enabled.png`
- Budget alert @ $80 + SNS email **confirmed** — `docs/screenshots/01-budget-alert-80-confirmed.png`
- Cost Anomaly Detection enabled — `docs/screenshots/02-cost-anomaly-enabled.png`
- Tags applied (`Project=W7Capstone`, `Team=G2`, `Owner=<name>`, `Environment=hackathon`) — `docs/screenshots/04-resource-tags-example.png`
- Bedrock model access granted — `docs/screenshots/03-bedrock-model-access.png`

### Three required cost screenshots


| When            | Screenshot                                    | Total spend |
| --------------- | --------------------------------------------- | ----------- |
| Day 1 EOD (Wed) | `docs/screenshots/21-cost-day1-eod.png`       | $`<X.XX>`   |
| Day 2 EOD (Thu) | `docs/screenshots/22-cost-day2-eod.png`       | $`<X.XX>`   |
| Friday pre-demo | `docs/screenshots/23-cost-friday-predemo.png` | $`<X.XX>`   |


### Top-3 cost drivers

1. `<Service — $X.XX — why>`
2. `<Service — $X.XX — why>`
3. `<Service — $X.XX — why>`

### Cost-per-feature

- `<e.g. each Haiku classification ≈ $0.0001; 2000 categorizations ≈ $0.20 in tokens.>`

### Cost risks avoided

- `<No NAT Gateway (used VPC endpoints) — saved ~$1.50/day; Single-AZ RDS; one CMK max; etc.>`

### Final spend vs $100 cap

- **Total: $`<X.XX>` of $100** → tier: `<under $30 / $30–60 / $60–100>`

---

## 8. Teardown Plan

> NOTE: Final deliverable Mon 2/6 = `docs/teardown_confirmed.png` (near-zero Cost Explorer).


| Order | Resource                                             | Owner    | Done |
| ----- | ---------------------------------------------------- | -------- | ---- |
| 1     | CloudFormation stacks (if IaC)                       | `<name>` | [ ]  |
| 2     | Lambda functions                                     | `<name>` | [ ]  |
| 3     | API Gateway                                          | `<name>` | [ ]  |
| 4     | Bedrock Agent / KB (if used)                         | `<name>` | [ ]  |
| 5     | RDS instances                                        | `<name>` | [ ]  |
| 6     | Empty S3 buckets                                     | `<name>` | [ ]  |
| 7     | Delete S3 buckets                                    | `<name>` | [ ]  |
| 8     | Cognito User Pool (if used)                          | `<name>` | [ ]  |
| 9     | KMS CMK (schedule deletion, 7-day)                   | `<name>` | [ ]  |
| 10    | CloudWatch dashboards/alarms/logs                    | `<name>` | [ ]  |
| 11    | VPC (subnets → SGs → NAT → IGW → route tables → VPC) | `<name>` | [ ]  |
| 12    | Verify Cost Explorer near-zero (Mon 2/6)             | `<name>` | [ ]  |


**Screenshots:** `docs/screenshots/27-teardown-before.png`, `docs/teardown_confirmed.png`

---

## Appendix — Demo & Lessons (not graded sections, helps prep)

### Demo

- Test account: `<username/password>`
- Sample input: `docs/sample_input/<file>`
- 3-min script: `docs/demo-script.md` | Backup video: `docs/demo.mp4`

### Lessons learned (≤200 words)

`<What went well, what you'd do differently, what surprised you. Reference the Cake AI parallel + one concrete failure case (e.g. "FT0024..." opaque codes → escalated to review queue at confidence < 0.6).>`

### Known limitations

- `<CSV has no transaction ID/timestamp; synthetic data; classifier misclassifies ambiguous merchants (GRAB → Transport vs GrabFood); simplified auth.>`