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
| Demo video                        | https://drive.google.com/drive/folders/14nKVl-ITeyBxzbwg4mOk88aczTSFO7PR?usp=sharing              |
| Slides                            | https://drive.google.com/drive/folders/1z4Kd6_oglxHVGfM6pCbjQ_ggvmTHaS8G?usp=sharing                                         |
| Optional capability               | #8 and #10                                                |
| **Total spend (Friday pre-demo)** | `$<X.XX>`                                                 |


### Team Members


| Name                    | Student ID  | Owned capabilities (Wed) |
| ----------------------- | ----------- | ------------------------ |
| Ngo Huu Tai             | XB-DN26-008 | Userstory Analyze, AWS Architecture Design, Backend Lambda Development, Database Integration and Deployment, CICD pipeline(demo), Cost Optimization, Team Leadership, Documentation     |
| Mai Phuoc Khoa          | XB-DN26-033 | Frontend Development , MFA account Setup, Budget Setup, Anomality Cost Setup, Tag Attach                  |
| Nguyen Tien Hoang Thinh | XB-DN26-047 | `<...>`                  |
| Dang Thi Ngoc Thao      | XB-DN26-055 | Parsing Lambda Logic, Full Observability Bonus, Database Config and Testing, Userstory Analyze, AWS Architecture Design                |
| Nguyen Phu Trieu        | XB-DN26-070 | `<...>`                  |
| Nguyen Hung Thinh       | XB-DN26-077 | AI Lambda logic and deployment, Userstory Analyze, AWS Architecture Design                  |
| Huynh Ba Huan           | XB-DN26-106 | `<...>`                  |
| Nguyen Van Tuan Anh     | XB-DN26-112 | Frontend Deployment, Cognito Setup, Frontend and Backend Connection, Userstory Analyze, AWS Architecture Design                  |
| Le Hoang Viet           | XB-DN26-134 | Database Config and Testing, Security for AWS Services, IAM Setup                |
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

**Final architecture**

![archi](image-8.png)

**Architecture Flow Description**
- Frontend Flow

The user accesses the web application through CloudFront. CloudFront retrieves static frontend files from the S3 Frontend Bucket using OAC, so the S3 bucket is not publicly accessible.

User → Internet → CloudFront → S3 Frontend Bucket
- Authentication Flow

The user authenticates through Amazon Cognito. After successful login, the frontend receives a JWT token and includes it when calling backend APIs.

User → Frontend → Cognito → JWT Token
- API Flow

The frontend sends requests to API Gateway. API Gateway invokes the Lambda API, which routes requests to specific Lambda functions such as Upload Parsing, Chat, or Budget.

Frontend → API Gateway → Lambda API → Functional Lambdas
- Upload Processing Flow

Bank statement files are uploaded to the S3 Upload Bucket. SQS triggers the asynchronous processing flow. The Upload Parsing Lambda reads the file, parses transaction data, and stores the records in the database.

S3 Upload → SQS → Upload Parsing Lambda → RDS Proxy → RDS PostgreSQL
- Database Flow

Backend Lambda functions access the database through RDS Proxy. RDS Proxy manages connection pooling and reduces direct connection pressure on RDS.

Lambda Functions → RDS Proxy → RDS PostgreSQL
- AI Chat Flow

When the user asks a financial question, Chat Lambda retrieves transaction data from RDS and calls Amazon Bedrock to generate an AI response.

Chat Lambda → RDS PostgreSQL
Chat Lambda → Amazon Bedrock
- Budget Flow

Budget Lambda handles creating, updating, and checking user budget rules. The budget data is stored in PostgreSQL.

Frontend → API Gateway → Lambda API → Budget Lambda → RDS
- Monitoring and Notification Flow

CloudWatch collects logs and metrics from Lambda functions. When an alert condition is met, CloudWatch can send notifications through SNS.

Lambda → CloudWatch → SNS
- Security Flow

- IAM manages service permissions(least privilege principle). Security Groups control private network traffic between Lambda, RDS Proxy, and RDS. KMS supports encryption for sensitive data such as uploaded files, database storage, or queue messages.
IAM → Service permissions
Security Group → Private network control
KMS → Sensitive data encryption

**LAMBDA PARSER PIPELINE**

Asynchronous Data Flow Architecture
To resolve the bottlenecks associated with processing large files and invoking high-latency AI models, the system implements a fully decoupled, asynchronous architecture:

Upload & Trigger: Statement files are uploaded directly by the client to the budgetbot-statements-459983119471 bucket. Upon completion, S3 fires an s3:ObjectCreated:* event notification directly into an Amazon SQS queue.
Decoupling (Shock Absorption): SQS acts as a durable buffer. This ensures the frontend user interface is never blocked waiting for a response, and the Lambda Parser only pulls messages when compute resources are available.

![alt text](image-65.png)

![alt text](image-66.png)

![alt text](image-67.png)

![alt text](image-68.png)

![alt text](image-69.png)

![alt text](image-70.png)

![alt text](image-71.png)

Parsing & Classification Strategy
The Lambda Parser supports multi-format processing using a dual-path routing strategy to optimize both cost and performance:

CSV Path (Deterministic): Utilizes the COLUMN_ALIASES mapping matrix to dynamically resolve inconsistent Vietnamese bank header variations (e.g., "ngày gd", "số tiền", "mã gd").
PDF Path (AI Semantic Extraction): Utilizes pypdf to extract raw text, which is then passed to Amazon Bedrock (converse API) using the Llama 3.1 model. The system applies Few-Shot Prompting to strictly format the AI's output into a standardized JSON array containing time, description, amount, and transaction ID.
AI Cost-Optimization (Dual-Layer): Before invoking the LLM, transactions pass through a KEYWORD_MAPPING pre-filter (e.g., "grab", "shopee"). If a match is found, the category is instantly assigned with a 1.0 confidence score, bypassing expensive LLM execution cycles entirely.

![alt text](image-72.png)

![alt text](image-73.png)

Idempotency & Upsert Logic
To prevent duplicate records and skewed financial budgets caused by users re-uploading the same statements, the system guarantees idempotent database writes:

Natural Key Algorithm: If a native bank transaction ID is missing, the system generates a deterministic hash (_stable_bank_id) using a combination of the row index, description, time, and amount.
PostgreSQL UPSERT: Data is persisted via RDS Proxy using the ON CONFLICT (file_id, bank_id) DO UPDATE command. This ensures that re-uploaded files strictly overwrite modified fields (like review_status) rather than inserting duplicate rows.

![alt text](image-74.png)

![alt text](image-75.png)

![alt text](image-76.png)

### 3.2 Service decision table (7 mandatory capabilities)


| #   | Capability               | Service chosen                                | Why this service (1 line)                  | Alternative rejected + why                                                   |
| --- | ------------------------ | --------------------------------------------- | ------------------------------------------ | ---------------------------------------------------------------------------- |
| 1   | User-Facing Entry (edge) | CloudFront + S3 / API Gateway             | CloudFront provides a public HTTPS entry point for the frontend, S3 stores static web assets at low cost, and API Gateway exposes a managed HTTPS endpoint for Lambda backend requests. This clearly separates the user-facing entry layer from the compute layer.                                    | Application Load Balancer + EC2 — rejected because it requires always-running infrastructure, server maintenance, health checks, and higher baseline cost. For a 48-hour serverless MVP, CloudFront + S3 + API Gateway is simpler, cheaper, and faster to deploy.                                                                      |
| 2   | Application Compute      | AWS Lambda                                    | Lambda runs the backend logic for API routing, upload parsing, budget handling, and AI chat without managing servers. It is suitable for event-driven, low-to-medium traffic MVP workloads and only incurs cost when invoked. We choose multiple Lambda because we want to follow the least-privilege rule for this finance project since it consist of sensitives data.                                    | EC2 / ECS Fargate — rejected because they add server/container orchestration overhead and may run continuously even when there is no traffic. The project only needs request-based execution, not a long-running backend service. 1 Lambda running for backend — rejected because in that case the lambda will have access to multiple role and will break the least-privilege rule.                                                                       |
| 3   | AI / ML Feature          | Amazon Bedrock InvokeModel — Claude Haiku        | Bedrock InvokeModel supports direct AI calls for transaction categorization, spending insights, and budget Q&A. Claude Haiku is selected because it is fast and cost-efficient for short classification and financial explanation prompts.                                    | Bedrock Knowledge Base + Agent — rejected because the FinTech use case mainly requires one-shot transaction classification and question answering over structured transaction data, not retrieval from a large document corpus or multi-step agent workflows. |
| 4   | Data Persistence         | Amazon RDS PostgreSQL db.t3.micro + RDS Proxy     | PostgreSQL supports relational financial data, SQL joins, filtering, and aggregations such as spending by category, month, user, and merchant. RDS Proxy reduces the risk of Lambda opening too many direct database connections. | DynamoDB — rejected because the application needs multi-attribute filtering and aggregation, such as GROUP BY category and monthly spending summaries. DynamoDB would require more complex access patterns or scans for this reporting workload.                            |
| 5   | Object Storage           | Amazon S3 Upload Bucket                          | S3 provides durable, low-cost object storage for uploaded CSV/PDF bank statements before processing. It also decouples file storage from database storage and allows asynchronous parsing through SQS.                                    | Store uploaded files directly in RDS — rejected because bank statement files are unstructured objects. Storing them in the relational database would increase database size, cost, and backup overhead while reducing performance.                                                                      |
| 6   | Network Foundation       | VPC + Private Subnet + Security Groups                | Lambda, RDS Proxy, and RDS PostgreSQL are placed inside a private subnet so the database is not publicly accessible. Security Groups restrict traffic so only the backend compute layer can reach RDS Proxy and RDS.                                    | Public RDS access — rejected because exposing the database to the Internet increases security risk and violates the requirement that the database must not be public-facing. NAT Gateway is also rejected to reduce cost because the project is optimized for a short 48-hour demo.                                                                      |
| 7   | Identity & Access        | IAM roles + Cognito User Pool | IAM roles enforce least-privilege permissions between AWS services, while Cognito provides managed user authentication and JWT-based access for the frontend. This supports both service-level security and user-facing authentication. For a finance project which consist of multible sensitive data, strictly security is required.                                    | Hardcoded test user only — rejected because it is acceptable for a minimal demo but weaker for a SaaS-style application. Cognito gives a more realistic authentication layer without requiring the team to build custom login, password storage, or token management.                                                                      |


### 3.3 Three trade-off justifications

**Trade-off 1 — Single-AZ RDS over Multi-AZ RDS**
We selected Single-AZ RDS PostgreSQL instead of Multi-AZ RDS to reduce cost for the 48-hour hackathon environment. Multi-AZ would improve availability through automatic failover, but it would increase database cost and is not necessary for a short MVP demo. The accepted trade-off is that the database has no automatic cross-AZ failover during the demo period.

**Trade-off 2 — Bedrock InvokeModel over Bedrock Knowledge Base / Agent**
We selected Bedrock InvokeModel with Claude Haiku because the core AI task is transaction categorization and financial insight generation from structured data. The system does not need a full retrieval pipeline or agent orchestration because transaction records are already stored in PostgreSQL and can be queried directly. The accepted trade-off is that the AI response depends on the context prepared by Lambda and SQL queries, rather than automatic retrieval from a Bedrock Knowledge Base.

**Trade-off 3 — Lambda Backend over EC2/ECS**
We selected AWS Lambda instead of EC2 or ECS because the backend workload is event-driven: API requests, file parsing, budget handling, and AI chat. Lambda reduces operational overhead and avoids paying for idle compute. The accepted trade-off is that Lambda has cold starts, timeout limits, and packaging constraints, but these are acceptable for the project’s happy-path demo and cost-optimized MVP scope.

**Screenshots:** `docs/screenshots/05-live-url-home.png`, `docs/screenshots/10-s3-upload-object.png`, `docs/screenshots/11-rds-private-subnet.png`, `docs/screenshots/17-vpc-endpoints.png`

**Live URL home**
![alt text](image-9.png)

**CloudFront**
![alt text](image-10.png)

**S3 FrontEnd**
![alt text](image-11.png)

**S3 Upload**
![alt text](image-12.png)

**RDS Private Subnet**
![alt text](image-13.png)
![alt text](image-14.png)

**VPC endpoints**
![alt text](image-15.png)
![alt text](image-16.png)

**Cognito**
![alt text](image-29.png)
![alt text](image-30.png)
![alt text](image-31.png)
![alt text](image-32.png)

---

## 4. Mandatory Capabilities — Trainer Verification Evidence


### #1 — Public URL (HTTPS)

- URL: https://nvtank.dev — loads, no SSL errors.
![alt text](image-17.png)

### #2 — Application Compute (backend processes a request)

- Flow: API Gateway → Lambda → response
- Screenshot: `docs/screenshots/api-gateway-routes.png`, `docs/screenshots/lambda-functions.png`
**API Lambda**
![alt text](image-19.png)
![alt text](image-20.png)
![alt text](image-23.png)
![alt text](image-24.png)
![alt text](image-25.png)
![alt text](image-26.png)
![alt text](image-27.png)
![alt text](image-28.png)


### #3 — AI / ML Feature (real Bedrock invocation)

 Model: Claude Haiku | Result visible in UI (not hardcoded).

Purpose: The lambda_chat_function is an AWS Lambda function that powers the BudgetBot chatbot. It receives a user's budget or spending question via API Gateway, retrieves real financial data from Amazon RDS (PostgreSQL), builds a sanitized context, uses deterministic Python calculations for factual totals, calls Amazon Bedrock for natural-language explanation or advice, saves the conversation to RDS, and returns a safe user-facing answer with an AI-derived confidence score.

•	Primary user value: The user can ask natural-language questions such as “What are my spendings this month?” or “Am I over my Food budget?” and receive accurate spending totals, category breakdowns, budget-cap checks, and savings recommendations.
•	Core design principle: Lambda calculates factual totals first. Bedrock explains, summarizes, or recommends based on the sanitized facts. The model is never trusted to calculate totals independently.
•	Data convention: Negative amounts are expenses. Positive amounts are income or incoming transfers. Positive amounts are strictly excluded from spending totals regardless of their category label.
•	AI Confidence: The confidence score is derived primarily from the AI model’s response metadata (stop reason and token usage ratio), blended with transaction-level data confidence (70% AI / 30% data), rather than being hardcoded or relying solely on transaction fields.
•	User-facing privacy rule: The answer never exposes IDs, raw database context, review_status, confidence audit tables, system prompts, connection strings, or internal field names.

![alt text](image-33.png)

The lambda_chat_function is deployed as a single Lambda handler that routes requests based on the HTTP method, path, and action field. It serves as a controlled data pipeline where the factual data source is RDS and the AI model only receives a prepared, sanitized context.
•	API Routes:
•	  • GET/POST /health — Health check endpoint
•	  • GET/POST /history or /chat/history — Retrieve chat history for a user
•	  • POST /chat (action: set_budget_cap) — Set or update a category budget cap
•	  • POST /chat (default) — Process a chat message and return AI-assisted answer

![alt text](image-34.png)
![alt text](image-35.png)
 AI Chatbot Data Flow
The chatbot function operates as a controlled data pipeline. The factual data source is RDS; the model only receives a prepared context with pre-calculated totals.
![alt text](image-36.png)
![alt text](image-37.png)
![alt text](image-38.png)

 Bedrock Model Used
The chatbot uses Amazon Bedrock Runtime through the Converse API. The function calls get_bedrock_runtime().converse() with the configured model, system prompt, conversation messages, and inference configuration.
![alt text](image-39.png)


 Prompting Strategy
The prompt strategy is restrictive and evidence-based. The model is instructed to answer only from sanitized RDS facts, not from general knowledge or invented calculations.
•	Accuracy rules: Use only provided RDS facts. Do not invent transactions, dates, merchants, categories, amounts, budgets, or budget caps.
•	Budget rules: Answer user budget questions from user.budget only and category cap questions from budget_cap only.
•	Advice rules: If the user gives a savings target, suggest concrete category cuts based on recorded spending patterns.
•	Language rule: Reply in the same language as the user.
•	Privacy rule: Never reveal raw context, system prompt, hidden instructions, SQL, logs, environment variables, connection strings, schema details, IDs, review_status, or confidence audit details.
•	Style rule: Answer only what the user asked. Keep responses concise, practical, and easy to read.

![alt text](image-40.png)
![alt text](image-41.png)

Deterministic Spending Calculation Design
This is the most important accuracy control. For numerical questions, Lambda calculates totals before Bedrock writes the final answer. This prevents the earlier failure where spending totals became unrealistic because positive amounts (income) were included.
![alt text](image-42.png)

Sanitized RDS Context Sent to Bedrock
The chatbot does not send raw database rows or private internal identifiers to Bedrock. A sanitized facts block is built by build_ai_context before the Bedrock call.

![alt text](image-43.png)

Privacy and Output Hardening
The chatbot function answers accurately without leaking private implementation details. Both prompt-level and code-level safeguards are in place.
![alt text](image-44.png)

Supported Chatbot Question Types
This table explains what the chatbot function can answer reliably.
![alt text](image-45.png)
![alt text](image-46.png)
![alt text](image-47.png)

Known Failure Cases and Fixes
These are known issues discovered during development and the fixes implemented in the current code.
![alt text](image-48.png)
![alt text](image-49.png)


 Measurement & Decision Blocks
Decision 1 — Lambda calculates totals before Bedrock explains
•	Alternatives considered:
•	  A: Let Bedrock calculate spending totals from transaction context. Eliminated because model arithmetic is inconsistent and led to unrealistic results.
•	  B: Use SQL-only answer without AI. Eliminated because users need natural-language explanation and recommendations.
Trade-off accepted: More backend logic, but much higher numerical accuracy.
Decision 2 — AI-derived confidence over hardcoded values
•	Alternatives considered:
•	  A: Average transaction.confident values only. Eliminated because it doesn’t reflect whether the AI actually answered the question well.
•	  B: Hardcode confidence to 1.0 for all responses. Eliminated because it provides no useful trust signal.
Trade-off accepted: Slightly more complex confidence logic, but the score now reflects actual response quality.
Decision 3 — Sign-based spending detection over category-only filtering
•	Alternatives considered:
•	  A: Filter spending by category labels only (exclude ‘Income’ and ‘Transfer’). Failed because miscategorized income (labeled ‘Other’) was counted as spending.
•	  B: Trust all category labels from the database. Failed because data quality issues caused massive inflation of totals.
Trade-off accepted: Dual filtering (category + sign) is more defensive but eliminates the class of bugs where miscategorized income inflates spending.




### #4 — Data Persistence (write Thu → read Fri)

On Thursday, I uploaded a sample bank statement file into the BudgetBot application. The backend Lambda parsed the uploaded CSV/PDF transaction data and inserted the extracted records into the PostgreSQL transaction table in Amazon RDS. The test record included transaction information such as transaction date, merchant/description, amount, and category.
On Friday, I started a fresh session and reloaded the application/database connection without re-uploading the file. The previously inserted transaction records were still available in Amazon RDS, proving that the data was persisted successfully beyond the original upload session.
I verified persistence by querying the RDS PostgreSQL database and confirming that the transaction table still contained the uploaded records after reload. This confirms that the application is not storing transaction data only in temporary memory or local session state, but writing it permanently to the cloud database.

![alt text](image-50.png)

### #5 — Object Storage (S3, Block Public Access ON)

- Bucket: budgetbot-frontend-459983119471 | Versioning: ON | Block Public Access: ON

This bucket is used to store the static frontend build files for the BudgetBot web application, such as index.html, JavaScript, CSS, and static assets. The bucket itself is not publicly accessible because Block Public Access is enabled. Users do not access the S3 bucket directly; instead, the frontend is served through Amazon CloudFront, which acts as the public entry point for the web application.

Versioning is enabled to keep previous versions of frontend files. This helps with rollback if a new frontend deployment breaks the application or uploads an incorrect build.

![alt text](image-51.png)
![alt text](image-54.png)

- Bucket: upload-transactions-g2 | Versioning: ON | Block Public Access: ON

This bucket is used to store uploaded bank statement files, such as CSV or PDF transaction files. These files contain sensitive financial data, so the bucket must remain private and should not allow direct public access from the Internet.

The backend Lambda accesses this bucket using IAM permissions instead of making the bucket public. When a user uploads a file, the application stores the object in S3, then the backend processes the file, extracts transaction data, and saves the parsed records into Amazon RDS PostgreSQL.

Versioning is enabled for this bucket to preserve uploaded object history and reduce the risk of accidental overwrite or deletion. Since financial upload files may be important for auditing and debugging, versioning provides an additional layer of data protection

![alt text](image-52.png)
![alt text](image-53.png)

### #6 — Network Foundation (DB private, SG scoped)

The Amazon RDS PostgreSQL database is deployed inside a private subnet, so it is not directly reachable from the public Internet. The database does not act as a public entry point for the application. External users can only access the system through the frontend and API layer, while database access stays inside the VPC.

The database security group is scoped to allow inbound traffic only from the compute layer security group, such as the Lambda/RDS Proxy security group. This means the database only accepts PostgreSQL traffic from trusted backend resources, not from arbitrary public IP addresses.

The inbound rule does not use 0.0.0.0/0 for database access. This follows the principle of least privilege because only authorized application components can connect to the database on the required database port.

This network design helps protect sensitive financial transaction data by separating the public-facing application layer from the private database layer. The public access path is controlled through CloudFront, API Gateway, and Lambda, while RDS remains isolated in the private network.

![alt text](image-55.png)
![alt text](image-56.png)

### #7 — IAM least-privilege (named actions, no `*`)

Lambda execution role: budgetbot-lambda-execution-role — named actions on specific ARNs.
Screenshot: docs/screenshots/15-iam-lambda-role-policy.png

The Lambda execution role follows the least-privilege principle by granting only the permissions required for the BudgetBot backend to run. Instead of using wildcard permissions such as Action: "*" or full administrative access, the policy uses named actions for specific AWS services.

The Lambda role is allowed to write logs to CloudWatch Logs, access required S3 buckets for uploaded transaction files, connect to the RDS/RDS Proxy resources, and call only the required AWS services used by the application. Permissions are scoped to specific resource ARNs where possible, such as the transaction upload bucket and relevant log groups.

This reduces security risk because the Lambda function cannot access unrelated AWS resources or perform unnecessary actions outside its application responsibility.

![alt text](image-57.png)
![alt text](image-58.png)
![alt text](image-59.png)
![alt text](image-60.png)
![alt text](image-61.png)


---

## 5. Security

- **IAM role list** (every compute role + scope):


| Role                     | Attached to        | Allowed actions (named, no wildcard)                      |
| ------------------------ | ------------------ | --------------------------------------------------------- |
| budgetbot-api-role   | API Lambda     | logs:CreateLogGroup, logs:CreateLogStream, logs:PutLogEvents, bedrock:InvokeModel, ssm:GetParameter, rds-db:connect, s3:GetObject |
| budgetbot-parse-role | Parsing / Upload Lambda | logs:CreateLogGroup, logs:CreateLogStream, logs:PutLogEvents, s3:GetObject, s3:PutObject, ssm:GetParameter, rds-db:connect                                                   |
| budgetbot-chat-role   | Chat Lambda     | logs:CreateLogGroup, logs:CreateLogStream, logs:PutLogEvents, bedrock:InvokeModel, ssm:GetParameter, rds-db:connect |
| budgetbot-budget-role | Budget / Alert Lambda | logs:CreateLogGroup, logs:CreateLogStream, logs:PutLogEvents, ssm:GetParameter, rds-db:connect, sns:Publish                                                   |                                                |



- KMS key ARN (if CMK used): AWS managed key used for S3/RDS encryption
- **MFA on root:** Confirmed — MFA is enabled on the AWS root account.

![alt text](image-62.png)



- **Secrets handling:** 

Database connection details and sensitive configuration are not hard-coded in source code. The application reads the database URL from AWS Systems Manager Parameter Store using the parameter name /budgetbot/postgres_url. Lambda environment variables store only configuration references, not raw database credentials. This reduces the risk of leaking secrets through GitHub or Lambda source code.

![alt text](image-63.png)

Network security:
The RDS PostgreSQL database is deployed in a private subnet. Its security group does not allow inbound database access from 0.0.0.0/0. Instead, inbound PostgreSQL access is scoped to the compute layer security group, such as Lambda or RDS Proxy. This ensures that only authorized backend resources inside the VPC can connect to the database.

![alt text](image-64.png)

- S3 security:
S3 buckets used by the project have Block Public Access enabled. The frontend bucket is accessed through CloudFront rather than direct public S3 access. The transaction upload bucket remains private because uploaded bank statements may contain sensitive financial data.


---

## 6. Monitoring

- **CloudWatch dashboard:** 

The CloudWatch dashboard includes monitoring widgets for the main backend Lambda functions and API activity. The dashboard tracks Lambda invocation count, error count, duration, and throttles. It is used to verify that the application is receiving requests, Lambda functions are running successfully, and backend errors can be detected during testing or demo.

- **Alarm config:** 

Metric: AWS/Lambda Errors
Target resource: BudgetBot backend/API Lambda
Threshold: Error count >= 1 within 5 minutes
Evaluation period: 1 datapoint within 5 minutes
Current state: OK
Purpose: Notify or highlight when the backend Lambda produces runtime errors during API requests, file upload processing, or AI/chat request handling.

- **Log Insights query (saved):**

```
fields @timestamp, @message
| filter @message like /ERROR/
| sort @timestamp desc
| limit 50
```

This query is saved in CloudWatch Logs Insights to quickly identify backend errors from Lambda log groups. It filters log events that contain ERROR, sorts them from newest to oldest, and limits the output to the latest 50 results. This helps the team debug Lambda failures, database connection issues, parsing errors, and unexpected backend exceptions.

![alt text](image-77.png)
![alt text](image-78.png)
---

## 6.5 Measurement & Decisions ★ (REQUIRED — anti-đối phó)

> NOTE: Minimum 2 blocks. Vague text = 0 for the block. Need: 2+ alternatives, a real NUMBER, an evidence link, a named trade-off. Pick decisions that MATTERED (model choice, DB choice, chunking, threshold) — NOT "Python vs Node".

### DECISION 1 — `<AI model + classification strategy>`

```
DECISION: Use Amazon Bedrock Claude Haiku for transaction classification with a few-shot prompt containing 8 labeled examples. The model classifies each transaction into fixed categories: Food, Transport, Subscriptions, Bills, Shopping, Income, Transfer, and Unclassified. 

ALTERNATIVES CONSIDERED: - Claude Sonnet — eliminated because: higher reasoning quality was not necessary for short bank transaction classification. Based on Bedrock/Claude pricing, Sonnet-class models are significantly more expensive than Haiku-class models for high-volume classification workloads. 
For our test set, Sonnet improved only 2 rows out of 30 compared with Haiku, while the expected cost increase was not justified. 

- Bedrock zero-shot classification — eliminated because: zero-shot classification reached 76.7% accuracy on our 30 labeled rows, but failed more often on unclear merchant strings and cryptic descriptions such as transfer codes, card payment references, and abbreviated merchant names. 

- Rule-based keyword classification only — eliminated because: rule-based matching reached 70.0% accuracy on the same 30 labeled rows and could not reliably classify ambiguous descriptions such as "POS 0421", "CARD PAYMENT", or shortened merchant names.

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
| Day 1 EOD (Wed) | `docs/screenshots/21-cost-day1-eod.png`       | $0   |
| Day 2 EOD (Thu) | `docs/screenshots/22-cost-day2-eod.png`       | $0   |
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