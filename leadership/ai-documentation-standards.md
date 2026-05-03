# AI-Assisted Documentation Standards

**Scope:** How to ensure AI-generated documentation is auditable, verifiable, and trustworthy
**Applies to:** Any project where Claude Code or another AI assistant contributes to architectural
documentation, design documents, ADRs, playbooks, or technical recommendations

---

## Core Principle: AI Recommendations Must Be Sourced

When an AI assistant produces documentation that names a technology, pattern, protocol, or
compliance framework as a recommendation, that recommendation must be traceable to a primary
source. Unsourced AI output is unverifiable — a reader cannot distinguish a well-grounded
recommendation from a confident-sounding hallucination.

This is not primarily a hallucination-prevention rule. It is an intellectual integrity rule:
the same standard that applies to a staff engineer writing a design document applies to
AI-generated output that carries the same weight.

---

## What Must Be Cited

### Technology and framework choices
Link to the official documentation for every tool selected. The official docs are the
authoritative source for capability claims, configuration, and limitations.

**Examples:**
- Choosing NestJS → link to [docs.nestjs.com](https://docs.nestjs.com)
- Choosing Prisma → link to [prisma.io/docs](https://www.prisma.io/docs/getting-started)
- Choosing Turborepo → link to [turbo.build/repo/docs](https://turbo.build/repo/docs)

### Protocol and specification choices
Link to the normative specification for every protocol or standard referenced.

**Examples:**
- OAuth 2.0 → [RFC 6749](https://datatracker.ietf.org/doc/html/rfc6749)
- PKCE → [RFC 7636](https://datatracker.ietf.org/doc/html/rfc7636)
- GraphQL → [spec.graphql.org](https://spec.graphql.org/October2021/)
- OIDC → [openid.net/specs/openid-connect-core-1_0.html](https://openid.net/specs/openid-connect-core-1_0.html)

### Architectural patterns
Link to the original paper, article, or book chapter that introduced or best defines the
pattern. Do not cite secondary summaries or Wikipedia.

**Examples:**
- Hexagonal Architecture → [Cockburn (2005)](https://alistair.cockburn.us/hexagonal-architecture/)
- Clean Architecture / Dependency Rule → [Uncle Bob (2012)](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)
- Dependency Injection → [Fowler (2004)](https://martinfowler.com/articles/injection.html)

### Compliance and regulatory references
Link to the primary regulatory or standards body source. Do not cite compliance vendor
summaries or blog posts as the authoritative source.

**Examples:**
- GDPR Article 17 → [gdpr-info.eu/art-17-gdpr](https://gdpr-info.eu/art-17-gdpr/)
- HIPAA Security Rule → [hhs.gov/hipaa/for-professionals/security](https://www.hhs.gov/hipaa/for-professionals/security/index.html)

---

## Where Citations Go

### In ADRs
A `## References` section at the bottom of every ADR. Each entry: a linked title, and
one sentence describing what decision in the ADR it supports.

```markdown
## References

- [RFC 6749 — OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) — The authorisation
  code flow used by Clerk and Auth0; defines the token exchange this ADR relies on.
- [Clerk — Documentation](https://clerk.com/docs) — Official docs for the primary identity
  provider chosen in the Decision section.
```

### In playbooks
A `## References` section at the bottom of any playbook that cites a specific framework,
methodology, or standard. Playbooks that contain only internal process guidance with no
external dependencies do not require citations.

### In AI responses
When Claude recommends a technology in a response (not only in committed documentation),
it should include the official documentation link inline. This makes the recommendation
immediately verifiable without requiring a follow-up search.

---

## What Does Not Require a Citation

- Internal cross-references to other ADRs, issues, or PRs in the same project
- Decisions that are entirely internal (e.g., a naming convention with no external basis)
- Widely understood facts that do not assert specific capability claims

---

## Consolidated Reference Index

For projects with multiple ADRs, maintain a consolidated reference index (e.g.,
`docs/adr-references.md`) that groups all sources by domain. This serves as:
- A single place to audit coverage ("are all our technology choices sourced?")
- A reading list for new contributors onboarding to the architecture
- A starting point for due-diligence reviews (security, ARB, compliance audits)

Update the index whenever an ADR's references change.

---

## Enforcing This Standard in Prompts

When opening a session in which documentation will be written or updated, include this in
the opening brief:

> All ADRs and design documents produced this session must include a ## References section
> with links to primary sources for every technology, pattern, and specification cited.
> See docs/adr-references.md for the established pattern.

For projects using CLAUDE.md, encode this as a standing instruction in the
**Documentation and Citations** section so it applies automatically every session.
