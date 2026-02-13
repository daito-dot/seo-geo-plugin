---
description: Research keywords for SEO/GEO optimization. Uses ~~SEO connector when available, falls back to WebSearch.
argument-hint: <keyword> [--location US|JP|UK|...] [--limit 20]
---

# Keyword Research

Research target keywords for SEO and GEO optimization.

## Procedure

Parse `$ARGUMENTS` to extract the seed keyword, optional location (default: US), and limit (default: 20).

### If ~~SEO connector is available

Use the connected SEO API to fetch:
- Search volume
- Keyword difficulty
- CPC (Cost Per Click)
- Related keywords
- SERP features

### If no ~~SEO connector (WebSearch fallback)

Perform the following WebSearch queries to gather keyword intelligence:

#### Step 1: Search volume and difficulty estimates

```
WebSearch: "{keyword} search volume keyword difficulty"
WebSearch: "{keyword} keyword research site:ahrefs.com OR site:semrush.com OR site:moz.com"
```

#### Step 2: Related and long-tail keywords

```
WebSearch: "{keyword} related keywords"
WebSearch: "{keyword} long-tail keywords ideas"
WebSearch: "people also ask {keyword}"
```

#### Step 3: Competitor analysis

```
WebSearch: "{keyword} best practices 2026"
WebSearch: "top {keyword} tools OR services OR solutions"
```

#### Step 4: Search intent analysis

Classify the keyword intent:
- **Informational**: "what is", "how to", "guide"
- **Navigational**: Brand-specific searches
- **Transactional**: "buy", "pricing", "best"
- **Commercial Investigation**: "review", "comparison", "vs"

### Step 5: Generate Report

```markdown
## Keyword Research: "{keyword}"
Location: {location}

### Primary Keyword
| Metric | Value |
|--------|-------|
| Keyword | {keyword} |
| Estimated Volume | {volume or range} |
| Estimated Difficulty | {low/medium/high} |
| Search Intent | {intent type} |

### Related Keywords
| Keyword | Est. Volume | Difficulty | Intent |
|---------|-------------|------------|--------|
| {related1} | {vol} | {diff} | {intent} |
| ... | | | |

### Long-Tail Opportunities
1. {long-tail keyword 1}
2. {long-tail keyword 2}
3. ...

### Content Strategy Recommendations
- **Primary target:** {keyword} - {recommendation}
- **Supporting content:** {related keywords to target}
- **GEO optimization:** Apply Princeton methods (citations +40%, statistics +37%)
- **Schema suggestion:** {FAQPage / Article / HowTo based on intent}

### SERP Analysis
- Current top results are: {analysis of what's ranking}
- Content gap opportunities: {what's missing from current results}
```

### Notes
- When using WebSearch fallback, volume and difficulty are estimates based on available public data
- For accurate data, connect an SEO tool via the ~~SEO connector
- Always verify estimates against multiple sources
