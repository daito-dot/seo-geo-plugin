---
name: schema-markup
description: |
  JSON-LD structured data templates for SEO and GEO optimization.
  Includes FAQPage, Article, WebPage, Product, Organization, HowTo,
  BreadcrumbList, LocalBusiness, SoftwareApplication, and SpeakableSpecification.
  Use when the user asks about schema markup, JSON-LD, structured data, or rich results.
---

# Schema Markup (JSON-LD Templates)

Ready-to-use JSON-LD structured data templates for SEO and GEO optimization.

## 1. FAQPage Schema (+40% AI Visibility)

**Best for:** FAQ sections, knowledge base pages, product pages with Q&A.

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What is [Your Product/Service]?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "[Comprehensive answer with statistics. According to X, 85% of users report Y benefit.]"
      }
    },
    {
      "@type": "Question",
      "name": "How does [Product/Service] work?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "[Step-by-step explanation.]"
      }
    }
  ]
}
```

## 2. WebPage Schema

**Best for:** Standard content pages, landing pages.

```json
{
  "@context": "https://schema.org",
  "@type": "WebPage",
  "name": "[Page Title]",
  "description": "[Page description, 150-160 characters]",
  "url": "https://example.com/page",
  "datePublished": "2024-01-15",
  "dateModified": "2024-12-20",
  "inLanguage": "en-US",
  "isPartOf": {
    "@type": "WebSite",
    "name": "[Site Name]",
    "url": "https://example.com"
  },
  "author": {
    "@type": "Person",
    "name": "[Author Name]",
    "url": "https://example.com/about"
  },
  "publisher": {
    "@type": "Organization",
    "name": "[Organization Name]",
    "logo": {
      "@type": "ImageObject",
      "url": "https://example.com/logo.png"
    }
  },
  "speakable": {
    "@type": "SpeakableSpecification",
    "cssSelector": ["h1", ".summary", ".key-points"]
  }
}
```

## 3. Article Schema

**Best for:** Blog posts, news articles, tutorials.

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "[Article Title - Max 110 characters]",
  "description": "[Article summary]",
  "image": [
    "https://example.com/image-1x1.jpg",
    "https://example.com/image-4x3.jpg",
    "https://example.com/image-16x9.jpg"
  ],
  "datePublished": "2024-01-15T08:00:00+00:00",
  "dateModified": "2024-12-20T10:30:00+00:00",
  "author": {
    "@type": "Person",
    "name": "[Author Name]",
    "url": "https://example.com/author/name",
    "jobTitle": "[Job Title]",
    "worksFor": {
      "@type": "Organization",
      "name": "[Company]"
    }
  },
  "publisher": {
    "@type": "Organization",
    "name": "[Publisher Name]",
    "logo": {
      "@type": "ImageObject",
      "url": "https://example.com/logo.png",
      "width": 600,
      "height": 60
    }
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://example.com/article-url"
  },
  "keywords": ["keyword1", "keyword2", "keyword3"],
  "articleSection": "[Category]",
  "wordCount": 2500
}
```

## 4. SoftwareApplication Schema

**Best for:** Tools, apps, software products.

```json
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "[App Name]",
  "description": "[App description]",
  "applicationCategory": "DeveloperApplication",
  "operatingSystem": "Cross-platform",
  "url": "https://example.com",
  "downloadUrl": "https://example.com/download",
  "softwareVersion": "1.0.0",
  "featureList": [
    "Feature 1 description",
    "Feature 2 description"
  ],
  "offers": {
    "@type": "Offer",
    "price": "0",
    "priceCurrency": "USD",
    "availability": "https://schema.org/InStock"
  },
  "author": {
    "@type": "Organization",
    "name": "[Company Name]",
    "url": "https://example.com"
  }
}
```

## 5. Organization Schema

**Best for:** About pages, company pages.

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "[Organization Name]",
  "alternateName": "[Alternate Name]",
  "url": "https://example.com",
  "logo": "https://example.com/logo.png",
  "description": "[Organization description]",
  "foundingDate": "2024",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "[City]",
    "addressRegion": "[State]",
    "addressCountry": "[Country]"
  },
  "contactPoint": {
    "@type": "ContactPoint",
    "contactType": "customer service",
    "email": "support@example.com"
  },
  "sameAs": [
    "https://twitter.com/example",
    "https://github.com/example",
    "https://linkedin.com/company/example"
  ]
}
```

## 6. Product Schema

**Best for:** E-commerce product pages.

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "[Product Name]",
  "description": "[Product description]",
  "image": ["https://example.com/product-image.jpg"],
  "sku": "[SKU]",
  "brand": {
    "@type": "Brand",
    "name": "[Brand Name]"
  },
  "offers": {
    "@type": "Offer",
    "url": "https://example.com/product",
    "priceCurrency": "USD",
    "price": "99.99",
    "priceValidUntil": "2025-12-31",
    "availability": "https://schema.org/InStock"
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.5",
    "reviewCount": "89"
  }
}
```

## 7. HowTo Schema

**Best for:** Tutorials, guides, how-to articles.

```json
{
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "How to [Do Something]",
  "description": "[Brief description]",
  "totalTime": "PT15M",
  "step": [
    {
      "@type": "HowToStep",
      "name": "Step 1: [Step Name]",
      "text": "[Detailed step instructions]",
      "url": "https://example.com/guide#step1"
    },
    {
      "@type": "HowToStep",
      "name": "Step 2: [Step Name]",
      "text": "[Detailed step instructions]",
      "url": "https://example.com/guide#step2"
    }
  ]
}
```

## 8. BreadcrumbList Schema

**Best for:** All pages with navigation hierarchy.

```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "https://example.com"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "[Category]",
      "item": "https://example.com/category"
    },
    {
      "@type": "ListItem",
      "position": 3,
      "name": "[Current Page]",
      "item": "https://example.com/category/page"
    }
  ]
}
```

## 9. LocalBusiness Schema

**Best for:** Local business pages.

```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "[Business Name]",
  "description": "[Business description]",
  "url": "https://example.com",
  "telephone": "+1-555-555-5555",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "[Street Address]",
    "addressLocality": "[City]",
    "addressRegion": "[State]",
    "postalCode": "[ZIP]",
    "addressCountry": "US"
  },
  "openingHoursSpecification": [
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"],
      "opens": "09:00",
      "closes": "17:00"
    }
  ]
}
```

## 10. SpeakableSpecification (GEO Enhancement)

**Best for:** Voice search optimization, AI extraction.

```json
{
  "@context": "https://schema.org",
  "@type": "WebPage",
  "name": "[Page Title]",
  "speakable": {
    "@type": "SpeakableSpecification",
    "cssSelector": [
      "h1",
      ".summary",
      ".key-takeaways",
      ".faq-answer"
    ]
  }
}
```

## Combined Schema Example (@graph)

For pages that need multiple schema types:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "WebPage",
      "name": "[Page Title]",
      "description": "[Description]",
      "url": "https://example.com",
      "dateModified": "2024-12-20",
      "speakable": {
        "@type": "SpeakableSpecification",
        "cssSelector": ["h1", ".hero-description", ".faq-answer"]
      }
    },
    {
      "@type": "SoftwareApplication",
      "name": "[App Name]",
      "applicationCategory": "DeveloperApplication",
      "offers": { "@type": "Offer", "price": "0", "priceCurrency": "USD" }
    },
    {
      "@type": "FAQPage",
      "mainEntity": [
        {
          "@type": "Question",
          "name": "[Question]?",
          "acceptedAnswer": { "@type": "Answer", "text": "[Answer]" }
        }
      ]
    },
    {
      "@type": "Organization",
      "name": "[Org Name]",
      "url": "https://example.com"
    }
  ]
}
```

## Validation Tools

1. **Google Rich Results Test:** `https://search.google.com/test/rich-results?url={url}`
2. **Schema.org Validator:** `https://validator.schema.org/?url={url}`
3. **Google Search Console:** Check "Enhancements" for schema issues
