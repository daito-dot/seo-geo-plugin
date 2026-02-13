---
description: Run a full GEO (Generative Engine Optimization) audit for AI search visibility. Checks technical visibility, content authority, agent infrastructure, and discovery strategy.
argument-hint: <url> [--launch-year YYYY]
---

# GEO Audit

Perform a comprehensive Generative Engine Optimization audit on the provided URL.

## Procedure

Parse `$ARGUMENTS` to extract the target URL and optional `--launch-year` parameter.

### Step 1: Technical Visibility Check

Use `WebFetch` to retrieve the page, then use `Bash` to measure technical metrics:

```bash
# Measure HTML size and load time
curl -o /tmp/geo-audit-page.html -s -w "TTFB: %{time_starttransfer}s\nTotal: %{time_total}s\nSize: %{size_download} bytes\n" "{url}"
```

Evaluate:
- **HTML Size**: Target < 1MB. Pages >1MB are abandoned by 18% of AI crawlers.
- **JS Dependency**: Check if substantial text content is present in raw HTML. If `<body>` contains mostly `<script>` tags with little text, flag as HIGH risk.
- **Content-to-Code Ratio**: `text_content_bytes / total_html_bytes * 100`. Target: >15%.
- **Script count**: Number of `<script>` tags.
- **TTFB**: Target < 500ms.

Rate each metric: EXCELLENT / GOOD / FAIR / POOR

### Step 2: Content Authority Analysis (Hedge Density)

From the fetched page content, extract the text (removing scripts, styles, nav, footer). Then:

1. Count total words in the content.
2. Search for hedge word patterns (case-insensitive):
   - **Uncertainty:** maybe, possibly, perhaps, might, could be, potentially
   - **Contrast:** however, although, nevertheless, nonetheless
   - **Perception:** it seems, it appears, arguably, apparently
   - **Opinion:** in my opinion, some believe, to some extent, I think, I believe
3. Calculate hedge density: `(hedge_count / word_count) * 100`
4. Rate:
   - <0.1% = EXCELLENT
   - 0.1-0.2% = GOOD
   - 0.2-0.5% = FAIR
   - >0.5% = POOR
5. List specific hedge words found with surrounding context.

### Step 3: Agent Infrastructure Check

Check for AgentFacts/NANDA protocol:

```bash
curl -sI "https://{domain}/.well-known/agent-facts"
```

If the endpoint returns 200:
- Fetch the JSON and validate required fields: `@context`, `id`, `agent_name`
- Check if `@context` starts with `https://nanda.dev`
- Check if `id` starts with `nanda:`
- Report: Present + Valid / Present + Invalid / Not Found

### Step 4: Discovery Strategy Assessment

If `--launch-year` was provided, calculate site age and recommend strategy:

| Site Age | Strategy | Focus |
|----------|----------|-------|
| <1 year | Web-augmented signals | Reddit, referring domains, social proof |
| 1-2 years | Hybrid approach | Web signals + basic GEO |
| 2-5 years | Full GEO optimization | Hedge density, AgentFacts, content refresh |
| 5+ years | Maintain and defend | Citation monitoring, advanced GEO |

If not provided, note: "Provide --launch-year for strategy recommendations."

### Step 5: Generate Report

```markdown
## GEO Audit Report: {url}
Generated: {timestamp}

### Technical Visibility
| Metric | Value | Rating |
|--------|-------|--------|
| HTML Size | {size} MB | {rating} |
| JS Dependency | {risk level} | {note} |
| Content-to-Code Ratio | {ratio}% | {rating} |
| Script Tags | {count} | |
| TTFB | {time}s | {rating} |

### Content Authority
| Metric | Value |
|--------|-------|
| Word Count | {count} |
| Hedge Words Found | {count} |
| Hedge Density | {density}% |
| Confidence Rating | {rating} |

Hedge examples found: {list}

### Agent Infrastructure
| Check | Status |
|-------|--------|
| AgentFacts (/.well-known/agent-facts) | Present/Missing |
| Schema Valid | Yes/No |

### Discovery Strategy
Status: {tier}
Estimated AI Visibility: {estimate}
Primary Strategy: {strategy}
Focus areas: {list}

### Priority Recommendations
1. [Most impactful action]
2. [Second priority]
3. [Third priority]
```
