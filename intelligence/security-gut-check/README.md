[README.md](https://github.com/user-attachments/files/27959833/README.md)
# security-gut-check

**Category:** Intelligence  
**Trigger:** Any request to review a workflow, system, or automation for security risks — especially where trust is assumed

---

## What It Does

Runs a defensive trust audit across seven risk domains on any described workflow, system, or automation. For each risk found, it explains what could go wrong, why a normal check would miss it, the safest practical fix, and whether expert review is needed. Closes with a prioritized action list and a monitoring checklist tailored to the system.

Defensive only. No exploit steps, attack code, or offensive content — ever.

---

## When to Use

- Before deploying a new workflow, integration, or automation
- When a system touches customer data, API keys, or automated irreversible actions
- After reading about a security incident that sounds uncomfortably familiar
- As a sanity check before sharing credentials, setting up a new integration, or going live
- Any time someone asks "is this safe?" about a technical system

---

## Trigger Phrases

- "Security review this"
- "Gut check this workflow"
- "Find the trust assumptions in this system"
- "What could go wrong here?"
- "Is this safe to deploy?"
- "Check this automation for risks"
- "Review this for security issues"

---

## Key Inputs

| Input | Required? | Notes |
|---|---|---|
| System / workflow description | ✅ | Paste or describe — the more detail, the sharper the review |
| Environment (prod / staging / internal) | Optional | Affects risk prioritization |
| Data types involved | Optional | PII, credentials, financial — shapes Domain 5 findings |
| Existing security controls | Optional | Avoids flagging things already addressed |

---

## The Seven Domains

1. **User accounts and permissions** — over-permissioning, implicit access, privilege escalation
2. **Third-party packages and integrations** — supply chain, transitive dependencies, webhook validation
3. **API keys, tokens, and credentials** — scope, rotation, exposure vectors
4. **Automated actions that could cause damage** — blast radius, irreversibility, cascading effects
5. **Data that should stay private** — log leakage, overly broad access, analytics exposure
6. **Approval steps before anything public or irreversible** — missing gates, developer shortcuts
7. **Monitoring and logs** — what to watch, how often, what absence of signal means

---

## Output Structure

- **Trust Surface Summary** — where this system extends trust
- **Findings** — each with: what could go wrong / why it's missed / the fix / expert review flag
- **Priority Summary table** — 🔴 Critical → 🟢 Low/Hardening
- **Cross-Domain Risk Combinations** — where findings compound each other
- **Monitoring Checklist** — specific logs and signals to check regularly
- **What to Do First** — three prioritized actions

---

## Example Finding

```
🔴 Critical Finding: API Key Scope Overage
Domain: API Keys, Tokens, and Credentials

- What could go wrong: The integration key has read/write access to all customer records,
  but the integration only needs to write to a single table. If the key is compromised,
  an attacker has full read access to your customer database.

- Why a normal check might miss it: Developers often grab the broadest available key
  to avoid permission errors during development, then never narrow it for production.

- Safest practical fix: Create a scoped service account with write access only to the
  specific table this integration uses. Rotate the existing key.

- Needs expert review: No — this is straightforward least-privilege implementation.
```

---

## What This Skill Won't Do

It will not provide exploit steps, attack code, specific vulnerability payloads, or instructions that could be used offensively. If you describe a system and ask how an attacker would exploit it, the skill redirects to the defensive finding and fix for that risk area.
