# Contributing to Suna

Thank you for your interest in contributing to Suna! This document outlines the contribution process and guidelines.

## Contribution Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -am 'feat(your_file): add some feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

## Development Setup

### Quick Setup (Recommended)

The fastest way to get started is using our quick start guide:

```bash
# Follow the 5-minute quick start
# See QUICKSTART.md for detailed instructions
```

This sets up Suna with minimal dependencies (Supabase + 1 LLM key) so you can start developing immediately.

### Full Setup

For a complete development environment with all features:

```bash
python setup.py
# Choose "Full Setup" mode when prompted
```

This will guide you through configuring all required and optional services.

### Detailed Setup Instructions

For detailed setup instructions, please refer to:

- [Quick Start Guide](./QUICKSTART.md) - 5-minute minimal setup
- [API Keys & Feature Guide](./docs/API_KEYS_GUIDE.md) - Understanding what each service enables
- [Backend Development Setup](backend/README.md) - Backend-specific development
- [Frontend Development Setup](frontend/README.md) - Frontend-specific development

### Required Services

Before contributing, ensure you have access to the minimum requirements:

**Required:**

- Supabase project (database and auth) - Free local or cloud option
- LLM provider API key (OpenAI, Anthropic, Groq, or OpenRouter) - Many have free tiers

**Optional (for specific features):**

- Daytona account (for sandboxed agent execution)
- Tavily API key (for web search)
- Firecrawl API key (for web scraping)
- RapidAPI key (for additional tools)
- Custom MCP server configurations

See [API Keys Guide](./docs/API_KEYS_GUIDE.md) for complete details including free tier options and cost estimates.

## Code Style Guidelines

- Follow existing code style and patterns
- Use descriptive commit messages
- Keep PRs focused on a single feature or fix
- Add tests for new functionality
- Update documentation as needed

## Reporting Issues

When reporting issues, please include:

- Steps to reproduce
- Expected behavior
- Actual behavior
- Environment details (OS, Node/Docker versions, etc.)
- Relevant logs or screenshots
- Configuration details (redacted API keys)

## Development Tips

- Use the setup wizard to ensure consistent configuration
- Check the troubleshooting section in the Self-Hosting Guide
- Test both Docker and manual setup when making changes
- Ensure your changes work with the latest setup.py configuration
