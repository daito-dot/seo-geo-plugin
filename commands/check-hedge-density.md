---
description: Analyze hedge density (uncertainty language) in content for AI visibility optimization. Accepts a URL, text, or file path.
argument-hint: <url|text|file>
---

# Check Hedge Density

Analyze content for uncertainty language that reduces AI citation probability.

## Procedure

Parse `$ARGUMENTS`:
- If it starts with `http://` or `https://`, treat as a URL
- If it's a file path that exists, read the file
- Otherwise, treat as inline text to analyze

### Step 1: Get content

**For URLs:** Use `WebFetch` to fetch the page. Extract the main text content (ignore navigation, footer, scripts, styles). Focus on `<main>`, `<article>`, or `<body>` content.

**For files:** Read the file content.

**For text:** Use the text directly.

### Step 2: Analyze hedge patterns

Search for these patterns (case-insensitive, word boundaries):

**Uncertainty hedges:**
- `\bmaybe\b`
- `\bpossibly\b`
- `\bperhaps\b`
- `\bmight\b`
- `\bcould be\b`
- `\bpotentially\b`

**Contrast hedges:**
- `\bhowever\b`
- `\balthough\b`
- `\bnevertheless\b`
- `\bnonetheless\b`

**Perception hedges:**
- `\bit seems\b`
- `\bit appears\b`
- `\barguably\b`
- `\bapparently\b`

**Opinion hedges:**
- `\bin my opinion\b`
- `\bsome believe\b`
- `\bto some extent\b`
- `\bi think\b`
- `\bi believe\b`

For each match, capture the surrounding context (approximately 30 characters before and after).

### Step 3: Calculate metrics

```
word_count = total words in content
hedge_count = total hedge matches
hedge_density = (hedge_count / word_count) * 100
```

### Step 4: Rate the content

| Density | Rating | Action |
|---------|--------|--------|
| <0.1% | EXCELLENT | Maintain current tone |
| 0.1-0.2% | GOOD | Minor improvements optional |
| 0.2-0.5% | FAIR | Review and reduce hedges |
| >0.5% | POOR | Significant rewrite needed |

### Step 5: Generate report

```markdown
## Hedge Density Analysis

| Metric | Value |
|--------|-------|
| Word Count | {count} |
| Hedge Words Found | {count} |
| Hedge Density | {density}% |
| Rating | {EXCELLENT/GOOD/FAIR/POOR} |

### Breakdown by Category
| Category | Count |
|----------|-------|
| Uncertainty | {count} |
| Contrast | {count} |
| Perception | {count} |
| Opinion | {count} |

### Hedges Found
1. "{hedge word}" ({category})
   Context: "...{surrounding text}..."

2. "{hedge word}" ({category})
   Context: "...{surrounding text}..."

[...up to 10 examples]

### Recommendations
{For each hedge found, provide a specific improvement suggestion:}
1. Replace "{hedge}" with {confident alternative}
2. ...

### Remediation Strategies
- **Direct Replacement:** Replace hedges with confident assertions backed by specifics
- **Quantify Claims:** Add numbers and metrics to support assertions
- **Cite Sources:** Transform uncertainty into attributed claims
- **Conditional Precision:** When uncertainty is legitimate, be precise about conditions
- **Remove Qualifiers:** Delete hedge words that add no value
```
