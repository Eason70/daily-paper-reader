---
title: "Safe and Efficient: A Primal-Dual Method for Offline Convex CMDPs under Partial Data Coverage"
title_zh: 安全高效：部分数据覆盖下的离线凸CMDP原对偶方法
authors: "Haobo Zhang, Xiyue Peng, Honghao Wei, Xin Liu"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=UuiZEOVtHx"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 面向凸约束马尔可夫决策过程的离线安全强化学习，原对偶方法
tldr: 离线安全强化学习通常需要强数据覆盖假设。本文针对凸CMDP提出基于线性规划的原对偶算法，引入不确定性参数以放宽覆盖要求。理论上样本复杂度达到最优，并改进了一个因子。实验验证了理论结果，展示了在部分覆盖下仍能学习安全策略。该工作提升了离线安全RL的数据效率。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-uuizeovthx/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 571, \"height\": 281, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-uuizeovthx/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1437, \"height\": 334, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-uuizeovthx/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1452, \"height\": 359, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-uuizeovthx/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1465, \"height\": 438, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-uuizeovthx/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1449, \"height\": 311, \"label\": \"Table\"}]"
motivation: 降低离线安全强化学习对数据覆盖的严格要求。
method: 基于线性规划的原对偶算法，引入不确定性参数处理部分数据覆盖。
result: 样本复杂度达到当前最优，且数值实验验证了有效性。
conclusion: 为离线安全强化学习在数据有限场景下的应用提供了高效方案。
---

## Abstract
Offline safe reinforcement learning (RL) aims to find an optimal policy using a pre-collected dataset when data collection is impractical or risky. We propose a novel linear programming (LP) based primal-dual algorithm for convex MDPs that incorporates ``uncertainty'' parameters to improve data efficiency while requiring only partial data coverage assumption. Our theoretical results achieve a sample complexity of $\mathcal{O}(1/(1-\gamma)\sqrt{n})$ under general function approximation, improving the current state-of-the-art by a factor of $1/(1-\gamma)$, where $n$ is the number of data samples in an offline dataset, and $\gamma$ is the discount factor. The numerical experiments validate our theoretical findings, demonstrating the practical efficacy of our approach in achieving improved safety and learning efficiency in safe offline settings.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题定义**：离线安全强化学习（Offline Safe RL）旨在从预先收集的静态数据集中学习一个策略，在最大化累积奖励的同时满足多个安全性约束。这类问题在实际应用中广泛存在，如自动驾驶、机器人、医疗等。
- **现有挑战**：
  - 传统离线RL通常需要全数据覆盖假设（即数据集覆盖所有策略诱导的状态-动作分布），这在安全场景中极其不现实，因为要求数据集涵盖所有危险策略访问的状态-动作对，代价高昂且危险。
  - 现有离线安全RL工作（如CoptiDICE、DPDL、MBCL、PDCA）均需全覆盖或强覆盖假设，且样本复杂度欠佳。
  - 凸MDP（Convex MDP）问题目标函数为凸（或凹）效用函数，而非标准RL的线性累积奖励，导致贝尔曼方程失效，传统动态规划方法不可用，理论研究薄弱。
- **本文贡献**：
  - 首次研究离线凸MDP在安全约束下的问题，并仅需部分数据覆盖假设（π*–concentrability）。
  - 提出基于线性规划（LP）的原对偶算法，引入“不确定性”参数（ζ, κ）处理分布偏移和安全不确定，提升数据效率。
  - 理论上证明在通用函数近似下样本复杂度达到$\mathcal{O}(1/(1-\gamma)\sqrt{n})$，相较现有最优结果改进了一个因子$1/(1-\gamma)$。
  - 实验验证算法在模仿学习和标准CMDP任务中的有效性，即使在完全随机且违反安全的数据集上也能表现良好。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

- **核心思想**：
  - 将凸CMDP问题重新表述为关于边际重要性权重（Marginalized Importance Weight, MIW）的等价形式，避免贝尔曼方程失效问题。
  - 利用离线数据集构建经验版本的问题，并引入松弛参数（ζ, κ）以抵消“不确定性”，这些参数的控制与样本大小呈$\mathcal{O}(1/\sqrt{n})$关系。
  - 采用原对偶方法迭代求解拉格朗日函数，保证算法计算高效且可扩展。
- **关键技术细节**：
  - **问题形式化**：原始问题为$\min_{d_\pi \in \mathcal{K}} f(d_\pi)$ s.t. $g(d_\pi) \le \tau$，其中$\mathcal{K}$为满足全局平衡方程的占比测度集。通过MIW $w(s,a)=d(s,a)/\mu(s,a)$转化为$\min_{w\ge 0} f(\mu\cdot w)$ s.t. $Kw = (1-\gamma)\mu_0$, $g(\mu\cdot w)\le \tau$。
  - **经验松弛问题**：使用数据经验分布$\mu_D$和$K_D$代替真实分布，加入松弛约束：$\|K_D w - (1-\gamma)\mu_0\|_1 \le \zeta$, $g(\mu_D \cdot w) - \tau \le \kappa$。
  - **拉格朗日函数**：$L(w, \lambda, \phi) = f(\mu_D \cdot w) + \lambda(\|K_D w - (1-\gamma)\mu_0\|_1 - \zeta) + \phi(g(\mu_D \cdot w) - \tau - \kappa)$。
  - **算法流程（POCC，Algorithm 1）**：
    1. 输入离线数据集，给定松弛参数ζ, κ，步长η=1/√K。
    2. 初始化w₁∈W，拉格朗日乘子λ₁=0, ϕ₁=0。
    3. 对k=1,...,K迭代：
       - 原始更新：$w_{k+1} = \mathcal{P}_\mathcal{W}(w_k - \eta \nabla_w L(w_k, \lambda_k, \phi_k))$。
       - 对偶更新：$\phi_{k+1} = [\tau_k - \eta \nabla_\phi L(w_k, \lambda_k, \phi_k)]_{\max 0}^{\phi_{k+1}}$，λ类似。
    4. 计算平均权重$\bar{w}_K$，根据公式(12)提取策略$\pi_K$。
  - **理论分析**：通过分解目标与约束违反为三项（I: 归一化误差、II: 经验近似误差、III: 原对偶收敛误差），分别利用集中不等式（Hoeffding）、李普希兹连续性和原对偶收敛定理给出界，得到最终样本复杂度。
- **关键假设**：π*–concentrability（部分覆盖）、可实现性（w*∈W）、完备性、有界性、李普希兹连续性及Slater条件。

## 3. 实验设计：数据集/场景、benchmark、对比方法

- **场景一：安全模仿学习（Safe Imitation Learning）**
  - **环境**：迷宫环境（修改自Geist et al. 2022），有4个动作（上下左右），墙壁和边界不改变状态，目标是通过专家演示学习策略，同时避免不安全状态。
  - **数据集**：专家演示，但随机移除25%的状态，造成数据不完整。
  - **任务**：最小化与专家分布的KL散度，同时满足成本约束（成本阈值为0）。
  - **对比**：未明确列出其他方法，主要展示算法在有无安全约束下的效果，对比不使用安全约束的情况。
- **场景二：标准离线CMDP（FrozenLake 8×8）**
  - **环境**：8×8网格世界，初始位置左上角，目标到达右下角避开洞（hole）。落入洞会获得成本1，到达目标获得奖励1，25步后终止。折扣因子γ=0.99。
  - **数据集**：由不同比例的随机策略和最优策略混合生成，运行200条轨迹（每条最多50步）。行为策略比例p∈{0.75, 0.5, 0.25, 0}（0表示完全随机）。
  - **对比方法**：COptiDICE（Lee et al. 2021），该方法是离线安全RL的经典基线。
  - **评价指标**：累积奖励和累积成本。
- **额外实验（连续环境）**：在SafetyGym（Liu et al. 2023a）上测试，包括AntRun、CarRun、BallRun、BallCircle、CarPush1五个任务。对比方法包括COptiDICE、CPQ、BEAR-Lagrangian、PDCA。成本阈值设为1，报告归一化奖励和成本。

## 4. 资源与算力

- 论文在“Compute setting”部分明确说明：使用NVIDIA GeForce RTX 3080 Ti 8-Core Processor（应为8核CPU，但GPU为RTX 3080 Ti）。未提及具体训练时长或GPU数量，也未说明总计算消耗。因此，算力信息部分详细，但未提供完整训练时间对比。

## 5. 实验数量与充分性

- **模仿学习实验**：一组迷宫环境，两种条件（有/无安全约束），展示了策略的occupancy measure热力图。未做重复实验或消融，但直观说明算法能复现专家分布并规避不安全区域。
- **FrozenLake实验**：采用四种行为策略比例（p=0.75,0.5,0.25,0）分别在200个训练步内观察奖励与成本；另外对不同数据集大小（约10²~10⁴）测试，每个点平均10次独立运行。实验数量较充分，覆盖不同数据质量与规模，且与COptiDICE对比。
- **SafetyGym实验**：5个任务，每种方法3个随机种子，每种子20个评估episode，结果为平均值。对比了4种基线方法。
- **充分性评估**：实验覆盖了部分覆盖假设（随机数据）和不同数据量，验证了理论优势。但缺乏对松弛参数ζ, κ的敏感性分析、不同函数逼近器（如神经网络结构）的消融、以及更多复杂环境（如高维连续控制任务）的测试。整体实验设计合理，但规模中等，足以支撑主要结论。

## 6. 论文的主要结论与发现

- **理论结果**：在π*–concentrability假设下，所提算法POCC在目标最优性和约束违反上均达到$\mathcal{O}(\frac{1}{(1-\gamma)\sqrt{n}} + \frac{1}{\sqrt{K}})$的样本复杂度。当迭代数K≥n时，收敛率为$\mathcal{O}(1/(1-\gamma)\sqrt{n})$，改进了现有最优结果一个因子$1/(1-\gamma)$。
- **实验结论**：
  - 在模仿学习中，算法能在25%状态缺失的情况下恢复专家分布，并在安全约束下避开危险区域（右上角）。
  - 在FrozenLake中，即使行为策略完全随机（p=0），算法仍能学到安全且最优的策略；而COptiDICE在随机数据下表现差（高成本或低奖励）。
  - 随数据集增大，算法性能稳定提升，方差低；COptiDICE在中等数据集下表现不稳定。
  - SafetyGym连续环境中，算法在多数任务中能同时满足成本约束（成本接近或低于阈值）且获得合理奖励，尤其AntRun任务中以低成本获得最高奖励。
- **总体发现**：部分覆盖假设在离线安全RL中是可行且实用的，借助不确定性松弛和原对偶算法，即使数据质量差（完全随机），也能学习安全策略。

## 7. 优点

- **理论创新**：首次在离线凸MDP和安全性约束下建立通用函数近似的样本复杂度，且仅需部分覆盖假设，实用性强；样本复杂度达到当前最优。
- **算法设计**：基于MIW的方法规避了贝尔曼方程失效问题，利用原对偶迭代可扩展至大状态-动作空间，无需求解复杂凸优化问题。
- **实验验证**：覆盖简单（离散）和复杂（连续）环境，对比基线包括最新方法（PDCA、CoptiDICE等），结果清晰展示算法在低质量数据下的鲁棒性。
- **代码开源**：论文承诺提供代码和数据，增强可重复性。
- **界限清晰**：理论证明中通过三项分解和集中不等式提供完整的概率界，假设合理且明确说明。

## 8. 不足与局限

- **假设限制**：
  - 要求函数类W和X满足可实现性和完备性，这在实践中不一定容易满足（尤其高维连续空间）。
  - Slater条件（存在严格可行的解）用于控制对偶变量界，若无此条件，原对偶方法的收敛性可能退化。
  - 部分覆盖假设仍需要行为策略覆盖最优策略的支撑，若最优策略访问稀疏状态，仍需一定探索。
- **实验范围**：
  - 离散实验只使用FrozenLake和简单迷宫，缺乏更复杂离散任务（如Atari）的测试。
  - 连续环境任务（SafetyGym）相对简单（低维动作空间），未在高维机器人任务（如Ant、Humanoid）中充分验证。
  - 未进行超参数敏感性分析（如ζ, κ的选取影响），仅在实验中固定为经验值。
- **实用性问题**：
  - 提取策略公式(12)假设已知或可估计行为策略πμ，文中使用行为克隆估计，但估计误差可能影响最终策略。
  - 算法需要K次迭代，K≥n时才能达到理论最优率，在大数据集上计算成本可能较高。
- **未提及内容**：
  - 未讨论奖励与成本之间的权衡（如成本阈值选择对性能的影响）。
  - 未对安全约束违规进行事后分析（如平均违规 vs. 最坏情况违规）。
  - 未与基于模型的离线安全RL方法对比。

**（完）**
