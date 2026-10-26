# Renewal Follow-Up Demo

An AI-assisted n8n portfolio demo for renewal milestones, contact research, email drafting, and call task preparation. Uses fictional accounts and template-generated text. No credentials are required.

## Milestone cadence

| Time before expiration | Prepared action |
| --- | --- |
| 60 days | Personalized renewal email draft |
| 30 days | Phone call task |
| 7 days | Email draft and phone call task |
| Every 7 days afterward | Repeat email and phone preparation while unresolved, including after expiration |
| Renewed or churned | Stop outreach preparation |

The demo catches a missed milestone within its active window: 31 through 60 days for the initial email, 8 through 30 days for the call, and 7 days or fewer for combined outreach. Later stages supersede missed earlier stages. Weekly outreach is due when the previous combined action was completed at least 7 days ago, or none has been completed.

## Workflow

Manual trigger → fictional accounts → stop resolved renewals → evaluate milestone cadence → filter due actions → contact research links and checklist → prepare email and call drafts → route by account health.

LinkedIn people searches and Google searches restricted to ZoomInfo are research links. They do not establish a company match or verify a contact. Contact status remains Pending manual review. Health scores below 60 receive High priority; others receive Normal priority.

Email subject and body are generated from templates using fictional account details and renewal timing. Wording distinguishes upcoming expiration, expiration today, and elapsed expiration. No price, discount, contract term, or service interruption is invented. Drafts require review. Call tasks are generated only for milestones that include a phone call.

## Run the demo

Import `renewal-follow-up.json` into n8n, select Execute workflow, and inspect the cadence node and final output nodes. The manual trigger simulates a daily review. This workflow does not create Gmail or Outlook draft objects, send emails, dial calls, or run on a live schedule.

## State and production requirements

Duplicate checks use fixture fields for completed milestones and elapsed days since the last combined outreach. Deterministic action keys identify the account, renewal cycle, and milestone or weekly bucket. This demo does not persist state across executions. Re-running unchanged fixtures can prepare the same drafts again.

For production, connect a daily schedule and authorized CRM or database. Read the current renewal status, real expiration date, contact verification, completed milestones, prior action keys, and last completed combined outreach date on each run. Use durable uniqueness/locking to avoid duplicate tasks. Persist completion only after the real action succeeds; generating a draft must not count as a sent email or completed call. Track email and call completion separately for partial failures. Recheck renewed/churned status and contact verification before any real outreach. Add a human approval step and email draft integration if desired.

## Validation

The sample set covers 60-day email, 30-day call, 7-day combined outreach, expiration-day weekly repeat, recent outreach suppression, renewed stop, churned stop, completed initial milestone suppression, and no action between milestones. Expected totals: 9 accounts, 2 resolved stopped, 7 evaluated, 4 due, 3 suppressed, 3 email drafts, and 3 call tasks.

Built and tested with AI assistance, including n8n Assistant. This is a portfolio demonstration, not a deployed customer system or a claim of measured business results.
