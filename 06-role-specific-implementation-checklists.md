# 6. Role-specific implementation checklists

[← Chapter index](README.md)

## Skill creators

- [ ] Bound purpose and non-goals; document stop/escalation behavior.
- [ ] Label user, retrieved, linked, and tool content as untrusted data.
- [ ] Declare every tool, permission, path, data class, destination, side effect, dependency, and limit.
- [ ] Remove embedded secrets and personal/sensitive test fixtures.
- [ ] Validate inputs/outputs; use safe command, path, archive, and parser APIs.
- [ ] Pin dependencies and remote references or bind them by integrity.
- [ ] Add negative, injection, exfiltration, privilege, resource, and failure tests.
- [ ] Define rollback, disablement, upgrade, and retirement behavior.
- [ ] Produce permission/behavior diffs and release notes.



## Users and administrators installing skills

- [ ] Verify source, publisher, version, digest, and organizational approval.
- [ ] Compare declared behavior with requested host permissions.
- [ ] Review scripts, network destinations, linked content, and update method.
- [ ] Test in a non-production sandbox with synthetic data.
- [ ] Bind a dedicated least-privilege identity; never reuse a personal admin token.
- [ ] Configure egress, filesystem, action, cost, time, and approval limits.
- [ ] Confirm audit events, kill switch, revocation, and rollback.
- [ ] Record every installation and reject unreviewed updates.



## Platform teams

- [ ] Provide approved immutable storage and deny unregistered artifacts.
- [ ] Enforce default-deny capability policy outside the model.
- [ ] Broker short-lived credentials without exposing them to context.
- [ ] Isolate code and restrict filesystem, process, network, and resources.
- [ ] Correlate user, agent, skill version, policy, tool, approval, and outcome.
- [ ] Enforce cumulative capability and source-to-sink data policies.
- [ ] Support canary, pin, rollback, suspend, version/hash deny, and fleet revocation.
- [ ] Reconcile runtime discoveries with inventory.



## Application security

- [ ] Validate tier and threat model across skill, host, tool/MCP, and model boundaries.
- [ ] Manually review instructions, metadata, hidden content, code, dependencies, and destinations.
- [ ] Test direct/indirect injection, tool poisoning, confused deputy, cross-tenant access, and exfiltration.
- [ ] Test cross-skill chains and platform migration.
- [ ] Verify authorization and approvals cannot be supplied by model prose.
- [ ] Record scanner limits, residual risk, findings, and retest triggers.



## Security operations

- [ ] Ingest publication, installation, activation, authorization, tool, egress, update, and revocation events.
- [ ] Baseline activity by skill/version and tier.
- [ ] Alert on undeclared destinations, scope changes, denied actions, secret access, high velocity, loops, and suspicious sequences.
- [ ] Protect audit integrity while minimizing sensitive log content.
- [ ] Maintain hash/version/domain blocks and rapid credential revocation.
- [ ] Exercise containment and feed incident patterns into detections and tests.



## Governance, risk, compliance, privacy, and procurement

- [ ] Maintain policy, risk taxonomy, inventory, hard stops, and decision rights.
- [ ] Map data use and controls to legal, privacy, records, sector, regional, and contractual duties.
- [ ] Assess publishers, maintenance, build/release, vulnerability handling, incident notice, and exit plan.
- [ ] Require current owners, review dates, expiring exceptions, and retirement plans.
- [ ] Sample evidence for design and operating effectiveness.
- [ ] Report residual risk and trend data without presenting a score as proof of safety.

## Chapter checklist

Source tags resolve in the [source catalog](13-sources.md).

- [ ] **P1** Train creators, reviewers, installers, approvers, users, and responders for their specific responsibilities. `[NIST-AI-RMF, ISO-42001]`
- [ ] **P0** Separate planning, authorization, approval, and execution so the model cannot approve its own proposed action. `[OWASP-AGENTIC, OPENAI-SAFETY]`
- [ ] **P0** Require independent review for source and release changes; prohibit self-approved production releases. `[SLSA, NIST-SSDF]`
- [ ] **P1** Review permissions regularly and revoke unused, orphaned, expired, or anomalous grants. `[NIST-ZTA, ISO-27001]`
- [ ] **P0** Validate typed, versioned schemas and natural-language intent at every handoff. `[OPENAI-STRUCTURED, OWASP-AGENTIC]`
- [ ] **P1** Use independent verification or multi-party approval for mission-critical multi-agent decisions. `[OWASP-AGENTIC, NIST-AI-RMF]`

[← Security best practices and control catalog](05-security-best-practices-and-control-catalog.md) · [Next: Intake, review, approval, and exception templates →](07-intake-review-approval-and-exception-templates.md)