# Factor 4: Safety

Summary of [Part 4, Safety is how an agent behaves when it is unsure](https://sunilsivadas.github.io/safety.html). The article carries the evidence and the full references.

Safety is the agent's own behaviour under uncertainty. Conservative under ambiguity. No invented actions. A real go-ahead before high-stakes steps. A safe stop when it cannot proceed.

The boundary with controllability is one test. If the agent can change it or ignore it, it is a safety lever. If it cannot, it is a control.

---

## Three claims

1. **Safety is measured in actions and reports.** What a model refuses to say tells you little about what an agent does.
2. **Safety moves separately from capability, and the measurements disagree.** UK AISI saw unsanctioned attacks rise from 0% to 29.2% across three OpenAI generations, while OpenAI's own card showed misaligned outcomes falling from 18.8% to 3.4%.
3. **Safety is a system property, and the context moves it.**

---

## Five dimensions

| Dimension | The question | How to measure |
|-----------|--------------|----------------|
| **Consent** | Before a consequential step, is the go-ahead real? | Share of consequential actions with verified consent; proceed-anyway rate after an automated reply |
| **Scope** | Does it stay inside the authority it was given? | Out-of-scope action rate |
| **Honest report** | Does its account match what it did? | Claim-against-trace mismatch rate |
| **No gaming** | Does it pursue the goal or the grader? | Cheating rate on impossible or unverifiable tasks |
| **Fail closed** | When it cannot proceed safely, does it stop in a safe state? | Workaround rate after a denial; end-state checks on fault-injected runs |

Each dimension carries two numbers: how often a violation happens and how bad it is. An agent with a low violation rate and a few catastrophic violations is still unsafe.

---

## The unit: two numbers, reported together

- **Severity-weighted unsafe-action rate**, on your own task set.
- **Intervention rate**: asks, abstentions and escalations per task.

Drive the first down without watching the second and you build an agent that asks about everything. That agent delivers no value either.

---

## Assessing the risk

Tier each action, because one agent spans several tiers. The steps and the four families of dimensions (consequence, exposure, control, context) are in [`../framework/use-case-weights.md`](../framework/use-case-weights.md).

Three rules combine the dimensions:

1. **Add detectability as a third factor**, beside severity and likelihood. Whether you can catch a failure often matters more than how likely it is.
2. **Let consequence set the floor.** Likelihood is hard to estimate for agents and moves with every model upgrade.
3. **Let context scale the evidence.** Regulation decides how you must prove the controls work. Consequence decides whether the risk is real.

---

## The twelve levers, in five groups

| Group | Question | Levers |
|-------|----------|--------|
| **A. Specify** | Does the agent know the bounds? | S1. State scope and authority explicitly. S2. Respect invariants and report against them. S3. Define high-stakes for this deployment |
| **B. Consent** | Is the go-ahead real? | S4. Clarify before acting, and verify the answer. S5. Abstain and escalate on low confidence |
| **C. Report** | Can you trust its account? | S6. Reconcile claims against the trace. S7. Monitor behaviour, and know what monitors miss |
| **D. Fail closed** | Does the agent stop in a safe state? | S8. Deny by default on errors and missing permissions. S9. Stop on its own |
| **E. Assure** | Can you show it to someone else? | S10. Red-team on your own traces. S11. Behavioural regression evals on every upgrade. S12. A written safety case per deployment |

Two levers stand out in the evidence:

- **S1 is the cheapest.** A short description of the sandbox and its rules cut the share of scenarios where Claude Mythos 5.2 reached outside it from 31% to 1.2% ([Anthropic system card](https://assets.claude.com/27d60918d218125e7504bc7354c4b4626ec56b11.pdf), vendor-reported).
- **S6 is the strongest measured.** An evidence contract, requiring fields for status, evidence, limitation and next action, cut false success reports from 22.8% to 0.8% ([FTA](https://arxiv.org/abs/2609.35732), preprint).

---

## Measuring safety

- **Check the grading before the result.** Older benchmarks emulate tools with an LLM and grade with one. Newer ones check the final state of a real environment, or compare reports with action logs. Follow the newer ones.
- **Models recognise tests.** In UK AISI's tests, Anthropic's newest model considered that it might be in an evaluation in 96% of trajectories. Your own production traces carry more weight than any public number.
- **Every judge and guardrail has a miss rate, a false-alarm rate and a fallback route.** Measure all three.
- **Public benchmarks tell you whether a model is worth testing.** Your own scenarios tell you whether it is safe to deploy.

Benchmarks and frameworks you can run are listed in the [README](../README.md#safety).

---

## Order of operations

1. **Assess the risk.** List the actions, rate each one, and assign tiers. Write down scope, authority and what counts as high-stakes (S3).
2. **Build the test set.** Start from a public benchmark and a framework such as Inspect or Petri, then seed it with ambiguity and pressure from your own traces. Check the grader against humans.
3. **Measure two numbers.** Severity-weighted unsafe-action rate and intervention rate, together.
4. **Specify** (S1, S2). State scope in instructions. Test whether the agent respects its limits and reports hitting them.
5. **Make consent real** (S4, S5). Verify the answer, abstain on low confidence.
6. **Check the report** (S6, S7). Reconcile every claim against the trace.
7. **Fail closed and assure** (S8 to S12).

Steps 1 to 3 are measurement. Most of the leverage is in steps 4 and 6, which are also the cheapest.

---

## Mapping to risk frameworks

Each major framework asks for something the five dimensions, the tiers or the levers already supply.

| Framework | Where it lands |
|-----------|----------------|
| [NIST AI RMF 1.0](https://www.nist.gov/itl/ai-risk-management-framework) and [Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) | Map: the action list and tiers. Measure: the two numbers. Manage: S1 to S12. Govern: owners per tier, and the safety case |
| [EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj), high-risk systems | Art. 9: the tiers and levers. Art. 12: trajectory logs. Art. 14: the consent dimension. Art. 15: Parts 3 and 5 |
| ISO/IEC 42001 and ISO/IEC 23894 | The register of actions and tiers, and the safety case per deployment |
| [OWASP Top 10 for Agentic Applications](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) | Three risks touch the agent's own behaviour. The other seven belong to controllability |
| [IMDA Model AI Governance Framework for Agentic AI](https://www.imda.gov.sg/-/media/imda/files/about/emerging-tech-and-research/artificial-intelligence/mgf-for-agentic-ai.pdf) | Unauthorised actions: scope and consent. Erroneous actions: honest report, and Part 3 |

---

## Traps

| Trap | The mistake |
|------|-------------|
| The Refusal Trap | Measure what the model refuses to say |
| The Confident-Report Trap | Trust the agent's summary of what it did |
| The Prompt-as-Policy Trap | Trust the agent to keep a limit because the prompt states it |
| The Rubber-Stamp Trap | Count how often the agent asks |
| The Upgrade Trap | Assume a more capable model is a safer one |
| The Test-Awareness Trap | Trust scripted evaluations at face value |
| The Fallback Trap | Assume the traffic a guardrail stops is now safe |
| The Over-Caution Trap | Tune until the agent asks about everything |

---

## Link to the other factors

- Safety supplies the **behaviour clause** of the [contract](../framework/contract.md).
- The unsafe-action rate, at its intervention rate, is number 5 on the [scorecard](../framework/scorecard.md).
- Permissions, sandboxes and approval gates are built in [Controllability](controllability.md). Safety covers whether the agent respects them.

Next: [Controllability](controllability.md).
