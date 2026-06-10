---
title: Constrained Reinforcement Learning Under Model Mismatch
title_zh: 模型失配下的约束强化学习
authors: "Zhongchang Sun, Sihong He, Fei Miao, Shaofeng Zou"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=GcW9pg4P9x"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 模型失配下的约束强化学习
tldr: 该论文提出鲁棒约束策略优化算法（RCPO），解决训练环境与真实环境模型失配导致的约束违反问题，适用于大规模/连续状态空间，具有最坏情况奖励提升和约束满足的理论保证，可迁移至安全控制领域。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-gcw9pg4p9x/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 778, \"height\": 286, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-gcw9pg4p9x/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 776, \"height\": 290, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-gcw9pg4p9x/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 772, \"height\": 291, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-gcw9pg4p9x/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 784, \"height\": 286, \"label\": \"Figure\"}]"
motivation: 解决约束强化学习模型失配导致的安全违规问题。
method: 提出鲁棒约束策略优化算法RCPO。
result: 在理论保证下实现奖励提升和约束满足。
conclusion: 首个适用于大规模连续空间的鲁棒约束RL方法。
---

## Abstract
Existing studies on constrained reinforcement learning (RL) may obtain a well-performing policy in the training environment. However, when deployed in a real environment, it may easily violate constraints that were originally satisfied during training because there might be model mismatch between the training and real environments. To address this challenge, we formulate the problem as constrained RL under model uncertainty, where the goal is to learn a policy that optimizes the reward and at the same time satisfies the constraint under model mismatch. We develop a Robust Constrained Policy Optimization (RCPO) algorithm, which is the first algorithm that applies to large/continuous state space and has theoretical guarantees on worst-case reward improvement and constraint violation at each iteration during the training. We show the effectiveness of our algorithm on a set of RL tasks with constraints.

---

## 论文详细总结（自动生成）

# 模型失配下的约束强化学习（Constrained Reinforcement Learning Under Model Mismatch）—— 详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：在机器人、自动驾驶、医疗等安全关键领域，强化学习策略必须满足约束（如能耗、安全距离）。现有约束强化学习（CMDP）方法在训练环境中表现良好，但部署到真实环境时，由于**模型失配**（即训练与真实环境的转移核不同，如 sim-to-real 差距、环境非平稳性或对抗攻击），原本满足的约束可能被违反，导致严重后果。
- **整体含义**：论文将问题建模为**模型不确定下的约束强化学习**，要求所学策略对于不确定集合内的**所有**转移核均满足约束，并同时最大化最坏情况下的累积奖励。这是首个针对连续/大规模状态空间的鲁棒约束强化学习理论框架。

## 2. 方法论：核心思想与关键技术细节
- **核心思想**：提出鲁棒约束策略优化算法（RCPO），在每轮迭代中采用**两步更新法**：
  1. **鲁棒策略改进步骤**：在当前策略的邻域内（通过 KL 散度约束）最大化鲁棒奖励优势函数，保证最坏情况奖励提升。
  2. **投影步骤**：将改进后的策略投影到鲁棒约束可行集，确保新策略对所有不确定转移核均满足约束。
- **关键技术细节**：
  - **鲁棒性能差异引理（Lemma 4.1）**：将两个策略的鲁棒价值函数之差用 KL 散度和鲁棒优势函数界住，为局部优化提供基础。
  - **局部近似**：由于最坏情况转移核与策略相关，无法直接优化，论文使用当前策略的 worst‑case 核（分别用于奖励和效用）替代，并证明该近似在邻域内一阶匹配，仍能保证单调改进。
  - **worst‑case 转移核估计**：通过投影梯度下降法（tablar 情形可直接求解，连续情形用参数化模型如高斯混合模型）分别估计奖励和效用对应的 worst‑case 核。
  - **策略参数化**：适用于大规模 MDP（连续状态空间），使用神经网络参数化策略，并通过泰勒展开将两步优化转化为凸二次规划（式 23、25），得到闭式更新规则（式 26）。

## 3. 实验设计
- **场景与数据集**：
  - **Tabular 情形**：Gambler Problem、N‑chain Problem、Frozen‑Lake Problem（均为有限状态/动作空间）。
  - **Deep 情形**：Mujoco 中的 Point Gather 任务（连续状态空间，带安全约束的标准 CMDP 环境）。
- **基准方法**：
  - PCPO（投影约束策略优化）
  - RVI（鲁棒价值迭代，仅优化无约束鲁棒奖励）
  - CPO（约束策略优化，非鲁棒）
  - R3C（鲁棒约束连续控制，启发式）
  - CUP（约束更新投影）
- **对比设置**：Tabular 中每种算法独立运行 5 次，取均值和标准差；Deep 中采用相同神经网络结构（两隐藏层 64、32），超参数统一（折扣因子 0.995，学习率 0.001，批大小 50000，约束阈值 0.1）。模型不确定性通过在环境中添加高斯噪声模拟。

## 4. 资源与算力
- **文中未明确说明**使用的 GPU 型号、数量、训练时长等计算资源信息。仅在 Deep 实验中提到使用 rllab 工具实现，未披露具体硬件配置或训练时间。

## 5. 实验数量与充分性
- **实验数量**：
  - Tabular：3 个环境 × 5 次独立运行 = 15 条 reward/utility 曲线。
  - Deep：仅 Point Gather 一个环境，对比 3‑4 种基线（CUP 因违反约束严重未报告 utility）。
- **充分性评价**：
  - **优点**：Tabular 实验覆盖了不同难度和特性（随机性、稀疏奖励）的环境，对比基线较全面（含鲁棒/非鲁棒、约束/无约束方法）。
  - **不足**：
    - Deep 实验只采用一个连续控制任务，泛化性不足。
    - **缺少消融实验**：未分析 δ（KL 散度限制）、不确定性半径、投影方式等超参数的影响。
    - 未与最新的鲁棒原‑对偶算法（如 RPD，尽管参考文献中有提及）进行实验比较。
    - 未提供置信区间外的统计检验（仅显示标准差）。
  - 总体而言，实验足以支持算法基本有效性，但全面性和深度有所欠缺。

## 6. 主要结论与发现
- RCPO 在 Tabular 任务中**始终满足鲁棒约束**（训练过程中 utility 从未低于阈值），而所有基线均出现不同程度违反。
- RCPO 的奖励值接近无约束鲁棒最优（RVI），说明在满足约束的同时保持了较高的奖励性能。
- 在连续控制任务（Point Gather）中，面对模型扰动（添加高斯噪声），RCPO 的奖励显著高于非鲁棒方法（CPO、PCPO、CUP），且 utility 满足约束，证明了其鲁棒性。
- 理论方面（定理 4.3、4.4）证明了每轮迭代最坏情况奖励提升下界和约束违反上界，且对连续情形的额外误差仅来自 worst‑case 核估计精度 ϵ。

## 7. 优点
- **理论创新**：首次为大规模/连续状态空间的鲁棒约束 RL 提供**每轮更新保证**（最坏情况奖励提升 + 约束满足上界），克服了先前启发式方法无保证的缺陷。
- **方法设计**：两步法有效规避了传统 CPO 可能无可行解的问题；局部近似策略兼顾了可计算性与性能保证。
- **可迁移性**：提出的鲁棒性能差异引理可独立用于其他鲁棒 RL 分析。
- **实验验证**：在多种 Tabular 环境和连续控制任务中展示了优于现有基线的鲁棒性和约束满足性。

## 8. 不足与局限
- **实验覆盖局限**：连续控制仅一个任务（Point Gather），缺少更多复杂环境（如自动驾驶、机器人 locomotion）的验证。
- **缺乏消融研究**：未分析 δ、不确定性半径、神经网络规模等超参数对性能的影响，也未见对 worst‑case 核估计精度的消融实验。
- **理论假设较强**：假设 (s,a)‑rectangular 不确定集（各状态‑动作对独立），且需要常数 M 有限（这可能限制了某些极端分布）。
- **计算开销**：每轮需要两次投影梯度下降估计 worst‑case 核，且需分别对奖励和效用进行，实际训练成本可能更高，文中未讨论。
- **泛化性问题**：参数化转移核（如高斯混合）的假设可能不适用于所有实际模型失配场景。
- **未报告样本复杂度或收敛速度**：仅给出每轮界限，未分析整体收敛所需的迭代次数或样本量。

（完）
