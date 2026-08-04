# Defect field reference (Target SWAT)

Derived from Mahmood's actual Defects on `Ideal Agile\Target SWAT`.

## Bug vs Defect — the deciding split

| Dimension | **Bug** (`bugger`) | **Defect** (this skill) |
|---|---|---|
| Where found | QA / Staging, testing a story or regression | **Production / live dealers** |
| Area path | `Ideal Agile\CRM Team` | `Ideal Agile\Target SWAT` (Kanban `Inbox → Done`) |
| Parent | linked to a **User Story** | usually **standalone**, no parent |
| Severity | set (`3 - Medium`) + `ValueArea = Business` | often unset; set `2 - Medium`/`1 - High` for impact |
| Defect taxonomy | not set | `DefectType1=Web`, `DMS=Ideal`, `Hosted=N/A`, `DataSyncIssue` |
| Tags | usually none | `By QA Team` + module + `QA` |
| Post-fix | — | `Dealer.ReleaseNote` (branch) + `Custom.RootCauseDetails` |
| Common to both | `Custom.QA = Mahmood`, `Custom.FoundWith = Manual Test`, `Priority = 2`, repro anatomy, "I know this is resolved when:" | |

## Field table

| Field | Reference name | Value |
|-------|---------------|-------|
| Type | `System.WorkItemType` | `Defect` |
| Area path | `System.AreaPath` | `Ideal Agile\Target SWAT` |
| Priority | `Microsoft.VSTS.Common.Priority` | `2` |
| Severity | `Microsoft.VSTS.Common.Severity` | usually unset; `2 - Medium` / `1 - High` for high impact |
| QA owner | `Custom.QA` | Mahmood Ahmad |
| Found with | `Custom.FoundWith` | `Manual Test` |
| Defect type | `Custom.DefectType1` | `Web` |
| DMS | `Custom.DMS` | `Ideal` (or the DMS involved) |
| Hosted | `Custom.Hosted` | `N/A` |
| Data sync | `Custom.DataSyncIssue` | `false` (set `true` for DMS↔TargetCRM sync issues) |
| Repro | `Microsoft.VSTS.TCM.ReproSteps` | HTML |
| Acceptance | `Microsoft.VSTS.Common.AcceptanceCriteria` | "I know this defect is resolved when:" |
| Sys info | `Microsoft.VSTS.TCM.SystemInfo` | creds block |
| Tags | `System.Tags` | `By QA Team; QA; <Module>` |
| Release note (post-fix) | `Dealer.ReleaseNote` | `<id>_<version>_<date>` e.g. `151089_3.4.0_06_March` |
| Root cause (post-fix) | `Custom.RootCauseDetails` | short dev RCA |

## Verbatim repro example (Defect 151089, production crash)

```html
<ul><li>Login to the production environment. </li><li>Navigate to <b>Settings &gt; EMAIL.</b> </li><li>Upload any attachment from local storage. </li><li>Click on the upload button. </li></ul>
<div><b>Observation:</b></div>
<div><ul><li>The app crashed on uploading any attachment. </li></ul>
<div><img src="…/attachments/429c7119-…?fileName=1.gif" alt=1.gif></div></div>
```

## Verbatim repro example (Defect 151381, multiple live dealers)

```html
<div>I have checked on multiple live dealers and for some of them, the EQUIPMENT &amp; PARTS LOCATOR is not working. </div>
<div>For reference, check the following dealers: </div>
<ul><li>SOHAR'S ALL SEASON MOWER SERVICE, INC. [10098004] </li></ul>
<div><img src="…/attachments/6cff4d08-…?fileName=1.gif" alt=1.gif></div>
```

## FINDINGS variant (Defect 169324, SSO investigation)

For auth/SSO/API investigations he uses a bold `FINDINGS` header with a numbered `<ol>` of investigation notes and pastes the API payload/JSON response inline. Example finding lines:
> 1. IDMS is able to generate the auth token (attachment #1). 2. TargetCRM is not handling the SSO efficiently. 3. IDEAL dev pointed out there are 2 users with Admin username — needs checking (payload below).

## Verbatim post-fix RootCauseDetails examples

- "There was a circular dependency on updating the email content in case of file upload which causes the application to run out of memory and crash the application."
- "there was issue with email place holder"

## Title examples (verbatim, production)

- `App crashed on uploading attachment in Settings > EMAIL on Production environment.`
- `Parts & Equipment locator not working for all dealers on production`
- `Download ORDERS module results is not working on production.`
- `SSO not working in TargetCRM through IDEAL WebView on Production test dealer.`
- `CLOSED invoices are syncing as OPEN form ASPEN to TARGET`  ← data-sync defect → set `DataSyncIssue: true`
