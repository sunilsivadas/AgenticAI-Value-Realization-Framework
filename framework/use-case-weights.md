# Use-case weights: finding the binding constraint

From [Part 1, The weights question](https://sunilsivadas.github.io/capability.html), with the tiers from [Part 4](https://sunilsivadas.github.io/safety.html) and the bars from [Part 3](https://sunilsivadas.github.io/reliability.html).

The four discounts apply to every use case. How much each one matters depends on the use case and the sector. The same model on the same task carries different weights, because the cost of an error changes. Weights follow consequences.

The weights are judgement calls, set by the deployment. They are not numbers to multiply. Their job is to tell you which factor binds first, so you know where to measure and where to spend.

---

## Step 1. Rate the use case on five attributes

| Attribute | The question | What it moves |
|-----------|--------------|---------------|
| **Stakes** | What does a wrong output cost? | As stakes rise, the safety and controllability weights rise faster than capability |
| **Autonomy** | How long does the agent work without a human checkpoint? | As autonomy rises, the reliability weight rises faster than capability, because per-step failures compound |
| **Reversibility** | Can a wrong output be undone? | As reversibility falls, controllability's weight rises |
| **Integration complexity** | How many external systems does the agent operate? | Raises the reliability, cost and controllability weights. Each system is a new failure surface, a new permission scope and a new blast radius |
| **Verifiability** | Can you tell whether the output is right? | Where the operator can grade the output, realized value rises fastest. Where it cannot, you depend on the agent's behaviour |

---

## Step 2. Read the binding constraint

The matrix from Part 1, applied to five common use cases:

| Use case | Stakes | Autonomy | Reversibility | Integration | Verifiability | Binding constraint |
|----------|--------|----------|---------------|-------------|---------------|--------------------|
| Internal meeting summariser | Low | Low | High | Low | Medium | Cost, then capability ceiling |
| Patient-chart summariser | High | Low | Medium | Medium | Low | Safety, then reliability |
| Trading agent | High | Variable | Low | High | High | Controllability, then reliability |
| Customer-support agent (refunds) | Medium-High | High | Low (issued refunds) | High | High | Reliability, then controllability |
| Coding agent (open PR, run tests) | Medium | High | High (tests can fail) | High | High | Capability ceiling, then reliability |

Capability binds first in some use cases, usually the verifiable, reversible ones, and second in many. The practical question is which of the five attributes are unfavourable.

Three versions of one tool show how the weights move:

- **A meeting-notes summariser for internal standups.** A person always reviews the output. Mistakes surface in seconds. Cost and reliability decide if it is worth running.
- **The same summariser on patient charts or audited filings.** A dropped contraindication or an invented figure is a clinical or regulatory incident. Safety and reliability move to the front. Same model, same capability.
- **An agent that places trades or submits orders.** Controllability leads: permissions, reversibility, blast radius, a person in the loop on anything irreversible.

---

## Step 3. Tier each action

One agent spans several tiers. A support agent that searches the knowledge base and issues refunds needs a different bar for each. So the unit of assessment is the action.

1. **List the actions.** Every tool the agent can call, and what each can touch: data read, data written, money moved, messages sent outside, production changed.
2. **Rate the severity of each action**, for each group it affects. Blast radius times reversibility, judged from the position of the person on the receiving end.
3. **Estimate likelihood from your own traces.** Vendor scores do not transfer.
4. **Assign a tier.** Severity sets the floor. A low likelihood never pulls an irreversible, high-severity action below High. Detectability can lower a tier only when a code or state check catches the failure before it reaches anyone.
5. **Let the tier set the levers, and the context set the evidence.** Regulation and risk appetite decide whether internal testing is enough or independent assurance is needed.

Part 4 rates each action on four families of dimensions:

| Family | The question |
|--------|--------------|
| Consequence | How bad is it if it goes wrong? Sets the floor |
| Exposure | How likely is it, and how often does the chance arise? Re-estimate on every model change |
| Control | Can you catch it and stop it in time? |
| Context | What bar must the evidence meet, and for whom? |

---

## Step 4. Set a reliability bar per tier

The author's proposal from Part 3. No industry standard exists yet.

| Tier | Example actions | Reliability bar | How to show it |
|------|-----------------|-----------------|----------------|
| Low | Search, summarise for a person who reads it | pass^3 on the golden set | Golden set run three times on each change; sampled review in production |
| Medium | Reversible writes: draft a reply, open a ticket | pass^4 on the golden set plus paraphrases; hand-back rate tracked | Repeated runs with paraphrased inputs; per-item results kept |
| High | A refund under a cap, a message to a customer | pass^8 on your own traces with injected faults, or a code verifier on every run; silent-failure rate near zero | Confidence interval reported; verifier miss rate measured; ledger reconciled |
| Critical | A payment, an order, a production change | A verifier or a person must catch a failure before it takes effect. pass^k alone is insufficient | Verifier and approval error rates measured; pass^k measured on the whole system, checks included |

Volume turns a rate into a count. To hold failures to one a day on average, an agent that runs 100 times a day needs 99% per run. At 10,000 runs a day it needs 99.99%.

---

## Two rules that keep the assessment honest

- **One agent spans tiers.** Gating every action at the highest tier is how approval rates reach 93%.
- **Re-assess on every change** that alters the action list or the agent's behaviour: a new tool, a wider permission, a model upgrade.

---

## Who gates what

Different teams gate different factors, and each can block the solution on its own factor.

| Factor | Usual gatekeeper |
|--------|------------------|
| Capability and reliability | Product and engineering |
| Cost | Finance |
| Safety | Risk and compliance |
| Controllability and security | CISO |
| Whether the work changes around the agent | The process owner |

Governance sets the bar each of them works to, and names who is accountable.
