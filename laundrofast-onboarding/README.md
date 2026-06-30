# Laundrofast Onboarding Automation

Laundrofast had several customer types — one-time vs. recurring, standard vs. premium — each needing a different welcome message and internal routing to the right factory/branch. Doing this by hand from form submissions meant inconsistent messaging and manual sorting. This workflow automates intake, customer-data storage, segmentation, and tiered welcome messaging end-to-end.

## Features

- **Form-based intake** — customers sign up via an n8n form (service type, plan, location, contact details)
- **Field normalization** — an Edit Fields (Set) node cleans and standardizes submitted data before it's stored
- **Customer data storage in Google Sheets** — every signup is logged centrally for the business's records
- **One-time vs. recurring routing** — an IF node splits the flow based on whether the customer selected a one-time or recurring service
- **Factory/branch-based routing** — recurring and one-time customers are routed to different factory branches based on their order type
- **Premium tier detection** — nested IF nodes detect premium customers within both the one-time and recurring branches
- **Tiered welcome emails** — premium recurring, premium one-time, and standard customers each receive a distinct, tailored welcome email via Gmail
- **Internal notification email** — a separate Gmail message notifies internal staff of the new signup

## How it works

1. Customer submits the signup form (Form Trigger)
2. Submitted fields are cleaned/standardized (Set node)
3. Customer record is stored in Google Sheets
4. An IF node checks one-time vs. recurring service type
5. Within each branch, a second IF node checks for premium tier
6. Based on the combination (one-time/recurring × standard/premium), the customer receives one of four tailored welcome emails
7. The appropriate factory branch is notified internally via Gmail

## Stack

n8n · Gmail · Google Sheets · n8n Form Trigger · n8n Set/IF nodes

## Setup

1. Import `workflow.json` into your n8n instance
2. Reconnect credentials: Gmail OAuth2 (note: this workflow uses two separate Gmail accounts — one for customer-facing emails, one for internal/factory notifications), Google Sheets OAuth2
3. Update the Google Sheets reference to your own customer log sheet
4. Update the factory/branch email addresses in the routing Gmail nodes
5. Customize each welcome email template's copy and branding
6. Activate the workflow and publish the form URL

## Notes

Built for a laundry service client to standardize and automate what was previously a manual, inconsistent onboarding process across multiple branches and customer tiers.
