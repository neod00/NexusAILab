# Operations, Performance & Cost (Deep Dive)

## 1) Operations
- Deployments: Netlify CI/CD (branch previews, protected main)
- Configuration: environment variables per env (dev/staging/prod)
- Runbooks: incident, rollback, traffic spike, provider outage
- Backups: Sheets version history + monthly CSV snapshot
- Change windows: weekly minor, monthly minor/infra, on-demand hotfix

## 2) SLOs & Error Budgets
| Metric | SLI | SLO Target |
|---|---|---|
| Availability (API) | % successful requests | ≥ 99.5% monthly |
| Latency (p95) | serverless function duration | ≤ 700 ms |
| Error rate | 5xx over total | ≤ 0.3% |
| Doc generation success | success/attempts | ≥ 99% |

- Error budget: 0.5% monthly unavailability; freeze releases if budget is exhausted

## 3) Performance Benchmarks (Targets)
- Static site TTFB: < 150 ms (CDN edge)
- API cold start: < 500 ms; warm paths < 200 ms
- Quotation generation: 5–10 s
- Sales report generation: 8–15 s

## 4) Caching & Optimization
- Edge/browser cache for static assets with immutable hashing
- Short-lived in-function cache for reference lookups, templates
- Gzip/Brotli enabled; minimize payloads; JSON field filtering

## 5) Capacity Planning
- Serverless concurrency auto-scales; set provider concurrency caps per env
- Quotas: cap heavy operations per user/day (doc/AI generation)
- Load tests before major launches; validate p95 latency and error rate

## 6) Monitoring & Alerting
- Logs: request id, route, status, latency, provider errors
- Metrics: invocation count, duration, 4xx/5xx, retries, AI/doc cost
- Alerts: error rate up, timeout spikes, cost anomaly (>X% daily)

## 7) Cost Model
| Cost Driver | Notes | Control |
|---|---|---|
| Netlify functions | invocations + duration | reduce cold starts; avoid heavy sync loops |
| CDN bandwidth | static files, reports | asset compression, cache rules |
| OpenAI/AI usage | tokens, requests | cap tokens, reuse context, cache results |
| Storage (Sheets) | minimal | data retention, archive to CSV |

- Budgeting: monthly budget per env; alert at 70%/90% thresholds
- Optimization tactics: batch non-urgent tasks, pre-generate templates, reuse partial computations

## 8) Incident Response
- Severity matrix (SEV1—complete outage; SEV2—major; SEV3—degraded)
- On-call: notify via chat/Email; status page (internal)
- Postmortem: timeline, root cause, actions, owners, deadlines
