# Cross-Functional Alignment Playbook

## Leadership Context

Engineering organizations that cannot align effectively with product, design, legal, finance, and sales do not just deliver slower — they deliver the wrong things, at the wrong time, with last-minute surprises that erode trust with every function they depend on. Cross-functional alignment is not a soft skill; it is an operational capability that determines whether engineering can make and keep commitments. The cost of misalignment compounds: a legal review that starts three weeks too late delays a launch by a quarter; a sales commitment made without engineering input creates a customer expectation no one can meet; a finance model built on the wrong headcount assumptions generates budget fights mid-year. This playbook establishes the decision authorities, rituals, and interfaces that keep engineering in alignment with every function it touches.

## When to Use This

- A new engineering leader is onboarding and needs to understand how engineering relates to its cross-functional partners
- A post-mortem on a missed launch or failed project reveals that coordination failure — not technical failure — was the root cause
- Rapid organizational growth (above ~30 engineers or after a significant acquisition) is creating coordination failures that did not exist when the org was smaller
- An engineering Chief of Staff or TPM is being asked to design or repair the org's cross-functional operating model

---

## The Three Partnership Failure Modes

Most cross-functional coordination problems trace to one of three root causes. Diagnosing the right one before attempting a fix matters — the solutions are different.

### Failure Mode 1: Too Much Gate-Keeping

Engineering has installed reviews, approval processes, and technical requirements gates that slow down cross-functional partners without providing proportionate value. Legal cannot get a privacy review without a 10-page technical spec. Product cannot start design without engineering sign-off on whether something is feasible. Finance cannot get headcount cost estimates without a formal request.

**Signal:** Cross-functional partners route around engineering, go directly to ICs without manager awareness, or stop including engineering in early planning because it creates more work than value.

**Fix:** Audit every approval process engineering owns. For each one, ask: who benefits from this gate, what problem does it prevent, and is the prevention worth the delay it adds? Remove any gate that fails this test.

### Failure Mode 2: Too Little Early Warning

Engineering is not included in decisions until after they are made — product roadmap commitments made without capacity input, legal requirements surfaced in the final week of a project, sales deals closed on features that do not exist. Engineering is then asked to react to a fait accompli.

**Signal:** Engineering leaders consistently describe being "surprised" by commitments, requirements, or decisions that were made without them.

**Fix:** Define the earliest point at which engineering needs to be in the room for each type of decision. Build that into cross-functional processes, not as a gate, but as a standing invitation.

### Failure Mode 3: No Shared Language for Priority

Engineering and its partners are operating with different mental models of what is urgent, what is important, and what can wait. Product thinks "high priority" means this quarter. Engineering thinks it means this sprint. Legal thinks it means before signature. Finance thinks it means before end of fiscal year.

**Signal:** Cross-functional escalations are frequent. Every stakeholder believes their request is the highest priority. Engineering feels constantly in triage mode.

**Fix:** Establish a shared priority taxonomy (see RACI section) and enforce it consistently. When a cross-functional request arrives without a priority label, return it for classification before accepting it into the queue.

---

## Engineering × Product

### Decision Authority Model

The most durable source of engineering-product friction is ambiguity about who decides what. The following model, adapted from product management practice, has worked at companies ranging from ActBlue (mission-driven, low margin for error) to Capital One (regulated, compliance-heavy):

| Decision type | Who decides | Who must be consulted | Who is informed |
|---|---|---|---|
| What problem to solve | Product | Engineering, Data | Design, Legal |
| Whether to ship a feature | Product | Engineering (feasibility), Design (UX) | Engineering team |
| How to build it (architecture) | Engineering | Product (constraints), Staff engineer | Product manager |
| When it will ship | Engineering | Product (priority), Manager | Product, Stakeholders |
| Whether to change scope mid-flight | Product + Engineering jointly | Design | Stakeholders |
| Whether to accept technical debt to meet a deadline | Engineering manager | Product manager | Director |
| Whether to deprecate a product capability | Product | Engineering (migration cost) | Legal, Support |

"Engineering owns the when" is the principle with the highest leverage and the most friction. Product managers who believe they own the timeline, or who make external commitments about ship dates without engineering input, create the conditions for the delivery surprises that damage trust across the org. The fix is not to remove product's ability to advocate for dates — it is to establish that no date is a commitment until engineering has confirmed it.

### Escalation Path

When engineering and product cannot agree on priority, scope, or timeline:

1. Manager-level conversation between engineering manager and product manager — most disagreements should resolve here
2. If unresolved within 48 hours: Director-level conversation between engineering director and product director
3. If unresolved within 48 hours: VP-level tiebreaker (VP Eng and CPO jointly, or escalated to CEO if both VPs cannot align)

The escalation path should be explicitly known to both engineering managers and product managers. The failure mode is when disagreements fester for weeks without escalation because neither party wants to "make it a thing." Unresolved disagreements are always a thing; they just become a worse thing later.

### The 3-Amigos Ritual

For any feature that requires coordination between product, engineering, and design, the 3-amigos ritual establishes shared understanding before implementation begins.

**What it is:** A 60-minute meeting between the product manager, engineering lead, and design lead, held after the design is far enough along to review but before engineering has started implementation.

**What it covers:**
- Product: What is the user problem this solves? What does success look like in measurable terms?
- Engineering: What are the technical constraints? Are there edge cases the design does not account for? Is the implementation plan roughly correct?
- Design: Are there UX implications of the technical approach? Are there design dependencies (component library, accessibility) that need to be in scope?

**What it produces:** A shared written summary (one page or less) with: the agreed problem statement, the agreed success metric, any scope items that were explicitly excluded, and any open questions with owners.

A 3-amigos session that produces no written artifact did not happen.

---

## Engineering × Design

### Design Handoff SLA

Unclear handoff between design and engineering is one of the highest-friction points in product development. The following handoff SLA defines what engineering needs from design before implementation begins, and what the timeline for receiving it is.

**Engineering needs from design, 5 business days before implementation sprint:**
- Final mockups in Figma (or equivalent) for all states: default, loading, error, empty, responsive breakpoints
- Annotation of any behavior that is not visually obvious (hover states, animation timing, validation logic)
- Confirmation from product that the design is approved for implementation
- Component specification: which existing design system components are used; which new components need to be built

**Engineering needs from design, 1 business day before handoff:**
- Confirmation that all feedback from the last design review is incorporated
- Written answer to: "Is there anything in this design that engineering should know but cannot see in the mockup?"

**What engineering does not need from design before starting:**
- Perfect pixel fidelity on every edge case — this is resolved in implementation review
- Animations that are "nice to have" but not in scope for the initial release

### Component Library Ownership

A component library is owned jointly by design and engineering but with clear individual accountabilities:

- **Design owns:** visual specification, accessibility requirements, usage guidelines, when to use which component
- **Engineering owns:** implementation, test coverage, documentation in the component catalog, deprecation process for old components
- **Joint ownership:** decisions about adding new components (both parties must agree that a new component is warranted vs. extending an existing one)

When a product team wants to ship a feature that requires a new component the design system does not have, the process is: design proposes the component, engineering estimates the implementation cost, the component team reviews for fit, and a decision is made before the implementation sprint begins. Not during it.

### When to Ship Without Perfect Design

There are legitimate situations where the product needs to ship before the design is final. The criteria for this to be acceptable:

- The product manager and engineering manager have both agreed, in writing, that the current state is acceptable for launch
- The design gap is documented with a specific plan to address it (not "backlog") — ideally in the next sprint
- The design gap does not create an accessibility issue or a material UX degradation for users
- Legal and compliance are not impacted by the design gap

"We'll fix it after launch" is only acceptable if the fix has a date attached and an owner named.

---

## Engineering × Legal

### Standard Review Tracks

Engineering works with legal on three categories of issues. Each has a different review lead time expectation.

**Track 1: Privacy and data handling**
Applicable when: a new feature collects, processes, or stores personal data; a new vendor will have access to personal data; a data retention policy is being changed; a new data-sharing arrangement is being established with a partner.

Lead time needed: 10–15 business days for a standard privacy review.

What legal needs from engineering to start: a data flow diagram showing what data is collected, where it is stored, who can access it, and how long it is retained.

**Track 2: Intellectual property**
Applicable when: engineering is incorporating open-source software with a new license type; engineering is creating code or models that the company intends to claim as IP; engineering is building on top of a third-party API in a way that the API terms of service may restrict.

Lead time needed: 5–10 business days for a standard IP review.

What legal needs from engineering to start: a description of the third-party software or API, the license or terms of service, and the proposed use.

**Track 3: Compliance and regulatory**
Applicable when: a feature touches a regulated domain (payments, healthcare, financial data, children's data); a new geographic market is being entered; an enterprise customer contract requires specific compliance certifications.

Lead time needed: 15–30 business days for a standard compliance review. This is not negotiable — regulatory review has external dependencies.

What legal needs from engineering to start: a product brief from the product manager, the relevant regulatory framework (GDPR, HIPAA, PCI DSS, etc.), and a technical description of the implementation approach.

### Expedited Path Criteria

Legal can provide an expedited review (5–7 business days) for standard track items if all of the following are true:
- Engineering has provided a complete intake packet (not a verbal summary)
- The feature is substantially similar to a previously reviewed feature
- The legal question is bounded (not "is this compliant with GDPR?" but "does this retention policy comply with GDPR Article 17?")

**What legal cannot review in 48 hours:**
- Novel privacy architectures
- Cross-border data transfer questions
- Any contract that requires negotiation with a third party
- Regulatory opinions in jurisdictions where outside counsel is required

If engineering surfaces a legal requirement 48 hours before a launch date, the launch date moves, not the legal review. The escalation path is engineering director → CPO/CEO → legal leadership to confirm whether a risk acceptance decision is available. It sometimes is. But the default is: legal review that is not complete means the feature does not ship.

---

## Engineering × Finance

### Headcount Model Handoff

Finance operates on an annual headcount plan and often a quarterly re-forecast. Engineering's role in this process:

**Annual plan (typically Q4 for the following year):**
Engineering director and engineering managers submit a headcount plan by role, level, and team — not by name. Finance converts this to a budget number using their compensation models. The plan should include: current headcount, proposed adds by quarter, and the initiative or business outcome each role supports.

**Quarterly re-forecast:**
Finance will ask engineering to confirm or revise the headcount plan based on what has actually been hired, what roles are being added to the plan, and what roles are being removed. Engineering should treat this as an opportunity to surface capacity constraints that affect delivery commitments.

**Headcount requests outside the plan:**
Use the headcount request memo format in the [Executive Communication Templates](executive-communication-templates.md). These requests require: business case, cost, and risk of not hiring. They are reviewed by the VP Eng (or Director in smaller orgs) and typically require CFO or CEO approval if above a threshold.

### Capitalized vs. Expensed Work (R&D Capitalization)

This matters to finance and to the audit committee. Engineering leaders who understand the basics avoid surprises during audit cycles.

**The rule (simplified from ASC 350-40):** Software development costs can be capitalized (treated as an asset on the balance sheet rather than an operating expense) once the project has reached the "application development stage" — after the preliminary project stage is complete and management has authorized funding. Costs in the planning phase are expensed.

**In practice for engineering:** Work on new features and products that meet the capitalization criteria can be tracked as a capitalized asset. This affects gross margin and EBITDA. Finance will ask engineering to classify projects as capitalized or expensed and to track engineering time allocation accordingly.

**What engineering needs to do:**
- Work with finance to understand which projects are classified as capitalized development
- Ensure engineering managers are tracking time allocation for capitalized projects (even a rough percentage split by engineer is usually sufficient for smaller orgs)
- Surface project completions to finance — a capitalized project that has shipped should stop accruing capitalized costs

Most engineering leaders never need to present this to a board. But engineering leaders who are involved in investor due diligence, who are building the financial model for a fundraise, or who work at a public company will encounter it. Understanding enough to ask the right questions is the goal.

### Cost Center Reporting

Engineering is typically a cost center — it does not generate revenue directly but supports the product that does. Finance will report engineering costs against budget on a monthly and quarterly basis. Engineering leaders should:

- Know their run-rate cost (headcount loaded + tools + infrastructure), updated monthly
- Know which costs are variable (cloud infrastructure scales with product usage) vs. fixed (headcount, tooling subscriptions)
- Flag cost overruns before they appear in the finance report — finance should never surface a cost overrun to the CFO that engineering did not already know about and communicate

---

## Engineering × Sales

### Feature Request Intake

Sales will bring customer feature requests to engineering. Without a defined intake process, these requests land informally (in Slack, in a hallway conversation, in a customer call), are routed inconsistently, and create commitments that engineering did not agree to.

**The intake process:**
1. Sales logs feature requests in a shared system (Productboard, Jira, or equivalent) with: customer name, ARR of that customer, what the customer asked for, and what problem the customer is trying to solve.
2. Product triages the request against the roadmap within 5 business days: is this on the roadmap, adjacent to something on the roadmap, or not in current plans?
3. Product communicates the triage outcome to sales with a timeline expectation or a "not in plan" response.
4. Engineering is not in the intake loop until product has triaged the request. Engineering does not receive feature requests directly from sales.

The reason for this: engineering receiving feature requests directly from sales creates pressure on ICs that bypasses product prioritization. It also creates inconsistent commitments when ICs give informal timeline estimates to customer-facing teams.

### Customer Commitment Process

**Who can promise what:**
- Sales can promise: features that are on the current quarter's roadmap, with "expected in Q[X]" framing (not an exact date)
- Sales cannot promise: features that are not on the roadmap, specific release dates, or custom implementation timelines
- Customer success can promise: standard SLA commitments defined by the product, existing feature roadmap items with product approval
- Engineering leadership can promise to a customer: technical architecture decisions, security and compliance posture, escalation path for critical issues

When a customer is asking for a commitment that sales cannot make, the escalation path is: sales → product (for roadmap commitments) or sales → engineering director (for technical or security commitments). This conversation happens before the customer is given any response.

**The danger of informal commitments:**
A sales engineer telling a customer "I think we can have that in 6 months" is a commitment in the customer's mind even if it is not in any contract. Engineering leaders who inherit customer expectation mismatches discover them at the worst time — when the customer is renewing, escalating, or churning. The fix is clear rules about who can say what to customers about engineering timelines.

---

## RACI Template: Cross-Functional Program Decisions

Use this template when a cross-functional program involves decisions that need clarity on authority.

**Instructions:** For each decision row, assign one person as Accountable (A) and one as Responsible (R). Multiple people can be Consulted (C) or Informed (I). If a cell is blank, that function is not involved in that decision.

| Decision | Engineering | Product | Design | Legal | Finance | Sales | CEO/Exec |
|---|---|---|---|---|---|---|---|
| Launch date for a major feature | A/R | C | C | C | I | I | I |
| Scope reduction to meet launch date | A (eng mgr) | A (PM) — joint | C | I | I | I | I |
| New enterprise customer compliance requirement | R | C | I | A | I | C | I |
| Price of new product tier | I | C | I | C | A | C | R |
| External API contract with a vendor | R | C | I | A | C | I | I |
| Headcount increase outside annual plan | R | I | I | I | C | I | A |
| Emergency patch to a customer-facing bug | R | C | I | I | I | I | I |
| Deprecating a product feature | C | A | C | C | I | R (customer impact) | I |

**A (Accountable):** The buck stops here. This person makes the final call.
**R (Responsible):** Does the work or drives the process.
**C (Consulted):** Must be consulted before the decision is made.
**I (Informed):** Told about the decision after it is made.

When two functions are listed as A/R jointly, both must agree before the decision is finalized. Use this sparingly — shared accountability often means no accountability. Joint ownership only makes sense when both parties have a genuinely equal stake in the outcome and no tiebreaker mechanism exists.

---

## Alignment Health Check

Run this check quarterly, either in the engineering leadership retrospective or as a standalone 30-minute conversation with the engineering director and cross-functional leads.

**Five questions:**

1. **Are there any cross-functional commitments engineering made in the last quarter that the other function was surprised by (positively or negatively)?** Surprises in either direction indicate that communication expectations are not calibrated.

2. **Did any cross-functional request arrive too late for engineering to respond without a quality tradeoff?** If yes, trace back to where in the process the request should have arrived and fix the entry point.

3. **Is there any function that engineering does not have a consistent 1:1 relationship with at the director level?** Informal alignment between ICs is not a substitute for leadership-level relationship-building.

4. **Are there any decisions that were made in the last quarter that engineering should have been consulted on but was not?** This surfaces gate-keeping vs. exclusion failure modes.

5. **Is there any decision that engineering is currently delaying because the accountability is unclear?** Name it and assign it before leaving the room.

If the answer to all five questions is "no, nothing notable," either alignment is working well or the check-in is not surfacing real information. The tie-breaker is to ask each function's leader separately whether they have any friction with engineering. If the answers differ from what engineering leadership reported, the problem is information flow, not alignment.
