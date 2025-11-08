# API Keys & Feature Guide

This guide explains which API keys enable which features in Suna. Use this to decide which services you need for your use case.

## Required Services (Minimal Setup)

These are the absolute minimum to run Suna:

### 1. Supabase (Database & Auth) - **REQUIRED**

**What it enables:**
- User authentication
- Conversation history
- Agent configurations
- File storage

**How to get it:**
- **Local (Free):** `cd backend && npx supabase start`
- **Cloud:** Sign up at [supabase.com](https://supabase.com)

**Environment variables:**
```bash
SUPABASE_URL=
SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
```

### 2. LLM Provider - **REQUIRED** (Choose at least one)

**What it enables:**
- Core AI agent functionality
- Natural language understanding
- Code generation and analysis

**Providers & How to Get Keys:**

| Provider | Cost | Get Key | Recommended For |
|----------|------|---------|----------------|
| **Anthropic (Claude)** | Pay-as-you-go | [console.anthropic.com](https://console.anthropic.com) | Best overall quality |
| **OpenAI (GPT)** | Pay-as-you-go | [platform.openai.com](https://platform.openai.com) | Reliable, fast |
| **Groq** | Free tier | [console.groq.com](https://console.groq.com) | Fast, cost-effective |
| **OpenRouter** | Pay-as-you-go | [openrouter.ai](https://openrouter.ai) | Access to many models |
| **Google (Gemini)** | Free tier | [aistudio.google.com](https://aistudio.google.com) | Free option |

**Environment variables (add at least one):**
```bash
ANTHROPIC_API_KEY=
OPENAI_API_KEY=
GROQ_API_KEY=
OPENROUTER_API_KEY=
GEMINI_API_KEY=
```

---

## Optional Services (Enhanced Features)

These services are **not required** to run Suna but enable additional capabilities:

### 3. Web Search - Tavily API (Optional)

**What it enables:**
- Real-time web search
- Current information retrieval
- News and research gathering

**Without it:**
- Agents can still function but won't be able to search the web
- Error message: "Web Search is not available. TAVILY_API_KEY is not configured."

**How to get it:**
- Sign up at [tavily.com](https://tavily.com)
- Free tier: 1,000 searches/month

**Environment variable:**
```bash
TAVILY_API_KEY=
```

### 4. Web Scraping - Firecrawl API (Optional)

**What it enables:**
- Extract full content from web pages
- Convert web pages to markdown
- Crawl multiple pages

**Without it:**
- Agents can't extract detailed content from URLs
- Error message: "Web Scraping is not available. FIRECRAWL_API_KEY is not configured."

**How to get it:**
- Sign up at [firecrawl.dev](https://firecrawl.dev)
- Free tier available

**Environment variable:**
```bash
FIRECRAWL_API_KEY=
```

### 5. Sandboxed Execution - Daytona (Optional)

**What it enables:**
- Isolated code execution environment
- Browser automation in sandbox
- Safe execution of untrusted code

**Without it:**
- Agents can still execute code but without isolation
- Some advanced features may be limited

**How to get it:**
- Sign up at [daytona.io](https://www.daytona.io)
- Create an API key from the dashboard

**Environment variables:**
```bash
DAYTONA_API_KEY=
DAYTONA_SERVER_URL=https://app.daytona.io/api
DAYTONA_TARGET=us
```

### 6. Data Providers - RapidAPI (Optional)

**What it enables:**
- Additional data sources
- Specialized data APIs
- Extended functionality

**Without it:**
- Core functionality unaffected
- Some specialized data queries won't work

**How to get it:**
- Sign up at [rapidapi.com](https://rapidapi.com)

**Environment variable:**
```bash
RAPID_API_KEY=
```

### 7. Advanced Search - Exa (Optional)

**What it enables:**
- People search functionality
- Company information lookup
- Professional data retrieval

**Without it:**
- These specific search types won't be available
- Basic web search still works with Tavily

**How to get it:**
- Sign up at [exa.ai](https://exa.ai)

**Environment variable:**
```bash
EXA_API_KEY=
```

### 8. Document Processing - Chunkr (Optional)

**What it enables:**
- Advanced document parsing
- PDF processing
- Document analysis

**How to get it:**
- Contact Chunkr for access

**Environment variable:**
```bash
CHUNKR_API_KEY=
```

---

## Production Services (Optional)

These services are recommended for production deployments:

### Monitoring & Observability - Langfuse (Optional)

**What it enables:**
- LLM call tracking
- Performance monitoring
- Cost analysis

**Environment variables:**
```bash
LANGFUSE_PUBLIC_KEY=
LANGFUSE_SECRET_KEY=
LANGFUSE_HOST=https://cloud.langfuse.com
```

### Billing - Stripe (Optional)

**What it enables:**
- Payment processing
- Subscription management

**Environment variables:**
```bash
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=
```

### Integrations - Composio (Optional)

**What it enables:**
- Third-party integrations
- OAuth workflows

**Environment variables:**
```bash
COMPOSIO_API_KEY=
COMPOSIO_WEBHOOK_SECRET=
```

---

## Quick Setup Matrix

| Use Case | Required Keys | Optional But Recommended |
|----------|---------------|-------------------------|
| **Basic Agent** | Supabase + 1 LLM | None |
| **Research Agent** | Supabase + 1 LLM | Tavily, Firecrawl |
| **Code Agent** | Supabase + 1 LLM | Daytona |
| **Full Featured** | Supabase + 1 LLM | Tavily, Firecrawl, Daytona, RapidAPI |
| **Production** | Supabase + 1 LLM | All of the above + Langfuse, Stripe |

---

## Testing Without Optional Services

You can test Suna with just Supabase + 1 LLM key. The agent will:

✅ **Work:**
- Respond to questions using LLM knowledge
- Execute code locally
- Create and edit files
- Analyze data
- Have conversations

❌ **Not Work:**
- Web search (needs Tavily)
- Web scraping (needs Firecrawl)
- Sandboxed execution (needs Daytona)
- Some specialized data queries (need RapidAPI/Exa)

The agent will provide clear error messages when attempting to use features that require missing API keys.

---

## Cost Estimate (Monthly)

For a typical development/testing setup:

| Service | Free Tier | Typical Dev Cost |
|---------|-----------|------------------|
| Supabase (Local) | Free | $0 |
| Supabase (Cloud) | 500MB DB, 1GB storage | $0 |
| Groq (LLM) | 10 req/min | $0 |
| Tavily | 1,000 searches | $0 |
| Firecrawl | Limited | $0-10 |
| Daytona | Free tier | $0-20 |

**Total for full featured dev setup: $0-30/month**

For production, costs scale with usage.
