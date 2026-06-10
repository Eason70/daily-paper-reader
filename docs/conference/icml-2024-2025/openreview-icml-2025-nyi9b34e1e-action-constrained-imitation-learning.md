---
title: Action-Constrained Imitation Learning
title_zh: 动作约束模仿学习
authors: "Chia-Han Yeh, Tse-Sheng Nan, Risto Vuorio, Wei Hung, Hung Yen Wu, Shao-Hua Sun, Ping-Chun Hsieh"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=NYi9B34E1e"
tags: ["query:safe-rl-cbf"]
score: 4.0
evidence: 动作约束模仿学习用于安全行为
tldr: 本文提出动作约束模仿学习新问题，解决模仿者动作空间小于专家时的不匹配问题，通过DTWIL轨迹对齐方法生成替代数据集，在机器人控制等安全关键场景中实现安全策略学习，验证了有效性。但未涉及RL或CBF。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-nyi9b34e1e/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1679, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nyi9b34e1e/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 855, \"height\": 586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nyi9b34e1e/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 792, \"height\": 401, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nyi9b34e1e/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 853, \"height\": 224, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nyi9b34e1e/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 840, \"height\": 462, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nyi9b34e1e/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1671, \"height\": 985, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nyi9b34e1e/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1028, \"height\": 534, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-nyi9b34e1e/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 716, \"height\": 542, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nyi9b34e1e/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1727, \"height\": 698, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nyi9b34e1e/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 651, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nyi9b34e1e/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 668, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nyi9b34e1e/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1304, \"height\": 167, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nyi9b34e1e/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 821, \"height\": 330, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nyi9b34e1e/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 675, \"height\": 237, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nyi9b34e1e/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 652, \"height\": 169, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nyi9b34e1e/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1418, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nyi9b34e1e/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 901, \"height\": 206, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nyi9b34e1e/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1345, \"height\": 329, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nyi9b34e1e/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 726, \"height\": 204, \"label\": \"Table\"}]"
motivation: 现实系统中智能体常受动作约束，从专家演示中学习安全策略存在动作不匹配。
method: 提出DTWIL，通过动态时间规整对齐轨迹，生成符合约束的替代演示。
result: 在多个控制任务上有效模仿专家同时满足动作约束。
conclusion: 轨迹对齐可有效解决动作约束下的模仿学习问题。
---

## Abstract
Policy learning under action constraints plays a central role in ensuring safe behaviors in various robot control and resource allocation applications.
In this paper, we study a new problem setting termed Action-Constrained Imitation Learning (ACIL), where an action-constrained imitator aims to learn from a demonstrative expert with larger action space.
The fundamental challenge of ACIL lies in the unavoidable mismatch of occupancy measure between the expert and the imitator caused by the action constraints. We tackle this mismatch through trajectory alignment and propose DTWIL, which replaces the original expert demonstrations with a surrogate dataset that follows similar state trajectories while adhering to the action constraints. Specifically, we recast trajectory alignment as a planning problem and solve it via Model Predictive Control, which aligns the surrogate trajectories with the expert trajectories based on the Dynamic Time Warping (DTW) distance. Through extensive experiments, we demonstrate that learning from the dataset generated by DTWIL significantly enhances performance across multiple robot control tasks and outperforms various benchmark imitation learning algorithms in terms of sample efficiency.

---

## 论文详细总结（自动生成）

## 论文总结：Action-Constrained Imitation Learning

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：在机器人控制、资源分配等安全关键应用中，智能体常受动作约束（如功率限制、运动学限制）。现有模仿学习（IL）通常假设专家和模仿者动作空间一致，但现实中模仿者的动作能力可能弱于专家（例如低扭矩机械臂模仿高扭矩机械臂）。这导致**占用度量不匹配（occupancy measure distortion）**，即专家动作超出模仿者可行集时，直接投影会引发轨迹偏差。
- **整体含义**：论文正式定义了 **动作约束模仿学习（Action-Constrained Imitation Learning, ACIL）** 问题，并指出传统IL方法（如行为克隆、对抗模仿）和动作约束RL方法均无法有效解决该问题，需要专门的轨迹对齐策略。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：将ACIL分解为两个阶段：  
  **阶段1**：利用专家演示，通过**轨迹对齐**生成一组**替代（surrogate）演示**，满足模仿者的动作约束且状态序列与专家相似。  
  **阶段2**：在替代演示上使用任何现成IL方法（如BC）训练策略。
- **关键技术细节**：
  - **轨迹对齐作为规划问题**：对每个专家轨迹，通过**模型预测控制（MPC）** 顺序地选择可行动作，使得替代轨迹的状态序列与专家轨迹的**动态时间规整（DTW）距离**最小化。MPC使用前向动力学模型（概率集成网络）和交叉熵方法（CEM）优化。
  - **DTW距离**：用于度量不同长度状态序列的相似性，通过动态规划递归计算，支持时间扭曲对齐。
  - **进度管理（Progression Management）**：根据DTW规整路径更新当前对齐到的专家时间步，允许模仿者以更慢的节奏跟随专家。
  - **专家正则化控制（Expert Regularized Control, ERC）**：在MPC采样初期混合专家动作，防止早期偏差导致任务失败（如Hopper摔倒）。
  - **算法流程**：  
    Algorithm 1（DTWIL主循环）：对每个专家轨迹，用Algorithm 2（Trajectory Alignment）生成替代轨迹，并更新替代数据集。  
    Algorithm 2：初始化agent状态为专家起始状态，循环：用CEM采样可行动作序列（经ERC和DTW评估），取第一个动作执行，更新进度，直到终止。

### 3. 实验设计：使用了哪些数据集/场景，它的 benchmark 是什么，对比了哪些方法
- **环境与任务**：四个连续控制任务：
  - **Maze2d-Medium-v1**（导航）
  - **HalfCheetah-v3**（奔跑）
  - **Hopper-v2**（跳跃）
  - **Table-Wiping**（Robosuite，机器人擦桌子）
- **约束类型**：包括**盒约束（+B）**、**状态依赖功率约束（+M, +O）**、**L2约束（+L2）**。共7个设置（M+B, M+O, HC+B, HC+O, H+B, H+M, W+B, W+L）。
- **对比方法**：
  - 模仿学习：BC（行为克隆，基线）、GAIL、GAIfO、OPOLO、CFIL-s/CFIL-sa、SAIL、DIFO。
  - 学习从观测（LfO）：BCO、GAIfO、OPOLO、DIFO等。
  - 所有基线在输出层添加投影层以满足动作约束。
- **benchmark**：各方法的返回（return）和DTW距离，重点关注**样本效率**（仅允许50K环境步训练在线方法）。

### 4. 资源与算力
- 论文未明确说明使用的GPU型号、数量及具体训练时长。仅在致谢中感谢国家高速网络与计算中心（NCHC）提供计算和存储资源，并提及使用了计算资源。没有给出硬件规格或运行时间。

### 5. 实验数量与充分性
- **实验数量**：在8个约束任务上进行主实验，每种设置3个随机种子，报告均值和标准差。此外开展了多项消融研究：
  - DTW vs ℓ2距离（表3）
  - DTWIL与BC对比（表4）
  - 将CFIL应用于替代数据（图5）
  - 输入归一化（表5）
  - 最终专家状态排除（表6）
  - 进度管理（异步 vs 同步，表7）
  - ERC消融（表8）
  - 超参数β和herc（表9）
  - MPC执行步数（表10）
  - 约束松紧度（表11）
  - 专家演示数量（表12）
- **充分性与公平性**：
  - 主实验限制所有方法环境步数相同（50K），聚焦样本效率，合理。
  - 附录A.3展示了基线方法延长至500K步的训练曲线，证明其需要更多数据，但DTWIL仍更高效。
  - 消融实验覆盖了关键设计选择，验证了方法的鲁棒性。
  - 所有方法均使用动作投影保证公平比较，实验整体客观公平。

### 6. 论文的主要结论与发现
- DTWIL在所有8个约束任务上均显著优于现有IL和LfO基线，尤其在样本效率方面（50K环境步内达到接近专家性能）。
- 基于DTW的距离优于ℓ2距离（表3），表明时间扭曲能力对动作约束下的对齐至关重要。
- 替代演示可泛化到其他IL方法（如CFIL），显示DTWIL作为数据增强模块的通用性。
- 专家正则化控制（ERC）对需要精确控制的任务（如Hopper）至关重要，可防止跌倒。
- 进度管理采用异步更新（而非同步）在复杂任务中更有效。
- 方法对约束紧密度和专家演示数量具有鲁棒性（表11、12）。

### 7. 优点：方法或实验设计上的亮点
- **问题新颖性**：首次定义ACIL并揭露占用度量失真问题。
- **方法巧妙**：将动作约束下的模仿分解为轨迹对齐+标准IL，解耦约束满足与策略学习，通用性强。
- **技术合理性**：DTW距离天然适合不等长序列对齐，MPC顺序规划可适应动态变化。
- **实验全面**：大量消融和超参数分析，验证了每个设计组件的必要性；对比基线覆盖主流IL类别，比较公平。
- **显著提升**：在样本效率上远超投影式方法，且能保持相近或更好性能。

### 8. 不足与局限
- **计算开销**：MPC+DTW+集成动力学模型在每步规划时需多次前向传播，计算成本高于简单投影方法。论文未量化运行时间或计算资源消耗。
- **依赖动力学模型**：性能受动力学模型精度影响，模型偏差可能导致次优对齐。虽然用在线数据更新，但初始模型可能仍不够准确。
- **场景局限**：仅在连续控制任务上验证，未涉及离散动作空间或高维视觉输入；任务中专家和模仿者动作空间维度相同（仅范围不同），未考虑维度变化。
- **基线对比局限性**：所有基线在50K步内可能未收敛，但其延长训练后的表现（附录A.3）仍不如DTWIL，但DTWIL本质上是离线利用MPC生成数据+BC，与在线方法比较样本效率时需注意差异。
- **理论分析缺乏**：未给出收敛性或性能边界证明，主要为实验性工作。
- **实际部署限制**：MPC需要可微分的动力学模型，对于复杂真实机器人系统可能难以获得或训练。

（完）
