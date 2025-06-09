# Guppy Mail

## Product Overview

**Name:** Guppy Mail (TBD if final) **Goal:** Help users stay on top of multiple email distribution lists and never miss important, relevant content (e.g. sales, events, meetups).

## Target Users

### Persona 1: Knowledge Workers

- Overwhelmed by high email volume
- Wants timely, relevant notifications
- Needs help staying engaged in important communities

### Persona 2: Community Moderators / Owners

- Needs visibility into group discussions
- Aims to boost member engagement
- Wants actionable analytics

## How It Works

Guppy Mail is a post-processing system for email that connects to Slack and uses AI to semantically surface relevant content. Users set up a separate inbox to capture distribution list email. Guppy Mail ingests, de-duplicates, embeds, and stores this email for search and proactive alerting.

## MVP Features

- Ingest plain text emails from a dedicated Gmail account via Gmail API or IMAP
- Pre-process: deduplication, formatting normalization
- Semantic embedding using OpenAI
- Store in Pinecone vector DB with metadata (thread ID, timestamp, sender, etc.)
- Slack integration for natural language queries and topic-based notifications
- Rule-based alerts triggered by keyword matches + semantic evaluation
- Basic web dashboard for search, keyword config, and alert management
- Free tier for users; paid tier for list owners with analytics and summaries

## Core Capabilities

1. **Pre-Process:** Deduplicates and normalizes emails
2. **Ingest & Index:** Stores into a vector database for semantic search
3. **Rules Engine:** Uses LLM to semantically match emails to keyword topics
4. **Slack Bot:** Notifies users and allows Q&A via ChatGPT
5. **Dashboard:** Configure interests, review history, and manage settings

## Slack Integration

- **Input:** Users can ask questions or give feedback
- **Output:** Notifications, thread summaries, ChatGPT answers

## Dashboard Features

- Built with Next.js + Supabase or Retool (TBD)
- Google OAuth login
- Manage topics of interest and alert rules
- View matched thread history and top topics
- Toggle Slack alerts on/off per topic

## Onboarding Flow

1. Connect a dedicated email account (suggest throwaway)
2. Add the Guppy Mail Slack bot
3. Guppy Mail begins ingesting messages
4. User defines topics of interest
5. Once ready, Guppy Mail sends a summary of active topics and allows user to opt-in

## Analytics & Success Metrics

### For Knowledge Workers

- Notified Topics Count
- Engagement Rate (click-throughs)
- Estimated Time Saved
- Trending Topics Matched

### For Moderators/Owners

- Policy Violation Alerts
- Top Topics (weekly/monthly)
- Top Contributors
- Engagement Growth Trends

## Architecture Overview

### Core Flow

1. Gmail API or IMAP sync every 10 minutes
2. New emails parsed and chunked (~500 tokens w/ 50-token overlap)
3. Text embedded with OpenAI and stored in Pinecone
4. Full message content stored in S3 or Firestore
5. Slack bot enables semantic query via RAG (retrieval + GPT)
6. Rule-based keyword matcher triggers proactive Slack alerts

### Data Components

- Vector store: Pinecone (cosine distance, namespace per user)
- Metadata: subject, thread ID, sender, timestamp, etc.
- Config store: JSON or Firestore for topics of interest and user settings
- Feedback system: collects input on relevance to improve future matches

## Retention

- Rolling 90-day data window
- Daily cleanup job for expired vectors and messages

## Tech Stack

- Gmail API / IMAP
- OpenAI (embeddings + GPT)
- Pinecone
- Slack bot
- Dashboard: Retool or Next.js + Supabase
- Backend: Python (FastAPI or Flask)
- Firestore or JSON store for config + rule storage

## Future Vision

- Personalized, automatic alerts based on engagement patterns
- Thread reconstruction UI and full web-based message browser
- Premium tools for list owners: summaries, community stats
- Feedback loops and user-driven onboarding growth
- Optional email digests and multi-channel support
