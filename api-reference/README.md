# API Reference Documentation

This directory contains the Rannah رنّة API documentation with OpenAPI specifications for both V2 (Legacy) and V3 APIs.

## 📁 Directory Structure

```
api-reference/
├── openapi.json              # V2 API spec (bundled, single file)
├── introduction.mdx          # API introduction page
├── authentication.mdx        # Authentication guide
├── endpoints.mdx             # Endpoints overview
│
├── agents/                   # V2 Agent API documentation
│   ├── intro.mdx
│   ├── get.mdx, post.mdx, delete.mdx
│   ├── interact/             # Chat interaction
│   ├── state/                # State management
│   ├── kb/                   # Knowledge Base
│   ├── convos/               # Conversations
│   └── analytics/            # Analytics
│
├── workspaces/               # V2 Workspace API documentation
│   ├── get.mdx, post.mdx, delete.mdx
│   ├── agencies/             # Agency management
│   ├── orgs/                 # Organization management
│   └── clients/              # Client management
│
└── v3/                       # V3 API (recommended)
    ├── intro.mdx
    ├── openapi/              # Split OpenAPI specs by domain
    │   ├── agents.json       # ~9,280 lines - Agent CRUD, export/import
    │   ├── calls.json        # ~4,700 lines - Outbound calls
    │   ├── tools.json        # ~1,650 lines - Tool management
    │   ├── variables.json    # ~1,000 lines - Variable management
    │   ├── conversations.json # ~1,160 lines - Conversation management
    │   ├── kb.json           # ~960 lines - Knowledge Base
    │   ├── leads.json        # ~960 lines - Lead management
    │   ├── workspaces.json   # ~750 lines - Workspace management
    │   ├── orgs.json         # ~720 lines - Organization management
    │   ├── campaigns.json    # ~650 lines - Campaign management
    │   ├── numbers.json      # ~440 lines - Twilio numbers
    │   ├── analytics.json    # ~330 lines - Usage analytics
    │   └── misc.json         # ~1,640 lines - Other endpoints
    │
    ├── agents/               # Agent MDX documentation
    ├── workspaces/           # Workspace MDX documentation
    ├── conversations/        # Conversation MDX documentation
    ├── kb/                   # Knowledge Base MDX documentation
    ├── leads/                # Lead MDX documentation
    ├── tools/                # Tool MDX documentation
    ├── variables/            # Variable MDX documentation
    ├── orgs/                 # Organization MDX documentation
    ├── calls/                # Calls MDX documentation
    └── numbers/              # Numbers MDX documentation
```

## 🔄 API Versions

### V3 (Recommended)
- **Location**: `v3/openapi/` (split by domain)
- **Benefits**: More maintainable, better organized, newer features
- **Endpoints**: `/v3/agents`, `/v3/workspaces`, etc.

### V2 (Legacy)
- **Location**: `openapi.json` (single bundled file)
- **Status**: Still supported but V3 is recommended for new integrations
- **Endpoints**: `/v2/agents`, `/v2/workspaces`, etc.

## 📝 OpenAPI Configuration

The OpenAPI specs are configured in `docs.json`:

```json
{
  "openapi": [
    "api-reference/openapi.json",
    "api-reference/v3/openapi/agents.json",
    "api-reference/v3/openapi/conversations.json",
    "api-reference/v3/openapi/kb.json",
    "api-reference/v3/openapi/leads.json",
    "api-reference/v3/openapi/tools.json",
    "api-reference/v3/openapi/variables.json",
    "api-reference/v3/openapi/workspaces.json",
    "api-reference/v3/openapi/orgs.json",
    "api-reference/v3/openapi/numbers.json",
    "api-reference/v3/openapi/calls.json",
    "api-reference/v3/openapi/analytics.json",
    "api-reference/v3/openapi/campaigns.json",
    "api-reference/v3/openapi/misc.json"
  ]
}
```

## 📚 MDX Documentation Pages

Each API endpoint has a corresponding `.mdx` file that references the OpenAPI spec:

```mdx
---
title: 'Get Agent'
openapi: 'GET /agents/{id}'
---

Additional documentation, tips, and examples go here.
```

Mintlify automatically generates the request/response documentation from the OpenAPI spec.

## ✅ Benefits of Split V3 Structure

| Benefit | Description |
|---------|-------------|
| **Maintainability** | Edit one domain without touching others |
| **Faster Load Times** | Smaller files are quicker to parse |
| **Team Collaboration** | Different team members can work on different APIs |
| **Clear Organization** | ~20k lines split into logical ~400-9k line files |
| **Version Control** | Changes are isolated to specific files |

## 🛠️ Making Changes

### Adding a V3 Endpoint

1. Add the endpoint to the appropriate file in `v3/openapi/`
2. Create a corresponding `.mdx` file in the right subdirectory
3. Add the page to `docs.json` navigation

### Updating V2 Endpoints

1. Edit `openapi.json` directly (bundled file)
2. Update the corresponding `.mdx` file if needed

### Response Field Descriptions

All response fields should have descriptions in the OpenAPI spec:

```json
{
  "properties": {
    "ID": {
      "type": "string",
      "description": "Unique identifier for the resource"
    }
  }
}
```

### Error Responses

All endpoints should include standard error responses:

```json
{
  "responses": {
    "401": { "$ref": "#/components/responses/unauthorized" },
    "403": { "$ref": "#/components/responses/forbidden" },
    "404": { "$ref": "#/components/responses/notFound" }
  }
}
```

## 🔗 Servers

| Region | V3 URL |
|--------|--------|
| EU | `https://eu-gcp-api.vg-stuff.com/v3` |
| NA | `https://na-gcp-api.vg-stuff.com/v3` |

## 📖 Documentation Tools

This structure works with:
- ✅ Mintlify (primary documentation platform)
- ✅ Swagger UI
- ✅ Postman (import individual spec files)
- ✅ OpenAPI validators
