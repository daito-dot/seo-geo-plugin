---
description: Run a technical SEO audit on a URL. Checks meta tags, robots.txt, sitemap, schema markup, page speed, and AI bot access.
argument-hint: <url>
---

# SEO Audit

Perform a comprehensive technical SEO audit on the provided URL.

## Procedure

Given the target URL `$ARGUMENTS`, execute the following steps:

### Step 1: Fetch the page and extract meta tags

Use `WebFetch` to retrieve the page content. Analyze the HTML for:

- **Title tag**: Extract `<title>` content. Check length (target: 50-60 chars). Check if it contains the likely primary keyword.
- **Meta description**: Extract `<meta name="description">` content. Check length (target: 150-160 chars).
- **H1 tag**: Extract the first `<h1>`. Verify only one H1 exists per page.
- **Open Graph tags**: Check for og:title, og:description, og:image, og:url, og:type.
- **Twitter Card tags**: Check for twitter:card, twitter:title, twitter:description, twitter:image.
- **JSON-LD schema**: Count `application/ld+json` script blocks. Identify schema types present.

### Step 2: Check robots.txt

Use `WebFetch` on `{origin}/robots.txt`. Check:

- Does robots.txt exist?
- Are these AI bots mentioned (allowed or blocked)?
  - GPTBot
  - PerplexityBot
  - ClaudeBot
  - anthropic-ai
  - ChatGPT-User
  - Bingbot
  - Google-Extended

### Step 3: Check sitemap

Use `WebFetch` on `{origin}/sitemap.xml`. Check:

- Does sitemap.xml exist?
- Does it contain `<urlset>` or `<sitemapindex>`?
- Approximate number of URLs listed

### Step 4: Check page performance

Use `Bash` to measure load time:
```bash
curl -o /dev/null -s -w "TTFB: %{time_starttransfer}s\nTotal: %{time_total}s\nSize: %{size_download} bytes\n" "{url}"
```

Evaluate:
- TTFB < 500ms (good) / < 1s (acceptable) / > 1s (slow)
- Total load < 3s (good) / > 3s (slow)
- HTML size < 1MB (safe for AI crawlers) / > 1MB (risk of abandonment)

### Step 5: Check HTTPS and redirects

```bash
curl -sI "{url}" | head -20
```

Verify:
- HTTPS is enabled
- Proper redirects (301 from http to https)

### Step 6: Generate report

Present results in this format:

```markdown
## SEO Audit Report: {url}

### Meta Tags
| Element | Status | Value |
|---------|--------|-------|
| Title | OK/MISSING | "{title}" ({length} chars) |
| Description | OK/MISSING | "{desc}" ({length} chars) |
| H1 | OK/MISSING | "{h1}" |
| OG Tags | OK/MISSING | {details} |
| JSON-LD | {count} blocks | {types} |

### Technical
| Check | Status | Details |
|-------|--------|---------|
| HTTPS | OK/FAIL | |
| robots.txt | OK/MISSING | |
| AI Bot Access | {status} | {bots allowed/blocked} |
| Sitemap | OK/MISSING | {url count} |
| TTFB | {time}s | {rating} |
| Page Size | {size} | {rating} |

### Recommendations
1. [Priority actions based on findings]
2. ...
```

### Step 7: GEO quick check

Additionally note:
- Whether FAQPage schema is present (critical for +40% AI visibility)
- Whether SpeakableSpecification is present
- Content structure quality (heading hierarchy, lists, tables)
- Whether content appears JS-dependent
