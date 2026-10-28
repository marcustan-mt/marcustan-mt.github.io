---
title: "Unveiling Matplotlib: Visualizing Betting Strategies and Monte Carlo Simulations"
subtitle: "Exploring Matplotlib's visualization capabilities through the Martingale strategy"
category: Python
tags: [python, matplotlib, monte-carlo, visualization]
order: 1
---

## Why Matplotlib?

Matplotlib is an essential tool in Python's data visualization ecosystem. Think of it as an artist's canvas — it works synergistically with libraries like Seaborn and Plotly for creating compelling data narratives. If you're doing any kind of data work in Python, you'll inevitably reach for it.

## The Martingale Strategy

The Martingale betting strategy involves doubling your wager after each loss, theoretically guaranteeing recovery of all losses plus a profit. Sounds foolproof, right? Not quite. Practical limitations undermine this strategy:

- Limited personal bankrolls
- Casino table betting limits
- The mathematical reality that losing streaks persist longer than you'd expect

This makes it a perfect candidate for Monte Carlo simulation — we can model thousands of scenarios and visualize the outcomes.

## Key Matplotlib Functions

### Axis Controls

```python
plt.xlim(0, 300)   # Set X-axis limits
plt.ylim(0, 300)   # Set Y-axis limits
```

### Labels and Titles

```python
plt.xlabel('a')     # X-axis label
plt.ylabel('b')     # Y-axis label
plt.title('a')      # Chart title
```

### Plotting and Visualization

```python
plt.plot(list_x, list_mean, label='Mean', color='green')
plt.axvline(x=dt.datetime(2008, 9, 19), color='r', linestyle='--')
plt.legend(loc='lower left')
```

### File Operations

```python
plt.clf()                           # Clear plot
plt.savefig('image/figure1.png')    # Save as PNG
```

## Simulation Results

Five visualizations were generated, each progressively adding realism:

1. **Figure 1** — 10 episodes of 1,000 consecutive bets (unlimited cash assumption)
2. **Figure 2** — Mean and standard deviation lines across 1,000 episodes
3. **Figure 3** — Median and standard deviation analysis
4. **Figure 4** — Mean/std dev with a realistic $256 bankroll constraint
5. **Figure 5** — Median/std dev under realistic conditions

## Key Insight

The simulations reveal a critical finding: without vast financial resources, beating casino odds through the Martingale strategy is mathematically improbable. The median line tells the real story — while the mean gets pulled up by rare lucky runs, most players go broke.

## Resources

- [Matplotlib Cheat Sheets](https://matplotlib.org/cheatsheets/)
- [Official API Documentation](https://matplotlib.org/stable/api/index)
- [GitHub Implementation](https://github.com/marcustan-mt/python/blob/main/ex.%20matplotlib.py)
