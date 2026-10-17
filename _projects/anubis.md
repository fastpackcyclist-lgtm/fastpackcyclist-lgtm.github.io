---
layout: project
title: Anubis
category: private-rd
status: Active — private R&D
summary: A domain-scoped AI classifier and deterministic compliance gate for agentic systems, built separately from A.R.C.H.O.N. by design.
---

Anubis sits at the decision threshold for AI agents — it judges whether a proposed action is allowed to execute, before it happens, not after. Instead of evaluating an action's name or intent, it evaluates the real consequence: a resource's security tags before and after the action (sensitivity, origin, category), checked against hard invariants written as plain predicates over that one proposed change.

It deliberately never tracks session history. A violation is caught by the resulting state an action would produce, not by remembering a sequence of prior steps — the design was stress-tested directly against a concrete multi-step exfiltration scenario before being written down, specifically because sequence-based monitors break the moment an attacker inserts a pause between steps.

- **Classification** — a small, purpose-built transformer (not a wrapped LLM) scoring four real dimensions: CSA's Agentic AI Autonomy Level (L0–L5), resource sensitivity, resource origin, and resource category.
- **Invariant gate** — hard, auditable rules evaluated against a single proposed delta; every invariant checked is logged, not just the ones that fire.
- **Separate by design** — its own repository, its own training pipeline, a portable trust layer meant to wrap any agentic system, not just this house's own.
