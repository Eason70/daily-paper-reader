---
title: Feasible Reachable Policy Iteration
title_zh: 可行可达策略迭代
authors: "Shentao Qin, Yujie Yang, Yao Mu, JIE LI, Wenjun Zou, Jingliang Duan, Shengbo Eben Li"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=ks8qSwkkuZ"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 安全强化学习结合可达性与安全约束
tldr: 带安全约束的目标到达任务中，现有安全RL将搜索空间限制在可行区域，但仍存在忽视目标导致的无效探索。本文提出可行可达函数，描述是否存在策略使智能体在有限时间内安全到达目标，从而同时考虑安全与目标，实现策略空间剪枝，提升探索效率。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 658, \"height\": 437, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 438, \"height\": 436, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1389, \"height\": 629, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 525, \"height\": 269, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 879, \"height\": 241, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 879, \"height\": 240, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 879, \"height\": 243, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 788, \"height\": 266, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 883, \"height\": 226, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 894, \"height\": 226, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 688, \"height\": 293, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 895, \"height\": 223, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 893, \"height\": 224, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 622, \"height\": 265, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 827, \"height\": 229, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-ks8qswkkuz/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 691, \"height\": 1386, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-ks8qswkkuz/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 787, \"height\": 526, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-ks8qswkkuz/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1178, \"height\": 147, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-ks8qswkkuz/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1138, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-ks8qswkkuz/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1085, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-ks8qswkkuz/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 927, \"height\": 1240, \"label\": \"Table\"}]"
motivation: 现有安全RL限制搜索空间但忽视目标，导致无效探索。
method: 提出可行可达函数，用于剪枝策略空间，同时满足安全约束和目标可达性。
result: 在仿真环境中有效提升了安全目标到达的成功率和效率。
conclusion: 可行可达策略迭代平衡了安全与目标，提高了安全RL的实用性。
---

## Abstract
The goal-reaching tasks with safety constraints are common control problems in real world, such as intelligent driving and robot manipulation. The difficulty of this kind of problem comes from the exploration termination caused by safety constraints and the sparse rewards caused by goals. The existing safe RL avoids unsafe exploration by restricting the search space to a feasible region, the essence of which is the pruning of the search space. However, there are still many ineffective explorations in the feasible region because of the ignorance of the goals. Our approach considers both safety and goals; the policy space pruning is achieved by a function called feasible reachable function, which describes whether there is a policy to make the agent safely reach the goals in the finite time domain. This function naturally satisfies the self-consistent condition and the risky Bellman equation, which can be solved by the fixed point iteration method. On this basis, we propose feasible reachable policy iteration (FRPI), which is divided into three steps: policy evaluation, region expansion, and policy improvement. In the region expansion step, by using the information of agent to reach the goals, the convergence of the feasible region is accelerated, and simultaneously a smaller feasible reachable region is identified. The experimental results verify the effectiveness of the proposed FR function in both improving the convergence speed of better or comparable performance without sacrificing safety and identifying a smaller policy space with higher sample efficiency.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：带安全约束的目标到达任务（如自动驾驶、机器人操作）在现实世界中非常普遍。这类问题的难点在于：安全约束会导致探索提前终止，而目标导向又使得奖励稀疏，从而产生大量无效的探索样本。
- **现有方法局限**：现有的安全强化学习（Safe RL）通常将搜索空间限制在“可行区域”（即保证全程安全的区域），本质上是对策略空间的**剪枝**。然而，可行区域内仍存在大量无法在有限时间内到达目标的区域（即“可达性”不足），导致探索效率低下。
- **核心问题**：如何同时考虑**安全性**（约束满足）和**可达性**（有限时间到达目标），进一步剪枝策略空间，实现更高效的探索，同时不牺牲安全性能。

---

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心概念**：提出**可行可达函数（Feasible Reachable Function, FR函数）**，该函数描述给定状态下是否存在一个策略能在有限时间内安全地到达目标集合。
- **FR函数定义**：
  - 根据到达目标的步数 \( N_g \) 和违反约束的步数 \( N_c \) 定义：若先到达目标则值为正（如 \(\gamma^{N_g}\)），若先违反约束则值为负（如 \(-\gamma^{N_c}\)），若两者均不发生则为0。
  - 该函数的零上水平集即为可行可达区域。
- **理论性质**：FR函数满足**自洽条件**（定理5.3）和**风险贝尔曼方程**（定理5.9），可通过定点迭代求解。
- **算法框架（Feasible Reachable Policy Iteration, FRPI）**：分为三个步骤：
  1. **策略评估（Policy Evaluation）**：更新Q函数。
  2. **区域扩展（Region Expansion）**：利用FR函数识别可行可达区域，并逐步扩大该区域（定理5.5）。
  3. **策略改进（Policy Improvement）**：在可行可达区域内最大化Q值，在区域外最大化FR函数值，从而实现区域感知的策略更新。
- **与SAC结合**：提出FRPI-SAC，在原有SAC框架上增加一个“场景（Scenery）”网络（即动作FR网络），并使用自洽条件训练。

---

### 3. 实验设计：使用了哪些数据集/场景，benchmark是什么，对比了哪些方法

- **实验场景**：
  - **冰冻湖（Frozen Lake）**：验证策略空间剪枝效果。
  - **经典控制任务**：自适应巡航控制（ACC）和四旋翼轨迹跟踪（Quadrotor），用于可视化可行可达区域扩展。
  - **Safety Gym基准**：四个高维机器人导航任务（PointGoal、PointPush、CarGoal、CarPush）。
- **对比方法**：
  - SAC-Lagrangian（直接法）
  - FPI-SAC（Feasible Policy Iteration，间接法，仅考虑可行区域）
  - SAC（无约束基线，用于提供性能上限）
  - RAC（Reachability Constrained RL，仅考虑可达性）
- **评价指标**：平均回合代价（约束违反）、平均回合回报、收敛速度、状态分布热力图等。

---

### 4. 资源与算力

- **文中说明**：训练在NVIDIA GPU 3090上，使用JAX框架，设置 `XLA_PYTHON_CLIENT_MEM_FRACTION=0.1`（分配约2720 MB GPU内存）。
- **推理时间**：FRPI-SAC约1.576 ms/步，与FPI-SAC（1.573 ms）相当，略快于SAC-Lag（1.742 ms），慢于SAC（0.983 ms）。
- **收敛时间**（表2）：以GPU训练时间为参考，例如PointGoal任务中FRPI-SAC收敛约2.0K秒，SAC约2.5K秒，FRPI明显更快。

---

### 5. 实验数量与充分性

- **实验组数**：
  - 冰冻湖：定性比较Q学习与FRPI的策略分布。
  - 经典控制：两个任务（ACC、Quadrotor），分别展示区域扩展过程及代价/回报曲线。
  - Safety Gym：四个任务，每个任务均报告平均代价和回报曲线，并附带表格汇总收敛速度及性能（表3）。
- **消融/分析**：通过对比FRPI与FPI，验证了“考虑可达性”能加速区域扩展并识别更小的有效策略空间。
- **公平性**：所有算法使用相同的网络架构、优化器、超参数（如折扣因子0.99、两层256神经元MLP），并在相同种子下运行。
- **充分性评价**：实验覆盖了简单离散环境（Frozen Lake）、连续控制（ACC、Quadrotor）和高维视觉导航（Safety Gym），对比方法涵盖主流的直接法和间接法，具有一定的全面性。但缺少真实机器人实验，且未在更大规模任务（如多机器人、复杂场景）中验证。

---

### 6. 论文的主要结论与发现

- FR函数能够同时编码安全约束和可达信息，有效识别策略空间中的**高效探索区域**。
- FRPI算法在**区域扩展速度**上比FPI快约3-5倍（ACC和Quadrotor实验中，FRPI在5k步即出现可行区域，而FPI需75k-150k步）。
- 在Safety Gym任务中，FRPI-SAC实现了接近零约束违反，且回报收敛速度显著快于SAC-Lag和FPI-SAC，在有限数据量下（200k-300k步）即达到高性能。
- 通过剪枝不必要的策略空间，FRPI在保证安全的同时提升了样本效率，且没有显著增加计算负担。

---

### 7. 优点：方法或实验设计上的亮点

- **理论创新**：首次将“可行区域”与“可达区域”结合，提出了统一的FR函数及其固定点迭代求解方法，并证明了自洽条件和风险贝尔曼方程。
- **算法设计**：区域感知的策略更新（区域内最大化Q值，区域外最大化FR值）保证了单调的区域扩展和策略改进，理论证明完备。
- **实验可视化**：在ACC和Quadrotor任务中清晰展示了FR区域随迭代的演变过程，直观验证了加速效果。
- **实用性**：与SAC结合的FRPI-SAC仅增加一个小规模的场景网络，计算开销可忽略，易于部署。
- **安全保证**：通过限制动作只能选择导致下个状态仍在可行可达区域的策略，实现了“零训练时违规”的硬约束。

---

### 8. 不足与局限

- **目标函数依赖**：对于调节型任务（如ACC），需要手动构建目标函数（goal function），其设计质量直接影响算法性能。论文承认了这一局限。
- **环境假设**：论文假设确定性MDP和已知动力学模型（用于理论证明），实际实现中使用了环境交互采样，但理论扩展至随机环境需要进一步论证。
- **实验范围**：缺乏真实机器人或复杂动态环境（如非平稳、高维避障）的验证；Safety Gym任务规模仍相对较小（最多16维状态），未测试更大状态/动作空间。
- **偏差风险**：超参数（如初始t值、t更新延迟等）可能对性能敏感，未进行充分的超参数灵敏度分析。
- **对比方法**：未与最新基于模型的Safe RL或离线Safe RL方法对比，存在一定局限性。

---

（完）
