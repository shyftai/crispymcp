---
name: sales-navigator
description: LinkedIn Sales Navigator automation using Crispy MCP tools. Use when the user has Sales Navigator and wants to leverage advanced search filters, saved leads, account lists, lead recommendations, boolean search, or Sales Nav-specific features through their AI agent. Triggers include "Sales Navigator", "Sales Nav", "advanced search", "saved leads", "lead list", "boolean search LinkedIn", "account list", "sales nav filters", "InMail credits", "lead recommendations", or any task that references LinkedIn Sales Navigator features.
license: MIT
metadata:
  author: crispy-sh
  version: "1.0.0"
---

# Sales Navigator with Crispy

Unlock the full power of LinkedIn Sales Navigator through your AI agent. Advanced filters, boolean search, lead management, and InMail outreach — all programmatic, all through MCP.

## Prerequisites

1. A LinkedIn account with **Sales Navigator** subscription (Core, Advanced, or Advanced Plus)
2. Crispy MCP server configured:

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

Crispy automatically detects your Sales Navigator subscription and unlocks advanced filters. No extra configuration needed.

## When to Apply

- User mentions Sales Navigator or Sales Nav
- User wants to use advanced search filters (seniority, company size, revenue, technologies)
- User asks for boolean search on LinkedIn
- User wants to manage saved leads or account lists
- User asks to send InMails
- User wants lead recommendations or buyer intent signals

## What Sales Navigator Unlocks

| Feature | Regular LinkedIn | With Sales Navigator |
|---------|-----------------|---------------------|
| Search filters | Basic (title, company, location) | 30+ advanced filters |
| Search results | Limited to ~100 | Up to 2,500 per search |
| Profile views | Shows you viewed | Anonymous browsing option |
| InMail | None (unless Premium) | 50/month (Core), 150/month (Advanced) |
| Saved leads | Not available | Up to 10,000 |
| Account lists | Not available | Up to 5,000 accounts |
| Buyer intent | Not available | Available on Advanced+ |
| TeamLink | Not available | See team's network |

## Core Tools for Sales Navigator

| Tool | Sales Nav Enhancement |
|------|----------------------|
| `search_people` | Advanced filters: seniority, function, company size, revenue, years in role, years at company, groups, schools |
| `search_companies` | Advanced filters: revenue, headcount growth, department size, technologies used, funding events |
| `get_profile` | Full profile data including mutual connections and TeamLink paths |
| `send_inmail` | Use your InMail credits to reach non-connections directly |
| `get_search_parameters` | Discover all available Sales Nav filter values |

## Advanced Search Patterns

### People Search with Sales Nav Filters

Sales Navigator adds powerful filters beyond basic LinkedIn search:

```
search_people with Sales Nav filters:

Seniority filters:
- seniority: "CXO" | "VP" | "Director" | "Manager" | "Senior" | "Entry"

Function filters:
- function: "Engineering" | "Sales" | "Marketing" | "Operations" | "Finance" | "HR"

Company filters:
- company_size: "1-10" | "11-50" | "51-200" | "201-500" | "501-1000" | "1001-5000" | "5001-10000" | "10001+"
- company_type: "Public" | "Private" | "Nonprofit" | "Government" | "Education"

Tenure filters:
- years_in_current_role: filter by how long in current position
- years_at_current_company: filter by company tenure
- years_of_experience: filter by total career experience

Other:
- groups: LinkedIn group memberships
- schools: Education background
- posted_on_linkedin: "Past 30 days" — people who actively post
- changed_jobs: "Past 90 days" — people who recently moved
```

### Boolean Search Mastery

Sales Navigator supports full boolean operators in keyword searches:

| Operator | Syntax | Example |
|----------|--------|---------|
| **AND** | `term1 AND term2` | `"product manager" AND "B2B SaaS"` |
| **OR** | `term1 OR term2` | `"VP Engineering" OR "CTO" OR "Head of Engineering"` |
| **NOT** | `NOT term` | `"software engineer" NOT "junior" NOT "intern"` |
| **Quotes** | `"exact phrase"` | `"machine learning"` |
| **Parentheses** | `(group)` | `("VP" OR "Director") AND "Sales" NOT "Assistant"` |

### Search Recipes

**Find decision-makers at mid-market SaaS companies:**
```
keywords: ("VP" OR "Director" OR "Head of") AND "Engineering"
company_size: "201-500"
industry: "Software" OR "SaaS"
seniority: "VP", "Director"
```

**Find recently promoted leaders (likely to buy):**
```
keywords: [your ICP title]
changed_jobs: "Past 90 days"
seniority: "Director", "VP", "CXO"
company_size: "51-200", "201-500"
```

**Find active posters in your niche (warm prospects):**
```
keywords: [your industry terms]
posted_on_linkedin: "Past 30 days"
seniority: "Manager", "Director", "VP"
function: [target function]
```

**Find champions who moved to new companies:**
```
keywords: [name or title of past champions]
changed_jobs: "Past 90 days"
```
This is gold — past champions at new companies are the warmest leads.

### Company Search with Sales Nav Filters

```
search_companies with Sales Nav filters:

- revenue: filter by annual revenue range
- headcount_growth: growing, shrinking, or stable
- department_size: size of specific departments
- technologies: tech stack the company uses
- funding_events: recently funded companies
- fortune: Fortune 500/1000 membership
```

**Find companies investing in your space:**
```
keywords: [your market]
headcount_growth: "Growing"
department_size: [relevant department] > 10
technologies: [related tech]
```

## Sales Navigator Workflows

### 1. Build a Saved Lead List from Scratch

```
Step 1: Define your ICP using Sales Nav filters
Step 2: Run search_people with advanced filters
Step 3: Review and qualify top results with get_profile
Step 4: Present qualified leads in structured format
Step 5: User saves to Sales Nav lead list manually (or continues in CRM)
```

### 2. Account-Based Search

```
Step 1: Start with target account list (company names)
Step 2: search_companies to get company profiles
Step 3: For each account, search_people with company + title filters
Step 4: Map the buying committee:
        - Economic buyer (VP/C-level who signs)
        - Champion (Director/Manager who advocates)
        - Influencer (IC who evaluates)
        - Blocker (Procurement, Legal — know who to navigate)
Step 5: Build multi-threaded outreach plan
```

**Output format:**
```
## Account: Acme Corp (Series C, 350 employees, Fintech)

### Buying Committee
| Role | Name | Title | LinkedIn | Approach |
|------|------|-------|----------|---------|
| Economic Buyer | Jane S. | VP Engineering | /in/janes | ROI-focused, reference [company] |
| Champion | Tom B. | Engineering Manager | /in/tomb | Pain-aware, recently posted about [problem] |
| Influencer | Sarah K. | Staff Engineer | /in/sarahk | Technical evaluation, share case study |
| Blocker | Mike L. | Head of Procurement | /in/mikel | Keep informed, don't surprise |
```

### 3. InMail Campaign

```
Tools: send_inmail, get_campaign_stats, list_conversations
```

InMail is your most valuable Sales Nav asset. Use it wisely.

**When to use InMail vs. connection request:**

| Scenario | Use |
|----------|-----|
| High-value prospect, time-sensitive | InMail |
| Long-term relationship building | Connection request |
| They post actively (warm signal) | Comment first, then connect |
| No mutual connections | InMail |
| Mutual connections exist | Ask for intro first |

**InMail best practices:**
- Subject line under 40 characters — curiosity-driven, not salesy
- Body under 100 words — respect their time
- Reference something specific (their post, company news, mutual connection)
- One clear ask (not "let me know if you'd like to chat sometime")
- Don't waste InMails on people you can reach through connection requests

**InMail budget planning:**

| Plan | Monthly InMails | Strategy |
|------|----------------|----------|
| Core (50/mo) | Reserve for top-tier prospects only. ~2-3/day. |
| Advanced (150/mo) | Tier prospects: Top 50 get InMail, rest get connection requests. ~5-7/day. |

### 4. Intent-Based Prospecting

Sales Navigator signals that indicate buying intent:

| Signal | What It Means | How to Find |
|--------|--------------|-------------|
| **Job change** | New leaders have budget + mandate to change things | `changed_jobs: "Past 90 days"` filter |
| **Company growth** | Growing companies invest in tools | `headcount_growth: "Growing"` filter |
| **Active posting** | Engaged users respond more to outreach | `posted_on_linkedin: "Past 30 days"` filter |
| **Profile views** | They looked at you — warmest signal possible | `get_profile_viewers` |
| **Funding event** | New money = new budget | `funding_events` company filter |
| **Technology adoption** | Using adjacent tools = likely need yours | `technologies` company filter |

**Intent-based outreach workflow:**
```
Step 1: Search with intent signals (job change + seniority + company size)
Step 2: get_profile to confirm fit and find personalization
Step 3: Craft message referencing the intent signal:
        "Congrats on the move to [Company]! When I joined a new team,
         [problem you solve] was one of the first things I tackled..."
Step 4: Send via InMail (high intent = worth the InMail credit)
```

### 5. TeamLink Warm Introductions

If you're on Sales Navigator Advanced, TeamLink shows connections your team has to prospects.

```
Step 1: search_people for target prospects
Step 2: Check for TeamLink connections in profile data
Step 3: If a teammate is connected, ask for an introduction
Step 4: If no TeamLink path, use InMail or connection request
```

Warm intros via TeamLink have 3-5x higher response rates than cold InMail.

## Daily Sales Nav Routine

```
Morning (30 min):
1. Check profile viewers — respond to any ICP visitors
2. Review inbox for InMail replies
3. Send follow-ups on active conversations

Midday (45 min):
4. Run targeted search with intent filters
5. Qualify top 10 results with get_profile
6. Send 3-5 InMails to highest-intent prospects
7. Send 10-15 connection requests to qualified prospects

End of day (15 min):
8. Engage with 5-10 prospect posts (comments, reactions)
9. Review campaign performance
10. Plan tomorrow's search focus
```

## InMail Templates

**New Job Signal:**
```
Subject: Quick thought on [their new challenge]

Hi [Name], congrats on the move to [Company].

When I started a similar role, [specific challenge] was top of mind.
We just helped [similar company] cut [metric] by [result] — thought
it might be relevant as you're ramping up.

Worth a 15-min chat to see if it applies?
```

**Company Growth Signal:**
```
Subject: [Company]'s growth + [your solution area]

Hi [Name], noticed [Company] has been scaling [department] fast —
[X new hires in Y months].

Fast-growing teams at [similar company] and [similar company] have
been using [your approach] to [solve problem without slowing down].

Happy to share what's working for them if useful.
```

**Shared Connection:**
```
Subject: [Mutual connection] suggested I reach out

Hi [Name], [mutual connection name] mentioned you're exploring
[problem area]. We helped them [specific result] and they
thought it could be relevant for [Company] too.

Would you be open to a quick call this week?
```

## Metrics to Track

| Metric | Target | How |
|--------|--------|-----|
| InMail open rate | 40-60% | Subject line quality |
| InMail reply rate | 15-25% | Message relevance + personalization |
| InMail-to-meeting rate | 5-10% | Qualification + timing |
| Connection acceptance | 30-50% | Note quality + profile strength |
| Search-to-qualified ratio | 20-30% | Filter precision |
| InMails remaining | Track weekly | Budget management |

## Learn More

- Prospecting tools: https://crispy.sh/features/prospecting
- Outreach tools: https://crispy.sh/features/outreach
- All 43 tools: https://crispy.sh/tools
- Safety Calculator: https://crispy.sh/tools/safety-calculator
