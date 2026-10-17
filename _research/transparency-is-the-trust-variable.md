---
layout: research-entry
title: "Human-AI Interaction: Transparency Is the Load-Bearing Trust Variable"
type: paper
status: Published — Human-AI Interaction
date: 2026-10-17
summary: Recent workplace-AI research identifies agent transparency as the single strongest predictor of user preference — ahead of accuracy, speed, or capability. Most agentic UIs still treat it as an afterthought.
---

## The topic, not just the project

Human-AI interaction research in 2026 keeps arriving at the same real finding from different directions: transparency — not raw capability — is what actually determines whether a person trusts an agentic system enough to let it act. A recent multi-method study of workplace AI-agent interaction (participatory design workshops, expert review, meta-analysis, interviews) found agent transparency has the strongest measured impact on user preference of any factor studied — users need to follow the agent's reasoning, see task status, know what data sources were used. Parallel work on trust calibration finds the same pattern from the explainability side: perceived explainability and perceived intention alignment are the two strongest predictors of whether a user's trust in a system is actually warranted, not just felt.

## Where most agentic interfaces get this backwards

The common failure isn't too little information — it's the wrong shape of it. A progress spinner and a success toast are not transparency; they're reassurance. Real transparency means showing the same routing decision the system itself used, not a simplified narrative written for the user afterward. Confidence levels, explicit "I don't know" states, and a visible record of what was actually checked are described across this research as a non-negotiable baseline, not a nice-to-have — because an agent that can't show its own uncertainty is structurally incapable of being trusted correctly, only trusted by accident.

PRISM's permission gates exist as one real instance of this: gates are rendered as actual UI a person has to engage with, not fine print beneath a button, and its diagnostic panel surfaces the same state the orchestration layer is actually using, not a dumbed-down summary of it. That's a direct, deliberate application of what this research keeps finding — not a UI nicety layered on top of a working system, part of what makes it trustworthy in the first place.

## The open question

How much transparency is actually useful before it becomes noise a user tunes out — and where that line moves as a system is trusted with more autonomy — is still a real, unresolved design question across this entire field, NARVI's own systems included.

Sources: [arXiv — A Framework of UX Principles for Human-AI Agent Interaction in the Workplace](https://arxiv.org/html/2607.19941v1), [arXiv — Tell Me Something That Will Help Me Trust You: A Survey of Trust Calibration](https://arxiv.org/pdf/2205.02987), [arXiv — Design Principles for Human-Agent Interaction](https://arxiv.org/pdf/2606.20630)
