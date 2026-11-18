# Babel Trip

This repository owns the **Babel Trip website, its current UI/runtime, and deployment**. The website entry point is `index.html`.

**Current active release: v1.7.14.** The sole user-facing itinerary is **https://babedrums.github.io/babel-trip/**. The previous `layout-review.html` preview has been retired to eliminate competing versions. Historical notes below describe previous releases and do not supersede the latest runtime contract in this file and index.html.

Expected GitHub Pages URL: https://babedrums.github.io/babel-trip/ (confirm published deployment before asserting it is live).

## Working contract
- Use the currently published website as the UI baseline; do not reconstruct it from older ChatGPT AppBlock or HTML snapshots in other repositories.
- Do not introduce, remove, or change visible UI, itinerary semantics, controls, layout, or behavior without the user's approval.
- For code changes, inspect latest main, active PRs and deployment; work through branch/PR, validate and verify published version before claiming it is live.
- When the user asks to view the trip, give the verified live page link, not a GitHub file/PR link or an in-chat render.
- `BabeDrums/babel-billz` owns financial and historical trip-planning context only. Its `TRIP_RENDER_CURRENT.html`, `TRIP_RENDER_APPBLOCK.txt`, and historical instructions in `TRIP_PLAN.md` are **not** website/runtime authority.
- `BabeDrums/babel-truth` owns shared Babel principles, not this website's specific UI.

This README documents authority only; it does not approve any new UI change.

## Deployment and version verification
- The version string in `index.html` identifies **source code**, not necessarily the version currently served by GitHub Pages.
- A release is confirmed live only after the GitHub Pages **pages build and deployment** workflow successfully completes for the containing commit, and ideally the published page itself is checked.
- If GitHub Actions reports `startup_failure` with no build/deploy jobs, diagnose the Pages/Actions run rather than rewriting UI code, incrementing the version, or assuming a browser cache issue.
- A documentation-only push can request another Pages build without changing the visible website. Confirm that build's actual conclusion before claiming it deployed.

## November 10 route evidence / November 11 branch clarification
These are **working route estimates**, captured from Apple Maps screenshots on November 10 at evening traffic conditions. They are not promised November 19 departure-time ETAs. **No family residential addresses are stored here.**

- Work → Ehrenberg fuel stop: **2 hr 13 min, 143 mi** (the site now uses this route duration; Work is the departure reference).
- Ehrenberg → Cousin's: **3 hr 10 min, 210 mi**, with Arizona-to-Pacific time-zone conversion of **minus one hour** during November.
- Cousin's → Mom's: maps **17 min, 5.5 mi**; site keeps a **20 min planning allowance**.
- Mom's → Rosalie: maps **4 min, 1.0 mi**; site keeps a **5 min planning allowance**.
- Mom's → Uno Tre Otto: **30 min, 10 mi**. Uno Tre Otto → Mom's: **21 min, 12 mi** (observed reverse route; not automatically interchangeable).
- Mom's → Rude Dogs: **5 min driving, 0.9 mi** or **18 min walking, 0.8 mi**, each way for the walking scenario.
- Rude Dogs → Cousin's: **14 min driving, 4.6 mi**.
- Home → Work commute estimate from screenshot: **16 min, 7.1 mi**, contextual only; not an extra stop added to the tracker.

**Decision semantics:** Mom joining remains the current **Yes** planning assumption. **No** and **TBD** are unresolved branches; the site displays the existing Alternative = TBD rather than inventing a new trip. A 5-minute **target** arrival buffer is reserved separately from driving time in the Mom dinner route. Overnight at Mom's means walk **18 minutes each way** to/from Rude Dogs; otherwise drive **5 minutes from Mom's** to Rude Dogs and then **14 minutes to Cousin's** for overnight. The Car choice is not yet wired to independent route behavior and must not silently override overnight mode. Client-side choices are not persisted across refreshes.

## November 11 — Historical / superseded — Dinner buffer and location-row grammar (v1.0.6)
- Rosalie 6:00 PM example: depart Cousin's **5:05 PM**, arrive at Mom's **5:25 PM**, visit Mom **25 minutes**, leave Mom's **5:50 PM**, arrive physically at Rosalie **5:55 PM**, target reservation **6:00 PM**. The **5-minute buffer** is planned parking/arrival slack, **not** additional drive time or a parking guarantee.
- Reservation changes back-propagate into Cousin's departure. All available pre-dinner slack belongs at Cousin's, not at Mom's; Mom's visit remains 25 minutes. If arrival is too late, retain the 20-minute minimum Cousin's visit and show actual lateness.
- Rosalie returns **directly** to Mom's using a provisional 5-minute return drive (not live traffic); Ubatuba is **omitted** in this branch.
- Uno Tre Otto retains the Ubatuba Açaí visit, related time/cost, and the Mom's return sequence. Dinner payment totals include the açaí amount **only for Uno**.
- In Thursday's travel itinerary, all rows share the same left-edge start. Action icons appear **before** location names with an 8px internal gap; icon-free locations and other rows do not reserve empty icon space. SVG paths, standard row height, and all decision controls remain unchanged.

## November 11 — Arrival icons (v1.0.7; current icon contract)
- Thursday itinerary uses three matching **circular** SVG symbols: **right arrow** = departure, **down arrow** = arrival, **pause** = settle/stop/drop-off.
- Every place row reads **icon → location → time** at the common left edge with existing 8px internal spacing. Ordinary facts, costs, decisions, and totals remain icon-free.
- This supersedes the v1.0.6 note about icon-free arrival/place rows. Icon geometry, row/card sizing, routes, time math, costs and decision behavior are otherwise unchanged.

## November 11 — Estimated fuel-range planning (v1.0.8)
- User-provided full-tank planning estimate: **340 miles**. Preferred next refill **by 300 miles driven since a full tank**, leaving a **40-mile planning reserve**. This is a conservative stop target, not an instrumented fuel-range reading.
- Wednesday pre-trip fuel plans a **full tank** and resets the **distance-to-next-refill counter to 300 miles** (while full estimated empty range remains 340 miles). Work → Ehrenberg: **143 miles**, leaving **157 mi left until refill**.
- **Confirmed trip decision:** Ehrenberg is a deliberate **fill-the-tank top-off** because it is the last preferred lower-priced fuel stop before continuing into California. The purpose is economical refueling and resetting the range to full, **not** that the tank is already low. This stop is required even when the vehicle has substantial fuel remaining. The editable **$20** is a preliminary budget, not a cap on purchasing enough fuel to fill the tank; actual spend can change. The plan resets the **miles-until-refill counter to 300** after the complete fill; the car's longer 340-mile empty-range estimate is retained only as the 40-mile reserve.
- Ehrenberg → Cousin's: **210 miles**, leaving **90 mi left until refill**. Cousin's → Mom's: another **5.5 miles**, leaving **84.5 miles until refill**, shown as **85 mi left** (rounded).
- At Mom's, approximately **84.5 more miles** can be traveled before the **300-mile refill target** is reached (assuming a complete Ehrenberg refill). No additional refueling stop is inserted or assumed before that threshold. Later unverified mileage is not used for false-precision fuel projections.
- Information rows retain their original left-side drive time, right-side leg mileage, and compact layout. Values are cleanly displayed without a leading tilde; fuel range remains an **estimate**, not a vehicle-measured or guaranteed reading. All schedules, branches, stops, costs, controls, and icon geometry remain unchanged.

## Confirmed Ehrenberg fuel intent — November 11, 2026
The driver explicitly confirmed that **Ehrenberg is the last preferred inexpensive fill-up opportunity before California**. The plan is to leave the stop with a **full tank**, regardless of arriving with **157 mi left until the regular 300-mile refill point**. The 300-mile guideline applies to subsequent distance since the most recent full tank; do not reinterpret the Ehrenberg stop as optional or as a fuel emergency. Any $20 fuel budget is only an estimate and must yield to the actual amount needed to top off.

## November 11 — Clean mileage labels (v1.0.9)
- Remove the visual `~` prefix from the three estimated remaining-range values and the provisional 1.0-mile restaurant-return leg. Display the existing planning numbers unadorned.
- The 340-mile full-tank assumption, 300-mile refueling goal, 40-mile range margin, and **intentional full-tank Ehrenberg top-off** remain unchanged. Driving-time buffers do not make estimated fuel range exact.
- No route, departure, reservation, payment, icon, interaction, or layout changes.

## November 11 — Historical / superseded — Schedule flexibility status (v1.1.0)
- The existing Thursday **Status** row is a planned scheduling indicator, not a live GPS/actual-arrival tracker.
- Minimum Cousin's stop is **20 minutes**, fixed Mom's visit is **25 minutes**, and the target restaurant arrival is **5 minutes before** the reservation. Remaining available time is held at Cousin's as extra visit time, not at Mom's.
- Compute signed flexibility as **target Cousin departure − (projected Cousin arrival + 20-minute minimum)**. Positive flexibility displays as **green negative minutes** (`-7 min` means seven minutes available beyond minimum), exactly zero displays **GOOD** in neutral text, and negative flexibility displays **red positive minutes** (`+1 min` means the *preferred arrival buffer* is missed by one minute). Missing the five-minute buffer does not necessarily mean missing the reservation.
- Update status whenever the planned departure, Ehrenberg stop duration, restaurant, or reservation changes; protect minimum Cousin and Mom visits rather than borrowing time from them. If dinner participation is No or TBD, status remains TBD because no reservation is established.
- For default 12:00 Arizona departure, 15-minute Ehrenberg stop and 6:00 Rosalie reservation: **-7 min**. Delaying by seven minutes gives **GOOD**; eight minutes gives **+1 min**. The underlying location timelines, controls, routes, and costs are unchanged.

## November 11 — Miles until next refill (v1.1.1; current fuel-display contract)
- Every visible `mi left` figure means **miles remaining until the preferred 300-mile refill interval**, **not** distance until empty. Physical full-tank planning range stays 340 miles, with the last 40 miles as an unadvertised margin.
- Both scheduled **full fills**—Wednesday fuel and the intentionally economical Ehrenberg top-off—have the same existing-style information row immediately beneath the Fuel amount: **Full tank** on the left and **300 mi left** on the right. This is planned refueling, not a live fuel sensor or proof the action happened.
- From the Wednesday full tank: Work → Ehrenberg 143 mi, **157 mi left** before the refill interval. After the required Ehrenberg full reset: Ehrenberg → Cousin's 210 mi, **90 mi left**; Cousin's → Mom's 5.5 mi, **85 mi left** when rounded from 84.5.
- These are planning distances, not a dynamic odometer. If the car is not filled to full, or more mileage is driven than planned, revise the counter. No other controls, route logic, stop durations, or status semantics changed.

## November 11 — Composed information-row experiment (v1.1.2; rejected after physical iPhone review)
- **Limited experiment in the real website:** only the Ehrenberg **Fuel** and subsequent Ehrenberg **departure** use a unified two-level row with their immediately related facts. All other information rows remain separate to enable comparison on iPhone and iPad.
- Content-driven minimum height: **44px** main/action line + **16px** supporting information line + **6px** between lines + **8px** top/bottom inset = **82px**. Rows can expand with content; this replaces two 56px rows (112px) for each of the two cases.
- Existing 17px primary and 13px secondary type, existing icons, right/left columns, controls, separator style, and facts are preserved. The existing invisible editable Fuel input in this sample has an explicit **44px** touch height and remains anchored over the price only.
- No unrelated rows, data, route timings, mileage, prices, status, controls, or branch behavior changed. Do not extend the pattern globally before visual verification on physical iPhone/iPad.

## November 11 — Revert composed-row experiment (v1.1.3; current visual contract)
- The user reviewed v1.1.2 **on a physical iPhone in dark mode** and rejected the hybrid layout. It caused inconsistent row rhythm, separator positions, and hierarchy by combining only two rows while retaining separate information rows elsewhere.
- Revert the **entire v1.1.2 composed-row UI experiment**: restore the v1.1.1 rows and CSS exactly, with the footer advanced to v1.1.3. Do not change any travel, fuel, payment, icon, status, control, or scheduling logic.
- Current approved visual rule: **all itinerary facts stay in their existing separate information rows**; do not use mixed row grammars in the same itinerary. A future alternative requires a *single coherent system-wide proposal* and user approval, evaluated on physical iPhone/iPad before promotion.
- Do not treat test-browser height measurements alone as proof of polished real-device visual quality. The 82px/84px experiment is a rejected historical test, not an active design token.

## November 11 — Historical / superseded — Dinner reservation menu (v1.1.4)
- Approved reservation choices: **6:00 PM, 6:30 PM, and 7:00 PM**, in that order. Previous 6:15 PM option is removed. **6:00 PM remains the default**.
- Only the three menu labels/values and footer version change. Cousin's arrival and minimum stay, Mom's 25-minute stay, restaurant buffer, dinner and overnight branches, and scheduling/status calculations remain unchanged.
- The existing Uno Açaí stay-time logic remains unchanged: 6:30 and 7:00 use the existing 15-minute later-reservation branch. This is not approval to modify that behavior.

## November 11 — Historical / superseded — Unified Decisions selection grammar (v1.1.5; UI pattern retained)
- All **seven** finite-choice Decisions rows (Dizzy, Dinner, Restaurant, Reservation, Car, Pays, Overnight) use a single full-row selection design: label on left and blue selected value alone on the right (no redundant chevron), 56px row tap target; all choices open the same checkmarked 44px-option menu.
- Retain seven selectable decisions, using the current reservation options and defaults specified in the newest planning contract. The Car choice remains visual-only with no route coupling. Car remains a visual-only choice without route coupling.
- The menu is single-open, closes on selecting another choice, outside click or Escape, and uses ARIA expanded/pressed states. Independent money/time fields elsewhere remain native editable inputs. No other card, itinerary, time, fuel, status, or spacing rules change.
- This interaction pattern is **Babel Trip local** pending user device review; do not promote it automatically to Babel Truth.

## November 11 — Blue-value-only Decisions (v1.1.6; current)
- Physical-device user feedback: the blue selected value already clearly signals interactivity, so **remove all seven downward chevrons** from the Decisions rows. Do not add alternate disclosure adornments.
- Preserve the same full-row selection trigger, option menus/checkmarks, values, costs, layout, and all itinerary logic. The blue selected value alone is the trailing affordance. No CSS spacing placeholders for the removed symbols.

## November 11 — Reservation display and clean dinner drive facts (v1.1.7; current)
- The Mom's → dinner travel info row uses the existing two aligned columns: **5 min drive** on the left and **1.0 mi** on the right for Rosalie; **30 min drive** left and **10 mi** right for Uno. Remove the visible **5 min buffer** string entirely, including its former right-column position.
- The dinner section now includes two distinct rows: the arrival-icon restaurant row shows the calculated physical arrival time, followed by an icon-free **Reservation** row showing the selected reservation time. The five-minute target buffer remains in schedule calculations, without reintroducing visible buffer text.
- **The 5-minute preferred arrival buffer is retained in the scheduling/back-calculation and flexibility Status.** With a 6:00 reservation and normal Rosalie route, aim to physically arrive by 5:55 while the dinner row displays 6:00. Do not remove or alter the time buffer just because it is not written in the UI.
- All other itinerary rows, route calculations, menu options, costs and decision controls remain unchanged.

## November 11 — Historical / superseded — Distinct dinner arrival and reservation (v1.1.8; UI pattern retained)
- The existing restaurant arrival row (Rosalie or Uno Tre Otto, retaining its current circular down-arrow) shows the **calculated physical arrival ETA** (e.g., 5:55 PM when the reservation is 6:00 PM and the trip is on schedule).
- Directly below it, an **icon-free Reservation row** shows the selected booking time (6:00, 6:30, or 7:00 PM), with no repeated restaurant name. Both use the same existing 56px row, type, neutral trailing color, separator and spacing vocabulary. Do not imply the read-only time is a clickable control.
- The physical arrival row turns red when projected arrival is later than the reservation; the reservation time remains steady and neutral. If arrival is only after the preferred five-minute buffer but before the reservation, Status may be positive without marking the restaurant arrival red.
- All back-calculated timing, Cousin/Mom visit minimums, travel facts, status, restaurant switching, costs, and downstream route behavior remain untouched. No new card, menu, or visual treatment.

## November 11 — Dinner stop and covered dinner total (v1.1.9; current)
- In the Mom/dinner itinerary, the previous **Stay** row is now a genuine stop: **circular pause icon + live restaurant name (Rosalie / Uno Tre Otto) + 1 hr**, after the arrival and separate Reservation. The same 60-minute stop and scheduling calculations remain unchanged.
- The old **Cost** becomes a separately grouped **Total** card **after** the restaurant stop, reusing the same one-row Total card treatment as the Wednesday and Thursday overall totals. The existing full-trip Total is unchanged.
- Display the estimated dinner price (**$50 Rosalie**, **$90 Uno**) instead of 'Mom'. When Pays = Mom, the amount is **muted and struck through**; when Pays = Me, the amount is normal. The overall trip amount counts the dinner only when the user pays, as before.
- Do not alter reservation/arrival semantics, routes, açaí pricing, controls or other card styling outside this dinner segment.

## November 11 — Historical / superseded — Fixed family visits and evening dinner options (v1.2.0)
- User approved **exactly 30 minutes at Cousin's and 30 minutes at Mom's** before dinner. Both are fixed durations, **not adjustable slack**. The app must calculate Cousin departure = arrival + 30, Mom arrival = Cousin departure + 20-minute planned drive, Mom departure = Mom arrival + 30, and restaurant ETA = Mom departure + selected restaurant's drive (Rosalie 5 / Uno 30 minutes).
- Reservation selector is now **6:30 PM (default), 7:00 PM, 7:30 PM**, replacing the earlier 6:00 / 6:30 / 7:00 choices. Reservation times are Pacific-local. Neither reservation selection nor restaurant choice should silently inflate the 30-minute family visits. The dinner reservation row shows the selected booking time; the restaurant arrival row shows projected ETA separately.
- If the fixed route arrives early, that gap is honest **pre-reservation waiting margin**, not extra family-visit minutes. Dinner's 1-hour meal is scheduled from the later of arrival or reservation, as it was previously.
- Thursday **Status** is still a predicted scheduling indicator, not GPS. Compare projected restaurant ETA to the **five-minute-early preferred target**: margin = selected reservation − 5 min − projected arrival. **Green negative minutes** indicate extra time beyond that 5-minute target, **GOOD** is exactly at target, **red positive minutes** indicate the target buffer was missed. Arrival time itself turns red only once later than the reservation. Dinner No/TBD means Status TBD.
- With the default noon Arizona departure, 15-minute Ehrenberg stop, Rosalie and 6:30 PM: Cousin arrives **4:38 PM PT**, departs **5:08 PM**, Mom arrives **5:28 PM**, departs **5:58 PM**, Rosalie arrives **6:03 PM**, reservation **6:30 PM**; Status **-22 min** (27 minutes between physical arrival and reservation, five minutes of which are the protected target buffer).
- With Uno and 6:30 PM under the same route, ETA is **6:28 PM**, two minutes before reservation; Status **+3 min** (the target buffer missed, but reservation not yet late). Its Açaí stay remains the existing **15 minutes** across the newly offered reservation times; the older shorter-evening special cases are obsolete.
- All other budgets, choices, routes, fuel intervals, icons, row styling, overnight branches, restaurant covered-price Total treatment, and downstream meal/stop behavior remain unchanged. Earlier sections are recorded history, **not competing active timing rules**.

## November 11 — Overnight destination labels (v1.2.1; CURRENT)
- The Overnight decision presents **Mom** (default) and **Cousin** instead of the ambiguous Yes / No labels, using the existing full-row menu and blue selected-value affordance.
- This is a **presentation-only rename**: internally `yes` still means stay overnight at Mom's (18-minute walks to and from Rude Dogs), while `no` still means drive to Rude Dogs and then Cousin's for overnight. The itinerary itself keeps natural place names “Mom's” and “Cousin's.” No routing, scheduling, overnight destination or financial logic changes.

## November 11 — Cousin's flexible visit; Mom fixed at 30 minutes (v1.2.2; CURRENT PLANNING CONTRACT)
- User supersedes v1.2.0's fixed Cousin duration: **Cousin's visit is minimum 30 minutes, plus any usable pre-dinner slack**, and **Mom's visit remains exactly 30 minutes**. Extra time belongs at Cousin's, not as unspecified waiting near the restaurant.
- For Dinner Yes, calculate target Cousin departure backwards from the selected Pacific dinner reservation: reservation − five-minute preferred arrival buffer − (Rosalie 5 min / Uno 30 min drive) − Mom's 30 min visit − Cousin-to-Mom 20 min drive. Actual Cousin departure is **max(Cousin arrival + 30 minutes, target Cousin departure)**. This preserves the minimum when the reservation is too early, and extends Cousin's visit when time permits. For Dinner No/TBD, keep Cousin's visit at 30 minutes because there is no confirmed dinner timing target.
- The displayed Cousin pause/stay duration is dynamic; **green only if greater than 30 min** (same green token as the Status value), neutral at exactly 30 min. This affects only the duration, not the row label or icon.
- Status must continue to report the **available signed margin over the 30-minute Cousin minimum**, not the artificial zero margin after spending the extra time at Cousin's. Compute target Cousin departure − (Cousin arrival + 30), displaying green negative time when positive, neutral GOOD at zero, red positive time when negative; Dinner No/TBD remains TBD. **The restaurant arrival row** continues to turn red only for a projected actual arrival after the reservation.
- Under default noon Arizona departure, 15-minute Ehrenberg stop, Rosalie, 6:30 PM reservation: Cousin arrival **4:38 PM PT**, pause **52 min** (green), departure **5:30 PM**; Mom arrival **5:50 PM**, pause **30 min**, departure **6:20 PM**; restaurant ETA **6:25 PM**, reservation **6:30 PM**, Status remains **−22 min** (the reusable slack represented by the additional Cousin time).
- Reservation options remain **6:30 / 7:00 / 7:30 PM**; other decisions, overnight branches, budgets, icons, individual row geometry, Açaí durations and dinner payment rules remain unchanged.

## November 11 — Covered dinner price strike placement (v1.2.3; current visual correction)
- On physical-device review, the browser font's native `text-decoration: line-through` placed the line off-center. Use a 1px `::after` line across the **visual center of the covered price's own box** instead, scoped to `.coveredPrice` only.
- Preserve the existing muted covered price, `Pays = Mom` / `Pays = Me` toggle, amounts ($50 Rosalie/$90 Uno), 56px Total row and all itinerary/financial logic. Do not add a second strike or change fonts, rows, icons or surrounding components.

## November 11 — Unified vertical spacing rhythm (v1.2.4; CURRENT VISUAL CONTRACT)
- Real iPhone screenshots showed inconsistent spacing: Decisions groups used an 18px gap and an 18px transition into Wednesday, Wednesday→Thursday used 34px, while stacked itinerary cards used 10px. This was accidental hierarchy, not approved meaning.
- Adopt two consistent levels within the existing website: **12px related/card gap** (Decisions groups and all `.stack` groups/cards) and **28px major section gap** (last Decisions group→Wednesday and Wednesday→Thursday). Section header→content spacing is **12px**. Footer spacing remains existing 28px.
- Keep all `row` heights at 56px, current card groups, labels, menu placement/behavior, icons, calculation logic, arrival/status semantics and dark/light palettes unchanged. Do not introduce decorative separators or new wrappers to patch spacing.
- This is app-local visual alignment pending physical iPhone/iPad review. Preserve the shared rhythm for future Babel Trip sections unless new device evidence warrants a deliberate change.

## November 11 — Collapse hidden Alternative card wrapper (v1.2.5; CURRENT SPACING FIX)
- Physical iPhone review exposed an exact double gap between Cousin's pause group and Mom's departure group. Root cause: the Alternative row was hidden while its containing group stayed in Thursday's stack, leaving a zero-height flex item and **two consecutive 12px gaps (24px total)**.
- Move the existing altPlan ID and hidden state from the inner row to the **entire Alternative group wrapper**. The existing render visibility toggle now hides/shows the full card; no empty flex item when Dinner = Yes. Dinner = No / TBD must still reveal the same Alternative = TBD card with one 56px row.
- Preserve all existing **12px gaps** across sibling itinerary cards and nested stacks, **28px** between major sections, **12px** heading spacing; no CSS changes, new wrappers, or one-off margins. No row data, timing, controls, colors, finances, branches or JavaScript calculations changed.
- General rule: optional itinerary cards must be removed from the layout when inactive. Do not merely hide their inner contents while leaving an otherwise empty stack child.

## November 11 — Default Arizona departure at 12:15 PM (v1.2.6; CURRENT DEFAULT)
- User explicitly changes Thursday Arizona departure **default from 12:00 PM to 12:15 PM Arizona time**. This is the initial time-input value and corresponding visible time; departure remains editable and schedules continue to recalculate from it.
- With the existing 15-minute Ehrenberg stop and Rosalie 6:30 PM reservation: Ehrenberg arrival **2:28 PM AZ**, depart **2:43 PM AZ**; Cousin's arrival **4:53 PM PT**, stay **37 min** (green), depart **5:30 PM PT**; Mom arrives **5:50 PM**, stays **30 min**, departs **6:20 PM**; Rosalie ETA **6:25 PM**, reservation **6:30 PM**; Status **−7 min**.
- Move the static initial HTML fallback times and status into alignment with this default. Do not change any travel durations, destination times downstream of Cousin's departure, menu defaults, budgets, spacing or itinerary calculation logic. Older noon-departure examples remain historical only.

## November 11 — Decisions grouped by purpose without labels (v1.2.7; grouping retained; Mom options superseded)
- User approved reorganizing the **existing seven** Decisions controls into exactly **three unlabeled group cards**, retaining the original Decisions header and existing 12px inter-card gap. Group 1: Dizzy, Mom. Group 2: Restaurant, Reservation, Pays. Group 3: Car, Overnight. Do **not** display headings, subtitles, category names, badges, icons or additional descriptions above the groups.
- The former **Dinner** decision is relabeled **Mom**, while retaining existing Yes/No/TBD choices, the same state key `dinnerMom`, and the same plan/Alternative=TBD semantics; Dinner/Mom=No/TBD still hides Restaurant and Reservation using existing toggles. No changes to choice values or state persistence.
- Use the same existing full-row blue-selected-value menus, 56px rows, 12px card spacing, dividers, and dark/light treatment. No new interaction behavior or computation; markup grouping and two Mom control label/ARIA strings only.
- Keep all amounts, reservations, family visit times, route options, conditional alternative card, overnight modes, icons, fuel counter and scheduling/status calculations unchanged.

## November 11 — Mom is a Yes / No decision (v1.2.8; CURRENT UI)
- User explicitly removed the **TBD** option from the **Mom** selector. Mom offers exactly **Yes** (default) and **No**. Leave Dizzy and all other selector options unchanged; keep the same first card `[Dizzy, Mom]`, other two unlabeled groups and existing styling/spacing.
- Keep the internal `dinnerMom` Yes/No logic untouched: Yes shows existing Mom-and-dinner itinerary; No shows the existing unresolved `Alternative = TBD` itinerary rather than inventing a new route. The **TBD text elsewhere is not itself a Mom option**.
- No runtime state or itinerary, timing, pricing, status, menu handling or style changes. Only remove the Mom menu's TBD button and bump the version.

## November 12 — Thursday 9 AM work-break fuel and Work departure (v1.2.9; CURRENT FUEL PLAN)
- User confirmed **Thursday, Nov 19 at 9:00 AM Arizona time** work break: top off to full tank at a station by work, then leave **Work at 12:15 PM** (existing editable departure default), rather than buying the initial trip fuel on Wednesday. Work-break refueling is completed before the departure clock starts; no extra driving time or stop gets inserted between Work and Ehrenberg.
- Move the existing editable **$45 Fuel** (`prepFuel` and `prepFuelText`) and accompanying `Full tank / 300 mi left` info row from Wednesday to a new Thursday card **after Status, before Work departure**. The new card has Work break = 9:00 AM, Fuel = editable $45, Full tank = 300 mi left. Rename only the existing departure row's place label **Arizona → Work**; keep its right-hand editable 12:15 PM and existing route, 143 mi / 157 mi left, unchanged.
- Financial accounting: Wednesday includes only $35 Haircut and $50 Tickets (2-person default), **Wednesday Total $85**. Thursday includes $45 pre-departure fuel, $20 intentional Ehrenberg top-off, $10 snacks, default $0 Rude Dogs, **Thursday Total $75**. Both days combined are still **$160**. The transferred $45 must appear once across the day totals, not twice. Keep both money inputs editable and honor existing Dizzy one/two-ticket scenarios.
- Keep intentional Ehrenberg full fill at the existing estimated $20 and its 15-minute stay. After Thursday's morning fill, Work → Ehrenberg 143 mi leaves 157 mi of the preferred 300-mile refill interval. The separate Ehrenberg full tank resets interval to 300 mi for California. Neither fill claims an exact vehicle sensor reading; budgets are estimated.
- Preserve all existing 56px rows, 12px inter-card spacing, Decisions, menus, travel-time math, stop times, dinner/overnight branches, Status, CSS and the unresolved Alternative case. Under Mom No the preexisting Thursday total stays TBD pending a trip alternative; this is not a second fuel expense.

## November 12 — Break row title (v1.2.10; CURRENT LABEL)
- Rename Thursday's **9:00 AM** row label from **Work break** to **Break**. This is a literal label-only presentation change. The editable $45 fuel fill, full-tank information, Work 12:15 PM departure, budgets, calculation logic and all other trip behavior remain unchanged.

## November 12 — Birthday outing Saturday Nov 14 (v1.3.0; historical, superseded by v1.3.1)
- Add a Saturday, Nov 14 section chronologically before California's Nov 18 and Nov 19 cards, keeping the original global Decisions section and all existing California content and logic unchanged. This is a separate Scottsdale birthday evening plan for four people tentatively (user, D'Angelo, Missy, Jada), not four confirmed tickets/bookings. Do not mix costs with California totals.
- Use only existing Babel Trip components and behavior patterns: day header, .stack/.group, 56px .row and .infoRow, arrival/departure .miniIcon SVGs copied from existing source, full-row .choice dropdown Yes/No, blue overlaid native time controls, .trailing, and status semantic .good/.red. No new CSS, bespoke widgets, buttons, decorative headers or UI idioms.
- Golf booked Yes/No defaults to No. This tracks the user's report; pressing Yes only changes the on-page tracking choice; the website does not book a tee time. The planned 8:00 PM golf target is unbooked, not live availability or a confirmed booking. Use editable birthdayGolf time input and editable birthdayArrival at 7:00 PM.
- Default timetable: Puttshack arrival 7:00 PM; dinner 45 min; golf check-in 7:45 PM (15 min before tee); target mini golf 8:00 PM, reserve 40 min for 9 holes and 5 min to leave; Puttshack departure 8:45 PM; planning drive allowance 30 min (not a live traffic ETA); Grapevine karaoke arrival 9:15 PM; karaoke 1 hr, Grapevine departure 10:15 PM; goodbyes 15 min, Missy leaves 10:30 PM at latest. Compute all downstream times from the editable target. Late restaurant arrival relative to check-in marks check-in red; projected Missy exit beyond 10:30 red.
- The 10:30 buffer uses signed minutes until the hard departure target, zero displayed as neutral 0 min (no real spare time), green negative when early, red positive when late. Do not imply extra wiggle room at the default. Four-person game may take 30–45 min according to Puttshack; 40 min is only a planning assumption.
- Saturday 9-hole advertised price $16 per player before unknown taxes/fees, as listed on official https://www.puttshack.com/locations/scottsdale/ . Puttshack encourages advance weekend booking and says walk-ins are not guaranteed (see https://www.puttshack.com/faq/ ). Grapevine official Saturday karaoke runs from 3 PM to closing at https://grapevineaz.com/ . Food, karaoke spending and personal total stay TBD until user decides who pays and spending plans; $16 is not automatically charged to the user for four people.
- Existing Wednesday/Thursday financial totals, fuel, Status and all trip math are unchanged. Decisions do not become global birthday decisions. No local storage/persistence is added; controls reset on reload as in the existing website.

## November 12 — Birthday iPhone, golf reservation and flexible karaoke (v1.3.1; CURRENT BIRTHDAY CONTRACT)
- Fix iPhone decision-row sizing shared by global Decisions and birthday Golf booked: `.menuGroup` and `.decisionRow` width 100%, min-width 0; normalize `.decisionTrigger` iOS button appearance, margin and max/min width, using existing selectors. Keep row height 56px and standard 12px stack spacing. Physical-device screenshot confirmation remains pending.
- Saturday top card is a standalone **Status** (same good/red/GOOD signed margin semantics as Thursday), followed by a standalone **Golf booked** Yes/No card, default **No**. Changing the on-page booked flag never actually books golf.
- Puttshack arrival editable (default 7:00 PM), Dinner duration editable as existing blue numeric control (default **45 min**), golf **Reservation** target editable as existing blue native time input (default **8:00 PM**, *not booked*); remove separate check-in row. A Saturday walk-in is possible but not guaranteed, especially weekends; Puttshack recommends advance tee-time booking.
- Dinner may finish early without moving a scheduled tee time. Actual golf starts at `max(reservation, arrival + dinner duration)`. Dinner running past the target makes the Reservation text red; it delays golf, which lasts assumed 40 min + 5 min exit. A fixed 30-min driving allowance then reaches Grapevine.
- Extra time goes to **Grapevine karaoke**, whose stay time is dynamically computed from arrival until **10:15 PM**. Protect 15-minute goodbyes and Missy's planned **10:30 PM** latest departure. If the arrival is too late, karaoke never becomes negative; leave immediately and mark Missy's actual projected leave late.
- Status measures one-hour minimum karaoke: `10:15 PM - (Grapevine arrival + 60 minutes)`. Green negative minutes = surplus time at Grapevine; neutral **GOOD** = exactly one hour; red positive minutes = deficit. The Missy leave row is red only if beyond 10:30.
- No new controls or bespoke component types; existing California decisions, totals, fuel, routes, and algorithms are preserved.

## November 12 — Correct shared iPhone decision padding and connect Grapevine pause (v1.3.2; CURRENT)
- User physical iPhone screenshot shows Decisions and Golf booked choice text shifted about 15px to the right of ordinary Status rows. **Verified root cause:** the later `@media(max-width:390px)` rule `.row{padding-left:15px;padding-right:15px}` overrides the earlier `.decisionRow{padding:0}` (equal CSS selector specificity). The nested `.decisionTrigger` then adds another 15px. Solve systemically by strengthening existing base selector to `.row.decisionRow{padding:0;...}`, which outranks the narrow `.row` rule, so button text has exactly one 15px mobile inset. No per-card offset, new component, or changes to normal Status row padding.
- Move the existing dynamic **1 hr Karaoke** row immediately below the **Grapevine arrival** row inside the same `.group`, using the **same Grapevine place label and existing pause icon** grammar as Cousin's and Mom's visited durations. Its dynamic value ID `birthdayKaraokeTime` and behavior remain unchanged. The next separate `.group` begins with Grapevine departure at 10:15 PM, followed by Goodbyes and Missy leaves. Preserve the 12px inter-card gap, row height, financial totals and all existing scripts.
- **Golf sequencing unchanged** while booking remains unconfirmed: Puttshack officially recommends arriving one hour ahead when eating before mini golf, so 7:00 PM dinner and 8:00 PM target remains the current planning assumption. If food ends at 7:30, a reserved 8:00 slot cannot be assumed to start early. Staff may accommodate an earlier round only if available; weekend walk-ins are not guaranteed. Do not silently flip dinner and golf or invent early capacity. The existing editable Reservation time handles a genuinely confirmed different tee time.

## November 12 — Remove Golf booked control (v1.3.3; CURRENT BIRTHDAY CONTRACT)
- On user's request, **remove the Golf booked Yes/No card entirely**, because golf booking is an external action, not an itinerary branch. Remove its unused `birthdayGolfBooked` JS state; do not replace with a new control or badge. Saturday begins Status then the existing Puttshack itinerary card. Keep the current iPhone dropdown CSS fix for the remaining decisions.
- The editable golf **Reservation** remains a **planned, not yet booked** 8:00 PM tee time. Recommend booking four players for **Saturday Nov 14 at 8 PM**, not 7:45, because the group arrives at 7 PM and Puttshack recommends an hour before golf if eating on-site. Walk-in play is possible but not guaranteed, especially Saturdays. Do not mark the reservation confirmed, attempt to book, or alter its displayed time without actual booking evidence. Keep the existing editable time field until real reservation details are provided.
- Preserve dinner 45m editable, karaoke pause attached to Grapevine arrival, 10:30 PM Missy deadline, all Saturday timing math, and the entire California itinerary, budget and styles unchanged.

## November 12 — Fixed birthday golf target at 8:00 PM (v1.3.4; CURRENT)
- User explicitly directs making Saturday's existing **Reservation** time non-editable. Render the same standard `row` with normal secondary `trailing` text **8:00 PM**, not blue and not a native time input. Remove the old `birthdayGolf` input, variable and listener. Lock the runtime planning anchor to 20*60 minutes; keep dinner duration editable and reserve time for Grapevine as in v1.3.3.
- This is a **chosen planning target, not a booking confirmation**. Saturday Nov 14 8:00 PM mini-golf for four people should be booked externally; until confirmed, do not imply inventory or a purchased slot. If the actual reservation differs, obtain user's approval before adjusting fixed planning anchor and published page.
- Preserve existing Saturday status, 7:00 PM Puttshack arrival, 45-minute dinner default, 40-minute golf assumption, 30-minute Grapevine drive allowance and 10:30 PM latest exit. Do not rewrite any Wednesday/Thursday California UI or calculations; all CSS stays unchanged.

## November 12 — Editable golf pace and earlier Grapevine (v1.3.5; CURRENT BIRTHDAY SCHEDULE)
- Fix Saturday Puttshack **arrival to 7:00 PM**, show plain secondary trailing text (not editable). Dinner stays native editable **45 min** default. Re-enable the same native time input pattern for **Reservation**, default **8:00 PM** but editable so an actually approved earlier tee time can be reflected. Still a planning target, not proof of a real booking; modifying the tracker does not reserve Puttshack.
- Change Saturday **Mini golf** to existing native blue numeric duration editor, default **40 min** with 5-minute step. **Remove the automatic 5-minute departure allowance** entirely: Puttshack departure occurs exactly at `max(reservation, 7:00 PM + dinner minutes) + mini golf minutes`. This is a user's optimistic planning assumption rather than a promise to leave the building instantaneously; if a real exit takes longer, adjust the plan.
- Keep 30-minute travel planning allowance to Grapevine and karaoke time derived from arrival until **10:15 PM**; 15-minute goodbyes protect Missy's **10:30 PM** latest departure. All time saved from earlier authorized golf or shorter rounds becomes time at Grapevine, not a new early endpoint. With default inputs, leave Puttshack **8:40 PM**, arrive Grapevine **9:10 PM**, karaoke **1 hr 5 min**, Saturday Status **−5 min** green. Status remains relative to one-hour karaoke baseline.
- If dinner exceeds the chosen tee time, retain the prior red Reservation indicator and use a delayed modeled golf start; this is planning only, not an assurance Puttshack honors missed tee time. Calendar date remains Saturday Nov 14, 2026. Existing CSS/component vocabulary, Wednesday/Thursday calculations, separate California expenses and seven Decisions unchanged.


## November 13 — Confirmed Thursday dinner/overnight and decision cleanup (v1.3.6)

User called Mom and confirmed that Thursday Nov 19 will follow one route: **Rosalie dinner at 7:30 PM PT (target, not independently verified restaurant booking)**, drive **user's car** from Mom's to Rosalie and back, park at Mom's, walk **18 min each way** between Mom's and Rude Dogs, and **overnight at Mom's**. Mom is joining. Friday guest **Dizzy** and Thursday dinner **Pays** remain unresolved and editable.

- Remove the former seven-row global Decisions section. Retain only **Dizzy** beside Wednesday tickets (its ticket-count relationship) and **Pays** beside Thursday restaurant cost, using the existing blue-value checkmark-menu component. No new global controls or visual grammar.
- Remove disabled alternate, Uno/Açaí, and Cousin-overnight driving DOM branches and obsolete state handlers. Fix dinner route to Rosalie; fix 7:30 PT dinner target, 5-min dinner drives, 30-min Mom visit, 5-min target-arrival buffer and 60-min dinner assumption. Return to Mom, park 5 minutes, walk to and from Rude Dogs. The 2h30 karaoke stay remains the existing estimate, not a guaranteed closing time.
- Display the confirmed car in the existing compact drive info rows and “Park at Mom’s” in the existing five-minute pause row, without creating extra cards. Change Thursday's “Reservation” field label to **Dinner target** so no third-party booking is implied.
- Keep independent editable Thursday Arizona departure, Ehrenberg duration/fuel, snacks, Thursday karaoke spend, and Saturday dinner/golf inputs. Saturday and Wednesday budget calculations remain unchanged except relocating Dizzy's choice. Payer continues to control the meal inclusion in financial totals. Status/back-calculation retain Cousin's 30-min minimum and Mom's 30-min fixed visit.
- Default 12:15 PM AZ departure / 15-minute Ehrenberg pause: arrive Cousin 4:53 PM PT, leave 6:30, Mom 6:50–7:20, Rosalie physically 7:25 for 7:30 target, dinner ends 8:30, park at Mom 8:35–8:40, Rude Dogs 8:58–11:28, walk home to Mom by 11:46 PM PT. Status -67 min beyond the Cousin minimum. Driving/walking times are planning estimates, not live traffic or guaranteed venue hours.
- UI approval: user “Bet whatever u think” to the scoped recommendation to simplify settled choices; branch/PR validation and deployment confirmation remain separate requirements.


## November 15 — Completed birthday outing archived from active trip (v1.3.7)

The user confirmed the **November 14 Scottsdale birthday outing was successfully completed** and explicitly requested removing Puttshack entirely from the itinerary. The actual outing was Puttshack mini golf with Missy followed by Grimaldi’s dinner with Missy and D’Angelo; the previously planned Grapevine karaoke did not occur. This is historical context, not a future itinerary or proof of a particular booking/expense.

- Remove the **entire completed Saturday Nov 14 birthday section** from active Babel Trip so the unvisited Grapevine plan is not left behind as a misleading standalone route.
- Remove associated birthday inputs, event bindings, schedule/status calculation and unused top-section CSS. No new replacement UI, completion card or archive surface.
- Preserve the remaining **Wednesday Nov 18 and Thursday Nov 19** California itinerary HTML and functionality exactly, including Dizzy and Pays choices, cost math, editable fuel/departure/stops, and confirmed Thursday Rosalie/overnight walking route.
- The history of previous birthday planning remains available via Git history/earlier documentation. Only active webpage content changes.


## November 16 — Wednesday departure, three local meals (v1.3.8)

**User-approved changes:** Thursday and Friday work leave confirmed; definitive departure **Wednesday Nov 18 after work at editable 3:15 PM Arizona time**, no departure-day toggle. Do not schedule GTA VI launch timing; games are unscheduled family time. **Mom refers to grandmother** (user's own name for her); this is the same stop. Keep original Babel Trip visual language unchanged; do not replace page with a new UI.

- Move **$35 Haircut** to **Tuesday Nov 17** prep with existing **Dizzy** and **Tickets** selector; default two tickets $50. Tuesday total $85.
- Wednesday **work break 9 AM** is a planning carry-forward, not a confirmed recurring work-break time. Fill to full for editable $45, drive from Work **3:15 PM AZ** with native time input preserved, Ehrenberg arrive **5:28 PM AZ**, full top-off **$20**, snacks **$10**, stop editable **15 min**, depart 5:43 PM AZ, Cousin arrive **7:53 PM PT**. Original fixed route estimates 133 + 190 min and 143 + 210 mi from Nov 10 screenshots, **not real-time traffic**. Fuel interval shows 157 miles left until 300-mile stop at Ehrenberg, resets to 300, and 90 miles left upon reaching Cousin. New local driving mileage is **TBD** until routed and is not silently subtracted.
- Wednesday food: settle 10 minutes; plan **5-minute drive each way** to **La Baja Tacos, 16423 Maplegrove St, La Puente CA** (local drive time allowance unverified; route mileage TBD). Arrival 8:08 PM; editable **Dinner target 8:10 PM PT**. Dinner lasts 25 minutes, return to Cousin **8:40 PM**; overnight at Cousin. Store lists Wednesday close **9 PM**, so Status shows time left until 9 PM **after planned dining** (default -25 min); arrival/departure turn red if too late. The 9PM close isn't a guarantee of last-order time; user should call if running late. Editable taco budget $15. Wednesday total $90.
- Thursday breakfast: depart Cousin 9:50 AM PT, plan 10-minute drive, **Caramelo Café Valinda branch, 1447 Valinda Ave, La Puente**, arrive 10 AM, eat 60 minutes, return Cousin 11:10 AM. Store lists Thurs 8 AM–3 PM, crêpes ~$15.99; editable personal breakfast budget **$20**. Drive length in miles TBD.
- Thursday lunch: leave Cousin 12:50 PM, plan 10-minute drive, **Jim's Burgers, 16023 Amar Rd, La Puente**, arrive 1 PM, eat 45 minutes, return Cousin **1:55 PM**, with **4 hr 35 min** free at Cousin until **6:30 PM**. Editable personal lunch budget **$15**; exact driving miles TBD.
- Thursday evening from Cousin 6:30 PM PT remains: Mom 6:50–7:20 PM (30 min), Rosalie arrival 7:25 PM and **7:30 PM dinner target** (not reservation proof), paid by Mom by default ($50 covered), Rosalie depart 8:30, Mom 8:35, park 5min, walk 18min to Rude Dogs 8:58, karaoke budget editable default $0 and stay 2h30, walk home to Mom 11:46 and overnight Mom. This markup/behavior is preserved verbatim except **Cousin→Mom fuel remaining text** now says 'range TBD' because local driving is newly unmeasured. The settled Mom/Pays decisions are not reopened.
- Default day totals: **Tue $85 + Wed $90 + Thu $35 = $210** of personal planning estimates, excluding later dates, any optional expenses, actual taxes/tips, and covered dinner. Under Dizzy None tickets become $25; Pays Me adds $50 to Thursday.
- UI: original 56px rows, card style, iconography, CSS, menus, and native editable input treatment retained. New meal rows re-use the same primitives, not a redesign. No GTA unlock claims.
- Restaurants verified Nov 16 from https://www.labajatacos.net/ , https://www.caramelo.cafe/ , and https://www.restaurantji.com/ca/la-puente/jims-burgers-2/ . Meal pricing is budgetary, not a verified final receipt.
- Follow-up: actual local driving mileages and traffic need in-car maps (do not invent route figures); verify Rosalie's 7:30 PM dinner as an external reservation if required. **Friday and Sunday still not detailed in runtime**, deliberately avoid inventing them.

## November 16 — Adaptive Wednesday arrivals and linked home stop (v1.4.0)

**Confirmed intent:** route mileage and drive duration are separate concepts. Travel times are planning estimates, not locked arrivals; the user can correct Ehrenberg arrival (Arizona clock) and Cousin's arrival (California clock) earlier/later after observing reality. Each manual arrival is a clock-time override and propagates downstream; it does not change route distance or silently alter the fuel counter. Each has a small reset-to-estimate action. Upstream edits continue recalculating estimated arrivals unless that specific arrival was manually corrected. This is a local Babel Trip behavior, not a shared foundation.

- Wednesday lunch fuel defaults to **12:00 PM Arizona**, full tank, **300 miles until preferred refill**. Editable Work departure defaults to **3:15 PM AZ** (earliest user scenario **3:05**), with estimated **16-minute / 7.1-mile** Work→Home leg. Home arrival **3:31 PM**. **Automatic** Home stay = clamp(4:00 PM AZ minus estimated Home arrival, **5 min minimum, 30 min maximum**). Thus 3:13 Work departure → 3:29 Home arrival → 30 min stay → 3:59 Home departure; 3:15 Work → 3:31 Home → 29 min → 4:00; 3:40 Work → 3:56 Home → 5 min → 4:01. The automatic bounds are preferences only, **not restrictions on manual edits**. No home or family street addresses belong in public source.
- Home→Ehrenberg provisional time allowance **2 hr 11 min**; its mileage is **TBD** until confirmed, and total range to Ehrenberg stays TBD rather than pretending the older Work→Ehrenberg 143 miles is still the route. Estimated Ehrenberg arrival **6:11 PM AZ**, adjustable. Ehrenberg full top-off remains **15 minutes**, with expense inputs untouched; time adjustment changes departure. Ehrenberg→Cousin keeps the *older observed* **3 hr 10 min / 210 miles** planning leg until refreshed. Default Cousin ETA **8:36 PM PT**, adjustable; after the full Ehrenberg refill, 210 miles leaves 90 miles until the preferred 300-mile refill.
- Wednesday Cousin settling, taco target, closing-time status, return, and budget derive from adjusted Cousin arrival; Thursday begins as a separate fixed-day schedule. Current La Baja Tacos remains a **provisional** dinner because a late arrival may miss the 9 PM close; do not silently select a different restaurant until the user settles it. Red status warns when dinner runs late. Default estimates are not live traffic or an arrival commitment.
- Both **Home stay** (numeric minutes) and **Leave Home** (native blue time picker, Arizona-local) are directly linked. In automatic mode they follow the 5–30-minute preference above. Editing stay switches to a manual **duration** override; Home departure recalculates. Editing Leave Home switches to a manual **departure-clock** override; Home stay recalculates, even when the observed stay is **0, 1, 4 or more than 30 minutes**. Changing Work departure while manual duration is active preserves duration; while manual departure-clock mode is active it preserves the chosen Home departure and recomputes stay. A small reset action appears for the manually overridden Home departure; tapping it returns to automatic. When an entered departure precedes calculated Home arrival, normalize to arrival (0 min), not negative stay. Every Home departure update flows to estimated Ehrenberg/Cousin arrival unless that later arrival was itself manually overridden. Red after 4 PM is a planning lateness indication, not an input prohibition.
- Native blue-value time inputs retain existing UI row grammar; reset controls appear only after a manual override. No GPS or background tracking, no local persistence, and no home/family street addresses in the public repository.

## November 17 — Friday–Sunday interactive trip shell and full budget (v1.4.1)

**User approval:** finish the remaining active California trip days (Friday Nov 20, Saturday Nov 21, Sunday Nov 22) in the **same approved grouped-row UI** and provide a dynamic grand total that follows all trip decisions. This is a working shell for physical iPhone review and later itinerary edits; it does not certify bookings or promise exact travel times. The existing Tuesday–Thursday route and design remain unchanged (except the page version).

### Friday Nov 20 — Mom's departure through overnight
- Start from **Mom's in Covina** because Thursday's verified itinerary ends overnight there. Do **not** use old Friday plans that start from Cousin's.
- Existing Tuesday **Dizzy** choice drives the Friday route. Weekend/Friday = editable **1:15 PM PT** departure, estimated 90-minute Mom's→Temecula pickup drive, editable 30-minute pickup/fuel window and **$50 fuel**, provisional 80-minute Temecula→Hanagi leg. None = default **4:10 PM PT** Mom's departure and direct provisional 45-minute Anaheim leg, without the pickup fuel charge.
- **Hanagi Japanese Restaurant** (Anaheim Majestic Garden Hotel): 5 PM dinner target, editable 75-minute dining allowance; budget **$110 for two** if Dizzy participates and **$65 solo**. Dinner is not a reservation. Hanagi states that it validates parking with an entrée purchase (https://hanagidining.com/location/).
- Plan **20 minutes** to GardenWalk; $30 editable parking allowance. Preferred GardenWalk P4 Purple parking (not reserved). Arrival status measures margin to **7:30 PM target**; negative green = early, positive red = behind this preferred arrival, while fixed **8 PM** event start remains the event anchor.
- **Stan Society Presents Olivia Rodrigo Night**, **Nov 20 8 PM**, **18+**, **House of Blues Anaheim**: it is a DJ tribute/night, **not an Olivia Rodrigo live concert**. Event length **150 minutes** editable; default separate editable event spending **$20 if Dizzy joins/$10 solo**. Earlier Ticketmaster one-ticket checkout was **$24 all-in**, rounded up to existing **$25 per ticket** (Tuesday budget), still not proven purchased. Sources: https://anaheim.houseofblues.com/shows and https://www.ticketmaster.com/house-of-blues-anaheim-tickets-anaheim/venue/74096 .
- **Weekend/None:** provisional 35-minute House of Blues→Grandpa drive, Friday overnight at Grandpa's as previously approved. **Friday only:** provisional 80-minute after-event drive to drop off Dizzy in Temecula, editable 10-minute farewell, then 75-minute drive to Cousin's for overnight. This latter route runs after midnight and is a **significant driving-fatigue risk**; never treat it as safe by default simply because the tracker shows a clock time.

### Saturday Nov 21 — family time, dinner, optional karaoke, drop-off
- **Weekend/None** begins at Grandpa's around 11 AM PT. **Friday-only** begins at Cousin's, with editable 11:20 AM departure and a provisional 40-minute trip to Grandpa's. The 11 AM value is a planning start, not a claim of a new Saturday arrival after sleeping over.
- Editable lunch/snacks **$50 for Weekend**, **$25 otherwise**. Dinner choice **TBD** (default, maintain a conservative editable reserve of **$85 Weekend / $45 solo**), **Grandpa** (no user dinner charge assumed *only if user explicitly selects that plan*), or **Hangout** (same reserve, tentative 20-minute drive to The Hangout in Seal Beach). Dinner target **6:30 PM PT**, editable, with 60-minute default stay. TBD is a budget envelope, **not a confirmed restaurant or reservation**.
- Karaoke choice **No** (default) / **Yes**. If Yes, provisional 15-minute travel to **Shanghai'd Room** and editable 90-minute stay, with editable $35 Weekend / $20 solo additional spending. Official venue says karaoke nightly from 8 PM (https://www.shanghaidroom.com/).
- With Weekend Dizzy, allow **85 minutes** to Temecula from the Saturday evening activity, editable 10-minute drop-off, then **75 minutes** to Cousin's overnight; no-Dizzy/Friday-only returns straight to Cousin's in an estimated **45 minutes**. These return drives are rough, can run past midnight and vary substantially by chosen starting point/traffic; should be refreshed in Maps. **No hotel** assumed or funded. Saturday night is a family lodging fallback, not an external reservation.

### Sunday Nov 22 — California return
- Depart Cousin's for tentative 10 AM **Caramelo Café** breakfast using a 10-minute local allowance, editable 60-minute dining stop and **$45 breakfast**. Return to Cousin's for editable 30-minute packing stop, then depart toward Arizona. Breakfast and nearby parking are not booked.
- Route checkpoint Ehrenberg after provisional **3 hr 10 min** from Cousin's, adjust **+1 hour for AZ clock**; 15-minute editable stop. Return Home from Ehrenberg is provisional **2 hr 11 min**, not live traffic. No private family/home street addresses are stored.
- Editable **$85 remaining trip fuel reserve** and **$10 road snacks** budgeted Sunday, but the fuel reserve covers **later top-offs on Saturday/Sunday**; it is **not** a claim that all that fuel will be purchased at Ehrenberg, nor that the vehicle can reach Ehrenberg without an earlier fill. The actual return refueling location must be chosen based on gauge/MPG and routing.

### One connected budget
- Day totals remain additive, each purchase is counted **once**. Tuesday ticket cost changes with Dizzy: **$50 for two** (Weekend/Friday) or **$25 solo**, and haircut remains $35. Wednesday/Thursday totals and Mom-pays decision retain current behavior.
- **Trip expenses** includes tickets plus Wednesday–Sunday costs, excluding Tuesday haircut. **Haircut · prep** adds $35; **Contingency** is editable, default $50; **Grand total** = Trip expenses + $35 + contingency. Fuel/Tickets/Lodging are **included breakdowns**, not extra charges.
- Initial Weekend / Mom pays / Saturday dinner TBD / Saturday karaoke No: Tue **$85**, Wed **$90**, Thu **$35**, Fri **$210**, Sat **$135**, Sun **$140**, contingency **$50** → **Grand total $745** (**Trip expenses $660** before haircut/buffer). No Dizzy default → **$550** grand total; Friday-only Dizzy default → **$680**. These are **planning envelopes, not verified expenses, affordability approval, or price guarantees**.
- Existing full-width decision menus, blue-value editable native inputs, circular departure/arrival/pause symbols, 56px primary rows, separate 13px info rows, 12px card rhythm, 28px major-section rhythm, light/dark palettes, and covered-dinner semantics remain app-local. **Inputs and choices do not persist after a page reload**.
- User has **not confirmed** Dizzy's attendance, paid event tickets, a Hanagi reservation, Friday GardenWalk parking validation, Saturday dinner, or exact fuel/route conditions. The existing **Wednesday 9 PM La Baja Tacos close** remains an outstanding dinner-location decision; the user requested a different late-night Mexican restaurant, but no replacement was explicitly locked, so do not silently change it as part of this Friday–Sunday build.
- No live GPS, traffic, reservation inventory, ticket purchase, parking guarantee, fuel-sensor readings, automatic bank synchronization, new product shell, or unrelated Babel app changes. Validate Sunday fuel reachability and the Friday-only late return on real maps before travel.

## November 17 — Wednesday Tacos Nogales pickup and eat at Cousin's (v1.4.2; historical change)

**Approved change:** Wednesday Nov 18 replaces La Baja Tacos dinner with **Tacos Nogales, 401 Nogales St, La Puente, CA 91744**. Instead of dining at the taco stand, the driver **picks up the food and returns to Cousin's house to eat and stay overnight**. This is a confirmed planning choice, **not** a prepaid/placed order or restaurant reservation. The user's reference to returning "home" on Wednesday means Cousin's place in the context of the established overnight; private residential addresses stay out of public sources.

- Waze and Restaurantji both list Tacos Nogales on Wednesday **5:30 PM–midnight PT**, much later than La Baja's former 9 PM close (https://www.waze.com/live-map/directions/us/ca/la-puente/tacos-nogales?to=place.ChIJ7aCFmgsrw4ARzWKKLvE12XY and https://www.restaurantji.com/ca/west-covina/tacos-nogales-/). These are third-party published hours, **not** verified last-order/pickup availability; call if significantly delayed. Local street-taco operation and wait time can vary; no actual food order has been placed.
- Wednesday estimated Cousin arrival retains **8:36 PM PT**, settle **10 min**. Leave Cousin's about **8:46 PM PT**. Allow **10 min** each way for local driving as **provisional estimates** with mileage TBD (not verified traffic), for a **8:56 PM** Tacos Nogales arrival. The native blue **Pickup target** is editable, default **9:00 PM**.
- The circular Tacos Nogales **pause** is an editable **10-minute pickup/wait duration** instead of the former 25-minute dine-in. Pickup departure defaults **9:10 PM**; return to Cousin's **9:20 PM**. Place **25-minute eating pause at Cousin's** after return, before Overnight Cousin's. This is where the meal happens, and it creates **no extra food charge**.
- Wednesday **Status** measures minutes until Tacos Nogales **midnight closing at the end of the modeled pickup wait** (default **-170 min**). Late pickup departure / arrival turns red accordingly. Changing Cousin arrival, pickup target, or pickup wait recomputes all subsequent Wednesday timing and status, retaining existing Arizona-vs-California time distinctions. This is an estimate and not a GPS/ordering guarantee.
- Keep **$15 editable Wednesday dinner budget** and the default **$90 Wednesday total**, **$745 all-in Weekend grand total** (including $35 haircut and $50 contingency). Tickets, fuel and all later-day/other-day controls unchanged. The earlier 9 PM La Baja closing constraint is **superseded**, not a competing runtime requirement.
- Preserve the exact established 56px rows, grouped cards, icons, separate info rows, blue native inputs, dark/light styling, and overall layout. Inputs remain non-persistent across reload.

## November 17 — Unified editable arrival/departure clocks (v1.5.0; historical change)

**User-approved system-level update:** every itinerary **arrival and departure** row now uses the established native blue editable clock control and receives a **↺ reset-to-recommended** action when changed. This is a shift from the previous incomplete mixture of a few editable rows and many static clocks, not a layout redesign. All recommendation calculations remain provisional travel allowances, **not GPS, live traffic, reservation confirmation, or autonomous tracking**. The user can record an actual time earlier or later than recommended. Such corrections propagate to later stops within that day's selected route, without silently rewriting earlier observed times or the independent mileage/fuel figures.

### Shared timing contract
- Existing Work, Home, Ehrenberg and Cousin time inputs retain their approved behavior and now follow the same **visible reset-control grammar**. The original editable Work departure (3:15 PM AZ), Friday Mom departure (1:15 PM PT with Dizzy or 4:10 PM solo), Friday-only Saturday Cousin departure (11:20 AM PT), and Sunday breakfast departure (9:50 AM PT) expose reset-to-recommendation after manual editing.
- **53 additional checkpoint rows** receive the same native clock input and reset (including home arrival, stop departures, restaurants, car trips, Friday/Saturday conditional branches, Sunday AZ return). A manual override changes only that checkpoint and its downstream estimates, not previous history. Later manual overrides remain their own authoritative checkpoint until reset; their local subsequent durations naturally recompute.
- Day-bounded calculation: Wednesday Arizona→Pacific shift remains -60 minutes at Cousin arrival; Sunday Pacific→Arizona shift remains +60 minutes at Ehrenberg. Midnight crossings show **+1** where needed, without treating next-day time as previous-day noon. Thursday food and Friday DJ event retain distinct *target times* instead of being moved arbitrarily by earlier delays.
- At **Home**, the current 5–30-minute automatic pause aiming near 4 PM AZ is unchanged; a manual Home departure or stay can go outside the automatic bounds and will continue recalculating Ehrenberg and Cousin. Home arrival is now editable too.
- Stop duration and departure are linked: editing **Ehrenberg, Tacos Nogales pickup, Friday Temecula pickup/drop-off, Hanagi, event end, Saturday karaoke/Temecula drop-off, Sunday breakfast/packing/Ehrenberg** departures updates the displayed adjacent stop duration where one has a numeric editor. Editing that pause later takes precedence over the departure override. Resetting a manually overridden departure restores its *previous planned duration* rather than locking in a newly inferred actual duration.
- At Thursday **Caramelo Café**, correcting the arrival later automatically moves breakfast finish and Cousin return later. Lunch departure stays at its preferred 12:50 PM only while that is feasible; if breakfast overflows it, lunch departure and arrival push later. Fixed lunch target **1 PM** remains an anchor, not a promise that the restaurant/meal will wait. Similar arrival/leave updates cascade through Mom/Rosalie/Rude Dogs and the Friday/Saturday routes.
- Friday House of Blues **8 PM event start** and Thursday Rosalie **7:30 PM dinner target** remain fixed planning anchors; recording real arrival does not shift the underlying official event. Saturday dinner and Sunday breakfast planned targets similarly remain distinct. Explicit earlier/later travel overrides never masquerade as confirmed reservations.
- Manual clock values before their immediately preceding departure/arrival are *shown with the existing red warning semantic*, not silently altered into another time. A few fixed-time event targets and elapsed-duration info rows stay non-clock controls because they are not arrival/departure events. Choices and spending amounts continue to update day totals and grand total; the default **$745** weekend budget is unchanged.
- Visible text sweep: rename **“Lunch · Fuel” → “Lunch”**, **“Pickup target” → “Pickup”**, appropriate *... target* labels to **“Target”**, **“Lunch + snacks” → “Lunch”**, **“Pickup + fuel” → “Pickup”**, **“Drop off Dizzy” → “Drop-off”**, **“Dinner reserve” → “Budget”**, event/karaoke spending labels to **“Spend”**, later trip fuel to **“Fuel”**, and the Mom parking pause to **“Parking”**. Retain venue and place names, where abbreviating would lose meaning. These are text changes, not new semantic decisions.
- Keep 56px primary rows, existing 12px card / 28px section spacing, separate information rows, same icons, CSS/dark mode, and original no-public-residential-address rule. **No persistence or actual app-side booking**: edits reset on page reload until explicitly implemented separately.

### Validation
- Mock-interaction runtime checks covered **22 distinct scenarios**, including Caramelo 10:20 and 12:45 arrivals, a later lunch, Home 3:29 arrival and 30-minute cap, Ehrenberg manual departure + pause recovery, Friday pickup and time resets, Sunday breakfast and pack edits with AZ shift, Saturday karaoke arriving 8:20 and late-night +1 return, all Dizzy branches, baseline Friday/Saturday reset, and unchanged default fuel/grand totals.
- JavaScript syntax, all 299 unique element IDs, every checkpoint input + reset, balanced HTML tag counts, original CSS byte-equivalence, seven active itinerary sections and no private home addresses checked before merge. Real-device review remains necessary; overlong source-side scripts/tests are not proof of iPhone touch polish.

## November 17 — Cousin's Wednesday wait becomes editable (v1.5.1; historical change)

**Approved standalone usability change:** the first Wednesday Cousin's stop (after the Arizona-to-California arrival, before driving to Tacos Nogales) now uses an editable native blue **duration field** instead of static inferred “10 min”. The **recommended starting stay is 15 minutes**, not a minimum or maximum. The user may set 0, 5, 20, 45, or any other nonnegative number to compensate for reality. The Wednesday Cousin ETA remains editable; the recommended taco departure is Cousin arrival + edited stay. Driving allowance to Tacos Nogales, 9 PM pickup target, editable pickup waiting time, return to Cousin, subsequent daily itinerary, time-zone rules and fuel/money totals are otherwise unchanged.

**Last-edit-wins, synchronized controls:** editing the wait updates the departure time and downstream pickup/return; editing Cousin departure explicitly updates the displayed stay duration. Resetting a manually overridden departure restores the stay duration that was set before the departure override, rather than locking in the inferred duration. Editing the duration again clears any departure-time override, while preserving the explicit new duration through subsequent ETA corrections. The same established iPhone card/row appearance is retained. No other creative redesign, typography, card-break changes, route choice, feature additions, or style changes are authorized as part of this release.

At the existing **8:36 PM PT** Cousin arrival, 15 minutes yields departure **8:51 PM**, tentative Tacos Nogales arrival **9:01 PM**, food pickup departure **9:11 PM** and Cousin return **9:21 PM**, using unverified 10-minute local drive estimates. Dinner cost remains **$15**, Wednesday planning total **$90**, weekend default grand total **$745**.

**Validation:** 11 runtime interaction scenarios covering the 15-minute default; overrides to 5/20/45 minutes; direct departure adjustment; reset restoring original duration; last-edited control precedence; later actual Cousin arrival preserving manually set wait; arrival reset; no-Dizzy and Grandpa-pays budget regression. No other visible structure or styling altered. The broader stop/leg information-architecture proposal is **unapproved, remains separate, and must be physically reviewed before any future merge**.

## November 17 — One production itinerary, adaptive pickup and clean time rows (v1.6.0; historical/superseded pickup behavior)

**User-verified physical iPhone evidence:** On the prior preview, the Tacos Nogales arrival could be edited to **8:18 PM** but its pickup remained **9:00 PM**. Visible blue reset arrows proliferated beside time edits and distracted from the redesigned stop-card layout. The user expressly requested a single **most-updated website**, not active vs preview variants. This release promotes the already reviewed stop-first structure and incorporates those corrections.

### Active presentation and interaction grammar
- **One destination = one stop card:** preserve native iPhone-style card surfaces, system typography, colors, icons, 56px touch rows, and original timing/expense editors. Within a stop: arrival, target or purpose, editable stay and budget if relevant, then departure. Shared destinations like Hanagi, Grandpa's, The Hangout use a single conditional stop card rather than split across branches. The original drive and walk estimates remain quiet 26px connectors between stops.
- **Tacos Nogales pickup adapts to the actual/suggested arrival:** default pickup time = latest displayed Tacos arrival **+4 minutes** (the original 8:56→9:00 allowance, now relative rather than a fixed clock target). E.g., 8:18 arrival implies **8:22 pickup**, with the user-set pickup duration applied before leaving. At the default current Wednesday itinerary, Cousin arrival 8:36 PM PT +15 min, drive 10 min → tacos arrival 9:01 PM, pickup **9:05 PM**, departure **9:15 PM**, Cousin return **9:25 PM**.
- **Manual pickup override remains possible:** a user-entered pickup clock time is preserved as reality moves; the display marks a manually selected time earlier than the actual arrival red, and the following departure cannot be scheduled before arrival. The optional manual target can be restored to arrival-relative recommendation through **Reset clocks**.
- **No inline reset-arrow clutter:** all per-field reset arrows remain code-wired but visually hidden throughout the itinerary. One quiet **Reset clocks** control appears below the budget **only when an arrival/departure clock is manually overridden**, and restores estimated clock inputs while leaving user-entered choices, spend amounts, and manually entered stay durations intact. This action is intentionally global for clock overrides, not a claim of individual or duration resets. It also restores any pauses that were modified only as a side-effect of an overridden departure.
- All original 300 controls, budget semantics, real time-zone conversions, alternative Dizzy paths, payable/covered Rosalie dinner, Saturday dinner and karaoke, and tentative fuel/drive estimates are maintained. No new bookings, addresses, live navigation, or payment assumptions. **Inputs still reset on page reload**; durable client persistence is not yet implemented.
- `layout-review.html` is intentionally **deleted** from the production branch. Do not send or build another competing public preview unless user explicitly requests one. Version `v1.6.0` is visible in the one live page footer.

### Verification and release constraints
- Initial source and markup checks: all original element IDs preserved; source JS parse valid; all DOM selector IDs resolved; card/section tags balanced; no private family addresses. **15 interaction scenarios** passed using a mock DOM, including screenshot exact 8:18→8:22 pickup, early/late arrival, manual pickup override, impossible early pickup warning, reset/recommendation recovery, Cousin wait edits, all Dizzy cost scenarios ($745 Weekend, $550 Solo, $680 Friday-only), Saturday payer/karaoke, and Sunday AZ shift.
- Device rendering must still be judged on a real iPhone for typographic rhythm, control accessibility, and scroll interactions; mock JavaScript tests alone are not a physical-device sign-off. Do not assert live until GitHub Pages workflow success for the exact merged commit.
- If the new structure proves worse physically, the previous `v1.5.1` Git commit remains a **rollback reference**, not a competing user-facing website.

## November 17 — Day-first itinerary and simplified walk-up pickup (v1.7.0; historical layout)

**User authorization:** "Whatever u think is best" in response to the proposed coherent one-panel-per-day simplification and the Tacos Nogales pickup discussion. This implementation changes the active `index.html` only, through branch/PR/test/merge; **one canonical site remains https://babedrums.github.io/babel-trip/** with no competing public preview.

### Current screen hierarchy
- Seven unified rounded **day panels**: Tuesday prep, Wednesday AZ→CA, Thursday Covina/family, Friday Anaheim event, Saturday Grandpa/evening, Sunday CA→AZ, and Trip budget. Every header always shows date/label, short route/purpose, dynamically computed **day total**, and native disclosure chevron. Wednesday is initially expanded; selecting another day opens it and collapses the preceding panel for low-scrolling orientation. All controls for all seven days remain mounted and calculations update when their panel is closed.
- Inside the selected panel is **one continuous white surface**. Travel times remain quiet separators (not standalone floating cards); stops are now brief entry rows plus a tappable **summary** showing stay/pickup duration, leaving time, and relevant cost. Tapping a stop's summary discloses its full original editable time/cost/detail rows; it can be collapsed without losing entered values. Cost/route equations are untouched outside the approved Tacos simplification.
- **Decisions remain immediately accessible** (Dizzy, Mom pays, Saturday dinner/karaoke); conditional Hanagi/Grandpa/Hangout arrival choices still use the correct current path. The end-of-page Trip budget panel displays the overall total in its closed header (default Weekend **$745**), without needing a second open page.
- Visual language remains original SF/system fonts, color variables, existing 56px native-editor controls (50px within day detail rows), rounded white grouped surfaces, blue editable values and subtle separators. No unrequested decorative icons, separate UI library, new navigation hierarchy, or unconfirmed "booked" statuses.
- Removed **mi TBD** and repeated **· planned** phrases from read-only travel annotations because these gave no actionable information; underlying travel estimates and distances already known remain unchanged. The original hidden per-row reset affordances stay visually hidden; the established **Reset clocks** action applies to adjusted time fields only. Session state is still not persistent across a page reload.

### Tacos Nogales ordering contract
- **No preorder verified or placed.** Third-party listings mention online ordering but do not resolve to a verified Tacos Nogales store checkout. Treat restaurant as **walk-up unless user confirms phone preorder**; (626) 912-9305 is the previously located listing number.
- Eliminate the arbitrary standalone **Pickup** clock and the old **arrival +4 min** rule. The stop now reads **Tacos Nogales arrival → editable 20-minute Order/Pickup duration → departure**. This is an *estimate*, not a claim about service speed or an actual pickup appointment. A preordered/short wait can be represented by editing the duration to e.g. 5 minutes; departure remains editable separately using the prior last-edit-wins duration and reset logic.
- With recommended Cousin arrival 8:36 PM PT, editable 15-minute settling time, and 10-minute local drive, **Tacos arrive 9:01 PM → leave 9:21 PM → Cousin return 9:31 PM**. No additional cost: dinner $15, Wednesday $90, Weekend total $745. Existing late pickup/restaurant closing checks and day time zones remain, now based on the completed order/pickup duration. The old pickup time is intentionally removed (no dead state).

### Verification and non-goals
- Runtime mock-DOM integration tests: **14 passes** for initial day totals, default Wednesday open, selecting another day, stop detail expand/collapse, 8:18 arrival +20 minute departure, manually shortening pickup duration, Cousin settling, revised Wednesday cost flowing into Grand total and day header, Solo $550, Friday-only $680, Weekend and Grandpa dinner/karaoke, Sunday AZ time-zone, and Reset clocks. JS parse, all DOM selectors, duplicate IDs, balanced HTML section/div tags and seven day panels checked on branch.
- **No assumption of confirmed advance ordering**, new event reservations, new spending approvals, live location/traffic, accurate mileage where unavailable, or storage between browser refreshes.
- Final public release claims require the exact merge commit's GitHub Pages **deployment success**; on-device visual/VoiceOver examination must still be reviewed, not guessed from static code or mock tests. Avoid making a new preview URL for the user.


## November 17 — Provisional Saturday dinner default (v1.7.1; historical layout)

- Active v1.7 day-panel design, stop disclosure, native time controls, 20-minute unpreordered Tacos Nogales pickup and every calculation remain unchanged.
- Change **Saturday dinner's default** from the unhelpful “TBD” to **The Hangout, Seal Beach**, already present as a selectable branch. Grandpa dinner and TBD remain selectable alternatives. The existing $85 Weekend / $45 solo dinner reserve, 6:30 PM target, estimated Hangout drive, Dizzy branches, karaoke setting and $745/$550/$680 scenario totals do not change. **This is a working plan, not a table booking.**
- Official restaurant hours for the Seal Beach location at 901 Ocean Ave list Friday/Saturday lunch/dinner service through **10 PM**: https://www.thehangoutrestaurant.com/contact-the-hangout . The itinerary does not confirm table availability, actual driving time, or cost of an order.
- **Only one site URL:** https://babedrums.github.io/babel-trip/ . No new preview or change to the day panel layout. Deploy only after PR merge + GitHub Pages exact commit success. An unmerged independent exploratory branch must never be promoted over newer `main` without reconciliation.

## November 17 — Restore stop cards (v1.7.2)

- Physical iPhone review rejected the continuous day surface and nested stop disclosures. Restore the v1.6.0 layout with separate rounded stop cards, quiet travel connectors and directly editable time and spending rows.
- Keep the 20-minute editable Tacos Nogales order/pickup duration and Saturday's provisional Hangout dinner default. Preserve the single canonical itinerary URL. Revisit visual changes only after physical-device review.

## November 17 — Day and budget shortcuts (v1.7.3)

- The existing continuous itinerary has date links and a Budget shortcut at the top. Use native in-page links so dates can be bookmarked and browser Back works. All stops and editors stay directly visible and the schedule and budget script is unchanged.

## November 17 — Simplified typography (v1.7.4)

- Physical iPhone feedback identified too many competing text treatments. Use 22px semibold for day headings and 16px for itinerary text. Reserve semibold within rows for stop names, totals, and selected navigation or decisions. Use existing color to distinguish editable values and secondary details. Card structure, controls, timing, and budget logic are unchanged.

## November 18 — On-device autosave (v1.7.5; rolled back)

- Times, durations, costs, choices, and clock reset state survive reloading and reopening in the same browser. The stable, trip-specific storage key is independent of release numbers. The base itinerary still opens with defaults when browser storage is unavailable or the stored JSON cannot be read.
- Autosave is local to the browser. It does not sync devices or make the page available offline. The itinerary layout and schedule and budget calculations are unchanged.

## November 18 — Restore approved itinerary and pause autosave

- Restored the exact v1.7.4 runtime after the user reported that v1.7.5 appeared to load an older plan. The restored page neither reads nor writes the v1.7.5 browser snapshot. Existing snapshots are left in place.
- Keep autosave paused until the user explicitly reopens the work. The precise cause of the reported older plan was not verified on the user's device.

## November 18 — Quieter top controls and Wednesday status (v1.7.6)

- Physical iPhone review narrowed the issue to the large date shortcut grid and Wednesday's unexplained signed status. Date and budget links now sit inside one collapsed Jump to control. Wednesday only shows a pickup warning when projected pickup ends at or after midnight.
- The approved typography, itinerary cards, calculations, and paused autosave remain in place.

## November 18 — Remove completed haircut and shorten Jump (v1.7.7)

- Remove the completed haircut from Tuesday and the trip budget. The Tuesday subtotal now covers tickets, and the default grand total is $710 including contingency. The date and budget menu is labeled Jump.

## November 18 — Right-align travel durations (v1.7.8)

- Travel connectors place mileage, refill-range notes, and qualifiers on the left and duration on the right, aligned with stop times. Driving and walking share the same row order. Fuel-only rows retain their original order.

## November 18 — Start the itinerary on Wednesday (v1.7.9)

- Remove Jump and the Tuesday section. Move the existing Dizzy decision and ticket amount into the first card under Wednesday. Remove the redundant prep subtotal. Tickets remain counted once in the trip budget.

## November 18 — Consistent itinerary row labels (v1.7.10)

- Supporting labels such as Fuel, Snacks, and Stay use the same regular-weight text. Departure labels use the existing semibold weight throughout the itinerary. Arrival and destination labels retain their hierarchy.

## November 18 — Mileage information (v1.7.11)

Full-tank range rows show only 300 miles left. Driving connectors show the duration without a drive suffix.

## November 18 — Standalone refill information (v1.7.12)

Both range rows use the travel connector outside the fuel card, immediately following the refill.

## November 18 — Consistent itinerary icons (v1.7.13)

Arrival, stay, and departure symbols share the same secondary gray and opacity.

## November 18 — Home to Ehrenberg mileage (v1.7.14)

The editable 144-mile default uses the Glendale-to-Ehrenberg city estimate from Travelmath. Remaining miles to the planned refill equal 300 minus the 7.1-mile commute minus the entered leg distance, rounded for display. The 2 hr 11 min time allowance is independent.
