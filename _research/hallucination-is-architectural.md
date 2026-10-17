---
layout: research-entry
title: "AI Safety Engineering: Hallucination Is an Architecture Problem, Not a Prompting One"
type: paper
status: Published — AI Safety Engineering
date: 2026-10-17
summary: "Layered guardrails cut hallucination 71–89% versus unguarded deployments — but every effective approach shares one trait: none of them trust the model to just not hallucinate. They structurally remove the opportunity."
---

## The topic, not just the project

Hallucination research in 2026 has converged on a real, useful taxonomy: factual, grounding, citation, and reasoning failures are different problems requiring different fixes, not one blanket "the model made something up." But the deeper convergence is architectural, not taxonomic — the approaches that actually move the needle (retrieval with strict citation contracts, structured output schemas with required confidence fields, deterministic validation layers) all share the same real property: they don't ask the model to be more careful. They remove the degrees of freedom that let it fabricate in the first place.

## Where this gets interesting: domains with no "close enough"

Text hallucination gets studied because text tolerates being approximately right. Geometry doesn't — a fabricated vertex is either the real coordinate or it's wrong, with no partial credit. Most systems avoid this problem by simply never asking a model to emit raw geometry. A.R.C.H.O.N.'s AXF kit takes the same real principle used in RAG-with-citations — never let the generative step touch the fact — and applies it to a domain where "the fact" is a 3D coordinate: a model names a part and its parameters, and a deterministic kit expands that into real geometry on-device. Cognition never touches the number.

## The real, quantified case for architecture over prompting

Guardrails layered together — grounding, structured schemas, real-time monitoring — cut hallucination rates by 71–89% compared to unguarded deployments. That's not a marginal improvement from better prompting; it's the difference between a system that occasionally lies convincingly and one that's structurally prevented from doing so in the domains it's been scoped to. The open question this field hasn't settled: how far the parametric-plus-deterministic-expansion pattern generalizes beyond narrow, well-specified domains like CAD geometry — and where a domain is simply too open-ended for any deterministic kit to expand into.

Sources: [FutureAGI — LLM Hallucination: A 2026 Architectural Deep Dive](https://futureagi.com/blog/llm-hallucination-deep-dive-2026/), [arXiv — Mitigating LLM Hallucinations through Domain-Grounded Tiered Retrieval](https://arxiv.org/html/2603.17872v1), [GetMaxim — LLM Hallucination Detection and Mitigation](https://www.getmaxim.ai/articles/llm-hallucination-detection-and-mitigation-best-techniques/)
