---
title: "CHPO: Constrained Hybrid-action Policy Optimization for Reinforcement Learning"
title_zh: CHPO：面向强化学习的约束混合动作策略优化
authors: "Ao Zhou, Jiayi Guan, Li Shen, Fan Lu, Sanqing Qu, Junqiao Zhao, Ziqiao Wang, Ya Wu, Guang Chen"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=KMaBmPHkVj"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 混合动作空间中的约束强化学习实现安全策略
tldr: 现有混合动作强化学习主要关注奖励最大化，忽视了安全约束。本文提出CHPO算法，重新定义约束混合动作RL的目标，通过策略优化同时处理离散-连续混合动作和成本约束，适用于安全关键应用。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1426, \"height\": 268, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1438, \"height\": 441, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1439, \"height\": 267, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1440, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1438, \"height\": 440, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1442, \"height\": 269, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1420, \"height\": 436, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-kmabmphkvj/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1444, \"height\": 460, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-kmabmphkvj/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1448, \"height\": 846, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-kmabmphkvj/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1035, \"height\": 722, \"label\": \"Table\"}]"
motivation: 混合动作空间中的安全强化学习缺乏有效的约束处理算法。
method: 提出约束混合动作策略优化算法，重构目标函数并设计专用优化方法。
result: 算法成功在混合动作空间中学习满足约束的安全策略。
conclusion: 为安全关键应用中的混合动作决策提供了有效方法。
---

## Abstract
Constrained hybrid-action reinforcement learning (RL) promises to learn a safe policy within a parameterized action space, which is particularly valuable for safety-critical applications involving discrete-continuous hybrid action spaces. However, existing hybrid-action RL algorithms primarily focus on reward maximization, which faces significant challenges for tasks involving both cost constraints and hybrid action spaces. In this work, we propose a novel Constrained Hybrid-action Policy Optimization algorithm (CHPO) to address the problems of constrained hybrid-action RL. Concretely, we rethink the limitations of hybrid-action RL in handling safe tasks with parameterized action spaces and reframe the objective of constrained hybrid-action RL by introducing the concept of Constrained Parameterized-action Markov Decision Process (CPMDP). Subsequently, we present a constrained hybrid-action policy optimization algorithm to confront the constrained hybrid-action problems and conduct theoretical analyses demonstrating that the CHPO converges to the optimal solution while satisfying safety constraints. Finally, extensive experiments demonstrate that the CHPO achieves competitive performance across multiple experimental tasks.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义
- **研究动机**：在安全关键应用（如自动驾驶、机器人操作）中，智能体需要在混合动作空间（离散动作+连续参数）下学习策略，同时满足安全约束（如避碰）。现有混合动作强化学习算法（如HPPO、PDQN）只关注奖励最大化，忽略成本约束；而简单加入约束（如拉格朗日乘子法）会导致训练不稳定、超参数敏感、陷入局部最优等问题。
- **整体含义**：本文首次系统性地定义了“约束混合动作强化学习”问题，并提出专门算法CHPO，目标是在参数化动作空间中学习既最大化累计奖励又满足给定成本约束的安全策略。

## 2. 方法论
- **核心思想**：引入**约束参数化马可夫决策过程（CPMDP）**框架，将成本约束纳入混合动作空间建模。基于CRPO的启发，直接对原始目标进行策略梯度优化，避免使用拉格朗日乘子。
- **关键技术细节**：
  - **架构**：构建约束混合动作Actor-Critic结构，包含奖励价值网络 \(V^r\)、成本价值网络 \(V^{c_i}\)、离散策略网络 \(\pi_{\theta_d}\) 和连续策略网络 \(\pi_{\theta_c}\)。
  - **策略更新规则**（式(8)）：
    - 若当前策略满足成本约束（使用无折扣成本回报 \(\bar{L}^{c_i}\) 判断），则更新目标是最大化奖励优势（式(12)）；
    - 若违反约束，则更新目标是最小化成本优势（式(13)）。
  - **更新方式**：使用带裁剪的PPO式重要性采样，对离散和连续策略分别更新。
- **理论分析**：
  - 证明策略收敛到最优的边界（Proposition 4.3）：\(L(\pi^*_{\theta_p}) - \mathbb{E}[L(\pi_{\theta_p}^K)] \leq \Theta\left(\frac{\sqrt{|S||A|}}{(1-\gamma)^{1.5}\sqrt{K}}\right)\)。
  - 证明成本收敛到约束阈值附近（Proposition 4.4）：\(\mathbb{E}[L(\pi_{\theta_p}^K)] - \bar{c}_i \leq \Theta\left(\sqrt{\frac{(1-\gamma)|S||A|}{K}}\right)\)。
  - 引入C/A比率（成本最小化更新步数占比）影响最终策略质量。

## 3. 实验设计
- **任务/场景**：
  - 三个DI-engine标准任务：Moving、Sliding、HardMove（均引入危险区域和成本）。
  - 自定义Parking任务（RS曲线停车，避碰）。
- **基准方法（Baselines）**：
  - PADDPG-Lag：PADDPG + 拉格朗日乘子。
  - HPPO-Lag：HPPO + 拉格朗日乘子。
  - PDQN-Rco：PDQN + 奖励约束（RCPO风格）。
- **评估指标**：累计奖励（↑）、累计成本（↓，需 ≤ 成本阈值 \(\bar{c}_i\)）。

## 4. 资源与算力
- 硬件配置：AMD Ryzen Threadripper 3960X CPU + NVIDIA RTX 3090 GPU。
- 文中未明确说明训练总时长、GPU数量或具体耗时，仅提及在单机上进行实验。

## 5. 实验数量与充分性
- **实验数量**：共4个任务，每个任务3个随机种子，报告均值和方差；成本阈值设置3种（1.0, 1.5, 2.0）；消融实验2组（约束模块去除、C/A比率变化）。
- **充分性评估**：
  - 实验覆盖了不同难度、不同混合动作维度（HardMove高维离散空间）的场景。
  - 对比了3种有代表性的基线，且基线均针对混合动作空间做了约束扩展。
  - 消融实验验证了关键组件（约束模块）和超参数（C/A比率）的影响。
  - 不足：任务数量有限（仅4个），且均为仿真环境，未包含真实机器人或更复杂的连续控制任务；成本约束只有单约束（i=1），未验证多约束情况。

## 6. 主要结论与发现
- CHPO能够在满足成本约束的前提下获得比所有基线更高的奖励，且训练过程更稳定。
- 在不同成本阈值下，CHPO都能自适应地调整策略，使成本紧贴阈值，同时保持高奖励。
- 消融实验表明约束模块是保证安全的必要条件；适当的C/A比率（约1/6～1/5）能平衡奖励与安全。
- 理论证明支持算法收敛到最优解且成本不越界。

## 7. 优点
- **问题定义新颖**：首次将约束强化学习与混合动作空间结合，提出CPMDP框架。
- **算法简洁有效**：直接优化原始目标，避免拉格朗日乘子带来的不稳定和调参负担。
- **理论支撑**：给出了收敛性和成本边界的证明，增强可信度。
- **实现细节完整**：提供了伪代码和开源代码（github.CHPO），可复现性强。
- **实验设计合理**：对比了多种经过改造的基线，消融实验验证了关键组件。

## 8. 不足与局限
- **实验覆盖有限**：仅4个仿真任务，未在真实机器人或复杂安全关键系统（如自动驾驶实车）上验证。
- **仅考虑单约束**：CPMDP定义允许多个成本，但实验均采用单成本约束（i=1），多约束场景未测试。
- **在线采样效率低**：依赖在线交互，实际应用中可能因样本不足而难以收敛；文中提到未来可探索离线RL方法。
- **C/A比率需手动调节**：虽然在一定范围内鲁棒，但最优比率因任务而异，仍需一定程度调参。
- **未与其他安全RL方法对比**（如CPO、PPO-Lagrange等）：基线仅从混合动作方法扩展而来，缺少与标准安全RL算法（但需适应混合动作）的横向比较。
- **理论边界较宽松**：证明中的 \(\Theta\) 界依赖于状态和动作维度，实际收敛速度可能受因素影响更多。

（完）
