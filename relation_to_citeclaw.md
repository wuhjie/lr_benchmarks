# Relation to CiteClaw

This document explains how the four included benchmarks relate to CiteClaw-style literature
expansion, and why none of them should be treated as a direct or final CiteClaw benchmark. The
goal is interpretation, not a claim that any benchmark "solves" the CiteClaw setting.

## CiteClaw-Style Literature Expansion

The relevant CiteClaw setting can be described as a pipeline:

```text
topic + seed papers + existing corpus
        → concept decomposition
        → query generation / search
        → retrieved candidate papers
        → feedback / refinement
        → expanded literature set
```

The defining characteristics are that the system is **conditioned on seed papers and an
existing corpus**, decomposes a topic into concepts, generates queries, retrieves candidates,
and **iteratively refines** to produce an expanded set of useful papers. The objective is
coverage and usefulness of newly discovered papers, not matching a single predetermined target.

## Why These Benchmarks Are Relevant

The four benchmarks are **adjacent** to this setting because each involves some combination of
literature retrieval, scholarly search, paper discovery, or research-agent evaluation:

- **LitSearch** models query-to-paper retrieval over a fixed corpus — the retrieval step of an
  expansion pipeline in isolation.
- **PaSa** models comprehensive, recall-oriented academic paper search — close to the goal of
  collecting many relevant papers.
- **ScholarQuest** models paper-search agents that return *sets* of relevant arXiv papers, with
  a topic-seed-driven construction process.
- **AutoResearchBench** models autonomous, multi-step research-agent behaviour, including
  comprehensive collection (Wide Research).

Together they cover retrieval quality, recall-oriented search, set retrieval, and agentic
process — all components that a CiteClaw-style system also exercises.

## Why They Are Not Direct CiteClaw Benchmarks

CiteClaw's `ExpandBySearch`-style setting appears to require capabilities that these benchmarks
do not directly evaluate:

- **Seed-paper conditioning** — expansion starts from a known set of papers; none of the
  benchmarks takes seed papers as an explicit input.
- **Corpus-aware expansion** — growth is relative to an existing corpus; the benchmarks either
  use a fixed corpus without a "starting set", or rely on external search backends.
- **Iterative query refinement** — expansion involves feedback loops; most benchmarks evaluate
  a final set rather than a refinement process.
- **Boolean or structured query generation** — expansion may require structured queries; the
  benchmarks generally assume natural-language queries.
- **Retrieval feedback diagnosis** — understanding *why* retrieval missed relevant papers is
  not part of the standard evaluations.
- **Evaluation of newly discovered useful papers** — expansion should be judged on useful
  *additions* relative to the seed set, whereas several benchmarks emphasise exact-target
  matching or fixed reference sets.

For these reasons, the benchmarks here are **partially suitable** at best and would need
adaptation before they could measure CiteClaw-style expansion.

## Possible Adaptation Directions

These benchmarks could nonetheless inform a CiteClaw evaluation in several ways:

- **Basic retrieval testing** — use LitSearch-style query-to-paper pairs to test the retrieval
  component in isolation.
- **Agentic paper discovery** — use PaSa- and ScholarQuest-style search settings to evaluate
  set collection and recall under agentic search.
- **Broader research workflow** — use AutoResearchBench-style tasks to probe multi-step
  discovery and process quality.
- **Seed-conditioned layer** — build a small custom layer that converts a topic plus seed
  papers into an expected pool of related papers, reusing query/answer structures from
  ScholarQuest or PaSa where possible.
- **Expansion-oriented metrics** — evaluate **recall, novelty, relevance, diversity, and
  coverage** of retrieved papers relative to a seed set, rather than only exact-target match.

These directions reuse parts of the existing benchmarks while adding the seed/corpus
conditioning and the expansion-specific metrics that CiteClaw needs.

## Main Conclusion

These benchmarks are useful for understanding the existing benchmark landscape around
literature search and research agents, and several of their components can be adapted. However,
**CiteClaw likely needs an adapted or custom evaluation protocol** for its specific
literature-expansion setting — one that is conditioned on seed papers and an existing corpus,
supports iterative refinement, and measures the usefulness of newly discovered papers. None of
the four benchmarks should be treated as a direct or final benchmark for CiteClaw.
