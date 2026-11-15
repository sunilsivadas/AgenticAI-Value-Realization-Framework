# Contributing

This repository is the companion to the [Realized Value](https://sunilsivadas.github.io/realized-value.html) article series. The articles are the source of truth. This repository follows them.

Corrections are welcome, and so are additions that meet the rules below.

## What belongs here

- The working parts of the framework: the scorecard, the cost model, the contract clauses, the build sequence and the worksheets.
- Key figures the series cites, with their sources.
- Benchmarks, tools and standards the series cites.

## What does not belong

- Sources the series does not cite. Propose them for the series first, by opening an issue.
- A tool or repository you have not opened and checked.
- Figures with no dated primary source.
- General LLM tutorials.

## Rules for every figure

1. **Link the primary source.** A paper, a leaderboard, a filing, a decision. A news summary is acceptable only when the primary source is not public, and then say so.
2. **Date it.** The date the measurement was taken or published.
3. **Label the evidence.** Use one of the labels in [`data/benchmarks.yaml`](data/benchmarks.yaml): peer-reviewed, government, independent, preprint, vendor-reported, self-reported, analyst, legal or computed.
4. **Quote the metric as defined.** State the model, the benchmark version and the measurement condition. Benchmark scores are not comparable across releases.
5. **Match the article.** A figure here must agree with the series. If you think the series is wrong, open an issue with the source.

## Rules for every link

- Open it. Check that it loads and that it is what the entry says it is.
- For a GitHub repository, check the owner. Link the official organisation, never a fork or a look-alike.
- Do not add a link you cannot verify.

## Style

The repository follows the series.

- Plain words. Short sentences.
- British spelling. The proper name "Realized Value" keeps its z.
- Say what the evidence shows, and how far it can be trusted. No superlatives.
- "Ceiling" means capability. "Binding constraint" means the factor nearest zero.

## How to propose a change

1. Fork the repository and create a branch.
2. Make the change in every file that carries the figure: `README.md`, the factor page, and `data/benchmarks.yaml`.
3. Add a line to [`CHANGELOG.md`](CHANGELOG.md).
4. Open a pull request, and link the primary source in the description.

## Reporting an error

Open an issue. Say which file and which figure, and link the source that contradicts it.
