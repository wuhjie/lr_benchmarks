# Benchmark Comparison

This document provides a detailed comparison of literature-retrieval-related benchmarks,
datasets, and representative systems. It complements [`benchmark_taxonomy.md`](benchmark_taxonomy.md),
which defines the task spectrum and identifies the currently uncovered setting.

The first part compares the four benchmarks bundled in this repository:

- AutoResearchBench
- LitSearch
- PaSa
- ScholarQuest

The second part summarises adjacent benchmark families, datasets, and systems that are useful
for understanding the broader literature-retrieval evaluation landscape. This broader landscape
is intentionally **representative rather than exhaustive**. The goal is to map task settings and
evaluation paradigms, not to maintain a complete bibliography of every related paper or product.

All descriptions are based on upstream documentation and publicly available information. Where
details are uncertain, the wording is cautious.

---

## Overview Table

| Benchmark | Original focus | Domain coverage | Input format | Output format | Evaluation style | Strength | Limitation | Typical use as an evaluation reference |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **AutoResearchBench** | Autonomous scientific literature discovery, including Deep and Wide research | Scientific literature; appears multi-domain | Research question / condition description | Target paper, paper set, and search trajectory | Exact target match, set overlap / IoU, and process-oriented judging | Captures multi-step, open-ended agentic search | Obfuscated release; depends on live search backends and API keys | Reference for broader research-agent evaluation and process quality |
| **LitSearch** | Scientific literature retrieval over a fixed corpus | Recent ML and NLP papers | Natural-language literature search query | Ranked papers / gold paper IDs | Standard retrieval / ranking against gold paper IDs | Clean, reproducible, fixed-corpus setup | Narrow domain; closed corpus; not agentic | Reference for query-to-paper retrieval and reranking |
| **PaSa** | Comprehensive academic paper search with an LLM agent | Academic papers, mainly arXiv / CS-oriented | Scholarly search query | Set of relevant papers | Recall-oriented set retrieval | Focuses on finding broad paper sets rather than only top-ranked results | Data-only copy in this repository; partial documentation; large external paper database | Reference for coverage-oriented paper discovery |
| **ScholarQuest** | Paper-search agent benchmark and construction pipeline | arXiv papers across taxonomy-derived domains | Paper-search query (`final_query`) | Set of relevant arXiv IDs | Set retrieval against answer ID sets | Controlled query categories and bounded answer sets | External search API dependency; corpus not bundled | Reference for set-retrieval evaluation and controlled query design |

---

## Benchmark Notes

### AutoResearchBench

- **Useful for:** evaluating multi-step, agentic literature discovery, including both pinpoint
  search and comprehensive paper collection.
- **Does not directly test:** seed-paper-conditioned expansion, corpus-aware growth from an
  existing set, or structured/Boolean query generation.
- **More suitable for:** research-agent evaluation rather than clean retrieval benchmarking.
- **Adaptation to seed-conditioned expansion:** partial. Its Wide Research setting is
  conceptually close to collecting a paper set, but it is not conditioned on seed papers or an
  existing corpus.

### LitSearch

- **Useful for:** controlled query-to-paper retrieval over a fixed corpus with gold paper IDs.
- **Does not directly test:** multi-step search, feedback-driven query refinement, open-corpus
  search, or expansion from seed papers.
- **More suitable for:** evaluating retrievers and rerankers.
- **Adaptation to seed-conditioned expansion:** limited. Its fixed corpus and query-paper pairs
  can support retrieval-component evaluation, but not full expansion.

### PaSa

- **Useful for:** recall-oriented scholarly search where the goal is to collect a broad set of
  relevant papers for a query.
- **Does not directly test:** expansion from seed papers or growth of an existing curated
  corpus.
- **More suitable for:** coverage-oriented paper-search evaluation.
- **Adaptation to seed-conditioned expansion:** moderate. Its query-to-paper-set structure is
  relevant, but seed conditioning and corpus-state modelling would need to be added.

### ScholarQuest

- **Useful for:** paper-set retrieval over arXiv, with controlled query categories and answer
  sets.
- **Does not directly test:** seed-paper-based retrieval, fixed-corpus expansion, or iterative
  corpus growth.
- **More suitable for:** paper-search-agent evaluation and controlled query design.
- **Adaptation to seed-conditioned expansion:** moderate. Its topic/query-to-answer-set
  construction is structurally useful, but seed papers and corpus awareness are not part of the
  core task.

---

## Cross-Benchmark Observations

- **LitSearch** is closest to clean, reproducible query-to-paper retrieval.
- **PaSa** and **ScholarQuest** are closer to paper-set search, where recall and coverage matter
  more than top-rank precision alone.
- **AutoResearchBench** is closest to multi-step research-agent evaluation, because it foregrounds
  process and trajectory.
- None of the four directly evaluates **seed-conditioned literature expansion**: starting from a
  topic, seed papers, and an existing corpus, then expanding the corpus with newly discovered
  relevant papers.
- The four benchmarks are therefore adjacent but not interchangeable. They cover different
  points along the literature-retrieval task spectrum.

---

# Broader Benchmark Landscape

The following sections summarise adjacent resources that help contextualise the four bundled
benchmarks. They are included because they represent important evaluation settings or reusable
building blocks.

This section is intentionally selective. Resources are included when they help clarify one of
the following:

1. a distinct task formulation;
2. a reusable dataset or benchmark;
3. a representative evaluation paradigm;
4. a system type relevant to literature retrieval, screening, synthesis, or expansion.

---

## 1. Boolean Query Generation and Search Strategy Design

This line of work is relevant because seed-conditioned expansion often requires generating or
refining search queries. However, most existing Boolean-query work is framed around systematic
review retrieval, especially biomedical systematic reviews.

| Work / resource | Link | Core task | Input | Output | Evaluation setting | Why it matters |
| --- | --- | --- | --- | --- | --- | --- |
| Automatic Boolean Query Refinement | [ACM WWW 2019](https://dl.acm.org/doi/10.1145/3308558.3313544) | Refine an existing Boolean query | Initial expert or generated Boolean query | Refined Boolean query | CLEF TAR 2017/2018 | Representative early work on improving Boolean search strategies |
| Automatic Boolean Query Formulation for Systematic Review Literature Search | [ACM WWW 2020](https://dl.acm.org/doi/10.1145/3366423.3380185) | Generate Boolean queries for systematic reviews | Review protocol / title / objective / PICO-like information | Boolean query | CLEF TAR 2018 | Representative work on automatic query formulation |
| Query Variation Sampling and Learning to Rank | [ACM WWW 2020](https://dl.acm.org/doi/10.1145/3366423.3380075) | Generate and rank query variants | Review topic / candidate query variants | Ranked Boolean queries | CLEF TAR 2017/2018 | Shows query generation can be treated as search over candidate strategies |
| ChatGPT Boolean Query Generation | [arXiv](https://arxiv.org/abs/2302.03495) / [SIGIR 2023](https://dl.acm.org/doi/10.1145/3539618.3591703) | Prompt LLMs to write Boolean queries | Systematic review topic | Boolean query | CLEF TAR; Seed Collection | Representative LLM-based Boolean query generation work |
| AutoBool | [arXiv](https://arxiv.org/abs/2602.00005) / [GitHub](https://github.com/ielab/AutoBool) | Optimise Boolean query generation with retrieval rewards | Review topic | Boolean query | AutoBool-65K; CLEF TAR; Seed Collection | Representative recent work directly optimising generated queries with retrieval metrics |
| SR4CS | [arXiv](https://arxiv.org/html/2604.16330v1) / [GitHub](https://github.com/webis-de/scolia26-sr4cs) | Dataset for CS systematic-review query generation and screening | CS systematic review topics and reported queries | Expert-like Boolean queries and screening labels | SR4CS | Important because it moves systematic-review query resources beyond medicine |

**Summary.** Boolean query generation provides useful components for search-strategy generation,
but the dominant setting is systematic review retrieval. These works usually evaluate query
quality against retrieval metrics, rather than evaluating iterative expansion of an existing
paper corpus.

---

## 2. Systematic Review Retrieval and Screening Benchmarks

Systematic-review benchmarks are important because they define high-recall retrieval and
screening tasks. They are often rigorous, but their task formulation differs from general
literature expansion.

| Benchmark / dataset | Link | Domain coverage | Input | Output / label | Main evaluated task | Why it matters |
| --- | --- | --- | --- | --- | --- | --- |
| CLEF TAR 2017/2018 | [CLEF-TAR GitHub](https://github.com/CLEF-TAR/tar) | Biomedical systematic reviews | Review topic and Boolean query | Relevance judgments and ranked retrieval outputs | High-recall retrieval and screening prioritisation | Established benchmark family for technology-assisted review |
| CLEF 2019 DTA / Intervention | [Task page](https://clefehealth.imag.fr/clefehealth.imag.fr/index1833.html?page_id=173) | Biomedical diagnostic and intervention reviews | Review topic and retrieved PubMed/MEDLINE records | Relevance labels | TAR retrieval and screening | Extends CLEF-style review retrieval beyond earlier DTA-only settings |
| Seed Collection | [arXiv](https://arxiv.org/abs/2204.03096) / [GitHub](https://github.com/ielab/sysrev-seed-collection) | Medical systematic reviews | Review topic, real seed studies, and PubMed query | Included studies, retrieved studies, snowballed studies | Seed-study retrieval, query formulation, screening, citation chasing | One of the closest existing resources to seed-based literature search |
| Literature Search Sandbox | [JAMIA Open](https://academic.oup.com/jamiaopen/article/7/3/ooae098/7775509) / [PubMed](https://pubmed.ncbi.nlm.nih.gov/39323560/) | Health systematic reviews | Review description / key question | Boolean search string | Supervised query generation | Useful paired resource for review-description-to-query generation |
| ASReview / SYNERGY-style datasets | [ASReview](https://asreview.nl/) / [SYNERGY dataset](https://github.com/asreview/synergy-dataset) | Systematic review screening collections | Candidate citation records | Relevant / irrelevant labels | Active-learning screening and stopping | Important downstream benchmark family, but assumes candidate papers have already been retrieved |

**Summary.** Systematic-review resources are strong for high-recall retrieval, screening, and
query design. However, they are often biomedical, protocol-driven, and review-specific. They do
not directly represent general-purpose seed-conditioned expansion over a growing research
corpus.

---

## 3. Scientific QA and Literature Synthesis Benchmarks

Scientific QA benchmarks evaluate whether systems can answer questions using papers. They are
related to literature retrieval, but the final output is usually an answer, not a paper set.

| Benchmark / system | Link | Domain coverage | Input | Output | Main evaluated task | Why it matters |
| --- | --- | --- | --- | --- | --- | --- |
| PaperQA / LitQA | [arXiv](https://arxiv.org/abs/2312.07559) / [GitHub](https://github.com/Future-House/paper-qa) | Scientific literature | Scientific question | Answer with cited evidence | Retrieval-augmented scientific QA | Representative benchmark/system for grounded scientific answering |
| OpenScholar / ScholarQABench | [Nature](https://www.nature.com/articles/s41586-025-10072-4) / [arXiv](https://arxiv.org/html/2411.14199v1) | Multi-domain scientific literature | Scientific question | Long-form answer with citations | Scientific QA and literature synthesis | Representative multi-domain scientific synthesis setting |
| Ai2 Scholar QA | [Official](https://scholarqa.allen.ai/) / [arXiv](https://arxiv.org/abs/2504.10861) | Scientific literature | Scholarly question | Organised answer with citations | Scientific QA assistant evaluation | Useful comparator for answer-oriented scholarly retrieval |

**Summary.** Scientific QA benchmarks require retrieval, but retrieval is evaluated indirectly
through answer quality and citation grounding. They are therefore adjacent to paper discovery,
not direct benchmarks for corpus expansion.

---

## 4. Citation Graph and Related-Paper Discovery

Citation-graph and related-paper systems are relevant because seed-conditioned expansion often
starts from known papers and follows citation or semantic neighbourhoods.

| Resource / system type | Link | Input | Output | Main evaluated task | Why it matters |
| --- | --- | --- | --- | --- | --- |
| S2ORC | [Official](https://allenai.org/data/s2orc) | Paper corpus and citation graph | Metadata, papers, citation links | Corpus-scale scholarly modelling | Useful infrastructure for citation-aware retrieval and expansion |
| OpenAlex | [Official](https://openalex.org/) / [API docs](https://docs.openalex.org/) | Scholarly metadata and graph queries | Papers, authors, venues, concepts, citations | Scholarly metadata retrieval | Open backend for large-scale metadata and graph expansion |
| Semantic Scholar API | [Official](https://www.semanticscholar.org/product/api) | Paper or query | Ranked papers and metadata | Scholarly search / metadata retrieval | Common infrastructure for academic search and paper recommendation |
| ResearchRabbit | [Official](https://www.researchrabbit.ai/) | Seed papers / collections | Related-paper graph and alerts | Citation-neighbourhood exploration | Representative seed-paper exploration product |
| Connected Papers | [Official](https://www.connectedpapers.com/) | Seed paper | Visual related-paper graph | Related-work exploration | Representative graph-based paper discovery product |
| Litmaps | [Official](https://www.litmaps.com/) | Seed papers / collections | Literature map and related papers | Literature mapping and monitoring | Representative citation-map system |

**Summary.** Citation-graph resources are highly relevant to seed-based expansion, but they
usually evaluate or present paper neighbourhoods rather than explicit query generation,
retrieval-feedback loops, or benchmarked expansion quality.

---

## 5. Literature Review Systems and Products

These systems help users search, screen, read, organise, or synthesise literature. They are
included as representative system categories, not as benchmark resources.

| System / product | Link | Category | Main output | Evaluation / public evidence | Why it matters |
| --- | --- | --- | --- | --- | --- |
| Elicit | [Official](https://elicit.com/) / [Evaluation blog](https://elicit.com/blog/how-we-evaluated-elicit-systematic-review) | AI literature review assistant | Search results, evidence tables, summaries, extracted data | Product-facing evaluation of search, screening, and extraction | Representative structured literature-review assistant |
| Consensus | [Official](https://consensus.app/) / [OpenAI case study](https://openai.com/index/consensus/) | Evidence-based academic search | Evidence-backed answers and paper summaries | Product-facing evidence for academic answer synthesis | Representative scientific answer engine |
| Scite | [Official](https://scite.ai/) / [Paper](https://direct.mit.edu/qss/article/2/3/882/102990/scite-A-smart-citation-index-that-displays-the) | Citation-context analysis | Supporting / contrasting / mentioning citation classifications | Evaluated as citation-statement classification | Representative citation-relation system |
| Rayyan | [Official](https://www.rayyan.ai/) | Systematic review screening platform | Screening workflow and collaboration tools | Widely used in review screening workflows | Representative screening-management tool |
| Covidence | [Official](https://www.covidence.org/) | Systematic review workflow platform | Screening, extraction, and review-management workflow | Product-facing review workflow evidence | Representative end-to-end review-management platform |
| ASReview | [Official](https://asreview.nl/) / [GitHub](https://github.com/asreview/asreview) | Active-learning screening | Prioritised screening order | Evaluated through screening simulations | Representative ML-assisted screening system |

**Summary.** Literature review systems demonstrate practical user needs around search,
screening, extraction, and synthesis. However, most report product-facing evidence rather than
benchmark-style evaluation of literature expansion.

---

## 6. Research-Agent and Report-Generation Systems

Research-agent systems are relevant because they evaluate multi-step tool use and literature
synthesis. However, they often produce reports, answers, or research artifacts rather than a
controlled expanded paper set.

| System / benchmark | Link | Input | Output | Main evaluated task | Why it matters |
| --- | --- | --- | --- | --- | --- |
| AutoResearchBench | Bundled in this repository | Research question / condition | Target paper, paper set, and search trajectory | Autonomous literature discovery | Closest bundled benchmark to multi-step research-agent evaluation |
| STORM | [Paper](https://arxiv.org/abs/2402.14207) / [GitHub](https://github.com/stanford-oval/storm) | Topic | Long-form report | Search-augmented report generation | Representative system for search-based synthesis and outline/report generation |
| AI Scientist-style systems | [Paper](https://arxiv.org/abs/2408.06292) | Research problem | Ideas, experiments, and paper-like outputs | Broader autonomous scientific workflow | Represents research automation beyond literature retrieval |

**Summary.** Research-agent systems capture process, planning, and tool use, but their outputs
are usually broader than paper-list discovery. They are therefore useful for process evaluation
ideas, but not direct replacements for literature-expansion benchmarks.

---

# Component Mapping for Seed-Conditioned Expansion

Existing resources provide useful building blocks for a seed-conditioned literature expansion
benchmark, but no single benchmark directly combines all required components.

| Required component | Closest existing resources | What they contribute | What remains missing |
| --- | --- | --- | --- |
| Fixed or controlled corpus | LitSearch; OpenAlex; Semantic Scholar; S2ORC | Reproducible retrieval space or large scholarly index | Corpus-state tracking and expansion from a known starting set |
| Query-to-paper retrieval | LitSearch | Clean retriever/reranker evaluation | Multi-step refinement and seed conditioning |
| Paper-set evaluation | PaSa; ScholarQuest; AutoResearchBench Wide | Recall and set-overlap style evaluation | Evaluation relative to a starting corpus and newly discovered papers |
| Search trajectory evaluation | AutoResearchBench; research-agent systems | Multi-step process and tool-use evaluation | Fine-grained diagnosis of query generation, feedback, and refinement |
| Boolean query generation | WWW 2019/2020 Boolean-query work; ChatGPT Boolean Query Generation; AutoBool; SR4CS | Search-strategy generation and retrieval-based query evaluation | General-domain expansion beyond systematic reviews |
| Seed-based retrieval | Seed Collection; citation-graph systems | Seed studies, citation chasing, related-paper exploration | General-purpose, multi-domain, corpus-aware expansion setting |
| Screening and filtering | CLEF TAR; ASReview; Rayyan; Covidence | Relevance labels and screening workflows | Upstream search expansion before candidate screening |
| Scientific synthesis | PaperQA; OpenScholar; Ai2 Scholar QA | Citation-grounded answer generation | Paper-list completeness and expansion quality |
| Citation-neighbourhood expansion | ResearchRabbit; Connected Papers; Litmaps; OpenAlex; S2ORC | Graph-based discovery from known papers | Benchmark metrics for iterative, query-driven expansion |

---

# Implications for Evaluating Seed-Conditioned Expansion

The preceding comparison suggests that the uncovered setting is not simply another
query-to-paper retrieval task. Instead, it combines elements of retrieval, search strategy
generation, paper-set evaluation, corpus growth, and iterative search.

A benchmark targeting this setting would likely require several components:

1. **Topic definition** — a clear research topic or information need.
2. **Seed papers** — one or more known relevant papers that define the starting point.
3. **Existing corpus** — a partial set of papers that the system should expand.
4. **Search space** — either a fixed corpus for reproducibility or a controlled search backend.
5. **Reference expansion set** — papers that should be discoverable beyond the seeds.
6. **Evaluation metrics** — relevance, coverage, novelty, redundancy, diversity, and trajectory quality.
7. **Ablation-friendly design** — support for evaluating retrieval, query generation, feedback
   diagnosis, and refinement separately.

Together, existing resources provide useful building blocks, but no existing benchmark directly
combines them into the full seed-conditioned expansion setting.

---

# Main Takeaway

The literature-retrieval evaluation landscape is broad but fragmented. Existing resources cover
clean query-to-paper retrieval, high-recall systematic-review retrieval, Boolean query
generation, paper-set search, screening, citation-graph exploration, scientific QA, and broader
research-agent workflows.

However, these settings evaluate different tasks. The currently underrepresented setting is
**seed-conditioned literature expansion**: starting from a topic, seed papers, and an existing
corpus, then discovering additional relevant papers through iterative search and refinement.

The four bundled benchmarks and the broader adjacent resources should therefore be treated as
useful reference points and building blocks, rather than direct substitutes for this full
evaluation setting.