---
title: An Optimistic Algorithm for online CMDPS with Anytime Adversarial Constraints
title_zh: 一种针对在线CMDP的乐观算法：任意时刻对抗约束
authors: "Jiahui Zhu, Kihyun Yu, Dabeen Lee, Xin Liu, Honghao Wei"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=fFgiXamW8E"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 乐观镜像下降原对偶算法用于在线安全RL对抗约束
tldr: 本文针对在线安全强化学习在对抗性、时变约束下的挑战，提出乐观镜像下降原对偶（OMDPD）算法，首次实现在任意时刻对抗约束下具有最优遗憾界。理论证明其遗憾与约束违反均达到最优，实验验证了在自动驾驶等动态环境中的有效性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-ffgixamw8e/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1407, \"height\": 547, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ffgixamw8e/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 848, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ffgixamw8e/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1322, \"height\": 516, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ffgixamw8e/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1748, \"height\": 370, \"label\": \"Table\"}]"
motivation: 现有在线CMDP方法无法处理对抗性时变约束。
method: 提出OMDPD，结合乐观镜像下降和原始-对偶框架。
result: 在对抗性约束下实现最优遗憾和强约束违反保证。
conclusion: 为在线安全RL在对抗环境中提供了理论完善且实用的算法。
---

## Abstract
Online safe reinforcement learning (RL) plays a key role in dynamic environments, with applications in autonomous driving, robotics, and cybersecurity. The objective is to learn optimal policies that maximize rewards while satisfying safety constraints modeled by constrained Markov decision processes (CMDPs). Existing methods achieve sublinear regret under stochastic constraints but often fail in adversarial settings, where constraints are unknown, time-varying, and potentially adversarially designed. In this paper, we propose the Optimistic Mirror Descent Primal-Dual (OMDPD) algorithm, the first to address online CMDPs with anytime adversarial constraints. OMDPD achieves optimal regret $\tilde{\mathcal{O}}(\sqrt{K})$ and strong constraint violation $\tilde{\mathcal{O}}(\sqrt{K})$ without relying on Slater’s condition or the existence of a strictly known safe policy. We further show that access to accurate estimates of rewards and transitions can further improve these bounds. Our results offer practical guarantees for safe decision-making in adversarial environments.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：在线安全强化学习（Safe RL）要求智能体在最大化累积奖励的同时满足安全约束，通常建模为约束马尔可夫决策过程（CMDP）。在自动驾驶、机器人、网络安全等动态环境中，约束条件可能是未知、时变甚至对抗性设计的。现有方法在处理随机约束时取得了次线性遗憾，但在对抗性约束下失效——它们通常需要Slater条件（严格可行策略的存在）或已知安全策略，且允许错误抵消的弱约束违反度量。
- **整体含义**：本文首次针对“任意时刻对抗约束”（adversarial constraints）的在线CMDP问题，提出**乐观镜像下降原对偶（OMDPD）**算法，在不依赖Slater条件或已知安全策略的前提下，同时实现最优的遗憾界 $\tilde{O}(\sqrt{K})$ 和硬约束违反界 $\tilde{O}(\sqrt{K})$（不允许错误抵消）。这为对抗性环境下的安全决策提供了理论完善且实用的算法。

## 2. 方法创新与关键技术细节（核心思想与算法流程）

- **核心思想**：结合乐观估计（optimistic estimation）、在线镜像下降（Online Mirror Descent, OMD）和原始-对偶（Primal-Dual）框架，利用指数势Lyapunov函数 $\Phi(x)=\exp(\beta x)-1$ 动态跟踪约束违反，从而自适应调整对违反的惩罚，避免依赖Slater条件。
- **关键技术细节**：
  - **乐观估计**：基于历史数据构造置信区间，得到乐观奖励 $\tilde{r}_k$、乐观成本 $\tilde{d}_k$ 以及转移核的候选集 $B_k$，确保真实模型以高概率被包含。
  - **替代目标函数**：每轮求解最大化问题：$\max_{q\in Q_k, d_k^\top q \le 0} r_k^\top q$，但用替代函数 $f_k(q) = \alpha(-\tilde{r}_k^\top q + \Phi'(\lambda_k)[\tilde{d}_k^\top q]_+) - \frac12\|q - q_k\|^2$ 进行近似，其中 $\lambda_k$ 是累积违反的原始变量。
  - **乐观OMD**：分两步：先根据当前梯度信息构造“乐观占用量” $\hat{q}_{k+1}$，再基于预测梯度更新真正的占用量 $q_{k+1}$。学习率自适应于梯度变化的累积。
  - **原始-对偶更新**：$\lambda_{k+1} = \lambda_k + \alpha[\tilde{d}_k^\top q_k]_+$（随机成本）或 $\lambda_{k+1} = \lambda_k + \alpha[d_k^\top q_k]_+$（对抗成本），仅记录正违反。
- **算法流程文字说明**：
  1. 初始化占用量 $q_1,\hat{q}_1$，参数 $\alpha,\beta$，设定初始估计为零。
  2. 对每个 episode $k=1,\dots,K$：
     - 用乐观OMD计算 $\hat{q}_{k+1}$ 和 $q_{k+1}$。
     - 从 $q_{k+1}$ 重构策略 $\pi_{k+1}$ 并执行。
     - 获取（估计）奖励、成本（对抗下全成本向量 $d_k$ 被揭露）并更新估计 $\tilde{r}_{k+1},\tilde{d}_{k+1}$。
     - 更新 $\lambda_{k+1}$，更新候选集 $Q_{k+1}$。
  3. 返回最终策略 $\pi_{K+1}$。

## 3. 实验设计：数据集/场景、基准方法与对比方法

- **实验场景**：使用一个合成的有限时间CMDP环境：状态空间 $S=\{0,1,2,3,4\}$（5个离散状态），动作空间 $A=\{0,1,2\}$（3个动作），回合长度 $H=5$。奖励和成本在随机设置中服从均匀分布；在对抗设置中，成本从 $\{-1.0,-0.6,-0.2,0,0.2,0.6,1.0\}$ 中随机抽取。转移核由狄利克雷分布（浓度参数 $\alpha=0.5$）生成，导致部分确定性行为。累积成本约束阈值为0。
- **基准方法**：文中未提供传统的baseline对比，因为本文宣称是第一个处理对抗性约束的方法。表1中列出了多篇现有工作的理论对比，但实验部分仅展示了OMDPD自身的性能曲线。
- **对比方法**：无（仅展示OMDPD在随机和对抗设置下的累积违反）。
- **数据集**：合成生成，无真实数据集。

## 4. 资源与算力

- 文中**未提及**所使用的GPU型号、数量、训练时长等算力信息。仅提及仿真环境在某个计算平台上运行（未具体说明）。

## 5. 实验数量与充分性

- **实验数量**：仅有一组实验（Figure 2），显示在K=3000 episodes下，随机和对抗两种设置下的累积约束违反曲线。
- **充分性评价**：实验设计较为薄弱。仅展示了算法自身违反的次线性增长，没有：
  - 与任何现有算法（即使是随机约束下的算法）进行定量比较。
  - 消融实验（如验证不同 $\alpha,\beta$ 选择、不同Lyapunov函数、不同乐观参数的影响）。
  - 在更大或更复杂环境（如自动驾驶或机器人仿真）上的验证。
  - 统计显著性分析（如多次运行的平均和方差）。
- **客观性与公平性**：由于缺乏对比基准，无法评估相对性能。实验仅用于说明理论界的可实现性，具有局限性。

## 6. 主要结论与发现

- OMDPD算法在对抗性成本函数下首次实现了 $\tilde{O}(\sqrt{K})$ 的最优遗憾和硬约束违反界，且不依赖Slater条件或已知安全策略。
- 当奖励固定、且有生成模型可准确估计奖励和转移核时，遗憾界可进一步降至 $O(1)$。
- 仿真实验验证了约束违反随episode数增长呈次线性（符合 $\tilde{O}(\sqrt{K})$ 趋势），表明算法在对抗性约束下能够保持安全。

## 7. 优点

- **理论贡献突出**：去除了常见假设（Slater条件、已知安全策略），首次解决对抗性约束下的在线CMDP，遗憾和违反界均达到最优（关于K）。
- **算法统一性强**：单框架同时处理随机和对抗成本，无需预知是哪一种。
- **方法创新**：结合乐观估计、乐观OMD和指数势Lyapunov函数，利用梯度变化自适应调整学习率，使得迭代效率更高，且推导出当奖励固定时可获得常数界。
- **分析严谨**：提供完整的理论证明及证明路线图（Figure 1），对估计误差和优化误差进行独立分析。

## 8. 不足与局限

- **实验覆盖不足**：仅在一个极简单的合成环境（$S=5$，$A=3$，$H=5$）上进行验证，缺少真实场景或复杂动力学环境的测试。未与其他算法（即使是处理随机约束的算法）进行对比，无法体现实际性能优势。
- **未讨论偏差风险**：乐观估计可能过于乐观，导致早期高风险，文中未分析失败概率或调整置信水平的实际影响。
- **应用限制**：算法要求能够构造置信区间并求解占用量线性规划，在大状态/动作空间下计算复杂度高。对抗成本需要全成本向量被揭露，这在某些在线场景中不现实（如仅观测到触碰约束时的成本）。
- **未报告算力与超参数敏感度**：缺少关于超参数 $\alpha,\beta$ 以及学习率 $\eta_k$ 对性能的影响分析。
- **未进行消融实验**：无法判断各个组件（乐观估计、OMD、指数势）的独立贡献。

（完）
