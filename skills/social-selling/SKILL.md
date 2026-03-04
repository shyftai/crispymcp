---
name: social-selling
description: Social selling system for LinkedIn. Use when the user wants to build pipeline through LinkedIn relationships, warm up prospects before outreach, use content to attract inbound leads, or combine personal branding with sales development. Triggers include "social selling", "warm outreach", "build pipeline on LinkedIn", "inbound leads from LinkedIn", "relationship selling", "sell on LinkedIn", "LinkedIn for sales", "attract leads", or any task combining content, engagement, and sales on LinkedIn.
license: MIT
metadata:
  author: crispy-sh
  version: "1.0.0"
---

# Social Selling on LinkedIn

Build pipeline through relationships instead of cold outreach. Combine content creation, strategic engagement, and warm conversations to generate inbound leads and book meetings on LinkedIn.

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

- User wants to generate leads from LinkedIn without cold outreach
- User asks about social selling or relationship-based selling
- User wants to combine content with pipeline building
- User asks to warm up prospects before reaching out
- User wants inbound leads from their LinkedIn presence
- User mentions "LinkedIn for sales" or "sell without being salesy"

## The Social Selling Framework

Social selling is NOT cold outreach with extra steps. It's a fundamentally different approach:

```
Cold outreach:  Find → Pitch → Hope
Social selling: Attract → Engage → Convert
```

### The 3 Pillars

```
┌─────────────────────────────────────────────────────┐
│                  SOCIAL SELLING                      │
├─────────────────┬──────────────────┬────────────────┤
│   1. ATTRACT    │   2. ENGAGE      │   3. CONVERT   │
│                 │                  │                │
│ Content that    │ Strategic        │ Warm           │
│ draws your ICP  │ relationship     │ conversations  │
│ to your profile │ building         │ that close     │
├─────────────────┼──────────────────┼────────────────┤
│ create_post     │ comment_on_post  │ send_message   │
│ list_posts      │ react_to_post    │ start_convo    │
│ get_top_posts   │ search_posts     │ send_invitation│
│ get_analytics   │ get_profile      │ list_convos    │
└─────────────────┴──────────────────┴────────────────┘
```

## Pillar 1: Attract — Content That Draws Your ICP

**Goal:** Post content that makes your ideal customers think "I need to talk to this person."

```
Tools: create_post, get_top_posts, get_post_analytics, get_content_summary
```

### Content Strategy for Social Sellers

Your content should do 3 things:
1. **Demonstrate expertise** in the problem you solve
2. **Build trust** through transparency and stories
3. **Create curiosity** about your solution (without pitching)

### The 5 Content Types for Social Sellers

| Type | Purpose | Example | Frequency |
|------|---------|---------|-----------|
| **Problem posts** | Show you understand their pain | "Most [ICPs] waste 10hrs/week on [problem]. Here's why..." | 2x/week |
| **Proof posts** | Show you can solve it | "We helped [client type] go from [before] to [after]" | 1x/week |
| **Process posts** | Show how you think | "Here's the exact framework we use to [solve problem]" | 1x/week |
| **Perspective posts** | Show you're a thinker | "The [industry] is changing. Here's what most people miss..." | 1x/week |
| **Personal posts** | Show you're human | "I learned something surprising this week..." | 1x/2 weeks |

### Analyze What Attracts Your ICP

```
Step 1: get_top_posts to find your best content
Step 2: get_profile_viewers after each post to see WHO it attracted
Step 3: Cross-reference viewers with your ICP
Step 4: Double down on content that attracts the right people (not just any engagement)
```

**Key insight:** A post with 500 impressions that attracts 3 ICP profile visitors is worth more than a viral post with 50,000 impressions and zero ICP visitors.

## Pillar 2: Engage — Strategic Relationship Building

**Goal:** Build familiarity with prospects so when you reach out, they already know your name.

```
Tools: search_posts, list_posts, comment_on_post, react_to_post, get_profile, search_people
```

### The Engagement Ladder

Before you ever send a message, climb the engagement ladder:

```
Level 1: React to their posts (they see your name)
         ↓
Level 2: Comment on their posts (they read your thoughts)
         ↓
Level 3: Share/reference their content in your posts (they feel valued)
         ↓
Level 4: DM with genuine context (they're open to conversation)
```

### Daily Engagement Routine

```
Step 1: Identify your target list (20-50 prospects + 10-20 industry voices)
Step 2: Use search_posts or list_posts to find their recent content
Step 3: Engage authentically:
        - React to 10-15 posts
        - Leave 3-5 substantive comments
        - Share 1 post with your own take
Step 4: Track who engages back
```

### How to Comment Like a Social Seller

**DO:**
- Add a perspective they didn't cover
- Share a relevant experience or data point
- Ask a thoughtful question that extends the conversation
- Respectfully challenge an assumption

**DON'T:**
- "Great post!" / "Love this!" / "So true!"
- Comment with your own pitch
- Drop links to your product
- Write a comment longer than the post

**Template:**
```
[Acknowledge their point] + [Add your perspective or experience] + [Optional: question]

Example:
"The point about [X] really resonates — we saw the same thing when [relevant experience].
What I'd add is [your unique insight]. Have you seen this play out differently in [their industry]?"
```

### Build Your Prospect Map

Use Crispy to build and maintain your engagement target list:

```
Step 1: search_people to find ICP prospects
Step 2: get_profile to understand their interests and activity
Step 3: search_posts to find their content
Step 4: Track engagement frequency per prospect

| Prospect | Company | Last Engaged | Engagement Level | Next Action |
|----------|---------|-------------|-----------------|-------------|
| Jane S.  | Acme    | 2 days ago  | Level 2 (Comment) | Comment on next post |
| John D.  | Beta    | 1 week ago  | Level 1 (React)   | Leave a comment |
| Sarah K. | Gamma   | Today       | Level 3 (Shared)  | Ready for DM |
```

## Pillar 3: Convert — Warm Conversations That Close

**Goal:** Turn engaged prospects into meetings and deals.

```
Tools: send_invitation, send_message, start_conversation, list_conversations, get_messages
```

### When to Move from Engagement to DM

A prospect is ready for a DM when:
- They've liked/commented on 2+ of your posts
- They've viewed your profile after your engagement
- They've responded to one of your comments
- You've been engaging with their content for 2+ weeks
- They've accepted your connection request

### The Warm DM Framework

**Step 1: Connect** (if not already connected)
```
"[Name], been enjoying your content on [topic] —
especially your point about [specific thing].
Would love to stay connected."
```

**Step 2: First DM** (after connection, reference real interaction)
```
"Hey [Name], thanks for connecting. Your post about [X]
stuck with me — I actually [did something related / have a
perspective to share].

Quick question: [genuine question about their challenge]?"
```

**Step 3: Value message** (if they respond, add value before asking)
```
"That makes sense. We've been working on exactly that with
[type of company]. Found that [insight or approach that helps].

Happy to share what we've learned if it's useful."
```

**Step 4: Meeting ask** (only when there's genuine interest)
```
"Sounds like [problem] is a real priority for you this quarter.
I have a few ideas on how [specific approach] could help —
worth a 15-min chat to see if there's a fit?

How's Thursday afternoon?"
```

### Conversation Signals to Watch For

| Signal | Meaning | Action |
|--------|---------|--------|
| They ask about your product | High intent | Share brief value prop, offer call |
| They share a challenge | Opening | Offer insight, then suggest meeting |
| They mention a timeline | Urgency | Propose specific next step |
| They go quiet | Cooling off | Re-engage on their content, don't chase |
| They say "not now" | Future opportunity | Set 90-day reminder, keep engaging content |

### Pipeline Tracking

```
## Social Selling Pipeline — [Week]

### Active Conversations
| Prospect | Stage | Last Touch | Next Action | Notes |
|----------|-------|-----------|-------------|-------|
| Jane S.  | DM stage 2 | Today | Wait for reply | Asked about their CRM stack |
| John D.  | Meeting booked | Yesterday | Prep call notes | Thursday 2pm |

### Engagement Funnel
- Prospects in target list: 40
- Engaged this week: 18
- Connection requests sent: 5
- DM conversations: 3
- Meetings booked: 1

### Content Attribution
- Profile views from ICP this week: 12
- Inbound connection requests: 4
- Inbound DMs: 1
```

## Weekly Social Selling Rhythm

| Block | Time | Activity | Tools |
|-------|------|----------|-------|
| **Mon AM** | 30 min | Review inbox, respond to DMs | `list_conversations`, `get_messages` |
| **Mon PM** | 20 min | Engage with prospect content | `search_posts`, `comment_on_post` |
| **Tue AM** | 30 min | Publish content (Attract) | `create_post` |
| **Tue PM** | 20 min | Engage with comments on your post | `list_post_comments`, `comment_on_post` |
| **Wed AM** | 30 min | Prospect research + warm DMs | `get_profile`, `send_message` |
| **Wed PM** | 20 min | Engage with prospect content | `list_posts`, `react_to_post` |
| **Thu AM** | 30 min | Publish content (Attract) | `create_post` |
| **Thu PM** | 20 min | Engage with comments + prospect content | `comment_on_post` |
| **Fri AM** | 30 min | Weekly review + analytics | `get_activity_analytics`, `get_profile_viewers` |
| **Fri PM** | 20 min | Plan next week's content | `get_top_posts` |

**Total time:** ~4 hours/week

## Social Selling vs. Cold Outreach

| | Cold Outreach | Social Selling |
|--|---------------|---------------|
| **Speed** | Fast (results in days) | Slow (results in weeks/months) |
| **Reply rate** | 5-15% | 30-60% |
| **Meeting quality** | Lower (cold conversations) | Higher (warm, informed) |
| **Scalability** | High (volume play) | Medium (relationship play) |
| **Risk** | Account restrictions | None |
| **Long-term ROI** | Degrades over time | Compounds over time |

**Best approach:** Combine both. Use social selling as the primary strategy, cold outreach for high-priority accounts where you can't wait.

## Learn More

- Content tools: https://crispy.sh/features/content
- Outreach tools: https://crispy.sh/features/outreach
- Analytics tools: https://crispy.sh/features/intelligence
- All 43 tools: https://crispy.sh/tools
