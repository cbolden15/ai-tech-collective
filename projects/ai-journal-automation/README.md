# AI Journal Automation

> Automated daily AI industry intelligence using n8n + Gemini 2.5 Flash

## 📖 What It Does

Generates and publishes daily AI industry journals with:
- **Top 5 AI Industry Signals** - Latest news, launches, and announcements
- **Use-Case Heatmap** - Where AI works right now in business
- **Money Patterns** - What's selling and why
- **Implementation Opportunities** - Specific business opportunities
- **Tool Stack Spotlights** - Practical tech stacks for entrepreneurs
- **Daily Learning Term** - One term to master each day
- **15-Minute Action** - One actionable task to build expertise

## 🚀 Live Output

📅 **View Journals:** [../../journals/](../../journals/)

Latest journals are automatically posted to Discord and committed to GitHub every day at 8 AM.

## 🎯 Focus Lens

All content is filtered through the perspective of:
- Entrepreneurs & small businesses
- Service providers (coaches, photographers, consultants, realtors)
- Creators (YouTube/TikTok)
- Online sellers (Etsy/Shopify)
- Busy parents running businesses

## 💰 Cost Breakdown

| Period | Cost |
|--------|------|
| Per run | $0.036 |
| Daily | $0.04 |
| Monthly | $1.08 |
| Yearly | $13.09 |

**98% of cost is Google Search grounding** - Gemini API itself costs <$0.001/run

### Breakdown:
- Gemini input tokens: $0.0001
- Gemini output tokens: $0.0008
- Google Search grounding: $0.035 (bulk of cost)

**Optimization tips:**
- Run weekdays only: Save $4/year
- Reduce output length: Minimal savings
- Remove Google Search: Save $12/year (but loses real-time news)

## 🛠️ Setup

### Prerequisites

- n8n instance (self-hosted or cloud)
- Google Gemini API key (free tier: 15 req/min)
- GitHub Personal Access Token (with `repo` scope)
- Discord webhook URL (optional, for notifications)

### Quick Start (5 minutes)

1. **Import workflow**
   ```bash
   # In n8n: Import from file
   # Select: workflow.json
   ```

2. **Add credentials**
   - **Gemini API**: Get key from https://aistudio.google.com/app/apikey
   - **GitHub API**: Generate token from https://github.com/settings/tokens (needs `repo` scope)
   - **Discord Webhook** (optional): Server Settings → Integrations → Webhooks

3. **Configure nodes**
   - Update "Create GitHub File" node with your repo name
   - Update "Post to Discord" node with your webhook URL
   - Optionally customize the prompt in "Generate Journal"

4. **Activate**
   - Toggle workflow to "Active" in n8n
   - Test manually or wait for scheduled run (8 AM daily)

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
GitHub Commit (new files only)
  ↓
Validation Check
  ↓
Summary Generation (Gemini 2.5)
  ↓
Discord Notification
```

**Nodes:** 20 total
**Execution time:** ~30-40 seconds
**Error handling:** Comprehensive with fallbacks

## 🎨 Customization

### Change Schedule

Edit "Schedule Trigger" node:

```
0 8 * * *      # Daily at 8 AM (default)
0 8 * * 1-5    # Weekdays only
0 8,20 * * *   # Twice daily (8 AM and 8 PM)
0 */6 * * *    # Every 6 hours
```

### Change Focus

Edit prompt in "Generate Journal" node to target:
- Different industries (healthcare, finance, retail)
- Different audience levels (technical vs non-technical)
- Different output formats (shorter, longer, different sections)

### Add Outputs

Connect new nodes after journal generation for:
- **Twitter/X threads** - Post daily highlights
- **LinkedIn posts** - Professional summaries
- **Email newsletters** - Send to subscribers
- **Slack notifications** - Team channels

## 🐛 Troubleshooting

**Empty file on GitHub?**
- Check "Encode to Base64" node uses `Buffer.from(content, 'utf-8')`
- Verify content is being passed from "Extract Content" node

**Workflow fails at condition?**
- Verify "Check Journal Generated" condition checks `content.length > 1000`
- For Gemini 2.5, check `parts[0].text.length` not `parts.length`

**File already exists error?**
- Normal if running multiple times same day
- Workflow creates new files only (no updates)
- Either delete existing file or wait until tomorrow

**Discord notification not working?**
- Verify webhook URL is correct and active
- Check Discord server permissions
- Test webhook with: `curl -X POST YOUR_WEBHOOK_URL -H "Content-Type: application/json" -d '{"content": "Test"}'`

**High API costs?**
- Reduce `maxOutputTokens` in Gemini nodes
- Disable Google Search (loses real-time news, saves $12/year)
- Run less frequently (weekdays only)

## 📊 Features

✅ Real-time AI news via Google Search grounding
✅ Entrepreneur-focused content filtering
✅ Markdown output optimized for GitHub
✅ Discord mobile-friendly summaries
✅ Error notifications with fallbacks
✅ Comprehensive logging
✅ Manual webhook trigger available
✅ Automatic scheduling (8 AM daily)

## 📝 Workflow Details

### Nodes
1. **Schedule Trigger** - Runs daily at 8 AM
2. **Webhook Trigger** - Manual execution via POST request
3. **Generate Journal** - Gemini 2.5 Flash with Google Search
4. **Check Journal Generated** - Validates content was created
5. **Handle Journal Error** - Error handling and logging
6. **Extract Content** - Parses journal from Gemini response
7. **Encode to Base64** - Prepares content for GitHub API
8. **Create GitHub File** - Commits journal to repository
9. **Check GitHub Commit** - Validates file was created
10. **Store GitHub URL** - Saves URL for Discord post
11. **Generate Summary** - Creates Discord-friendly summary
12. **Check Summary Generated** - Validates summary creation
13. **Use Fallback Summary** - Default summary if generation fails
14. **Extract Summary** - Parses summary from Gemini
15. **Post to Discord** - Sends notification with journal link
16. **Check Discord Posted** - Validates Discord post
17. **Handle Discord Error** - Discord-specific error handling
18. **Success** - Marks workflow as successful
19. **Send Error Notification** - Notifies on failures
20. **Error End** - Terminates with error message

### Execution Flow
- **Success path**: Trigger → Generate → Encode → Commit → Summarize → Discord → Success
- **Error handling**: Any failure routes to error handlers with notifications
- **Fallbacks**: Summary generation has fallback text if Gemini fails

## 🤝 Contributing

This is part of the [AI/Tech Collective](../../) project.

See [Contributing Guidelines](../../CONTRIBUTING.md)

## 📜 License

MIT License - Free to use, modify, and distribute

---

**Part of the AI/Tech Collective automation toolkit**
