# Appendix – Templates (Expanded)

## Quotation (DOCX) Template
- Header/Footer: LRQA branding, logo, date, reference number
- Placeholders
  - {{company_name}}
  - {{contact_name}}
  - {{iso_list}}
  - {{employee_count}}
  - {{sites}}
  - {{scope}}
  - {{audit_days.stage1}}
  - {{audit_days.stage2}}
  - {{surveillance.year1}}
  - {{surveillance.year2}}
  - {{recert.year3}}
  - {{costs.application_fee}}
  - {{costs.initial_cert}}
  - {{costs.surveillance_total}}
  - {{costs.recert}}
  - {{costs.travel_expenses}}
  - {{costs.total_3y}}
- Notes
  - Multi-standard integration discounts applied when applicable
  - Currency/symbol configurable per environment

## Sales Report (HTML) Template
- Sections: Executive summary, ISO status/history, market position, outlook
- Placeholders
  - {{company_profile}}
  - {{industry}}
  - {{locations}}
  - {{employees}}
  - {{current_certs}}
  - {{recent_news}}
  - {{competitors}}
  - {{recommendations}}
  - {{links}}
- Print Styles
  - Page-breaks between sections when exporting to PDF
  - High-contrast palette for print-friendliness

## i18n
- All static labels pass through translation map
- Date/number formatting derived from `language` field
