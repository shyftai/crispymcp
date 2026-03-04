---
name: linkedin-prospecting
description: LinkedIn prospecting and lead generation using Crispy MCP tools. Use when the user wants to search LinkedIn for people, companies, or posts, build lead lists, research prospects, find decision-makers, or do competitive research. Triggers include "find leads", "search LinkedIn", "build a prospect list", "research this company", "find people who", "look up this person on LinkedIn", "get their LinkedIn profile", or any task requiring LinkedIn search and discovery.
license: MIT
metadata:
  author: crispy-sh
  version: "1.0.0"
---

# LinkedIn Prospecting with Crispy

Search LinkedIn for people, companies, and content programmatically using Crispy's MCP tools. Build targeted lead lists, research prospects, and find decision-makers.

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

- User asks to find people on LinkedIn (by title, company, location, industry)
- User wants to research a specific person or company
- User needs to build a lead list or prospect list
- User asks to search LinkedIn posts or content
- User wants competitive intelligence on companies
- User asks to "look up" someone on LinkedIn

## Core Tools

| Tool | Purpose | Key Parameters |
|------|---------|---------------|
| `search_people` | Find LinkedIn members by keywords, title, company, location | `keywords`, `title`, `company`, `location`, `limit` |
| `search_companies` | Find companies by name, industry, size | `keywords`, `industry_id`, `company_size` |
| `get_profile` | Get full profile (experience, education, skills) | `account_id`, `profile_url` |
| `get_company_profile` | Get company details (size, industry, description) | `account_id`, `company_url` |
| `search_posts` | Find posts by keyword or author | `account_id`, `keywords`, `author_id` |
| `get_search_parameters` | List valid filter values (industries, regions) | `account_id`, `type` |
| `get_feed` | Get LinkedIn feed posts | `account_id` |
| `get_my_profile` | Get the connected user's own profile | `account_id` |

## Workflow Patterns

### 1. Build a Targeted Lead List

```
Step 1: Use search_people with specific filters
Step 2: For top matches, use get_profile to get full details
Step 3: Present results in a structured table
```

Example prompt flow:
- "Find 20 VP of Engineering at Series B startups in Berlin"
- Search with `title: "VP Engineering"`, `location: "Berlin"`, `limit: 20`
- Enrich top results with `get_profile` for experience and company details
- Format as table: Name | Title | Company | LinkedIn URL

### 2. Research a Prospect Before Outreach

```
Step 1: get_profile for full background
Step 2: search_posts to see their recent activity
Step 3: get_company_profile for their employer
Step 4: Summarize findings for personalized outreach
```

### 3. Competitive Intelligence

```
Step 1: get_company_profile for competitor details
Step 2: search_people to find their team members
Step 3: search_posts for their content strategy
Step 4: Summarize hiring patterns, content themes, growth signals
```

### 4. Content Discovery

```
Step 1: search_posts with industry keywords
Step 2: Analyze engagement patterns
Step 3: Identify trending topics and top voices
```

## Best Practices

1. **Start broad, then narrow.** Use `search_people` with loose filters first, then refine based on results.
2. **Always get full profiles** for your top candidates — the search results are summaries.
3. **Use `get_search_parameters`** to discover valid filter values before searching (industries, regions, company sizes).
4. **Batch requests thoughtfully.** Don't pull 100 full profiles at once — prioritize the most relevant matches.
5. **Respect rate limits.** Pro plan: 500 API calls/day. Team plan: unlimited.
6. **Crispy never stores data.** All results are returned directly to your agent. Store what you need in your own systems.

## Output Format

When presenting search results, use this format:

```
| # | Name | Title | Company | Location | Profile URL |
|---|------|-------|---------|----------|-------------|
| 1 | Jane Smith | VP Engineering | Acme Corp | Berlin | linkedin.com/in/janesmith |
```

For prospect research, structure as:
- **Name & Title** — current role
- **Company** — size, industry, recent news
- **Background** — past roles, education, skills
- **Recent Activity** — posts, engagement patterns
- **Personalization Angles** — shared connections, interests, talking points

## Learn More

- All tools: https://crispy.sh/tools
- Prospecting tools: https://crispy.sh/features/prospecting
- Documentation: https://crispy.sh/docs
