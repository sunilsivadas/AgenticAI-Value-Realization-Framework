# Contributing

Contributions that improve the quality and coverage of this resource catalog are welcome.

## What Belongs Here

This repository catalogs tools, benchmarks, frameworks, papers, and datasets relevant to evaluating agentic AI deployments through the lens of the five-factor Realized Value framework:

- **Capability**: Benchmarks, evaluation harnesses, autonomy metrics
- **Cost**: Token tracking, cost optimization, pricing references
- **Reliability**: Testing frameworks, production observability, resilience patterns
- **Safety**: Guardrails, behavioral testing, safety standards
- **Controllability**: Sandboxes, permission engines, audit tooling, HITL patterns

## What Does Not Belong

- General LLM tutorials or introductory content
- Resources unrelated to enterprise deployment evaluation
- Commercial-only tools with no open documentation or pricing transparency
- Duplicate entries (check before adding)

## Adding a Resource

1. Fork the repository and create a branch.
2. Add your entry to the relevant table in `README.md` and the corresponding file under `factors/`.
3. Use the standard table row format:

```markdown
| [Project Name](https://github.com/owner/repo) | ![stars](https://img.shields.io/github/stars/owner/repo?style=flat-square) | tag1, tag2, tag3 | One-line description under 20 words. |
```

For non-GitHub resources (papers, standards, tools):

```markdown
| [Resource Name](https://url) | — | tag1, tag2 | One-line description under 20 words. |
```

4. Keep descriptions factual and neutral. No superlatives.
5. Tags should be lowercase, hyphen-separated, and drawn from the existing tag vocabulary where possible.
6. Open a pull request with a brief explanation of why the resource is relevant.

## Updating Benchmark Data

Benchmark figures in `data/benchmarks.yaml` and the metrics table in `README.md` should include:
- The source (paper, blog post, or dataset)
- The date the measurement was taken or published
- The exact metric definition (not a paraphrase)

Submit a PR with a link to the primary source.

## Updating Factor Deep-Dives

The `factors/` directory contains deeper writeups per factor. PRs that expand analysis, add nuance from the article series, or correct factual errors are welcome. Match the existing tone: precise, practitioner-focused, no marketing language.

## Code of Conduct

Be precise. Be honest about what resources do and don't do. Disagree constructively.
