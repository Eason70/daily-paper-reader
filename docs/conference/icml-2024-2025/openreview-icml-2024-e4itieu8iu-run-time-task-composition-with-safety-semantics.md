---
title: Run-Time Task Composition with Safety Semantics
title_zh: 具有安全语义的运行时任务组合
authors: "Kevin Leahy, Makai Mann, Zachary Serlin"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=E4ItiEU8Iu"
tags: ["query:safe-rl-cbf"]
score: 4.0
evidence: 安全组合强化学习与连续动作
tldr: 针对强化学习中的布尔组合任务，提出两种组合安全语义（避免约束），并证明其正确性。该方法将安全组合从离散动作空间扩展到连续动作空间，通过修改值迭代算法在基准环境中验证了可行性。为安全强化学习提供了可组合的约束框架。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-e4itieu8iu/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 728, \"height\": 690, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-e4itieu8iu/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 764, \"height\": 869, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-e4itieu8iu/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 863, \"height\": 963, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-e4itieu8iu/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1802, \"height\": 1976, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-e4itieu8iu/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 649, \"height\": 596, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-e4itieu8iu/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 712, \"height\": 579, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-e4itieu8iu/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1163, \"height\": 1931, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-e4itieu8iu/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 822, \"height\": 326, \"label\": \"Table\"}]"
motivation: 现有强化学习的布尔组合仅支持到达满足状态，不支持可组合的安全避免约束。
method: 提出两种组合安全语义定义，并证明如何强制执行每种语义，同时将方法扩展到连续动作空间。
result: 在修改的值迭代实验中展示了两种安全语义的有效性及权衡。
conclusion: 为安全强化学习的可组合约束提供了理论基础和实用算法。
---

## Abstract
Compositionality is a critical aspect of scalable system design. Here, we focus on Boolean composition of learned tasks as opposed to functional or sequential composition. Existing Boolean composition for Reinforcement Learning focuses on reaching a satisfying absorbing state in environments with discrete action spaces, but does not support composable safety (i.e., avoidance) constraints. We provide three contributions: i) introduce two distinct notions of compositional safety semantics; ii) show how to enforce either safety semantics, prove correctness, and analyze the trade-offs between the two safety notions; and iii) extend Boolean composition from discrete action spaces to continuous action spaces. We demonstrate these techniques using modified versions of value iteration in a grid world, Deep Q-Network (DQN) in a grid world with image observations, and Twin Delayed DDPG (TD3) in a continuous-observation and continuous-action Bullet physics environment

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：现有强化学习中的布尔任务组合方法（如 Nangue Tasse 等人）仅支持**到达（reachability）**任务，即学习如何到达满足特定布尔公式的目标状态，但不支持**可组合的安全避免（avoidance）约束**。例如，一个运载危险废弃物的卡车需要避免经过居民区，而现有的组合框架无法让用户运行时动态地将某个区域标记为“需避开”。
- **动机**：实现可扩展的系统设计需要组合性。本文希望训练少量基元策略，在部署时通过布尔运算零样本组合出更复杂的行为，同时满足不同层次的安全约束。
- **整体含义**：提出两种新的安全语义（最小违反 MV 和优先安全 PS），并证明了正确性；同时将布尔组合从离散动作空间扩展到连续动作空间，为安全强化学习的可组合约束奠定了理论基础和实用算法框架。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：通过精心设计的**罚分层次结构（penalty hierarchy）**，对不同的不良行为（如经过非目标区域、终止在错误状态等）赋予不同数量级的负奖赏，使得最优策略优先选择纯路径（不产生任何无关标签），其次是最小违反路径，然后才是优先安全路径。
- **关键技术细节**：
  - **罚分乘子** \( \eta \) ：定义为环境中所有可能最长的最短路径长度上界。保证即使绕路 \( \eta \) 步也比遭受一次更高等级的惩罚更优。
  - **最小违反（MV）奖励函数（公式 2）**：
    - 终端在正确目标：大正奖励 \( R_{goal} \)；
    - 步进到非目标状态：\( R_{step} \)（负）；
    - 步进到带有其他标签（非目标）的状态：\( R_{badstep} = \eta R_{step} \)；
    - 终止在错误目标（非期望标签）：\( R_{badterm} = \eta^2 R_{step} \)；
    - 终止在否定目标：\( R_{worstterm} = \eta^3 R_{step} \)。
    层次保证了纯路径优于任何带一个不良标签的路径。
  - **优先安全（PS）奖励函数（公式 3）**：针对否定任务单独训练，额外惩罚经过需避开的标签状态（\( R_{worststep} = \eta^2 R_{step} \)），并交换目标与非目标的终止奖励。
  - **扩展Q值函数**：将目标作为输入 \( \bar{Q}(s, g, a) \)，保存所有目标下的最优值，支持布尔运算。
  - **组合规则**（离散动作）：
    - 析取：\( \max\{\bar{Q}_1^*, \bar{Q}_2^*\} \)；
    - 合取：\( \min\{\bar{Q}_1^*, \bar{Q}_2^*\} \)；
    - 否定：利用最大/最小策略的扩展Q值计算。
  - **连续动作空间扩展**：不能直接取最大/最小动作，而是根据扩展Q值比较两个基元策略的动作，选择使复合Q值更大的那个策略（公式 21、22）。否定任务需单独学习并归一化。
- **理论证明**：在确定性MDP假设下，定理1-5分别证明了MV奖励产生MV路径、PS奖励产生PS路径，以及组合运算保持原有安全语义。

## 3. 实验设计
- **数据集/场景**：三个环境：
  1. **2D静态网格世界**（5动作：上、下、左、右、停留），标签有 A、B、C等，使用**值迭代**得到最优策略。
  2. **2D物品收集网格世界**（图像观测，4动作：方向），使用**DQN**学习基元策略（如收集“蓝色”、“圆形”等）。
  3. **Bullet-Safety-Gym**（连续动作：2维力向量；96维激光雷达观测），使用**TD3**学习。
- **基准（Benchmark）**：主要对比**原始到达语义（RO）**，即 Nangue Tasse 等人的方法，其组合不考虑路径上的避免。论文展示了RO与SA（安全感知）在不同组合下的轨迹差异（图2）。
- **对比方法**：三种语义（MV、PS（朴素组合）、PS（预训练组合））在网格世界中的表现对比（图7）。未与现存的安全RL方法（如Shielding、Constrained PPO）进行数值对比，因为本文聚焦于可组合性而非训练方法。

## 4. 资源与算力
- **明确信息**：文中提到所有函数近似实验使用 **NVIDIA Volta GPU**（具体型号未说明，可能是V100），**单卡**运行。
- **训练步数**：
  - DQN网格世界：初始训练约2M步收敛，后经20-60K步微调；
  - TD3连续环境：随机环境训练4M步，再在静态环境训练1M步。
- **未明确信息**：GPU数量（推测单卡）、具体型号、内存等细节未给出。

## 5. 实验数量与充分性
- **实验组数**：
  - 三个环境中展示了多种布尔组合的示例轨迹（图3、4、7），包括纯路径、MV路径、PS路径。
  - 刻意设计了一个存在振荡风险的环境（图7），比较MV、PS朴素组合、PS预训练组合的效果。
  - 附录D补充了更多网格世界组合示例（图4）。
- **充分性评价**：
  - **优点**：覆盖了离散和连续动作空间，以及最优策略和函数近似两种范式；包含了理论证明与实验验证的对齐。
  - **不足**：
    - 实验以**定性可视化为主**，缺少量化指标（如成功率、平均到达步数、违反次数、收敛速度等）。
    - **缺乏与现有安全RL方法的对比**（如Shielded RL、Constrained Policy Optimization），因此无法评估在纯粹安全性能上的优劣。
    - 没有消融研究（如图像观测的影响、η取值对收敛的影响等）。
    - 数据集规模小（网格世界和单场景的Bullet环境），泛化性待验证。

## 6. 主要结论与发现
- **纯路径优先**：如果纯路径存在，最优策略会选择不产生任何无关标签的路径。
- **MV与PS可正确实现**：MV路径最小化非目标标签的经过次数；PS路径可完全避开特定标签（但可能需要预先学习）。
- **连续动作空间可行**：首次将布尔任务组合扩展到连续动作空间，并给出理论与实验验证。
- **模块化优势**：训练少量基元策略（如6个）即可零样本组合大量新任务（如M+2N个），远优于分别训练每个组合（指数级增长）。

## 7. 优点
- **理论清晰**：明确定义两种安全语义，给出罚分层次的设计原则和理论保证。
- **组合性**：在运行时无需再训练，通过布尔代数即可获得满足安全约束的新策略。
- **扩展性**：从离散动作空间到连续动作空间，从表格型到深度强化学习，适用范围广。
- **实用导向**：示例（垃圾车）反映了实际需求，方法便于理解和实现。

## 8. 不足与局限
- **实验覆盖不足**：缺乏大规模定量实验（如成功率对比、与SOTA安全RL方法的比较）。
- **假设强**：理论依赖确定性MDP，函数近似环境中的正确性仅为实验验证，没有理论保证。
- **PS语义的限制**：组合多个否定任务可能振荡（chattering），需要额外假设（Assumption 4.1）或预先训练组合，限制了灵活性。
- **训练难度增加**：安全罚分使奖励稀疏且负值较大，需要课程学习才能收敛，实际调参复杂。
- **应用风险**：在连续环境中使用函数近似，组合策略可能局部最优或偏离理论保证；未讨论安全性方面的风险（如违反安全约束的概率）。
- **缺乏公平对比**：未与同样支持任务组合的其他方法（如逻辑规范分解、分层RL）进行比较。

（完）
