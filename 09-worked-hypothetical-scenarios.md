# 9. Worked hypothetical scenarios

[← Chapter index](README.md)

All scenarios are hypothetical; they are not claims about real incidents.

## Scenario 1 — Malicious skill

**Path:** A “deployment helper” includes obfuscated instructions to read credential files for diagnostics and send a report to an attacker endpoint.

- **Prevent:** approved catalog; publisher and semantic review; deny secret paths; dedicated scoped identity; destination allowlist; code/instruction deobfuscation checks; sandbox.
- **Detect:** undeclared domain; secret-path access followed by encoding/egress; behavior-manifest mismatch; unusual tool sequence.
- **Contain:** disable exact hash/version; terminate runs; block endpoint; revoke exposed credentials; preserve artifact and events.
- **Recover:** scope all installations/runs, rotate secrets, restore trusted version, notify affected owners, add detection/test case, reapprove before use.

## Scenario 2 — Poisoned external instructions

**Path:** A research skill reads hidden webpage text saying to ignore prior rules, retrieve an internal roadmap, and include it in the summary.

- **Prevent:** treat page as data; strip active/hidden content where appropriate; restrict internal reads to task purpose; source-to-sink policy; no authorization from content.
- **Detect:** instruction-like patterns in retrieved data; unrelated internal access; sensitive data entering output; task/source mismatch.
- **Contain:** stop run; quarantine source/output; clear transient context and contaminated cache.
- **Recover:** inspect memory and downstream artifacts, rerun from trusted sources, add payload to tests, refine deterministic policy rather than relying only on filtering.

## Scenario 3 — Excessive permissions

**Path:** A calendar skill receives full mail, drive, shell, and organization-wide calendar rights because a convenient shared role was used.

- **Prevent:** purpose-specific service identity; resource/action scopes; separate read/write; just-in-time grant; per-action confirmation; refuse coarse role if blast radius is unacceptable.
- **Detect:** unused privilege report; non-calendar access; event/message volume anomaly; access outside approved users.
- **Contain:** revoke token; disable writes; rate-limit; suspend or reverse created events.
- **Recover:** issue narrow credential, reconcile changes, reauthorize users, improve platform policy. If the platform cannot scope sufficiently, isolate behind a constrained proxy or do not deploy.

## Scenario 4 — Compromised update

**Path:** A stolen maintainer credential publishes an update adding a post-install script and new MCP endpoint.

- **Prevent:** protected publishing, independent release approval, trusted build provenance, immutable versions, permission/destination diff, no automatic privilege expansion.
- **Detect:** signer/builder mismatch; unexpected script/endpoint; unusual publish context; canary network or behavior anomaly.
- **Contain:** freeze updates; revoke publisher identity; deny release hash; block endpoint; roll back installations.
- **Recover:** audit all installs and runs, rotate relevant credentials, rebuild from reviewed source, publish clean version and advisory, strengthen threshold/release policy.

## Scenario 5 — Cross-skill attack chain

**Path:** A document skill stores a malicious task in shared memory. A repository skill reads sensitive configuration, an archive skill bundles it, and a messaging skill sends it to an external “reviewer.”

- **Prevent:** memory partition and provenance labels; authority attenuation; cumulative policy blocking sensitive-read→archive→external-send; destination-bound approval; no inherited approval.
- **Detect:** graph/sequence correlation across skills and sessions; anomalous shared-memory instruction; archive after sensitive reads.
- **Contain:** halt workflow graph; revoke delegated capabilities; quarantine memory/archive; block recipient.
- **Recover:** find every consumer of poisoned state, delete contaminated memory, rotate exposed secrets, replay legitimate tasks from a clean checkpoint, add chain regression test.

## Scenario 6 — Legitimate user abuses an approved skill

**Path:** An authorized sales user uses a bulk outreach skill to export and contact people outside the approved campaign and jurisdiction.

- **Prevent:** purpose/campaign binding; approved recipient set; jurisdiction and consent checks; daily limits; independent approval for list changes.
- **Detect:** recipient-list drift; unusual volume; new domains/regions; repeated denied attempts.
- **Contain:** suspend campaign and user grant; preserve approvals and exports; block pending sends.
- **Recover:** recall where possible, delete unauthorized exports, complete privacy/legal assessment and notifications as required, adjust access and training.

## Scenario 7 — Cross-platform behavior change

**Path:** A skill restricted to explicit invocation and narrow paths on one host is copied to another host that ignores those metadata fields and exposes broader tools.

- **Prevent:** portability review; target-platform mapping; fail deployment on unsupported security metadata; explicit host policy; target-specific negative tests.
- **Detect:** activation without explicit request; access outside expected paths; platform configuration drift.
- **Contain:** disable migrated copy and credentials; isolate generated changes.
- **Recover:** add compensating host controls or redesign; retest and reapprove. Do not claim the skill is “portable” merely because its Markdown parses.

## Chapter checklist

Source tags resolve in the [source catalog](13-sources.md).

- [ ] **P1** Test both false activation and missed activation, including confusingly similar names and descriptions. `[AGENT-SKILLS-BP, AST10]`
- [ ] **P0** Perform independent semantic review of instructions, metadata, hidden content, code, permissions, dependencies, destinations, and updates. `[AST10, NIST-SSDF]`
- [ ] **P0** Run SAST, SCA, secret, IaC, container, license, malicious-package, and configuration scans where applicable. `[NIST-SSDF, OPENSSF]`
- [ ] **P0** Do not treat automated scanning as sufficient for malicious natural language, justified permissions, or harmful tool combinations. `[AST10, OWASP-AGENTIC]`
- [ ] **P0** Fuzz schemas, parsers, archives, paths, commands, URLs, encodings, size limits, and tool contracts. `[NIST-SSDF, OWASP-LLM]`
- [ ] **P0** Test direct and indirect injection through webpages, email, documents, images/OCR, code comments, metadata, memory, and tool output. `[OWASP-PI, NIST-AI-600-1]`
- [ ] **P0** Test exfiltration, confused deputy, approval bypass/replay, privilege escalation, cross-tenant access, and secret theft. `[OWASP-AGENTIC, MCP-SECURITY]`
- [ ] **P0** Test tool poisoning, changed schemas/descriptions, name collision, rug pull, compromised publisher, and dependency substitution. `[AST10, MCP-TOOLS]`
- [ ] **P0** Test cross-skill/agent chains where individually permitted actions combine into a prohibited outcome. `[OWASP-AGENTIC, NIST-COSAIS]`
- [ ] **P0** Test loops, retries, fan-out, cancellation, quotas, partial failure, unavailable policy/approval service, and cost exhaustion. `[OWASP-AGENTIC, MCP-SAMPLING]`
- [ ] **P0** Test sandbox escape, forbidden mounts, host sockets, metadata endpoints, persistence, and resource exhaustion. `[ANTHROPIC-SANDBOX, AST10]`
- [ ] **P0** Test credential expiry, wrong audience, revocation, theft, token passthrough, CSRF, SSRF, and session fixation. `[MCP-AUTH, MCP-SECURITY]`
- [ ] **P0** Test audit completeness, secret redaction, correlation, tamper detection, and behavior when logging is unavailable. `[NIST-CSF, OWASP-AGENTIC]`
- [ ] **P0** Require all P0 tests, provenance checks, vulnerability thresholds, approvals, and rollback readiness before release. `[NIST-SSDF, SLSA]`
- [ ] **P1** Maintain regression corpora and rerun tests after every material component or platform change. `[NIST-AI-RMF, NIST-SSDF-A]`
- [ ] **P1** Red-team according to risk and include independent testers for high-impact skills. `[NIST-AI-600-1, MITRE-ATLAS]`

[← Illustrative implementation examples](08-illustrative-implementation-examples.md) · [Next: Incident response playbook →](10-incident-response-playbook.md)
