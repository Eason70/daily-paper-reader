---
title: "OASIS: Conditional Distribution Shaping for Offline Safe Reinforcement Learning"
title_zh: OASIS：面向离线安全强化学习的条件分布塑造
authors: "Yihang Yao, Zhepeng Cen, Wenhao Ding, Haohong Lin, Shiqi Liu, Tingnan Zhang, Wenhao Yu, Ding Zhao"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=3uDEmsf3Jf"
tags: ["query:safe-rl-cbf"]
score: 5.0
evidence: 通过条件分布塑造实现离线安全强化学习
tldr: 针对离线安全强化学习中演示数据与期望性能不匹配的问题，提出数据驱动的OASIS方法，利用条件扩散模型对离线数据集进行重分布，引导数据朝向安全且高回报的目标域，结合正则化技术有效提升策略的安全性和性能。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-3udemsf3jf/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 605, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-3udemsf3jf/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 547, \"height\": 545, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-3udemsf3jf/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 642, \"height\": 676, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-3udemsf3jf/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1420, \"height\": 458, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-3udemsf3jf/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1430, \"height\": 506, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-3udemsf3jf/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 700, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-3udemsf3jf/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1412, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-3udemsf3jf/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1424, \"height\": 438, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-3udemsf3jf/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1454, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-3udemsf3jf/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1053, \"height\": 796, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-3udemsf3jf/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1412, \"height\": 399, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-3udemsf3jf/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1410, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-3udemsf3jf/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1174, \"height\": 374, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-3udemsf3jf/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1448, \"height\": 724, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-3udemsf3jf/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 724, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-3udemsf3jf/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 973, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-3udemsf3jf/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 577, \"height\": 298, \"label\": \"Table\"}]"
motivation: 离线安全强化学习面临次优演示数据与期望性能之间的不匹配。
method: 提出OASIS，利用条件扩散模型合成离线数据，重塑数据分布至目标域。
result: 在多个离线安全RL基准上提升了策略的安全性和回报。
conclusion: 为离线安全RL提供了一种数据驱动的有效范式。
---

## Abstract
Offline safe reinforcement learning (RL) aims to train a policy that satisfies con- straints using a pre-collected dataset. Most current methods struggle with the mismatch between imperfect demonstrations and the desired safe and rewarding performance. In this paper, we mitigate this issue from a data-centric perspective and introduce OASIS (cOnditionAl diStributIon Shaping), a new paradigm in offline safe RL designed to overcome these critical limitations. OASIS utilizes a conditional diffusion model to synthesize offline datasets, thus shaping the data dis- tribution toward a beneficial target domain. Our approach makes compliance with safety constraints through effective data utilization and regularization techniques to benefit offline safe RL training. Comprehensive evaluations on public benchmarks and varying datasets showcase OASIS’s superiority in benefiting offline safe RL agents to achieve high-reward behavior while satisfying the safety constraints, out- performing established baselines. Furthermore, OASIS exhibits high data efficiency and robustness, making it suitable for real-world applications, particularly in tasks where safety is imperative and high-quality demonstrations are scarce. More details are available at the website https://sites.google.com/view/saferl-oasis/home.

---

## 论文详细总结（自动生成）

# 论文总结：OASIS: Conditional Distribution Shaping for Offline Safe Reinforcement Learning

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：离线安全强化学习（Offline Safe RL）旨在从预先收集的静态数据集中学习满足安全约束的策略。然而，实际中收集到的演示数据往往是不完美的（例如，低回报或不安全的行为），导致策略与期望的安全高性能之间存在**安全数据集不匹配（Safe Dataset Mismatch, SDM）问题**。具体表现为：
  - **诱惑数据集（Tempting Dataset）**：行为策略过于激进，回报高但成本也高，导致学习到的策略违反安全约束。
  - **保守数据集（Conservative Dataset）**：行为策略过于保守，成本低但回报也低，导致任务效率低下。
- **研究背景**：现有算法（如正则化、悲观估计等）在处理SDM时面临挑战：强制策略贴近次优行为策略会加剧性能退化；而数据重加权方法在数据集覆盖不全时效果有限。
- **整体含义**：本文从**数据驱动（Data-centric）**视角出发，提出通过条件分布塑造（Conditional Distribution Shaping）来改善离线数据集的质量，从而从根源上缓解SDM问题，使后续的离线安全RL训练更有效。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

### 核心思想
- **OASIS（cOnditionAl diStributIon Shaping）**：利用条件扩散模型（Conditional Diffusion Model）作为数据生成器，对原始离线数据集进行重新分布，生成**低成本和/或高回报**的新数据集，供后续的离线安全RL算法（如BCQ-Lag）训练。
- 该方法与模型中心的算法正交，可兼容多种离线安全RL算法。

### 关键技术细节
1. **训练阶段（数据生成器训练）**：
   - 将轨迹视为序列数据，训练一个**条件扩散模型**，以轨迹的累积成本`C(τ)`和累积回报`R(τ)`作为条件。
   - 使用**无分类器引导（Classifier-free guidance）**，同时学习无条件去噪核和条件去噪核，通过掩码训练（以概率p=0.25丢弃条件）。
   - 同时训练逆动力学模型`f̂`（从`s, s'`预测动作a）、奖励模型`r̂`和成本模型`ĉ`，用于后续标签生成。

2. **生成阶段（数据集生成）**：
   - **算法1：OASIS（数据生成）**
     1. 从原始数据集随机采样一个初始状态s。
     2. 初始化一个长度为L的带噪子轨迹（初始状态固定为s，其余为高斯噪声）。
     3. 确定生成条件`yc`（例如设置`Ĉ ≤ κ`以符合安全偏好）。
     4. 逐步执行反向扩散（K步去噪），利用去噪核计算`ϵθ(xk, yc, k)`（公式8）。
     5. 得到生成的干净子轨迹`τg`。
     6. 通过逆动力学模型`f̂`获取动作序列，通过奖励/成本模型获取对应的奖励和成本。
     7. 返回生成的子轨迹及其过渡对。

3. **下游训练**：
   - 将生成的数据集`Dg`用于常规离线安全RL算法（本文采用BCQ-Lag）训练。

### 理论分析
- **定理1（分布塑造误差界）**：在合理的假设下（分数估计误差有界、逆动力学误差有界），生成数据的状态-动作分布与最优策略分布之间的总变差距离（TV）是有界的，且随着去噪步数K增加而减小。
- **定理2（约束违反界）**：基于生成数据集训练的离线安全RL策略，其成本违反程度同样有界，从而提供了安全保证。

## 3. 实验设计

### 数据集与场景
- **基准环境**：采用**Bullet-Safety-Gym**，包含两类任务（Run和Circle）和三种机器人（Ball, Car, Drone），共6个任务：BallRun, CarRun, DroneRun, BallCircle, CarCircle, DroneCircle。
- **数据集类型**：基于原始离线数据集，构造四种类型：
  - **Full**：完整覆盖
  - **Tempting（诱惑）**：包含稀疏的安全演示，且大部分轨迹成本高
  - **Conservative（保守）**：缺乏高回报数据点
  - **Hybrid（混合）**：中等回报、中等成本的轨迹稀缺
- **成本阈值**：主要实验中成本阈值设置为`κ=20`（归一化后为1）。

### 对比方法（Baselines）
- **模型中心方法**：
  - 基于Q学习：BCQ-Lag, BEAR-Lag, CPQ
  - 模仿学习：Behavior Cloning (BC)
  - 分布校正估计：COptiDICE
  - 序列建模：CDT, FISOR
- **数据中心方法**：
  - CVAE-BCQL：用条件变分自编码器（CVAE）替代扩散模型生成数据，其余与OASIS相同。

### 实验数量与充分性
- **主要实验（表1）**：在6个任务上、使用**诱惑数据集**（最具挑战性），对比8种基线方法，每个结果报告3个种子的平均和标准差。
- **多数据集实验（图5）**：在BallCircle和CarCircle任务中，分别使用Full, Conservative, Hybrid数据集，对比相同基线。
- **消融实验**：
  - **去噪步数K（表2）**：测试K=10,20,40对Ball-Circle和Ball-Run任务的影响。
  - **数据效率实验（图6）**：在BallCircle任务中，改变用于训练的数据量（α从0.16%到6.63%），比较OASIS与基线。
  - **分布塑造可视化（图7）**：展示OASIS和CVAE在不同条件下的生成数据分布（回报、成本、轨迹密度）。
- **数据重加权验证（图3）**：在完整数据集上的初步实验。
- **基线敏感性**：在不同数据集和成本阈值下比较。

**充分性评价**：实验覆盖了多种任务、多种数据集类型、多种基线方法和多种评估维度（回报、成本、数据效率、超参数鲁棒性），且均报告了均值与标准差，结果较全面客观。但所有任务均基于模拟器Bullet-Safety-Gym，未在真实世界或更复杂环境验证，存在泛化局限。

## 4. 资源与算力

论文明确说明了计算资源（附录C.3）：
- **硬件**：2×AMD EPYC 7542 32-Core Processor CPU, 2×NVIDIA RTX A6000 GPU, 252 GB内存。
- **训练时长**：
  - 数据生成器训练：约**4小时**（200,000步）。
  - 下游BCQ-Lag训练：约**1.5小时**（200,000步）。
- **总运行**：每项单次实验约5.5小时，但未报告所有实验的总GPU小时数。考虑到多任务、多种子、多超参数，总消耗合理。

## 5. 评价：实验是否充分、客观、公平？

- **充分性**：如上所述，实验规模较大，涵盖了主要变量（任务、数据集类型、基线、超参数、数据量）。消融实验和数据效率测试加强了结论的可靠性。
- **客观性**：所有结果均基于标准基准（Bullet-Safety-Gym）和公开数据集（OSRL），报告了多次独立运行的统计量，未选择性呈现有利结果。
- **公平性**：
  - 对比了多种代表性基线（包括Q学习、分布校正、序列建模、数据增强）。
  - OASIS采用BCQ-Lag作为下游算法，与BCQ-Lag直接对比，体现了数据增强带来的增益。
  - 数据生成条件（成本≤κ）与安全目标一致，未过度倾斜。
- **潜在不足**：所有实验均在物理模拟环境中，未涉及实际机器人或自动驾驶等真实场景。此外，数据集构造可能偏向于表现OASIS的优势（诱惑数据集最困难），但论文也报告了其他数据集上的对比，仍显示OASIS优于基线。

## 6. 论文的主要结论与发现

1. **SDM问题普遍存在**：在离线安全RL中，演示数据（无论诱惑还是保守）都会导致正则化方法性能退化，难以同时保证安全和高回报。
2. **OASIS有效缓解SDM**：通过条件扩散模型生成低风险高回报的数据分布，显著提升了后续策略的安全性（归一化成本≤1）和回报，在6个任务上均优于所有基线（唯一能同时满足安全且回报最高的方法）。
3. **高数据效率**：仅需少量高质量生成数据（α<2%）即可学习良好策略，而基线方法在数据稀少时性能崩溃。
4. **鲁棒性**：对超参数（如去噪步数K）不敏感，在K=10~40范围内性能稳定。
5. **理论保证**：提供了分布塑造误差界和约束违反界，确保方法的安全性能。

## 7. 优点

- **创新性**：首次将数据分布塑造（Data-centric）引入离线安全RL，区别于传统的模型中心方法，开辟了新范式。
- **通用性**：可兼容任何离线安全RL算法，只需替换数据集。
- **有效性**：在多个具有挑战性的数据集上显著优于现有方法，尤其适用于高质量演示稀缺场景。
- **理论保障**：提供严格的性能界，增强了方法的可信度。
- **鲁棒性**：对关键超参数不敏感，数据效率高，实际部署潜力大。
- **可视化分析**：通过分布可视化（图7）直观展示了生成数据如何向安全低风险区域迁移。

## 8. 不足与局限

- **训练耗时较长**：需要先训练扩散模型（约4小时）和逆动力学模型，再训练下游策略，整体计算成本高于直接训练基线。
- **零约束违规仍具挑战**：在诱惑数据集上，尽管OASIS实现了安全（归一化成本<1），但仍有小规模违规，完美安全的策略还无法保证。
- **依赖预定义的逆动力学和奖励/成本模型**：这些模型的学习误差会影响最终生成数据的质量。
- **环境限制**：实验仅在Bullet-Safety-Gym模拟器中，未验证在更复杂、高维的真实世界任务（如自动驾驶、机器人操控）中的表现。
- **数据集构造的人为因素**：Tempting, Conservative等数据集是人工筛选的，真实应用中的分布偏移可能更加复杂。
- **潜在的负面社会影响**：论文指出，若方法被误用（如故意生成不安全数据），可能引发有害后果。
- **评估指标**：仅使用累积回报和成本，未考虑风险敏感指标（如最差情况成本）或多约束场景。

（完）
