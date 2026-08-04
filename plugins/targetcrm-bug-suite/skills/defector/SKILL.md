---
name: defector
description: File a production Defect work item on the TargetCRM "Ideal Agile" Azure DevOps project (Target SWAT board), in Mahmood Ahmad's QA house style. Use this skill WHENEVER the user wants to log, file, raise, draft, or create a DEFECT found on PRODUCTION / live dealers — e.g. "log a production defect", "file a defect for this live issue", "raise a SWAT defect", "customers are seeing X on prod, log it", or pastes a production issue and asks to turn it into a Defect. For issues found while testing a story or in regression on QA/Staging use `bugger` (Bug) instead; for posting a comment on an existing ticket use `commentor`.
---

# TargetCRM Production Defect Filing

File a **Defect** the way Mahmood files production issues: a sharp negative-state title, production-first repro bullets ("Login to the production environment" / "checked on multiple live dealers [ID]"), a bolded `OBSERVATION`/`FINDINGS` block, a screenshot, and a "I know this is resolved when:" acceptance line — then create it as a **Defect** work item on the **Target SWAT** board with the production defect-taxonomy fields populated.

Defector is the production sibling of `bugger`: same voice and repro anatomy, but a different work-item type, board, and field set. The deciding test: **was it found on production / a live dealer?** → Defect (this skill). Found in QA/Staging against a story or in regression? → Bug (`bugger`).

## Context you can assume (from project memory)

- **Org:** constellationdealer · **Project:** Ideal Agile (GUID `af3343be-7762-4c0e-ad1f-157f66a850d9`)
- **Board / area path:** `Ideal Agile\Target SWAT` — the production-support / SWAT Kanban board (`Inbox → Done`).
- **Author / QA identity:** Mahmood Ahmad (`mahmood.ahmad@constellationdealer.com`). Never "QA Mahmood Ahmad".
- **Auth:** use the PAT-based `mcp__azure-devops__*` tools only — never the Cowork OAuth ADO plugin.
- **FRS knowledgebase:** behaviour/flow docs at `TARGET DOCS\FRS`. Read the relevant `modules\*.md` + `RULES.md` before analysing the issue. Verify any `[UNCLEAR]`/`[ASSUMED]` flags.

## Workflow

1. **Gather the production facts:** which live dealer(s) + dealer ID, which DMS (ASPEN / INFINITY / EVEREST / IDEAL), the exact steps to reproduce on prod, the actual broken result, and screenshots/GIF. Ask for credentials if a specific prod test dealer is involved.
2. **Read the FRS module** the defect touches (+ `RULES.md`) to name the correct expected behaviour. Flag `[UNCLEAR]`/`[ASSUMED]` rather than asserting.
3. **Decide if it's a data-sync issue** (DMS↔TargetCRM feed). If so set `Custom.DataSyncIssue: true`.
4. **Draft the Defect** (title + repro + acceptance) and **show the user for approval before creating.**
5. **Create the Defect** work item (see "Creating in ADO").
6. Production defects are usually **standalone** (no Story parent). Link to a related ticket only if the user names one.
7. **Report the new Defect ID and URL.**

## Title — same house style as bugger

Declarative negative-state statement; ALL-CAPS the domain keywords (`CLOSED`, `EMAIL`, `MMS`, `PDF`, `ASPEN`, `INFINITY`, `EVEREST`, `IDEAL`, `PRODUCTION`); name the module/screen; end with the environment (here: production/live). Include bracketed dealer ID when dealer-specific.

Real production examples:
- `App crashed on uploading attachment in Settings > EMAIL on Production environment.`
- `Parts & Equipment locator not working for all dealers on production`
- `Download ORDERS module results is not working on production.`
- `SSO not working in TargetCRM through IDEAL WebView on Production test dealer.`
- `CLOSED invoices are syncing as OPEN form ASPEN to TARGET`

## Repro Steps — the anatomy (field: `Microsoft.VSTS.TCM.ReproSteps`, HTML)

Production-first `<ul>` bullets, key UI terms **bolded**, then a bold **`OBSERVATION:`** (or **`FINDINGS`** for deeper investigations) header, then the screenshot/GIF.

```html
<ul>
  <li>Login to the production environment.</li>
  <li>Navigate to <b>Settings &gt; EMAIL.</b></li>
  <li>Upload any attachment from local storage.</li>
  <li>Click on the upload button.</li>
</ul>
<div><b>OBSERVATION:</b></div>
<div><ul><li>The app crashed on uploading any attachment.</li></ul></div>
<div><img src="PASTE_ATTACHMENT_URL?fileName=1.gif" alt=1.gif></div>
```

Multi-dealer variant (narrative + dealer list):
```html
<div>I have checked on multiple live dealers and for some of them, the EQUIPMENT &amp; PARTS LOCATOR is not working.</div>
<div>For reference, check the following dealers:</div>
<ul><li>SOHAR'S ALL SEASON MOWER SERVICE, INC. [10098004]</li></ul>
<div><img src="PASTE_ATTACHMENT_URL?fileName=1.gif" alt=1.gif></div>
```

- First step names **production / the live dealer**. Use `FINDINGS` with a numbered `<ol>` when documenting an investigation (e.g. SSO/auth/API issues), and you may paste the relevant API payload/JSON response inline.
- Screenshot/GIF near-universal (`1.gif` recording, `image.png` still). Leave the `<img>` placeholder and tell the user to attach if not supplied.

## Other fields

Credentials/test data → `Microsoft.VSTS.TCM.SystemInfo` (DmsDealerId / Username / Password block).

Acceptance criteria → `Microsoft.VSTS.Common.AcceptanceCriteria`, phrased "I know this defect is resolved when:".

Field defaults for a **Defect** (full table in `references/ado-defect-fields.md`):

| Field | Value |
|-------|-------|
| `workItemType` | `Defect` |
| `areaPath` | `Ideal Agile\Target SWAT` |
| `priority` | `2` |
| `Microsoft.VSTS.Common.Severity` | usually left unset; set `2 - Medium` (or `1 - High`) for high-impact prod issues |
| `Custom.QA` | `mahmood.ahmad@constellationdealer.com` |
| `Custom.FoundWith` | `Manual Test` |
| `Custom.DefectType1` | `Web` |
| `Custom.DMS` | `Ideal` (or the DMS involved) |
| `Custom.Hosted` | `N/A` |
| `Custom.DataSyncIssue` | `false` (set `true` if it's a DMS↔TargetCRM sync issue) |
| Tags | `By QA Team` + a module tag (e.g. `Settings`, `Broadcasts`, `Inventory`) + `QA` |

`Custom.RootCauseDetails` and `Dealer.ReleaseNote` (branch, format `<id>_<version>_<date>`) are filled **after** the fix by dev/at verification — leave blank at creation.

## Creating in ADO

```
mcp__azure-devops__create_work_item
  workItemType: "Defect"
  title: "<title per house style>"
  projectId: "Ideal Agile"
  areaPath: "Ideal Agile\\Target SWAT"
  priority: 2
  additionalFields:
    "Microsoft.VSTS.TCM.ReproSteps": "<repro HTML>"
    "Microsoft.VSTS.Common.AcceptanceCriteria": "<acceptance HTML>"
    "Microsoft.VSTS.TCM.SystemInfo": "<creds block, if any>"
    "Custom.QA": "mahmood.ahmad@constellationdealer.com"
    "Custom.FoundWith": "Manual Test"
    "Custom.DefectType1": "Web"
    "Custom.DMS": "Ideal"
    "Custom.Hosted": "N/A"
    "Custom.DataSyncIssue": false
    "System.Tags": "By QA Team; QA; <Module>"
```

## Voice rules

Identical to `bugger`: declarative, exact UI/error strings, production-first repro, `OBSERVATION:`/`FINDINGS`, "I know this is resolved when:" fix bar, no ceremony, no hedging.

## Hard rules

- **Always show the draft and get approval before creating** — creation is a real write.
- **Always create as Mahmood Ahmad**, never "QA Mahmood Ahmad".
- If the issue was found in **QA/Staging against a story or in regression**, it's a **Bug** — use `bugger`, not this skill.
