# Sending owner emails with AppFolio Letters

Realm-X can message tenants in bulk but not owners. Owner emails go out as an AppFolio **owner letter**. Paths below are relative to the franchise's AppFolio address (`https://<database>.appfolio.com`): ask the user once.

## Where things are

| What | Path |
|---|---|
| All letter templates (Tenant, Owner, Vendor, Applicant sections) | `/letter_writing/document_templates` (menu: Communication › Letters) |
| An owner letter's recipient screen | `/letter_writing/owner_letters/<id>/filter` (click the letter's name) |
| Edit an owner letter template | `/letter_writing/owner_letters/<id>/edit` |
| A tenant letter's recipient screen | `/letter_writing/tenant_letters/<id>/filter` |

Search the Owner and Tenant sections of the Letters page for a letter from an earlier season (names containing "survey", "input" or "feedback"). Names and ids differ by franchise and change over time.

## Recipient screen

- Filters: **Owners** (name search), **Property Group** (default **All**) or **Property**. Click **Search**.
- With Property Group All, the list should be close to Realm-X's count of owners linked to visible properties. Hidden owners and owners of hidden properties don't appear.
- Columns: Email, Letter (checkboxes), Owner, Last Letter, Date Sent. **Email** is ticked by default for every owner with an email address. "All / None" toggles each column.
- Buttons: **Email**, **Labels**, **Envelopes**, **Letters** (print PDF). Clicking **Email** opens a step to add an optional BCC and a comment for the email body, then **Send**.
- Each sent letter is saved in the owner's Letters section, and emailed letters also in their Emails section.

## Template editor

- Settings: Name, Description, "Include company logo", **If emailing, send letter as**: an email attachment or **part of email body** (use part of email body for a short note), margins, font.
- **Insert Field** adds merge fields. Owner letters have **Owner First Name** (merge key `owner.contact_info.first_name`), so greet with "Hello [Owner First Name]," instead of "Hello,".
- Optional PDF attachments are merged into one PDF.
- **Preview** shows the result; **Cancel** leaves without saving.

## Texting owners

AppFolio has no bulk text for owners. Texts go one at a time from the owner's Contact section, and Letters can't be sent by text.

## AppFolio Help Center articles

- [Email or Print Letters from AppFolio](https://knowledge.appfolio.com/en/articles/6985531-email-or-print-letters-from-appfolio)
- [Create Custom Letters](https://knowledge.appfolio.com/en/articles/6983432-create-custom-letters)
- [Email a Property Owner](https://knowledge.appfolio.com/en/articles/7321549-email-a-property-owner) (one owner at a time)
- [Send Bulk Messages with Realm-X](https://knowledge.appfolio.com/en/articles/17272110-send-bulk-messages-with-realm-x) (tenants only)
- [Texting from AppFolio](https://knowledge.appfolio.com/en/articles/6977892-texting-from-appfolio)
- [Create & Use Text Message Templates](https://knowledge.appfolio.com/en/articles/7235329-create-use-text-message-templates)
