# Crispy Skills

Agent skills for LinkedIn automation using [Crispy](https://crispy.sh) — the LinkedIn MCP server and API.

## Install

```bash
npx skills add shyftai/crispymcp
```

Or install individual skills:

```bash
npx skills add shyftai/crispymcp --skill linkedin-prospecting
npx skills add shyftai/crispymcp --skill linkedin-outreach
npx skills add shyftai/crispymcp --skill linkedin-content
npx skills add shyftai/crispymcp --skill linkedin-intelligence
npx skills add shyftai/crispymcp --skill sdr-playbook
npx skills add shyftai/crispymcp --skill personal-branding
npx skills add shyftai/crispymcp --skill social-selling
npx skills add shyftai/crispymcp --skill linkedin-recruiter
npx skills add shyftai/crispymcp --skill lead-enrichment
npx skills add shyftai/crispymcp --skill competitor-research
```

## Skills

### LinkedIn Tools

| Skill | Description |
|-------|-------------|
| **[linkedin-prospecting](skills/linkedin-prospecting/SKILL.md)** | Search LinkedIn for people, companies, and posts. Build targeted lead lists and research prospects. |
| **[linkedin-outreach](skills/linkedin-outreach/SKILL.md)** | Send personalized messages, connection requests, and InMails. Manage conversations and run campaigns. |
| **[linkedin-content](skills/linkedin-content/SKILL.md)** | Create and publish LinkedIn posts. Engage with content, manage comments, and optimize your strategy. |
| **[linkedin-intelligence](skills/linkedin-intelligence/SKILL.md)** | Track post performance, profile analytics, network growth, and competitive intelligence. |

### Playbooks

| Skill | Description |
|-------|-------------|
| **[sdr-playbook](skills/sdr-playbook/SKILL.md)** | Complete SDR/BDR workflow — prospect identification, research, multi-touch outreach sequences, objection handling, and meeting booking. |
| **[personal-branding](skills/personal-branding/SKILL.md)** | Build and grow your personal brand on LinkedIn — profile optimization, content strategy, audience growth, and performance tracking. |
| **[social-selling](skills/social-selling/SKILL.md)** | Generate pipeline through relationships — attract with content, engage strategically, convert through warm conversations. |
| **[linkedin-recruiter](skills/linkedin-recruiter/SKILL.md)** | Source candidates, build talent pipelines, send recruiting outreach, and manage hiring on LinkedIn. |
| **[lead-enrichment](skills/lead-enrichment/SKILL.md)** | Enrich contact and company lists with LinkedIn profile data — titles, experience, company details, and profile URLs. |
| **[competitor-research](skills/competitor-research/SKILL.md)** | Competitive intelligence from LinkedIn — hiring signals, org charts, content strategy, team growth, and market mapping. |

## Requirements

- A [Crispy](https://crispy.sh) account (from EUR 19/mo)
- A connected LinkedIn profile
- Any MCP-compatible AI agent (Claude, Cursor, VS Code, etc.)

## Quick Start

1. Sign up at [crispy.sh](https://crispy.sh/signup)
2. Connect your LinkedIn profile via the Chrome extension
3. Get your API key from the [dashboard](https://crispy.sh/dashboard/api-keys)
4. Add Crispy to your MCP client:

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

5. Install skills: `npx skills add shyftai/crispymcp`

## 43 LinkedIn Tools

These skills cover Crispy's full tool set across 4 categories:

- **Prospecting** (8 tools) — search_people, search_companies, get_profile, get_company_profile, search_posts, get_search_parameters, get_feed, get_my_profile
- **Outreach** (10 tools) — send_message, send_invitation, send_inmail, start_conversation, get_messages, list_conversations, create_campaign, list_campaigns, archive_campaign, get_campaign_stats
- **Content** (9 tools) — create_post, list_posts, get_post, comment_on_post, react_to_post, list_post_comments, list_post_reactions, get_content_summary, get_top_posts
- **Intelligence** (8 tools) — get_post_analytics, get_cached_post_analytics, get_profile_analytics, get_activity_analytics, get_profile_viewers, get_connections, get_top_posts, purge_analytics_cache

Full tool documentation: [crispy.sh/tools](https://crispy.sh/tools)

## License

MIT
