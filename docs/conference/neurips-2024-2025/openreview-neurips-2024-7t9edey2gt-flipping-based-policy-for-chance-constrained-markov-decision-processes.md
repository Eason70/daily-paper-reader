---
title: Flipping-based Policy for Chance-Constrained Markov Decision Processes
title_zh: 面向机会约束马尔可夫决策过程的翻转策略
authors: "Xun Shen, Shuo Jiang, Akifumi Wachi, Kazumune Hashimoto, Sebastien Gros"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=7t9eDEY2GT"
tags: ["query:safe-rl-cbf"]
score: 5.0
evidence: 机会约束下的安全强化学习
tldr: 针对带机会约束的安全强化学习问题，提出基于翻转的策略，通过投掷偏倚硬币在两个候选动作间选择，建立了机会约束MDP的贝尔曼方程并证明最优策略存在性，为概率安全约束下的决策提供了理论基础。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-7t9edey2gt/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1419, \"height\": 421, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-7t9edey2gt/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1426, \"height\": 403, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-7t9edey2gt/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1256, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-7t9edey2gt/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1238, \"height\": 390, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-7t9edey2gt/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1390, \"height\": 324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-7t9edey2gt/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1429, \"height\": 142, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-7t9edey2gt/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1446, \"height\": 272, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-7t9edey2gt/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1446, \"height\": 271, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-7t9edey2gt/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1444, \"height\": 285, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-7t9edey2gt/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1444, \"height\": 287, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-7t9edey2gt/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1353, \"height\": 737, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-7t9edey2gt/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 782, \"height\": 212, \"label\": \"Table\"}]"
motivation: 期望累积安全约束有时不适用于不确定性下的实际安全需求，机会约束更实用。
method: 提出基于翻转的策略，在状态依赖的偏倚硬币下选择动作，并证明最优性。
result: 建立了机会约束MDP的贝尔曼方程，理论证明了翻转策略的最优性。
conclusion: 为机会约束安全RL提供了新的策略框架和理论支撑。
---

## Abstract
Safe reinforcement learning (RL) is a promising approach for many real-world decision-making problems where ensuring safety is a critical necessity. In safe RL research, while expected cumulative safety constraints (ECSCs) are typically the first choices, chance constraints are often more pragmatic for incorporating safety under uncertainties. This paper proposes a \textit{flipping-based policy} for Chance-Constrained Markov Decision Processes (CCMDPs). The flipping-based policy selects the next action by tossing a potentially distorted coin between two action candidates. The probability of the flip and the two action candidates vary depending on the state. We establish a Bellman equation for CCMDPs and further prove the existence of a flipping-based policy within the optimal solution sets. Since solving the problem with joint chance constraints is challenging in practice, we then prove that joint chance constraints can be approximated into Expected Cumulative Safety Constraints (ECSCs) and that there exists a flipping-based policy in the optimal solution sets for constrained MDPs with ECSCs. As a specific instance of practical implementations, we present a framework for adapting constrained policy optimization to train a flipping-based policy. This framework can be applied to other safe RL algorithms. We demonstrate that the flipping-based policy can improve the performance of the existing safe RL algorithms under the same limits of safety constraints on Safety Gym benchmarks.

---

## 论文详细总结（自动生成）

# 论文结构化总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：在安全强化学习（Safe RL）中，通常采用期望累积安全约束（ECSC）来保证安全，但在实际不确定性环境下（如无人机轨迹规划、行星探测），更合理的约束是“在有限时域内以高概率满足安全要求”，即**联合机会约束（Joint Chance Constraint）**。然而，联合机会约束的求解极为困难。
- **核心问题**：机会约束马尔可夫决策过程（CCMDP）中，最优策略是否一定是随机策略？如何设计一种可实际求解且能保证最优性的策略形式？
- **整体含义**：本文首次从理论上证明了 CCMDP 的最优策略可以简化为一种**翻转策略**（flipping-based policy），即在每个状态下以状态依赖的概率在两个候选动作之间随机选择。这一结论为机会约束下的安全 RL 提供了新的策略框架和理论基础，并进一步给出了保守近似方法和实用算法，使得现有安全 RL 算法（如 CPO）能够通过训练翻转策略来提升性能。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：
  - 对于 CCMDP，定义价值函数 $V^\pi(s)$ 和动作价值函数 $Q^\pi(s,a)$，并引入联合概率 $P^*(s,a)$ 表示从 $(s,a)$ 开始未来 $T$ 步都安全的概率。
  - 通过概率测度优化问题（PMO）和翻转策略优化问题（FPO），证明存在一个**状态依赖的二进制分布**（两个候选动作及其概率）作为最优策略，即 flipping-based policy。
  - 为求解实际中的联合机会约束，证明其可被**保守近似**为期望累积安全约束（ECSC），从而利用成熟的安全 RL 算法（如 CPO）训练。
  - 提出参数化翻转策略的学习框架：先训练一组不同成本限（对应不同安全阈值）的确定性策略，然后通过线性规划（LP）求解最优线性组合（最多两个非零权重），得到翻转策略的权重和两个基策略。

- **关键技术细节**：
  - **定理1 & 2**：CCMDP 的最优值等于 FPO 的最优值，且存在一个翻转策略（状态依赖的二进制分布）达到最优。
  - **定理3**：当 $\alpha = 0$（几乎肯定安全）时，确定性策略即可达到最优。
  - **定理4**：类似结论推广到 ECSC 约束的 CMDP，翻转策略仍为最优。
  - **定理5**：在一定条件下，ECSC（$H_{\text{unsafe}}(\theta,s)\le\alpha$）是联合机会约束的保守近似（需选择足够大的 $\gamma_{\text{unsafe}}$ 和足够小的 $T$）。
  - **定理6**：参数化翻转策略问题（PFPRL）与参数化随机策略问题（PSPRL）最优值相等；若最优值函数关于成本限严格凸，则翻转策略优于确定性策略。
  - **定理7**：通过采样成本限 $S$ 个点并求解 LP，得到的近似翻转策略可通过 $S\to\infty$ 收敛到最优。
  - **定理8**：有限样本下，以概率 $1-\exp(-2N(\alpha_s-\tilde\alpha_s)^2(1-\gamma_{\text{unsafe}})^2)$ 保证 CPO 更新后的策略对原机会约束可行。

- **算法流程**（Algorithm 1 & 2）：
  1. 从 $[0,1]$ 均匀采样 $S$ 个成本限 $\tilde\alpha_i$。
  2. 对每个 $\tilde\alpha_i$，用现有安全 RL 算法（如 CPO）训练一个最优确定性策略 $\tilde\theta_i$。
  3. 求解线性规划 LP，得到最优组合（两个非零权重 $\nu_s(j^*)1,\nu_s(j^*)2$ 及其对应的策略索引 $j^*1,j^*2$）。
  4. 实现时，每步以概率 $\nu_s(j^*)1$ 采用策略 $\tilde\theta_{j^*1}$，否则采用 $\tilde\theta_{j^*2}$。

## 3. 实验设计

- **使用的场景 / 数据集**：
  - **数值例子**：点从 $(0,0)$ 到 $(15,15)$，规避两个圆形危险区域，受高斯扰动；评价指标为累积逆距离（奖励）和碰撞概率（机会约束）。
  - **Safety Gym 基准**：使用 `SafetyPointGoal2-v0` 和 `CarGoal2-v0` 环境（修改障碍物布局以保证任务可解）。

- **Benchmark 和对比方法**：
  - 对比方法：CPO (Achiam et al., 2017)、PCPO (Yang et al., 2020)、P3O (Zhang et al., 2022)、CUP (Yang et al., 2022)。
  - 基线：原始算法训练得到的确定性策略 vs. 基于该算法训练的翻转策略（由两个不同成本限的确定性策略组合而成）。

- **评价指标**：
  - 期望累积奖励（Reward）和期望累积成本（Cost / Safety）。
  - 碰撞概率（Violation Probability）在不同 $T$ 下的曲线（图4）。

## 4. 资源与算力

- 论文明确指出使用机器配置：Intel Core i7-14700 CPU，32GB RAM，NVIDIA 4060 GPU。
- 未明确报告单次训练时长或总计算量。仅说明每个算法运行在5（CPO, PCPO）或3（P3O, CUP）个随机种子上，训练500个epoch，测试60个epoch。
- **因此，算力信息不完全公开，但提供的硬件细节可大致评估。**

## 5. 实验数量与充分性

- **实验数量**：
  - 数值例子：5组独立仿真，每组1000条轨迹。
  - Safety Gym：CPO和PCPO在PointGoal2上5个随机种子，P3O和CUP在PointGoal2上3个种子；CarGoal2上所有方法3个种子。每个方法在10个成本限（40-180，间隔10）上训练并测试。此外还验证了不同 $T$ 下的碰撞概率（图4）。
- **充分性**：
  - 优势：覆盖了多个基线算法、两个环境、多种成本限，结果具有统计意义（误差棒）。
  - 不足：缺少消融实验（如改变采样个数 $S$、不同近似参数 $\gamma_{\text{unsafe}}$ 和 $T$ 的影响）；仅基于 Safety Gym，未在其他连续控制任务（如 MuJoCo 安全版）上验证；未与最新的安全 RL 方法（如 RCRL、ISSAFE 等）对比；翻转策略的固定权重（非状态依赖）与理论最优有差距，但未系统评估该差距的影响。

## 6. 论文的主要结论与发现

- **理论结论**：
  - CCMDP 的最优策略可通过状态依赖的二进制分布（翻转策略）实现（定理2）。
  - 联合机会约束可被期望累积安全约束保守近似（定理5），且后者也最优支持翻转策略（定理4）。
  - 当最优值函数关于成本限严格凸时，翻转策略优于确定性策略（定理6）。

- **实验发现**：
  - 数值例子：在相同碰撞概率（17%）下，翻转策略的平均奖励（1.8259）远高于确定性策略（0.8667），且轨迹分布显示它能更激进地穿越危险间隙从而获得更高奖励。
  - Safety Gym：对于 CPO、PCPO、P3O、CUP，在成本限与奖励具有凸性关系的区间内，翻转策略显著提升奖励，且不违反成本约束。但在非凸区间则无明显提升（符合定理6）。
  - 碰撞概率与期望累积成本呈正相关，且 $T$ 越大，相同成本下碰撞概率越高（验证定理5的保守性）。

## 7. 优点

- **理论贡献**：首次建立 CCMDP 的贝尔曼方程并证明翻转策略的最优性，将无限维概率测度优化简化为有限维问题。
- **实用框架**：提出保守近似将机会约束转化为 ECSC，使得现有安全 RL 算法（如 CPO）能够直接训练翻转策略，无需重新设计优化器。
- **通用性**：框架可适配多种安全 RL 算法，实验中验证了四种算法。
- **安全性保证**：提供了有限样本下的概率可行性保证（定理8），增加了实际部署的理论依据。
- **实验验证**：数值例子直观展示翻转策略的行为差异，Safety Gym 实验证明性能提升在多个基线上成立。

## 8. 不足与局限

- **算法局限性**：
  - 实际算法（Algorithm 1）的翻转权重是固定的（不依赖状态），与理论最优（状态依赖）存在差距（论文也承认这一点）。
  - 需要先训练多个确定性策略才能进行线性组合，计算开销较大；且需要事先知道成本限与奖励的凸性区间才能获得提升。
  - 无状态依赖的翻转概率可能限制在更复杂环境中的最优性。

- **实验覆盖不足**：
  - 仅测试了 Safety Gym 的两个环境，缺少在更复杂连续控制任务（如 Humanoid、Ant）或真实世界基准上的验证。
  - 未与最新的安全 RL 方法（如 CUP 本身、RADAR、FOCOPS 等）进行充分对比，仅将翻转策略应用于原算法本身。
  - 未系统分析参数 $S$、$\gamma_{\text{unsafe}}$、$T$ 对最终性能的影响（消融实验缺失）。
  - 实验显示翻转策略可能增大置信区间，论文解释为高斯噪声，但未通过控制方差实验来缓解。

- **理论假设**：
  - 要求连续性和紧致性假设（Assumption 1, 2），对于非连续系统或离散动作空间有局限。
  - 保守近似的有效性依赖于 $\gamma_{\text{unsafe}}$ 足够大且 $T$ 足够小，但未给出具体选择方法，仅建议“接近 1”。

- **其他**：
  - 论文未提供开源代码（虽然提交时包含匿名代码，但系统部署仍需额外工作）。
  - 对负面的社会影响讨论较为简略，仅声称未发现。

（完）
