# 11. Maturity model and metrics


A maturity score measures process adoption and evidence quality. It does **not** prove that a skill or organization is safe or compliant.

| Level | Characteristics | Evidence of progress |
|---|---|---|
| **0 Unmanaged** | ad hoc installation, unreliable inventory/ownership | baseline discovery report and risk exposure |
| **1 Documented** | policy, inventory, intake, owners, basic review | ≥70% inventoried/owned; decisions retained |
| **2 Enforced** | technical gates, least privilege, logging, exceptions | ≥90% production coverage; zero unowned high-risk skills beyond SLA |
| **3 Measured** | operating effectiveness, tiered monitoring, exercises | ≥95% required audit-field completeness; 100% exceptions expire; quarterly revocation tests |
| **4 Adaptive** | incidents/red teams/threat intelligence update controls; composition analysis | material changes trigger re-review; cross-skill simulations; declining recurrence by root-cause class |

Recommended metrics, always reported with numerator, denominator, source, time range, owner, exceptions, and confidence:

- percentage of observed skills in inventory and on approved versions;
- percentage with current owners, tier, evidence, and review;
- median/95th percentile age of unreviewed updates and open high findings;
- proportion of permissions used versus granted, by risk tier;
- number of blocked undeclared actions/destinations and confirmed false positives;
- percentage of consequential actions with valid scoped approval;
- audit event completeness and correlation success;
- mean/95th percentile time to disable a skill and revoke credentials;
- injection, exfiltration, isolation, and composition regression pass rates;
- exception count, age, expiry breaches, and compensating-control health;
- incident recurrence by cause and corrective-action closure time;
- inventory drift and unsupported-platform security gaps.

Do not combine these into a single “safety score” without preserving the underlying measures and uncertainty.

## Chapter checklist

Source tags resolve in the [source catalog](13-sources.md).

- [ ] **P2** Measure inventory coverage, unsupported versions, overdue reviews, exception age, control failures, incidents, and mean time to disable. `[NIST-CSF, NIST-AI-RMF]`
- [ ] **P1** Log installation, discovery, activation, shadowing/collisions, update, disablement, and removal. `[AST10, NIST-CSF]`
- [ ] **P0** Log lifecycle events and every material action with initiating user, agent, skill/version/digest, session, policy decision, credential identity, tool, target, approval, result, and correlation ID. `[NIST-CSF, OWASP-AGENTIC]`
- [ ] **P0** Preserve end-to-end causation IDs across agents, tools, queues, and external services. `[NIST-COSAIS, OWASP-AGENTIC]`
- [ ] **P0** Record the exact action displayed for approval and the exact action executed. `[MCP-TOOLS, OWASP-AGENTIC]`
- [ ] **P0** Protect logs with restricted writers, integrity controls, trusted time, retention, and independent export. `[NIST-CSF, ISO-27001]`
- [ ] **P0** Redact secrets and unnecessary sensitive data while retaining security-relevant provenance. `[MCP-SECURITY, NIST-AI-600-1]`
- [ ] **P0** Alert on undeclared tools/destinations, permission drift, denied actions, injection indicators, secret access, unusual data volume, loops, cost spikes, and suspicious action sequences. `[OWASP-AGENTIC, MITRE-ATLAS]`
- [ ] **P0** Detect missing events, telemetry disablement, selective deletion, clock anomalies, and policy-engine outages. `[NIST-CSF, OWASP-AGENTIC]`
- [ ] **P1** Baseline activity by skill version, user/agent identity, environment, data class, and risk tier. `[NIST-CSF, MITRE-ATLAS]`
- [ ] **P1** Reconcile observed runtime skills, tools, servers, permissions, and versions against the approved inventory. `[AST10, NIST-CSF]`
- [ ] **P1** Attribute token, compute, tool, and external-service costs to the initiating identity and workflow. `[OWASP-AGENTIC]`

[← Incident response playbook](10-incident-response-playbook.md) · [Next: 30/60/90-day adoption roadmaps →](12-30-60-90-day-adoption-roadmaps.md)
