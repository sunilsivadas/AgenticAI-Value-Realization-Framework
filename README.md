# Realized Value — Agentic AI Evaluation Framework

> Companion repository to the **[Realized Value](https://sunilsivadas.github.io/realized-value.html)** article series: *A Framework for Evaluating Agentic AI in the Enterprise*.

[![Entries](https://img.shields.io/badge/resources-120+-blue)](#catalog)
[![Factors](https://img.shields.io/badge/factors-5-green)](#the-five-factors)
[![Series](https://img.shields.io/badge/articles-6-orange)](#article-series)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)](CONTRIBUTING.md)

---

## The Framework

```
Realized Value = Capability × Cost × Reliability × Safety × Controllability
```

The factors **multiply**. One near-zero factor zeros the product.

| Factor | Role | Primary Veto Holder |
|--------|------|---------------------|
| **Capability** | Value creator — the only term that *adds* value; all others discount it | Product / Engineering |
| **Cost** | First discount — cost per successful task, retries and failures counted in | Finance |
| **Reliability** | Second discount — pass@always, not pass@1 | Product / Engineering |
| **Safety** | Third discount — conservative behavior under ambiguity | Governance / Risk |
| **Controllability** | Fourth discount — operator leverage, blast radius, kill switches | CISO |

Enterprise product-market fit requires crossing **all five** thresholds simultaneously.

---

## Article Series

| Part | Title | Status |
|------|-------|--------|
| [Part 0](https://sunilsivadas.github.io/realized-value.html) | Introduction: The Realized Value Framework | Published |
| Part 1 | Capability: Realizing the Ceiling vs. Buying It | Forthcoming |
| Part 2 | Cost: The Economics of the Successful Task | Forthcoming |
| Part 3 | Reliability: pass@always | Forthcoming |
| Part 4 | Safety: Agent Behavior Under Uncertainty | Forthcoming |
| Part 5 | Controllability: Operator Leverage and Security Positioning | Forthcoming |

---

## How to Use This Repository

- **Evaluating a deployment?** Start with [`templates/evaluation-worksheet.md`](templates/evaluation-worksheet.md) and the [`framework/scorecard.md`](framework/scorecard.md).
- **Researching a specific factor?** Jump to its catalog section or the [`factors/`](factors/) deep-dive files.
- **Tracking benchmark data?** See [`data/benchmarks.yaml`](data/benchmarks.yaml).
- **Adding a resource?** Read [`CONTRIBUTING.md`](CONTRIBUTING.md).

---

## Category Overview

| Category | Resources |
|----------|-----------|
| [Capability: Benchmarks & Evals](#1-capability--benchmarks--evals) | 28 |
| [Cost: Observability & Optimization](#2-cost--observability--optimization) | 18 |
| [Reliability: Testing & Production Harnesses](#3-reliability--testing--production-harnesses) | 22 |
| [Safety: Guardrails & Behavior](#4-safety--guardrails--behavior) | 20 |
| [Controllability: Permissions, Sandboxing & Audit](#5-controllability--permissions-sandboxing--audit) | 20 |
| [Framework Resources & Templates](#6-framework-resources--templates) | 12 |

---

## Catalog

### 1. Capability — Benchmarks & Evals

Measures the ceiling: what agents can accomplish under ideal conditions.

#### Agent Task Benchmarks

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [SWE-bench](https://github.com/princeton-nlp/SWE-bench) | ![stars](https://img.shields.io/github/stars/princeton-nlp/SWE-bench?style=flat-square) | eval, coding, tasks | Industry-standard benchmark for resolving real GitHub issues |
| [SWE-bench Verified](https://openai.com/index/introducing-swe-bench-verified/) | — | eval, coding, verified | Human-validated subset with higher-quality labels |
| [METR Task Standard](https://github.com/METR/task-standard) | ![stars](https://img.shields.io/github/stars/METR/task-standard?style=flat-square) | eval, autonomy, tasks | Standard for defining and measuring autonomous task completion |
| [AgentBench](https://github.com/THUDM/AgentBench) | ![stars](https://img.shields.io/github/stars/THUDM/AgentBench?style=flat-square) | eval, multi-env, benchmark | Multi-environment benchmark across OS, DB, web, and code tasks |
| [OSWorld](https://github.com/xlang-ai/OSWorld) | ![stars](https://img.shields.io/github/stars/xlang-ai/OSWorld?style=flat-square) | eval, computer-use, desktop | Benchmark for desktop GUI agents on real computer tasks |
| [WebArena](https://github.com/web-arena-x/webarena) | ![stars](https://img.shields.io/github/stars/web-arena-x/webarena?style=flat-square) | eval, web, browser | Realistic web environment benchmark for autonomous agents |
| [WorkArena](https://github.com/ServiceNow/WorkArena) | ![stars](https://img.shields.io/github/stars/ServiceNow/WorkArena?style=flat-square) | eval, enterprise, workflow | ServiceNow-based enterprise task benchmark |
| [tau-bench](https://github.com/sierra-research/tau-bench) | ![stars](https://img.shields.io/github/stars/sierra-research/tau-bench?style=flat-square) | eval, customer-service, tool-use | Benchmark for tool-use agents in real-world service tasks |
| [AppWorld](https://github.com/stonybrooknlp/appworld) | ![stars](https://img.shields.io/github/stars/stonybrooknlp/appworld?style=flat-square) | eval, multi-app, tasks | Benchmark across realistic multi-app task environments |

#### Capability Measurement Tools

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [LM-Eval Harness](https://github.com/EleutherAI/lm-evaluation-harness) | ![stars](https://img.shields.io/github/stars/EleutherAI/lm-evaluation-harness?style=flat-square) | eval, harness, llm | Unified framework for evaluating language models across tasks |
| [Evals (OpenAI)](https://github.com/openai/evals) | ![stars](https://img.shields.io/github/stars/openai/evals?style=flat-square) | eval, framework, tasks | Framework for building and running model evaluations |
| [HELMET](https://github.com/princeton-nlp/HELMET) | ![stars](https://img.shields.io/github/stars/princeton-nlp/HELMET?style=flat-square) | eval, long-context, rag | Holistic evaluation of long-context language models |
| [BrowserBench](https://github.com/web-arena-x/browserbench-main) | — | eval, browser, web | Browser-based agent capability benchmark |
| [GAIA](https://huggingface.co/datasets/gaia-benchmark/GAIA) | — | eval, general, agi | General AI Assistants benchmark for real-world task solving |

#### Autonomy Horizon Resources

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [METR Autonomy Evals](https://metr.org/blog/2023-08-01-new-report-autonomous-replication-and-adaptation/) | — | autonomy, safety, risk | Research on measuring autonomous replication and adaptation |
| [Remote Labor Index](https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/) | — | autonomy, labor, tasks | METR survey measuring AI ability to complete long real-world tasks |
| [GDPval Methodology](https://arxiv.org/abs/2312.11805) | — | capability, economics, valuation | Occupational task completion approach to economic value estimation |

#### Leaderboards & Trackers

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [LMSYS Chatbot Arena](https://lmarena.ai/) | — | leaderboard, elo, human-pref | Human-preference Elo leaderboard for chat models |
| [Open LLM Leaderboard](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard) | — | leaderboard, open, benchmarks | HuggingFace benchmark leaderboard for open models |
| [Agent Arena](https://agentarena.ai/) | — | leaderboard, agents, behavior | Real-world agent session behavior and control observations |
| [Scale HELM](https://crfm.stanford.edu/helm/) | — | leaderboard, holistic, evaluation | Holistic evaluation of language models across scenarios |

---

### 2. Cost — Observability & Optimization

Cost per successful task — retries and failures counted in.

#### Token & Cost Tracking

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [Langfuse](https://github.com/langfuse/langfuse) | ![stars](https://img.shields.io/github/stars/langfuse/langfuse?style=flat-square) | observability, cost, tracing | Open-source LLM observability with cost tracking per trace |
| [LiteLLM](https://github.com/BerriAI/litellm) | ![stars](https://img.shields.io/github/stars/BerriAI/litellm?style=flat-square) | proxy, cost, multi-provider | Unified LLM API proxy with cost tracking across 100+ providers |
| [OpenLLMetry](https://github.com/traceloop/openllmetry) | ![stars](https://img.shields.io/github/stars/traceloop/openllmetry?style=flat-square) | observability, opentelemetry, cost | OpenTelemetry-based LLM observability SDK |
| [Helicone](https://github.com/Helicone/helicone) | ![stars](https://img.shields.io/github/stars/Helicone/helicone?style=flat-square) | proxy, observability, cost | Open-source LLM observability and cost management proxy |
| [OpenMeter](https://github.com/openmeterio/openmeter) | ![stars](https://img.shields.io/github/stars/openmeterio/openmeter?style=flat-square) | metering, billing, usage | Usage metering infrastructure for AI/cloud workloads |

#### Prompt & Context Optimization

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [DSPy](https://github.com/stanfordnlp/dspy) | ![stars](https://img.shields.io/github/stars/stanfordnlp/dspy?style=flat-square) | optimization, prompts, programming | Framework for algorithmically optimizing prompts and pipelines |
| [LLMLingua](https://github.com/microsoft/LLMLingua) | ![stars](https://img.shields.io/github/stars/microsoft/LLMLingua?style=flat-square) | compression, context, cost | Prompt compression to reduce token cost while preserving quality |
| [TokenCount](https://github.com/openai/tiktoken) | ![stars](https://img.shields.io/github/stars/openai/tiktoken?style=flat-square) | tokenization, cost-estimation, tooling | Fast tokenizer for accurate cost estimation before API calls |

#### Model Routing & Efficiency

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [RouteLLM](https://github.com/lm-sys/RouteLLM) | ![stars](https://img.shields.io/github/stars/lm-sys/RouteLLM?style=flat-square) | routing, cost, efficiency | Cost-efficient routing between strong and weak LLMs |
| [OpenRouter](https://github.com/OpenRouterAI/openrouter-runner) | ![stars](https://img.shields.io/github/stars/OpenRouterAI/openrouter-runner?style=flat-square) | routing, multi-model, cost | Unified API routing across models with cost transparency |

#### Cost Calculators & References

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [llm-price-check](https://github.com/AmberSahdev/Open-Interface) | — | pricing, comparison, reference | LLM pricing comparison across providers |
| [AI Cost Calculator](https://huggingface.co/spaces/philschmid/llm-pricing) | — | pricing, huggingface, calculator | HuggingFace-hosted LLM pricing estimation tool |

---

### 3. Reliability — Testing & Production Harnesses

Distinguishes benchmark pass@1 from production pass@always.

#### Agent Testing Frameworks

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [AgentEval](https://github.com/microsoft/autogen/tree/main/samples/tools/agenteval) | — | eval, autogen, reliability | AutoGen-based framework for quantifying agent task utility |
| [Promptfoo](https://github.com/promptfoo/promptfoo) | ![stars](https://img.shields.io/github/stars/promptfoo/promptfoo?style=flat-square) | testing, ci, regression | LLM test framework for CI/CD regression and reliability testing |
| [DeepEval](https://github.com/confident-ai/deepeval) | ![stars](https://img.shields.io/github/stars/confident-ai/deepeval?style=flat-square) | testing, metrics, evaluation | Unit-testing framework for LLM applications |
| [RAGAS](https://github.com/explodinggradients/ragas) | ![stars](https://img.shields.io/github/stars/explodinggradients/ragas?style=flat-square) | rag, evaluation, metrics | Evaluation framework for RAG pipelines |
| [UpTrain](https://github.com/uptrain-ai/uptrain) | ![stars](https://img.shields.io/github/stars/uptrain-ai/uptrain?style=flat-square) | evaluation, monitoring, reliability | Open-source LLM evaluation and monitoring platform |

#### Production Observability

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [LangSmith](https://smith.langchain.com/) | — | tracing, debugging, production | LangChain's production monitoring and debugging platform |
| [Langfuse](https://github.com/langfuse/langfuse) | ![stars](https://img.shields.io/github/stars/langfuse/langfuse?style=flat-square) | tracing, sessions, production | Open-source LLM observability with session-level tracing |
| [Arize Phoenix](https://github.com/Arize-ai/phoenix) | ![stars](https://img.shields.io/github/stars/Arize-ai/phoenix?style=flat-square) | observability, evals, tracing | Open-source AI observability and evaluation platform |
| [Weights & Biases Weave](https://github.com/wandb/weave) | ![stars](https://img.shields.io/github/stars/wandb/weave?style=flat-square) | tracing, evals, production | W&B toolkit for tracking and evaluating LLM applications |

#### Retry & Resilience Patterns

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [Tenacity](https://github.com/jd/tenacity) | ![stars](https://img.shields.io/github/stars/jd/tenacity?style=flat-square) | retry, resilience, python | Python retry library for transient failure handling |
| [Instructor](https://github.com/jxnl/instructor) | ![stars](https://img.shields.io/github/stars/jxnl/instructor?style=flat-square) | structured-output, validation, retry | Structured output extraction with validation and retry logic |
| [Outlines](https://github.com/outlines-dev/outlines) | ![stars](https://img.shields.io/github/stars/outlines-dev/outlines?style=flat-square) | structured-output, reliability, generation | Guaranteed structured text generation for reliable outputs |

#### Integration Reliability

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [Pydantic](https://github.com/pydantic/pydantic) | ![stars](https://img.shields.io/github/stars/pydantic/pydantic?style=flat-square) | validation, schema, integration | Data validation to guard against schema drift across integrations |
| [MCP (Model Context Protocol)](https://github.com/modelcontextprotocol/servers) | ![stars](https://img.shields.io/github/stars/modelcontextprotocol/servers?style=flat-square) | protocol, tools, integration | Standardized protocol reducing integration surface fragility |

---

### 4. Safety — Guardrails & Behavior

Agent's inherent behavioral properties under uncertainty.

#### Guardrail Frameworks

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [Guardrails AI](https://github.com/guardrails-ai/guardrails) | ![stars](https://img.shields.io/github/stars/guardrails-ai/guardrails?style=flat-square) | guardrails, validation, safety | Framework for structured output and behavioral guardrails |
| [NeMo Guardrails](https://github.com/NVIDIA/NeMo-Guardrails) | ![stars](https://img.shields.io/github/stars/NVIDIA/NeMo-Guardrails?style=flat-square) | guardrails, dialogue, safety | NVIDIA's toolkit for adding safety rails to LLM applications |
| [LlamaGuard](https://github.com/meta-llama/PurpleLlama/tree/main/Llama-Guard3) | — | safety, classification, content | Meta's safety classifier for detecting policy violations |
| [Rebuff](https://github.com/protectai/rebuff) | ![stars](https://img.shields.io/github/stars/protectai/rebuff?style=flat-square) | prompt-injection, safety, defense | Self-hardening prompt injection detector |

#### Safety Standards & Research

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [Anthropic's Model Spec](https://anthropic.com/claude/model-spec) | — | safety, alignment, principles | Claude's character, values and decision-making framework |
| [Anthropic's RSP](https://anthropic.com/rsp) | — | safety, policy, responsible-scaling | Responsible Scaling Policy with safety thresholds |
| [METR Safety Evals](https://metr.org/) | — | safety, autonomy, evaluation | Research on catastrophic risk from advanced AI systems |
| [NIST AI RMF](https://airc.nist.gov/RMF_Overview) | — | safety, risk, governance | NIST AI Risk Management Framework for trustworthy AI |
| [AI Safety Fundamentals](https://course.aisafetyfundamentals.com/) | — | safety, education, fundamentals | Structured curriculum on AI safety concepts |

#### Behavioral Testing

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [Giskard](https://github.com/Giskard-AI/giskard) | ![stars](https://img.shields.io/github/stars/Giskard-AI/giskard?style=flat-square) | testing, safety, red-teaming | Open-source testing framework for LLM safety vulnerabilities |
| [PyRIT](https://github.com/Azure/PyRIT) | ![stars](https://img.shields.io/github/stars/Azure/PyRIT?style=flat-square) | red-teaming, safety, automation | Microsoft's Python Risk Identification Toolkit for red-teaming |
| [HarmBench](https://github.com/centerforaisafety/HarmBench) | ![stars](https://img.shields.io/github/stars/centerforaisafety/HarmBench?style=flat-square) | benchmark, safety, harm | Standardized evaluation of automated red-teaming methods |

#### Prompt Injection Defense

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [Lakera Guard](https://github.com/lakeraai/pint-benchmark) | — | prompt-injection, benchmark, defense | Prompt injection and jailbreak benchmark for safety testing |
| [Vigil](https://github.com/deadbits/vigil-llm) | ![stars](https://img.shields.io/github/stars/deadbits/vigil-llm?style=flat-square) | prompt-injection, scanner, safety | LLM prompt injection and jailbreak detection scanner |

---

### 5. Controllability — Permissions, Sandboxing & Audit

Operator's external leverage over agent behavior, blast radius, and kill switches.

#### Execution Sandboxes

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [E2B](https://github.com/e2b-dev/e2b) | ![stars](https://img.shields.io/github/stars/e2b-dev/e2b?style=flat-square) | sandbox, code-execution, isolation | Secure cloud sandboxes for AI code execution |
| [Daytona](https://github.com/daytonaio/daytona) | ![stars](https://img.shields.io/github/stars/daytonaio/daytona?style=flat-square) | sandbox, devcontainer, isolation | Secure development environment manager for agent execution |
| [Modal](https://github.com/modal-labs/modal-client) | ![stars](https://img.shields.io/github/stars/modal-labs/modal-client?style=flat-square) | sandbox, serverless, isolation | Serverless cloud with strong isolation for AI workloads |
| [Firecracker](https://github.com/firecracker-microvm/firecracker) | ![stars](https://img.shields.io/github/stars/firecracker-microvm/firecracker?style=flat-square) | sandbox, microvm, isolation | AWS's lightweight microVM for secure workload isolation |
| [gVisor](https://github.com/google/gvisor) | ![stars](https://img.shields.io/github/stars/google/gvisor?style=flat-square) | sandbox, container, kernel | Google's container sandbox providing kernel-level isolation |

#### Permissions & Policy Engines

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [Open Policy Agent](https://github.com/open-policy-agent/opa) | ![stars](https://img.shields.io/github/stars/open-policy-agent/opa?style=flat-square) | policy, authorization, rego | Unified policy enforcement engine for access control |
| [Cedar](https://github.com/cedar-policy/cedar) | ![stars](https://img.shields.io/github/stars/cedar-policy/cedar?style=flat-square) | policy, authorization, aws | Amazon's policy language and engine for fine-grained permissions |
| [Cerbos](https://github.com/cerbos/cerbos) | ![stars](https://img.shields.io/github/stars/cerbos/cerbos?style=flat-square) | authorization, policy, rbac | Open-source authorization service with role-based policies |

#### Audit & Observability

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [OpenTelemetry](https://github.com/open-telemetry/opentelemetry-python) | ![stars](https://img.shields.io/github/stars/open-telemetry/opentelemetry-python?style=flat-square) | audit, tracing, observability | Vendor-neutral observability framework for distributed traces |
| [Vector](https://github.com/vectordotdev/vector) | ![stars](https://img.shields.io/github/stars/vectordotdev/vector?style=flat-square) | logging, audit, pipeline | High-performance observability data pipeline for audit logs |
| [Falco](https://github.com/falcosecurity/falco) | ![stars](https://img.shields.io/github/stars/falcosecurity/falco?style=flat-square) | security, runtime, audit | Runtime security monitoring for detecting anomalous behavior |

#### Human-in-the-Loop Patterns

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [Temporal](https://github.com/temporalio/temporal) | ![stars](https://img.shields.io/github/stars/temporalio/temporal?style=flat-square) | workflow, hitl, durability | Durable workflow engine with human approval step support |
| [Prefect](https://github.com/PrefectHQ/prefect) | ![stars](https://img.shields.io/github/stars/PrefectHQ/prefect?style=flat-square) | workflow, hitl, orchestration | Workflow orchestration with manual approval and pause capabilities |

#### Agent Frameworks with Built-in Controls

| Resource | Stars | Tags | Description |
|----------|-------|------|-------------|
| [LangGraph](https://github.com/langchain-ai/langgraph) | ![stars](https://img.shields.io/github/stars/langchain-ai/langgraph?style=flat-square) | orchestration, hitl, state | Graph-based agent framework with checkpointing and interrupts |
| [CrewAI](https://github.com/crewAIInc/crewAI) | ![stars](https://img.shields.io/github/stars/crewAIInc/crewAI?style=flat-square) | orchestration, roles, permissions | Multi-agent framework with role-based access and guardrails |

---

### 6. Framework Resources & Templates

| Resource | Description |
|----------|-------------|
| [`framework/scorecard.md`](framework/scorecard.md) | Five-factor evaluation scorecard with scoring rubric |
| [`framework/use-case-weights.md`](framework/use-case-weights.md) | Context-dependent factor weighting guide by use case type |
| [`templates/evaluation-worksheet.md`](templates/evaluation-worksheet.md) | Practitioner worksheet for scoring a specific deployment |
| [`templates/deployment-checklist.md`](templates/deployment-checklist.md) | Pre-deployment checklist covering all five factors |
| [`data/benchmarks.yaml`](data/benchmarks.yaml) | Structured benchmark data cited in the article series |

---

## Key Metrics Referenced in the Series

| Metric | Source | Value | Notes |
|--------|--------|-------|-------|
| Capability ceiling (GDPval) | Anthropic | 47.6% → ~83% | wins-or-ties vs. expert humans, Sept 2025 → mid-2026 |
| Productivity gain with HITL | METR Survey | 1.4×–2× | median change in work value |
| Autonomous task completion | Remote Labor Index | 2.5% | at acceptable quality, best agents |
| Task horizon at 50% reliability | METR | ~14.5 hours | maximum economically viable task length |
| Task horizon at 80% reliability | METR | ~1 hour | drops sharply with higher reliability bar |
| Control reversion rate | Agent Arena | 2.3× | users pull control back vs. hand over more |
| Canceled agentic AI projects | Gartner | >40% | projected cancellation by end of 2027 |

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on adding resources, updating benchmarks, or proposing structural changes.

---

## License

[MIT](LICENSE)
