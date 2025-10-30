# Governance & Compliance (Deep Dive)

## 1) Governance Model
- Decision records: Architecture Decision Records (ADR) in repo
- RACI (sample)
| Activity | R | A | C | I |
|---|---|---|---|---|
| Architecture changes | Lead Architect | Head of Eng | Security, Product | Ops, QA |
| Data schema changes | Data Owner | Head of Eng | Product, Security | Ops |
| Release approval | Release Manager | Head of Eng | Product | All |

- Change Management
  - Proposal → Design Review → Staging Test → Approval → Release → Post-release review
  - Emergency changes allowed with retrospective postmortem

## 2) Compliance Framework
- GDPR: lawful basis, minimization, purpose limitation, retention
- Data Subject Rights (DSR): access/export/delete workflow
- Vendor & subprocessor review (AI providers, hosting)

### GDPR Mapping (Key Points)
| Area | Control |
|---|---|
| Lawful basis | Consent for newsletter; legitimate interest for ops |
| Minimization | Only required fields in forms; avoid free-text PII |
| Retention | 12–24 months default; periodic purge |
| Security | HTTPS, access control, secrets mgmt, logs masking |
| DSR | Documented process; SLA on response |

### DPIA (Summary)
- Context: processing of application data incl. contact info
- Risks: unauthorized access, data leakage, over-retention
- Mitigations: least-privilege, encryption-in-transit, retention, logging, reviews

## 3) Audit Readiness
- Evidence Catalog
  - Access logs, API gateway logs, function invocation logs
  - Change logs (Git history, PR reviews, release notes)
  - Data retention reports and purge logs
  - Incident postmortems and corrective actions
- Controls Testing
  - Quarterly: access review, secret rotation check, backup verification

## 4) Policies (Pointers)
- Security Policy: secrets, patching cadence, vulnerability handling
- Privacy Policy: collection, usage, retention, DSR handling
- Acceptable Use: admin access, sharing rules, export controls
