# Mainland Houses — AI Telegram Real Estate Chatbot

A real estate agency was fielding the same property questions over and over on Telegram — availability, pricing, viewing requests — with staff manually checking spreadsheets and calendars to reply. This bot replaces that manual back-and-forth with a RAG-powered AI assistant that answers questions from real property data, captures leads, and books viewings, all inside Telegram.

## Features

- **Telegram-native conversational agent** — built on n8n's AI Agent node, responds to text and voice messages
- **Voice message support** — incoming audio is downloaded and transcribed (OpenAI Whisper) before being passed to the agent
- **Retrieval-Augmented Generation (RAG)** — property documents are embedded (Google Gemini `text-embedding-004`) and stored in a Supabase vector store, so answers are grounded in actual listing data instead of hallucinated
- **Auto-syncing knowledge base** — a Google Drive trigger watches for new/updated property documents and automatically re-embeds them into the vector store
- **Property listings + lead capture in Google Sheets** — the agent can query live listings and write new leads directly into a Sheets-based CRM
- **Calendar-integrated viewing scheduling** — the agent checks availability and books property viewings directly on Google Calendar
- **Multi-format replies** — the bot can send text, images, and structured listing info back into the Telegram chat
- **Conversation memory** — a buffer window memory keeps context across a user's conversation so the bot doesn't lose track mid-chat
- **Email handoff** — the agent can trigger a Gmail message for follow-ups that need a human touch

## How it works

1. A user messages the Telegram bot (text or voice)
2. Voice messages are downloaded and transcribed to text first
3. The AI Agent (OpenAI/Gemini-backed) receives the message with conversation memory and access to its tools
4. For property questions, the agent queries the Supabase vector store (populated from documents synced via Google Drive) to ground its answer in real listing data
5. For leads or bookings, the agent writes to Google Sheets and/or checks and books on Google Calendar
6. The agent replies in Telegram with text, image, or a confirmation message

## Stack

n8n · Telegram · OpenAI (Whisper transcription + chat model) · Google Gemini (embeddings) · Supabase (pgvector) · Google Sheets · Google Calendar · Google Drive · Google Docs · Gmail

## Setup

1. Import `workflow.json` into your n8n instance
2. Reconnect credentials: Telegram Bot API, OpenAI, Google Gemini (PaLM API), Supabase, Google Sheets/Drive/Calendar/Docs OAuth2, Gmail OAuth2
3. Create a Supabase project with the `pgvector` extension enabled and set up a matching table for the vector store node
4. Point the Google Drive trigger at the folder containing your property documents
5. Update the Google Sheets node references to your own listings/leads sheet
6. Activate the workflow and start chatting with your Telegram bot

## Notes

Originally built for a real estate client (Mainland Houses) to handle inbound buyer/renter questions without staff manually checking listings. The RAG architecture (Supabase + Gemini embeddings) was chosen specifically so the bot's answers stay accurate as listings change, without retraining anything — just re-syncing the document store.
