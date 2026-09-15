---
layout: project
title: A.R.C.H.O.N.
status: Active — private R&D
summary: A multi-agent orchestration system built around a biomimetic safety architecture.
---

A multi-agent orchestration system: a supervising agent coordinates bounded, single-function "Nano-AI" processes under hard safety limits. The goal was never another chatbot — it's a system that reasons, checks itself, and doesn't hallucinate its way past a wrong answer.

- **Nano-AI Safety Architecture** — a supervising agent delegates bounded, single-function, non-agentic narrow processes that each perform one deterministic task and connect only to explicitly wired data sources.
- **Evaluation Harness** — a deterministic evaluation harness that grades agent-loop directives against fixed test cases: deterministic assertions plus an LLM-judged quality score.
- **Observability & Permission Gating** — a live diagnostic panel exposing real-time node state and inter-agent messages, paired with a hard permission gate requiring explicit human sign-off before any autonomous code-writing or state-changing action.
- **Memory & Knowledge Architecture** — a multi-layer memory system: working buffer (short-term), persistent memory (long-term, confidence-weighted RAG), and immutable historical memory (append-only).

A.R.C.H.O.N. is private. [PRISM](/projects/prism/) is the public research vehicle for the same architecture.
