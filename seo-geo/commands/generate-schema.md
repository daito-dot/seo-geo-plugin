---
description: Interactively generate JSON-LD structured data schema for a webpage. Supports FAQPage, Article, Product, Organization, HowTo, and more.
argument-hint: [page-type] [--url url]
---

# Generate Schema

Generate JSON-LD structured data markup for SEO and GEO optimization.

## Procedure

Parse `$ARGUMENTS`:
- If a page type is provided (faq, article, product, organization, howto, software, local-business, breadcrumb), use it directly.
- If `--url` is provided, fetch the page to auto-detect the appropriate schema type.
- If neither, ask the user what type of page they need schema for.

### Step 1: Determine schema type

Available types:

| Type | Best For | GEO Impact |
|------|----------|------------|
| **faq** / FAQPage | FAQ sections, Q&A pages | +40% AI visibility |
| **article** / Article | Blog posts, news, tutorials | Standard |
| **product** / Product | E-commerce product pages | Standard |
| **organization** / Organization | About pages, company info | Standard |
| **howto** / HowTo | Tutorials, guides | Standard |
| **software** / SoftwareApplication | Tools, apps | Standard |
| **local** / LocalBusiness | Local business pages | Standard |
| **breadcrumb** / BreadcrumbList | Navigation hierarchy | Standard |
| **webpage** / WebPage | General content pages | Standard |
| **combined** | Multiple types (@graph) | High |

### Step 2: Collect information

Ask the user for the relevant fields based on schema type. Use information from `--url` page fetch if available.

**Common fields (all types):**
- Page URL
- Page title
- Description

**Type-specific fields:**

**FAQPage:** List of questions and answers (at least 3-5 recommended)

**Article:** Headline, author name/credentials, publish date, modified date, image URLs, category, word count

**Product:** Product name, SKU, brand, price, currency, availability, rating, review count

**Organization:** Name, logo URL, founding date, address, contact, social links

**HowTo:** Steps (name + instructions for each), total time, supplies needed

**SoftwareApplication:** App name, category, OS, version, download URL, price, features

**LocalBusiness:** Name, address, phone, hours, price range, geo coordinates

### Step 3: Generate the JSON-LD

Output the complete JSON-LD in a code block, ready to be added to the page's `<head>`:

```html
<script type="application/ld+json">
{generated JSON-LD here}
</script>
```

### Step 4: GEO enhancement suggestions

After generating the base schema, suggest GEO-specific enhancements:

1. **Add SpeakableSpecification** for voice search optimization:
   ```json
   "speakable": {
     "@type": "SpeakableSpecification",
     "cssSelector": ["h1", ".summary", ".key-points"]
   }
   ```

2. **Add FAQPage alongside** other schemas using `@graph` if not already FAQ type

3. **Include datePublished and dateModified** for content freshness signals

4. **Add author credentials** for E-E-A-T signals

### Step 5: Validation links

Provide links for the user to validate their schema:
- Google Rich Results Test: `https://search.google.com/test/rich-results?url={url}`
- Schema.org Validator: `https://validator.schema.org/?url={url}`

### Notes
- Always use `@context: "https://schema.org"`
- For multiple schema types on one page, use `@graph` array
- FAQPage schema provides the highest GEO impact (+40% AI visibility)
- Keep answers in FAQPage schema comprehensive and include statistics/citations
