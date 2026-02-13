# SEO/GEO Plugin for Cowork

Comprehensive SEO and GEO (Generative Engine Optimization) plugin for Claude. Optimize websites for both traditional search engines (Google, Bing) and AI search engines (ChatGPT, Perplexity, Gemini, Copilot, Claude).

## Features

### Skills (Auto-loaded Domain Knowledge)

| Skill | Description |
|-------|-------------|
| **seo-fundamentals** | SEO audit methodology, meta tags, E-E-A-T, Core Web Vitals |
| **geo-optimization** | Princeton 9 methods, GEO metrics, AI-optimized content structure |
| **platform-algorithms** | ChatGPT/Perplexity/Google AI/Copilot/Claude ranking factors |
| **schema-markup** | JSON-LD templates (FAQPage, Article, Product, Organization, etc.) |
| **hedge-density** | Hedge word analysis, calculation, thresholds, remediation strategies |
| **agentfacts-nanda** | NANDA protocol, AgentFacts schema specification |
| **discovery-strategies** | Site age-based strategies, discovery gap analysis |
| **technical-visibility** | AI crawler requirements, HTML 1MB limit, JS dependency risk |

### Commands (Slash Commands)

| Command | Description |
|---------|-------------|
| `/seo-audit <url>` | Technical SEO audit (meta tags, robots.txt, sitemap, schema, speed) |
| `/geo-audit <url>` | GEO audit (technical visibility, hedge density, AgentFacts, strategy) |
| `/keyword-research <keyword>` | Keyword research with SEO API or WebSearch fallback |
| `/check-hedge-density <url>` | Analyze content confidence for AI citation optimization |
| `/generate-agentfacts` | Create NANDA-compliant AgentFacts JSON-LD schema |
| `/generate-schema` | Generate JSON-LD structured data for any page type |
| `/competitor-gap <url1> <url2>` | Keyword gap and competitive analysis between domains |

## Installation

### Cowork (claude.com/plugins)

1. Upload or link this plugin directory
2. Skills are automatically loaded when relevant topics are discussed
3. Commands are available via `/command-name`

### Local Development

```bash
git clone https://github.com/ReScienceLab/opc-skills.git
cd seo-geo-plugin
```

## Optional: SEO API Connection

For enhanced keyword research and competitor analysis, connect an SEO tool API via `.mcp.json`:

- **Ahrefs** - Keyword research, backlink analysis
- **Semrush** - Domain overview, position tracking
- **DataForSEO** - Keyword data, SERP analysis

Without an API connection, commands fall back to WebSearch-based analysis.

## Key Concepts

### GEO vs SEO

| Aspect | SEO | GEO |
|--------|-----|-----|
| Goal | Rank in search results | Be cited by AI |
| Signals | Backlinks, keywords | Confidence, citations, structure |
| Optimization | Meta tags, page speed | Hedge density, schema, AgentFacts |
| Platforms | Google, Bing | ChatGPT, Perplexity, Claude, Gemini |

### Princeton GEO Methods (Top 3)

1. **Cite Sources** (+40%) - Add authoritative citations
2. **Statistics Addition** (+37%) - Include specific data points
3. **Quotation Addition** (+30%) - Add expert quotes with attribution

### Critical Thresholds

| Metric | Target | Why |
|--------|--------|-----|
| Hedge Density | <0.2% | Confident content cited 3x more |
| HTML Size | <1MB | 18% of larger pages abandoned by AI crawlers |
| Page Speed | <3s | Crawler timeout avoidance |
| Content Ratio | >15% | AI-friendly content density |

## Project Structure

```
seo-geo-plugin/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── .mcp.json                # Optional SEO tool API connection
├── CONNECTORS.md            # Connector documentation
├── README.md                # This file
├── LICENSE                  # MIT License
├── skills/                  # Auto-loaded domain knowledge
│   ├── seo-fundamentals/SKILL.md
│   ├── geo-optimization/SKILL.md
│   ├── platform-algorithms/SKILL.md
│   ├── schema-markup/SKILL.md
│   ├── hedge-density/SKILL.md
│   ├── agentfacts-nanda/SKILL.md
│   ├── discovery-strategies/SKILL.md
│   └── technical-visibility/SKILL.md
├── commands/                # Slash commands
│   ├── seo-audit.md
│   ├── geo-audit.md
│   ├── keyword-research.md
│   ├── check-hedge-density.md
│   ├── generate-agentfacts.md
│   ├── generate-schema.md
│   └── competitor-gap.md
└── scripts/                 # Original Python scripts (power users)
    ├── README.md
    └── *.py
```

## Credits

- Princeton GEO Research: arXiv:2311.09735 (KDD 2024)
- SE Ranking ChatGPT Study: 129K domains analyzed
- Salt.Agency & Botify: AI crawler behavior research
- NANDA Protocol: https://nanda.dev

## License

MIT
