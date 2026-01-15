# 🚀 Start Here After Restart - n8n MCP Testing

**Date:** January 15, 2026  
**Status:** Ready to test n8n MCP integration

---

## ✅ What We Just Completed

1. ✅ **Created 43 specialized agents:**
   - Mobile: iOS, Android, SwiftUI, React Native, Flutter (5)
   - Desktop: Electron, Tauri, PWA (3)
   - Business: Market Researcher, Product Marketer, Sales Strategist (3)
   - Trading: Trading Analyst (crypto, US stocks, IDX Indonesia) (1)
   - Backend, Database, Core: 31+ agents

2. ✅ **Integrated n8n MCP Server:**
   - Package: `@pagelines/n8n-mcp@0.3.6`
   - URL: `https://n8n.fonti.dev`
   - API Key: Configured in `opencode.json`
   - Version control: Enabled (max 20 snapshots)
   - Features: Auto-validation, auto-fix, version control

3. ✅ **Created Documentation:**
   - `N8N_MCP_GUIDE.md` - Complete usage guide
   - `N8N_MCP_TEST.md` - Testing procedures
   - `SESSION_CONTINUATION_GUIDE.md` - How to continue sessions

4. ✅ **Pushed to GitHub:**
   - Repository: https://github.com/januarfonti/opencode-template-configured
   - Latest commit: `4201be2` - n8n MCP integration

---

## 🎯 Next Step: TEST N8N MCP

You just restarted OpenCode to load the new n8n MCP server.

### Test 1: Connection Test (START HERE)

Run this command:
```bash
opencode "List my n8n workflows"
```

**Expected:** Should connect to https://n8n.fonti.dev and return your workflows

---

### Test 2: Node Discovery

```bash
opencode "Show me available n8n node types for Slack"
```

**Expected:** Should list Slack-related nodes

---

### Test 3: Create Test Workflow

```bash
opencode "Create a simple n8n workflow that:
1. Has a webhook trigger
2. Sends a message to Slack channel #general
3. Name it 'test_slack_notifier'"
```

**Expected:** Creates workflow with auto-validation and version control

---

### Test 4: Workflow Execution

```bash
opencode "Execute workflow [use-id-from-test-3]"
```

**Expected:** Executes the workflow and returns execution details

---

### Test 5: Version Control

```bash
opencode "Save a version of workflow [workflow-id] with message 'Initial test version'"
```

**Expected:** Saves snapshot, returns version ID

---

## 📋 Full Test Checklist

Follow the comprehensive tests in `N8N_MCP_TEST.md`:

- [ ] Test 1: Connection (list workflows)
- [ ] Test 2: Node types discovery
- [ ] Test 3: Get workflow details
- [ ] Test 4: Create new workflow
- [ ] Test 5: Validation & auto-fix
- [ ] Test 6: Version control (save, list, rollback)
- [ ] Test 7: Workflow execution

---

## 📁 Important Files

| File | Purpose |
|------|---------|
| `N8N_MCP_GUIDE.md` | Complete n8n MCP documentation |
| `N8N_MCP_TEST.md` | Detailed testing guide |
| `SESSION_CONTINUATION_GUIDE.md` | How to continue after restart |
| `opencode.json` | n8n MCP configuration |
| `CONTINUE_HERE.md` | This file - your starting point |

---

## 🔧 Configuration Summary

```json
{
  "n8n": {
    "type": "local",
    "command": ["npx", "-y", "@pagelines/n8n-mcp"],
    "environment": {
      "N8N_API_URL": "https://n8n.fonti.dev",
      "N8N_API_KEY": "[configured]",
      "N8N_MCP_VERSIONS": "true",
      "N8N_MCP_MAX_VERSIONS": "20"
    },
    "enabled": true
  }
}
```

---

## 🐛 If Something Goes Wrong

### Can't connect to n8n?

1. Check n8n instance is running: https://n8n.fonti.dev
2. Verify API key is valid in n8n settings
3. Check `opencode.json` configuration

### MCP server not loading?

1. Ensure OpenCode was restarted after adding n8n MCP
2. Check for errors in OpenCode startup logs
3. Try: `npx -y @pagelines/n8n-mcp` manually to test

### Reference troubleshooting guide:
See **"Troubleshooting"** section in `N8N_MCP_TEST.md`

---

## 💡 Quick Reference Commands

```bash
# List workflows
opencode "List my n8n workflows"

# Create workflow
opencode "Create an n8n workflow for [purpose]"

# Execute workflow
opencode "Execute workflow [id]"

# Validate
opencode "Validate workflow [id]"

# Version control
opencode "Save version of workflow [id]"
opencode "Show me versions of workflow [id]"
```

---

## 🎊 What You've Accomplished So Far

### Session Highlights

**Agent Collection:** 43 specialized agents
- 11 Development agents (mobile, desktop, web)
- 4 Business & Finance agents
- 28+ Backend, database, and core agents

**MCP Servers:** 11 integrations
- n8n (workflow automation) ⭐ NEW
- context7, exa, Ref (search & docs)
- firecrawl, morph (scraping & editing)
- zai, chrome-devtools (AI & browser)
- next-devtools, shadcn, nuxt-mcp-dev (framework tools)

**Documentation:** Comprehensive guides
- Agent usage guides
- MCP integration docs
- Session continuation guide
- Testing procedures

---

## 🚀 After Testing n8n MCP

Once testing is complete, you might want to:

1. **Build production workflows**
   - Slack notifications
   - Data pipelines
   - Monitoring & alerts
   - Content automation

2. **Test other agents**
   - Trading Analyst: `opencode "Analyze BTC/USDT"`
   - Market Researcher: `opencode "Analyze [market]"`
   - iOS Developer: `opencode "Build iOS app for [purpose]"`

3. **Create new agents**
   - Specialized for your needs
   - Industry-specific
   - Custom workflows

---

## 📞 Need Help?

### Documentation
- All guides in this repository
- Check `N8N_MCP_GUIDE.md` for detailed n8n help
- `SESSION_CONTINUATION_GUIDE.md` for continuation tips

### Resources
- n8n Docs: https://docs.n8n.io
- n8n Community: https://community.n8n.io
- GitHub Repo: https://github.com/januarfonti/opencode-template-configured

---

## ✅ Your Next Command

**Copy and paste this after restart:**

```bash
opencode "We just integrated n8n MCP server for https://n8n.fonti.dev. Configuration is complete. Now let's test it - start by listing my workflows."
```

Or even simpler:

```bash
opencode "List my n8n workflows"
```

---

**Good luck with testing! 🎯**

_This file was created as your session continuation point. Delete it once you've successfully tested n8n MCP._
