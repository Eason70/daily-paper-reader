---
title: Near-Optimal Sample Complexity for Online Constrained MDPs
title_zh: 在线约束马尔可夫决策过程的近最优样本复杂度
authors: "Chang Liu, Yunfan Li, Lin Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=kYisDXzTk7"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 在线约束MDP，模型基原对偶算法，平衡遗憾和违规
tldr: 在线约束MDP中，现有方法常导致大量安全违规或高样本复杂度。本文针对宽松和严格两种可行性设定，提出模型基原对偶算法，平衡累计遗憾与约束违规。理论证明在宽松设定下达到次线性遗憾和违规，在严格设定下实现零违规的亚线性遗憾。为在线安全RL提供了高效且安全的理论保障。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 解决在线约束MDP中安全违规与样本效率的矛盾。
method: 提出模型基原对偶算法，针对不同可行性设定优化策略。
result: 在松弛和严格两类设定下均实现了理论上的最优或近最优性能。
conclusion: 为在线安全强化学习提供了样本高效且合规的算法框架。
---

## Abstract
Safety is a fundamental challenge in reinforcement learning (RL), particularly in real-world applications such as autonomous driving, robotics, and healthcare. To address this, Constrained Markov Decision Processes (CMDPs) are commonly used to enforce safety constraints while optimizing performance. However, existing methods often suffer from significant safety violations or require a high sample complexity to generate near-optimal policies. We address two settings: relaxed feasibility, where small violations are allowed, and strict feasibility, where no violation is allowed. We propose a model-based primal-dual algorithm that balances regret and bounded constraint violations, drawing on techniques from online RL and constrained optimization. For relaxed feasibility, we prove that our algorithm returns an $\varepsilon$-optimal policy with $\varepsilon$-bounded violation with arbitrarily high probability, requiring $\tilde{O}\left(\frac{SAH^3}{\varepsilon^2}\right)$ learning episodes, matching the lower bound for unconstrained MDPs. For strict feasibility, we prove that our algorithm returns an $\varepsilon$-optimal policy with zero violation with arbitrarily high probability, requiring $\tilde{O}\left(\frac{SAH^5}{\varepsilon^2\zeta^2}\right)$ learning episodes, where $\zeta$ is the problem-dependent Slater constant characterizing the size of the feasible region. This result matches the lower bound for learning CMDPs with access to a generative model. Episodic tabular CMDPs serve as a crucial benchmark for safe RL, providing a structured environment for theoretical analysis and algorithmic validation. Our results demonstrate that learning CMDPs in an online setting is as easy as learning with a generative model and is no more challenging than learning unconstrained MDPs when small violations are allowed.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：在强化学习（RL）的实际部署（如自动驾驶、机器人、医疗）中，安全是根本挑战。传统 RL 算法在训练过程中可能产生严重的安全违规（如碰撞、设备损坏），因此需要在优化奖励的同时严格限制代价（成本）违约。约束马尔可夫决策过程（CMDP）是为此类问题建模的标准框架。
- **核心问题**：现有在线 CMDP 方法要么导致大量安全违规，要么需要极高的样本复杂度才能学习到近似最优策略。特别地，在 **宽松可行性**（允许小幅度违约）和 **严格可行性**（零违约）两种设定下，能否达到理论最优的样本效率尚不清楚。
- **整体含义**：作者希望设计一种在线安全 RL 算法，在两种设定下都实现 **近最优的样本复杂度**（匹配无约束 MDP 的下限），同时保证高概率下的近似奖励最优性。研究结果证明：在在线场景下学习 CMDP 与使用生成模型（随机访问）学习一样容易；在允许小违规时甚至不比学习无约束 MDP 难。

### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：采用 **模型基原对偶算法**（model-based primal-dual algorithm），结合 **双批更新**（doubling batch updates）来解耦经验模型与价值估计之间的相关性，从而获得紧致的理论边界。
- **关键技术细节**：
  - 构建经验 CMDP，使用 **UCB 风格奖励奖励奖励金**（optimistic bonus）和 **悲观成本估计**（pessimistic cost estimate）来鼓励探索并确保安全性。
  - 在每一集内，通过 **T 轮原-对偶迭代** 求解拉格朗日形式的鞍点问题。每轮先更新原始策略（最大化奖励减去拉格朗日加权成本），再对偶变量（梯度下降后离散化到 ε-网格）。
  - 最终执行 **混合策略**（mixture policy）：将 T 轮迭代得到的策略平均，然后用于收集数据更新经验模型。
  - 在宽松可行性设定中，将约束常数 **乐观上移**（b' = b + τ）；在严格可行性设定中，将约束常数 **悲观下移**（b' = b - Δ）。
  - 使用 **双批更新** 技巧：仅当某个状态-动作对的累积访问计数翻倍时才更新经验转移矩阵，从而限制可能的“剖面”（profile）数量，使联合界可行。

### 3. 实验设计
- **论文为纯理论研究，未包含任何实验**。因此无数据集、benchmark 或对比方法。

### 4. 资源与算力
- 论文未涉及任何实验运行，未提及计算资源或算力需求。故此项不适用。

### 5. 实验数量与充分性
- 不适用。所有结果均为数学证明，理论推导完整（附有详细附录）。因此无需实验来验证结论。

### 6. 论文的主要结论与发现
- **宽松可行性设定**：算法能以高概率返回一个 ε-近优且 ε-违约策略，样本复杂度为 \(\tilde{O}(SAH^3/\varepsilon^2)\)，匹配无约束 MDP 已知下界。
- **严格可行性设定**：算法能以高概率返回一个 ε-近优且 **零违约** 策略，样本复杂度为 \(\tilde{O}(SAH^5/(\varepsilon^2\zeta^2))\)（ζ 为 Slater 常数），匹配带生成模型存取的下界。
- 两个设定下的 regret 和 constraint violation 均可被理论边界控制，并通过设置合适参数转化为样本复杂度界。
- 这些结果首次表明：在线 CMDP 学习在宽松设定下与无约束 MDP 一样“容易”；严格设定下与带生成模型的 CMDP 学习一样“容易”。

### 7. 优点
- **理论贡献显著**：首次在在线表格型 CMDP 中达到 minimax 最优样本复杂度（两种设定）。
- **技术新颖**：巧妙结合了双批更新、原-对偶优化、乐观/悲观奖励/成本塑造、离散化对偶变量等技巧，克服了经典 CMDP 分析方法中策略与模型相关性的难题。
- **结论全面**：同时给出 regret 和 violation 的边界，并转换为 ε-最优样本复杂度，覆盖了实际关注的两种安全约束严格程度。
- **匹配下界**：证明与已知下界紧贴，表明算法理论上不可改进。

### 8. 不足与局限
- **缺乏实验验证**：作为纯理论论文，没有在仿真或真实环境中验证算法实际表现；理论假设（如已知奖励和成本函数、表格状态空间）在实际大规模应用中有较大限制。
- **应用限制**：
  - 仅适用于有限状态-动作空间的表格设定，未扩展到函数近似或连续控制。
  - 严格可行性设定依赖 Slater 常数 ζ，若 ζ 很小则样本复杂度需很大，且需要已知 ζ 来设定参数。
  - 对偶变量离散化（ε-网格）可能引入额外的近似误差，实际调参困难。
- **偏差风险**：理论证明使用大量常数与对数项，实际常数可能较大，导致实际所需样本数远高于理论下界。
- 未考虑多约束或部分可观测等更复杂场景。

（完）
