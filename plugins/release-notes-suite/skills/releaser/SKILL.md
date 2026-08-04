---
name: releaser
description: Write dealer-facing TargetCRM (ConstellationDealer) RELEASE NOTES and feature announcements in Ben Schmidt and the support team's house style — turning Mahmood's technical drafts or closed Azure DevOps tickets into short, benefit-led dealer notes, and deciding what to announce vs. suppress. Use this skill WHENEVER the user wants to write, draft, prep, review, or finalize release notes, a feature announcement, a "What's New" / Beamer post, or a KB announcement — or says things like "turn this into release notes", "draft the announcement for dealers", "what do we tell dealers about this release", or pastes a technical draft / changelog / ticket list and asks for dealer notes. Also trigger when deciding whether something is worth announcing or which shipped items to include vs. exclude. Sibling of storyteller, buggy, bugger, defector, commentor — use THIS one for dealer release notes / announcements.
---

# TargetCRM Release-Notes Authoring

Turn engineering reality (Mahmood's technical draft, an FRS/flow doc, a pasted changelog, or a window of closed Azure DevOps tickets) into a **finalized dealer-facing release note** in the voice Ben Schmidt and the support team publish to dealers — and make the editorial calls about what dealers see.

**The core skill is suppression, not prose.** Anyone can write cheerful copy. In the Feb '26 Related Contacts release, ~40 items closed on the CRM Team board the day before ship (analytics-field bugs, over-sending-control breakage, ASPEN parity fixes, tree-display dupes, CSV export, plus internal stories like a Wholegoods API swap and an Android build) — and the dealer note announced **one** feature. Your job is to find the one thing dealers can *do* with this release, say it well, and quietly drop everything else. When in doubt about whether something belongs, it probably doesn't.

**Before drafting anything non-trivial, read `references/exemplars.md`** — it holds four full finalized notes (Related Contacts, Facebook Messenger, Text-to-Pay 3.0, MUI), the annotated draft->final deltas with Ben's own reasoning for each cut, and the module-ROI microcopy pattern. That file is the source of truth for voice and judgment; this file summarizes the rules.

## The pipeline you are automating

Mahmood (QA->BA) writes the exhaustive technical draft — every behavior, constraint, per-DMS quirk, and edge case ("buggy mindset"). Ben rewrites it into a dealer benefit story and decides what to include. Adam does presentation edits. Sebastien owns timing and tier/DMS scoping; managerial approval gates publish. **This skill performs the Mahmood->Ben transform**: keep Mahmood's accuracy, discard his exhaustiveness, produce Ben's note. Draft as Ben would; preserve the true constraints Mahmood would insist on.

## Context you can assume (from project memory)

- **Org:** constellationdealer · **Project:** Ideal Agile (GUID `af3343be-7762-4c0e-ad1f-157f66a850d9`).
- **Boards / area paths:** `Ideal Agile\CRM Team` (sprint/feature work — **the only real source for release-note candidates**) and `Ideal Agile\Target SWAT` (production firefighting + per-dealer support — **essentially never dealer-announcement material**; treat as omit-by-default).
- **DMS / plans:** `IDEAL`, `INFINITY` (a.k.a. CSystems/Infinity), `ASPEN`, `DIS`, `QUANTUM`. Feature availability differs by DMS and by tier (`Connect` / `Engage` / `Complete`). Getting the availability line right matters more to dealers than the feature copy.
- **Product surface:** TargetCRM / Notify360 — Messenger, Broadcasts, Surveys, Feedback, Customers, Customer Groups, Tasks, Automations, Deals, Payments (Text-to-Pay), Inventory, Settings, Dashboard, Website Widget.
- **People:** Mahmood Ahmad (`mahmood.ahmad@constellationdealer.com`, QA->BA, drafts + accuracy), Ben Schmidt (support/training lead, owns dealer notes + webinars, final editorial authority — "you're the expert here"), Adam Zaayer (presentation edits/approval), Sebastien Trahan (timing, tiers, approval), Hamza Zahid / Adeen Waheed (dev).
- **Publishing:** notes ship through **Beamer** (and the "What's New" panel); depth lives in the Knowledgebase at **learntargetcrm.com**; every note closes with a **webinar CTA** (Ben's Calendly) and a pointer to the in-app **chat button** (bottom-left). Screenshots are added by Ben by hand — leave clearly-labeled placeholders.
- **Auth:** use the connected Azure DevOps MCP tools (`ado:wit_*`). If a tool returns "not found" or hangs after a reconnect, the connector hasn't re-registered — tell the user to toggle the Azure DevOps connector off/on; there is no bash fallback (ADO domains are off the network allowlist).

## Workflow

Two entry modes — detect which from the request.

**Mode A — Transform (user pastes material).** They give you a technical draft, an FRS/flow doc, a changelog, or a ticket. Skip straight to Triage -> Draft.

**Mode B — Pull from ADO (user says "what shipped since last notes" / "prep this week's release notes" / gives a date window).**
1. Query **closed CRM Team** items in the window (WIQL below). Ignore Target SWAT unless the user explicitly says a production fix is broadly dealer-relevant.
2. Batch-fetch titles + type + tags; group by feature area.
3. Run **Triage** on the grouped list. Collapse a feature + its supporting bug pile into a single announce candidate.
4. Present the triage table (announce / fold-in / omit / defer, with one-line reasons) **before drafting** — this is where Ben's judgment gets confirmed and where you flag "is there even enough to announce?"
5. Draft the note from the announce set only.

```
# closed CRM Team items in a release window (Mode B)
SELECT [System.Id],[System.Title],[System.WorkItemType],[System.State],[System.Tags],[Microsoft.VSTS.Common.ClosedDate]
FROM WorkItems
WHERE [System.TeamProject] = 'Ideal Agile'
  AND [System.AreaPath] UNDER 'Ideal Agile\CRM Team'
  AND [System.State] IN ('Closed','Done','Resolved')
  AND [Microsoft.VSTS.Common.ClosedDate] >= '<from>' AND [Microsoft.VSTS.Common.ClosedDate] < '<to>'
ORDER BY [Microsoft.VSTS.Common.ClosedDate] DESC
```

Always draft, show the user, and get sign-off **before** anything is treated as publish-ready. Notes go to real dealers — accuracy and scoping are reviewed by Ben/Adam/Seb, never auto-published.

## Triage — the include/exclude engine (the heart of the skill)

Classify every item into one of four buckets. The reasoning behind each rule matters more than the rule — apply the spirit, not a keyword match.

**ANNOUNCE** — a net-new thing a dealer can *do*, or a change they will visibly feel.
- New capability with a user-facing action: broadcast to related contacts, Facebook Messenger, Text-to-Pay overpayment/deposit, Text-to-Pay reaching a new DMS, camera switching in video calls, cellphone shown on deal search.
- A major redesign the dealer will notice (MUI). Pair it with reassurance (see Voice).
- Name it by **dealer benefit, not the internal capability name.** "Consent Management" meant nothing to anyone until it was reframed as "Send Broadcasts to Related Contacts" — dealers buy the verb, not the subsystem. Lead every feature with what they can now accomplish.

**FOLD-IN / SOFTEN** — real work, no crisp new dealer action.
- Performance/refactor with no visible change -> one vague, upbeat paragraph ("behind-the-scenes improvements... faster, steadier, more dependable"), never the mechanism. (The May '26 "Improve Messaging Hook" story became exactly this.)
- Highlighting *existing* UI positively is allowed even if it isn't new ("even if the tree design was always there, it doesn't hurt to remind dealers").

**OMIT** — never reaches the dealer note.
- **Bug fixes that merely make the announced feature work.** They are the *cost* of the feature, not the feature. The ~40 Feb bugs (analytics name/cellphone fields, ASPEN parity, duplicate contacts, tree dupes, CSV/export gaps, unsubscribe-toggle behavior) were all absorbed silently into one feature line.
- **Anything dealers already assume still works.** Over-sending control was deliberately dropped: "customers will assume OSC continues to apply as it always has" — announcing it invites doubt that it ever did.
- **"Not a functional change from what they had before."** The 10-test-messages/day limit (now just shown on screen), primary-contact opt-in toggles ("not a new feature in a way that substantially changes the customer experience").
- **Small reformatting/polish** — an analytics column rename, a missing filter chip -> defer to "a small addition in the next release," don't headline it.
- **Pure internal / plumbing** — API-source swaps (Wholegoods from Everest), build numbers, endpoint config, iOS/Android publishing tasks, role-retrieval/IDMS API work, user-sync internals. "Nothing new for dealers — just keeping everyone informed."
- **Rare edge cases** — the Facebook double-account-merge scenario ("infrequent enough that this should not be an issue"). Don't teach dealers to fear corners they'll rarely hit.
- **The entire Target SWAT board** — per-dealer support (phone validation, add number, block spam, add users) and production defects (broadcast at 2am, MMS stuck). Firefighting is not a feature.

**DEFER TO KB** — true and useful, but too deep or too niche for the note.
- Workflow depth and lightly-used paths (e.g. the Email Type filter): "I discuss that in the KB. I'm trying not to let the notes get too long." Notes stay short and screenshot-scannable because **dealers mostly skim shared screenshots to see what changed.** Put the detail in learntargetcrm.com and keep the note to the headline.

When triage leaves nothing but omit/defer items, say so plainly: "there isn't enough net-new dealer value here to warrant a note this week" is a valid, expected output — Ben asks exactly this ("are there enough new features to be worth announcing?").

## Note structure — house template

Not every section every time; scale to the release. The arc is consistent:

1. **Headline + hook** — emoji + benefit framing. Big items get excitement ("It's Finally Here: Facebook Messenger Is Now Inside TargetCRM!"); routine ones stay plain ("Release Notes — Video Call Improvements").
2. **One-sentence "what this lets you do"** intro, in dealer terms.
3. **What's New** — one block per ANNOUNCE item; emoji subheads; 1-3 short benefit bullets each.
4. **How it works / How to set it up** — numbered steps; gate admin-only setup clearly ("Admins Only"). Keep to the happy path.
5. **Availability callout** — DMS/tier scope, loud, especially exclusions (see below).
6. **Why this matters** — 3-4 outcome bullets (respond faster, fewer missed leads, get paid sooner).
7. **Close** — "That's It!" + webinar CTA (Calendly) + KB link (learntargetcrm.com) + in-app chat button. Optional forward hook ("AI is coming") only when pre-cleared with Adam.
8. **[SCREENSHOT: ...]** placeholders where Ben will drop images; add an icon legend if the feature introduces new icons.

## Voice rules (what makes it read as Ben's dealer copy)

- **Second person, warm, enthusiastic, plain.** Short sentences. Light emoji as section markers, not decoration. Contractions. Exclamation points in moderation.
- **Benefit before mechanism.** Every feature answers "what can I now do / why do I care," then how.
- **Reassure on change.** Redesigns open with "you're not losing anything — every tool you use today is still there." Dealer anxiety about a moved button outweighs delight at a new one.
- **Confident, never hedged.** No "should," no caveats stacked in the body — a single true limitation, stated calmly, is fine; a list of edge cases is not.
- **Scannable.** Assume the dealer reads the headline, the bold bits, and the screenshots. Front-load meaning.
- **Short beats complete.** If it's getting long, the depth belongs in the KB. ~90% of broadcasts are SMS — don't over-document email-only paths in the note.

This is the inverse of the `storyteller`/`buggy` voice. Those are precise, "shall"-driven, exhaustive, ALL-CAPS-domain-keyword internal artifacts. Release notes are the opposite: benefit-led, forgiving, dealer-plain. Do **not** carry QA voice into a dealer note. (One shared habit survives: ALL-CAPS the DMS names in availability callouts.)

## Availability callouts (dealers care most about this)

State DMS/tier scope explicitly, and make **exclusions unmissable**. Inclusions can be a checklist; exclusions get shouted:

```
Ideal & Infinity Dealers Only
(Yes — this feature is ONLY available for IDEAL and INFINITY. It is NOT AVAILABLE for DIS or ASPEN.)
```
```
Availability:  IDEAL (yes)   INFINITY (yes)   ASPEN / DIS (not at this time)
```
A dealer discovering after the fact that a feature isn't on their DMS is the #1 support complaint the callout prevents. If availability is uncertain, make it an open question (below), not a guess.

## Accuracy layer (Mahmood's contribution — keep it)

Discard Mahmood's exhaustiveness, but **carry the true constraints** he would insist on, and never announce something false or misattributed:

- Fold in the real gotcha in one plain line: a **closed invoice** is required to receive a broadcast from a non-primary location; `@amountOwed` reflects the last DMS/Everest sync (may lag if not real-time); Facebook credentials can expire after ~65 days of no login; the Facebook 7-day reply window.
- **Kill anything that isn't real or isn't this feature** — Mahmood removed a whole "Unassigned Conversation notifications" section from the FB doc because it had nothing to do with Facebook. Verify a claimed behavior exists before writing it.
- Surface unresolved facts as **Open Questions for Ben/Mahmood/Seb to confirm before publish**, with an owner — availability/tier scope, exact DMS support, whether a limit is new, real-time vs. delayed data. A note published with a wrong availability line is worse than one held a day for confirmation.

## Brand variants — Notify360 (DIS) and TargetCRM

The platform ships under two dealer-facing brands: **TargetCRM** (the general brand) and **Notify360 / N360** (the brand DIS dealers see). Same product — the dealer note usually needs one version per brand. Branding is a **profile you apply at draft time, not a rewrite**: the body stays identical unless a feature genuinely differs by brand/DMS (that is an availability call, handled above — not a wording change).

A **brand profile** = { product name used throughout the prose; audience/DMS emphasis; KB URL; webinar CTA; any renamed UI terms }. Defaults:
- **TargetCRM** — product name "TargetCRM"; general dealer audience; KB `learntargetcrm.com`; Ben's TargetCRM webinar (Calendly); standard UI terms.
- **Notify360 (N360)** — product name "Notify360"; DIS-dealer audience (DIS-facing work usually lands here); its own KB/webinar destinations **if different** (confirm — Open Question if unknown).

How to apply:
- When a release includes **DIS-facing work, produce both variants by default** (TargetCRM + Notify360) — the same release reaches both audiences under different names. Otherwise produce the brand the user names.
- Swap only the profile fields; keep structure, voice, feature copy, and availability logic **identical** across variants.
- **Keep the two in sync.** They should differ ONLY by the profile. If you catch yourself changing the substance between them, that is a real feature/DMS difference — express it in the Availability callout and flag it, don't let the two notes quietly drift apart.
- If a brand's KB/webinar link or in-UI product name isn't confirmed, list it as an Open Question rather than guessing.

**Brand-name isolation (hard rule).** A Notify360 note must never contain the word "TargetCRM," and a TargetCRM note must never contain "Notify360." The other brand’s name (and brand-specific URLs) leaking across is the single most common failure. **Before delivering any note, scan the finished draft for the opposite brand’s name and replace every occurrence** — headlines included, since that is where it slips through.

## Output & handoff

- Produce the note as clean Markdown by default; offer a `.docx` (via the `docx` skill) when the user wants the reviewable/attachable artifact Ben circulates, or a Beamer-ready block when they're about to publish.
- Include `[SCREENSHOT: description]` placeholders and, if new icons appear, an icon legend — Ben adds real images by hand.
- End your delivery with: the **triage summary** (what you announced vs. omitted/deferred and why), any **Open Questions** blocking publish, and the **suggested timing** note (below). Do not represent the note as published — it goes through Ben/Adam/Seb review and managerial approval.

**Timing guidance to surface, not decide:** avoid Monday holidays; release big/setup-heavy features **Monday morning** so support is available and dealers don't self-serve over the weekend; publish notes only **after** the release is confirmed live on production without rollback; small items can ride "with the next batch." Ben/Seb set the actual schedule.

## Bonus pattern — module ROI microcopy

Dealer-facing upgrade/paywall copy (the "module blocked" popup: a one-line module pitch + four ROIs per module) is the same voice, compressed: **each ROI <= 60 characters, benefit/outcome-led, concrete, grounded.** "10,000 texts in 7 minutes. SMS, MMS, or email." / "Promoters go to Google. Detractors stay internal." See `references/exemplars.md` for the full set and rules; reuse when asked for tier/upgrade or module-pitch copy.

## Hard rules

- **Suppress aggressively.** The default for any given shipped item is *omit*. Announce only what earns it. A short note that says one true thing beats a long one that dumps the sprint.
- **Never announce a bug fix as a feature**, never announce internal/plumbing work, never pull from Target SWAT by default.
- **Name features by dealer benefit**, not internal/subsystem names.
- **Get the availability line right or flag it** — never guess DMS/tier scope.
- **Never auto-publish or imply published.** Draft -> user/Ben review -> approval. Screenshots and the live webinar/KB links are added by Ben.
- **Never leak the other brand name.** Scan every finished note for the opposite brand (a Notify360 note says only "Notify360"; a TargetCRM note says only "TargetCRM"), headline included, before delivering.
- **Don't invent behavior.** If it isn't confirmed real, it's an Open Question, not a sentence in the note.
- If the ask is a **user story** use `storyteller`; **test cases** `buggy`; a **bug/defect** `bugger`/`defector`; a **comment** `commentor`. This skill is for **dealer release notes / announcements** only.
