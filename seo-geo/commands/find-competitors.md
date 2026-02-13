---
description: Discover SEO/AIO competitors for a domain or keyword, then benchmark their search strength, ranking keywords, and AI citation presence.
argument-hint: <domain or keyword> [--depth deep] [--market JP|US|UK|...]
---

# Find Competitors

Automatically discover competitors and benchmark their SEO and AIO (AI Overview / AI search) strength.

## Procedure

Parse `$ARGUMENTS`:
- If it looks like a domain (contains `.`), treat as domain-based discovery
- Otherwise, treat as keyword-based discovery
- `--depth deep` triggers extended analysis (more competitors, more keywords)
- `--market` specifies the target market (default: detect from domain TLD, fallback to US)

---

### Phase 1: Competitor Discovery

#### If ~~SEO is connected (Ahrefs/Semrush)

Use the SEO API to pull:
- Organic competitor domains (domains competing for the same keywords)
- Top 5-10 competitors ranked by keyword overlap percentage

#### If no ~~SEO (WebSearch fallback)

Run these searches to identify competitors:

```
WebSearch: "{domain} competitors"
WebSearch: "{domain} alternatives"
WebSearch: "companies like {domain}"
WebSearch: "site:{domain}" (to understand what they do)
```

If keyword-based:
```
WebSearch: "{keyword} best tools OR services OR platforms 2026"
WebSearch: "{keyword} top companies"
WebSearch: "{keyword} market leaders"
```

From results, extract 5-10 competitor domains. Prioritize:
- Direct product/service competitors (same offering)
- Content competitors (ranking for the same keywords)
- Exclude generic platforms (Wikipedia, Reddit, YouTube) unless they dominate the SERP

---

### Phase 2: SEO Strength Analysis

For each competitor (and the user's own domain), gather:

#### If ~~SEO is connected
- Domain Rating / Domain Authority
- Total organic keywords
- Estimated organic traffic
- Top 10 ranking keywords with positions
- Referring domains count

#### If no ~~SEO (WebSearch fallback)

For each competitor:
```
WebSearch: "site:{competitor} {main keyword}"
WebSearch: "{competitor} domain authority OR domain rating"
WebSearch: "{competitor} organic traffic estimate"
```

Also use `WebFetch` on the competitor's homepage to check:
- Title tag and meta description (keyword targeting)
- Schema markup presence (JSON-LD count and types)
- robots.txt AI bot policy
- Content volume (blog, resources section)

Estimate relative SEO strength on a scale: Strong / Moderate / Emerging / Weak

---

### Phase 3: AIO (AI Overview / AI Search) Presence Analysis

For each competitor, check AI search visibility:

#### 3a. Google AI Overview check

Pick the top 5 keywords relevant to the market. For each:
```
WebSearch: "{keyword}"
```
Note which competitors appear in AI Overview snippets or featured snippets.

#### 3b. AI citation check

For key branded and non-branded queries, check how AI platforms reference each competitor:

```
WebSearch: "ChatGPT {competitor name} recommendation"
WebSearch: "Perplexity {competitor name}"
WebSearch: "{main keyword} best according to AI"
```

#### 3c. Technical AI readiness

For each competitor, use `WebFetch` or `Bash` (curl) to check:

```bash
# AgentFacts presence
curl -sI "https://{competitor}/.well-known/agent-facts" | head -5

# robots.txt AI bot policy
curl -s "https://{competitor}/robots.txt" | grep -iE "GPTBot|ClaudeBot|PerplexityBot|anthropic"

# HTML size (1MB limit for AI crawlers)
curl -sI "https://{competitor}" | grep -i content-length

# Schema markup count
```

Rate AI readiness: AI-Ready / Partial / Not Optimized

---

### Phase 4: Keyword Battle Map

Identify the top 15-20 keywords in the market and map each competitor's presence:

#### If ~~SEO is connected
Pull keyword intersection data across all discovered competitors.

#### If no ~~SEO
For each key keyword:
```
WebSearch: "{keyword}"
```
Check which competitors appear in the top 10 organic results, and which appear in AI Overview.

---

### Phase 5: Gap & Opportunity Analysis

Compare the user's domain against all competitors to identify:

1. **Keyword gaps**: Keywords competitors rank for that the user doesn't
2. **AIO gaps**: Topics where competitors get AI citations but the user doesn't
3. **Technical gaps**: Schema, AgentFacts, AI crawler access differences
4. **Content gaps**: Content types or topics competitors cover
5. **Quick wins**: Low-difficulty keywords where competitors are weak

---

## Output

### Executive Summary

3-5 sentences summarizing the competitive landscape:
- Who are the main competitors
- Where the user stands relative to them
- The biggest opportunity

### Competitor Overview Table

| # | Competitor | Est. SEO Strength | Organic KWs | AI Readiness | AI Citations | Top Keyword |
|---|-----------|-------------------|-------------|-------------|-------------|-------------|
| 1 | {comp1} | Strong | ~X,XXX | AI-Ready | Seen in ChatGPT | "{kw}" |
| 2 | {comp2} | Moderate | ~X,XXX | Partial | Not seen | "{kw}" |
| 3 | {comp3} | ... | ... | ... | ... | ... |
| -- | **Your site** | **{rating}** | **~X,XXX** | **{status}** | **{status}** | **"{kw}"** |

### Keyword Battle Map

| Keyword | Vol. | Your Rank | Comp 1 | Comp 2 | Comp 3 | In AI Overview? | Owner |
|---------|------|-----------|--------|--------|--------|-----------------|-------|
| {kw1} | High | -- | #3 | #7 | #1 | Yes (Comp 3) | Comp 3 |
| {kw2} | Med | #12 | #5 | -- | #2 | No | Comp 1 |
| ... | | | | | | | |

### AI Visibility Comparison

| Platform | Your Site | Comp 1 | Comp 2 | Comp 3 |
|----------|----------|--------|--------|--------|
| Google AI Overview | Not seen | 2 queries | 0 | 3 queries |
| ChatGPT citation | Not seen | Mentioned | Not seen | Frequently cited |
| AgentFacts | No | No | No | Yes |
| AI Bot Access | Partial | Full | Blocked | Full |
| Schema (FAQ) | No | Yes | No | Yes |

### Technical Readiness Comparison

| Feature | Your Site | Comp 1 | Comp 2 | Comp 3 |
|---------|----------|--------|--------|--------|
| robots.txt AI bots | {status} | {status} | {status} | {status} |
| HTML < 1MB | {status} | {status} | {status} | {status} |
| JSON-LD Schema | {count} types | {count} | {count} | {count} |
| FAQPage Schema | Yes/No | Yes/No | Yes/No | Yes/No |
| Content Freshness | {date} | {date} | {date} | {date} |

### Gap Analysis & Opportunities

#### Quick Wins (This Week)
1. {Action} — {Rationale} — Impact: HIGH
2. ...

#### Content Opportunities (This Month)
1. Create content for "{keyword}" — Competitors rank but content is weak
2. ...

#### AIO Opportunities (This Quarter)
1. Add FAQPage schema — Competitors without it are missing AI Overview
2. Implement AgentFacts — No competitor has this yet = first-mover advantage
3. ...

#### Strategic Moves (Long-term)
1. Build topical authority in {topic cluster} — Competitor coverage is thin
2. ...

### Recommended Priority

| Priority | Action | Target Competitor | Expected Impact |
|----------|--------|-------------------|-----------------|
| 1 | {action} | Beat {comp} | {impact} |
| 2 | {action} | Match {comp} | {impact} |
| 3 | {action} | Leapfrog {comp} | {impact} |

---

## Follow-Up

After presenting the analysis, ask:

"Would you like me to:
- Deep-dive into a specific competitor?
- Run `/competitor-gap` against the strongest competitor?
- Create a content plan targeting the keyword gaps?
- Run `/seo-audit` or `/geo-audit` on your site for detailed recommendations?
- Check hedge density on competitor content vs yours?"
