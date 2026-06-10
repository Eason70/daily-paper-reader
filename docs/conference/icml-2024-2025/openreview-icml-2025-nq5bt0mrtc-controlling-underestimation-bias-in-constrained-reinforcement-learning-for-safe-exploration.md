---
title: Controlling Underestimation Bias in Constrained Reinforcement Learning for Safe Exploration
title_zh: 控制约束强化学习中的低估偏差以实现安全探索
authors: "Shiqing Gao, Jiaxin Ding, Luoyi Fu, Xinbing Wang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=nq5bt0mRTC"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 控制约束RL中的低估偏差以实现安全探索
tldr: 该论文识别出约束强化学习中成本价值函数低估是训练期约束违规的关键因素，提出记忆驱动内在成本估计（MICE）方法，引入内在成本以减少低估并控制偏差，受闪光灯记忆启发，有效提升安全探索能力。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1720, \"height\": 687, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 858, \"height\": 311, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1777, \"height\": 706, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1778, \"height\": 702, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1766, \"height\": 335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1773, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1776, \"height\": 648, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1769, \"height\": 652, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1769, \"height\": 658, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1766, \"height\": 331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1753, \"height\": 606, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1769, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1776, \"height\": 655, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1781, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nq5bt0mrtc/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1782, \"height\": 513, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-nq5bt0mrtc/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1682, \"height\": 712, \"label\": \"Table\"}]"
motivation: 减少约束强化学习训练过程中的安全违规。
method: 提出记忆驱动内在成本估计方法MICE。
result: 实验证明MICE有效降低约束违反次数。
conclusion: 为安全探索提供了新的偏差控制手段。
---

## Abstract
Constrained Reinforcement Learning (CRL) aims to maximize cumulative rewards while satisfying constraints. However, existing CRL algorithms often encounter significant constraint violations during training, limiting their applicability in safety-critical scenarios. In this paper, we identify the underestimation of the cost value function as a key factor contributing to these violations. To address this issue, we propose the Memory-driven Intrinsic Cost Estimation (MICE) method, which introduces intrinsic costs to mitigate underestimation and control bias to promote safer exploration. Inspired by flashbulb memory, where humans vividly recall dangerous experiences to avoid risks, MICE constructs a memory module that stores previously explored unsafe states to identify high-cost regions. The intrinsic cost is formulated as the pseudo-count of the current state visiting these risk regions. Furthermore, we propose an extrinsic-intrinsic cost value function that incorporates intrinsic costs and adopts a bias correction strategy. Using this function, we formulate an optimization objective within the trust region, along with corresponding optimization methods. Theoretically, we provide convergence guarantees for the proposed cost value function and establish the worst-case constraint violation for the MICE update. Extensive experiments demonstrate that MICE significantly reduces constraint violations while preserving policy performance comparable to baselines.

---

## 论文详细总结（自动生成）

### 论文总结：控制约束强化学习中的低估偏差以实现安全探索

#### 1. 核心问题与整体含义（研究动机和背景）
- **问题**：现有约束强化学习（CRL）方法在训练过程中普遍出现严重约束违反（constraint violations），限制了其在安全关键场景（如机器人、自动驾驶）中的部署。
- **关键发现**：论文识别出成本价值函数（cost value function）的**低估偏差（underestimation bias）** 是导致约束违反的主要因素。由于函数近似噪声，成本价值被低估，使得高风险状态显得安全，诱使智能体探索这些区域，频繁违反约束。
- **目标**：提出一种方法以缓解成本低估，在保证探索安全性的同时不牺牲策略性能。

#### 2. 方法论：核心思想、关键技术细节与算法流程
- **核心思想**：受人类“闪光灯记忆”（flashbulb memory）机制启发——人类会生动回忆危险经历以规避风险——论文提出**记忆驱动的内在成本估计（MICE）** 方法，引入内在成本（intrinsic cost）来修正低估偏差，并控制偏差方向以促进安全探索。
- **关键技术细节**：
  - **闪光灯记忆模块**：存储已探索过的不安全状态（高风险区域），使用随机投影层降维，并通过Johnson-Lindenstrauss引理保持距离近似。
  - **内在成本计算**：基于当前状态嵌入与记忆中k个最近邻的相似度求和（伪计数），采用核函数 \(K(x,y)=\frac{\xi}{l^2(x,y)+\xi}\)，归一化后作为内在成本 \(c_I\)。
  - **外在-内在成本价值函数**：\(Q^{EI}_C(s,a) = (1-\alpha)Q^{EI}_C(s,a) + \alpha(c_E + \beta c_I + \gamma \mathbb{E}_{s'}[Q^{EI}_C(s',a')])\)，其中\(\beta\)为内在因子，通过自适应偏差校正机制调整：\(\beta' = \max\{\gamma^n(\beta_n - \alpha \epsilon_n / c_I), 0\}\)，\(\epsilon_n = Q_n - Q^*\)为上一轮估计偏差。
  - **优化目标**：将标准约束\(J_C\)替换为外在-内在累积折扣成本\(J^{EI}_C\)，并在参数空间内引入信任域约束（KL散度≤φ），确保更新的策略与记忆采样策略一致。
  - **求解方法**：提供两种实现：**MICE-CPO**（基于CPO的一阶近似+二阶KL约束，利用共轭梯度求解）和**MICE-PIDLag**（基于PID Lagrangian的拉格朗日乘子动态调整）。
- **理论保证**：
  - 定理4.3：给出任意两策略外在-内在约束差异的上界。
  - 定理4.4：MICE更新策略的最坏情况约束违反上界严格小于CPO（因包含内在成本项I）。
  - 定理4.5：在标准假设下，外在-内在成本价值函数以概率1收敛到最优值\(Q^*_C\)。

#### 3. 实验设计
- **数据集/场景**：
  - **Safety Gym**：4个导航任务（Point/Car + Goal/Circle），每个环境中包含障碍物（Hazards）和边界约束。
  - **Safety MuJoCo**：4个连续控制任务（Ant, HalfCheetah, Humanoid, Hopper），约束为速度上限。
- **Baseline方法**：
  - 主对比：PIDLag, CUP, Saute, Simmer（强调零违反）。
  - 额外对比：CPO（用于MICE-CPO），TD3成本价值函数等。
  - 消融实验：固定常数内在成本 vs. 记忆驱动内在成本；随机投影层有效性。
  - 敏感性分析：阈值（0,15,25）和KNN邻居数k。
- **评价指标**：累积折扣回报（越高越好）和累积折扣成本（需低于阈值25）。每组实验使用6个随机种子，报告均值和标准差。

#### 4. 资源与算力
- 论文在附录C.5明确提到：所有实验在**Ubuntu 20.04.2 LTS**上运行，使用单张**NVIDIA GeForce RTX 3090 GPU**，深度学习框架为PyTorch 2.0.0 + CUDA 11.3。
- 未明确说明每个实验的精确训练时长（总步数固定为1e7步，最大轨迹长度1000步），但可推测算力需求适中。

#### 5. 实验数量与充分性
- **实验数量**：
  - 主实验：8个环境 × 多个baseline（至少5种方法对比）→ 约40+组学习曲线。
  - 偏差验证实验（Figure 2, 5）：在多个环境中对比估计值与真实值。
  - 消融实验：内在成本替换为常数（3,5,15）；随机投影层有/无。
  - 敏感性分析：阈值（k=10固定，另测其他值）；阈值0,15,25。
  - 额外复杂任务：CarButton1, PointButton1。
- **充分性与公平性**：
  - 所有方法使用统一超参数设置（表1），在相同种子和步数下训练。
  - 实验覆盖了离散/连续动作空间、不同难度任务，并包含多种对比方法（包括最新状态增强方法）。
  - 多次消融和敏感性分析验证了各组件必要性，且理论推导与实验现象一致（如偏差渐近零）。
  - 唯一不足：未在真实机器人或仿真器外验证，但安全问题的常见做法。

#### 6. 主要结论与发现
- MICE在所有测试环境中**显著减少约束违反**（尤其在Safety MuJoCo中保持零违反），同时**策略回报与baseline相当或更优**。
- 记忆驱动的内在成本比固定常数更有效，能够精准抑制高成本区域的低估，而不过度保守。
- 内在成本配合自适应偏差校正，使成本估计偏差渐近收敛到零，验证了理论收敛性。
- MICE对约束阈值鲁棒，能够适应严格（0）或宽松（25）的设定。
- 随机投影层在不损失性能前提下大幅降低计算复杂度。

#### 7. 优点
- **问题定位准确**：首次明确指出CRL中的成本低估偏差是训练期约束违反的根源，并提供理论证明。
- **方法新颖且生物启发**：将闪光灯记忆机制引入CRL，内在成本设计巧妙（基于伪计数），且自适应误差校正避免过度保守。
- **理论完备**：包含收敛性证明、最坏情况违反上界、约束差异界，为方法提供坚实保证。
- **实验扎实**：多环境、多baseline、消融、敏感性分析全面，代码开源，可复现。
- **通用性强**：MICE可集成到不同CRL算法（CPO、PIDLag），且内存记录标准可灵活调整（如基于期望累积成本）。

#### 8. 不足与局限
- **实验覆盖范围**：仅仿真环境（Safety Gym / MuJoCo），未涉及真实机器人或自动驾驶等实际部署场景。论文提及可用离线数据集构建记忆，但未实验验证。
- **依赖成本信号质量**：当前存储规则“成本>0”依赖环境给出的精确成本，若成本带噪或延迟，可能效果下降。论文建议用期望累积成本作为替代，但未系统评估。
- **计算开销**：KNN搜索（O(MN)）和随机投影可能在高维状态空间或大记忆容量下成为瓶颈，虽然k设10且使用投影降维，但大规模场景需进一步优化。
- **超参数敏感**：内在因子β的初始值和更新率、KNN邻居数k、投影维度等需要调参，文中仅统一k=10，缺乏跨任务系统调参分析。
- **理论假设较强**：收敛性证明依赖表格型Q值和无限采样假设，在深度神经网络近似下需更严格分析。
- **分布偏移问题**：当策略快速变化时，记忆可能无法及时反映当前高风险区域，信任域约束虽部分缓解，但理论上界依赖TV散度，实际边界可能松弛。

（完）
