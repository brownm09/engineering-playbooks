# Engineering Rhythm of Business

## Leadership Context

An engineering org without a defined operating cadence makes decisions at the wrong level and at the wrong time. Some decisions do not get made at all. Strategy set in Q1 goes invisible by Q2 because no meeting is designed to surface whether it is still alive; the VP learns about a critical platform risk in the same briefing as the CTO. This playbook defines the meeting and ritual structure that reduces decision latency and gives cross-functional partners a predictable coordination surface. When the cadence holds, surprises shrink and the business gains a reliable picture of engineering health.

## Background and Motivation

This playbook was developed from the operating cadence work at ActBlue Technical Services (2024–2025), where I set and ran the meeting and ritual structure for a platform directorate of approximately 50 engineers across 6 teams. The cadence described here reflects what sustained delivery rhythm looks like in practice at that scale.

## When to Use This

- A new VP or Director is stepping into an existing org and needs to understand what cadence is already in place (and what is broken)
- Post-acquisition integration: two engineering orgs are merging and need a unified operating model
- The org has crossed 30 engineers and ad hoc coordination is failing: meetings proliferate without structure, decisions get made in Slack threads and forgotten
- An engineering Chief of Staff or TPM is being asked to own the operating cadence and needs a reference model

---

## The Three Failure Modes This Cadence Prevents

**Failure mode 1: Decision latency.** Decisions that should take 48 hours take two weeks because there is no standing forum at the right level with the right people. The weekly eng staff meeting exists to fix this.

**Failure mode 2: Altitude mismatch.** Senior leaders are pulled into execution details; team leads are excluded from decisions they need context on. The tiered meeting structure keeps problems at the level where they belong.

**Failure mode 3: Strategy decay.** Quarterly and annual direction-setting happens but there is no mechanism to check whether it is still alive mid-quarter. The monthly metrics review and quarterly retrospective exist to surface decay before it compounds.

---

## Weekly Tier

### Engineering Staff Meeting

**Attendees:** Engineering Director/VP, engineering managers, staff-level tech leads (optional)
**Frequency:** Weekly, 60 minutes
**Owner:** Engineering Director/VP or Chief of Staff

The weekly staff meeting is the primary decision-making forum for engineering leadership. Status is handled async. A topic earns a slot here when it requires a decision or depends on cross-team alignment that cannot happen in a Slack thread.

**Agenda template:**

```
[5 min]  Pulse check — what happened last week that leadership needs to know
[10 min] Blocking items — anything stalled that requires a decision in this room
[15 min] Rotating deep-dive — one team or topic per week (delivery health, architecture concern, 
         incident debrief, etc.)
[15 min] Cross-functional updates — product, design, legal, finance items that affect eng
[10 min] Upcoming — what is shipping or going live in the next two weeks
[5 min]  Actions review — close out last week's actions; confirm owners
```

What does not belong in this meeting:
- Individual sprint status: belongs in team standups
- Technical implementation debates: belong in architecture review or async RFCs
- Performance conversations: belong in 1:1s with HR follow-up as needed

**How to know this meeting is broken:**
- More than 40% of the time is updates with no decision point
- The same topics recur week over week without resolution
- Engineering managers dread attending and send delegates
- Actions are assigned but not tracked or closed

**How to fix it:**
Start by auditing the last four weeks of meeting notes. Categorize each agenda item: decision, alignment, update, or bloat. Move update items to a written pre-read. Eliminate bloat. If more than two items recur across weeks without closing, they represent a broken process somewhere upstream. Surface that explicitly; do not let the meeting absorb the dysfunction.

---

### On-Call Sync

**Attendees:** Current on-call IC, engineering manager on call, platform/SRE lead
**Frequency:** Weekly, 30 minutes (Monday or Wednesday, depending on rotation handoff day)
**Owner:** Platform lead or on-call IC

See also: [On-Call Restructuring Framework](../incident-management/on-call-restructuring-framework.md)

Purpose: handoff the rotation and review prior-week incidents. Alert health and runbook gaps are the standing third item.

**Standing agenda:**
```
[5 min]  Rotation handoff — who is IC, who are the responders, how to reach them
[10 min] Prior week incidents — severity, TTR, postmortem status (complete / scheduled / not yet)
[10 min] Alert health — any alerts that fired and should not have; runbook gaps surfaced
[5 min]  Upcoming risk — planned releases, infrastructure changes, or external dependencies in the next week
```

If there are no incidents from the prior week and no upcoming risk, this meeting can be shortened to 15 minutes or replaced with a written update to a shared channel. Do not run a 30-minute meeting to confirm that nothing happened.

---

### 1:1 Cadence Guidance

The 1:1 is the most important leadership tool for engineering managers, and the one most consistently converted into a status meeting.

**Recommended structure for manager-to-direct-report 1:1s (30–45 min, weekly):**

Do not start with status. Status should be async. The 1:1 is for:
- Development and growth: what is the person working toward; what is getting in the way
- Concerns the person would not raise in a group: org friction, morale signals, interpersonal issues
- Feedback in both directions: manager to report and report to manager
- Strategic context: things the report should know about the direction of the org or team

**Manager-to-manager 1:1s (30 min, biweekly):**
Engineering directors should hold biweekly 1:1s with each of their managers. The agenda is:
- What is one thing that is going well that I should amplify?
- What is one thing that is stuck that you need me to unblock?
- What is one person on your team I should know more about (in either direction)?

**Engineering leader to cross-functional peer 1:1s (30 min, monthly):**
Engineering VP or Director should hold monthly 1:1s with product, design, and data leads. These are relationship meetings. The goal is early warning and trust; coordination happens in cross-functional forums.

---

## Monthly Tier

### Engineering All-Hands

**Attendees:** All engineers, engineering managers, invited cross-functional guests
**Frequency:** Monthly, 60–75 minutes
**Owner:** Engineering Director/VP with CoS support on logistics

The all-hands does two things: gives engineers a view of where the org is going and what its health metrics actually show, and closes the gap between decisions made at the leadership layer and the people executing against them.

**Format:**

```
[10 min] Opening — what is true about the org right now (not what we wish were true)
[15 min] Metrics — 3–5 key health metrics, trend direction, what we are doing about the ones moving wrong
[15 min] Featured team — one team presents what they shipped, what they learned, and what is next
[10 min] Cross-functional update — one partner (product, design, data) gives a 5-minute view from their seat
[10 min] Asks and offers — what leadership needs from the IC layer; what ICs should know leadership is working on
[10 min] Q&A — live and async (Slido or equivalent)
```

What does not belong in the all-hands:
- Long roadmap recaps: belong in written updates or team-level planning sessions
- Performance callouts (positive or negative): recognition belongs in team forums, not all-hands
- Vendor pitches or tooling demos, unless the org is actively deciding on adoption

**Common failure:** The all-hands becomes a leadership broadcast, and engineers stop attending because nothing they care about surfaces. Reserve the featured team slot for ICs presenting their own work. Make Q&A open to pre-submitted and live questions. Every three months, ask in a skip-level or anonymous channel: what do you want to know that you are not being told?

---

### Architecture Review

**Attendees:** Staff engineers, architects, engineering managers of affected teams, relevant product leads
**Frequency:** Monthly, 90 minutes (or as-needed for major changes)
**Owner:** Principal/Staff engineer or architecture working group

Purpose: gate proposed system changes that exceed a defined scope or risk threshold before any team commits to building them. Approvals carry weight; deferred or conditional decisions are expected and acted on.

**Threshold criteria for requiring architecture review:**
- New service or major service decomposition
- Changes to data model that affect more than one team's systems
- Third-party integrations that carry compliance or security implications
- Any change with estimated implementation effort >4 engineer-weeks

**Meeting structure:**
```
[15 min] Proposing team presents: problem, proposed solution, alternatives considered, tradeoffs
[30 min] Questions and feedback from reviewers — structured around: correctness, scalability, operability, security, team burden
[15 min] Decision: approve / approve with conditions / defer for revision
[30 min] Open slot for async RFC reviews or carry-over items
```

Decisions are written and stored in a shared location (Confluence, Notion, or equivalent). A decision that exists only in a meeting recording is not discoverable by the next engineer who needs to understand why the system looks the way it does.

---

### Metrics Review

**Attendees:** Engineering Director/VP, engineering managers, data or analytics partner
**Frequency:** Monthly, 45–60 minutes
**Owner:** Engineering Director/VP or CoS

The dashboards carry the numbers. The metrics review answers what those trends mean for system health and what the org commits to changing.

**Metric categories to cover:**

| Category | Example metrics |
|---|---|
| Delivery health | Cycle time, deployment frequency, change failure rate, MTTR |
| Platform reliability | Error rate by service, p99 latency, uptime vs. SLA |
| Team health | On-call incident load, incident-per-engineer rate, sprint completion rate |
| Technical debt | Open critical/high severity bugs, dependency freshness, test coverage trend |
| People metrics | Attrition rate, open headcount, time-to-fill |

**Structure:**
- Each manager submits a 3-sentence metric summary before the meeting: what moved, which direction, and what is being done
- Meeting focuses on items that are below threshold or trending the wrong way
- For each problem metric: what is the hypothesis, who owns the recovery, what is the target date

Do not spend time discussing metrics that are healthy and stable unless they are about to be stressed by an upcoming change.

---

## Quarterly Tier

### Engineering QBR

**Attendees:** Engineering Director/VP, engineering managers, product VP or CPO, CTO if present
**Frequency:** Quarterly, 120 minutes
**Owner:** Engineering Director/VP with CoS managing prep and logistics

The engineering QBR is a leadership-layer forcing function: a structured accounting of prior-quarter commitments and delivery, followed by next-quarter direction. The meeting is sized for structural problems; achievements that belong in a monthly update email stay out of it.

**What goes in the QBR:**

1. **Delivery recap:** commitments vs. actuals for the quarter. Not a polished slide; an honest accounting. What shipped, what did not ship, and why.
2. **Health metrics:** 90-day trend on delivery, reliability, and team health metrics. Red/yellow/green with commentary.
3. **Capacity and risk:** headcount vs. plan; open roles; technical debt load; risks entering the next quarter.
4. **OKR grade:** score on each key result (0.0–1.0), one-sentence explanation, what was learned.
5. **Next quarter commitments:** what the org is committing to, at what confidence level, with what dependencies.
6. **Asks:** what the engineering org needs from the company to deliver on next quarter's commitments (headcount approvals, cross-functional prioritization, tooling budget, executive decision needed).

**What stays out of the QBR:**
- Sprint-level delivery detail (too granular for this audience)
- Technical architecture debates: belong in architecture review
- Individual performance: belongs in talent reviews

**Pre-read requirement:** A written pre-read covering sections 1–4 is distributed at least 48 hours before the QBR. The meeting is for discussion, not for reading slides aloud.

---

### Planning Kickoff

**Attendees:** Engineering managers, product managers, design leads, data leads
**Frequency:** Quarterly (8 weeks before end of quarter), 2-hour working session
**Owner:** Engineering Director/VP with product VP as co-owner

The planning kickoff opens the next quarter's planning cycle. The goal is shared context on company direction and engineering capacity, with the largest bets identified before detailed planning begins. Commitments come later.

**Working session structure:**
```
[20 min] Company context: product VP presents top company priorities for next quarter
[20 min] Capacity baseline: engineering director presents headcount, known constraints, carry-over commitments
[60 min] Initiative mapping: cross-functional teams map proposed initiatives to capacity in rough T-shirt sizing
[20 min] Dependency identification: what requires legal review, infrastructure work, data availability, or vendor contracts
```

Output: a draft list of initiatives, rough relative priority, and a list of questions to resolve before planning is finalized.

---

### Quarterly Retrospective

**Attendees:** Engineering managers and interested ICs (opt-in)
**Frequency:** Quarterly, 90 minutes
**Owner:** Rotating facilitation; engineering director is a participant, not the facilitator

Sprint retrospectives address team-level friction within a delivery cycle. The quarterly retrospective is for patterns that span teams and compound across quarters, the problems no single sprint ceremony was designed to catch.

**Format:**

Async pre-work (24 hours before): each team submits three inputs on a shared board:
- One thing that worked and should be preserved
- One thing that did not work and should be changed
- One thing that was unclear and should be defined

Meeting:
```
[15 min] Read the board — silent review of all submissions
[40 min] Theme discussion — facilitator groups submissions into 3–5 themes; group discusses root causes
[20 min] Action selection — group picks 2–3 actions to carry into next quarter; assigns owners and success criteria
[15 min] Feedback on the retrospective itself — was it useful? What should change?
```

If the 2–3 actions from last quarter are not reviewed at the start of this one, the process has no credibility with the people who participated in it.

---

## Annual Tier

### Technology Strategy Review

**Attendees:** Engineering leadership (VP, directors, principal engineers), product leadership, CTO
**Frequency:** Annual (Q4, in parallel with business planning)
**Owner:** CTO or VP Engineering with principal engineer input

The session forces a single question: given where the business is going in the next 12–18 months, does the technology platform have the capacity and architecture to support it? The scope is the architectural foundation and the org's capability profile.

**Agenda:**
```
[30 min] Business direction brief — product or strategy team presents where the company is going
[45 min] Platform assessment — where is the system strong; where is it a risk to future business objectives
[30 min] Team capability assessment — where are the skills we have vs. the skills we need
[30 min] Strategic bets — what are 2–3 technology investments we need to make in the next year that are not currently planned
[15 min] Outputs and owners — who writes the strategy memo; who presents it to the executive team
```

Output: a 2–3 page strategy memo that feeds into the annual planning process.

---

### Roadmap Reset

**Attendees:** Engineering and product leadership
**Frequency:** Annual (concurrent with strategy review)
**Owner:** Product VP with engineering VP as co-owner

The roadmap reset is upstream of planning. Where planning produces sprint-level commitments, the roadmap reset produces a 12-month view of bets with honest confidence levels attached.

Each initiative in the roadmap should have:
- A one-sentence problem statement (not a feature name)
- The business metric it is expected to move
- A confidence level (high / medium / low) and the primary uncertainty driving that confidence level
- An owning team and an engineering lead
- A rough quarter when work is expected to begin

The roadmap is a forecast with confidence levels attached. The prior year's roadmap was partially correct, and this one will be too; the reset frames planning around that assumption.

---

### Org Health Survey

**Frequency:** Annual (or biannual for orgs with high change velocity)
**Owner:** Engineering Director/VP with HR partnership

An annual survey covering: clarity of direction, psychological safety, manager effectiveness, career growth, cross-functional collaboration, and on-call/operational load. Not optional; participation should be the norm, not the exception.

Outputs from the survey go into the next quarter's planning cycle as engineering-org inputs. If the survey results do not influence any decision, engineers will correctly conclude that their feedback is performative, and participation will drop.

---

## Decision Accountability Model

Use a DACI (Driver, Approver, Consulted, Informed) framework to define which decisions belong where. The following table maps common engineering-org decisions to the right level.

| Decision type | Driver | Approver | Consulted | Informed |
|---|---|---|---|---|
| Adopt a new primary programming language or framework | Staff engineer | VP Eng | Engineering managers, architects | All engineers |
| Add a service to the production topology | Owning team tech lead | Engineering manager | Platform lead | On-call rotation |
| Change on-call rotation structure | Platform lead | Engineering Director | Engineering managers | All on-call participants |
| Deprecate a service | Owning team tech lead | Engineering manager | Dependent teams | All engineers |
| Approve a headcount request | Engineering Director | VP Eng or CFO | HR, Finance | Hiring managers |
| Commit engineering capacity to a product initiative | Engineering manager | Engineering Director | Product manager | Team |
| Select a vendor for a production system | Lead engineer evaluating | Engineering Director | Security, Finance, Legal | Engineering managers |
| Promote an engineer to staff level | Engineering manager | Engineering Director | Peer staff engineers | Engineering org |

**How to use this table:** When a decision is stuck (either no one is moving it, or everyone is arguing about who should move it), the first question to ask is: who is the Driver? If there is no named Driver, the decision will not move. Assign one before doing anything else.

---

## Meeting Health Principles

**A meeting is broken when:**
- It recurs on the calendar but no one can articulate what decision it produces or what would happen if it were canceled
- The same person speaks more than 60% of the time
- Action items from the previous meeting were not reviewed
- Attendees are present but not engaged (camera off, no contributions, clearly doing other work)
- The meeting could have been a well-written document

**How to audit a meeting:**
At the end of a quarter, pull the last 8 meeting notes for any standing meeting. Ask:
1. What decisions were made in this meeting that could not have been made another way?
2. Which agenda items were updates vs. discussion vs. decisions?
3. Were actions assigned and closed?

If you cannot answer question 1 with at least two concrete decisions, the meeting is a candidate for elimination or restructuring.

**The one-meeting-per-quarter cancellation rule:**
Once a quarter, cancel one standing meeting as an experiment. If someone needs it back, the burden of proof is on them to explain what decision would be lost without it.

---

## CoS Role in Running This Cadence

A Chief of Staff or senior TPM who owns the operating cadence is one of the highest-leverage roles in an engineering org. The responsibilities fall into three phases:

**Preparation:**
- Owns the agenda for the weekly staff meeting: collects inputs from managers 24 hours in advance, sequences items by urgency and decision-type, circulates the agenda the evening before
- Manages the all-hands run-of-show: confirms speakers, collects slides, seeds the Q&A queue
- Drives QBR prep: distributes the pre-read template, chases submissions from managers, assembles the consolidated deck, flags where commitments vs. actuals need an explanation

**During meetings:**
- Takes notes in the staff meeting, capturing decisions and owners in a consistent format
- Time-keeps and cuts discussion that is going past its slot
- Names when a discussion has become circular and surfaces what decision is missing

**After meetings:**
- Publishes action items within 24 hours to a shared channel or doc
- Owns the action register: tracks open items week over week, flags overdue items to the engineering director
- Escalation flags: if an item has been in the action register for more than two weeks without movement, it goes to the director with a recommendation for whether to close, reassign, or escalate

**Escalation judgment:** The CoS is often the first person to see that something is wrong before the director does. That visibility only converts to value if the CoS has a calibrated sense of what needs immediate escalation. One test: if this goes unresolved for 48 hours, does it cost money, or does it generate a compliance or executive surprise? If yes, surface it the same day.

---

## Sample Weekly Calendar: 50-Engineer Org

```
Monday
  9:00 AM   On-call sync (IC, on-call manager, platform lead) — 30 min
  10:00 AM  Engineering staff meeting (managers + staff leads) — 60 min
  
Wednesday  
  10:00 AM  Product × Engineering sync (product + eng managers) — 45 min
  
Thursday
  Various   Engineering manager 1:1s with reports
  
Friday
  2:00 PM   Weekly written update published to #eng-leadership Slack:
            - Top 3 things that shipped
            - Top 3 things that are at risk
            - One metric to watch
```

## Sample Monthly Calendar: 50-Engineer Org

```
Week 1
  Wednesday: Architecture review (staff engineers, affected team leads) — 90 min

Week 2
  Monday:    Metrics review (engineering managers + data lead) — 60 min

Week 3
  All-hands (all engineers, open Q&A) — 75 min

Week 4
  Cross-functional 1:1s (VP Eng with product VP, design lead, legal, finance) — 30 min each
  [Engineering director 1:1s with each manager happen weekly; not listed separately]
```

**Monthly written artifact:** A 1–2 page engineering update covering: delivery summary, health metrics, team changes, and any decisions the exec team should be aware of. Published in the last week of each month. This is the artifact that builds executive trust without requiring executives to attend engineering meetings.

---

## Implementation Notes

**Start with the weekly staff meeting.** It carries the highest leverage in the cadence and decays fastest without a structured agenda. Get that template right before building the rest.

**Run the cadence before adding new meetings.** Every org has too many meetings. Audit what already exists before adding from this playbook. The goal is replacement and repair, applied one tier at a time.

**Cadence debt compounds.** An org that skips the quarterly retrospective for two quarters and lets the metrics review slide into a status update will re-accumulate the coordination failures this cadence is designed to prevent. The discipline of maintaining the cadence is what matters; the meeting formats are the scaffolding.

## Further Reading

| Topic | Resource |
|---|---|
| Management operating cadence | Grove, *High Output Management* (Vintage, 1995) |
| Goal-setting and measurement | Doerr, *Measure What Matters* (Portfolio/Penguin, 2018) |
