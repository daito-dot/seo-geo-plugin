---
description: Discover SEO/AIO competitors for a domain or keyword, then benchmark their search strength, ranking keywords, and AI citation presence. Outputs Excel and/or Word report.
argument-hint: <domain or keyword> [--depth deep] [--market JP|US|UK|...] [--format xlsx|docx|both]
---

# Find Competitors

Automatically discover competitors and benchmark their SEO and AIO (AI Overview / AI search) strength. Generate a professional report as Excel and/or Word file.

## Procedure

Parse `$ARGUMENTS`:
- If it looks like a domain (contains `.`), treat as domain-based discovery
- Otherwise, treat as keyword-based discovery
- `--depth deep` triggers extended analysis (more competitors, more keywords)
- `--market` specifies the target market (default: detect from domain TLD, fallback to US)
- `--format` specifies output format: `xlsx` (Excel), `docx` (Word), or `both` (default: `both`)

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

First, display the analysis results in chat (markdown tables). Then generate the file report(s).

### Chat Display

Show the following sections as markdown tables in the conversation:
- Executive Summary (3-5 sentences)
- Competitor Overview Table
- Keyword Battle Map (top 10)
- Key findings and top 3 recommended actions

### File Report Generation

After the chat display, generate the report file(s). First ensure dependencies are installed:

```bash
pip install -q openpyxl python-docx
```

#### Excel Report (.xlsx)

Generate using the following Python approach via Bash:

```bash
python3 -c "
import openpyxl
from openpyxl.styles import Font, PatternFill, Alignment, Border, Side
from openpyxl.utils import get_column_letter
from datetime import datetime

wb = openpyxl.Workbook()

# --- Styles ---
header_font = Font(bold=True, color='FFFFFF', size=11)
header_fill = PatternFill(start_color='2F5496', end_color='2F5496', fill_type='solid')
subheader_fill = PatternFill(start_color='D6E4F0', end_color='D6E4F0', fill_type='solid')
good_fill = PatternFill(start_color='C6EFCE', end_color='C6EFCE', fill_type='solid')
warn_fill = PatternFill(start_color='FFEB9C', end_color='FFEB9C', fill_type='solid')
bad_fill = PatternFill(start_color='FFC7CE', end_color='FFC7CE', fill_type='solid')
thin_border = Border(
    left=Side(style='thin'), right=Side(style='thin'),
    top=Side(style='thin'), bottom=Side(style='thin')
)

def style_header(ws, row, cols):
    for col in range(1, cols + 1):
        cell = ws.cell(row=row, column=col)
        cell.font = header_font
        cell.fill = header_fill
        cell.alignment = Alignment(horizontal='center', wrap_text=True)
        cell.border = thin_border

def style_cells(ws, start_row, end_row, cols):
    for row in range(start_row, end_row + 1):
        for col in range(1, cols + 1):
            cell = ws.cell(row=row, column=col)
            cell.border = thin_border
            cell.alignment = Alignment(wrap_text=True)

def auto_width(ws, cols):
    for col in range(1, cols + 1):
        max_len = 0
        for row in ws.iter_rows(min_col=col, max_col=col):
            for cell in row:
                if cell.value:
                    max_len = max(max_len, len(str(cell.value)))
        ws.column_dimensions[get_column_letter(col)].width = min(max_len + 4, 40)

# === Sheet 1: Summary ===
ws = wb.active
ws.title = 'Summary'
# ... populate with Executive Summary, Competitor Overview data ...

# === Sheet 2: Keyword Battle Map ===
ws2 = wb.create_sheet('Keyword Battle Map')
# ... populate with keyword comparison grid ...

# === Sheet 3: AI Visibility ===
ws3 = wb.create_sheet('AI Visibility')
# ... populate with AI Overview, ChatGPT citations, technical readiness ...

# === Sheet 4: Technical Comparison ===
ws4 = wb.create_sheet('Technical Comparison')
# ... populate with robots.txt, schema, AgentFacts, HTML size data ...

# === Sheet 5: Gap Analysis ===
ws5 = wb.create_sheet('Gap Analysis')
# ... populate with keyword gaps, content gaps, opportunities ...

# === Sheet 6: Action Plan ===
ws6 = wb.create_sheet('Action Plan')
# ... populate with prioritized recommendations ...

wb.save('{output_path}.xlsx')
print('Saved: {output_path}.xlsx')
"
```

The Excel file MUST contain these 6 sheets:

1. **Summary** — Competitor overview table with color-coded SEO strength and AI readiness
2. **Keyword Battle Map** — Full keyword grid with rank positions, color-coded (green=top 3, yellow=4-10, red=not ranking)
3. **AI Visibility** — Platform-by-platform AI citation and readiness comparison
4. **Technical Comparison** — robots.txt, schema, HTML size, content freshness per competitor
5. **Gap Analysis** — All keyword/content/AIO gaps with volume and difficulty
6. **Action Plan** — Prioritized actions with impact, effort, and target competitor

Apply conditional formatting:
- Green cells for strengths / top positions
- Yellow for moderate / opportunities
- Red for weaknesses / missing items

#### Word Report (.docx)

Generate using the following Python approach via Bash:

```bash
python3 -c "
from docx import Document
from docx.shared import Inches, Pt, Cm, RGBColor
from docx.enum.text import WD_ALIGN_PARAGRAPH
from docx.enum.table import WD_TABLE_ALIGNMENT
from datetime import datetime

doc = Document()

# --- Styles ---
style = doc.styles['Normal']
style.font.name = 'Calibri'
style.font.size = Pt(10.5)

# Title
title = doc.add_heading('Competitive SEO/AIO Analysis Report', level=0)
doc.add_paragraph(f'Target: {domain}')
doc.add_paragraph(f'Market: {market}')
doc.add_paragraph(f'Generated: {datetime.now().strftime(\"%Y-%m-%d %H:%M\")}')
doc.add_paragraph(f'Competitors Analyzed: {num_competitors}')
doc.add_page_break()

# Table of Contents
doc.add_heading('Table of Contents', level=1)
toc_items = [
    '1. Executive Summary',
    '2. Competitor Overview',
    '3. SEO Strength Analysis',
    '4. AI Visibility Analysis',
    '5. Keyword Battle Map',
    '6. Technical Readiness',
    '7. Gap Analysis',
    '8. Action Plan & Recommendations',
]
for item in toc_items:
    doc.add_paragraph(item)
doc.add_page_break()

# ... Each section as heading + paragraphs + tables ...
# Use doc.add_table(rows, cols) for data tables
# Apply table style: 'Light Grid Accent 1' or 'Medium Shading 1 Accent 1'

doc.save('{output_path}.docx')
print('Saved: {output_path}.docx')
"
```

The Word document MUST contain these sections:

1. **Cover page** — Title, target domain, market, date, competitor count
2. **Table of Contents**
3. **Executive Summary** — 3-5 sentence overview with key findings
4. **Competitor Overview** — Table with all competitors, SEO strength, AI readiness
5. **SEO Strength Analysis** — Detailed per-competitor SEO metrics
6. **AI Visibility Analysis** — Platform-by-platform citation data
7. **Keyword Battle Map** — Table with rank positions per keyword per competitor
8. **Technical Readiness** — robots.txt, schema, HTML size comparison table
9. **Gap Analysis** — Keyword gaps, content gaps, AIO gaps
10. **Action Plan** — Prioritized quick wins + strategic investments table

Format requirements:
- Use professional table styles with alternating row colors
- Bold key metrics and findings
- Include section numbers
- A4 page size with 2.5cm margins

### File Naming and Location

Save files to the user's current working directory:
- Excel: `{domain}_competitor_analysis_{YYYYMMDD}.xlsx`
- Word: `{domain}_competitor_analysis_{YYYYMMDD}.docx`

After saving, report the file paths to the user.

---

## Follow-Up

After presenting the analysis and generating files, ask:

"Report files generated:
- 📊 `{filename}.xlsx`
- 📄 `{filename}.docx`

Would you like me to:
- Deep-dive into a specific competitor?
- Run `/competitor-gap` against the strongest competitor?
- Create a content plan targeting the keyword gaps?
- Run `/seo-audit` or `/geo-audit` on your site for detailed recommendations?
- Check hedge density on competitor content vs yours?"
