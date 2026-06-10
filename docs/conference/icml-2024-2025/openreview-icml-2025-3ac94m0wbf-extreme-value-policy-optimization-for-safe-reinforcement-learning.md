---
title: Extreme Value Policy Optimization for Safe Reinforcement Learning
title_zh: 面向安全强化学习的极值策略优化
authors: "Shiqing Gao, Yihang Zhou, Shuai Shao, Haoyu Luo, Yiheng Bing, Jiaxin Ding, Luoyi Fu, Xinbing Wang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=3aC94m0wbF"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 提出了使用极值理论的安全强化学习算法
tldr: 传统的约束强化学习使用期望成本约束，忽略了罕见但高影响力的极端事件，可能导致严重违规。EVO算法利用极值理论建模并利用极值奖励和成本样本，引入极端分位数优化目标，显著降低约束违规，提升安全强化学习的实际安全性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-3ac94m0wbf/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 861, \"height\": 371, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3ac94m0wbf/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 830, \"height\": 298, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3ac94m0wbf/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1778, \"height\": 700, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3ac94m0wbf/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1781, \"height\": 700, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3ac94m0wbf/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1770, \"height\": 342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3ac94m0wbf/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 756, \"height\": 571, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3ac94m0wbf/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1774, \"height\": 798, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3ac94m0wbf/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1763, \"height\": 335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3ac94m0wbf/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1776, \"height\": 655, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3ac94m0wbf/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1777, \"height\": 654, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3ac94m0wbf/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1780, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3ac94m0wbf/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1786, \"height\": 514, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-3ac94m0wbf/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1813, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3ac94m0wbf/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1343, \"height\": 557, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3ac94m0wbf/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1154, \"height\": 711, \"label\": \"Table\"}]"
motivation: 现有约束强化学习忽略罕见极端事件，导致严重违规；需要更精细的安全约束建模。
method: 提出EVO算法，结合极值理论建模尾部分布，引入极端分位数优化目标来减少违规。
result: 在安全强化学习基准中有效降低了约束违规率，同时保持奖励性能。
conclusion: EVO通过考虑极端事件提高了安全强化学习的可靠性。
---

## Abstract
Ensuring safety is a critical challenge in applying Reinforcement Learning (RL) to real-world scenarios. Constrained Reinforcement Learning (CRL) addresses this by maximizing returns under predefined constraints, typically formulated as the expected cumulative cost. However, expectation-based constraints overlook rare but high-impact extreme value events in the tail distribution, such as black swan incidents, which can lead to severe constraint violations. To address this issue, we propose the Extreme Value policy Optimization (EVO) algorithm, leveraging Extreme Value Theory (EVT) to model and exploit extreme reward and cost samples, reducing constraint violations. EVO introduces an extreme quantile optimization objective to explicitly capture extreme samples in the cost tail distribution. Additionally, we propose an extreme prioritization mechanism during replay, amplifying the learning signal from rare but high-impact extreme samples. Theoretically, we establish upper bounds on expected constraint violations during policy updates, guaranteeing strict constraint satisfaction at a zero-violation quantile level. Further, we demonstrate that EVO achieves a lower probability of constraint violations than expectation-based methods and exhibits lower variance than quantile regression methods. Extensive experiments show that EVO significantly reduces constraint violations during training while maintaining competitive policy performance compared to baselines.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：传统约束强化学习（CRL）采用期望值约束（如期望累积成本低于阈值），但忽视了成本分布尾部的罕见但高影响力的极端事件（如黑天鹅事件）。这些极端事件可能导致严重的约束违规，即使期望成本达标，实际违规概率仍可能很高。
- **研究动机**：在自动驾驶、金融交易等安全关键场景中，极端事件虽发生概率低，但后果严重。现有概率约束方法（如WCSAC使用高斯近似CVaR）无法准确捕捉尾部行为，且未充分利用极值样本。
- **整体含义**：针对CRL中极端事件被忽略的问题，提出结合极值理论（EVT）的EVO算法，通过建模尾部分布、引入极端分位数约束和极端优先重放机制，显著降低约束违规概率，提升安全性。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

### 核心思想
- 利用极值理论中的广义帕累托分布（GPD）建模成本分布的尾部，并引入极端分位数约束（即风险边界）来替代传统期望约束，从而显式捕获极端样本。
- 设计极端优先重放机制，基于GPD分位数水平赋予极值样本更高重放概率，增强学习信号。
- 采用离策略重要重采样扩充极值样本量，降低GPD拟合方差。

### 关键技术细节
- **极端分位数约束**：将约束条件设为 \( q_{\mu+\nu} \le d \)，其中 \( q_\mu \) 为安全边界（由期望成本决定），\( \nu \) 为极端范围。尾部建模使用GPD：\( z = q_{\mu+\nu} - q_\mu \) 遵循GPD，风险边界表示为 \( q_\mu + q_H^{\nu/(1-\mu)} \)。
- **GPD参数估计**：通过最大似然估计拟合形状参数 \( \xi \) 和尺度参数 \( \sigma \)，风险边界计算公式为 \( q_\mu + \frac{\sigma}{\xi}\left[(1-\frac{\nu n}{N_\mu})^{-\xi} - 1\right] \)。
- **极端优先机制**：对奖励和成本分别拟合GPD，计算每个样本在各自GPD中的分位数水平 \( \omega_r,\omega_c \)，优先级 \( p = \omega_r + \omega_c \)，重放概率 \( P(s_i) = p(s_i)/\sum p(s_k) \)。
- **离策略重要重采样**：利用历史策略样本，通过重要性权重 \( \pi(a|s)/\pi_0(a|s) \) 调整样本值，扩充极值样本集。
- **策略优化**：基于CPO的信任域优化，目标函数为最大化回报优势，约束为 \( J_C(\pi_k) + \frac{1}{1-\gamma}E[A_C] + q_H^{\nu/(1-\mu)} \le d \)，配合KL散度约束。

### 算法流程（文字说明）
1. 收集当前策略轨迹，计算累积成本和优势函数。
2. 更新价值网络。
3. 对缓冲区的离策略样本进行重要性重采样。
4. 使用重采样后的成本样本拟合成本GPD，计算风险边界。
5. 使用重采样后的奖励样本拟合奖励GPD，计算奖励极端边界。
6. 根据两个GPD的分位数水平计算每个样本的极端优先级。
7. 在信任域内优化策略，使回报优势最大化并满足极端分位数约束。
8. 重复至收敛。

## 3. 实验设计：使用的数据集/场景、benchmark、对比方法

- **场景与数据集**：
  - **Safety Gymnasium**：导航任务，包括Point和Car两种机器人，以及Goal（到达目标并避开危险）和Circle（绕圈并避免出界）两种任务，共4个环境（PointGoal1, CarGoal1, PointCircle1, CarCircle1）。
  - **Safety MuJoCo**：速度控制任务，包括Ant、HalfCheetah、Humanoid、Swimmer的Velocity变体，共4个环境。
- **Benchmark**：标准开源安全强化学习基准，使用OmniSafe框架。
- **对比方法**：
  - 期望约束：CPO
  - 概率约束：WCSAC
  - 状态增强：Saute, Simmer
  - 额外基线（附录）：PPO-Lagrangian, RCPO

## 4. 资源与算力

- **文中明确说明**：所有实验在PyTorch 2.0.0、CUDA 11.3、Ubuntu 20.04.2 LTS上运行，使用单块GeForce RTX 3090 GPU。
- **训练时长**：以SafetyPointCircle1为例，EVO训练时间约11h53m，GPD拟合时间仅8-9秒，比CPO（11h23m）增加有限。表1给出了不同样本数下的具体训练时间。
- 未提及更详细的能耗或分布式训练信息。

## 5. 实验数量与充分性

- **实验数量**：在8个环境（4个Safety Gym + 4个Safety MuJoCo）上进行主实验，每个方法使用6个随机种子，结果以均值±标准差呈现。
- **消融实验**：3组：去掉EVT约束（改用常数分位数）、去掉极端优先机制、去掉离策略重采样（仅用on-policy样本拟合GPD）。
- **敏感性分析**：成本限制敏感性（阈值0,25,35）；GPD拟合样本量敏感性（10,20,50,100）；GPD与高斯拟合精度对比（使用KS检验）。
- **充分性判断**：实验覆盖了多个任务类型、多种基线方法，消融和敏感性分析充分，结果客观（有统计误差线），对比公平（统一超参数和训练步数10^7步）。因此实验设计较为充分、客观。

## 6. 论文的主要结论与发现

- **主要结论**：EVO能显著降低训练过程中的约束违规，在大多数环境中实现接近零违规，同时保持与CPO竞争的策略回报，优于WCSAC、Saute、Simmer等基线。
- **理论发现**：推导了约束违规上界（比CPO更紧），证明了零违规分位水平的存在性；证明了EVO的约束违规概率低于期望约束方法；证明了EVO的方差低于分位数回归方法。
- **GPD拟合优势**：通过KS检验验证GPD比高斯分布更准确捕捉尾部行为。
- **鲁棒性**：在成本阈值变化、小样本（如10个样本）下仍有效。

## 7. 优点：方法或实验设计上的亮点

- **方法创新**：首次将极值理论系统引入约束强化学习，解决极端事件被忽视的问题，理论分析扎实。
- **技术亮点**：
  - 极端分位数约束显式建模尾部，提供更严格的安全保障。
  - 极端优先重放机制有效利用稀缺极值样本。
  - 离策略重要重采样缓解极值样本稀疏导致的高方差。
- **实验设计亮点**：
  - 多环境、多基线对比，包括标准CRL方法和状态增强方法。
  - 详尽的消融和敏感性分析，验证各组件贡献。
  - 提供综合评估指标（回报/违规率比值），避免单一指标偏差。
  - 代码开源，可复现。

## 8. 不足与局限

- **GPD拟合依赖**：当极值与正常值差异不明显时，GPD拟合精度可能下降（文中提及可通过非线性变换改进），但实验未充分探讨此场景。
- **阈值选择**：安全边界 \( q_\mu \) 设定为期望成本，但实际中期望成本随训练变化，可能导致GPD拟合不稳定。
- **实验环境限制**：仅在模拟器（Safety Gym和MuJoCo）中验证，未在真实机器人或真实自动驾驶场景中测试，实际部署可能存在sim-to-real gap。
- **计算开销**：虽比CPO增加有限，但需要额外进行GPD拟合和重要性重采样，对于极高维或实时性要求严格的场景可能仍有瓶颈。
- **多约束扩展**：论文仅处理单约束，未讨论多约束或约束间相互影响的情况。
- **基线覆盖**：对比方法中缺少最新基于模型或在线安全方法的比较，如Lagrangian-PID、LOOP等。

（完）
