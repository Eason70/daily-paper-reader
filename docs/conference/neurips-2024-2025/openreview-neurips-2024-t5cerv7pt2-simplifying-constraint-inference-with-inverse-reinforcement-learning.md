---
title: Simplifying Constraint Inference with Inverse Reinforcement Learning
title_zh: 简化逆强化学习的约束推断
authors: "Adriana Hugessen, Harley Wiltzer, Glen Berseth"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=T5Cerv7PT2"
tags: ["query:safe-rl-cbf"]
score: 4.0
evidence: 利用逆强化学习推断安全约束，与安全强化学习相关
tldr: 传统安全强化学习需通过试错学习约束，效率低且风险高。本文提出利用逆强化学习从专家数据中提取安全约束，仅需少量次优专家轨迹即可学习安全策略。该方法简化了约束推断过程，在安全关键应用中降低了学习风险。实验表明，即便在专家数据不完美的情况下，也能有效恢复关键安全约束。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-t5cerv7pt2/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1434, \"height\": 558, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-t5cerv7pt2/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1350, \"height\": 522, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-t5cerv7pt2/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1437, \"height\": 746, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-t5cerv7pt2/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1441, \"height\": 576, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-t5cerv7pt2/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1322, \"height\": 1541, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-t5cerv7pt2/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1320, \"height\": 1464, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-t5cerv7pt2/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1443, \"height\": 497, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-t5cerv7pt2/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 753, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-t5cerv7pt2/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1043, \"height\": 141, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-t5cerv7pt2/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 550, \"height\": 538, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-t5cerv7pt2/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 934, \"height\": 412, \"label\": \"Table\"}]"
motivation: 减少安全强化学习中对试错学习的依赖。
method: 通过逆强化学习从专家轨迹中推断安全约束，将其融入策略学习。
result: 在次优专家数据下仍能有效推断并满足安全约束。
conclusion: 提供了一种低风险的约束学习范式，适用于安全关键应用。
---

## Abstract
Learning safe policies has presented a longstanding challenge for the reinforcement learning (RL) community. Various formulations of safe RL have been proposed; However, fundamentally, tabula rasa RL must learn safety constraints through experience, which is problematic for real-world applications. Imitation learning is often preferred in real-world settings because the experts' safety preferences are embedded in the data the agent imitates. However, imitation learning is limited in its extensibility to new tasks, which can only be learned by providing the agent with expert trajectories. For safety-critical applications with sub-optimal or inexact expert data, it would be preferable to learn only the safety aspects of the policy through imitation, while still allowing for task learning with  RL. The field of inverse constrained RL, which seeks to infer constraints from expert data, is a promising step in this direction. However, prior work in this area has relied on complex tri-level optimizations in order to infer safe behavior (constraints). This challenging optimization landscape leads to sub-optimal performance on several benchmark tasks. In this work, we present a simplified version of constraint inference that performs as well or better than prior work across a collection of continuous-control benchmarks. Moreover, besides improving performance, this simplified framework is easier to implement, tune, and more readily lends itself to various extensions, such as offline constraint inference.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：在安全强化学习（Safe RL）中，传统的“白板学习”需要智能体通过试错来学习安全约束，这在真实世界安全关键应用中风险极高且不可行。
- **背景**：模仿学习可以从专家数据中嵌入安全偏好，但无法超越专家或适应新任务；离线RL虽可优化奖励，但无法保证约束满足。逆约束强化学习（ICRL）旨在从专家轨迹中推断未知约束，使得后续任务学习可以保持安全。
- **现有瓶颈**：先前ICRL方法依赖复杂的三层优化（约束-拉格朗日乘子-策略），导致优化困难、实现复杂、在多个基准任务上表现次优。
- **本文目标**：证明ICRL可简化为逆强化学习（IRL），并提出实用改进，使得约束推断更简单、性能更优、更易扩展（如离线推断）。

## 2. 方法论

### 核心思想
- **理论等价性**（定理4.1）：当约束函数类 \( \mathcal{F}_c \) 是一个凸锥时，ICRL的三层优化等价于IRL的双层优化（即最大化专家与策略的回报差异）。证明分两步：首先证明ICRL与简化版S-ICRL等价，再证明IRL可解S-ICRL。
- **实践意义**：直接用最大熵IRL（MaxEnt IRL）学习一个“虚拟奖励” \( \tilde{r}(s,a) = r(s,a) - c(s,a) \)，其中 \( c \) 即为需要推断的约束函数，且学习到的 \( c \) 可以缩放后作为下游CMDP中的约束。

### 关键技术细节
- **约束函数表示**：使用线性输出激活的神经网络，满足凸锥性质（通过Leaky ReLU + L2正则化替代硬裁剪）。
- **改进措施**（Section 4.2）：
  - **L2正则化**：在损失中加入专家轨迹上约束值的平方惩罚，防止约束在安全状态上过大。
  - **单独评论家（Separate Critics）**：对奖励和约束分别使用独立的Q函数，避免约束更新干扰奖励学习。
  - **策略重置（Policy Resetting）**：周期性重置约束评论家的最后一层，缓解塑性损失（plasticity loss）问题。
- **算法流程**（Algorithm 1）：交替收集经验、更新奖励/约束评论家、更新策略、更新约束函数。策略联合使用奖励Q和约束Q： \( Q(s,a) = Q_\alpha(s,a) - Q_\theta(s,a) \)。

## 3. 实验设计

- **数据集/场景**：使用Liu et al. (2023a) 提出的五个MuJoCo连续控制环境（Ant, HalfCheetah, Walker2D, Swimmer, InvertedPendulum），每个环境有位置相关的二进制约束。
- **基准对比方法**：MECL（最大熵ICRL，Malik et al. 2021 的 Lagrangian 方法）和 GACL（GAIL用于约束推断）。
- **评估指标**：可行奖励（Feasible Rewards，首次违规前的累积回报）和违规率（Violation Rate，包含至少一次违规的回合比例）。
- **实验设置**：每个方法5个随机种子，训练5M环境步，使用SAC作为前向RL算法。IRL部分基于Zeng et al. (2022)的实现。

## 4. 资源与算力

- **明确说明**：论文附录A.2指出，每个运行（一个配置，5个种子）使用一个节点，配备单GPU（型号未具体说明）、6个CPU、每个CPU 6GB RAM。单个运行约1.5天完成训练。
- **未明确**：GPU的具体型号、显存大小以及总计算量（例如总GPU小时数）未提供。

## 5. 实验数量与充分性

- **实验组数**：主要实验包括：
  - 主比较实验（图1）：在所有5个环境上对比IRL-Base、IRL-Plus与MECL、GACL。
  - 子最优专家数据实验（图2）：在HalfCheetah上测试20%/50%/80%违规率子最优数据。
  - 消融实验（图3、4）：逐一分析L2正则化、单独评论家、策略重置的效果，共6种变体。
- **充分性**：
  - 每个实验5个种子，使用95% Bootstrap置信区间和IQM/Median/Mean/Optimality Gap四类统计量，符合推荐做法。
  - 对比方法选取合理，基线来自原论文作者提供的实现，公平性较好。
  - 消融实验系统，覆盖了各个改进因素。
  - 不足：仅在5个MuJoCo连续控制环境上测试，缺乏离散控制、高维视觉或真实场景验证；子最优实验仅在一个环境上进行；未测试离线IRL扩展（仅在讨论中提及）。

## 6. 主要结论与发现

- **IRL可替代ICRL**：基础IRL（IRL-Base）在可行奖励和违规率上即达到或超过MECL水平。
- **IRL-Plus更优**：加入L2正则化+单独评论家+策略重置后（IRL-Plus），在聚合指标上显著优于MECL和GACL，且统计显著。
- **简单易用**：IRL-Plus无需大量环境特定超参数调整（仅调节约束学习率），代码和调参比ICRL更简单。
- **子最优鲁棒性**：在高达80%子最优数据场景下，IRL-Plus仍优于MECL，而GACL完全失效。

## 7. 优点

- **理论贡献**：严格证明ICRL与IRL在凸锥约束类下的等价性，简化了问题本质。
- **实用改进**：提出的三点改进（L2正则化、单独评论家、策略重置）可轻松集成到任何IRL算法中。
- **实验严谨**：使用标准化基准、多种子、统计显著性检验（Bootstrap CI）、推荐聚合统计量。
- **开源代码**：提供GitHub仓库，便于复现和扩展。
- **启发未来**：理论框架打开了利用IRL子领域（如离线IRL）解决约束推断问题的大门。

## 8. 不足与局限

- **实验覆盖有限**：仅五个连续控制环境，且约束类型简单（位置二进制约束），未测试更复杂约束（如速度、力、高维约束）或离散/图像域。
- **方差较大**：图4显示各方法在环境间有高方差，尤其在InvertedPendulum和Swimmer上，性能不稳定。
- **子最优实验单一**：仅在HalfCheetah上测试，未在其他环境验证子最优鲁棒性。
- **与基线对齐问题**：由于使用SAC（而非PPO），与原始MECL实现存在算法差异，尽管作者声称公平比较，但可能仍有配置差异影响。
- **未实现离线扩展**：虽在引言和讨论中强调离线IRL的潜力，但并未提供离线实验验证。
- **理论假设限制**：凸锥约束类假设在实践中有一定合理性（通过激活函数近似），但严格凸锥性在实际深度学习近似中难以保证。

（完）
