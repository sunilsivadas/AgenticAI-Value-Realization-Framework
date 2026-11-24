# Factor 3: Reliability

Summary of [Part 3, Reliability is getting it right every time](https://sunilsivadas.github.io/reliability.html). The article makes the argument in about 25 minutes. Its [reference page](https://sunilsivadas.github.io/reliability-reference.html) carries the detail and the sources.

Benchmarks report pass@1. Production needs pass@always. Reliability is the second discount: does the agent finish every time, recover from mid-task errors, and fail safely when it cannot?

---

## Three claims

1. **Reliability is its own property, and it moves on a different curve from capability.**
2. **Reliability is a system property, like capability.**
3. **The unit that matters is pass^k on your own task distribution.**

---

## The unit

**pass^k**: the share of tasks solved on all k tries. It is the number a customer gets.

On Mercor's APEX-Agents, the best agent passed 24% of tasks on a single try and 13.4% on all eight ([Mercor](https://arxiv.org/abs/2601.14242)).

Report pass^k with two rates beside it, because production has three outcomes for every run:

| Outcome | What happened | What it costs |
|---------|---------------|---------------|
| **Correct** | The result is right, checked against the golden answer or the system state | The run |
| **Handed back** | The agent stopped and said so. A person picks it up | Attention. Budget for it |
| **Silently wrong** | The agent finished, reported success, and the result is wrong | Money. Nobody knows until it lands |

Out-of-date source data is a direct cause of silent failures. The agent retrieves a passage that has been replaced and answers from it with confidence. On the HOH benchmark, outdated passages in the retrieved context caused a performance drop of at least 20%, and the authors conclude that outdated information is a greater risk than having no relevant information ([Ouyang et al.](https://aclanthology.org/2025.acl-long.301.pdf), peer-reviewed). So some silent failures are fixed in the source, and no change to the agent removes them.

Real work shows success falling as tasks get longer. On research tasks that OpenAI's own researchers handed to coding agents, estimated success without human intervention in October 2026 was 46% for tasks of two to four hours and 35% for tasks of four to eight hours ([OpenAI](https://openai.com/index/research-acceleration-jagged-frontier/), vendor-reported). A model estimated the task lengths, and the tasks are the ones researchers chose to delegate.

Take two agents. Agent A is correct on 80% of runs and silently wrong on 20%. Agent B is correct on 75%, hands back 20% and is silently wrong on 5%. On pass@1, A wins. In production, B is the one you can deploy.

---

## The test you already hold

Run your golden dataset k times and sort every item into one of three groups:

- **Always passes.** Reliable on this item.
- **Never passes.** A capability gap. More runs will not fix it. Go back to Part 1.
- **Sometimes passes.** The flaky middle. This is the reliability problem, and a single run hides it.

Set k by tier. See the bar per tier in [`../framework/use-case-weights.md`](../framework/use-case-weights.md).

---

## Metrics to ask for

Ask for these from any team, vendor or harness, measured on your own golden set and traffic.

| Metric | What it tells you |
|--------|-------------------|
| pass^k at a stated k, with a confidence interval | How often the system gets it right every time |
| Per-item split: always, sometimes, never | Which failures are reliability and which are capability |
| Hand-back rate and silent-failure rate, per run | Whether failures arrive labelled or land unseen |
| Strict pass beside partial credit, with the count of unfinished and timed-out runs | Whether the work was finished, or mostly done |
| Worst run, beside the average | The run that matters most for high-recall tasks |
| pass^k per channel and user group | Whether one channel or group carries the failures |
| Per-step tool error and retry rates | Where the compounding starts |
| Recovery rate after an injected fault | Whether the agent resumes or starts over |
| Calibration of the confidence used to hand back | Whether hand-backs fire on the right runs |
| Verifier false-accept and false-reject rates | Silent failures let through, and retries wasted |
| Judge true positive and true negative rates against an expert's labels | Whether grader error is moving pass^k |
| Change after a model, harness, tool or infrastructure upgrade | Whether reliability moved when accuracy did not |

---

## The twelve levers, in five groups

| Group | Question | Levers |
|-------|----------|--------|
| **D. Design out variance** | Can the run avoid the failure at all? | R1. Workflow before agent. R2. Fewer steps. R3. Deterministic tools and a fixed environment |
| **V. Verify** | Does the run know when it is wrong? | R4. Code verifiers and tests. R5. Critic or verifier loops. R6. Ask before guessing |
| **R. Recover** | Can the run resume after an error? | R7. Checkpoints and resumable state. R8. Idempotent, retry-safe tools. R9. Bounded retries with fallback |
| **C. Contain** | Does the run stop before it does damage? | R10. Abstain on low confidence |
| **O. Observe** | Will you see the drift? | R11. Trace-level telemetry. R12. Regression evals on every change |

---

## Order of operations

1. **Set the bar per action.** List the actions, rate consequence, exposure and detection, and write down the k and silent-failure rate each tier needs. Governance signs off the bar and names its owner.
2. **Run the golden set k times.** Add paraphrases, faults and long sessions. Count three outcomes. Check the grader against humans, and use code where the answer is known.
3. **Separate the failures.** Items that never pass are capability problems. Items that pass some of the time are reliability problems. Mark each failure as caused by the agent or by the source data: out of date, duplicated or undocumented. The second kind is fixed in the source.
4. **Design out variance** (R1 to R3).
5. **Add verification** (R4 to R6). Code checks first, critics where code cannot reach. Measure the verifier's two error rates.
6. **Add recovery** (R7 to R9).
7. **Add containment** (R10). Hand back on low confidence, within a hand-back budget.
8. **Observe** (R11, R12). Trace production, compute pass^k from real runs, feed incidents into the golden set, and re-run it on every change.

Steps 1 to 3 are measurement. Most of the leverage is in steps 4 and 5.

---

## Traps

| Trap | The mistake |
|------|-------------|
| The Golden-Set Trap | Run the golden dataset once before each release |
| The Pass@1 Trap | Write an SLA around a single-try score |
| The Best-Run Trap | Judge the agent on a demo |
| The Averaging Trap | Report mean success |
| The Small-Sample Trap | Compare pass^k on a few dozen tasks. At 30 tasks the interval is about ±18 points |
| The Grader Trap | Trust an LLM judge on a new model |
| The Retry-Hides-It Trap | Let retries absorb flakiness |
| The Version Trap | Compare scores across benchmark releases |
| The Upgrade Regression Trap | Swap the model, keep the harness, skip the evals |
| The Max-Effort Trap | Set effort to max and assume the best result |

---

## Link to the other factors

- Reliability supplies the **measurement clause** of the [contract](../framework/contract.md).
- pass^k, the hand-back rate and the silent-failure rate are numbers 2 to 4 on the [scorecard](../framework/scorecard.md).
- Verification costs money. Reliability levers raise cost per run, so re-measure cost per successful task after adding them.

Benchmarks and tools you can run are listed in the [README](../README.md#reliability).

Next: [Safety](safety.md).
