---
name: SEO Tool Connector
connector: ~~SEO
description: Optional connection to SEO tool APIs for advanced keyword research, competitor analysis, and backlink data.
---

# SEO Tool Connector (~~SEO)

This plugin optionally connects to SEO tool APIs for enhanced functionality.

## Supported Tools

| Tool | Use Case | Setup |
|------|----------|-------|
| **Ahrefs** | Keyword research, backlink analysis, competitor gap | API key via Ahrefs dashboard |
| **Semrush** | Keyword research, domain overview, position tracking | API key via Semrush account |
| **DataForSEO** | Keyword data, SERP analysis, competitor intersection | Login + password credentials |

## When Connected (~~SEO available)

Commands that benefit from the SEO connector:
- `/keyword-research` - Uses API for accurate search volume, difficulty, and CPC data
- `/competitor-gap` - Uses API for domain intersection analysis
- `/seo-audit` - Can pull backlink and domain authority data

## When Not Connected (Fallback)

All commands gracefully fall back to **WebSearch**-based analysis:
- `/keyword-research` - Searches for keyword data from public sources
- `/competitor-gap` - Compares visible content and rankings via web search
- `/seo-audit` - Performs technical audit using direct URL fetching

## Configuration

To enable the SEO connector, configure `.mcp.json` with your chosen tool's MCP server.
