# Benchmark Taxonomy

## Motivation

The four benchmarks in this repository are related — all of them involve finding scientific
papers — but they are **not equivalent**. They evaluate different tasks, assume different
inputs and outputs, and judge success in different ways. Treating them as interchangeable
"literature search benchmarks" would obscure these differences. This document categorises all
four in a single table along the dimensions that matter for comparison — task formulation,
input, output, corpus, evaluation style, and domain coverage — and then adds supporting notes
on the task-type, input/output, and evaluation perspectives. A final section identifies the
task setting that none of the four directly covers.

The taxonomy is descriptive. Where the source documentation is not explicit, entries are
written cautiously (for example, "partial" or "unclear").

## Consolidated Benchmark Table

| Benchmark | Task type / focus | Input | Output | Corpus / index | Evaluation style | Domain coverage |
| --- | --- | --- | --- | --- | --- | --- |
| **AutoResearchBench** | Autonomous research-agent benchmark: multi-step discovery of a target paper (Deep) or comprehensive set (Wide) | Research question / condition description | Target paper (Deep) or paper set (Wide), plus a search trajectory | Live search backend (requires search APIs / keys) | Exact target match (Deep) and set-overlap / IoU (Wide); appears to use model-based judging | Scientific literature; appears multi-domain |
| **LitSearch** | Query-to-paper retrieval over a fixed corpus | Natural-language query | Ranked papers / gold paper IDs | Fixed, bundled corpus | Standard retrieval / ranking against gold paper IDs | Recent ML and NLP papers (arXiv-heavy) |
| **PaSa** | Comprehensive academic paper search (agentic) | Scholarly search query (AutoScholarQuery / RealScholarQuery) | Set of relevant papers | Large paper database (data-only copy in this repository) | Recall-oriented set retrieval | Academic papers (arXiv / CS-oriented database) |
| **ScholarQuest** | Paper-search agent / set retrieval, with controlled query categories | Paper-search query (`final_query`) | Set of relevant arXiv IDs (reported 5–200 per query) | External search API (Lewen) / arXiv; corpus not bundled | Set retrieval against answer ID sets | arXiv papers across taxonomy-derived domains |

The table groups task formulation, input/output format, corpus, and evaluation style for the four
benchmarks in one place. The sections below expand on the dimensions that benefit from more
nuance.

## Task-Type Spectrum and the Uncovered Setting

Placing the four benchmarks on a task-type spectrum makes the missing setting explicit:

| Task type | Description | Typical input | Typical output | Closest benchmark(s) |
| --- | --- | --- | --- | --- |
| Query-to-paper retrieval | Retrieve relevant papers for a query over a fixed corpus | Natural-language query | Retrieved / ranked paper list | LitSearch |
| Scholarly search / academic QA | Satisfy a scholarly information need through search | Natural-language question | Paper set or answer | PaSa (partial) |
| Paper-search agent | An agent collects a set of relevant papers using search tools | Search query | Set of relevant papers | ScholarQuest, PaSa |
| Autonomous research-agent benchmark | Multi-step discovery of a target paper or comprehensive set | Research question / condition | Target paper or paper set, with a search process | AutoResearchBench |
| **Seed-conditioned literature expansion** | Grow a known set of papers using a topic and seeds against a corpus | Topic + seed papers + existing corpus | Expanded set of related papers | **None directly** |

The four benchmarks span the first four rows. The final row — expansion conditioned on a topic,
seed papers, and an existing corpus — is the clearest **gap**: none of the four is built around
topic + seed papers + existing corpus as the conditioning input.

## Input/Output Detail

Values are `yes`, `no`, `partial`, or `unclear`, based on the fetched documentation.

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

- **Seed papers as an explicit input** are essentially absent across all four benchmarks.
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
setting that is not directly represented is **seed-conditioned literature expansion** —
conditioning on a topic, seed papers, and an existing corpus to grow a known set — which would
require adaptation rather than direct reuse of any single benchmark.
