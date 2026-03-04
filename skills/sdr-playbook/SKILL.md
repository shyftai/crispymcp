---
name: sdr-playbook
description: Complete SDR and BDR playbook for AI-powered sales development. Use when the user wants to prospect, build pipeline, run outreach sequences, book meetings, or manage their sales development workflow on LinkedIn. Triggers include "find prospects", "build pipeline", "outreach sequence", "book meetings", "sales development", "SDR workflow", "BDR", "cold outreach", "prospect list", "sales cadence", or any task related to B2B sales development and prospecting.
license: MIT
metadata:
  author: crispy-sh
  version: "1.0.0"
---

# SDR Playbook — AI-Powered Sales Development

A complete sales development workflow: prospect identification, research, multi-touch outreach, objection handling, and meeting booking — all powered by LinkedIn MCP tools.

## Prerequisites

Crispy MCP server must be configured for LinkedIn access:

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

- User asks to find prospects or build a pipeline
- User wants to run an outreach sequence or cadence
- User needs to research accounts before reaching out
- User asks to book meetings or generate leads
- User wants to manage their SDR/BDR workflow
- User mentions cold outreach, prospecting, or sales development

## The SDR Workflow

```
┌─────────────┐    ┌──────────────┐    ┌─────────────┐    ┌──────────────┐    ┌─────────────┐
│  1. Target   │───▶│  2. Research  │───▶│  3. Outreach │───▶│  4. Follow-up│───▶│  5. Book     │
│  Account List│    │  & Qualify    │    │  First Touch │    │  Sequence    │    │  Meeting     │
└─────────────┘    └──────────────┘    └─────────────┘    └──────────────┘    └─────────────┘
```

## Phase 1: Build Your Target Account List

**Goal:** Identify companies that match your ICP (Ideal Customer Profile).

```
Tools: search_companies, get_company_profile
```

### Steps

1. Define your ICP criteria: industry, company size, location, growth signals
2. Use `search_companies` to find matching companies
3. Use `get_company_profile` to validate each company against ICP
4. Score and rank accounts by fit

### ICP Scoring Framework

| Signal | Weight | How to Check |
|--------|--------|-------------|
| Right industry | High | `search_companies` with `industry_id` |
| Right size (headcount) | High | `get_company_profile` → employee count |
| Growth signals (hiring) | Medium | `search_people` for recent job postings |
| Tech stack fit | Medium | Company profile description + website |
| Geographic fit | Low | Company headquarters location |

### Output Format

```
## Target Account List
| # | Company | Industry | Size | Score | Rationale |
|---|---------|----------|------|-------|-----------|
| 1 | Acme Corp | Fintech | 200-500 | A | Series B, hiring 5 engineers, ICP match |
```

## Phase 2: Research & Qualify Prospects

**Goal:** Find the right people at target accounts and gather personalization data.

```
Tools: search_people, get_profile, search_posts, get_company_profile
```

### Steps

1. For each target account, `search_people` for decision-makers and champions
2. `get_profile` on top matches — check title, tenure, background
3. `search_posts` to find their recent LinkedIn activity
4. Build a personalization brief for each prospect

### Who to Target (Decision Matrix)

| Role | Priority | Approach |
|------|----------|----------|
| **Economic buyer** (VP/C-level) | High | Direct value prop, ROI-focused |
| **Champion** (Manager/Director) | High | Problem-aware, show how you solve it |
| **Influencer** (IC/Tech Lead) | Medium | Technical proof, case studies |
| **Gatekeeper** (EA/Chief of Staff) | Low | Respect their role, be concise |

### Prospect Research Brief

For each prospect, compile:

```
## [Name] — [Title] at [Company]
- **LinkedIn:** [URL]
- **Tenure:** [X years in role]
- **Previous:** [Past companies/roles of note]
- **Recent activity:** [Summary of last 3-5 posts or engagement]
- **Personalization hooks:**
  - Posted about [topic] on [date]
  - Previously worked at [company you know]
  - Connected to [mutual connection]
  - Company just [raised funding / launched product / hired for X]
- **Recommended approach:** [Champion / Economic buyer]
- **Opening angle:** [Specific personalization for first touch]
```

## Phase 3: First Touch Outreach

**Goal:** Make a personalized first contact that gets a response.

```
Tools: send_invitation, send_inmail, create_campaign
```

### Channel Selection

| Scenario | Channel | Tool |
|----------|---------|------|
| Not connected, no InMail credits | Connection request + note | `send_invitation` |
| Not connected, have InMail | InMail | `send_inmail` |
| Already connected | Direct message | `start_conversation` |

### Connection Request Framework (max 300 chars)

```
[Observation about them] + [Lightweight reason to connect]
```

Examples:
- "Saw your post on [topic] — sharp insight about [specific point]. Building in the same space and would love to follow your thinking."
- "Noticed [Company] is scaling the [team] — went through the same at [my company]. Happy to share what worked for us."
- "[Mutual connection] mentioned you're exploring [problem area]. We just solved this for [similar company]."

**Rules:**
- No pitch in the connection request. Ever.
- Reference something real and specific
- Keep under 250 characters (leave buffer)
- No links, no "I'd love to add you to my network"

### InMail Framework

```
Subject: [Short, specific, curiosity-driven — under 40 chars]

[1-2 sentences: Observation about them or their company]

[1-2 sentences: Bridge to your relevance]

[1 sentence: Low-commitment ask]
```

### Track Everything

Use `create_campaign` to track your outreach cohort. Tag by account tier, persona, or messaging angle.

## Phase 4: Follow-Up Sequence

**Goal:** Stay top of mind without being annoying. Convert attention into meetings.

```
Tools: list_conversations, get_messages, send_message, get_campaign_stats
```

### Cadence

| Day | Action | Tool |
|-----|--------|------|
| Day 0 | Connection request or InMail | `send_invitation` / `send_inmail` |
| Day 3 | Engage with their content (like/comment) | `react_to_post` / `comment_on_post` |
| Day 5 | Follow-up message (if connected) | `send_message` |
| Day 10 | Value-add message (share relevant insight) | `send_message` |
| Day 17 | Breakup message | `send_message` |

### Follow-Up Message Templates

**Follow-up 1 (Day 5):** Add value, don't ask
```
Thanks for connecting, [Name]. Saw [Company] is [doing X] —
we just published a case study on how [similar company] approached this.
Thought it might be useful: [insight, not link]
```

**Follow-up 2 (Day 10):** Soft ask
```
Quick question — is [specific problem] on your radar this quarter?
We've been helping [type of company] with this and I had a thought
that might be relevant to [Company].
```

**Breakup (Day 17):** Last touch, no guilt
```
[Name] — I'll stop bugging you. If [problem area] ever becomes a priority,
I'm here. Meanwhile, your post about [topic] was great — shared it with my team.
```

### Inbox Management

Use `list_conversations` daily to:
1. Check for responses to outreach
2. Prioritize hot replies (interested, asking questions)
3. Flag objections for handling
4. Track non-responders for follow-up cadence

## Phase 5: Book the Meeting

**Goal:** Convert interested prospects into scheduled calls.

### Meeting Ask Framework

When a prospect responds positively:
1. **Acknowledge** their response specifically
2. **Propose** a specific time (not "when are you free?")
3. **Set expectations** for what the call covers (15-20 min)
4. **Make it easy** — suggest 2-3 specific slots

```
Great to hear [problem] is a priority. Happy to walk through
how [similar company] solved this — takes about 15 minutes.

Would Thursday 2pm or Friday 10am work?
```

### Objection Handling

| Objection | Response Strategy |
|-----------|------------------|
| "Not the right time" | Ask when to reconnect. Set a reminder. |
| "Send me info" | Send a concise 3-bullet summary, then follow up in 3 days. |
| "We already have a solution" | Ask what they'd improve about it. Position as complement. |
| "Talk to [other person]" | Ask for an intro. This is a win — you have a referral. |
| "Not interested" | Thank them. Ask if you can stay connected for future. |

## KPIs to Track

Use `get_campaign_stats` to monitor:

| Metric | Target | Formula |
|--------|--------|---------|
| Connection acceptance rate | 30-40% | Accepted / Sent |
| Reply rate | 15-25% | Replies / Messages sent |
| Positive reply rate | 8-15% | Positive replies / Total replies |
| Meeting book rate | 3-8% | Meetings / Total prospects touched |
| Pipeline generated | Varies | Opportunities created from outreach |

## Daily SDR Routine

```
Morning (30 min):
1. Check inbox — respond to hot replies immediately
2. Review campaign stats — identify what's working
3. Send follow-ups due today

Midday (45 min):
4. Research 5-10 new prospects
5. Send first-touch outreach
6. Engage with target prospects' content (3-5 comments)

End of day (15 min):
7. Update campaign tracking
8. Queue tomorrow's follow-ups
9. Note any objections or insights
```

## Learn More

- Prospecting tools: https://crispy.sh/features/prospecting
- Outreach tools: https://crispy.sh/features/outreach
- Safety Calculator: https://crispy.sh/tools/safety-calculator
- All 43 tools: https://crispy.sh/tools
