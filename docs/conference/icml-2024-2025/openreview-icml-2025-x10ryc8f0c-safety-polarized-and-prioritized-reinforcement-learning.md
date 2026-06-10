---
title: Safety-Polarized and Prioritized Reinforcement Learning
title_zh: 安全极化与优先级强化学习
authors: "Ke Fan, Jinpeng Zhang, Xuefeng Zhang, Yunze Wu, Jingyu Cao, Yuan Zhou, Jianzhu Ma"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=x10ryC8F0C"
tags: ["query:safe-rl-cbf"]
score: 9.0
evidence: 提出MaxSafe安全强化学习框架，优先最小化不安全概率
tldr: 该文针对安全优先的现实应用，提出一个机会约束双层优化框架MaxSafe，先最小化不安全概率再最大化回报。设计定制Q学习算法学习最优动作掩码，并引入安全极化和安全优先级经验回放技术以支持大规模实验。理论证明收敛性，实验表明在多个安全RL基准上取得优异的安全性能。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-x10ryc8f0c/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1659, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x10ryc8f0c/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1339, \"height\": 863, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x10ryc8f0c/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1344, \"height\": 846, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x10ryc8f0c/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1604, \"height\": 531, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x10ryc8f0c/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1625, \"height\": 832, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x10ryc8f0c/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1646, \"height\": 1522, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x10ryc8f0c/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1658, \"height\": 1518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x10ryc8f0c/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1345, \"height\": 1726, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x10ryc8f0c/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1408, \"height\": 1958, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-x10ryc8f0c/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1366, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-x10ryc8f0c/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1121, \"height\": 848, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-x10ryc8f0c/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 828, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-x10ryc8f0c/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1362, \"height\": 424, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-x10ryc8f0c/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1829, \"height\": 763, \"label\": \"Table\"}]"
motivation: 现有安全强化学习方法常将安全作为约束置于回报之后，而现实应用中安全应是第一优先级。
method: 提出MaxSafe框架，使用机会约束双层优化，先最小化不安全概率，再在安全策略中最大化回报。
result: 在多个安全强化学习基准任务上，MaxSafe在安全违反率上显著低于现有方法，同时保持较高的回报。
conclusion: 安全极化方法有效实现了安全优先的强化学习，为实际安全关键应用提供了可靠框架。
---

## Abstract
Motivated by the first priority of safety in many real-world applications, we propose \textsc{MaxSafe}, a chance-constrained bi-level optimization framework for safe reinforcement learning. \textsc{MaxSafe} first minimizes the unsafe probability and then maximizes the return among the safest policies. We provide a tailored Q-learning algorithm for the \textsc{MaxSafe} objective, featuring a novel learning process for \emph{optimal action masks} with theoretical convergence guarantees. To enable the application of our algorithm to large-scale experiments, we introduce two key techniques: \emph{safety polarization} and \emph{safety prioritized experience replay}. Safety polarization generalizes the optimal action masking by polarizing the Q-function, which assigns low values to unsafe state-action pairs, effectively discouraging their selection. In parallel, safety prioritized experience replay enhances the learning of optimal action masks by prioritizing samples based on temporal-difference (TD) errors derived from our proposed state-action reachability estimation functions. This approach efficiently addresses the challenges posed by sparse cost signals.  Experiments on diverse autonomous driving and safe control tasks show that our methods achieve near-maximal safety and an optimal reward-safety trade-off.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：在自动驾驶等安全关键应用中，安全必须是第一优先级，而现有强化学习方法常将安全作为回报的约束（例如CMDP框架），只能保证用户指定的安全预算，无法实现最小化不安全概率。此外，现有方法依赖密集成本信号，难以处理稀疏但后果严重的成本（如碰撞）。
- **整体含义**：论文提出一个机会约束双层优化框架 **MaxSafe**，旨在**先最小化不安全概率，再在安全策略中最大化累积回报**，从而在理论上实现“安全最优”和“回报最优”的兼顾。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将安全目标形式化为双层优化：外层最大化回报，内层要求策略属于不安全概率最小的策略集合。通过**最优动作掩码**实现安全策略的提取：每个状态只允许选择具有最小不安全概率的动作。
- **关键技术细节**：
  - **状态-动作可达性估计函数（SA-REF）** ψπ(s,a)：估计当前策略π下，从(s,a)出发最终进入不安全状态的概率。通过反向迭代（Lemma 4.2, Theorem 4.3）收敛到最优SA-REF ψ*。
  - **最优动作掩码** Cζ(s) = {a | ψ*(s,a) ≤ ζ(s)}，其中 ζ(s)=min_a ψ*(s,a)，状态依赖的安全阈值是关键创新。
  - **安全Q学习**：Q更新时，下一状态的动作选取仅限于掩码集合，理论证明收敛到最优策略（Theorem 4.4）。
  - **安全极化**：用一个单调递增的极化函数 fpol（如10·log(x)）对Q值进行软惩罚：Q(s,a) + fpol(1-ψ(s,a))，从而避免硬掩码带来的早期训练问题。
  - **安全优先级经验回放（Safety PER）**：根据SA-REF的TD误差对经验进行优先采样，提高稀疏成本信号下的学习效率。

### 3. 实验设计：数据集/场景、Benchmark、对比方法

- **实验场景**：
  - 自动驾驶任务（highway-env）：TwoWay、Merge、Roundabout、Intersection。
  - 经典安全控制任务：自适应巡航控制（ACC）、圆形区域保持（Circle）。
- **评估指标**：**SWU（Safety-Weighted Utility）** 分数（兼顾报酬和安全）、崩溃率（Crash Rate）、回合奖励（Episode Reward）。
- **对比方法**：
  - **无安全约束**：DQN。
  - **奖励塑造**：RewsDQN（碰撞时惩罚-10）。
  - **直接ε-掩码**：SafeQ（固定阈值ε=0.1）。
  - **动作修正**：Recovery RL（基于安全批评家的恢复策略）。
  - **CMDP方法**：RCDQN（拉格朗日法）、RESPO、PPOLag（基于PPO）。所有baseline尽可能统一为DQN基实现以确保公平。

### 4. 资源与算力

- 论文**未明确说明** GPU 型号、数量或训练时长。仅提供超参数（学习率、批量大小、隐藏层尺寸等），在常规工作站上即可复现。这可能是发表格式惯例，未强调算力。

### 5. 实验数量与充分性

- **实验数量**：共6个任务（4个 highway + 2 个经典控制），每个任务用6个随机种子运行，报告均值和置信区间。此外进行了**消融实验**（极化函数选择、直接硬掩码对比）。总体实验量适中。
- **充分性与公平性**：
  - 优点：对比了多种类型baseline（无约束、奖励塑造、直接掩码、动作修正、CMDP），覆盖了主流安全RL范式。
  - 不足：所有baseline统一为DQN实现，但PPO基的RESPO和PPOLag在稀疏成本下表现极差，可能存在调参不足（论文已说明基线“fail to optimize”）。
  - 缺乏连续动作空间的实验（仅离散动作），限制了通用性结论。
  - 缺乏与更多最新方法的对比（如CBF、CBF-SRL等）。

### 6. 论文的主要结论与发现

- **MaxSafe框架**（以安全极化+优先级经验回放实现）在几乎所有任务中取得了**最低碰撞率**或接近最低的碰撞率，同时保持**较高回报**，SWU分数显著优于所有baseline。
- 安全极化作为硬掩码的软泛化，能避免早期训练中的过度保守，且更易适应深度学习。
- 安全优先级经验回放有效加速了SA-REF的学习，对长视界稀疏成本场景尤为有效。
- 状态依赖的安全阈值（ζ(s)）比固定阈值（SafeQ）更优，理论证明其能收敛到全局最优安全策略。

### 7. 优点：方法或实验设计上的亮点

- **理论严谨**：给出了最优动作掩码、SA-REF收敛、Q学习收敛的完整证明。
- **方法创新**：机会约束双层优化、状态依赖最优掩码、安全极化软惩罚、优先级经验回放专门针对安全批评学习。
- **实验设计**：多场景、多seed、多指标，并提供了代码仓库，可复现。
- **实用价值**：稀疏成本场景下，SPOM_PER性能提升明显，贴合真实安全应用。

### 8. 不足与局限

- **实验覆盖**：仅测试离散动作空间，未扩展到连续控制；仅评估了自动驾驶和简单控制任务，未涉及机器人、游戏等更具挑战的环境。
- **偏差风险**：假设不安全状态是吸收态（episode终止），在实际中可能不成立（如一次碰撞后仍可继续但代价高昂）。
- **方法局限**：需要预选极化函数，不同函数对性能有影响（需调参）；双网络（Q和ψ）增加了计算开销。
- **公平性**：部分baseline（如RESPO、PPOLag）在稀疏成本下几乎未学习到有效策略，可能因超参数未充分调优而低估其性能。
- **应用限制**：状态依赖阈值需满足“最小不安全概率的充分分离”条件（公式15），在实际噪声环境中可能难以严格满足。

（完）
