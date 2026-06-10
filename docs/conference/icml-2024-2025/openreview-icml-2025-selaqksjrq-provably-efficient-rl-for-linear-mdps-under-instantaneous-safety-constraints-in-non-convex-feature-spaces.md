---
title: Provably Efficient RL for Linear MDPs under Instantaneous Safety Constraints in Non-Convex Feature Spaces
title_zh: 非凸特征空间中瞬时安全约束下线性MDP的高效强化学习
authors: "Amirhossein Roknilamouki, Arnob Ghosh, Ming Shi, Fatemeh Nourzad, Eylem Ekici, Ness Shroff"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=sElAqKsJrQ"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 面向自动驾驶的瞬时安全约束强化学习，提供理论保证
tldr: 本文针对非凸特征空间中的线性MDP提出高效强化学习算法，严格处理瞬时安全约束。在自动驾驶等场景中，该算法以高概率实现零违规，并建立次线性遗憾界。为安全关键控制提供了理论保障。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-selaqksjrq/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 833, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-selaqksjrq/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 842, \"height\": 404, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-selaqksjrq/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 709, \"height\": 516, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-selaqksjrq/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1074, \"height\": 680, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-selaqksjrq/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1766, \"height\": 921, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-selaqksjrq/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 584, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-selaqksjrq/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 709, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-selaqksjrq/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 795, \"height\": 589, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-selaqksjrq/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 713, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-selaqksjrq/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1068, \"height\": 801, \"label\": \"Figure\"}]"
motivation: 现有强化学习方法在处理非凸决策空间中的瞬时安全约束时效果不佳。
method: 提出基于线性MDP的强化学习算法，通过安全阈值设计确保零违规。
result: 在非凸特征空间下获得次线性遗憾界，且安全违规概率为零。
conclusion: 该工作为安全强化学习在自动驾驶等领域的应用提供了理论支撑。
---

## Abstract
In Reinforcement Learning (RL), tasks with instantaneous hard constraints present significant challenges, particularly when the decision space is non-convex or non-star-convex. This issue is especially relevant in domains like autonomous vehicles and robotics, where constraints such as collision avoidance often take a non-convex form. In this paper, we establish a regret bound of $\tilde{\mathcal{O}}((1 + \tfrac{1}{\tau})  \sqrt{\log(\frac{1}{\tau})  d^3 H^4 K})$, applicable to both star-convex and non-star-convex cases, where $d$ is the feature dimension, $H$ the episode length, $K$ the number of episodes, and $\tau$ the safety threshold.  Moreover, the violation of safety constraints is zero with high probability throughout the learning process. A key technical challenge in these settings is bounding the covering number of the value-function class, which is essential for achieving value-aware uniform concentration in model-free function approximation. For the star-convex setting, we develop a novel technique called *Objective–Constraint Decomposition* (OCD) to properly bound the covering number. This result also resolves an error in a previous work on constrained RL. In non-star-convex scenarios, where the covering number can become infinitely large, we propose a two-phase algorithm, Non-Convex Safe Least Squares Value Iteration (NCS-LSVI), which first reduces uncertainty about the safe set by playing a known safe policy. After that, it carefully balances exploration and exploitation to achieve the regret bound. Finally, numerical simulations on an autonomous driving scenario demonstrate the effectiveness of NCS-LSVI.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题背景**：强化学习（RL）在安全关键应用（如自动驾驶、机器人）中面临**瞬时硬约束**：在每个决策步骤必须满足安全性（例如避免碰撞），而非仅期望上满足。这些约束的决策空间可能是**非凸**甚至**非星凸**的（例如由避撞模块产生的断开的可行区域）。现有工作大多限于星凸空间或累积约束。
- **研究动机**：现有方法（Amani et al., 2021）在星凸设置下证明次线性遗憾，但存在关键错误——错误地直接引用无约束RL的覆盖数引理，忽略了依赖于数据的安全集合的动态变化。此外，非星凸空间中覆盖数可能无限大，需要全新算法。
- **核心目标**：为线性MDP模型下的瞬时硬约束RL提供**高效、安全**的算法，在星凸和非星凸特征空间中均实现**零违规**和**次线性遗憾**。

### 2. 论文提出的方法论

- **核心思想**：通过控制价值函数类的**覆盖数**（covering number）来实现值感知一致集中（value-aware uniform concentration）。
- **关键技术细节**：
  - **Star-Convex 场景**：提出 **OCD（Objective–Constraint Decomposition）** 技术，将价值函数差异分解为目标参数差异和安全约束参数差异两部分。利用星凸性保证参数微小变化不会导致可行集剧烈变化，从而正确界定了覆盖数（包含 \( \sqrt{\log(1/\tau)} \) 项，修正先前工作错误）。
  - **Non-Star-Convex 场景**：提出 **NCS-LSVI（Non-Convex Safe Least Squares Value Iteration）** 两阶段算法：
    - **阶段一（纯安全探索）**：在初始安全动作的 \(\epsilon\)-邻域内随机采样（满足局部点假设），使得安全集估计稳定，限制覆盖数。
    - **阶段二（安全探索-利用）**：使用RLS估计安全集和Q函数，加入鼓励探索的bonus项 \( g_{kh,\nu} = \frac{2}{\tau} \beta_2 \|\phi(s,a) - \phi(s,a^0_s)\|_{(\Lambda^{k,\gamma}_h)^{-1}} H \)，保证乐观性和安全。
- **算法流程**：Algorithm 1 详细描述了NCS-LSVI的步骤，包括纯探索K'个episode，之后每步计算RLS更新、构建估计安全集 \( \mathcal{A}^k_h(s) \) 和Q函数 \( Q^k_h(s,a) = \langle \phi(s,a), w^k_h \rangle + b^k_h(s,a) \)，并选择最大化Q的动作。

### 3. 实验设计

- **场景**：自动驾驶合并场景（intersection merging），车辆需决策等待或加速通过，碰撞避免模块（Collav）使决策空间非星凸但满足局部点假设。
- **数据集/环境**：用连续状态空间（位置、速度）、离散动作网格（18×18），线性MDP特征 \(\phi(s,a)\) 由状态和动作构成。
- **Benchmark 与方法对比**：
  - 自身算法NCS-LSVI取不同纯探索长度 \(K' = 1, 300, 2000\)。
  - 安全子优基线：始终保持在初始安全策略的\(\epsilon\)-邻域内。
  - 无约束RL算法LSVI-UCB（Jin et al., 2020），会违反安全约束。
- **未见大规模标准基准数据集**（如MuJoCo），仅用自制场景。

### 4. 资源与算力

- 论文**未明确说明**使用的算力资源（GPU型号、数量、训练时长等）。仅称在模拟环境中运行，未提及具体计算需求。

### 5. 实验数量与充分性

- **实验数量**：主要展示了若干条遗憾曲线（图3、6-10），不同K'值及两个对比方法的比较。此外在附录中补充了星凸情况下的实验（图10）。
- **充分性与公平性**：实验规模较小，未做大规模重复或参数敏感性分析。对比方法较少，仅两个（一个安全子优、一个无安全约束），未与其它瞬时安全约束RL算法（如Shi et al. 2023）对比。因此实验覆盖有限，但作为理论性论文已足够验证主要结论。

### 6. 论文的主要结论与发现

- 在星凸和非星凸线性MDP下，提出的算法均可实现**零安全违规**（高概率）和**次线性遗憾**（\(\tilde{\mathcal{O}}(\sqrt{K})\)）。
- 星凸情况：纠正了先前工作中的覆盖数错误，给出正确遗憾界。
- 非星凸情况：首次给出非凸决策空间下瞬时硬约束RL的理论保证，通过纯探索阶段控制覆盖数。
- 模拟实验证实了次线性遗憾趋势和零违规，支持理论结果。

### 7. 优点

- **理论创新**：提出OCD技术，深入分析了安全约束下价值函数覆盖数的难题，解决了已有工作遗留的错误。
- **场景覆盖全面**：同时处理星凸和非星凸特征空间，并给出了相应的算法与理论界。
- **严格安全保证**：算法在整个学习过程中以高概率满足瞬时硬约束，无违反。
- **验证有效**：自动驾驶模拟实验展示了实际可行性，遗憾曲线符合理论。

### 8. 不足与局限

- **假设限制**：依赖局部点假设（Assumption 3.2），该假设保证了纯探索阶段的有效性，但未必在所有实际非凸场景成立。
- **线性MDP假设**：仍要求转移、奖励、代价均为特征线性函数，限制了在更复杂非线性环境的应用。
- **实验局限**：仅在一个自制自动驾驶场景上验证，缺乏标准基准和更多对比方法；实验规模小，未充分检验算法鲁棒性。
- **可扩展性问题**：非星凸情况下的遗憾界包含 \( \frac{1}{\epsilon^2 \iota^2} \) 因子，是否最优仍是开放问题。
- **计算细节未公开**：未说明超参数调优过程及算力消耗，复现难度较高。

（完）
