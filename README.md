LR_BENCHMARKS

Overview

This repository is an internal benchmark scouting note for CiteClaw-related literature retrieval benchmarks.

It collects four existing benchmarks that are adjacent to literature retrieval, academic paper search, scholarly discovery, and research-agent evaluation:

* AutoResearchBench
* LitSearch
* PaSa
* ScholarQuest

The purpose of this repository is not to propose a new benchmark, and these benchmarks should not be treated as direct CiteClaw evaluation benchmarks. Instead, this repo records what has been checked, how these benchmarks differ, and why they only partially match the CiteClaw setting.

Repository Structure

LR_BENCHMARKS/
├── autoresearch/        # AutoResearchBench
├── litsearch-dataset/   # LitSearch dataset
├── pasa-dataset/        # PaSa dataset
└── scholarquest/        # ScholarQuest

Each folder contains a fetched copy of the corresponding benchmark repository or dataset. The folders are kept close to their upstream versions.

Top-level notes:

* benchmark_taxonomy.md: task-type and input/output taxonomy.
* benchmark_comparison.md: detailed comparison across benchmarks.

Benchmark Summary

Benchmark	Main focus	Typical input	Typical output	Main limitation for CiteClaw
AutoResearchBench	Autonomous research-agent evaluation	Research question / condition	Target paper or paper set	More agent-task oriented than clean literature expansion
LitSearch	Query-to-paper retrieval	Natural-language query	Ranked papers / gold paper IDs	Mostly ML/NLP and closed-corpus retrieval
PaSa	Comprehensive academic paper search	Scholarly search query	Relevant paper set	Closer to paper search, but still not CiteClaw-style seed-paper expansion
ScholarQuest	Paper-search agent / set retrieval	Scholarly paper-search query	Relevant arXiv IDs	CS/arXiv-heavy and dependent on external search API

Why This Repo Exists

These benchmarks are grouped together because they represent nearby evaluation settings for literature search, paper retrieval, and research agents. However, they test different things:

* LitSearch is closer to query-to-paper retrieval.
* PaSa and ScholarQuest are closer to academic paper-search agents.
* AutoResearchBench is closer to autonomous research-agent evaluation.

This helps clarify that “literature search benchmark” can mean several different tasks.

The four benchmarks here are related, but none directly evaluates this full setting.

Main gaps:

* limited support for seed-paper-conditioned search;
* limited corpus-aware expansion;
* many tasks are CS/ML/NLP or arXiv-heavy;
* most benchmarks focus on retrieval, paper-set search, or research-agent tasks rather than iterative literature expansion.
