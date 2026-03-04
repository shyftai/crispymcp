---
name: linkedin-recruiter
description: LinkedIn recruiting and talent sourcing using Crispy MCP tools. Use when the user wants to source candidates, send recruiting InMails, manage a hiring pipeline, do boolean candidate searches, research talent pools, or run recruiting outreach on LinkedIn. Triggers include "find candidates", "source engineers", "recruiting", "talent sourcing", "hiring pipeline", "send recruiting InMail", "boolean search candidates", "headhunting", "recruit on LinkedIn", or any task related to recruiting, talent acquisition, or hiring through LinkedIn.
license: MIT
metadata:
  author: crispy-sh
  version: "1.0.0"
---

# LinkedIn Recruiter — AI-Powered Talent Sourcing

Source candidates, build talent pipelines, send personalized recruiting outreach, and manage your hiring process on LinkedIn — all through your AI agent.

## Prerequisites

Crispy MCP server must be configured:

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

- User asks to find candidates for a role
- User wants to source engineers, designers, salespeople, etc.
- User needs to send recruiting InMails or messages
- User wants to build a talent pipeline
- User asks for boolean search help for recruiting
- User wants to research a candidate before an interview

## The Recruiting Workflow

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  1. Define    │───▶│  2. Source    │───▶│  3. Outreach  │───▶│  4. Manage    │
│  Role & ICP   │    │  Candidates   │    │  & Engage     │    │  Pipeline     │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
```

## Phase 1: Define the Ideal Candidate Profile

Before searching, build a clear candidate profile:

```
## Role: [Title]
- Must-have skills: [list]
- Nice-to-have skills: [list]
- Experience level: [years / seniority]
- Industry background: [preferred industries]
- Location: [required / open to remote]
- Company stage preference: [startup / scaleup / enterprise]
- Compensation range: [if known]
- Deal-breakers: [anything that disqualifies]
```

### Sourcing Strategy by Role Type

| Role Type | Primary Search | Secondary Signals |
|-----------|---------------|-------------------|
| **Engineers** | Skills + languages in headline/experience | Open source contributions, tech blog posts |
| **Sales** | Current quota-carrying title + industry | Sales Navigator, revenue mentions in posts |
| **Marketing** | Channel expertise in headline | Content they've published, campaign results |
| **Product** | PM title + domain experience | Product thinking visible in posts |
| **Executive** | Title + company stage + industry | Board roles, speaking engagements, thought leadership |

## Phase 2: Source Candidates

```
Tools: search_people, get_profile, search_companies, get_company_profile, get_search_parameters
```

### Basic Candidate Search

```
Step 1: Use get_search_parameters to find valid filter values
Step 2: search_people with role-specific filters
Step 3: Review results, identify top matches
Step 4: get_profile on promising candidates for deep evaluation
```

### Boolean Search Patterns

Build effective search queries by combining:

| Pattern | Example | Use When |
|---------|---------|----------|
| **Title + Skill** | `title: "Senior Engineer"`, `keywords: "React TypeScript"` | Searching for specific technical roles |
| **Company tier** | Search people at known companies, then find similar profiles | You want candidates from specific caliber companies |
| **Location + Remote** | `location: "Berlin"` or `keywords: "remote"` | Geographic requirements |
| **Seniority ladder** | Search "Staff Engineer" then also "Principal Engineer", "Tech Lead" | Title varies across companies |

### Candidate Evaluation Framework

For each promising candidate, pull `get_profile` and evaluate:

```
## Candidate: [Name]
- **Current role:** [Title] at [Company] ([tenure])
- **Relevance score:** [1-5]

### Must-haves
- [ ] [Skill 1]: [Evidence from profile]
- [ ] [Skill 2]: [Evidence from profile]
- [ ] [Experience level]: [Years / progression]

### Nice-to-haves
- [ ] [Skill 3]: [Evidence]
- [ ] [Industry background]: [Evidence]

### Signals
- Career trajectory: [Up / Lateral / Stagnant]
- Tenure pattern: [Stable / Job hopper / Normal]
- Activity level: [Active poster / Passive / Ghost]
- Open to opportunities: [If visible]

### Personalization notes
- [Recent post about X]
- [Went to same university as hiring manager]
- [Previously worked at company we know]

### Verdict: [Reach out / Maybe / Pass]
```

### Build a Talent Map

For strategic hiring, map the entire talent landscape:

```
Step 1: Identify 5-10 companies known for strong [role] talent
Step 2: get_company_profile for each — understand size, growth, culture
Step 3: search_people at each company for the target role
Step 4: Build a map of where talent sits

## Talent Map: Senior Frontend Engineers — Berlin
| Company | Team Size (est.) | Notable People | Notes |
|---------|-----------------|----------------|-------|
| Acme Corp | ~15 FE engineers | Jane S. (Staff), John D. (Senior) | Series C, might have retention issues |
| Beta GmbH | ~8 FE engineers | Sarah K. (Lead) | Just laid off 10%, talent may be available |
```

## Phase 3: Recruiting Outreach

```
Tools: send_invitation, send_inmail, send_message, start_conversation, create_campaign
```

### Channel Selection

| Scenario | Best Channel | Tool |
|----------|-------------|------|
| Not connected, no InMail credits | Connection request with recruiting note | `send_invitation` |
| Not connected, have InMail | InMail | `send_inmail` |
| Already connected | Direct message | `send_message` |
| Referred by someone | Connection request mentioning referrer | `send_invitation` |

### Recruiting Message Framework

**Connection request (max 300 chars):**
```
Hi [Name] — I'm hiring for a [Role] at [Company] and your background
in [specific skill/experience] stood out. Would love to connect
and share more if you're open to it.
```

**InMail:**
```
Subject: [Role] at [Company] — your [specific thing] caught my eye

Hi [Name],

I'm [Your name], [your role] at [Company]. We're building [what you're building]
and I came across your profile — your work on [specific project/skill] at
[their company] is exactly the background we're looking for.

We're hiring a [Role] to [key responsibility]. The team is [size], the stack is
[tech], and we're at [stage/funding].

Would you be open to a quick chat? Even if the timing isn't right,
happy to stay connected for the future.

[Your name]
```

### What Makes Recruiting Messages Work

**DO:**
- Reference something specific from their profile (not just their title)
- Lead with the opportunity, not your company's life story
- Be transparent about the role, team, and stage
- Make it easy to say yes to a conversation (not a commitment)
- Respect their time — keep it under 150 words

**DON'T:**
- "I came across your impressive profile" (generic, everyone says this)
- Send the same message to 50 people
- Hide the company name
- Oversell — let the opportunity speak for itself
- Follow up more than twice if no response

### Outreach Sequence

| Day | Action | Tool |
|-----|--------|------|
| Day 0 | InMail or connection request | `send_inmail` / `send_invitation` |
| Day 3 | Engage with their content (if they post) | `react_to_post` / `comment_on_post` |
| Day 7 | Follow-up message (shorter, add new info) | `send_message` |
| Day 14 | Final touch (respect their decision) | `send_message` |

### Track Campaigns

Use `create_campaign` per role to track outreach:

```
Campaign: "Senior FE Engineer — Berlin — Q1 2026"
- Candidates sourced: 40
- Outreach sent: 25
- Replies: 12 (48%)
- Interested: 7 (28%)
- Screens scheduled: 5
- Moved to interview: 3
```

## Phase 4: Pipeline Management

```
Tools: list_conversations, get_messages, get_campaign_stats, send_message
```

### Daily Recruiting Routine

```
Morning (20 min):
1. Check inbox for candidate replies — respond immediately to interested candidates
2. Review campaign stats — which messages are working?

Midday (40 min):
3. Source 5-10 new candidates for open roles
4. Send personalized outreach
5. Engage with target candidates' content

End of day (15 min):
6. Follow up with candidates in pipeline
7. Update pipeline status
8. Flag candidates ready for hiring manager review
```

### Pipeline Report

```
## Recruiting Pipeline — [Role] — Week of [Date]

### Funnel
- Sourced: 40
- Outreach sent: 25
- Replied: 12 (48% response rate)
- Interested: 7
- Screen scheduled: 5
- Interviewing: 3
- Offer stage: 1

### This Week's Activity
- New candidates sourced: 8
- InMails sent: 6
- Follow-ups sent: 4
- Screens completed: 2

### Top Candidates
| Name | Current Role | Status | Next Step | Notes |
|------|-------------|--------|-----------|-------|
| Jane S. | Staff Eng @ Acme | Screen done | HM interview Thu | Strong systems design |
| John D. | Senior Eng @ Beta | Replied interested | Schedule screen | Ex-Google, React expert |

### Message Performance
- Connection request acceptance: 62%
- InMail reply rate: 44%
- Best performing hook: "[specific project] caught my eye"
```

## Diversity Sourcing

### Expanding Your Talent Pool

1. **Search beyond obvious titles.** "Software Engineer" misses "Developer", "Programmer", "SWE", "Full Stack", etc.
2. **Look at non-traditional backgrounds.** Bootcamp grads, career changers, self-taught developers.
3. **Broaden company targets.** Don't just source from FAANG — look at agencies, consultancies, startups.
4. **Check communities.** Search for posts mentioning diversity groups, ERGs, community leadership.
5. **Vary your search terms.** Different demographics may describe the same skills differently.

### Reducing Bias in Evaluation

- Focus on skills and impact, not pedigree
- Use the same evaluation framework for every candidate
- Look at career trajectory, not just current title
- Consider adjacent experience that transfers

## Learn More

- Prospecting tools: https://crispy.sh/features/prospecting
- Outreach tools: https://crispy.sh/features/outreach
- All 43 tools: https://crispy.sh/tools
- Safety Calculator: https://crispy.sh/tools/safety-calculator
