---
layout: page
title: "Portfolio Optimization <a href='https://github.com/eleanorfleming96/Portfolio/blob/main/Optimization.ipynb' target='_blank'>[GitHub]</a>"
browser-title: "Portfolio Optimization"
---
>At <a href="https://www.blackrock.com/aladdin" target="_blank">BlackRock</a> from January 2022 to October 2022, I worked with 10+ enterprise clients to optimize their fixed income and equity portfolios using the Aladdin risk and trading system. 
>
> Below, I walk through a streamlined example of portfolio optimization to demonstrate the analytical approaches and strategies used to align client objectives with real-world constraints. If you need a refresher on what optimization is, jump down [to this section](#what-is-optimization).
>

---
## Solution Overview

In our final example, we combine risk minimization with ESG (Environmental, Social, and Governance) maximization for a 3-security, fully invested, long-only portfolio. 

The left chart illustrates changes in risk, while the right chart shows ESG performance. We can compare the baseline allocation (blue marker) to the optimized solution (black marker).
<!-- EMBED THE HTML CHART -->
<style>
iframe {
    border: none;
    box-shadow: none;
}
.chart-container {
    display: flex;
    gap: 20px;
}
.chart-container > div {
    flex: 1;
}
</style>
<div class="chart-container">
    <div>
        <iframe src="/public/charts/2.html" width="100%" height="600px"></iframe>
    </div>
    <div>
        <iframe src="/public/charts/3.html" width="100%" height="600px"></iframe>
    </div>
</div>
<!-- END EMBEDDING THE HTML CHART -->
 The optimized solution removes Asset C and allocates the portfolio equally between Assets A and B (50/50), striking a more favorable balance between ESG and risk. 
 
 In the sections below, we’ll build up to this result step by step.

## Example 1: Minimizing Portfolio Risk ##

Imagine you currently own a mix of three stocks. **Current Weight** represents your initial allocation to each stock. Your goal is to populate the **New Weight** column `x₁, x₂, x₃` by adjusting how much money you have invested in each stock (by buying more or selling some) to reduce the overall risk of your portfolio.

In this analysis, **Risk/Volatility** is measured using the standard deviation of individual asset returns. Standard deviation quantifies the volatility of each asset independently, providing a straightforward measure of risk.

>In a real optimization example, we would use a covariance matrix to capture the relationship between assets, which is essential for accuracy. Rather than evaluating each asset's risk in isolation, a covariance matrix accounts for how assets move in relation to one another and allows us to capture diversification effects.
>
>
For example, consider a utility stock and a technology stock. Utility stocks are stable and less affected by economic cycles, while technology stocks are more volatile and tied to economic growth. These two stocks may have low or negative correlation, meaning when one declines, the other might hold steady or rise. The covariance matrix captures this relationsihp.
>

While trying to achieve the lowest risk, we have a few constraints to consider. 

1. All your money needs to stay invested—no leftover cash. In other words, you are **fully invested**.
2. You can’t borrow stocks to sell them; you can only sell what you already own. In other words, **no shorting**.

| **Stock** | **Current Weight** | **New Weight** | **Risk/Volatility** | **Sector**   |
|:---------|:-------------------|:--------------|:-------------------|:-------------|
| A         | 20%               | x₁            | 20                  | Technology   |
| B         | 30%               | x₂            | 30                  | Energy       |
| C         | 50%               | x₃            | 40                  | Energy       |

The **objective function** for this problem is to **minimize portfolio risk**, expressed as:

`Z(x) = 20x₁ + 30x₂ + 40x₃`

The **constraints** for this problem are:

1. **Remain Fully Invested**:  
   100% of the available capital must be allocated.  
   `x₁ + x₂ + x₃ = 1`

2. **No Shorting**:  
   This is a long-only portfolio, in other words, there can be no negative short positions.  
   `x₁, x₂, x₃ ≥ 0`

>Real-world optimizations often include 5–20 additional constraints beyond the basics, such as maintaining sector exposure (e.g., 10% in technology), limiting single-stock allocations (e.g., max 10%), ensuring liquidity (e.g., 20% in liquid assets), and managing tracking error (e.g., under 2% relative to a benchmark).
>

### Optimal Solution
<!-- EMBED THE HTML CHART -->
<style>
iframe {
    border: none;
    box-shadow: none;
}
</style>
<iframe src="/public/charts/1.html" width="100%" height="600px"></iframe>
<!-- END EMBEDDING THE HTML CHART -->

Unsurprisingly, the optimal solution is to allocate 100% of the portfolio to **Stock A**, as this is the stock with the lowest risk. This satisfies the objective of minimizing portfolio risk under the given constraints of remaining fully invested and no shorting.

>While this example is straightforward, real-world optimization problems often involve more complex constraints that can make the case infeasible (impossible to solve). In these cases, intuitive diagnostic tools are critial to diagnose and resolve conflicting constraints efficiently.
>
>Imagine a portfolio with two rules: all the funds must be fully invested (100% allocated), and no single stock can make up more than 40% of the portfolio. Now, add another rule requiring at least 70% of the portfolio to be invested in technology stocks—but the technology sector only has two stocks available. These rules clash because meeting the 70% sector requirement would force each tech stock to exceed the 40% cap.
>
To resolve this conflict, you could adjust the rules, such as raising the stock limit to 50% or lowering the sector requirement. This example shows how overly strict constraints can make optimization infeasible and often require adjustments to find a workable solution.
>

---

## Example 2: Minimizing Risk While Maximizing ESG Scores ##

Building on the first example, let’s now introduce a second objective: **maximizing ESG (Environmental, Social, and Governance) scores**, which aims to measure the sustainability and ethical impact of an investment.

| **Stock** | **Current Weight** | **New Weight** | **ESG Score** | **Risk/Volatility** | **Sector**   |
|:---------|:-------------------|:--------------|:-------------|:-------------------|:-------------|
| A         | 20%               | x₁            | 10            | 20                  | Technology   |
| B         | 30%               | x₂            | 15            | 30                  | Energy       |
| C         | 50%               | x₃            | 20            | 40                  | Energy       |

The new objective is to balance minimizing portfolio risk with maximizing ESG scores. The problem setup remains the same, with the following additions:

### Dual Objective Optimization Problem

To balance the two objectives, we define a **weighted objective function**:

`Z(x) = w₁ * (20x₁ + 30x₂ + 40x₃) - w₂ * (10x₁ + 15x₂ + 20x₃)`

Where `w₁` and `w₂` are weights that reflect the relative importance of minimizing risk and maximizing ESG scores, respectively.

>Choosing weights in an optimization problem is not a perfect science because the relationship between objectives (e.g., maximizing ESG scores and minimizing risk) is often nonlinear, interdependent, and difficult to quantify precisely. In other words, there is no guarantee that setting `w１` = 1 and `w２` = 2 will result in achieving exactly twice the ESG improvement for a given unit of risk reduction.
>

The weights `w₁` and `w₂` allow us to decide which goal, or objective, takes priority:
- If `w₁` > `w₂`, we want the model to prioritize minimizing risk.
- If `w₂` > `w₁`, we want the model prioritize maximizing ESG scores.

The **constraints** for this problem remain the same - we need to remain **fully invested and no shorting**.

### Optimal Solution

When `w１` = 1 and `w２` = 2, we are prioritizing maximizing ESG scores over minimizing risk. This results in the following optimal solution:

| **Stock** | **Current Weight** | **New Weight** | **ESG Score** | **Risk/Volatility** | **Sector**   |
|:---------|:-------------------|:--------------|:-------------|:-------------------|:-------------|
| A         | 20%               | 50%            | 10            | 20                  | Technology   |
| B         | 30%               | 50%            | 15            | 30                  | Energy       |
| C         | 50%               | 0%             | 20            | 40                  | Energy       |

<!-- EMBED THE HTML CHART -->
<style>
iframe {
    border: none;
    box-shadow: none;
}
.chart-container {
    display: flex;
    gap: 20px;
}
.chart-container > div {
    flex: 1;
}
</style>
<div class="chart-container">
    <div>
        <iframe src="/public/charts/2.html" width="100%" height="600px"></iframe>
    </div>
    <div>
        <iframe src="/public/charts/3.html" width="100%" height="600px"></iframe>
    </div>
</div>
<!-- END EMBEDDING THE HTML CHART -->

While Blackrock has proprietary solvers for more complex optimization problems, in this case I used an optimization solver in Python. These solvers are designed to systematically evaluate possible allocations, finding the one that meets all constraints while achieving the best outcome for the objective function. They balance precision and efficiency to identify the optimal result.

In this case, the solution to maximize ESG scores while minimizing risk is to sell Asset C entirely and allocate funds equally between Asset A and Asset B (50/50). This result makes snese because Asset A and B both offer higher ESG scores and lower risk compared to Asset C, making them the better choices for achieving the defined objectives.

---

## Efficient Frontier

The efficient frontier is a tool in portfolio optimization that visualizes how shifting the relative importance of risk and ESG goals (by adjusting `w₁` and `w₂`) impacts your portfolio—revealing how prioritizing one objective often requires compromises in the other.

Each point on the efficient frontier corresponds to a portfolio that:
1. Minimizes risk for a given level of ESG score, or
2. Maximizes ESG score for a given level of risk.

<!-- EMBED THE HTML CHART -->
<style>
iframe {
    border: none;
    box-shadow: none;
}
</style>
<iframe src="/public/charts/4.html" width="100%" height="600px"></iframe>
<!-- END EMBEDDING THE HTML CHART -->

By adjusting weights `w₁` and `w₂`, the optimization process identifies portfolios along this frontier, helping investors choose the one that aligns with their priorities. Portfolios below the efficient frontier are less efficient, as you could either achieve a higher ESG score for the same risk or lower risk for the same ESG score. 

>In practice, the efficient frontier is not just a visualization tool but a powerful way to communicate trade-offs to stakeholders. For example, compared to the initial allocation marked by the star, portfolios along the efficient frontier offer better ESG scores for the same or lower levels of risk.
>

---

## What is Optimization?

**Optimization** is the process of finding the best solution to a problem from a set of possible solutions. It involves selecting the values of certain variables (**decision variables**) to either:

- **Maximize** something desirable (e.g., profit, efficiency, or happiness), and/or  
- **Minimize** something undesirable (e.g., cost, time, or waste),  

while satisfying certain **constraints** (rules or limits) imposed by the problem. 

Let’s apply optimization to a financial portfolio. The goal is to adjust a mix of investments (e.g., stocks or other securities) to meet specific objectives and constraints.

Once the problem is defined, running the optimization finds the **optimal mix of investments** that satisfies all the requirements.
