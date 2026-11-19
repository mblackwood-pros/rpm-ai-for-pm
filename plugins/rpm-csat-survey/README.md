# RPM CSAT Survey

Runs the twice-yearly Real Property Management customer satisfaction (CSAT/NPS) survey cycle for a franchise on AppFolio.

## Skills

| Skill | What it does | Ask it |
|---|---|---|
| CSAT Survey Data Prep | Checks AppFolio through Realm-X, read only, and returns a one-screen readiness table; clean-up lists on request | "Run CSAT data prep" |
| CSAT Survey Communication | Drafts the pre-survey, reminder and thank-you notes from the franchisor templates, shows the audience count, and opens a resident send in AppFolio only after your yes | "Send the CSAT heads-up to residents" |
| CSAT Survey Analysis | Gathers every NPS Scorecard it can find (RPM Intranet, coach's email, your uploads), builds a private results sheet and a shareable trend dashboard, checks the franchisor's figures, finds top promoter and detractor issues, and uses Realm-X to flag respondents who left and properties with repeat responses | "Analyze our CSAT results" |

All three use the coach's timeline email for the season to know which step is due.

## Connectors

| Connector | Needed for | Required? |
|---|---|---|
| AppFolio Realm-X | Counts, checks and resident sends; matching respondents in analysis | Yes for data prep and communication; optional for analysis |
| Work email (Microsoft 365 / Outlook or Gmail) | Finding the coach's timeline and results emails | Optional; otherwise paste the dates |
| Browser (Claude's built-in browser or Claude in Chrome) | Reading NPS Scorecards and the current CSAT templates on the RPM Intranet, and preparing owner letters in AppFolio; you sign in yourself | Optional; otherwise upload the files |

If a required connector is missing, the skill stops and says how to connect it.

## What Realm-X can and can't send (checked November 2026)

- Bulk email and text to tenants: yes. Realm-X opens a draft in AppFolio, and you click Send.
- Bulk messages to owners: not yet (listed as planned). The communication skill prepares owner emails as an AppFolio owner letter (Communication › Letters) in the browser, and you click Send. AppFolio has no bulk text to owners.
- Scheduling: not supported; sends go when you click Send.
- Texts go only to Financially Responsible, non-hidden tenants with a mobile number. Confirm consent and opt-out settings with AppFolio support before the first bulk text.

## Safety

- Data prep and analysis never change AppFolio.
- The analysis results sheet holds respondent emails and comments and stays in your own files; the trend dashboard shows scores only.
- Nothing is sent without your explicit yes to the exact message and audience count.
- Names, contact details and survey comments stay inside your franchise.
