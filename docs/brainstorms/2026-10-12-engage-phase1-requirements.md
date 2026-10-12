---
title: "Engage Phase 1: companion app requirements"
date: 2026-10-12
status: draft for review
scope: Phase 1 only (platform-neutral web companion app)
---

# Engage Phase 1: Companion App Requirements

## 1. Summary

Engage is an engagement layer that sits beside any video meeting tool. Phase 1 is a web app that attendees open from a link pasted into the meeting chat, in a second window or on a phone. It gives long meetings (1 to 2 hours) light, optional ways to stay involved, and gives the host a team-level view of how the room is doing.

Phase 1 does not listen to the meeting. It sees only what attendees do inside the app. That limit shapes almost every decision below, and the document is honest about it.

**Phase 1 gate:** 5 hosts each run a real meeting with it.

## 2. Problem and target

In 1 to 2 hour corporate meetings, most attendees speak for about 5 minutes and are idle the rest of the time. Hosts and senior people want everyone engaged without it feeling like micromanagement.

**Primary user (host):** the person running a recurring or long meeting: team lead, program/project manager, scrum master, workshop or training facilitator, all-hands organizer.
**Secondary user (attendee):** anyone invited, on any meeting platform, often on a phone while the main window is the video call.

## 3. Design principles (constraints, not goals)

| # | Principle | What it forces |
|---|-----------|----------------|
| P1 | Never compete with the speaker | Games are tiered by attention cost. The host controls when bigger games can appear. Default is quiet. Silent by default (no sound). |
| P2 | Team-level health, not surveillance | Host sees room-level numbers. No per-person idle list anywhere, including exports. |
| P3 | Individual data is positive-only | Individuals see and are celebrated for contributions. Absence of activity is never attributed to a person. |
| P4 | Transparency | Attendees can open a "What the host can see" panel that matches the host dashboard in content. Nothing is collected that the panel does not list. |
| P5 | Interaction signals only | Taps, answers, reactions. No camera, microphone, face, gaze or attention inference. |
| P6 | Effortless joining | One link, no signup, display name only, works on a phone browser. |

## 4. Resolutions to the open questions

### Q1. How do we measure engagement fairly when only people who joined are visible?

Phase 1 can only measure the joined population, so the design avoids pretending otherwise.

**Two separate numbers, never blended:**
1. **Reach:** joined attendees vs. expected headcount (host enters it, or it is left blank). This is an adoption signal, not an engagement signal. A low reach says "few people opened the app," not "the room is disengaged."
2. **Responsiveness:** of the prompts that were actually offered, what share of joined people responded, per time window. Using offered prompts as the denominator makes the measure fair across quiet and busy stretches. Raw click counts reward whoever taps most and punish meetings where the host showed few prompts.

**Fairness rules:**
- Engagement is computed only over windows where something was offered. During stretches with nothing offered, the dashboard shows "no prompts" and not "low engagement."
- Host-marked "heads-down" or "presentation" segments suppress prompts and are excluded from the score.
- Ambient reactions count as a low-weight signal. Responses to a direct prompt count as a high-weight signal. The weights are visible in the transparency panel.
- Joined-but-silent is not a negative event. The room score is the share responding, trended over time, shown as three bands (warm / steady / cooling) with a sparkline, not a raw percentage the host can read as a grade.
- **Minimum group size:** below a threshold (proposed: 5 joined) the dashboard shows only qualitative bands and hides counts that could single out a person.
- Speaking is invisible in phase 1. The dashboard says so plainly, and the product never claims to know who has or has not spoken.

**Consequence for the nudge in the brief.** "3 people haven't spoken in 40 minutes" requires the phase 2 bot. Phase 1 nudges are room-level and interaction-based. Examples: "Responsiveness has cooled for 12 minutes. Try a 20-second pulse check or call the break at 45 min." "Break point at 45 min is coming up in 5 minutes." The "invite their view" nudge is deferred to phase 2.

### Q2. Which 3 to 4 games ship first?

**What makes a game good for a corporate audience:**
- Understandable in under 10 seconds with no instructions.
- One thumb, a phone, no sound.
- No knowledge or skill prerequisite, no way to be humiliated.
- Team-first scoring. Individual scores exist but the headline is the team.
- Low-stakes content. The host controls the content, with a safe built-in default library.
- Fully skippable. Ignoring a game costs nothing and is invisible.
- Accessible: not color-only, readable text sizes, no flashing.

**Recommended first four (one per attention tier, plus the one that earns the leaderboard):**

| # | Game | Tier | Why it ships first | Notes |
|---|------|------|--------------------|-------|
| 1 | **Reactions + room mood** | Ambient | Lowest cost, always on, produces the base engagement signal, proves attendees are using the app | Small fixed emoji set, rate-limited per person, no free text |
| 2 | **Buzzword bingo** | Ambient | Best fit for "doesn't compete with the speaker": attendees must listen to play, so it pulls attention toward the meeting | Host sets keywords (or picks a pack) before the meeting. Attendees self-mark on hearing a term, honor system. Card completion adds team points |
| 3 | **Quick pulse and prediction** | Micro-moment (10 to 30 s) | One component serving two uses: a host-authored one-tap question ("clear so far?", a quick trivia on what was just discussed) and the "will this run over?" prediction that resolves at the end | Host types the question in under 15 seconds, or uses a saved one. No transcript, so trivia content is host-written in phase 1 |
| 4 | **Team trivia round** | Break block (2 to 5 min) | One break game is enough to test the whole break flow: host starts it, the room plays, a live leaderboard appears, the room returns to the meeting | Co-op or team-vs-team format, host-chosen or default question packs |

**Deferred:** reaction race (cheap, a good fast follow, candidate for slot 5 if capacity allows), jigsaw, co-op word game, Pictionary (drawing needs real-time canvas and moderation concerns), full tournament brackets.

**Hypothesis to test in the 5 meetings:** ambient games alone may deliver most of the value, and break blocks may be rarely used. The test meetings should reveal which.

### Q3. Minimum useful host dashboard on day one

One screen, readable at a glance in a side window:
1. **Room pulse:** three-band indicator and a 60-minute sparkline of responsiveness, with the agenda break points marked.
2. **Reach:** joined vs. expected.
3. **Controls:** pause all games (big, always visible), start pulse check, start/end break block, current game state.
4. **One suggested nudge card** at a time, dismissible, room-level only, with a plain explanation of why it appeared.
5. **Agenda strip:** items with break points the host can mark, with time elapsed.

Not on day one: per-game analytics, cross-meeting trends, individual views, notifications to the host, anything ranked.

### Q4. First-meeting experience for a new host

Goal: from landing page to a live room in under 3 minutes, with no way to accidentally disrupt the meeting.

1. Host enters a meeting name and duration (and optionally expected headcount). Identity is a lightweight email magic link so the report can be delivered; attendees need nothing.
2. The app suggests a **light-mode starter setup**: ambient games on, micro-moments allowed, break blocks off until the host triggers one. It proposes a break point at roughly the halfway mark for meetings over 60 minutes.
3. Optional agenda entry (paste a list). Host can add keywords for bingo or choose a pack.
4. **Rehearsal mode:** host sees the attendee view with simulated activity so they know what attendees will see and what the dashboard shows. Removes fear of "what if it goes wrong live."
5. **One-tap "Copy invite for chat"** produces a short message with the link and one line explaining what it is ("optional, ignore it any time, here is what the host can see"). A QR code option is available for phones.
6. In the meeting, the host posts the link and says one sentence. The dashboard shows people arriving.
7. First nudge in the live room is usually "try a pulse check," giving the host a guided first action.
8. After the meeting, the report arrives (see Q5) and asks for a one-minute host feedback form.

### Q5. Post-meeting report contents

Delivered to the host and, for transparency, a matching attendee-safe version is available to everyone who joined.

**Contents:**
- Meeting header: duration, reach (joined vs. expected), peak concurrent.
- Engagement timeline: responsiveness over time with agenda items and break points overlaid, and a plain-language read ("steady for 35 min, cooled after the budget review, recovered after the break").
- Prompt effectiveness: which prompts or games drew the most responses (team-level).
- Pulse and poll results, and the "will this run over?" outcome.
- Team highlights: total contributions, bingo completions, trivia winners. Top contributors are celebrated by name (opt-in to being named; default is display names shown on the leaderboard during the meeting and in the report).
- Host-only suggestions: 2 to 3 observations tied to timing ("engagement cooled 38 to 52 min; consider a break at 40").
- A short "what this report cannot see" note (no speaking data, only app users).

**Never in the report:** any list, count or ranking of idle or non-responsive people, per-person engagement scores for the host, or anything the transparency panel did not disclose.

### Q6. First buyer: team lead, HR or L&D

**Recommendation: target the team lead (or equivalent meeting owner) as the first user, with L&D/training facilitators as the second-wave paying buyer hypothesis. Do not lead with HR.**

| Buyer | Strengths | Risks | Feature priority it implies |
|-------|-----------|-------|----------------------------|
| **Team lead / meeting owner** | Feels the problem directly, decides alone, no procurement, can run a real meeting within days. This is what the phase 1 gate needs. | Small budgets, hard to monetize alone | Fast setup, quiet defaults, simple report, host controls |
| **L&D / training facilitator** | Runs long sessions (2 hours is routine), actively wants engagement, content-driven (quiz on session material), recognizes a budget line | Wants more content tooling and completion tracking, which pulls toward individual tracking | Custom question content, reusable templates, session recap |
| **HR** | Cross-company rollout, culture agenda | Reads as surveillance, works councils and privacy scrutiny, would want exactly the individual idle data the product forbids | Cross-meeting aggregates, compliance documentation, SSO (all later) |

**How this changes priorities:** team-lead-first means cutting scope on content authoring and analytics depth, and spending effort on setup speed, quiet defaults and a report a lead will forward. If L&D proves stronger in discovery, content templates and a recap move up. If an HR buyer appears, the individual-data limits become a selling point, not a gap.

**Validation needed:** recruit the 5 phase 1 hosts across at least two of these three profiles, and ask each who would pay and from what budget.

## 5. Scope

### In scope for phase 1
- Web app, mobile-browser first, desktop second-window supported.
- Host room creation, game controls, dashboard, agenda break points, post-meeting report.
- Attendee join via link and display name, collapsible side panel, own score, team leaderboard.
- Four games (Section 4, Q2), transparency panel, pause/stop-all.
- Interaction-signal analytics only.

### Out of scope for phase 1
- Meeting bot: live transcript, speaker timing, auto-pause when a name is called, "who has not spoken" nudges.
- Native Zoom/Teams/Meet add-ons.
- On-camera games.
- Zoho-specific integration.
- Any camera, microphone or face-based tracking (permanently out per P5, not only for phase 1).
- Cross-meeting analytics, org-level dashboards, SSO, billing.

## 6. User flows

### Host flow
1. **Create:** name, duration, optional expected headcount, optional agenda and break points, optional bingo keywords. Sign in via email link.
2. **Rehearse (optional):** preview attendee view with simulated activity.
3. **Invite:** copy chat message or QR. Post in meeting chat.
4. **Run:** watch room pulse and reach. Use pause-all, start pulse check, start/end break block. Accept or dismiss nudges. Mark break points as the agenda moves.
5. **Break block:** host starts, room sees the game, live leaderboard, host ends or it times out, panel returns to ambient.
6. **End:** host ends the meeting. A "wrap-up" screen shows the team highlights, and optionally a final prediction resolves.
7. **Review:** report by email and link. One-minute host feedback form.

### Attendee flow
1. **Join:** open link, enter a display name (pre-filled option, no account). Short plain-language notice: what this is, optional, what the host can see.
2. **Land:** a collapsible side panel. Default view: reactions and bingo card, own score, team score. Everything is optional.
3. **Participate:** tap reactions, mark bingo terms, answer pulse questions (10 to 30 s prompts appear unobtrusively, expire on their own).
4. **Break block:** host-started game appears as a clear invitation, never an auto-takeover. Attendee can decline, and declining is invisible to the host as an individual.
5. **See own data:** own score and contributions, team leaderboard celebrating top contributors, the "What the host can see" panel.
6. **Leave or return:** rejoin on the same device restores their name and score. Post-meeting recap link.

## 7. Prioritized requirements

IDs are stable for the plan step. Priorities: **P0** = needed to meet the gate, **P1** = strongly improves the gate meetings, **P2** = later in phase 1 or deferred.

### Host and room
| ID | Requirement | Pri |
|----|-------------|-----|
| H1 | Create a room in under 3 minutes with sensible defaults (light mode) | P0 |
| H2 | One-tap copy of chat invite text plus link, QR code for phones | P0 |
| H3 | Pause-all control, always visible, takes effect for everyone immediately | P0 |
| H4 | Start/end break block; host must trigger it, never automatic | P0 |
| H5 | Start a pulse check (host types a question or picks a saved one) | P0 |
| H6 | Agenda with host-markable break points | P1 |
| H7 | Rehearsal mode with simulated attendees | P1 |
| H8 | Host can set which game tiers are allowed in the meeting (ambient only / + micro / + breaks) | P0 |
| H9 | Remove a participant or reset a display name (moderation) | P1 |
| H10 | Saved question and keyword packs, reusable across meetings | P2 |

### Dashboard
| ID | Requirement | Pri |
|----|-------------|-----|
| D1 | Room pulse in three bands with a sparkline, over offered-prompt denominators | P0 |
| D2 | Reach: joined vs. expected (clearly labeled as adoption, not engagement) | P0 |
| D3 | Single suggested-nudge card, room-level, with a reason, dismissible | P1 |
| D4 | Minimum group size rule hides counts below threshold | P0 |
| D5 | Dashboard states what it cannot see (speaking, non-users) | P0 |
| D6 | No per-person idle or non-participation data anywhere in the UI, API or export | P0 |

### Attendee
| ID | Requirement | Pri |
|----|-------------|-----|
| A1 | Join by link with display name only; works on mobile browsers | P0 |
| A2 | Collapsible side panel, quiet by default (no sound, no forced focus) | P0 |
| A3 | Own score and team leaderboard that celebrates top contributors | P0 |
| A4 | "What the host can see" transparency panel | P0 |
| A5 | Rejoin on same device restores identity | P1 |
| A6 | Accessible: not color-only, readable on small screens, reduced-motion respected | P1 |
| A7 | Option to appear as "a teammate" on the leaderboard instead of by name | P2 |

### Games
| ID | Requirement | Pri |
|----|-------------|-----|
| G1 | Reactions + room mood (ambient) | P0 |
| G2 | Buzzword bingo with host keywords (ambient) | P0 |
| G3 | Pulse/quick trivia and "will this run over?" prediction (micro) | P0 |
| G4 | Team trivia round with live leaderboard (break block) | P0 |
| G5 | Reaction race (micro) | P2 |
| G6 | Jigsaw, co-op word game, Pictionary, tournament | P2 (post-gate) |

### Report
| ID | Requirement | Pri |
|----|-------------|-----|
| R1 | Timeline, reach, results and highlights delivered after the meeting | P0 |
| R2 | Plain-language host observations tied to timing | P1 |
| R3 | Attendee-safe version of the report | P1 |
| R4 | "What this report cannot see" statement | P0 |

## 8. Success metrics

### Gate (must-have)
- **5 hosts each run a real meeting.** "Real" means: at least 30 minutes, at least 4 attendees, an actual agenda and an actual team (not a demo, not the builders' own team), at least 3 of the hosts outside the founders' direct circle.

### Quality signals measured across those meetings
| Metric | Target to treat as a positive signal | Why |
|--------|--------------------------------------|-----|
| Time from landing to live room | under 3 min for 4 of 5 hosts | Validates effortless setup |
| Reach (joined / expected) | 50% or more average | Link-in-chat joining works without a bot |
| Joined attendees who interact at least once | 60% or more | The games are worth opening |
| Joined attendees active in the last third of the meeting | 40% or more | Engagement holds in long meetings |
| Attendees reporting the app distracted them from the meeting | under 15% (one-question post-meeting poll) | P1 is honored |
| Attendees who open the transparency panel | tracked, no target | Learn whether trust needs more work |
| Host uses pause-all at least once or confirms they knew where it was | tracked | Control feels real |
| Hosts who say they would run it again | 4 of 5 | Core product-market signal |
| Hosts who actually schedule a second meeting within 2 weeks | 3 of 5 | Behavior beats stated intent |
| Complaints of "being watched" | zero | Guards the trust premise |

### Learning objectives (qualitative)
- Do ambient games alone carry the value, or do break blocks matter?
- Do hosts read and act on nudges?
- Who in the room joins first and who does not (profile only, never individual)?
- Which of the three buyer profiles shows the strongest pull?

## 9. Risks and assumptions

| Risk | Mitigation |
|------|-----------|
| Second-window joining is too much friction in a full meeting | Phone-first design, QR code, one sentence in the invite, measure reach early |
| Attendees read it as surveillance | Transparency panel, positive-only individuals, no idle lists, explicit "cannot see" statements, plain-language notice on join |
| Games distract from the speaker | Quiet default, host-gated tiers, pause-all, expiring prompts, distraction poll |
| Without a bot the dashboard feels empty or misleading | Honest framing (reach vs. responsiveness), offered-prompt denominators, limits stated in the UI |
| Small meetings make aggregates identifying | Minimum group size rule |
| Display name abuse with no signup | Host removal and rename tools, fixed emoji set, no free text in ambient games |
| Privacy law and works-council scrutiny in some regions | Data minimization, stated retention period, no personal data beyond display name and device token, document before the 5 hosts start |
| Assumption: hosts can enter keywords and questions quickly enough | Saved packs, default packs, measure host prep time |

## 10. Remaining open questions

1. **Host identity.** Is an email magic link acceptable for hosts, or must even hosts need no signup? This affects report delivery and abuse control.
2. **Content for bingo and trivia.** Ship built-in default packs (which topics, whose review for tone), or require host input from day one?
3. **Scoring design.** How do ambient reactions, bingo, pulse answers and trivia combine into one score without rewarding spam? How do we cap reaction points?
4. **Leaderboard naming.** Named by default or opt-in? Celebration vs. social pressure may vary by company culture. Recommend named by default with an easy opt-out, to be tested.
5. **Attendee data retention.** How long are display names, scores and per-meeting data kept, and can an attendee delete their own record?
6. **Minimum group size.** Is 5 the right threshold, and how should rooms below it behave (qualitative only, or dashboard off)?
7. **Nudge rules.** Which room-level signals are reliable enough to trigger nudges in the first release, and what is the cooldown so nudges do not nag?
8. **Host-reported speaking.** Should the host have an optional manual way to note "invited X's view" for the report, or is that too close to individual tracking? Current lean: no, leave for phase 2.
9. **Multi-host and co-host.** Can a co-host or the meeting organizer share the host view? Needed for all-hands and training sessions.
10. **Recording the link in chat.** Some tools strip or block links, and some companies block unknown domains. How much do we test across Meet, Zoom, Teams and Zoho chat before the gate?
11. **Pricing hypothesis.** Free for the first 5 hosts is assumed. When and how is willingness to pay tested?
12. **Prediction game resolution.** "Will this run over?" needs the host to confirm the real end time. Is that one extra tap acceptable?

## 11. Next step

Review this document, resolve open questions 1, 3, 4 and 5 (they shape the plan most), then move to the plan step for architecture and sequencing. No stack or implementation choices have been made here.
