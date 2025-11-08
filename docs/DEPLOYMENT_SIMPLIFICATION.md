# Deployment Simplification - Summary of Changes

## What Changed?

This update makes Suna **dramatically easier to deploy** by reducing the required setup from 6+ API keys to just 2 essential items.

## Key Improvements

### 1. Quick Start Mode ⚡

**Before:**
- 17-step mandatory wizard
- Required: Supabase, LLM, Daytona, Tavily, Firecrawl, RapidAPI
- ~30+ minutes to set up
- Had to sign up for 6+ services

**After:**
- Choose: "Quick Start" (5 min) or "Full Setup" (complete)
- Required: **Only Supabase + 1 LLM key**
- **<5 minutes** to get running
- Optional services can be added later

### 2. Free Tier Options 💰

We now highlight free tier options:
- **Groq**: Free fast LLM inference
- **Google Gemini**: Free LLM tier
- **Local Supabase**: Free via Docker
- **Tavily**: 1,000 free searches/month
- **Cloud Supabase**: Generous free tier

**Estimated cost for dev setup: $0-30/month** (can be $0 with free tiers!)

### 3. Clear Documentation 📚

New comprehensive guides:
- **QUICKSTART.md**: 5-minute setup guide
- **docs/API_KEYS_GUIDE.md**: What each service enables, with:
  - Feature availability matrix
  - Free tier information
  - Cost estimates
  - Links to sign up
- **Troubleshooting section**: Common issues and solutions

### 4. Graceful Degradation ✨

Backend already handles missing optional services gracefully:
- No web search key? Clear error: "Web Search is not available. TAVILY_API_KEY is not configured."
- No Daytona? Agent still works, just without sandboxed execution
- No Firecrawl? Web scraping tools don't load, but core features work

### 5. Simplified Docker Setup 🐳

New `docker-compose.simple.yaml`:
- Runs only Redis
- Backend/frontend run natively (easier debugging)
- Perfect for local development

## For Users

### Getting Started (Choose One)

**Option 1: Quick Start (Recommended for First Time)**
```bash
git clone https://github.com/kortix-ai/suna.git
cd suna
# Follow QUICKSTART.md - takes <5 minutes
```

**Option 2: Full Setup Wizard**
```bash
python setup.py
# Choose "Quick Start" or "Full Setup" when prompted
```

### What You Need (Minimal)

1. **Supabase** (Database & Auth)
   - Free local: `npx supabase start`
   - OR free cloud: supabase.com

2. **One LLM API Key** (AI Functionality)
   - Free options: Groq or Google Gemini
   - Best quality: Anthropic Claude or OpenAI GPT

That's it! You can add optional services (web search, scraping, sandboxes) later.

### What Features Work With Minimal Setup?

✅ **Works with just Supabase + LLM:**
- AI agent conversations
- Code generation and analysis
- File creation and editing
- Data analysis
- Local code execution
- Mathematical computations

❌ **Requires additional services:**
- Web search (needs Tavily)
- Web scraping (needs Firecrawl)
- Sandboxed execution (needs Daytona)
- Specialized data queries (need RapidAPI/Exa)

## For Developers

### Files Changed

- `setup.py`: Added quick start mode
- `QUICKSTART.md`: New 5-minute guide
- `docs/API_KEYS_GUIDE.md`: New comprehensive feature matrix
- `backend/.env.defaults`: Clear documentation
- `frontend/.env.defaults`: Minimal config template
- `docker-compose.simple.yaml`: Simplified local dev
- `README.md`: Updated with quick start prominence
- `CONTRIBUTING.md`: References new guides

### Backward Compatibility

✅ **100% backward compatible**
- Existing setups continue to work
- Full setup wizard still available
- All features remain unchanged
- Just adds new quick start option

### Configuration

New `.env.defaults` files provide templates with:
- Clear annotations of required vs optional
- Sensible defaults for local development
- Comments explaining what each service enables

## Testing

The changes have been:
- ✅ Syntax validated
- ✅ Backend graceful degradation verified
- ✅ Security scanned (no issues)
- ✅ Documentation reviewed
- ⏳ Manual end-to-end testing recommended

## Migration Guide

**Existing users**: No action needed - your setup continues to work.

**New users**: Follow QUICKSTART.md for fastest setup.

**Want to simplify existing setup?**
1. Check `docs/API_KEYS_GUIDE.md` to see what's optional
2. Remove optional keys you don't need from `.env`
3. Restart services

## Links

- [Quick Start Guide](../QUICKSTART.md)
- [API Keys & Features](./API_KEYS_GUIDE.md)
- [Main README](../README.md)
- [Contributing Guide](../CONTRIBUTING.md)

## Questions?

- GitHub Issues: https://github.com/kortix-ai/suna/issues
- Discord: https://discord.gg/Py6pCBUUPw
