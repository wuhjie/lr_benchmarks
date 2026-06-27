# LR_BENCHMARKS

## Overview

This repository collects and compares existing benchmarks related to literature
retrieval, scholarly paper search, paper-set discovery, and research-agent evaluation.
It is intended as a benchmark landscape repository. The goal is to make nearby
evaluation settings easier to compare, especially in terms of task formulation,
input/output format, domain coverage, and evaluation style.

This repository does not propose a new benchmark. It records what has been surveyed,
how these benchmarks differ in task formulation and evaluation style, and where they
sit relative to one another in the literature-search landscape.

## Repository Structure

```text
LR_BENCHMARKS/
├── autoresearch/         # AutoResearchBench (fetched snapshot)
├── litsearch-dataset/    # LitSearch (fetched snapshot)
├── pasa-dataset/         # PaSa (fetched snapshot)
├── scholarquest/         # ScholarQuest (fetched snapshot)
├── benchmark_taxonomy.md     # consolidated categorisation of the four benchmarks
└── benchmark_comparison.md   # detailed per-benchmark comparison + landscape survey
```

Each benchmark folder contains a fetched copy of the corresponding upstream
repository or dataset, kept close to its upstream version.

## Included Benchmarks

| Benchmark | Main focus | Typical input | Typical output |
| --- | --- | --- | --- |
| **AutoResearchBench** | Autonomous research-agent evaluation | Research question / condition | Target paper (Deep) or paper set (Wide) |
| **LitSearch** | Query-to-paper retrieval | Natural-language query | Ranked papers / gold paper IDs |
| **PaSa** | Comprehensive academic paper search | Scholarly search query | Set of relevant papers |
| **ScholarQuest** | Paper-search agent / set retrieval | Paper-search query | Set of relevant arXiv IDs |

## Comparison Documents

- [`benchmark_taxonomy.md`](benchmark_taxonomy.md) — a single consolidated table that
  categorises the four benchmarks by task formulation, input/output format, corpus,
  evaluation style, and domain coverage, with supporting notes.
- [`benchmark_comparison.md`](benchmark_comparison.md) — detailed per-benchmark
  comparison, plus a broader landscape survey of adjacent benchmarks, datasets, and
  systems.

## Main Takeaway

The included benchmarks are adjacent but not equivalent. They span a spectrum from
clean query-to-paper retrieval (LitSearch), through recall-oriented scholarly and
agentic search (PaSa, ScholarQuest), to autonomous multi-step research
(AutoResearchBench). Domain coverage is concentrated in CS/ML/NLP and is arXiv-heavy.
One task setting they do not directly cover is seed-conditioned literature expansion —
growing a known set of papers from a topic, seed papers, and an existing corpus — which
would require adaptation rather than direct reuse of any single benchmark.

## Note on Snapshots

The upstream benchmark folders (`autoresearch/`, `litsearch-dataset/`,
`pasa-dataset/`, `scholarquest/`) are point-in-time snapshots of their upstream
sources. They are not modified here and may differ from the current upstream
versions.
