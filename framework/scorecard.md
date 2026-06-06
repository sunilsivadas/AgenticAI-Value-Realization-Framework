# Realized Value Scorecard

Use this scorecard to score an agentic AI deployment across all five factors. Because the formula is multiplicative, a score near zero on any single factor is disqualifying regardless of performance elsewhere.

```
Realized Value = Capability x Cost x Reliability x Safety x Controllability
```

---

## Scoring Guide

Each factor is scored **0.0-1.0**. The composite score is the product of all five.

| Score | Interpretation |
|-------|---------------|
| 0.9-1.0 | Exceeds requirements; not a constraint |
| 0.7-0.89 | Acceptable; minor gaps to address |
| 0.5-0.69 | Material risk; requires a remediation plan |
| 0.2-0.49 | Binding constraint; blocks deployment |
| 0.0-0.19 | Near-zero; zeros the product |

**Composite score interpretation:**

| Composite | Interpretation |
|-----------|---------------|
| > 0.5 | Strong deployment candidate |
| 0.2-0.5 | Conditional; address binding constraints first |
| < 0.2 | Not ready; identify the near-zero factor |

---

## Factor 1: Capability

*Can the agent actually complete the target task class?*

| Dimension | Evidence Required | Score (0-1) |
|-----------|------------------|-------------|
| Task completion rate on benchmark | Pass rate on relevant eval (e.g., SWE-bench, tau-bench, domain-specific) | |
| Autonomy horizon match | Agent's reliable task horizon (hrs) >= target task length | |
| Tool use fidelity | Correct tool selection and parameter handling rate | |
| Domain knowledge adequacy | Qualitative or eval-based assessment of domain coverage | |

**Factor 1 Score:** _____ / 1.0

Notes:
_____________________________________________

---

## Factor 2: Cost

*Is the cost per successful task below the value it delivers?*

| Dimension | Evidence Required | Score (0-1) |
|-----------|------------------|-------------|
| Cost per successful task | Measured with retries and failure overhead included | |
| Cost vs. labor displaced | Cost < fully-loaded cost of equivalent human effort | |
| Integration overhead | Fixed integration costs amortized across expected volume | |
| Token efficiency | Context size and call count are optimized, not bloated | |

**Factor 2 Score:** _____ / 1.0

Notes:
_____________________________________________

---

## Factor 3: Reliability

*Does the agent perform consistently in production, not just under benchmark conditions?*

| Dimension | Evidence Required | Score (0-1) |
|-----------|------------------|-------------|
| Production pass rate | Measured in real or realistic staging environment | |
| Failure mode analysis | Known failure modes are documented and bounded | |
| Integration failure surface | Rate-limiting, token expiry, schema drift are handled | |
| Recovery behavior | Agent fails gracefully; errors are surfaced, not silently swallowed | |

**Factor 3 Score:** _____ / 1.0

Notes:
_____________________________________________

---

## Factor 4: Safety

*Does the agent behave conservatively under ambiguity and avoid unauthorized actions?*

| Dimension | Evidence Required | Score (0-1) |
|-----------|------------------|-------------|
| Conservative under ambiguity | Agent asks before acting on ambiguous instructions | |
| No invented actions | Agent does not take actions outside its defined scope | |
| High-stakes step confirmation | Agent pauses before irreversible or high-blast-radius actions | |
| Safe failure mode | When uncertain, agent fails safely (does nothing vs. wrong thing) | |

**Factor 4 Score:** _____ / 1.0

Notes:
_____________________________________________

---

## Factor 5: Controllability

*Does the operator have sufficient leverage to constrain, monitor, and stop the agent?*

| Dimension | Evidence Required | Score (0-1) |
|-----------|------------------|-------------|
| Permission scope | Minimum necessary permissions granted; least-privilege enforced | |
| Blast radius bounds | Maximum damage from a single agent run is bounded and documented | |
| Audit trail | Complete, tamper-evident log of all agent actions exists | |
| Kill switch | Agent can be stopped mid-task without cascading side effects | |
| Human override path | Clear mechanism for human to intervene at any point | |

**Factor 5 Score:** _____ / 1.0

Notes:
_____________________________________________

---

## Composite Score

| Factor | Weight* | Score | Weighted |
|--------|---------|-------|----------|
| Capability | 1.0 | | |
| Cost | 1.0 | | |
| Reliability | 1.0 | | |
| Safety | 1.0 | | |
| Controllability | 1.0 | | |
| **Composite (product)** | | | |

\* Default weights are equal (1.0). Adjust per [`framework/use-case-weights.md`](use-case-weights.md) for your use case context.

---

## Binding Constraint

The factor nearest zero determines deployment readiness. Identify it explicitly:

**Binding constraint factor:** _____________________

**Remediation plan:**
_____________________________________________
_____________________________________________

---

## Sign-off

| Stakeholder | Role | Factor Owned | Approved |
|-------------|------|--------------|----------|
| | Finance | Cost | [ ] |
| | CISO | Controllability | [ ] |
| | Governance/Risk | Safety | [ ] |
| | Product/Engineering | Capability, Reliability | [ ] |
