# Literature Retrieval Landscape
<!-- literature-retrieval-landscape -->

## Overview

This repository surveys benchmarks, datasets, and systems related to literature
retrieval, scholarly paper search, paper-set discovery, Boolean query generation,
systematic-review automation, and research-agent evaluation.

The goal is not to propose a new benchmark or to rank existing systems. Instead, this
repository organises nearby evaluation settings so they can be compared by:

- task formulation
- input and output format
- corpus or search index
- domain coverage
- supervision / annotation style
- evaluation metrics
- whether the task evaluates retrieval, screening, synthesis, or agentic search

The repository includes four fetched benchmark snapshots as concrete reference points.
The surrounding documentation provides a broader landscape survey that also covers
Boolean query generation datasets, systematic-review retrieval benchmarks, scientific
QA benchmarks, and adjacent literature-review products.

## Repository Structure

```text
LR_BENCHMARKS/
├── benchmarks/                    # fetched benchmark snapshots
│   ├── autoresearch/              # AutoResearchBench fetched snapshot
│   ├── litsearch-dataset/         # LitSearch fetched snapshot
│   ├── pasa-dataset/              # PaSa fetched snapshot
│   └── scholarquest/              # ScholarQuest fetched snapshot
├── benchmark_taxonomy.md          # concise taxonomy of the four bundled benchmarks
└── benchmark_comparison.md        # detailed comparison + broader landscape survey
```

The fetched benchmark folders are kept close to their upstream versions. The added
value of this repository is the categorisation, comparison, and landscape mapping in
the markdown documents.

## What This Repository Covers

This repository covers three related but distinct areas.

### 1. Bundled literature-search benchmarks

The four fetched benchmark snapshots all involve finding scientific papers, but they
are not equivalent. They differ in task formulation, input/output format, corpus
assumptions, and evaluation style.

| Benchmark | Main focus | Typical input | Typical output |
| --- | --- | --- | --- |
| AutoResearchBench | Autonomous research-agent evaluation | Research question / condition | Target paper or paper set, often with a multi-step process |
| LitSearch | Query-to-paper retrieval | Natural-language query | Ranked papers / gold paper IDs |
| PaSa | Comprehensive academic paper search | Scholarly search query | Set of relevant papers |
| ScholarQuest | Paper-search agent / set retrieval | Paper-search query | Set of relevant arXiv IDs |

See [`benchmark_taxonomy.md`](benchmark_taxonomy.md) for a consolidated taxonomy of
these four benchmarks.

### 2. Broader benchmark and dataset landscape

Beyond the four bundled snapshots, this repository also records adjacent benchmarks
and datasets for:

- automated Boolean query generation
- systematic-review search and technology-assisted review
- seed-study-based literature retrieval
- active-learning screening
- scientific question answering
- citation graph / related-paper recommendation
- paper-search agent evaluation

Examples include CLEF TAR, Seed Collection, AutoBool-65K, SR4CS, Literature Search
Sandbox, ASReview/SYNERGY-style datasets, ScholarQABench, LitQA/PaperQA, and related
resources.

These resources are not bundled as folders in this repository. They are listed as
landscape references to clarify nearby evaluation settings and their task boundaries.

### 3. Adjacent systems and products

The repository also maps deployed tools and research systems that touch literature
search, paper discovery, screening, citation analysis, or synthesis.

Examples include Elicit, Consensus, Scite, ResearchRabbit, Litmaps, Connected Papers,
Semantic Scholar, OpenAlex, Rayyan, Covidence, ASReview, PaperQA, OpenScholar, and
other related tools.

These systems are included to document the surrounding ecosystem. They are not treated
as directly comparable benchmarks unless they provide a clear public evaluation setup.

## Comparison Documents

- [`benchmark_taxonomy.md`](benchmark_taxonomy.md) — provides a concise taxonomy of the
  four bundled benchmarks. It compares task type, input, output, corpus/index,
  evaluation style, and domain coverage. It also highlights the setting that none of the
  four directly covers: seed-conditioned literature expansion from a topic, seed papers,
  and an existing corpus.
- [`benchmark_comparison.md`](benchmark_comparison.md) — provides a more detailed
  per-benchmark comparison of AutoResearchBench, LitSearch, PaSa, and ScholarQuest. It
  also includes a broader landscape survey of automated Boolean query generation,
  systematic-review datasets, scientific QA benchmarks, citation/recommendation
  resources, and related systems/products.

## Main Takeaway

Existing benchmarks and systems cover related but different parts of the literature
review pipeline.

Some benchmarks evaluate clean query-to-paper retrieval. Others focus on Boolean query
generation for systematic reviews, active-learning screening, citation graph expansion,
scientific QA, or broader agentic research workflows. Several strong resources are
concentrated in biomedical systematic reviews, CS/ML/NLP, or arXiv-heavy corpora.
Therefore, these benchmarks are useful reference points, but they should not be treated
as interchangeable.

A recurring uncovered setting is seed-conditioned literature expansion: starting from a
topic, seed papers, and possibly an existing corpus, then evaluating whether a system
can expand the set with relevant and diverse papers. None of the four bundled benchmarks
directly evaluates this setting without adaptation.

## Note on Snapshots

The upstream benchmark folders are point-in-time snapshots of their original
repositories or datasets. They are not modified here and may differ from the current
upstream versions. For the latest version of each benchmark, refer to the corresponding
upstream repository or project page.
