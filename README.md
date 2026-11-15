# Realized Value: an evaluation framework for agentic AI

Companion repository to the **[Realized Value](https://sunilsivadas.github.io/realized-value.html)** article series by Sunil Sivadas: *A Framework for Evaluating Agentic AI in the Enterprise*.

The articles make the argument and carry the evidence. This repository holds the working parts: the scorecard, the cost model, the contract clauses, the build sequence, worksheets you can fill in, and the key figures as data.

Aligned with the series as published on 15 November 2026. See [CHANGELOG.md](CHANGELOG.md).

---

## The framework

```
realized value = capability × cost × reliability × safety × controllability
```

Capability is the only factor that creates value. The other four discount it. The factors multiply, so the one nearest zero sets the outcome. That factor is the binding constraint.

This is a mental model. Only cost has a clean unit, the dollar. The series gives each of the other factors a unit and a test, so a team can find its weakest factor and spend there.

| Factor | What it is | Unit | Usual gatekeeper |
|--------|------------|------|------------------|
| **Capability** | The ceiling: what the system can do under generous conditions | Score on a relevant, unsaturated benchmark or your own eval, with no reliability threshold | Product and engineering |
| **Cost** | What each success costs | Cost per successful task | Finance |
| **Reliability** | Getting it right every time | pass^k, with the hand-back and silent-failure rates | Product and engineering |
| **Safety** | The agent's own behaviour when it is unsure | Severity-weighted unsafe-action rate, at its intervention rate | Risk and compliance |
| **Controllability** | What the operator can do when the agent is wrong | Bounded share, bound-leak rate, time-to-halt, gate load | CISO |

The five factors price the agent per task. The organisation around the agent decides how much of that becomes a return: the volume routed to the agent, the work redesigned around it, and what people do with the time freed, after fixed costs. Governance sets the bar for each factor and checks the evidence.

---

## The article series

| Part | Title | What it gives you | Reading time | Detail |
|------|-------|-------------------|--------------|--------|
| [Introduction](https://sunilsivadas.github.io/realized-value.html) | Realized Value: A Framework for Evaluating Agentic AI in the Enterprise | The framework, and how the five factors multiply | ~15 min | |
| [Part 1](https://sunilsivadas.github.io/capability.html) | Capability is a system property | Seven layers where capability comes from, and five attributes that set the weights | ~25 min | [Reference](https://sunilsivadas.github.io/capability-reference.html) |
| [Part 2](https://sunilsivadas.github.io/cost.html) | Cost engineering for agentic AI | Cost per successful task, and eighteen levers | ~25 min | [Reference](https://sunilsivadas.github.io/cost-levers.html) |
| [Part 3](https://sunilsivadas.github.io/reliability.html) | Reliability is getting it right every time | pass^k, three outcomes per run, and twelve levers | ~25 min | [Reference](https://sunilsivadas.github.io/reliability-reference.html) |
| [Part 4](https://sunilsivadas.github.io/safety.html) | Safety is how an agent behaves when it is unsure | Five dimensions, risk tiers per action, and twelve levers | ~25 min | [Reference](https://sunilsivadas.github.io/safety-reference.html) |
| [Part 5](https://sunilsivadas.github.io/controllability.html) | Controllability is what you can do when the agent is wrong | Six tests, four numbers, twelve levers, and the three-clause contract | ~25 min | [Reference](https://sunilsivadas.github.io/controllability-reference.html) |
| [Part 6](https://sunilsivadas.github.io/roi.html) | From framework to ROI | The cost model, a worked case, one build sequence and one scorecard | ~20 min | |

All seven are published. Parts 1 to 5 each make their argument in about 25 minutes, and a linked reference page holds the lever-by-lever detail and sources. The series is a living document and is updated with each major model release. Each article carries its own change log.

---

## How to use this repository

| If you want to | Start here |
|----------------|------------|
| Work out which factor binds for your use case | [`framework/use-case-weights.md`](framework/use-case-weights.md) |
| Put a price on each factor | [`framework/cost-model.md`](framework/cost-model.md) |
| Report one sheet to engineering, finance and risk | [`framework/scorecard.md`](framework/scorecard.md) |
| Buy an agent, or write terms for one | [`framework/contract.md`](framework/contract.md) |
| Evaluate a specific deployment | [`templates/evaluation-worksheet.md`](templates/evaluation-worksheet.md) |
| Plan the build | [`templates/deployment-checklist.md`](templates/deployment-checklist.md) |
| Go deeper on one factor | [`factors/`](factors/) |
| Reuse the figures | [`data/benchmarks.yaml`](data/benchmarks.yaml) |

A short path for a first pass:

1. Rate the use case on stakes, autonomy, reversibility, integration complexity and verifiability.
2. Measure the factor nearest zero on your own tasks.
3. Spend there.
4. Check the organisation: volume, redesign, redeployment, fixed costs, and a named owner per factor.
5. Re-run on every change of model, harness or tool. The binding constraint moves.

---

## Key figures in the series

As published on 15 November 2026. Every figure carries its evidence type, because the series treats a vendor's number and a peer-reviewed number differently. The same figures, with dates and source links, are in [`data/benchmarks.yaml`](data/benchmarks.yaml).

### The gap

| Figure | Value | Source | Evidence |
|--------|-------|--------|----------|
| GDPval, wins or ties against experts | 47.6% at launch (Claude Opus 4.1, Sep 2025); 84.9% (GPT-5.5, Apr 2026) | [Patwardhan et al.](https://arxiv.org/abs/2510.04374); [OpenAI](https://openai.com/index/introducing-gpt-5-5/) | Preprint; vendor-reported |
| Remote Labor Index, projects finished with no person in the loop | 2.5% (Oct 2025); 21.25% (Claude Opus 5.5, Oct 2026); 41.3% (Claude Fable 5.2, Nov 2026) | [Scale AI and CAIS](https://arxiv.org/abs/2510.26787); [Scale leaderboard](https://labs.scale.com/leaderboard/rli); [Anthropic system card](https://assets.claude.com/27d60918d218125e7504bc7354c4b4626ec56b11.pdf) | Preprint; independent leaderboard; run by Scale AI, vendor-reported |
| Epoch Capabilities Index, best score | 122 (GPT-4) to 173 (Claude Fable 5.2) in 44 months | [Epoch AI](https://epoch.ai/eci) | Independent |
| Change in the value of work, with a person in the loop | 1.4 to 2× (median, 349 technical workers) | [METR survey, May 2026](https://metr.org/blog/2026-05-11-ai-usage-survey/) | Self-reported |
| CIOs reporting significant or transformational value from AI | 13% of 2,002 | [Gartner, Oct 2026](https://www.gartner.com/en/newsroom/press-releases/2026-10-19-gartner-survey-finds-only-13-percent-of-cios-say-their-enterprise-has-realized-significant-or-transformational-value-from-ai) | Analyst survey |
| Agentic AI projects expected to be cancelled by end of 2027 | Over 40% | [Gartner, Jun 2025](https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027) | Analyst forecast |

### One figure per factor

| Factor | Figure | Value | Source | Evidence |
|--------|--------|-------|--------|----------|
| Capability | Task horizon of one model at two reliability bars (Claude Opus 4.6) | About 12 hours at 50%; about 70 minutes at 80% | [METR](https://metr.org/time-horizons/) | Independent; tracker no longer updated since Sep 2026 |
| Cost | Cost per solved task on Terminal-Bench 4.0, among models above 55% | About $3 to about $31, a spread of about 10× | [Vals AI, 11 Nov 2026](https://www.vals.ai/benchmarks/terminal-bench-4) | Independent |
| Cost | Model pairs where the cheaper list price has the higher total cost | 32%, by up to 28× | [Chen et al.](https://arxiv.org/abs/2603.23971) | Preprint |
| Reliability | APEX-Agents, best agent: single try against all eight tries | 24% against 13.4% | [Mercor](https://arxiv.org/abs/2601.14242) | Vendor-built benchmark |
| Reliability | OSWorld 2.1, Claude Fable 5.2: partial credit against strict pass | 89.3% against 54.6% | [Anthropic system card](https://assets.claude.com/27d60918d218125e7504bc7354c4b4626ec56b11.pdf) | Vendor-reported |
| Safety | Unsanctioned attacks across three OpenAI generations, in simulations | 0% to 29.2% | [UK AISI](https://www.aisi.gov.uk/blog/gpt-6-astra-performs-unsanctioned-supply-chain-attacks-in-simulations) | Government |
| Safety | False success reports after a tool fails, without and with an evidence contract | 22.8% to 0.8% | [FTA](https://arxiv.org/abs/2609.35732) | Preprint |
| Controllability | OpenAI's September 2026 incident: time to alert, and time to stop | 11 min 48 s; 2 h 44 min | [OpenAI](https://alignment.openai.com/misalignment-reports/an-agent-used-dns-to-reach-an-external-chatbot/) | Vendor-reported |
| Controllability | Injection defences that fell to adaptive attacks | 12 of 12, most at over 90% success | [Nasr et al.](https://www.usenix.org/system/files/usenixsecurity26-nasr.pdf) | Peer-reviewed |

### The worked case (Part 6)

| Figure | Value | Source | Evidence |
|--------|-------|--------|----------|
| Human cost per live contact | $8.01 | [Gartner, Sep 2019](https://www.gartner.com/en/newsroom/press-releases/2019-09-25-gartner-says-only-9--of-customers-report-solving-thei) | Reported; seven years old |
| Agent price | $0.99 per resolution | [Fin](https://www.intercom.com/help/en/articles/8205718-fin-resolutions) | Published list price, checked 1 Nov 2026 |
| Resolution rate | 76% vendor average; 50.8% in one deployment | [Fin, Mar 2026](https://fin.ai/learn/roi-ai-customer-service-agents-benchmarks) | Vendor-reported |
| Saving per conversation, with no silent failures | $5.34 at 76%; $3.57 at 50.8% | Computed in Part 6 | Arithmetic on the inputs above |
| Silent-failure rate that erases the saving, at US$600 a failure | 0.9% at 76%; 0.6% at 50.8% | Computed in Part 6; [Moffatt v. Air Canada](https://decisions.civilresolutionbc.ca/crt/crtd/en/525448/1/document.do) | Arithmetic; tribunal decision |
| Silent-failure rate in the public record | Unreported | No source found | Missing |

---

## Sources by factor

Benchmarks, tools and standards the series cites. Every link was checked on 14 November 2026. The articles carry the full reference lists.

### Capability

| Source | What it is | Evidence |
|--------|------------|----------|
| [GDPval](https://arxiv.org/abs/2510.04374) | 1,320 real deliverables across 44 occupations, judged blind against experts | Preprint (OpenAI) |
| [GDPval-AA](https://artificialanalysis.ai/evaluations/gdpval-aa) | The same target, run through a standard open harness | Independent |
| [Remote Labor Index](https://arxiv.org/abs/2510.26787) and its [leaderboard](https://labs.scale.com/leaderboard/rli) | 240 paid freelance projects, finished with no person in the loop | Preprint; independent leaderboard |
| [Epoch Capabilities Index](https://epoch.ai/eci) and its [public repository](https://github.com/epoch-research/eci-public) | Composite scale stitching 40+ benchmarks | Independent |
| [METR time horizons](https://metr.org/time-horizons/) | Task length at a stated reliability threshold | Independent; no longer updated |
| [Agents' Last Exam](https://snorkel.ai/blog/agents-last-exam-reading-group/) | 1,500 professional workflows across 55 fields, graded by code where possible | Preprint |
| [Terminal-Bench 4.0](https://www.tbench.ai/news/terminal-bench-4-0) | 66 long agentic tasks in a terminal | Independent; rated "Flawed" by Epoch AI |
| [SWE-bench Pro](https://labs.scale.com/leaderboard/swe_bench_pro_public) | Real GitHub issues in larger codebases. State which measurement condition you quote | Independent leaderboard |
| [SWE-bench Live](https://swe-bench-live.github.io/) | The same target, on issues never seen in training | Independent |
| [HAL](https://arxiv.org/pdf/2510.11977) | Cost-aware agent evaluation across nine benchmarks | Peer-reviewed (ICLR 2026) |
| [BFCL v4](https://gorilla.cs.berkeley.edu/blogs/17_bfcl_v4_prompt_variation.html) | Function calling, web search, memory, multi-turn | Independent |
| [MTEB](https://huggingface.co/spaces/mteb/leaderboard) | Retrieval and embedding capability | Independent leaderboard |
| [OSWorld 2.0](https://arxiv.org/abs/2606.29537) and its [repository](https://github.com/xlang-ai/OSWorld-V2) | 108 long workflows across desktop applications | Preprint |

### Cost

| Source | What it is | Evidence |
|--------|------------|----------|
| [Vals AI, Terminal-Bench 4.0](https://www.vals.ai/benchmarks/terminal-bench-4) | Every model in the same minimal harness, with cost per test | Independent |
| [LLM Frontier](https://llm-frontier.catalystneuro.com/) and its [repository](https://github.com/catalystneuro/llm-frontier) | The cheapest way to reach each level of the Artificial Analysis Intelligence Index | Independent |
| [Artificial Analysis Intelligence Index v5](https://artificialanalysis.ai/articles/artificial-analysis-intelligence-index-v5) | Composite index with measured cost per task | Independent |
| [Price reversal in reasoning models](https://arxiv.org/abs/2603.23971) | List price against total cost, eight models, twelve tasks | Preprint |
| [RouteLLM](https://arxiv.org/abs/2406.18665) | Model routing: 95% of GPT-4 quality at 26% strong-model calls | Peer-reviewed (ICLR 2025) |
| [FrugalGPT](https://arxiv.org/abs/2305.05176) | Cascades and confidence gating | Peer-reviewed (TMLR) |
| [AgentDiet](https://arxiv.org/abs/2509.23586) | Trajectory reduction for agents | Peer-reviewed (FSE 2026) |
| [LLMLingua](https://github.com/microsoft/LLMLingua) | Prompt compression | Peer-reviewed (EMNLP 2023) |
| [Mini-SWE-Agent](https://github.com/SWE-agent/mini-swe-agent) | A minimal harness, used as the baseline in harness comparisons | Open source |
| [Anthropic, Building effective agents](https://www.anthropic.com/research/building-effective-agents) | Workflow or agent | Provider guidance |
| [Anthropic, Contextual Retrieval](https://www.anthropic.com/news/contextual-retrieval) | Retrieval engineering | Provider, self-reported |

### Reliability

| Source | What it is | Evidence |
|--------|------------|----------|
| [τ-bench](https://arxiv.org/abs/2406.12045) and [τ²-bench](https://github.com/sierra-research/tau2-bench) | Agents serving simulated users under a written policy, graded on the final database state, with pass^k built in | Preprint |
| [APEX-Agents](https://arxiv.org/abs/2601.14242) and [APEX-Agents 1.1](https://www.mercor.com/blog/introducing-apex-agents-1-1/) | Banking, consulting and legal work, with pass@k and pass^k | Vendor-built |
| [HAL Reliability Dashboard](https://hal.cs.princeton.edu/reliability/) and [hal-harness](https://github.com/princeton-pli/hal-harness) | Twelve reliability metrics, with paraphrase and injected faults | Peer-reviewed (ICML 2026) |
| [Inspect](https://inspect.aisi.org.uk/) and its [repository](https://github.com/UKGovernmentBEIS/inspect_ai) | Evaluation framework with a built-in pass^k reducer | Government (UK AISI) |
| [Husain and Shankar, evals FAQ](https://hamel.dev/blog/posts/evals-faq/) | How to build a golden set from real traces | Practitioner guidance |
| [IMDA starter kit for testing agentic systems](https://www.imda.gov.sg/assets/603572eb-724a-46cf-ac12-14fe38e1558c.pdf) | Repeated runs, worst run, trajectory capture | Government (Singapore) |
| [Anthropic, Demystifying evals for AI agents](https://anthropic.com/engineering/demystifying-evals-for-ai-agents) | Grader design for agents | Provider guidance |
| [OpenTelemetry GenAI semantic conventions](https://github.com/open-telemetry/semantic-conventions/releases/tag/v1.42.0) | Agent and tool spans for traces | Open standard |

### Safety

| Source | What it is | Evidence |
|--------|------------|----------|
| [UK AISI on GPT-6 Astra](https://www.aisi.gov.uk/blog/gpt-6-astra-performs-unsanctioned-supply-chain-attacks-in-simulations) | Unsanctioned attacks in simulated environments | Government |
| [OpenAgentSafety](https://arxiv.org/abs/2507.06134) | 356 tasks with real tools, graded on the final environment state | Peer-reviewed (ICLR 2026) |
| [ToolEmu](https://arxiv.org/abs/2309.15817) | Risky tool use in an LLM-emulated sandbox | Peer-reviewed (ICLR 2024) |
| [OS-Harm](https://arxiv.org/abs/2506.14866) | 150 computer-use tasks | Peer-reviewed (NeurIPS 2025) |
| [Agent-SafetyBench](https://arxiv.org/abs/2412.14470) | 2,000 cases in 349 environments | Preprint |
| [SHADE-Arena](https://arxiv.org/abs/2506.15740) | A hidden harmful side task, and monitors that try to catch it | Preprint |
| [MASK](https://arxiv.org/abs/2503.03750) | Whether a model contradicts its own beliefs under pressure | Preprint |
| [FTA](https://arxiv.org/abs/2609.35732), [OverclaimBench](https://arxiv.org/abs/2609.20812), [CAPE-Bench](https://arxiv.org/abs/2610.17301), [AgentDecept](https://arxiv.org/abs/2610.39377) | Whether the agent's report matches what it did | Preprints |
| [Petri](https://alignment.anthropic.com/2025/petri) | Open-source auditing tool built on Inspect | Provider |
| [Project Moonshot](https://aiverifyfoundation.sg/project-moonshot/) | Benchmarking and red-teaming toolkit for LLM applications | Government-backed (Singapore) |
| [NIST AI RMF 1.0](https://www.nist.gov/itl/ai-risk-management-framework) and [Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) | Govern, Map, Measure, Manage | Standard |
| [EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) | Articles 9, 12, 14 and 15 for high-risk systems | Regulation |
| [IMDA Model AI Governance Framework for Agentic AI v1.5](https://www.imda.gov.sg/-/media/imda/files/about/emerging-tech-and-research/artificial-intelligence/mgf-for-agentic-ai.pdf) | Governance framework for agents | Government (Singapore) |

### Controllability

| Source | What it is | Evidence |
|--------|------------|----------|
| [OpenAI, An agent used DNS to reach an external chatbot](https://alignment.openai.com/misalignment-reports/an-agent-used-dns-to-reach-an-external-chatbot/) | Incident report with a halt timeline | Vendor-reported |
| [The Attacker Moves Second](https://www.usenix.org/system/files/usenixsecurity26-nasr.pdf) | Twelve injection defences against adaptive attacks | Peer-reviewed (USENIX Security 2026) |
| [CaMeL](https://arxiv.org/abs/2503.18813) | A design that keeps the plan apart from untrusted data: 0 of 949 attacks succeeded | Preprint |
| [The lethal trifecta](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/) | Private data, untrusted content and an outside channel | Practitioner analysis |
| [OWASP Top 10 for Agentic Applications](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) | Ten security risks, ASI01 to ASI10 | Industry standard |
| [MAS Guidelines on AI Risk Management](https://www.mas.gov.sg/regulation/guidelines/guidelines-on-artificial-intelligence-risk-management-for-financial-institutions) | Inventory, least privilege, kill switches tested regularly | Regulator (Singapore) |
| [Anthropic, Claude Code auto mode](https://www.anthropic.com/engineering/claude-code-auto-mode) | Permission prompts and approval rates | Vendor-reported |
| [Breaking Claude Code with Opus 5 and auto mode](https://embracethered.com/blog/posts/2026/breaking-claude-code-opus-5-and-automode/) | An attacker who has read the defence | Independent researcher |
| [Anthropic system card, Claude Fable 5.2 and Claude Mythos 5.2](https://assets.claude.com/27d60918d218125e7504bc7354c4b4626ec56b11.pdf) | Safeguard tests, fallback route, external red team | Vendor-reported |

### The business case

| Source | What it is | Evidence |
|--------|------------|----------|
| [Klarna Q3 2025 investor presentation](https://www.sec.gov/Archives/edgar/data/2003292/000162828025052805/exhibit992klarnapresenta.htm) | The longest public record of a customer service agent | Company-reported |
| [Fin resolutions](https://www.intercom.com/help/en/articles/8205718-fin-resolutions) | Price per resolution, and what counts as resolved | Published definition |
| [Moffatt v. Air Canada, 2024 BCCRT 149](https://decisions.civilresolutionbc.ca/crt/crtd/en/525448/1/document.do) | What one wrong answer cost | Tribunal decision |
| [STABL, The missing quadrant](https://stablai.substack.com/p/the-missing-quadrant-in-responses) | Automation, augmentation and organisational change | Researcher analysis |

---

## Honest limits

- The formula is a diagnostic. It finds the binding constraint. It does not produce a single score, and this repository no longer asks for one.
- Only cost aggregates cleanly. Safety and controllability resist that arithmetic.
- The factors trade off. Cutting cost can cost capability. Tighter controls can cost latency.
- The newest evidence is mostly vendor-run, and the newest models increasingly recognise when they are being tested. Treat lab safety numbers as a best case.
- Figures date quickly. Check the article change logs before quoting a number from here.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)
