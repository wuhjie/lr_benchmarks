# Benchmark Comparison

This document provides a more detailed, per-benchmark comparison than the top-level README. All
statements are based on the documentation inside the fetched folders; uncertain details are
phrased cautiously.

## Overview Table

| Benchmark | Original focus | Domain coverage | Input format | Output format | Evaluation style | Strength | Limitation | Possible use for CiteClaw-related analysis |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **AutoResearchBench** | Autonomous scientific literature discovery (Deep + Wide research) | Scientific literature, appears multi-domain | Research question / condition description | Single target paper (Deep) or paper set (Wide), via a multi-step process | Exact target match (Deep) and set-overlap / IoU (Wide); appears to use model-based judging | Captures multi-step, open-ended agentic search; challenging | Obfuscated release; requires search backends and API keys; low baselines | Reference for evaluating broader research workflows and process quality |
| **LitSearch** | Retrieval benchmark for scientific literature search | Recent ML and NLP papers | Natural-language query | Ranked papers / gold paper IDs over a fixed corpus | Standard retrieval/ranking against gold paper IDs | Clean, reproducible, fixed corpus | Narrow domain; closed corpus; not agentic | Basic query-to-paper retrieval testing component |
| **PaSa** | LLM agent for comprehensive academic paper search | Academic papers (arXiv / CS-oriented database) | Scholarly search query (AutoScholarQuery / RealScholarQuery) | Set of relevant papers | Recall-oriented set retrieval | Recall-focused "find all relevant papers" setting | Data-only copy here; partial documentation; large paper database | Reference for recall/coverage-style evaluation of discovered papers |
| **ScholarQuest** | Paper-search agent benchmark + construction pipeline | arXiv papers across taxonomy-derived domains | Paper-search query (`final_query`) | Set of relevant arXiv IDs (reported 5–200 per query) | Set retrieval against answer ID sets | Documents both data and construction; controlled query categories | Depends on external search API/keys; corpus not bundled | Reference for set-retrieval evaluation and controlled query design |

## Benchmark Notes

### AutoResearchBench

- **Useful for:** evaluating multi-step, agentic literature discovery, including both
  pinpoint search (Deep Research) and comprehensive collection (Wide Research). It is the only
  included benchmark that foregrounds the search *process* rather than only the final set.
- **Does not directly test:** seed-paper-conditioned expansion, corpus-aware growth from a
  known set, or structured/Boolean query generation.
- **More suitable for:** research-agent evaluation. It is less suited to clean retrieval
  benchmarking because of its obfuscated release and reliance on live search backends.
- **Adaptation to topic/seed-paper expansion:** partial. Its Wide Research format (collect
  papers satisfying conditions) is conceptually close to expansion, but it is not conditioned
  on seed papers or an existing corpus, so adaptation would be required.

### LitSearch

- **Useful for:** controlled, reproducible query-to-paper retrieval over a fixed corpus, with
  gold paper IDs and quality/specificity annotations.
- **Does not directly test:** agentic, multi-step search; recall over an open or growing
  corpus; or expansion from seed papers.
- **More suitable for:** retrieval (and reranking) evaluation. It is the cleanest of the four
  for isolating retriever quality.
- **Adaptation to topic/seed-paper expansion:** limited but useful. Its query–paper pairs and
  fixed corpus can support a basic retrieval component of an expansion pipeline, but it does
  not model seed conditioning or corpus growth.

### PaSa

- **Useful for:** recall-oriented scholarly search, where the objective is to comprehensively
  collect relevant papers for a query rather than rank a few. Includes both synthetic
  (AutoScholarQuery) and real (RealScholarQuery) query styles.
- **Does not directly test:** seed-paper conditioning or expansion of an existing curated set;
  in this repository, it also does not include the agent code (data only).
- **More suitable for:** search-agent evaluation framed around coverage/recall.
- **Adaptation to topic/seed-paper expansion:** moderate. Its comprehensive-search framing
  aligns with expansion goals, and its query/answer structure can be interpreted as a target
  pool, but seed papers and an explicit existing corpus would need to be introduced.

### ScholarQuest

- **Useful for:** set-retrieval evaluation over arXiv, with queries organised by controlled
  categories (e.g., method capability, setting anchor, claim comparison, scope control) and
  answer sets of bounded size.
- **Does not directly test:** retrieval from seed papers or from a fixed bundled corpus; the
  underlying search index (Lewen API) is an external dependency.
- **More suitable for:** paper-search-agent evaluation, particularly for measuring the quality
  of a retrieved *set* against a reference set.
- **Adaptation to topic/seed-paper expansion:** moderate. Its topic-seed → query →
  answer-set construction is structurally close to expansion, and could be adapted by adding
  seed-paper conditioning and corpus awareness.

## Cross-Benchmark Observations

- Some benchmarks are closer to **clean retrieval**: LitSearch provides a fixed corpus and gold
  paper IDs, making it the most directly measurable.
- Some are closer to **agentic search**: PaSa and ScholarQuest emphasise collecting sets of
  relevant papers, often through search tools rather than a single ranking pass.
- Some evaluate **broader research-task completion**: AutoResearchBench foregrounds multi-step
  discovery and process quality.
- **None should be treated as a complete evaluation protocol for CiteClaw** without adaptation.
  In particular, none is conditioned on seed papers plus an existing corpus, and none directly
  measures the usefulness of *newly discovered* papers relative to a starting set.
