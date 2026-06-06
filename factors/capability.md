# Factor 1: Capability

> Covered in depth in **Part 1** of the Realized Value series (forthcoming).

Capability is the only term in the formula that *creates* value. Every other factor discounts it. It represents the ceiling of what the agent can accomplish — but that ceiling is jointly set by the model and its scaffold (the harness, tools, retrieval, memory, and prompting strategy).

---

## What Capability Measures

The article distinguishes two questions:

1. **What is the model's theoretical ceiling?** (GDPval-style occupational benchmarks, frontier evals)
2. **What ceiling can your deployment actually realize?** (task-specific evals, real-task completion, autonomy horizon)

The gap between these two is where most enterprise deployments stall.

---

## Autonomy Horizon

The autonomy horizon is the maximum task length at which the agent succeeds at an acceptable rate. It scales sharply with the reliability bar:

| Reliability Target | Autonomy Horizon |
|--------------------|------------------|
| 50% | ~14.5 hours |
| 80% | ~1 hour |

This means agents that appear capable on benchmarks may fail economically on tasks longer than their reliability-adjusted horizon.

---

## Measuring Capability

### Phase 1: Benchmark Orientation

Use standard benchmarks to establish a baseline and compare against reference points:

- **Coding tasks**: SWE-bench, SWE-bench Verified
- **Autonomous tasks**: METR Task Standard, Remote Labor Index
- **Multi-environment**: AgentBench
- **Computer use**: OSWorld, WebArena
- **Enterprise workflows**: WorkArena, tau-bench

Benchmarks give pass@1 under ideal conditions. This is the ceiling, not the floor.

### Phase 2: Real-Task Measurement

Run the agent against >=20 tasks from your actual task class. Measure:

- Task completion rate
- Average task duration
- Failure mode distribution
- Tool use fidelity (did it call the right tools with correct parameters?)

### Phase 3: Scaffold Optimization

The harness can significantly move capability scores:

- **Retrieval**: Does the agent have access to relevant context? RAG or tool access?
- **Memory**: Can it maintain relevant state across long tasks?
- **Tool design**: Are tools well-described? Do schemas match actual APIs?
- **Prompting**: Is the system prompt precise about scope and output format?

---

## Key Resources

See the [Capability section of the main catalog](../README.md#1-capability--benchmarks--evals) for full resource tables.

### Highlighted Resources

| Resource | Why It Matters |
|----------|---------------|
| [SWE-bench](https://github.com/princeton-nlp/SWE-bench) | Gold standard for coding capability; widely reported |
| [METR Task Standard](https://github.com/METR/task-standard) | Best framework for defining what "autonomous completion" means |
| [METR Remote Labor Index](https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/) | Only public dataset measuring real-world autonomous completion rates |
| [AgentBench](https://github.com/THUDM/AgentBench) | Broadest multi-domain coverage |
| [tau-bench](https://github.com/sierra-research/tau-bench) | Best for enterprise customer-facing and tool-use scenarios |

---

## Common Pitfalls

- **Benchmark overfitting**: A model that scores well on SWE-bench may not generalize to your specific codebase or toolchain.
- **Ignoring the scaffold**: Swapping models on a weak harness often produces smaller gains than improving retrieval or tool descriptions.
- **Confusing ceiling with floor**: Capability benchmarks measure best-case performance. Production reliability is a separate measurement.
- **Autonomy horizon mismatch**: Deploying an agent on tasks longer than its reliability-adjusted horizon guarantees a poor production pass rate.
