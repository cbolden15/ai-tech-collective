# Repository Reorganization Plan

## Current Problem
- Repository looks like a single project (AI Journal)
- Hard to add more tools without confusion
- Main README is project-specific, not a portfolio index

## Proposed Structure

```
ai-tech-collective/
├── README.md                           # Portfolio landing page
├── projects/                           # All automation tools
│   ├── ai-journal-automation/
│   │   ├── README.md                  # Project docs (moved from main)
│   │   ├── workflow.json              # n8n workflow
│   │   ├── SETUP.md                   # Setup guide
│   │   └── screenshots/               # Optional: workflow screenshots
│   ├── future-tool-1/
│   │   └── README.md
│   └── future-tool-2/
│       └── README.md
├── journals/                           # Generated content (stays here)
│   └── 2026-01-20.md
├── docs/                               # Global documentation
│   └── CONTRIBUTING.md
└── .github/
    └── workflows/                      # Optional: GitHub Actions
```

## New Main README.md

Transform into a portfolio index:

```markdown
# AI/Tech Collective - Open Source Automation Tools

> A collection of practical AI and automation tools for entrepreneurs and small businesses

## 🎯 Mission

Build and share automation tools that help entrepreneurs leverage AI without technical complexity or high costs.

## 🛠️ Projects

### 1. [AI Journal Automation](./projects/ai-journal-automation/)
**Daily AI industry intelligence delivered to Discord**

- 📊 Automated daily journals with latest AI news
- 💰 Cost: $0.04/day ($13/year)
- ⚡ Setup time: 5 minutes
- 🔧 Tech: n8n + Gemini 2.5 Flash + GitHub + Discord

**Status:** ✅ Production | **Live Output:** [View Journals](./journals/)

---

### 2. [Coming Soon] Email Automation Suite
**AI-powered email classification and response suggestions**

Status: 🚧 In Development

---

### 3. [Coming Soon] Content Repurposing Pipeline
**Turn long-form content into multi-platform posts**

Status: 📝 Planned

---

## 📚 Documentation

- [Contributing Guidelines](./docs/CONTRIBUTING.md)
- [Community Discord](#) _(coming soon)_

## 🎯 Focus

All tools are designed for:
- Entrepreneurs & small businesses
- Service providers (coaches, consultants, realtors)
- Creators (YouTube/TikTok)
- Online sellers (Etsy/Shopify)
- Busy parents running businesses

## 📊 Generated Content

- [📅 Daily AI Journals](./journals/) - Auto-generated industry intelligence

## 💡 Principles

1. **Practical** - Solve real problems, not theoretical ones
2. **Affordable** - Most tools cost <$20/year to run
3. **Open Source** - MIT licensed, fork and customize
4. **Well-Documented** - Step-by-step guides, no assumptions
5. **Battle-Tested** - We use these tools daily

## 🤝 Contributing

We welcome contributions! See [CONTRIBUTING.md](./docs/CONTRIBUTING.md) for guidelines.

## 📜 License

MIT License - Free to use, modify, and distribute

---

**Maintained by the AI/Tech Collective community**
```

## Project-Specific README

Move current README content to `projects/ai-journal-automation/README.md`:

```markdown
# AI Journal Automation

> Automated daily AI industry intelligence using n8n + Gemini 2.5 Flash

## 📖 What It Does

Generates and publishes daily AI industry journals with:
- Top 5 AI Industry Signals
- Use-Case Heatmap (where AI works right now)
- Money Patterns (what's selling)
- Implementation Opportunities
- Tool Stack Spotlights
- Daily Learning Term
- 15-Minute Action Item

## 🚀 Live Output

📅 **View Journals:** [../../journals/](../../journals/)

Latest journals are automatically posted to Discord and committed to GitHub.

## 💰 Cost Breakdown

| Period | Cost |
|--------|------|
| Per run | $0.036 |
| Daily | $0.04 |
| Monthly | $1.08 |
| Yearly | $13.09 |

**98% of cost is Google Search grounding** - Gemini API itself costs <$0.001/run

## 🛠️ Setup

### Prerequisites

- n8n instance (self-hosted or cloud)
- Google Gemini API key (free tier: 15 req/min)
- GitHub Personal Access Token
- Discord webhook URL (optional)

### Quick Start (5 minutes)

1. **Import workflow**
   ```bash
   # In n8n: Import from file
   # Select: workflow.json
   ```

2. **Add credentials**
   - Gemini API: https://aistudio.google.com/app/apikey
   - GitHub: https://github.com/settings/tokens (scope: `repo`)
   - Discord: Server Settings → Integrations → Webhooks

3. **Configure nodes**
   - Update GitHub repo name in "Create GitHub File"
   - Update Discord webhook URL in "Post to Discord"
   - Customize prompt if desired

4. **Activate**
   - Toggle "Active" in n8n
   - Default schedule: 8 AM daily

📖 **Detailed Guide:** [SETUP.md](./SETUP.md)

## 🏗️ Architecture

```
Triggers (Webhook + Schedule)
  ↓
Gemini 2.5 Flash (with Google Search)
  ↓
Content Extraction & Validation
  ↓
Base64 Encoding
  ↓
GitHub Commit
  ↓
Summary Generation
  ↓
Discord Notification
```

**Nodes:** 20 total
**Execution time:** ~30-40 seconds
**Error handling:** Comprehensive with fallbacks

## 🎨 Customization

### Change Schedule
```
0 8 * * *      # Daily at 8 AM (default)
0 8 * * 1-5    # Weekdays only
0 8,20 * * *   # Twice daily
```

### Change Focus
Edit prompt in "Generate Journal" node to target:
- Different industries
- Different audience levels
- Different output formats

### Add Outputs
Connect new nodes for:
- Twitter threads
- LinkedIn posts
- Email newsletters
- Slack notifications

## 🐛 Troubleshooting

**Empty file on GitHub?**
- Check Base64 encoding in "Encode to Base64" node

**File already exists error?**
- Normal if running multiple times same day
- Workflow creates new files only

**High API costs?**
- Reduce `maxOutputTokens` in Gemini nodes
- Disable Google Search (loses real-time news)

## 📊 Features

✅ Real-time AI news via Google Search grounding
✅ Entrepreneur-focused content filtering
✅ Markdown output optimized for GitHub
✅ Discord mobile-friendly summaries
✅ Error notifications
✅ Fallback handling
✅ Comprehensive logging

## 🤝 Contributing

This is part of the [AI/Tech Collective](../../) project.

See [Contributing Guidelines](../../docs/CONTRIBUTING.md)

## 📜 License

MIT License
```

## Migration Steps

### 1. Create New Structure
```bash
cd /Users/calebbolden/Projects/ai-tech-collective

# Create projects directory
mkdir -p projects/ai-journal-automation/screenshots

# Move workflow
mv workflow.json projects/ai-journal-automation/

# Move setup docs
mv docs/SETUP.md projects/ai-journal-automation/

# Create new project README (content above)
# Create new main README (content above)
```

### 2. Update Documentation
- New main README.md (portfolio index)
- New projects/ai-journal-automation/README.md (project-specific)
- Update CONTRIBUTING.md path references

### 3. Update Links
- Update all relative links in documentation
- Update GitHub URLs in n8n workflow (stays same)
- Update README badges if any

### 4. Test
- Verify all links work
- Test workflow still runs (GitHub paths unchanged)
- Check journal generation still works

### 5. Commit Changes
```bash
git add .
git commit -m "Refactor: Reorganize as project portfolio

- Move AI Journal to projects/ directory
- Transform main README to portfolio index
- Prepare for additional automation tools
- Keep journals/ output at root for visibility"

git push origin main
```

## Benefits

✅ **Scalability** - Easy to add new tools
✅ **Clarity** - Clear this is a collection, not one project
✅ **Navigation** - Main README is now a directory
✅ **Separation** - Each project is self-contained
✅ **Professional** - Portfolio presentation

## Future Projects Ideas

Based on this structure, you could add:

1. **Email Automation Suite**
   - Gmail label automation
   - AI-powered classification
   - Response templates

2. **Content Repurposing**
   - YouTube → Blog posts
   - Long-form → Tweet threads
   - Podcast → Show notes

3. **Lead Generation Tools**
   - Scraper + enrichment workflows
   - CRM integration tools
   - Outreach automation

4. **Analytics Dashboards**
   - Social media metrics
   - Business KPIs
   - Custom reporting

Each lives in `projects/[tool-name]/` with its own README, workflow files, and documentation.
