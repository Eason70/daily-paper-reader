---
title: Temporal Logic Specification-Conditioned Decision Transformer for Offline Safe Reinforcement Learning
title_zh: 时序逻辑规范条件化决策Transformer用于离线安全强化学习
authors: "Zijian Guo, Weichao Zhou, Wenchao Li"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=7bg10Jj3bG"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 离线安全强化学习结合时序逻辑规范，与安全控制相关
tldr: 本文提出时序逻辑规范条件化决策Transformer，将信号时序逻辑与Transformer结合，用于离线安全强化学习。该框架能处理具有丰富时序逻辑结构的复杂安全约束，在DSRL基准上表现优越。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-7bg10jj3bg/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 844, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-7bg10jj3bg/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1776, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-7bg10jj3bg/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 842, \"height\": 681, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-7bg10jj3bg/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1770, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-7bg10jj3bg/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1753, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-7bg10jj3bg/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1771, \"height\": 365, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-7bg10jj3bg/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1588, \"height\": 1144, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-7bg10jj3bg/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 859, \"height\": 478, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-7bg10jj3bg/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1780, \"height\": 601, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-7bg10jj3bg/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 798, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-7bg10jj3bg/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1768, \"height\": 1036, \"label\": \"Table\"}]"
motivation: 现有离线安全强化学习方法难以处理复杂时序逻辑约束。
method: 提出SDT框架，利用信号时序逻辑表达时序规则，并结合决策Transformer的序列建模能力。
result: 在DSRL基准测试中展现更好的安全约束满足能力。
conclusion: SDT为复杂时序安全约束的强化学习提供了有效方案。
---

## Abstract
Offline safe reinforcement learning (RL) aims to train a constraint satisfaction policy from a fixed dataset. Current state-of-the-art approaches are based on supervised learning with a conditioned policy. However, these approaches fall short in real-world applications that involve complex tasks with rich temporal and logical structures. In this paper, we propose temporal logic Specification-conditioned Decision Transformer (SDT), a novel framework that harnesses the expressive power of signal temporal logic (STL) to specify complex temporal rules that an agent should follow and the sequential modeling capability of Decision Transformer (DT). Empirical evaluations on the DSRL benchmarks demonstrate the better capacity of SDT in learning safe and high-reward policies compared with existing approaches. In addition, SDT shows good alignment with respect to different desired degrees of satisfaction of the STL specification that it is conditioned on.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：离线安全强化学习（Offline Safe RL）旨在从固定数据集中学习满足约束的策略。现有最先进方法基于监督学习（如条件策略），但它们在处理具有丰富时序和逻辑结构的复杂真实任务时表现不足。例如，自动驾驶车辆必须在停止标志处完全停下、短暂停顿、且仅在无其他车辆时通过。这类约束难以用简单的成本函数定义。
- **研究背景**：时序逻辑（Temporal Logic, TL）能形式化描述系统随时间的行为（如安全、活性、顺序性等）。信号时序逻辑（STL）作为TL的一个变体，具有定量语义（鲁棒值），可量化轨迹满足STL公式的程度。同时，决策Transformer（DT）在离线RL中展现了强大的序列建模能力。
- **核心目标**：将STL的表达式力与DT的序列建模能力相结合，提出**时序逻辑规范条件化决策Transformer（SDT）**，以解决涉及复杂时序约束的离线安全RL问题。

## 2. 方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：将离线安全RL视为有监督的序列建模问题，在DT的基础上额外引入两个输入token——**前缀鲁棒值**（prefix robustness）和**后缀鲁棒值**（suffix robustness），它们基于STL规范的定量语义，分别提供轨迹已发生部分和未来部分的约束满足信息。
- **关键技术细节**：
  - **STL鲁棒值计算**：STL的定量语义定义在公式(3)中，通过min/max操作嵌套得到轨迹在每个时刻的鲁棒值。前缀鲁棒值 $\rho_{pre}(\tau, t, \phi) = \rho(\tau_{1:t}, 1, \phi)$，后缀鲁棒值 $\rho_{suf}(\tau, t, \phi) = \rho(\tau_{t:T}, 1, \phi)$。
  - **输入序列**：在时间步 $t$，输入序列 $o_t$ 包含前缀 $\{P_{pre}\}$、后缀 $\{P_{suf}\}$、回报-去($R_{t-K:t}$)、状态 $s_{t-K:t}$ 和动作 $a_{t-K:t}$。
  - **策略表示**：采用高斯随机策略 $\pi_\theta(\cdot|o) = \mathcal{N}(\mu_\theta(o), \Sigma_\theta(o))$，训练目标为最大化条件对数似然加上熵正则化：
    $$\max_\theta \mathbb{E}_{o \sim \tau, \tau\sim D} \left[ \log \pi_\theta(a|o) + \lambda \mathcal{H}[\pi_\theta(\cdot|o)] \right].$$
  - **训练与评估**：训练时从数据集采样序列，用梯度下降优化损失。评估时（Algorithm 1）给定目标奖励和目标后缀（每个时间步预先指定，不能像回报-去那样自回归更新），策略生成动作。
  - **前缀与后缀的作用**：后缀提供未来信息但存在稀疏性问题（因STL的min/max操作使许多时刻的后缀值相同）、且无法像成本-去那样自回归更新。前缀补充了已发生的约束满足信息，两者结合可缓解稀疏性，并提供轨迹整体安全性的对比信息，提升策略学习。

## 3. 实验设计

- **环境与场景**：
  - 使用**Bullet-Safety-gym**基准中的三个任务：**Run**（快速移动但须在安全边界内且不超过速度阈值）、**Circle**（圆周运动但保持在安全区域内）、**Reach**（除Circle任务外还需顺序到达两个目标点）。
  - 机器人类型：Ball、Car、Drone、Ant。
- **STL规范**：
  - $\phi_{run}$：始终在边界内，若超速则需在5步内减速。
  - $\phi_{circle}$：若进入不安全区域，则需在5步内离开。
  - $\phi_{reach}$：满足$\phi_{circle}$的同时，按顺序到达两个目标。
- **数据集**：使用**DSRL**提供的离线数据集，并针对STL规范对成本进行重新标注（例如将连续5步违规标记为1）。注意，Reach环境因难以设计精确成本函数，仅使用鲁棒值进行训练。
- **对比基线**：
  - 约束优化方法：BCQ-Lagrangian、BEAR-Lagrangian、CPQ、COptiDICE。
  - 条件RL方法：CDT（使用成本-去）、RvS-RC（回报+成本）、RvS-R$\rho$（回报+前缀+后缀）、BC-Safe（仅使用满足规范的轨迹进行行为克隆）。
- **评估指标**：归一化累计奖励、累计重标成本（越低越好）、STL规范满足率（越高越好）。
- **计算资源**：论文中**未明确说明**使用的GPU型号、数量或训练时长，仅提及训练了200,000步以保证收敛。

## 4. 实验数量与充分性

- **实验数量**：
  - **主要实验**：在3个环境（Run/Circle/Reach）上，每种环境使用多种机器人，共9个子任务。每个实验使用3个随机种子、每个种子20条轨迹，结果取均值和标准差（Table 2）。
  - **对齐实验**（Fig. 2）：变化目标奖励和目标后缀，评估SDT和RvS-R$\rho$的实际后缀与奖励对齐情况。
  - **消融实验**（Fig. 4 left）：移除前缀或后缀，分析对性能的影响。
  - **目标后缀配置消融**（Fig. 4 right）：比较固定、线性、均值、最大值四种后缀配置。
  - **谓词缩放鲁棒性实验**（Table 3）：对不同的缩放因子($\alpha_b, \alpha_v$)测试。
  - **额外实验**（Appendix C）：在D4RL Gym环境上测试DT和带奖励前缀的DT。
- **充分性与公平性**：
  - 实验覆盖了多种任务、多种机器人、多种基线，横向比较全面。
  - 消融实验系统地解释了各组件贡献，满足率、成本、奖励多维度评价公平。
  - 但是，实验仅基于Bullet-Safety-gym这一基准，未在更广泛的离线安全RL基准（如SafetyGymnasium中的Goal/Button/Push）上验证，可能限制了泛化性。另外，未与最新的基于扩散模型或离线RL方法（如IQL、CQL）结合安全约束的变体进行比较。

## 5. 论文的主要结论与发现

- **性能优越**：SDT在所有环境中达到了最高的满足率和最低的成本，同时保持与安全基线相当甚至更高的奖励。相比之下，现有方法（如CDT、RvS-RC、CPQ、COptiDICE）由于非马尔可夫成本或模型限制，难以学到满足时序约束的策略。
- **对齐能力**：SDT可以随目标后缀的变化而调整实际行为，且当目标后缀设置为负值时仍能保持安全，展现出强对齐与泛化能力。而RvS-R$\rho$在高目标后缀或冲突目标时表现较差。
- **前缀和后缀的必要性**：去除前缀或后缀均导致满足率显著下降；后缀对安全影响更大。且引入前缀（奖励前缀）也能提升标准DT在D4RL上的性能。
- **对不同目标后缀配置的鲁棒性**：固定目标后缀（接近零的正值）在所有配置中表现最好；线性、均值、最大值配置因冲突目标或过激/保守行为导致满足率下降，但仍优于大多数基线。
- **对谓词缩放的鲁棒性**：缩放因子变化对SDT的奖励和满足率影响很小，表明SDT对STL内部谓词尺度不敏感。

## 6. 优点

- **方法创新**：首次将STL的定量语义融入DT的条件化框架，解决了离线安全RL中复杂时序约束的难题，超越了仅依赖马尔可夫成本的方法。
- **前缀+后缀设计**：有效缓解STL鲁棒值的稀疏性且提供互补信息，比单纯使用成本-去或回报-去更强大。
- **灵活的评估**：后缀可以作为超参数在推理时设定，无需重新训练，支持安全裕度的调整。
- **全面的实证验证**：在多个环境和多种机器人上，对安全、奖励、对齐、消融、缩放鲁棒性进行了系统评估，结果支持结论。
- **代码开源**（基于OSRL库和STLCG工具箱），可复现性强。

## 7. 不足与局限

- **计算资源未披露**：论文未报告GPU型号、训练时间等算力信息，不利于评估计算成本。
- **实验覆盖有限**：仅在Bullet-Safety-gym上进行测试，未在更丰富或高度随机的环境（如SafetyGymnasium的Goal/Button/Push）中验证，这些环境在先前文献中被提及存在噪声和随机性问题，可能影响RCSL方法的表现。
- **依赖预定义的STL规范**：需要领域专家手动设计STL公式，在实际应用中可能难以获得精确规范；且规范选择不当可能导致严重后果（论文在Impact Statement中提及）。
- **基线更新**：虽包含典型基线，但未与最近的一些离线安全RL工作（如使用扩散模型的方法）对比。
- **未讨论超参数敏感性**：例如目标后缀的固定值如何选择（实验中通过从安全轨迹中选取正的小值），未给出通用指导原则。
- **Reach环境缺少精确成本标签**：使部分基线无法评估，可能导致比较不完全公平。

---

（完）
