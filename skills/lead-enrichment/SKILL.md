---
name: lead-enrichment
description: Enrich leads and contacts with LinkedIn profile data using Crispy MCP tools. Use when the user has a list of names, emails, or companies and wants to pull LinkedIn data for each — titles, companies, experience, profile URLs, company details. Triggers include "enrich these leads", "look up these contacts on LinkedIn", "get LinkedIn data for this list", "enrich my CRM", "fill in missing profile data", "research these companies", "bulk profile lookup", or any task requiring lead or contact enrichment from LinkedIn.
license: MIT
metadata:
  author: crispy-sh
  version: "1.0.0"
---

# Lead Enrichment with LinkedIn Data

Take a list of leads, contacts, or companies and enrich them with LinkedIn profile data — titles, experience, company details, and profile URLs. Turn sparse CRM records into actionable intelligence.

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

- User has a list of names and wants LinkedIn data
- User wants to enrich CRM contacts with profile information
- User asks to "look up these people on LinkedIn"
- User has a company list and wants employee data
- User wants to fill in missing titles, companies, or profile URLs
- User asks to research a batch of leads or accounts

## Core Tools

| Tool | Purpose | Use For |
|------|---------|---------|
| `search_people` | Find profiles by name + company | Matching leads to LinkedIn profiles |
| `get_profile` | Pull full profile details | Enriching matched profiles with experience, education, skills |
| `search_companies` | Find company pages | Matching company names to LinkedIn pages |
| `get_company_profile` | Pull company details | Enriching with size, industry, description, HQ |
| `get_search_parameters` | Get valid filter values | Looking up industry IDs and regions |

## Enrichment Workflows

### Workflow 1: Enrich a Contact List

**Input:** List of names + companies (e.g., from a CRM export, event attendee list, spreadsheet)

```
Step 1: For each contact, search_people with name + company as keywords
Step 2: Match the correct profile (verify name, title, company)
Step 3: get_profile for matched profiles to pull full data
Step 4: Return enriched data in structured format
```

### Workflow 2: Enrich a Company List

**Input:** List of company names

```
Step 1: For each company, search_companies by name
Step 2: Match the correct company page
Step 3: get_company_profile for full details
Step 4: Optionally, search_people at each company for key contacts
Step 5: Return enriched company data
```

### Workflow 3: Find Decision-Makers at Target Accounts

**Input:** List of company names + target titles

```
Step 1: For each company, search_people with company + title filter
Step 2: get_profile on matches to verify role and seniority
Step 3: Return a contact map per company
```

### Workflow 4: Enrich from LinkedIn URLs

**Input:** List of LinkedIn profile URLs

```
Step 1: For each URL, get_profile directly
Step 2: Extract all available data
Step 3: Return structured enrichment data
```

## Matching Strategy

Matching names to the correct LinkedIn profile is the most critical step. Follow this approach:

### Matching Rules

| Signal | Weight | How to Check |
|--------|--------|-------------|
| **Full name match** | Required | First + last name in search results |
| **Company match** | High | Current or recent company matches input |
| **Title match** | Medium | Title is plausible for the context |
| **Location match** | Low | If location is provided, use as tiebreaker |

### Handling Ambiguity

- **Multiple matches:** If search returns several people with the same name at the same company, use title or location to disambiguate. If still ambiguous, flag for human review.
- **No match found:** The person may not be on LinkedIn, may use a different name, or the company name may differ. Try variations (e.g., "IBM" vs "International Business Machines"). Flag as "not found" rather than guessing.
- **Company name variations:** Try the exact name first, then common variations. "McKinsey" vs "McKinsey & Company", "Google" vs "Alphabet".

### Confidence Scoring

For each enriched record, assign a confidence level:

```
HIGH   — Name + company + title all match exactly
MEDIUM — Name + company match, title differs or missing
LOW    — Name matches, company is ambiguous or different
NONE   — No match found
```

## Output Format

### Enriched Contact List

```
## Enriched Contacts — [Source]
Enriched: [X] of [Y] contacts | High confidence: [N] | Needs review: [N]

| # | Name | Title | Company | Location | LinkedIn URL | Confidence |
|---|------|-------|---------|----------|-------------|------------|
| 1 | Jane Smith | VP Engineering | Acme Corp | Berlin, DE | linkedin.com/in/janesmith | HIGH |
| 2 | John Doe | CTO | Beta Inc | New York, US | linkedin.com/in/johndoe | HIGH |
| 3 | Sarah K. | — | Gamma LLC | — | Not found | NONE |
```

### Enriched Contact Detail (per person)

```
## Jane Smith
- **LinkedIn:** linkedin.com/in/janesmith
- **Title:** VP of Engineering
- **Company:** Acme Corp (201-500 employees, Fintech, Berlin)
- **Tenure:** 2 years 3 months
- **Previous:** Senior Eng Manager at Beta Inc (3 years), Software Engineer at Gamma (2 years)
- **Education:** MSc Computer Science, TU Berlin
- **Skills:** Python, Kubernetes, Team Leadership, System Design
- **Recent activity:** Posted about engineering culture (2 days ago)
- **Confidence:** HIGH
```

### Enriched Company List

```
## Enriched Companies

| # | Company | Industry | Size | HQ | LinkedIn URL | Founded |
|---|---------|----------|------|----|--------------|---------|
| 1 | Acme Corp | Fintech | 201-500 | Berlin, DE | linkedin.com/company/acme | 2018 |
| 2 | Beta Inc | SaaS | 51-200 | New York, US | linkedin.com/company/beta | 2020 |
```

### Decision-Maker Map

```
## Decision-Makers at Target Accounts

### Acme Corp (Fintech, 201-500, Berlin)
| Name | Title | LinkedIn | Personalization Note |
|------|-------|----------|---------------------|
| Jane Smith | VP Engineering | linkedin.com/in/janesmith | Posted about hiring challenges |
| Tom Brown | CTO | linkedin.com/in/tombrown | Ex-Google, systems background |

### Beta Inc (SaaS, 51-200, New York)
| Name | Title | LinkedIn | Personalization Note |
|------|-------|----------|---------------------|
| Sarah Lee | Head of Product | linkedin.com/in/sarahlee | Active poster, product-led growth |
```

## Rate Limit Planning

Each enrichment operation uses API calls. Plan accordingly:

| Operation | API Calls Per Record | Pro (500/day) | Team (unlimited) |
|-----------|---------------------|---------------|------------------|
| Search + match | 1 | 500 contacts/day | Unlimited |
| Search + full profile | 2 | 250 contacts/day | Unlimited |
| Company enrichment | 1-2 | 250-500/day | Unlimited |
| Full enrichment (contact + company) | 3 | ~165 contacts/day | Unlimited |

### Optimization Tips

1. **Batch by company.** If multiple contacts work at the same company, search the company once and reuse the data.
2. **Skip full profiles for low-priority leads.** Search results include name, title, company, and URL — often enough for initial qualification.
3. **Use LinkedIn URLs when available.** `get_profile` with a URL skips the search step, saving 1 API call per contact.
4. **Prioritize.** Enrich high-value leads first if you're on the Pro plan.

## Integration Patterns

### CRM Enrichment Flow

```
1. Export contacts from CRM (name, company, email)
2. Run enrichment workflow
3. Review confidence scores
4. Import enriched data back to CRM
5. Flag "NONE" matches for manual review
```

### Event Follow-Up

```
1. Export attendee list (name, company from badges/registrations)
2. Run enrichment to get titles and LinkedIn URLs
3. Prioritize by title/seniority
4. Pass to outreach workflow (use linkedin-outreach skill)
```

### Inbound Lead Qualification

```
1. New lead comes in (name, email, company from form)
2. Enrich with LinkedIn data
3. Score based on title, company size, industry fit
4. Route to appropriate sales rep
```

## Best Practices

1. **Always verify matches.** Never assume the first search result is correct. Check name + company + title.
2. **Handle not-found gracefully.** ~10-20% of contacts won't have findable LinkedIn profiles. That's normal.
3. **Respect rate limits.** Pro: 500 calls/day. Plan your batch sizes accordingly.
4. **Crispy never stores data.** Enriched data is returned to your agent. Store it in your own CRM/database.
5. **Keep data fresh.** People change jobs. Re-enrich quarterly for active prospects.

## Learn More

- Prospecting tools: https://crispy.sh/features/prospecting
- All 43 tools: https://crispy.sh/tools
- Documentation: https://crispy.sh/docs
