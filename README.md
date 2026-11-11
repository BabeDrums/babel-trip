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
