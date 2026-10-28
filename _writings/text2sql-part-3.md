---
title: "Large Language Model Application — Text2SQL (Part 3)"
subtitle: "Hyperparameter tuning, knowledge base construction, testing, and deployment"
category: LLMs
tags: [llm, text2sql, hyperparameters, deployment, aws, bedrock]
order: 13
---

Part 3 of the Text2SQL series — the implementation details that make or break a production deployment.

## Action Groups and API Design

For this phase, we avoided Lambda/microservices complexity and prioritized simplicity in SQL query generation. Future iterations may incorporate action groups for dashboard automation via Tableau, but that's deprioritized for now.

## Hyperparameter Tuning

Three critical parameters balance creativity versus accuracy:

### Top-p Sampling

Selects the next token from the smallest possible set whose cumulative probability exceeds a specified threshold. This enables diverse yet relevant outputs — the set size adapts dynamically to each prediction.

### Top-k Sampling

Limits selections to the K most probable tokens. More rigid than top-p: the set size is always exactly K. Top-p offers dynamic adjustment while top-k maintains a focused, fixed window.

### Temperature

Scales logits before softmax activation. T > 1 increases randomness and creativity; T < 1 reduces it and makes outputs more deterministic. For SQL generation, lower temperatures are generally better — you want precision, not creativity.

## Knowledge Base Construction

Three essential components:

1. **DDL Information** — Column data types and descriptions prevent confusion between similar column names (e.g., `encrypted_customer_id` vs `customer_id`)
2. **SQL Pipelines** — Understanding upstream data sources and permissible column values
3. **Sample Queries** — Complex SQL demonstrating relationships across tables

**Chunking strategy:** Files exceeding 8,192 tokens use semantic chunking to maintain context within each chunk.

## Testing Framework

Rather than BLEU/ROUGE scores (which measure text similarity, not SQL correctness), we test by comparing LLM-generated SQL outputs against expected results. Questions are categorized as Easy, Medium, and Hard to assess performance across complexity levels.

## Latency Optimization

Following AWS best practices: single knowledge bases, minimal action groups, avoid unnecessary user prompts, and use default orchestration. The agent deploys in us-west-1 with potential CDN expansion for APAC/EU users.

## Limitations

### Generative AI Challenges
- Hallucinations persist despite prompt engineering
- Black-box interpretability issues
- Limited simultaneous access to multiple foundation models

### Bedrock-Specific Constraints
- No blue-green/canary deployments — changes go to all users at once
- Maximum 2 knowledge bases per agent (1M files each)
- Shared capacity throttling despite per-account limits
