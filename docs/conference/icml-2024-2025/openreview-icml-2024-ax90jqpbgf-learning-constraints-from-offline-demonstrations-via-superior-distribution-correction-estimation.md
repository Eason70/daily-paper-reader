---
title: Learning Constraints from Offline Demonstrations via Superior Distribution Correction Estimation
title_zh: 通过优越分布校正估计从离线演示中学习约束
authors: "Guorui Quan, zhiqiang xu, Guiliang Liu"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=Ax90jQPbgF"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 离线逆约束强化学习
tldr: 该论文提出离线逆约束强化学习求解器ICSDICE，从次优演示中学习可行约束，无需在线交互，适用于危险数据采集场景，学习到的约束可用于安全策略设计。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-ax90jqpbgf/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 838, \"height\": 495, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ax90jqpbgf/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 870, \"height\": 571, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ax90jqpbgf/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 809, \"height\": 362, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ax90jqpbgf/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 848, \"height\": 301, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ax90jqpbgf/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1758, \"height\": 438, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ax90jqpbgf/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1753, \"height\": 1475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ax90jqpbgf/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1769, \"height\": 562, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ax90jqpbgf/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1341, \"height\": 833, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-ax90jqpbgf/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 874, \"height\": 559, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-ax90jqpbgf/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1778, \"height\": 308, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-ax90jqpbgf/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-ax90jqpbgf/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 856, \"height\": 226, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-ax90jqpbgf/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 858, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-ax90jqpbgf/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 667, \"height\": 320, \"label\": \"Table\"}]"
motivation: 解决逆约束强化学习对在线交互环境的依赖问题。
method: 提出ICSDICE从优越分布中提取约束。
result: 在离线设置下有效学习约束。
conclusion: 扩展了逆约束RL的适用范围。
---

## Abstract
An effective approach for learning both safety constraints and control policies is Inverse Constrained Reinforcement Learning (ICRL). Previous ICRL algorithms commonly employ an online learning framework that permits unlimited sampling from an interactive environment. This setting, however, is infeasible in many realistic applications where data collection is dangerous and expensive. To address this challenge, we propose Inverse Constrained Superior Distribution Correction Estimation (ICSDICE) as an offline ICRL solver. ICSDICE extracts feasible constraints from superior distributions, thereby highlighting policies with expert-exceeding rewards maximization ability. To estimate these distributions, ICSDICE solves a regularized dual optimization problem for safe control by exploiting the observed reward signals and expert preferences. Striving for transferable constraints and unbiased estimations, ICSDICE actively encourages sparsity and incorporates a discounting effect within the learned and observed distributions. Empirical studies show that ICSDICE outperforms other baselines by accurately recovering the constraints and adapting to high-dimensional environments. The code is available at https://github.com/quangr/ICSDICE.

---

## 论文详细总结（自动生成）

# 论文总结：通过学习约束从离线演示中通过优越分布校正估计

## 1. 核心问题与整体含义（研究动机和背景）

- **研究问题**：传统逆约束强化学习（ICRL）需要在在线交互环境中不断采样，这在许多现实应用中（如自动驾驶、医疗、机器人）因数据采集危险或昂贵而不可行。本文旨在解决**离线ICRL**问题：仅从固定的离线数据集（包含专家演示和次优数据）中恢复未知的安全约束，从而推导出安全策略。
- **核心挑战**：①离线数据集覆盖有限，未访问状态存在不确定性；②传统ICRL依赖在线策略回滚；③离线ICRL存在严重的不适定性——多种约束组合都能解释相同专家行为。需要设计一个有意义的可识别目标。

## 2. 方法论：核心思想、关键技术细节、算法流程

### 核心思想
- 引入**优越分布（Superior Distributions）** 的概念：指那些累计奖励**超过**专家策略的访问分布。根据命题4.2，可行的约束函数必须满足：所有优越分布中至少有一个状态-动作对（state-action pair）被赋予正成本，而专家分布中所有状态-动作对成本为零。
- 将离线ICRL转化为两阶段优化：**前向阶段**（Forward Stage）——在给定当前成本函数下，通过求解带约束的马尔可夫决策过程（CMDP）得到最优分布（该分布必属优越分布）；**逆向阶段**（Inverse Stage）——更新成本函数，对优越分布的支持集分配高成本，以“惩罚”高风险区域，逐步逼近期望的专家分布。
- 通过交替优化，当最优分布与专家分布足够接近时，即可得到最终约束。

### 关键技术细节
1. **摆脱传统策略回滚约束**：直接优化**访问分布**（occupancy distribution）而非策略，将CMDP问题转化为凸优化问题。
2. **正则化对偶优化**：在目标中加入f-散度正则项（具体采用卡方散度），防止分布偏离离线数据集覆盖范围，使得学习分布具有稀疏性。
3. **稀疏性保障**：使用卡方散度对应的截断线性函数（ReLU形式），当时间的差分（TD error）小于阈值时，直接令分布为零，从而只对高奖励的风险区域分配成本，约束函数自然稀疏。
4. **折扣访问分布**：将离线数据集的访问分布从经验分布替换为**折扣访问分布**（定义5.1），实现无偏的拉格朗日乘子估计，解决传统DICE方法中吸收状态值函数估计偏差的问题。
5. **策略抽取**：从最终学习的最优分布中，通过优势加权回归（advantage-weighted regression）提取策略。

### 公式与算法流程（文字说明）
- **前向目标**（公式7-10）：引入拉格朗日乘子V(s)，将带约束的分布优化转化为无约束对偶问题。利用f散度的凸对偶性得到闭式解（公式9）：d*(s,a) = d_O(s,a)·1_{c=0}·w*_f(δV)。
- **逆向成本学习**（公式11-12）：最小化平方损失，使得优越分布中状态-动作对的成本接近1，同时通过专家分布上成本为零的约束和L2正则化控制稀疏性与泛化性。
- **算法1（ICSDICE）**：初始化c₀=0，迭代K次：①基于当前成本函数学习价值函数V_k；②求解分布d*_k并加入集合O_k；③更新成本函数c_k；④提取策略。

## 3. 实验设计

### 使用数据集/场景
- **离散网格世界（7×7 Gridworld）**：四种不同约束设置（如避免特定状态），提供专家轨迹（50条）和随机次优轨迹。
- **连续MuJoCo环境**：HalfCheetah(Obstacle)、Ant(LS)、Ant(Blocked)、Hopper(Blocked)、Walker(LS)共5种任务，引入预定义的硬约束（速度限制、关节角速度限制等）。数据集来自早期停止的SAC和PPO-lag算法。
- **现实HighD高速驾驶数据集**：利用commonroad-RL环境提取特征，构建“车速≤40m/s”和“车距≥20m”两种约束场景。使用CNN处理图像输入。

### Benchmark与对比方法
- **基线**：①行为克隆（BC）；②离线逆强化学习LS-IQ（Least Square Inverse Q-Learning）；③SMODICE；④OptiDICE-Constraint；⑤SMODICE-Constraint（加入奖励信息）。
- **评价指标**：约束违反率、可行累积奖励、ROC曲线下面积（AUC）。

## 4. 资源与算力

- **硬件**：论文提到使用搭载多个RTX 3090 GPU（24GB显存）的集群，每个任务使用一个节点。
- **训练时长**：在连续控制环境中，运行一个随机种子约需**40分钟**。
- **说明**：未明确说明使用的GPU数量，也未给出完整训练总时长。

## 5. 实验数量与充分性

- **实验数量**：在5个连续控制任务上+4个离散网格+2个现实交通任务，总计**超过10组**任务场景。每实验使用5个不同随机种子，报告均值±标准差。
- **对比全面性**：覆盖了纯模仿学习、离线RL、带约束离线RL等多种基线。
- **消融实验**：①“w/o discount”（不使用折扣分布）；②“w/o constraint”（去掉成本学习）；③不同ξ_r超参数影响。此外还评估了成本函数在不同专家比例（100% vs 50%）和可迁移性（修改奖励方向）。
- **充分性与公平性**：实验设计较为充分，指标客观（违反率、收益、AUC），并且对基线进行了奖励信息增强的公平处理（如添加奖励信号）。但未包含在线ICRL基线的迁移或对比，可能不完全体现离线与在线差距。

## 6. 主要结论与发现

- ICSDICE在所有环境下**一致地学习到稀疏且准确的约束**，同时获得低违反率和高收益的可行策略。
- 与OptiDICE-Constraint相比，ICSDICE在成本识别（ROC AUC）上显著更优，说明其学习到的成本函数更精确。
- 在可迁移性实验中，ICSDICE学到的成本能够适应新的奖励函数，而OptiDICE-Constraint和零成本策略均失败。
- 消融实验证实了折扣分布和稀疏性机制对无偏估计和成本可迁移性的关键作用。

## 7. 优点

- **首创性**：首个系统性地解决**离线ICRL**问题的工作。
- **理论支撑**：提供了优越分布与可行约束之间的充分必要条件（命题4.2），以及有限MDP下的收敛性分析（命题4.4）。
- **实用性**：通过稀疏性和折扣分布设计，解决了离线ICRL的不适定性和估计偏差问题，学到的约束可迁移到新环境。
- **实验丰富**：涵盖离散/连续/真实图像环境，评价指标全面，并提供开源代码。

## 8. 不足与局限

- **假设限制**：论文假设硬约束（ϵ=0）且奖励函数已知。在奖励未知或约束为软约束的现实中适用性有限。
- **收敛性分析有限**：仅在有限MDP框架下证明了有限步收敛，未提供一般连续环境下的收敛率或样本复杂度。
- **计算资源需求**：虽然采用离线方法，但训练仍需GPU（3090级别），且每个种子约40分钟，对大规模复杂任务可能成本较高。
- **实验覆盖的偏差风险**：所有连续任务均基于MuJoCo的特定改造，真实世界场景仅用HighD数据集（图像任务仅有AUC报告），实际安全关键应用（如医疗、无人机）未验证。
- **与在线ICRL对比缺失**：未与主流的在线ICRL方法（如MCLI、VC-LCS等）在同等资源下进行对比，无法定量评估离线学习带来的性能损失。

（完）
