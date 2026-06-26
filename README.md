# LR_BENCHMARKS

## Overview

A curated collection of existing benchmarks related to **literature retrieval, academic paper
search, scholarly discovery, and research-agent evaluation**. It gathers several adjacent
benchmarks into one place and adds a categorisation and comparison layer, so their tasks,
inputs, outputs, and evaluation styles can be examined side by side.

The four benchmark folders are fetched copies of their original repositories / datasets and are
kept as upstream snapshots. The added value of this repository is the categorisation and
comparison provided by the top-level documentation:

- [`benchmark_taxonomy.md`](benchmark_taxonomy.md) — task-type and input/output taxonomy.
- [`benchmark_comparison.md`](benchmark_comparison.md) — detailed, per-benchmark comparison.

## Repository Structure

```text
LR_BENCHMARKS/
├── autoresearch/        # AutoResearchBench: inference/evaluation code + dataset/ (released bundle)
├── litsearch-dataset/   # LitSearch: query set + retrieval corpus
├── pasa-dataset/        # PaSa: AutoScholarQuery / RealScholarQuery data + paper database
└── scholarquest/        # ScholarQuest: benchmark data + construction pipeline + search API
```

- **`autoresearch/`** — a fetched copy of the AutoResearchBench code repository (batch
  inference, Deep/Wide evaluation scripts, search backends, and the bundle-decryption
  utility). The released benchmark bundle is consolidated under `autoresearch/dataset/`.
- **`litsearch-dataset/`** — the LitSearch dataset: a query set and a retrieval corpus
  provided in cleaned and S2ORC forms.
- **`pasa-dataset/`** — the PaSa dataset: AutoScholarQuery splits, a RealScholarQuery test
  set, a paper database, and supporting training data.
- **`scholarquest/`** — a fetched copy of the ScholarQuest repository: the released benchmark
  data, the benchmark-construction pipeline, and the Lewen academic search API.

Folder names are kept as fetched. Very large artefacts (multi-GB corpora, archive blobs, and
the decrypted AutoResearchBench questions) are excluded from version control via `.gitignore`.

## Included Benchmarks

### AutoResearchBench
- Code: <https://github.com/CherYou/AutoResearchBench>
- Data: <https://huggingface.co/datasets/Lk123/AutoResearchBench>

AutoResearchBench is primarily designed for **autonomous scientific literature discovery** by
research agents. It defines two task types: *Deep Research*, which requires tracking down a
specific target paper through a multi-step probing process, and *Wide Research*, which
requires collecting a set of papers satisfying given conditions. Typical input is a research
question or a condition description; typical output is either a single target paper (Deep) or
a set of qualifying papers (Wide). It is related to research-agent evaluation because it
stresses multi-step search and reasoning over scientific literature. *Caveat:* the data is
released in an obfuscated bundle that must be decrypted locally, and reported baseline scores
are low, so it can be interpreted as a deliberately difficult, agent-oriented setting rather
than a clean retrieval test.

### LitSearch
- Code: <https://github.com/princeton-nlp/LitSearch>
- Data: <https://huggingface.co/datasets/princeton-nlp/LitSearch>
- Paper: <https://arxiv.org/abs/2407.18940>

LitSearch is a **retrieval benchmark for scientific literature search**, primarily focused on
recent ML and NLP papers. According to its documentation it contains 597 realistic
literature-search queries with gold paper IDs, over a corpus of 64,183 documents provided both
as cleaned titles/abstracts and in the S2ORC schema. Typical input is a natural-language query;
typical output is a ranked list of papers (or matched gold paper IDs) from a fixed corpus. It
is directly relevant to literature-search systems as a clean, reproducible setting for
comparing retrievers and rerankers. *Caveat:* its scope is limited to recent ML/NLP papers and
a closed corpus, so it does not test open-ended or agentic search.

### PaSa
- Code: <https://github.com/bytedance/pasa>
- Data: <https://huggingface.co/datasets/CarlanLark/pasa-dataset>
- Paper: <https://arxiv.org/abs/2501.10120>

PaSa accompanies *PaSa: An LLM Agent for Comprehensive Academic Paper Search*. It is designed
around **comprehensive academic paper search**, where the goal is to collect the relevant
papers for a scholarly query rather than answer a single question. The dataset copy here
includes AutoScholarQuery splits (synthetic scholarly queries) and a RealScholarQuery test set,
together with a paper database. Typical input is a scholarly search query; typical output is a
set of relevant papers. It is relevant to literature search as a recall-oriented, agent-style
search setting. *Caveat:* this folder mirrors the released data only; the PaSa agent code lives
upstream, and exact split statistics are not fully documented in the dataset card.

### ScholarQuest
- Code & data: <https://github.com/pty12345/ScholarQuest>

ScholarQuest is designed for evaluating **paper-search agents**, framed as retrieving *sets* of
relevant arXiv papers for realistic scholarly queries rather than answering factoid questions.
Its documentation states the released dataset contains 1,111 benchmark queries, each with a
list of relevant arXiv IDs and between 5 and 200 answers, plus a larger metadata pool (13,097
records) describing query topics, domains, and four controlled query categories. Typical input
is a paper-search query; typical output is a set of relevant arXiv IDs. It is relevant as an
open-arXiv set-retrieval benchmark that also documents its construction pipeline and search
API. *Caveat:* it is construction-focused and depends on the Lewen search API and external
keys; the underlying paper corpus is not bundled.

## Quick Comparison

| Benchmark | Broad category | Typical input | Typical output | Main relevance | Main caveat |
| --- | --- | --- | --- | --- | --- |
| **AutoResearchBench** | Autonomous research-agent benchmark | Research question / condition | Target paper (Deep) or paper set (Wide) | Multi-step agentic literature discovery | Obfuscated release; needs search backends + keys; low baselines |
| **LitSearch** | Query-to-paper retrieval | Natural-language query | Ranked papers / gold paper IDs | Clean, reproducible retrieval comparison | ML/NLP scope; closed corpus; not agentic |
| **PaSa** | Scholarly / comprehensive paper search | Scholarly search query | Set of relevant papers | Recall-oriented "find all relevant papers" | Data-only copy; partial documentation |
| **ScholarQuest** | Paper-search agent (set retrieval) | Paper-search query | Set of relevant arXiv IDs | Open-arXiv set retrieval + construction pipeline | Depends on external search API/keys; corpus not bundled |

## Why This Repository Exists

Collecting these benchmarks together is more useful than a list of links because:

- It clarifies that "literature search benchmark" can mean quite different things in practice.
- It separates **query-to-paper retrieval** (LitSearch), **scholarly / comprehensive search**
  (PaSa), **paper-search agents** (ScholarQuest), and **autonomous research agents**
  (AutoResearchBench).
- It helps identify which benchmarks may be **adaptable** for literature-expansion settings,
  and which only partially overlap.
- By mapping the space, it makes **gaps** more visible — for example, the absence of a
  benchmark built around topic + seed papers + an existing corpus as the conditioning input.

## How to Use This Repository

- Use the **original benchmark folders** for exact code, data, and setup instructions; their
  in-folder documentation is authoritative.
- Use the **top-level documentation files** (`benchmark_taxonomy.md`, `benchmark_comparison.md`)
  for comparison and interpretation.
- Check the **upstream repositories** linked above for the most recent versions; the copies
  here are point-in-time snapshots.

## Notes on Upstream Repositories

The four benchmark folders are intended to remain as close as possible to their fetched
upstream versions. They are not restructured or edited beyond what is necessary to store and
organise them here (for example, consolidating the AutoResearchBench data under
`autoresearch/dataset/` and excluding very large artefacts from version control). For any
discrepancy, the upstream repositories and dataset pages are authoritative.
