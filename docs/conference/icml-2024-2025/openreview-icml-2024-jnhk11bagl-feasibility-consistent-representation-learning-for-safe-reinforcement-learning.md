---
title: Feasibility Consistent Representation Learning for Safe Reinforcement Learning
title_zh: 可行性一致的表示学习用于安全强化学习
authors: "Zhepeng Cen, Yihang Yao, Zuxin Liu, Ding Zhao"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=JNHK11bAGl"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 安全强化学习与可行性表示
tldr: 针对安全强化学习中安全约束估计困难（稀疏信号）的问题，提出可行性一致安全强化学习（FCSRL）。该框架将表示学习与可行性导向目标结合，通过自监督学习从原始状态提取安全相关信息，并采用更可学的安全度量。在多个安全RL基准上，FCSRL在满足约束的同时取得了更高的奖励，证明了其有效性。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-jnhk11bagl/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 816, \"height\": 585, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-jnhk11bagl/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-jnhk11bagl/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1678, \"height\": 1051, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-jnhk11bagl/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 835, \"height\": 517, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-jnhk11bagl/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 683, \"height\": 623, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-jnhk11bagl/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1698, \"height\": 698, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-jnhk11bagl/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 495, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-jnhk11bagl/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1671, \"height\": 1654, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-jnhk11bagl/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 818, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-jnhk11bagl/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 821, \"height\": 390, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-jnhk11bagl/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 795, \"height\": 196, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-jnhk11bagl/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1757, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-jnhk11bagl/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 896, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-jnhk11bagl/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1041, \"height\": 671, \"label\": \"Table\"}]"
motivation: 安全强化学习中安全约束估计比奖励估计更困难，因约束信号稀疏。
method: 提出FCSRL框架，结合表示学习和可行性目标，利用自监督学习提取安全相关信息。
result: 在多个基准任务中，FCSRL在满足约束的同时获得更高奖励。
conclusion: 为安全强化学习提供了一种有效的表示学习方法。
---

## Abstract
In the field of safe reinforcement learning (RL), finding a balance between satisfying safety constraints and optimizing reward performance presents a significant challenge. A key obstacle in this endeavor is the estimation of safety constraints, which is typically more difficult than estimating a reward metric due to the sparse nature of the constraint signals. To address this issue, we introduce a novel framework named Feasibility Consistent Safe Reinforcement Learning (FCSRL). This framework combines representation learning with feasibility-oriented objectives to identify and extract safety-related information from the raw state for safe RL. Leveraging self-supervised learning techniques and a more learnable safety metric, our approach enhances the policy learning and constraint estimation. Empirical evaluations across a range of vector-state and image-based tasks demonstrate that our method is capable of learning a better safety-aware embedding and achieving superior performance than previous representation learning baselines.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：在安全强化学习（Safe RL）中，智能体需要在最大化任务奖励的同时满足安全约束。然而，与奖励信号相比，安全约束（cost）信号的估计更加困难，主要因为：
  - 原始状态的高复杂性导致单步成本预测困难；
  - 成本信号的稀疏性加剧了值函数估计的非平滑性和噪声，导致对长期安全的估计不准确。
- **整体含义**：为解决这一挑战，论文提出**可行性一致的安全强化学习（FCSRL）**框架，通过表示学习从原始状态中提取与安全相关的信息，从而改善约束估计和政策学习，在满足安全约束的同时获得更高的奖励。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：将表示学习与可行性导向的目标结合，利用自监督学习从环境转移动力学中学习潜在结构，并引入一种更平滑的安全度量——**可行性得分**（feasibility score）作为辅助任务，引导表示学习提取安全相关特征。
- **关键技术细节**：
  - **转移动力学一致性损失**（Transition Dynamics Consistency）：使用编码器 \( g \) 将状态 \( s_t \) 映射为嵌入 \( z_t \)，通过转移模型 \( h \) 预测下一状态嵌入 \( \hat{z}_{t+1} = h(z_t, a_t) \)，并与目标编码器（动量更新）生成的目标嵌入 \( z^{(m)}_{t+1} \) 计算SimSiam风格的相似性损失。
  - **可行性一致性损失**（Feasibility Consistency）：定义可行性得分 \( F^\pi(s, a) = \mathbb{E}_\rho [\max_t \gamma^t c(s_t, a_t)] \)，表示最大折扣成本。该指标满足贝尔曼方程，且比传统成本值函数更平滑（论文通过命题4.3证明）。使用预测头 \( \tilde{f} \) 从嵌入 \( z_t \) 预测可行性得分，并与自举估计的目标 \( F^{(m)}(s_t) \) 进行KL散度损失（离散回归）。
  - **整体目标**：\( L_\theta = \mathbb{E}_{\tau \sim \mathcal{D}} [L_\theta^{\text{dyn}}(\tau) + \lambda_{\text{fea}} L_\theta^{\text{fea}}(\tau)] \)，训练编码器、转移模型和预测头。
  - **与RL算法集成**：使用目标编码器 \( g^{(m)} \) 生成的嵌入作为策略和值函数的输入，避免表示学习更新对RL训练的噪声干扰。兼容任何无模型安全RL算法（如PPO-Lagrangian、TD3-Lagrangian）。

## 3. 实验设计

- **数据集/场景**：使用 Safety-Gymnasium 中的6个向量状态任务（PointGoal1、PointButton1、PointPush1、PointGoal2、CarGoal1、CarButton1）和3个图像状态任务（PointButton1、PointGoal2、CarGoal1）。
- **Baseline方法**：
  - 原始状态输入（Raw state input）
  - 前向原始模型（Forward raw model）
  - 前向潜在模型（Forward latent model）
  - 逆模型（Inverse model）
  - 时间对比学习（TCL）
  - SALE（Fujimoto et al., 2023）
  - 值一致模型（VC）：预测成本值函数
  - 图像任务额外对比：CURL、SPR
- **评价指标**：归一化奖励（NR）和归一化成本（NC），成本阈值 \( \epsilon \) 在向量任务中为10（TD3-Lag）或25（PPO-Lag），图像任务中为10。

## 4. 资源与算力

- 论文未明确说明使用的GPU型号、数量及训练时长。仅在实验设置中说明每个方法训练了2M环境步数，但未提供硬件细节。因此，无法总结具体算力消耗。

## 5. 实验数量与充分性

- **实验数量**：
  - 主实验：向量状态任务6个，分别基于PPO-Lag和TD3-Lag进行对比，共12组实验；图像任务3组训练曲线。
  - 不同成本阈值实验：2个任务（PointPush1、CarGoal1），5个阈值 \( \epsilon \in \{5,10,20,30,40\} \)，共10组。
  - 消融实验：2个任务（PointGoal2、PointButton1），分别去除动力学损失、可行性损失、仅输入嵌入，共8组。
  - 预测长度消融：1个任务（PointPush1），4种长度（2,4,6,8），共4组。
  - 嵌入质量对比：线性回归预测成本值和可行性得分的MSE。
- **充分性与公平性**：
  - 实验覆盖多种任务类型（向量和图像、不同难度），对比多个主流表示学习方法，采用相同网络结构和超参数。
  - 消融实验验证了各组件贡献，成本阈值实验检验了方法的泛化能力。
  - 统计分析基于5个随机种子，报告均值和标准差，结果可靠。
  - 但图像任务仅进行3个任务，覆盖略少；未与其他安全RL基线（如CPO、FOCOPS等）在图像任务上对比（但在附录B.4中与CPO、PPO-Lag、FOCOPS、CVPO在向量任务上进行了额外对比，显示FCSRL优于它们）。

## 6. 主要结论与发现

- FCSRL在几乎所有向量状态和图像任务上，在满足成本约束的同时获得了最高的奖励，显著超过所有基线方法。
- 可行性得分比成本值函数更平滑，作为表示学习监督信号能更好地提取安全相关特征，尤其在成本约束严格时优势更明显。
- 动力学一致性损失和可行性一致性损失均起重要作用，但可行性损失更为关键。
- 预测长度增加（如K=4）有利于性能，但过长收益递减。
- 输入原始状态与嵌入的拼接对向量任务有益，但仅输入嵌入会损失奖励相关信息。

## 7. 优点

- **理论贡献**：证明了可行性得分的时间平滑性优于成本值函数（命题4.3），并阐明其与安全概率的关系（命题4.1）。
- **方法创新**：将可行性得分引入表示学习，作为辅助任务提升安全感知嵌入学习，且兼容主流无模型安全RL算法。
- **实验充分**：涵盖向量和图像任务、多种baseline、消融、超参数分析及与经典安全RL方法的对比，结果稳健。
- **应用价值**：在严格安全约束下仍能取得高奖励，对实际安全关键系统有重要潜力。

## 8. 不足与局限

- **实验覆盖**：图像任务仅3个，且未在更复杂或高维图像任务（如自动驾驶场景）上验证。
- **算力信息缺失**：未提供计算资源消耗，不利于复现和成本评估。
- **可迁移性**：方法依赖于二进制成本信号，对于连续成本信号或更复杂的安全定义可能需要调整。
- **理论局限**：命题4.3仅针对单轨迹估计，无法保证在整个状态空间上的全局平滑性。
- **潜在偏差**：在向量任务中，输入原始状态与嵌入的拼接可能会引入冗余信息，导致对原始状态的依赖；未深入分析表示学习对奖励相关信息的保留程度。

（完）
