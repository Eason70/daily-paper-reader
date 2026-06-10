---
title: HMARL-CBF – Hierarchical Multi-Agent Reinforcement Learning with Control Barrier Functions for Safety-Critical Autonomous Systems
title_zh: HMARL-CBF：基于控制屏障函数的分层多智能体强化学习用于安全关键自主系统
authors: "H M Sabbir Ahmad, Ehsan Sabouni, Alexander Wasilkoff, Param Budhraja, Zijian Guo, Songyuan Zhang, Chuchu Fan, Christos Cassandras, Wenchao Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=fcLVqvyiqV"
tags: ["query:safe-rl-cbf"]
score: 9.0
evidence: HMARL-CBF：分层多智能体强化学习结合控制屏障函数用于安全关键自主系统
tldr: 该论文针对多智能体安全关键自主系统，提出分层多智能体强化学习与控制屏障函数相结合的框架（HMARL-CBF）。高层学习联合协作行为，低层基于CBF确保每个智能体个体安全，实现任务完成与安全约束的平衡。在多机器人仿真环境中验证了方法在安全性和任务效率上的优势。该工作直接契合安全强化学习结合CBF的主题，为无人系统安全控制提供了可迁移方法。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-fclvqvyiqv/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1443, \"height\": 864, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fclvqvyiqv/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1017, \"height\": 710, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fclvqvyiqv/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1445, \"height\": 273, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fclvqvyiqv/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1447, \"height\": 274, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fclvqvyiqv/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1446, \"height\": 273, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fclvqvyiqv/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1126, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fclvqvyiqv/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1157, \"height\": 344, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fclvqvyiqv/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 541, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fclvqvyiqv/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 987, \"height\": 425, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fclvqvyiqv/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 911, \"height\": 640, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fclvqvyiqv/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1288, \"height\": 266, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-fclvqvyiqv/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1446, \"height\": 487, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fclvqvyiqv/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1451, \"height\": 544, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fclvqvyiqv/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1455, \"height\": 456, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fclvqvyiqv/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1383, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fclvqvyiqv/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1454, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fclvqvyiqv/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 825, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fclvqvyiqv/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1452, \"height\": 199, \"label\": \"Table\"}]"
motivation: 多智能体自主系统需同时保证各智能体安全与协同任务完成，现有方法难以兼顾。
method: 提出分层框架，高层使用多智能体RL学习协作策略，低层基于CBF进行安全滤波，确保个体行为始终满足安全约束。
result: 在多智能体安全关键场景中，HMARL-CBF实现了零安全违规，同时保持了高水平任务回报。
conclusion: 分层集成CBF与MARL有效解决了多智能体安全控制难题，可推广至无人艇、无人机等系统。
---

## Abstract
We address the problem of safe policy learning in multi-agent safety-critical autonomous systems.
In such systems, it is necessary for each agent to meet the safety requirements at all times while also cooperating with other agents to accomplish the task. Toward this end, we propose a safe Hierarchical Multi-Agent Reinforcement Learning (HMARL) approach based on Control Barrier Functions (CBFs). Our proposed hierarchical approach decomposes the overall reinforcement learning problem into two levels –- learning joint cooperative behavior at the higher level and learning safe individual behavior at the lower or agent
level conditioned on the high-level policy. Specifically, we propose a skill-based HMARL-CBF algorithm in which the higher-level problem involves learning a joint policy over the skills for all the agents and the lower-level problem involves
learning policies to execute the skills safely with CBFs. We validate our approach on challenging environment scenarios whereby a large number of agents have to safely navigate through conflicting road networks. Compared with existing state-of-the-art methods, our approach significantly improves the safety achieving near perfect (within $5\%$) success/safety rate while also improving performance across all the environments.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）
多智能体安全关键自主系统（如自动驾驶车队、无人机编队）要求**每个智能体在任意时刻满足安全性约束**，同时相互协作完成任务。现有方法主要存在以下不足：
- 约束马尔可夫决策过程（CMDP）只能保证**轨迹期望上的安全**，而非**逐点时间硬约束**，不适用于安全关键场景；
- 平坦策略在智能体数量增多时面临**可扩展性差**和**样本复杂度高**的问题；
- 部分可观测环境中分散执行困难，且约束数量随智能体线性增长。

为解决这些问题，本文提出**分层多智能体强化学习结合控制屏障函数（HMARL-CBF）**，在确保点态安全的前提下实现高效协作。

## 2. 论文提出的方法论
### 核心思想
- **分层架构**：将问题分解为两层：
  - **高层**（策略 $\pi_H$）：学习所有智能体在技能（skill）上的联合协作策略，采用**集中式训练-分散式执行（CTDE）**范式（如MAPPO或QMIX）。
  - **低层**（策略 $\pi_z$）：对于每个技能，学习一个基于CBF的安全执行策略，确保智能体**逐点满足安全约束**。
- **技能定义**：每个技能为一个七元组，包含起始集、终止集、最大执行时间、安全约束集合、奖励函数及安全策略。技能可解释（如定速巡航、加速、减速、左换道、右换道）。
- **CBF安全保证**：低层策略通过求解**二次规划（QP）**获得确定性动作，其中CBF约束确保前向不变性（Forward Invariance），CLF约束辅助技能终止。
- **参数化QP**：CBF/CLF约束中的参数由神经网络学习（利用重参数化技巧），允许使用策略梯度更新。

### 关键技术细节
- 问题形式化为**带点态硬约束的随机最优控制问题**，区别于CMDP的期望约束。
- 高层使用**半马尔可夫决策过程（SMDP）**建模，技能执行时长可变。
- 低层QP的目标函数为二次型，约束包括CBF约束（相对度大于1时使用高阶CBF）和CLF松弛约束。
- 联合训练：高层和低层策略交替更新，共享网络参数。

### 算法流程（Algorithm 1）
1. 初始化高层策略参数 $\theta$ 和低层策略参数 $\nu$；
2. 每轮episode开始，采样初始技能；
3. 每个时间步：
   - 低层QP根据当前技能生成原始动作；
   - 环境反馈外部奖励和内在奖励；
   - 根据终止方案更新技能；
4. 更新高层策略（PPO/Q-learning）；
5. 更新低层QP参数（利用梯度计算）。

## 3. 实验设计
### 仿真环境
- **METADRIVE模拟器**（5个场景）：Merging, Intersection, Roundabout, Bottleneck, Tollgate。每个场景中多辆自动驾驶车辆需从起点安全到达终点，存在冲突区域。
- **Lidar-based环境套件**（3个场景）：Target（双积分器动力学）、Spread（覆盖任务）、Target-Bicycle（自行车模型动力学）。

### 对比基准方法
- **METADRIVE**：CoPo, IPPO, MFPO, MAPPO-Lagrangian, MACPO, Curriculum Learning (CL)。
- **Lidar套件**：DGPPO, InforMARL, MAPPO-Lagrangian。

### 评估指标
- **主要指标**：Success rate（成功率）；
- **辅助指标**：Success-weighted average time, Success-weighted average energy。

### 训练设置
- 智能体数量：Merging 15辆，Intersection/Roundabout 30辆，Bottleneck 25辆，Tollgate 40辆。
- 本文方法训练**300k iterations**，基线方法训练**1M iterations**。

## 4. 资源与算力
- **硬件**：单张NVIDIA RTX A5000 GPU，32 CPU cores。
- **训练时长**：由于分层分解加速收敛，本文方法在300k次迭代内达到稳定；基线方法需1M迭代（且需要2000+小时个体驾驶经验预训练）。
- **备注**：论文未给出具体训练小时数，但指出主要计算开销来自数据采集，训练和收敛高效。

## 5. 实验数量与充分性
### 实验组数
- **主实验**：5个METADRIVE环境×5个随机种子×5个评估episode = 25次运行，报告均值和标准差。
- **消融实验**（Table 2）：6种消融设置，涵盖：
  - 去掉分层（平坦策略）；
  - 随机高层策略；
  - CBF约束随机丢弃；
  - 替换低层为LQR（无CBF）；
  - 固定低层参数。
- **泛化实验**：车道宽度变化（3种）、技能迁移（跨环境）、交通密度变化（3种密度）。
- **Lidar套件**：3个环境×不同基线对比，含可扩展性测试（智能体数量变化）。

### 充分性与公平性
- 基线方法使用**最优超参数**并运行更长时间（1M vs 300k），且对比了不同惩罚因子（Table 3），结果仍然显著弱于本文方法。
- 消融实验揭露了各组件（分层、CBF、技能学习）的必要性。
- 泛化实验验证了方法对**环境变化**的鲁棒性。
- 总体而言，实验设计**客观、公平、充分**，覆盖了多种场景和变体。

## 6. 论文的主要结论与发现
- HMARL-CBF在所有环境中实现了**接近100%的成功率**，而基线方法成功率普遍低于50%（部分为0%）。
- 在**时间效率和能量消耗**方面同样优于或持平于基线方法（成功加权后）。
- 分层结构显著**加速收敛**（300k内达到最优），且低层CBF保证了**点态安全**。
- 技能具有可解释性，高层可学习合理的协作模式（如让行、加速、换道）。
- 泛化实验表明方法对车道宽度、交通密度、技能迁移均具有**良好鲁棒性**。

## 7. 优点
- **严格的安全保证**：CBF提供理论上的前向不变性，确保任意时刻约束满足。
- **分层降 complexity**：将协作学习与个体安全解耦，降低样本复杂度，适合大规模系统。
- **CTDE框架**：训练集中、执行分散，适用于部分可观测场景。
- **技能可解释**：技能具有语义（如“加速”、“让行”），便于理解和调试。
- **参数化QP可微**：允许端到端梯度更新，无缝集成RL。
- **实验充分**：在多种动力学、多种环境、多种基线下验证，结果稳定。

## 8. 不足与局限
- **模型依赖**：CBF构建需要近似动力学模型（论文使用了运动学单车模型），在真实系统中模型误差可能影响安全保证（论文提及可用鲁棒CBF缓解，但未深入验证）。
- **技能预定义**：技能集合需人工设计，限制了自动发现复杂行为的能力（未来工作可联合学习技能）。
- **超参数敏感**：QP中各权重（CBF/CLF参数）需学习，但上限需人为设置，可能影响性能。
- **扩展性挑战**：虽提及分组策略可用于更大规模智能体，但实验最大为45辆车，未验证数百辆以上场景。
- **未在真实系统验证**：所有实验在仿真器（METADRIVE、Lidar仿真）中进行，真实世界的传感器噪声、执行器延迟等未被考虑。
- **假设约束初始满足**：CBF需要初始状态在安全集内，实际部署中需保证初始化安全。

（完）
