# n8n MCP Testing Guide

## Test Status: Ready to Test

Your n8n MCP is configured and ready to test! Follow these steps to verify the integration.

---

## 🔧 Configuration Summary

```json
{
  "n8n": {
    "url": "https://n8n.fonti.dev",
    "api_key": "✓ Configured",
    "version_control": "✓ Enabled (max 20 versions)",
    "status": "✓ Ready to test"
  }
}
```

---

## ✅ Pre-Test Checklist

Before testing, verify:

- [x] n8n MCP added to `opencode.json`
- [x] n8n URL configured: `https://n8n.fonti.dev`
- [x] API key configured
- [x] Version control enabled
- [ ] **Restart OpenCode** (required to load new MCP)
- [ ] Run test commands

---

## 🧪 Test Plan

### Test 1: Connection Test ⭐ START HERE

**Command:**
```bash
opencode "List all my n8n workflows"
```

**Expected Output:**
```json
{
  "workflows": [
    {
      "id": "abc123",
      "name": "workflow_name",
      "active": true,
      "tags": [],
      "createdAt": "2026-01-15T..."
    }
  ],
  "total": 5
}
```

**If it works:** ✅ Connection successful!  
**If it fails:** See [Troubleshooting](#troubleshooting) below

---

### Test 2: Get Available Node Types

**Command:**
```bash
opencode "Show me available n8n node types for Slack"
```

**Expected Output:**
```json
{
  "nodes": [
    {
      "name": "n8n-nodes-base.slack",
      "displayName": "Slack",
      "description": "Consume Slack API"
    },
    {
      "name": "n8n-nodes-base.slackTrigger",
      "displayName": "Slack Trigger",
      "description": "Wait for Slack events"
    }
  ]
}
```

**If it works:** ✅ Node discovery working!

---

### Test 3: Get Workflow Details

**Prerequisites:** You need at least one workflow in your n8n instance

**Command:**
```bash
opencode "Show me details for workflow [paste-workflow-id-here]"
```

**Expected Output:**
```json
{
  "id": "workflow-id",
  "name": "my_workflow",
  "nodes": [...],
  "connections": {...},
  "active": true,
  "settings": {...}
}
```

**If it works:** ✅ Workflow retrieval working!

---

### Test 4: Create New Workflow

**Command:**
```bash
opencode "Create a simple n8n workflow that:
1. Has a webhook trigger
2. Sends a message to Slack channel #general
3. Name it 'test_slack_notifier'"
```

**Expected Behavior:**
- Creates workflow with snake_case name
- Auto-validates nodes
- Saves initial version (snapshot)
- Returns workflow ID

**If it works:** ✅ Workflow creation working!

---

### Test 5: Validation & Auto-Fix

**Command:**
```bash
opencode "Validate my workflow [workflow-id]"
```

**Expected Output:**
```json
{
  "valid": true,
  "warnings": [
    {
      "type": "naming",
      "message": "Node 'SendSlack' should use snake_case",
      "autofix": "send_slack"
    }
  ],
  "errors": []
}
```

**Then auto-fix:**
```bash
opencode "Auto-fix my workflow [workflow-id]"
```

**If it works:** ✅ Validation & auto-fix working!

---

### Test 6: Version Control

**Command:**
```bash
opencode "Save a version of workflow [workflow-id] with message 'Initial version'"
```

**Expected Output:**
```json
{
  "versionId": "v1",
  "workflowId": "workflow-id",
  "message": "Initial version",
  "timestamp": "2026-01-15T...",
  "saved": true
}
```

**List versions:**
```bash
opencode "Show me all versions of workflow [workflow-id]"
```

**If it works:** ✅ Version control working!

---

### Test 7: Workflow Execution

**Command:**
```bash
opencode "Execute workflow [workflow-id]"
```

**Expected Output:**
```json
{
  "executionId": "exec-123",
  "workflowId": "workflow-id",
  "status": "success",
  "startedAt": "2026-01-15T...",
  "finishedAt": "2026-01-15T...",
  "data": {...}
}
```

**If it works:** ✅ Execution working!

---

## 📊 Test Results Template

Copy this and fill it out as you test:

```markdown
## Test Results: [Date]

### Environment
- n8n URL: https://n8n.fonti.dev
- OpenCode Version: [version]
- n8n MCP Version: @pagelines/n8n-mcp@0.3.6

### Test 1: Connection
- Status: [ ] Pass [ ] Fail
- Notes: 

### Test 2: Node Types
- Status: [ ] Pass [ ] Fail
- Notes:

### Test 3: Workflow Details
- Status: [ ] Pass [ ] Fail
- Workflow ID tested:
- Notes:

### Test 4: Create Workflow
- Status: [ ] Pass [ ] Fail
- Created workflow ID:
- Notes:

### Test 5: Validation
- Status: [ ] Pass [ ] Fail
- Issues found:
- Auto-fix applied:
- Notes:

### Test 6: Version Control
- Status: [ ] Pass [ ] Fail
- Versions created:
- Notes:

### Test 7: Execution
- Status: [ ] Pass [ ] Fail
- Execution ID:
- Notes:

### Overall Status
- [ ] All tests passed ✅
- [ ] Some tests failed ⚠️
- [ ] Major issues ❌
```

---

## 🐛 Troubleshooting

### Error: "Cannot connect to n8n instance"

**Possible causes:**
1. n8n URL incorrect
2. API key invalid
3. n8n instance not accessible

**Solutions:**
```bash
# 1. Verify n8n URL is accessible
curl https://n8n.fonti.dev

# 2. Check API key
# - Go to https://n8n.fonti.dev/settings/api
# - Verify the API key is active
# - Regenerate if needed

# 3. Test API directly
curl -H "X-N8N-API-KEY: your-api-key" https://n8n.fonti.dev/api/v1/workflows
```

---

### Error: "Invalid node type"

**Example:**
```
Error: Invalid node type 'n8n-nodes-base.slackk' (typo)
```

**Solution:**
```bash
# List available node types
opencode "Show me all n8n node types"

# Or search for specific nodes
opencode "Find n8n nodes for Slack"
```

---

### Error: "Workflow not found"

**Solution:**
```bash
# List all workflows to get valid IDs
opencode "List all my n8n workflows"

# Use the correct workflow ID from the list
```

---

### Error: "API key unauthorized"

**Solution:**
1. Go to n8n settings: https://n8n.fonti.dev/settings/api
2. Check if API key is still valid
3. Regenerate if needed
4. Update `opencode.json` with new key:

```json
{
  "n8n": {
    "environment": {
      "N8N_API_KEY": "new-api-key-here"
    }
  }
}
```

5. Restart OpenCode

---

### Error: "MCP server timeout"

**Solution:**
```bash
# Increase timeout in opencode.json
{
  "n8n": {
    "timeout": 120000  // Increase to 2 minutes
  }
}
```

---

## 🔍 Verification Commands

### Quick Health Check

```bash
# 1. Connection test
opencode "List my n8n workflows"

# 2. Node discovery test
opencode "Show me n8n node types"

# 3. If you have workflows, get one
opencode "Show me workflow details for [id]"
```

### Detailed Test

```bash
# Full workflow CRUD test
opencode "
1. Create a test workflow
2. Validate it
3. Save a version
4. Update it
5. Show me the diff
6. Rollback if needed
7. Delete the test workflow
"
```

---

## 📈 Performance Benchmarks

Expected response times:

| Operation | Expected Time |
|-----------|---------------|
| List workflows | 1-3 seconds |
| Get workflow | 1-2 seconds |
| Create workflow | 2-5 seconds |
| Update workflow | 2-5 seconds |
| Execute workflow | 3-10 seconds (depends on workflow) |
| Validation | <1 second |
| Version save | 1-2 seconds |

---

## 💡 Example Test Scenarios

### Scenario 1: Create a Slack Notification Workflow

```bash
opencode "Create an n8n workflow that:
1. Triggers on webhook POST to /alert
2. Parses the incoming JSON data
3. Sends notification to Slack #alerts channel
4. Returns success message
Name it: alert_to_slack"
```

**Verify:**
- Workflow created with correct nodes
- snake_case naming enforced
- Validation passed
- Version v1 auto-saved

---

### Scenario 2: Data Processing Pipeline

```bash
opencode "Create an n8n workflow that:
1. Runs every day at 9 AM
2. Fetches data from API: https://api.example.com/data
3. Transforms with JavaScript
4. Saves to Google Sheets
Name it: daily_data_sync"
```

**Verify:**
- Cron trigger configured correctly
- HTTP Request node set up
- JavaScript code node included
- Google Sheets node connected

---

### Scenario 3: Version Control Test

```bash
# Step 1: Create workflow
opencode "Create a simple webhook workflow named test_versions"

# Step 2: Save initial version
opencode "Save version of workflow [id] 'Initial setup'"

# Step 3: Make changes
opencode "Update workflow [id] to add a Set node"

# Step 4: Save new version
opencode "Save version of workflow [id] 'Added Set node'"

# Step 5: Compare
opencode "Show me diff between v1 and v2 of workflow [id]"

# Step 6: Rollback
opencode "Rollback workflow [id] to v1"
```

---

## 🎯 Success Criteria

The n8n MCP integration is successful if:

- ✅ Can list workflows
- ✅ Can create workflows
- ✅ Can update workflows
- ✅ Can execute workflows
- ✅ Auto-validation works
- ✅ Version control works
- ✅ Node type discovery works
- ✅ Response times are acceptable (<5s for most operations)

---

## 📝 Report Template

After testing, use this template to report results:

```markdown
# n8n MCP Test Report

**Date:** [Date]  
**Tester:** [Your name]  
**Environment:** https://n8n.fonti.dev

## Summary
- Total tests: 7
- Passed: [X]
- Failed: [X]
- Success rate: [X]%

## Detailed Results
[Copy test results from above]

## Issues Found
1. [Issue description]
2. [Issue description]

## Recommendations
1. [Recommendation]
2. [Recommendation]

## Conclusion
[ ] Ready for production use
[ ] Needs fixes before production
[ ] Major issues - not ready
```

---

## 🚀 Next Steps After Successful Testing

1. **Create production workflows**
   - Start with simple workflows
   - Test thoroughly before activating
   - Use version control

2. **Set up monitoring**
   - Monitor workflow executions
   - Set up alerts for failures
   - Review execution logs

3. **Build automation library**
   - Document common patterns
   - Create reusable templates
   - Share with team

4. **Explore advanced features**
   - Custom nodes
   - Sub-workflows
   - Error workflows
   - Advanced expressions

---

## 📚 Additional Resources

- **n8n API Docs:** [https://docs.n8n.io/api/](https://docs.n8n.io/api/)
- **Workflow Templates:** [https://n8n.io/workflows](https://n8n.io/workflows)
- **Community Forum:** [https://community.n8n.io](https://community.n8n.io)
- **PageLines MCP Docs:** [https://github.com/PageLines/n8n-mcp](https://github.com/PageLines/n8n-mcp)

---

## ⚠️ Important Notes

1. **Restart Required:** After adding n8n MCP to `opencode.json`, you must restart OpenCode
2. **API Key Security:** Never commit your API key to public repositories
3. **Version Control:** Auto-saves versions before mutations (max 20)
4. **Rate Limits:** n8n API may have rate limits, be mindful
5. **Production Use:** Test thoroughly before using in production workflows

---

**Ready to test?** Start with Test 1 (Connection Test) and work your way through!

Good luck! 🚀
