# Loan Processing Funnel

Most loan processing workflows require staff to manually review applications, calculate interest, send offer emails, chase responses, and update spreadsheets and CRMs by hand. This workflow automates the entire post-application pipeline — eligibility assessment, interest calculation, offer delivery, response tracking, and CRM logging — so the loan team only steps in when a decision needs human override.

## Features

- **Application intake via n8n form** — captures applicant name, email, salary range, loan amount, and reason for loan
- **Salary-based eligibility routing** — checks eligibility against salary bands and routes applicants down separate flows accordingly
- **Tiered interest calculation** — Code nodes calculate interest rate, total payable, and monthly repayment differently depending on loan size (e.g. 40% interest for loans above 1M, 50% for 500K–1M)
- **Welcome and decline emails** — every applicant receives an immediate response confirming eligibility status
- **Offer emails with embedded actions** — eligible applicants get a structured offer email and the workflow listens for their Accept/Decline response
- **Response-or-no-response branching** — IF nodes check whether the applicant responded within the wait window and branch accordingly
- **CRM logging in Google Sheets and Airtable** — every applicant and their status is logged and kept in sync across both Sheets and Airtable as the workflow progresses
- **Internal Slack notifications** — the loan team gets a Slack alert when key decision events occur
- **Approval/decline messaging** — final approval or decline emails are sent automatically once a decision is reached

## How it works

1. Applicant submits the loan form (n8n Form Trigger)
2. Their data is stored in Google Sheets/Airtable as the initial CRM record
3. A salary-range IF node determines eligibility; ineligible applicants receive an immediate decline email and exit the flow
4. Eligible applicants are routed through a Switch node that calculates interest and repayment terms based on loan amount tier
5. An offer email is sent and the workflow waits for the applicant's response
6. Response branches: if accepted → approval flow + CRM update + Slack alert; if declined or no response → decline flow + CRM update

## Stack

n8n · Gmail · Google Sheets · Airtable · Slack · n8n Code nodes (JavaScript) for interest/repayment math

## Setup

1. Import `workflow.json` into your n8n instance
2. Reconnect credentials: Gmail OAuth2, Google Sheets OAuth2, Airtable Personal Access Token, Slack OAuth2
3. Update the Google Sheets / Airtable base IDs to point to your own CRM sheet/base
4. Adjust salary bands and interest rate logic inside the Code nodes to match your lending criteria
5. Activate the workflow and publish the form trigger URL

## Notes

This was built for a real lending client and reflects an actual production deal funnel — salary bands, interest tiers, and offer/decline logic are simplified/genericized in this public version.
