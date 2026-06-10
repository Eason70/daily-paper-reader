---
title: Dynamic Model Predictive Shielding for Provably Safe Reinforcement Learning
title_zh: 面向可证明安全强化学习的动态模型预测屏蔽
authors: "Arko Banerjee, Kia Rahmani, Joydeep Biswas, Isil Dillig"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=x2zY4hZcmg"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 具有动态屏蔽的可证明安全强化学习以兼顾任务进展
tldr: 模型预测屏蔽（MPS）虽能保证安全，但保守的任务无关备份策略常阻碍任务进展。本文提出动态模型预测屏蔽（DMPS），通过局部规划器动态选择安全恢复动作，兼顾短期进展和长期奖励，同时保持可证明安全。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-x2zy4hzcmg/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1387, \"height\": 265, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-x2zy4hzcmg/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 704, \"height\": 353, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-x2zy4hzcmg/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1452, \"height\": 337, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-x2zy4hzcmg/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1457, \"height\": 336, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-x2zy4hzcmg/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1361, \"height\": 427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-x2zy4hzcmg/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 873, \"height\": 651, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-x2zy4hzcmg/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1343, \"height\": 479, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-x2zy4hzcmg/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1473, \"height\": 489, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-x2zy4hzcmg/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1559, \"height\": 488, \"label\": \"Table\"}]"
motivation: 现有MPS方法使备份策略保守且忽视任务进展。
method: 引入动态局部规划器，在线选择最大化进展的安全恢复动作。
result: DMPS在保证安全的同时显著提升了任务效率。
conclusion: 为可证明安全RL提供了更有效的动态屏蔽机制。
---

## Abstract
Among approaches for provably safe reinforcement learning, Model Predictive Shielding (MPS) has proven effective at complex tasks in continuous, high-dimensional state spaces, by leveraging a *backup policy* to ensure safety when the learned policy attempts to take risky actions. However, while MPS can ensure safety both during and after training, it often hinders task progress due to the conservative and task-oblivious nature of backup policies.
This paper introduces *Dynamic Model Predictive Shielding* (DMPS), which optimizes reinforcement learning objectives while maintaining provable safety. DMPS employs a local planner to dynamically select safe recovery actions that maximize both short-term progress as well as long-term rewards. Crucially,  the planner and the neural policy  play a synergistic role in DMPS. When planning recovery actions for ensuring safety,  the planner utilizes the neural policy to estimate long-term rewards, allowing it to *observe* beyond its short-term planning horizon. 
Conversely, the neural policy under training learns from the recovery plans proposed by the planner, converging to policies that are both *high-performing* and *safe* in practice.
This approach guarantees safety during and after training, with bounded recovery regret that decreases exponentially with planning horizon depth. Experimental results demonstrate that DMPS converges to policies that rarely require shield interventions after training and achieve higher rewards compared to several state-of-the-art baselines.

---

## 论文详细总结（自动生成）

# 中文总结：动态模型预测屏蔽（DMPS）

## 1. 核心问题与整体含义（研究动机和背景）

- **背景**：可证明安全强化学习（Provably Safe RL, PSRL）追求在训练和部署中零安全违规。模型预测屏蔽（MPS）是其中一类有效方法，它通过学习策略 + 备份策略的切换机制保证安全，在连续高维状态空间任务中表现出色。
- **核心问题**：MPS 的备份策略（如急停、退回到安全平衡点）是任务无关的、保守的，导致在恢复安全时严重阻碍任务进展——即使存在同样安全但更优的迂回路径，MPS 也会选择最保守的动作，造成较大的**恢复遗憾**（Recovery Regret）。
- **整体含义**：本文提出的 DMPS 通过引入局部规划器，在保证安全的前提下动态选择最大化短期进展和长期回报的恢复动作，从而显著提升任务性能，同时保持严格的安全保证。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：在 MPS 的屏蔽框架基础上，用**动态备份策略** π*_backup 替代固定的任务无关备份策略。该动态策略由局部规划器 `planRec` 实现，规划器在执行前向搜索时不仅考虑有限步内的即时奖励，还利用神经网络策略的 Q 函数估计长期回报，从而做出更优的恢复决策。
- **关键技术细节**：
  - **控制切换规则**（式 1）：若学习策略 π_hat 在下一状态不可恢复，则调用 π*_backup 而非直接使用 π_backup。
  - **规划器目标**（式 2）：`planRec(s0, Q) = argmax_{a0:n} [ Σ γ^i R(si,ai) + γ^n Q(sn, an) ]`，约束所有中间状态均可恢复（isRec 检查）。该目标融合短期奖励和长期价值估计。
  - **规划器实现**：使用蒙特卡洛树搜索（MCTS）的连续动作变体，具备概率完备性和渐近最优性。
  - **训练算法**（Algorithm 1）：每个 episode 中，若学习动作导致不可恢复状态，先向回放缓冲区记录高惩罚，然后使用规划器或回退策略选择安全动作；训练中规划器为神经网络提供示范，神经网络改进后 Q 函数更准确，形成协同进化。
  - **理论保证**（Theorem 5.1）：恢复遗憾随规划深度 n 以指数级 O(γ^n) 衰减（γ 为折扣因子），在渐进最优规划器下几乎必然成立。

## 3. 实验设计

- **数据集/场景**：共 13 个 benchmark。
  - 5 个静态（ST）：obstacle, obstacle2, mount-car, road, road2d (来自 prior work)
  - 8 个动态场景，每个考虑两种动力学：double integrator (DI) 和 differential drive (DD)：
    - dynamic-obst（移动障碍物）
    - single-gate（单层旋转门）
    - double-gates（双层旋转门）
    - double-gates+（加厚双层旋转门，更困难）
- **对比方法**：
  - PSRL 基线：MPS（标准模型预测屏蔽）、REVEL（神经符号可验证强化学习，仅用于静态环境）
  - SRL 基线：CPO（约束策略优化）、PPO-Lag（PPO 拉格朗日法）、TD3（加入惩罚的深度确定性策略梯度）
- **评测指标**：每 episode 的防护触发次数（安全指标）和总回报（性能指标），结果均为 5 个随机种子的均值±标准差。

## 4. 资源与算力

- **硬件**：服务器配备 64 核 Intel Xeon Gold 5218 CPU @2.30GHz，264GB 内存，8 块 NVIDIA GeForce RTX 2080 Ti GPU。
- **运行方式**：每个 benchmark 在 1 个 CPU 线程和 1 个 GPU 上运行。静态环境训练 100k~400k timesteps，动态环境训练 200k timesteps，每 episode 最大 500 步。平均每次防护触发时规划耗时约 0.4s/timestep（未优化 Python 单线程实现）。

## 5. 实验数量与充分性

- **数量**：13 个 benchmark × 5 种子 ×（DMPS + MPS + 3~5 个基线）= 至少 65 组独立实验。附录还包含规划深度消融实验（H=1,5,9）、计算开销缩放分析等。
- **充分性**：实验覆盖多种动力学（DI、DD）、静态和动态障碍、不同难度级别；对比了 PSRL 和 SRL 中最先进或最常用的方法；结果提供了完整均值和标准差，且在图 3、4 展示了随训练过程的趋势。作者还分析了训练早/晚期轨迹行为。总体充分、客观、公平。

## 6. 主要结论与发现

- **安全方面**：DMPS 在动态 benchmark 中平均每 episode 防护触发 24.7 次，远低于 MPS 的 124.1 次（减少约 76%），且标准差更小，表明行为更稳定。SRL 方法（CPO, PPO-Lag, TD3）在动态环境下频繁违规，而 DMPS 和 MPS 实现零违规。
- **性能方面**：DMPS 在所有动态 benchmark 上总回报均优于 MPS 及其他基线，在静态 benchmark 上与 MPS 相当或更好（obstacle/obstacle2 显著优于 MPS）。相比第二好的 MPS，DMPS 收敛后回报平均提高约 29%。
- **学习收敛**：DMPS 的防护触发次数随训练减少，学习策略逐渐学会安全地靠近目标；而 MPS 的防护触发有时反而增加（因策略倾向于直行但被障碍反复阻挡）。
- **规划深度影响**：消融实验显示 H=1 性能很差，H=5 和 H=9 最终收敛到相同效果，但 H=9 收敛更快，验证了理论指数衰减的实用意义。

## 7. 优点

- **方法创新**：首次将动态规划器集成到可证明安全屏蔽框架中，实现恢复优化的同时保留严格安全保证；规划器与策略之间形成正反馈协同（规划器利用 Q 函数实现长远视野，策略从规划器示范中学习）。
- **理论坚实**：给出了恢复遗憾随规划深度指数衰减的正式定理，规划器具备渐近最优性。
- **实验扎实**：13 个 benchmark、多种动力学、多个对比基线、消融和计算开销分析，统计结果完整。
- **实用性**：训练后模型可几乎不触发防护（高自主安全），降低在线计算开销。

## 8. 不足与局限

- **确定性假设**：要求完美已知的确定性环境模型，不适用于随机动力学（虽然可通过扩展处理，但本文未实现）。
- **计算开销**：规划阶段复杂度 O(exp(H))，实验中平均 0.4s/步（Python 单线程），在实时部署中可能成为瓶颈（虽可通过 C++、并行化缓解）。
- **规划深度依赖**：虽然理论保证指数衰减，但实际中需要足够深度（本文选 H=5）来应对复杂场景，而 H=1 失效，表明仍需一定计算资源。
- **实验覆盖**：未涉及真实机器人或更复杂的高维系统（如视觉输入），也未与基于控制屏障函数（CBF）等经典控制方法对比。
- **可扩展性**：多智能体扩展未讨论；REVEL 基线仅用于静态环境，动态环境下未比较，略显不足。

（完）
