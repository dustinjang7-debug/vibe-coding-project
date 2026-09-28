# Engineering Handoff Note

> Module 4 · Production Specs. Open the black box, make the build legible to an engineer.

## What this is

_One paragraph an engineer can read in 60 seconds._

Daymark is a React/Vite sales follow-up prototype, not a connected CRM. It shows a four-item Today queue, a Follow-up detail screen, Quick log and Feedback dialogs, and an Experiment signals screen. Navigation, local search, logging, complete/snooze status, feedback selection, and the demo activity states work in the browser. All customer records, the displayed identity/date, interview quotes, and experiment figures are fixtures; actions live only in React memory and reset on reload. The app does not call the separately running API server or database, and it does not emit analytics events. Use docs/daymark-prd.md for product intent and unresolved production decisions; do not use the displayed adoption or timing figures as measured outcomes.

## Architecture (plain language)

- **Frontend:** Frontend: The Daily Follow-ups web artifact is a React + TypeScript app served by Vite at the root preview path (/). artifacts/daily-followups/src/App.tsx supplies the app shell, Wouter route, navigation, and screen composition. The PRD-named screens live under src/features/today/, follow-up-detail/, and experiment-signals/; the supporting dialogs live under quick-log/ and feedback/. The follow-ups/ feature holds the shared record shape and avatar.
- **Backend / data:** Backend and data: The workspace also has an Express API server, but Daymark's frontend makes no requests to it. Four follow-ups come from src/features/follow-ups/fixtures.ts. Experiment values and interview copy come from src/features/experiment-signals/fixtures.ts; displayed date, greeting, and teammate presence come from src/features/today/fixtures.ts. The hook src/app/useDaymarkState.ts owns all session-only state and actions. The app wraps the UI in a React Query provider, but it does not use queries or mutations for these flows.
- **Key flows:** Key flows: Today filters fixture follow-ups locally by contact, company, or deal. Opening a row selects its detail and writes a followUp query parameter; the detail shows a fixture recommendation and activity context. Quick log selects Call, Email, Meeting, or Note; Save updates latest-touch text and a local counter, then closes the dialog. Complete and Snooze update local status for the selected follow-up. Feedback stores the selected answer in memory and shows a response; Experiment signals displays mostly fixed figures. ?followUp=1&activityState=loading|empty|error demonstrates detail activity states on initial load. Retry waits 700 ms and always returns to ready; it does not retry a request.

## What's solid vs. what's duct tape

| Area | State | Notes |
|---|---|---|
| Screen-level code and fixture data are grouped by feature; shared types and app-level state are separated from display. | solid | _____ |
| typechecks and builds.	Queue membership, deal signals, recommendations, presence, date, and most experiment numbers are hardcoded. The activities count starts at a fixture baseline of 14 and increments once per distinct logged follow-up in the current session, not once per saved activity. | rough | _____ |

## Risks & assumptions for the team

Do not interpret fixtures as evidence. The 18% adoption, 11-minute baseline, two-minute target, week label, teammate count, and interview quotations are represented in the prototype; original research records, sample size, and telemetry are not in this workspace.
Avoid data loss expectations. Users can appear to save an activity or feedback, but a reload resets it. Decide ownership, authoritative source, failure behavior, and persistence before inviting real reps to rely on the app.

## How to run it

```
From the workspace root, run pnpm install if dependencies are not installed.
In Replit, start or restart the existing artifacts/daily-followups: web workflow. It runs pnpm --filter @workspace/daily-followups run dev with the artifact's port and base-path configuration; open the Daily Follow-ups preview at /. The API server is not required for this frontend prototype.
Check the frontend with pnpm --filter @workspace/daily-followups run typecheck. To build from a standalone shell, run BASE_PATH=/ PORT=18935 pnpm --filter @workspace/daily-followups run build (the managed workflow supplies these variables when it runs the app).
For a quick smoke check, open Today, select a follow-up, log an activity, return to Today, open Experiment signals, and submit Feedback. To inspect the simulated failure view directly, open /?followUp=1&activityState=error at the app's preview root and click Retry.
```
