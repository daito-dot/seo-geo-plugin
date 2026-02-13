# Scripts (Power User CLI Tools)

These are the original Python scripts from the `seo-geo` and `geo-optimizer` skills. They are preserved here for power users who want to run them directly from the command line.

> **Note:** The Cowork plugin uses markdown-based commands instead of executing these scripts directly. The `/seo-audit`, `/geo-audit`, etc. commands provide equivalent functionality through Claude's built-in tools (WebFetch, WebSearch, Bash).

## Available Scripts

### From seo-geo skill

| Script | Usage | Dependencies |
|--------|-------|--------------|
| `seo_audit.py` | `python3 seo_audit.py "https://example.com"` | None (stdlib only) |
| `keyword_research.py` | `python3 keyword_research.py "keyword"` | DataForSEO API |
| `competitor_gap.py` | `python3 competitor_gap.py "domain1" "domain2"` | DataForSEO API |
| `serp_analysis.py` | `python3 serp_analysis.py "keyword"` | DataForSEO API |
| `backlinks.py` | `python3 backlinks.py "domain"` | DataForSEO API |
| `domain_overview.py` | `python3 domain_overview.py "domain"` | DataForSEO API |
| `related_keywords.py` | `python3 related_keywords.py "keyword"` | DataForSEO API |
| `autocomplete_ideas.py` | `python3 autocomplete_ideas.py "keyword"` | DataForSEO API |
| `dataforseo_api.py` | API client library | requests |
| `credential.py` | API credential helper | None |

### From geo-optimizer skill

| Script | Usage | Dependencies |
|--------|-------|--------------|
| `audit-geo.py` | `python3 audit-geo.py "https://example.com"` | requests, beautifulsoup4 |
| `check-hedge-density.py` | `python3 check-hedge-density.py --url "https://example.com"` | requests, beautifulsoup4 |
| `generate-agentfacts.py` | `python3 generate-agentfacts.py --domain example.com` | requests (optional) |

## DataForSEO API Setup

Scripts that depend on DataForSEO require API credentials:

1. Sign up at [DataForSEO](https://dataforseo.com/)
2. Set environment variables:
   ```bash
   export DATAFORSEO_LOGIN="your-login"
   export DATAFORSEO_PASSWORD="your-password"
   ```
3. Or use `credential.py` to configure credentials

## Installing Dependencies

```bash
pip install requests beautifulsoup4
```
