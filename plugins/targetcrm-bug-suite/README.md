# TargetCRM Bug Suite

Three skills for the TargetCRM **Ideal Agile** Azure DevOps project, modeled on Mahmood Ahmad's actual authoring patterns (analyzed across 400+ Bugs and 180+ Defects he created).

| Skill | Files what | Board / type | Trigger examples |
|-------|-----------|--------------|------------------|
| **bugger** | A **Bug** found while testing a story or during regression (QA/Staging) | CRM Team · `Bug` | "file a bug for story 160728", "log this regression", "raise a bug on QA" |
| **defector** | A **Defect** found on **production**/live dealers | Target SWAT · `Defect` | "log a production defect", "file a defect for the live issue", "SWAT defect" |
| **commentor** | A **comment** on any work item, in Mahmood's voice | any | "comment on 149764", "post an update/RCA on this ticket", "CC the dev team" |

## How they relate to the existing skills

- **bugger** is the bug-filing counterpart to the existing **buggy** test-case skill. It reuses buggy's house style, FRS-reading rule, ADO-write conventions, and identity rules — but its job is creating **Bug** work items, not Test Cases. buggy (test cases) and tester (QA review) are unchanged.
- **defector** is bugger's production sibling: same voice, different work-item type, board, and field taxonomy.
- **commentor** handles discussion/`System.History` updates on existing tickets.

## Conventions baked in (from pattern analysis)

- **Identity:** created/QA = Mahmood Ahmad (`mahmood.ahmad@constellationdealer.com`), never "QA Mahmood Ahmad".
- **Auth:** uses the PAT-based `mcp__azure-devops__*` tools only.
- **FRS first:** read the relevant `TARGET DOCS\FRS\modules\*.md` + `RULES.md` before analysing a ticket.
- **Repro anatomy:** `<ul>` steps (environment first) → bold `OBSERVATION:` block → screenshot/GIF → "I know this is resolved when:" acceptance criteria.
- **Bug vs Defect field split, severity defaults, tags, and title conventions** are encoded in each skill's `references/` file.

## Install

Install the packaged `targetcrm-bug-suite.plugin` from **Settings → Capabilities**, or drop the `skills/` folders into your skills directory.
