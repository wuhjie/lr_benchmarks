# Research Synthesis

## Purpose

This document synthesises the benchmark taxonomy and comparison in this repository into a
higher-level view of the literature-retrieval evaluation landscape. The goal is not to introduce
a new benchmark or to rank existing systems, but to clarify what current benchmarks and adjacent
systems actually evaluate, how their task formulations differ, and which evaluation setting
remains under-covered.

The main observation is that many resources are described broadly as literature search,
literature retrieval, academic discovery, or research-agent benchmarks, but they evaluate
substantially different tasks. Some focus on clean query-to-paper retrieval, some on
recall-oriented paper-set collection, some on Boolean query generation for systematic reviews,
some on screening after papers have already been retrieved, and some on scientific question
answering or broader research-agent workflows. These settings are related, but they are not
interchangeable.

## Task Landscape

Existing resources can be grouped into several broad task families.

### 1. Query-to-paper retrieval

This is the cleanest retrieval setting. A system receives a natural-language query and retrieves
or ranks papers from a fixed corpus. Evaluation is usually based on gold paper identifiers and
standard retrieval or ranking metrics.

LitSearch is the clearest example in this repository. It provides a controlled corpus and gold
paper IDs, making it useful for isolating retriever or reranker quality. However, this setting
mainly evaluates whether a system can retrieve papers for a given query. It does not evaluate
multi-step search behaviour, query refinement, corpus growth, or expansion from seed papers.

### 2. Recall-oriented scholarly paper search

A second family evaluates whether a system can collect a set of relevant papers for a scholarly
information need. The output is usually a paper set rather than a single ranked list, and the main
concern is coverage or recall.

PaSa and ScholarQuest are closer to this setting. They are more relevant to comprehensive
literature discovery than pure query-to-paper ranking because they focus on finding a broader
set of relevant papers. However, they still start primarily from a query or paper-search request.
They do not explicitly condition the task on a known seed set of papers plus an existing corpus
that should be expanded.

### 3. Paper-search agents and autonomous research agents

A third family evaluates agentic or multi-step search behaviour. These benchmarks care not only
about the final paper set, but also about the process by which a system searches, follows clues,
uses tools, and reaches a target.

AutoResearchBench is the most relevant benchmark in this direction among the bundled resources.
Its Deep and Wide settings foreground multi-step scientific literature discovery, making it
closer to research-agent evaluation than to standard retrieval evaluation. However, this also
makes it less suitable as a clean retrieval benchmark: it depends on live search backends and
focuses on broader task completion rather than a controlled seed-conditioned expansion setting.

### 4. Boolean query generation for systematic reviews

A large adjacent line of work studies automatic Boolean query generation or refinement,
especially for systematic reviews. These methods typically take a review topic, protocol,
objective, PICO-style description, or initial search strategy, and output a Boolean query or
refined search string. Evaluation often uses CLEF TAR, Seed Collection, AutoBool-style datasets,
or other systematic-review resources.

This direction is highly relevant to search-strategy generation. It provides useful ideas for
query formulation, refinement, recall--precision trade-offs, MeSH expansion, and retrieval-based
query optimisation. However, it is usually framed around systematic review retrieval, especially
in biomedical or health settings. It also often treats query generation as a direct task, rather
than as one component inside an iterative literature-expansion loop with feedback from retrieved
results.

### 5. Screening and systematic-review workflow benchmarks

Another group of resources evaluates screening, prioritisation, or evidence-synthesis workflow
after a candidate set of papers has already been retrieved. Examples include active-learning
screening datasets, ASReview-style simulations, Rayyan-like screening workflows, RobotReviewer,
Covidence, EPPI-Reviewer, and other systematic-review management tools.

These resources are important for downstream review automation, but they do not directly test
the upstream search problem. They usually assume the candidate records already exist, so they are
less informative for evaluating whether a system can discover missing papers or expand a
literature set.

### 6. Scientific QA and literature synthesis

Scientific QA and literature synthesis systems evaluate whether a model can answer scientific
questions with citations or produce grounded summaries. Examples include PaperQA, LitQA,
OpenScholar, ScholarQABench, and related scientific QA systems.

These systems rely on retrieval, but their main output is an answer, explanation, or synthesis
rather than a paper set. Their evaluation therefore focuses on answer correctness, citation
support, attribution, or synthesis quality. They are adjacent to literature discovery, but they do
not directly evaluate the completeness, diversity, or usefulness of an expanded paper list.

### 7. Citation-graph and related-paper exploration

Tools such as ResearchRabbit, Litmaps, Connected Papers, Scite, Semantic Scholar, OpenAlex, and
citation-graph datasets support related-paper discovery, citation exploration, and literature
mapping. They are especially relevant when the starting point is one or more known papers.

However, these tools are often product-facing or infrastructure-oriented, and public evaluation
is usually not framed as a controlled benchmark for iterative expansion. Citation-graph expansion
also differs from search-query generation: it explores neighbourhoods in a citation or metadata
graph rather than explicitly generating and refining search strategies.

## Cross-Cutting Observations

### Existing benchmarks cover different slices of the pipeline

The surveyed resources cover many parts of the literature-review pipeline, including retrieval,
Boolean query generation, screening, citation exploration, QA, summarisation, and broader
research-agent workflows. However, they usually evaluate one slice at a time.

A retrieval benchmark may tell us whether relevant papers can be ranked for a query. A screening
benchmark may tell us whether candidate records can be prioritised. A scientific QA benchmark may
tell us whether retrieved evidence can support an answer. A research-agent benchmark may tell us
whether an agent can complete a broad discovery task. These are all useful, but they measure
different capabilities.

### Input assumptions differ substantially

The most important distinction is the input setting. Many benchmarks start from a natural-language
query. Systematic-review datasets often start from a review topic, protocol, or expert query.
Citation tools often start from a seed paper. Research-agent benchmarks may start from a broad
research question or condition.

The setting that remains under-represented is the combined input:

```text
Topic + seed papers + existing corpus
```

This input is important because it reflects a common literature-review scenario: the user already
has a partial corpus or a few known papers and wants to expand that set in a controlled way.

### Output assumptions also differ

Some benchmarks expect a ranked list. Others expect an unordered set of relevant papers. Some
expect a target paper, a long-form answer, a citation-supported synthesis, or a search trajectory.
These outputs should not be treated as equivalent.

For literature expansion, the most relevant output is not simply a ranked list or a final answer.
It is an expanded set of papers that improves the starting corpus by adding relevant, diverse,
and non-duplicative papers.

### Evaluation is still fragmented

Current evaluation styles include exact match, retrieval metrics, ranking metrics, set overlap,
recall, screening workload reduction, answer quality, citation support, and qualitative product
evaluation. These metrics are useful but incomplete for seed-conditioned expansion.

An expansion benchmark would need to evaluate not only whether retrieved papers are relevant, but
also whether they add value relative to the seed set and existing corpus. This suggests evaluation
criteria such as expansion coverage, novelty beyond seeds, redundancy control, topical coherence,
diversity across subtopics, and the quality of the iterative search trajectory.

## The Under-Covered Setting: Seed-Conditioned Literature Expansion

Across the bundled benchmarks and broader landscape, the clearest gap is seed-conditioned
literature expansion:

```text
Input:  topic + seed papers + existing corpus
Output: expanded set of relevant papers
Process: iterative search, retrieval feedback, diagnosis, and refinement
```

This setting is adjacent to several existing tasks, but not identical to any of them.

It is related to query-to-paper retrieval because it requires finding papers from search queries.
It is related to comprehensive paper search because the goal is coverage rather than a single
answer. It is related to Boolean query generation because search strategies may be explicit and
iteratively refined. It is related to citation-graph exploration because seed papers can guide
expansion. It is related to research-agent evaluation because the process may involve multiple
steps and feedback loops.

However, it differs from all of these because the system must reason from an existing partial
corpus, identify missing conceptual areas, generate or refine search strategies, inspect retrieved
results, and decide how to expand the paper set without simply duplicating what is already known.

## Implications for Future Benchmark Design

The preceding comparison suggests that the uncovered setting is not simply another
query-to-paper retrieval task. Instead, it combines elements of retrieval, search
strategy generation, paper-set evaluation, and iterative search.

A benchmark targeting this setting would therefore likely need several components:

1. **Topic definition** — a clear research topic or information need.
2. **Seed papers** — one or more known relevant papers that define the starting point.
3. **Existing corpus** — a partial set of papers that the system should expand.
4. **Search space** — either a fixed corpus for reproducibility or a controlled search backend.
5. **Gold or reference expansion set** — papers that should be discoverable beyond the seeds.
6. **Evaluation metrics** — relevance, coverage, novelty, redundancy, diversity, and trajectory quality.
7. **Ablation-friendly design** — support for evaluating retrieval, query generation, feedback diagnosis, and refinement separately.

Existing resources can contribute pieces of this design. LitSearch is useful for fixed-corpus
retrieval. PaSa and ScholarQuest are useful for paper-set evaluation. AutoResearchBench is useful
for multi-step process evaluation. Seed Collection and Boolean-query benchmarks are useful for
query formulation and seed-based retrieval ideas. Citation-graph systems are useful for modelling
paper-neighbourhood expansion. But none of these resources directly provides the full setting.

## Summary

The literature-retrieval evaluation landscape is broad but fragmented. Existing benchmarks and
systems cover query-to-paper retrieval, paper-set search, Boolean query generation, systematic
review retrieval, screening, citation exploration, scientific QA, and autonomous research-agent
workflows. These are all adjacent to literature expansion, but they do not directly evaluate the
same task.

The main uncovered setting is seed-conditioned iterative literature expansion: starting from a
topic, seed papers, and an existing corpus, then expanding that corpus through search, feedback,
and refinement. This gap motivates treating literature expansion as a distinct evaluation problem
rather than assuming that existing retrieval, QA, screening, or research-agent benchmarks are
sufficient substitutes.
