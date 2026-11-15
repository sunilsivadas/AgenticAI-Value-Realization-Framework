# Factor 2: Cost

Summary of [Part 2, Cost engineering for agentic AI](https://sunilsivadas.github.io/cost.html). The article makes the argument in about 25 minutes. Its [reference page](https://sunilsivadas.github.io/cost-levers.html) carries the detail and the sources.

Cost is the first discount, and the one factor with a clean unit. Its savings multiply cleanly. An agent that costs more than the labour it replaces zeros the product.

---

## Three claims

1. **Cost is a system property.** The same model can cost several times more or less depending on its harness, context budget, routing policy and effort setting. The effort setting alone moves cost per task about 9 to 10× on the current flagships.
2. **The cheapest model on the Pareto frontier that clears your quality bar usually wins.** The top-scoring model is rarely the most cost-efficient.
3. **Order matters as much as choice.** The order in which you apply the levers decides whether savings multiply or cancel out. In the author's experience, steps 2 to 5 of the order of operations deliver most of the saving.

---

## The unit

```
cost per successful task = cost per run ÷ success rate
```

Take a model that is 10% cheaper per run but drops success from 90% to 70%. Its cost per successful task rises by about 16%, before escalation and rework.

Price lists misrank this number. On Terminal-Bench 4.0 in November 2026, cost per solved task varied about 10× among models scoring above 55%, from about $3 to about $31 ([Vals AI](https://www.vals.ai/benchmarks/terminal-bench-4)). A preprint comparing eight reasoning models finds the cheaper-listed model costs more in 32% of model pairs, by up to 28× ([Chen et al.](https://arxiv.org/abs/2603.23971)).

Two rules follow for every lever. Route on measured cost per task. Treat that cost as a distribution with a spread.

If you cannot measure cost per step and success rate per cohort, stop and instrument first. Every lever depends on it.

---

## The eighteen levers, in five groups

| Code | Group | Question it answers | Levers | Indicative savings |
|------|-------|---------------------|--------|--------------------|
| C1 | CONTROL | What work should run at all? | 1 to 4 | 30 to 60% |
| C2 | COMPACT | How much information per call? | 5 to 10 | 40 to 80% |
| C3 | CONSTRAIN | How does the runtime behave? | 11 to 13 | 15 to 50% |
| C4 | COMMODITISE | What does each unit cost? | 14 to 17 | 30 to 95% |
| C5 | CALIBRATE | How do we know any of this works? | 18 | Foundation |

The savings are upper bounds for each group at the same quality. They are not guaranteed to stack.

| # | Lever | One line | Evidence verdict |
|---|-------|----------|------------------|
| 1 | Model routing | Route each step to its own tier | Strong |
| 2 | Deflection | Answer without calling the model | Strong |
| 3 | Workflow or agent | This choice comes before every other lever | Adequate |
| 4 | Confidence-gated work | Pay for extra checks only when a cheap signal asks for them | Adequate |
| 5 | Context engineering | Put only what each step needs into the prompt | Strong |
| 6 | Data quality and retrieval engineering | Good retrieval keeps the context small | Adequate |
| 7 | Caching | The lever with the largest single effect, in the author's reading | Strong |
| 8 | Retrieval economics | Retrieve less, and store vectors more cheaply | Adequate |
| 9 | Output shaping | Output tokens are the expensive ones | Adequate |
| 10 | Prompt compression | Shrink the tokens, keep the information | Adequate |
| 11 | Harness engineering | Bound what the agent can spend | Adequate |
| 12 | Tool design and call discipline | Keep tools few, schemas short and outputs compact | Adequate |
| 13 | Reasoning discipline | Set the effort level per workload | Adequate |
| 14 | Fine-tuning and distillation | Make a small model good at one narrow task | Strong |
| 15 | Service tiers and time-shifting | Run each workload in the cheapest tier that meets its deadline | Adequate |
| 16 | Self-hosted or managed APIs | Own the serving stack only when utilisation pays for it | Adequate |
| 17 | Speculative and parallel execution | Do independent work at the same time | Adequate |
| 18 | FinOps telemetry | Attribute every dollar to a step, a tenant and an outcome | Adequate |

**How the verdicts are set.** Each lever is checked against three independent types of evidence: a peer-reviewed paper, provider documentation with measured numbers, and a production case from a named team. A lever is Strong when all three are present, Adequate when one is missing or its mechanism differs from the claim, and Thin when the anchors are workshop-grade or absent. Five levers are Strong and thirteen are Adequate. None is Thin.

The [reference page](https://sunilsivadas.github.io/cost-levers.html) names the evidence for every lever.

---

## Order of operations

0. Instrument cost per step and success rate.
1. Decide workflow or agent.
2. Turn on prompt caching, with the prefix restructured.
3. Set reasoning effort per workload.
4. Set context budgets and retrieval top_k.
5. Route at task or phase boundaries.
6. Deflect: exact-match cache first, then semantic cache.
7. Add output schemas and length caps.
8. Move work to Batch, Flex and off-peak windows.
9. Add contextual retrieval with reranking.
10. Fine-tune or distil stable narrow tasks.
11. Self-host once baseload is predictable.

Steps 0 and 1 are measurement. Steps 2 to 5 deliver most of the saving. Fine-tuning and self-hosting matter only at scale, or after the earlier steps are done.

---

## Traps

| Trap | What it looks like |
|------|--------------------|
| The Small Model Fallacy | Force the cheapest tier on every step |
| The Frontier Trap | Default to the top model on every step |
| The Launch-Price Trap | Plan on an introductory price |
| The Max-Effort Trap | Treat max effort as the safe setting |
| The Cold-Cache Trap | Switch models on every step of a long session |
| The Stale-Cache Trap | High hit rate, weak invalidation |
| The Over-Compaction Trap | Drop history aggressively |
| The Agent-for-a-Form Trap | A multi-step agent loop for a form |
| The Token KPI Trap | A dashboard that counts tokens and ignores tasks |
| The Prefix-Order Trap | Turn on caching without restructuring the prompt |
| The Batch-for-Interactive Trap | Turn on batch for all traffic |

---

## Link to the other factors

The denominator links cost to reliability. Each failed run is paid for and delivers nothing, so the failures Part 3 measures raise cost per successful task directly.

Cost per successful task is number 1 on the [scorecard](../framework/scorecard.md) and the "run cost" line of the [cost model](../framework/cost-model.md).

Next: [Reliability](reliability.md).
