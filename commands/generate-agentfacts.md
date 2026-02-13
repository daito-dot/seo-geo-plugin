---
description: Interactively generate a NANDA-compliant AgentFacts JSON-LD schema for AI agent discovery. Place at /.well-known/agent-facts.
argument-hint: [--domain example.com] [--validate url]
---

# Generate AgentFacts

Create or validate a NANDA-compliant AgentFacts schema for AI agent discovery.

## Procedure

Parse `$ARGUMENTS`:
- If `--validate <url>` is provided, run validation mode
- If `--domain <domain>` is provided, use that domain
- Otherwise, ask the user for their domain

### Validation Mode

If `--validate` is specified:

1. Use `WebFetch` or `Bash` (curl) to fetch `{url}`:
   ```bash
   curl -s "{url}" | python3 -m json.tool
   ```

2. Check required fields:
   - `@context` exists and starts with `https://nanda.dev`
   - `id` exists and starts with `nanda:`
   - `agent_name` exists

3. Check recommended fields: `endpoints`, `capabilities`, `trust`

4. Validate capability values:
   - modalities: text, image, audio, video, code
   - certification: self-attested, third-party, audited

5. Report results:
   ```
   AgentFacts Validation: {url}
   Status: VALID / INVALID
   Errors: {list}
   Warnings: {list}
   ```

### Generation Mode

Collect information from the user (use provided arguments or ask interactively):

1. **Domain** (required): The domain name (e.g., example.com)
2. **Agent Name** (optional): Display name for the agent service. Default: domain title-cased.
3. **Description** (optional): Brief description of the service.
4. **Capabilities** (optional): What modalities does the service support?
   - text, image, audio, video, code
   - Default: text
5. **Authentication** (optional): What auth methods are supported?
   - oauth2, jwt, apikey, none
   - Default: none
6. **Endpoints** (optional): API endpoint URLs.
   - Default: `https://api.{domain}/v1/agent`
7. **Human Oversight** (optional): true, false, on-request
   - Default: true

### Generate the schema

```json
{
  "@context": "https://nanda.dev/ns/agent-facts/v1",
  "id": "nanda:{domain}",
  "agent_name": "urn:agent:{domain_with_colons}",
  "version": "1.0.0",
  "description": "{description}",
  "homepage": "https://{domain}",
  "endpoints": {
    "static": ["{endpoint_urls}"]
  },
  "capabilities": {
    "modalities": ["{modalities}"],
    "authentication": {
      "methods": ["{auth_methods}"]
    }
  },
  "trust": {
    "certification": "self-attested",
    "human_oversight": "{oversight}"
  },
  "metadata": {
    "created": "{current_iso_datetime}",
    "modified": "{current_iso_datetime}",
    "ttl": 86400
  }
}
```

### Provide deployment instructions

After generating the schema, explain:

1. **Save** the JSON to a file (e.g., `agent-facts.json`)
2. **Deploy** to `/.well-known/agent-facts` on your domain
3. **Set headers:**
   - Content-Type: `application/ld+json`
   - Cache-Control: `public, max-age=86400`
   - Access-Control-Allow-Origin: `*`

4. **Framework examples:**

   **Nginx:**
   ```nginx
   location /.well-known/agent-facts {
       default_type application/ld+json;
       add_header Access-Control-Allow-Origin *;
       add_header Cache-Control "public, max-age=86400";
   }
   ```

   **Next.js:**
   ```typescript
   // app/.well-known/agent-facts/route.ts
   export async function GET() {
     return NextResponse.json(schema, {
       headers: { 'Content-Type': 'application/ld+json' }
     });
   }
   ```

5. **Test** with:
   ```bash
   curl -I https://{domain}/.well-known/agent-facts
   curl https://{domain}/.well-known/agent-facts | jq .
   ```
