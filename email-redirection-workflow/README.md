# Email Redirection Workflow

Inbound support inboxes often become a bottleneck — every email has to be manually read and forwarded to the right department (technical, HR, marketing, finance) before anyone can act on it. This workflow uses an AI classifier agent to read each incoming email and automatically route it to the correct department's inbox, with a Slack notification so the team knows it landed.

## Features

- **Automatic email triggering** — listens for new mail on a Gmail inbox in real time
- **AI Email Classifier Agent** — an LLM agent (Google Gemini) reads the subject and body and classifies the email into a department category
- **Structured JSON output parsing** — a Code node parses and validates the agent's classification output before routing
- **Department-based routing (Switch node)** — routes the email into one of four flows: Technical, HR, Marketing, or Finance
- **Auto-forwarding by department** — each branch forwards the original email to the relevant department's Gmail address
- **Slack notifications per department** — each routing branch also posts a Slack message so the relevant team is notified instantly, not just via email

## How it works

1. A new email arrives in the monitored Gmail inbox (Gmail Trigger)
2. The Email Classifier Agent (Gemini-backed) reads the email content and outputs a structured classification
3. A Code node cleans and parses that JSON output
4. A Switch node routes the email down one of four paths based on the classified department
5. Each path forwards the email to the correct department inbox and posts a Slack alert to that team's channel

## Stack

n8n · Gmail · Google Gemini (PaLM API) · Slack · n8n Code node (JSON parsing/cleaning)

## Setup

1. Import `workflow.json` into your n8n instance
2. Reconnect credentials: Gmail OAuth2, Google Gemini (PaLM) API, Slack OAuth2
3. Update the department email addresses in each Gmail "forward" node to match your real team inboxes
4. Update the Slack channel/webhook targets in each "Send a message" node
5. Adjust the classifier agent's prompt if your department categories differ from Technical/HR/Marketing/Finance
6. Activate the workflow

## Notes

Built to remove the manual triage step from a shared support inbox — instead of one person reading and forwarding every email, the AI agent handles classification and routing instantly, with Slack acting as the real-time notification layer.
