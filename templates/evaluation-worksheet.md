# Evaluation worksheet

Fill this in for one deployment. It follows the first four steps of the [build sequence](deployment-checklist.md), which decide whether to build at all, and then sets the thresholds for the [scorecard](../framework/scorecard.md).

Deployment: ______________________  Date: ______________  Completed by: ______________________

Model, harness and tool versions: ______________________

---

## 1. Frame the use case

One sentence on what the agent does, for whom:

______________________________________________________________

Rate the five attributes ([guide](../framework/use-case-weights.md)):

| Attribute | Rating (Low / Medium / High) | Why |
|-----------|------------------------------|-----|
| Stakes: what does a wrong output cost? | | |
| Autonomy: how long without a human checkpoint? | | |
| Reversibility: can a wrong output be undone? | | |
| Integration complexity: how many systems? | | |
| Verifiability: can you tell if the output is right? | | |

Expected binding constraint, from the ratings: ______________________

---

## 2. List and tier the actions

Every tool the agent can call. Severity sets the floor. Detectability can lower a tier only when a code or state check catches the failure before it reaches anyone.

| Action | What it touches | Reversible? | Who bears a failure | Tier (Low / Medium / High / Critical) | Reliability bar (k, and maximum silent-failure rate) |
|--------|-----------------|-------------|---------------------|----------------------------------------|------------------------------------------------------|
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |

Scope and authority, in one paragraph the agent will be given (lever S1):

______________________________________________________________

What counts as high-stakes for this deployment (lever S3):

______________________________________________________________

---

## 3. Measure the human baseline

Without a baseline there is no return to report.

| Measure | Value | How it was measured | Date |
|---------|-------|---------------------|------|
| Cost per case | | | |
| Time per case | | | |
| Error rate per case | | | |
| Volume per month | | | |

---

## 4. Build the golden set

| Item | Value |
|------|-------|
| Number of tasks | |
| Where the tasks came from (real cases, confirmed failures) | |
| Grader for each check (code, state check, LLM judge, person) | |
| If an LLM judge: true positive and true negative rates against an expert's labels | |
| Paraphrases, injected faults and long sessions included? | |

---

## 5. Measure the ceiling

Under generous conditions: best effort, ideal harness, no time pressure, no reliability threshold.

| Measure | Value |
|---------|-------|
| Benchmark or internal eval used | |
| Score | |
| Score the task needs | |

If the ceiling sits below what the task needs, stop here. No later step recovers it.

Decision: ☐ Proceed  ☐ Stop  ☐ Narrow the scope and re-measure

---

## 6. Run the golden set k times

| Result | Value |
|--------|-------|
| k | |
| pass^k, with confidence interval | |
| Items that always pass | |
| Items that sometimes pass (reliability work) | |
| Items that never pass (capability gap: back to step 5) | |
| Hand-back rate, per run | |
| Silent-failure rate, per run, from an audited sample of ___ | |
| Worst run | |

---

## 7. Price one case

The [cost model](../framework/cost-model.md), with your own numbers.

| Input | Value | Source |
|-------|-------|--------|
| Human cost per case (from section 3) | | |
| Run cost per case | | |
| Hand-back rate | | |
| Silent-failure rate | | |
| Cost of an error | | |
| Unsafe-action rate | | |
| Loss per unsafe action (who judged it, on what evidence) | | |
| Gate rate | | |
| Approver cost per approval | | |

```
agent cost per case = run cost
                    + hand-back rate      × human cost per case
                    + silent-failure rate × cost of an error
                    + unsafe-action rate  × loss per unsafe action
                    + gate rate           × approver cost
```

| Result | Value |
|--------|-------|
| Agent cost per case | |
| Realized value per case (human cost − agent cost) | |
| Fixed monthly cost (evaluation, monitoring, ownership) | |
| Break-even volume (fixed monthly cost ÷ saving per case) | |
| Largest loss a single case can cause, without the bounds | |
| Largest loss a single case can cause, with the bounds | |
| Silent-failure rate at which the saving is gone | |

---

## 8. Write the kill criteria

Before the pilot. Beside each threshold, write what happens if it is missed: fix it, narrow the scope, or stop.

| Criterion | Threshold | Action if missed | Owner |
|-----------|-----------|------------------|-------|
| pass^k at the tier's k | | | |
| Maximum silent-failure rate, from audited samples | | | |
| Maximum cost per successful task | | | |
| Maximum severity-weighted unsafe-action rate | | | |
| Minimum bounded share | | | |
| Maximum time-to-halt in a drill | | | |
| Break-even volume, reached by (date) | | | |

---

## 9. Check the organisation

| Question | Answer |
|----------|--------|
| Which work is routed to the agent, and how much of it? | |
| What changes in the work so the gates open wider? | |
| What do people do with the time freed? How is its value counted? | |
| Who owns each factor? | |
| Who is accountable when the agent is wrong? | |
| When is the next re-run (model, harness or tool change)? | |

---

## Outcome

Binding constraint, as measured: ______________________

Decision: ☐ Build  ☐ Narrow the scope  ☐ Stop

Signed off by: ______________________  Date: ______________
