# Use-Case Factor Weights

The five-factor framework uses equal weights by default. However, consequence severity and operational context shift which factors become binding constraints in practice. This guide provides worked examples.

---

## Weighting Principle

Adjusting weights does not change the formula — all factors still multiply. It changes how you **prioritize** during evaluation and remediation: lower a factor's weight if your use case genuinely tolerates weakness there; raise it if failure in that dimension is catastrophic.

The article states: "the same model with inverted weights" is still the same model — what changes is which factor your organization will veto on.

---

## Use Case Archetypes

### 1. Low-Stakes Internal Summarization

*Examples: meeting notes, internal standup summaries, document digests*

| Factor | Weight | Rationale |
|--------|--------|-----------|
| Capability | High | Must produce useful output — that's the entire value |
| Cost | High | Low-value task can't justify high per-task cost |
| Reliability | Medium | Occasional misses are acceptable; human review is fast |
| Safety | Low | Consequences of error are minimal; no external exposure |
| Controllability | Low | Blast radius is negligible; audit rarely needed |

**Typical binding constraint:** Cost or Capability. If it's cheaper to let a human skim the doc, the agent has no case.

---

### 2. High-Stakes Regulated Summarization

*Examples: patient chart summaries, legal document analysis, audited financial filings*

| Factor | Weight | Rationale |
|--------|--------|-----------|
| Capability | High | Must be accurate; errors have real consequences |
| Cost | Medium | Higher cost is acceptable if reliability and safety are strong |
| Reliability | Very High | A missed summary or hallucination can cause serious harm |
| Safety | Very High | Hallucination or overconfident output is a liability |
| Controllability | High | Full audit trail required; human review gate mandatory |

**Typical binding constraint:** Safety or Reliability. Regulatory bodies will veto if either is weak.

---

### 3. Transactional / Execution Agents

*Examples: trade execution, purchase orders, infrastructure provisioning, SaaS workflow automation*

| Factor | Weight | Rationale |
|--------|--------|-----------|
| Capability | Medium | Enough capability to do the task reliably matters more than ceiling |
| Cost | Medium | Acceptable if the task is high-value |
| Reliability | High | Repeated failures cause operational disruption and trust erosion |
| Safety | High | Must not execute unintended or ambiguous instructions |
| Controllability | Very High | Reversibility, blast radius bounds, and kill switches are non-negotiable |

**Typical binding constraint:** Controllability. CISO and Compliance will veto without it.

---

### 4. Developer / Engineering Automation

*Examples: code review assistance, CI/CD pipeline agents, PR generation, test writing*

| Factor | Weight | Rationale |
|--------|--------|-----------|
| Capability | Very High | Weak capability on coding tasks is immediately obvious and unusable |
| Cost | Medium | Engineers tolerate moderate cost for high-quality output |
| Reliability | High | Flaky agents slow down the engineering loop |
| Safety | Medium | Sandbox already limits blast radius; hallucinations in code are caught by tests |
| Controllability | Medium | Git provides natural audit trail and reversal mechanism |

**Typical binding constraint:** Capability. If it can't write/review code well, the rest doesn't matter.

---

### 5. Customer-Facing Agents

*Examples: support chatbots, sales qualification, onboarding flows*

| Factor | Weight | Rationale |
|--------|--------|-----------|
| Capability | High | Users notice poor responses immediately |
| Cost | High | Per-conversation cost must be below LTV or resolution cost |
| Reliability | Very High | A broken customer experience destroys trust at scale |
| Safety | Very High | Harmful, biased, or misleading responses are brand and legal risks |
| Controllability | High | Escalation paths and override mechanisms are table stakes |

**Typical binding constraint:** Safety or Reliability, depending on regulatory exposure.

---

## Integration Complexity Modifier

The article identifies that multi-system deployments unevenly shift scores:

| System Count | Reliability | Cost | Controllability |
|-------------|-------------|------|----------------|
| 1 | Baseline | Baseline | Baseline |
| 2-3 | -10-20% | +10% | -10% |
| 4-6 | -30-40% | +20-30% | -20-30% |
| 7+ | Severe degradation | High overhead | Very difficult |

For high-integration deployments, apply a downward adjustment to Reliability and Controllability scores before computing the composite, or treat integration complexity as a separate pre-check gate.

---

## References

- Part 0: [Realized Value Framework](https://sunilsivadas.github.io/realized-value.html) -- use case weight discussion
- [`framework/scorecard.md`](scorecard.md) -- scoring rubric
