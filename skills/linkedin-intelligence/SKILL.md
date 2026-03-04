---
name: linkedin-intelligence
description: LinkedIn analytics and intelligence using Crispy MCP tools. Use when the user wants to track LinkedIn post performance, monitor profile views, analyze engagement metrics, track network growth, get audience insights, or do competitive analysis. Triggers include "how are my posts doing", "who viewed my profile", "post analytics", "engagement rate", "LinkedIn metrics", "track performance", "analyze my LinkedIn", "competitive analysis", or any task requiring LinkedIn data analysis and reporting.
license: MIT
metadata:
  author: crispy-sh
  version: "1.0.0"
---

# LinkedIn Intelligence with Crispy

Track post performance, profile analytics, network growth, and competitive intelligence using Crispy's MCP tools. Build dashboards and reports from live LinkedIn data.

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

- User asks about their LinkedIn post performance
- User wants to know who viewed their profile
- User needs engagement metrics or analytics
- User wants to compare their performance over time
- User asks for competitive intelligence on competitors' LinkedIn activity
- User wants a LinkedIn performance report or dashboard

## Core Tools

| Tool | Purpose | Key Parameters |
|------|---------|---------------|
| `get_post_analytics` | Detailed metrics for a specific post | `account_id`, `post_id` |
| `get_cached_post_analytics` | Fast cached analytics (lower API cost) | `account_id`, `post_id` |
| `get_profile_analytics` | Profile-level metrics (views, search appearances) | `account_id` |
| `get_activity_analytics` | Activity summary across all content | `account_id` |
| `get_profile_viewers` | Who viewed your profile recently | `account_id` |
| `get_connections` | List connections with details | `account_id`, `limit` |
| `get_top_posts` | Best-performing posts ranked | `account_id`, `limit` |
| `purge_analytics_cache` | Clear cached data for fresh metrics | `account_id` |

## Workflow Patterns

### 1. Weekly Performance Report

```
Step 1: get_activity_analytics for overall metrics
Step 2: get_top_posts (limit: 10) for best performers
Step 3: For top 3 posts, get_post_analytics for detailed breakdown
Step 4: get_profile_analytics for profile-level data
Step 5: get_profile_viewers to identify warm leads
Step 6: Compile into formatted report
```

### 2. Post-by-Post Analysis

```
Step 1: list_posts to get recent posts
Step 2: get_post_analytics on each post
Step 3: Calculate engagement rates (reactions + comments / impressions)
Step 4: Identify patterns: best topics, formats, posting times
Step 5: Present ranking with actionable insights
```

### 3. Profile Viewer Intelligence

```
Step 1: get_profile_viewers for recent visitors
Step 2: Cross-reference viewers with ideal customer profile
Step 3: For hot leads, get_profile for full details
Step 4: Prioritize for outreach (use linkedin-outreach skill)
```

### 4. Competitive Intelligence

```
Step 1: list_posts for competitor profiles
Step 2: Analyze posting frequency, topics, engagement
Step 3: Compare against user's own metrics
Step 4: Identify content gaps and opportunities
Step 5: Recommend strategy adjustments
```

### 5. Network Growth Tracking

```
Step 1: get_connections for current network
Step 2: get_profile_analytics for search appearances
Step 3: Correlate with outreach campaigns
Step 4: Identify which activities drive the most growth
```

## Key Metrics to Track

### Post Metrics
| Metric | What It Measures | Benchmark |
|--------|-----------------|-----------|
| Impressions | Total views | Varies by network size |
| Engagement rate | (Reactions + Comments + Shares) / Impressions | 2-5% good, 5%+ excellent |
| Comment rate | Comments / Impressions | 0.5-1% good |
| Click-through rate | Link clicks / Impressions | 1-3% good |
| Dwell time | Average time spent on post | Higher = better distribution |

### Profile Metrics
| Metric | What It Measures | Benchmark |
|--------|-----------------|-----------|
| Profile views | Weekly visitors | Trending up = good |
| Search appearances | Found in LinkedIn search | Correlates with SEO quality |
| Connection growth | Net new connections/week | Depends on outreach volume |

## Analysis Framework

When analyzing content performance, evaluate:

1. **What topics resonate?** — Group posts by topic, compare engagement rates.
2. **What formats work?** — Text vs. list vs. story vs. contrarian take.
3. **When is the audience active?** — Compare metrics by day of week and time.
4. **What drives comments vs. reactions?** — Comments signal deeper engagement.
5. **Who engages most?** — Profile your most active audience members.

## Data Freshness

- **Live analytics** (`get_post_analytics`): Real-time data from LinkedIn. Each call counts as 1 API call.
- **Cached analytics** (`get_cached_post_analytics`): Cached for performance. Use for dashboards and repeated queries.
- **Purge cache** (`purge_analytics_cache`): Clear cache when you need fresh data for a specific report.

Use cached analytics for routine monitoring, live analytics for important reports.

## Output Format

### Performance Report

```
## LinkedIn Performance Report — Week of [Date]

### Summary
- Impressions: 12,450 (+18% vs. last week)
- Engagement rate: 4.3% (avg)
- Profile views: 234 (+12%)
- New connections: 28

### Top Posts
| Post | Published | Impressions | Engagement | Comments |
|------|-----------|------------|------------|----------|
| "3 things I learned..." | Mon | 4,200 | 5.8% | 34 |
| "Hot take: AI won't..." | Wed | 3,800 | 4.9% | 28 |

### Profile Viewers (Potential Leads)
| Name | Title | Company | Action |
|------|-------|---------|--------|
| Jane Smith | VP Sales | Acme Corp | Consider outreach |

### Recommendations
1. Story-style posts outperform lists by 40% — publish more narratives
2. Wednesday 8 AM posts get 2x the impressions — shift posting schedule
3. 3 profile viewers match ICP — send connection requests
```

## Learn More

- All tools: https://crispy.sh/tools
- Analytics tools: https://crispy.sh/features/intelligence
- Documentation: https://crispy.sh/docs
