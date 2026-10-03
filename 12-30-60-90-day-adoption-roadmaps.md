# 12. Prioritized 30/60/90-day adoption roadmaps

## Minimum defensible baseline

Before expanding adoption:

- inventory every skill and owner;
- classify risk before installation;
- verify origin and immutable version;
- review instructions, code, dependencies, destinations, and permission differences;
- default-deny tools, resources, filesystem paths, network destinations, and data flows;
- deliver short-lived credentials through a broker rather than the model context;
- isolate executable code and untrusted content;
- require scoped approval for consequential actions;
- log the skill version, initiating identity, authorization, tool call, target, approval, and outcome;
- detect cumulative cross-skill behavior;
- support immediate disablement, credential revocation, rollback, and retirement; and
- reassess after every material change or platform migration.

## Small team

**Days 0–30 — contain unknown risk**

- Name a program owner and inventory all production/pilot skills, versions, tools, credentials, and owners.
- Freeze unknown or unowned Tier 3+ skills.
- Adopt tiering, intake, review, hard stops, and exceptions.
- Restrict highest-risk credentials/destinations and establish a manual kill switch.
- Review skills that execute code, access production/sensitive data, communicate externally, move money, or decide consequential outcomes.

Exit: complete high-risk list, accountable owners, decisions, and tested emergency contact/procedure.

**Days 31–60 — establish enforceable baseline**

- Centralize approved immutable versions and integrity records.
- Add capability/destination controls and baseline audit events.
- Test prompt injection, exfiltration, unauthorized actions, sandbox, revocation, and rollback.
- Establish incident contacts and run a tabletop.
- Set review and exception expiry.

Exit: policy/test evidence, sample logs, remediations, and tabletop report.

**Days 61–90 — automate and measure**

- Automate manifest, secret, dependency, permission-diff, and regression gates.
- Alert on denied actions, drift, new destinations, sensitive-read→send, and loops.
- Reconcile observed skills to inventory.
- Publish initial metrics with limitations.
- Retire unsupported/unowned high-risk skills.

## Large enterprise

**Days 0–30 — governance and discovery**

- Establish executive sponsor and cross-functional business, platform, AppSec, SOC, IAM, data/privacy, legal, procurement, and GRC owners.
- Define taxonomy, tiers, prohibited uses, evidence, and decision rights.
- Discover skills across endpoints, repositories, catalogs, agent platforms, CI, and business units.
- Quarantine unknown Tier 4/5 deployments; identify regulatory/regional and supplier obligations.

**Days 31–60 — platform and supplier foundations**

- Launch governed registry/catalog and federated ownership.
- Integrate IAM/credential brokering, deterministic policy, sandbox/egress, audit pipeline, and inventory.
- Establish Tier 3–5 architecture/testing patterns and supplier provenance/change/incident clauses.
- Pilot with representative local, cloud, CI, and third-party platforms.
- Build SOC detections and response procedures.

**Days 61–90 — enforce high-risk gates**

- Enforce release/install/update gates for Tier 3+.
- Integrate inventory with asset, risk, change, procurement, and incident systems.
- Run cross-skill, publisher-compromise, credential-revocation, and fleet-disable exercises.
- Report exposure and control effectiveness by business unit and tier.
- Fund post-90-day legacy remediation, continuous assurance, and independent evaluation.

## Chapter checklist

Source tags resolve in the [source catalog](13-sources.md).

- [ ] **P0** Assign named business, technical, security, privacy/data, platform, and incident-response owners. `[NIST-AI-RMF, NIST-CSF, ISO-42001]`
- [ ] **P0** Give the skill a unique ID, owner, version, immutable digest, lifecycle state, and support contact. `[AST10, NIST-SSDF]`
- [ ] **P0** Inventory all skill files, scripts, hooks, prompts, references, assets, tools, MCP servers, models, datasets, memories, identities, credentials, dependencies, and destinations. `[AST10, OWASP-AGENTIC, NIST-AI-600-1]`
- [ ] **P0** Record where every copy is installed, who installed it, who can invoke it, and its last review and scan status. `[AST10]`
- [ ] **P0** Define intended users, purpose, allowed environments, data, actions, destinations, and explicit non-goals. `[NIST-AI-RMF, NIST-AI-600-1]`
- [ ] **P0** Define prohibited uses and hard-stop conditions, including uses the model must not attempt. `[NIST-AI-RMF, OWASP-AGENTIC]`
- [ ] **P1** Integrate skills into CMDB/asset management, IAM, vulnerability management, SOC, procurement, and offboarding. `[AST10, NIST-CSF]`
- [ ] **P1** Establish coordinated vulnerability disclosure and security contact procedures. `[NIST-SSDF, OPENSSF]`
- [ ] **P1** Canary releases, monitor them, retain known-good artifacts, and test rollback. `[CISA-AI, NIST-SSDF]`
- [ ] **P1** Continuously monitor vulnerabilities, malicious-package reports, maintainer changes, repository archival, and end-of-life notices. `[NIST-SSDF, OPENSSF]`
- [ ] **P1** Define a publisher-compromise response including denylisting versions/hashes, fleet disablement, credential rotation, and notification. `[AST10, NIST-CSF]`

[← Maturity model and metrics](11-maturity-model-and-metrics.md) · [Next: Sources →](13-sources.md)
