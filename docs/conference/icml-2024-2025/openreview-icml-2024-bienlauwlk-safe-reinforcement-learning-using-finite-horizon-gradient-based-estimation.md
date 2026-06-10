---
title: Safe Reinforcement Learning using Finite-Horizon Gradient-based Estimation
title_zh: 使用有限时域梯度估计的安全强化学习
authors: "Juntao Dai, Yaodong Yang, Qian Zheng, Gang Pan"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=BiENLaUwlK"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 基于有限时域梯度估计的安全强化学习
tldr: 该论文针对安全强化学习中有限时域非折扣约束的估计问题，提出基于梯度的估计方法（GBE），克服了传统优势估计在有限时域中的灾难性误差，理论分析和实验证明GBE能有效避免安全违规更新，是安全RL的重要进展。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 831, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 782, \"height\": 344, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1719, \"height\": 709, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 835, \"height\": 500, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 835, \"height\": 495, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 838, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 888, \"height\": 516, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1642, \"height\": 531, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1400, \"height\": 613, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 682, \"height\": 680, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1721, \"height\": 703, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1721, \"height\": 708, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1729, \"height\": 1191, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1515, \"height\": 333, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-bienlauwlk/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 699, \"height\": 684, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-bienlauwlk/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1736, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-bienlauwlk/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1759, \"height\": 770, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-bienlauwlk/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1730, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-bienlauwlk/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1732, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-bienlauwlk/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1074, \"height\": 705, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-bienlauwlk/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1641, \"height\": 831, \"label\": \"Table\"}]"
motivation: 解决安全强化学习中有限时域约束估计不准导致的安全违规。
method: 提出基于轨迹解析梯度的GBE方法。
result: 在多种任务中有效避免安全约束违反。
conclusion: 为深度安全RL提供了新的约束估计方法。
---

## Abstract
A key aspect of Safe Reinforcement Learning (Safe RL) involves estimating the constraint condition for the next policy, which is crucial for guiding the optimization of safe policy updates. However, the existing *Advantage-based Estimation* (ABE) method relies on the infinite-horizon discounted advantage function. This dependence leads to catastrophic errors in finite-horizon scenarios with non-discounted constraints, resulting in safety-violation updates. In response, we propose the first estimation method for finite-horizon non-discounted constraints in deep Safe RL, termed *Gradient-based Estimation* (GBE), which relies on the analytic gradient derived along trajectories. Our theoretical and empirical analyses demonstrate that GBE can effectively estimate constraint changes over a finite horizon. Constructing a surrogate optimization problem with GBE, we developed a novel Safe RL algorithm called *Constrained Gradient-based Policy Optimization* (CGPO). CGPO identifies feasible optimal policies by iteratively resolving sub-problems within trust regions. Our empirical results reveal that CGPO, unlike baseline algorithms, successfully estimates the constraint functions of subsequent policies, thereby ensuring the efficiency and feasibility of each update.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机和背景）
- **问题**：现有深度安全强化学习（Safe RL）算法普遍采用基于无限时域折扣优势函数的**优势估计（ABE）**方法来预测下一策略的约束值。然而，实际安全基准（如Safety-Gym）中的约束多为**有限时域非折扣累积和**（例如 \(\sum_{t=0}^{T-1} c_t \le b\)）。ABE在有限时域场景下会产生巨大误差（相对误差超过1.0），导致策略更新时发生安全违规，如图1所示。
- **意义**：需要一种专门针对有限时域非折扣约束的估计方法，以正确指引安全策略优化，确保每次更新的可行性和效率。

### 2. 方法论：核心思想、关键技术细节
- **核心思想**：利用环境的**可微分性**（如可微分物理引擎或World Model），沿轨迹反向传播计算**一阶梯度**，从而直接估计策略参数微小变化后目标函数和约束函数的变化。
- **关键技术细节**：
  - **梯度估计（GBE）**：对可微分函数 \(J_f(\theta)\)（包括奖励 \(J_R\) 和代价 \(J_C\)），在 \(\theta_0\) 处进行一阶泰勒展开：\(\hat{J}_f(\theta_0+\delta) = J_f(\theta_0) + \delta^\top \nabla_\theta J_f(\theta_0)\)。误差上界为 \(\frac{1}{2}\epsilon \|\delta\|_2^2\)，其中 \(\epsilon\) 是Hessian范数的最大值。
  - **替代子问题**：在第k次迭代，给定信任区域半径 \(\hat{\delta}\)，求解：
    \[
    \max_{\delta} \; g_k^\top \delta \quad \text{s.t.} \quad c_k + q_k^\top \delta \le 0,\; \delta^\top\delta \le \hat{\delta}
    \]
    其中 \(g_k=\nabla J_R(\theta_k), q_k=\nabla J_C(\theta_k), c_k=J_C(\theta_k)-b\)。
  - **三种更新情景**：
    - 整个信任区域不可行（\(c_k>0\) 且距离阈值大于半径）：沿约束梯度负方向更新。
    - 整个信任区域可行（\(c_k\le 0\) 且距离阈值大于半径）：沿目标梯度正方向更新。
    - 部分相交：通过KKT条件求解，得到解析解 \(\delta = (g_k - \nu q_k)/\lambda\)，其中\(\lambda,\nu\)为最优对偶变量。
  - **自适应信任区域半径**：根据实际与估计的误差调整 \(\hat{\delta}\)，以避免过大的估计误差。
  - **实际实现**：基于SHAC（Short-Horizon Actor-Critic）方法，结合值函数 \(V_R, V_C\) 将轨迹切分为短窗口，通过BPTT计算梯度。

### 3. 实验设计：数据集/场景、benchmark、对比方法
- **场景与数据集**：基于可微分物理引擎Brax构建了**四个不同的安全RL任务**：
  - CartPole（位置约束）、Reacher（位置约束）、HalfCheetah（速度约束）、Ant（速度约束）。
  - 每个任务均保持环境可微分。
- **Benchmark**：没有使用已有的Safety-Gym等，因为要求可微分性；因此作者自己构建了可微分安全环境。
- **对比方法**：
  - 传统Safe RL方法：PDO, APPO, CPO, CUP。
  - 与可微分RL结合的Lagrangian方法：BPTT-Lag, SHAC-Lag。
  - 消融实验还比较了GBE vs ABE误差、ZoBG vs FoBG、自适应半径 vs 固定半径、World Model扩展（在非可微分任务上用MLP训练世界模型）。

### 4. 资源与算力
- **文中未明确说明**具体的GPU型号、数量、训练时长等算力信息。仅提到实验使用了5个随机种子，可能在中档GPU（如NVIDIA V100或类似）上运行，但无官方披露。

### 5. 实验数量与充分性
- **主要实验**：在4个任务上对比6种基线算法，每个任务5个随机种子，绘制学习曲线（图4），报告收敛步数（表1）和安全违规比例（表1）。
- **消融实验**：
  - GBE与ABE相对误差对比（图5），在简单函数环境和HalfCheetah上做100次重复。
  - 世界模型扩展实验（图6）：在非可微分FunctionEnv和Swimmer任务上测试。
  - 自适应信任区域半径分析（图7），以及超参数敏感性（附录D.2，5个子图）。
  - ZoBG vs FoBG对比（附录B，表2、3、图10）。
- **充分性与公平性**：
  - 对比方法种类多（传统+可微分+Lagrangian），覆盖主流方向。
  - 超参数设置详细，附录F给出了全部超参数（表4）。
  - 实验设计较为充分，消融研究深入。但任务数量偏少（仅4个），且所有任务都来自Brax同类控制域，泛化性证据有限。

### 6. 主要结论与发现
- GBE相比ABE能**更准确地估计有限时域非折扣约束**，相对误差在0.1以下，而ABE常超过1.0。
- 基于GBE的CGPO算法在**样本效率和约束满足**方面均显著优于所有基线：收敛所需环境步数减少28.8%~91.7%，安全违规比例降低至3.96%~14.29%（基线为5.96%~74.58%）。
- 自适应信任区域半径能够进一步提升性能和约束满足度。
- 通过World Model扩展，CGPO可以应用于非可微分环境（如Swimmer），展现一定泛化潜力。

### 7. 优点
- **理论贡献**：首次提出针对有限时域非折扣约束的梯度估计方法，并给出误差上界和最坏情况分析。
- **算法设计**：将信任区域与梯度估计结合，三种情景解析解清晰，且自适应半径策略实用。
- **实验设计**：自建可微分安全环境，对比方法全面，消融研究深入，验证了方法的必要性和有效性。
- **可拓展性**：支持通过World Model处理不可微分环境，为实际应用提供了可能路径。

### 8. 不足与局限
- **环境依赖**：GBE要求环境可微分或可训练World Model，限制了直接应用范围（如黑盒模拟器）。
- **系统误差**：在可微性差的系统中（如HalfCheetah中的冲击接触），梯度噪声增大，估计误差上升，即使自适应半径也可能降低更新效率。
- **实验覆盖**：仅测试了4个机器人控制任务，未涉及更复杂的安全场景（如自动驾驶、安全对齐等）。数据集规模有限。
- **资源信息缺失**：未报告GPU型号、训练时长等，不利于复现和公平比较。
- **World Model扩展**：用于非可微分任务的世界模型仅为简单MLP，梯度精度低，未来需更精确的模型（如高斯过程或概率模型）。
- **收敛性**：虽然提供了最坏情况界，但未在理论上证明整体收敛到最优可行策略。

（完）
