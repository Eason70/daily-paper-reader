---
title: Boundary-to-Region Supervision for Offline Safe Reinforcement Learning
title_zh: 面向离线安全强化学习的边界到区域监督
authors: "Huikang Su, Dengyun Peng, Zifeng Zhuang, YuHan Liu, Qiguang Chen, Donglin Wang, Qinghe Liu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=vFLrQgI6MW"
tags: ["query:safe-rl-cbf"]
score: 4.0
evidence: 离线安全强化学习，非对称成本条件
tldr: 该论文针对离线安全强化学习中的成本-回报不对称问题，提出边界到区域（B2R）框架，将成本目标重新定义为固定安全预算下的边界约束。方法在成本信号对齐后将条件生成变为非对称，提升了约束满足的可靠性。实验表明B2R在离线安全RL基准上显著降低了违规。该工作聚焦安全RL方法创新，但未包含控制屏障函数。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-vflrqgi6mw/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1444, \"height\": 615, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-vflrqgi6mw/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 651, \"height\": 374, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-vflrqgi6mw/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 709, \"height\": 316, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-vflrqgi6mw/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 652, \"height\": 305, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-vflrqgi6mw/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1424, \"height\": 842, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-vflrqgi6mw/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 715, \"height\": 400, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-vflrqgi6mw/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 704, \"height\": 345, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-vflrqgi6mw/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1360, \"height\": 845, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-vflrqgi6mw/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1449, \"height\": 1034, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-vflrqgi6mw/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1442, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-vflrqgi6mw/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1249, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-vflrqgi6mw/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 928, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-vflrqgi6mw/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 808, \"height\": 547, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-vflrqgi6mw/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 667, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-vflrqgi6mw/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1299, \"height\": 674, \"label\": \"Table\"}]"
motivation: 现有序列模型对回报-成本使用对称条件，忽视各自角色差异，导致分布外成本轨迹下约束满足不可靠。
method: 提出B2R框架，通过成本信号重对齐将成本目标设为边界约束，并设计非对称条件生成机制。
result: 在多个离线安全RL数据集上，B2R相比基线实现了更低的违规率和更高的任务成功率。
conclusion: 该工作揭示了成本-回报对称条件的缺陷，提供了更鲁棒的离线安全学习范式，但未涉及CBF。
---

## Abstract
Offline safe reinforcement learning aims to learn policies that satisfy predefined safety constraints from static datasets. Existing sequence-model-based methods condition action generation on symmetric input tokens for return-to-go and cost-to-go, neglecting their intrinsic asymmetry: RTG serves as a flexible performance target, while CTG should represent a rigid safety boundary. This symmetric conditioning leads to unreliable constraint satisfaction, especially when encountering out-of-distribution cost trajectories. To address this, we propose Boundary-to-Region (B2R), a framework that enables asymmetric conditioning through cost signal realignment . B2R redefines CTG as a boundary constraint under a fixed safety budget, unifying the cost distribution of all feasible trajectories while preserving reward structures. Combined with rotary positional embeddings , it enhances exploration within the safe region. Experimental results show that B2R satisfies safety constraints in 35 out of 38 safety-critical tasks while achieving superior reward performance over baseline methods. This work highlights the limitations of symmetric token conditioning and establishes a new theoretical and practical approach for applying sequence models to safe RL.

---

## 论文详细总结（自动生成）

# 论文总结：Boundary-to-Region Supervision for Offline Safe Reinforcement Learning

## 1. 核心问题与整体含义（研究动机和背景）

离线安全强化学习旨在从静态数据集中学习满足预定安全约束的策略。现有基于序列模型（如Constrained Decision Transformer, CDT）的方法将回报-预估值（RTG）和成本-预估值（CTG）作为对称的输入令牌来条件化动作生成，忽视了它们固有的不对称性：RTG是灵活的性能目标，而CTG应代表刚性的安全边界。这种对称条件导致约束满足不可靠，尤其当遇到分布外的成本轨迹时。本文提出了一种非对称条件框架B2R，通过成本信号重对齐来解决该问题，实现更可靠的安全合规策略学习。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：将原本稀疏的“边界监督”（仅使用成本接近阈值的轨迹）转化为稠密的“区域监督”（利用所有安全轨迹），通过重新对齐CTG来统一所有可行轨迹的成本分布，同时保留奖励结构。这使模型能够从更丰富、更多样的安全行为中学习，从而提升约束满足的鲁棒性。

- **关键技术细节**：
  - **轨迹过滤（Trajectory Filtering）**：从数据集中筛选出总成本不超过阈值κ的轨迹，构成安全数据集Dsafe。
  - **CTG重对齐（CTG Realignment）**：对每条安全轨迹中的每个时间步的CTG进行偏移：`Ĉ'_t = Ĉ_t + (κ - C(τ))`，使得初始CTG`Ĉ'_0 = κ`，且保持原有成本下降的时序轮廓。这样所有训练轨迹都使用相同的初始成本令牌，但背后的行为可以来自整个安全区域。
  - **旋转位置编码（RoPE）**：替代标准的绝对位置编码，更好地捕捉相对时序依赖关系，以适应CT重对齐后精细的逐时间步成本动态。
  - **模型训练与推理**：基于Transformer的架构，通过行为克隆（负对数似然）最小化动作预测误差。推理时用固定的初始RTG和CTG（Ĉ₀=κ）作为条件。

- **理论分析**（Theorem 1 & 2）：
  - 在假设安全对齐数据和有界预测误差下，B2R能提供高概率和期望成本的安全保证。
  - B2R的奖励性能不低于边界监督方法，因为其包含所有边界监督轨迹，并有机会利用更多高奖励可行轨迹。

## 3. 实验设计

- **数据集与场景**：使用DSRL基准，包含38个安全关键任务，涵盖三个环境组：
  - **SafetyGymnasium**（如PointButton, CarCircle, AntVelocity等）
  - **BulletSafetyGym**（如BallRun, CarRun, DroneCircle, AntCircle等）
  - **MetaDrive**（自动驾驶场景，分为easy/medium/hard稀疏/均值/密集等9种配置）
- **对比方法**：BC-All, BC-Safe, CDT, BCQ-Lag, CPQ, COptiDICE, TraC（以及附录中的FISOR, OASIS, LSPC, FAWAC）。
- **评估指标**：归一化奖励（越高越好）、归一化成本（低于1为安全），每个任务在3个成本阈值（L1-L3）和3个随机种子下评估。

## 4. 资源与算力

论文在附录C.6中说明：实验在一台Linux服务器上进行，配备Intel Core i9-14900K 32核CPU、一块NVIDIA GeForce RTX 4070 GPU、64GB RAM。每个任务训练约100K步（20个epoch，每epoch 5000步），平均训练时长约2小时。算力消耗适中，与CDT等Transformer方法相当。

## 5. 实验数量与充分性

- **主要实验**：38个任务的全表对比（表1），覆盖奖励与成本表现。
- **消融实验**：9个代表任务上对CTG重对齐、RoPE、轨迹过滤三个组件分别去除（图6），验证各自贡献。
- **扩展实验**：
  - CTG重对齐策略对比（Shift/Scale/Avg/Rand，9个任务，图8）
  - 与近期离线安全RL方法（FISOR, OASIS, LSPC, FAWAC）对比（表2，6个任务）
  - 缓冲阈值CDT对比（表3，4个任务）
  - 数据稀缺鲁棒性测试（5%/20%/50%/100%安全数据，表4，4个任务）
  - 多目标约束扩展验证（表5，3个任务）
  - 严格成本限制对比FISOR（表6，6个任务）
- **充分性评价**：实验设计比较充分。主要对比了7种主流基线，消融实验拆解关键组件，并在多种难度、多种成本阈值下进行。但部分扩展实验（如多目标、数据稀缺）仅在小范围任务上进行，统计显著性未提供误差条。总体而言，实验覆盖了主流场景和挑战，结论可信。

## 6. 主要结论与发现

1. B2R在35/38个安全关键任务中满足安全约束，同时在20个任务中获得最高奖励，综合性能优于所有基线。
2. 对称令牌条件（如CDT）是离线安全RL的根本缺陷，B2R的非对称条件通过区域监督本质性地提高了约束满足可靠性。
3. CTG重对齐是性能提升的核心，轨迹过滤和RoPE均对安全性和稳定性有显著贡献。
4. B2R在数据稀缺或严格成本限制下仍能保持较好的安全-奖励平衡，具有鲁棒性。

## 7. 优点

- **问题识别精准**：清晰指出现有序列模型对RTG和CTG对称处理的缺陷，并给出了形式化定义（边界监督 vs 区域监督）。
- **方法简洁有效**：通过简单的CTG偏移即可实现区域监督，无需复杂架构或额外训练目标，易于实现。
- **理论支撑**：提供了安全保证和性能下界的形式化证明（简化假设下），增强了方法可信度。
- **实验全面**：在38个任务、多个基线、多种消融、数据稀缺、多目标扩展等条件下进行了充分验证。
- **代码开源**：提供了可复现的GitHub仓库。

## 8. 不足与局限

- **依赖安全轨迹可用性**：当数据集中几乎无安全轨迹或安全轨迹极度稀缺时，B2R性能会下降（论文在附录中通过少样本实验验证了优雅退化，但仍是一个局限）。
- **仅考虑单一固定阈值**：虽然附录展示了多目标扩展的可行性，但主要实验均基于单一κ值。多目标训练时的性能权衡未深入分析。
- **理论假设较强**：安全保证需要假设预测误差有界、训练数据完全安全对齐，现实环境中这些假设可能被违背。
- **未与CBF类方法对比**：论文聚焦序列模型方法，未涉及控制屏障函数（CBF）等基于模型的方法，应用范围受限。
- **部分实验统计不足**：消融和扩展实验仅报告均值，未给出方差或统计显著性检验，难以判断差异是否显著。
- **计算资源描述较简略**：仅提及单GPU和约2小时训练，未提供完整训练的总GPU小时数或对比其他方法的计算成本。

（完）
