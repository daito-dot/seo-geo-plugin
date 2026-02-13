---
name: agentfacts-nanda
description: |
  AgentFacts and NANDA (Networked Agent Discovery Architecture) protocol specification.
  Machine-readable metadata schema for AI agent discovery and interaction.
  Use when the user asks about AgentFacts, NANDA protocol, agent discovery, or .well-known/agent-facts.
---

# AgentFacts & NANDA Protocol

Machine-readable metadata for AI agent discovery and interaction.

## Overview

AgentFacts is part of the **NANDA** (Networked Agent Discovery Architecture) protocol, providing a standardized way for websites to declare their AI agent capabilities, endpoints, and trust parameters.

## Why AgentFacts Matters

1. **Discoverability:** AI systems need structured data about your capabilities
2. **Trust:** Explicit trust declarations help AI systems assess reliability
3. **Interoperability:** Standard schema enables cross-platform compatibility
4. **Future-proofing:** Early adoption positions you for the agentic web era

## File Location

AgentFacts must be placed at:
```
https://yourdomain.com/.well-known/agent-facts
```

Alternative locations:
- `/agent-facts.json`
- `/_agent-facts`

## Schema Reference

### Minimal Valid Schema
```json
{
  "@context": "https://nanda.dev/ns/agent-facts/v1",
  "id": "nanda:example.com",
  "agent_name": "Example Service"
}
```

### Full Schema
```json
{
  "@context": "https://nanda.dev/ns/agent-facts/v1",
  "id": "nanda:example.com",
  "agent_name": "urn:agent:example:com",
  "version": "1.0.0",
  "description": "Human-readable description of the service",
  "homepage": "https://example.com",
  "documentation": "https://docs.example.com",
  "endpoints": {
    "static": ["https://api.example.com/v1/agent"],
    "adaptive_resolver": {
      "url": "https://resolver.example.com/dispatch",
      "policies": ["geo", "load", "capability"]
    }
  },
  "capabilities": {
    "modalities": ["text", "image", "audio", "video", "code"],
    "operations": ["query", "create", "update", "delete"],
    "domains": ["search", "analytics", "automation"],
    "languages": ["en", "es", "fr", "de"],
    "authentication": {
      "methods": ["oauth2", "jwt", "apikey", "none"],
      "scopes": ["read", "write", "admin"]
    },
    "rate_limits": {
      "requests_per_minute": 60,
      "requests_per_day": 10000
    }
  },
  "trust": {
    "certification": "self-attested",
    "human_oversight": "true",
    "audit_log": "https://example.com/audit",
    "privacy_policy": "https://example.com/privacy",
    "terms_of_service": "https://example.com/terms"
  },
  "contact": {
    "email": "ai-support@example.com",
    "abuse": "abuse@example.com"
  },
  "metadata": {
    "created": "2024-01-15T00:00:00Z",
    "modified": "2025-06-20T00:00:00Z",
    "ttl": 86400
  }
}
```

## Schema Fields

### Core Fields (Required)
| Field | Description |
|-------|-------------|
| `@context` | NANDA namespace URI: `https://nanda.dev/ns/agent-facts/v1` |
| `id` | Unique identifier, format: `nanda:domain.com` |
| `agent_name` | URN or human-readable name |

### Endpoints
- **static**: Fixed URLs that always respond
- **adaptive_resolver**: Dynamic routing with policies (geo, load, capability, version)

### Capabilities
- **modalities**: text, image, audio, video, code
- **operations**: query, create, update, delete
- **authentication**: oauth2, jwt, apikey, none

### Trust
| Field | Values |
|-------|--------|
| `certification` | self-attested, third-party, audited |
| `human_oversight` | true, false, on-request |
| `audit_log` | URL to audit trail |

### Metadata
- `ttl`: Time-to-live in seconds for caching (typical: 86400 = 24 hours)

## Implementation Examples

### SaaS Application
```json
{
  "@context": "https://nanda.dev/ns/agent-facts/v1",
  "id": "nanda:myapp.com",
  "agent_name": "MyApp AI Assistant",
  "description": "Project management with AI automation",
  "endpoints": { "static": ["https://api.myapp.com/agent/v1"] },
  "capabilities": {
    "modalities": ["text"],
    "operations": ["query", "create", "update"],
    "authentication": { "methods": ["oauth2"], "scopes": ["read:projects", "write:tasks"] }
  },
  "trust": { "certification": "self-attested", "human_oversight": "true" }
}
```

### E-commerce Site
```json
{
  "@context": "https://nanda.dev/ns/agent-facts/v1",
  "id": "nanda:shop.example.com",
  "agent_name": "Example Shop",
  "description": "Product catalog and ordering",
  "endpoints": { "static": ["https://api.shop.example.com/agent"] },
  "capabilities": {
    "modalities": ["text", "image"],
    "operations": ["query"],
    "authentication": { "methods": ["none", "apikey"] },
    "rate_limits": { "requests_per_minute": 30 }
  },
  "trust": { "certification": "self-attested", "human_oversight": "on-request" }
}
```

### Content Platform
```json
{
  "@context": "https://nanda.dev/ns/agent-facts/v1",
  "id": "nanda:blog.example.com",
  "agent_name": "Example Blog",
  "description": "Technical articles and tutorials",
  "endpoints": { "static": ["https://blog.example.com/api/content"] },
  "capabilities": {
    "modalities": ["text", "code"],
    "operations": ["query"],
    "languages": ["en"],
    "authentication": { "methods": ["none"] }
  },
  "trust": { "certification": "self-attested", "human_oversight": "true" }
}
```

## Validation

### Required Fields Check
Required: `@context`, `id`, `agent_name`
- `@context` must start with `https://nanda.dev`
- `id` must start with `nanda:`

### JSON-LD Validation
Validate at: https://json-ld.org/playground/

## Serving AgentFacts

### Nginx
```nginx
location /.well-known/agent-facts {
    default_type application/ld+json;
    add_header Access-Control-Allow-Origin *;
    add_header Cache-Control "public, max-age=86400";
}
```

### Express.js
```javascript
app.get('/.well-known/agent-facts', (req, res) => {
  res.type('application/ld+json');
  res.sendFile(path.join(__dirname, 'agent-facts.json'));
});
```

### Next.js (App Router)
```typescript
// app/.well-known/agent-facts/route.ts
import { NextResponse } from 'next/server';
import agentFacts from './agent-facts.json';

export async function GET() {
  return NextResponse.json(agentFacts, {
    headers: {
      'Content-Type': 'application/ld+json',
      'Cache-Control': 'public, max-age=86400'
    }
  });
}
```

## Testing
```bash
# Verify accessibility
curl -I https://yourdomain.com/.well-known/agent-facts
# Should return 200 with Content-Type: application/ld+json

# Validate JSON
curl https://yourdomain.com/.well-known/agent-facts | jq .
```

## Best Practices

1. **Keep it current:** Update `metadata.modified` when capabilities change
2. **Be accurate:** Only declare capabilities you actually support
3. **Set reasonable TTL:** 86400 (24 hours) is typical
4. **Include contact info:** AI systems may need to report issues
5. **Start minimal:** Add fields as you implement features
6. **Version your schema:** Use `version` field for tracking changes
