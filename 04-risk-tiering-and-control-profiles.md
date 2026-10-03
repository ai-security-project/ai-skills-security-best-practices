# 4. Risk tiering and control profiles

Score each dimension from 1 to 5. The overall tier is the **highest** score, not an average. Raise one tier, up to Tier 5, if composition materially increases authority or if uncertainty is high.

| Score | Capability | Data | Autonomy | Exposure | Potential impact |
|---|---|---|---|---|---|
| **1** | generate/read public data | public | advice only | isolated | negligible, reversible |
| **2** | bounded low-impact tools | internal | approval per action | authenticated internal | minor |
| **3** | external write or isolated code | confidential/personal | bounded multi-step | third party or limited internet | material operational/privacy |
| **4** | production/admin/financial action | regulated/restricted/credentials | long-running delegated work | public/adversarial or broad egress | severe legal, financial, security, safety |
| **5** | security-critical, self-modifying, agent-creating, or physical action | bulk crown-jewel or safety-critical | open-ended planning/delegation | untrusted at scale or cross-tenant | catastrophic/systemic |

Tiers:

- **Tier 1 — Minimal:** baseline controls; creator peer review; annual review.
- **Tier 2 — Moderate:** baseline plus independent installer review and six-month review.
- **Tier 3 — Significant:** enhanced AppSec review, sandbox, destination controls, behavioral tests, SOC monitoring, quarterly review.
- **Tier 4 — High:** independent authorization, short-lived credentials, dual control where appropriate, canary, formal incident exercise, monthly control monitoring.
- **Tier 5 — Critical:** default prohibition. Deployment requires an approved safety case, executive risk acceptance, independent assurance, continuous monitoring, strict bounded autonomy, and a tested fail-safe. Some uses remain unacceptable.

Automatic minimum Tier 3 triggers: sensitive data, arbitrary or generated code execution, production writes, external communication, transfers of value, security administration, identity decisions, employment/credit/health/legal or other consequential decisions.

## Chapter checklist

Source tags resolve in the [source catalog](13-sources.md).

- [ ] **P0** Classify risk by autonomy, privilege, data sensitivity, external impact, reversibility, scale, and worst credible harm. `[NIST-AI-RMF, OWASP-AGENTIC]`
- [ ] **P0** Maintain an exception process with owner, rationale, compensating controls, expiry, monitoring, and automatic revocation. `[NIST-CSF, ISO-27001]`
- [ ] **P1** Define review triggers and maximum review intervals by risk tier. `[NIST-AI-RMF, ISO-42001]`
- [ ] **P1** Document residual risk and trace every threat to prevention, detection, response, acceptance, or prohibition. `[NIST-AI-RMF, NIST-CSF]`

[← Threat model](03-threat-model.md) · [Next: Security best practices and control catalog →](05-security-best-practices-and-control-catalog.md)
