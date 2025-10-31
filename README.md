# NexusAILab – Technical White Paper Site

This repository hosts the technical white paper site for the LRQA AI-based ISO Application Platform.

## Stack
- MkDocs + Material theme
- Markdown sources in `docs/`
- Netlify deployment (builds MkDocs and serves `site/`)

## Local development
```bash
pip install -r requirements.txt
mkdocs serve  # http://127.0.0.1:8000
```

## Build
```bash
mkdocs build  # outputs to ./site
```

## Netlify
- Build command: `pip install -r requirements.txt && mkdocs build && [ -d submission ] && cp -r submission site/submission || true`
- Publish directory: `site`
- Access submission documents: `https://nexusailab.netlify.app/submission/`

## Structure
```
NexusAILab/
  docs/
    index.md
    executive-summary.md
    architecture.md
    data-ai-security.md
    operations-performance-cost.md
    integrations.md
    governance-compliance.md
    testing-pilot.md
    limitations-risks.md
    appendix/
      api.md
      data-schema.md
      templates.md
      faq.md
  submission/
    Mission_AI_Possible_Submission.html
    LRQA_User_Guide.html
  overrides/
    assets/stylesheets/extra.css
  mkdocs.yml
  netlify.toml
  requirements.txt
```

## Branding
- Primary: #111827 (ink)
- Accent: #00d4aa (LRQA teal)
- Font: Inter
- Logo: LRQA white logo on dark bg
