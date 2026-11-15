# The scorecard: twelve numbers

From [Part 6, From framework to ROI](https://sunilsivadas.github.io/roi.html#one-scorecard).

Twelve numbers carry the whole case: ten for the agent and two for the organisation. Engineering, finance and risk can read the same sheet, because each number feeds a line of the business case.

An earlier version of this file asked for a score from 0 to 1 on each factor and multiplied the five. The series does not support that. Only cost has a clean unit, and a composite score hides the factor that binds. Report the twelve numbers below, each with its own threshold.

---

## The twelve

| # | Number | Factor | Business-case line it feeds | Defined in |
|---|--------|--------|-----------------------------|------------|
| 1 | Cost per successful task | Cost | Run cost | [Part 2](https://sunilsivadas.github.io/cost.html) |
| 2 | pass^k, with its confidence interval | Reliability | How far the reliability lines can be trusted | [Part 3](https://sunilsivadas.github.io/reliability.html) |
| 3 | Hand-back rate | Reliability | People's time | Part 3 |
| 4 | Silent-failure rate | Reliability | Rework, refunds, complaints | Part 3 |
| 5 | Severity-weighted unsafe-action rate, at its intervention rate | Safety | Expected loss | [Part 4](https://sunilsivadas.github.io/safety.html) |
| 6 | Bounded share | Controllability | Share of the risk with a cap | [Part 5](https://sunilsivadas.github.io/controllability.html) |
| 7 | Bound-leak rate | Controllability | Whether the cap holds | Part 5 |
| 8 | Time-to-halt | Controllability | Size of the worst day | Part 5 |
| 9 | Gate load | Controllability | Approver time, and whether the gates still work | Part 5 |
| 10 | Realized value per case | All five | Saving per case | [Part 6](https://sunilsivadas.github.io/roi.html) |
| 11 | Volume routed to the agent | Organisation | Scale of the saving, and the break-even point | Part 6 |
| 12 | Return per month | Organisation | Volume × saving + redeployed value − fixed costs | Part 6 |

Capability has no row of its own. It decides which cases the agent can attempt at all, and it is measured before the scorecard starts (step 4 of the [build sequence](../templates/deployment-checklist.md)). Cases beyond the ceiling stay with people.

---

## Definitions

**1. Cost per successful task.** Cost per run divided by success rate. Failed runs are paid for and deliver nothing, so they raise this number directly.

**2. pass^k.** The share of tasks solved on all k tries. State k, the task set and the grader. Report the confidence interval.

**3. Hand-back rate.** Share of runs where the agent stopped and said so: it abstained, asked, or escalated to a person. The failure is visible.

**4. Silent-failure rate.** Share of runs where the agent finished, reported success, and the result was wrong. Measure it by sampling "successful" runs and checking them against the record. It is the input that moves the business case most, and the public record leaves it out.

**5. Severity-weighted unsafe-action rate.** How often the agent acts outside its authority, weighted by how bad each action is. Report it with the intervention rate: asks, abstentions and escalations per task. Drive the first down without watching the second and you build an agent that asks about everything.

**6. Bounded share.** Share of High and Critical actions behind a hard limit or a gate.

**7. Bound-leak rate.** Share of red-team attempts that get past a stated bound.

**8. Time-to-halt.** From first bad action to stop, in drills and incidents. Also from action to block, for each guardrail.

**9. Gate load.** Approvals per person per hour, and the approval rate. A rising approval rate is the sign that people have stopped reading the prompts.

**10. Realized value per case.** Human cost per case minus agent cost per case. See [`cost-model.md`](cost-model.md).

**11. Volume routed to the agent.** Cases per month. It sets the scale of the saving and the break-even point.

**12. Return per month.** Volume × saving per case, plus the value of redeployed time, minus fixed costs.

---

## How to run it

The scorecard is the governance instrument.

1. **Before the first run**, governance sets a threshold beside each number, with the action if it is missed: fix it, narrow the scope, or stop. These are the kill criteria.
2. **Name an owner** for each number.
3. **After launch**, report the twelve together, every month.
4. **Re-run** after every change of model, harness or tool.

---

## The sheet

Deployment: ______________________  Period: ______________  Model and harness version: ______________

| # | Number | Threshold | Action if missed | Owner | This period | Last period |
|---|--------|-----------|------------------|-------|-------------|-------------|
| 1 | Cost per successful task | | | | | |
| 2 | pass^k (k = ___), with interval | | | | | |
| 3 | Hand-back rate | | | | | |
| 4 | Silent-failure rate (audited sample of ___) | | | | | |
| 5 | Severity-weighted unsafe-action rate | | | | | |
| 5b | Intervention rate | | | | | |
| 6 | Bounded share | | | | | |
| 7 | Bound-leak rate (red-team protocol: ___) | | | | | |
| 8 | Time-to-halt (last drill: ___) | | | | | |
| 9 | Gate load, and approval rate | | | | | |
| 10 | Realized value per case | | | | | |
| 11 | Volume routed to the agent | | | | | |
| 12 | Return per month | | | | | |

Binding constraint this period: ______________________

What changed since the last report (model, harness, tools, scope): ______________________

---

## Where the arithmetic stops

- **Cost and reliability** convert to money cleanly. Runs, hand-backs and rework can be counted.
- **Safety** converts as expected loss, and the loss per unsafe action is a judgement call. Write down who made it, and on what evidence.
- **Controllability** converts worst. Its main value is the cap on the worst day, and an average hides the worst day. Report the largest loss a single case can cause, with and without the bounds, beside the expected value.
- **The ceiling moves.** A business case written against one model generation needs re-running on the next, and so does the scorecard.

The public customer-service record covers three of the twelve: cost, the resolution rate behind the hand-back rate, and volume.
