# Executive Stakeholder Demo & Productization Workshop

**Product:** Veridian IT Support Agent — a multi-agent internal helpdesk assistant
(OpenAI Agents SDK) at the end of a 6-week pilot.
**Question on the table:** does it move from prototype to productized release?

## → [**executive-summary.md**](executive-summary.md) ←

One page. The recommendation is **launch with conditions**.

---

## How to review these artifacts

Read in this order — it takes about fifteen minutes.

| # | Artifact | What it is | Read for |
|---|---|---|---|
| 1 | [**executive-summary.md**](executive-summary.md) | one page, the recommendation | the decision and the five conditions |
| 2 | [**demo-deck.html**](demo-deck.html) | the presentation artifact — 11 slides, self-contained, open in any browser | what the room was shown |
| 3 | [**demo-script.md**](demo-script.md) | the 7-minute script, timed, with delivery notes | what was said over each slide, and the workshop agenda |
| 4 | [**feedback-log.md**](feedback-log.md) | captured live during the workshop | decisions, objections, questions, 9 dated actions |
| 5 | [**productization-plan.md**](productization-plan.md) | launch scope → release criteria → onboarding → metrics → support → ops → risks → backlog | whether this is actually releasable |

**Demo artifact:** `demo-deck.html` is the durable artifact in place of a recording — it is a
single file with no external dependencies, so it renders identically in five years.
Download and open it, or view it through
[htmlpreview](https://htmlpreview.github.io/?https://github.com/pavansunkara958/stakeholder-demo-productization/blob/main/demo-deck.html).
The demo itself ran live in staging on anonymized real tickets; `demo-script.md` §0 lists
the environment and the recorded fallback.

### The trace to follow

Each artifact feeds the next, and that chain is the point:

```
demo  →  objection O1  →  action A3  →  risk row 1  →  backlog item 4
        ("volunteers")   (re-baseline)   (likelihood    (funded, above
                                          HIGH)          the launch line)
```

A feedback log that only records agreement means the demo was a presentation, not a review.

---

## The three things this set argues

### 1 · A demo that shows a failure you chose is believed about everything else

Flow C in the script is a German-language ticket that the agent correctly refuses to handle.
It is on screen deliberately. 31% of Veridian staff are in Benelux and DACH, and that limit
is what shapes the launch cohort — so a demo that hid it would have produced a launch
decision made on a false scope.

### 2 · The pilot's best number is reported as its weakest

Containment was **61%**, against a 55% target. It is in the summary table *and* flagged in
the same document as measured on an opt-in cohort — so it is a pilot observation, not a
forecast, and everything downstream depends on a re-baseline that has not happened yet.

The objection that produced that (O1, from the Finance BP) is the most valuable thing in the
feedback log. Carrying 61% into a business case unchanged would have been a silent lie.

### 3 · Containment is the headline metric and the most gameable one

A ticket closed by an agent that did not help still counts as contained. So **reopen rate**
and **escape-hatch rate** sit on the same dashboard panel as containment, not in an
appendix. An adoption metric with no counter-metric measures enthusiasm, not value.

---

## Frameworks used

| Framework | Where |
|---|---|
| **SAFe System Demo** | demo format — the *integrated* increment, which is what a release decision needs; Sprint Review shows iteration output instead |
| **Scrum Guide, Sprint Review** | workshop structure: inspect the increment, adapt the backlog, in a timebox |
| **Prosci ADKAR** | onboarding plan, plan §3 — one measurable signal per stage |
| **Google HEART** | adoption metrics, plan §4 — plus three counter-metrics |
| **Aha! launch checklist** | release criteria, plan §2 — ten binary gates checked at go/no-go |

- https://framework.scaledagile.com/system-demo/
- https://scrumguides.org/scrum-guide.html
- https://www.prosci.com/methodology/adkar
- https://research.google/pubs/measuring-the-user-experience-on-a-large-scale-user-centered-metrics-for-web-applications/
- https://www.aha.io/roadmapping/guide/release-management/what-is-a-good-product-launch-checklist

---

*Veridian Group is a composite enterprise used throughout this course. Ticket volumes,
pilot results and stakeholder names are illustrative and internally consistent across all
five artifacts.*
