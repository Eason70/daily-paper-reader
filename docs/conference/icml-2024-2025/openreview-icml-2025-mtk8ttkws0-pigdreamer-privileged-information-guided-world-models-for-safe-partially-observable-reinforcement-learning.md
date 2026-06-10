---
title: "PIGDreamer: Privileged Information Guided World Models for Safe Partially Observable Reinforcement Learning"
title_zh: PIGDreamer：特权信息引导的世界模型用于安全部分可观测强化学习
authors: "Dongchi Huang, Jiaqi WANG, Yang Li, Chunhe Xia, Tianle Zhang, Kaige Zhang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=mtk8tTKWs0"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 特权信息引导的世界模型用于安全部分可观测强化学习
tldr: 本文针对部分可观测环境下安全强化学习难以识别风险的问题，提出Asymmetric Constrained POMDP理论框架，并设计PIGDreamer模型，在训练时利用特权信息增强安全性。理论分析证明了特权信息带来的优势，实验表明该方法在部分可观测安全RL任务中显著降低成本违反。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-mtk8ttkws0/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1710, \"height\": 778, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mtk8ttkws0/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 866, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mtk8ttkws0/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 838, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mtk8ttkws0/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1770, \"height\": 728, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mtk8ttkws0/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 834, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mtk8ttkws0/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1767, \"height\": 564, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mtk8ttkws0/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 835, \"height\": 295, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mtk8ttkws0/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 686, \"height\": 561, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mtk8ttkws0/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1762, \"height\": 702, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-mtk8ttkws0/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 828, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mtk8ttkws0/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 946, \"height\": 1792, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mtk8ttkws0/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 905, \"height\": 836, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mtk8ttkws0/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 627, \"height\": 1058, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mtk8ttkws0/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1764, \"height\": 378, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mtk8ttkws0/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1764, \"height\": 339, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mtk8ttkws0/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1767, \"height\": 325, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mtk8ttkws0/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1765, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mtk8ttkws0/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1763, \"height\": 261, \"label\": \"Table\"}]"
motivation: 部分可观测性阻碍安全RL识别风险和奖励。
method: 基于ACPOMDP框架，利用特权信息指导世界模型学习。
result: 在部分可观测环境中的安全性显著提升。
conclusion: 特权信息可有效缓解部分可观测性对安全RL的挑战。
---

## Abstract
Partial observability presents a significant challenge for Safe Reinforcement Learning (Safe RL), as it impedes the identification of potential risks and rewards. Leveraging specific types of privileged information during training to mitigate the effects of partial observability has yielded notable empirical successes. In this paper, we propose Asymmetric Constrained Partially Observable Markov Decision Processes (ACPOMDPs) to theoretically examine the advantages of incorporating privileged information in Safe RL. Building upon ACPOMDPs, we propose the Privileged Information Guided Dreamer (\textit{PIGDreamer}), a model-based RL approach that leverages privileged information to enhance the agent's safety and performance through privileged representation alignment and an asymmetric actor-critic structure.
Our empirical results demonstrate that \textit{PIGDreamer} significantly outperforms existing Safe RL methods. Furthermore, compared to alternative privileged RL methods, our approach exhibits enhanced performance, robustness, and efficiency.
Codes are available at: https://github.com/hggforget/PIGDreamer.

---

## 论文详细总结（自动生成）

# PIGDreamer 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：在真实世界的强化学习应用中，环境往往具有部分可观测性，即智能体无法直接获取底层状态，只能基于观测历史进行决策。这给安全强化学习带来了巨大挑战，因为难以准确识别潜在风险与奖励。
- **现有不足**：现有的安全强化学习方法大多假设完全可观测的马尔可夫决策过程（CMDP），忽略了部分可观测性；而部分可观测下的方法（如基于世界模型的SafeDreamer）虽然能利用历史信息，但仍面临计算和统计困难。
- **研究动机**：如何在部分可观测条件下，利用训练阶段可获取的特权信息（如底层状态、本体传感器等）来提升安全性和性能？目前对特权信息的理论理解和高效利用方法仍然不足。
- **核心贡献**：提出非对称约束部分可观测马尔可夫决策过程（**ACPOMDPs**）理论框架，证明了非对称输入能减少评论家更新次数并得到更优策略。在此基础上设计了**PIGDreamer**模型，通过特权表示对齐和非对称演员-评论家结构实现安全、高性能且高效的训练。

## 2. 方法论

### 核心思想
- 在训练阶段，利用特权信息增强世界模型、预测器、表示和评论家的学习；部署阶段只使用部分观测，保持轻量。
- 基于ACPOMDP框架，将评论家的输入从部分观测扩展到包含特权信息，从而更准确地估计价值函数并指导策略优化。

### 关键技术细节

1. **世界模型构建**：
   - 同时训练两个世界模型：**朴素世界模型**（仅基于部分观测）和**特权世界模型**（基于底层状态）。
   - 每个世界模型包含编码器、解码器、动力学模型、后验模型。
   - 在朴素世界模型中引入**Oracle后验**，使用特权信息增强表示，并通过**表示对齐损失**（`L_align`）迫使朴素表示接近Oracle表示。

2. **特权预测器**：
   - 奖励和成本预测器同时使用朴素表示和特权表示，以提高预测准确性。

3. **特权评论家**：
   - 奖励评论家和成本评论家接收朴素表示和特权表示，进行更精确的长期回报估计。

4. **Twisted Imagination**：
   - 同时使用两个世界模型生成抽象轨迹：从当前表示开始，演员根据朴素表示选择动作，然后两个世界模型分别预测下一步表示，直至想象展望H=15。这样生成同步的想象轨迹用于演员-评论家学习。

5. **约束策略优化**：
   - 采用**增广拉格朗日方法**将安全约束转化为无约束优化问题，在策略目标中加入惩罚项，确保满足成本阈值。
   - 目标函数：`L(θ) = - Σ [sg(Rλ) + ηH(π) - Ψ(Cλ, λ, μ)]`

### 公式与算法流程（文字描述）

- 世界模型损失：`L_ϕ = L_dyn + L_align + L_dec + L_pred`，分别对应动力学预测、表示对齐、输入重建、奖励/成本预测。
- 演员-评论家学习：基于想象轨迹计算TD(λ)回报Rλ和Cλ，利用增广拉格朗日法更新演员策略，评论家使用均方误差更新。

## 3. 实验设计

### 数据集/场景

- **Safety-Gymnasium**：包含5个任务（CarGoal1, PointButton1, PointGoal2, PointPush1, RacecarGoal1），智能体只能看到64×64的RGB图像。
- **Guard**：包含3个任务（GoalAnt8Hazards, GoalAnt8Ghosts, GoalHumanoid8Hazards），同样使用视觉输入。

### Benchmark

- 使用平均未折扣回合回报和平均未折扣回合成本作为指标。
- 所有方法在4M环境步后进行评估（每个任务评估10个回合，每回合1000步）。

### 对比方法

- **基线安全强化学习方法**：SafeDreamer, LAMBDA, Safe-SLAC, CPO, FOCOPS, PPO-Lag, TRPO-Lag。
- **特权信息变体**：Scaffolder(Lag), Informed-Dreamer(Lag), Distill-Dreamer(Lag)。
- 消融变体：PIG-No Rep（不对齐），PIG-Unprivileged（无特权信息），NLI（嵌套潜在想象代替Twisted Imagination）。

## 4. 资源与算力

- **明确说明**：实验使用单个A100-PCIE-40GB GPU（40GB显存），10 vCPU Intel Xeon处理器，72GB内存。
- 训练时间方面：
  - PIGDreamer平均训练时长约为33.68小时（2M步，各任务综合），相比SafeDreamer（27.51小时）增加约22.4%。
  - 与其他特权方法对比：Scaffolder(Lag)需要48.05小时（增加69%），Informed-Dreamer(Lag)需要29.16小时（增加10%）。
  - 本文方法在仅增加28%训练时间的情况下实现136%性能提升，体现了更好的效率。

## 5. 实验数量与充分性

- **实验数量**：
  - 在5个Safety-Gymnasium任务和3个Guard任务上进行了主实验。
  - 消融实验：撤除表示对齐、撤除所有特权信息、替换想象力方法（NLI）。
  - 超参数分析：表2、3、4、5列出详细设置。
  - 与模型无关方法对比：表7与CPO、FOCOPS等比较。
- **充分性评估**：
  - 使用了rliable库计算中位数、IQM、均值及95%置信区间，统计严谨。
  - 每个实验至少3个不同随机种子运行，结果鲁棒。
  - 对比方法覆盖了主流model-free和model-based方法，包括特权变体，公平性较好。
  - 不足之处：未在更多复杂场景（如连续动作高维任务）验证，但Guard和Safety-Gymnasium是公认的安全RL基准。

## 6. 主要结论与发现

1. **理论验证**：ACPOMDP框架证明，利用特权信息可减少评论家更新次数并得到更优策略（定理3.3），同时避免成本低估。
2. **性能领先**：PIGDreamer在所有任务上平均奖励超越现有方法，尤其在Guard上将奖励提升136%（相对Scaffolder等）。
3. **安全性优异**：接近零成本违反，远低于设定的成本阈值（2.0）。
4. **效率高**：相比其他特权方法（如Scaffolder），PIGDreamer在更短训练时间内取得更好效果。
5. **局限性发现**：在PointButton1任务中，特权信息未带来显著提升，说明某些特权类型对特定任务增益有限。

## 7. 优点

- **理论奠基**：首次从理论上分析特权信息在安全RL中的优势，提出ACPOMDP框架。
- **方法创新**：通过表示对齐、特权预测器、特权评论家以及Twisted Imagination等多种组件协同，有效利用特权信息，避免模型蒸馏的信息丢失。
- **高效实用**：仅增加少量训练成本（28%）却带来大幅性能提升，适合实际部署。
- **公平评估**：使用标准化基准和统计方法报告结果，对比全面。
- **开源性**：提供代码和详细超参数，便于复现。

## 8. 不足与局限

- **实验覆盖有限**：只在两类基准上测试，未涉及更复杂或真实世界场景（如机器人操控、自动驾驶），泛化性待验证。
- **特权信息依赖**：某些任务中特权信息无增益（如PointButton1），暗示需要自动选择或设计更适合的特权特征。论文未深入分析何时、何种特权信息有效。
- **偏差风险**：模拟器中获取的特权信息在sim-to-real中可能不准确，论文未讨论对实际部署的影响。
- **计算资源**：相比普通世界模型，需要同时训练两个世界模型，内存和计算有所增加（虽然增长可控）。
- **未探讨**：不同特权信息组合的效果、多约束场景下的表现、以及连续动作空间的特性等。

（完）
