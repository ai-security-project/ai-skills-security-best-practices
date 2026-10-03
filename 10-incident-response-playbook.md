# 10. Incident response playbook

Unauthorized action, suspicious skill selection, prompt-injection success, data disclosure, credential exposure, supply-chain warning, permission drift, unexpected destination, runaway activity, cross-tenant access, log failure, or publisher compromise.

## 1. Triage and declare

1. Open an incident and assign severity/commander.
2. Record skill ID/version/hash, platform, environment, initiator, agent/session, execution identity, model, tools/MCP servers, destinations, and time range.
3. Determine whether actions continue, credentials are exposed, and regulated/safety-critical systems or data are involved.
4. Preserve relevant artifacts and audit records with controlled access. Avoid unnecessary collection of sensitive prompts/content.

## 2. Contain

1. Suspend discovery/activation and deny the affected hash/version.
2. Stop active and scheduled runs where safe.
3. Revoke sessions, tokens, delegated credentials, publisher/build identities, and approvals as relevant.
4. Block malicious domains, MCP servers, packages, artifacts, and update channels.
5. Quarantine shared memory, outputs, and downstream artifacts.
6. Verify containment from runtime events, not only administrative UI state.

## 3. Investigate and scope

1. Reconstruct publisher→install→load→instruction/retrieval→authorization→tool→effect.
2. Distinguish malicious content, compromised supply chain, model error, authorization defect, host weakness, misuse, and monitoring failure.
3. Identify every installation, invocation, identity, data object, system, recipient, and downstream consumer.
4. Validate audit completeness; note uncertainty explicitly.

## 4. Eradicate and recover

1. Remove malicious/vulnerable artifacts and poisoned state.
2. Rotate credentials and correct permissions, policies, isolation, approvals, and detections.
3. Rebuild from reviewed source on a trusted path.
4. Re-run abuse and regression tests.
5. Restore by controlled canary with enhanced monitoring and explicit reapproval.
6. Reconcile and reverse unauthorized effects where possible.

## 5. Notify

Engage security, business, privacy, legal, compliance, safety, supplier, customer, insurer, and regulator processes according to established obligations. Communicate confirmed facts, uncertainty, containment status, user actions, and update times.

## 6. Learn and close

Complete root-cause analysis; update controls, catalog intelligence, tests, detections, platform policy, supplier requirements, and training; track actions to verified closure; decide reapproval or retirement.

Measure time to detect, suspend, terminate effects, revoke credentials, determine scope, notify, recover, and close corrective action.

## Chapter checklist

Source tags resolve in the [source catalog](13-sources.md).

- [ ] **P0** Maintain an AI/agent-specific playbook integrated with the organizational incident process. `[OWASP-IR, NIST-800-61]`
- [ ] **P0** Provide independently enforceable pause/kill controls for agent, skill version/hash, tool, MCP server, credential, tenant, queue, and network egress. `[OWASP-AGENTIC, NIST-CSF]`
- [ ] **P0** Test that stopping active work prevents further effects, queued actions, retries, delegation, and credential use. `[OWASP-AGENTIC, NIST-CSF]`
- [ ] **P0** On suspected compromise, revoke credentials/sessions, block egress, disable integrations, quarantine memory/artifacts, and preserve evidence. `[OWASP-IR, NIST-800-61]`
- [ ] **P0** Capture skill/model/tool versions, hashes, prompts, memory, identities, approvals, destinations, logs, and affected resources for scoping. `[OWASP-IR, NIST-800-61]`
- [ ] **P0** Restore only from verified known-good artifacts and prevent poisoned memory or state from re-entering production. `[NIST-CSF, OWASP-AGENTIC]`
- [ ] **P0** Re-threat-model, retest, and reapprove before reactivation. `[NIST-AI-RMF, NIST-SSDF]`
- [ ] **P1** Exercise malicious update, publisher compromise, injection-driven exfiltration, cross-agent propagation, credential theft, and fleet-disable scenarios. `[AST10, OWASP-IR]`
- [ ] **P1** Feed incident findings into controls, tests, detections, supplier reviews, and user training. `[NIST-CSF, NIST-AI-RMF]`
- [ ] **P0** At retirement, revoke identities and keys, disable installations and integrations, remove catalog entries, and notify users. `[NIST-CSF, ISO-27001]`
- [ ] **P0** Delete or archive data, memory, artifacts, and logs according to policy while retaining required incident/audit evidence. `[ISO-27001, NIST-CSF]`

[← Worked hypothetical scenarios](09-worked-hypothetical-scenarios.md) · [Next: Maturity model and metrics →](11-maturity-model-and-metrics.md)
