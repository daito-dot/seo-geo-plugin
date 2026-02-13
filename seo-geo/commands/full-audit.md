---
description: Run a comprehensive SEO + GEO + competitive analysis on a site. Combines all audit commands into one integrated workflow and outputs Excel/Word reports.
argument-hint: <domain> [--market JP|US|UK|...] [--depth deep] [--format xlsx|docx|both]
---

# Full Audit

Run a complete, integrated SEO/GEO/competitive analysis on a single domain. This command orchestrates all individual audit commands in sequence and produces a unified report.

## Procedure

Parse `$ARGUMENTS`:
- `domain` (required): Target domain or URL
- `--market`: Target market (default: detect from TLD, fallback to US)
- `--depth deep`: Extended analysis with more keywords and competitors
- `--format`: Output format — `xlsx`, `docx`, or `both` (default: `both`)

Normalize the domain: strip `https://`, trailing slashes. Keep the base domain for competitor research, use full URL for page-level audits (default to homepage).

---

### Phase 1: Technical SEO Audit

Perform the same analysis as `/seo-audit`:

1. **Fetch the homepage** with `WebFetch`
2. **Extract meta tags**: title (length, keyword presence), meta description (length), H1, OG tags, Twitter Cards
3. **Count JSON-LD schema blocks** and identify types (FAQPage, Article, Organization, etc.)
4. **Check robots.txt**: exists? AI bots allowed/blocked? (GPTBot, ClaudeBot, PerplexityBot, anthropic-ai, Bingbot)
5. **Check sitemap.xml**: exists? URL count?
6. **Measure performance**:
   ```bash
   curl -o /dev/null -s -w "TTFB:%{time_starttransfer} Total:%{time_total} Size:%{size_download}" "https://{domain}"
   ```
7. **Check HTTPS** and redirects

Store results in internal data structure for the final report.

---

### Phase 2: GEO Audit

Perform the same analysis as `/geo-audit`:

1. **HTML size check**: raw byte size, risk assessment (< 1MB = safe)
2. **JS dependency assessment**: script tag count, raw text length, content-to-code ratio
3. **Hedge density analysis**:
   - Extract main text content (strip scripts, styles, nav, footer)
   - Count hedge words across 4 categories (uncertainty, contrast, perception, opinion)
   - Calculate density: `(hedge_count / word_count) * 100`
   - Rate: EXCELLENT (<0.1%) / GOOD (<0.2%) / FAIR (<0.5%) / POOR (>0.5%)
   - List top 10 hedge examples with context
4. **AgentFacts check**: `curl -sI https://{domain}/.well-known/agent-facts`
   - If 200: validate @context, id, agent_name fields
5. **Discovery strategy**: estimate site age and recommend tier-based strategy

Store results.

---

### Phase 3: Competitor Discovery & Benchmarking

Perform the same analysis as `/find-competitors`:

1. **Discover 5-10 competitors** via ~~SEO API or WebSearch fallback
2. **SEO strength** per competitor: DA, organic KWs, traffic estimate, top keywords
3. **AIO presence** per competitor: AI Overview appearances, ChatGPT citations, AgentFacts
4. **Technical readiness** per competitor: robots.txt AI policy, HTML size, Schema types
5. **Keyword battle map**: top 15-20 keywords mapped across all competitors

Store results.

---

### Phase 4: Deep Dive on Top Competitor

Automatically select the strongest competitor (highest SEO strength + most AI citations). Run `/competitor-gap` style analysis:

1. **Keyword gaps**: keywords where top competitor ranks but user doesn't
2. **Content gaps**: topics/formats competitor covers that user is missing
3. **Technical gaps**: Schema, AgentFacts, AI bot access differences
4. **AIO gaps**: queries where competitor gets AI citations but user doesn't

Store results.

---

### Phase 5: Keyword Opportunities

Run `/keyword-research` style analysis for the user's primary keywords:

1. Identify 3-5 primary keywords from the site's title, H1, meta description
2. For each, research:
   - Related keywords and long-tail opportunities
   - Search intent classification
   - Competitor coverage
3. Compile top 20 keyword opportunities ranked by potential impact

Store results.

---

### Phase 6: Hedge Density on Key Pages

Beyond the homepage (Phase 2), check hedge density on 2-3 additional important pages:

1. Identify key pages from sitemap or navigation (blog, about, product/service pages)
2. For each, run hedge density analysis
3. Compare scores across pages

Store results.

---

### Phase 7: Recommendations Generation

Synthesize all findings into prioritized recommendations:

#### Quick Wins (This Week)
- Fix missing/broken meta tags
- Add missing Schema markup (especially FAQPage)
- Update robots.txt to allow AI bots
- Remove high-impact hedge words from key pages

#### Short-term (This Month)
- Create content for top keyword gaps
- Implement AgentFacts if missing
- Refresh outdated content (>30 days)
- Improve page speed if TTFB >500ms

#### Strategic (This Quarter)
- Build topical authority in identified content gaps
- Develop content cluster strategy
- Implement comprehensive Schema across site
- Hedge density remediation across all key pages

#### Long-term (6+ Months)
- AI citation monitoring program
- Regular competitive benchmarking cadence
- AgentFacts maintenance and updates
- Protocol innovation adoption

---

## Output

### Chat Display

Display a condensed summary in the conversation:

```markdown
## Full Audit Complete: {domain}

### Scores at a Glance
| Category | Score | Rating |
|----------|-------|--------|
| Technical SEO | {score}/100 | {rating} |
| GEO Readiness | {score}/100 | {rating} |
| AI Visibility | {score}/100 | {rating} |
| Content Confidence | {hedge_density}% | {rating} |
| Competitive Position | #{position} of {total} | {rating} |

### Top 5 Actions
1. {highest impact action}
2. {second action}
3. {third action}
4. {fourth action}
5. {fifth action}

### Key Findings
- {finding 1}
- {finding 2}
- {finding 3}

Full reports saved as Excel and Word files (see below).
```

### Score Calculation

Calculate scores (0-100) for each category:

**Technical SEO Score:**
- Title tag present and correct length: +15
- Meta description present and correct length: +10
- H1 present: +10
- Schema markup present: +15 (bonus +5 for FAQPage)
- robots.txt exists and allows AI bots: +15
- Sitemap exists: +10
- HTTPS: +10
- Page speed <3s: +10
- Mobile meta viewport: +5

**GEO Readiness Score:**
- HTML < 1MB: +20
- JS dependency low: +15
- Content-to-code ratio >15%: +15
- Hedge density <0.2%: +20
- AgentFacts present and valid: +15
- FAQPage schema: +15

**AI Visibility Score:**
- AI bots allowed in robots.txt: +25
- Schema markup for AI extraction: +20
- Content confidence (low hedge density): +20
- AgentFacts/NANDA: +15
- Seen in AI Overview/ChatGPT: +20

### File Report Generation

First install dependencies:
```bash
pip install -q openpyxl python-docx
```

#### Excel Report (.xlsx)

Generate a comprehensive Excel workbook with these sheets:

1. **Dashboard** — Scores at a glance, radar chart data, key metrics summary
   - Category scores with color coding (green >80, yellow 50-80, red <50)
   - Overall grade: A (90+) / B (75-89) / C (60-74) / D (40-59) / F (<40)

2. **SEO Audit** — Full technical SEO findings
   - Meta tags analysis table
   - Schema markup inventory
   - robots.txt status
   - Sitemap status
   - Performance metrics

3. **GEO Audit** — AI visibility technical factors
   - HTML size and risk
   - JS dependency assessment
   - Content-to-code ratio
   - AgentFacts validation

4. **Hedge Density** — Content confidence analysis per page
   - Page-by-page hedge density scores
   - Hedge word inventory with categories
   - Remediation suggestions per hedge found

5. **Competitor Overview** — All competitors benchmarked
   - SEO strength comparison
   - AI readiness comparison
   - Key metric comparison table

6. **Keyword Battle Map** — Full keyword grid
   - Color-coded rank positions (green=top 3, yellow=4-10, red=not ranking)
   - AI Overview presence per keyword
   - Opportunity score per keyword

7. **AI Visibility** — Platform-by-platform analysis
   - Google AI Overview presence
   - ChatGPT citation status
   - AgentFacts comparison
   - Technical AI readiness per competitor

8. **Gap Analysis** — All identified gaps
   - Keyword gaps with volume and difficulty
   - Content gaps with recommended formats
   - AIO gaps with opportunity assessment

9. **Action Plan** — Prioritized recommendations
   - Quick wins / Short-term / Strategic / Long-term
   - Each with: action, impact, effort, target, category

Apply formatting:
- Header row: dark blue background, white bold text
- Alternating row colors for readability
- Conditional coloring: green (good), yellow (warning), red (critical)
- Auto-fitted column widths
- Frozen header rows

#### Word Report (.docx)

Generate a professional Word document with these sections:

1. **Cover Page**
   - Title: "Comprehensive SEO/GEO Audit Report"
   - Domain, market, date, auditor (Claude AI)
   - Overall grade and score summary

2. **Table of Contents**

3. **Executive Summary** (1 page)
   - Overall assessment
   - Top 3 strengths
   - Top 3 critical issues
   - Competitive position summary

4. **Scores Dashboard**
   - Score table for all categories
   - Overall grade with explanation

5. **Technical SEO Audit**
   - Meta tags analysis with pass/fail table
   - Schema markup inventory
   - robots.txt and sitemap status
   - Performance metrics
   - Recommendations

6. **GEO Readiness Audit**
   - HTML size assessment
   - JS dependency analysis
   - Content-to-code ratio
   - AgentFacts status
   - Discovery strategy recommendation

7. **Content Confidence (Hedge Density)**
   - Per-page analysis table
   - Worst offenders list
   - Before/after improvement examples
   - Remediation priority

8. **Competitive Landscape**
   - Competitor overview table
   - SEO strength comparison
   - AI visibility comparison
   - Key takeaways

9. **Keyword Analysis**
   - Keyword battle map table
   - Top opportunities
   - Gap analysis

10. **Action Plan**
    - Quick Wins table (this week)
    - Short-term actions (this month)
    - Strategic investments (this quarter)
    - Long-term roadmap

11. **Appendix**
    - Full hedge word inventory
    - Complete keyword list
    - Technical check details
    - Methodology notes

Format:
- A4, 2.5cm margins
- Calibri 10.5pt body, section numbering
- Professional table styles with alternating row colors
- Bold key metrics, color-coded ratings where possible
- Page breaks between major sections

### File Naming

Save to user's current working directory:
- `{domain}_full_audit_{YYYYMMDD}.xlsx`
- `{domain}_full_audit_{YYYYMMDD}.docx`

---

## Follow-Up

After generating reports:

"Audit complete for {domain}.

Scores: SEO {score}/100 | GEO {score}/100 | AI Visibility {score}/100 | Overall Grade: {grade}

Reports generated:
- 📊 `{filename}.xlsx` (9 sheets)
- 📄 `{filename}.docx` ({page_count} pages)

Would you like me to:
- Deep-dive into a specific area (SEO/GEO/competitors/keywords)?
- Start implementing the Quick Win actions?
- Generate missing Schema or AgentFacts for your site?
- Run the same audit on a competitor for comparison?
- Set up a monthly re-audit schedule?"
