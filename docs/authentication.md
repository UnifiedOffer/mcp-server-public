# Authentication Guide

## Getting Your API Key

1. Visit [https://unifiedoffer.com](https://unifiedoffer.com)
2. Sign up for a free account
3. Navigate to your dashboard
4. Generate an API key

## Key Types

### Developer Keys (`dk_*`)
- Search across **ALL shops** in the platform
- Optimized for customer value (best price, quality, features)
- Perfect for: AI shopping assistants, price comparison tools

### Merchant Keys (`mk_*`)
- Shop-scoped search (only your products)
- Optimized for merchant margin
- Perfect for: Your own AI sales assistant

## Using Your API Key

### Standard Header (Recommended)
```bash
curl -X POST https://api.unifiedoffer.com/functions/v1/mcp-http-wrapper \
  -H "x-api-key: dk_YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"tool":"searchProducts","arguments":{"query":"laptop"}}'
```

### Alternative Authorization Header
```bash
-H "X-Authorization: Bearer dk_YOUR_API_KEY"
```

### Query Parameter (Fallback)
```bash
?api_key=dk_YOUR_API_KEY
```

## Security Best Practices

- ✅ Store API keys in environment variables
- ✅ Never commit API keys to Git
- ✅ Rotate keys regularly (every 90 days)
- ✅ Use different keys for dev/staging/production
- ❌ Never expose keys in client-side code
- ❌ Never log API keys in application logs

## Rate Limits

| Tool Category | Limit |
|---------------|-------|
| Light | 100 requests/minute |
| Standard | 60 requests/minute |
| Heavy | 30 requests/minute |
| Batch | 20 requests/minute |

See the [mcp.json](../mcp.json) manifest for tool categorization.
