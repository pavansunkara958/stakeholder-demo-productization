# Executive Summary — Veridian IT Support Agent

**To:** Steering group (CIO, Head of IT Service Delivery, CISO, Finance BP, HR Ops)
**From:** Delivery team · **Date:** 22 October 2026 · **Decision requested:** go/no-go for productized release

---

## Recommendation: **LAUNCH WITH CONDITIONS**

Release to **1,200 users (Finance, Legal, Corporate Functions)** on **16 November**, limited
to the three intents proven in pilot. Five conditions must close first; four are in flight.

**Not "ready to launch"**, because the approval workflow still depends on a human copying a
token between ServiceNow and the agent — the control works, the integration does not.
**Not "not ready"**, because the containment, quality and safety evidence is measured on real
tickets, not projected.

---

## What the pilot proved

Six weeks, 400 users, **1,180 real tickets** across password resets, group membership and
software installs — 38% of Veridian's ticket volume.

| | Pilot | Baseline | Target |
|---|---|---|---|
| Resolved without a human | **61%** | — | 55% |
| Routing accuracy (24-case eval) | **94%** | — | ≥ 90% |
| p95 response latency | **8.4 s** | 4.2 h first response | < 15 s |
| Cost per handled ticket | **€0.04** | €6.80 | < €1.00 |
| Guardrail false-positive rate | **3.1%** | — | < 5% |
| CSAT (HEART · Happiness) | **4.3 / 5** | 3.6 / 5 | ≥ 3.6 |
| Unauthorized privileged grants | **0** | — | 0 |

Annualized at pilot containment, in-scope volume represents **~€560k/year** of deflected
handling cost. That figure is a *ceiling on the opportunity*, not a committed saving —
see the productization plan's benefit note.

## What is not done

| Gap | Impact | Condition |
|---|---|---|
| ServiceNow approval integration is manual | privileged requests take 4h+ and need a human relay | **C1 — blocking** |
| Entitlement data is a nightly snapshot | up to 24h stale on the Knowledge agent | **C2 — blocking** |
| Dutch and German not supported | 31% of staff; excluded from scope at launch | C3 — scope limit |
| After-hours paging never exercised live | unknown on-call behaviour | **C4 — blocking** |
| Single-region deployment, no failover | outage = full fallback to the service desk | C5 — accepted, documented |

## The five conditions

1. **C1** — ServiceNow approval integration live, with token verification failures alarmed to the SOC. *Owner: Platform · 7 Nov*
2. **C2** — entitlement sync at ≤ 15 min lag, or the Knowledge agent ships read-only against public-tier content only. *Owner: Identity · 7 Nov*
3. **C3** — language detection routes non-English tickets to the service desk, measured weekly. *Owner: Delivery · 11 Nov*
4. **C4** — one live after-hours escalation drill, signed off by the on-call lead. *Owner: Ops · 11 Nov*
5. **C5** — documented fallback: feature flag disables the agent in < 60 s and all traffic returns to the existing queue. Rehearsed once. *Owner: Platform · 13 Nov*

## Decision asks

- Approve conditional launch to 1,200 users on 16 Nov, three intents only
- Approve 0.5 FTE service-desk L2 for 8 weeks as approval reviewer
- Agree the stop rule: **unauthorized privileged grant > 0, or CSAT < 3.6 for two consecutive weeks → the flag goes off, no further discussion required**

---

*Evidence: [demo-script.md](demo-script.md) · [feedback-log.md](feedback-log.md) ·
[productization-plan.md](productization-plan.md)*
