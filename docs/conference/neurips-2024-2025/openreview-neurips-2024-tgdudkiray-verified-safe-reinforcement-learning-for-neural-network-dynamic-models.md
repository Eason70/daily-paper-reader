---
title: Verified Safe Reinforcement Learning  for Neural Network Dynamic Models
title_zh: 面向神经网络动态模型的可验证安全强化学习
authors: "Junlin Wu, Huan Zhang, Yevgeniy Vorobeychik"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=tGDUDKirAy"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 使用课程学习在神经网络动态模型上进行可验证安全强化学习
tldr: 在非线性神经动态系统中学习可验证安全的控制器是信任自主性的核心难题。本文提出三部分方法：课程学习逐步增加已验证安全时域，增量验证重用先前验证信息，以及学习多个验证子集。最大化性能同时提供形式化安全保证。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-tgdudkiray/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1310, \"height\": 603, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-tgdudkiray/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1432, \"height\": 2201, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-tgdudkiray/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1378, \"height\": 184, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-tgdudkiray/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1077, \"height\": 852, \"label\": \"Table\"}]"
motivation: 训练可形式验证安全的神经网络控制器仍是一大挑战。
method: 结合课程学习、增量验证和多子集学习，迭代提升已验证安全时域。
result: 成功学习到可验证安全且性能优异的神经控制器。
conclusion: 为神经动态系统的可验证安全控制提供了有效方法，推动了可信自主性发展。
---

## Abstract
Learning reliably safe autonomous control is one of the core problems in trustworthy autonomy. However, training a controller that can be formally verified to be safe remains a major challenge. We introduce a novel approach for learning verified safe control policies in nonlinear neural dynamical systems while maximizing overall performance. Our approach aims to achieve safety in the sense of finite-horizon reachability proofs, and is comprised of three key parts. The first is a novel curriculum learning scheme that iteratively increases the verified safe horizon. The second leverages the iterative nature of gradient-based learning to leverage incremental verification, reusing information from prior verification runs. Finally, we learn multiple verified initial-state-dependent controllers, an idea that is especially valuable for more complex domains where learning a single universal verified safe controller is extremely challenging. Our experiments on five safe control problems demonstrate that our trained controllers can achieve verified safety over horizons that are as much as an order of magnitude longer than state-of-the-art baselines, while maintaining high reward, as well as a perfect safety record over entire episodes. Our code is available at https://github.com/jlwu002/VSRL.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：在非线性神经动态系统中，如何学习一个既能最大化性能（如奖励）又能被**形式化验证安全**的控制器，是可信自主系统的一大挑战。
- **背景**：现有安全强化学习方法大多仅提供经验安全评估（如CMDP方法）或渐进/理想化假设下的安全证明（如李雅普诺夫/屏障函数），缺乏对神经网络控制器的具体、可计算的形式化安全保证。前向不变性方法在复杂非线性动态中难以适用。
- **本文立场**：采用**有限时域可达性验证**（K-step reachability）这一更务实的安全概念，结合先进的神经网络验证工具（α,β-CROWN），在可证明安全的前提下最大化控制性能。

## 2. 方法论：核心思想、关键技术细节、算法流程

### 核心思想
将深度强化学习与**可微分的可达性上近似**工具相结合，通过课程学习、增量验证和初始状态依赖的多控制器学习，实现长时域的可验证安全控制。

### 关键技术细节
1. **课程学习（Curriculum Learning with Memorization，Algorithm 1）**：
   - 将目标安全时域K划分为K个阶段，每个阶段k训练控制器使前k步被验证安全。
   - 使用可微分的边界传播工具（α,β-CROWN）计算前向可达集上界，并检查与不安全区域的交集。
   - 定义损失函数：`L(x) = L_SafeRL(x) + λ L_Bound(Suc ∪ B)`，其中`L_Bound`惩罚可达边界与不安全区域的交叠。
   - **记忆缓冲区B**：存储每阶段接近不安全的初始状态子区域，保证全程安全性。
   - 对初始状态区域S0进行自适应网格划分（基于安全相关维度梯度的分裂策略）。

2. **增量验证（Incremental Verification）**：
   - 将长时域K分解为若干短间隔（如[0,k1], [k1,k2], ...），每次仅构建短步数的计算图，显著降低GPU内存消耗。
   - 利用梯度迭代中参数变化小的特点，重用先前验证信息，加速训练。

3. **初始状态依赖控制器（Initial-State-Dependent Controller，Algorithm 2）**：
   - 学习一个映射`h: S0 → Θ`，为不同初始状态子集分配不同的控制器参数。
   - 流程：对初始策略进行完整K步验证 → 将未验证区域按安全违反类型聚类 → 对每个聚类微调控制器 → 迭代直至全区域可验证安全。
   - 决策时根据初始状态选择对应的已验证安全控制器。

## 3. 实验设计

### 使用场景（5个控制问题）
| 场景 | 状态维度 | 特点 |
|------|----------|------|
| Lane Following（车道保持） | 3维 | 离散时间自行车模型，安全约束（横向位移、角度、速度） |
| Vehicle Avoidance（车辆避障，移动障碍物） | 4维 | 5个移动障碍物，安全约束（速度、角度） |
| 2D Quadrotor Fixed Obstacles（2D四旋翼固定障碍） | 6维 | 5个矩形固定障碍，角度和高度约束 |
| 2D Quadrotor Moving Obstacles（2D四旋翼移动障碍） | 6维 | 5个移动障碍 |
| 3D Quadrotor Fixed Obstacles（3D四旋翼固定障碍） | 12维 | 5个3D矩形障碍，动力学更复杂 |

### 对比方法（6个基线）
- PPO-Lag：带拉格朗日惩罚的PPO
- PPO-PID：PID拉格朗日方法的PPO
- CAP：自适应惩罚的模型基安全RL
- MBPPO：模型基约束PPO
- CBF-RL：控制屏障函数基RL
- RESPO：迭代可达性估计的安全RL

### 评估指标
- **Verified-K**：初始区域中可验证K步安全的比例
- **Verified-Max**：全区域可验证的最大步数
- **Emp-k**：采样1000万数据点的经验安全比例（k=K和k=全episode长度）
- **Avg Reward**：10个episodes的平均奖励（含标准差）

## 4. 资源与算力

- **硬件**：AMD Ryzen 9 5900X CPU（12核） + NVIDIA GeForce RTX 3090 GPU（24GB显存）。
- **训练时间**：文中未给出每个实验的总训练时长，但附录A.1给出了**20个训练epoch**的**增量验证运行时对比**（表2）。例如无增量验证时，20步的2D Quadrotor需152.1秒，有增量验证仅需19.6秒。说明增量验证显著加速。
- **总体算力**：单GPU可完成，算力需求适中。

## 5. 实验数量与充分性

- **主要实验**：在5个场景上对7种方法（VSRL + 6基线）进行了全面对比，报告了4项指标（Table 1），每个场景有明确结果。
- **消融实验**：
  - **增量验证消融**（表2）：在4个场景下对比有/无增量验证的运行时，证实必要性。
  - **多控制器消融**（表3）：在4个场景下对比单控制器 vs 多控制器的Verified-K比例，多控制器均达100%，单控制器在3D四旋翼仅74.7%。
- **充分性**：覆盖了不同维度、不同复杂度的动态系统，包含固定和移动障碍，基线方法多样。指标设计兼顾验证安全、经验安全和奖励。实验设计公平：相同初始区域、相同验证工具。但仅报告了一次数值结果（含标准差），未说明多次独立重复。

## 6. 主要结论与发现

- **验证安全显著提升**：VSRL在5个场景中均实现100% Verified-K（目标K值），而最佳基线仅达到K=14（2D四旋翼固定障碍）甚至更低。验证安全时域可达基线的**10倍**（车道保持：80 vs 8）。
- **经验安全完美**：在所有场景的全episode（如500步）上，VSRL均实现100%经验安全，而大多数基线存在违规（最高达40%以上）。
- **奖励性能**：除车道保持外，VSRL奖励与最佳基线相当或更好（如车辆避障401±4 vs 393±35）。车道保持奖励较低（214 vs 382），主要原因是安全优先于效率，可通过调整权衡。
- **务实有效性**：证明了有限时域可达性验证是实际可行的安全合成路径，即使理论保证弱于前向不变性，在实践中可实现完美安全记录。

## 7. 优点

- **创新性组合**：首次将课程学习、增量验证和初始状态依赖控制器结合到可验证安全RL中，解决长时域验证困难问题。
- **实用性强**：利用现有可微分验证工具（α,β-CROWN），可与任何可微验证方法兼容，具有扩展性。
- **实验全面**：覆盖多种动态系统（3D~12D），包含固定和移动障碍，对比基线充分，消融实验清晰。
- **代码开源**（GitHub），可复现。

## 8. 不足与局限

- **理论保证较弱**：仅保证有限时域（K步）安全，而非传统前向不变性（无限时域）。虽然实验显示整个episode的经验安全完美，但无法证明更长远的安全性。
- **依赖模型已知性**：假设动态F由ReLU神经网络精确表示且已知，实际系统需先进行近似建模，模型误差可能影响验证可靠性。
- **计算开销**：尽管增量验证缓解，但训练过程仍需要多轮验证和微调（尤其多控制器学习），在更大规模系统上可能耗时。
- **奖励权衡**：车道保持场景中奖励明显下降，说明安全验证可能牺牲效率，未全面探讨不同权衡参数的影响。
- **实验局限**：
  - 未报告多次独立重复的结果（仅一组数值+标准差），统计稳定性不够充分。
  - 未在高维复杂系统（如更多障碍或更大初始集）上测试。
  - 未与更近期的方法（如zonotope投影方法）对比（虽然文中列为相关工作）。
- **应用限制**：验证工具（α,β-CROWN）的紧缩度受网络深度和分支预算影响，可能不适用于极深网络或极高精度要求。

（完）
