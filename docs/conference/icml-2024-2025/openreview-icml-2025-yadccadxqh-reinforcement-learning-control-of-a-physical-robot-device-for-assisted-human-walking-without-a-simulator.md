---
title: Reinforcement Learning Control of a Physical Robot Device for Assisted Human Walking without a Simulator
title_zh: 无需仿真器的物理机器人设备强化学习控制：用于辅助人类行走
authors: "Junmin Zhong, Emiliano Quinones Yumbla, Seyed Yousef Soltanian, Ruofan Wu, Wenlong Zhang, Jennie Si"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=yAdcCADXqH"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 强化学习控制确保人类安全
tldr: 针对外骨骼辅助步行场景，提出一种在线适应离线模仿专家策略（AIP）的强化学习控制方法。该方法无需仿真器，通过模仿人类专家演示学习初始策略，并在线微调以适应个体差异，同时通过约束确保人类安全。实验表明该方法能快速适应、低计算开销地实现个性化安全控制，为物理机器人安全控制提供了新思路。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-yadccadxqh/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1452, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-yadccadxqh/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1624, \"height\": 291, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-yadccadxqh/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1623, \"height\": 339, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-yadccadxqh/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1606, \"height\": 361, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-yadccadxqh/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1628, \"height\": 674, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-yadccadxqh/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1593, \"height\": 461, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-yadccadxqh/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1651, \"height\": 764, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-yadccadxqh/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1448, \"height\": 632, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-yadccadxqh/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1635, \"height\": 1847, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-yadccadxqh/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1601, \"height\": 978, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-yadccadxqh/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1781, \"height\": 339, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-yadccadxqh/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 896, \"height\": 204, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-yadccadxqh/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 839, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-yadccadxqh/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1782, \"height\": 105, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-yadccadxqh/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1427, \"height\": 131, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-yadccadxqh/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 903, \"height\": 185, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-yadccadxqh/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 615, \"height\": 412, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-yadccadxqh/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 616, \"height\": 414, \"label\": \"Table\"}]"
motivation: 现有RL方法难以在无仿真器的物理设备上实时安全控制外骨骼，面临数据有限、计算开销大和适应性问题。
method: 提出在线适应离线模仿专家策略（AIP），先利用人类行走演示离线学习模仿策略，再在线微调以适应个体差异并保证安全。
result: 在真实外骨骼上验证了方法可实现快速个性化安全控制，计算开销低。
conclusion: 该工作为无仿真器的物理机器人安全RL控制提供了可行方案。
---

## Abstract
This study presents an innovative reinforcement learning (RL) control approach to facilitate soft exosuit-assisted human walking. Our goal is to address the ongoing challenges in developing reliable RL-based methods for controlling physical devices. To overcome key obstacles—such as limited data, the absence of a simulator for human-robot interaction during walking, the need for low computational overhead in real-time deployment, and the demand for rapid adaptation to achieve personalized control while ensuring human safety—we propose an online Adaptation from an offline Imitating Expert Policy (AIP) approach. Our offline learning mimics human expert actions through real human walking demonstrations without robot assistance. The resulted policy is then used to initialize online actor-critic learning, the goal of which is to optimally personalize robot assistance. In addition to being fast and robust, our online RL method also posses important properties such as learning convergence, dynamic stability, and solution optimality. We have successfully demonstrated our simple
and robust framework for safe robot control on all five tested human participants, without selectively presenting results. The qualitative performance guarantees provided by our online RL, along with the consistent experimental validation of AIP control, represent the first demonstration of online adaptation for softsuit control personalization and serve as important evidence for the use of online RL in controlling a physical device to solve a real-life problem.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：软外骨骼（soft exosuit）在辅助人类行走时，面临缺乏高保真仿真器（因人体-机器人交互动力学复杂、软体执行器非线性、传感噪声和延迟等）的挑战。传统离线-在线强化学习方法通常依赖大量模拟数据或结构化环境，难以直接应用于生理设备的安全、高效控制。
- **整体含义**：本文提出一种无仿真器的在线强化学习控制框架——**AIP（在线适应离线模仿专家策略）**，旨在通过有限的人体行走示范数据学习初始策略，再通过在线微调实现个性化、安全的辅助控制，最终降低人类行走的肌肉努力。

### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：将离线模仿学习（Behavior Cloning, BC）与在线actor-critic学习（直接启发式动态规划，dHDP）相结合，形成“离线模仿→在线适应”的两阶段流程。关键点在于**数据为中心**而非算法为中心，通过提高数据质量（RIIV方法）来缓解分布偏移，并利用dHDP实现有限数据下的鲁棒学习。
- **关键技术细节**：
  - **状态与控制变量**：状态 $s = [t_A, d_A, t_C, d_C, \theta_f]^T$（表示步态相位时间点/时长和膝关节峰屈角）。控制变量 $u = [t_1, d_1, t_2, d_2]^T$（表示软执行器充气起始时刻和持续时间）。
  - **离线模仿学习**：使用单名受试者150个步态周期的数据（通过MoCap采集），采用行为克隆学习初始策略 $\pi(s)$，损失函数为动作散度（action divergence）$c_k = \frac{1}{2}(\pi(s_k) - \pi_k)^2$。
  - **数据质量改进（RIIV）**：先归一化步态周期比例（将实际时间转换为步态百分比），再使用生物力学文献中的上下界将状态归一化到[-1,1]，减少个体内/间变异。
  - **在线个性化控制**：使用dHDP（确定性策略梯度方法），学习最小化阶段成本 $c_k = \epsilon_s + \epsilon_e$，其中 $\epsilon_s = (s - \tilde{s})^2$ 保证步态正常性和安全约束，$\epsilon_e$ 为EMG肌肉努力（积分值）。在线训练基于每5步一个样本，共约30个样本进行一次策略更新，共训练约150步。
  - **安全约束**：执行器压强≤206.8 kPa，控制时序和时长限制在步态生理范围内，并设置状态误差容限。

### 3. 实验设计：数据集/场景、基准、对比方法
- **数据集/场景**：
  - **线下数据**：从1名受试者（S1）获取150个步态周期的MoCap和IMU数据（正常行走，无外骨骼辅助）。
  - **线上实验**：5名健康受试者（3男2女，平均年龄28岁），在跑步机以1 m/s恒定速度行走，外骨骼穿戴并实时控制。
  - **泛化实验**：7度斜坡行走（2名受试者）。
- **基准和对比**：
  - 离线部分：对比**RIIV方法**与直接归一化（**Direct**）在动作散度上的差异。
  - 在线部分：对比**离线策略固定**（Freeze） vs **在线协同适应**（AIP）；以及消融实验：对比**仅EMG目标**、**仅运动学目标**、**完整目标**。
  - 对比无外骨骼辅助的**基线**（Baseline）EMG努力。
- **评价指标**：阶段成本、峰值膝角误差（步态正常性）、EMG努力、收敛时间、动作散度。

### 4. 资源与算力
- 论文未明确提及GPU型号和数量。实验使用**Intel Core i9-12900K桌面处理器**，采用**PyTorch**实现。未报告具体训练时长，但线下训练200 episode，线上每session约150步（约10分钟），算力需求较低，符合“低计算开销”设计目标。

### 5. 实验数量与充分性
- **实验数量**：
  - 线下：1名受试者，150数据点，5个随机种子。
  - 线上：5名受试者，每人3次在线session，共约15组在线训练实验。
  - 消融实验：3种目标函数对比（在同一受试者上）。
  - 泛化实验：2名受试者斜坡行走（各3次）。
- **充分性与客观性**：
  - 优点是未选择性报告结果，所有5名受试者的结果均展示；消融实验设计清晰，验证了成本函数各成分的必要性。
  - 不足：样本量较小（仅5人），且均为健康年轻成年人；斜坡行走仅2人；线下数据仅来自1名受试者，可能存在过拟合风险；未与其他主流RL算法（如DDPG, SAC）在同一物理平台直接对比（论文解释因安全问题未使用随机策略）。

### 6. 论文的主要结论与发现
- RIIV数据质量改进方法显著降低了动作散度，提高了离线策略对真实步态的拟合度。
- 在线AIP方法能有效个性化适应不同受试者，使所有受试者EMG努力降低（平均约20%以上，最高达48.2%），并实现正常步态（峰值膝角误差小）。
- 人类单独适应无法一致改善性能，人-机共同适应才是EMG降低的关键。
- 控制目标必须同时包含运动学安全约束和EMG降低，缺一不可（消融实验证实）。
- AIP可泛化至斜坡行走场景。

### 7. 优点
- **无仿真器**：直接学习物理学系统，解决软外骨骼模型缺失的核心难题。
- **数据高效**：仅需少量离线演示（150步）即可初始化，在线收敛快（约150步）。
- **安全保证**：显式安全约束 + 理论收敛性与稳定性证明（附录F），确保人类受试者安全。
- **全面验证**：覆盖5人、消融、斜坡，且所有受试者结果均展示，无选择性发表。
- **可解释性**：通过分析控制时序与步态相位的调整，揭示了人-机协同适应机制。

### 8. 不足与局限
- **样本局限**：仅5名健康受试者，未覆盖老年人、残障人群；线下数据仅来源于1人，可能无法泛化至更广泛人群。
- **场景局限**：仅测试恒定速度（1 m/s）的水平路面和7度斜坡，未涉及变速、楼梯、不规则地面等复杂现实环境。
- **算法对比不足**：未与DDPG、SAC等经典方法在物理平台上比较（论文解释因随机策略可能危及安全而未尝试）。
- **硬件依赖**：使用高精度MoCap系统获取离线真值，实际部署中仅靠IMU可能有精度损失；执行器延迟（约0.2s充气、0.25s放气）虽被在线适应，但仍是性能瓶颈。
- **单侧控制**：仅控制单腿，未来需扩展到双侧协调。

（完）
