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
