# Jaako's Restaurant — AI Booking Assistant

Restaurant booking lines and inboxes mean staff repeatedly handling the same "is X time available?" questions and manually updating a calendar and tracking sheet for every reservation. This workflow gives the restaurant a conversational AI assistant that checks calendar availability, books tables, sends confirmation emails, and logs every reservation — without staff touching it.

## Features

- **Webhook-triggered conversational agent** — receives booking requests via webhook (designed to sit behind a chat widget or messaging integration)
- **Two-stage AI Agent design** — one agent handles initial conversation/intent, a second handles the actual booking action, each backed by its own Google Gemini chat model
- **Calendar availability checking** — the agent checks Google Calendar in real time before confirming any booking slot
- **Automated booking creation** — once a slot is confirmed, the agent creates the calendar event directly via a Google Calendar tool
- **Confirmation emails** — a Gmail tool sends the customer a confirmation email once their booking is finalized
- **Reservation logging in Google Sheets** — every booking is recorded to a Sheets-based log for the restaurant's records
- **Wait/response handling** — a Wait node manages timing between conversational steps so the assistant doesn't rush or drop context
- **Documented with sticky notes** — the workflow includes inline sticky-note documentation explaining each stage, for easier handover/maintenance

## How it works

1. A booking request comes in via webhook (e.g. from a website chat widget)
2. The first AI Agent interprets the customer's intent (date, time, party size) and checks calendar availability
3. Once a valid slot is identified, the second AI Agent finalizes the booking — creating the calendar event and updating the Sheets log
4. A confirmation email is sent to the customer via Gmail
5. The webhook responds back to the calling client with the booking confirmation

## Stack

n8n · Google Gemini · Google Calendar · Google Sheets · Gmail · n8n Webhook/Respond to Webhook nodes

## Setup

1. Import `workflow.json` into your n8n instance
2. Reconnect credentials: Google Gemini (PaLM) API, Google Calendar OAuth2, Google Sheets OAuth2, Gmail OAuth2
3. Point the Google Calendar nodes at the restaurant's actual booking calendar
4. Update the Google Sheets node to your own reservation log sheet
5. Wire the webhook URL into your chat widget or messaging front-end
6. Activate the workflow

## Notes

Built for a restaurant client to remove manual reservation handling — the two-agent design (intent agent + booking agent) keeps conversation handling and the actual write actions (calendar/sheet/email) cleanly separated, which made debugging and prompt-tuning much easier during development.
