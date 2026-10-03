# 7. Intake, review, approval, and exception templates

[← Chapter index](README.md)

## 7.1 Skill intake questionnaire

Record respondent, date, attachments, and evidence references.

**Ownership and purpose**

1. Skill ID, name, version, owner, publisher, source repository, and support contact?
2. Business purpose, intended users/environments, non-goals, and prohibited uses?
3. Is it instruction-only? List scripts, binaries, dependencies, links, hooks, and generated code.

**Capability and autonomy**

4. Which tools, MCP servers, APIs, commands, files, systems, and destinations are used?
5. Can it create, modify, delete, deploy, communicate, purchase, transfer, decide, approve, schedule, delegate, or persist state?
6. Is it advisory, approval-per-action, bounded multi-step, scheduled, or open-ended?
7. What limits apply to time, actions, retries, recursion, cost, output, and delegation?

**Data and identity**

8. Which data classes are received, retrieved, generated, retained, logged, or sent?
9. Can data cross user, tenant, region, environment, supplier, or organizational boundaries?
10. What user/service identities and credentials are used? Scope, audience, lifetime, storage, rotation, and revocation?

**Instructions and external content**

11. How are instruction authority and conflict handled?
12. Which untrusted sources can influence context? How are data and instructions separated?
13. What actions are deterministically validated and authorized outside the model?

**Supply chain and change**

14. How are publisher, source, version, build, integrity, dependencies, and licenses verified?
15. Are mutable remote references used?
16. How are updates diffed, reviewed, canaried, rolled back, and communicated?

**Operations**

17. Which actions require human or dual approval?
18. What lifecycle and runtime events are logged and detected?
19. How is the skill suspended, revoked, contained, recovered, and retired?
20. What tests, known limitations, exceptions, and residual risks exist?

Required attachments: architecture/data flow, threat model, permission manifest, materials inventory, tests, release/rollback plan, and owner acceptance.

## 7.2 Review form

- Review ID; skill ID/version/hash; platform/environment; proposed tier.
- Business, technical, data, security, and incident owners.
- Change from prior review, including semantic/permission/destination diff.
- For each control: `Pass / Partial / Fail / Not applicable`, evidence, finding, owner, due date.
- Findings by severity and exploit/abuse path.
- Residual risks and compensating controls.
- Decision: `Approved / Approved with conditions / Time-limited pilot / Rework / Rejected`.
- Approvers, expiry, deployment constraints, next review, and retest triggers.

## 7.3 Approval criteria and hard stops

All production approvals require:

- verified ownership, origin, immutable version, and inventory;
- complete data, capability, permission, destination, and dependency declarations;
- least-privilege execution configuration and credential handling;
- reviewed threat model and passed negative/abuse tests;
- deterministic authorization and meaningful approval for consequential actions;
- tested audit, detection, disablement, revocation, and rollback;
- no open critical/high finding without authorized exception; and
- review expiry and retirement owner.

**Do not approve** if ownership or origin is unknown; raw privileged secrets reach model context; instructions can redefine authorization; permissions materially exceed purpose; consequential effects lack independent approval; activity is not attributable/auditable; the version cannot be reliably disabled; or critical risk is unmitigated.

## 7.4 Exception template

- Exception ID; requirement; skill/version/hash/platform/environment.
- Requestor and accountable risk owner.
- Business justification and why compliant alternatives are infeasible.
- Exact scope, users, data, systems, duration, and affected threats.
- Likelihood, impact, and residual risk.
- Compensating prevention, detection, response, and monitoring.
- Validation evidence and remediation milestones.
- Start, expiry, review cadence, and automatic action at expiry.
- Security, data/privacy, legal/compliance, and business approvals.
- Closure criteria and evidence.

Exceptions MUST be narrow, time-bound, visible in inventory, revocable, and unable to renew silently.

## Chapter checklist

Source tags resolve in the [source catalog](13-sources.md).

- [ ] **P0** Require formal intake, independent review, approval, and evidence before installation or publication. `[AST10, NIST-SSDF]`
- [ ] **P1** Track applicable privacy, records, intellectual-property, sector, export, accessibility, and regional obligations. `[NIST-AI-RMF, ISO-42001, ISO-27001]`
- [ ] **P0** Verify publisher identity, ownership, source repository, support status, and vulnerability-reporting route. `[AST10, NIST-SSDF]`
- [ ] **P0** Review the complete package: frontmatter, prose, scripts, hooks, MCP configuration, manifests, assets, references, and dependencies. `[AST10, CURSOR-HARDENING]`

[← Role-specific implementation checklists](06-role-specific-implementation-checklists.md) · [Next: Illustrative implementation examples →](08-illustrative-implementation-examples.md)
