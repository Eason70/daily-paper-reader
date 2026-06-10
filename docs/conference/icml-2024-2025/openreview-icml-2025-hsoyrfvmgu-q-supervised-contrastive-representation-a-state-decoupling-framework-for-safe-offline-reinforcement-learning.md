---
title: "Q-Supervised Contrastive Representation: A State Decoupling Framework for Safe Offline Reinforcement Learning"
title_zh: Q监督对比表示：安全离线强化学习的状态解耦框架
authors: "Zhihe Yang, Yunjian Xu, Yang Zhang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=hsoyRfvMGu"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 安全离线强化学习，通过状态解耦分离奖励与成本表示
tldr: 本文针对安全离线强化学习中测试阶段因状态组合爆炸导致的分布外不安全问题，提出Q监督对比表示的状态解耦框架SDQC，将全局观测解耦为奖励相关和成本相关表示，从而提升泛化能力与安全性。实验证明该方法在多个安全离线RL基准上优于现有方法，为安全关键应用提供了可靠策略学习方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 718, \"height\": 530, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1638, \"height\": 673, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1601, \"height\": 746, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1603, \"height\": 733, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 899, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1601, \"height\": 490, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1218, \"height\": 635, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1771, \"height\": 856, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1599, \"height\": 792, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1608, \"height\": 1269, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1516, \"height\": 1196, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1520, \"height\": 1195, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1515, \"height\": 828, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hsoyrfvmgu/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1518, \"height\": 1569, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-hsoyrfvmgu/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1685, \"height\": 908, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hsoyrfvmgu/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 403, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hsoyrfvmgu/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 578, \"height\": 333, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hsoyrfvmgu/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1213, \"height\": 896, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hsoyrfvmgu/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1304, \"height\": 506, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hsoyrfvmgu/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1066, \"height\": 372, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hsoyrfvmgu/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1405, \"height\": 291, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hsoyrfvmgu/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1581, \"height\": 293, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hsoyrfvmgu/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1079, \"height\": 112, \"label\": \"Table\"}]"
motivation: 现有安全离线RL方法因奖励与成本状态组合无限导致测试时分布外不安全。
method: 提出SDQC框架，利用Q监督对比学习解耦观测中的奖励和成本特征。
result: 在多个安全离线RL基准中取得了更低的成本违反和更高的奖励。
conclusion: 状态解耦有效缓解分布外问题，提升安全离线RL的泛化安全性。
---

## Abstract
Safe offline reinforcement learning (RL), which aims to learn the safety-guaranteed policy without risky online interaction with environments, has attracted growing recent attention for safety-critical scenarios. However, existing approaches encounter out-of-distribution problems during the testing phase, which can result in potentially unsafe outcomes. This issue arises due to the infinite possible combinations of reward-related and cost-related states. In this work, we propose State Decoupling with Q-supervised Contrastive representation (SDQC), a novel framework that decouples the global observations into reward- and cost-related representations for decision-making, thereby improving the generalization capability for unfamiliar global observations. Compared with the classical representation learning methods, which typically require model-based estimation (e.g., bisimulation), we theoretically prove that our Q-supervised method generates a coarser representation while preserving the optimal policy, resulting in improved generalization performance. Experiments on DSRL benchmark problems provide compelling evidence that SDQC surpasses other baseline algorithms, especially for its exceptional ability to achieve almost zero violations in more than half of the tasks, while the state-of-the-art algorithm can only achieve the same level of success in a quarter of the tasks. Further, we demonstrate that SDQC possesses superior generalization ability when confronted with unseen environments.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，以下是对论文《Q-Supervised Contrastive Representation: A State Decoupling Framework for Safe Offline Reinforcement Learning》的详细结构化、深入且客观的中文总结。

## 1. 核心问题与整体含义（研究动机和背景）

*   **核心问题**：安全离线强化学习旨在仅利用预先收集的静态数据集，学习安全策略，避免与环境的危险在线交互。然而，现有方法在测试阶段普遍面临**分布外 (Out-of-Distribution, OOD) 问题**。具体来说，奖励相关的状态和成本相关的状态存在无限种组合。当测试中遇到来自训练数据中未曾出现的状态组合时，智能体可能做出错误的、不安全的决策。
*   **整体含义**：本文旨在解决上述OOD问题，通过改进的安全离线强化学习框架，增强模型在面对陌生全局观测时的泛化能力和安全性，使学习到的策略在安全攸关场景（如自动驾驶、工业控制）中更可靠。

## 2. 论文提出的方法论

### 2.1 核心思想：状态解耦 (State Decoupling)

*   核心观点是，全局观测通常包含两类信息：`奖励相关信息`（如导航目标位置）和`成本相关信息`（如障碍物位置）。这些信息在观测中是混叠的。
*   本文提出**将全局观测解耦**为两个独立的表示：**奖励相关表示 (reward-related representation, `s_r`)** 和 **成本相关表示 (cost-related representation, `s_c`)**。
*   基于此表示，框架采用分而治之的决策方式：
    *   若安全评估确认绝对安全（`V_h ≤ 0`），使用仅依赖`奖励表示`的**奖励策略**，专注于最大化奖励。
    *   若安全评估判定为不安全（`V_h > 0 `），使用仅依赖`成本表示`的**成本策略**，专注于规避危险。
    *   若评估结果为边界安全 (borderline safe)，则使用同时依赖两种表示的**权衡策略**，平衡奖励与安全。

### 2.2 关键技术：Q监督对比表示学习 (Q-Supervised Contrastive Representation)

*   **动机**：手动分离奖励/成本信息通常不切实际。观察到最优Q函数（无论是奖励还是成本）只包含其训练目标（奖励或成本）的信息，与另一个因素无关。
*   **核心思想**：利用最优Q函数 `Q*` 作为监督信号，通过对比学习，将具有相似 `Q*` 值的状态在表示空间中聚拢。
*   **技术细节**：
    1.  **距离度量**：定义状态间距离 `d(s1, s2)` 为 `Q*` 差值在所有动作上的上确界。
    2.  **软相似度**：通过指数函数将距离转化为软相似度 `Γ(s, s_tilde)`。
    3.  **对比学习损失**：设计一个对比损失函数，鼓励具有相似 `Q*` 值的状态（通过状态间距离度量）具有相似的表示，而`Q*`值不相似的状态表示则被推远。
    4.  **联合训练**：表示网络与Q函数网络**联合训练**，确保二者能够相互适应，共同优化。表示学习的损失项被添加进价值函数的学习目标（如IQL的损失函数）中。例如，奖励表示的损失函数为 `L_reward = L_V_r + L_Q_r + δ * L_θ_r`，其中 `L_θ_r` 是对比损失。

### 2.3 算法流程

论文包含一个三阶段训练过程：
1.  **行为克隆器训练**：预训练一个扩散模型作为行为克隆器，用于为每个状态生成数据集内的支持动作 (in-support actions)，以解决OOD动作查询问题。
2.  **价值函数与表示联合优化**：分别对奖励和成本模块执行联合训练，学习最优Q函数、V函数以及对应的解耦表示。
3.  **策略提取**：使用加权回归的扩散模型，根据学习到的价值函数和表示，分别训练三个独立的策略：奖励策略 (`π_r`)、成本策略 (`π_h`) 和权衡策略 (`π_to`)。

## 3. 实验设计

*   **数据集/场景**：在**DSRL (Datasets and Benchmarks for Offline Safe Reinforcement Learning)** 基准上进行评估。该基准包含两大类环境：
    1.  **Safety-Gymnasium**：包含基于MuJoCo的Point、Car、Ant等智能体的避障和速度约束任务，共12个任务。
    2.  **Bullet-Safety-Gym**：包含基于PyBullet的Ball、Car、Drone、Ant等智能体的导航任务，共8个任务。
*   **对比方法**：与6种主流安全离线RL算法进行比较，包括：
    *   **BCQ-Lag**：基于PID-Lagrangian和批次约束Q学习的方法。
    *   **CPQ**：约束惩罚Q学习方法。
    *   **COptiDICE**：基于分布修正估计的Lagrangian方法。
    *   **CDT**：基于决策Transformer的未来成本推断方法。
    *   **TREBI**：基于扩散模型的实时成本预算推断方法。
    *   **FISOR**：本文的强基线，也是首个引入硬约束和HJ可达性分析的安全离线RL方法。

## 4. 资源与算力

*   **文中明确提及了**：实验在配备一块 **NVIDIA RTX 4090 (24GB)** 和一颗 **AMD Ryzen 9 7950X CPU** 的单机上进行。
*   **训练时间**：总训练过程包含三个阶段，耗时约 **6 小时**（行为克隆器1小时，表示和价值函数训练1-4小时，扩散策略约1小时）。
*   **推理时间**：在执行推理时，SDQC需要约 **11.13 秒/1000步**，高于BCQ等非自回归模型，但远低于TREBI，属于可接受范围。其中，采样16个候选动作并选择最安全的一个是其耗时略长的主要原因。

## 5. 实验数量与充分性

*   **实验数量**：实验较为丰富，主要包括：
    1.  **DSRL基准测试**：在全部21个任务（12安全健身房 + 8子弹安全健身房 + 1个平均结果）上进行了主实验。
    2.  **泛化测试**：在4个任务（CarGoal, CarPush, PointGoal, PointPush）上进行了源环境到目标场景的泛化迁移测试。
    3.  **消融实验**：对`Q监督对比损失`、`网络结构`、`锚点数量`等多个超参数进行了消融研究。
*   **充分性与公平性**：
    *   **充分性**：实验覆盖了从简单到复杂的多种任务，包含了标准测试和泛化测试，并进行了深入的消融实验，整体上验证了方法的有效性。
    *   **客观与公平**：
        *   基准算法结果主要引用自FISOR，但特别说明了部分需独立运行。实验均使用3个随机种子，结果取平均，一定程度上保证了统计稳定性。
        *   消融实验设计合理，清晰展示了各组件对性能的影响。
        *   存在的风险：部分超参数（如对比损失系数、锚点数）在不同任务和网络结构（ATN vs MLP）上需要调整，这引入了调参偏差和公平性问题，但论文也对此进行了说明和对比。与FISOR的对比图（附录F.3）也说明了其相对优劣。

## 6. 论文的主要结论与发现

1.  **显著提升了安全性**：SDQC在**超过一半的任务中实现了近乎零的违规 (zero violations)**，远优于FISOR等最先进方法，充分证明了其强大的安全保障能力。
2.  **卓越的泛化能力**：在面对未见过的、更复杂的环境时，SDQC是唯一能保证成本不增加（成本几乎为零），且奖励仅有轻微下降的算法。其他所有基线方法在成本上都有显著上升。
3.  **性能优越性**：在DSRL基准测试中，SDQC在获得更低成本的同时，在多个任务中保持了具有竞争力的奖励值。
4.  **理论优势**：从理论上证明了其提出的Q监督对比学习方法比传统的基于模型的双模拟（bisimulation）方法产生更粗糙的表示，但**仍然保留了最优策略**，从而带来更好的泛化性能。

## 7. 优点

*   **理论创新**：将Q函数作为监督信号进行对比学习，不需要额外估计系统模型，避免了双模拟等方法在奖励/成本稀疏时误差大的问题。并提供了理论支撑，论证了其表示更粗糙但能保持最优策略的优越性。
*   **方法创新**：首次将状态解耦应用于安全离线RL的决策过程，提出了一个“分而治之”的决策框架（奖励策略、成本策略、权衡策略），克服了传统方法依赖全局观测处理混叠信息的局限。
*   **实证优势**：在标准测试和泛化测试中均展示了压倒性的安全性能提升，特别是其近乎零违规的能力对于安全关键应用至关重要。

## 8. 不足与局限

*   **计算成本较高**：三阶段的训练流程，特别是扩散行为克隆器和注意力编码器的使用，导致训练和推理的时间成本高于一些简单基线（如BCQ-Lag, CPQ），部署时对算力有一定要求。
*   **框架复杂性**：模型结构相对复杂，需要同时维护奖励/成本两条线的价值网络、表示网络以及三个独立的扩散策略，增加了模型训练和调参的难度。
*   **超参数敏感性**：性能对部分超参数（如对比损失系数、锚点数量、状态编码器结构）的选择较为敏感，需要根据任务的特点进行调整，这降低了方法的普适性和便利性。
*   **应用限制**：虽然泛化能力强，但仍是在模拟器环境中验证的。其在实际物理系统（如真实机器人）中面对更大、更不可预测的分布偏移时的表现尚待验证。同时，对高维度、视觉输入的观测空间的处理能力也未作探讨，主要挑战停留在状态观测层面。

（完）
