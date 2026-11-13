# Babel Trip

This repository owns the **Babel Trip website, its current UI/runtime, and deployment**. The website entry point is `index.html`.

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
