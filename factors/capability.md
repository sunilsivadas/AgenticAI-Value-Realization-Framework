# Factor 1: Capability

Summary of [Part 1, Capability is a system property](https://sunilsivadas.github.io/capability.html). The article makes the argument in about 25 minutes. Its [reference page](https://sunilsivadas.github.io/capability-reference.html) carries the detail and the sources.

> The model sets the ceiling. The system decides how much of it you get. Between generational releases, the model you picked is rarely what holds you back.

Capability is the only factor that creates value. It is the potential economic value: the ceiling of what could be automated or augmented. The other four factors discount it.

---

## Three claims

1. **Capability is a system property, and where the system adds it depends on the model tier.** For flagship models, vendor and minimal harnesses score within about two points of each other on Terminal-Bench 4.0. For mid-tier models and cross-vendor pairings, the harness moves results by about 3 to 12 points either way. Optimised harnesses add 13 points or more on a fixed model.
2. **Frontier models cluster, separate, and cluster again.** A new generation raises the ceiling by double digits. Between generations, what an enterprise controls is the system around the model.
3. **Measuring capability at a production reliability threshold double-counts reliability.** Measure capability under generous conditions: best effort, ideal harness, no time pressure.

---

## The unit

A score on a relevant, unsaturated benchmark, or on an internal eval built from production traces, measured under generous conditions with no reliability threshold.

Why no threshold: METR measured one model, Claude Opus 4.6, at a task horizon near 12 hours at 50% reliability and about 70 minutes at 80% ([METR](https://metr.org/time-horizons/)). Fold a success-rate threshold into capability and you count reliability twice.

---

## Where capability comes from: seven layers

| Layer | Capability lever | Indicative same-system uplift |
|-------|------------------|-------------------------------|
| 1. Model | Cheapest frontier model that meets the task ceiling | About 2 points within a generation; 2 to 54 points across one |
| 2. Harness | Agent architecture | Flagship, off-the-shelf: about 0 on Terminal-Bench 4.0. Flagship, context-management fit: 6 to 18. Cheaper tiers: about 3 to 9. Cross-vendor mismatch: up to −12. Optimised: 13 and more |
| 3. Tools | Catalogue, descriptions, invocation discipline | No single figure. Tool-trained small models beat larger ones on BFCL v3 and GAIA |
| 4. Retrieval primitives | Primitive choice and tuning | 14+ points on deep-research |
| 5. Context engineering | Budgets, compaction, prefix structure | GPT-4o loses about 30 points at 32K on NoLiMa |
| 6. Test-time compute | Reasoning depth, best-of-n, verifier loops | Small at the top: 3 points from high to max effort on one benchmark, and a loss on another |
| 7. Specialisation | Skills, narrow fine-tunes, distillation | Task-dependent; the same quality at a fraction of the foundation-model cost |

For layer 4, the state of the data matters as much as the retrieval method. On BEAVER, a benchmark built from three private company data warehouses, the best agent answered 11.4% of questions correctly, although the same method scores 62.9% on Spider 2.0. Telling the agent which tables, join keys and columns to use raised the best method from about 9.5% to 18.9% ([BEAVER](https://arxiv.org/abs/2409.02038), preprint). The hints were written by the benchmark's authors, so they show the most that documentation could give.

The figures vary widely because each layer's leverage depends on the others. Within a generation, the non-model layers move capability further than the choice between frontier models. The exception is an off-the-shelf harness at the flagship tier. Across a generation, the model moves it furthest.

---

## Measurement discipline

- **Measure under generous conditions.** Best effort, ideal harness, no time pressure.
- **Keep capability and adoption apart.** Usage depends on all five factors.
- **Avoid saturated and contaminated benchmarks.** SWE-bench Verified, Aider Polyglot and BFCL v3 all saturated or were contaminated.
- **State the measurement condition.** SWE-bench Pro has three: vendor-reported, standardised public, and private commercial. They differ by tens of points.
- **Prefer the median of independent boards** to any single number.

Benchmarks the article recommends, by what each measures, are listed in the [README](../README.md#capability).

---

## Order of operations

0. **Define the use case.** Rate it on stakes, autonomy, reversibility, integration and verifiability. See [`../framework/use-case-weights.md`](../framework/use-case-weights.md).
1. **Pick a relevant, unsaturated benchmark.** Or build an internal eval on production traces.
2. **Measure under generous conditions.**
3. **Identify the weakest capability layer.**
4. **Engineer that layer.** Below the flagship tier, this is often harness fit or context.
5. **Re-measure under the new system.** Record the uplift the lever produced.
6. **Stack the next layer.** Tools, retrieval, context, compute, specialisation, in that order.
7. **Revisit the model choice.** Pick the cheapest model that meets the target.
8. **Hand the system to the four discounts.**

Steps 0 to 2 are measurement. Skip them and every later step gets the wrong answer. Steps 3 to 6 are the realisation work, and most of the leverage is there. When a new generation ships, go back to step 2.

---

## Traps

| Trap | What it looks like |
|------|--------------------|
| The Frontier Trap | Default to the top model on every task, simple ones included |
| The MMLU Trap | Measure on saturated or non-agentic benchmarks |
| The Pass@1 Trap | Confuse capability with reliability |
| The Adoption Trap | Treat usage as evidence of capability |
| The Saturation Trap | Keep trusting a benchmark after it saturates |
| The Harness Portability Trap | Assume a harness tuned to one model works on the next |
| The Vendor Demo Trap | Confuse demo capability with production capability |

---

## What this means for a programme

Capability is plentiful. What is scarce is the system that turns a capable model into something that ships: harnesses, tool catalogues, retrieval, context budgets, evaluations and operational discipline.

Vendors price by model tier. Realized capability depends on system design. The enterprises that do best will own capability investments that move across models: evaluations, harnesses and governance.

Next: [Cost](cost.md).
