---
title: "Improving LLM Accuracy is Hard"
subtitle: "Strategies for enhancing LLM application accuracy, with Text2SQL as a case study"
category: LLMs
tags: [llm, accuracy, evaluation, rlhf, text2sql, rag]
order: 15
---

Improving LLM accuracy is a fundamentally different challenge from traditional ML optimization. Unlike classical ML, there are no standardized methods — the field is young and still evolving.

## The Core Challenge

Two specific pain points:
- **Position effects** — Where information appears in context affects outcomes (similar to human recency/primacy effects)
- **Syntactic sensitivity** — Minor phrasing changes produce drastically different results

## Metrics Framework

### LLM-Level Metrics

- Precision, Recall, Spearman Rho, Cohen's Kappa, Kendall's Tau
- For Text2SQL: **Execution Accuracy (EX)** is the primary metric — does the generated SQL return correct results?
- Exact Match Accuracy (EM) also matters but is less important than EX

### Knowledge Base Metrics

- **Mean Reciprocal Rank (MRR)** — How high does the relevant document rank?
- **Normalized Discounted Cumulative Gain (nDCG)** — Evaluates both relevance and ranking quality

## Improvement Methodologies

### 1. LLM-as-a-Judge / LLM Ensembles

Use one LLM to evaluate another's outputs.

**Strengths:** Scalable, explainable evaluation without extensive human involvement.

**Limitations:**
- O(n^2) time complexity for pairwise comparison
- Position bias, verbosity bias, and self-enhancement bias
- Pairwise comparison becomes quadratically expensive at scale

### 2. Workflow Decomposition

Break the task into specialized sub-tasks.

**DIN-SQL** decomposes into: schema linking, classification, SQL generation, and self-correction — improving execution accuracy from 79.9% to 85.3% on the Spider dataset.

**DEA-SQL** adds adaptability through targeted error handling and active learning.

**Limitations:** More stages means more cost, latency, and instability from probabilistic LLM outputs compounding.

### 3. RLHF / Supervised Fine-Tuning

Reinforcement Learning from Human Feedback aligns models with user intent.

The InstructGPT result is remarkable: a 1.3B parameter model fine-tuned with RLHF was preferred over the 175B GPT-3 85% of the time, with a 21% reduction in hallucinations.

**RLAIF** (from AI Feedback) reduces costs by replacing human evaluators with LLM evaluations.

**Limitations:** Resource-intensive, human bias in feedback loops, inapplicable when datasets change frequently.

## Synthesis

| Goal | Recommended Approach |
|------|---------------------|
| Overall accuracy | LLM Ensembles |
| Precision/Recall | RLHF |
| Knowledge base retrieval (nDCG/MRR) | Workflow Decomposition |

No single technique solves everything. The practical answer is usually a combination — and the willingness to iterate continuously.
