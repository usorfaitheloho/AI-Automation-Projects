# AI Automation Projects

A collection of production-style AI and workflow automation builds, designed and shipped for real clients across finance, real estate, hospitality, and local services. Built primarily in **n8n**, combining LLMs (Google Gemini, OpenAI), vector search, CRM tooling, and messaging platforms to automate workflows that would otherwise require manual staff time.

Each folder is a self-contained project with its own README and exported `workflow.json` (importable directly into n8n).

## Projects

| Project | Industry | Core Problem Solved |
|---|---|---|
| [Loan Processing Funnel](./loan-processing-funnel) | Finance | End-to-end loan eligibility, interest calculation, offer delivery, and CRM logging |
| [Mainland Houses — AI Telegram Real Estate Chatbot](./mainland-houses-telegram-chatbot) | Real Estate | RAG-powered Telegram assistant for property Q&A, lead capture, and viewing scheduling |
| [Email Redirection Workflow](./email-redirection-workflow) | Internal Ops | AI classifies and routes inbound support emails to the correct department |
| [Jaako's Restaurant Booking Assistant](./jaakos-restaurant-booking) | Hospitality | Conversational AI agent for table bookings via calendar and email |
| [Laundrofast Onboarding](./laundrofast-onboarding) | Local Services | Automated customer onboarding and tiered welcome sequences from form submissions |

## Stack

n8n · Google Gemini · OpenAI · Supabase (pgvector) · Google Sheets/Docs/Drive/Calendar · Gmail · Slack · Telegram · Airtable

## Note on credentials

All credential references in the exported workflows have been stripped/replaced with placeholders. You'll need to reconnect your own OAuth credentials for Gmail, Google Sheets, Slack, etc. in n8n before importing and running any of these workflows.

## About

Built by [Faith Usor](https://www.linkedin.com/in/faith-usor/) — AI Automation Engineer based in Helsinki, Finland. Portfolio: [faithyautomate.lovable.app](https://faithyautomate.lovable.app)
