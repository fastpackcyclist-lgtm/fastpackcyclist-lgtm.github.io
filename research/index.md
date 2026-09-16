---
layout: page
title: Research
permalink: /research/
---

I work on the applied side of a question that mostly gets asked in theory: how do you make an AI system trustworthy enough to actually act, not just answer? Everything below is a real line of investigation running through A.R.C.H.O.N. and PRISM, not a settled result — each one is stated as the question it actually is.

## Closed-world tool grounding

Can an agentic system be made structurally incapable of claiming a capability it doesn't have? A.R.C.H.O.N.'s tool manifest is closed and re-validated server-side on every routing decision — an unknown instrument is never executed, and a model's own claim about what it did is never trusted without a matching record. The open question is how far this generalizes: closed-world grounding is straightforward for a fixed tool registry, harder as the registry grows and starts composing tools together.

## Self-critique under a bounded budget

A system that reviews every one of its own actions is either too slow to be useful or, if the review itself can loop, too slow to ever finish. A.R.C.H.O.N.'s self-critique gate runs under tiered rigor (off, writes-only, all) with a hard refusal budget — after a fixed number of rejections, further writes close deterministically rather than looping. The open question is where that budget should sit for a given class of action, and whether it should adapt based on what the system has actually gotten wrong before.

## Anti-hallucination by construction, applied to geometry

Text hallucination gets studied. Geometric hallucination — a model inventing a vertex that doesn't correspond to anything real — mostly doesn't, because most systems don't ask a model to emit geometry at all. AXF never lets cognition touch a coordinate: it names a part and its parameters, and a deterministic kit expands that into real geometry on-device. The open question is how far this pattern travels beyond CAD — anywhere a model is tempted to output something precise and checkable, parametric-plus-deterministic-expansion may be the more honest architecture than direct generation.

## Self-report checked against evidence, not asserted

Most AI systems describe their own capabilities in whatever language a human wrote for them. A.R.C.H.O.N.'s capability map distinguishes LIVE (backed by real execution records) from WIRED (built but never exercised), computed fresh from actual traces rather than declared. The open question is whether a system can extend this to genuinely uncertain claims — not just "have I done this," but "how reliably do I do this," measured rather than guessed at.

## What a directed AI system should feel like to use

Most of the interesting failure modes in human-AI interaction aren't about model quality — they're about whether the person using the system can tell what it's actually doing. PRISM's permission gates are real UI, not fine print; its diagnostic panel shows the same routing decision the system used, not a simplified summary of it. The open question is how much transparency is actually useful before it becomes noise, and where that line moves as a system gets more autonomous.

---

This page will grow as these questions get answered, revised, or replaced by better ones. Follow the [Projects](/projects/) and [Notes](/notes/) sections for the write-ups as they happen.
