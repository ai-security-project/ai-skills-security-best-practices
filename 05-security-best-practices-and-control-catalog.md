# 5. Security best practices and control catalog

[← Chapter index](README.md)

> **This is the primary best-practices chapter.** Implement P0 controls as deployment gates, P1 controls before production or broad use, and P2 controls through a funded maturity plan.

## Design and instructions

| ID | Pri. | Control, scope, owner | Implementation | Verification | Evidence |
|---|---:|---|---|---|---|
| **DES-01** | P0 | **Purpose and risk boundary.** Baseline. Business owner. | MUST state one bounded purpose, users, environments, allowed data/actions, non-goals, worst credible effects, tier, and stop/escalation conditions. | Reviewer attempts to map every declared capability to purpose; undeclared and out-of-scope cases are denied. | Charter, tier rationale, capability/data map, owner acceptance. |
| **DES-02** | P0 | **Least-agency architecture.** Baseline; enhanced for Tier 3+. Security architect. | MUST minimize tools, permissions, autonomy, delegation depth, workflow duration, and blast radius. Separate planning, approval, and execution. | Attempt undeclared tool/resource use, scope expansion, self-approval, and delegation to broader authority. | Architecture, policy map, denial tests. |
| **DES-03** | P1 | **Safe defaults and failure.** Enhanced for writes or irreversible effects. Engineering owner. | MUST fail closed on authorization uncertainty, bound retries/time/cost, preserve recoverable state, and define rollback or compensation. | Inject timeout, malformed output, partial write, unavailable approver, and dependency failure. | Failure-mode analysis, test logs, recovery procedure. |
| **INS-01** | P0 | **Instruction hierarchy.** Baseline. Skill owner. | MUST label policy, task instructions, user input, retrieved data, and tool output by authority. Lower-authority content MUST NOT override policy. | Direct, indirect, nested, encoded, multilingual, and delayed override tests. | Versioned instruction specification and attack corpus results. |
| **INS-02** | P0 | **Behavioral contract.** Baseline. Product owner. | MUST define inputs, outputs, required checks, prohibited behavior, limitations, uncertainty handling, and exact conditions to stop or escalate. Critical invariants MUST be enforced outside prose. | Requirement-to-test trace for every boundary and prohibition. | Contract, tests, review record. |
| **INS-03** | P0 | **Untrusted-content separation.** Applies whenever external/user/tool content is processed. AppSec owner. | MUST pass content as data through constrained interfaces; sanitize active content; avoid dynamic concatenation into authoritative instructions; authorize proposed effects independently. | Poison webpages, documents, metadata, images/OCR, code comments, and tool outputs; verify no unauthorized effect. | Data-flow design, sanitization config, red-team results. |

## Identity, provenance, and supply chain

| ID | Pri. | Control, scope, owner | Implementation | Verification | Evidence |
|---|---:|---|---|---|---|
| **PRO-01** | P0 | **Immutable identity and integrity.** Baseline. Release owner. | MUST assign skill ID/version, enumerate included files, compute digests, and reject altered or unapproved artifacts. SHOULD sign and attest releases where the distribution path supports enforceable verification. | Change one byte/file and confirm publish, install, or load fails. | Manifest, digests, verification logs, signatures/attestations. |
| **PRO-02** | P1 | **Publisher and ownership verification.** Enhanced for third party/shared. Procurement or repository owner. | Verify legal/organizational owner, maintainer identities, source, support contact, transfer process, and vulnerability reporting route. | Trace deployed artifact to source, build, reviewers, publisher, and current owner. | Due diligence, CODEOWNERS/approvals, lineage record. |
| **SUP-01** | P0 | **Dependency control.** Applies to code, references, tools, models, schemas, datasets, and packages. Supply-chain owner. | MUST inventory and pin/constraint versions, verify integrity/license, scan, and block unreviewed substitution. Remote mutable references SHOULD be vendored or integrity-bound. | Replace a dependency or remote reference; gate must fail or trigger review. | SBOM/materials list, lockfiles, hashes, scan results. |
| **SUP-02** | P0 | **Controlled build and release.** Enhanced for executable/Tier 3+. Release engineering. | Protect branches and publishing identities; isolate build; require independent review; generate provenance; separate build from release; retain rollback artifacts. | Rebuild from recorded source and compare; attempt release from untrusted builder/identity. | CI policy, provenance, reproducibility result, release approvals. |
| **SUP-03** | P0 | **Update safety and compromised-publisher response.** Baseline. Platform owner. | MUST disable silent privilege expansion; diff instructions, permissions, dependencies, destinations, and behavior; canary; support pin/rollback; maintain denylist and emergency notice process. | Simulate malicious update and stolen publisher credential. | Diff report, canary logs, rollback test, compromise playbook. |

## Permissions, authorization, secrets, and data

| ID | Pri. | Control, scope, owner | Implementation | Verification | Evidence |
|---|---:|---|---|---|---|
| **AUT-01** | P0 | **Distinct identities.** Baseline. IAM owner. | MUST attribute action to initiating user/service, exact skill/version, agent/session, and executing service. Shared privileged accounts are prohibited. | Reconstruct sampled actions and distinguish initiator from executor. | Identity map, auth config, audit samples. |
| **AUT-02** | P0 | **Execution-time least privilege.** Baseline. Authorization owner. | Default deny. Scope by tool/action, resource/path, environment, tenant, purpose, destination, data class, amount, and time. Recheck at execution, not just plan creation. | Cross-resource, traversal, cross-environment, expired, replayed, and undeclared-action tests. | Policies, access review, denial logs. |
| **AUT-03** | P0 | **Cumulative capability policy.** Enhanced when multiple skills/tools operate. Security architect. | MUST evaluate combinations such as sensitive-read + archive + external-send. Delegation MUST attenuate authority. Isolate approvals, memory, and credentials by task. | Execute prohibited cross-skill sequences using individually allowed calls. | Composition graph, sequence policy, test results. |
| **AUT-04** | P0 | **Meaningful human approval.** Applies to consequential actions. Business process owner. | Bind approval to exact action, target, content hash/amount, identity, version, and short expiry. Show effect, destination, data, reversibility, and policy result. Prevent self-approval and replay. | Alter target/content after approval, replay, bundle requests, and test approval fatigue limits. | Approval policy/events, UX test, replay results. |
| **SEC-01** | P0 | **Credential delivery and lifecycle.** Any authenticated integration. Secrets owner. | Secrets MUST NOT appear in skill files, prompts, tool arguments unless strictly required, outputs, or logs. Use brokered, audience-bound, short-lived, scoped credentials; rotate and revoke. | Secret scans plus expiry, audience, scope, theft, and revocation tests. | Secret inventory, broker policy, scan and rotation logs. |
| **DAT-01** | P0 | **Data minimization and purpose binding.** Baseline. Data owner. | Enumerate fields and purpose; reject unnecessary data; redact/tokenize; prohibit undeclared secondary use and training; define residency and legal basis where applicable. | Sample transactions and inject unnecessary sensitive fields. | Data-flow/field inventory, privacy assessment, samples. |
| **DAT-02** | P0 | **Isolation, retention, and deletion.** Applies to state/logs/artifacts. Data governance owner. | Isolate users, tenants, tasks, environments, and skill memory; set retention; prevent stale instruction reuse; delete primary, cache, derived, and backup data per policy. | Cross-boundary access and end-to-end deletion test. | Retention schedule, isolation tests, deletion proof. |
| **DAT-03** | P0 | **Outbound data control.** Any network/output sink. Data protection owner. | Allowlist destinations and data classes; inspect payloads; block secret/high-risk patterns and covert encodings; require exceptional-disclosure approval. | Attempt disallowed domain, DNS/URL encoding, archive, oversized payload, and alternate channel exfiltration. | Egress policy, DLP events, blocked tests. |

## Code, execution, tools, and approvals

| ID | Pri. | Control, scope, owner | Implementation | Verification | Evidence |
|---|---:|---|---|---|---|
| **EXE-01** | P0 | **Input, command, and path safety.** Executable skills. Engineering owner. | Use typed schemas and allowlists; avoid shell interpolation; use argument arrays; canonicalize and constrain paths; reject traversal/symlinks as appropriate; safely parse untrusted formats. | Fuzz malformed, injected, ambiguous, oversized, traversal, archive, and encoding inputs. | Schemas, code review, fuzz results. |
| **EXE-02** | P0 | **Execution isolation.** Any code/command/active content. Runtime security. | Use disposable sandbox/container/VM as risk requires; non-root; read-only base; minimal mounted paths; blocked host sockets/devices; network deny by default; CPU/memory/time/process/output quotas; no persistence. | Escape, mount, metadata-service, forbidden network, fork bomb, disk fill, and persistence tests. | Sandbox baseline, test report, runtime policy. |
| **EXE-03** | P0 | **Tool contract validation.** Every tool/MCP call. Tool owner. | Strictly validate arguments and output schema; constrain targets; independently authenticate/authorize; treat descriptions/results as untrusted; do not infer approval from prose. | Schema confusion, tool-name collision, forged result/approval, out-of-range and unexpected-field tests. | Tool schema, enforcement code, contract tests. |
| **EXE-04** | P1 | **Transaction and replay safety.** State-changing workflows. Service owner. | Use idempotency keys, preconditions, bounded retries, duplicate detection, prepare/commit where appropriate, reconciliation, and compensating actions. | Replay and interrupt between every step; confirm no duplicate or partial unsafe effect. | Transaction design, chaos tests, reconciliation logs. |
| **OVR-01** | P0 | **Stop, suspend, and revoke.** Enhanced for autonomous/long-running. Operations owner. | Provide pause/cancel, credential and capability revocation, version/hash deny, task budget, escalation, and safe terminal state. | Stop an active workflow and prove no further effects or credential use. | Kill-switch drill, revocation logs, safe-state proof. |

## Testing, deployment, operations, and governance

| ID | Pri. | Control, scope, owner | Implementation | Verification | Evidence |
|---|---:|---|---|---|---|
| **TST-01** | P0 | **Independent review and threat modeling.** Before release/material change. AppSec. | Review metadata, instructions, hidden content, code, dependencies, permissions, destinations, update path, abuse cases, and cross-skill flows. | Reviewer traces each threat to prevention, detection, response, acceptance, or prohibition. | Threat model, review form, findings and closure. |
| **TST-02** | P0 | **Layered assurance.** Baseline; enhanced for Tier 3+. Test owner. | Combine lint/schema validation, code review, SAST/SCA/secret scans, instruction review, sandbox tests, behavioral/adversarial/abuse testing, and post-change regression. | Seed known defects and malicious semantics; verify relevant gates detect them. | Tool configs, corpora, results, seeded-control test. |
| **OPS-01** | P0 | **Approved inventory and configuration.** Production/broad use. Portfolio owner. | Track ID/version/hash, owner, tier, source, dependencies, users, platforms, environments, identities, permissions, destinations, approvals, review date, status, and retirement. Detect shadow copies. | Reconcile runtime/endpoint/registry observations to inventory. | Inventory, configuration baseline, reconciliation report. |
| **OPS-02** | P0 | **Audit and detection.** Baseline; behavioral correlation for Tier 3+. SOC owner. | Log lifecycle changes and each material action: initiator, skill/version, session, policy decision, credential identity, tool, target, data class, approval, result, and correlation ID. Redact secrets. Detect anomalies and sequences. | Simulate injection, denial, sensitive-read→send, drift, runaway loop, and log outage. | Event schema, detections, alert tests, retention policy. |
| **OPS-03** | P0 | **Incident readiness.** Baseline. Incident response owner. | Maintain triage, disablement, token rotation, quarantine, scoping, evidence, notification, clean restoration, and reapproval procedures. Exercise by tier. | Tabletop and technical containment drill. | Playbook, exercise timing, actions and closure. |
| **GOV-01** | P0 | **Policy and accountability.** Baseline. Executive risk owner. | Assign business, technical, security, data, platform, and response owners. Define prohibited uses, tier gates, decision rights, training, and consequences. | Sample skills for complete and current ownership and decisions. | Policy, RACI, training, acceptance records. |
| **GOV-02** | P0 | **Intake, approval, third-party, and exceptions.** Baseline. GRC/procurement. | Use standard intake and evidence; apply hard stops; assess supplier and contract; record residual risk. Exceptions MUST be narrow, monitored, expiring, and auto-escalated. | Sample approvals and expired exceptions; test that expiry removes access. | Intake/review, contracts, exception register, expiry logs. |
| **GOV-03** | P1 | **Periodic assurance and executive reporting.** Baseline. GRC. | Reassess by tier and on triggers; report inventory gaps, high-risk exposure, overdue reviews, exceptions, incidents, drift, control tests, and corrective actions. | Trace reported metrics to source and sample operating effectiveness. | Review calendar, evidence samples, leadership reports. |
| **POR-01** | P0 | **Platform portability review.** Whenever host/platform changes. Architecture owner. | Re-map instruction precedence, discovery/loading, supported metadata, actual permissions, approval semantics, sandbox, filesystem/network access, credentials, logging, and update behavior. Unsupported security metadata MUST fail closed or have a compensating control. | Run equivalent negative and behavioral tests on each target platform. | Platform mapping, gap/risk assessment, retest and approval. |

## Limits of automated scanning

Scanners are valuable for secrets, known vulnerable packages, dangerous API patterns, suspicious URLs, obfuscation, and schema errors. They cannot reliably determine whether natural-language steps are deceptive, whether a permission is justified by business purpose, whether a remote reference will change, whether several benign tools form a harmful chain, or whether a model will follow injected content. Scanner success MUST NOT replace manual semantic review, runtime enforcement, adversarial testing, or monitoring.

## Chapter checklist

Source tags resolve in the [source catalog](13-sources.md).

- [ ] **P0** Minimize agency: prefer deterministic workflows where open-ended planning is unnecessary. `[OWASP-AGENTIC, NIST-AI-600-1]`
- [ ] **P0** Put deterministic enforcement outside the model for every critical invariant. `[CURSOR-HARDENING, GOOGLE-ADK, OPENAI-SAFETY]`
- [ ] **P1** State platform-specific assumptions and refuse unsupported hosts rather than silently weakening controls. `[AST10, AGENT-SKILLS-SPEC]`
- [ ] **P0** Use distinct identities for initiating user/service, agent, exact skill version, host, and executing tool/service. `[NIST-ZTA, GOOGLE-IDENTITY]`
- [ ] **P0** Prohibit shared privileged accounts and ambient personal administrator credentials. `[NIST-ZTA, OWASP-AGENTIC]`
- [ ] **P0** Default deny and authorize at execution time—not only when the plan is created. `[NIST-ZTA, OWASP-AGENTIC]`
- [ ] **P0** Scope authorization by action, resource, path, tenant, environment, purpose, destination, data class, amount, time, and task. `[NIST-ZTA, OWASP-AGENTIC]`
- [ ] **P0** Ensure delegated authority can only stay the same or decrease; cap delegation depth and duration. `[OWASP-AGENTIC, NIST-COSAIS]`
- [ ] **P0** Evaluate cumulative capability and workflow sequences, not only individual tool calls. `[OWASP-AGENTIC, NIST-COSAIS]`
- [ ] **P0** Require meaningful approval for destructive, privileged, externally visible, financial, legal, safety-critical, persistent, or sensitive-data actions. `[MCP-TOOLS, OWASP-AGENTIC]`
- [ ] **P0** Show approvers the exact tool, action, target, recipient, arguments, data, amount, side effect, reversibility, and policy result. `[MCP-TOOLS, OPENAI-SAFETY]`
- [ ] **P0** Bind approval to exact arguments/content hash, identity, skill/tool version, and short expiry. `[OWASP-AGENTIC, MICROSOFT-HOOKS]`
- [ ] **P0** Reapprove after any argument, target, identity, content, permission, or tool transformation. `[MICROSOFT-HOOKS]`
- [ ] **P0** Prevent self-approval, approval replay, approval laundering, hidden bundling, and stale approval reuse. `[OWASP-AGENTIC, MCP-SECURITY]`
- [ ] **P1** Rate-limit and aggregate prompts to reduce approval fatigue without concealing distinct effects. `[OWASP-AGENTIC]`
- [ ] **P1** Preserve denies over allows and make critical policy-hook failures fail closed. `[CLAUDE-PERMISSIONS, CURSOR-HOOKS]`
- [ ] **P0** Keep secrets out of prompts, skill files, model context, memory, generated code, logs, tool results, and sandbox environments. `[NIST-SSDF, OWASP-AGENTIC]`
- [ ] **P0** Broker short-lived, task-bound, audience-bound, least-privilege credentials at the execution boundary. `[NIST-ZTA, MCP-AUTH]`
- [ ] **P0** Store long-lived credentials in an approved secret manager; rotate and revoke them independently of the skill. `[GOOGLE-ADK, NIST-SSDF]`
- [ ] **P0** Validate token signature, issuer, expiry, audience/resource, scopes, and authorization context on every request. `[MCP-AUTH, MCP-SECURITY]`
- [ ] **P0** Accept only tokens issued for the MCP server; never use generic or unrelated audiences. `[MCP-AUTH]`
- [ ] **P0** Never pass the client bearer token through to a downstream API; obtain a separate downstream token. `[MCP-AUTH, MCP-SECURITY]`
- [ ] **P0** Use OAuth authorization code flow with PKCE, exact redirect validation, CSRF/state protection, and per-client consent where applicable. `[MCP-AUTH, MCP-SECURITY]`
- [ ] **P0** Constrain dynamic client registration, metadata discovery, and redirects against impersonation and SSRF. `[MCP-SECURITY]`
- [ ] **P0** Bind local servers to loopback, validate `Origin`, and authenticate local connections. `[MCP-SECURITY]`
- [ ] **P0** Never use `Mcp-Session-Id` or possession of an opaque state handle as authorization. `[MCP-SECURITY]`
- [ ] **P1** Encrypt token storage, expire caches, detect theft, and test revocation during active workflows. `[MCP-SECURITY, NIST-ZTA]`
- [ ] **P0** Reassess every target host; identical Markdown does not imply identical security behavior. `[AST10, AGENT-SKILLS-SPEC]`
- [ ] **P0** Map actual instruction precedence, skill discovery, invocation, workspace trust, permission, approval, sandbox, network, filesystem, hook, logging, and update semantics. `[AST10, CURSOR-HARDENING, CLAUDE-PERMISSIONS]`
- [ ] **P0** Confirm whether `allowed-tools` grants, restricts, or is ignored; the open specification marks it experimental. `[AGENT-SKILLS-SPEC, CLAUDE-SKILLS]`
- [ ] **P0** Confirm whether hooks fail open or fail closed and configure critical hooks to block on crash, timeout, invalid output, and policy unavailability. `[CURSOR-HOOKS, CLAUDE-HOOKS]`
- [ ] **P0** Verify ignore files, workspace trust, and UI approvals against terminal, MCP, plugin, subprocess, and non-interactive execution paths. `[CURSOR-HARDENING, CLAUDE-PERMISSIONS]`
- [ ] **P0** Treat remote MCP content and annotations as untrusted even when the server is authenticated. `[MCP-TOOLS, MICROSOFT-SKILLS]`
- [ ] **P0** Fail closed or add a tested compensating control when the destination platform cannot enforce required metadata or policy. `[AST10, NIST-ZTA]`
- [ ] **P1** Repeat negative and behavioral tests on every supported platform and version. `[AST10, NIST-AI-RMF]`

[← Risk tiering and control profiles](04-risk-tiering-and-control-profiles.md) · [Next: Role-specific implementation checklists →](06-role-specific-implementation-checklists.md)
