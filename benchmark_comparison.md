# Benchmark Comparison

This document provides a more detailed, per-benchmark comparison than the top-level README. All
statements are based on the documentation inside the fetched folders; uncertain details are
phrased cautiously.

The first part compares the four included benchmarks (AutoResearchBench, LitSearch, PaSa,
ScholarQuest). For a single consolidated categorisation of these four by task, input/output,
corpus, and evaluation style, see [`benchmark_taxonomy.md`](benchmark_taxonomy.md). The
[Broader Benchmark Landscape](#broader-benchmark-landscape) section at the end surveys
additional, adjacent benchmarks, datasets, and systems that were encountered during scouting
but are not bundled as folders in this repository.

## Overview Table

| Benchmark | Original focus | Domain coverage | Input format | Output format | Evaluation style | Strength | Limitation | Typical use as an evaluation reference |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **AutoResearchBench** | Autonomous scientific literature discovery (Deep + Wide research) | Scientific literature, appears multi-domain | Research question / condition description | Single target paper (Deep) or paper set (Wide), via a multi-step process | Exact target match (Deep) and set-overlap / IoU (Wide); appears to use model-based judging | Captures multi-step, open-ended agentic search; challenging | Obfuscated release; requires search backends and API keys; low baselines | Reference for evaluating broader research workflows and process quality |
| **LitSearch** | Retrieval benchmark for scientific literature search | Recent ML and NLP papers | Natural-language query | Ranked papers / gold paper IDs over a fixed corpus | Standard retrieval/ranking against gold paper IDs | Clean, reproducible, fixed corpus | Narrow domain; closed corpus; not agentic | Reference for basic query-to-paper retrieval testing |
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
- **None directly covers seed-conditioned literature expansion** without adaptation. In
  particular, none is conditioned on seed papers plus an existing corpus, and none directly
  measures the usefulness of *newly discovered* papers relative to a starting set.

## Broader Benchmark Landscape

Beyond the four bundled benchmarks, scouting surfaced a wider set of related benchmarks,
datasets, and systems. These are recorded here for landscape context. They are **not** bundled
as folders in this repository, and they are listed to map nearby evaluation settings rather than
to endorse any of them. All are best viewed as adjacent resources. Links point to upstream
sources; the descriptions summarise publicly reported details and may need manual verification
before reuse.

### Automated Boolean Query Generation for Literature Search

This line of work generates or refines structured (Boolean) search queries, most often for
systematic-review retrieval. It is adjacent to the query-generation step of an expansion
pipeline, though it is concentrated in the systematic-review setting.

| Work / line | Link | Core task | Input | Output | Dataset / benchmark used | Evaluation |
|---|---|---|---|---|---|---|
| Automatic Boolean Query Refinement | [ACM WWW 2019](https://dl.acm.org/doi/10.1145/3308558.3313544) | Improve an existing Boolean query | Initial expert or generated Boolean query | Refined Boolean query | [CLEF TAR 2017](https://ceur-ws.org/Vol-1866/invited_paper_12.pdf); CLEF TAR 2018 | Maintain recall while improving precision or reducing retrieved set size |
| Automatic Boolean Query Formulation for Systematic Review Literature Search | [ACM WWW 2020](https://dl.acm.org/doi/10.1145/3366423.3380185) | Generate Boolean queries for systematic reviews | Review protocol / title / objective / PICO-like information | Boolean query | CLEF TAR 2018 | Recall, precision, F-score, number of retrieved records |
| Query variation sampling + learning to rank | [ACM WWW 2020](https://dl.acm.org/doi/10.1145/3366423.3380075) | Generate multiple query variants and rank them | Review topic / candidate query variants | Ranked Boolean queries | CLEF TAR 2017; CLEF TAR 2018 | Select better-performing query variants |
| searchrefiner / query visualisation tools | [ACM CIKM 2018](https://dl.acm.org/doi/abs/10.1145/3269206.3269215) | Help human experts inspect Boolean queries | Boolean query + validation citations | Visualised query clauses and retrieved citations | CLEF TAR 2017; CLEF TAR 2018 | User/tool-assistance evaluation |
| Computational approach for objectively derived search strategies | [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC7148214/) / [ECIR 2020 accepted paper listing](https://ecir2020.org/accepted-papers/) | Derive systematic search strategies computationally | Review objective / protocol | Search strategy | CLEF TAR 2018 | Retrieval effectiveness versus expert strategies |
| ChatGPT Boolean Query Generation, SIGIR 2023 | [arXiv](https://arxiv.org/abs/2302.03495) / [ACM SIGIR 2023](https://dl.acm.org/doi/10.1145/3539618.3591703) | Prompt LLMs to write Boolean queries | Systematic review title/objective; sometimes guided examples | Boolean query | CLEF TAR 2017; CLEF TAR 2018; Seed Collection | Precision/recall trade-off; LLM queries often high precision but lower recall |
| Reassessing LLM Boolean Query Generation, 2025 | [arXiv](https://arxiv.org/abs/2505.07155) | Reproduce and stress-test LLM Boolean query generation | Review topics, prompts, formatting constraints, seed examples | Boolean query | CLEF TAR 2017; CLEF TAR 2018; Seed Collection | Query effectiveness under different prompts/models; reproducibility |
| Reproducibility and Generalizability Study of LLMs for Query Generation | [arXiv](https://arxiv.org/abs/2411.14914) | Reproduce and extend LLM Boolean query generation studies | Review topic + LLM prompt | Boolean query | CLEF TAR 2017; CLEF TAR 2018; Seed Collection | Replicability, reliability, failure analysis, comparison across ChatGPT and open-source models |
| Literature Search Sandbox / fine-tuned LLM query generation | [JAMIA Open](https://academic.oup.com/jamiaopen/article/7/3/ooae098/7775509) / [PubMed](https://pubmed.ncbi.nlm.nih.gov/39323560/) | Fine-tune LLM to generate search strategies | Review title / key question / description | Boolean search string | Literature Search Sandbox dataset | Query-generation quality, retrieval usefulness |
| AutoBool, 2026 | [arXiv](https://arxiv.org/abs/2602.00005) / [ACL Anthology](https://aclanthology.org/2026.eacl-long.68/) / [GitHub](https://github.com/ielab/AutoBool) | RL-trained LLM for Boolean query generation | Review topic | Boolean query | AutoBool-65K; CLEF TAR; Seed Collection | Retrieval measures directly optimized; reports outperforming zero/few-shot prompting and retrieving fewer documents than expert-like baselines |
| Adaptive search query generation and refinement in systematic literature review | [Information Systems](https://doi.org/10.1016/j.is.2023.102231) / [Institution page](https://www.hsbi.de/publikationsserver/record/3334) | Adaptive query generation and refinement for SLR search | SLR topic / search context | Search query / refined query | Paper-specific SLR dataset; exact public benchmark name not clearly stated | Retrieval effectiveness and refinement performance |
| Automated MeSH Term Suggestion for Effective Query Formulation in Systematic Reviews Literature Search | [arXiv](https://arxiv.org/abs/2209.08687) | Suggest MeSH terms to improve systematic review Boolean queries | Initial Boolean query with free-text terms | Suggested MeSH terms / expanded Boolean query | CLEF TAR 2017; CLEF TAR 2018; Seed Collection | Retrieval effectiveness before/after MeSH expansion |
| Generating Natural Language Queries for More Effective Systematic Review Screening Prioritisation | [PDF](https://ielab.io/publications/pdfs/shuai2024sigirapgenerating.pdf) | Generate natural-language queries for systematic review screening/ranking | Review title / Boolean query / topic information | Natural-language query | CLEF 2019 DTA; CLEF 2019 Intervention; Seed Collection | Screening prioritisation / retrieval effectiveness |
| SR4CS: Systematic Reviews in Computer Science | [arXiv](https://arxiv.org/html/2604.16330v1) / [CEUR PDF](https://ceur-ws.org/Vol-4187/short-07.pdf) | Dataset for Boolean query generation and screening in CS systematic reviews | CS systematic review topics | Expert-like Boolean queries / retrieved studies / screening labels | SR4CS | Boolean query generation, retrieval paradigms, screening behaviour |

### Adjacent Benchmarks and Datasets for Literature Search and Review

These benchmarks and datasets cover retrieval, screening, and scientific QA. Several are
concentrated in the biomedical or systematic-review setting, and the task formulation generally
differs from seed-paper-conditioned expansion; they are useful primarily as reference points.

| Benchmark / dataset | Link | Domain coverage | Reported details | Input | Output / label | Main evaluated task | Notes |
|---|---|---|---|---|---|---|---|
| CLEF TAR 2017 | [CEUR overview PDF](https://ceur-ws.org/Vol-1866/invited_paper_12.pdf) / [CLEF-TAR GitHub](https://github.com/CLEF-TAR/tar) | Biomedical / empirical medicine; Diagnostic Test Accuracy systematic reviews | 50 DTA systematic review topics; 20 development topics + 30 test topics; topic files include title/query/PIDs; relevance judgments at abstract and full-text levels | Review topic, original Boolean query, PubMed records | Relevant / irrelevant article judgments; ranked retrieval outputs for evaluation | Technology-assisted review, high-recall retrieval, title/abstract screening | Established benchmark for biomedical systematic-review retrieval; domain-specific and focused on DTA reviews |
| CLEF TAR 2018 | [CEUR overview PDF](https://ceur-ws.org/Vol-2125/invited_paper_6.pdf) / [CLEF-TAR GitHub](https://github.com/CLEF-TAR/tar) | Biomedical / empirical medicine; Diagnostic Test Accuracy systematic reviews | Additional DTA systematic review topics beyond CLEF 2017; commonly used together with CLEF TAR 2017 in Boolean query generation and TAR studies | Review topic, original Boolean query, PubMed records | Relevance judgments and ranked retrieval outputs | Protocol-driven retrieval and screening prioritisation | Still DTA-focused; useful for query generation / screening |
| CLEF 2019 DTA | [CLEF eHealth 2019 Task 2](https://clefehealth.imag.fr/clefehealth.imag.fr/index1833.html?page_id=173) / [CEUR overview PDF](https://ceur-ws.org/Vol-2380/paper_250.pdf) | Biomedical / empirical medicine; Diagnostic Test Accuracy reviews | 2019 expands beyond previous DTA-only setting; DTA category builds on earlier CLEF TAR DTA topics and includes new DTA testing topics; broader CLEF TAR collection reports 80 DTA reviews in total | Review topic, Cochrane Boolean query, PubMed/MEDLINE retrieved records | Relevance labels for studies; ranked results for TAR evaluation | High-recall retrieval and screening prioritisation for DTA reviews | Continuity with 2017/2018; biomedical and review-protocol-based |
| CLEF 2019 Intervention | [CLEF eHealth 2019 Task 2](https://clefehealth.imag.fr/clefehealth.imag.fr/index1833.html?page_id=173) / [CEUR overview PDF](https://ceur-ws.org/Vol-2380/paper_250.pdf) | Biomedical / empirical medicine; Intervention systematic reviews | CLEF 2019 added Intervention reviews; reported collection includes 40 Intervention reviews overall; task page indicates the 2019 collection mixes DTA and Intervention topics | Review topic, Cochrane Boolean query, PubMed/MEDLINE retrieved records | Relevance labels for studies; ranked results for screening/retrieval evaluation | TAR retrieval and screening for intervention reviews | Common SR type; clinical / systematic-review-specific |
| Seed Collection | [arXiv](https://arxiv.org/abs/2204.03096) / [GitHub](https://github.com/ielab/sysrev-seed-collection) | Medical systematic reviews | 40 medical systematic review topics; each topic includes title, description, date restrictions, PubMed Boolean query, real seed studies, included studies, retrieved studies, and snowballed studies | Review topic + real seed studies + PubMed query | Included studies, retrieved studies, snowballed studies, seed-study metadata | Seed-study-based retrieval, query formulation, screening prioritisation, citation chasing | Among the closest to seed-paper search; medical and systematic-review-specific |
| AutoBool-65K | [arXiv](https://arxiv.org/abs/2602.00005) / [GitHub](https://github.com/ielab/AutoBool) | Medical systematic review search | 65,588 systematic review topics created for RL-based Boolean query generation; evaluated together with CLEF TAR and Seed Collection | Review topic | Generated Boolean query; retrieval results; no need for gold target query during RL optimisation | Automatic Boolean query generation optimised directly with retrieval metrics | Large and relevant for Boolean query generation; medical-SR-oriented |
| SR4CS | [arXiv](https://arxiv.org/html/2604.16330v1) / [CEUR PDF](https://ceur-ws.org/Vol-4187/short-07.pdf) / [Zenodo](https://doi.org/10.5281/zenodo.17163932) / [GitHub](https://github.com/webis-de/scolia26-sr4cs) | Computer science systematic reviews | 1,212 systematic reviews; 104,316 resolved references; 89,447 references with abstracts; includes original expert-designed Boolean queries and normalized approximated title/abstract queries | CS systematic review title/objective + reported Boolean query + reference pool | Curated reference pools; approximated expert Boolean queries; metadata such as objectives, inclusion/exclusion criteria, databases, temporal constraints | Boolean query generation, retrieval paradigm comparison, screening behaviour | Moves beyond medicine; CS-only and systematic-review-framed |
| Literature Search Sandbox dataset | [JAMIA Open](https://academic.oup.com/jamiaopen/article/7/3/ooae098/7775509) / [PubMed](https://pubmed.ncbi.nlm.nih.gov/39323560/) | Medical / health systematic reviews | 10,346 natural-language review descriptions paired with Boolean searches; evaluation reported on 57 systematic reviews with librarian assessment | Review title, key question, or natural-language review description | Generated Boolean search query | Fine-tuned LLM query generation from review descriptions to Boolean searches | Supervised query-generation resource; requires paired review-description-to-query data; SR/health setting |
| SIGIR 2017 SysRev Query Collection | [GitHub](https://github.com/ielab/SIGIR2017-SysRev-Collection) | Biomedical systematic reviews | 94 Cochrane reviews; based on large MEDLINE reference pool; used for systematic review retrieval and screening experiments | Systematic review topic / query | Relevant and irrelevant references mapped to MEDLINE identifiers | Retrieval and screening prioritisation | Historical SR retrieval benchmark; biomedical and not seed-paper-focused |
| CSMeD / systematic-review screening datasets | [GitHub](https://github.com/WojciechKusa/systematic-review-datasets) | Software engineering / CS / mixed systematic review screening datasets | Meta-dataset of systematic review screening collections; candidate studies are already retrieved | Already retrieved candidate studies | Include / exclude labels | Citation screening | Evaluates screening after retrieval, not upstream search expansion |
| ASReview / SYNERGY-style datasets | [ASReview](https://asreview.nl/) / [ASReview GitHub](https://github.com/asreview/asreview) / [SYNERGY dataset](https://github.com/asreview/synergy-dataset) | Systematic review screening collections | Labelled candidate records for active-learning screening simulations | Candidate citation records | Relevant / irrelevant screening labels | Active-learning screening and stopping | Screening-focused rather than a search-strategy benchmark |
| ScholarQABench / OpenScholar | [Nature](https://www.nature.com/articles/s41586-025-10072-4) / [arXiv](https://arxiv.org/html/2411.14199v1) | Multi-domain scientific literature: CS, physics, neuroscience, biomedicine | Expert-written scientific questions and long-form reference answers | Scientific question | Long-form answer + citations | Scientific QA and literature synthesis | Multi-domain; evaluates answer quality rather than paper-list discovery |
| LitQA / PaperQA | [arXiv](https://arxiv.org/abs/2312.07559) / [OpenReview](https://openreview.net/forum?id=clU5xWyItb) / [GitHub](https://github.com/Future-House/paper-qa) | Scientific QA over papers | Question-answer benchmark requiring retrieval and synthesis from papers | Natural-language scientific question | Answer with cited evidence | Retrieval-augmented scientific QA | Tests answer correctness after retrieval rather than completeness of a paper set |
| ScholarQuest | [arXiv paper](https://arxiv.org/pdf/2606.20235) | Scholarly paper search / literature QA; domain coverage depends on construction | Query-oriented scholarly discovery benchmark | Query or paper-seeking question | Target paper(s), paper list, or answer depending on task design | Paper finding / literature QA | Bundled in this repository; CS/arXiv-oriented depending on construction |
| LitSearch | [arXiv](https://arxiv.org/abs/2407.18940) / [GitHub](https://github.com/princeton-nlp/LitSearch) | Primarily CS / arXiv-oriented literature search | Query set and retrieval corpus for literature search | Literature search query | Relevant papers | Literature search / paper retrieval | Bundled in this repository; arXiv-heavy domain |
| Citation graph / related-paper recommendation datasets | [S2ORC](https://allenai.org/data/s2orc) / [OpenAlex](https://openalex.org/) | Paper graph or citation network | Seed paper or paper graph context | Related papers / citations | Recommendation, citation prediction, related-paper discovery | Tests graph expansion rather than explicit search-query generation |

### Related Systems and Products

These are deployed tools and research systems that touch literature search, discovery,
screening, or synthesis. Most report product-facing rather than benchmark-style evaluation, so
public evidence varies. They are included to map the surrounding ecosystem.

| System / product | Link | Category | Main output | Evaluation style / public evidence | Notes |
|---|---|---|---|---|---|
| Elicit | [Official](https://elicit.com/) / [Systematic review evaluation](https://elicit.com/blog/how-we-evaluated-elicit-systematic-review) | AI literature review assistant | Paper search results, evidence tables, summaries, extracted data | Product-facing evaluation of search, screening, extraction, and systematic-review workflow accuracy | Structured literature-review workflow |
| Consensus | [Official](https://consensus.app/) / [OpenAI case study](https://openai.com/index/consensus/) | Evidence-based academic search / synthesis | Evidence-backed answer, paper summaries | Public material emphasises academic search and answer synthesis over large scholarly corpora | Scientific answer engine |
| Scite | [Official](https://scite.ai/) / [Scite paper](https://direct.mit.edu/qss/article/2/3/882/102990/scite-A-smart-citation-index-that-displays-the) | Citation-context analysis | Citation classified as supporting, contrasting, or mentioning | Original Scite work evaluates citation-statement classification at scale | Citation relation / claim support |
| ResearchRabbit | [Official](https://www.researchrabbit.ai/) | Citation graph exploration | Related-paper graph, collections, alerts | Mainly product/user-facing; related papers, citation maps, research trends | Snowballing from seed papers |
| Litmaps | [Official](https://www.litmaps.com/) | Citation graph / literature map | Literature map, related papers, monitoring | Product-oriented; compared as a citation-network discovery tool | Paper-neighbourhood exploration |
| Connected Papers | [Official](https://www.connectedpapers.com/) | Graph-based paper discovery | Visual graph of related papers | Product-facing; limited public recall/coverage benchmark | Visual related-work exploration |
| Semantic Scholar | [Official](https://www.semanticscholar.org/) / [API](https://www.semanticscholar.org/product/api) | Academic search engine | Ranked paper results, semantic search, paper metadata | Large-scale scholarly search infrastructure and API-backed retrieval | General-purpose scholarly search baseline |
| OpenAlex | [Official](https://openalex.org/) / [API docs](https://docs.openalex.org/) | Open scholarly metadata/search infrastructure | Paper metadata, authors, venues, concepts, citation graph | Public scholarly index and API; used as retrieval/database infrastructure | Open backend for large-scale retrieval and metadata expansion |
| Google Scholar | [Official](https://scholar.google.com/) | General scholarly search engine | Ranked scholarly search results | Widely used manually; limited API/accessibility and opaque ranking | Real-world baseline for human literature search |
| PubMed | [Official](https://pubmed.ncbi.nlm.nih.gov/) / [PubMed API](https://www.ncbi.nlm.nih.gov/books/NBK25501/) | Biomedical literature search engine | Biomedical paper records | Standard backend for medical/systematic-review retrieval; supports Boolean search | Domain-specific search baseline for biomedical topics |
| arXiv | [Official](https://arxiv.org/) / [API](https://info.arxiv.org/help/api/index.html) | Preprint search / scholarly repository | Preprint records | Often used for CS/AI benchmark construction and retrieval tasks | Backend for AI/CS and physics preprints |
| Semantic Reader / Allen AI tools | [Semantic Reader](https://www.semanticscholar.org/product/semantic-reader) / [Ai2](https://allenai.org/) | Paper reading and scholarly tooling | Enhanced paper reading, citations, related-work support | Product/research infrastructure around scholarly reading and retrieval | Adjacent infrastructure for reading and citation navigation |
| Rayyan | [Official](https://www.rayyan.ai/) | Systematic review screening platform | Screening decisions, collaboration workflow, deduplication/PICO assistance | Commonly evaluated around title/abstract screening efficiency and review workflow support | Downstream review workflow |
| Covidence | [Official](https://www.covidence.org/) | Systematic review workflow platform | Screening, extraction, PRISMA-style review workflow | Evaluated/deployed around evidence synthesis workflow, screening, and extraction | Review-management system |
| ASReview | [Official](https://asreview.nl/) / [GitHub](https://github.com/asreview/asreview) | Active-learning screening | Prioritised screening order | Evaluated by simulation on labelled screening datasets | Reduces screening burden |
| RobotReviewer | [Official](https://www.robotreviewer.net/) / [Paper](https://www.jmir.org/2016/4/e102/) | Systematic review automation / risk-of-bias assistance | Risk-of-bias assessment, PICO extraction, evidence tables | Evaluated on SR automation tasks such as bias assessment and information extraction | Automation of evidence assessment after papers are identified |
| Abstrackr | [Official](http://abstrackr.cebm.brown.edu/) / [Paper](https://pubmed.ncbi.nlm.nih.gov/23937834/) | Semi-automated citation screening | Prioritised abstracts and screening predictions | Evaluated for reducing abstract-screening workload in systematic reviews | Classic screening baseline |
| EPPI-Reviewer | [Official](https://eppi.ioe.ac.uk/cms/Default.aspx?tabid=2914) | Systematic review management / evidence synthesis | Screening, coding, synthesis workflow | Used in evidence synthesis workflows; supports machine-learning-assisted reviewing | Evidence synthesis workflow system |
| DistillerSR | [Official](https://www.distillersr.com/) | Systematic review automation platform | Screening, extraction, audit trails, review management | Product-facing evaluation around review automation and efficiency | Enterprise systematic-review workflow tool |
| PaperQA / PaperQA2 | [GitHub](https://github.com/Future-House/paper-qa) / [Paper](https://arxiv.org/abs/2312.07559) | Retrieval-augmented scientific QA | Answer with citations | Evaluated on scientific QA benchmarks such as LitQA | Grounded scientific answering |
| OpenScholar | [Nature](https://www.nature.com/articles/s41586-025-10072-4) / [arXiv](https://arxiv.org/html/2411.14199v1) | Scientific literature synthesis | Long-form answer with citations | Evaluated on multi-domain scientific QA / synthesis benchmarks | Synthesis and attribution |
| Ai2 Scholar QA | [Official](https://scholarqa.allen.ai/) / [arXiv](https://arxiv.org/abs/2504.10861) | Scientific QA assistant | Organised answer with scholarly citations | Evaluated as scientific QA / literature synthesis | Adjacent system |
| Perplexity / academic search mode | [Official](https://www.perplexity.ai/) | General AI search / answer engine | Web-backed answer with citations | Product-facing; evaluated by answer usefulness and citation grounding | Mainstream AI search comparator |
| SciSpace | [Official](https://scispace.com/) | AI paper search, reading, and writing assistant | Paper summaries, explanations, related papers, writing support | Product-facing; focuses on paper understanding and writing assistance | Reading and comprehension workflows |
| Scholarcy | [Official](https://www.scholarcy.com/) | Paper summarisation / reading assistant | Flashcards, summaries, key points | Product-facing; usefulness for reading and summarising papers | Faster paper processing |
| Iris.ai | [Official](https://iris.ai/) | AI research discovery and extraction | Literature maps, extraction, RSpace-style research workflows | Product-facing; discovery, mapping, and extraction | Literature discovery product |
| Undermind | [Official](https://www.undermind.ai/) | AI scientific discovery / literature search assistant | Search results and literature discovery support | Product-facing; emphasises deeper scientific search/discovery assistance | Close comparator for literature discovery |
| PapersFlow | [Official](https://papersflow.com/) | AI literature review / paper management assistant | Search, summaries, paper organisation | Product-facing | Market comparator |
| ResearchPilot | [arXiv](https://arxiv.org/abs/2603.14629) | Multi-agent literature synthesis / related-work drafting | Related-work draft, synthesis report | Often evaluated with local end-to-end runs, qualitative or task-completion criteria | Feasibility of literature-review agents |
| STORM | [Paper](https://arxiv.org/abs/2402.14207) / [GitHub](https://github.com/stanford-oval/storm) | Long-form report generation from web search | Wikipedia-style article / report | Evaluated on long-form generation, outline quality, citation quality, and human preference | Search-augmented writing |
| AI Scientist-style systems | [AI Scientist paper](https://arxiv.org/abs/2408.06292) | Autonomous scientific ideation / experimentation | Research ideas, experiments, papers | Evaluated by generated research workflows and paper-like outputs | Broader automation of the research process |

> Several rows above reference works with dates or identifiers that may postdate routine
> verification (for example, items labelled 2025/2026). Treat links and reported statistics as
> provisional and confirm against the upstream sources before reuse.
