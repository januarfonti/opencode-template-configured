# n8n MCP Integration Guide

## Overview

The n8n MCP server provides AI-powered workflow automation capabilities through n8n, allowing you to create, manage, and execute workflows directly from your AI assistant.

### What You Can Do

- ✅ **Create & manage workflows** - Build automation workflows
- ✅ **Execute workflows** - Run workflows on-demand
- ✅ **Monitor executions** - Track workflow runs and results
- ✅ **Auto-validate** - Automatic validation and fixes
- ✅ **Version control** - Snapshot and rollback workflows
- ✅ **Node validation** - Prevent invalid node types

---

## Configuration

### Your n8n Instance

```json
{
  "n8n": {
    "url": "https://n8n.fonti.dev",
    "enabled": true
  }
}
```

### Features Enabled

| Feature | Status | Description |
|---------|--------|-------------|
| Version Control | ✅ Enabled | Auto-saves workflow versions (max 20) |
| Auto-Validation | ✅ Enabled | Validates and auto-fixes on create/update |
| Node Type Check | ✅ Enabled | Blocks invalid node types |
| Expression Validation | ✅ Enabled | Catches syntax errors and circular dependencies |

---

## Available Tools

### 1. Workflow Management

```bash
# List all workflows
opencode "List my n8n workflows"

# Get workflow details
opencode "Show me workflow details for [workflow-id]"

# Create new workflow
opencode "Create a new n8n workflow that sends Slack notifications"

# Update workflow
opencode "Update workflow [id] to add email notification"

# Delete workflow
opencode "Delete workflow [id]"

# Activate/Deactivate
opencode "Activate workflow [id]"
opencode "Deactivate workflow [id]"
```

### 2. Workflow Execution

```bash
# Execute workflow
opencode "Execute workflow [id]"

# Execute with data
opencode "Execute workflow [id] with data: {name: 'John', email: 'john@example.com'}"

# List executions
opencode "Show me recent workflow executions"

# Get execution details
opencode "Show me execution details for [execution-id]"
```

### 3. Validation & Quality

```bash
# Validate workflow
opencode "Validate my workflow [id]"

# Auto-fix issues
opencode "Auto-fix my workflow [id]"

# Format workflow
opencode "Format workflow [id]"
```

### 4. Version Control

```bash
# List versions
opencode "Show me versions for workflow [id]"

# Save version
opencode "Save current version of workflow [id]"

# Rollback to version
opencode "Rollback workflow [id] to version [version-id]"

# Compare versions
opencode "Show me diff between workflow versions"

# Version stats
opencode "Show me version statistics"
```

### 5. Discovery

```bash
# List available node types
opencode "Show me available n8n node types"

# Search for nodes
opencode "Find n8n nodes for Slack"
```

---

## Best Practices Enforced

The n8n MCP automatically enforces these best practices:

### ✅ Naming Conventions
- **Enforced:** snake_case for all node names
- **Auto-fix:** Converts CamelCase/kebab-case to snake_case
- **Example:** `SendSlackMessage` → `send_slack_message`

### ✅ Explicit References
- **Enforced:** Use `$('node_name')` instead of `$json`
- **Why:** Prevents breakage when nodes are reordered
- **Auto-fix:** Suggests explicit references

### ✅ No Hardcoded Secrets
- **Warning:** Detects hardcoded API keys, passwords
- **Recommendation:** Use environment variables
- **Example:** `{{ $env.SLACK_TOKEN }}` instead of hardcoded token

### ✅ Expression Validation
- **Checks:** Syntax errors, circular dependencies, missing refs
- **Prevents:** Runtime errors from bad expressions
- **Blocks:** Invalid expressions before saving

### ✅ AI Structured Output
- **Auto-configures:** JSON mode for AI nodes
- **Ensures:** Consistent, parseable AI responses

---

## Common Use Cases

### 1. Slack Notification Workflow

```bash
opencode "Create an n8n workflow that:
1. Triggers on webhook
2. Processes the data
3. Sends notification to Slack channel #alerts
4. Logs to Google Sheets"
```

### 2. Data Processing Pipeline

```bash
opencode "Create an n8n workflow that:
1. Fetches data from API every hour
2. Transforms data with JavaScript
3. Stores in PostgreSQL
4. Sends summary email"
```

### 3. Monitoring & Alerts

```bash
opencode "Create an n8n workflow that:
1. Checks website status every 5 minutes
2. If down, sends alert to Slack and PagerDuty
3. Logs incident to database"
```

### 4. Content Automation

```bash
opencode "Create an n8n workflow that:
1. Monitors RSS feeds
2. Filters by keywords
3. Posts to Twitter
4. Archives to Notion"
```

---

## Example: Build a Complete Workflow

### Step 1: Create Workflow

```bash
opencode "Create a new n8n workflow called 'github_issue_notifier'"
```

### Step 2: Add Nodes

```bash
opencode "Add these nodes to workflow [id]:
1. Webhook trigger (on POST /webhook)
2. GitHub node (get issue details)
3. Slack node (send notification to #dev-team)
4. Set node (format data for logging)
5. HTTP Request (log to external API)"
```

### Step 3: Configure & Validate

```bash
opencode "Validate and auto-fix workflow [id]"
```

### Step 4: Test

```bash
opencode "Execute workflow [id] with test data: {issue_id: 123}"
```

### Step 5: Activate

```bash
opencode "Activate workflow [id]"
```

---

## Version Control Workflow

### Save Before Major Changes

```bash
# Save current state
opencode "Save version of workflow [id] with message 'Before adding error handling'"

# Make changes
opencode "Update workflow [id] to add error handling nodes"

# If something breaks
opencode "Rollback workflow [id] to previous version"
```

### Compare Versions

```bash
# See what changed
opencode "Show me diff between current and previous version of workflow [id]"

# List all versions
opencode "Show me all versions of workflow [id]"
```

---

## Troubleshooting

### Invalid Node Type

```
❌ Error: Invalid node type 'n8n-nodes-base.slackk' (typo)
✅ Suggestion: Did you mean 'n8n-nodes-base.slack'?
```

**Solution:** The MCP will suggest valid node types automatically.

### Expression Error

```
❌ Error: Expression '$json.name' will break if node is reordered
✅ Fix: Use '$('previous_node').json.name' instead
```

**Solution:** Run `opencode "Auto-fix workflow [id]"` to apply fixes.

### Circular Dependency

```
❌ Error: Circular reference detected: node_a → node_b → node_a
```

**Solution:** Restructure workflow to remove circular dependencies.

---

## API Reference

### Workflow Tools

| Tool | Description | Parameters |
|------|-------------|------------|
| `workflow_list` | List all workflows | `tags`, `active` |
| `workflow_get` | Get workflow details | `id` (required) |
| `workflow_create` | Create new workflow | `name`, `nodes`, `connections` |
| `workflow_update` | Update workflow | `id`, `name`, `nodes`, `connections` |
| `workflow_delete` | Delete workflow | `id` (required) |
| `workflow_activate` | Activate workflow | `id` (required) |
| `workflow_deactivate` | Deactivate workflow | `id` (required) |
| `workflow_execute` | Execute workflow | `id`, `data` |

### Execution Tools

| Tool | Description | Parameters |
|------|-------------|------------|
| `execution_list` | List executions | `workflowId`, `status`, `limit` |
| `execution_get` | Get execution details | `id` (required) |

### Validation Tools

| Tool | Description | Parameters |
|------|-------------|------------|
| `validate` | Validate workflow | `id` or `workflow` object |
| `autofix` | Auto-fix issues | `id` or `workflow` object |
| `format` | Format workflow | `id` or `workflow` object |

### Version Tools

| Tool | Description | Parameters |
|------|-------------|------------|
| `version_list` | List versions | `workflowId` |
| `version_get` | Get version | `workflowId`, `versionId` |
| `version_save` | Save version | `workflowId`, `message` |
| `version_rollback` | Rollback to version | `workflowId`, `versionId` |
| `version_diff` | Compare versions | `workflowId`, `fromVersion`, `toVersion` |
| `version_stats` | Version statistics | `workflowId` |

### Discovery Tools

| Tool | Description | Parameters |
|------|-------------|------------|
| `node_types_list` | List available nodes | `category`, `search` |

---

## Configuration Options

### Environment Variables

```json
{
  "N8N_API_URL": "https://n8n.fonti.dev",
  "N8N_API_KEY": "[your-api-key]",
  "N8N_MCP_VERSIONS": "true",
  "N8N_MCP_MAX_VERSIONS": "20"
}
```

| Variable | Default | Description |
|----------|---------|-------------|
| `N8N_API_URL` | required | Your n8n instance URL |
| `N8N_API_KEY` | required | n8n API key |
| `N8N_MCP_VERSIONS` | `true` | Enable version control |
| `N8N_MCP_MAX_VERSIONS` | `20` | Max versions per workflow |

---

## Tips & Tricks

### 1. Use Explicit Node Names

```javascript
// ❌ Bad - breaks on reorder
$json.name

// ✅ Good - explicit reference
$('fetch_user').json.name
```

### 2. Environment Variables for Secrets

```javascript
// ❌ Bad - hardcoded secret
const apiKey = 'sk-abc123...'

// ✅ Good - environment variable
const apiKey = $env.SLACK_API_KEY
```

### 3. Save Versions Before Big Changes

```bash
# Before refactoring
opencode "Save version of workflow [id] 'Before webhook refactor'"

# After changes, if broken
opencode "Rollback workflow [id] to previous version"
```

### 4. Use Validation Early

```bash
# After building workflow
opencode "Validate workflow [id]"

# Fix issues automatically
opencode "Auto-fix workflow [id]"
```

---

## Learn More

- **n8n Documentation:** [https://docs.n8n.io](https://docs.n8n.io)
- **n8n Workflows:** [https://n8n.io/workflows](https://n8n.io/workflows)
- **n8n Community:** [https://community.n8n.io](https://community.n8n.io)
- **PageLines n8n MCP:** [https://github.com/PageLines/n8n-mcp](https://github.com/PageLines/n8n-mcp)

---

## Quick Start Checklist

- [x] n8n MCP configured in opencode.json
- [x] n8n instance URL set: `https://n8n.fonti.dev`
- [x] API key configured
- [x] Version control enabled
- [ ] Create your first workflow
- [ ] Test workflow execution
- [ ] Try version control features

**Next:** Try creating a simple workflow with `opencode "Create a simple n8n workflow that sends a Slack message"`
