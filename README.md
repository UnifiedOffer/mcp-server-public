# 🌐 Universal MCP Server

**AI-powered e-commerce integration for intelligent shopping assistants**

[![NPM Version](https://img.shields.io/npm/v/@unifiedoffer/mcp-server.svg)](https://www.npmjs.com/package/@unifiedoffer/mcp-server)
[![PyPI Version](https://img.shields.io/pypi/v/uop-mcp-server.svg)](https://pypi.org/project/uop-mcp-server/)
[![Docker Pulls](https://img.shields.io/docker/pulls/unifiedoffer/mcp-server.svg)](https://hub.docker.com/r/unifiedoffer/mcp-server)
[![MCP Protocol](https://img.shields.io/badge/MCP-v2024--11--05-blue)](https://modelcontextprotocol.io)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](./LICENSE)

Connect your AI applications to 3+ e-commerce platforms (Shopify, WooCommerce, Shopware 6) with automatic product search, price negotiation, and intelligent discount generation through the Model Context Protocol.

---

## ✨ Features

- **🔍 Product Search** - Natural language queries across all connected platforms
- **💰 Price Negotiation** - Intelligent pricing with automatic discount generation
- **🔗 Smart Links** - Direct product links with automatic discount application
- **🤖 Multi-LLM Support** - Works with 6 AI providers (OpenAI, Anthropic, Google, Mistral, Cohere, Groq)
- **🧵 Thread Management** - Persistent conversations with 24h expiry
- **🌍 Multi-Currency** - Supports 12 currencies (EUR, USD, GBP, CHF, etc.)
- **⚡ Production-Ready** - Enterprise-grade performance and security
- **🆓 Free to Use** - No fees, no commissions, open for everyone

---

## 🚀 Quick Start

### Option 1: Direct HTTP API (Recommended)

```bash
# Get your free API key at https://unifiedoffer.com
curl -X POST https://api.unifiedoffer.com/functions/v1/mcp-http-wrapper \
  -H "x-api-key: YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "tool": "searchProducts",
    "arguments": {
      "query": "gaming laptop under $1500",
      "limit": 5
    }
  }'
```

### Option 2: NPM Package

```bash
npm install @unifiedoffer/mcp-server
```

### Option 3: PyPI Package

```bash
pip install uop-mcp-server
```

### Option 4: Docker

```bash
docker pull unifiedoffer/mcp-server:latest
docker run -p 8080:8080 -e UOP_API_KEY=your_key unifiedoffer/mcp-server
```

---

## 🛠️ Available Tools

| Tool | Description | Latency | Complexity |
|------|-------------|---------|------------|
| **searchProducts** | Search products across all platforms | ~1.7s | Medium |
| **generateLinks** | Create direct product links with discounts | ~2.1s | Medium |
| **negotiatePrice** | Intelligent price negotiation | ~2.3s | High |
| **negotiateBatch** | Competitive batch pricing | ~2.8s | High |
| **negotiateMultiRound** | Progressive multi-round negotiation | ~3.2s | High |
| **chat** | AI shopping assistant (6 LLM providers) | ~5.7s | High |
| **listThreads** | List conversation threads | ~0.6s | Low |
| **getThread** | Retrieve thread history | ~0.8s | Low |
| **extendThread** | Extend thread expiration | ~0.8s | Low |

**Average Response Time**: 2.2s | **Success Rate**: 100%

---

## 📚 Documentation

### Getting Started
- [Authentication Guide](./docs/authentication.md) - API key setup
- [Quick Start Guide](./docs/quick-start.md) - First steps
- [Code Examples](./docs/examples.md) - Integration examples

### API Reference
- [Tool Specifications](./mcp.json) - Complete MCP manifest
- [OpenAPI Spec](https://api.unifiedoffer.com/functions/v1/mcp-openapi-spec) - REST API docs

### Advanced Topics
- [Multi-LLM Configuration](https://unifiedoffer.com/docs/llm) - Provider setup
- [Thread Management](https://unifiedoffer.com/docs/threads) - Conversation persistence
- [Rate Limits](https://unifiedoffer.com/docs/limits) - Usage quotas

---

## 🌍 Supported Platforms

| Platform | Product Sync | Discount Codes | Webhooks | Status |
|----------|-------------|----------------|----------|--------|
| **Shopify** | ✅ | ✅ | ✅ | Production |
| **WooCommerce** | ✅ | ✅ | ✅ | Production |
| **Shopware 6** | ✅ | ✅ | ✅ | Production |
| **Magento** | ⏳ | ⏳ | ⏳ | Planned |

---

## 💡 Use Cases

### AI Shopping Assistants
```javascript
// Natural language product search
const response = await fetch('https://api.unifiedoffer.com/functions/v1/mcp-http-wrapper', {
  method: 'POST',
  headers: {
    'x-api-key': 'YOUR_API_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    tool: 'chat',
    arguments: {
      message: 'I need a laptop for video editing under $2000',
      configName: 'openai-gpt-4o'
    }
  })
});
```

### Price Comparison Tools
```python
# Compare multiple products competitively
import requests

response = requests.post(
    'https://api.unifiedoffer.com/functions/v1/mcp-http-wrapper',
    headers={'x-api-key': 'YOUR_API_KEY'},
    json={
        'tool': 'negotiateBatch',
        'arguments': {
            'productIds': ['prod_123', 'prod_456', 'prod_789']
        }
    }
)
```

### E-Commerce Integration
```bash
# Generate product links with automatic discounts
curl -X POST https://api.unifiedoffer.com/functions/v1/mcp-http-wrapper \
  -H "x-api-key: YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "tool": "generateLinks",
    "arguments": {
      "productIds": ["prod_abc", "prod_def"]
    }
  }'
```

---

## 🔐 Authentication

Get your free API key at [https://unifiedoffer.com](https://unifiedoffer.com)

**Two key types available**:
- **Developer Keys** (`dk_*`) - Search across ALL shops, optimize for customer value
- **Merchant Keys** (`mk_*`) - Shop-scoped search, optimize for merchant margin

**Usage**:
```bash
# Standard header (recommended)
-H "x-api-key: dk_YOUR_API_KEY"

# Alternative authorization header
-H "X-Authorization: Bearer dk_YOUR_API_KEY"

# Query parameter (fallback)
?api_key=dk_YOUR_API_KEY
```

---

## ⚡ Rate Limits

| Tool Category | Limit | Tools |
|---------------|-------|-------|
| **Light** | 100 req/min | listThreads, getThread, extendThread |
| **Standard** | 60 req/min | searchProducts, generateLinks |
| **Heavy** | 30 req/min | negotiatePrice, chat |
| **Batch** | 20 req/min | negotiateBatch, negotiateMultiRound |

---

## 🌐 Multi-Currency Support

Automatic currency handling for 12 currencies:

EUR (€) • USD ($) • GBP (£) • CHF (CHF) • CAD (C$) • AUD (A$) • JPY (¥) • SEK (kr) • NOK (kr) • DKK (kr) • PLN (zł) • CZK (Kč)

Minimum discounts automatically adjusted per currency (e.g., €1.00, $1.00, £0.85).

---

## 🤖 AI Provider Support

Works seamlessly with 6 LLM providers (40+ models):

| Provider | Models | Features |
|----------|--------|----------|
| **OpenAI** | GPT-5, GPT-4.1, GPT-4o series (8 models) | Best function calling, JSON mode |
| **Anthropic** | Claude Sonnet 4.5, Opus 4.1, Claude 3.5 (5 models) | Best coding, 1M context |
| **Google** | Gemini 2.5 Pro, 2.5 Flash, 2.0 Flash (5 models) | Best price-performance |
| **Mistral** | Medium 3, Devstral Small, Large/Small (6 models) | Multilingual support |
| **Cohere** | Command A, Aya Expanse (5 models) | 23 languages |
| **Groq** | OpenAI GPT-OSS, Llama 4 Vision (12 models) | Ultra-fast inference |

**BYOK Model**: Bring Your Own Key - use your own LLM API keys for zero cost.

---

## 🏗️ Architecture

```
┌─────────────────┐
│   AI App/Agent  │
└────────┬────────┘
         │ MCP Protocol (HTTP/WebSocket)
         ▼
┌─────────────────┐
│  MCP Server     │
│  (Edge Func)    │
└────────┬────────┘
         │ REST API
         ▼
┌─────────────────────────────────┐
│  Product Database (PostgreSQL)  │
│  - Shopify Products             │
│  - WooCommerce Products         │
│  - Shopware Products            │
└─────────────────────────────────┘
```

---

## 📊 Performance

- **Uptime**: 99.9%
- **Average Latency**: 2.2s
- **Success Rate**: 100%
- **Concurrent Requests**: 1000+
- **Database**: Enterprise PostgreSQL with 145+ optimized indexes

---

## 🔒 Security

- ✅ API keys hashed before storage
- ✅ 170 active Row-Level Security policies
- ✅ Rate limiting with fail-safe defaults
- ✅ CORS properly configured
- ✅ Zero secrets in responses
- ✅ Grade A+ security audit

---

## 📦 Distribution Channels

| Channel | Package | Status |
|---------|---------|--------|
| **NPM** | [@unifiedoffer/mcp-server](https://www.npmjs.com/package/@unifiedoffer/mcp-server) | ✅ v2.0.4 |
| **PyPI** | [uop-mcp-server](https://pypi.org/project/uop-mcp-server/) | ✅ v2.0.5 |
| **Docker Hub** | [unifiedoffer/mcp-server](https://hub.docker.com/r/unifiedoffer/mcp-server) | ✅ v2.0.0 |
| **GitHub MCP Registry** | io.github.Chris85appding/unified-offer-protocol | ✅ v2.0.5 |
| **PulseMCP** | Auto-indexing | ⏳ Pending |
| **MCP.so** | Manual submission | ⏳ Pending |

---

## 🤝 Support & Community

- **Website**: https://unifiedoffer.com
- **Documentation**: https://unifiedoffer.com/mcp
- **API Endpoint**: https://api.unifiedoffer.com/functions/v1/mcp-http-wrapper
- **Email**: support@unifiedoffer.com
- **Issues**: https://github.com/UnifiedOffer/mcp-server-public/issues

---

## 📄 License

MIT License - see [LICENSE](./LICENSE) for details.

---

## 🎯 Roadmap

### v2.1 (Q1 2026)
- [ ] Magento platform integration
- [ ] Real-time inventory sync
- [ ] Enhanced batch negotiation strategies
- [ ] WebSocket transport layer

### v2.2 (Q2 2026)
- [ ] Multi-region deployment
- [ ] GraphQL API endpoint
- [ ] Enhanced analytics dashboard
- [ ] Custom LLM fine-tuning

---

## 🌟 Why Choose UOP MCP Server?

✅ **Production-Ready** - Enterprise-grade performance and security  
✅ **Zero Setup** - Direct HTTP API, no complex configuration  
✅ **Multi-Platform** - Works with Shopify, WooCommerce, Shopware 6  
✅ **Cost-Effective** - BYOK model, pay only for what you use  
✅ **Fully Featured** - 9 tools covering search, negotiation, links, chat  
✅ **Well-Documented** - Comprehensive guides and examples  
✅ **Open Source** - MIT License, community-driven  
✅ **100% Free** - No fees, no commissions, no hidden costs  

---

<p align="center">
  <strong>Built with ❤️ by the Unified Offer Protocol Team</strong><br>
  <a href="https://unifiedoffer.com">Get Started Free</a> • 
  <a href="https://unifiedoffer.com/docs">Documentation</a> • 
  <a href="https://github.com/UnifiedOffer/mcp-server-public/issues">Report Bug</a>
</p>
