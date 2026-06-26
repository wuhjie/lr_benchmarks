# Benchmark Taxonomy

## Motivation

The four benchmarks in this repository are related — all of them involve finding scientific
papers — but they are **not equivalent**. They evaluate different tasks, assume different
inputs and outputs, and judge success in different ways. Treating them as interchangeable
"literature search benchmarks" would obscure these differences. This document organises them
along two axes: by **task type** and by **input/output structure**, and then comments on the
**evaluation perspectives** they emphasise.

The taxonomy is descriptive. Where the source documentation is not explicit, entries are
written cautiously (for example, "partial" or "unclear").

## Task-Type Taxonomy

| Task type | Description | Typical input | Typical output | Closest benchmark(s) | Fit to CiteClaw-style expansion |
| --- | --- | --- | --- | --- | --- |
| Query-to-paper retrieval | Retrieve relevant papers for a query over a fixed corpus | Natural-language query | Retrieved / ranked paper list | LitSearch | Partial — useful as a retrieval sub-component, not for seed-based expansion |
| Scholarly search / academic QA | Satisfy a scholarly information need through search | Natural-language question | Paper set or answer | PaSa (partial) | Partial — closer to recall-oriented search than to expansion |
| Paper-search agent | An agent collects a set of relevant papers using search tools | Search query | Set of relevant papers | ScholarQuest, PaSa | Partial-to-moderate — agentic set collection overlaps with expansion |
| Autonomous research-agent benchmark | Multi-step discovery of a target paper or comprehensive set | Research question / condition | Target paper or paper set, with a search process | AutoResearchBench | Partial — process-oriented, but not seed/corpus-conditioned |
| Literature expansion / corpus growth | Grow a known set of papers using a topic and seeds against a corpus | Topic + seed papers + existing corpus | Expanded set of related papers | None directly | Closest to CiteClaw — **not directly covered** by any included benchmark |

The final row corresponds most closely to the CiteClaw setting and is the clearest **gap** in
the current landscape: none of the four benchmarks is built around topic + seed papers +
existing corpus as the conditioning input.

## Input/Output Taxonomy

Rows are input or output elements; columns are benchmarks. Values are `yes`, `no`, `partial`,
or `unclear`, based on the fetched documentation.

| Element | AutoResearchBench | LitSearch | PaSa | ScholarQuest |
| --- | --- | --- | --- | --- |
| **Input: natural-language query** | yes | yes | yes | yes |
| **Input: research question** | yes | partial | partial | partial |
| **Input: topic** | partial | no | partial | yes (topic seeds) |
| **Input: seed papers** | unclear | no | no | no |
| **Input: existing corpus** | partial (search backend) | yes (fixed corpus) | yes (paper database) | partial (Lewen / arXiv) |
| **Output: retrieved paper list** | yes (Wide) | yes | yes | yes |
| **Output: ranked paper list** | partial | yes | partial | partial |
| **Output: answer / report** | partial (Deep → target paper) | no | no | no |
| **Output: search trajectory** | yes (multi-step) | no | partial | partial (construction-time) |
| **Output: supporting evidence / citations** | partial | partial (citations in corpus) | partial | partial |

Observations:

- **Seed papers as an explicit input** are essentially absent across all four benchmarks; this
  is central to CiteClaw-style expansion.
- **A fixed, well-defined corpus** is clearest in LitSearch; the others either rely on live
  search backends or do not bundle the corpus.
- **Search trajectories** are an explicit concern mainly in AutoResearchBench (multi-step
  agentic process), while the others focus on the final paper set.

## Evaluation Perspective

Different benchmarks emphasise different notions of "doing well":

- **Retrieval accuracy** — whether the correct papers are found at all. Most relevant to
  LitSearch (gold paper IDs over a fixed corpus) and to AutoResearchBench Deep Research (a
  specific target paper).
- **Ranking quality** — whether relevant papers are placed near the top. Most natural for
  LitSearch; only partially applicable to the set-oriented benchmarks.
- **Paper relevance (set quality)** — whether a collected set matches a target set. Central to
  AutoResearchBench Wide Research, PaSa, and ScholarQuest, which are recall- and
  set-overlap-oriented.
- **Agent process quality** — whether the search process itself is sound (steps, tool use).
  Most relevant to AutoResearchBench; partially visible in PaSa/ScholarQuest construction.
- **Evidence quality** — whether retrieved papers are supported by citations or rationale.
  Only partially captured by any of the four.
- **End-task success** — whether a broader research objective is achieved. Approached most
  directly by AutoResearchBench, and only indirectly by the others.

These perspectives are not mutually exclusive, and no single benchmark covers all of them.

## Main Takeaway

The four benchmarks are **adjacent but not equivalent**. They sit at different points along a
spectrum from clean query-to-paper retrieval (LitSearch), through recall-oriented scholarly and
agentic search (PaSa, ScholarQuest), to autonomous multi-step research (AutoResearchBench). The
literature-expansion task that is central to CiteClaw — conditioning on a topic, seed papers,
and an existing corpus — is not directly represented, and would require adaptation rather than
direct reuse.
