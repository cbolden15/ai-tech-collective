# Detailed Setup Guide

Complete instructions for setting up your own AI Journal automation workflow.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Step 1: n8n Setup](#step-1-n8n-setup)
3. [Step 2: Get API Keys](#step-2-get-api-keys)
4. [Step 3: Import Workflow](#step-3-import-workflow)
5. [Step 4: Configure Credentials](#step-4-configure-credentials)
6. [Step 5: Update Node Configuration](#step-5-update-node-configuration)
7. [Step 6: Test the Workflow](#step-6-test-the-workflow)
8. [Step 7: Activate Automation](#step-7-activate-automation)
9. [Troubleshooting](#troubleshooting)

---

## Prerequisites

### Required Services

1. **n8n Instance**
   - **Self-hosted** (recommended): https://docs.n8n.io/hosting/
   - **n8n Cloud**: https://n8n.io/cloud/
   - Minimum: 1GB RAM, 1 CPU core

2. **Google Gemini API**
   - Free tier available: 15 requests/minute
   - Get key: https://aistudio.google.com/app/apikey

3. **GitHub Account**
   - For storing journal files
   - Need: Personal Access Token with `repo` scope

4. **Discord Server** (optional)
   - For daily summaries
   - Need: Webhook URL

### Technical Skills Needed

- ✅ Basic understanding of API keys
- ✅ Ability to use web interfaces
- ❌ No coding required
- ❌ No server management needed (if using n8n Cloud)

---

## Step 1: n8n Setup

### Option A: n8n Cloud (Easiest)

1. Go to https://n8n.io/cloud/
2. Sign up for free account
3. Launch your n8n instance
4. Skip to Step 2

### Option B: Self-Hosted (Most Control)

**Using Docker (Recommended):**

```bash
# Create volume
docker volume create n8n_data

# Run n8n
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  n8nio/n8n

# Access at http://localhost:5678
```

**Alternative: npm**

```bash
npm install -g n8n
n8n start
```

---

## Step 2: Get API Keys

### 2.1 Google Gemini API Key

1. Visit https://aistudio.google.com/app/apikey
2. Click "Get API key"
3. Select existing project or create new one
4. Copy the API key (starts with `AIza...`)
5. **Save this key** - you'll need it in Step 4

**Free Tier Limits:**
- 15 requests per minute
- 1,500 requests per day
- More than enough for daily journal

### 2.2 GitHub Personal Access Token

1. Go to https://github.com/settings/tokens
2. Click "Generate new token" → "Generate new token (classic)"
3. Give it a name: `n8n-ai-journal`
4. Set expiration: 90 days (or longer)
5. **Select scopes:**
   - ✅ `repo` (Full control of private repositories)
6. Click "Generate token"
7. **Copy the token** (starts with `ghp_...`)
8. **Save immediately** - GitHub won't show it again!

### 2.3 Discord Webhook (Optional)

1. Open your Discord server
2. Go to Server Settings → Integrations
3. Click "Webhooks" → "New Webhook"
4. Name it: `AI Journal`
5. Select channel: `#ai-news` (or your preferred channel)
6. Click "Copy Webhook URL"
7. **Save this URL** - looks like:
   ```
   https://discord.com/api/webhooks/123456789/abcdef...
   ```

---

## Step 3: Import Workflow

1. **Download workflow.json**
   - From this repo: [`workflow.json`](../workflow.json)
   - Or: `wget https://raw.githubusercontent.com/cbolden15/ai-tech-collective/main/workflow.json`

2. **Import to n8n**
   - Open n8n web interface
   - Click "+" (new workflow)
   - Click "⋮" menu → "Import from file"
   - Select `workflow.json`
   - Click "Import"

3. **Workflow loaded!**
   - You should see 15+ nodes
   - Layout may need adjustment (that's normal)

---

## Step 4: Configure Credentials

### 4.1 Add Gemini API Credential

1. Click any "Generate Journal" or "Generate Summary" node
2. In parameters panel, click credential dropdown
3. Click "+ Create New"
4. Select "Google Gemini API"
5. **Configure:**
   - **Name:** `Gemini API`
   - **API Key:** Paste your key from Step 2.1
6. Click "Save"

### 4.2 Add GitHub API Credential

1. Click "Create GitHub File" node
2. In parameters panel, find "Authentication"
3. Select "Predefined Credential Type"
4. Credential Type: `githubApi`
5. Click "+ Create New"
6. **Configure:**
   - **Name:** `GitHub API`
   - **Access Token:** Paste your token from Step 2.2
7. Click "Save"

### 4.3 Update Discord Webhook (Optional)

1. Click "Post to Discord" node
2. Find "URL" parameter
3. Replace `YOUR_DISCORD_WEBHOOK_URL` with your actual webhook URL from Step 2.3
4. Repeat for "Send Error Notification" node

---

## Step 5: Update Node Configuration

### 5.1 Update GitHub Repository

**In "Create GitHub File" node:**

1. Find "URL" parameter
2. Change this part:
   ```
   repos/cbolden15/ai-tech-collective/contents/journals/
   ```
   To your repo:
   ```
   repos/YOUR_USERNAME/YOUR_REPO/contents/journals/
   ```

**Example:**
- Before: `https://api.github.com/repos/cbolden15/ai-tech-collective/contents/journals/{{ $json.fileName }}`
- After: `https://api.github.com/repos/johndoe/my-ai-journal/contents/journals/{{ $json.fileName }}`

### 5.2 Create journals/ Directory in Your Repo

**Via GitHub web:**
1. Go to your repository
2. Click "Add file" → "Create new file"
3. Type: `journals/.gitkeep`
4. Commit the file

**Via command line:**
```bash
cd your-repo
mkdir journals
touch journals/.gitkeep
git add journals/.gitkeep
git commit -m "Add journals directory"
git push
```

### 5.3 Optional: Customize Prompt

**In "Generate Journal" node:**

1. Click the node
2. Find "jsonBody" parameter
3. Click "⋮" → "Edit as JSON"
4. Find the `text` field (the long prompt)
5. Modify to your preferences:
   - Change focus area
   - Adjust sections
   - Modify output length

**Tips:**
- Keep structure similar for best results
- Test changes with small edits first
- Can adjust `maxOutputTokens` (current: 8192)

---

## Step 6: Test the Workflow

### 6.1 Manual Test

1. Click "Execute Workflow" button (top right)
2. **Or** click "Webhook Trigger" node → "Listen for Test Event" → Trigger

3. **Watch execution:**
   - Green = success
   - Red = error
   - Follow the path through nodes

4. **Check outputs:**
   - Click "Generate Journal" node → View output
   - Should see long text with markdown formatting
   - Check GitHub for new file in `journals/`

### 6.2 Common Test Issues

**"No active trigger" error:**
- Solution: Click "Webhook Trigger" → "Execute Node"

**"Credential not found":**
- Solution: Reconfigure credentials in Step 4

**Empty file on GitHub:**
- Solution: Check "Encode to Base64" node is present
- Verify it uses `Buffer.from(content, 'utf-8').toString('base64')`

**GitHub 422 error:**
- Solution: File already exists for today
- Either delete it or wait until tomorrow

---

## Step 7: Activate Automation

### 7.1 Enable Workflow

1. Toggle "Active" switch (top right)
2. Switch should turn green
3. Workflow will now run on schedule

### 7.2 Verify Schedule

**In "Schedule Trigger" node:**
- Default: `0 8 * * *` (8 AM daily, every day)
- Format: Cron expression
- Test tool: https://crontab.guru/

**Common schedules:**
- `0 8 * * 1-5` - Weekdays at 8 AM
- `0 8,20 * * *` - Daily at 8 AM and 8 PM
- `0 */6 * * *` - Every 6 hours

### 7.3 Monitor Execution

**View execution history:**
1. Go to "Executions" tab (left sidebar)
2. See all workflow runs
3. Click any to see details
4. Green = success, Red = failed

**Set up notifications:**
- Already configured if you added Discord webhook!
- Errors automatically posted to Discord

---

## Troubleshooting

### Issue: Workflow won't activate

**Symptoms:** Toggle switch won't stay green

**Solutions:**
1. Check all nodes have green checkmarks
2. Verify credentials are saved
3. Ensure Schedule Trigger is configured
4. Check n8n logs for errors

### Issue: Journal not generated

**Symptoms:** Workflow runs but no output

**Solutions:**
1. Check Gemini API quota (free tier limits)
2. Verify API key is valid
3. Check "Generate Journal" node output
4. Look for error messages in execution log

### Issue: File not appearing on GitHub

**Symptoms:** Workflow succeeds but no file

**Solutions:**
1. Verify GitHub token has `repo` scope
2. Check repository name is correct
3. Ensure `journals/` directory exists
4. Check GitHub API rate limits

### Issue: Discord notification not working

**Symptoms:** Journal created but no Discord post

**Solutions:**
1. Verify webhook URL is correct
2. Test webhook with curl:
   ```bash
   curl -X POST YOUR_WEBHOOK_URL \
     -H "Content-Type: application/json" \
     -d '{"content": "Test message"}'
   ```
3. Check Discord server permissions
4. Webhook may have been deleted - regenerate it

### Issue: High API costs

**Symptoms:** Unexpected charges

**Solutions:**
1. Check execution count in n8n
2. Verify workflow isn't running too frequently
3. Consider reducing `maxOutputTokens`
4. Remove Google Search (saves $0.035/run)
5. Run on weekdays only

### Issue: Duplicate files created

**Symptoms:** Multiple files for same date

**Solutions:**
1. Check for multiple active workflows
2. Verify schedule trigger isn't duplicated
3. Deactivate old workflow versions

---

## Next Steps

### Customize Your Journal

1. **Adjust focus area** - Modify prompt for your industry
2. **Add more sections** - Extend the template
3. **Change schedule** - Run more/less frequently
4. **Add outputs** - Create tweet threads, newsletters

### Advanced Features

1. **Multi-language support** - Generate in different languages
2. **Email delivery** - Add email node after Discord
3. **Analytics** - Track which topics get most engagement
4. **Archive** - Create monthly summaries

### Join the Community

- Share your customizations
- Report issues on GitHub
- Contribute improvements
- Help others with setup

---

## Support

**Need help?**
- GitHub Issues: https://github.com/cbolden15/ai-tech-collective/issues
- n8n Community: https://community.n8n.io/
- Gemini API Docs: https://ai.google.dev/gemini-api/docs

**Found a bug?**
- Open an issue with:
  - n8n version
  - Error message
  - Steps to reproduce

---

**Setup Time:** ~15 minutes
**Cost:** $13/year
**Maintenance:** None (fully automated!)

**Happy Automating! 🚀**
