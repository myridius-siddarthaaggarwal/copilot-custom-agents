---
description: "Run BRD-Jira comparison and generate gap analysis, TDD, and implementation checklist. Use when you want to compare a BRD document against a Jira Epic."
name: "BRD-Jira Compare"
argument-hint: "Jira Epic key (e.g. PROJ-123) and optionally doc filenames"
agent: "agent"
---

# BRD ↔ Jira Comparison Workflow

You are running the **BRD-Jira Comparison Pipeline**. Hand off to the **BRD-Jira Orchestrator** agent to execute the full workflow.

## User Input

Please confirm the following before starting:

1. **Jira Epic Key**: `{EPIC_KEY}` — replace with the real Epic key (e.g. `CRM-42`, `SF-100`, `PROJ-123`)
2. **BRD Documents**: files in `inputs/` to analyse (or type `all` to use all files except README.md)

---

## What Will Happen

The orchestrator will run this Salesforce-specific 4-stage pipeline:

| Stage | Agent | Action |
|------|-------|--------|
| 1 | Jira Read-Edit Specialist | Read (and optionally update) Epic/tickets/subtasks and build normalized Jira dataset |
| 2 | BRD + Salesforce Context Reader | Read BRDs and Salesforce metadata context to build requirement+context map |
| 3 | Salesforce Comparison Analyst | Compare both datasets and classify COVERED/PARTIAL/MISSING with Salesforce risk notes |
| 4 | Salesforce Output Finalizer | Write final output files and validate consistency plus Salesforce best-practice checks |

Final files generated:
- `outputs/requirements-covered.md`
- `outputs/requirements-missing.md`
- `outputs/technical-design-document.md`
- `outputs/implementation-checklist.md`

---

## Start the Pipeline

To begin, invoke the **BRD-Jira Orchestrator** with the Epic key and document list provided above.

Replace `{EPIC_KEY}` with the actual Jira Epic key and specify which files to process (or say "all files in inputs/").
