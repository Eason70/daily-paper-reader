---
title: "Real-DRL: Teach and Learn at Runtime"
title_zh: Real-DRL：运行时教学与学习
authors: "Yanbing Mao, Yihao Cai, Lui Sha"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=gXZlZAeqay"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 针对安全关键自主系统的运行时安全深度强化学习框架
tldr: 安全关键自主系统在线学习时需保证安全性。本文提出Real-DRL框架，包含深度强化学习学生、物理模型教师和触发器三部分，通过教师实时补丁与学生教学相长范式，确保运行时学习安全高效。物理教师提供安全备份，触发器根据安全状态调度采样。实验表明该方法在保证安全的同时提升了性能。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-gxzlzaeqay/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1370, \"height\": 719, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gxzlzaeqay/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 745, \"height\": 401, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gxzlzaeqay/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 725, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gxzlzaeqay/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 735, \"height\": 504, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gxzlzaeqay/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1433, \"height\": 514, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gxzlzaeqay/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 711, \"height\": 447, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gxzlzaeqay/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 966, \"height\": 822, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gxzlzaeqay/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 802, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gxzlzaeqay/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1416, \"height\": 811, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gxzlzaeqay/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1433, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gxzlzaeqay/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1442, \"height\": 873, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gxzlzaeqay/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1447, \"height\": 929, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-gxzlzaeqay/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1440, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gxzlzaeqay/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1449, \"height\": 472, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gxzlzaeqay/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 885, \"height\": 449, \"label\": \"Table\"}]"
motivation: 现有深度强化学习在线部署时难以同时保证安全和高性能。
method: 提出Real-DRL框架，结合物理模型教师、安全状态依赖采样和教学相长范式。
result: 在真实系统中实现了安全且高性能的运行时学习。
conclusion: Real-DRL为安全关键自主系统提供了有效的在线安全强化学习方案。
---

## Abstract
This paper introduces the Real-DRL framework for safety-critical autonomous systems, enabling runtime learning of a deep reinforcement learning (DRL) agent to develop safe and high-performance action policies in real plants while prioritizing safety. The Real-DRL consists of three interactive components: a DRL-Student, a PHY-Teacher, and a Trigger. The DRL-Student is a DRL agent that innovates in the dual self-learning and teaching-to-learn paradigm and the safety-status-dependent batch sampling. On the other hand, PHY-Teacher is a physics-model-based design of action policies that focuses solely on safety-critical functions. PHY-Teacher is novel in its real-time patch for two key missions: i) fostering the teaching-to-learn paradigm for DRL-Student and ii) backing up the safety of real plants. The Trigger manages the interaction between the DRL-Student and the PHY-Teacher. Powered by the three interactive components, the Real-DRL can effectively address safety challenges that arise from the unknown unknowns and the Sim2Real gap. Additionally, Real-DRL notably features i) assured safety, ii) automatic hierarchy learning (i.e., safety-first learning and then high-performance learning), and iii) safety-informed batch sampling to address the experience imbalance caused by corner cases. Experiments with a real quadruped robot, a quadruped robot in Nvidia Isaac Gym, and a cart-pole system, along with comparisons and ablation studies, demonstrate the Real-DRL's effectiveness and unique features.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在安全关键自主系统中，深度强化学习（DRL）在线运行时（real plant）必须同时保证安全性和高性能，但面临两大挑战：
  - **未知未知（Unknown Unknowns）**：系统动态包含已知已知（牛顿力学）、已知未知（噪声统计特性）以及未知未知（如深度神经网络庞大参数空间、不可预测环境如冻雨）。这些难以建模、难以仿真、缺乏历史数据，传统安全方法无法应对。
  - **Sim2Real 差距（Sim2Real Gap）**：仿真训练的策略部署到真实环境时会因环境差异导致性能显著下降甚至不安全。
- **研究背景**：现有安全DRL方法（如CLF类奖励、残差策略、Phy-DRL）多依赖于可管理的Sim2Real差距和未知未知假设，实际中难以保证安全；容错DRL（如Neural Simplex、运行时保证）假定高保证模块（物理模型控制器）具有安全保证，但模型失配（尤其动态环境）时仍会失效。
- **论文目标**：提出 **Real-DRL 框架**，使DRL代理在真实系统中在线学习时**优先保证安全**，同时学习高性能策略。框架通过物理教师实时补丁、学生双重学习范式、安全状态依赖采样，从理论到实现同时应对未知未知和Sim2Real差距。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：基于 Simplex 架构，构建三个交互组件——**DRL-Student**（学生）、**PHY-Teacher**（物理教师）、**Trigger**（触发器），实现运行时“教学相长”和“安全优先”学习。
- **关键技术细节**：
  - **DRL-Student**：采用 Actor-Critic 架构，拥有**双经验回放缓冲区**（自学习和教学学习）。其创新在于：
    - **双重学习范式**：在安全自学习空间（L）内通过自学习（trial-and-error）优化任务性能（如最小化旅行时间和能耗）；在边缘安全空间（S\L）通过教师教学学习安全。
    - **安全知情批量采样**（Safety-Informed Batch Sampling）：根据实时安全状态指标 \( V(s) = s^\top P s \) 动态分配来自教学缓冲区和自学习缓冲区的样本数量。当系统接近安全边界（\( V(s) \to 1 \)）时，更多采样来自教学（边缘案例）经验，解决经验不平衡问题。\( P \) 通过最大化体积椭球计算。
  - **PHY-Teacher**：基于物理模型（如牛顿力学）设计的**实时补丁**（Real-Time Patch）策略，专注安全功能。其关键：
    - 定义**实时补丁空间** \( \mathcal{P}_k \)（以当前状态 \( s(k) \) 缩小的安全区域）和**控制目标** \( s_k^* = \chi s(k) \)（\( 0<\chi<1 \)），确保目标在自学习空间内。
    - 通过**线性矩阵不等式**（LMI）在线求解反馈增益 \( F_k \)，使跟踪误差 \( e(t) \) 在未知模型失配 \( h(e) \) 有界假设下，状态始终保持在安全集 \( \mathcal{S} \) 内，且最终返回自学习空间 \( \mathcal{L} \)（定理5.2）。
    - **自适应机制**（附录F）：当模型失配超出假设阈值时，通过实时估计并施加补偿动作恢复假设有效性。
  - **Trigger**：监控实时安全状态，当系统状态离开自学习空间（\( s(k-1)\in\mathcal{L},\ s(k)\in\partial\mathcal{L} \)）时激活教师，教师接管控制直至状态返回空间 \( \mathcal{L} \)，然后切换回学生。
- **算法流程**（Algorithm 1）：学生主动控制，一旦触发条件满足，教师更新模型知识、计算实时补丁和安全策略，并控制植物同时产生教学经验数据；教师激活期间学生网络仍通过安全批量采样更新。学生重新获得控制后继续自学习。

## 3. 实验设计：数据集/场景、Benchmark、对比方法

- **实验场景**：
  1. **真实四足机器人（Unitree A1）室内环境**：在真实机器人上运行，设置与仿真不同的速度命令（0.35 m/s vs 0.6 m/s），引入五种组合未知未知（Beta分布干扰、随机负载、人类踢击、DoS、侧推）。
  2. **NVIDIA Isaac Gym 四足机器人（Unitree Go2）野外环境**：构建包含不平整地形、移动石块、树木、大岩石、突然冰面（低摩擦）的动态恶劣环境，模拟真实非平稳状况。机器人需通过导航模块自主穿越并到达目标点。
  3. **Cart-Pole 系统**（OpenAI Gym）：用于消融研究，引入未知未知（Beta分布干扰摩擦力和学生动作），系统状态包括角度、位置、速度。
- **Benchmark 与对比方法**：
  - 对于真实四足机器人：对比 **Phy-DRL**（带有域随机化和延迟随机化）、**Continual Phy-DRL**（持续学习）、以及我们的 Real-DRL。
  - 对于 Isaac Gym 野外环境：对比 **CLF-DRL**（安全奖励）、**Phy-DRL**（安全奖励+残差策略）、**Neural Simplex**（容错）、**Runtime Assurance**（运行时保证）、以及仅 **PHY-Teacher**。
  - 对于 Cart-Pole：进行**消融实验**，对比有/无安全知情批量采样、有/无教学机制（teaching-to-learn）、以及自动层次学习（禁用教师观察学生独立行为）。

## 4. 资源与算力

- 论文中明确给出了硬件配置：
  - 真实四足机器人实验：台式机 Ubuntu 22.04，12th Gen Intel Core i9-12900K 16核 CPU，64 GB RAM，NVIDIA GeForce GTX 3090 GPU。
  - Isaac Gym 野外环境实验：台式机 Ubuntu 22.04，13th Gen Intel Core i9-13900K 16核 CPU，64 GB RAM，NVIDIA GeForce GTX 4090 GPU。
  - Cart-Pole 实验：同上第一台配置（i9-12900K，GTX 3090）。
- 训练时间：未明确给出总训练时长，但提及真实机器人每 episode 15 秒； Cart-Pole 每 episode 1000 步（50 Hz 即20秒）； Isaac Gym 训练了 4500 个 episodes。
- 教师策略 LMI 求解时间：使用 Python CVXPY 约 49.15 ms（台式机）至 509.41 ms（树莓派4），使用 C ECVXCONE 可降低至 13.81 ms 至 149.87 ms，适合边缘设备。

## 5. 实验数量与充分性

- **实验数量**：
  - 真实四足机器人：对比实验（图3，阶段图）+ 视频演示（5种未知未知组合）+ 验证教学效果的视频。
  - Isaac Gym 野外环境：5种基准方法对比，每个模型测试 4500 个 episodes，统计成功率、碰撞数、旅行时间、平均功率、总能量（表1）。同时提供 episode return 曲线（图4）和对比视频。
  - Cart-Pole 消融研究：
    - 安全批量采样消融：5次随机初始状态实验，比较有/无 SBS 的阶段图和奖励（图5、图11）。
    - 教学机制消融：100个 episodes 的平均奖励（95% CI）（图6a）。
    - 自动层次学习：100个 episodes 的教师激活率（图6b）以及 episode 5 vs 50 的阶段图（图12）。
  - 此外，附录中包含 LMIs 求解性能对比（4个平台），以及模型失配补偿机制实验（视频）。
- **充分性与公平性**：
  - 场景覆盖真实机器人、高保真仿真（Isaac Gym）、经典控制（Cart-Pole），具有多样性。
  - 对比方法包括当前最先进的安全DRL（Phy-DRL、CLF-DRL）和容错DRL（Neural Simplex、Runtime Assurance），并且在与Phy-DRL比较时确保了相同的超参数和网络结构，仅改变框架组件。
  - 消融研究逐一验证三个创新点的贡献，并设置公平基准（如双缓冲区 vs 单缓冲区容量相同）。
  - 学习曲线（episode return）显示重复性（图4、图6a带置信区间）。
  - 客观性：对比结果中，Phy-DRL等对比方法在真实机器人上无法保证安全（图3），而Real-DRL始终安全；野外环境中只有Real-DRL和纯教师成功完成任务且无跌倒（表1），对比方法均失败或跌倒。

## 6. 论文的主要结论与发现

- Real-DRL 能在面对未知未知和 Sim2Real 差距时**保证实际系统运行安全**，同时通过学习获得高性能策略。
- 教师（PHY-Teacher）的**实时补丁**设计使得即使在动态恶劣环境（低摩擦、石块、未建模干扰）中也能提供可验证的安全备份，并有效教导学生学会安全。
- **安全知情批量采样**显著改善因边缘案例造成的经验不平衡，提升学生策略的鲁棒性（在仅含10%边缘案例的环境中，带SBS的策略表现更稳定、奖励更高）。
- **教学机制**大幅提升样本效率，加速收敛，并获得更高奖励（图6a）。
- **自动层次学习**：学生最初依赖教师保证安全，随着学习推进逐渐独立，教师激活率降至接近0（图6b），学生策略趋向于目标（聚类更紧密，图12）。
- 综合实验表明 Real-DRL 在安全性和性能之间取得了良好平衡，优于现有安全DRL和容错DRL方法。

## 7. 优点：方法或实验设计上的亮点

1. **理论上的可证明安全性**：教师策略通过 LMI 实时求解，在模型失配有界假设下保证状态始终在安全集内且返回自学习空间（定理5.2），实现了可验证的安全保证。
2. **框架集成度高**：将安全监控、教师备份、学生在线学习、经验平衡采样有机融合，形成完整的运行时学习系统。
3. **实用性强**：教师 LMI 求解可嵌入 C（ECVXCONE），资源占用低（树莓派4上149ms），适合边缘计算。
4. **实验验证充分**：包含真实机器人（多种真实未知干扰）+ 高保真仿真（复杂动态环境）+ 经典控制消融，视频辅助证明，结果可信。
5. **消融设计清晰**：分别隔离三个创新点（教学机制、安全采样、层次学习）进行对比，逻辑严谨。
6. **公平比较**：与最先进方法比较时，保持网络结构、超参数、任务定义一致，并考虑了持续学习版本。

## 8. 不足与局限

1. **假设条件**：教师的安全保证依赖于 Assumption 5.1（模型失配有界），虽然在附录F中设计了补偿机制，但理论上仍不能覆盖所有极端未知情况（如无穷大干扰）。
2. **实验覆盖**：
   - 真实机器人实验仅在一台 Unitree A1 室内环境进行，未测试不同机器人平台或多机器人系统。
   - 野外环境实验使用 Isaac Gym 模拟，虽接近真实但毕竟非真实物理系统，Sim2Real 差距可能仍存在。
   - 仅测试了导航与运动控制任务，未涉及更高层决策（如多智能体协调）、人机交互等场景。
3. **计算开销**：实时 LMI 求解虽然已有加速，但在极端低功耗设备（如早期树莓派）上仍可能影响控制实时性（149 ms）。对于千赫兹级别控制频率的系统可能不够。
4. **调参需求**：安全知情采样参数 \( \rho_1, \rho_2 \) 需要手动调整，缺乏自适应机制。
5. **混合系统复杂性**：触发器条件（6）基于边界离开，可能存在噪声敏感或边界扰动导致的频繁切换问题，论文未详细分析。
6. **对比方法选择**：未对比最新世界模型方法或基于屏障函数的在线学习（如RL-CBF），部分对比方法（如Neural Simplex）可能未针对动态环境优化。
7. **开放性问题**：论文未讨论当教师本身知识（线性化模型）在强非线性或大扰动下失效时的边界情况，尽管补偿机制存在，但缺乏理论保证。

（完）
