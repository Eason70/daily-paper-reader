---
title: "C2IQL: Constraint-Conditioned Implicit Q-learning for Safe Offline Reinforcement Learning"
title_zh: C2IQL：面向安全离线强化学习的约束条件隐式Q学习
authors: "Zifan LIU, Xinran Li, Jun Zhang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=97N3XNtFwy"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 安全离线强化学习结合约束条件
tldr: 安全离线强化学习面临分布外问题导致策略不安全。C2IQL通过约束条件隐式Q学习，将隐式更新扩展到约束设置，并估计成本值函数，避免分布外动作，同时提升性能和安全性。实验证明其在多个安全离线RL任务中优于现有方法。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-97n3xntfwy/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 678, \"height\": 644, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-97n3xntfwy/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1686, \"height\": 777, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-97n3xntfwy/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1181, \"height\": 690, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-97n3xntfwy/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 490, \"height\": 662, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-97n3xntfwy/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 538, \"height\": 379, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-97n3xntfwy/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 540, \"height\": 378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-97n3xntfwy/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1240, \"height\": 719, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-97n3xntfwy/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1780, \"height\": 947, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-97n3xntfwy/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1244, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-97n3xntfwy/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1200, \"height\": 328, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-97n3xntfwy/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 464, \"height\": 501, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-97n3xntfwy/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1346, \"height\": 548, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-97n3xntfwy/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1668, \"height\": 441, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-97n3xntfwy/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1767, \"height\": 189, \"label\": \"Table\"}]"
motivation: 现有安全离线RL方法受分布外问题影响，导致策略不安全且次优。
method: 提出约束隐式Q学习，将隐式奖励价值函数扩展到约束设置，并估计隐式成本价值函数。
result: 在安全离线RL基准中有效避免了分布外动作，提升了安全性和奖励。
conclusion: C2IQL为安全离线RL提供了一种有效的隐式学习方法。
---

## Abstract
Safe offline reinforcement learning aims to develop policies that maximize cumulative rewards while satisfying safety constraints without the need for risky online interaction. However, existing methods often struggle with the out-of-distribution (OOD) problem, leading to potentially unsafe and suboptimal policies. To address this issue, we first propose Constrained Implicit Q-learning (CIQL), a novel algorithm designed to avoid the OOD problem. In particular, CIQL expands the implicit update of 
reward value functions to constrained settings and then estimates cost value functions under the same implicit policy. Despite its advantages, the further performance improvement of CIQL is still hindered by the inaccurate discounted approximations of constraints. Thus, we further propose Constraint-Conditioned Implicit Q-learning (C2IQL). Building upon CIQL, C2IQL employs a cost reconstruction model to derive non-discounted cumulative costs from discounted values and incorporates a flexible, constraint-conditioned mechanism to accommodate dynamic safety constraints. Experiment results on DSRL benchmarks demonstrate the superiority of C2IQL compared to baseline methods in achieving higher rewards while guaranteeing safety constraints under different threshold conditions.

---

## 论文详细总结（自动生成）

# 中文详细总结：C2IQL: Constraint-Conditioned Implicit Q-learning for Safe Offline Reinforcement Learning

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：强化学习（RL）依赖在线交互，但在自动驾驶、机器人等场景中，交互成本高、风险大。离线RL利用预收集数据集学习策略，避免了在线交互，但面临分布外（OOD）问题：智能体可能高估数据集外状态-动作对的价值，导致不安全策略。
- **核心问题**：安全离线强化学习（Safe Offline RL, SORL）需要在最大化累积奖励的同时满足安全约束。现有方法存在两个主要缺陷：
  - 不能完全避免OOD问题，仅通过检测或正则化缓解，仍可能产生不安全策略。
  - 约束处理不精准且不灵活：使用折扣成本近似非折扣累积成本，导致误判（假阳性/假阴性）；固定阈值无法适应动态安全预算。
- **整体目标**：提出一种既能完全避免OOD问题，又能精确、灵活处理约束的安全离线RL算法，实现高奖励与约束满足的双重目标。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 2.1 核心思想
- 基于**隐式Q学习（IQL）**扩展至约束设置，避免OOD问题。
- 引入**成本重建模型（Cost Reconstruction Model, CRM）**从折扣成本值重建非折扣累积成本，消除折扣近似误差。
- 设计**约束条件机制（Constraint-Conditioned Mechanism）**，将约束阈值作为输入，使策略能够根据剩余预算动态调整。

### 2.2 关键技术细节
1. **约束隐式Q学习（CIQL）**：
   - 利用约束惩罚更新（类似CPQ）将IQL的奖励价值函数扩展至约束场景，公式为：
     - $Q^{\pi}_{r|c}(s,a) = \mathbb{1}(Q^{\pi}_{c}(s,a) \leq \tilde{L}) Q^{\pi}_{r}(s,a)$
     - 使用分位数回归（expectile regression）更新价值函数。
   - 通过IDQL理论推导出隐式策略形式，并在此基础上估计成本价值函数，无需显式提取策略，避免OOD。

2. **成本重建模型（CRM）**：
   - 针对折扣成本近似的不准确性，CRM从多个折扣因子下的成本Q值重建非折扣累积成本。
   - 训练方式：使用离线数据集和随机生成数据，以MSE损失优化，输入为多个折扣成本值，输出为重建的非折扣成本。

3. **约束条件机制**：
   - 将约束阈值$\hat{L}$作为价值函数和策略网络的输入，如$V^{\pi}_{r}(s,\hat{L})$、$V^{\pi}_{c}(s,\hat{L})$。
   - 训练时随机采样阈值，使模型学习不同安全预算下的适应能力。

4. **整体算法流程（C2IQL）**：
   - 初始化网络：价值函数、Q函数、策略、CRM。
   - 每个迭代：采样转移，随机选择阈值；通过CRM获得重建成本；计算约束惩罚Q值；更新价值函数、成本价值函数、Q函数；提取策略（使用分位数回归权重）。

## 3. 实验设计

### 3.1 数据集与环境
- **主要环境**：Bullet-Safety-Gym，包含四类机器人（Ant, Ball, Car, Drone）和两类任务（Run, Circle）。
- **数据集**：DSRL（基于D4RL格式）预收集数据。
- **额外验证**：SafetyGymnasium上的7个更复杂任务（Point和Velocity任务）。

### 3.2 对比方法
- 基线方法包括：BCQ-Lag、BEAR-Lag（原始-对偶优化）、CPQ（约束惩罚）、COptiDICE（分布校正）、FISOR（可行性引导扩散模型）、VOCE（变分优化）、WSAC（加权安全演员-评论家）、CDT（约束决策Transformer）。

### 3.3 评价指标
- 归一化奖励回报：$R_{norm} = (R_\pi - R_{min})/(R_{max} - R_{min})$。
- 归一化成本回报：$C_{norm} = C_\pi / L$（L为阈值）。
- 测试三种不同安全阈值（小、中、大），全面评估约束满足与奖励最大化。

## 4. 资源与算力
- **硬件**：NVIDIA GeForce RTX 3080 GPU。
- **训练时长**：C2IQL单次训练约5小时41分钟（针对AntCircle任务，400,000次迭代），与其他方法相当（CDT最长约11.5小时，FISOR最短约2小时）。
- **未说明**：论文未提及使用的GPU数量、是否多卡训练等详细信息。

## 5. 实验数量与充分性
- **主要实验**：在Bullet-Safety-Gym的8个任务（4种机器人×2种任务）上对比8种基线，每种配置使用5个随机种子、10个评估回合、3个阈值，总计约8×8×5×10×3=9600次评估（粗略估算）。
- **消融实验**：移除CRM（C2IQL w/o CR）、移除约束条件（C2IQL w/o CC）、纯CIQL，在CarCircle和DroneCircle任务上对比，并展示训练曲线。
- **超参数分析**：对分位数参数$\kappa_1$和$\kappa_2$进行网格搜索分析。
- **鲁棒性实验**：向CRM输入添加不同级别噪声，测试性能退化。
- **额外验证**：在SafetyGymnasium的7个任务上对比FISOR和CDT。
- **充分性评估**：实验设计较为全面，覆盖多任务、多阈值、多种基线，消融和超参数分析合理；但缺乏在更复杂或高维任务（如人类驾驶数据）上的验证。

## 6. 论文的主要结论与发现
- C2IQL在大多数任务上实现了**最高奖励且满足约束**，优于所有基线。
- 相比现有方法，C2IQL能**灵活应对不同安全阈值**，阈值增大时奖励自然提升，而CDT等模型在某些阈值下表现不佳。
- **消融实验表明**：
  - 取消CRM会导致奖励下降（因成本估计不准确），取消约束条件会导致过于保守或成本超标。
  - CIQL（无二者）过于保守，成本接近零但奖励低。
- **成本重建模型**能显著减少假阳性/假阴性，提升约束满足精度。
- **约束条件机制**使策略能动态分配预算，提高鲁棒性。

## 7. 优点（方法/实验设计亮点）
- **理论创新**：将IQL隐式更新扩展到约束设置，反直觉地推导出成本价值函数的更新方法，避免OOD问题。
- **实用贡献**：成本重建模型有效解决折扣近似误差，约束条件机制增强灵活性，两者结合实现了精度与适应性的平衡。
- **实验严谨**：多任务、多阈值、多基线的系统性对比；消融实验清晰证明每个模块的贡献；超参数和鲁棒性分析增强了可信度。
- **代码可复现**：提供了详细的超参数表（附录B.2），便于复现。

## 8. 不足与局限
- **实验覆盖不足**：
  - 主要基于Bullet-Safety-Gym（机器人控制），缺乏真实世界机器人、自动驾驶等高维复杂场景验证。
  - 未测试极端数据分布（如数据集质量极低或高度专家数据）下的表现。
  - 成本类型单一（均为二元或连续成本），未涉及多约束或逻辑约束（如“不能进入特定区域”）。
- **计算开销**：成本重建模型需要预训练（1e6步），且训练C2IQL时间略长于部分轻量方法（如FISOR），可能限制在实时应用中的部署。
- **潜在偏差**：
  - 基线选择未包括最新的一些模型（如OASIS（2024）等），论文中提及OASIS但未纳入对比。
  - 超参数$\kappa_1$和$\kappa_2$在不同任务中可能需手动调整，通用性存疑。
- **理论局限**：隐式策略推导依赖于IDQL理论，假设凸损失函数，实践中分位数回归是凸的，但其他损失函数可能不满足。
- **通用性**：约束条件机制需要预定义阈值集合，且测试时需线性缩放（公式23），在长时域任务中可能引入误差。

（完）
