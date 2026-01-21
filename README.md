# AI/Tech Collective - Daily Journal

> Daily AI industry intelligence and business implementation insights for entrepreneurs and small business owners

## 📖 About

This repository contains daily AI market journals automatically generated and curated for the **AI/Tech Collective** community. Each journal provides:

- **Top AI Industry Signals** - Latest news, launches, and announcements
- **Use-Case Heatmap** - Where AI is working right now in business
- **Money Patterns** - What's selling and why
- **Implementation Opportunities** - Specific business opportunities
- **Tool & Stack Spotlights** - Practical tech stacks for entrepreneurs
- **Daily Learning** - One term to master each day
- **15-Minute Action** - One actionable task to build expertise

## 🎯 Focus Lens

All content is filtered through the perspective of:
- Entrepreneurs & small businesses
- Service providers (coaches, photographers, consultants, realtors)
- Creators (YouTube/TikTok)
- Online sellers (Etsy/Shopify)
- Busy parents running businesses

## 📅 Journal Archive

Daily journals are stored in the [`journals/`](./journals/) directory, organized by date:

- [journals/2026-01-20.md](./journals/2026-01-20.md)
- [journals/2026-01-21.md](./journals/2026-01-21.md)
- ...and more

## 🤖 Automation

These journals are automatically generated daily using:
- **Google Gemini 2.5 Flash** with Google Search for latest AI news
- **n8n workflow** for automation (included in this repo!)
- **Real-time sources** cited in each journal

**Cost:** ~$0.04 per day ($13/year) - Far cheaper than paid newsletters!

## 🚀 For the Community

This is a resource for the **AI/Tech Collective** community to:
- Stay current on AI industry developments
- Identify monetizable opportunities
- Build expert-level awareness through daily repetition
- Take practical actions to implement AI in business

## 📊 What Makes This Different

- **Action-Oriented** - Every journal includes concrete actions
- **Business-Focused** - How to make/save money with each development
- **Jargon-Free** - Technical terms explained in one line
- **Source-Cited** - Real news, real sources
- **Daily Consistency** - Build expertise through repetition

## 🔗 Connect

Join the conversation:
- [Discord Community](#) _(link coming soon)_
- [AI/Tech Collective](#) _(link coming soon)_

---

## 🛠️ Run This Yourself

Want to create your own automated AI journal? The complete n8n workflow is included in this repository!

### Quick Start

**Prerequisites:**
- n8n instance (self-hosted or cloud)
- Google Gemini API key (free tier available)
- GitHub Personal Access Token (with `repo` scope)
- Discord webhook URL (optional, for notifications)

**Setup (5 minutes):**

1. **Import the workflow**
   - Open n8n
   - Click "Import from file"
   - Select [`workflow.json`](./workflow.json)

2. **Add credentials**
   - **Gemini API**: Get key from https://aistudio.google.com/app/apikey
   - **GitHub API**: Generate token from https://github.com/settings/tokens (needs `repo` scope)
   - **Discord Webhook** (optional): Server Settings → Integrations → Webhooks

3. **Configure nodes**
   - Update "Create GitHub File" node with your repo name
   - Update "Post to Discord" node with your webhook URL
   - Optionally customize the prompt in "Generate Journal"

4. **Activate**
   - Toggle workflow to "Active"
   - Test manually or wait for scheduled run (8 AM daily)

**📖 Detailed Setup Guide:** See [SETUP.md](./docs/SETUP.md)

### Cost Breakdown

| Period | Cost |
|--------|------|
| Per run | $0.036 |
| Daily | $0.04 |
| Monthly | $1.08 |
| Yearly | $13.09 |

**Breakdown:**
- Gemini input tokens: $0.0001
- Gemini output tokens: $0.0008
- Google Search grounding: $0.035 (bulk of cost)

**Optimization tips:**
- Run weekdays only: Save $4/year
- Reduce output length: Minimal savings
- Remove Google Search: Save $12/year (but loses real-time news)

### Customization

**Change schedule:** Edit "Schedule Trigger" node
- Default: `0 8 * * *` (8 AM daily)
- Weekdays only: `0 8 * * 1-5`
- Twice daily: `0 8,20 * * *`

**Change focus:** Edit prompt in "Generate Journal" node
- Target different industries
- Adjust for different audiences
- Modify output format

**Add outputs:** Connect new nodes after journal generation
- Tweet threads
- LinkedIn posts
- Email newsletters
- Slack notifications

### Architecture

```
Schedule Trigger (8 AM)
  ↓
Generate Journal (Gemini 2.5 + Google Search)
  ↓
Extract & Validate Content
  ↓
Encode to Base64
  ↓
Commit to GitHub
  ↓
Generate Summary
  ↓
Post to Discord
```

### Troubleshooting

**Empty file on GitHub?**
- Check "Encode to Base64" node uses `Buffer.from(content, 'utf-8')`

**Workflow fails at condition?**
- Verify condition checks `content.length > 1000`

**GitHub 422 error?**
- File already exists for today - this is normal

**High costs?**
- Reduce `maxOutputTokens` in Gemini nodes
- Disable Google Search (loses real-time news)
- Run less frequently

---

**Last Updated**: January 2026
**Maintained By**: AI/Tech Collective
**Automation**: n8n + Google Gemini 2.5 Flash
**License**: MIT - Free to use, modify, and distribute
