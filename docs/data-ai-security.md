# Data, AI & Security (Deep Dive)

## 1) Data Lifecycle
- Collection: Client form (multi-language), admin edits, system-enriched fields
- Validation: server-side schema validation, normalization (phone/email/locale)
- Storage: Google Sheets (submission tab + reference tabs)
- Processing: quotation/report generation, analytics exports
- Sharing: internal-only; exports via CSV/XLSX/Sheets links
- Retention: configurable by environment; default 12–24 months (GDPR-aligned)
- Deletion: data subject request workflow; soft-delete flag + periodic purge job

```mermaid
flowchart LR
C[Client Form] --> V[Validate & Normalize]
V --> S[(Google Sheets)]
S --> P[Processors (Quotation/Report)]
S --> A[Analytics/Exports]
A --> BI[External BI]
```

## 2) Logical Schema (Sheets)
- Submissions: core application data (company/contact/iso/scope/employees/sites)
- Reference: industries, iso code lists, language map
- Ops: status, owner, follow-up date, notes

| Sheet | Key Columns | Purpose |
|---|---|---|
| submissions | timestamp, company_name, reg_no, industry, contact_name, email, phone, address, iso_list, employee_count, sites, scope, language, status | source of truth |
| ops | application_id, owner, status, follow_up, priority, tags | workflow ops |
| ref_industries | code, name | normalization |
| ref_iso | iso_code, name | validation |

ERD (conceptual):
```mermaid
erDiagram
  SUBMISSIONS ||--o{ OPS : tracks
  SUBMISSIONS {
    string id
    datetime timestamp
    string company_name
    string reg_no
    string industry
    string contact_name
    string email
    string phone
    string address
    string[] iso_list
    int employee_count
    int sites
    string scope
    string language
    string status
  }
  OPS {
    string id
    string application_id
    string owner
    string status
    date follow_up
    string[] tags
  }
```

## 3) RAG Pipeline for AI
- Knowledge Sources: IAF MD5 parameters, quotation templates, FAQ, policy snippets
- Indexing: section-level chunks with metadata (type, version, locale)
- Retrieval: top-k similarity + rule-based filters (locale/standard)
- Prompt Assembly: system → policy → retrieved → user → tools
- Guardrails: banned topics, PII redaction, length & cost limits

```mermaid
flowchart TB
K[Docs/Templates] -->|chunk| IDX[Vector Index]
Q[User Query] --> RET[Retriever]
RET --> CXT[Context Builder]
CXT --> LLM[ISO-Guardian]
LLM --> OUT[Answer/Snippet]
```

## 4) Prompt Governance
- Templates: versioned prompts per task (faq, gap, quotation-assist)
- Variables: locale, standard, employee bracket, scope keywords
- Policies: safe-completion, refusal cases, escalation phrases
- Observability: prompt+output hashing, sampled reviews, drift watch

## 5) Evaluation (AI & UX)
- Offline: RAG relevance@k, answer faithfulness, toxicity/safety checks
- Online: CSAT, time-to-answer, fallback rate, deflection rate (reduced human escalations)
- Golden Set: curated Q/A for ISO 9001/14001/45001 + gap scenarios
- Regression: threshold gates in CI before prompt/model upgrades

## 6) Security & Privacy Controls
- Transport: HTTPS/TLS; strict CORS
- Access: admin auth, least privilege on Sheets sharing
- Input Security: server-side validation, escaping, file-type allowlist
- Secrets: environment variables, no secrets in code/logs
- PII: data minimization, masking in logs/exports, retention policy
- DSR: data subject request workflow (export/delete) documented

## 7) Cost/Quota Management (AI)
- Per-action quotas: quotation/report generation daily caps per admin
- Token budget: max tokens per request, truncation policy
- Backoff & Retry: exponential for 429/5xx; circuit breaker on spikes

## 8) Data Quality
- Required field coverage dashboard (Sheets formulas)
- Duplicate detection: company + reg_no composite key
- Anomaly rules: out-of-range employee counts, invalid scopes
- Review queue: low-confidence records flagged to admin

## 9) Export & Interop
- Exports: CSV/XLSX/PDF; BI connectors via Sheets
- Downstream: CRM export template; Dynamics 365 mapping (roadmap)

## 10) Checklists
- Privacy
  - [ ] Data minimization, purpose limitation, retention defined
  - [ ] Log masking, PII export controls
  - [ ] DSR process (access/delete) in place
- Security
  - [ ] Secrets/keys in environment variables
  - [ ] CORS/input validation policies verified
  - [ ] Least-privilege sharing on Sheets
- AI
  - [ ] RAG sources up-to-date and versioned
  - [ ] Prohibited topics/sensitivity guidelines applied
  - [ ] Offline/online evaluation metrics dashboarded
