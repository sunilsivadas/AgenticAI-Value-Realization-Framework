# Factor 3: Reliability

> Covered in depth in **Part 3** of the Realized Value series (forthcoming).

Reliability is the factor most severely impacted by the gap between benchmark conditions and production reality. Benchmarks report pass@1. Production demands pass@always.

---

## The pass@1 vs. pass@always Gap

Benchmarks measure whether an agent *can* complete a task. Production requires it to complete that task *consistently*, across heterogeneous inputs, with real tool integrations, under load.

The METR Remote Labor Index (2025) found the best autonomous agents completing only **2.5% of real-world tasks at acceptable quality** — despite frontier models scoring well above 50% on coding benchmarks under ideal conditions.

The gap is explained by:

1. **Distribution shift**: Production tasks differ from benchmark tasks in ways that matter
2. **Integration failure surface**: Every real tool adds rate limits, authentication expiry, and schema drift
3. **Compounding errors**: Multi-step agents accumulate errors; a 95% per-step rate means 60% over 10 steps
4. **Context degradation**: Long-running tasks fill context windows, degrading later-step quality

---

## The Reliability-Horizon Interaction

The autonomy horizon — how long a task can be before agents fail economically — shrinks sharply as the required reliability bar rises:

| Reliability Target | Maximum Viable Task Length |
|--------------------|---------------------------|
| 50% | ~14.5 hours |
| 80% | ~1 hour |

This is not a model limitation. It's a system property. Improving reliability directly extends the class of tasks the agent can viably handle.

---

## Failure Mode Taxonomy

Understanding failure mode distribution helps target improvements:

| Failure Mode | Cause | Mitigation |
|-------------|-------|------------|
| Tool call error | Bad parameter, missing field | Output validation, schema enforcement |
| Integration timeout | Rate limit, network latency | Retry with backoff, circuit breakers |
| Context overflow | Long task fills context window | Summarization, memory management |
| Hallucinated action | Model invents non-existent tool/step | Output validation, tool schema strictness |
| Compounding error | Early error propagates through steps | Checkpointing, step-level validation |
| Silent failure | Agent reports success but output is wrong | Output verification, eval-as-judge |

---

## Measuring Production Reliability

### Staging Environment Requirements

A staging environment must match production on:
- Tool integrations (not mocked)
- Input distribution (sample from real task queue, not curated examples)
- Load profile (test at representative concurrency)
- Auth environment (real tokens that expire)

### Reliability Metrics to Track

| Metric | Definition |
|--------|------------|
| Task success rate | % of tasks completed successfully end-to-end |
| First-attempt success rate | Success without any retry |
| Mean attempts per success | Average retries needed when task eventually succeeds |
| Silent failure rate | Tasks reported as complete but output is incorrect |
| Integration error rate | Failures attributable to external tool/API issues |

---

## Key Resources

See the [Reliability section of the main catalog](../README.md#3-reliability--testing--production-harnesses) for full resource tables.

### Highlighted Resources

| Resource | Why It Matters |
|----------|---------------|
| [Promptfoo](https://github.com/promptfoo/promptfoo) | Best tool for CI/CD regression testing of LLM behavior |
| [DeepEval](https://github.com/confident-ai/deepeval) | Unit-test style framework for output quality evaluation |
| [Arize Phoenix](https://github.com/Arize-ai/phoenix) | Production trace analysis for identifying reliability degradation |
| [Instructor](https://github.com/jxnl/instructor) | Structured output extraction with automatic retry on validation failure |
| [MCP Servers](https://github.com/modelcontextprotocol/servers) | Standardized tool protocol that reduces schema drift across integrations |

---

## Common Pitfalls

- **Staging with mocked tools**: Mocked integrations hide the most common production failure modes.
- **Measuring pass@1 only**: A 70% first-attempt rate looks acceptable until you realize 30% of tasks retry 5+ times, blowing the cost model.
- **Ignoring silent failures**: Agents that return plausible-but-wrong output are harder to detect than crashes and cause more downstream damage.
- **No step-level monitoring**: Task-level success rates don't show where in a multi-step pipeline failures cluster.
