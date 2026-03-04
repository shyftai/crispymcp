---
name: competitor-research
description: Competitive intelligence and market research using LinkedIn data via Crispy MCP tools. Use when the user wants to research competitors, track hiring trends, analyze competitor content strategy, map competitor org charts, monitor market movements, or gather intelligence on companies. Triggers include "research competitor", "competitive analysis", "who are they hiring", "competitor content", "market research", "company intelligence", "track competitor", "org chart", "competitive landscape", or any task requiring business intelligence gathered from LinkedIn.
license: MIT
metadata:
  author: crispy-sh
  version: "1.0.0"
---

# Competitor Research with LinkedIn Intelligence

Gather competitive intelligence from LinkedIn — hiring signals, org structure, content strategy, team growth, and market positioning. Turn public LinkedIn data into strategic insights.

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

- User asks to research a competitor
- User wants to know what competitors are hiring for
- User asks to analyze a competitor's content or LinkedIn presence
- User wants to map a company's org structure
- User needs market or competitive landscape analysis
- User asks about hiring trends in their industry

## Intelligence Categories

```
┌────────────────────────────────────────────────────────────────┐
│                    COMPETITOR INTELLIGENCE                      │
├────────────────┬─────────────────┬──────────────┬─────────────┤
│  1. COMPANY    │  2. PEOPLE      │  3. CONTENT  │  4. SIGNALS │
│                │                 │              │             │
│  Profile       │  Org chart      │  Posts       │  Hiring     │
│  Size & growth │  Key hires      │  Topics      │  Departures │
│  Industry      │  Team structure │  Engagement  │  Pivots     │
│  Description   │  Backgrounds    │  Frequency   │  Expansion  │
├────────────────┼─────────────────┼──────────────┼─────────────┤
│ get_company_   │ search_people   │ search_posts │ All of the  │
│ profile        │ get_profile     │ list_posts   │ above       │
│ search_        │                 │ get_post     │ combined    │
│ companies      │                 │              │             │
└────────────────┴─────────────────┴──────────────┴─────────────┘
```

## Research Workflows

### Workflow 1: Full Competitor Deep Dive

The comprehensive analysis covering all intelligence categories.

```
Step 1: get_company_profile — size, industry, description, HQ
Step 2: search_people at the company — map the org
Step 3: get_profile on key leaders — backgrounds, tenure, trajectory
Step 4: search_posts from company employees — content strategy
Step 5: Analyze hiring patterns — what roles are open, what teams are growing
Step 6: Synthesize into intelligence report
```

### Workflow 2: Hiring Signal Analysis

What a company hires for tells you what they're building next.

```
Tools: search_people, get_profile, get_company_profile
```

```
Step 1: get_company_profile for baseline size
Step 2: search_people with recent tenure (joined < 6 months)
Step 3: Categorize new hires by department
Step 4: Identify patterns: which teams are growing fastest?
Step 5: Infer strategic direction from hiring patterns
```

**Signal interpretation:**

| Hiring Pattern | What It Means |
|---------------|---------------|
| Many engineers hired | Building new product or scaling existing |
| Sales team growing | Entering growth phase, new market push |
| First enterprise sales hires | Moving upmarket |
| Data/ML hires | AI/ML product investment |
| International hires | Geographic expansion |
| New C-level | Strategic shift, possibly new direction |
| Hiring paused | Cash conservation, potential trouble |
| Key departures | Culture issues, strategy disagreements, or acqui-hires |

### Workflow 3: Org Chart Mapping

Understand who does what and how teams are structured.

```
Tools: search_people, get_profile
```

```
Step 1: search_people at [Company] with various title filters
Step 2: Group by department (Engineering, Sales, Marketing, Product, etc.)
Step 3: get_profile on leaders to understand reporting structure
Step 4: Map the hierarchy

## [Company] — Org Structure

### Leadership
- CEO: [Name] (ex-[Company], [background])
- CTO: [Name] (joined [date], ex-[Company])
- VP Sales: [Name] (joined [date])

### Engineering (~45 people)
- [Name] — VP Engineering
  - [Name] — Engineering Manager, Backend
  - [Name] — Engineering Manager, Frontend
  - [Name] — Staff Engineer (ML)

### Sales (~20 people)
- [Name] — VP Sales
  - [Name] — Sales Director, Enterprise
  - [Name] — Sales Director, SMB
```

### Workflow 4: Content Strategy Analysis

Understand what competitors talk about and what resonates with their audience.

```
Tools: search_posts, list_posts, get_post
```

```
Step 1: Identify competitor's key voices (CEO, marketing, sales leaders)
Step 2: list_posts for each voice (last 20-30 posts)
Step 3: Categorize posts by topic, format, tone
Step 4: Analyze engagement patterns
Step 5: Identify their messaging strategy and gaps
```

```
## [Company] Content Strategy Analysis

### Key Voices
| Person | Role | Post Frequency | Avg Engagement | Primary Topics |
|--------|------|---------------|----------------|---------------|
| [CEO] | CEO | 3x/week | 4.2% | Vision, culture, fundraising |
| [VP Mktg] | VP Marketing | 2x/week | 2.8% | Product launches, case studies |
| [AE] | Sr AE | 1x/week | 5.1% | Sales tips, customer stories |

### Topic Distribution
- Product updates: 30%
- Industry insights: 25%
- Culture / hiring: 20%
- Customer stories: 15%
- Thought leadership: 10%

### What's Working for Them
- [Topic] posts get 2x average engagement
- Personal stories from [CEO] outperform product posts
- They avoid [topic] — potential gap

### What's NOT Working
- Product launch posts get minimal engagement
- [Topic] posts underperform despite frequency

### Opportunities for Us
1. They don't cover [topic] — we can own this
2. Their [audience segment] is underserved
3. Their tone is [corporate/formal] — we can differentiate with [authentic/casual]
```

### Workflow 5: Market Landscape Mapping

Map all competitors in a space, not just one.

```
Tools: search_companies, get_company_profile, search_people
```

```
Step 1: search_companies with industry keywords
Step 2: get_company_profile for each relevant result
Step 3: Build landscape map with positioning, size, and differentiators
Step 4: Identify whitespace and opportunities
```

```
## Competitive Landscape — [Market]

| Company | Size | HQ | Positioning | Funding | Key Differentiator |
|---------|------|-----|------------|---------|-------------------|
| Acme | 201-500 | Berlin | Enterprise platform | Series C | Compliance focus |
| Beta | 51-200 | NYC | SMB self-serve | Series A | Easy setup |
| Gamma | 11-50 | London | Agency tool | Bootstrapped | Multi-client |
| Us | [size] | [HQ] | [positioning] | [stage] | [differentiator] |

### Market Gaps
1. No one is serving [segment] well
2. [Feature/approach] is underexplored
3. [Region] is wide open
```

## Analysis Frameworks

### SWOT from LinkedIn Data

| | Positive | Negative |
|--|---------|----------|
| **Internal** | **Strengths:** Strong engineering team (8 Staff+ engineers), active content presence, CEO is industry voice | **Weaknesses:** Small sales team, no enterprise sales leader, slow hiring pace |
| **External** | **Opportunities:** Expanding into [market], [competitor] just laid off talent, [trend] is accelerating | **Threats:** [Big company] entering space, [competitor] raised $50M, talent war in [city] |

### Competitive Moat Assessment

| Moat Type | Evidence from LinkedIn | Strength |
|-----------|----------------------|----------|
| **Talent** | # of senior engineers, backgrounds, tenure | Strong / Weak |
| **Network effects** | Customer mentions, partner posts, ecosystem | Strong / Weak |
| **Brand** | Follower count, engagement rates, thought leadership | Strong / Weak |
| **Speed** | Hiring velocity, new product posts, iteration signals | Strong / Weak |

## Output Format

### Quick Competitor Brief

```
## Competitor Brief: [Company]

**Overview:** [1-2 sentence description]
**Size:** [employees] | **HQ:** [location] | **Founded:** [year]
**Funding:** [stage / amount if known]

**Key People:**
- CEO: [Name] — [background in 10 words]
- CTO: [Name] — [background in 10 words]
- VP Sales: [Name] — [background in 10 words]

**Recent Signals:**
- Hired [N] people in [department] last quarter
- [Key person] joined/left
- Content focus shifted to [topic]
- [Any other notable signal]

**Strategic Assessment:**
- Building toward: [inference from hiring + content]
- Strengths: [based on team + positioning]
- Vulnerabilities: [gaps in team, silent on LinkedIn, etc.]
```

### Full Intelligence Report

Use the workflows above to compile a comprehensive report covering:

1. **Company overview** (size, positioning, leadership)
2. **Org map** (departments, key people, backgrounds)
3. **Hiring analysis** (what they're building, growth rate)
4. **Content strategy** (topics, engagement, messaging)
5. **Competitive assessment** (SWOT, moat, opportunities)
6. **Recommendations** (how to position against them)

## Best Practices

1. **Focus on signals, not vanity metrics.** A company's follower count matters less than who they're hiring.
2. **Track over time.** A single snapshot is useful. Monthly tracking reveals trends.
3. **Cross-reference signals.** Hiring + content + departures together tell a story that no single signal reveals.
4. **Respect privacy.** Use publicly available data. Don't try to access private information.
5. **Crispy never stores data.** All intelligence is returned directly. Store insights in your own systems.
6. **Act on intelligence.** The best competitive research is useless if it doesn't inform decisions.

## Learn More

- Prospecting tools: https://crispy.sh/features/prospecting
- Analytics tools: https://crispy.sh/features/intelligence
- All 43 tools: https://crispy.sh/tools
- Documentation: https://crispy.sh/docs
