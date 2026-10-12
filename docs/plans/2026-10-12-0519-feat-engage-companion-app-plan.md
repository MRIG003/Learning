---
title: Engage Companion App (Phase 1) - Plan
type: feat
date: 2026-10-12
topic: engage-companion-app
artifact_contract: ce-unified-plan/v1
product_contract_source: ce-brainstorm
execution: code
---

# Engage Companion App (Phase 1) - Plan

## Goal Capsule

- **Objective:** In a 1-2 hour corporate meeting run on any video tool, most attendees stay engaged for the whole meeting, and the host can see room-level health without any attendee feeling watched.
- **Means:** A platform-neutral web companion app that attendees open from a link pasted into the meeting chat. No meeting bot, no native add-on.
- **Product authority:** The brief's design principles (below as R-IDs) are fixed constraints. Everything marked "proposed" in Key Decisions is this brainstorm's recommendation and can be overridden by the product owner.
- **Open blockers:** None block planning. See Outstanding Questions, "Resolve Before Planning" (two items).

## Product Contract

### Summary

Engage is a companion web app for live meetings. The host creates a room, pastes a link into the meeting chat, and attendees join in one tap on a phone or second window. The app offers light games grouped by how much attention they cost, gives the host a team-level health view and a small set of controls, and sends the host a post-meeting report. Phase 1 succeeds when 5 hosts each run a real meeting with it.

### Problem Frame

In a long corporate meeting, most attendees speak for about five minutes and are idle the rest of the time. Hosts and senior people want everyone involved, but visible monitoring feels like micromanagement and makes attendees resent the meeting. Existing meeting tools offer reactions and polls but nothing that sustains attention over an hour or gives a host a fair read on the room.

Without a bot, the app sees only people who join it and only what they tap. The design has to work honestly inside that limit.

### Key Decisions

Principles stated in the brief are user-directed constraints and appear as requirements. The decisions below answer the brief's six open questions; all are proposed defaults unless marked otherwise.

- **Measure participation among joiners, never "engagement of the meeting."** The dashboard reports interaction among people who joined, always shown next to joined-versus-expected coverage. Governs R16, R17, R18.
- **Silence in the app is not disengagement.** Someone watching quietly is normal, so the app never infers anything about an individual from inactivity. Governs R12, R19, R20.
- **Game budget by attention cost.** Ambient play is on by default; micro-moments are host-triggered or host-approved; break blocks run only at host-marked break points or when the host starts one. Governs R5, R6, R7, R8.
- **The host's example nudge ("3 people haven't spoken in 40 minutes") is deferred to phase 2.** It needs speaker timing, which needs the bot. Phase 1 nudges use interaction signals only. Governs R18.
- **First buyer and primary user is the individual host: a team lead or senior presenter running recurring meetings.** L&D and HR needs (cross-meeting analytics, org rollups, consent review) are phase 2 or later.
- **Host identity is lightweight, attendee identity is none.** Hosts sign in by email link so they can retrieve reports; attendees join with a nickname and no account. Governs R1, R3.

### Actors

- A1. Host: runs the meeting, creates the room, controls games, reads the dashboard and report.
- A2. Attendee: joins from the chat link on a phone or second window, plays, reacts.
- A3. Speaker: whoever is presenting at the moment; not a user of the app, but the party games must never compete with.
- A4. Senior stakeholder: reads the post-meeting report; does not use the app live.

### Requirements

**Joining and identity**

- R1. A host can create a room in under two minutes with no payment and sign-in by emailed link only.
- R2. An attendee joins from a single shared link, with no account and no install, on a phone browser or desktop window, in under 15 seconds.
- R3. An attendee chooses a nickname on join (a suggested one is prefilled) and the same device rejoins as the same person after a refresh or a dropped connection.
- R4. The room link works for late joiners, who start in the ambient layer and are never forced into a game in progress.

**Games, by attention cost**

- R5. Ambient play is available at all times unless the host pauses it: emoji reactions, buzzword bingo with host-set keywords, and a "will this run over?" prediction that resolves at the meeting end.
- R6. Micro-moments last 10-30 seconds and appear only when the host triggers one or approves one the app suggests: a reaction race and a host-authored quick trivia question about what was just discussed.
- R7. Break blocks last 2-5 minutes, start only when the host starts one or at a host-marked break point, and end when the host ends them or the timer expires.
- R8. No game audio plays by default, and no game interrupts a screen the attendee is actively using for the meeting (no takeover popups; the panel signals, it does not seize).
- R9. A host-authored trivia question needs only a question, up to four options, and a correct answer, and can be created and launched in under 30 seconds.
- R10. Every game can be skipped or ignored by an attendee without penalty to team standing.

**Host controls**

- R11. The host can start a pulse check (a one-tap, 1-5 question to the room), start or end a break block, pause all games in one action, and resume them.
- R12. While games are paused, attendees see a quiet "paused by host" state, and nothing in the app is scored or recorded as inactivity.
- R13. The host can mark break points on an agenda before the meeting and add one live during it.

**Attendee view and scoring**

- R14. The attendee view is a collapsible side panel, with a collapsed state that still shows only a small activity indicator.
- R15. Each attendee sees their own score and a team leaderboard that lists only top contributors; no one is shown a rank below the highlighted top group.

**Host dashboard**

- R16. The dashboard shows participation as a room-level pulse over time (a rolling, bucketed line), not a feed of individuals.
- R17. The dashboard always shows joined count against the host's expected count, and labels the pulse "indicative" when coverage is below a threshold set at planning.
- R18. The dashboard shows at most one suggested nudge at a time, generated from interaction signals only (for example "a third of joined attendees have not interacted in 20 minutes; try a micro-moment"), and the host can dismiss it.
- R19. Individual data anywhere in the product is positive-only: contributions, scores, and streaks. No list, count, or export names who was idle.
- R20. No data in the product is derived from camera, microphone, or screen content; only taps, answers, and reactions inside the app count as signals.

**Transparency**

- R21. Attendees can open a "what the host sees" view that shows exactly the same dashboard-level data the host sees, in the same terms.
- R22. The join screen states in one plain sentence what is collected and what the host can see.

**Post-meeting report**

- R23. When the meeting ends, the host receives a report with: coverage (joined vs expected), participation over time, which games ran and how much each drew, peak and quiet moments with the agenda point or break-block they fell near, top contributors (positive-only), pulse check results, and the over-run prediction outcome.
- R24. The report contains no individual idleness data and names no one outside the positive-only contributions of R19.
- R25. The host can share the report with others by link, and attendees can see the report they would be shown under R21.

### Key Flows

- F1. Host first meeting (setup)
  - **Trigger:** A host who has never used Engage has a meeting in the next day.
  - **Actors:** A1
  - **Steps:** Opens the site; signs in by emailed link; picks a meeting length and a preset (for example "60-minute team meeting"), which preloads ambient games, a starter bingo keyword list, and break points at sensible times. Edits the keywords and agenda marks if wanted; enters expected attendee count; copies a ready-written chat message containing the link; optionally opens the attendee view on their own phone to preview it.
  - **Outcome:** The room is ready in under two minutes, and nothing except ambient play will run unless the host chooses.
  - **Covered by:** R1, R5, R7, R9, R13

- F2. Host in meeting
  - **Trigger:** Meeting starts and the host pastes the link in chat.
  - **Actors:** A1, A2, A3
  - **Steps:** Watches joined count rise toward expected; during a long segment the pulse dips and the dashboard shows a nudge; host triggers a micro-moment; at the marked break point host starts a break block; if the speaker needs the room's full attention, host pauses all games and later resumes.
  - **Outcome:** Games appear only when the host wants them, and the host never sees a named list of the idle.
  - **Covered by:** R11, R12, R13, R16, R17, R18, R19

- F3. Attendee
  - **Trigger:** An attendee taps the link in the meeting chat.
  - **Actors:** A2
  - **Steps:** Lands on the join screen with the one-sentence data note and a prefilled nickname; taps join; sees the collapsed panel with ambient options; reacts, marks a bingo word, or ignores it; when a micro-moment or break block starts, a small notification appears; they play or dismiss it; at the end they see their score, the team leaderboard, and the "what the host sees" view.
  - **Outcome:** The attendee participates at a level of their choosing and never gets a penalty for ignoring a game.
  - **Covered by:** R2, R3, R4, R8, R10, R14, R15, R21, R22

- F4. Post-meeting
  - **Trigger:** The host ends the room or it times out.
  - **Actors:** A1, A4
  - **Steps:** The host receives the report by email with a link; they review and optionally share it.
  - **Outcome:** The host and any stakeholder can learn from the meeting without individual data.
  - **Covered by:** R23, R24, R25

### Acceptance Examples

- AE1. **Covers R12, R19, R20.** Given a host pauses all games for a speaker's 10-minute segment, when the host opens the dashboard, then no individual is shown as inactive for that segment and no inactivity data is recorded against anyone.
- AE2. **Covers R17.** Given the host expected 20 attendees and 6 joined, when the host views the pulse, then the dashboard shows "6 of 20 joined" and labels the pulse indicative rather than presenting a health score as fact.
- AE3. **Covers R7, R13.** Given a break point is marked at 40 minutes, when the clock reaches it, then the host is prompted to start a break block and none starts without the host's action.
- AE4. **Covers R3.** Given an attendee's phone locks and reconnects mid-meeting, when they reopen the link, then they return as the same nickname with their score intact.
- AE5. **Covers R21.** Given an attendee opens "what the host sees," then they see the same room-level pulse and coverage numbers as the host, and nothing more.

### Success Criteria

Phase 1 gate: 5 hosts each run a real meeting with it. A run counts when it meets a floor that planning confirms (proposed: at least 30 minutes and at least 5 attendees joined).

Proposed metrics for the 5 runs (targets are starting points to be calibrated after the first run):

- **Join rate:** joined / expected at the 10-minute mark; target at least 50%.
- **Participation rate:** share of joined attendees with at least one interaction; target at least 70% per meeting.
- **Sustained participation:** share of 10-minute windows where at least a third of joined attendees interacted; target at least 60%.
- **Distraction:** share of post-meeting attendee responses saying "it distracted me from the meeting" (single question on the end screen); target under 10%.
- **Host satisfaction:** at least 4 of 5 hosts say they would run it again; at least 3 of 5 use pause or a micro-moment on purpose.
- **Time to ready:** median host setup under 5 minutes in the first meeting.

### Scope Boundaries

**Deferred for later**

- Meeting bot: live transcript, speaker timing, auto-pause when a name is called, and the "3 people haven't spoken in 40 minutes" nudge.
- Native Zoom, Teams, and Meet add-ons, and Zoho-specific integration.
- Pictionary, jigsaw, and live-leaderboard tournament break blocks (heavier real-time and content needs).
- AI-generated trivia from what was discussed (needs transcript).
- Org-level analytics, multi-meeting trends, and buyer features for HR or L&D.

**Outside this product's identity**

- On-camera or face-based attention tracking.
- Any ranked or named list of idle attendees.
- A new video platform.

### Dependencies / Assumptions

- Attendees can open a link on a phone or second window; the meeting chat allows pasting links (true for all four named tools).
- Hosts will accept an emailed sign-in link; if not, the host-identity decision (R1) reopens.
- Attendees will join voluntarily in meaningful numbers; the product's value depends on that, which is what the join-rate metric tests.
- The first-ship game set (below) is enough variety for one 60-minute meeting.

### Prioritization (feature list)

**P0, needed for the gate**

- Room creation, share-message, nickname join with rejoin (R1-R4, R22)
- Ambient layer: reactions, bingo with host keywords, over-run prediction (R5)
- Host-authored trivia micro-moment (R6, R9) and one break block: a co-op team word game (R7)
- Host controls: pause all, pulse check, start/end break, break-point marks (R11-R13)
- Attendee side panel with own score and top-contributors leaderboard (R14, R15)
- Minimum host dashboard: joined vs expected, room pulse over time, one nudge slot, game state (R16-R18)
- Transparency view and positive-only data rule (R19-R21)
- Post-meeting report (R23-R25)

**P1, after the first two runs**

- Reaction race micro-moment
- Preset meeting templates beyond the first
- Dashboard "what happened at this agenda point" markers
- Host rehearsal mode

**P2, phase 2 or later**

- Everything under Deferred for later

### The first four games, and what makes one good

Ship, in order: (1) emoji reactions plus the "will this run over?" prediction as one ambient layer; (2) buzzword bingo with host-set keywords, where attendees self-mark words they hear; (3) host-authored quick trivia on what was just discussed; (4) one co-op team word game as the break block.

A good corporate game passes all of these: learnable in 30 seconds; one-handed on a phone; silent; cooperative or team-scored so no individual loses publicly; skippable; tied to the meeting content where possible (bingo, trivia); works for a late joiner; safe content with no personal topics.

### Open-question answers (summary)

1. **Fair measurement:** report participation among joiners, always beside joined-vs-expected coverage; label low coverage as indicative; never infer anything about individuals from silence (Key Decisions, R16-R20).
2. **First games:** the four above.
3. **Minimum dashboard:** joined vs expected, pulse over time, game state with the pause and break controls, one nudge slot (R16-R18).
4. **First meeting:** Flow F1.
5. **Report:** R23-R25.
6. **First buyer:** individual team lead or senior presenter. This favors setup speed, host control, and positive-only reporting. Choosing L&D would shift priorities toward content-based trivia and learning reports; choosing HR would shift them toward org rollups and consent review, which delays everything else.

## Outstanding Questions

### Resolve Before Planning

- Teams: is the "team" in the team leaderboard the whole room, auto-assigned small groups of 4-6, or groups the host defines? The default assumed above is auto-assigned small groups for tournaments and a whole-room view for the leaderboard; confirm.
- Coverage threshold: what joined-versus-expected ratio makes the pulse "indicative" rather than reliable? Needs a value or a rule before the dashboard is built.

### Deferred to Planning

- Exact sizes for the "pulse" buckets and rolling window.
- Nudge rules: which interaction patterns trigger a suggestion, and how often a nudge may appear.
- Data retention period for room, scores, and reports.
- Whether the over-run prediction resolves from the host ending the room or from the agenda end time.
- Accessibility baseline (screen reader, color contrast, reduced motion) for the attendee panel.
- What "shipit" requires for the launch itself (deadline, format, or listing constraints), which this brainstorm did not cover.
