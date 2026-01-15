# Session Continuation Guide

## How to Continue Conversations After Restart

OpenCode doesn't automatically continue previous conversations after restart, but there are several strategies to maintain context and continue where you left off.

---

## 🔄 Quick Answer

**After restarting OpenCode, to continue:**

### Option 1: Use Context Files (Recommended)
```bash
# Create a context file before restarting
opencode "Create a summary of our conversation in CURRENT_SESSION.md"

# After restart, reference it
opencode "Read CURRENT_SESSION.md and continue where we left off"
```

### Option 2: Use Session Summary
```bash
# After restart, provide brief context
opencode "We were working on [topic]. I want to continue by [next step]"
```

### Option 3: Use Project Context
```bash
# OpenCode will read your project files automatically
# Just mention what you're working on
opencode "Continue working on the n8n integration we started"
```

---

## 📋 Best Practices for Session Continuity

### 1. Create a Session Notes File

Before major breaks or restarts, create a session notes file:

```bash
opencode "Create a file SESSION_NOTES.md with:
- What we accomplished today
- Current task/goal
- Next steps
- Any pending issues
- Important context to remember"
```

**Example SESSION_NOTES.md:**
```markdown
# Session Notes - Jan 15, 2026

## Accomplished
- ✅ Created 43 specialized agents (mobile, desktop, business, trading)
- ✅ Integrated n8n MCP server
- ✅ Configured for https://n8n.fonti.dev

## Current Task
Testing n8n MCP integration

## Next Steps
1. Restart OpenCode
2. Test n8n MCP connection: "List my n8n workflows"
3. Create test workflow
4. Verify version control

## Important Context
- n8n API key configured in opencode.json
- Version control enabled (max 20 snapshots)
- Using @pagelines/n8n-mcp package

## Pending Issues
- None

## Commands to Try After Restart
```bash
opencode "List my n8n workflows"
opencode "Show me available n8n node types"
```
```

---

### 2. Use the .opencode/context/ Directory

OpenCode automatically reads files from `.opencode/context/` directory:

```bash
# Create context file (will be auto-loaded)
opencode "Create .opencode/context/current-work.md with summary of what we're doing"
```

**Location:** `/Users/januarfonti/.opencode/opencode-template/context/current-work.md`

This file will be automatically included in the context for every conversation!

---

### 3. Maintain a TODO.md File

Keep a running TODO list:

```bash
opencode "Update TODO.md with:
## In Progress
- [ ] Test n8n MCP integration
- [ ] Create first workflow

## Completed Today
- [x] Set up 43 agents
- [x] Configured n8n MCP

## Next Session
- [ ] Build production workflows
- [ ] Test trading analyst agent
"
```

---

### 4. Use Git Commit Messages

Your git history serves as session notes:

```bash
# View recent work
git log --oneline -10

# See what changed
git diff HEAD~5..HEAD --stat
```

Your commits tell the story:
- `4201be2` - n8n MCP integration
- `565ec2d` - Business & trading agents
- `3a3caa3` - Android, SwiftUI, PWA agents
- `b0bf9a2` - Mobile & desktop agents

---

## 🎯 Continuation Strategies

### Strategy 1: Project-Based Context

OpenCode reads your project structure automatically. Just mention the project:

```bash
# After restart
opencode "Continue working on the OpenCode template we've been building"
```

OpenCode will:
- Read your project files
- See recent changes
- Understand the context

---

### Strategy 2: Reference Recent Files

```bash
# After restart
opencode "I want to continue from where we left off. 
Read N8N_MCP_GUIDE.md and SESSION_NOTES.md to understand context."
```

---

### Strategy 3: Direct Context

Simply tell OpenCode what you were doing:

```bash
opencode "We just integrated n8n MCP server. 
I restarted OpenCode and now want to test the integration.
Please help me test it by listing my workflows."
```

---

## 📁 Recommended File Structure

Create these files to maintain context across sessions:

```
/Users/januarfonti/.opencode/opencode-template/
├── SESSION_NOTES.md           # Current session notes
├── TODO.md                     # Running TODO list
├── CHANGELOG.md                # What changed each session
├── context/
│   ├── current-work.md        # Auto-loaded context
│   ├── project-goals.md       # Long-term goals
│   └── key-decisions.md       # Important decisions made
└── docs/
    └── sessions/
        ├── 2026-01-15.md      # Session log
        └── 2026-01-14.md      # Previous session
```

---

## 🔧 Template Files to Use

### SESSION_NOTES.md Template

```markdown
# Session Notes - [Date]

## Current Goal
[What you're trying to accomplish]

## Accomplished This Session
- [x] Item 1
- [x] Item 2

## In Progress
- [ ] Item 1
- [ ] Item 2

## Next Steps
1. [First thing to do next session]
2. [Second thing]

## Important Context
- [Key info to remember]
- [Configuration details]
- [Decisions made]

## Commands to Run Next
```bash
# List commands here
```

## Files Modified
- file1.md
- file2.json

## Links
- [Relevant URL 1]
- [Relevant URL 2]
```

---

### context/current-work.md Template

```markdown
# Current Work Context

**Project:** OpenCode Template Configuration
**Focus:** n8n MCP Integration
**Status:** Testing phase

## What We're Building
[Brief description]

## Recent Accomplishments
- Created 43 specialized agents
- Integrated n8n MCP

## Current Task
Testing n8n MCP integration at https://n8n.fonti.dev

## Key Configuration
- n8n URL: https://n8n.fonti.dev
- MCP Package: @pagelines/n8n-mcp@0.3.6
- Version control: Enabled (max 20)

## Next Actions
1. Test connection
2. Create workflow
3. Verify features
```

---

## 🚀 Quick Start After Restart

### Scenario 1: Continue Exactly Where You Left Off

**Before restart:**
```bash
opencode "Create SESSION_RESUME.md with exact context of what we're doing"
```

**After restart:**
```bash
opencode "Read SESSION_RESUME.md and continue from there"
```

---

### Scenario 2: Pick Up General Work

**After restart:**
```bash
opencode "What were we working on? Check recent files and git commits"
```

OpenCode will analyze:
- Recent file changes
- Git commits
- File structure
- And infer what you were doing

---

### Scenario 3: Start New Task But Keep Context

**After restart:**
```bash
opencode "We've been building an OpenCode template with 43 agents and n8n integration.
Now I want to test the trading analyst agent. 
Analyze BTC/USDT for buy/sell signal."
```

---

## 💡 Pro Tips

### Tip 1: Use Descriptive File Names

```bash
# Good - tells the story
NEXT_SESSION_START_HERE.md
CURRENT_FOCUS_N8N_TESTING.md

# Less helpful
notes.md
temp.md
```

---

### Tip 2: Create Session Logs

At end of each session:

```bash
opencode "Create docs/sessions/$(date +%Y-%m-%d).md with:
- What we accomplished
- What we learned
- Next steps
- Useful commands"
```

---

### Tip 3: Commit Often with Good Messages

```bash
git commit -m "🚧 WIP: Testing n8n MCP - left off at workflow creation"
```

Next session, you can see:
```bash
git log -1
# Shows: "🚧 WIP: Testing n8n MCP - left off at workflow creation"
```

---

### Tip 4: Use .opencode/context/ for Auto-Loading

Files in `.opencode/context/` are automatically included in every conversation:

```bash
# This file will always be loaded
echo "## Current Focus
Testing n8n MCP integration
URL: https://n8n.fonti.dev" > .opencode/context/current-focus.md
```

---

## 📖 Example: Complete Session Handoff

### End of Session (Before Restart)

```bash
opencode "
Create a session handoff document in CONTINUE_HERE.md with:

# Session Handoff - Jan 15, 2026

## Where We Left Off
Just finished integrating n8n MCP server. Configuration is complete.
Ready to test the integration.

## What's Configured
- n8n MCP: @pagelines/n8n-mcp@0.3.6
- URL: https://n8n.fonti.dev  
- API Key: Configured in opencode.json
- Features: Version control, auto-validation, auto-fix

## Next Steps (In Order)
1. Restart OpenCode (required to load new MCP)
2. Test connection: 'List my n8n workflows'
3. Test node discovery: 'Show me n8n node types for Slack'
4. Create test workflow
5. Test version control
6. Document results in N8N_MCP_TEST.md

## Files to Reference
- N8N_MCP_GUIDE.md - Full documentation
- N8N_MCP_TEST.md - Testing guide
- opencode.json - Configuration

## Commands Ready to Run
\`\`\`bash
opencode 'List my n8n workflows'
opencode 'Show me available n8n node types'
opencode 'Create a test Slack notification workflow'
\`\`\`

## Success Criteria
- ✅ Can list workflows
- ✅ Can create workflows  
- ✅ Can execute workflows
- ✅ Version control works

## Context for AI
We're building a comprehensive OpenCode template with 43 agents.
Latest addition is n8n MCP integration for workflow automation.
This is the first time testing it after configuration.
"
```

---

### Start of Next Session (After Restart)

```bash
opencode "Read CONTINUE_HERE.md and let's start testing from step 1"
```

---

## 🎓 Advanced: Create a Session Manager

Create a helper script:

```bash
# .opencode/scripts/session-manager.sh

#!/bin/bash

case "$1" in
  save)
    echo "# Session Saved: $(date)" > .opencode/LAST_SESSION.md
    echo "" >> .opencode/LAST_SESSION.md
    echo "## Files Changed" >> .opencode/LAST_SESSION.md
    git diff --name-only >> .opencode/LAST_SESSION.md
    echo "" >> .opencode/LAST_SESSION.md
    echo "## Last Commit" >> .opencode/LAST_SESSION.md
    git log -1 --pretty=format:"%h - %s" >> .opencode/LAST_SESSION.md
    echo "Session saved to .opencode/LAST_SESSION.md"
    ;;
    
  resume)
    cat .opencode/LAST_SESSION.md
    echo ""
    echo "Run: opencode 'Read LAST_SESSION.md and continue'"
    ;;
    
  *)
    echo "Usage: $0 {save|resume}"
    ;;
esac
```

Usage:
```bash
# Before restart
./opencode/scripts/session-manager.sh save

# After restart
./opencode/scripts/session-manager.sh resume
opencode "Read LAST_SESSION.md and continue where we left off"
```

---

## 🎯 Your Current Session Summary

Since you're about to restart to test n8n MCP, here's your continuation command:

**After restart, run this:**
```bash
opencode "We just integrated n8n MCP server (@pagelines/n8n-mcp) for https://n8n.fonti.dev.
Configuration is complete with version control enabled.
Now I want to test the integration. Start by listing my n8n workflows."
```

Or even simpler:
```bash
opencode "Test my n8n MCP by listing workflows from https://n8n.fonti.dev"
```

---

## 📚 Summary

### To Continue After Restart:

1. **Create context files** before restarting (SESSION_NOTES.md)
2. **Use .opencode/context/** for auto-loaded context
3. **Reference recent files** after restart
4. **Provide brief context** in your first message
5. **Check git history** to see what you were doing

### Quick Commands After Restart:

```bash
# Simple approach
opencode "Continue where we left off with n8n MCP testing"

# With context
opencode "Read SESSION_NOTES.md and continue from there"

# Specific task
opencode "We integrated n8n MCP. Let's test it by listing workflows"
```

---

## ✅ Before You Restart Checklist

- [ ] Create SESSION_NOTES.md or CONTINUE_HERE.md
- [ ] Commit recent changes with descriptive message
- [ ] Note what you want to do next
- [ ] Save any important commands to run
- [ ] Update context/current-work.md if exists

**You're ready to restart! Just reference the context after restart.** 🚀
