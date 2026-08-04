# Inventory Format + Worked Example

The harvester output is an **internal, exhaustive, grouped** list. Match this format exactly.

## Format rules

- **Numbered themes**, major initiative first:
  `N. <Theme title> — <one-line what-it-is> (<date range>)` then a sentence of context.
- **Items** under a theme, one bullet each:
  `* <ID> — <title> (<date>), <what/where it touched>. incl. <sub-variant/tests>. PRs (<nums>). Touched <files/services>.`
  Keep it dense: work-item ID, human title, date, code area, PR numbers, and any noteworthy behavior (e.g. a PR that "deliberately held" scope).
- **Non-ticketed deployments** (the whole point of the git sweep) get their own bullets, clearly marked:
  `* <PR #NNNNN / commit sha> — <title> (<date>) — no work item. Touched <files>.`
- **Delineate core vs. generalization.** Put adjacent/reused work in its own theme and say so ("Not DIS itself, but extends the DIS pattern to other DMS types — worth knowing since it reused the DIS foundation.").
- Note **environment** (Staging/Prod) and **DMS** in ALL-CAPS (`DIS`, `ASPEN`, `INFINITY`, `IDEAL`, `QUANTUM`).
- If the git-layer sweep didn't run, put the `⚠ Git-layer sweep not run …` banner at the top.
- End with a one-line hand-off to `releaser` and note the two brand variants (Notify360 for DIS audience, TargetCRM otherwise).

## Worked example — "DIS Two-Way Sync" inventory (the gold standard for shape)

This is the target shape: themes, dense items with IDs + dates + PRs + code touchpoints, core-vs-generalization delineation.

1. **DIS Two-Way Sync — the major initiative (May 11 – Jun 3).** Syncing customer/contact data in both directions between TargetCRM (N360) and DIS, plus an inbound webhook.
   * 168616 — DIS Two-Way Sync implementation (May 29), incl. a Data Review variant and unit tests (PRs 23130/23131/23132/23147). Touched `CustomerReviewHubApi`, customer `Startup`, and the shared sync layer. One PR deliberately held the two-way sync to the Data Review screen only pending review.
   * 168932 — DIS Webhook (merged Jun 3). Inbound customer webhook — `CustomerApi`, `spAddCustomerFromJson`, sync search proc, plus config (`DISCustomerWebhook`). The shared `DisService`/`IDisService` is the core (webhook fires when `dmsType == DmsTypeEnum.DIS`).
   * 170671 — 2-way sync for web Leads on the Deals screen (May 18–20). `DealWebhookService`/`DealWebhookApi` (Leads), `ReceiveMessageFromTwilioHook` (Messaging), and +91 lines to `DisService.cs`.
   * 170666 — no sync for customers created by inbound texts/widget (fix, May 11–13).
   * 170658 — cell phones not syncing from N360 correctly (fix, May 11–13).
   * 170670 — website widget saving a new phone as a related contact (fix, bundled with above).

2. **Phone-number validation for DIS (May 30 & Jul 9).**
   * 172095 — Validate DIS cell phones via Twilio Lookup API (May 30). New `PhoneValidationApi` endpoint + request/response DTOs (~164 new lines).
   * 176095 — Additional validation on DIS numbers (Jul 9). `CustomerPhoneService` (+99), `PhoneValidationApi` (+232), a new `PhoneValidationProcess` table, and the `UpdateValidatedPhoneNumbers` proc.

3. **DIS customer merge tags / automation (May 27).**
   * 170857 — New merge tags for DIS customers, refactored to be generic for all DMS types. Large rewrite of the automation data procs (Email/Task/Text/WorkOrder automation, ReadyToSend*), ~612 insertions / 781 deletions.

4. **DIS-specific features (Jun 15 – Jul 14).**
   * 173515 — Inventory WG: show Suggested Retail Price for DIS dealers (Jun 15).
   * 176450 — Add Transaction Reference for DIS dealers (Jul 14) — surfaced in the messaging conversation panel (final touch in `conversation-panel.tsx`; landed across PRs 24827/24849/24883/24884).

5. **DIS bug fixes, mostly post-launch on staging/prod (Jun 17–18).**
   * 173753 — Order detail drawer returns 500 for DIS dealer (Staging) — fixed (Jun 17).
   * 173898 — Order details APIs fixed for DIS on Prod (Jun 18).
   * 173965 — DIS can no longer see payments — fixed in `paymentPage.tsx` (Jun 18).
   * 173950 — User Context failing for DIS dealers — fixed (PR 24025).

6. **Supporting / generalization work built on the DIS sync (Jun 17–25).** Not DIS itself, but extends the DIS two-way-sync pattern to other DMS types — worth knowing since it reused/generalized the DIS foundation.
   * Support dynamic default location IDs for dealers (Jun 18) — infra the DIS sync depends on.
   * ASPEN/INFINITY DMS hooks + "unify hosted dealer logic" and 173436 ASPEN Two-Way Sync (Jun 17–25).

### What to notice in this example
- Fix-type items (170666/170658/170670, and theme 5) are captured in full here even though `releaser` will almost certainly suppress them — completeness is harvester's job.
- PR numbers are carried on every item that has them; a non-ticketed PR would appear as its own `* PR #NNNNN — … — no work item` bullet.
- Theme 6 is explicitly fenced off as generalization, not the DIS initiative.
- Environments (Staging/Prod) and "deliberately held" scope notes are preserved.
