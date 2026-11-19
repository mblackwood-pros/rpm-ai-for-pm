---
name: csat-survey-analysis
description: "This skill should be used when the user asks to \"analyze our CSAT results\", \"pull our NPS scorecards\", \"compare this survey to last time\", \"show our NPS trend\", \"what are detractors complaining about\", \"pull past CSAT results from the Intranet\", or wants an action plan or team review from RPM franchise customer satisfaction (NPS) survey results. It gathers the NPS Scorecards (RPM Intranet, coach's email or uploaded copies), builds a private consolidated results sheet and a shareable trend dashboard, checks the franchisor's figures, finds the top issues for promoters and detractors, and, with AppFolio Realm-X, flags respondents who have since left and properties with more than one response.\n"
metadata:
  version: "0.5.0"
---

# CSAT Survey Analysis

Turn every NPS Scorecard the franchise has into one consolidated picture: a private sheet with every response, a trend dashboard for owners and residents, a check of the franchisor's numbers, the top issues by promoters and detractors, and a read on how much repeat or departed respondents move the score. Read `references/csat-program.md` for the timeline and rules.

## What the results look like

Results arrive as **NPS Scorecards**, one per audience per season (spring and fall).

- **File names:** `[Office code] [Season Year] Owner NPS Scorecard.pdf` and `[Office code] [Season Year] Resident NPS Scorecard.pdf`. Older owner files say "Investor". Sometimes also a summary picture (`[Office code] NPS [Season Year].png`), a raw export (`.xlsx`) and a peer comparison (`... PEER Data ... Comparison.xlsx`).
- **Page 1:** office code and season; total responses; Promoters (9 to 10), Neutrals (7 to 8) and Detractors (0 to 6) with counts and percentages; the NPS; 1 to 5 ratings for communication and responsiveness; a side column with the NPS for past seasons back to about 2019. Owner cards still say "Investor Satisfaction" and "Investor NPS" on page 1 even when the file name says Owner; treat Investor and Owner as the same audience.
- **Rating blanks:** some respondents give a score but skip the two ratings, so the rating counts add up to less than the total. The page 1 rating percentages divide by all responses, blanks included (for example 40 of 88 shows as 45% even though only 80 rated).
- **Pages 2 onward:** one row per response: email, owner or resident (O or R), score, comment, communication rating, responsiveness rating (either rating may be blank). This is personal data (see Privacy).

## 1. Gather every scorecard you can find

Find the scorecards yourself before asking the user for anything. Look in all of these and collect every season you find, newest first. Ask the user to upload files, or to ask their coach, only for seasons you can't find in any of them.

1. **RPM Intranet** (needs a browser tool such as Claude in Chrome).
   - Open https://www.rpmintranet.com. If it shows the login page, ask the user to sign in themselves in that window, then continue. Never ask for, type or store a password or code. Leave "Keep me logged in" unticked.
   - Search **NPS Scorecard** (or a season, such as "Spring 2026") in the "Search anything..." box, or go to Office Documents › Franchise Offices Files › [franchise] › [office code_owner] › [office code - owner] › **Customer Experience**. (The `CSAT Survey FBO [year]` subfolder holds prep material, not results.) Scorecards the user uploaded themselves show up there too, with the user as author.
   - The search results show each scorecard's page 1 text (totals, counts and the history column), which is enough for the season table. Ignore the "AI Overview".
   - For the response rows: click a result's title to show its file actions; the **Download** link is `https://www.rpmintranet.com/mjanus/f/<id>`. The Intranet page has PDF.js loaded (`pdfjsLib`), so in the browser you can fetch that link with the user's session and read the text with positions: an email at the left starts each row; O/R, score, comment, communication and responsiveness sit in columns to its right; comment lines that wrap belong to the nearest row; a rating cell reads "5 - Highly Satisfied" (keep the digit). Check row counts against page 1 before using them.
   - **Getting the rows into the user's files (one file, no dialogs):** after reading every scorecard in the browser, build one CSV of all responses in the page (Season, Audience, Email, Score, Group, Comment, Communication, Responsiveness; quote fields; start with a UTF-8 BOM) and save it with a script-created `Blob` and a temporary `<a download>` click, named `[Office code] CSAT responses [first season]-[last season].csv`. The browser may show a Save dialog for each download, so make exactly one download: never download the scorecard PDFs one by one, never open the Intranet's Download links or file URLs, and never start several downloads in a loop. Before the download, tell the user one Save dialog may appear and to save into Downloads (or the CSAT folder). Then copy the CSV from Downloads into the CSAT folder and load it into the Responses sheet with a short script on the user's computer. Don't copy rows through the chat.
   - This needs the user's **Downloads** folder connected. Ask for it only at that point, with the steps in "Saving to the user's files", and tell the user the CSV stays in Downloads until they delete it, since it holds emails and comments.
   - Read only: never post, comment, like, pin or share.
2. **Coach's email**, if a mail connector is connected: search for scorecards or "NPS" from the franchise business coach and read the attachments.
3. **The user's own files and uploads** in this conversation or project.

Then tell the user in one short table which seasons you found for owners and residents, and where each came from.

**If nothing is found,** or seasons are missing, say which, and suggest two ways to fill the gap: upload any copies they have (scorecard PDFs or the vendor's spreadsheet), or ask their Franchise Business Coach for past survey results. Offer to draft a short note to the coach for them to send. Never send it yourself.

## Saving to the user's files

The results sheet and follow-up list hold emails and verbatim comments, so they live in a folder on the user's computer, never in the chat or an artifact. Do the gathering and analysis first; check for a folder only when it's time to save.

- **A folder is connected:** use it. With several, ask once which one the CSAT work goes in. Prefer a OneDrive or SharePoint-synced folder, and remind the user in one line to check who it's shared with.
- **None connected, or the scorecard PDFs are only in Downloads:** ask the user, in short steps, to add the folder you need:
  1. In the Claude desktop app, click **Add folder** under the message box.
  2. Pick the folder. For one that syncs, click **OneDrive – [company name]** in the left-hand list and open or create a folder such as **CSAT**. For downloaded scorecards, pick **Downloads**.
  3. Check that the path at the top of the window is the one they meant, then click **Select Folder**, and send any message so you can continue.
- After they add it, confirm you can see it by naming it. If it isn't there, they most likely picked a different folder: ask them to try again or paste the path from File Explorer's address bar, and request access to that path.
- If no folder can be connected, still publish the dashboard (counts only) and give the report, and say the private sheet and follow-up list need a folder.

## 2. Build the consolidated results sheet (private)

Create one spreadsheet (use the xlsx skill if available) saved in the user's own files, named `[Office code] CSAT results [first season]-[last season].xlsx`:

- **Responses**: one row per response from every scorecard: Season, Audience (Owner or Resident), Email, Score (0 to 10), Group (Promoter, Neutral, Detractor), Comment, Communication (1 to 5), Responsiveness (1 to 5), and the Realm-X columns from step 5 (Match, Property, Unit, Role, Status now, Left on, Responses from this property).
- **Season summary**: per season and audience: responses, % promoters, % neutrals, % detractors, NPS, number who rated communication and responsiveness, and % rating each 4 or 5 two ways: of all responses (matches the scorecard) and of those who rated (the fairer trend). Order seasons by date: Spring comes before Fall in the same year.
- **Franchisor check**: the table from step 3.
- **Adjusted views**: the table from step 5.

Check the row count per scorecard against its "Total Results" before going on. If rows can't be read cleanly from a PDF (wrapped comments, split pages), ask for the vendor's spreadsheet instead of guessing.

This sheet holds emails and comments. Never publish it as a page, attach it to anything shared, or post it to the Intranet.

## 3. Check the franchisor's figures

For each scorecard, recompute from the Responses rows and compare with page 1:

| Season | Audience | Responses: scorecard / rows | NPS: scorecard / recomputed | Match |

- NPS = % promoters minus % detractors, rounded to a whole number.
- Flag any count mismatch or an NPS difference of more than 1 point, and say which is likely right.
- Check that promoters, neutrals and detractors add up to the total, and that each rating's counts add up to no more than the total; report the blanks rather than flagging them as errors.
- Check the page 1 history column too: its season labels are sometimes wrong (a season repeated, given the wrong year such as "Fall 2026" for Fall 2025, or given the wrong audience). Prefer each season's own scorecard; use the history column only for seasons with no scorecard, and say so.
- Ignore the Intranet's "AI Overview" in search results; it has misreported scores and pointed to unrelated documents.

## 4. Build the trend dashboard (shareable)

Publish one dashboard page (in Claude, an artifact; use the **Data** type, or a Dashboard type, if one is offered, with the counts as attached CSV files) with **counts and scores only, no emails, names, addresses or comments**:

- Owner NPS and Resident NPS by season, as two lines on one chart or two small charts.
- Promoter, neutral and detractor share by season for each audience (stacked bars).
- Communication and responsiveness (% of those who rated giving 4 or 5) by season for each audience, with a note that the scorecard's own figure divides by all responses.
- **What to fix and what to keep doing:** per audience, the 1 to 3 issues and the strengths from step 6, each with its comment count, the number of comments it was counted from, and the change to make. Paraphrased themes only.
- **Detractors still with us:** per audience, latest-season detractors, how many are still customers, how many have left, and how many weren't found (step 5). Counts only; the named list stays in the private workbook.
- The franchisor check table, and the adjusted views from step 5 if Realm-X ran.
- A footnote with the source of each season and the NPS definition.

**Update, don't duplicate.** Before creating a dashboard, list the user's artifacts of the Data type and look for an earlier CSAT dashboard for this office (title like "[Office code] CSAT Trend"). If one exists, update it: replace its attached files with ones that include the new season (keep every earlier season's rows), refresh the fix/keep and detractor sections for the latest season, and tell the user which headline numbers changed, old and new. Create a new dashboard only if none exists or the user asks for one. Keep the same title so the link the team already has keeps working.

## 5. Look behind the score with AppFolio Realm-X (read only)

Skip this step if Realm-X isn't connected, and say so in one line with how to connect it. Never change anything in AppFolio.

The scorecards list emails, not addresses, so match on email first:

1. Ask Realm-X, in batches of about 25 emails, to find each email among owners and tenants, current and past, and return: property address, unit, role (owner, co-owner, tenant, other occupant), current status (Current, Notice, Past or no longer an owner) and the move-out or end date. Keep each question to one batch so counts can be checked.
2. Record matches in the Responses sheet. Count emails with no match; don't try other sources to identify them.
3. Flag:
   - **Left since the survey:** residents now Past or on Notice, and owners who no longer have a property under management.
   - **Repeat responses:** more than one response from the same property in the same season (roommates, co-owners, spouses). Note whether the scores agree.
4. Show how much these move the number, side by side, per audience and season:

| View | Responses | NPS |
| --- | --- | --- |
| As reported (franchisor) | | |
| One response per property (average the property's scores, then group) | | |
| Current customers only | | |

The franchisor's NPS stays the official number. The adjusted views are for the team's understanding only; never present them as the score.

5. **Detractor follow-up list (latest season).** Owner emails often sit on hidden owners or in a second email field, and resident emails on a non-primary field: when a first lookup misses, ask again including hidden records and all email fields before counting an email as not found. Then, in a "Follow-up" sheet in the private workbook, list every latest-season detractor who is still a customer: audience, email, score, ratings, property, status now, the issue in a few words, a specific recommended action (who should call, what to review before calling, what to offer), blank "Who calls" and "Done?" columns, and the verbatim comment. Order by score, lowest first. Flag for the user privately: anyone who asks for the owner or senior management, a complaint about a commitment the owner made, and an owner and resident at the same property.

## 6. Find the top issues by promoters and detractors

The point of the analysis is to tell the Franchise Business Owner, for each audience, **the 1 to 3 issues to fix** and **what they already do well, so they can do more of it**. Read every detractor and promoter comment of the latest season yourself and group them; don't rely on keyword counts. For each issue give the count of comments, a one-line paraphrase, and one concrete change. Then check earlier seasons for whether each issue is new, growing or fading. If a comment criticizes a staff member's language or another trait, report the underlying service problem (for example response time), not the trait.

For each audience, latest season first, then the trend across seasons:

- **Detractors (0 to 6):** group comments into themes (for example maintenance speed, maintenance request app, communication, move-in or move-out, deposits, fees, owner statements, rent pricing, vacancy). Give the top 3 to 5 issues with counts and share of detractor comments.
- **Promoters (9 to 10):** the top 3 things they praise, with counts. Staff praised by name: give a count only, and the detail privately if asked.
- **Neutrals (7 to 8):** one line on what would move them up, if the comments show it.
- Note which issues are new, growing or fading compared with earlier seasons.
- Paraphrase every theme. Never quote a comment word for word or tie it to a name, email, property or unit outside the private sheet.
- If a comment raises a safety, fair housing or legal concern, tell the user privately and separately.

## 7. Report

Keep the first view to one screen:

1. One sentence on how the latest season went for owners and for residents, with the trend.
2. Per audience: **Fix** (the 1 to 3 issues, with counts and the change to make) and **Keep doing** (what promoters credit).
3. Detractors still with us vs left, per audience, and the top-priority calls (counts and roles only in chat; names stay in the workbook).
4. One table per audience: Measure | Latest | Previous | Same season last year.
5. One line on the franchisor check, and one line on the adjusted views if Realm-X ran.
6. Where to find the private sheet (folder and file name) and the dashboard link.

Offer the details only on request. Offer to hand the themes to the communication skill for the thank-you notes.

## Privacy

- Emails, names, addresses, units and verbatim comments live only in the private sheet in the user's own files.
- The dashboard, the report and anything for the team, coach or fellow franchisees use counts, scores and paraphrased themes only.
- Realm-X lookups stay inside the franchise's own AppFolio and are read only.
