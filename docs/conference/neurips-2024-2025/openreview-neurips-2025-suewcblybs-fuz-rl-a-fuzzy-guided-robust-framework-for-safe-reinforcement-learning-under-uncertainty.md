---
title: "Fuz-RL: A Fuzzy-Guided Robust Framework for Safe Reinforcement Learning under Uncertainty"
title_zh: Fuz-RL：一种基于模糊引导的不确定性下安全强化学习鲁棒框架
authors: "Xu Wan, Chao Yang, Cheng Yang, Jie Song, Mingyang Sun"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=SuewCbLYBS"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 针对不确定性的安全强化学习框架
tldr: 安全强化学习在现实应用中面临多源不确定性挑战。本文提出Fuz-RL框架，采用模糊测度Choquet积分构建鲁棒Bellman算子，从理论上证明求解模糊RL问题等价于求解分布鲁棒CMDP问题。该方法提升了可解释风险和鲁棒决策能力，为安全RL提供了新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1441, \"height\": 664, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1448, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1439, \"height\": 646, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1422, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1452, \"height\": 365, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1382, \"height\": 797, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1449, \"height\": 672, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1446, \"height\": 681, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1448, \"height\": 669, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1449, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1446, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1441, \"height\": 676, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1449, \"height\": 531, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-suewcblybs/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1454, \"height\": 1704, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-suewcblybs/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1445, \"height\": 1038, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-suewcblybs/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1458, \"height\": 698, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-suewcblybs/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1393, \"height\": 695, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-suewcblybs/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1403, \"height\": 525, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-suewcblybs/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1299, \"height\": 184, \"label\": \"Table\"}]"
motivation: 现实环境的多源不确定性导致安全强化学习决策难以解释且鲁棒性不足。
method: 提出模糊测度引导的鲁棒框架，利用Choquet积分定义模糊Bellman算子进行值函数估计。
result: 理论上证明模糊RL与分布鲁棒CMDP等价，框架具有可解释性和鲁棒性。
conclusion: 为安全RL在不确定性环境下的应用提供了理论扎实且可解释的新方法。
---

## Abstract
Safe Reinforcement Learning (RL) is crucial for achieving high performance while ensuring safety in real-world applications. However, the complex interplay of multiple uncertainty sources in real environments poses significant challenges for interpretable risk assessment and robust decision-making. To address these challenges, we propose Fuz-RL, a fuzzy measure-guided robust framework for safe RL. 
Specifically, our framework develops a novel fuzzy Bellman operator for estimating robust value functions using Choquet integrals. Theoretically, we prove that solving the Fuz-RL problem (in Constrained Markov Decision Process (CMDP) form) is equivalent to solving distributionally robust safe RL problems (in robust CMDP form), effectively reformulating the min-max optimization problem into a tractable CMDP with Choquet-integrated value functions. Empirical analyses on safe-control-gym and safety-gymnasium scenarios demonstrate that Fuz-RL effectively integrates with existing safe RL baselines in a model-free manner, significantly improving both safety and control performance under various types of uncertainties in observation, action, and dynamics.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现实环境中的安全强化学习（Safe RL）受到多源不确定性（如传感器噪声、执行器延迟、环境动态变化）的耦合影响，导致现有方法在可解释的风险评估与鲁棒决策上面临挑战。
- **现有方法的不足**：
  - 传统 min-max 方法过于保守且计算困难；
  - 分布鲁棒方法通常假设不确定性独立，并采用 KL 散度或高斯扰动简化处理，忽略了多种不确定性相互作用时可能表现出的超加性效应；
  - 风险敏感方法（如 CVaR）需要精细调参，且难以同时处理多个噪声源。
- **整体含义**：该论文旨在将模糊测度理论引入安全 RL，通过 Choguet 积分建模不确定性的非加性影响，从而在无需求解复杂的 min-max 优化问题下实现可解释的鲁棒决策。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 核心思想
- 引入 **λ-模糊测度**（λ-fuzzy measure）来描述不同不确定性水平之间的相互作用（超加性或次加性），并用 **Choquet 积分** 对值函数进行鲁棒估计。
- 提出 **模糊 Bellman 算子**（fuzzy Bellman operator），将标准 Bellman 算子中的期望替换为基于 Choquet 积分的鲁棒期望，从而在值函数更新中自动编码最坏情况。

### 关键技术细节
- **模糊 Bellman 算子定义**：
  \[
  \mathcal{F}(V)(s) = \mathbb{E}_{a\sim\pi}\left[ r(s,a) + \gamma (C)\int_{\mathcal{P}_{as}} \mathbb{E}_{s'\sim p}[V(s')] \, dm(p) \right]
  \]
  其中 \(m\) 是凸 λ-模糊测度，(C)∫ 表示 Choquet 积分。

- **理论性质**：证明该算子满足 γ-收缩性（γ-contraction）并收敛到唯一不动点，从而保证值迭代的稳定性。

- **等价性定理**：证明求解模糊鲁棒 CMDP（式 7）等价于求解分布鲁棒 CMDP（式 3），将 min-max 问题转化为可解的带 Choquet 积分值的 CMDP。

- **实际实现（算法流程）**：
  1. **模糊密度网络**：用两层 MLP（softmax 激活）从状态 \(s\) 学习每个不确定性水平的密度 \(g_k\)，并钳制到 \([10^{-4}, 1-10^{-4}]\)。
  2. **求解 λ**：通过求解特征方程 \(\prod_{k=1}^K (1+\lambda g_k) = 1+\lambda\) 得到 λ（使用混合二分-牛顿法）。
  3. **计算模糊测度**：对任意子集 \(A\)，\(m(A) = \frac{\prod_{k\in A}(1+\lambda g_k)-1}{\lambda}\)。
  4. **分层扰动采样**：对每个不确定性水平 \(k\)，施加独立高斯扰动 \(\tilde{s}_k = s + \epsilon_k \cdot n_k\)，取 M=5 个样本平均得到值估计。
  5. **Choquet 积分近似**：对奖励值按降序排列，成本值按升序排列，用离散形式计算积分。
  6. **值网络更新**：使用带 Choquet 积分目标的时间差分学习更新 \(V_\theta^r\) 和 \(V_\theta^c\)。
  7. **策略更新**：采用原对偶（primal-dual）方法求解拉格朗日目标函数（式 18），与底层安全 RL 算法（如 PPO-Lagrange）集成。

## 3. 实验设计：使用的数据集/场景、benchmark、对比方法

- **测试场景**：
  - **Safe-Control-Gym**：Cartpole-Stab、Cartpole-Track、Quadrotor-Stab、Quadrotor-Track（共 4 个任务）。
  - **Safety-Gymnasium**：Safety-PointGoal1-v0、Safety-PointButton1-v0、Safety-PointCircle1-v0、Safety-PointPush1-v0（共 4 个任务）。
  - 额外在 **Double Integrator** 环境中进行对比分析。

- **不确定性设置**：
  - 观测不确定性：高斯白噪声，扰动强度 ε 从 -1 到 1 以 0.1 步长变化（Safe-Control-Gym）；Safety-Gymnasium 取 ε∈[0,0.5]。
  - 动作不确定性：脉冲噪声扰动（公式 19），幅度 ε∈[-0.1,0.1]。
  - 动力学不确定性：对动力学参数（如杆长、四旋翼质量）施加高斯扰动。
  - 多源不确定性：同时施加以上三种不确定性。

- **对比基线**：
  - 基础安全 RL 算法：PPO-Lagrangian (PPOL)、Conservative Update Policy (CUP)、CVaR-PPO (CPPO)。
  - 鲁棒安全 RL 算法：Risk-Averse Model Uncertainty (RAMU，使用 Wang transform)。
  - 对应的 Fuz-RL 变体：Fuz-PPOL、Fuz-CUP、Fuz-CPPO。

## 4. 资源与算力

论文在 NeurIPS 论文清单中声称提供了计算资源信息（附录 C.3），但**提取的文本中未包含具体内容**。根据清单回答，作者应已在附录中说明。从实验设置推断，实验可能使用单 GPU（如 NVIDIA V100 或类似）和 CPU 集群，但具体型号、数量、训练时长在提供的文本中未明确说明。建议参考原始论文附录获取详细信息。

## 5. 实验数量与充分性

- **实验数量**：
  - Safe-Control-Gym：4 个任务 × 3 种不确定性（观测、动作、动力学），共 12 组比较（每组含 4 个基线算法 + 3 个 Fuz 变体 + RAMU）。结果在表 1 和附录中报告，每组运行 10 episodes × 10 seeds。
  - Safety-Gymnasium：4 个任务，仅对比 PPOLag 和 Fuz-PPOLag（训练曲线和测试结果，图 1、图 2）。
  - 消融实验：针对不确定性级别 K（1, 5, 10, 15, 25）在三个控制任务上进行，结果如图 3。
  - 额外分析：在双积分器环境对比模糊算子与 min-max 算子（图 5、图 6）。
  - 电力系统任务（IEEE 39-bus）：表 4 对比 PPOL 和 Fuz-PPOL 在三种不确定性下的性能。

- **充分性评价**：
  - 实验覆盖了多种不确定性类型和组合，任务包括低维（Cartpole）到中高维（四旋翼、Safety-Gymnasium），以及一个实际场景（电网频率控制）。
  - 对比基线包括当前 SOTA 鲁棒安全 RL 方法（RAMU），消融实验探讨了关键超参数 K。
  - 统计上使用 10 个种子报告均值±标准差，具有较好的可重复性。
  - 但未在真实机器人上验证，且 Safety-Gymnasium 仅用了一个基线（PPOLag），缺乏对其他基线的 Fuz 变体（Fuz-CUP、Fuz-CPPO）的测试，可能不够全面。

## 6. 论文的主要结论与发现

- **Fuz-RL 显著提升鲁棒性**：在 Safe-Control-Gym 任务中，94.9% 的情况下 Fuz-RL 比对应基线降低平均风险（AvgRisk），88.9% 的任务提升平均回报（AvgRet）。例如 Fuz-CUP 相比 CUP 回报提升 61.4%，风险降低 16.7%。
- **优于现有鲁棒方法**：相比 RAMU，Fuz-RL 在 83.3% 的任务中获得更高回报，且在所有动作不确定性任务中表现更好；RAMU 虽在某些任务上风险更低，但以牺牲奖励为代价。
- **方差降低**：Fuz-RL 的 AvgRet 方差降低 20.7%（观测）、9.9%（动作）、8.6%（动力学）；AvgRisk 方差降低 13.2%、7.1%、22.6%。
- **最佳不确定性级别 K**：消融实验表明 K 取中间值（5~15）效果最优，K=1 风险过高，K=25 训练困难且回报下降。
- **理论贡献**：验证了模糊 Bellman 算子的 γ-收缩性、收敛性，以及 Fuz-RL 与分布鲁棒 CMDP 的等价性。

## 7. 优点：方法或实验设计上的亮点

- **方法创新**：首次将 λ-模糊测度与 Choquet 积分系统性地引入约束马尔可夫决策过程，提供了一种可解释且无需显式 min-max 优化的鲁棒机制。
- **理论严谨**：完整证明了模糊 Bellman 算子的收敛性与等价定理，为方法提供了坚实的数学基础。
- **即插即用**：Fuz-RL 可无缝集成到现有的安全 RL 算法中（如 PPOL、CUP、CPPO），只需修改值函数更新部分，无需改变策略优化框架。
- **实验全面**：涵盖多个基准环境（Safe-Control-Gym、Safety-Gymnasium、电力系统），多种不确定性类型（观测、动作、动力学）及其组合，并与当前最先进的鲁棒方法（RAMU）对比。
- **开源代码**：提供完整代码和配置，有利于复现和扩展。

## 8. 不足与局限

- **实验覆盖有限**：
  - Safety-Gymnasium 仅测试了 PPOLag 基线，缺少 Fuz-CUP 和 Fuz-CPPO 的对比，无法全面评估框架对不同算法的适应性。
  - 未在真实物理机器人或更复杂的高维任务（如自动驾驶、人形机器人）上验证，可扩展性存疑。
- **计算成本**：每步需要生成 K×M 个扰动样本并计算模糊测度，增加了训练时间（论文未报告具体开销）。
- **模糊测度选择**：仅使用 λ-模糊测度，未探索其他模糊测度（如可能性测度、必要性测度）的影响，可能忽略了更丰富的不确定性结构。
- **超参数敏感**：不确定性级别 K、基础扰动规模 ε_base、采样数 M 等需要人工设定，消融实验只针对 K，其他参数未系统分析。
- **偏差风险**：实验均在仿真环境中进行，真实环境的未建模噪声、延迟等可能使性能退化，缺乏 sim-to-real 讨论。
- **伦理与社会影响**：虽然论文在结论部分提及了潜在积极影响，但未讨论负面社会影响（如应用于自主武器系统等），也缺乏对算法安全使用边界的探讨。

（完）
