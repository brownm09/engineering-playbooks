# Engineering OKR Framework

## Leadership Context

OKRs are one of the most frequently adopted and most frequently broken planning tools in engineering organizations. When they work, they create a direct line from an IC's quarterly work to a company-level outcome, make accountability legible at every level of the org, and give engineering leaders a credible answer when executives ask "what is engineering doing and why does it matter?" When they fail — which is most of the time — they become a performance theater exercise that consumes three weeks of Q1 planning and is forgotten by April. This playbook covers the mechanics and judgment calls that determine which outcome you get.

## When to Use This

- Annual or quarterly planning cycle is underway and OKRs need to be set, refined, or re-anchored to company priorities
- A new engineering leader is inheriting OKRs that no one owns, no one checks, and no one grades
- Post-Q1 check-in reveals that OKRs were set but not reviewed — the "set and forget" failure mode is active
- An executive or board member asks engineering leadership to explain how engineering work connects to company strategy

---

## The Two OKR Failure Modes

Before writing a single OKR, name the two failure modes and check for them explicitly.

### Failure Mode 1: Activity OKRs (We Will Ship X)

Activity OKRs describe what the team will do, not what will change as a result. They are the most common failure mode because they are easy to write and easy to grade — if the thing shipped, it is a 1.0.

**Example (broken):**
> Objective: Improve our infrastructure
> KR1: Migrate 12 services to Kubernetes by March 31
> KR2: Complete the database upgrade project
> KR3: Document all runbooks

These are project milestones. They belong in a project plan. They are not OKRs.

**Why they are dangerous:** A team can score 1.0 on every activity OKR and still have made no progress on the business problem that motivated the work. The Kubernetes migration is complete, but page load time did not improve. The database upgrade is done, but checkout error rate is unchanged. Activity OKRs measure effort, not impact.

**How to fix them:** For every "we will ship X," ask: "What will be true after X ships that is not true now, and how will we measure it?" The answer to that question is the Key Result.

---

### Failure Mode 2: Aspiration Without Measurement

The opposite failure: the KR sounds impactful but has no measurement mechanism.

**Example (broken):**
> KR: Significantly improve platform reliability

"Significantly" is not a number. Without a baseline and a target, this KR cannot be graded, which means it cannot hold anyone accountable, which means it will be ignored.

**How to fix it:** Define the baseline metric, the target value, and the measurement method. "Reduce P0 incident frequency from 4/month to 1/month, measured by the incident log, by March 31."

---

## OKR Hierarchy: What Lives at Each Level

### Company Level

Company OKRs are set by the CEO and exec team. They describe the most important outcomes for the business in the next quarter or year. Engineering may inform them but does not own them.

Examples of well-formed company-level objectives:
- Grow net revenue retention from 105% to 115%
- Expand into two new enterprise verticals with at least three design partners each
- Achieve SOC 2 Type II certification

Engineering's job with company OKRs: understand them well enough to connect team-level work to them, and to push back when a company-level commitment requires engineering work that is not in the plan.

---

### Engineering Org Level

Engineering org OKRs are owned by the VP or Director of Engineering. They describe what the engineering organization will accomplish — not just ship — in the quarter, and they connect directly to company-level outcomes.

A well-formed engineering org OKR:
- Connects to a company OKR (explicitly — name it)
- Is measurable at the end of the quarter
- Is at a level of abstraction that makes sense for the org, not for a single team

**Example:**

> Company OKR: Achieve SOC 2 Type II certification
>
> Engineering Org Objective: Build the infrastructure and evidence trail required for SOC 2 Type II certification
>
> KR1: 100% of production systems have audit logging enabled, confirmed by a third-party audit firm pre-scan by March 15
> KR2: Mean time to revoke access for a departed employee reduced from 72 hours to 4 hours, measured in the IAM system
> KR3: Zero critical findings in the third-party penetration test scheduled for February

Each KR has a number, a measurement method, and a deadline. None of them describe activities; all describe the state of the world at the end of the period.

---

### Team Level

Team OKRs are owned by the engineering manager, with input from the team. They connect to org-level OKRs and to the specific work that team is best positioned to do.

**The connection test:** For every team KR, the manager should be able to name which org-level KR it supports, in one sentence, without hedging. If they cannot, the team KR is probably a project milestone in disguise.

Team-level KRs should be specific enough that a new team member reading them would know exactly what the team considers success.

---

## How to Write a Good Key Result

A Key Result that cannot answer all five questions below is not ready to commit to:

1. **What changes?** Not "we complete X" but "X moves from A to B."
2. **Who measures it?** There is a named person responsible for tracking this number.
3. **Where does the data come from?** The measurement system exists today or will exist before the measurement period begins.
4. **By when?** Quarter end is the default, but interim checkpoints should be defined for KRs with long lead times.
5. **Who owns it?** One person's name. Not "the team." Not "engineering."

**SMART test:**
- **Specific:** The KR describes a single outcome, not a cluster of activities
- **Measurable:** There is a number
- **Achievable:** A score of 1.0 is possible but not guaranteed — if it is guaranteed, the KR is not ambitious enough
- **Relevant:** The KR connects to an objective that connects to a company priority
- **Time-bound:** The deadline is explicit

---

## Cascade Mechanics

Cascading OKRs is not about translating objectives down line-by-line. It is about alignment — ensuring that what each team is working on connects to what the org is trying to accomplish, without requiring every team KR to be a direct copy of an org KR.

**How to cascade without micromanaging:**

Step 1: Engineering Director shares org-level OKRs with all managers, with the context for why each one was chosen and which company OKR it connects to.

Step 2: Each manager drafts team OKRs independently and writes one sentence next to each KR explaining which org OKR it supports.

Step 3: Director reviews for coverage (are all org OKRs supported by at least one team?) and for conflicts (are any two teams pulling in opposite directions on the same system?).

Step 4: Director does not rewrite team KRs. If a KR is unclear or disconnected, the conversation is: "Help me understand how this KR supports [org OKR]. Can you explain the connection?" That conversation often reveals either a gap in the team's understanding of priorities, or a gap in the director's understanding of what the team actually does.

**Coverage gap vs. conflict:**
- A coverage gap means an org OKR has no team-level work supporting it. Either the org OKR needs a team assigned to it, or it needs to be removed.
- A conflict means two teams are making incompatible assumptions about how a shared system will work. Surface this during cascade, not mid-quarter.

---

## Grading

### The 0.7 Target

Google popularized the idea that a 1.0 score on an OKR means the target was too easy. The engineering interpretation: if every KR scores 1.0 every quarter, the organization is not setting ambitious enough targets. The right calibration is that hitting 0.7 across the board is considered strong performance.

This only works if the grading is honest. A team that inflates its scores to look good destroys the information value of OKRs. The engineering director's job during scoring is to press on scores that look inflated, not to accept them in the name of positivity.

### What to Do With a 1.0

Two questions to ask:
1. Was this a legitimate stretch that we executed exceptionally well? If yes, celebrate it and use it to recalibrate ambition upward next quarter.
2. Was the target set too conservatively? If yes, that is planning feedback, not a performance win. Recalibrate the target for next quarter.

If a team consistently scores 1.0 on every KR every quarter, the targets are too conservative and the planning process needs fixing.

### What to Do With a 0.3

A 0.3 means something significant did not happen. Before attributing this to execution failure, ask:

1. Was the KR still valid at the end of the quarter? Company priorities shift; a KR that was right in January may have been explicitly deprioritized by March. If so, grade it N/A or "deprioritized" rather than 0.3 — penalizing a team for acting on changed priorities is wrong.
2. Was there a blocker that should have been escalated? A 0.3 that was visible in week 4 and not surfaced until scoring is a leadership failure, not just an execution failure.
3. Was the KR unrealistic to begin with? If so, that is a planning failure. Fix the planning process.

A 0.3 that represents genuine execution failure — the team committed, had the capacity, was not blocked, and still did not deliver — warrants a direct conversation about what happened and what changes next quarter.

---

## Quarterly OKR Review Format

**Cadence:** Monthly check-in (30–45 min), with a formal score at quarter end
**Audience:** Engineering director with all managers; managers run an equivalent with their teams
**Owner:** Engineering director drives the check-in; each manager is accountable for their KRs

**Monthly check-in template:**

| KR | Owner | Target | Current | Score (0–1) | Status | Next 30-day action |
|---|---|---|---|---|---|---|
| P0 incident frequency: 4/mo → 1/mo | Platform lead | 1/mo | 2.5/mo | 0.4 | At risk | Root cause the two November incidents; fix alert sensitivity by Dec 15 |
| Checkout error rate: 2.3% → 0.8% | Payments team TL | 0.8% | 1.1% | 0.7 | On track | Ship the payment retry logic fix in sprint 3 |
| Access revocation time: 72h → 4h | Security eng | 4h | 4h | 1.0 | Complete | Maintain; document the process for audit evidence |

**Status definitions:**
- **On track:** Current score and trajectory suggest 0.7+ by quarter end
- **At risk:** Current score and trajectory suggest 0.4–0.7 by quarter end without intervention
- **Off track:** Current score suggests <0.4 by quarter end even with intervention
- **Complete:** KR is at 1.0 and the work is done
- **Deprioritized:** KR was explicitly deprioritized during the quarter due to changed company direction

The monthly check-in is not about explaining why scores are what they are. It is about the "Next 30-day action" column — what will actually change before the next check-in?

---

## Retrospective: What to Learn From OKRs

At the end of each quarter, before setting next quarter's OKRs, run a 30-minute retrospective focused on the OKRs themselves:

**Questions to answer:**
1. Which KRs scored below 0.5? Was this an execution problem, a planning problem, or a changed-priorities problem? Each has a different fix.
2. Which KRs scored 1.0? Were they too easy, or were they genuine stretch achievements?
3. Were there things the team did in the quarter that were not in any KR? If yes, why? Was it unplanned work that should have been anticipated? Was it reactive work that should have been prevented? Was it valuable work that should be in next quarter's OKRs?
4. Were the measurement systems in place? If a KR was hard to grade because the data did not exist or was not trustworthy, that is a setup failure.

**What to celebrate:**
- KRs that scored 0.7–0.9 on a genuinely ambitious target — this is the system working
- KRs where the team surfaced a blocker in week 4 and escalated it, even if the score was low — this is the behavior the system is supposed to incentivize
- KRs that were deprioritized cleanly and transparently when company priorities changed — this is organizational adaptability, not failure

**What not to celebrate:**
- 1.0s on targets that were conservative
- Completing activities that were listed as KRs but did not move any outcome metric

---

## Common Failure Modes

### Too Many OKRs

The optimal number of OKRs for a team is 1–2 objectives with 2–4 key results each. A team with 5 objectives and 15 key results does not have priorities — it has a wish list.

A useful forcing function: every new KR proposed must displace an existing one, or the manager must explain in one sentence why the team has capacity for more than the cap.

### OKRs Set by Committee

OKRs set by a committee of stakeholders with no clear owner produce KRs that are acceptable to everyone and owned by no one. The manager who owns the objective needs to write the first draft. Stakeholders refine. The director approves or asks questions. One name at the end.

### KRs That Measure Output, Not Outcome

"Deploy the new checkout flow" is an output. "Increase mobile checkout conversion from 62% to 70%" is an outcome. The fact that something was deployed is meaningless if it did not change anything in the world.

This distinction matters especially for infrastructure and platform work, where the temptation is to use deployment milestones as KRs. The question is always: what will be better for someone — a user, an engineer, an operator — after this work ships?

### OKRs That Cannot Fail

If every KR is structured as "complete X initiative" and the team controls whether X is complete, the KR cannot fail. It can slip, but slipping is reported as "in progress" not as "failed," which means the accountability mechanism never engages.

OKRs need to be structured so that the world can tell you whether you succeeded, not just your internal retrospective.

### Grading Season Theater

Teams that spend hours debating whether a KR deserves a 0.6 or a 0.7 are wasting the mechanism. Scoring should take 15 minutes per KR. The value is not in the number; it is in the honest conversation that producing the number requires. If grading is taking more than two hours for a full team's OKRs, the KRs are probably not measurable enough.

---

## Templates

### OKR Draft Template (Team Level)

```
**Objective:** [One sentence describing the outcome, not the activity. Should be inspiring 
               but grounded in something real.]

**Connects to:** [Org-level objective name]

**KR1:** [Metric] moves from [baseline] to [target] by [date]
  Owner: [Name]
  Measurement: [How and where this is tracked]
  Confidence: [High / Medium / Low — and one sentence on the primary uncertainty]

**KR2:** [Metric] moves from [baseline] to [target] by [date]
  Owner: [Name]
  Measurement: [How and where this is tracked]
  Confidence: [High / Medium / Low — and one sentence on the primary uncertainty]
```

### Monthly Check-In Prompt (Manager to Director)

A one-paragraph written update submitted 24 hours before the monthly OKR check-in:

```
This month: [What moved, by how much]
At risk: [Which KR is most at risk and why]
What I need: [Any unblock, decision, or resource needed from leadership]
My call: [Whether I expect to be on track, at risk, or off track at quarter end, in one sentence]
```

---

## Implementation Sequence

**Week 1 of a new quarter (OKR setting):**
- Director shares company and org OKRs with managers, with written context
- Managers draft team OKRs independently, due end of week
- Director reviews for coverage, conflicts, and measurement quality

**Week 2:**
- Director holds 30-minute 1:1s with each manager to review their draft OKRs
- Managers refine and finalize team OKRs
- All OKRs published to a shared, accessible location (Notion, Confluence, or equivalent)

**Month 2 check-in:**
- Managers submit one-paragraph written update
- 30-minute group check-in with director and all managers
- At-risk KRs get an explicit recovery action assigned

**Quarter end (grading):**
- Managers submit scores with one-sentence explanation per KR
- 30-minute retrospective on the OKR process itself
- Planning for next quarter begins the following week

---

## A Note on Trust

The OKR system only works if people believe that honest low scores will be treated as information, not as performance failures. An engineering director who responds to a 0.3 with criticism rather than curiosity will get inflated scores next quarter. The question when a KR scores low is: what does this tell us about what we planned vs. what was actually possible? That is a planning question, not a performance question — unless the pattern of low scores persists across multiple quarters with the same owner and the same explanations.

Building that distinction into how you respond to scores is more important than any template in this document.

## Further Reading

| Topic | Resource |
|---|---|
| OKR methodology | Doerr, *Measure What Matters* (Portfolio/Penguin, 2018) |
| OKRs in practice | Google re:Work — [Set Goals with OKRs](https://rework.withgoogle.com/guides/set-goals-with-okrs/) |
