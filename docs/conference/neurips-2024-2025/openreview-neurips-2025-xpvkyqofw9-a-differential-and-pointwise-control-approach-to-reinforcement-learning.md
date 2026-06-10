---
title: A Differential and Pointwise Control Approach to Reinforcement Learning
title_zh: 强化学习的微分与逐点控制方法
authors: "Minh Phuong Nguyen, Chandrajit L. Bajaj"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=xpVkYQofw9"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 从连续时间控制角度重新表述的微分强化学习，包含哈密顿结构
tldr: 连续状态动作空间强化学习在科学计算中样本效率低且缺乏路径一致性。本文从连续时间控制角度提出微分强化学习框架，通过微分对偶形式诱导哈密顿结构嵌入物理先验，无需显式约束即可保证轨迹一致性。开发的逐点阶段算法dfPO提升了样本效率与动态对齐。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-xpvkyqofw9/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1397, \"height\": 406, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-xpvkyqofw9/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1447, \"height\": 254, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xpvkyqofw9/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1313, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xpvkyqofw9/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1306, \"height\": 255, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xpvkyqofw9/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1309, \"height\": 588, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xpvkyqofw9/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1311, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xpvkyqofw9/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1305, \"height\": 568, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xpvkyqofw9/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1199, \"height\": 145, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xpvkyqofw9/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1303, \"height\": 209, \"label\": \"Table\"}]"
motivation: 现有强化学习在科学计算中缺乏物理一致性和样本效率。
method: 提出微分强化学习框架dfPO，从连续时间控制角度引入哈密顿结构。
result: 无需显式约束即保证路径物理一致性，提升样本效率。
conclusion: 微分强化学习为物理约束控制提供新范式。
---

## Abstract
Reinforcement learning (RL) in continuous state-action spaces remains challenging in scientific computing due to poor sample efficiency and lack of pathwise physical consistency. We introduce Differential Reinforcement Learning (Differential RL), a novel framework that reformulates RL from a continuous-time control perspective via a differential dual formulation. This induces a Hamiltonian structure that embeds physics priors and ensures consistent trajectories without requiring explicit constraints. To implement Differential RL, we develop Differential Policy Optimization (dfPO), a pointwise, stage-wise algorithm that refines local movement operators along the trajectory for improved sample efficiency and dynamic alignment. We establish pointwise convergence guarantees, a property not available in standard RL, and derive a competitive theoretical regret bound of $\mathcal{O}(K^{5/6})$. Empirically, dfPO outperforms standard RL baselines on representative scientific computing tasks, including surface modeling, grid control, and molecular dynamics, under low-data and physics-constrained conditions.

---

## 论文详细总结（自动生成）

# 论文总结：强化学习的微分与逐点控制方法

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：连续状态-动作空间的强化学习（RL）在科学计算领域面临两大核心挑战：样本效率低下以及缺乏路径上的物理一致性（pathwise physical consistency）。标准 RL 方法通常依赖全局价值估计，无法有效编码物理定律或结构先验，而模型基 RL（MBRL）又常需要获取完整奖励函数或其导数，这在许多科学计算问题中不可行（奖励仅能在沿轨迹的点上获得）。
- **整体目标**：提出一种新的强化学习框架——**Differential RL**（微分强化学习），将 RL 从连续时间控制的角度重新解释，通过微分对偶（differential dual）形式引入哈密顿结构，从而嵌入物理先验，无需显式约束即可保证轨迹一致性，并提升样本效率。

## 2. 方法论

- **核心思想**：将标准的离散时间累积奖励最大化问题转换为连续时间控制视角下的积分奖励最大化问题，并利用庞特里亚金最大值原理（Pontryagin's Maximum Principle）引入对偶变量（协态变量 \( p \)），形成哈密顿系统：
  - 哈密顿函数 \( \mathcal{H}(s,p,a) = p^\top f(s,a) - r(s,a) \)。
  - 通过最优动作 \( a^* = \arg\min_a \mathcal{H} \) 得到降阶哈密顿量 \( h(s,p) \)。
  - 状态和协态变量组成扩展向量 \( x = (s,p) \)，其演化由哈密顿梯度流描述：\( \dot{x} = \mathbf{S} \nabla h(x) \)，其中 \( \mathbf{S} \) 为辛矩阵。
- **关键技术细节**：
  - 使用可学习的评分函数 \( g(x) \approx h(x) \) 近似哈密顿量，并通过自动微分将策略参数化为 \( G_\theta = \text{Id} + \Delta t \, \mathbf{S} \nabla g_\theta \)。
  - 该参数化隐式编码了辛结构（symplectic form），作为物理先验注入学习过程。
- **算法：Differential Policy Optimization (dfPO)**
  - 一种逐点、阶段式（stage-wise）算法，类似于 Dijkstra 式的时间扩展。
  - 在每一阶段 \( k \) 使用当前策略收集轨迹和评分，将标签数据（状态与评分）加入回放缓冲池，训练新的评分网络 \( g_{\theta_k} \)，然后更新策略 \( G_{\theta_k} \)。算法确保新策略在旧策略已表现良好的点附近不偏离。
  - 输出最终策略 \( G_{\theta_{H-1}} \)。
- **理论保证**：建立了逐点收敛性定理（pointwise convergence），证明了各阶段误差随样本数增加而消失；导出了悔界（regret bound）\( \mathcal{O}(K^{5/6}) \)（在弱凸且线性有界的假设下）。

## 3. 实验设计

- **数据集 / 场景**：三个代表性的科学计算任务：
  1. **Surface Modeling**（曲面建模）：通过控制点对二维边界进行变形，优化基于形状指示函数分布导数的成本函数（类似材料工程中的目标形状）。
  2. **Grid-based Modeling**（网格建模）：在粗网格上施加控制，在细网格上评估，成本函数为细网格重建函数的变分形式。
  3. **Molecular Dynamics**（分子动力学）：以八丙氨酸（octa-alanine）的分子构象（二面角）为状态，利用 PyRosetta 计算能量作为成本，初始分布故意选择为小范围均匀分布以测试有限探索能力。
- **基准方法**：对比 12 种基线算法（6 种标准 RL 算法 + 6 种能量重塑变体）：
  - 标准算法：TRPO, PPO, DDPG, SAC, CrossQ, TQC（前缀“S-”）。
  - 能量重塑变体：使用 \( r(s,a) = \beta^{-t}(\frac12\|a\|^2 - F(s)) \)。
- **训练/测试设置**：
  - 前两个任务使用 100,000 步训练样本，分子动力学任务因奖励评估成本高仅用 5,000 步。
  - 每个模型在 200 个测试回合中评估，时间范围归一化到 [0,1]。
  - 所有实验在 NVIDIA A100 GPU 上运行，模型尺寸较小。
- **评估指标**：终端步骤的成本函数 \( F(s) \)（越低越好）。

## 4. 资源与算力

- **GPU 型号**：NVIDIA A100 GPU（单卡，未说明数量，推测单机单卡或多卡但未详述）。
- **训练时长**：论文在附录 Table 7 中给出了各算法的近似训练时间（小时）：
  - dfPO 约 1.0 小时；
  - 其他算法从 PPO 0.3h 到 TQC/CrossQ 2.0h 不等。
- **模型大小**：dfPO 模型大小为 0.17–0.66 MB（取决于任务），属于小型网络。
- **未明确说明**：未提及使用的 CPU 内存、存储等具体信息。

## 5. 实验数量与充分性

- **主要实验**：在三个不同科学计算任务上比较 13 种算法，每个任务使用 10 个随机种子，每个种子 200 个测试回合，报告均值和方差，并进行了 t 检验。
- **消融实验**：对主要基线算法（CrossQ, SAC, TQC, DDPG, PPO, TRPO）进行了超参数消融（如 critic 数量、熵系数、噪声、剪裁参数等），结果在附录 Table 2 和 Table 5 中。
- **额外实验**：在经典控制任务（Pendulum, Mountain Car, CartPole）上进行了附加评估（Table 8），结果显示 dfPO 表现合理，但优势不如科学计算任务明显。
- **评估客观性**：实验设计相对全面，包含多种竞争基线，使用标准库 Stable-Baselines3 实现，超参数变化下结果稳定。但科学计算任务的自定义成本函数和初始分布可能对传统 RL 不利，论文也讨论了这一点。总体上实验充分且公平。

## 6. 主要结论与发现

- **性能优势**：dfPO 在所有三个科学计算任务上一致优于 12 种基线，达到最低的终端成本值（最低能量或最优形状）。尤其在分子动力学任务上，标准 RL 算法（如 TRPO, PPO）完全无法收敛（成本 ~1842），而 dfPO 收敛至 53.34。
- **样本效率**：在低样本条件下（分子动力学仅 5,000 步），dfPO 仍能高效学习，而传统方法要么无法学习，要么需要更多数据。
- **物理一致性**：通过哈密顿结构嵌入的辛先验使得轨迹更符合物理动态，减少了无效探索。
- **理论贡献**：提供了 RL 中罕见的逐点收敛保证和维数无关的遗憾界（在特定假设下 \( \mathcal{O}(K^{5/6}) \)）。

## 7. 优点

- **新颖性强**：将 RL 与连续时间控制、庞特里亚金原理和哈密顿力学有机结合，提出了一个统一的理论框架。
- **算法简洁有效**：dfPO 不需要复杂的信任域约束或熵正则化，仅通过局部逐点更新即可实现高效学习。
- **理论扎实**：提供了逐点收敛证明和遗憾界，这在连续状态-动作空间的 RL 中较为少见。
- **实验设计全面**：涵盖多种科学计算场景，与大量基线对比，并进行了消融和统计检验。
- **实用性强**：代码已开源，易于复现。

## 8. 不足与局限

- **假设限制**：理论分析依赖于一定的 Lipschitz 条件和函数空间假设（如弱凸、线性有界），在实际问题中可能不完全满足。
- **实验覆盖不全面**：
  - 实验任务仅限于三个特定科学计算场景，虽然具有代表性，但未涵盖更广泛的科学计算问题（如多物理场、随机偏微分方程控制等）。
  - 标准 RL 基准（如 Pendulum, Mountain Car）上的优势不明显，说明 dfPO 在非科学计算领域可能不具备显著优越性。
- **计算成本与扩展性**：虽然模型较小，但算法需要逐阶段收集新样本并重新训练网络，阶段数等于回合步数 \( H \)，时间复杂度为 \( O(H^2 \epsilon^{-6}) \)，当 \( H \) 较大时可能昂贵。
- **对初始分布敏感性**：理论假设初始分布连续，实际中可能不满足。
- **缺乏与其他连续时间 RL 方法的直接对比**：文中仅在相关工作中提及，未与 Jia & Zhou (2023) 等连续时间 Q-learning 方法进行实验比较。

（完）
