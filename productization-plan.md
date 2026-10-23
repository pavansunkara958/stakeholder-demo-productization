# Productization Plan — Veridian IT Support Agent

From pilot to productized release. Built from the workshop output in
[feedback-log.md](feedback-log.md); every action here traces to an item there.

---

## 1 · Launch scope

**In scope at launch (16 Nov):**

| Intent | Volume share | Containment target |
|---|---|---|
| Password reset, standard accounts | 17% | 70% |
| Group membership, non-privileged | 12% | 55% |
| Software install from the approved catalogue | 9% | 60% |

**Explicitly out of scope, and why:**

| Excluded | Reason |
|---|---|
| MFA reset | account-takeover vector; L2-gated, deferred by CISO decision (O2) |
| Privileged group membership | requires the ServiceNow integration (C1) to be more than a manual relay |
| Dutch, German | unsupported; routed to the service desk (C3) |
| Hardware faults, VPN | not piloted — no evidence |
| `remote_wipe`, P1 declaration | **not a tool the agent has**, at any stage |

Scope is defined by *what was measured*, not by what the system can technically do. An
intent with no pilot data is an assumption, and assumptions do not belong in a launch scope.

---

## 2 · Release criteria

Launch is permitted only when **all** of the following hold. These are binary, measured, and
checked at the go/no-go on 13 November.

| # | Criterion | Measure | Owner |
|---|---|---|---|
| R1 | Approval integration live | 20 consecutive approvals round-trip through ServiceNow with no manual step | Platform |
| R2 | Token verification failures alarmed | synthetic bad token raises a SOC alert within 60 s | Platform + SOC |
| R3 | Entitlement freshness | sync lag ≤ 15 min, measured over 48 h | Identity |
| R4 | Eval suite green | 24/24 cases, 21/21 checks on the release build | Delivery |
| R5 | Routing accuracy | ≥ 90% on the held-out set | Delivery |
| R6 | Guardrail FP rate | < 5% over the final pilot week | Delivery |
| R7 | After-hours drill | one live escalation, signed off by on-call lead | Ops |
| R8 | Kill switch | agent disabled in < 60 s, traffic returns to the existing queue, rehearsed | Platform |
| R9 | Runbooks | 5 runbooks reviewed by the people who will be paged | Ops |
| R10 | Language routing | non-English tickets route to the service desk, 0 false negatives in 100 samples | Delivery |

**R2 and R8 are the two that are easy to skip and expensive to have skipped.** A control
nobody has seen fail is a control nobody has tested, and a kill switch that has never been
pulled is a hypothesis.

---

## 3 · Target users and onboarding (Prosci ADKAR)

**Launch cohort:** 1,200 employees in Finance, Legal and Corporate Functions. Chosen because
they are English-first, high ticket volume per head, and *not* the pilot volunteers — which
is the point of A3.

| ADKAR stage | What we do | Evidence it worked |
|---|---|---|
| **Awareness** | Email from the CIO, not from IT. Names the three things it does and the two it does not. | open rate > 60% |
| **Desire** | Lead with the 4.2h → under-a-minute change; no efficiency language, which reads as a threat | first-week unique users > 35% of cohort |
| **Knowledge** | One 90-second video, one page of examples. No training session — a tool that needs a class has an interface problem. | — |
| **Ability** | Available in the existing Teams channel employees already use. No new app, no new login. | task success ≥ 85% |
| **Reinforcement** | Week-4 note with real numbers, including what it got wrong | week-8 usage ≥ week-2 usage |

**The 'get me a human' escape is on every message.** Making the exit obvious is what makes
the entrance safe — people try a tool they can leave.

---

## 4 · Adoption metrics (Google HEART)

| HEART | Metric | Target | Source |
|---|---|---|---|
| **Happiness** | post-resolution CSAT | ≥ 3.6 (baseline parity) | in-chat prompt |
| **Engagement** | tickets per active user per month | ≥ 1.4 | telemetry |
| **Adoption** | unique users in first 4 weeks | ≥ 45% of cohort | telemetry |
| **Retention** | week-8 users who also used in week 2 | ≥ 60% | telemetry |
| **Task success** | **containment** — resolved with no human touch | re-baselined in wk 1–2, then ≥ 50% | trace analysis |

Plus three counter-metrics, because adoption metrics alone can all improve while the product
gets worse:

| Counter-metric | Threshold | Why |
|---|---|---|
| **Escape-hatch rate** (user asks for a human mid-flow) | < 15% | rising usage with rising escapes means people are being forced through it |
| **Reopen rate** (same user, same issue, < 48 h) | < 8% | containment counts a closed ticket, not a solved problem |
| **Routing-mix drift** vs baseline | alarm on shape change | silent misrouting — **every RED metric improves when it happens** |

**Containment is the headline and also the most gameable number in this document.** A ticket
closed by an agent that did not help is counted as contained. That is why reopen rate sits
next to it on the same dashboard panel, not in an appendix.

---

## 5 · Support model

| Tier | Who | Handles | Target |
|---|---|---|---|
| 0 | the agent | the three in-scope intents | — |
| 1 | service desk | anything escalated; agent-escalated tickets arrive with a redacted transcript attached | unchanged SLA |
| 2 | service desk L2 | approval review (0.5 FTE, D3) | approvals within 1 h in business hours |
| 3 | platform team | runtime, model, integration failures | P2 within 4 h |
| — | SOC | approval-token verification failures only | P1, 15 min |

**Agent-escalated tickets must not look different in the queue.** If they do, the service
desk forms an opinion about "the AI tickets" rather than about the tickets. They carry the
transcript as an attachment and nothing else.

---

## 6 · Operations

| | |
|---|---|
| Service owner | IT Service Delivery (R. Okonjo) — owns scope, metrics, the stop rule |
| Runtime owner | Platform (K. Reiss) — owns deploys, alerts, the kill switch |
| On-call | existing platform rotation; agent alerts route there, no new rota |
| Deploy cadence | weekly, behind the flag; eval suite gates every deploy |
| Model changes | version pinned; an upgrade is a change request with a full eval run |
| Telemetry retention | traces 30 days, metrics 13 months, approval records 7 years |
| Weekly review | containment, reopen rate, guardrail FPs, routing mix — 30 min, standing |

**9 alerts, 5 runbooks**, carried over from the observability work. Each runbook was reviewed
by the person who will actually be woken by it; a runbook written by the author of the system
tends to assume the author's knowledge.

---

## 7 · Risks, dependencies, mitigations

| Risk | Likelihood | Impact | Mitigation | Residual |
|---|---|---|---|---|
| **Containment falls sharply on a non-volunteer cohort** (O1) | **High** | Medium | re-baseline in wk 1–2; business case restated as capacity released (A7) | Medium |
| Approval integration slips past 7 Nov | Medium | High | launch date moves; manual relay is **not** an acceptable launch state (O3) | Low |
| Stale entitlements expose restricted policy | Low | High | C2: 15-min sync, else public-tier content only | Low |
| Prompt injection reaching a privileged tool | Low | Critical | tool-layer approval, signature-bound, verified server-side; worst case is a declined *request* | Low |
| Service desk disengages ("it's IT's robot") | Medium | Medium | A9 training; agent tickets indistinguishable in the queue | Medium |
| Single-region outage | Low | Medium | kill switch returns traffic to the existing queue in < 60 s | **Accepted** |
| Model vendor deprecates the pinned version | Medium | Medium | eval suite gates the upgrade; 2-week notice monitoring | Low |
| Cost growth with volume | Low | Low | per-ticket budget, tiered models, cost alarm | Low |

**Dependencies outside the team:** ServiceNow platform team (A1), Identity directory sync
(A2), SOC alert routing (R2), HR Ops comms slot (A8). Three of the four blocking conditions
depend on a team that does not report to this project — which is the real schedule risk, not
the engineering.

---

## 8 · Prioritized backlog

Ordered by value against effort. Everything above the line is funded; below the line is
candidate work.

| # | Item | Value | Effort | Why this order |
|---|---|---|---|---|
| **1** | ServiceNow approval integration (C1) | blocking | M | nothing privileged ships without it |
| **2** | Entitlement sync ≤ 15 min (C2) | blocking | M | security residual, raised by the CISO |
| **3** | After-hours drill + kill-switch rehearsal (C4, C5) | blocking | S | cheap; the cost of skipping is an outage with no rehearsed exit |
| **4** | Re-baseline containment (A3) | high | S | every forecast downstream depends on it |
| **5** | Reopen-rate instrumentation | high | S | containment is not trustworthy without it |
| ─ | ─ *launch line* ─ | | | |
| 6 | Dutch + German support (C3) | high | L | unlocks 31% of staff; largest single expansion |
| 7 | MFA reset with dual approval | high | M | highest-volume remaining intent, highest risk — sequenced after C1 is proven |
| 8 | VPN + device intents | medium | M | needs its own pilot; no data yet |
| 9 | Self-service onboarding for new cohorts | medium | S | removes Delivery from every expansion |
| 10 | Multi-region failover | medium | L | parked (P3) until the service is load-bearing |
| 11 | HR / Facilities expansion | low now | L | parked (P2) until 8 weeks of IT-only operation |

**Item 7 is deliberately not item 6.** MFA reset is the biggest remaining containment win and
the single worst thing to get wrong. It waits until the approval integration has run in
production for a full cycle, because a control that works in staging is a control that has
not yet met real traffic.

---

## 9 · Benefit note

At pilot containment, in-scope volume represents roughly **€560k/year** of deflected handling
cost at €6.80 per human-handled ticket.

That number is a **ceiling on the opportunity, not a committed saving**, for three reasons:
pilot containment was measured on volunteers (O1), the launch cohort is 1,200 of 28,000
people, and the benefit is realized as capacity released rather than cost removed (D5). The
honest statement to Finance is: *the service desk absorbs more volume without growing*, and
that is what gets reported at week 8.

---

## References

- SAFe System Demo — https://framework.scaledagile.com/system-demo/
- Scrum Guide, Sprint Review — https://scrumguides.org/scrum-guide.html
- Prosci ADKAR — https://www.prosci.com/methodology/adkar
- Google HEART — https://research.google/pubs/measuring-the-user-experience-on-a-large-scale-user-centered-metrics-for-web-applications/
- Aha! product launch checklist — https://www.aha.io/roadmapping/guide/release-management/what-is-a-good-product-launch-checklist
