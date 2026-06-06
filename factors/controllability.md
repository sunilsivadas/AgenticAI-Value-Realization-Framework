# Factor 5: Controllability

> Covered in depth in **Part 5** of the Realized Value series (forthcoming).

Controllability measures the operator's external leverage over the agent: the ability to constrain what it can do, observe what it has done, and stop it when necessary. It is the CISO's primary lens on any agentic deployment.

---

## The Control Stack

Controllability is not a single property. It is a stack of capabilities:

```
+-----------------------------+
|        Kill Switch          |  Can I stop the agent right now?
+-----------------------------+
|     Human Override Path     |  Can I intervene at any step?
+-----------------------------+
|        Audit Trail          |  Do I know what it did?
+-----------------------------+
|       Blast Radius          |  What's the worst case per run?
+-----------------------------+
|    Permission Scope         |  What can it access?
+-----------------------------+
```

Each layer assumes the one below it is working. A kill switch is only meaningful if the audit trail tells you when to use it.

---

## Controllability vs. Safety

This distinction matters because the remediations are different:

| | Safety | Controllability |
|--|--------|----------------|
| **Question** | Does the agent behave well? | Can I stop it if it doesn't? |
| **Failure** | Agent takes unauthorized action | Operator can't stop or reverse it |
| **Defense** | Model selection, system prompt, behavioral testing | Permissions, sandboxing, audit, kill switches |
| **Owner** | Model provider + prompt engineer | Platform / security team |

An agent that is controllable but not safe requires constant external intervention. An agent that is safe but not controllable is a deployment without a safety net.

---

## Integration Complexity and Controllability

The article identifies controllability as the factor most degraded by multi-system deployments:

- **Single system**: One permission scope, one audit trail, one rollback mechanism
- **3+ systems**: Multiple permission scopes must be coordinated; audit trails are fragmented across systems; rollback may be impossible if side effects are distributed

Controllability should be designed before multi-system integrations are wired up, not retrofitted after.

---

## Blast Radius Bounding

Every agent deployment should have a documented blast radius: the maximum harm that could result from a single agent run going wrong.

Blast radius is bounded by:
1. **Permission scope**: What systems and data can the agent touch?
2. **Reversibility**: Can the actions the agent takes be undone?
3. **Rate limits**: How many actions can it take before a human would notice?
4. **Scope duration**: Does the agent's permission scope expire?

Document the worst-case scenario explicitly. Then test that the kill switch stops the agent before it reaches that scenario.

---

## Human-in-the-Loop Design Patterns

The Agent Arena data shows users pull control back 2.3x more often than they hand it over. Effective HITL design works with this pattern:

| Pattern | When to Use |
|---------|-------------|
| **Checkpoint approval** | Before high-stakes or irreversible steps |
| **Intent confirmation** | Before starting tasks with large blast radius |
| **Exception escalation** | When agent detects ambiguity or unexpected state |
| **Periodic check-in** | For long-running tasks; progress report + override option |
| **Post-hoc review** | For low-stakes tasks; audit trail enables after-the-fact correction |

Design the override mechanism before the happy path. It's easier to build an escape hatch into the workflow than to bolt one on later.

---

## Key Resources

See the [Controllability section of the main catalog](../README.md#5-controllability--permissions-sandboxing--audit) for full resource tables.

### Highlighted Resources

| Resource | Why It Matters |
|----------|---------------|
| [E2B](https://github.com/e2b-dev/e2b) | Best-in-class cloud sandbox for isolating code execution |
| [Open Policy Agent](https://github.com/open-policy-agent/opa) | Industry standard for fine-grained permission policy enforcement |
| [LangGraph](https://github.com/langchain-ai/langgraph) | Built-in checkpointing and interrupt patterns for HITL workflows |
| [Temporal](https://github.com/temporalio/temporal) | Durable workflow engine with first-class human approval steps |
| [OpenTelemetry](https://github.com/open-telemetry/opentelemetry-python) | Vendor-neutral audit trail that survives multi-system deployments |
| [Falco](https://github.com/falcosecurity/falco) | Runtime security monitoring to detect anomalous agent behavior |

---

## Common Pitfalls

- **Permissions granted for convenience**: Development-time permissions (admin, broad read/write) persist to production because no one revisited them.
- **Audit trail as an afterthought**: Adding logging after deployment means early production runs have no audit record when the first incident occurs.
- **Untested kill switches**: Kill switches that have never been tested in production often don't work — or cause cascading side effects when they do.
- **Blast radius undocumented**: If the blast radius was never written down, it was never bounded.
- **HITL as bottleneck, not safety valve**: Human checkpoints that require approval for every action slow the agent to below human speed. Design them for exceptions, not the happy path.
