---
name: personal-branding
description: Build and grow a personal brand on LinkedIn. Use when the user wants to grow their LinkedIn presence, create a content strategy, optimize their profile, increase engagement, build thought leadership, or grow their audience. Triggers include "grow my LinkedIn", "personal brand", "LinkedIn strategy", "content calendar", "thought leadership", "grow my audience", "LinkedIn profile optimization", "what should I post", "engagement strategy", or any task related to building a professional presence on LinkedIn.
license: MIT
metadata:
  author: crispy-sh
  version: "1.0.0"
---

# Personal Branding on LinkedIn

A complete system for building and growing your personal brand on LinkedIn — from profile optimization to content strategy to audience growth. Powered by LinkedIn MCP tools for data-driven decisions.

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

- User wants to grow their LinkedIn audience or engagement
- User asks for a content strategy or content calendar
- User wants to optimize their LinkedIn profile
- User asks "what should I post on LinkedIn?"
- User wants to build thought leadership in their space
- User asks to analyze what content is working

## The Personal Branding System

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  1. Audit     │───▶│  2. Strategy  │───▶│  3. Create    │───▶│  4. Grow      │
│  Your Profile │    │  & Pillars    │    │  & Publish    │    │  & Optimize   │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
```

## Phase 1: Profile Audit

**Goal:** Ensure your profile converts visitors into followers and connections.

```
Tools: get_my_profile, get_profile_analytics, get_profile_viewers
```

### Steps

1. Pull current profile with `get_my_profile`
2. Check `get_profile_analytics` for baseline metrics
3. Review `get_profile_viewers` to understand who's looking
4. Audit each profile section against best practices

### Profile Optimization Checklist

| Section | Best Practice | Common Mistake |
|---------|--------------|----------------|
| **Headline** | "I help [audience] do [outcome]" or "[Role] at [Company] • [Expertise]" | Just job title ("Marketing Manager at Acme") |
| **Banner** | Visual CTA or value prop. Include website/offer. | Default LinkedIn blue or blurry photo |
| **About** | First 3 lines = hook (visible before "see more"). Tell your story. End with CTA. | Copy-paste of resume |
| **Experience** | Results and impact, not job descriptions. Use numbers. | Bullet-point job duties |
| **Featured** | Pin your best post, a lead magnet, or your newsletter | Empty or outdated |
| **Skills** | Top 3 should match your brand positioning | Random skills from 2015 |

### Profile Visitor Analysis

Use `get_profile_viewers` to understand your audience:

```
## Profile Visitor Analysis
- Total viewers this week: [N]
- Top industries: [list]
- Top titles: [list]
- Match with target audience: [High/Medium/Low]
- Action: [Adjust content/profile to attract more of target audience]
```

## Phase 2: Content Strategy & Pillars

**Goal:** Define what you'll be known for and create a repeatable system.

```
Tools: get_top_posts, list_posts, search_posts
```

### Find Your Content Pillars (3-5 topics)

Content pillars are the recurring themes you'll post about. They should sit at the intersection of:

1. **Your expertise** — what you know deeply
2. **Audience interest** — what your target audience cares about
3. **Business relevance** — what drives toward your goals

Example pillars for a B2B SaaS founder:
- Building in public (product updates, learnings)
- Sales and GTM tactics
- Founder life (hiring, fundraising, culture)
- Industry insights (AI, SaaS trends)

### Analyze What Works

Use `get_top_posts` to pull your best-performing content, then identify patterns:

```
Step 1: get_top_posts (limit: 20)
Step 2: Categorize each post by: topic, format, tone, posting time
Step 3: Calculate average engagement per category
Step 4: Identify top patterns
```

### Study Your Space

Use `search_posts` to find top-performing content in your niche:

```
Step 1: search_posts with keywords from your pillars
Step 2: Analyze what gets engagement: topics, formats, hooks
Step 3: Identify gaps — what's not being said?
Step 4: Note successful hooks and structures to adapt
```

### Content Calendar Framework

| Day | Pillar | Format | Goal |
|-----|--------|--------|------|
| Monday | Expertise | How-to / Tactical | Establish authority |
| Wednesday | Story | Personal narrative | Build connection |
| Friday | Opinion | Contrarian take / Hot take | Drive discussion |

Aim for 3 posts/week to start. Consistency beats volume.

## Phase 3: Create & Publish

**Goal:** Write posts that get engagement and build your audience.

```
Tools: create_post, list_posts, get_post
```

### The Post Formula

Every high-performing LinkedIn post follows this structure:

```
HOOK (line 1-2)
↓
Gap or tension (line 3-4)
↓
BODY (lines 5-15)
Story, framework, or insight
↓
PAYOFF (line 16-17)
Key takeaway
↓
CTA (last line)
Question that invites comments
```

### Hook Templates (steal and adapt)

**Contrarian:**
- "Everyone says [common belief]. They're wrong."
- "I stopped [common practice] 6 months ago. Here's what happened."
- "Unpopular opinion: [bold statement]"

**Story:**
- "Last week, a [customer/colleague] told me something that changed how I think about [topic]."
- "I [failed/succeeded] at [thing] and learned 3 things."
- "In 2019, I [was in situation]. Today, [different situation]. Here's the turning point."

**Curiosity:**
- "After [researching/testing/interviewing], I found something surprising about [topic]."
- "[Number] [things/lessons/mistakes] that separate [good] from [great]."
- "Most [role] get [topic] completely wrong. Here's why."

**Data:**
- "We analyzed [N] [things] and found [surprising insight]."
- "[Specific number]. That's [what it represents]."

### Format Guidelines

- **Line length:** Short. One idea per line.
- **Paragraphs:** 1-3 sentences max. Use line breaks liberally.
- **Emojis:** Sparingly. 0-3 per post. Never as bullet points.
- **Hashtags:** 3-5 at the end. Mix broad (#Leadership) and niche (#SaaSGrowth).
- **Links:** Never in the post body. Put in first comment.
- **Length:** 800-1500 characters for most posts. Longer for stories.
- **First 210 characters:** This is what shows before "see more". Make it count.

### Publishing Workflow

```
Step 1: Write draft based on pillar and format for today
Step 2: Review hook — would YOU click "see more"?
Step 3: Check: Is there a clear takeaway? A CTA?
Step 4: Publish via create_post
Step 5: Immediately comment with any links or additional context
Step 6: Respond to every comment in the first 60 minutes
```

### Best Posting Times

| Day | Time (local) | Why |
|-----|-------------|-----|
| Tuesday | 7:30-8:30 AM | Peak commute + morning scroll |
| Wednesday | 12:00-1:00 PM | Lunch break browsing |
| Thursday | 7:30-8:30 AM | Highest weekday engagement |
| Tuesday-Thursday | 5:00-6:00 PM | End-of-day wind-down |

Avoid: weekends, Mondays before 10 AM, Fridays after 2 PM.

## Phase 4: Grow & Optimize

**Goal:** Build feedback loops and scale what works.

```
Tools: get_post_analytics, get_profile_analytics, get_profile_viewers,
       get_activity_analytics, get_top_posts, react_to_post, comment_on_post
```

### Weekly Review Ritual

Every Friday, run this analysis:

```
Step 1: get_activity_analytics for week overview
Step 2: get_top_posts for performance ranking
Step 3: get_profile_analytics for follower/viewer trends
Step 4: get_profile_viewers for audience composition
Step 5: Compare against last week
Step 6: Identify: What worked? What didn't? What to do more of?
```

### Growth Levers

| Lever | How | Impact |
|-------|-----|--------|
| **Engage first** | Comment on 5-10 posts from target audience daily | High — builds reciprocity |
| **Reply to every comment** | Within 60 min of posting | High — boosts algorithmic reach |
| **Consistent schedule** | Same days/times each week | Medium — trains your audience |
| **Repurpose winners** | Rewrite top posts with new angles every 4-6 weeks | Medium — proven content |
| **Cross-pollinate** | Mention people, tag companies (sparingly) | Medium — expands reach |
| **Ride trends** | Comment on trending topics in your space | Low-medium — timely visibility |

### Engagement Strategy

Use Crispy tools to engage strategically:

```
Step 1: Identify 20-30 accounts in your niche (prospects, peers, influencers)
Step 2: Use list_posts to find their recent content
Step 3: react_to_post on posts you genuinely find valuable
Step 4: comment_on_post with substantive comments (not "Great post!")
Step 5: Do this daily before you publish your own content
```

**Good comment formula:**
- Add a perspective they didn't mention
- Share a relevant experience
- Ask a thoughtful follow-up question
- Respectfully disagree with a point

### Monthly Metrics Dashboard

```
## Personal Brand Report — [Month]

### Growth
- Followers: [N] (+[X]% vs last month)
- Profile views: [N] (+[X]%)
- Search appearances: [N] (+[X]%)

### Content Performance
- Posts published: [N]
- Total impressions: [N]
- Avg engagement rate: [X]%
- Best post: "[hook]" — [N] impressions, [X]% engagement

### Audience
- Top viewer titles: [list]
- Top viewer industries: [list]
- ICP match rate: [X]%

### What Worked
- [Topic/format] posts averaged [X]% higher engagement
- [Day/time] consistently outperforms

### Next Month Focus
1. [Specific action based on data]
2. [Specific action based on data]
3. [Specific action based on data]
```

## Common Mistakes

1. **Posting without a strategy.** Random posts = random results. Pick pillars and stick to them.
2. **All value, no personality.** People follow people, not textbooks. Share stories and opinions.
3. **Selling in every post.** The 80/20 rule: 80% value, 20% promotion. Even less when starting out.
4. **Ignoring comments.** Every unanswered comment is a missed relationship.
5. **Giving up after 2 weeks.** LinkedIn growth compounds. Most creators see traction at 3-6 months.
6. **Copying formats exactly.** Adapt, don't copy. Your voice is your differentiator.

## Learn More

- Content tools: https://crispy.sh/features/content
- Analytics tools: https://crispy.sh/features/intelligence
- All 43 tools: https://crispy.sh/tools
