# Release-Notes Exemplars, Deltas & Reasoning

This file is the voice-and-judgment source of truth. It has three parts:
1. **Full finalized notes** — the published dealer copy, to match register.
2. **Draft->final deltas** — what Ben/Adam cut or changed, with Ben's actual reasoning (quotes). This is where the judgment lives.
3. **ADO calibration + ROI microcopy pattern.**

Read the deltas closely: the finished notes teach the *voice*, the deltas teach *what never makes it in and why*.

---

## EXEMPLAR 1 — "Send Broadcasts to Related Contacts" (Feb '26)

Internal name: **Consent Management**. Shipped Feb 17. This is the richest example of the transform.

### 1a. Mahmood's technical draft (condensed) — the input
Titled "Consent Management & Related Contacts Broadcasting." Exhaustive and precise:
- Contacts now have a Birthday column; Cellphone + Email Opt-In toggles (primary and related).
- Include Related Contacts toggle in Customer Group filters (hidden for DIS). Filters apply to customers first, then contacts populate under the parent in a tree.
- Cellphone filter uses AND logic, overriding other filters (used to target one specific contact).
- Broadcast segments include contacts; Survey segments auto-exclude them.
- OSC (over-sending control) logs now created for contacts; contacts suppressed during the OSC window.
- Cancel Broadcast applies to contacts.
- Broadcast location rule: from a non-primary location (given a CLOSED invoice there) the customer gets that location's marketing number; **related contacts always receive from the primary location's marketing number.**
- Unified tree UI across Messenger / Broadcast Analytics / Customer Groups; "Organization / Name / First / Last" columns collapsed to a single **Name** column; contact stats in expanded analytics; contacts included in CSV/Excel exports.

### 1b. The finalized dealer note (published, Adam-edited) — the output
> **February '26 New Feature Update: Send Broadcasts to Related Contacts!**
> You can now send text and email broadcasts not only to a customer's main contact, but also to any related contacts (i.e. business managers, billing department, close family, etc.) Our additions enable easier ways to reach your customers.
>
> **Updates to Contacts** — Within a customer's contact list you'll now see a Birthday column, and when editing/creating a contact, Phone and Email opt-in toggles to opt in/out of broadcast. *Note: Only broadcasts can be sent to related contacts at this time. Surveys are planned in a future release.*
>
> **Add Related Contacts to Customer Groups** — An Include Related Contacts switch within filters lets you automatically include/exclude related contacts when building Customer Groups. Choose your usual filters; when the toggle is on, related contacts display underneath the main customer record in a tree-style list.
>
> **Targeting a Specific Related Contact** — Make sure the contact has a phone number and is opted in; apply the phone number as a filter; turn on Include Related Contacts; search by contact phone number. Phone filters are very precise, so only related contacts with matching phone numbers will appear.
>
> **Which Number Sends the Message if I have multiple locations?** — If a customer record has a closed invoice at a secondary location: the primary customer record phone/email receives from that secondary location's marketing number; related contacts always receive from the primary location's marketing number.
>
> **UI & Analytics Improvements** — a clearer tree structure showing customers with their related contacts underneath; delivery info for contacts on broadcast cards; a simplified Name field replacing multiple name columns; analytics stats for related contacts when included; look for these icons within related contacts: [ICON LEGEND].
>
> **Summary** — Easily include key related contacts in your broadcasts; control who receives messages with simple opt-in settings; more organized tree contacts display.
>
> **That's It!** We hope you love these updates! To attend a free webinar, click here to register! If you have questions, use the chat button on the bottom left corner of your TargetCRM.

### 1c. The deltas — what changed and why (the lesson)
- **Renamed the whole feature.** "Consent Management" -> "Send Broadcasts to Related Contacts." Ben, after a long thread, still couldn't tell what "Consent Management" *did*; once it was clear the only consent managed was broadcast opt-in for related contacts, the note was named for the dealer action. **Lesson: name by the verb the dealer performs, not the subsystem.**
- **Cut Over-Sending Control entirely.** Ben: *"I deliberately removed the section about Over-sending control. This is certainly a valuable feature, but customers will assume that over-sending control will continue to apply for all broadcasts as they always have."* **Lesson: don't announce what dealers already assume is true — it plants doubt.**
- **Cut primary-contact opt-in toggles.** Ben: *"The Primary contacts situation is not a new feature in a way that substantially changes the customer experience, so I do not believe it bears mentioning."* (Also slated for removal next phase.)
- **Cut the analytics/export reformatting as its own item.** Ben: *"my stance is that this change is relatively small, and does not bear specific announcement."* (The column collapse to "Name" is mentioned in passing under UI, not headlined.)
- **Kept the tree design even though it wasn't new in Messenger.** Ben: *"Even if the tree design was always available in Messenger, it doesn't hurt to highlight it to dealers."* **Lesson: positively re-surfacing existing UI is fine.**
- **Deferred a live bug to next release.** A missing filter chip when the related-contacts toggle is active -> Adam: *"let's add this as a small addition to the story that can go out in the next release."*
- **Added Mahmood's true constraint.** Mahmood: *"customer needs to have a closed invoice (payment done) to receive broadcast from that specific non-primary location"* -> "invoice" became "closed invoice" in the final. And Mahmood supplied the **icon legend** for dealers.
- **Suppressed ~40 bug fixes silently.** Everything that made the feature actually work (analytics name/cellphone fields showing N/A or first-name-only, ASPEN parity, duplicate contacts, unsubscribe-toggle behavior, CSV export gaps) never appears. They are the cost of the feature, not the feature.
- **Adam's presentation edits.** Reworded the relatable examples ("additional employees, spouses, or business partners" -> "business managers, billing department, close family, etc.") and simplified phrasing. Softer, more dealer-relatable.

---

## EXEMPLAR 2 — "Facebook Messenger Is Now Inside TargetCRM!"

Input: Mahmood's multi-page FRS flow doc (account linking, page->department mapping, filters, customer creation, merge, sync, limitations, "What If" scenarios). Output note:

> **It's Finally Here: Facebook Messenger Is Now Inside TargetCRM!**
> This is a big one. Customers have been asking for this for a long time, and it's finally live! You can now connect Facebook Messenger directly to TargetCRM, so your team can manage Facebook messages without leaving the CRM. Faster replies, better tracking, and fewer missed leads — all in one place.
>
> **What's New?** Facebook messages show up in TargetCRM Messenger; reply right away; conversations stay tied to the correct department (each Page connects to one department). Facebook conversations are clearly marked with an icon, and you can filter your inbox to Text-only or Facebook-only.
>
> **How to Set It Up (Admins Only)** — Step 1: Settings -> Departments, pick the location (Facebook accounts are tied to locations), click Link Facebook, log in with the dealership's Facebook credentials and approve access. Step 2: find the department, click the gray Facebook icon, choose the Page, click Link Page. When connected the icon turns blue; each department = one Page and each Page = one department.
>
> **Facebook Customers & Records** — a customer record is created automatically and marked with the connected Facebook account. Recommendation: if the customer already exists, merge; if not, use Sync on the Customer Review tab to create the record in your DMS. Keeps data clean and avoids duplicates.
>
> **Merging Facebook Customers** — all history stays with the main record, conversations move over, nothing important is lost. Best practice: merge Facebook leads as soon as possible.
>
> **Important Facebook Rules to Know** — *Login expiration (low risk):* credentials may expire after 65 days with no one logging into TargetCRM; for most dealers not a concern since users log in daily; an admin can reconnect. *7-Day messaging window (very important):* if 7 days pass since the last message received, the conversation times out and you can't reply — check Facebook messages at least once a week. *Other limits:* conversations can't be reassigned or archived; they stay with the connected department.
>
> **Why This Matters** — respond faster, keep conversations in one place, track Facebook like any other channel, prevent missed/dropped conversations.
>
> **We're Excited — and We Know You Are Too.** Connect your Pages, assign them to departments, and start replying today. Click HERE for a free webinar!

### Deltas & reasoning
- **Removed a whole misattributed section.** Mahmood: *"the document holds an unwanted section. Please ignore the email notifications stuff... Facebook integration has nothing to do with the email notifications."* -> cut. **Lesson: never announce behavior that isn't part of this feature; verify it's real.**
- **Cut the double-account-merge edge case.** Mahmood flagged that after merging, replies still go to two separate FB threads (correct, since Facebook can't merge identities). Ben: *"I expect that exact issue... will come up infrequently enough that this should not be an issue."* -> omitted.
- **Kept two limitations, framed calmly.** The 65-day expiry (reframed "Low Risk for Most Dealers") and the 7-day reply window ("Very Important") — real constraints dealers must know, stated without alarm.
- **Reframed a technical fact as reassurance.** Mahmood clarified the 65-day expiry only triggers with no *login* for 65 days, and daily API activity keeps it alive -> became "for most dealers, this should not be a concern."
- **Suppressed the FRS depth.** Attachment formats, voice-note web-vs-mobile limits, Data Review routing, the Social Channels column mechanics, opt-in-all-vs-current-pages Meta permission choice — all live in the doc/KB, none in the note.
- **Timing call captured for reference.** Big/setup-heavy feature -> released Monday morning ("so we don't get a ton of customers trying to set it up over the weekend while support is unavailable"), notes published only after prod confirmed stable.

---

## EXEMPLAR 3 — "Text-to-Pay 3.0 Is Here for More Dealers!"

Note the **loud availability handling** — this is the pattern to copy whenever a feature is DMS-gated.

> **Big News: Text-to-Pay 3.0 Is Here for More Dealers!** Now, both IDEAL dealers and CSystems/Infinity can use Text-to-Pay 3.0 — faster payments, clearer requests, fewer mistakes, no matter which system you use.
>
> **Three Easy Ways to Request Payment** — *Balance:* pick the order, click send, customer pays via link, auto-applied to the correct invoice in your DMS. *Deposit:* ask for a fixed dollar amount or percentage; great for deposits/partial payments; minimums apply. *Manual:* the classic option (still works for IDEAL, Infinity, and Aspen) — send a link for any amount and apply it manually in the DMS.
>
> **Why This Is Awesome** — get paid faster, less confusion, easy to track, works for all dealer types.

And the companion **Overpayment** update (published May 14) shows the shouted-exclusion style:

> **Request Overpayments on Text-to-Pay Deposits** — *Ideal & Infinity Dealers Only* (Yes — this feature is ONLY available for Ideal and Infinity. This feature is NOT AVAILABLE for DIS or ASPEN.) You can now request an overpayment when sending a Text-to-Pay deposit request: request more than the invoice total, up to $1,000 extra — perfect for special orders or items that need money up front.

### Deltas & reasoning
- **Availability is the loudest thing on the page**, repeated at top and bottom, with exclusions in caps. Dealers on the wrong DMS discovering this later is the support cost this prevents.
- **Omitted the "What's Fixed" list.** Mahmood's draft had validation fixes (blocked alphabets in the percentage field, prevented empty percentage, fixed amount-field behavior when switching options — that's Improvement 170097). None announced; only the positive capability.
- **Simplified the mechanic.** The $1,000-above-order cap and real-time validation errors stayed as a benefit ("up to $1,000 extra"); the exact error string and per-entry-point enforcement went to the KB.

---

## EXEMPLAR 4 — "TargetCRM Has a Brand-New Look" (MUI)

The redesign playbook: reassure first, tease the future, push depth to KB.

> **TargetCRM Has a Brand-New Look — and a Lot of New Features!** ... Here's the most important thing to know up front: **you're not losing anything.** Every tool you use today is still there. Some buttons have moved. Some screens look different. But everything still works — and in most cases, it works better than ever.
> ... [Fresh look; panels dock right instead of pop-ups; "My [Items]" filters; collapsible left menu; smarter Dashboard; Broadcasts details panel + test-send; five-tab Customer Details; Surveys+Feedback merged; step-by-step Customer Group builder; fully rebuilt Deals with tabs, products, quotes] ...
> **Getting Ready for What's Next** — Artificial intelligence is coming to TargetCRM. We're not ready to share all the details yet, but this new structure is designed to make room for AI-powered tools... Stay tuned.
> **Watch the Walkthrough Webinars** [Ideal / Infinity / Aspen / Quantum] ... Or visit our full knowledge base: learntargetcrm.com.

### Deltas & reasoning
- **Reassurance leads**, because dealer anxiety about a redesign ("where did my button go?") is the real risk, not the features.
- **AI forward-hook** was cleared with Adam before inclusion ("Yeah, I cleared that paragraph with Adam"). Mahmood noticed and liked "the glimpse hook of AI feature." **Lesson: forward teases only with management sign-off.**
- **Cut the 10-test-messages/day limit.** Ben: *"Since it is not a functional change from what they had before, no. They've always had a limit of ten... now we just put a note about it on screen."*
- **Deferred the Email Type filter to KB.** Ben: *"I discuss that in greater detail in the Knowledgebase Documentation. I'm trying not to let the release notes get too long."* Mahmood agreed: dealers "are likely to only see shared screenshots to scan what's changed," and email workflows won't be read in a long note. (~90% of broadcasts are SMS.)
- **Publish discipline.** "Release through Beamer as soon as the MUI update is confirmed live, and not needing a rollback."

---

## ADO calibration (what the boards prove)

Use this to gut-check how ruthless the suppression is.

- **Feb '26 Related Contacts window, CRM Team board:** ~40 items closed the day before release — almost all Bugs about the feature's internals (analytics name/cellphone fields, ASPEN parity, OSC breaking customer groups, tree dupes, CSV export), plus User Stories that were pure plumbing (Wholegoods screen API call = "Inventory whole-goods now fetched from new Everest API, no user-facing changes"; Android build 20.0.0; "testing environments still point to old endpoints"). **Dealer note announced: one feature.**
- **May '26 window, CRM Team board:** announced overpayment (story 168765) + mobile video + a vague Messenger-perf paragraph (story 167954 "Improve Messaging Hook"). Shipped same window but **not announced:** widget Zip/Postal search + its bugs, "privacy policy displayed twice" widget fixes, "Analyse IDMS APIs / productid filtering for role retrieval" (user-sync plumbing), iOS/Android Publishing Details tasks, a per-dealer Survey defect.
- **Target SWAT board (any window):** phone validation, add text-enabled number, block spam number, add users, remove location, "broadcast sent at 2am," "MMS stuck in In Progress," "user cannot login." **Zero of these are release-note material.** SWAT = firefighting.

Ratio to internalize: **one dealer-facing feature can sit on top of dozens of closed items.** The note names the one; the rest stay invisible.

---

## Module ROI microcopy pattern (tier/upgrade copy)

Same voice, maximally compressed. Used for the "module blocked" upgrade popup: a one-line module pitch ("Upgrade your workspace to unlock unified messaging...") + exactly **four** ROIs chosen per module. Rules: **<= 60 characters each, outcome/benefit-led, concrete, grounded (no vague adjectives).**

Samples that hit the mark:
- Broadcasts: "10,000 texts in 7 minutes. SMS, MMS, or email." / "Insert names so mass texts feel one-to-one."
- Surveys: "Every closed invoice triggers a survey — hands-free." / "Promoters go to Google. Detractors stay internal."
- Messenger: "SMS, email, and Facebook — one inbox, zero tabs." / "Send a pay link. Get paid from their phone."
- Payments: "No more waiting for checks. Paid same day."
- Automations: "Status changes in DMS -> auto-text to customer." / "Ideal, Infinity, Aspen — works with all three."
- Deals: "Drag-and-drop deals across custom stages." / "Value, rep, days in stage — stalled deals in red."

Pick the four that best sell the module to a dealer; lead with the most visceral outcome; keep DMS names ALL-CAPS.
