# Quick Start Guide

Get started with the Universal MCP Server in 5 minutes!

## Step 1: Get Your API Key

Visit [https://unifiedoffer.com](https://unifiedoffer.com) and create a free account to get your API key.

## Step 2: Make Your First Request

```bash
curl -X POST https://api.unifiedoffer.com/functions/v1/mcp-http-wrapper \
  -H "x-api-key: YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "tool": "searchProducts",
    "arguments": {
      "query": "laptop",
      "limit": 5
    }
  }'
```

## Step 3: Try Other Tools

### Price Negotiation
```bash
curl -X POST https://api.unifiedoffer.com/functions/v1/mcp-http-wrapper \
  -H "x-api-key: YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "tool": "negotiatePrice",
    "arguments": {
      "productId": "PRODUCT_ID",
      "requestedDiscount": 15
    }
  }'
```

### AI Chat Assistant
```bash
curl -X POST https://api.unifiedoffer.com/functions/v1/mcp-http-wrapper \
  -H "x-api-key": YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "tool": "chat",
    "arguments": {
      "message": "I need a laptop for video editing",
      "configName": "openai-gpt-4o"
    }
  }'
```

## Step 4: Integration Examples

See [examples.md](./examples.md) for code examples in:
- JavaScript/TypeScript
- Python
- PHP
- Go
- Ruby
- Java
- C#

## Next Steps

- [Authentication Guide](./authentication.md) - API key management
- [Tool Reference](../mcp.json) - All available tools
- [Rate Limits](https://unifiedoffer.com/docs/limits) - Usage quotas

## Need Help?

- 📧 Email: support@unifiedoffer.com
- 🐛 Issues: [GitHub Issues](https://github.com/UnifiedOffer/mcp-server-public/issues)
- 📚 Docs: [https://unifiedoffer.com/docs](https://unifiedoffer.com/docs)
