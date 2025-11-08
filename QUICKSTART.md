# Quick Start Guide

Get Suna running in **under 5 minutes** with minimal configuration!

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) (for Redis and optional local Supabase)
- [Node.js 18+](https://nodejs.org/) and npm
- [Python 3.11+](https://www.python.org/downloads/)
- [uv](https://github.com/astral-sh/uv#installation) (Python package manager)

## Quick Start (Minimal Setup)

### Step 1: Clone the Repository

```bash
git clone https://github.com/kortix-ai/suna.git
cd suna
```

### Step 2: Set Up Supabase

**Option A: Local Supabase (Recommended for development)**

```bash
cd backend
npx supabase start
# Save the output - you'll need the API URL and keys
cd ..
```

**Option B: Cloud Supabase**

1. Create a free account at [supabase.com](https://supabase.com)
2. Create a new project
3. Get your project URL and keys from Project Settings → API

### Step 3: Configure Environment

**Backend Configuration:**

```bash
cd backend
cp .env.defaults .env
# Edit .env and add:
# - Your Supabase URL, anon key, and service role key
# - At least one LLM API key (Anthropic, OpenAI, Groq, etc.)
cd ..
```

**Frontend Configuration:**

```bash
cd frontend  
cp .env.defaults .env.local
# Edit .env.local and add:
# - Your Supabase URL and anon key
cd ..
```

### Step 4: Start Suna

**Start Redis:**
```bash
docker compose up redis -d
```

**Start Backend (in a new terminal):**
```bash
cd backend
uv run api.py
```

**Start Worker (in a new terminal):**
```bash
cd backend
uv run dramatiq run_agent_background
```

**Start Frontend (in a new terminal):**
```bash
cd frontend
npm install
npm run dev
```

### Step 5: Access Suna

Open your browser to [http://localhost:3000](http://localhost:3000)

🎉 **You're done!** You can now start using Suna.

## What's Included in Minimal Setup?

With just Supabase + 1 LLM key, you get:

✅ **Core AI Agent Functionality**
- Natural language conversation
- File management and editing
- Code execution
- Data analysis

❌ **Optional Features Not Included** (can be added later):

- Web search (requires Tavily API key)
- Web scraping (requires Firecrawl API key)  
- Isolated sandboxes (requires Daytona account)
- Additional data providers (requires RapidAPI key)

## Adding Optional Features

To enable additional features, add the corresponding API keys to your `.env` file.

📖 **See [API Keys & Feature Guide](./docs/API_KEYS_GUIDE.md) for complete details on:**
- What each service enables
- How to get free API keys
- Cost estimates
- Feature availability matrix

### Quick Reference

**Web Search** (Tavily):
```bash
TAVILY_API_KEY=your_key_here
```
Free tier: 1,000 searches/month at [tavily.com](https://tavily.com)

**Web Scraping** (Firecrawl):
```bash
FIRECRAWL_API_KEY=your_key_here
```
Get a key at [firecrawl.dev](https://firecrawl.dev)

**Sandboxed Execution** (Daytona):
```bash
DAYTONA_API_KEY=your_key_here
DAYTONA_SERVER_URL=https://app.daytona.io/api
DAYTONA_TARGET=us
```
Sign up at [daytona.io](https://www.daytona.io)

## Full Setup Wizard

If you prefer an interactive setup with all features:

```bash
python setup.py
```

This wizard will guide you through configuring all available services.

## Troubleshooting

### Redis connection error

**Problem:** Backend can't connect to Redis

**Solution:**
```bash
# Make sure Docker is running
docker --version

# Check if Redis is running
docker compose ps

# If not running, start Redis
docker compose -f docker-compose.simple.yaml up -d
# OR
docker compose up redis -d
```

### Supabase connection error

**Problem:** "Could not connect to Supabase" or authentication errors

**Solution:**
- Verify your keys are correct in `backend/.env`
- For local Supabase:
  ```bash
  cd backend
  npx supabase status  # Check if it's running
  npx supabase start   # Start if needed
  ```
- For cloud Supabase:
  - Go to your project settings → API
  - Verify URL and keys are correct
  - Make sure the project is not paused

### Frontend can't connect to backend

**Problem:** Frontend shows connection errors

**Solution:**
- Make sure backend is running on port 8000
  ```bash
  # Check if backend is running
  curl http://localhost:8000/health
  ```
- Verify `NEXT_PUBLIC_BACKEND_URL` in `frontend/.env.local`:
  ```bash
  NEXT_PUBLIC_BACKEND_URL="http://localhost:8000/api"
  ```
- Check for port conflicts:
  ```bash
  lsof -i :8000  # On macOS/Linux
  netstat -ano | findstr :8000  # On Windows
  ```

### Dependencies installation fails

**Problem:** `uv run` or `npm install` fails

**Solution:**
- Make sure you have the right versions:
  ```bash
  node --version  # Should be 18+
  python --version  # Should be 3.11+
  uv --version    # Should be latest
  ```
- For backend:
  ```bash
  cd backend
  rm -rf .venv
  uv sync
  ```
- For frontend:
  ```bash
  cd frontend
  rm -rf node_modules package-lock.json
  npm install
  ```

### Worker not processing tasks

**Problem:** Background tasks aren't running

**Solution:**
- Check if worker is running:
  ```bash
  cd backend
  uv run dramatiq run_agent_background
  ```
- Verify Redis connection in worker logs
- Make sure `REDIS_HOST` is set correctly in `.env`

### LLM API errors

**Problem:** "API key invalid" or LLM errors

**Solution:**
- Verify your API key is correct in `backend/.env`
- Check your API provider's dashboard for:
  - Key is active
  - Sufficient credits/quota
  - No rate limiting
- Try a different LLM provider if available

### Port already in use

**Problem:** "Address already in use" error

**Solution:**
```bash
# Find what's using the port
# For port 3000 (frontend)
lsof -ti:3000 | xargs kill -9  # macOS/Linux
netstat -ano | findstr :3000   # Windows

# For port 8000 (backend)
lsof -ti:8000 | xargs kill -9  # macOS/Linux
netstat -ano | findstr :8000   # Windows
```

### Database migration errors

**Problem:** Supabase migrations fail

**Solution:**
```bash
cd backend
npx supabase db reset  # For local Supabase
# Then restart the backend
```

### Still having issues?

1. **Check logs:**
   - Backend: Look at terminal where `api.py` is running
   - Frontend: Check browser console (F12) and terminal
   - Worker: Check terminal where dramatiq is running

2. **Clean start:**
   ```bash
   # Stop everything
   docker compose down
   
   # Clean and restart
   cd backend && npx supabase stop
   cd backend && npx supabase start
   docker compose up redis -d
   
   # Then start backend, worker, and frontend again
   ```

3. **Get help:**
   - [GitHub Issues](https://github.com/kortix-ai/suna/issues)
   - [Discord Community](https://discord.gg/Py6pCBUUPw)

## Next Steps

- Read the [full documentation](./README.md)
- Learn about [agent configuration](./docs/AGENT_CONFIG.md)
- Join our [Discord community](https://discord.gg/Py6pCBUUPw)
