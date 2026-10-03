# 2. Lifecycle model and security gates

[← Chapter index](README.md)

Every phase produces evidence for the next. Skipping a gate requires a documented exception; an emergency response may suspend or revoke first and document immediately after containment.

| Phase | Main risks | Mandatory gate and retained evidence |
|---|---|---|
| **Design** | excessive purpose, unsafe autonomy, unclear stop conditions | Named owner; purpose and non-goals; initial risk tier; capability/data map; misuse cases |
| **Authoring** | hidden directives, unsafe scripts, secrets, injection-prone templates | Peer review; instruction hierarchy; secure coding; secret scan; dependency inventory |
| **Testing** | unknown boundary behavior, false confidence from happy paths | Functional, negative, adversarial, authorization, isolation, failure, and composition results |
| **Publishing** | publisher impersonation, tampering, misleading metadata | Verified publisher; immutable version/digest; reviewed manifest; changelog; signature/attestation where supported |
| **Discovery** | poisoned search, deceptive names/descriptions, shadow catalogs | Approved catalogs; metadata validation; risk and ownership visible before selection |
| **Procurement** | weak supplier practices, abandonment, contractual gaps | Third-party assessment; security/update/incident terms; exit and continuity plan |
| **Installation** | substituted artifact, scope mismatch, unsafe defaults | Digest/provenance verification; platform compatibility review; sandbox installation; inventory record |
| **Loading** | automatic exposure of descriptions or full content, context poisoning | Policy-filtered discovery; explicit invocation for sensitive skills; content hash recorded |
| **Activation** | wrong trigger, stale approval, skill collision | Exact skill/version selected; user/task context bound; required approval and credential issuance |
| **Execution** | injection, unauthorized tools, code escape, exfiltration, loops | Per-action policy decision; isolated execution; source-to-sink controls; resource limits; audit event |
| **Monitoring** | invisible misuse, log leakage, fragmented chains | Correlated telemetry; anomaly and sequence detections; tested response ownership |
| **Update** | semantic drift, dependency swap, new permissions/destinations | Treat as new release; permission and behavior diff; retest; canary; rollback; reapproval when material |
| **Suspension** | continued scheduled or cached execution | Block activation and new credentials; terminate active runs as appropriate; preserve evidence |
| **Revocation** | residual tokens, installed copies, trusted signatures | Revoke identities/keys; deny hashes/versions; block destinations; verify enforcement fleet-wide |
| **Retirement** | orphaned automations, retained data, fallback to unsafe versions | Remove discovery/install paths; migrate workflows; delete state; revoke access; confirm zero active use |

## Material-change triggers

Re-review is mandatory when any of these change:

- instructions that affect action choice, scope, stopping, escalation, or data handling;
- publisher, owner, repository, build, registry, signing identity, or update channel;
- scripts, binaries, dependencies, model, linked content, or generated artifacts;
- tools, MCP servers, permissions, resources, credentials, destinations, or network behavior;
- data class, retention, region, tenant model, user population, or environment;
- autonomy, schedule, delegation, approval behavior, limits, or potential impact; or
- host platform, execution mode, or instruction precedence.

## Chapter checklist

Source tags resolve in the [source catalog](13-sources.md).

- [ ] **P1** Use progressive disclosure; load only the minimum metadata and content needed for the current task. `[AGENT-SKILLS-SPEC]`
- [ ] **P1** Make activation explicit for sensitive skills and constrain activation to known skill identifiers. `[AGENT-SKILLS-CLIENT, CURSOR-SKILLS]`
- [ ] **P1** Define deterministic collision and precedence rules for duplicate skill and tool names. `[MCP-TOOLS, AST10]`
- [ ] **P1** Keep linked references local, immutable, or integrity-bound where possible; treat fetched content as untrusted. `[AST10, CLAUDE-MCP]`
- [ ] **P0** Obtain skills only from approved publishers, repositories, registries, or organization marketplaces. `[AST10, CISA-SBD]`
- [ ] **P0** Generate a manifest of every included file and verify its digest before load and execution. `[SLSA, NIST-SSDF]`
- [ ] **P0** Pin skill versions, commits, dependencies, images, actions, tools, models, schemas, and remote references to immutable identifiers. `[SLSA, OPENSSF, AST10]`
- [ ] **P0** Verify signatures and attestations against an approved identity and policy; remember that integrity does not prove benign behavior. `[SIGSTORE, SLSA]`
- [ ] **P0** Produce and verify build provenance linking source revision, builder, inputs, parameters, and artifact digest. `[SLSA, NIST-SSDF]`
- [ ] **P0** Maintain an SBOM/materials inventory that includes transitive code, model, data, prompt, tool, and remote-reference dependencies. `[NIST-SSDF-A, OPENSSF]`
- [ ] **P0** Protect branches, tags, CI, registries, release identities, signing keys, and maintainer accounts with least privilege and MFA. `[SLSA, OPENSSF]`
- [ ] **P0** Build in isolated environments without production credentials and separate build from release authority. `[SLSA, NIST-SSDF]`
- [ ] **P0** Detect typosquatting, dependency confusion, publisher takeover, unexpected install scripts, and anomalous transitive additions. `[AST10, OPENSSF]`
- [ ] **P0** Diff instructions, metadata, permissions, destinations, dependencies, hooks, and behavior before every update. `[AST10, OWASP-AGENTIC]`
- [ ] **P0** Block silent privilege expansion and require reapproval for material changes. `[AST10, NIST-SSDF]`
- [ ] **P0** Treat newly cloned repositories and project-provided skills as untrusted until the workspace is explicitly trusted. `[AGENT-SKILLS-CLIENT, CLAUDE-PERMISSIONS]`
- [ ] **P0** Review any `allowed-tools`, hooks, MCP servers, helper commands, environment changes, and plugin content before opening or invoking a repository skill. `[CLAUDE-SKILLS, CURSOR-HARDENING]`
- [ ] **P0** Do not let a repository approve its own tools, server, publisher, or trust decision. `[CLAUDE-MCP, AGENT-SKILLS-CLIENT]`
- [ ] **P0** Separate permission to discover metadata, load instructions, read resources, execute scripts, and access external services. `[AGENT-SKILLS-CLIENT, MICROSOFT-SKILLS]`
- [ ] **P0** Restrict skill roots to approved directories and reject traversal, unsafe symlinks, device files, and path escapes. `[AGENT-SKILLS-CLIENT, OWASP-LLM]`
- [ ] **P0** Bound archive size, expanded size, file count, depth, extension, and decompression ratio. `[MICROSOFT-SKILLS, OWASP-LLM]`
- [ ] **P0** Validate frontmatter and metadata with strict schemas, lengths, types, encodings, and safe parsers. `[AGENT-SKILLS-SPEC, AST10]`
- [ ] **P0** Treat names, descriptions, icons, authors, ratings, licenses, and compatibility metadata as untrusted claims. `[AST10, MCP-TOOLS]`
- [ ] **P0** Prevent automatic execution of bundled scripts merely because a skill was discovered or loaded. `[AGENT-SKILLS-CLIENT, MICROSOFT-SKILLS]`
- [ ] **P1** Bound scanning directories, recursion depth, file sizes, parsing time, and catalog size. `[AGENT-SKILLS-CLIENT, OWASP-AGENTIC]`

[← System definition and boundaries](01-system-definition-and-boundaries.md) · [Next: Threat model →](03-threat-model.md)
