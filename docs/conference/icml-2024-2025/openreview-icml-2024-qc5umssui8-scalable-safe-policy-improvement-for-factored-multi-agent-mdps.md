---
title: Scalable Safe Policy Improvement for Factored Multi-Agent MDPs
title_zh: 可扩展的因子化多智能体MDP安全策略改进
authors: "Federico Bianchi, Edoardo Zorzi, Alberto Castellini, Thiago D. Simão, Matthijs T. J. Spaan, Alessandro Farinelli"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=Qc5umSsUi8"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 面向多智能体MDP的可扩展安全策略改进，包括多无人机评估
tldr: 本文针对大规模多智能体系统安全策略改进困难的问题，利用蒙特卡洛树搜索和因子化价值函数，提出可扩展到多智能体领域的安全策略改进算法，并通过Max-Plus扩展约束联合动作以保证安全。在多智能体SysAdmin和多无人机任务上验证了有效性和可扩展性。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-qc5umssui8/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 848, \"height\": 260, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-qc5umssui8/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 775, \"height\": 1083, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-qc5umssui8/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 857, \"height\": 890, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-qc5umssui8/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1719, \"height\": 1121, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-qc5umssui8/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1737, \"height\": 638, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-qc5umssui8/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1767, \"height\": 828, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-qc5umssui8/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1025, \"height\": 496, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-qc5umssui8/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1009, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-qc5umssui8/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1774, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-qc5umssui8/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1752, \"height\": 472, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-qc5umssui8/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 907, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-qc5umssui8/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 872, \"height\": 602, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-qc5umssui8/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1787, \"height\": 1447, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-qc5umssui8/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1781, \"height\": 1042, \"label\": \"Table\"}]"
motivation: 现有安全策略改进方法无法应对大规模多智能体状态和动作空间。
method: 结合MCTS和Max-Plus约束选择联合动作，利用分解模型扩展性。
result: 在无人机等大规模多智能体场景中取得安全且高性能的策略。
conclusion: 因子化方法有效支持多智能体安全策略改进的可扩展性。
---

## Abstract
In this work, we focus on safe policy improvement in multi-agent domains where current state-of-the-art methods cannot be effectively applied because of large state and action spaces. We consider recent results using Monte Carlo Tree Search for Safe Policy Improvement with Baseline Bootstrapping and propose a novel algorithm that scales this approach to multi-agent domains, exploiting the factorization of the transition model and value function. Given a centralized behavior policy and a dataset of trajectories, our algorithm generates an improved policy by selecting joint actions using a novel extension of Max-Plus (or Variable Elimination) that constrains local actions to guarantee safety criteria. An empirical evaluation on multi-agent SysAdmin and multi-UAV Delivery shows that the approach scales to very large domains where state-of-the-art methods cannot work.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）
- **问题背景**：多智能体强化学习（MARL）在现实世界应用（如仓库机器人、环境监控无人机）中面临安全挑战——收集经验可能导致危险后果。离线RL通过学习历史数据来减少交互，但存在分布偏移导致性能不可靠。安全策略改进（SPI）旨在保证新策略性能不低于行为策略（π₀），但现有SPI方法（如SPIBB）在处理大规模多智能体场景时因状态和动作空间巨大而失效。
- **核心目标**：提出一种可扩展的多智能体安全策略改进算法，能在状态空间≥10⁴¹、动作空间≥10¹⁶的超大规模环境中，利用因子化结构实现安全且高效的策略提升。

## 2. 方法论
### 核心思想
- 融合**蒙特卡洛树搜索（MCTS）**、**因子化转移模型**和**因子化价值函数**，将单智能体SPI方法扩展到多智能体领域。
- 提出两种新颖的**约束动作选择策略**（Constrained Max-Plus 和 Constrained Var-El），保证安全约束始终满足，避免遍历全部联合动作。

### 关键技术细节
1. **高效局部状态-动作计数**：利用转移模型的因子化分解，将全局计数转为对局部依赖组件的计数，显著增大非引导（non-bootstrapped）状态-动作对的数量，提升样本效率。
2. **Factored-Value MCTS-SPIBB (FV-MCTS-SPIBB)**：算法流程：
   - 根据行为策略π₀采样一个联合动作ā。
   - 若( s̄, ā )属于**引导集**（未充分观测），则直接返回π₀的动作。
   - 否则，使用**Constrained Max-Plus**或**Constrained Var-El**仅从非引导局部动作空间中，通过消息传递求解最优联合动作，保证所选动作不属于引导集。
3. **Constrained Max-Plus**：为每个智能体定义非引导局部动作集，在消息传递时仅对这些动作最大化，确保最终联合动作安全。
4. **Constrained Var-El**：类似地，在Variable Elimination过程中限制搜索空间为非引导动作，保证最优性（适用于任意结构协调图，但复杂度较高）。

### 理论保证
- 在MCTS仿真次数趋于无穷、Max-Plus/Var-El收敛到最优（对无环图Max-Plus保证，Var-El适用于任意图）、UCB可分解的假设下，算法渐近收敛到SPIBB策略，满足ζ-近似安全改进。

## 3. 实验设计
### 数据集/场景
- **multi-agent SysAdmin**（经典MMDP基准）：环状和星状拓扑，状态空间9ⁿ，动作空间2ⁿ（n为智能体数）。
- **multi-UAV Delivery**（来自Choudhury et al., 2021）：动态协调图，无人机移动、避免碰撞、到达目标区域。

### Benchmark与对比方法
- 对比方法：
  - **SPIBB** (Laroche et al., 2019)
  - **Lower-SPIBB、DUIPI、Adv-Approx-Soft-SPIBB、Lower-Approx-Soft-SPIBB、Approx-Soft-SPIBB**（均为基于策略迭代的SPI方法）
  - **MCTS-SPIBB** (Castellini et al., 2023，单智能体MCTS-SPI)
  - **FV-MCTS-Max-Plus / FV-MCTS-Var-El**（无安全约束的基线）
- 本文方法：FV-MCTS-SPIBB-Max-Plus 和 FV-MCTS-SPIBB-Var-El。

### 实验设置
- 评估指标：平均回报 ρ̄(π, M*)、15% CVaR（最差情况性能）。
- SysAdmin：100次运行×20步；UAV：50次运行×50步。
- 数据集大小（轨迹数）：SysAdmin中从5到50000，UAV中从50到20000。

## 4. 资源与算力
- 论文中**未明确提及**所使用的GPU型号、数量、训练时长等算力信息，仅提到代码已开源（GitHub）。实验主要依赖CPU模拟运行MCTS，算力需求适中，但未给出具体硬件配置。

## 5. 实验数量与充分性
- **实验数量**：覆盖两个领域、多种拓扑（环、星）、多种智能体规模（4~32）、多种数据集大小、多种对比方法，并进行了超参数敏感性分析（探索常数、树深度、仿真次数）。
- **充分性**：实验设计较为全面，既验证了可扩展性，也验证了安全性（与无安全约束的基线对比），还进行了样本效率对比。所有对比方法在同一条件下运行，结果客观。但未在更大规模（如100+智能体）或更复杂场景（如竞争环境）中测试，存在一定局限性。

## 6. 主要结论与发现
1. **可扩展性**：在环状SysAdmin中，FV-MCTS-SPIBB-Max-Plus可扩展到32个智能体，而MCTS-SPIBB在24个智能体时已失败；Var-El版本可到16个智能体。
2. **安全性**：在小数据集（如5条轨迹）下，无安全约束的FV-MCTS-Max-Plus性能低于行为策略，而FV-MCTS-SPIBB始终优于或等于π₀，验证了安全保证。
3. **样本效率**：因子化计数使非引导状态-动作对更多，在相同数据集下FV-MCTS-SPIBB比MCTS-SPIBB获得更高性能提升（如8智能体时约22 vs 13）。
4. **多无人机场景**：8和16个智能体下均能显著提升行为策略（回报从~450提升至~650/750），且安全性维持。

## 7. 优点
- **方法创新**：首次将MCTS-SPIBB扩展到多智能体，巧妙利用因子化结构和约束消息传递避免穷举联合动作，理论上有安全保证。
- **可扩展性强**：在超大规模（10⁴¹状态、10¹⁶动作）场景中仍可运行，远超现有SPI方法。
- **实验详尽**：涵盖不同拓扑、不同智能体数、不同数据集大小，并与无安全基线对比有力证明安全性。
- **代码开源**：便于复现和后续研究。

## 8. 不足与局限
- **理论假设较强**：需要MCTS仿真无穷、UCB可分解等假设，实际中可能不完全满足；Max-Plus在循环图上不保证最优，虽经验有效但无理论保证。
- **Var-El扩展性有限**：随树宽度指数增长，仅适用于较小规模（≤16智能体）。
- **实验覆盖有限**：未在高维连续动作空间或部分可观测环境中测试；未与最新深度离线MARL方法（如OMAR、CQL等）对比（但那些方法通常缺乏安全保证）。
- **硬件资源不明确**：缺少对计算成本的定量描述，难以评估实际部署代价。
- **仅考虑合作场景**：未涉及竞争或混合任务，安全定义可能需调整。

（完）
