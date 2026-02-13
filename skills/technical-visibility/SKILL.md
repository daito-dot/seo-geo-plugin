---
name: technical-visibility
description: |
  AI crawler technical requirements and content accessibility.
  HTML 1MB size limit, JavaScript dependency risk, content-to-code ratio,
  and crawler-specific optimization. Use when the user asks about AI crawlers,
  page size limits, JS rendering, or technical GEO requirements.
---

# Technical Visibility for AI Crawlers

Understanding how LLM crawlers access and process web content.

## AI Crawler Landscape

| Crawler | Renders JS | Size Limit | User-Agent |
|---------|------------|------------|------------|
| GPTBot | Yes | ~1MB | GPTBot |
| ClaudeBot | No | Unknown | ClaudeBot |
| PerplexityBot | Sometimes | ~1MB | PerplexityBot |
| Google-Extended | Yes | Standard | Google-Extended |
| Anthropic-AI | No | Unknown | anthropic-ai |

## The 1MB HTML Limit

### Research Findings (Salt.Agency & Botify)
- **18% of pages >1MB were abandoned** by AI crawlers
- Crawlers truncate or skip large payloads
- No warning or partial indexing - content simply isn't seen

### Size Budget Breakdown

| Component | Max Budget | Notes |
|-----------|------------|-------|
| Core content | 500KB | Actual article/page content |
| Navigation/UI | 200KB | Headers, footers, menus |
| Inline CSS | 100KB | Critical styles only |
| Inline JS | 100KB | Essential scripts only |
| Metadata | 50KB | Schema, OpenGraph, etc |
| Buffer | 50KB | Safety margin |

### Reducing HTML Size
1. Remove inline SVGs - link instead of embedding
2. Defer non-critical CSS
3. Remove HTML comments in production
4. Minify HTML
5. Lazy load below-fold content
6. Externalize scripts to separate files

## JavaScript Dependency Risk

Many AI crawlers don't execute JavaScript:
- Content rendered client-side is invisible
- SPAs show empty shells
- Dynamically loaded content isn't indexed

### JS Dependency Score
```
js_dependency = (rendered_text_length - raw_html_text_length) / rendered_text_length * 100
```

| Score | Risk Level | Action |
|-------|------------|--------|
| <10% | Low | Content mostly visible |
| 10-30% | Medium | Audit critical content |
| 30-50% | High | Implement SSR/SSG |
| >50% | Critical | Major architecture change needed |

### Mitigation Strategies

1. **SSR (Server-Side Rendering):** Next.js `getServerSideProps`, Nuxt, SvelteKit
2. **SSG (Static Site Generation):** Next.js `getStaticProps`, Astro, 11ty
3. **Hybrid:** Static shell + hydration, progressive enhancement
4. **Prerendering Service:** Prerender.io, Rendertron (for SPAs that can't be refactored)

## Content-to-Code Ratio

```
content_ratio = text_content_bytes / total_html_bytes * 100
```

| Ratio | Assessment |
|-------|------------|
| >25% | Excellent - Content-dense, AI-friendly |
| 15-25% | Good - Typical for content sites |
| 5-15% | Fair - Consider reducing boilerplate |
| <5% | Poor - Likely invisible to AI |

### Improving Content Ratio
1. Remove duplicate navigation
2. Trim footer bloat
3. Reduce widget HTML
4. Eliminate tracking pixels (move to JS)
5. Simplify forms

## Performance Budget

AI crawlers have timeout thresholds:

| Metric | Target |
|--------|--------|
| TTFB | <500ms |
| Full load | <3s |
| HTML delivery | <1s |

## robots.txt for AI Crawlers

```
User-agent: GPTBot
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: anthropic-ai
Allow: /

User-agent: Bingbot
Allow: /

# Block specific paths from AI training
User-agent: GPTBot
Disallow: /private/
```

## Mobile-First Considerations

AI crawlers increasingly use mobile user-agents. Watch for:
- Hamburger menus hiding content
- Accordion content collapsed by default
- "Read more" truncation
- Infinite scroll without pagination

## Technical Visibility Audit Checklist

- [ ] HTML size under 1MB
- [ ] Critical content visible without JS
- [ ] Content-to-code ratio >15%
- [ ] TTFB under 500ms
- [ ] Mobile rendering works
- [ ] robots.txt allows AI crawlers
- [ ] No infinite scroll without fallback
- [ ] Pagination present for lists
- [ ] Core content in initial HTML
- [ ] No render-blocking resources for content
