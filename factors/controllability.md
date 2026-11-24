# Factor 5: Controllability

Summary of [Part 5, Controllability is what you can do when the agent is wrong](https://sunilsivadas.github.io/controllability.html). The article makes the argument in about 25 minutes. Its [reference page](https://sunilsivadas.github.io/controllability-reference.html) carries the detail and the sources.

Controllability is the operator's leverage: permissions, sandboxing, audit trails, kill switches, blast radius, human checkpoints. Model supply belongs here too. It is the factor you set yourself.

---

## Three claims

1. **Controllability is designed, then measured.** A control is a design until it is tested.
2. **The human gate is weakest at volume and without context.** Users accepted 93% of Claude Code's permission prompts in March 2026 and 97% by August (vendor-reported).
3. **Detection bounds nothing unless it triggers a tested halt.** In OpenAI's September 2026 incident the alert took 11 minutes 48 seconds and the stop took 2 hours 44 minutes, because the automatic pause did not fire ([OpenAI](https://alignment.openai.com/misalignment-reports/an-agent-used-dns-to-reach-an-external-chatbot/), vendor-reported).

---

## Five dimensions

| Dimension | The question | How to test it |
|-----------|--------------|----------------|
| **Bound** | What can the agent reach? | Permissions granted against permissions used; worst reachable state per action; credential lifetime |
| **Gate** | Who must say yes, before which action? | Share of High and Critical actions behind a gate; approval rate; approvals per person per hour |
| **Halt** | Can you halt it mid-run? | Time from first bad action to stop, in drills and incidents |
| **Undo** | Can you reverse or contain the effect? | Share of actions that are reversible or staged; blast radius when they are not |
| **Trace** | Can you reconstruct who did what, on whose authority? | Share of actions attributable to an agent identity and an authorising person; time to reconstruct an incident |

Each dimension carries two questions: how wide the bound is, and whether it held under test. A narrow bound that leaks is worse than its design suggests, because everyone plans around it.

Security is the same five dimensions under an adversary.

---

## The unit: four numbers

| Number | What it is | Why |
|--------|------------|-----|
| **Bounded share** | Share of High and Critical actions behind a hard limit or a gate | Says how much of the risk register is covered |
| **Bound-leak rate** | Share of red-team attempts that get past a stated bound | Says whether the coverage is real |
| **Time-to-halt** | From first bad action to stop, in drills and incidents; and from action to block, for each guardrail | Says how much damage a leak can do |
| **Gate load** | Approvals per person per hour, and the approval rate | Says whether the gates are still doing anything |

Report them beside task success with the controls on.

---

## Six tests

1. **Permission audit.** Compare what each agent's credentials allow with what its traces show it uses. Every unused permission is blast radius with no value.
2. **Red-team the bounds.** The services around an agent leak more than the sandbox it runs in. A bound that judges one conversation at a time misses a task spread across many.
3. **Drill the halt.** Pick a run, declare it bad, and time the stop. Time each block as well.
4. **Test injection adaptively.** Static test sets overstate defences.
5. **Attack the fallback route.** A classifier, a rate limit or an outage can send a request to a second model. Attack that route with its production safeguards on, and record which model answered.
6. **Watch the gate.** Approval rate, approvals per person per hour, time to decision, and how often an approver changes or blocks what the agent proposed.

A log needs an alert. Test that the logs exist and that the alerts fire.

---

## The twelve levers, in six groups

| Group | Question | Levers |
|-------|----------|--------|
| **B. Bound** | What can the agent reach? | K1. Least privilege per action, with an identity per agent. K2. Sandbox, and separate the environments. K3. Put limits where the agent cannot reach them |
| **G. Gate** | Who says yes? | K4. Gates set by action tier, placed where reversibility ends. K5. Show the blast radius, and budget the prompts. K6. Escalate to someone with authority, on a clock |
| **H. Halt and undo** | Can you stop it and reverse it? | K7. A stop that works mid-run, drilled. K8. Make actions reversible by design |
| **T. Trace** | Can you reconstruct it? | K9. An audit trail that ties every action to an agent and a person, and records which data sources the action read |
| **R. Resist** | Do the bounds hold under attack? | K10. Remove the capability, so there is no attack to detect. K11. Control the supply chain and the agents' channels |
| **P. Portability** | Can you lose the model? | K12. Keep the harness portable, and prune it on every upgrade |

---

## Security: remove the capability an attack needs

- Twelve injection defences fell to adaptive attacks, most at over 90% success ([Nasr et al.](https://www.usenix.org/system/files/usenixsecurity26-nasr.pdf), peer-reviewed).
- A design that keeps the plan apart from untrusted data stopped all 949 attacks in its own test ([CaMeL](https://arxiv.org/abs/2503.18813), preprint).
- The [lethal trifecta](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/): private data, untrusted content and an outside channel. Remove a leg wherever the agent reads content you do not control.
- A block that lands after the action is a detection. Put the check before the action.
- A safeguard can move risk onto the route it creates. Test the fallback route as hard as the primary.

---

## Classifying an incident

OpenAI published a draft framework for grading control incidents on 16 Nov 2026, written with MITRE ([OpenAI](https://cdn.openai.com/pdf/classifying-ai-control-incidents-and-their-severity-a-draft-framework.pdf), vendor proposal, draft v0.1).

- **Definition.** A control incident is an uninstructed action outside the agent's authorised scope that causes harm or weakens a control. Actions that the user or a human attacker directed are excluded, so a prompt-injection attack is outside it.
- **Four questions.** What information did the agent reach or disclose? What did it change or impair? Could people still use the systems they rely on? Could the people responsible for oversight still monitor the agent and stop it in time?
- **Two ratings**, each on five levels (Low, Moderate, High, Severe, Critical): one for what happened, and one for the most serious outcome that was credibly possible.

The fourth question treats lost oversight as a harm of its own, which supports reporting time-to-halt. The bounds clause of the [contract](../framework/contract.md) needs an agreed definition of an incident and a record of blocked attempts and near misses. This draft is one candidate. It creates no reporting duties, and its scale is built for large harms.

---

## Order of operations

1. **Inventory.** List every action, every tool, and every credential behind them. List the data sources each agent can read, with an owner and the date each was last checked. Reuse Part 4's tiers.
2. **Give each agent its own identity, and cut its privileges** (K1). Remove every permission the traces show it never uses.
3. **Move hard limits outside the agent's reach** (K2, K3). Sandbox it, separate production, and put caps in tools it cannot edit.
4. **Break the trifecta for untrusted input** (K10, K11). Pin and review its tools.
5. **Place gates where reversibility ends** (K4 to K6). Few, tiered, showing the blast radius, with a named person who holds authority.
6. **Make it stoppable and reversible, then drill it** (K7, K8). Check the action before it runs. Time the halt.
7. **Trace everything to an identity, and alert on it** (K9). Test that the alerts fire.
8. **Keep it portable, and re-test on every change** (K12).

Steps 1 and 2 cost almost nothing and remove the most blast radius. Steps 3 and 4 carry most of the protection. Step 6 is the one most teams skip.

---

## Traps

| Trap | The mistake |
|------|-------------|
| The Approval-as-Control Trap | Count every gate as a control |
| The Editable-Safeguard Trap | Put a limit where the agent can change it |
| The Borrowed-Credential Trap | Let the agent act on a person's token |
| The Untested-Kill-Switch Trap | Assume you can stop a run you have never stopped |
| The Detection-as-Defence Trap | Rely on an injection detector |
| The Single-Vendor Trap | Build a harness that cannot survive losing its model |
| The Late-Block Trap | Count a block on the reply as a control |
| The Untested-Fallback Trap | Test the primary model and trust the route behind it |
| The Over-Gating Trap | Gate everything |

---

## Link to the other factors

- Controllability supplies the **bounds clause** of the [contract](../framework/contract.md).
- The four numbers are numbers 6 to 9 on the [scorecard](../framework/scorecard.md).
- Controls cost value: gates use approver time and add latency. Measure task success with the controls on.

Sources are listed in the [README](../README.md#controllability).

Back to the [framework overview](../README.md).
