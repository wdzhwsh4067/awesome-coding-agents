# Awesome Coding Agents

> A curated list of papers, benchmarks, harness design notes, workflow-native systems, and open-source tools for LLM-based coding agents.

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

Coding agents are moving beyond autocomplete and chat. The interesting action now sits at the intersection of repository context, tool use, verification loops, issue-to-PR workflows, and deployment controls.

This repository tracks that shift with a systems-first lens.

## Why This List Is Different

- It is organized around workflow, evaluation, and system design rather than vendor hype.
- It separates benchmark evidence from product claims and official engineering notes.
- It focuses on repository-scale and workflow-native coding agents, not generic code generation.

## Quick Start

- New to the area: start with [Surveys and Roadmaps](#surveys-and-roadmaps)
- Want the benchmark picture: jump to [Benchmarks and Evaluation](#benchmarks-and-evaluation)
- Care about what actually makes agents work: read [Harness and Repository-Aware Design](#harness-and-repository-aware-design)
- Tracking products and deployment surfaces: see [Workflow-Native Products and Systems](#workflow-native-products-and-systems)
- Looking for tooling: browse [Open-Source Projects](#open-source-projects)

## Contents

- [Surveys and Roadmaps](#surveys-and-roadmaps)
- [Benchmarks and Evaluation](#benchmarks-and-evaluation)
- [Harness and Repository-Aware Design](#harness-and-repository-aware-design)
- [Workflow-Native Products and Systems](#workflow-native-products-and-systems)
- [Open-Source Projects](#open-source-projects)
- [Selected Software Engineering Papers](#selected-software-engineering-papers)
- [Reading Paths](#reading-paths)
- [Contribution Principles](#contribution-principles)
- [Contributing](#contributing)
- [License](#license)

## Surveys and Roadmaps

Foundational overviews for understanding the coding-agent landscape at a high level.

- [AI Agentic Programming: A Survey of Techniques, Challenges, and Opportunities](https://arxiv.org/abs/2508.11126)
  A broad survey of agentic programming patterns, useful for framing planning, tools, memory, and evaluation as reusable components.
- [A Comprehensive Survey on Benchmarks and Solutions in Software Engineering of LLM-Empowered Agentic System](https://arxiv.org/abs/2510.09721)
  A benchmark-heavy map of the emerging software-engineering agent landscape, especially useful as a coverage reference.
- [Agentic Software Engineering: Foundational Pillars and a Research Roadmap](https://arxiv.org/abs/2509.06216)
  A roadmap-style view that helps connect coding agents to larger questions of trust, governance, and engineering practice.

## Benchmarks and Evaluation

Benchmarks are useful, but they often hide scaffold sensitivity, weak tests, contamination, or workflow mismatch.

### Core coding-agent benchmarks

- [SWE-bench: Can Language Models Resolve Real-World GitHub Issues?](https://openreview.net/forum?id=VTF8yNQM66)
  The benchmark that made repository-level issue resolution the center of coding-agent evaluation.
- [SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering](https://proceedings.neurips.cc/paper_files/paper/2024/hash/5a7c947568c1b1328ccc5230172e1e7c-Abstract-Conference.html)
  A landmark paper showing how interface and scaffold design can materially change real-world software task performance.
- [Introducing SWE-bench Verified](https://openai.com/index/introducing-swe-bench-verified/)
  Important for understanding why benchmark curation, underspecification, and flawed tests matter so much.
- [Why SWE-bench Verified No Longer Measures Frontier Coding Capabilities](https://openai.com/index/why-we-no-longer-evaluate-swe-bench-verified/)
  A strong warning that benchmark saturation and evaluation contamination can distort frontier conclusions.
- [SWE-rebench: An Automated Pipeline for Task Collection and Decontaminated Evaluation of Software Engineering Agents](https://openreview.net/forum?id=nMpJoVmRy1)
  Useful for readers interested in fresher, more automated, and more contamination-aware benchmark construction.
- [BigCodeBench: Benchmarking Code Generation with Diverse Function Calls and Complex Instructions](https://openreview.net/forum?id=YrycTjllL0)
  Expands the evaluation picture beyond narrow toy tasks toward more tool-rich programming scenarios.
- [MLE-bench: Evaluating Machine Learning Agents on Machine Learning Engineering](https://openai.com/index/mle-bench/)
  Extends the agent benchmark conversation into ML engineering, where setup and workflow complexity are first-class constraints.

### Evaluation questions worth keeping in mind

- How realistic is the task setup?
- How much does the result depend on the harness or scaffold?
- Are the tests trustworthy, stable, and contamination-resistant?
- Does the benchmark reflect issue-to-PR or CI-coupled work, or just isolated patching?
- Is environment setup part of the problem, or silently abstracted away?

## Harness and Repository-Aware Design

This section covers the substrate that often matters as much as the model itself: retrieval, repo maps, execution setup, monitors, and long-running harness design.

- [RepoCoder: Repository-Level Code Completion Through Iterative Retrieval and Generation](https://aclanthology.org/2023.emnlp-main.151/)
  An early and influential paper showing how retrieval quality can dominate repository-scale code assistance.
- [Repoformer: Selective Retrieval for Repository-Level Code Completion](https://proceedings.mlr.press/v235/wu24a.html)
  A strong reference for selective context construction instead of naïvely stuffing more repository text into the prompt.
- [Repo2Run: Automated Building Executable Environment for Code Repository at Scale](https://openreview.net/forum?id=fZsd3KLMje)
  Especially valuable if you care about the often ignored bottleneck of reconstructing runnable environments.
- [Monitor-Guided Decoding of Code LMs with Static Analysis of Repository Context](https://proceedings.neurips.cc/paper_files/paper/2023/hash/662b1774ba8845fc1fa3d1fc0177ceeb-Abstract-Conference.html)
  Shows how static analysis and monitoring can improve repository-aware generation beyond plain prompting alone.
- [Harness Engineering: Leveraging Codex in an Agent-First World](https://openai.com/index/harness-engineering/)
  A practical systems note on why harness quality, evaluation loops, and task design now matter as much as model choice.
- [Harness Design for Long-Running Application Development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
  A useful engineering perspective on long-running coding tasks, resets, verification, and operational agent reliability.

## Workflow-Native Products and Systems

The product shift is no longer just about generating code. It is about where agents live, what they can touch, and how they participate in software delivery workflows.

### Official docs and product notes

- [About GitHub Copilot Coding Agent](https://docs.github.com/en/copilot/concepts/coding-agent/about-copilot-coding-agent)
  A product-facing doc that shows how GitHub is turning coding assistance into a workflow-native repository surface.
- [Pick Your Agent: Use Claude and Codex on Agent HQ](https://github.blog/news-insights/company-news/pick-your-agent-use-claude-and-codex-on-agent-hq/)
  Helpful for tracking the shift from single assistants toward hosted multi-agent workflows inside GitHub.
- [Claude Code](https://www.anthropic.com/product/claude-code)
  A reference point for terminal-native coding agents that emphasize tool use, patching, and long-horizon task flow.
- [Jules: Build with Your Asynchronous Coding Agent](https://blog.google/innovation-and-ai/models-and-research/google-labs/jules/)
  Useful for understanding asynchronous cloud-executed coding tasks rather than purely interactive assistance.
- [Jules Documentation](https://jules.google/docs/)
  The best place to see how a hosted coding agent is actually framed in terms of user workflow and capabilities.
- [Jules Environment Setup](https://jules.google/docs/environment)
  Worth reading because environment policy and setup constraints often determine practical agent success.
- [Cognition Devin](https://cognition.ai/)
  A high-visibility example of the autonomous software engineer framing in commercial product positioning.
- [Cursor Changelog](https://www.cursor.com/changelog)
  A useful running log of how an editor-native coding product evolves toward more agentic behavior.
- [Windsurf Cascade Overview](https://docs.windsurf.com/windsurf/cascade/cascade)
  A concise product view of agent-assisted editing, context management, and collaborative developer flow.
- [Windsurf Editor Changelog](https://windsurf.com/changelog)
  Good for tracking how agent features arrive incrementally through product iteration rather than one static release.
- [Introducing GPT-5.2-Codex](https://openai.com/index/introducing-gpt-5-2-codex/)
  A model and product update that is most interesting when read as harness and workflow evidence, not just capability marketing.
- [Introducing GPT-5.3-Codex](https://openai.com/index/introducing-gpt-5-3-codex/)
  Another useful checkpoint for how coding systems are described in increasingly agent-first terms.

### Workflow surfaces to watch

- Issue intake and triage
- Repository navigation and retrieval
- Shell and tool execution
- Pull request generation
- Review-thread follow-up
- CI-aware iteration
- Human approval and governed deployment

## Open-Source Projects

If you want to study real tools instead of just papers, these are useful starting points.

- [OpenHands](https://github.com/OpenHands/OpenHands)
  One of the most important open-source references for end-to-end agentic software development workflows.
- [Aider](https://github.com/Aider-AI/aider)
  A practical terminal-first tool that is especially helpful for studying human-in-the-loop agent workflows.
- [py_ralph_frame](https://github.com/rxdt/py_ralph_frame)
  A lightweight spec-driven loop harness for Claude Code, Codex, and Gemini CLI, with fresh-context runs, specs, commits, and verification gates.
- [SWE-bench](https://github.com/SWE-bench/SWE-bench)
  The official benchmark repository, useful for understanding task construction and evaluation mechanics directly.

## Selected Software Engineering Papers

Representative work adjacent to coding agents, with emphasis on repair, testing, verification, and repository-scale software engineering.

### Repository-scale repair and auditing

- [AutoCodeRover: Autonomous Program Improvement](https://2024.issta.org/details/issta-2024-papers/127/AutoCodeRover-Autonomous-Program-Improvement)
  A strong software-engineering reference on autonomous improvement loops rather than one-shot patch generation.
- [RepoAudit: An Autonomous LLM-Agent for Repository-Level Code Auditing](https://openreview.net/forum?id=TXcifVbFpG)
  Useful for seeing how repository-level agents extend beyond repair into auditing and broader quality tasks.
- [A Deep Dive into Large Language Models for Automated Bug Localization and Repair](https://2024.esec-fse.org/details/fse-2024-research-papers/17/A-Deep-Dive-into-Large-Language-Models-for-Automated-Bug-Localization-and-Repair)
  A good grounding paper if you want a more careful SE view of repair strengths, limits, and failure modes.
- [ConDefects: A Complementary Dataset to Address the Data Leakage Concern for LLM-based Fault Localization and Program Repair](https://2024.esec-fse.org/details/fse-2024-demonstrations/20/ConDefects-A-Complementary-Dataset-to-Address-the-Data-Leakage-Concern-for-LLM-based)
  Relevant for readers who want to think seriously about leakage and validity in repair evaluation.

### Testing, verification, and reliability

- [Oracle-Guided Program Selection from Large Language Models](https://2024.issta.org/details/issta-2024-papers/51/Oracle-Guided-Program-Selection-from-Large-Language-Models)
  A useful reminder that verification and candidate selection can matter as much as raw generation quality.
- [UniTSyn: A Large-Scale Dataset Capable of Enhancing the Prowess of Large Language Models for Program Testing](https://2024.issta.org/details/issta-2024-papers/85/UniTSyn-A-Large-Scale-Dataset-Capable-of-Enhancing-the-Prowess-of-Large-Language-Mod)
  Helpful for readers interested in how testing workloads become part of the coding-agent capability stack.
- [Large Language Models for Equivalent Mutant Detection: How Far Are We?](https://2024.issta.org/details/issta-2024-papers/138/Large-Language-Models-for-Equivalent-Mutant-Detection-How-Far-Are-We-)
  A narrower but high-signal example of how LLMs interact with difficult verification and testing subtasks.
- [Towards AI-Assisted Synthesis of Verified Dafny Methods](https://2024.esec-fse.org/details/fse-2024-research-papers/75/Towards-AI-Assisted-Synthesis-of-Verified-Dafny-Methods)
  A useful bridge between coding agents and formal methods, where correctness constraints are explicit.
- [Can Large Language Models Transform Natural Language Intent into Formal Method Postconditions?](https://2024.esec-fse.org/details/fse-2024-research-papers/51/Can-Large-Language-Models-Transform-Natural-Language-Intent-into-Formal-Method-Postco)
  Worth scanning if you want to see how natural-language intent maps into formal verification artifacts.

### Broader software engineering tasks

- [CoderUJB: An Executable and Unified Java Benchmark for Practical Programming Scenarios](https://2024.issta.org/details/issta-2024-papers/11/CoderUJB-An-Executable-and-Unified-Java-Benchmark-for-Practical-Programming-Scenario)
  Broadens the benchmark conversation beyond Python-heavy settings into more practical Java workloads.
- [LPR: Large Language Models-Aided Program Reduction](https://2024.issta.org/details/issta-2024-papers/22/LPR-Large-Language-Models-Aided-Program-Reduction)
  Shows how LLMs can support debugging-adjacent reduction workflows instead of only direct code synthesis.
- [Software Model Evolution with Large Language Models](https://arxiv.org/abs/2406.17651)
  Useful for readers interested in software evolution tasks beyond classic bug-fix benchmarks.
- [Leveraging Large Language Models for the Auto-remediation of Microservice Applications](https://2024.esec-fse.org/details/fse-2024-industry/34/Leveraging-Large-Language-Models-for-the-Auto-remediation-of-Microservice-Application)
  An industry-oriented paper that highlights remediation in distributed systems rather than isolated code snippets.

## Reading Paths

- Benchmark-focused: start with SWE-bench, SWE-agent, SWE-bench Verified, and SWE-rebench.
- Systems-focused: read RepoCoder, Repoformer, Repo2Run, and the harness design write-ups.
- Product-focused: compare GitHub Agent HQ, Claude Code, Jules, Codex, Cursor, Windsurf, OpenHands, and Aider.
- SE-impact-focused: focus on evaluation realism, repository legibility, review loops, CI integration, and deployment controls.

## Contribution Principles

- Prefer primary sources over summaries.
- Distinguish benchmark evidence from product claims.
- Prefer stable links to papers, docs, and official repositories.
- Keep annotations short, factual, and easy to scan.
- Avoid hype when a more precise description is available.

## Contributing

Suggestions and pull requests are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)
