# The three-clause contract

From [Part 5, The contract, and the series answer](https://sunilsivadas.github.io/controllability.html#the-contract-and-the-series-answer).

Part 1 asked for a way to specify "can do X" precisely enough to write into a contract. Parts 3, 4 and 5 each supply one clause.

The first two clauses say what the agent will do. The third says what happens when it does not. A buyer with only the first two has a forecast. A buyer with all three has a limit on the downside.

This is the author's recommendation. He found no enterprise publishing terms like these as of November 2026. The Monetary Authority of Singapore's guidelines come closest: an inventory, least privilege, and kill switches tested regularly are most of the bounds clause.

---

## The clauses

| Clause | From | What it states |
|--------|------|----------------|
| **Measurement** | Part 3 | pass^k at a stated k, with its confidence interval, beside the hand-back and silent-failure rates, on a stated task set, with a stated grader |
| **Behaviour** | Part 4 | A severity-weighted unsafe-action rate and a claim-against-trace mismatch rate, on a stated task set, at a stated intervention rate |
| **Bounds** | Part 5 | The action inventory and tiers; the bounded share of High and Critical actions; the bound-leak rate under a stated red-team protocol; time-to-halt in a stated drill; gate load; the fallback route and its tests; notice periods for model deprecation and withdrawal |

---

## Questions to put to a vendor

A vendor's headline rate becomes checkable when it arrives with all three clauses, measured on your own cases.

### Measurement

- [ ] What is pass^k on our tasks, and at what k?
- [ ] What is the confidence interval, and how many tasks and runs produced it?
- [ ] Who or what graded the runs? If an LLM judge, what are its true positive and true negative rates against an expert's labels?
- [ ] What are the hand-back rate and the silent-failure rate, per run?
- [ ] How were unfinished and timed-out runs scored?
- [ ] What changed in these numbers after the last model, harness or tool upgrade?

### Behaviour

- [ ] What is the severity-weighted unsafe-action rate on our task set?
- [ ] What is the intervention rate at which that was measured: asks, abstentions and escalations per task?
- [ ] How often does the agent's report differ from its trace?
- [ ] For each guardrail and judge: what are the miss rate and the false-alarm rate?

### Bounds

- [ ] What is the full action inventory, and which tier is each action in?
- [ ] What share of High and Critical actions sits behind a hard limit or a gate?
- [ ] Under which red-team protocol was the bound-leak rate measured, and what was it?
- [ ] How long does a halt take in a drill? When was the last drill?
- [ ] How many approvals does each person handle per hour, and what is the approval rate?
- [ ] Which model answers when the vendor's safeguards block a request? Has that fallback route been attacked with its production safeguards on?
- [ ] What notice do we get before a model is deprecated or withdrawn?

---

## Why the fallback question is there

A safeguard can move risk onto the route it creates. Anthropic's system card for Claude Fable 5.2 reports that requests its cyber classifier blocks can be handed to an older model. In one adaptive test run by Gray Swan, 99.46% of answered requests took that route and 90.31% of those were compromised ([system card](https://assets.claude.com/27d60918d218125e7504bc7354c4b4626ec56b11.pdf), vendor-reported). On the API the fallback is opt-in, so it is the operator's setting.

Test the fallback route as hard as the primary.
