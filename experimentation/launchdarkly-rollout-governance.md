# LaunchDarkly Rollout Governance

## Leadership Context

Feature flags are the primary mechanism for decoupling deployment from release — which is what allows an engineering org to ship continuously without betting the business on each deploy. The governance question is not whether to use flags, but whether they remain a controlled instrument or become hidden complexity that slows delivery, obscures system behavior, and accumulates technical debt no one is willing to clean up.

## Purpose

Feature flags without governance become permanent conditionals that no one understands and no one removes. This guide covers the policies and practices that keep a LaunchDarkly implementation useful over time: flag naming, lifecycle management, targeting rules, rollout sequencing, and the cleanup process that prevents flag debt from accumulating.

## Background and Motivation

This governance framework was developed from the LaunchDarkly rollout at ActBlue Technical Services (2022–2024). I managed the vendor relationship, designed the proof-of-concept, and drove cross-team adoption across teams inside and outside my direct management. The platform team built the proof-of-concept; product engineering teams participated in rollout. The first customer-facing flag reached production within 4 months of the program mandate.

## Flag Taxonomy

Flags serve different purposes and should be managed differently. The most useful distinction:

| Type | Purpose | Expected lifespan |
|------|---------|-------------------|
| Release flag | Gates a feature in development from reaching users | Short: days to weeks; removed after full rollout |
| Experiment flag | Controls exposure for an A/B or multivariate test | Medium: duration of the experiment; removed after conclusion |
| Permission flag | Gates access by user segment, plan tier, or account | Long: may be permanent if tied to entitlements |
| Kill switch | Allows a feature to be disabled in production without a deploy | Indefinite; reviewed periodically |
| Operational flag | Controls system behavior (timeout values, rate limits, algorithm selection) | Varies; reviewed on a defined schedule |

Mixing these types without labeling them produces a flag list where no one can tell which flags are safe to clean up, which are load-bearing, and which have been abandoned.

**Recommended approach:** Use LaunchDarkly tags to label flag type (e.g., `release`, `experiment`, `kill-switch`). Add a second tag for the owning team.

## Naming Convention

Consistent naming makes the flag list scannable. A flag named `flag-123` or `new-checkout` tells the next engineer nothing.

**Format:** `[team]-[area]-[description]`

Examples:
- `payments-checkout-new-flow` — payments team, checkout area, new flow feature
- `platform-api-rate-limit-v2` — platform team, API area, rate limit v2
- `growth-onboarding-ab-step3` — growth team, onboarding experiment, step 3 variant

Rules:
- All lowercase, hyphen-separated
- No dates in flag names (use the flag creation date in LaunchDarkly metadata instead)
- Description should describe what the flag controls, not what it is for ("new-flow" not "q3-initiative")

## Flag Lifecycle

Every flag should move through defined states. LaunchDarkly's built-in lifecycle stages (Active, Deprecated, Archived) map to this:

1. **Created:** Flag is in development. Targeting rules are configured. Default serves the control (off/false) for all users.
2. **Active rollout:** Flag is being rolled out. Targeting rules are live. Flag owner monitors metrics.
3. **Fully rolled out:** Flag serves the treatment (on/true) for 100% of users. Flag is a candidate for removal.
4. **Deprecated:** Flag is scheduled for code removal. Engineers are notified. Removal PR is open or assigned.
5. **Archived:** Code references removed. Flag is archived in LaunchDarkly. Not deleted (for audit purposes).

The failure mode is flags that reach "fully rolled out" and stay there indefinitely. Step 3 should trigger a task, not a resting state.

## Rollout Sequencing

Do not go from 0% to 100% in one step.

**Standard rollout sequence for a release flag:**

1. Internal users only (employees, internal accounts) — validate basic functionality
2. 5% of production traffic — watch error rates, latency, business metrics for 24-48 hours
3. 25% — continue monitoring; confirm metrics are stable
4. 50% — confirm no long-tail issues
5. 100% — full rollout; schedule flag removal

Adjust the timing between steps based on traffic volume. A high-traffic payments flow needs more time at each step than a low-traffic admin feature. For high-risk changes (payment processing, authentication), treat the 5% step as a canary with automated rollback triggers configured.

**Rollback:** The flag serves as the rollback mechanism. Before a feature ships behind a flag, the team confirms: "if something goes wrong, we can set this flag to off and the problem goes away." If that is not true, the flag is not actually controlling the right surface area.

## Targeting Rules

Targeting rules determine who sees what. Poorly configured targeting is one of the most common sources of flag-related incidents.

**Principles:**

- Default rule (what users get when no other rule matches) should be the safe/control state until the flag is fully rolled out
- Do not use targeting rules to approximate what should be a permission system; if access control is the requirement, use the application's permission layer
- Targeting by user ID for experiments; by percentage rollout for gradual releases; by account/org attribute for entitlement flags
- Document why a targeting rule exists if it is non-obvious; LaunchDarkly flag descriptions are indexed and searchable

**Experiment targeting:** A/B tests require consistent user assignment (the same user sees the same variant on every visit). Use LaunchDarkly's built-in consistent bucketing by user key, not by session. Inconsistent assignment degrades experiment validity.

## Metrics and Guardrails

For any flag backing a release or experiment, define success metrics and guardrail metrics before the flag goes live.

**Success metrics:** What the flag is intended to improve (conversion rate, page load time, error rate).

**Guardrail metrics:** What must not get worse (payment success rate, p99 latency, error budget). If a guardrail metric degrades during rollout, the rollout pauses and the flag rolls back, regardless of success metric performance.

LaunchDarkly Experimentation integrates with analytics and monitoring platforms. For teams using Datadog, connect flag state changes to Datadog events so that flag rollouts are visible on dashboards alongside infrastructure and application metrics. This makes it straightforward to correlate a metric change with a flag state change.

## Flag Cleanup Policy

Flag debt compounds. A project that ships a flag per sprint without a cleanup policy will have hundreds of stale flags within a year.

**Cleanup triggers:**
- Release flag at 100% rollout for 2+ weeks with no rollback incidents: schedule removal
- Experiment flag with a concluded result: archive within one sprint of conclusion
- Flag with no evaluation events in 30 days: review and archive if no longer needed

**Cleanup process:**
1. Identify candidates (LaunchDarkly flag health report, or a periodic audit in the sprint backlog)
2. Search codebase for flag key references
3. Open PR to remove flag evaluation code and dead code branches
4. Merge and deploy
5. Archive flag in LaunchDarkly (do not delete; archived flags preserve audit history)

Assign flag cleanup as a recurring task, not something that happens when someone has spare time. One sprint per quarter dedicated to flag debt keeps the list manageable.

## Governance Checklist for New Flags

Before creating a flag:

- [ ] Flag type is defined (release, experiment, kill switch, permission, operational)
- [ ] Flag name follows the naming convention
- [ ] Owning team tag is applied
- [ ] Default rule serves the control state
- [ ] Success and guardrail metrics are defined (for release and experiment flags)
- [ ] Rollout plan is documented (percentage steps and timing)
- [ ] Rollback procedure is confirmed: setting flag to off restores the prior state

Before archiving a flag:

- [ ] All code references to the flag key have been removed
- [ ] Dead code branches have been cleaned up (not just the flag call, but the conditional logic it controlled)
- [ ] PR is merged and deployed to all environments
- [ ] Flag is archived in LaunchDarkly

## Common Problems

**Flags that cannot be turned off:** The code path for the "off" state was removed after full rollout, so the flag is now load-bearing in the on position. The kill switch is gone. Fix: do not remove the off code path until the flag is archived.

**Experiment results ignored:** An experiment concluded, one variant won, but the flag was never cleaned up and the losing variant is still in the codebase. Fix: treat experiment conclusion as a trigger for a cleanup task, not just an analytics event.

**Targeting rules owned by one person:** A targeting rule was set up by an engineer who left the team. No one knows what it does or whether it can be changed. Fix: document targeting rules; review and reassign ownership during offboarding.

**Flag created to avoid a deploy:** Sometimes the right answer is a deploy, not a flag. Flags add evaluation overhead and long-term maintenance cost. Use flags when you need gradual rollout, instant rollback, or controlled experimentation. Do not use them to avoid the discomfort of deploying.
