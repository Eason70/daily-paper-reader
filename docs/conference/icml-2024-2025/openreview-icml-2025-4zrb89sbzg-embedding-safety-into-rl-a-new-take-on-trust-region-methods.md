---
title: "Embedding Safety into RL: A New Take on Trust Region Methods"
title_zh: 将安全嵌入强化学习：信任区域方法的新视角
authors: "Nikola Milosevic, Johannes Müller, Nico Scherf"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=4zRb89SbzG"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: C-TRPO保证信任区域内仅含安全策略的约束RL
tldr: 本文提出Constrained TRPO（C-TRPO），通过重塑策略空间几何形状确保信任区域仅包含安全策略，从而在训练全程满足安全约束，避免奖励牺牲。理论分析揭示了与TRPO、CPO的联系，实验表明C-TRPO在减少约束违反的同时保持了高回报，为约束RL提供了更强的安全保证。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 745, \"height\": 276, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 862, \"height\": 431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1659, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 595, \"height\": 527, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1378, \"height\": 710, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 826, \"height\": 366, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1705, \"height\": 880, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1734, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1731, \"height\": 506, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1746, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1748, \"height\": 522, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 820, \"height\": 557, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1770, \"height\": 557, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4zrb89sbzg/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 821, \"height\": 557, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-4zrb89sbzg/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1228, \"height\": 2084, \"label\": \"Table\"}]"
motivation: 现有约束RL方法要么牺牲奖励要么允许不安全训练。
method: 重塑策略空间几何，保证信任区域只含安全策略。
result: 在多个CMDP任务中违反约束少且回报高。
conclusion: C-TRPO提供了一种更安全且高效的约束策略优化方法。
---

## Abstract
Reinforcement Learning (RL) agents can solve diverse tasks but often exhibit unsafe behavior. Constrained Markov Decision Processes (CMDPs) address this by enforcing safety constraints, yet existing methods either sacrifice reward maximization or allow unsafe training. We introduce Constrained Trust Region Policy Optimization (C-TRPO), which reshapes the policy space geometry to ensure trust regions contain only safe policies, guaranteeing constraint satisfaction throughout training. We analyze its theoretical properties and connections to TRPO, Natural Policy Gradient (NPG), and Constrained Policy Optimization (CPO). Experiments show that C-TRPO reduces constraint violations while maintaining competitive returns.

---

## 论文详细总结（自动生成）

# 论文结构化总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：强化学习（RL）在连续控制任务中表现优异，但训练过程中可能探索不安全行为，在真实世界应用中存在风险。
- **现有方法的不足**：
  - 基于约束马尔可夫决策过程（CMDP）的算法要么在训练中允许不安全行为（如CPO会振荡于约束边界），要么牺牲奖励最大化（如PCPO过度保守）。
  - 拉格朗日方法（如PPO-Lag、TRPO-Lag）存在乘子振荡、超调问题；惩罚方法（如P3O）会引入优化偏差，导致次优解。
- **本文目标**：提出一种既能保证训练全程安全（零/低违规），又能保持高回报的通用CMDP求解方法。

## 2. 方法论

### 核心思想
- **重塑策略空间几何**：将信任区域（trust region）限制在安全策略集内部，而非像传统TRPO那样覆盖整个策略空间。
- **关键工具**：构造一种新的Bregman散度——**受约束KL散度**（Constrained KL-Divergence, DC），由带屏障函数（barrier function）的镜像函数Φ_C诱导，使得散度值在策略接近成本约束边界时趋向无穷大，从而信任区域自动避开不安全策略。

### 技术细节
1. **安全镜像函数**：
   \[
   \Phi_C(d) = \Phi_K(d) + \sum_{i=1}^m \beta_i \phi(b_i - c_i^\top d),
   \]
   其中\(\Phi_K\)是条件负熵，\(\phi\)为满足\(\phi'(x) \to +\infty\; (x\to 0^+)\)的凸函数（如\(\phi(x)=x\log x\)或\(-\log x\)）。
2. **受约束KL散度**：
   \[
   D_C(d_{\pi_k}\| d_\pi) = D_K(d_{\pi_k}\| d_\pi) + \sum_i \beta_i D_{\phi_i}(d_{\pi_k}\| d_\pi),
   \]
   其中\(D_{\phi_i}\)是Bregman散度，依赖于成本值函数。
3. **代理散度\(\bar D_C\)**：实践中用成本优势函数近似真实成本差，避免计算新策略的成本回报，实现局部可计算。
4. **C-TRPO更新**：
   - 若当前策略安全，求解带代理散度约束的优化问题（线性近似目标、二次近似约束，共轭梯度法求解）。
   - 若当前策略不安全，执行**恢复步**：仅最小化成本（使用TRPO式更新）。
   - **滞回机制**：设置更严格的恢复阈值\(b_H\)（如0.8b），帮助策略远离边界。
5. **C-NPG（连续时间版本）**：C-TRPO的二次近似等价于自然梯度流，理论保证了安全集的不变性和全局收敛性。

### 算法流程（文字描述）
- 初始化安全策略\(\pi_0\)，超参数\(\beta, b_H\)。
- 每轮迭代：
  1. 从环境采样轨迹。
  2. 若当前策略在滞回安全集内：计算奖励优势\(A_r\)，使用\(\bar D_C\)作为散度约束，执行TRPO更新。
  3. 否则：使用负成本优势\(-A_c\)，以\(\bar D_{KL}\)为散度约束，执行TRPO更新。
  4. 得到新策略。

## 3. 实验设计

- **环境与场景**：Safety Gymnasium 基准，包含**8个任务**：
  - 4个导航任务：CarButton、PointGoal、RacecarCircle、PointPush。
  - 4个运动任务：AntVelocity、HalfCheetahVelocity、HumanoidVelocity、HopperVelocity。
- **对比方法**（共9种）：
  - CPO、PCPO（投影式）、CPPO-PID（PID拉格朗日）、PPO-Lag、TRPO-Lag、FOCOPS、CUP、IPO、P3O。
- **评估指标**：
  - 最终成本（阈值归一化，负值表示安全）。
  - 奖励（PPO归一化）。
  - **成本遗憾**（公式2）：训练过程中累计的超出成本阈值之和。
- **超参数**：固定\(\beta=1\)，滞回分数\(b_H=0.8b\)，所有实验一致。

## 4. 资源与算力

- **文中未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅提及训练步数为10 million environment steps，采用5个随机种子。

## 5. 实验数量与充分性

- **主实验**：8个任务 × 5种子 = 40次独立训练，报告IQM（25%分位数均值）及分层bootstrap置信区间。
- **消融/补充实验**：
  - β参数影响（AntVelocity上测试β=0.05, 0.2, 1）。
  - 滞回分数\(b_H\)影响（1 vs 0.2）。
  - **消融研究**：分别比较CPO+C-TRPO（带/不带滞回），共4种组合，验证核心组件贡献。
  - 噪声敏感性实验：在成本值估计中加不同强度高斯噪声（σ=0.05~0.5）。
- **充分性评价**：实验设计较全面，覆盖多类型任务（导航与运动），对比方法多，报告了统计不确定性。但缺乏计算效率对比（时间/样本），且未在其他标准基准（如Safety Gym的更多变体）上验证。总体充分，但未做跨算法超参数调优的公平性声明。

## 6. 主要结论与发现

- C-TRPO在保证**低成本遗憾**的同时取得了**与最优方法相当的奖励回报**，优于大多数现有方法（如CPO、CUP、TRPO-Lag等）。
- 与CPO相比，C-TRPO显著减少了训练过程中的成本违规（成本遗憾更低），且避免了振荡；与P3O相比，C-TRPO奖励更高。
- **理论贡献**：证明C-NPG流保持安全集不变性，并收敛到最优安全策略的Bregman投影，满足对约束的最小等值满足（as few constraints as required）。
- **实用推荐**：\(\beta=1\)，\(b_H=0.8b\)作为默认设置。

## 7. 优点

- **方法创新**：将屏障函数融入信任区域几何，而非简单地添加外部约束，从根本上确保安全。
- **理论严谨**：提供了更新界（worst-case violation）、安全不变性、全局收敛证明，与TRPO/CPO/NPG的联系清晰。
- **实验全面**：多种指标（特别是成本遗憾）更真实反映训练安全；消融和噪声实验验证了鲁棒性。
- **实现简洁**：几乎与CPO同复杂度，仅多估计一个成本值函数，无额外计算负担。

## 8. 不足与局限

- **依赖估计精度**：代理散度\(\bar D_C\)依赖成本优势函数的准确估计，噪声或偏差可能导致不安全的更新（尽管有滞回机制补救）。
- **有限样本分析缺失**：未给出C-TRPO有限样本下的遗憾界或收敛速率，仅提供连续时间理论。
- **屏障函数的保守性**：大的β会过度惩罚靠近边界的策略，可能牺牲最优性；实验中β=1表现良好，但理论上最优策略可能恰在边界上，屏障函数会阻止接近。
- **应用限制**：方法基于折扣CMDP，对逐时步或逐轨迹安全性约束（如必须避免某些状态）无法直接保证，需要额外机制。
- **计算资源信息缺失**：未报告GPU型号、训练时长等，不利于复现和效率评估。
- **未做跨算法超参数搜索**：所有方法可能使用默认参数，C-TRPO的优势可能部分来自特定β和滞回设置，需更多公平比较。

（完）
