---
title: Probabilistic Constrained Reinforcement Learning with Formal Interpretability
title_zh: 具有形式可解释性的概率约束强化学习
authors: "YANRAN WANG, QIUCHEN QIAN, David Boyle"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=Zo9zXdVhW2"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 约束强化学习结合形式化方法，提供可解释性
tldr: 本文提出自适应Wasserstein变分优化方法，将约束强化学习视为概率推理，通过形式化方法增强可解释性。该方法能处理随机动态并保证安全约束，为安全RL提供了可解释的推理工具。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-zo9zxdvhw2/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 847, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-zo9zxdvhw2/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1710, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-zo9zxdvhw2/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1711, \"height\": 1041, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-zo9zxdvhw2/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 857, \"height\": 468, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-zo9zxdvhw2/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 852, \"height\": 495, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-zo9zxdvhw2/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1711, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-zo9zxdvhw2/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 868, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-zo9zxdvhw2/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1199, \"height\": 780, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-zo9zxdvhw2/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1375, \"height\": 709, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-zo9zxdvhw2/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1617, \"height\": 1231, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-zo9zxdvhw2/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1434, \"height\": 876, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-zo9zxdvhw2/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1254, \"height\": 542, \"label\": \"Table\"}]"
motivation: 强化学习在顺序决策中缺乏可解释性，尤其是奖励函数和策略的解释。
method: 提出AWaVO方法，利用Wasserstein变分优化将约束RL建模为概率推理。
result: 在多种动态环境下有效推理安全约束，并提供形式化可解释性。
conclusion: 该方法弥合了强化学习与可解释安全控制之间的差距。
---

## Abstract
Reinforcement learning can provide effective reasoning for sequential decision-making problems with variable dynamics. Such reasoning in practical implementation, however, poses a persistent challenge in interpreting the reward function and the corresponding optimal policy. Consequently, representing sequential decision-making problems as probabilistic inference can have considerable value, as, in principle, the inference offers diverse and powerful mathematical tools to infer the stochastic dynamics whilst suggesting a probabilistic interpretation of policy optimization. In this study, we propose a novel Adaptive Wasserstein Variational Optimization, namely AWaVO, to tackle these interpretability challenges. Our approach uses formal methods to achieve the interpretability: convergence guarantee, training transparency, and intrinsic decision-interpretation. To demonstrate its practicality, we showcase guaranteed interpretability including a global convergence rate $\Theta(1/\sqrt{T})$ not only in simulation but also in real-world quadrotor tasks. In comparison with state-of-the-art benchmarks, including TRPO-IPO, PCPO, and CRPO, we empirically verify that AWaVO offers a reasonable trade-off between high performance and sufficient interpretability.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：强化学习（RL）在顺序决策问题中具有很强的推理能力，但其实际应用面临严重挑战——**缺乏可解释性**。具体包括三个关键挑战：(a) **收敛保证**——框架能否保证收敛到最优策略；(b) **训练透明度**——训练过程中收敛速率的可预测性；(c) **决策解释**——为何做出特定序列决策，以及潜在因素对决策的量化影响。
- **背景**：现有可解释性方法多为事后解释（如显著性图），可能不完整或不准确；而固有可解释性方法虽能提供决策解释，但无法保证收敛和训练透明。本文首次提出一种**固有可解释的约束RL框架**，通过概率推理视角重新构建约束RL，从而同时解决三个关键挑战。

## 2. 方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：将约束马尔可夫决策过程（CMDP）重新表述为**Wasserstein变分优化**问题，利用增广概率图模型（PGM）作为基础推理框架，提出**自适应切片Wasserstein变分优化（AWaVO）**。
- **关键技术细节**：
  - **Wasserstein变分推理（WVI）**：使用自适应广义切片Wasserstein距离（A-GSWD）替代KL散度，处理动态不确定性。A-GSWD通过ORPO-DR自适应确定超曲面切片方向，提升分布距离计算的精度和效率。
  - **最优性纠正策略优化与分布表示（ORPO-DR）**：基于分布表示（整个动作值函数的分布）进行策略更新，提供收敛过程的透明度。策略更新分为两种情况：若约束满足，则最大化奖励似然；否则最小化约束似然。
  - **形式化可解释性证明**：
    - 证明A-GSWD满足伪度量性质（非负、对称、三角不等式）。
    - 证明全局收敛性：当且仅当奖励算子族F满足单调性条件时，策略序列单调收敛到最优。
    - 证明全局收敛率$\Theta(1/\sqrt{T})$，且约束违反时具有次线性率$\Theta(1/\sqrt{T})$。
    - 提供概率化决策解释：通过链式法则分解后验概率$p(\tau|D)$，量化潜在因素（如外部力、障碍物）对轨迹的影响。

## 3. 实验设计
- **数据集/场景**：
  - 模拟环境：OpenAI Gym（Acrobot、Cartpole）、GUARD基准（Walker、Drone）。
  - 真实环境：四旋翼飞行器（三个飞行任务：FT1无障碍追踪、FT2密集障碍物追踪、FT3外力+密集障碍物追踪）。
- **对比基准方法**：
  - 模拟任务：PaETS（贝叶斯RL）、TRPO-IPO、PCPO、CRPO（原始约束RL方法）。
  - 真实任务：主要与PCPO对比。
- **评估指标**：平均奖励、约束满足程度、收敛速度、决策概率解释等。

## 4. 资源与算力
- 论文**未明确说明**所使用的GPU型号、数量、训练时长等算力信息。仅提到实验在“适当”的硬件上运行，但未提供具体细节。

## 5. 实验数量与充分性
- **实验数量**：
  - 模拟任务：4个不同环境（Acrobot、Cartpole、Walker、Drone），每个重复10次随机种子。
  - 真实任务：3种飞行场景，每种场景进行对比。
  - 消融分析：未显式设计消融实验，但通过对比A-GSWD与SWD/GSWD、以及与传统KL散度，间接验证了A-GSWD的有效性。
- **充分性与公平性**：
  - 实验设计较为充分：覆盖多类型环境（离散/连续、简单/复杂）、包含真实机器人验证，对比方法均为近年SOTA。
  - 公平性：参数设置基于基准（CRPO、GUARD），但对超参数进行了适当调整。未进行严格的超参数敏感性分析，但给出了收敛率证明。

## 6. 论文的主要结论与发现
- AWaVO在模拟和真实任务中均实现了合理的**性能-可解释性权衡**，虽然CRPO在某些任务中性能略优，但AWaVO提供了更强的可解释性。
- 从形式化角度证明了全局收敛率$\Theta(1/\sqrt{T})$，并通过实验验证了收敛速率落在$\Theta(1/\sqrt{T})$到$\Theta(1/T^{1.2})$之间。
- 通过概率化决策解释（$p(\tau|L)$），首次在四旋翼飞行任务中量化了外部力、障碍物等潜在因素对轨迹决策的影响程度，为安全关键领域提供了可操作的分析工具。

## 7. 优点
- **理论贡献**：首次将约束RL与概率推理、Wasserstein距离、形式化方法结合，提供了三个关键挑战的完整可解释性保证（收敛性、透明性、决策解释）。
- **方法创新**：A-GSWD自适应切片策略避免了手动选择超曲面参数，提高了距离计算精度；ORPO-DR使用分布表示增强了训练透明度。
- **实验验证**：涵盖模拟到真实机器人，验证了实际部署可行性；并提供了直观的概率解释图，提升了实际可用性。

## 8. 不足与局限
- **可扩展性限制**：论文通过Lorenz 96系统初步测试了可扩展性（最多1000状态），但未在更大规模真实RL问题（如高维视觉任务）中验证。作者承认需要进一步研究可扩展性。
- **后验概率置信度**：critic网络作为贝叶斯网络，其后验概率的置信区间未建立，作者提到是正在进行的工作。
- **人类中心验证缺失**：缺乏用户研究来评估人类对概率解释的理解程度；也未涉及政策与伦理问题。
- **超参数敏感性**：虽然给出了理论收敛率，但实际性能对学习率、网络宽度等超参数较敏感，未提供鲁棒性分析。
- **消融实验不充分**：对比方法未系统消融A-GSWD与ORPO-DR各自贡献，存在一定程度的效果耦合。

（完）
