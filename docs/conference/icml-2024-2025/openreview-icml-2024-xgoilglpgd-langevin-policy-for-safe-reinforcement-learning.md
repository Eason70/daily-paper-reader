---
title: Langevin Policy for Safe Reinforcement Learning
title_zh: 安全强化学习的朗之万策略
authors: "Fenghao Lei, Long Yang, Shiting Wen, Zhixiong Huang, Zhiwang Zhang, Chaoyi Pang"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=xgoilgLPGD"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 朗之万策略用于安全强化学习
tldr: 本文探索采样方法在安全强化学习中的应用，提出朗之万策略与Langevin Actor-Critic算法，通过连续时间朗之万动力学直接推断动作，替代传统参数化策略。该方法避免了优化方法的局部最优问题，在安全RL基准上取得了与先进方法相当的性能，并加速了策略推理过程。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-xgoilglpgd/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 844, \"height\": 271, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-xgoilglpgd/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1768, \"height\": 696, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-xgoilglpgd/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1767, \"height\": 708, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-xgoilglpgd/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1766, \"height\": 738, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-xgoilglpgd/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1762, \"height\": 352, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-xgoilglpgd/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1767, \"height\": 746, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-xgoilglpgd/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1684, \"height\": 700, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-xgoilglpgd/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1766, \"height\": 391, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-xgoilglpgd/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1765, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-xgoilglpgd/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 838, \"height\": 608, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-xgoilglpgd/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1525, \"height\": 905, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-xgoilglpgd/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1593, \"height\": 907, \"label\": \"Table\"}]"
motivation: 现有安全RL主要基于优化，采样方法潜力未充分探索。
method: 提出朗之万策略和LAC算法，利用朗之万动力学直接采样动作。
result: 在多个安全RL任务中达到竞争性能，并加速策略推理。
conclusion: 采样方法可成为安全RL的有效替代范式。
---

## Abstract
Optimization and sampling based algorithms are two branches of methods in machine learning, while existing safe reinforcement learning (RL) algorithms are mainly based on optimization, it is still unclear whether sampling based methods can lead to desirable performance with safe policy. This paper formulates the Langevin policy for safe RL, and proposes Langevin Actor-Critic (LAC) to accelerate the process of policy inference. Concretely, instead of parametric policy, the proposed Langevin policy provides a stochastic process that directly infers actions, which is the numerical solver to the Langevin dynamic of actions on the continuous time. Furthermore, to make Langevin policy practical on RL tasks, the proposed LAC accumulates the transitions induced by Langevin policy and reproduces them with a generator. Finally, extensive empirical results show the effectiveness and superiority of LAC on the MuJoCo-based and Safety Gym tasks.

---

## 论文详细总结（自动生成）

# 论文总结：Langevin Policy for Safe Reinforcement Learning

## 1. 论文的核心问题与整体含义

- **研究动机**：现有安全强化学习（Safe RL）方法主要基于优化（如 CPO、FOCOPS、CUP 等），而采样方法（如 MCMC）在 RL 中的潜力尚未被充分探索。本文旨在回答：采样方法能否在安全 RL 中取得理想性能？
- **整体含义**：提出基于朗之万动力学（Langevin Dynamics）的采样策略（Langevin Policy），并设计 Langevin Actor-Critic（LAC）算法，将安全 RL 的最优更新策略视为能量基模型，通过 MCMC 直接采样子动作，从而在避免参数化策略的局部最优问题的同时，在多个基准任务上达到竞争性表现。

## 2. 论文提出的方法论

### 核心思想
- 将安全约束策略优化（CPO）中理论推导出的最优更新策略（能量基模型）用朗之万 MCMC 进行采样，替代传统的参数化策略输出动作。
- 引入生成器（参数化策略 π_ϕ）来近似朗之万链的输出，加速策略推理。

### 关键技术细节
1. **Langevin Policy（算法 1）**：
   - 基于 CPO 的最优策略形式：  
     π†(a|s) ∝ π_ϕk(a|s) × exp((A_R - ν A_C)/λ)。
   - 改写为能量基模型：  
     π†(a|s) = (1/Z) exp(-E(s,a;ϕ))，其中 E = (ν Q_C - Q_R)/λ - log π_ϕk。
   - 通过朗之万迭代更新动作：  
     ã_i = ã_{i-1} - (η/2)∇_a E + √η z_i，初始动作 ã_0 来自 π_ϕ。
   - 理论保证（定理 3.1）：在能量函数强凸且梯度 Lipschitz 条件下，有限步后分布与目标分布的 KL 散度可任意小。

2. **LAC 算法（算法 2）**：
   - **生成器近似**：用参数化策略 π_ϕ 与环境交互，避免每次运行完整朗之万链。
   - **信息性初始化**：以 π_ϕ 的输出作为朗之万链的起点（而非无关分布），并用固定小步数 T（如 30~50）加速收敛。
   - **裁剪双 Q 学习**：对奖励 Q 取最小值，对成本 Q 取最大值，以减轻值函数估计偏差。
   - **更新规则**：
     - Actor：最大化负对数似然（heuristic loss）并可加入 KL 正则化。
     - Critic：通过 TD 误差更新，目标值使用朗之万策略生成的动作。
     - 对偶变量 ν：通过梯度下降更新 ν ← {ν - η(b - J_C)}_+，λ 固定。

## 3. 实验设计

- **场景与数据集**：
  - **MuJoCo 任务**：Velocity（Ant-v3, Swimmer-v3, Humanoid-v3）和 Circle（HumanoidCircle-v0）任务。
  - **Safety Gym 任务**：Goal 和 Button 任务，使用 Point 和 Car 两种机器人，Level 1 难度。
- **基准方法**：CPO, FOCOPS, CUP, PCPO, P3O, RESPO, PPO-L, TRPO-L。
- **评估指标**：平均奖励（越高越好）和平均成本（需低于预设阈值）。
- **设置**：MuJoCo 任务训练 2.5M 步，Safety Gym 任务训练 2.5M 步；每个实验多次运行（MuJoCo 10 次，Safety Gym 不少于 3 次），报告均值和标准差。

## 4. 资源与算力

- 论文未明确说明使用的 GPU 型号、数量或训练时长。
- 仅提及实验运行在 Intel Core i9-9900K CPU（8 核）上，未提及 GPU 加速。
- 因此，算力细节不透明，可能影响复现效率和资源需求评估。

## 5. 实验数量与充分性

- **主要实验**：共 8 个环境（4 个 MuJoCo + 4 个 Safety Gym），每个环境与多个基线对比，并给出学习曲线和数值表格。
- **消融实验**：在 PointGoal 和 CarGoal 上进行了：
  - 初始化方法（非信息性 vs 信息性），不同朗之万步数 T。
  - KL 正则化系数 β 的影响。
  - 不同 T 的敏感性分析（从 10 到 500）。
- **充分性评价**：实验覆盖了多种连续控制任务和最新的基线，消融实验较为全面。但缺乏在更高难度 Safety Gym 等级或真实世界场景的验证，且未提供统计显著性检验（如 t 检验）。

## 6. 论文的主要结论与发现

1. **性能优势**：LAC 在 MuJoCo 的 Humanoid-v3、HumanoidCircle-v0 和 Ant-v3 上获得最高奖励且满足成本约束；在 Safety Gym 的所有四个任务中，LAC 在满足约束的前提下获得了最高或接近最高的奖励。
2. **采样方法的可行性**：证明了基于朗之万采样的安全 RL 方法能够与优化方法竞争，甚至更优。
3. **设计有效性**：信息性初始化显著优于非信息性初始化，中等步长 T 即可取得良好性能；KL 正则化能提升稳定性但收益有限。

## 7. 优点

- **方法创新**：首次将朗之万 MCMC 引入安全 RL，拓展了采样范式的应用。
- **理论支撑**：给出了朗之万策略收敛到最优更新策略的 KL 散度上界。
- **实用设计**：通过生成器+信息性初始化+裁剪 Q 学习，解决了 MCMC 效率低和值函数偏差问题。
- **实验结果全面**：在多个连续控制任务上全面对比，消融实验充分，代码开源。

## 8. 不足与局限

- **生成器近似误差**：使用高斯策略作为生成器，可能限制表达能力，引入的误差未被量化分析。
- **超参数敏感**：λ 需要手动固定，T、β 等需调参；未见自动调优方案。
- **算力信息缺失**：未说明 GPU 使用情况，实验可重复性受影响。
- **场景覆盖有限**：仅涉及中等复杂度任务，未在更高难度 Safety Gym（Level2）或真实机器人上测试。
- **对比基线选择性**：未与最新的基于扩散模型的安全 RL 方法（如 FISOR）直接对比。
- **统计显著性**：未提供置信区间之外的统计检验，部分结果波动较大（如 Humanoid-v3 的 CUP 方差很大）。

（完）
