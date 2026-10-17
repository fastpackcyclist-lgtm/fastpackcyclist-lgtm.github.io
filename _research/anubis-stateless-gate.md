---
layout: research-entry
title: "A Stateless Compliance Gate for AI Agents"
type: prototype
status: Active build — Anubis
date: 2026-10-17
summary: A real design exchange, stress-tested against a concrete multi-step exfiltration scenario, for judging an AI agent's proposed action by its resulting state rather than its stated intent or a remembered sequence.
---

## The real design question

Anubis sits at the decision threshold for AI agents — it judges whether a proposed action is allowed to execute, before it happens, not after. The question that actually shaped the architecture: does the gate need to remember a session to do that job, or not?

Session memory can catch a multi-step attack a single-action check can't — four individually-fine actions (make a directory → make it public → copy sensitive data in → download it) that only look harmful assembled in sequence. But it costs real things: the audit ledger stops being a simple append-only log and becomes a graph that has to be walked to explain any one decision; the gate stops being a fast stateless function and needs a live state store on every call; and it opens a new attack surface — an attacker (or just noise) flushing the window between steps.

## The commitment: never track history, judge the resulting state

Anubis never asks "is this action allowed" (which can't see the pattern across steps). It asks "does the state this action would produce violate a hard rule" (which doesn't need to know how you got there). The four-step exfiltration above dies at step 3 — not because Anubis remembers steps 1–2, but because "an internal-DB-tagged resource in a publicly-exposed path" is a hard violation the instant it would exist, regardless of the path that led there.

Every resource Anubis might gate carries security-relevant tags — sensitivity, category, origin, whether a human has reviewed it. Every evaluated action is a proposed delta: what the resource looked like before, what it would look like after, scored against a set of invariants written as plain predicates over that one delta, nothing else. A predicate reads only the single proposed change passed to it — no external state, no session, no memory — enforced structurally, not by convention.

This keeps the thing that makes Anubis worth building: fast, stateless, deterministic, genuinely auditable — a real compliance gate, not a cosmetic filter that falls apart the moment an attacker inserts a pause between steps.

## The honest limit

Stated plainly rather than hidden: a violation that never produces one bad snapshot — an attacker who moves data through a series of equally-restricted locations before a final, human-authorized export — isn't caught by delta invariants alone. That's a real, accepted gap for later work, not a claimed solution.
