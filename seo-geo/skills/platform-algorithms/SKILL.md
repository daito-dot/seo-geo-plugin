---
name: platform-algorithms
description: |
  Ranking factors and optimization strategies for each AI search platform:
  ChatGPT, Perplexity, Google AI Overview, Microsoft Copilot, Claude AI, and traditional Google.
  Use when the user asks about platform-specific optimization or ranking factors.
---

# Platform Algorithms

Detailed ranking factors for AI search engines and traditional search engines (2025-2026).

## Cross-Platform Summary

| Platform | Primary Index | Key Factor | Unique Requirement |
|----------|--------------|------------|-------------------|
| ChatGPT | Web (Bing-based) | Domain Authority | Content-Answer Fit |
| Perplexity | Own + Google | Semantic Relevance | FAQ Schema |
| Google SGE | Google | E-E-A-T | Knowledge Graph |
| Copilot | Bing | Bing Index | MS Ecosystem |
| Claude | Brave | Factual Density | Brave Indexing |
| Google (traditional) | Google | Backlinks | Core Web Vitals |

## 1. ChatGPT Ranking Factors

### Ranking Factor Weights
| Factor | Weight |
|--------|--------|
| **Authority & Credibility** | 40% |
| **Content Quality & Utility** | 35% |
| **Platform Trust** | 25% |

### Key Findings (SE Ranking Study - 129K domains)
| Metric | Impact |
|--------|--------|
| **Referring Domains** | Strongest predictor. >350K domains = 8.4 avg citations |
| **Domain Trust Score** | 91-96 = 6 citations; 97-100 = 8.4 citations |
| **Content Recency** | 30-day old content gets 3.2x more citations |
| **Branded vs Third-party** | Branded domains cited 11.1 points more |

### Content-Answer Fit Analysis (400K pages study)
| Factor | Relevance |
|--------|-----------|
| **Content-Answer Fit** | 55% - Most important |
| **On-Page Structure** | 14% |
| **Domain Authority** | 12% |
| **Query Relevance** | 12% |
| **Content Consensus** | 7% |

### Top Citation Sources
1. Wikipedia (7.8%)
2. Reddit (1.8%)
3. Forbes (1.1%)
4. Brand Official Sites (variable)
5. Academic Sources (variable)

### Optimization
- Build strong backlink profile
- Update content within 30 days
- Use clear H1/H2/H3 structure
- Include verifiable statistics with citations
- Write in ChatGPT's conversational style

## 2. Perplexity AI Ranking Factors

### Architecture: RAG with 3-layer reranking
1. **L1**: Basic relevance retrieval
2. **L2**: Traditional ranking factors
3. **L3**: ML quality evaluation (can discard entire result sets)

### Core Factors
| Factor | Details |
|--------|---------|
| **Authoritative Domain Lists** | Manual lists: Amazon, GitHub, academic sites get boost |
| **Freshness Signals** | Time decay algorithm |
| **Semantic Relevance** | Content similarity, not keyword matching |
| **Topical Weighting** | Tech, AI, Science topics get multipliers |
| **User Engagement** | Click rates, weekly metrics |

### Sonar Model Insights
- FAQ Schema (JSON-LD) pages cited more often
- Publicly hosted PDFs prioritized
- Content velocity matters more than keyword density
- Clear, atomic paragraphs preferred

### Technical Requirements
```
User-agent: PerplexityBot
Allow: /
```

### Optimization
- Allow PerplexityBot in robots.txt
- Implement FAQ Schema markup
- Create publicly accessible PDF resources
- Focus on semantic relevance, not keywords
- Build topical authority

## 3. Google AI Overview (SGE)

### 5-Stage Source Prioritization
1. Retrieval - Identify candidates
2. Semantic Ranking - Topical relevance
3. LLM Re-ranking - Contextual fit (Gemini)
4. E-E-A-T Evaluation - Expertise/authority/trust
5. Data Fusion - Synthesize with citations

### Key Statistics
| Metric | Value |
|--------|-------|
| AI Overviews in searches | 85%+ |
| Overlap with traditional Top 10 | Only 15% |
| SGE-optimized visibility boost | 340% |
| Authoritative citations boost | +132% |
| Authoritative tone boost | +89% |

### Optimization
- Implement comprehensive Schema markup
- Build topical authority with content clusters
- Include authoritative citations and references
- Use E-E-A-T signals (author bios, credentials)
- Optimize for Google Merchant Center (e-commerce)

## 4. Microsoft Copilot / Bing AI

### Architecture
Integrated into: Edge, Windows 11, Microsoft 365, Bing Search.
Uses **Bing Index** as primary data source.

### Ranking Factors
| Factor | Details |
|--------|---------|
| **Bing Index** | Must be indexed by Bing |
| **Microsoft Ecosystem** | LinkedIn, GitHub mentions provide boost |
| **Crawlability** | BingBot + PermaBot access |
| **Page Speed** | < 2 seconds load time |
| **Entity Clarity** | Clear definitions of entities |

### Technical Requirements
```
User-agent: Bingbot
Allow: /

User-agent: msnbot
Allow: /
```

### Optimization
- Submit site to Bing Webmaster Tools
- Use IndexNow for new content
- Optimize page speed (< 2 seconds)
- Build presence on LinkedIn, GitHub

## 5. Claude AI

### Architecture
**Important:** Claude uses **Brave Search**, NOT Google or Bing.

### Ranking Factors
| Factor | Details |
|--------|---------|
| **Brave Index** | Must be indexed by Brave Search |
| **Factual Density** | Data-rich content preferred |
| **Structural Clarity** | Easy to extract information |
| **Source Authority** | Well-sourced content |

### Key Statistic
**Crawl-to-Refer Ratio: 38,065:1** - Claude consumes massive content but is very selective about citations.

### Technical Requirements
```
User-agent: ClaudeBot
Allow: /

User-agent: anthropic-ai
Allow: /
```

### Optimization
- Ensure Brave Search indexing
- Create high factual density content
- Use clear, extractable structure
- Include verifiable data points

## 6. Traditional Google SEO (2026)

### Top 10 Ranking Factors
| Rank | Factor |
|------|--------|
| 1 | **Backlinks** - Quality referring domains |
| 2 | **E-E-A-T** - Experience, Expertise, Authority, Trust |
| 3 | **Content Quality** - Original, comprehensive, helpful |
| 4 | **Page Experience** - Core Web Vitals |
| 5 | **Mobile-First** - Non-mobile sites may not be indexed |
| 6 | **Search Intent Match** |
| 7 | **Content Freshness** |
| 8 | **Technical SEO** - Crawlable, indexable, HTTPS |
| 9 | **User Signals** - Dwell time, bounce rate, CTR |
| 10 | **Structured Data** - Schema markup |

## Universal Best Practices

1. **Allow all major bots** in robots.txt
2. **Implement Schema markup** (FAQPage, Article, Organization)
3. **Build authoritative backlinks**
4. **Update content regularly** (within 30 days)
5. **Use clear structure** (H1 > H2 > H3, lists, tables)
6. **Include statistics and citations**
7. **Optimize page speed** (< 2 seconds)
8. **Ensure mobile-friendly design**
