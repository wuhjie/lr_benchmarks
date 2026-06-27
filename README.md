# LR_BENCHMARKS

## Overview

This repository surveys benchmarks, datasets, and systems related to literature
retrieval, scholarly paper search, paper-set discovery, Boolean query generation,
systematic-review automation, and research-agent evaluation.

The goal is not to propose a new benchmark or to rank existing systems. Instead, the
repository organises nearby evaluation settings so they can be compared by:

- task formulation
- input and output format
- corpus and domain coverage
- supervision / annotation style
- evaluation metrics
- whether the benchmark evaluates retrieval, screening, synthesis, or agentic search

The repository includes a small number of fetched benchmark snapshots, but its main
purpose is broader: to provide a structured landscape of existing evaluation resources
for literature search and paper discovery.

## Repository Structure

```text
LR_BENCHMARKS/
├── autoresearch/              # AutoResearchBench fetched snapshot
├── litsearch-dataset/         # LitSearch fetched snapshot
├── pasa-dataset/              # PaSa fetched snapshot
├── scholarquest/              # ScholarQuest fetched snapshot
├── benchmark_taxonomy.md      # taxonomy of included benchmark snapshots
├── benchmark_comparison.md    # detailed comparison of included benchmarks
├── boolean_query_generation.md # Boolean query generation methods and datasets
├── benchmark_landscape.md     # broader benchmark / dataset landscape
└── system_landscape.md        # adjacent systems, products, and evaluation styles
```

The fetched benchmark folders are kept close to their upstream versions. The added
value of this repository is the surrounding categorisation and comparison documents.

## What This Repository Covers

This repository covers three related but distinct areas.

### 1. Literature retrieval and paper-search benchmarks

These benchmarks evaluate whether a system can retrieve papers from a topic, query,
research question, or search intent.

Examples include:

| Benchmark | Main focus | Typical input | Typical output |
| --- | --- | --- | --- |
| AutoResearchBench | Autonomous research-agent evaluation | Research question / condition | Target paper or paper set |
| LitSearch | Query-to-paper retrieval | Natural-language query | Ranked papers / gold paper IDs |
| PaSa | Comprehensive academic paper search | Scholarly search query | Set of relevant papers |
| ScholarQuest | Paper-search agent / set retrieval | Paper-search query | Set of relevant arXiv IDs |

### 2. Boolean query generation and systematic-review search datasets

This line of work focuses on generating, refining, or evaluating search strategies,
especially Boolean queries for systematic reviews.

Examples include:

| Dataset / benchmark | Main focus |
| --- | --- |
| CLEF TAR 2017 / 2018 | Biomedical technology-assisted review and systematic-review retrieval |
| CLEF 2019 DTA / Intervention | Diagnostic-test and intervention review retrieval |
| Seed Collection | Seed-study-based systematic-review search |
| AutoBool-65K | Large-scale Boolean query generation |
| SR4CS | Systematic-review search in computer science |
| Literature Search Sandbox | Natural-language review description to Boolean search generation |

### 3. Adjacent literature-review systems and products

The repository also records nearby systems and products, such as academic search
engines, AI literature review assistants, citation graph tools, screening platforms,
and scientific QA systems. These systems are not all benchmarks, but they are useful
for understanding how evaluation differs across retrieval, screening, synthesis, and
workflow automation.

Examples include Elicit, Consensus, Scite, ResearchRabbit, Litmaps, Connected Papers,
Semantic Scholar, OpenAlex, Rayyan, Covidence, ASReview, PaperQA, OpenScholar, and
related tools.

## Comparison Documents

- [`benchmark_taxonomy.md`](benchmark_taxonomy.md) — categorises the fetched benchmark
  snapshots by task formulation, input/output format, corpus, evaluation style, and
  domain coverage.
- [`benchmark_comparison.md`](benchmark_comparison.md) — provides a detailed comparison
  of the included benchmark snapshots and discusses how they relate to broader
  paper-search and research-agent evaluation settings.
- [`boolean_query_generation.md`](boolean_query_generation.md) — summarises automated
  Boolean query generation and refinement methods, including the datasets and evaluation
  protocols used in prior work.
- [`benchmark_landscape.md`](benchmark_landscape.md) — summarises broader datasets and
  benchmarks for literature search, systematic-review retrieval, paper recommendation,
  screening, and scientific QA.
- [`system_landscape.md`](system_landscape.md) — summarises adjacent research systems,
  products, and startups, with emphasis on their task scope, main output, and public
  evaluation style.

## Main Takeaway

Existing benchmarks and systems cover related but different parts of the literature
review pipeline.

Some benchmarks evaluate clean query-to-paper retrieval. Others focus on Boolean query
generation for systematic reviews, active-learning screening, citation graph expansion,
or retrieval-augmented scientific QA. Many strong resources are concentrated in
biomedical systematic reviews, CS/ML/NLP, or arXiv-heavy corpora. As a result, these
benchmarks are useful for comparison, but they are not interchangeable.

A recurring gap is the lack of a broad, domain-diverse benchmark for literature search
expansion: starting from a topic, seed papers, or a partial corpus, and evaluating
whether a system can discover a comprehensive and diverse set of relevant papers.

## Note on Snapshots

The upstream benchmark folders are point-in-time snapshots of their original
repositories or datasets. They are not modified here and may differ from the current
upstream versions. For the latest version of each benchmark, please refer to the
corresponding upstream repository or project page.
