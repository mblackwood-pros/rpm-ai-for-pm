# RPM AI for PM

Claude plugins and skills for Real Property Management franchise offices. Built and used by a franchise owner, and shared with other franchisees through the **AI in Property Management** group on the RPM Intranet. Use and adapt them for your office.

These assume you have your own access: an AppFolio database (with the Realm-X connector in Claude), an RPM Intranet login, and your coach's emails. Nothing here contains franchisor documents or any office's data; the skills read the current versions from your own systems each time they run.

## Contents

| Path | What it is |
|---|---|
| `plugins/rpm-csat-survey/` | CSAT/NPS survey cycle: AppFolio data prep, owner and resident communication, and results analysis with a trend dashboard. See its README. |
| `skills/` | Standalone skills (none yet). |

## Installing a plugin in Claude (desktop app)

1. Download this repo (Code › Download ZIP) and unzip it.
2. Zip the contents of the plugin folder you want (for example everything inside `plugins/rpm-csat-survey/`, so `.claude-plugin/` is at the top of the zip) and rename the zip to `rpm-csat-survey.plugin`.
3. Drag the `.plugin` file into a Claude chat, or upload it from the plugin settings, and accept it.
4. Connect AppFolio Realm-X (and optionally your work email) from Claude's connector settings.

## First run

The skills ask once for details that differ by office, such as your AppFolio address and the property group (if any) you use for listing-only properties. Each skill says what it needs.

## Contributing

Issues and pull requests are welcome. Never commit franchisor documents, templates copied from the RPM Library, or any owner, resident, or survey data.

## Disclaimer

Not an official Real Property Management or Neighborly product.
