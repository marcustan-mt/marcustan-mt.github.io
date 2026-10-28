---
title: "Reinforcement Learning Algorithms in Blackjack and Frozen Lake"
subtitle: "Exploring Value Iteration, Policy Iteration, and Q-Learning in two contrasting environments"
category: Machine Learning
tags: [machine-learning, reinforcement-learning, q-learning, openai-gym]
order: 9
---

Reinforcement learning is where an agent learns how to behave in an environment by trying different actions and observing results — like training a pet with rewards and penalties. This article explores RL through two OpenAI Gymnasium environments.

## Markov Decision Processes

An MDP structures RL problems with agents, states, actions, transition probabilities, rewards, and policies. The critical assumption: past states don't matter in deciding the next action — only the current state does.

## Algorithms

### Value Iteration

Iteratively updates value functions using the Bellman equation until convergence. Conceptually straightforward: keep recalculating how good each state is until the numbers stabilize.

### Policy Iteration

Alternates between policy evaluation (how good is the current policy?) and policy improvement (can we do better?). Typically converges in fewer iterations than Value Iteration, but each iteration is more expensive.

### Q-Learning

A model-free approach that learns optimal action-value functions without requiring a model of the environment. The most flexible but slowest to converge.

## Frozen Lake Results

- Value Iteration converged within ~20 iterations; Policy Iteration within <10
- Larger grid sizes exponentially increased runtime
- Higher discount factors (gamma) produced greater rewards in complex environments
- Q-Learning struggled with convergence in large stochastic settings

## Blackjack Results

- Both Value and Policy Iteration converged rapidly (within 4 iterations)
- Only 6 of 290 states showed policy differences between the two algorithms
- Q-Learning converged around 2,000 iterations — significantly slower
- State space reduction improved efficiency but decreased performance

## Key Takeaways

1. Model-based algorithms (Value/Policy Iteration) excel in large, unpredictable environments
2. Q-Learning requires extensive parameter tuning for stochastic settings
3. Algorithm choice matters less in small, deterministic environments
4. Each approach trades off between computational efficiency and information requirements
