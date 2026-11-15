# The cost model: pricing each factor per case

From [Part 6, From framework to ROI](https://sunilsivadas.github.io/roi.html).

The formula is a mental model. A business case needs the same idea in money, per case handled. Each factor maps onto one line.

---

## The lines

| Factor | Business-case line | Unit from the series |
|--------|--------------------|----------------------|
| Capability | Which cases the agent can attempt at all. Cases beyond the ceiling stay with people | Measured under generous conditions (Part 1) |
| Cost | What each run costs | Cost per successful task (Part 2) |
| Reliability | Hand-backs cost a person's time. Silent failures cost rework, refunds and complaints | pass^k, with the hand-back and silent-failure rates (Part 3) |
| Safety | Expected loss from actions outside the agent's authority: rate times severity | Severity-weighted unsafe-action rate, at its intervention rate (Part 4) |
| Controllability | The cap on the worst case, and the approver time the gates use | Bounded share, bound-leak rate, time-to-halt, gate load (Part 5) |

---

## The formula

For the cases inside the ceiling:

```
agent cost per case = run cost
                    + hand-back rate      × human cost per case
                    + silent-failure rate × cost of an error
                    + unsafe-action rate  × loss per unsafe action
                    + gate rate           × approver cost

realized value per case = human cost per case − agent cost per case
```

Part 2's cost per successful task already counts the failed runs you pay for. This formula goes one step further and prices what each failure does after the run.

One level up, the organisation turns the saving into a return:

```
return = volume × saving per case
       + value of redeployed time
       − fixed costs

break-even volume = fixed monthly cost ÷ saving per case
```

Fixed costs include integration with the systems of record, the golden set and its graders, the controls, the drills, the monitoring, and a named owner. Compute the break-even volume before the pilot.

---

## Worked case: customer service

Customer service is where agents have the longest public record. Under outcome pricing, a failed attempt costs the buyer nothing extra: the vendor is unpaid, and the case goes to a person at the usual cost. So the model reduces to two terms.

```
saving per conversation = resolution rate × (human cost − price per resolution)
                        − silent-failure rate × cost of a silent failure
```

### Inputs

| Input | Value | Source | Status |
|-------|-------|--------|--------|
| Human cost per live contact | $8.01, the average across phone, chat and email | [Gartner, Sep 2019](https://www.gartner.com/en/newsroom/press-releases/2019-09-25-gartner-says-only-9--of-customers-report-solving-thei) | Reported; seven years old |
| Agent price | $0.99 per resolution, charged only when resolved | [Fin](https://www.intercom.com/help/en/articles/8205718-fin-resolutions) | Published list price, checked 1 Nov 2026 |
| Resolution rate, vendor average | 76% across 12,000 customers | [Fin, Mar 2026](https://fin.ai/learn/roi-ai-customer-service-agents-benchmarks) | Vendor-reported |
| Resolution rate, one deployment | 50.8% | [Fin, Mar 2026](https://fin.ai/learn/roi-ai-customer-service-agents-benchmarks) | Vendor-reported |
| Silent-failure rate | Unreported | No source found | Missing |
| Cost of a silent failure | From one repeat contact ($8.01) to C$812.02 ordered by a tribunal, about US$600 | Gartner; [Moffatt v. Air Canada](https://decisions.civilresolutionbc.ca/crt/crtd/en/525448/1/document.do) | Reported range |

### Result

Saving per conversation, by resolution rate and silent-failure assumption:

| Resolution rate | No silent failures | 5% silent, each a repeat contact | 1% silent, each costing US$600 |
|-----------------|--------------------|----------------------------------|--------------------------------|
| 76% (vendor average) | $5.34 | $4.94 | −$0.66 |
| 50.8% (one deployment) | $3.57 | $3.17 | −$2.43 |

At US$600 a failure, the whole saving is gone when 0.9% of conversations fail silently at the 76% rate, and 0.6% at the 50.8% rate.

Check the first cell: 0.76 × (8.01 − 0.99) = 5.34.

### Break-even

At $5.34 a conversation, each $10,000 a month of evaluation, monitoring and ownership needs about 1,900 conversations a month. At $3.57, about 2,800. The build cost comes on top.

### What the case shows

- **The agent's fee is the smallest line.** At a 76% resolution rate, fees come to $0.75 a conversation. Hand-backs cost $1.92. Ten points of resolution rate are worth $0.70 a conversation, nearly the whole fee.
- **The market prices a single-try number.** A resolution counts when the customer stops asking. That number includes some silent failures.
- **The tail decides.** Most silent failures cost a repeat contact, and the case survives them easily. A few cost far more, and under 1% of those erases the saving. The lever is scope: keep answers about policy, refunds and legal terms inside retrieved, checked text, and send them to a person when the check fails.
- **Quality shows up late.** Klarna's cost numbers improved for over a year before its CEO said quality had suffered.

---

## Greenfield

A company built around agents from the start has no human contact to avoid. Its saving per case becomes a margin:

```
return = volume × (price − agent cost per case) − fixed costs
```

The same lines apply. Run cost shows in gross margin. Hand-backs show as the people the company still needs. Silent failures and unsafe actions show as liability, which stays with the company.

---

## Use your own numbers

Every input above is public and dated. None of them is yours. Replace each one with a measurement from your own process before you rely on the result, starting with the two that move it most: the resolution rate and the silent-failure rate.

The worksheet in [`../templates/evaluation-worksheet.md`](../templates/evaluation-worksheet.md) has a blank version of this model.
