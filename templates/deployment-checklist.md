# Pre-Deployment Checklist

A compressed checklist for teams moving from evaluation to production. Each item maps to a factor in the Realized Value framework.

---

## Before You Deploy

### Capability

- [ ] Agent has been evaluated on a benchmark relevant to the target task class
- [ ] Real-task completion rate has been measured (not just benchmark pass rate)
- [ ] Autonomy horizon of agent >= target task length at the required reliability bar
- [ ] Domain-specific knowledge gaps have been assessed by subject matter experts
- [ ] Retrieval or tool augmentation has been tested if required for domain coverage

### Cost

- [ ] Cost per **successful** task is measured (retries and failures included in denominator)
- [ ] Agent cost per task is lower than equivalent human cost
- [ ] Integration and setup costs are amortized across expected task volume
- [ ] Context window size and call count per task are optimized
- [ ] Cost monitoring is instrumented before go-live (not added later)

### Reliability

- [ ] Agent has been tested in realistic staging conditions, not just benchmark environment
- [ ] All unique failure modes are documented with reproduction steps
- [ ] Integration failure injection tested: rate limits, expired tokens, schema drift
- [ ] Error surfacing verified: failures are visible, not silent
- [ ] Retry logic and graceful degradation are implemented for transient failures
- [ ] Reliability over production-representative task set >= required threshold

### Safety

- [ ] Agent behavior on ambiguous inputs is documented and acceptable
- [ ] Agent does not take actions outside its defined scope
- [ ] Confirmation prompts are in place before high-blast-radius or irreversible actions
- [ ] Safe failure mode verified: agent does nothing rather than the wrong thing when uncertain
- [ ] Prompt injection resistance tested if agent processes external/user-controlled text
- [ ] Safety behavior reviewed by Governance/Risk stakeholder

### Controllability

- [ ] Permissions are least-privilege -- only what the task requires
- [ ] Maximum blast radius from a single run is defined and documented
- [ ] Every agent action is logged with sufficient context for reconstruction
- [ ] Audit log is tamper-evident and has a defined retention period
- [ ] Kill switch tested: agent can be stopped mid-task without cascading side effects
- [ ] Human override path is documented, accessible, and tested
- [ ] All permission scopes reviewed and approved by CISO

---

## At Launch

- [ ] Monitoring dashboards are live before the first production task
- [ ] Alerting thresholds are set for cost, reliability, and error rate
- [ ] On-call rotation knows how to escalate agent incidents
- [ ] Rollback plan is documented and tested

---

## Post-Launch (First 30 Days)

- [ ] Production pass rate is being tracked and compared to staging baseline
- [ ] Cost per successful task is being monitored continuously
- [ ] Unexpected behaviors are being logged and reviewed weekly
- [ ] Agent Arena or session replay is available for spot-checking behavior
- [ ] Stakeholder sign-off checklist is complete and on file

---

## References

- [`framework/scorecard.md`](../framework/scorecard.md) -- full scoring rubric
- [`templates/evaluation-worksheet.md`](evaluation-worksheet.md) -- evidence-gathering worksheet
- [`framework/use-case-weights.md`](../framework/use-case-weights.md) -- context-dependent weighting
