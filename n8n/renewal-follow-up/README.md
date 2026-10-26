# Renewal Follow-Up Demo

An AI-assisted n8n portfolio demo that identifies upcoming renewals, prepares contact research links, and prioritizes follow-up actions using fictional account data.

## What it does

1. Starts manually.
2. Loads three fictional sample accounts.
3. Keeps accounts with renewals due within 90 days.
4. Builds LinkedIn people-search links and Google searches restricted to ZoomInfo.
5. Adds a contact verification checklist and a Pending manual review status.
6. Routes health scores below 60 to priority outreach preparation; other accounts go to standard follow-up preparation.

The workflow prepares next actions only. It does not verify contacts automatically, pause for approval, connect to a CRM, call an external service, or send outreach. All records have contactVerified set to false. The contact checklist is reference information, not a completed verification step.

## Run it

Import `renewal-follow-up.json` into n8n, open the editor, and select Execute workflow. No credentials are required. Inspect the output of each final node to see the account, contact research links, checklist, priority, and next action.

## Sample test results

Tested in n8n on October 26, 2026. Both output branches completed successfully.

| Fictional account | Days until renewal | Health score | Expected result |
| --- | --- | --- | --- |
| Acme Manufacturing | 45 | 45 | High priority; schedule a renewal risk review |
| Summit Logistics | 75 | 85 | Normal priority; schedule a renewal planning call |
| Harbor Services | 150 | 70 | Excluded by the 90-day filter |

Both retained accounts carry research links and Pending manual review status. A search link is not evidence of a matched company or verified contact. Company identity, current employer, renewal responsibility, and contact details must be checked by a person before any real outreach.

## Design choices

A manual trigger and fictional data make the demo easy to reproduce without customer systems. The 90-day window and health threshold are illustrative business rules. No live enrichment integration or measured business impact is claimed.

Built and tested with AI assistance, including n8n Assistant. Future work could replace sample input with authorized CRM data, add a human approval step, and integrate licensed enrichment services.
