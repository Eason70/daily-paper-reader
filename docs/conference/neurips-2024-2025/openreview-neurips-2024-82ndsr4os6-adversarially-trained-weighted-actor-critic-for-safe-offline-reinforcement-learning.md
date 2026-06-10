---
title: Adversarially Trained Weighted Actor-Critic for Safe Offline Reinforcement Learning
title_zh: 对抗训练加权演员-评论家用于安全离线强化学习
authors: "Honghao Wei, Xiyue Peng, Arnob Ghosh, Xin Liu"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=82Ndsr4OS6"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 加权安全演员-评论家用于离线安全强化学习，采用对抗训练
tldr: 离线安全强化学习面临数据覆盖有限和策略改进鲁棒性的挑战。本文提出WSAC算法，设计为两玩家Stackelberg博弈，演员策略对抗两个重要性加权贝尔曼误差的评论家，聚焦于策略劣势场景。理论证明使用无遗憾优化可实现首个安全离线RL的全面保证，实验验证了其有效性。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-82ndsr4os6/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 658, \"height\": 381, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-82ndsr4os6/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1163, \"height\": 296, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-82ndsr4os6/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1218, \"height\": 1691, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-82ndsr4os6/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1321, \"height\": 388, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-82ndsr4os6/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1450, \"height\": 741, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-82ndsr4os6/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1443, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-82ndsr4os6/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1124, \"height\": 476, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-82ndsr4os6/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1086, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-82ndsr4os6/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1441, \"height\": 240, \"label\": \"Table\"}]"
motivation: 离线安全强化学习数据覆盖有限，策略优化鲁棒性差。
method: 提出WSAC，基于两玩家Stackelberg博弈，对抗训练加权评论家。
result: 理论保证安全离线RL的首次全面结果，实验表现优异。
conclusion: WSAC为安全离线强化学习提供了鲁棒且可证明的方法。
---

## Abstract
We propose WSAC (Weighted Safe Actor-Critic), a novel algorithm for Safe Offline Reinforcement Learning (RL) under functional approximation, which can robustly optimize policies to improve upon an arbitrary reference policy with limited data coverage. WSAC is designed as a two-player Stackelberg game to optimize a refined objective function. The actor optimizes the policy against two adversarially trained value critics with small importance-weighted Bellman errors, which focus on scenarios where the actor's performance is inferior to the reference policy. In theory, we demonstrate that when the actor employs a no-regret optimization oracle, WSAC achieves a number of guarantees: $(i)$ For the first time in the safe offline  RL setting, we establish that WSAC can produce a policy that outperforms {\bf any} reference policy while maintaining the same level of safety, which is critical to designing a safe algorithm for offline RL. $(ii)$ WSAC achieves the optimal statistical convergence rate of $1/\sqrt{N}$ to the reference policy, where $N$ is the size of the offline dataset. $(iii)$ We theoretically show that WSAC guarantees a safe policy improvement across a broad range of hyperparameters that control the degree of pessimism, indicating its practical robustness. Additionally, we offer a practical version of WSAC and compare it with existing state-of-the-art safe offline RL algorithms in several continuous control environments. WSAC outperforms all baselines across a range of tasks, supporting the theoretical results.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：离线强化学习（Offline RL）在安全关键领域（如自动驾驶、机器人）中，要求从离线数据集学习既高效又安全的策略。但离线数据覆盖有限，现有安全离线RL算法大多依赖“所有策略集中性”（all-policy concentrability）这一不切实际的假设，且无法保证策略改进时安全性不退化。
- **核心问题**：如何在仅需弱数据覆盖假设（单策略 ℓ2 集中性）下，设计一种算法，使得学到的策略能在**任何参考策略**（包括行为策略）的基础上同时提升回报并维持相同安全水平，即实现**安全鲁棒策略改进（SRPI）**。
- **贡献**：本文首次在函数近似离线安全RL中提出满足SRPI的算法WSAC，并达到最优统计速率 \(1/\sqrt{N}\)，同时仅使用单策略 ℓ2 集中性。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：构建一个两玩家Stackelberg博弈。演员（actor）优化一个经过限制的目标函数，两个评论家（critic）分别通过对抗训练（adversarially trained）保证重要性加权的贝尔曼误差（importance-weighted Bellman error）小，从而聚焦于演员表现劣于参考策略的情形。
- **关键技术细节**：
  - 使用重要性权重函数类 \(\mathcal{W}\) 来衡量策略的状态-动作占用与数据分布之比，仅需**单策略 ℓ2 集中性**（即 \(w^\pi\) 的 ℓ2 范数有界，且 \(w^{\pi_{\text{ref}}} \in \mathcal{W}\)）。
  - 提出**aggression-limited 目标函数**：\(f_r(s_0, \pi) - \lambda \cdot [f_c(s_0, \pi)]_+\)，其中 \([ \cdot ]_+ = \max\{\cdot,0\}\)，通过选择足够大的 \(\lambda\) 惩罚不安全策略，避免传统对偶变量调优所需的全策略集中性。
  - 评论家训练：奖励评论家通过最小化 \(L_{\mathcal{D}}(\pi, f_r) + \beta E_{\mathcal{D}}(\pi, f_r)\) 获得最悲观的估计；成本评论家通过最小化 \(-\lambda L_{\mathcal{D}}(\pi, f_c) + \beta \hat{E}_{\mathcal{D}}(\pi, f_c)\) 获得最乐观的估计。其中 \(E_{\mathcal{D}}\) 和 \(\hat{E}_{\mathcal{D}}\) 是基于经验数据的加权贝尔曼误差。
  - 演员更新：使用**无遗憾策略优化预言机**（no-regret policy optimization oracle），输入函数 \(f_r^k(s,a) - \lambda [f_c^k(s,a) - f_c^k(s,\pi_{\text{ref}})]_+\) 来更新策略 \(\pi_{k+1}\)。
- **算法流程**（Algorithm 1）：
  1. 输入离线数据集 \(\mathcal{D}\)，超参数 \(\beta, \lambda\)，参考策略 \(\pi_{\text{ref}}\)。
  2. 对于 \(k=1,\dots,K\)：
     - 计算奖励评论家 \(f_r^k\)（步骤4）。
     - 计算成本评论家 \(f_c^k\)（步骤6）。
     - 通过无遗憾预言机更新策略 \(\pi_{k+1}\)（步骤7）。
  3. 输出均匀混合策略 \(\bar{\pi} = \text{Unif}(\pi_1, \dots, \pi_K)\)。
- **理论结果**：定理5.2表明，以高概率，WSAC输出的策略与任何满足集中性的参考策略相比，奖励差距和成本差距均被 \(O(\epsilon_{\text{stat}} + C_{\ell_2}^* \sqrt{\epsilon_1}) + \epsilon_{\text{opt}}\) 项控制，其中统计误差项 \(\epsilon_{\text{stat}} \propto 1/\sqrt{N}\)。定理5.6进一步证明对行为策略 \(\mu\) 的SRPI。

## 3. 实验设计：使用的数据集 / 场景，benchmark，对比方法
- **环境**：四个连续控制任务，来自Offline Safe RL Benchmark (Liu et al., 2023a)：**BallCircle**（球绕圆圈运动，边界安全）、**CarCircle**（汽车绕圈）、**PointButton**（点状机器人按正确按钮）、**PointPush**（推动箱子到目标）。
- **数据集**：由专家策略与环境交互收集的离线数据。
- **对比方法**：Behavior Cloning (BC)、Safe-BC、BCQL (Batch-Constrained Q-learning with Lagrangian PID)、BEARL (Bootstrapping Error Accumulation Reduction with Lagrangian PID)、CPQ (Constraints Penalized Q-learning)、COptiDICE (State-of-the-art offline safe RL)。

## 4. 资源与算力
- 论文在Appendix D.3中说明：所有实验使用 **NVIDIA GeForce RTX 3080 Ti** 和 **8核处理器**。未明确给出GPU数量、训练时长等详细信息。

## 5. 实验数量与充分性
- **主要结果**（表2）：在4个环境下报告归一化奖励和成本，每个结果基于20个评估片段和3个随机种子，显示WSAC在所有环境下均保证安全（归一化成本<1），平均奖励最高。
- **不同成本极限**（表4）：在BallCircle/CarCircle使用成本极限[10,20,40]，PointButton/PointPush使用[20,40,80]，WSAC仍保持安全性且性能最佳或相当。
- **消融研究**（表5）：在表格情境下分析三个组件（加权贝尔曼正则化、aggression-limited目标、无遗憾优化）的贡献，表明加权贝尔曼正则化对安全性贡献最大。
- **超参数敏感性**（图4）：展示不同 \(\beta, \lambda\) 设定下性能稳定。
- **充分性**：实验覆盖多个环境、多个基线、多个成本阈值，并进行了消融和敏感性分析，较为充分。结果客观，WSAC一致优于或持平最佳基线。

## 6. 论文的主要结论与发现
- **理论发现**：WSAC首次在离线安全RL中实现**安全鲁棒策略改进（SRPI）**，即学到的策略在回报和安全性上均不差于行为策略，且适用范围广（\(\beta \geq 0\)）。收敛速度达到最优 \(1/\sqrt{N}\)，且仅需**单策略 ℓ2 集中性**，远弱于此前所有工作的全策略或 ℓ∞ 集中性。
- **实验发现**：WSAC在所有测试环境中均能输出安全策略（成本低于阈值），平均奖励优于或等于所有基线；尤其在困难任务（如PointButton）中其他基线均不安全，唯WSAC保持安全。

## 7. 优点
- **理论创新**：首次在函数近似离线安全RL中证明SRPI，去除了全策略集中性的不合理假设。采用aggression-limited目标避免对偶变量调优，实现更简单的单级优化。
- **算法实用性**：提供了深度RL版本，采用两时间尺度Adam更新，代码随论文发布，易于复现。
- **实验全面**：覆盖多种连续控制任务，对比多种基线，消融和敏感性分析完整，验证了各组件作用。

## 8. 不足与局限
- **假设依赖**：需要参考策略（\(\pi_{\text{ref}}\)）的集中性假设（\(w^{\pi_{\text{ref}}} \in \mathcal{W}\)），若参考策略未知需行为克隆近似，可能引入误差（论文已讨论但未深入分析）。
- **实验覆盖**：仅在4个连续控制环境中验证，缺乏离散动作空间或更大规模（如高维视觉任务）的评估。
- **计算效率**：未报告训练时间、收敛步数等，可扩展性未知。
- **权重函数类简化**：实践中将 \(\mathcal{W}\) 取为 \(\{0, C_\infty\}\)，相当于使用常数权重，可能损失部分灵活性。
- **安全约束仅考虑单约束**：虽然提及可扩展到多约束，但未实验验证。

（完）
