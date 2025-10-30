# Limitations & Risks (Deep Dive)

## 1) Known Limitations
- AI responses can be generic; human review for edge/regulated content
- YouTube thumbnails availability varies for unlisted/age-restricted videos
- Google Sheets as primary store: row-based ops; not ideal for complex joins

## 2) Assumptions
- Moderate volume of submissions manageable via serverless + Sheets
- Admin usage primarily business hours with occasional peaks
- Newsletter/marketing integrations remain batch-oriented in near term

## 3) Out of Scope (Current)
- Full CRM bi-directional sync (Dynamics 365) — roadmap
- RBAC with fine-grained permissions — roadmap
- Real-time streaming analytics — roadmap

## 4) Risk Register
| ID | Risk | Likelihood | Impact | Owner | Mitigation |
|---|---|---|---|---|---|
| R1 | Provider outage (Netlify/Sheets) | Medium | High | Ops | fallback comms, queue retries, status page |
| R2 | AI costs spike | Medium | Medium | Product | quotas, caching, token caps, budget alerts |
| R3 | PII leak via logs/exports | Low | High | Security | mask logs, export controls, reviews |
| R4 | Data schema drift | Medium | Medium | Data Owner | schema versioning, migration scripts |
| R5 | Performance regressions | Medium | Medium | Eng | perf tests in CI, alerts on p95 |
| R6 | Spam/abuse on forms | Medium | Low | Eng | rate limit, captcha/hidden fields |

## 5) Monitoring & Review
- Quarterly risk review; update likelihood/impact; track mitigations to done
