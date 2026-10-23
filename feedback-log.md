# Stakeholder Feedback Log

**Session:** Executive demo + productization workshop · 22 October 2026 · 60 min
**Attendees:** CIO (M. Haugen), Head of IT Service Delivery (R. Okonjo), CISO (L. Brandt),
Finance BP (S. Petrova), HR Ops lead (T. Vermeulen), Delivery lead (scribe)

Captured live during the session. Every item is classified as **Decision**, **Action**,
**Objection** or **Parked** — anything that is none of those four was noise and is not here.

---

## Decisions

| # | Decision | Made by | Note |
|---|---|---|---|
| D1 | Conditional launch approved — 1,200 users, three intents, 16 Nov | CIO | contingent on C1, C2, C4 closing |
| D2 | Launch cohort is Finance, Legal, Corporate Functions (English-first) | CIO + HR Ops | explicitly excludes Benelux/DACH until C3 |
| D3 | 0.5 FTE L2 approval reviewer funded for 8 weeks | Head of Service Delivery | reviewed at week 8, not open-ended |
| D4 | **Stop rule agreed:** any unauthorized privileged grant, or CSAT < 3.6 for two consecutive weeks → feature flag off, no further discussion | CIO + CISO | CISO asked for this in writing; it is condition C5's acceptance criterion |
| D5 | Benefit is tracked as *capacity released*, not headcount reduction | Finance BP | changed how the business case is reported — see P1 |

---

## Objections

| # | Objection | Raised by | Response | Status |
|---|---|---|---|---|
| O1 | "You are showing me a 61% containment rate on a self-selected pilot group. Volunteers are more tolerant." | Finance BP | Fair. Pilot cohort was opt-in. Launch cohort is not, so containment will likely fall. We will re-baseline in the first two weeks rather than carry the pilot number forward. | **Accepted — A3** |
| O2 | "If the agent resets MFA, that is the exact path an attacker wants. I do not want it in scope." | CISO | MFA reset is already gated behind a different human (service desk L2) and is **not in launch scope**. Confirmed on screen. | **Resolved in session** |
| O3 | "A human copying an approval token between two systems is a workaround, and workarounds become permanent." | Head of Service Delivery | Agreed — this is why C1 is blocking rather than fast-follow. | **Accepted — C1 stays blocking** |
| O4 | "We have been told before that a tool would reduce ticket volume and it did not." | Head of Service Delivery | Not disputed. Mitigation is the weekly containment report against a re-baselined figure, and the stop rule in D4. | **Parked to week-4 review** |
| O5 | "Why is the knowledge agent allowed to read policy documents at all?" | CISO | It searches an index filtered by the **requester's** entitlements, not the agent's. Demonstrated. The residual risk is the 24h staleness of that entitlement data — which is C2. | **Resolved; C2 raised to blocking** |

**O1 is the most valuable thing that happened in the session.** The pilot number was honest
but it was measured on volunteers, and carrying it into a business case unchanged would have
been a silent lie. It is now re-baselined rather than defended.

---

## Questions and answers

| # | Question | Answer |
|---|---|---|
| Q1 | "What happens at 2am when it pages someone wrongly?" | Rate-limited, requires an existing incident, capped at P2. Never exercised live — that is C4. |
| Q2 | "Can an employee tell they are talking to an agent?" | Yes, stated in the first line and in the handoff message. Not configurable. |
| Q3 | "What does it cost at full volume?" | €0.04/ticket at pilot mix; ~€8.7k/year at 4,200 tickets/week if all intents were in scope. Launch scope is a fraction of that. |
| Q4 | "Who owns it after launch?" | IT Service Delivery owns the service; the platform team owns the runtime. Named in the productization plan §6. |
| Q5 | "What if the model vendor changes the model under us?" | Version pinned; eval suite (24 cases, 21 checks) gates any upgrade. |
| Q6 | "How do we handle someone who hates it?" | Every conversation has a one-click 'get me a human' path that bypasses triage entirely. |

---

## Actions

| # | Action | Owner | Due | Blocking launch? |
|---|---|---|---|---|
| A1 | ServiceNow approval integration + SOC alarm on token verification failure | Platform (K. Reiss) | 7 Nov | **Yes — C1** |
| A2 | Entitlement sync ≤ 15 min, or Knowledge agent restricted to public-tier content | Identity (A. Dufour) | 7 Nov | **Yes — C2** |
| A3 | Re-baseline containment on a non-volunteer cohort in weeks 1–2; report against the new figure | Delivery | 27 Nov | No — reporting change |
| A4 | Language detection → service desk routing, with a weekly count | Delivery | 11 Nov | No — scope limit, C3 |
| A5 | One live after-hours escalation drill, signed off by on-call lead | Ops (J. Mbeki) | 11 Nov | **Yes — C4** |
| A6 | Rehearse the kill switch end to end; document < 60s disable | Platform | 13 Nov | **Yes — C5** |
| A7 | Rewrite the business case as capacity released, not FTE saved | Finance BP | 30 Oct | No |
| A8 | Onboarding comms pack (ADKAR Awareness + Desire) for the 1,200 cohort | HR Ops | 10 Nov | No |
| A9 | Service desk training: how to recognise and handle an agent-escalated ticket | Service Delivery | 12 Nov | No |

---

## Parked

| # | Item | Revisit |
|---|---|---|
| P1 | Headcount implications of sustained containment | Q1 2027, after re-baselined data exists |
| P2 | Extending to HR and Facilities tickets | after 8 weeks of IT-only operation |
| P3 | Multi-region failover | roadmap, not launch |
| P4 | Voice / phone channel | out of scope indefinitely |

---

## Scribe's note

Two items changed the plan materially rather than merely being recorded:

- **O1 → A3.** The 61% containment figure survived the room, but only as a pilot
  observation, not as a forecast. Every downstream number now depends on a re-baseline
  that has not happened yet.
- **O5 → C2 promoted to blocking.** Entitlement staleness was a fast-follow before the
  session. The CISO's question about read scope is what moved it.

A feedback log that only records agreement means the demo was a presentation, not a review.
