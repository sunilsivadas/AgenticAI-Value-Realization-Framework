# Factor 2: Cost

> Covered in depth in **Part 2** of the Realized Value series (forthcoming).

Cost is the most cleanly quantifiable factor in the formula. The critical metric is **cost per successful task** — measured with retries and failures counted in, not cost per API call or cost per benchmark pass.

---

## The Right Cost Metric

Most teams measure cost wrong initially. Common mistakes:

| Wrong Metric | Why It Misleads |
|-------------|----------------|
| Cost per API call | Ignores failed calls that don't produce successful tasks |
| Benchmark cost | Ideal conditions; doesn't include retry loops or error handling |
| Model cost only | Ignores tool call costs, retrieval costs, infrastructure overhead |
| Median cost | Outlier tasks with many retries skew the true per-task economics |

**Correct metric:** `Total cost of all runs / Number of successfully completed tasks`

This single number determines whether the agent is economically viable.

---

## Cost Components

```
Total Task Cost = Model Tokens
               + Tool / Function Call Costs
               + Retrieval / Embedding Costs
               + Infrastructure / Compute
               + Human Review (if HITL)
               + Amortized Integration Setup
```

For multi-step or long-horizon agents, context window size often dominates. Long contexts mean the full conversation history (tools, results, observations) accumulates and recurs in every subsequent call.

---

## The Break-Even Calculation

```
Viable if: Cost per successful task < Fully-loaded human cost per equivalent task
```

Fully-loaded human cost includes salary, benefits, management overhead, and the cost of errors humans make. Agents need to clear this bar — not just token cost vs. hourly rate.

---

## Cost Optimization Levers

### Token Reduction
- Prompt compression (LLMLingua, etc.)
- Context summarization between steps
- Caching repeated prefixes (prompt caching)
- Structured output to reduce verbose completions

### Model Routing
- Route easy subtasks to cheaper models (RouteLLM pattern)
- Reserve frontier models for steps where quality matters most
- Speculative execution on cheaper models with frontier fallback

### Reliability's Impact on Cost
Reliability and cost interact. A 10% improvement in pass rate on a retrying agent can dramatically reduce cost per successful task if the alternative is 3-5 full retries on failure.

---

## Key Resources

See the [Cost section of the main catalog](../README.md#2-cost--observability--optimization) for full resource tables.

### Highlighted Resources

| Resource | Why It Matters |
|----------|---------------|
| [Langfuse](https://github.com/langfuse/langfuse) | Best open-source solution for per-trace cost attribution |
| [LiteLLM](https://github.com/BerriAI/litellm) | Multi-provider proxy with cost normalization across models |
| [DSPy](https://github.com/stanfordnlp/dspy) | Algorithmic prompt optimization that directly reduces token cost |
| [LLMLingua](https://github.com/microsoft/LLMLingua) | Prompt compression with measurable cost reduction |
| [RouteLLM](https://github.com/lm-sys/RouteLLM) | Strong/weak routing to reduce cost without capability loss |

---

## Common Pitfalls

- **Not counting failed tasks**: An agent with 60% success rate that you only pay for successes still has its 40% failure rate baked into the retry cost.
- **Ignoring context growth**: In multi-step agents, context window fills up with tool call histories, leading to exponential cost growth per task.
- **Benchmark cost extrapolation**: Benchmark tasks are often shorter and cleaner than production tasks. Cost per production task is typically 3-5x benchmark cost.
- **Fixed cost blindness**: Integration setup, schema maintenance, and prompt engineering are real costs that must amortize over task volume.
