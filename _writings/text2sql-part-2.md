---
title: "Large Language Model Application — Text2SQL (Part 2)"
subtitle: "Technical architecture and design decisions for operationalizing Text2SQL"
category: LLMs
tags: [llm, text2sql, rag, bedrock, aws, architecture]
order: 12
---

Part 2 of the Text2SQL series — diving into the technical architecture and key design decisions.

## Technical Architecture

Three core engineering questions drive the architecture:
1. Which foundational models and agents to use?
2. How to implement Retrieval-Augmented Generation (RAG)?
3. What prompt engineering strategies work?

## Agent Selection: Bedrock Claude Sonnet v3

The decision came down to three criteria:

- **Cost** — In-house integration with existing tools like the vector database service
- **Security** — Data encryption at rest and in transit, reducing leak risks
- **Infrastructure Simplicity** — Managed service reduces operational burden

### LangChain vs. Bedrock

| Aspect | LangChain | Bedrock |
|--------|-----------|---------|
| Strengths | Framework versatility, customizability, open-source | Managed service, AWS ecosystem, scalability |
| Weaknesses | Learning curve, resource management burden | Limited to specific vendors, customization constraints |

## RAG Implementation

### Why RAG?

LLMs face three inherent limitations: limited access to comprehensive data, risk of outdated information, and inability to provide context-specific responses. RAG addresses all three.

### Components

- **Knowledge base** for indexing domain-specific information
- **Vector embeddings** using Titan v2 (8,192 token capacity)
- **Amazon OpenSearch Serverless** as the vector database

### Knowledge Base Contents

1. **DDL information** — Column data types and descriptions
2. **Pipeline details** — How datasets are sourced and what they describe
3. **Sample queries** — Demonstrating table relationships and common patterns

## Runtime Flow

1. User submits a natural language query
2. Query is converted to vector embeddings
3. Approximate Nearest Neighbor (ANN) search finds relevant context
4. Context is augmented into the LLM prompt
5. LLM generates SQL based on enriched context

## Prompt Engineering Challenges

Three issues encountered during implementation:

1. **Database Cluster Identification** — The LLM struggles to identify which cluster data lives in and mistakenly assumes cross-cluster querying is possible
2. **Inconsistent Results** — Limited training data and insufficient sample queries create variability
3. **Incorrect Join Logic** — Models frequently default to inner joins instead of LEFT or RIGHT joins

*Part 3 covers hyperparameter tuning, testing, and deployment.*
