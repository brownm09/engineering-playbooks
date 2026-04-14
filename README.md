# Engineering Playbooks

Operational frameworks from production engineering work across payments, platform, and compliance contexts. Each document reflects decisions made in real systems, not hypothetical best practices.

## Contents

### Disaster Recovery
**[fire-drill-template.md](disaster-recovery/fire-drill-template.md)**
Tabletop exercise format for stress-testing DR posture and incident management protocols. Covers scenario sequencing (catastrophic failure first), participant structure, pre/post checklists, and what to watch for. Built from exercises run at ActBlue to validate payment continuity under failure scenarios.

### Incident Management
**[on-call-restructuring-framework.md](incident-management/on-call-restructuring-framework.md)**
Framework for restructuring an on-call program that has outgrown its original design. Covers the IC/responder split, rotation structure, Wed-Wed cadence, metrics instrumentation via Jeli and Jira, and the rollout approach. Based on a restructuring that expanded the on-call program from a 5-person SRE team absorbing everything to per-team responder rotations backed by a 12-person incident commander rotation.

### Compliance
**[pci-dss-gap-analysis-checklist.md](compliance/pci-dss-gap-analysis-checklist.md)**
Engineering-focused checklist for a PCI-DSS v4.0 gap analysis. Organized by all 12 requirement domains, with emphasis on the controls engineering teams are most likely to own or partially own. Includes a section on common gaps found in first assessments.

### CI/CD
**[pipeline-governance-guide.md](ci-cd/pipeline-governance-guide.md)**
Governance model for CI/CD pipelines at scale: ownership, required gates, secret management, audit requirements, and change control. Covers the shared template model, DORA metric instrumentation, and the most common governance failures.

### Experimentation
**[launchdarkly-rollout-governance.md](experimentation/launchdarkly-rollout-governance.md)**
Flag lifecycle management for LaunchDarkly at scale. Covers flag taxonomy, naming conventions, rollout sequencing, targeting rules, experiment guardrails, and the cleanup policy that prevents flag debt from accumulating.

### AI Adoption
**[ai-adoption-readiness-framework.md](ai-adoption/ai-adoption-readiness-framework.md)**
Framework for rolling out AI-assisted development tools (GitHub Copilot, Claude, Claude Code, Cursor) across engineering organizations. Covers a four-stage IC fluency rubric, role-differentiated use cases (IC vs. manager), task classification by risk level, a three-tier observability model, and a phased gate model that sequences access to higher-risk workflows on demonstrated readiness. Developed across two production rollouts (ActBlue 2024–2025, CTA 2025–2026). Includes a worked example and rollback triggers.

## Context

These frameworks were developed and applied across high-volume, regulated platforms including a payments processor handling 1M+ transactions/day under PCI-DSS. They are written to be adapted, not followed verbatim. The right answer for your system depends on your scale, team structure, and constraints.
