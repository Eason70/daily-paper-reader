---
title: "From Text to Trajectory: Exploring Complex Constraint Representation and Decomposition in Safe Reinforcement Learning"
title_zh: 从文本到轨迹：探索安全强化学习中复杂约束的表示与分解
authors: "Pusen Dong, Tianchen Zhu, Yue Qiu, Haoyi Zhou, Jianxin Li"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=MDpIQ9hQ7H"
tags: ["query:safe-rl-cbf"]
score: 4.0
evidence: 使用自然语言约束的安全强化学习
tldr: 安全强化学习通常需要人工设计代价函数来表达约束，费时且缺乏可迁移性。本文利用文本的双重角色，提出轨迹级文本约束翻译器（TTCT），将自然语言约束转化为训练信号，无需手动设计成本函数。实验表明该方法能有效处理复杂约束，提升灵活性和可迁移性。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1448, \"height\": 533, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 914, \"height\": 353, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1423, \"height\": 327, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1457, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1427, \"height\": 326, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1450, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 866, \"height\": 380, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1301, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 863, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 646, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1463, \"height\": 651, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 999, \"height\": 1351, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 847, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 865, \"height\": 382, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mdpiq9hq7h/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 845, \"height\": 416, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-mdpiq9hq7h/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1455, \"height\": 312, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-mdpiq9hq7h/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1456, \"height\": 868, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-mdpiq9hq7h/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 833, \"height\": 476, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-mdpiq9hq7h/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 694, \"height\": 118, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-mdpiq9hq7h/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1456, \"height\": 244, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-mdpiq9hq7h/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1455, \"height\": 247, \"label\": \"Table\"}]"
motivation: 现有自然语言约束安全强化学习需要人工设计成本函数。
method: 提出TTCT，利用文本作为约束和训练信号，自动生成约束表征。
result: 无需手动设计代价函数，有效处理复杂约束。
conclusion: TTCT提升了安全强化学习灵活性和可迁移性。
---

## Abstract
Safe reinforcement learning (RL) requires the agent to finish a given task while obeying specific constraints. Giving constraints in natural language form has great potential for practical scenarios due to its flexible transfer capability and accessibility. Previous safe RL methods with natural language constraints typically need to design cost functions manually for each constraint, which requires domain expertise and lacks flexibility. In this paper, we harness the dual role of text in this task, using it not only to provide constraint but also as a training signal. We introduce the Trajectory-level Textual Constraints Translator (TTCT) to replace the manually designed cost function. Our empirical results demonstrate that TTCT effectively comprehends textual constraint and trajectory, and the policies trained by TTCT can achieve a lower violation rate than the standard cost function. Extra studies are conducted to demonstrate that the TTCT has zero-shot transfer capability to adapt to constraint-shift environments.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题**：安全强化学习（Safe RL）中，传统方法需要为每条约束手动设计代价函数（cost function），这既依赖领域专业知识，又缺乏灵活性；同时现有工作只能处理基于单状态/单实体的简单约束，无法表达涉及多状态、多实体、时序关系的复杂安全要求（如“喝酒后不能开车”或“触碰熔岩不能超过三次”）。
- **意义**：作者提出使用**轨迹级文本约束**（trajectory-level textual constraints），用自然语言直接描述整个回合的复杂安全条件，并设计 TTCT 框架将文本约束自动转换为代价信号，无需人工设计代价函数，从而提升安全 RL 的通用性和可迁移性。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将文本约束同时作为约束来源和训练信号，通过对比学习对齐轨迹编码与文本编码，并用因果 Transformer 捕获轨迹时序信息；进一步利用注意力机制将回合级稀疏代价分解到每个状态-动作对上，缓解代价稀疏问题。
- **关键技术细节**：
  - **文本-轨迹对齐组件**：使用因果 Transformer 编码轨迹序列得到隐状态 {H_t}，使用预训练语言模型（BERT）编码文本得到 L；通过对比学习（KL 散度版 MC Loss）和轨迹内时序对比损失（WT Loss）最大化违规轨迹与对应文本的余弦相似度，最小化非匹配对的相似度。
  - **代价分配组件**：引入注意力分数 e_t = sigmoid(cosine(H_t, L)) 衡量每步对约束违规的影响；用一个代价分配层 F_c 生成单步代价 ĉ_t，同时用另一个网络预测回合代价 Ĉ(y)；通过均方误差损失 L_CA 约束两者之和相等，从而将稀疏的回合代价分配到各步。
  - **推理阶段**：若当前轨迹与文本相似度超过阈值 β，则判定违规并输出代价 1；否则输出分配的单步代价。
- **整体训练**：三部分损失（L_MC + L_WT + L_CA）端到端联合优化。

### 3. 实验设计

- **数据集/场景**：
  - **2D 网格探索**：Hazard-World-Grid（Grid），12×12 网格，包含熔岩、水、草地等危险/有益元素。
  - **3D 机器人导航**：SafetyGoal（Goal），基于 Safety-Gymnasium，包含花瓶、危险物等。
  - **零样本迁移场景**：LavaWall（Grid 变体，含随机熔岩墙）。
- **约束类型**：超过 200 条轨迹级文本约束，分为四类：定量（如“触碰熔岩不超过 8 次”）、顺序（如“踩水后不能踩熔岩”）、关系（如“与危险物保持距离”）、数学（如“20 HP，熔岩减 3，草地减 2，水回复 1，不要死”）。
- **对比方法**：PPO（无约束）、PPO_Lagrangian、CPPO_PID、FOCOPS。
- **训练模式**：地面真值代价模式（GC，使用人工定义的损失函数）和代价预测模式（CP，使用 TTCT 预测的代价）。
- **评估指标**：平均回合奖励（Avg. R）和平均回合代价（Avg. C，即违规率）。

### 4. 资源与算力

- 论文附录 A.3 指出：TTCT 训练使用 **A100 GPU**，训练约 **1 天**。未提供训练轮数或具体 GPU 数量，但提及 batch size=194，epochs=32，学习率 1e-6。

### 5. 实验数量与充分性

- 主要实验：在 Grid 和 Goal 两个任务上，对四种安全 RL 算法（PPO_Lag、CPPO_PID、FOCOPS）分别比较 CP 与 GC 模式，并对比 PPO 基线。
- 消融实验：去掉代价分配组件（CP w/o CA），展示其贡献。
- 额外实验：
  - **Pareto 前沿**：在三种算法上分别绘制 200 个策略的奖励-代价前沿，证明 CP 更优。
  - **零样本迁移**：Grid 训练的 TTCT 直接用于 LavaWall，无需微调。
  - **分析实验**：违规预测 ROC（AUC=0.98）、不同文本编码器（BERT、GPT2、Transformer）、轨迹长度敏感性、推理时间等。
- **充分性**：实验覆盖了多种算法、任务、约束类型，消融和迁移实验设计合理，结果充分支持结论。但未涉及真实机器人或更复杂 3D 场景，样本效率分析较少。

### 6. 论文的主要结论与发现

1. TTCT 能准确预测轨迹是否违反文本约束（AUC=0.98，F1=0.88）。
2. 使用 TTCT 预测代价训练的智能体，在几乎所有算法和任务上违规率都低于使用地面真值代价的智能体（最多降低 4×），且奖励保持相当。
3. 代价分配组件显著提升了安全性（消融实验证明了其必要性）。
4. TTCT 具有零样本迁移能力，可在约束改变的环境中直接应用。
5. 通过注意力可视化，发现代价分配能够正确识别关键违规步（如顺序约束中“先踩熔岩再踩草地”的触发步），并为危险趋势提供逐步增加的代价。

### 7. 优点

- **方法创新**：首次将轨迹级复杂自然语言约束与安全 RL 结合，用文本作为唯一监督信号，避免了人工设计代价函数。
- **技术亮点**：采用对比学习和时序分解解决稀疏代价问题；使用因果 Transformer 保持左到右时序；代价分配组件兼具可解释性。
- **实验全面**：涵盖两类环境、四种安全 RL 算法、多种约束类型、消融、零样本、Pareto 前沿以及可视化案例，结果稳健。
- **可迁移性**：零样本适应能力展示了实际应用潜力。

### 8. 不足与局限

- **违规率非零**：虽低于基线但仍存在违规，无法保证绝对安全（论文也承认这一点）。
- **轨迹长度限制**：当轨迹变长（超过 200 步），AUC 下降（Transformer 长程能力瓶颈）。
- **计算开销**：推理时需同时运行因果 Transformer 和语言模型，可能不适合实时或低计算资源场景。
- **实验范围**：仅测试了 2D 和 3D 模拟环境，未涉及真实物理系统或更复杂的高自由度机器人。
- **约束生成依赖**：200+ 条约束基于模板自动生成，未与人类众包标注对比，开放性约束理解泛化能力尚未充分验证。
- **样本效率**：对历史轨迹的依赖可能导致需要更多数据才能收敛（论文未详细分析样本复杂度）。

（完）
