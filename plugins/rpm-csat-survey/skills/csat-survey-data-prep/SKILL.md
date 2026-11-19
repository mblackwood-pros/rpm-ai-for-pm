---
name: csat-survey-data-prep
description: "This skill should be used when the user asks to \"run CSAT data prep\", \"get our data ready for the CSAT survey\", \"check owner and resident contact data before the survey\", \"is our AppFolio data ready\", or mentions the franchisor's CSAT Survey Data Prep guide. It checks AppFolio through Realm-X, read only, and returns a one-screen readiness summary with clean-up lists on request.\n"
metadata:
  version: "0.3.0"
---

# CSAT Survey Data Prep

Replace the franchisor's "CSAT Survey Data Prep" guide (three customized AppFolio directory reports checked by hand) with a handful of Realm-X questions that return only the problems that matter. Read `references/csat-program.md` first for the timeline, population definitions and rules.

The goal is a true answer to "will the survey reach the right people?", not a list of every imperfect record. Narrow every finding before reporting it, and judge it against the materiality threshold.

## 1. Check connectors first

- **AppFolio Realm-X** is required. If its ask tool (ask_appfolio) isn't available, stop. Tell the user in two lines that this skill needs the AppFolio Realm-X connector, that they can add it from their connector settings while signed in to AppFolio with an account that can see owners and tenants, and to run the skill again once it's connected. Do nothing else.
- **Mail** (Microsoft 365 / Outlook or Gmail) is optional. Use it to find the coach's CSAT timeline email as `references/csat-program.md` describes. If no mail connector is available, ask the user to connect their work email or paste the clean-up deadline. If they skip both, continue and leave the deadline blank.
- Use only Realm-X and mail. Don't depend on any other data source.

## 2. Get the deadline

Find the AppFolio data clean-up deadline and the survey start date in the coach's email. Show them in one line and ask the user to confirm. Don't hold up the checks while waiting; run them, then fill in the deadline once confirmed. If the deadline is today or past, say so in the first line of the report.

## 3. Run the checks quietly

Use ask_appfolio only. Never call propose_appfolio_action or anything that changes AppFolio. Ask for **counts only** ("Counts only, no names or contact details"). Keep owner and property questions in one Realm-X conversation and resident questions in another, passing the continuation_id back each time.

Don't narrate the questions, show Realm-X's prose, or print attached files. Read the summary numbers and move on.

### A. Affects the survey

| # | Check | Ask Realm-X (counts only) |
|---|---|---|
| 1 | Owners reachable | Owner Directory default filter (owners not hidden), linked to at least one visible property: total; of those, no email, malformed email. Also the Owner Directory row count. |
| 2 | Resident households | Tenant Directory, status Current, active tenants on active properties, residential leases only, one row per occupancy, Financially Responsible tenants only: number of occupancies. Also the Tenant Directory row count for Current. |
| 3 | Households with no email | Of those occupancies: how many have no Financially Responsible tenant with an email. |
| 4 | Bad resident emails | Among those Financially Responsible tenants: malformed emails; emails shared with another tenant. |
| 5 | Hidden properties that should be surveyed | See narrowing rule 5 below. Report only the final count. |
| 6 | Households missed because their tenants are hidden | See narrowing rule 6 below. Report only the final count. |
| 7 | Notice residents | Occupancies in Notice status on active properties (left out by the household rule; the coach decides). |

### B. Housekeeping (after the survey)

| # | Check | Ask Realm-X (counts only) |
|---|---|---|
| 8 | Missing management end dates | See narrowing rule 8 below. |
| 9 | Stale "Current" records | Count of hidden-tenant occupancies from rule 6 that were dropped because they are not on the current rent roll. |
| 10 | Owners or households with no phone | Phone only matters for text reminders, never for the survey itself. |

### Narrowing rules

Realm-X's first answer to a "hidden" question includes years of old records. Never report that first number. Narrow it in the same conversation:

- **Rule 5, hidden properties.** Start with hidden properties that have a residential occupancy in Current status, no move-out date, and a lease end date in the future or blank. Then split by management end date and property group:
  - Management end date in the past → correctly excluded. ✅, not counted.
  - Blank end date and in the franchise's **listing-only property group** → hidden is expected. ✅, not counted. Ask the user once which property group (if any) holds listing-only properties; don't guess a name.
  - Blank or future end date and **not** listing-only → the only ones reported. Before reporting, ask whether each had rent charged or an owner distribution in the last 90 days. Only those with activity count as "should be surveyed"; the rest move to check 8.
- **Rule 6, hidden tenants.** Start with Financially Responsible tenants on hidden tenant records who sit on a visible property with a Current residential occupancy and no move-out date, and whose occupancy has no other visible Financially Responsible tenant. Then ask Realm-X which of those occupancies are on the **current rent roll** with rent charged or paid in the last 90 days. Count only those. The rest go to check 9.
- **Rule 8, management end dates.** Hidden properties with a management start date and blank end date. Exclude the listing-only property group. Of the rest, report how many had no rent or owner distribution in the last 90 days and no owner linked to another visible property; those can't affect the survey.

### Sanity checks

- Compare checks 1 and 2 with the Owner and Tenant Directory row counts and with the user's sense of portfolio size if they offer it.
- If any number is more than a third of the survey population, ask Realm-X how it defined it and re-ask using the definitions in the reference file.

## 4. Apply the materiality threshold

A finding in section A needs fixing before the deadline only when it is **material**:

- it affects **2% or more** of the survey owners (check 1) or survey households (check 2), or
- it is concentrated in a way that could skew results: one team, one property group, one area or one property type.

Below the threshold, mark it ℹ️ and list it with the after-survey clean-up. Section B is never ⚠️ before the survey. Let the user change the threshold if they ask; use their number for the rest of the session.

## 5. Report on one screen

Lead with one sentence: ready or not ready, how many material items need fixing, and the deadline if it's today or past.

Then two short tables, nothing else.

**Affects the survey**

| Check | Count | % of list | Status | Fix |
|---|---|---|---|---|

**After the survey**

| Check | Count | Fix |
|---|---|---|

- Status is ✅ (nothing to fix), ⚠️ (material, fix before deadline) or ℹ️ (below threshold, or a decision for the coach).
- Fix is a few words: "Add email in AppFolio", "Unhide tenant", "Add management end date", "Enter move-out", "Ask coach".
- One footnote line under the tables with the population definitions and the threshold used.
- End with one offer: "Want the clean-up lists?"

Don't add commentary, method notes or Realm-X wording unless the user asks.

## 6. Lists only on request

- Ask Realm-X for just the requested rows: property ID, address, unit, occupancy ID or owner ID, and the field that's wrong. No names, emails or phone numbers.
- Realm-X returns relative links (`/properties/123`) and can't tell you the database web address. Ask the user once for their AppFolio address (for example `yourcompany.appfolio.com`) and build full links: `https://<address>/properties/<id>` and `https://<address>/owners/<id>`.
- Build **one Excel workbook** with one sheet per list, a clickable "Open in AppFolio" link on each row, a short "Likely type" or "Read" column where the data supports a guess, and a blank "Done?" column for staff. Drop property groups that appear on nearly every property (such as bank-change groups) from any group column. Add a one-line note at the bottom of each sheet saying what the list is and how to fix it.
- Deliver the workbook to the user. If a folder is connected, save it there too. If none is, tell the user in one line they can click **Add folder** under the message box and pick a folder (a OneDrive folder such as CSAT keeps it backed up) so lists save straight to their computer. Never paste names or contact details into chat, docs, videos or Intranet posts.

## 7. Re-check

When the user says fixes are done, re-run section A and show the same table with "Before" and "Now" columns.

## Limits

- Realm-X can't tell whether an email actually delivers; a valid-looking address can still bounce.
- This skill is read-only. If the user asks Realm-X or Claude to hide, unhide or edit records, say in one line that this check doesn't change AppFolio and staff make the fix there.
- Realm-X can't see property tags. If a decision depends on a tag, say so and include it as a column for staff to check.
