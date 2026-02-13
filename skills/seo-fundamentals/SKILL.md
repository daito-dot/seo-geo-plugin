---
name: seo-fundamentals
description: |
  Traditional SEO audit methodology, meta tag optimization, E-E-A-T signals,
  Core Web Vitals, and comprehensive on-page/off-page SEO checklist.
  Use when the user asks about SEO audits, meta tags, page speed, indexing, or search rankings.
---

# SEO Fundamentals

Comprehensive SEO (Search Engine Optimization) knowledge for auditing and optimizing websites for traditional search engines (Google, Bing).

## Key Concepts

**SEO** optimizes websites for traditional search engine rankings. Unlike GEO (which focuses on AI citations), SEO focuses on ranking in search result pages.

## SEO Audit Checklist

### Technical SEO

#### P0 - Critical
- `robots.txt` allows important pages
- Site is accessible (no 5xx errors)
- HTTPS enabled (valid SSL certificate)
- Mobile-responsive design
- No critical pages blocked by `noindex`
- Site is indexed in Google (`site:domain.com`)

#### P1 - Important
- `robots.txt` allows AI bots (GPTBot, PerplexityBot, ClaudeBot)
- XML sitemap exists and is submitted
- Site is indexed in Bing (for Copilot visibility)
- Canonical tags properly implemented
- No duplicate content issues
- Page load time < 3 seconds
- LCP (Largest Contentful Paint) < 2.5s

#### P2 - Recommended
- FID (First Input Delay) < 100ms
- CLS (Cumulative Layout Shift) < 0.1
- Images optimized (WebP format, lazy loading)
- CSS/JS minified
- GZIP/Brotli compression enabled
- CDN configured

### On-Page SEO

#### P0 - Critical
- Unique `<title>` tag (50-60 characters) containing primary keyword
- Unique `<meta description>` (150-160 characters)
- Single H1 tag per page containing primary keyword

#### P1 - Important
- Logical heading hierarchy (H1 > H2 > H3)
- All images have `alt` attributes
- Internal links to related content
- No broken links (404s)
- Descriptive anchor text

#### P2 - Recommended
- Open Graph tags (og:title, og:description, og:image, og:url, og:type)
- Twitter Card tags (twitter:card, twitter:title, twitter:description, twitter:image)
- Short paragraphs (2-3 sentences)
- Bullet points for lists, tables for comparisons

### Schema Markup (Structured Data)

#### P1 - Important
- Organization schema on homepage
- WebPage schema on all pages
- Article schema on blog posts
- Schema passes Google Rich Results Test

#### P2 - GEO Enhanced
- FAQPage schema on FAQ sections (+40% AI visibility)
- BreadcrumbList schema for navigation
- SpeakableSpecification for voice search
- datePublished and dateModified included
- Author information with credentials

## Meta Tags Template

```html
<title>{Primary Keyword} - {Brand} | {Secondary Keyword}</title>
<meta name="description" content="{Compelling description with keyword, 150-160 chars}">

<!-- Open Graph -->
<meta property="og:title" content="{Title}">
<meta property="og:description" content="{Description}">
<meta property="og:image" content="{Image URL 1200x630}">
<meta property="og:url" content="{Canonical URL}">
<meta property="og:type" content="website">

<!-- Twitter Cards -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="{Title}">
<meta name="twitter:description" content="{Description}">
<meta name="twitter:image" content="{Image URL}">
```

## Core Web Vitals

| Metric | Good | Needs Improvement | Poor |
|--------|------|-------------------|------|
| **LCP** (Largest Contentful Paint) | < 2.5s | 2.5-4s | > 4s |
| **FID** (First Input Delay) | < 100ms | 100-300ms | > 300ms |
| **CLS** (Cumulative Layout Shift) | < 0.1 | 0.1-0.25 | > 0.25 |

## E-E-A-T Signals

| Signal | How to Demonstrate |
|--------|-------------------|
| **Experience** | First-hand experience, case studies |
| **Expertise** | Author credentials, detailed knowledge |
| **Authoritativeness** | Backlinks, mentions, citations |
| **Trustworthiness** | Accurate info, transparent, secure site |

### E-E-A-T Checklist
- Author bios with credentials
- About page with company info
- Contact information visible
- Privacy policy and terms
- Trust badges/certifications if applicable
- Customer reviews/testimonials

## Off-Page SEO

### Backlinks
- Quality backlinks from relevant sites
- Diverse referring domains
- No toxic/spammy backlinks
- Brand mentions (even without links)

### Social Presence
- Active social media profiles
- Links to social profiles on website
- Consistent branding across platforms

## Content Strategy

- All pages have unique, valuable content
- No thin content (< 300 words for main pages)
- Content matches search intent
- Content is up-to-date (within 30 days for news/tech)
- Primary keyword identified for each page
- No keyword cannibalization

## Monitoring & Analytics

### Setup
- Google Analytics installed
- Google Search Console connected
- Bing Webmaster Tools connected
- Sitemap submitted to both

### Regular Checks
- Weekly: Check Search Console for errors
- Weekly: Review Core Web Vitals
- Monthly: Analyze organic traffic trends
- Quarterly: Full SEO audit

## Priority Matrix

| Priority | Task | Impact |
|----------|------|--------|
| **Critical** | Fix crawl errors | Blocks indexing |
| **Critical** | HTTPS enabled | Trust + ranking |
| **High** | Core Web Vitals | UX + ranking |
| **High** | Mobile-friendly | 60%+ traffic |
| **High** | FAQPage schema | +40% AI visibility |
| **Medium** | Meta descriptions | CTR improvement |
| **Medium** | Internal linking | Authority distribution |
| **Low** | Social meta tags | Share appearance |
