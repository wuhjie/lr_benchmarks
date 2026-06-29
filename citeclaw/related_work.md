# Related Work

## Literature Review

| Work | Area | Main focus | Relation to CiteClaw | Gap / limitation relative to CiteClaw |
|---|---|---|---|---|
| [OpenScholar](https://www.nature.com/articles/s41586-025-10072-4) | Scientific RAG | Retrieval-augmented scientific QA with citation-backed answers | Strong comparison for literature-grounded answer generation | Final output is an answer/synthesis, while CiteClaw targets paper-set expansion and search trace |
| [PaperQA](https://arxiv.org/abs/2312.07559) | Scientific RAG | RAG agent for answering questions over scientific papers | Related agentic retrieval and source assessment | Optimized for QA over literature, not explicit search-strategy evolution |
| [PaperQA2](https://github.com/Future-House/paper-qa) | Scientific RAG | Agentic RAG over scientific papers | Related to tool-using scientific literature agents | Focuses on answering questions and summarizing evidence rather than constructing a reproducible search process |
| [Automatic Boolean Query Refinement for Systematic Review Literature Search](https://dl.acm.org/doi/10.1145/3308558.3313544) | Boolean query refinement | Automatic refinement of Boolean queries | Very close to ExpandBySearch | Focuses on refining systematic-review queries, not a broader agentic discovery loop |
| [A Comparison of Automatic Boolean Query Formulation for Systematic Reviews](https://link.springer.com/article/10.1007/s10791-020-09381-1) | Boolean query generation | Comparing automatic Boolean query formulation methods | Useful background for search-string generation | Evaluation is query-focused rather than system-level literature discovery |
| [Reassessing Large Language Model Boolean Query Generation for Systematic Reviews](https://arxiv.org/html/2505.07155v2) | LLM Boolean query generation | Evaluation of LLM-generated Boolean search strings | Important modern related work | Still centered on query quality, not full literature-expansion workflows |
| [Rocchio Relevance Feedback](https://en.wikipedia.org/wiki/Rocchio_algorithm) | Query refinement / IR | Classical relevance-feedback query refinement | Conceptual foundation for feedback-based search | General IR method, not specialized for scholarly discovery or concept-block reasoning |
| [Conversational Information Seeking](https://doi.org/10.1561/1500000066) | Conversational search | Multi-turn search interaction | Related to iterative clarification and retrieval | Dialogue-centric, not necessarily focused on literature corpus construction |
| [Local Citation Recommendation](https://dl.acm.org/doi/10.1145/2806416.2806494) | Citation recommendation | Recommending citations for a manuscript context | Related to finding relevant papers | Manuscript-centric rather than topic/corpus-centric |
| [Global Citation Recommendation](https://dl.acm.org/doi/10.1145/3077136.3080740) | Citation recommendation | Recommending citations from global context | Related to paper recommendation | Optimizes citation insertion, not literature coverage |
| [The AI Scientist](https://arxiv.org/abs/2408.06292) | Scientific agents | Automated scientific discovery pipeline | Related to agentic research systems | Literature search is only one part of a broader autonomous science pipeline |
| [SciToolAgent](https://arxiv.org/abs/2402.11444) | Scientific agents | Tool-using scientific agents | Related to tool-augmented research workflows | General scientific tool use rather than literature expansion specifically |
| [PRISMA 2020 Statement](https://www.prisma-statement.org/) | Evidence synthesis methodology | Reporting standard for systematic reviews | Important for auditability and reproducibility | Human reporting guideline, not an automated discovery system |
| [Cochrane Handbook](https://training.cochrane.org/handbook) | Evidence synthesis methodology | Methodological guide for systematic reviews | Useful rigor standard for search documentation | Manual methodology rather than agentic implementation |
| [LitSearch](https://github.com/princeton-nlp/LitSearch) | Literature retrieval benchmark | Literature search benchmark | Useful evaluation background | Benchmark, not the main related-work comparison for CiteClaw |
| [ScholarQuest](https://arxiv.org/pdf/2606.20235) | Literature retrieval benchmark | Scholarly retrieval / research benchmark | Useful evaluation context | Benchmark-oriented and not the same as CiteClaw’s system contribution |
| [AutoResearchBench](https://github.com/CherYou/AutoResearchBench) | Research-agent benchmark | Benchmarking research-agent abilities | Related background for research agents | Benchmark-oriented, not a system for iterative literature discovery |



## Commercial / Public Systems

| System / Product | Area | Main focus | Relation to CiteClaw | Gap / limitation relative to CiteClaw |
|---|---|---|---|---|
| [Google Scholar](https://scholar.google.com/) | Academic search engine | General academic search | Basic infrastructure for finding papers | Relies heavily on user-written queries; limited support for iterative search planning |
| [Semantic Scholar](https://www.semanticscholar.org/) | Academic search engine | Semantic scholarly search and citation metadata | Useful retrieval backend / comparison system | Strong search engine, but not designed as an auditable search-refinement agent |
| [OpenAlex](https://openalex.org/) | Scholarly metadata graph | Open scholarly metadata and citation graph | Useful source for metadata, citation links, venues, authors | Infrastructure rather than an end-to-end literature discovery workflow |
| [PubMed](https://pubmed.ncbi.nlm.nih.gov/) | Academic search engine | Biomedical literature search | Important source for systematic and medical literature retrieval | Requires carefully designed search strings; discovery logic remains user-driven |
| [Crossref](https://www.crossref.org/) | Scholarly metadata infrastructure | DOI and publication metadata | Useful for metadata normalization | Infrastructure, not literature discovery logic |
| [Semantic Scholar API](https://api.semanticscholar.org/api-docs/) | Scholarly API | Paper metadata, citations, recommendations | Useful retrieval and citation source | API/backend rather than complete discovery agent |
| [Elicit](https://elicit.com/) | AI literature review assistant | AI-assisted paper search, screening, extraction, and review generation | Closest product-level comparison for literature-review support | More focused on search, extraction, and synthesis than transparent iterative corpus expansion |
| [SciSpace](https://typeset.io/) | AI literature review assistant | Paper search, explanation, and AI copilot for reading papers | Related to AI-assisted literature understanding | More focused on reading/summarizing papers than search-strategy refinement |
| [Consensus](https://consensus.app/) | AI literature review assistant | Evidence-oriented academic search and scientific QA | Related to natural-language evidence retrieval | Optimized for answering questions, not building an auditable paper set |
| [Scholarcy](https://www.scholarcy.com/) | AI literature review assistant | Paper summarization and reading support | Useful comparison for downstream paper understanding | Does not mainly address discovery or iterative paper expansion |
| [Iris.ai](https://iris.ai/) | AI literature discovery assistant | AI-assisted research discovery and literature mapping | Related to exploratory literature search | Search process and expansion rationale are not the main research artifact |
| [Rayyan](https://www.rayyan.ai/) | Systematic review tool | Screening and collaboration for systematic reviews | Related to systematic review workflow | Works mainly after candidate papers have already been retrieved |
| [ASReview](https://asreview.nl/) | Systematic review tool | Active-learning-assisted screening | Relevant to reducing screening workload | Optimizes screening, not the upstream search-query generation process |
| [Covidence](https://www.covidence.org/) | Systematic review tool | Systematic review management | Related to review workflow infrastructure | Assumes search results already exist; not focused on search expansion |
| [EPPI-Reviewer](https://eppi.ioe.ac.uk/cms/Default.aspx?alias=eppi.ioe.ac.uk/cms/er4) | Evidence synthesis tool | Evidence synthesis and review management | Related to structured review methodology | More workflow/tooling oriented than agentic literature discovery |
| [ResearchRabbit](https://www.researchrabbit.ai/) | Citation-based discovery | Citation-based literature discovery and mapping | Strong comparison for seed-paper expansion | Recommendation and visualization are strong, but search strategy is less explicit |
| [Connected Papers](https://www.connectedpapers.com/) | Citation-based discovery | Visual graph of related papers | Related to citation-network exploration | Useful for exploration, but less suitable for reproducible search traces |
| [Litmaps](https://www.litmaps.com/) | Citation-based discovery | Citation-network discovery, visualization, and monitoring | Related to paper-set expansion from known papers | Discovery is graph/recommendation driven rather than query-diagnosis driven |
| [Inciteful](https://inciteful.xyz/) | Citation-based discovery | Citation graph exploration | Related to snowballing and citation expansion | Limited emphasis on Boolean query generation and iterative retrieval feedback |
| [VOSviewer](https://www.vosviewer.com/) | Literature mapping | Bibliometric visualization and science mapping | Useful for analyzing a collected corpus | Mainly post-hoc analysis, not active paper discovery |
| [CiteSpace](https://citespace.podia.com/) | Literature mapping | Citation and knowledge-domain visualization | Related to research-field mapping | Focuses on visualization/analysis after retrieval |
| [Bibliometrix](https://www.bibliometrix.org/) | Literature mapping | Bibliometric analysis in R | Useful for corpus-level analysis | Not designed as an autonomous search/refinement system |