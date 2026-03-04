---
name: linkedin-content
description: LinkedIn content creation and publishing using Crispy MCP tools. Use when the user wants to create LinkedIn posts, manage their content strategy, engage with posts (comments, reactions), analyze content performance, or manage their LinkedIn presence. Triggers include "write a LinkedIn post", "publish to LinkedIn", "comment on this post", "react to", "engage with", "check my post performance", "what are my top posts", "content strategy", or any task requiring LinkedIn content management.
license: MIT
metadata:
  author: crispy-sh
  version: "1.0.0"
---

# LinkedIn Content with Crispy

Create, publish, and manage LinkedIn content programmatically using Crispy's MCP tools. Engage with posts, track performance, and build your content strategy.

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

- User asks to write or publish a LinkedIn post
- User wants to engage with posts (like, comment, react)
- User needs to check post performance or analytics
- User wants content ideas based on what's working
- User asks to manage comments on their posts
- User wants to analyze their content strategy

## Core Tools

| Tool | Purpose | Key Parameters |
|------|---------|---------------|
| `create_post` | Publish a text post to LinkedIn | `account_id`, `text` |
| `list_posts` | List posts by a profile | `account_id`, `profile_url`, `limit` |
| `get_post` | Get a specific post with engagement data | `account_id`, `post_id` |
| `comment_on_post` | Add a comment to a post | `account_id`, `post_id`, `text` |
| `react_to_post` | React to a post (like, celebrate, etc.) | `account_id`, `post_id`, `reaction_type` |
| `list_post_comments` | Get all comments on a post | `account_id`, `post_id` |
| `list_post_reactions` | Get all reactions on a post | `account_id`, `post_id` |
| `get_content_summary` | Get aggregated content metrics | `account_id` |
| `get_top_posts` | Get best-performing posts | `account_id`, `limit` |

## Workflow Patterns

### 1. Write and Publish a Post

```
Step 1: Understand the topic, audience, and tone
Step 2: Draft the post following LinkedIn best practices
Step 3: Review with the user
Step 4: Publish via create_post
```

### 2. Content Performance Analysis

```
Step 1: get_top_posts to see what's working
Step 2: list_posts to get recent post history
Step 3: For key posts, get_post for detailed metrics
Step 4: Analyze patterns: topics, formats, posting times
Step 5: Present insights and recommendations
```

### 3. Engagement Strategy

```
Step 1: Identify target profiles to engage with
Step 2: list_posts to find their recent content
Step 3: react_to_post on relevant posts
Step 4: comment_on_post with thoughtful, value-adding comments
Step 5: Track engagement reciprocity over time
```

### 4. Comment Management

```
Step 1: list_posts to find user's recent posts
Step 2: list_post_comments on posts with engagement
Step 3: Draft thoughtful replies to each comment
Step 4: Post replies via comment_on_post
```

## Post Writing Framework

### Structure (for maximum engagement)

1. **Hook** (first 2 lines) — Must stop the scroll. Visible before "see more."
   - Lead with a bold claim, surprising stat, or contrarian take
   - Use line breaks after the hook for visual separation

2. **Body** (3-8 short paragraphs)
   - One idea per paragraph
   - Short sentences (under 20 words)
   - Use line breaks between paragraphs (LinkedIn collapses dense text)
   - Include specifics: numbers, names, timeframes

3. **CTA** (last line)
   - Ask a question to drive comments
   - Or share a resource/link in first comment (not in post body)

4. **Hashtags** — 3-5 relevant hashtags at the end

### Post Types (ranked by typical engagement)

| Type | Engagement | Best For |
|------|-----------|----------|
| Personal story | Very high | Building trust, authenticity |
| Contrarian take | Very high | Thought leadership, discussion |
| Tactical how-to | High | Demonstrating expertise |
| List post | High | Broad reach, saves |
| Before/after | Medium-high | Case studies, results |
| Industry commentary | Medium | Staying relevant |
| Link post | Low | Driving traffic (algorithm penalizes) |

### Engagement Optimization

- **First hour matters.** Reply to every comment within 60 minutes.
- **Don't edit** within the first hour — it resets distribution.
- **External links reduce reach.** Put links in the first comment instead.
- **Dwell time drives distribution.** Longer posts that hold attention rank higher.
- **Comments > reactions.** Write CTAs that invite discussion.

## Safety Guidelines

1. **Authentic engagement only.** Don't mass-react or mass-comment on random posts.
2. **Quality over quantity.** Thoughtful comments build reputation; generic "Great post!" does not.
3. **Ramp up posting gradually.** 2-3 posts/week is sustainable for most profiles.
4. **Crispy never stores content.** Posts are published directly to LinkedIn. Crispy retains nothing.

## Output Format

When presenting content analytics:

```
## Content Performance (Last 30 Days)
- Posts published: 12
- Total impressions: 45,230
- Average engagement rate: 4.2%
- Top post: "Why we stopped using..." (8,340 impressions, 6.1% engagement)

### Top 5 Posts
| Post | Impressions | Reactions | Comments | Engagement |
|------|------------|-----------|----------|------------|
| "Why we stopped..." | 8,340 | 142 | 67 | 6.1% |
```

## Learn More

- All tools: https://crispy.sh/tools
- Content tools: https://crispy.sh/features/content
- Documentation: https://crispy.sh/docs
