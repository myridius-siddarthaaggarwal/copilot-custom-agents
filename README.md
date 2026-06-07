# Copilot Custom Agents

A collection of reusable GitHub Copilot custom agent files (`.agent.md`) for Salesforce delivery, BRD/Jira analysis, and GitHub operations.

---

## Agents Included

| File | Agent Name | Purpose |
|------|-----------|--------|
| `github.agent.md` | GitHub Operator | All GitHub operations: repos, issues, PRs, branches, commits, forks, search |
| `orchestrator.agent.md` | BRD-Jira Orchestrator | Runs the full 4-stage BRD vs Jira comparison pipeline |
| `brd-salesforce-context-reader.agent.md` | BRD + Salesforce Context Reader | Extracts BRD requirements and maps them to Salesforce metadata |
| `jira-read-edit-specialist.agent.md` | Jira Read-Edit Specialist | Reads and normalizes Jira epics/stories/subtasks; creates/updates Jira items |
| `salesforce-comparison-analyst.agent.md` | Salesforce Comparison Analyst | Classifies each BRD requirement as COVERED / PARTIAL / MISSING |
| `salesforce-developer.agent.md` | Salesforce Developer | Implements Apex, LWC, Flows, metadata from Jira tickets and BRD docs |
| `salesforce-output-finalizer.agent.md` | Salesforce Output Finalizer | Writes final analysis markdown files with validation checks |

---

## Prerequisites

- [VS Code](https://code.visualstudio.com/) with the **GitHub Copilot** extension installed
- GitHub Copilot Chat enabled (Agent mode)
- For Jira agents: [Atlassian MCP server](https://github.com/atlassian/atlassian-mcp) configured in VS Code
- For GitHub agent: [GitHub MCP server](https://github.com/github/github-mcp-server) configured in VS Code

---

## How to Use

### Step 1 — Copy the agent files into your project

Create a `.github/agents/` folder in your workspace root and copy the `.agent.md` files you want to use:

```
your-project/
  .github/
    agents/
      github.agent.md
      orchestrator.agent.md
      salesforce-developer.agent.md
      ... (pick what you need)
```

### Step 2 — Open GitHub Copilot Chat in Agent mode

1. Open VS Code
2. Open Copilot Chat (`Ctrl+Alt+I` or click the Copilot icon)
3. Click the **agent selector** (top of the chat panel) to switch to a custom agent

### Step 3 — Pick an agent and give it a task

Select the agent from the dropdown and describe your task. Examples:

```
@GitHub Operator  list all open PRs in owner/my-repo

@BRD-Jira Orchestrator  Epic: PROJ-100, BRD file: inputs/requirements.txt

@Salesforce Developer  Implement ticket PROJ-42 — add Incoming Exchange flow to ProgramEnrollment
```

### Step 4 — Review and iterate

Agents marked `user-invocable: false` are sub-agents invoked automatically by the Orchestrator. You do not need to call them directly — the Orchestrator delegates to them in sequence.

---

## Folder Structure in Your Project

For the Salesforce + BRD/Jira agents to work correctly, your project should have:

```
your-project/
  inputs/          # Place BRD / spec / HLD documents here
  outputs/         # Agents write analysis files here
  force-app/       # Salesforce DX source (standard sfdx layout)
  docs/            # Agents write summary, technical, and test-case docs here
  manifest/        # Agents generate package.xml manifests here
```

---

## MCP Server Setup (Quick Reference)

### GitHub MCP
Add to your VS Code `mcp.json`:
```json
{
  "servers": {
    "io.github.github/github-mcp-server": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp/"
    }
  }
}
```

### Atlassian MCP
Add to your VS Code `mcp.json`:
```json
{
  "servers": {
    "com.atlassian/atlassian-mcp-server": {
      "type": "http",
      "url": "https://mcp.atlassian.com/v1/mcp"
    }
  }
}
```

---

## License

MIT
