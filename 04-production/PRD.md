# Living PRD

> Module 4 · Production Specs. Refactor for readability; extract a living PRD that stays true as the build evolves.

## Problem

_What user problem does this solve? Tie to the validated hypothesis._

Sales representatives and account executives lose selling time when the information needed for a follow-up is spread across dashboard surfaces and when logging a simple deal update feels like management-oriented data entry. The prototype represents two qualitative signals from onboarding interviews: one rep could not find the relevant surface because “every screen looks like a settings page,” and another felt that activity logging served management rather than helping them sell.

The validated hypothesis represented by the prototype is: a smaller sales cockpit that surfaces only the most important follow-ups and lets a rep record the next action in under two minutes will help reps act without returning to a shadow spreadsheet. The proposed behavioral proof is repeat, unprompted use: weekly active adoption and activity logging should rise together. The prototype’s decision rule is to keep the product only if reps return without being asked.

This validation is qualitative and provisional. The workspace contains the two interview quotes and the experiment framing, but it does not contain the original research records, participant count, interview methodology, or evidence that the quotes are representative. The displayed 18% weekly adoption, 14 activities logged, 11-minute current workflow, eight required fields, two-minute target, “week 02 of 04,” and teammate activity are hardcoded or locally derived prototype values—not production telemetry.

## Users & jobs

- **Primary user:** A sales representative or account executive responsible for several active opportunities and time-sensitive customer follow-ups during the workday.
- **Job to be done:** When I begin my day or finish a customer interaction, help me identify the few follow-ups most likely to move a deal forward, understand why each one matters, and record what happened quickly so I can return to selling instead of navigating a CRM or maintaining a separate spreadsheet.

## Scope

- **In:** A responsive Today screen with a focused queue of time-sensitive follow-ups.
Queue context including contact, company, deal, amount, due time, urgency, and deal signal.
Search across contact name, company, and deal name.
A follow-up detail view with customer and deal context, recommended next move, rationale, status, and recent activity.
Quick activity logging for calls, emails, meetings, and notes.
Complete and snooze actions for the selected follow-up.
Recent-activity loading skeletons, an empty state, an error state, and Retry.
An Experiment signals view showing the hypothesis, behavioral measures, decision rule, workflow-time comparison, and qualitative feedback.
A lightweight feedback prompt with positive, mixed, and spreadsheet-preference responses.
Desktop and mobile presentation of the core flows.
- **Out (explicitly):** Authentication, authorization, user accounts, roles, teams, or tenant isolation.
A backend API, database, durable activity history, or cross-session persistence.
CRM, calendar, email, calling, marketing automation, or data-warehouse integrations.
A real prioritization or recommendation model.
Real-time teammate presence, notifications, or collaboration.
Server-driven search, pagination, sorting, filters, or queue configuration.
Production analytics collection, experiment assignment, reporting, or statistical analysis.
Creating, editing, deleting, or reassigning opportunities and contacts.
Working browser Back and Forward synchronization for client-side detail navigation.
Offline support, conflict resolution, audit logs, compliance controls, or data retention policies.

## Requirements

| # | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| 1 | Search follow-ups | Must | A rep can search the current queue by contact name, company, or deal, without case sensitivity. A no-results state explains that no follow-ups match and provides a way to restore the full queue. The prototype searches only local fixture data. |
| 2 | Experiment signals view | Must | The view states the hypothesis, success measures, current-versus-target task time, decision rule, and qualitative signals. Production values must come from defined sources and display a measurement window and freshness state; prototype values are fixtures except for the locally incremented activity count. |

## Data & events

_What gets stored, what gets tracked._

Visible entities and fields

User: display name, initials, organization or tenant, role, and permissions. Only a hardcoded “Jordan / JR” presentation exists today.
Follow-up: identifier, contact name and initials, company, deal name, opportunity amount, due timestamp, urgency label, deal signal, recommended next move, latest touch, and status.
Activity: identifier, follow-up identifier, type (Call, Email, Meeting, or Note), optional note, actor, occurred timestamp, and created timestamp.
Snooze: follow-up identifier, actor, snoozed-at timestamp, wake timestamp, and optional reason.
Feedback response: actor or anonymous participant identifier, response (Yes, Somewhat, or Spreadsheet), timestamp, experiment version, and optional qualitative detail.
Experiment definition: hypothesis, start and end dates, audience or assignment rule, success measures, guardrails, decision threshold, and status.
Experiment observation: active-user count, eligible-user count, activities logged, task duration, return frequency, measurement window, and data freshness.

## Open questions

What research artifact supports the two interview quotes, how many reps were interviewed, and which segments did they represent?
Which part of the hypothesis is considered validated: the pain, the focused-queue concept, the sub-two-minute interaction, or repeat usage?
