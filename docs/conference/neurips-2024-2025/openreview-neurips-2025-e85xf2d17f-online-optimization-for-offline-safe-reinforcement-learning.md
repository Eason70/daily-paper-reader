---
title: Online Optimization for Offline Safe Reinforcement Learning
title_zh: 离线安全强化学习的在线优化方法
authors: "Yassine Chemingui, Aryan Deshwal, Alan Fern, Thanh Nguyen-Tang, Jana Doppa"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=e85xf2d17F"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 离线安全强化学习结合在线优化，通用安全约束方法
tldr: 离线安全强化学习面临数据有限和约束难满足的挑战。本文提出一种将离线RL与在线优化结合的框架，通过极小极大目标函数求解安全策略。理论证明该方法的近似最优性，并在DSRL基准上验证了其在严格成本预算下有效满足安全约束。此方法可适配任意离线RL算法，降低了安全策略学习的门槛。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-e85xf2d17f/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1276, \"height\": 578, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e85xf2d17f/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 712, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-e85xf2d17f/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1446, \"height\": 810, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-e85xf2d17f/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1452, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-e85xf2d17f/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1457, \"height\": 596, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-e85xf2d17f/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1170, \"height\": 235, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-e85xf2d17f/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1168, \"height\": 201, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-e85xf2d17f/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1171, \"height\": 715, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-e85xf2d17f/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1164, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-e85xf2d17f/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1031, \"height\": 926, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-e85xf2d17f/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1458, \"height\": 530, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-e85xf2d17f/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1031, \"height\": 926, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-e85xf2d17f/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 754, \"height\": 809, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-e85xf2d17f/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 654, \"height\": 750, \"label\": \"Table\"}]"
motivation: 针对离线数据环境下学习安全策略的挑战。
method: 将离线安全强化学习建模为极小极大问题，利用在线优化与离线RL结合求解。
result: 在DSRL基准上，方法在严格成本约束下实现了高回报。
conclusion: 提出了一种无需离线策略评估的通用离线安全强化学习方案。
---

## Abstract
We study the problem of Offline Safe Reinforcement Learning (OSRL), where the goal is to learn a reward-maximizing policy from fixed data under a cumulative cost constraint. We propose a novel OSRL approach that frames the problem as a minimax objective and solves it by combining offline RL with online optimization algorithms. We prove the approximate optimality of this approach when integrated with an approximate offline RL oracle and no-regret online optimization. We also present a practical approximation that can be combined with any offline RL algorithm, eliminating the need for offline policy evaluation. Empirical results on the DSRL benchmark demonstrate that our method reliably enforces safety constraints under stringent cost budgets, while achieving high rewards. The code is available at https://github.com/yassineCh/O3SRL.

---

## 论文详细总结（自动生成）

# 中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：离线安全强化学习（OSRL）旨在从固定数据集中学习一个最大化累积奖励且满足累积成本约束的策略。在实际安全关键应用（如医疗、智能电网）中，不仅需要处理离线强化学习固有的分布偏移（out-of-distribution）挑战，还需要确保学得的策略满足严格的成本/安全约束。现有方法（如基于拉格朗日松弛的策略优化）往往不稳定，导致振荡、发散或学习过于保守的策略，尤其当成本阈值（κ）很小时性能严重退化。这一问题在先前工作中缺乏系统研究。
- **核心问题**：如何在严格的安全预算下，从离线数据中学到既高奖励又满足约束的策略？
- **整体含义**：本文提出了一种新的在线优化方法（O3SRL）来解耦离线策略学习和约束满足，通过一个极小极大目标函数并利用无遗憾在线优化算法更新拉格朗日乘子，实现了理论保证和实际有效性。

## 2. 论文提出的方法论
- **核心思想**：将离线约束RL问题建模为极小极大优化问题，采用迭代方法交替执行两个步骤：
  1. **策略分布求解**：给定当前拉格朗日乘子 λₜ₋₁，将离线安全数据集中的奖励和成本组合成新的奖励函数 r' = r - λₜ₋₁(c - (1-γ)κ)，然后调用任意离线RL oracle（如TD3+BC）求解最大化新奖励的策略分布。
  2. **拉格朗日乘子更新**：使用无遗憾在线优化算法（无遗憾算法，如EXP3）基于当前策略分布更新λₜ。
- **理论框架 (Algorithm 1)**：假设存在一个离线RL oracle（满足误差界ε_offline-RL(n)）和一个无遗憾算法（满足遗憾界R_T(Λ)），则最终输出平均策略分布和平均λ的近似最优性由Theorem 1保证，误差为 ε_offline-RL(n) + R_T(Λ)/T。
- **实用近似 (Algorithm 2)**：为解决连续λ空间需调用离策略评估（OPE）的不稳定性及迭代运行离线RL至收敛的高计算成本，提出两个简化：
  - 将λ离散化为K个值，转化为多臂赌博机（MAB）问题，使用EXP3算法避免OPE。
  - 在不完全收敛的假设下，采用随机离线RL oracle，每次迭代只进行M步随机梯度更新（从上一轮策略初始化），返回最后一步策略而非平均策略。
- **最终算法**：结合EXP3 MAB和TD3+BC（或其他离线RL算法），在DSRL基准上展示性能。

## 3. 实验设计
- **数据集 / 场景**：DSRL Bullet benchmark，包含8个连续控制任务：BallRun、CarRun、DroneRun、AntRun、BallCircle、CarCircle、DroneCircle、AntCircle。每个任务中，agent需要在高奖励目标（如快速移动）和安全约束（如速度、位置限制）间平衡。
- **Benchmark**：DSRL（Datasets and Benchmarks for Offline Safe Reinforcement Learning），提供标准化的离线数据集和评估协议。
- **对比方法**：包括BC-Safe、BEAR-Lag、CPQ、COptiDICE、CDT、CCAC、CAPS、FISOR等8种主流离线安全RL方法。此外还进行了消融实验。

## 4. 资源与算力
- **硬件**：一张NVIDIA A40 GPU（48GB内存）。
- **训练时间**：每个任务单次随机种子约20分钟（服务器空闲时）。论文未明确说明总实验小时数，但基于实验设置（8个任务×3 seeds × 多个消融变体），总时间估计在数十小时级别。

## 5. 实验数量与充分性
- **主要实验**：在8个任务上对比了8种基线，每个方法取3个随机种子，每个种子评估20个episode。结果报告均值和标准差（表2）。
- **消融实验**：
  - 不同臂数K (2,5,10) 对奖励和成本的影响（表1）。
  - 不同成本阈值κ (5,20,40) 下的表现（表3）。
  - 不同基础离线RL算法（TD3+BC vs IQL）的适用性（表4）。
  - 不同λ最大值C (2,5,10) 的影响（附表7）。
  - 不同λ离散化方式（均匀 vs 自适应）的影响（附表8）。
  - 不同离线RL更新步数M (1,10,100) 的影响（附表9）。
  - 在额外SafetyGym环境（7个任务）验证泛化性（附表5）。
  - 固定λ作为超参数的对比（附表6）。
  - 6个随机种子稳定性验证（附表10）。
- **充分性与公平性**：实验设计比较全面，涵盖了任务多样性、算法对比、超参数敏感性、泛化能力、统计稳定性。对比方法部分来自公开实现，但注意不是所有方法都有全面超参数调整，但论文声称遵循DSRL标准配置。总体客观性良好。

## 6. 论文的主要结论与发现
- O3SRL 是唯一在所有8个DSRL任务上一致满足成本约束的方法（成本归一化值≤1），尤其在严格成本预算下表现突出。
- 在满足安全约束的方法中，O3SRL 在2/8任务中获得了最高奖励，在其他任务中稳定位列第二，实现了奖励和安全的较好平衡。
- 使用K=5臂即可获得很好的效果，增加K带来边际收益递减（K=2已经有效）。
- O3SRL 在不同成本阈值下均能自适应，且可与不同离线RL算法（如TD3+BC和IQL）兼容。
- 训练曲线显示成本快速下降并稳定低于阈值，奖励稳步提升。

## 7. 优点
- **理论保证**：提供了极小极大解收敛到ϵ-近似均衡的证明，且误差项可分解为离线RL误差、在线优化遗憾和离散化误差。
- **避免OPE**：通过离散化λ并采用无遗憾MAB算法，彻底避免了不稳定的离策略评估（OPE），解决了前人方法中OPU误差传播和计算开销问题。
- **即插即用**：可以简洁地将任何现成离线RL算法包装成安全版本，无需对原算法做修改。
- **有效处理严格约束**：在严格成本阈值下（κ=5）表现优异，解决了先前方法在此场景下性能崩溃的问题。
- **实验全面**：大量消融实验验证了各组件作用，并在额外SafetyGym任务上验证了泛化能力。

## 8. 不足与局限
- **实验覆盖**：虽使用DSRL和SafetyGym，但环境均为仿真连续控制任务，未在真实世界或离散动作空间任务上验证。可能存在领域选择偏差。
- **理论近似**：最终实用算法（Algorithm 2）做了多项近似（离散λ、M步更新、返回last-iterate而非平均），理论与实际之间仍有差距，但论文通过消融实验展示了近似版本的有效性。
- **计算效率**：尽管避免了OPE，但每轮仍需进行M步策略更新，总训练步数为T×M。论文未讨论与直接运行一次离线RL加后处理相比的计算开销对比。
- **超参数敏感**：需要设定臂数K、最大λ值C、更新频率M等超参数，论文虽进行了消融，但未提供自动调参策略，实际应用可能需手动调整。
- **未讨论在线部署前验证**：模型输出的策略虽在训练集上满足约束，但实际部署时由于数据分布变化可能仍会有成本溢出，论文未对此进行分析。

（完）
