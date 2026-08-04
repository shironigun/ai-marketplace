# AI Marketplace Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Scaffold the `shironigun/ai-marketplace` GitHub repository with a Claude Code marketplace manifest, the QA Toolkit plugin, and placeholder skill files ready for real content.

**Architecture:** Monorepo — all plugins live under `plugins/`. The `.claude-plugin/marketplace.json` at the repo root is the install target. The QA Toolkit plugin lives at `plugins/qa-toolkit/` with its own `plugin.json` and four skill directories.

**Tech Stack:** Plain JSON and Markdown files. Git for version control.

## Global Constraints

- Working directory: `C:\Users\temp\Downloads\Projects\AI Marketplace`
- GitHub handle: `shironigun`
- GitHub repo name: `ai-marketplace`
- Marketplace name identifier: `shironigun`
- Plugin: `qa-toolkit` v1.0.0
- All JSON paths must use `./` prefix (relative, forward slashes)
- Skill files are placeholders — content is transferred from another machine

---

## File Map

| File | Purpose |
|---|---|
| `.claude-plugin/marketplace.json` | Marketplace manifest — lists available plugins |
| `plugins/qa-toolkit/.claude-plugin/plugin.json` | Plugin identity, version, author, keywords |
| `plugins/qa-toolkit/skills/api-failure-to-bug/SKILL.md` | Placeholder skill |
| `plugins/qa-toolkit/skills/api-test-cases/SKILL.md` | Placeholder skill |
| `plugins/qa-toolkit/skills/testcase-to-tracker/SKILL.md` | Placeholder skill |
| `plugins/qa-toolkit/skills/ui-test-cases/SKILL.md` | Placeholder skill |
| `plugins/qa-toolkit/README.md` | Plugin documentation |
| `README.md` | Marketplace install instructions |

---

### Task 1: Init git repo and create directory structure

**Files:**
- Create: `.git/` (via `git init`)
- Create: `.claude-plugin/` directory
- Create: `plugins/qa-toolkit/.claude-plugin/` directory
- Create: `plugins/qa-toolkit/skills/api-failure-to-bug/`
- Create: `plugins/qa-toolkit/skills/api-test-cases/`
- Create: `plugins/qa-toolkit/skills/testcase-to-tracker/`
- Create: `plugins/qa-toolkit/skills/ui-test-cases/`

**Interfaces:**
- Produces: Initialized git repo + full directory skeleton for all subsequent tasks

- [ ] **Step 1: Initialize git repo**

```bash
git init "C:\Users\temp\Downloads\Projects\AI Marketplace"
```

Expected: `Initialized empty Git repository in ...`

- [ ] **Step 2: Create all required directories**

```powershell
$base = "C:\Users\temp\Downloads\Projects\AI Marketplace"
New-Item -ItemType Directory -Force "$base\.claude-plugin"
New-Item -ItemType Directory -Force "$base\plugins\qa-toolkit\.claude-plugin"
New-Item -ItemType Directory -Force "$base\plugins\qa-toolkit\skills\api-failure-to-bug"
New-Item -ItemType Directory -Force "$base\plugins\qa-toolkit\skills\api-test-cases"
New-Item -ItemType Directory -Force "$base\plugins\qa-toolkit\skills\testcase-to-tracker"
New-Item -ItemType Directory -Force "$base\plugins\qa-toolkit\skills\ui-test-cases"
```

Expected: All directories created with no errors.

- [ ] **Step 3: Verify structure**

```powershell
Get-ChildItem -Recurse "C:\Users\temp\Downloads\Projects\AI Marketplace" -Directory
```

Expected: Directories `.claude-plugin`, `plugins`, `plugins\qa-toolkit`, `plugins\qa-toolkit\.claude-plugin`, and four skill directories all present.

---

### Task 2: Write the marketplace and plugin manifests

**Files:**
- Create: `.claude-plugin/marketplace.json`
- Create: `plugins/qa-toolkit/.claude-plugin/plugin.json`

**Interfaces:**
- Consumes: Directory structure from Task 1
- Produces: Valid JSON manifests that Claude Code will parse when the marketplace is added

- [ ] **Step 1: Write `.claude-plugin/marketplace.json`**

Create the file with this exact content:

```json
{
  "$schema": "https://anthropic.com/claude-code/marketplace.schema.json",
  "name": "shironigun",
  "description": "AI tools marketplace by shironigun — skills, plugins, and MCP servers for AI-assisted workflows",
  "owner": {
    "name": "shironigun",
    "url": "https://github.com/shironigun"
  },
  "plugins": [
    {
      "name": "qa-toolkit",
      "description": "QA workflow automation — generate API and UI test cases, convert failures to bugs, push to your tracker",
      "source": "./plugins/qa-toolkit",
      "category": "testing"
    }
  ]
}
```

- [ ] **Step 2: Write `plugins/qa-toolkit/.claude-plugin/plugin.json`**

```json
{
  "name": "qa-toolkit",
  "version": "1.0.0",
  "description": "QA workflow automation — generate API and UI test cases, convert failures to bugs, push to your tracker",
  "author": {
    "name": "shironigun",
    "url": "https://github.com/shironigun"
  },
  "homepage": "https://github.com/shironigun/ai-marketplace/tree/main/plugins/qa-toolkit",
  "repository": "https://github.com/shironigun/ai-marketplace",
  "license": "MIT",
  "keywords": ["testing", "qa", "automation", "test-cases", "bug-tracker"]
}
```

- [ ] **Step 3: Validate both JSON files parse cleanly**

```powershell
Get-Content "C:\Users\temp\Downloads\Projects\AI Marketplace\.claude-plugin\marketplace.json" | ConvertFrom-Json
Get-Content "C:\Users\temp\Downloads\Projects\AI Marketplace\plugins\qa-toolkit\.claude-plugin\plugin.json" | ConvertFrom-Json
```

Expected: PowerShell prints the parsed objects with no errors.

- [ ] **Step 4: Commit**

```bash
git add .claude-plugin/marketplace.json plugins/qa-toolkit/.claude-plugin/plugin.json
git commit -m "feat: add marketplace and qa-toolkit plugin manifests"
```

---

### Task 3: Write the four placeholder SKILL.md files

**Files:**
- Create: `plugins/qa-toolkit/skills/api-failure-to-bug/SKILL.md`
- Create: `plugins/qa-toolkit/skills/api-test-cases/SKILL.md`
- Create: `plugins/qa-toolkit/skills/testcase-to-tracker/SKILL.md`
- Create: `plugins/qa-toolkit/skills/ui-test-cases/SKILL.md`

**Interfaces:**
- Consumes: Skill directories from Task 1
- Produces: Valid (but placeholder) SKILL.md files Claude Code will load. Replace content from your other machine before pushing.

- [ ] **Step 1: Write `skills/api-failure-to-bug/SKILL.md`**

```markdown
# api-failure-to-bug

<!-- PLACEHOLDER: Replace this entire file with the real skill content from your other machine. -->
<!-- This skill converts an API failure into a structured bug report. -->

Use this skill when an API call fails and you want to convert the failure
into a structured bug report for your tracker.

## Instructions

[Paste your real skill instructions here from the other machine.]
```

- [ ] **Step 2: Write `skills/api-test-cases/SKILL.md`**

```markdown
# api-test-cases

<!-- PLACEHOLDER: Replace this entire file with the real skill content from your other machine. -->
<!-- This skill generates test cases from an API spec or response. -->

Use this skill when you want to generate test cases from an API
specification or an actual API response.

## Instructions

[Paste your real skill instructions here from the other machine.]
```

- [ ] **Step 3: Write `skills/testcase-to-tracker/SKILL.md`**

```markdown
# testcase-to-tracker

<!-- PLACEHOLDER: Replace this entire file with the real skill content from your other machine. -->
<!-- This skill pushes generated test cases to a bug/issue tracker. -->

Use this skill when you have generated test cases and want to push
them to your bug or issue tracker.

## Instructions

[Paste your real skill instructions here from the other machine.]
```

- [ ] **Step 4: Write `skills/ui-test-cases/SKILL.md`**

```markdown
# ui-test-cases

<!-- PLACEHOLDER: Replace this entire file with the real skill content from your other machine. -->
<!-- This skill generates UI test cases from a screen or user flow. -->

Use this skill when you want to generate UI test cases from a screen
description or a user flow.

## Instructions

[Paste your real skill instructions here from the other machine.]
```

- [ ] **Step 5: Commit**

```bash
git add plugins/qa-toolkit/skills/
git commit -m "feat: add qa-toolkit skill placeholders"
```

---

### Task 4: Write the READMEs and make initial commit

**Files:**
- Create: `plugins/qa-toolkit/README.md`
- Create: `README.md`

**Interfaces:**
- Consumes: Everything from Tasks 1–3
- Produces: A complete, documented repo ready to push to GitHub

- [ ] **Step 1: Write `plugins/qa-toolkit/README.md`**

```markdown
# QA Toolkit

QA workflow automation for Claude Code — generate API and UI test cases,
convert failures to bug reports, and push test cases to your tracker.

## Skills

| Skill | Trigger | Description |
|---|---|---|
| `api-failure-to-bug` | `/qa-toolkit:api-failure-to-bug` | Convert an API failure into a structured bug report |
| `api-test-cases` | `/qa-toolkit:api-test-cases` | Generate test cases from an API spec or response |
| `testcase-to-tracker` | `/qa-toolkit:testcase-to-tracker` | Push generated test cases to your bug/issue tracker |
| `ui-test-cases` | `/qa-toolkit:ui-test-cases` | Generate UI test cases from a screen or user flow |

## Installation

First add the marketplace:

```bash
claude plugin marketplace add shironigun/ai-marketplace
```

Then install this plugin:

```bash
claude plugin install qa-toolkit
```

## Usage

In any Claude Code session, invoke a skill by name:

```
/qa-toolkit:api-test-cases
```
```

- [ ] **Step 2: Write root `README.md`**

```markdown
# shironigun/ai-marketplace

AI tools marketplace for Claude Code — skills, plugins, and MCP servers
for AI-assisted workflows.

## Install

```bash
claude plugin marketplace add shironigun/ai-marketplace
```

## Plugins

| Plugin | Category | Description |
|---|---|---|
| [qa-toolkit](./plugins/qa-toolkit/) | testing | QA workflow automation — test case generation, bug conversion, tracker integration |

## Adding a plugin to this marketplace

1. Create `plugins/<your-plugin>/`
2. Add `.claude-plugin/plugin.json` with name, version, description, author
3. Add your skill/agent/command files under the plugin directory
4. Add one entry to `.claude-plugin/marketplace.json`
5. Open a PR or push directly
```

- [ ] **Step 3: Final commit**

```bash
git add README.md plugins/qa-toolkit/README.md
git commit -m "feat: add READMEs — marketplace ready to push"
```

- [ ] **Step 4: Verify final structure**

```powershell
Get-ChildItem -Recurse "C:\Users\temp\Downloads\Projects\AI Marketplace" | Where-Object { -not $_.PSIsContainer } | Select-Object FullName
```

Expected files present:
- `.claude-plugin/marketplace.json`
- `plugins/qa-toolkit/.claude-plugin/plugin.json`
- `plugins/qa-toolkit/skills/api-failure-to-bug/SKILL.md`
- `plugins/qa-toolkit/skills/api-test-cases/SKILL.md`
- `plugins/qa-toolkit/skills/testcase-to-tracker/SKILL.md`
- `plugins/qa-toolkit/skills/ui-test-cases/SKILL.md`
- `plugins/qa-toolkit/README.md`
- `README.md`

---

## After Implementation

1. **Create the GitHub repo**: Go to github.com/shironigun and create `ai-marketplace` (public, no auto-init)
2. **Push**:
   ```bash
   git remote add origin https://github.com/shironigun/ai-marketplace.git
   git branch -M main
   git push -u origin main
   ```
3. **Fill in real skill content**: Copy the actual `SKILL.md` files from your other machine, replacing the placeholders
4. **Test install**: On any machine with Claude Code: `claude plugin marketplace add shironigun/ai-marketplace`
