---
title: A Provable Approach for End-to-End Safe Reinforcement Learning
title_zh: 端到端安全强化学习的可证明方法
authors: "Akifumi Wachi, Kohei Miyaguchi, Takumi Tanabe, Rei Sato, Youhei Akimoto"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=3qDFW07Lw7"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 用于端到端安全的可证明终身安全强化学习
tldr: 现有安全强化学习方法难以保证从学习到运行全程的策略安全性。本文提出PLS方法，将离线安全强化学习与安全策略部署相结合，通过回归条件监督学习离线训练策略，并利用高斯过程谨慎优化目标回报参数。理论上证明了该方法能提供终身安全保证，实验验证了其有效性。为安全强化学习提供了可证明的新范式。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-3qdfw07lw7/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1434, \"height\": 656, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3qdfw07lw7/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1446, \"height\": 385, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3qdfw07lw7/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1402, \"height\": 681, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-3qdfw07lw7/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1446, \"height\": 736, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3qdfw07lw7/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1480, \"height\": 1670, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3qdfw07lw7/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1442, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3qdfw07lw7/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 668, \"height\": 452, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3qdfw07lw7/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1236, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3qdfw07lw7/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1132, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3qdfw07lw7/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1446, \"height\": 737, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3qdfw07lw7/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1460, \"height\": 1179, \"label\": \"Table\"}]"
motivation: 现有安全强化学习无法保证策略在全过程中的安全性。
method: 提出PLS方法，结合离线安全强化学习与基于高斯过程的安全策略部署。
result: 理论证明了终身安全保证，实验验证了安全性。
conclusion: PLS为安全强化学习提供了可证明的端到端安全方案。
---

## Abstract
A longstanding goal in safe reinforcement learning (RL) is a method to ensure the safety of a policy throughout the entire process, from learning to operation. However, existing safe RL paradigms inherently struggle to achieve this objective. We propose a method, called Provably Lifetime Safe RL (PLS), that integrates offline safe RL with safe policy deployment to address this challenge. Our proposed method learns a policy offline using return-conditioned supervised learning and then deploys the resulting policy while cautiously optimizing a limited set of parameters, known as target returns, using Gaussian processes (GPs). Theoretically, we justify the use of GPs by analyzing the mathematical relationship between target and actual returns. We then prove that PLS finds near-optimal target returns while guaranteeing safety with high probability. Empirically, we demonstrate that PLS outperforms baselines both in safety and reward performance, thereby achieving the longstanding goal to obtain high rewards while ensuring the safety of a policy throughout the lifetime from learning to operation.

---

## 论文详细总结（自动生成）

### 论文核心问题与整体含义（研究动机和背景）

- **核心问题**：在安全强化学习（Safe RL）中，确保策略从学习到运行的整个生命周期（lifetime）内始终满足安全约束，是长期追求但未被现有方法有效解决的目标。
- **背景**：现有的在线安全RL方法在训练初期容易违反安全约束，离线安全RL方法虽然训练阶段无风险，但部署时因分布偏移可能导致策略不安全或过于保守。现有方法难以同时保证高奖励回报和全程安全。

### 方法论：核心思想、关键技术细节与流程

- **核心思想**：将离线策略学习与在线安全策略部署相结合，通过**回归条件监督学习（RCSL）**（如Constrained Decision Transformer, CDT）离线训练策略，然后利用**高斯过程（Gaussian Processes, GPs）**在线上谨慎优化策略条件化的**目标回报向量**（target returns z = (R, G)），从而在保证安全的前提下最大化奖励。
- **关键技术细节**：
  - **离线策略学习**：使用RCSL（如CDT）从预先收集的离线数据集中学习策略π_z，该策略以目标回报z为条件。
  - **目标回报与实际回报的关系建模**：通过定理1证明，目标回报与实际回报之差可分解为高斯过程项、小偏差项和渐近可忽略项，为使用GPs建模提供了理论依据。
  - **安全探索与优化**：使用两个独立的GPs分别建模奖励和成本回报。在安全探索阶段，构造保守的安全集Y_N，选择不确定性最大的目标回报以扩大安全集；在奖励最大化阶段，在安全集内选择置信上界最高的目标回报。
  - **理论保证**：定理2保证每次迭代的选择都满足安全约束（概率≥1-Δ）；定理3保证在有限步数内找到近最优的目标回报。
- **算法流程**（文字说明）：
  1. 输入离线数据集、安全阈值b、初始安全集Z0、Lipschitz常数L。
  2. 通过RCSL（如CDT）离线训练条件化策略π_z。
  3. 安全探索阶段（0~N†）：
     - 根据GP上界和安全集递推公式更新Y_N。
     - 计算可能扩大安全集的候选集E_N，选择不确定性最大的z。
     - 更新GPs。
  4. 奖励最大化阶段（N†+1~N†+N♯）：
     - 在Y_N内选择置信上界最大的z。
     - 更新GPs。
  5. 长期运行：使用最终选择的目标回报z。

### 实验设计

- **数据集/场景**：使用**Bullet-Safety-Gym**和**Safety-Gymnasium**基准中的连续机器人运动任务，包括：
  - Ant-Run, Ant-Circle, Car-Circle, Drone-Run, Drone-Circle（来自Bullet-Safety-Gym）
  - Ant-Velocity, Walker2d-Velocity, HalfCheetah-Velocity, Hopper-Velocity（来自Safety-Gymnasium Velocity任务）
- **Baseline方法**：对比了六种离线安全RL方法：BCQ-Lag, BEAR-Lag, CPQ, COptiDICE, CDT, CCAC。
- **评价指标**：归一化的奖励回报和成本回报。安全定义为归一化成本≤1。
- **实验设置**：安全阈值b分别设置为20和40；每个算法运行5次，报告均值和标准差。此外还包括与CDT微调（CDT-FT）的对比实验。

### 资源与算力

- **计算资源**：论文明确说明使用工作站配置为**Intel Xeon Silver 4316 CPU @2.30GHz**和**1块NVIDIA A100-SXM4-80GB GPU**。未报告具体的训练时长或GPU总耗时，但提到GP优化只需少量迭代（约20次）且每次评估用20条轨迹，计算开销主要集中在离线策略训练阶段。

### 实验数量与充分性

- **实验数量**：在10个任务上进行了两组阈值（b=20,40）的实验，共约20个主要实验组。还包括与CDT-FT的对比（10个任务）、安全探索过程可视化（6个任务）。此外，论文未进行消融实验（如去掉GP或使用不同核），但进行了离线-在线微调对比。
- **充分性与公平性**：实验覆盖了多种运动控制任务，基线方法来自公开库（OSRL、DSRL）且使用默认超参数，结果以均值和标准差呈现，可视为公平。但缺乏对高随机性环境的评估，且未报告训练过程中的方差（如随机种子差异），略微削弱了结论的鲁棒性。

### 论文主要结论与发现

- PLS是唯一在所有任务和安全阈值下均满足安全约束的方法（归一化成本≤1），而所有基线方法至少在一种任务上违反约束。
- PLS在多数任务上获得了最高的或接近最高的奖励回报，实现了安全与奖励性能的良好平衡。
- PLS的安全探索阶段能有效保证探索过程中的安全性（图3显示偶尔违规但能迅速恢复）。
- 与CDT微调相比，PLS在实现相似最终奖励的同时，在线适应阶段的安全性违规数量显著减少。

### 优点

- **方法论创新**：首次将离线RCSL与基于GP的在线安全优化结合，实现了可证明的终身安全保证，解决了安全RL领域长期存在的难题。
- **理论严谨性**：提供了目标回报与实际回报关系的严格定理，并证明了安全性和近最优性，理论推导完整（附于附录）。
- **样本效率**：仅优化二维目标回报向量，在线交互次数少（约400条轨迹），远低于传统在线RL或微调方法，符合安全关键应用的低风险需求。
- **实验验证充分**：在多个具挑战性的连续控制任务上验证，与六种代表性基线对比，结果清晰展示PLS的优势。

### 不足与局限

- **理论假设的局限性**：定理1依赖于近确定性转移、初始覆盖、有界性、连续性等较强假设，实际环境中可能不完全满足。论文虽指出框架可作为更通用的元算法，但理论保证仅在假设成立时有效。
- **策略无法在线更新**：PLS在离线训练后策略固定，未利用在线数据进行策略网络更新。若环境存在分布偏移，固定策略可能无法适应，论文仅计划未来扩展至离线-在线持续学习。
- **对GP模型的依赖**：安全保证依赖于GP的准确建模，若GP方差估计不当或噪声假设不成立，可能导致违规。实验显示偶尔有违规，但能快速恢复。
- **实验覆盖不足**：未在高维或高度随机环境（如自动驾驶、无人机复杂场景）中测试；未报告不同随机种子下的稳定性和失败案例；缺乏对基线方法超参数调优的说明，可能影响公平性。
- **计算资源报告不完整**：未详细说明离线训练阶段的具体GPU耗时，仅描述硬件配置，不利于复现。

（完）
