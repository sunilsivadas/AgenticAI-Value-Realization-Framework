# Build sequence and deployment checklist

From [Part 6, Building it: one sequence](https://sunilsivadas.github.io/roi.html). Each part of the series ends with its own order of operations. Merged, they give one sequence of ten steps.

The first four steps decide whether to build at all, and they cost the least. On a model, harness or tool change, return to step 3.

---

## Decide (steps 1 to 4)

### 1. Frame

- [ ] The use case is written down
- [ ] It is rated on stakes, autonomy, reversibility, integration complexity and verifiability ([guide](../framework/use-case-weights.md))
- [ ] Every action is listed, with what it can touch
- [ ] Each action has a tier: Low, Medium, High or Critical
- [ ] Each tier has a reliability bar: a k and a maximum silent-failure rate
- [ ] Governance has signed off the bars and named an owner for each factor

### 2. Baseline

- [ ] Cost, time and error rate per case are measured for the human process
- [ ] The measurement is dated, and the method is written down

### 3. Golden set

- [ ] The set is built from real cases and confirmed failures
- [ ] Deterministic checks are used wherever the answer is known
- [ ] Each LLM judge is checked against people, on true positive and true negative rates
- [ ] The set includes paraphrases, injected faults and long sessions

### 4. Ceiling

- [ ] Capability is measured under generous conditions: best effort, ideal harness, no reliability threshold
- [ ] The ceiling clears what the task needs. If it does not, stop here

---

## Build (steps 5 to 7)

### 5. Realise

- [ ] The weakest capability layer is identified: model, harness, tools, retrieval, context, compute or specialisation
- [ ] That layer is engineered first, and the uplift is recorded
- [ ] The model is the cheapest one that clears the bar

### 6. Cost

- [ ] Cost per step and success rate are instrumented
- [ ] The workflow-or-agent decision is made
- [ ] Prompt caching is on, with the prefix restructured
- [ ] Reasoning effort is set per workload
- [ ] Context budgets and retrieval top_k are set
- [ ] Routing happens at task or phase boundaries
- [ ] Deflection is in place where queries repeat: exact-match cache first, then semantic cache
- [ ] Cost per successful task is reported, with its spread

### 7. Reliability

- [ ] Every task is run k times
- [ ] Items that never pass go back to step 5
- [ ] Variance is designed out: workflow before agent, fewer steps, deterministic tools
- [ ] Verification is added: code checks first, then critics. The verifier's false-accept and false-reject rates are measured
- [ ] Recovery is added: checkpoints, idempotent tools, bounded retries
- [ ] Hand-backs are designed, with a budget, so failures arrive labelled
- [ ] pass^k is reported with the hand-back and silent-failure rates

---

## Bound and launch (steps 8 to 10)

### 8. Behaviour

- [ ] Scope and authority are stated in the agent's instructions
- [ ] "High-stakes" is defined for this deployment
- [ ] Consent is verified before high-tier actions. An automated reply does not count
- [ ] The agent's claims are reconciled against its trace
- [ ] The agent denies by default on errors and missing permissions
- [ ] Each guardrail and judge has a measured miss rate and false-alarm rate
- [ ] The behavioural suite includes pressure and ambiguity from your own traces
- [ ] The severity-weighted unsafe-action rate is reported with the intervention rate
- [ ] A safety case is written for the deployment

### 9. Bounds

- [ ] Each agent has its own identity
- [ ] Permissions granted match permissions used. Unused ones are removed
- [ ] The agent runs in a sandbox, with production separated
- [ ] Hard limits sit in tools the agent cannot edit
- [ ] Wherever the agent reads untrusted content, one leg of the lethal trifecta is removed
- [ ] Gates sit where reversibility ends. They are few, tiered, and show the blast radius
- [ ] Each escalation goes to a named person with authority, on a clock
- [ ] The halt works mid-run, and it has been drilled and timed
- [ ] Checks run before the action, wherever possible
- [ ] Every action is traced to an agent identity and an authorising person
- [ ] Alerts are tested, and they fire
- [ ] The fallback route is tested with its production safeguards on
- [ ] The harness survives a model change
- [ ] Bounded share, bound-leak rate, time-to-halt and gate load are reported

### 10. Launch narrow, then widen

- [ ] Shadow mode first, then the lowest tier
- [ ] Kill criteria are written, each with a threshold, an action and an owner
- [ ] Break-even volume is computed
- [ ] The twelve-number [scorecard](../framework/scorecard.md) is reported monthly
- [ ] Volume widens only while the scorecard holds
- [ ] The freed time has a destination, and its value is counted separately
- [ ] The whole suite is re-run on every model, harness or tool change

---

## Per-factor detail

Each factor page has the full order of operations for its part:

- [Capability](../factors/capability.md): nine steps, measurement first
- [Cost](../factors/cost.md): twelve steps, instrumentation first
- [Reliability](../factors/reliability.md): eight steps, the bar per action first
- [Safety](../factors/safety.md): seven steps, the risk assessment first
- [Controllability](../factors/controllability.md): eight steps, the inventory first
