# Claims Email Triage Bot (AI Communications Mining)

An event-driven, serverless automation workflow built in **UiPath Studio Web** that ingests unstructured insurance customer emails from **Gmail**, classifies intent and sentiment using **Generative AI**, routes urgent escalations to **Slack**, and logs structured metadata into **Google Sheets** for straight-through processing (STP).

---

## Business Problem & Impact
Insurance operations teams receive thousands of unstructured emails daily regarding claims, renewals, and billing disputes. Manual inbox triage delays SLA response times and risks customer churn.
* **Zero Escalation Latency:** Detects `Urgent_Negative` complaints and alerts claims managers on Slack in **~6 seconds**.
* **Eliminates Manual Data Entry:** Extracts `Policy_Number`, `Claim_ID`, and `Customer_Name` automatically with zero copy-pasting.
* **Prevents Alert Fatigue:** Filters out routine `Neutral` and `Positive` inquiries from Slack while maintaining a 100% audit trail.

---

## End-to-End Architecture

1. **Real-Time Ingestion (`Gmail Integration Service`):** Listens for incoming emails matching `Policy Inquiry` or `Claim Update` subject filters.
2. **AI Communications Mining (`UiPath GenAI`):** Uses zero-shot prompt engineering with a strict JSON schema to classify `Intent`, detect `Sentiment`, and extract `Entities`.
3. **Conditional Triage Router (`JavaScript Expression + If Block`):** Evaluates `sentiment === "Urgent_Negative"` to separate exception handling from routine traffic.
4. **Priority Escalation (`Slack Integration`):** Fires real-time alerts to `#claims-escalations` exclusively for high-risk complaints.
5. **Straight-Through Processing Audit Log (`Google Sheets`):** Appends 100% of inquiries (urgent and routine) with timestamps and extracted fields into `Claims_Triage_Log`.

---

## Tech Stack
* **Orchestration:** UiPath Studio Web (Serverless API Workflow)
* **AI / NLP:** UiPath GenAI (`Content Generation` with Deterministic JSON Schema)
* **Integrations:** UiPath Integration Service (Gmail, Slack, Google Sheets)
* **Data Parsing:** JavaScript ES6 Expressions

---

## Live Execution Screenshots

### 1. UiPath Studio Web Workflow
![Workflow Architecture](workflow-architecture.png)

### 2. Automated Extraction & Audit Log (Google Sheets)
![Google Sheets Audit Log](sheets-audit-log.png)

### 3. Real-Time Urgent Escalation Alert (Slack)
![Slack Escalation Alert](slack-escalation-alert.png)
