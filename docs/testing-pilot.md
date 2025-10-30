# Testing & Pilot (Deep Dive)

## 1) Test Strategy
- Shift-left: unit → integration → e2e → perf → security → UAT
- Environments: dev (feature), staging (pre-prod), prod (internal-only for docs)
- Test Data: sanitized fixtures; avoid real PII during tests

## 2) Test Matrix (Examples)
| Area | What to test | Tooling |
|---|---|---|
| Forms | required fields, validation, autosave | Playwright/Cypress |
| Admin | login, search, pagination, actions | Playwright/Cypress |
| API | input validation, happy/sad paths, rate-limit | REST tests |
| Docs | quotation/report generation | integration tests |
| AI | prompt templates, guardrails, RAG relevance | offline eval harness |

## 3) Categories
- Functional: core flows, edge cases, error handling
- Performance: API latency, concurrency, doc generation time
- Security: authN/Z, CORS, input sanitization, secret access
- Accessibility: keyboard nav, contrast, ARIA, focus states
- Internationalization: language switch, rtl (Arabic), numeric/date formats

## 4) Performance Tests
- API p95 latency SLIs; cold vs warm paths
- Quotation: 10 concurrent admins, < 10 s; Report: 10–20 concurrent, < 15 s
- Spike tests around releases; monitor timeouts and throttling

## 5) Pilot (Internal)
- Scope: staff-only pilot; no production client data
- KPIs: completion time reduction, task success rate, help (AI) deflection
- Feedback: usability surveys, bug backlog, prioritization cadence

## 6) Exit Criteria
- SLOs met for two consecutive sprints
- Critical bugs (P0/P1) zero; P2 trending down
- Security checks passed; data retention settings verified
