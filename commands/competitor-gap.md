---
description: Compare two domains to find keyword gaps and competitive opportunities. Uses ~~SEO connector when available, falls back to WebSearch analysis.
argument-hint: <your-domain> <competitor-domain> [--location US|JP|UK|...]
---

# Competitor Gap Analysis

Analyze keyword gaps between two domains to find competitive opportunities.

## Procedure

Parse `$ARGUMENTS` to extract:
- `your_domain`: Your domain (e.g., example.com)
- `competitor_domain`: Competitor's domain (e.g., competitor.com)
- `--location`: Optional location filter (default: US)

### If ~~SEO connector is available

Use the connected SEO API to perform domain intersection analysis:
- Fetch keywords where competitor ranks but you don't
- Get search volume, difficulty, and competitor position for each
- Sort by opportunity (high volume + low difficulty + competitor ranking well)

### If no ~~SEO connector (WebSearch fallback)

#### Step 1: Analyze your domain

```
WebSearch: "site:{your_domain}"
WebSearch: "{your_domain} keywords OR topics"
```

Note the main topics, pages, and content themes of your site.

#### Step 2: Analyze competitor domain

```
WebSearch: "site:{competitor_domain}"
WebSearch: "{competitor_domain} keywords OR topics"
```

Note the main topics, pages, and content themes of the competitor.

#### Step 3: Identify gaps

```
WebSearch: "{competitor_domain} -site:{your_domain} {common industry terms}"
WebSearch: "{competitor_domain} popular pages OR top content"
```

Look for:
- Topics competitor covers that you don't
- Keywords competitor ranks for that you're missing
- Content types competitor uses (guides, tools, calculators)
- Schema types competitor implements

#### Step 4: GEO gap analysis

For AI visibility specifically:
- Check if competitor has FAQPage schema (use WebFetch on competitor pages)
- Check if competitor has AgentFacts (`{competitor_domain}/.well-known/agent-facts`)
- Compare content confidence (are they using more authoritative tone?)
- Check content freshness (when was their content last updated?)

### Step 5: Generate Report

```markdown
## Competitor Gap Analysis
Your Domain: {your_domain}
Competitor: {competitor_domain}
Location: {location}

### Keyword Gaps
Keywords where {competitor_domain} ranks but {your_domain} doesn't:

| Keyword | Est. Volume | Difficulty | Competitor Position | Priority |
|---------|-------------|------------|--------------------|---------|
| {keyword1} | {vol} | {diff} | {pos} | HIGH/MED/LOW |
| ... | | | | |

### Content Gaps
| Topic | Competitor Has | You Have | Action |
|-------|---------------|----------|--------|
| {topic1} | Yes (URL) | No | Create content |
| ... | | | |

### Technical Gaps
| Feature | Competitor | You | Impact |
|---------|-----------|-----|--------|
| FAQPage Schema | Yes/No | Yes/No | +40% AI visibility |
| AgentFacts | Yes/No | Yes/No | AI agent discovery |
| Content Freshness | {date} | {date} | 3.2x more citations if <30 days |

### Opportunity Score
Top 5 highest-impact opportunities:
1. {opportunity with rationale}
2. ...

### Recommended Actions
1. [Immediate: Quick wins]
2. [Short-term: Content creation]
3. [Long-term: Authority building]

**Tip:** Focus on keywords with high volume and low difficulty where the competitor ranks in the top 10.
```
