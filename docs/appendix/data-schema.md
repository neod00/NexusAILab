# Appendix – Data Schema (Expanded)

| Column | Type | Description | Validation |
|---|---|---|---|
| Timestamp | datetime | Submission timestamp | ISO8601; server-assigned |
| Company Name | string | Registered company name | 2–200 chars |
| Business Registration No. | string | Government ID | regex by country |
| Industry Type | enum | Industry classification | must exist in `ref_industries` |
| Contact Person | string | Name | 2–120 chars |
| Email | string | Contact email | RFC5322 pattern |
| Phone | string | Contact phone | E.164 recommended |
| Address | string | Company address | 2–300 chars |
| ISO Standards | string[] | Requested standards | each exists in `ref_iso` |
| Employee Count | number | Total employees | 1–100000 |
| Number of Sites | number | Locations to certify | 1–100 |
| Certification Scope | string | Scope text | 2–300 chars |
| Existing Certification | string | Current certs | free-text; optional |
| Consultant | string | Consultant name | optional |
| Status | enum | Application status | Pending/Approved/Rejected/Quoted |
| Language | enum | Form language | en, ko, ja, zh, es, fr, de, pt, ar, ru |

## Reference Tables
- `ref_industries(code, name)` – managed list
- `ref_iso(iso_code, name)` – e.g., ISO 9001, ISO 14001, ISO 45001

## Constraints & Keys
- Primary key: synthetic `id` (e.g., `app_YYYY_NNNNN`)
- Composite uniqueness: `(company_name, reg_no)` to detect duplicates
- Foreign validation: `industry` ∈ `ref_industries`; `iso_list` ⊆ `ref_iso`

## Derived Fields (Optional)
- `employee_bracket`: computed from `employee_count` (IAF MD5 brackets)
- `risk_profile`: derived from industry and multi-site indicator
