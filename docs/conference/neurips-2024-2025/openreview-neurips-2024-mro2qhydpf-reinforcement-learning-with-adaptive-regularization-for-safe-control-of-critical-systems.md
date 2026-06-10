---
title: Reinforcement Learning with Adaptive Regularization for Safe Control of Critical Systems
title_zh: 面向关键系统安全控制的自适应正则化强化学习
authors: "Haozhe Tian, Homayoun Hamedmoghadam, Robert Noel Shorten, Pietro Ferraro"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=MRO2QhydPF"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 通过自适应正则化实现安全强化学习控制
tldr: 针对强化学习在关键控制系统中的安全挑战，提出RL-AR算法，通过焦点模块将RL策略与硬编码安全约束的正则化器动态组合，在未充分探索状态优先依赖安全策略，在已探索状态实现无偏收敛，在多个关键控制任务中证明了安全性与性能的平衡。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-mro2qhydpf/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1201, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mro2qhydpf/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1423, \"height\": 1414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mro2qhydpf/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1444, \"height\": 586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mro2qhydpf/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 714, \"height\": 447, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mro2qhydpf/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1424, \"height\": 609, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mro2qhydpf/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1423, \"height\": 514, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mro2qhydpf/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1163, \"height\": 567, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-mro2qhydpf/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1420, \"height\": 489, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-mro2qhydpf/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 818, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-mro2qhydpf/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 924, \"height\": 401, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-mro2qhydpf/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1031, \"height\": 1034, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-mro2qhydpf/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1320, \"height\": 471, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-mro2qhydpf/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 759, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-mro2qhydpf/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1081, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-mro2qhydpf/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 851, \"height\": 737, \"label\": \"Table\"}]"
motivation: 强化学习在关键系统中可能产生不安全动作，亟需一种安全探索方法。
method: 提出RL-AR算法，利用焦点模块根据状态动态组合RL策略与安全正则化器。
result: 在多个关键控制应用中，RL-AR在保证安全的同时实现了有效学习。
conclusion: RL-AR为关键系统安全控制提供了一种有效且通用的安全强化学习范式。
---

## Abstract
Reinforcement Learning (RL) is a powerful method for controlling dynamic systems, but its learning mechanism can lead to unpredictable actions that undermine the safety of critical systems. Here, we propose RL with Adaptive Regularization (RL-AR), an algorithm that enables safe RL exploration by combining the RL policy with a policy regularizer that hard-codes the safety constraints. RL-AR performs policy combination via a "focus module," which determines the appropriate combination depending on the state—relying more on the safe policy regularizer for less-exploited states while allowing unbiased convergence for well-exploited states. In a series of critical control applications, we demonstrate that RL-AR not only ensures safety during training but also achieves a return competitive with the standards of model-free RL that disregards safety.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **关键系统控制的安全挑战**：在核聚变、机器人手术、患者治疗等关键系统中，控制动作必须保证不损害系统功能。强化学习（RL）通过试错学习最优策略，但其探索过程容易产生不安全动作，违反安全约束。现有安全RL方法要么在训练阶段无法保证安全（如CPO、SEditor），要么需要巨大的计算开销进行动作验证。而传统控制方法（如MPC）依赖于精确的环境模型，实际应用中模型往往不准确。
- **研究背景**：许多关键场景中，可以基于历史数据构建一个“估计模型”，并从中推导出次优的安全控制策略（如MPC）。但实际环境与估计模型存在偏差（参数差异、未建模动态等），需要RL的适应性来弥补。本文的目标是在“单次生命”（single-life）设置下，即在真实环境中不允许出现任何不安全行为的前提下，实现安全的RL训练并收敛到高性能策略。

## 2. 方法论：核心思想、关键技术细节、公式/算法流程

- **核心思想**：提出**RL with Adaptive Regularization (RL-AR)**，通过一个“焦点模块”（focus module）动态组合两个并行策略：
  - **安全正则化器**（Safety Regularizer）：基于估计模型的约束MPC，硬编码安全约束，提供确定性的安全动作 \(a_{reg}\)。
  - **离线RL智能体**（Off-policy RL Agent）：采用Soft Actor-Critic (SAC)，提供随机探索的RL策略 \(a_{rl}\)。
  - **焦点模块**：学习一个状态依赖的权重 \(\beta(s) \in [0,1]\)，组合动作为 \(a_\beta(s) = \beta(s)a_{reg}(s) + (1-\beta(s))a_{rl}(s)\)。初始时 \(\beta(s)\) 接近1，优先依赖安全正则化器；随着对状态s的充分探索，\(\beta(s)\) 逐渐减小到0，允许RL策略无偏收敛。

- **关键技术细节**：
  - **安全正则化器**：MPC求解N步前瞻的约束优化问题，硬编码状态约束 \(g(s_k) \ge 0\)，并利用估计模型 \(\tilde{f}\) 预测未来轨迹。
  - **策略正则化（Lemma 1）**：组合策略的期望等价于一个正则化优化问题的解，正则化参数 \(\lambda = \beta/(1-\beta)\)，在未充分探索的状态下强制策略接近安全正则化器。
  - **安全界限（Theorem 1）**：推导了组合策略与安全正则化器期望回报差的上界，与 \((1-\beta(s))\) 成正比，从而保证了在 \(\beta\) 接近1时，RL策略的次优性不会导致严重的安全偏离。
  - **焦点模块更新**（公式10）：通过最大化组合动作的Q值来更新 \(\beta(s)\)，使用梯度上升。该更新在表格情况下能保证单调性能提升（Theorem 2）。
  - **无偏收敛（Lemma 2 & Theorem 3）**：当RL策略收敛到最优策略时，\(\beta(s)\) 收敛到0，组合策略与最优策略的总变差距离为0，实现无偏收敛。
  - **算法流程**（Algorithm 1）：
    1. 初始化：空回放缓冲区 \(D\)，MPC控制器（含估计模型），策略网络 \(\pi_\theta\)，Q网络，焦点模块 \(\beta_\psi\)（预训练输出接近1）。
    2. 每步：观测状态 \(s\)，计算组合动作 \(a = \beta a_{reg} + (1-\beta)a_{rl}\)，执行并存储转移 \((s,a,s',r,d,a_{reg})\)。
    3. 更新Q网络（标准SAC，公式3），更新策略网络 \(\pi_\theta\)（公式5），更新焦点模块 \(\beta_\psi\)（公式12）。
    4. 软更新目标Q网络。

## 3. 实验设计：场景、Benchmark、对比方法

- **四个安全关键仿真环境**：
  - **Glucose**：血糖调控，单输入（胰岛素），安全约束为血糖范围，基于Magni风险函数奖励。
  - **BiGlucose**：更复杂的血糖模型，12个状态（11不可观测），双输入（胰岛素+胰高血糖素），大延迟，非光滑动力学。
  - **CSTR**：连续搅拌釜反应器，四状态（浓度、温度），双输入（进料、热流），安全约束防止爆炸。
  - **Cart Pole**：平衡倒立摆，四状态（位置、角度及导数），单输入（水平力），连续动作空间。
- **估计模型**：每个环境均从实际环境参数中设置偏差（如参数 \(n, p_2\) 等），估计模型基于假设的已知参数。
- **对比方法**：
  - **MPC**：使用估计模型的经典控制方法（不更新）。
  - **SAC**：标准模型无关RL（不考虑安全）。
  - **RPL (Residual Policy Learning)**：在MPC基础上加残差策略的RL方法。
  - **CPO (Constrained Policy Optimization)**：基于约束的信任区域方法。
  - **SEditor**：学习安全编辑器转换不安全动作的最近方法。
  - 注意：所有方法（MPC、RPL自带估计模型）中，SAC、CPO、SEditor在训练前先使用估计模型进行预训练（-pt），以公平比较。

## 4. 资源与算力

- 论文未明确报告使用的GPU型号、数量及具体训练时长。仅在附录C中提到实验环境：Python 3.12.5，Ubuntu 22.04，13th Gen Intel Core i7-13850HX CPU，Nvidia RTX 3500 Ada GPU，32GB RAM。并报告了RL-AR每步平均决策时间约0.037秒（包括交互和网络更新），满足实时性要求。但总体算力消耗未量化。

## 5. 实验数量与充分性

- **主要实验**：
  - **训练安全评估**（表1、图2）：对每个环境进行5次独立运行（不同随机种子），统计前100个episode中的失败次数，并绘制归一化回报曲线。对比了RL-AR、MPC、SAC、RPL、CPO、SEditor。
  - **收敛后性能对比**（图3）：展示各方法收敛策略的轨迹和归一化回报。
  - **参数敏感性分析**（图4）：在Glucose环境中改变两个关键参数 \(n\) 和 \(p_2\) 的偏差程度，统计训练失败次数，评估RL-AR对模型误差的鲁棒性。
  - **消融实验**（附录D.1）：对比状态依赖焦点模块 vs 标量权重，验证状态依赖的有效性。
  - **RL智能体选择消融**（附录D.2）：比较使用SAC vs TD3作为RL模块，说明熵正则化的好处。
  - **额外环境验证**（附录D.4）：在Acrobot环境中进一步验证。
- **充分性评价**：实验覆盖了四个不同动力学特性的关键场景，包含单输入/多输入、可观测/部分可观测、平滑/非光滑等。每个实验进行多次独立重复并报告均值和标准差。对比方法全面（包括经典控制、模型无关RL、安全RL）。消融实验针对核心模块进行了评估。实验设计较为充分、客观、公平（通过预训练保证公平比较）。

## 6. 主要结论与发现

- RL-AR在训练过程中**完全避免了不安全失败**（四个环境中前100episode失败数为0），而其他RL方法（包括预训练后）均出现多次失败。
- RL-AR的归一化回报**收敛速度快且最终性能与不考虑安全的SAC相当甚至更好**（在Glucose、BiGlucose、CSTR中优于SAC，在Cart Pole中相当）。
- 即使估计模型与实际环境存在**60%以上参数偏差**，RL-AR仍能保持安全训练（当偏差极大导致MPC本身失败时，RL-AR可通过快速降低 \(\beta\) 恢复）。
- 焦点模块的**状态依赖特性**比标量权重带来更稳定的性能提升。
- 使用SAC作为RL模块（带有熵正则化）比TD3更有利于探索和稳定。

## 7. 优点

- **理论与实践结合**：提供了坚实的理论分析（安全上界、单调改进、无偏收敛），支撑了算法设计。
- **新颖的焦点模块**：状态依赖的权重学习机制，既保证了探索不足状态的安全，又允许充分探索状态的无偏优化。
- **训练零失败**：在单次生命设置下真正实现了安全训练，无需任何先验失败经验。
- **与现有方法兼容**：可灵活选择不同的离线RL算法和安全正则化器（文中使用SAC+MPC）。
- **计算效率高**：每步平均0.037秒，满足实时控制要求。
- **实验全面**：涵盖多个关键领域，参数敏感性分析验证了鲁棒性。

## 8. 不足与局限

- **对估计模型质量的假设**：方法要求估计模型具备“合理的安全性能”，若模型严重失准（如文中极端偏差情况），MPC本身失败，RL-AR虽能恢复但仍依赖初始安全性能。实际中构建可靠估计模型不一定总是可行。
- **未更新估计模型**：RL-AR没有利用真实环境交互数据更新估计模型，可能限制在持续漂移环境中的适用性。论文指出这可以是未来工作方向。
- **单次生命设定范围**：假设不能容忍任何训练失败，这限制了方法的通用性（例如自动机器人可以在仿真中试错）。但对于实际关键系统，该假设合理。
- **实验环境均为仿真**：未在真实物理系统或实际患者数据上验证，奖励函数和约束设置可能存在简化。
- **缺乏与其他最新安全RL方法的更广泛对比**：例如基于安全屏障函数（CBF）的方法、基于验证的屏蔽方法等，仅对比了CPO和SEditor。此外未对比最近的应用于医疗的带约束RL方法。
- **可扩展性讨论不足**：对于超高维状态/动作空间，焦点模块的学习可能面临挑战，论文未讨论。

（完）
