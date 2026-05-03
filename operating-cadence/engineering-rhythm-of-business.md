# Engineering Rhythm of Business

## Leadership Context

Operating cadence is the meeting and ritual structure that determines what an engineering org can decide, when, and at what altitude. When the structure is missing — or worse, present but ceremonial — the symptoms are predictable: strategy set in Q1 is invisible by Q2, engineering managers spend their 1:1s on status because there's nowhere else for it to go, and the VP learns about a critical platform risk in the same briefing as the CTO. The playbook below is what cadence looked like at a 50-engineer platform directorate (2024–2025) across 6 teams: the meetings that actually carried weight, the ones that drifted, and the recovery patterns when they did.

## Background and Motivation

This playbook came out of the operating cadence work at ActBlue Technical Services (2024–2025), where I set and ran the structure for a platform directorate of ~50 engineers across 6 teams. What's below is the cadence as it actually ran at that scale — the meetings, the written artifacts, the escalation patterns — not what it looks like in a deck.

## When to Use This

- A new VP or Director is stepping into an existing org and needs to understand what cadence is already in place (and what is broken)
- Post-acquisition integration: two engineering orgs are merging and need a unified operating model
- The org has crossed 30 engineers and ad hoc coordination is failing: meetings proliferate without structure, decisions get made in Slack threads and forgotten
- An engineering Chief of Staff or TPM is being asked to own the operating cadence and needs a reference model

---

## The Three Failure Modes This Cadence Prevents

**Failure mode 1 — decision latency.** Decisions that should take 48 hours take two weeks because no standing forum exists at the right level with the right people. The weekly staff meeting exists for exactly this.

**Failure mode 2 — altitude mismatch.** Senior leaders get pulled into execution; team leads get cut out of decisions they need context on. The tiered structure keeps problems at the level where they belong.

**Failure mode 3 — strategy decay.** Quarterly and annual direction-setting happens, but no mechanism checks whether the direction is still alive mid-quarter. The monthly metrics review and quarterly retrospective surface decay before it compounds.

---

## Weekly Tier

### Engineering Staff Meeting

**Attendees:** Engineering Director/VP, engineering managers, staff-level tech leads (optional)
**Frequency:** Weekly, 60 minutes
**Owner:** Engineering Director/VP or Chief of Staff

The weekly staff meeting is the primary decision-making forum at the director-and-above layer. Status is async — Slack thread, written update, dashboard, whatever the team uses. A topic earns a slot here when a decision is required and the room can resolve it. If both conditions aren't true, it doesn't belong.

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
Pull the last four weeks of meeting notes. Tag each agenda item: decision, alignment, update, or bloat. Move updates into a written pre-read. Cut bloat. If two or more items have recurred across weeks without closing, the broken process isn't this meeting — it's upstream. Surface that. Don't let the meeting absorb the dysfunction.

---

### On-Call Sync

**Attendees:** Current on-call IC, engineering manager on call, platform/SRE lead
**Frequency:** Weekly, 30 minutes (Monday or Wednesday, depending on rotation handoff day)
**Owner:** Platform lead or on-call IC

See also: [On-Call Restructuring Framework](../incident-management/on-call-restructuring-framework.md)

Purpose: hand off the rotation, walk through prior-week incidents, and check alert health. The third item is where most of the value comes from — the alerts that fired but shouldn't have, the runbook gaps the on-call IC discovered at 2 AM.

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

The 1:1 is the most important leadership tool an engineering manager has. It is also the most commonly wasted.

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
The Engineering VP or Director should hold monthly 1:1s with the product, design, and data leads. These are relationship meetings, not coordination ones — the goal is early warning and trust before either is needed. Coordination happens in cross-functional forums; if it's happening here, the forums aren't working.

---

## Monthly Tier

### Engineering All-Hands

**Attendees:** All engineers, engineering managers, invited cross-functional guests
**Frequency:** Monthly, 60–75 minutes
**Owner:** Engineering Director/VP with CoS support on logistics

The all-hands does two things — and only two. Engineers need a view of where the org is actually going and what the health metrics actually show, not the version sanded down for the QBR. The all-hands also has to close the gap between decisions made at the leadership layer and the people executing against them. Everything else that ends up on the agenda is filler.

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

**Common failure:** the all-hands becomes a leadership broadcast and engineers quietly stop attending — not by skipping, but by joining with their cameras off and other windows open. Reserve the featured team slot for ICs presenting their own work. Make Q&A open to pre-submitted and live questions, and read the live ones in the order they came in (not the order leadership prefers). Every quarter, ask in a skip-level or anonymous channel: what do you want to know that we aren't telling you?

---

### Architecture Review

**Attendees:** Staff engineers, architects, engineering managers of affected teams, relevant product leads
**Frequency:** Monthly, 90 minutes (or as-needed for major changes)
**Owner:** Principal/Staff engineer or architecture working group

Purpose: gate proposed system changes that exceed a defined scope or risk threshold before any team commits to building them. The forum has authority — approvals carry weight, conditional approvals carry conditions, and deferrals come with a written reason and a path back to a decision.

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

Decisions are written and stored in a shared location — Confluence, Notion, the engineering wiki, whatever the org uses. An architecture decision that lives only in a meeting recording is not a decision; it's a memory.

---

### Metrics Review

**Attendees:** Engineering Director/VP, engineering managers, data or analytics partner
**Frequency:** Monthly, 45–60 minutes
**Owner:** Engineering Director/VP or CoS

The dashboards carry the numbers. The metrics review is for the next question: what do these trends mean for system health, what's the hypothesis about why they're moving, and what's the org committing to change because of them?

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

The engineering QBR is a leadership-layer forcing function: an honest accounting of what the org committed to last quarter, what it actually delivered, and what it's committing to next. The room is sized for structural problems — the things that need a leadership decision to resolve, not the wins that could go in a monthly update email.

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

The planning kickoff opens the next quarter's planning cycle. The goal is shared context — what the company is trying to accomplish, where engineering's capacity actually sits, and what the largest bets in play are. Commitments come later, after the dependencies are mapped and the questions are resolved.

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

Sprint retrospectives surface team-level friction inside a delivery cycle. The quarterly retrospective is for the problems that span teams and compound — the ones no single sprint ceremony was designed to catch, and that none of them will catch alone.

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

A retrospective without assigned actions is a venting session. If the 2–3 actions from last quarter aren't reviewed at the start of this one, no one in the room will trust the next round.

---

## Annual Tier

### Technology Strategy Review

**Attendees:** Engineering leadership (VP, directors, principal engineers), product leadership, CTO
**Frequency:** Annual (Q4, in parallel with business planning)
**Owner:** CTO or VP Engineering with principal engineer input

The session forces a single question: given where the business is going in the next 12–18 months, can the technology platform actually support it? Scope is structural — the architecture, the team capability profile, and the strategic technology bets the org isn't currently making but should be.

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

The roadmap reset is upstream of planning. Planning produces sprint-level commitments; the reset produces a 12-month view of bets with honest confidence levels attached — the kind of confidence that admits "we don't know yet, and here's what we'd need to learn."

Each initiative in the roadmap should have:
- A one-sentence problem statement (not a feature name)
- The business metric it is expected to move
- A confidence level (high / medium / low) and the primary uncertainty driving that confidence level
- An owning team and an engineering lead
- A rough quarter when work is expected to begin

The roadmap is a forecast, not a contract. The prior year's roadmap was partially right and partially wrong, and this one will be too — the reset frames planning around that fact, not around the wish that this time will be different.

---

### Org Health Survey

**Frequency:** Annual (or biannual for orgs with high change velocity)
**Owner:** Engineering Director/VP with HR partnership

An annual survey covering clarity of direction, psychological safety, manager effectiveness, career growth, cross-functional collaboration, and on-call/operational load. Participation isn't optional in any meaningful sense — if engineers don't fill it out, the org doesn't have signal on whether the work is sustainable.

Survey results feed into the next quarter's planning cycle as engineering-org inputs. If they don't influence any decision, engineers will correctly read it as performative and stop responding next year. The signal degrades fast.

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

**How to use this table:** When a decision is stuck — either no one is moving it, or everyone is arguing about who should — the first question is: who is the Driver? If there isn't one, the decision won't move. Assign one before doing anything else.

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

A Chief of Staff or senior TPM who owns the operating cadence is one of the highest-leverage roles in an engineering org — and one of the most commonly under-spec'd. The work spans three phases:

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

**Escalation judgment:** the CoS sees things going wrong before the director does. That visibility only converts to value if the CoS has a calibrated sense of what to escalate immediately and what to hold for the next staff meeting. One test: in 48 hours, will this cost money, create compliance exposure, or land as a surprise on someone above the director? Anything that's a yes, surface the same day.

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

**Monthly written artifact:** a 1–2 page engineering update covering delivery summary, health metrics, team changes, and any decisions the exec team should know about. Published in the last week of each month. This is the artifact that builds executive trust over time without putting executives in engineering meetings.

---

## Implementation Notes

**Start with the weekly staff meeting.** It carries the highest leverage in the cadence and decays the fastest without a structured agenda. Get that template right — get it written, get it on the calendar, get it followed for four weeks — before building the rest.

**Run the cadence before adding new meetings.** Every org has too many meetings. Before adding anything from this playbook, audit what's already on the calendar — most of the time the broken meeting is hiding in plain sight. The goal is replacement and repair, one tier at a time.

**Cadence debt compounds.** An org that skips two quarterly retrospectives and lets the metrics review slide into a status update will re-accumulate every coordination failure this cadence was designed to prevent — usually within a quarter. Discipline maintains the cadence; the meeting formats are scaffolding.

## Further Reading

| Topic | Resource |
|---|---|
| Management operating cadence | Grove, *High Output Management* (Vintage, 1995) |
| Goal-setting and measurement | Doerr, *Measure What Matters* (Portfolio/Penguin, 2018) |
