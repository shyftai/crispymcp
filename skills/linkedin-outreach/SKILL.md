---
name: linkedin-outreach
description: LinkedIn outreach and messaging using Crispy MCP tools. Use when the user wants to send LinkedIn messages, connection requests, InMails, manage conversations, run outreach campaigns, or handle their LinkedIn inbox. Triggers include "send a message on LinkedIn", "connect with this person", "send connection request", "InMail", "outreach campaign", "reply to LinkedIn messages", "check my inbox", "follow up with", or any task requiring LinkedIn messaging and relationship building.
license: MIT
metadata:
  author: crispy-sh
  version: "1.0.0"
---

# LinkedIn Outreach with Crispy

Send personalized messages, connection requests, and InMails programmatically using Crispy's MCP tools. Manage conversations and run multi-step outreach campaigns.

## Prerequisites

Crispy MCP server must be configured. Add to your MCP client config:

```json
{
  "mcpServers": {
    "crispy": {
      "url": "https://crispy.sh/api/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

Get your API key at https://crispy.sh/dashboard/api-keys

## When to Apply

- User asks to send a LinkedIn message or connection request
- User wants to run an outreach campaign
- User needs to check or manage their LinkedIn inbox
- User wants to follow up with prospects
- User asks to send InMails to non-connections
- User wants to create or manage LinkedIn campaigns

## Core Tools

| Tool | Purpose | Key Parameters |
|------|---------|---------------|
| `send_message` | Send a message to a connection | `account_id`, `conversation_id`, `text` |
| `send_invitation` | Send a connection request with note | `account_id`, `profile_url`, `message` |
| `send_inmail` | Send InMail to non-connections | `account_id`, `profile_url`, `subject`, `body` |
| `start_conversation` | Start a new message thread | `account_id`, `profile_url`, `text` |
| `get_messages` | Read messages in a conversation | `account_id`, `conversation_id` |
| `list_conversations` | List all conversations | `account_id`, `limit` |
| `create_campaign` | Create an outreach campaign | `account_id`, `name`, `description` |
| `list_campaigns` | List existing campaigns | `account_id` |
| `archive_campaign` | Archive a completed campaign | `account_id`, `campaign_id` |
| `get_campaign_stats` | Get campaign performance metrics | `account_id`, `campaign_id` |

## Workflow Patterns

### 1. Personalized Connection Request

```
Step 1: Use get_profile to research the prospect
Step 2: Identify personalization angles (shared connections, recent posts, mutual interests)
Step 3: Craft a personalized connection note (max 300 chars)
Step 4: Send via send_invitation
```

Example:
- Research prospect with `get_profile`
- Note their recent post about AI
- Send: "Hi [Name], loved your take on AI in fintech — especially the point about regulatory challenges. I'm building in the same space and would love to connect."

### 2. Inbox Triage and Response

```
Step 1: list_conversations to see recent threads
Step 2: get_messages on priority conversations
Step 3: Draft and send replies based on context
Step 4: Flag important threads for the user
```

### 3. Multi-Step Outreach Sequence

```
Step 1: Search for prospects (use linkedin-prospecting skill)
Step 2: Create a campaign with create_campaign
Step 3: Send connection requests with personalized notes
Step 4: After acceptance, send follow-up message
Step 5: Track results with get_campaign_stats
```

### 4. Follow-Up Campaign

```
Step 1: list_conversations to find unanswered threads
Step 2: Identify conversations older than N days without reply
Step 3: Draft contextual follow-up messages
Step 4: Send follow-ups via send_message
```

## Message Writing Guidelines

### Connection Requests (max 300 characters)
- Lead with something specific about them (not about you)
- No "I'd love to add you to my network" — be genuine
- One clear reason to connect
- No links, no pitches

### First Messages
- Reference something specific (their post, company news, shared connection)
- Keep under 3 short paragraphs
- End with a low-commitment ask (question, not a meeting request)
- Write like a human, not a template

### Follow-Ups
- Reference the previous message
- Add new value (insight, resource, relevant news)
- Keep shorter than the original message
- Wait 3-5 business days between follow-ups

## Safety Guidelines

1. **Respect LinkedIn's daily limits.** ~100 connection requests/day, ~50-100 messages/day for established accounts.
2. **Ramp up gradually.** New accounts should start with 10-20 requests/day and increase over weeks.
3. **Personalize every message.** Bulk generic outreach gets flagged. Use prospect data to personalize.
4. **Don't spam.** If someone doesn't respond after 2 follow-ups, stop.
5. **Use the Safety Calculator** at https://crispy.sh/tools/safety-calculator to check your account's safe limits.
6. **Crispy never stores messages.** All content is sent directly through LinkedIn. Nothing is retained.

## Output Format

When reporting on outreach activities:

```
## Outreach Summary
- Connection requests sent: 15
- Messages sent: 8
- Follow-ups sent: 3
- Pending responses: 12

### Sent Today
| Prospect | Action | Message Preview |
|----------|--------|----------------|
| Jane Smith (VP Eng, Acme) | Connection request | "Loved your post about..." |
```

## Learn More

- All tools: https://crispy.sh/tools
- Outreach tools: https://crispy.sh/features/outreach
- Safety Calculator: https://crispy.sh/tools/safety-calculator
- Documentation: https://crispy.sh/docs
