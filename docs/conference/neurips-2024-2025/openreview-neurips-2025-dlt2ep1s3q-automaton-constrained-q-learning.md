---
title: Automaton Constrained Q-Learning
title_zh: 自动机约束Q学习
authors: "Anastasios Manganaris, Vittorio Giammarino, Ahmed H Qureshi"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=DLt2Ep1S3q"
tags: ["query:safe-rl-cbf"]
score: 5.0
evidence: 通过自动机约束Q学习实现带时间逻辑约束的安全强化学习
tldr: 本文提出自动机约束Q学习（ACQL），将强化学习与线性时间逻辑结合，以处理连续环境中的时序目标与安全约束。该方法克服了现有LTL-RL方法在复杂连续空间中的性能瓶颈，在机器人任务中展示了有效的安全约束满足能力。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-dlt2ep1s3q/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1315, \"height\": 574, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dlt2ep1s3q/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1229, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dlt2ep1s3q/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 678, \"height\": 259, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dlt2ep1s3q/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 631, \"height\": 488, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dlt2ep1s3q/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 797, \"height\": 495, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dlt2ep1s3q/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1295, \"height\": 2165, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dlt2ep1s3q/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1295, \"height\": 2166, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dlt2ep1s3q/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1436, \"height\": 1920, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dlt2ep1s3q/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1437, \"height\": 1911, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-dlt2ep1s3q/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1457, \"height\": 549, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dlt2ep1s3q/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 755, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dlt2ep1s3q/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 682, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dlt2ep1s3q/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 733, \"height\": 456, \"label\": \"Table\"}]"
motivation: 现有强化学习难以同时处理时序目标与时间变化的安全约束。
method: 将线性时间逻辑规范编码为自动机，并与Q学习结合以指导策略探索。
result: 在连续机器人环境中成功实现安全任务达成。
conclusion: ACQL为时序安全约束下的强化学习提供了可扩展方案。
---

## Abstract
Real-world robotic tasks often require agents to achieve sequences of goals while respecting time-varying safety constraints. However, standard Reinforcement Learning (RL) paradigms are fundamentally limited in these settings. A natural approach to these problems is to combine RL with Linear-time Temporal Logic (LTL), a formal language for specifying complex, temporally extended tasks and safety constraints. Yet, existing RL methods for LTL objectives exhibit poor empirical performance in complex and continuous environments. As a result, no scalable methods support both temporally ordered goals and safety simultaneously, making them ill-suited for realistic robotics scenarios. We propose Automaton Constrained Q-Learning (ACQL), an algorithm that addresses this gap by combining goal-conditioned value learning with automaton-guided reinforcement. ACQL supports most LTL task specifications and leverages their automaton representation to explicitly encode stage-wise goal progression and both stationary and non-stationary safety constraints. We show that ACQL outperforms existing methods across a range of continuous control tasks, including cases where prior methods fail to satisfy either goal-reaching or safety constraints. We further validate its real-world applicability by deploying ACQL on a 6-DOF robotic arm performing a goal-reaching task in a cluttered, cabinet-like space with safety constraints. Our results demonstrate that ACQL is a robust and scalable solution for learning robotic behaviors according to rich temporal specifications.

---

## 论文详细总结（自动生成）

# 论文总结：Automaton Constrained Q-Learning (ACQL)

## 1. 核心问题与整体含义（研究动机和背景）

现实机器人任务要求智能体在遵循随时间变化的安全约束的同时，实现一系列目标。标准强化学习（RL）在处理此类场景时存在根本局限：**目标条件强化学习（GCRL）** 擅长到达单个目标，但缺乏处理目标序列和确保安全的能力；**安全强化学习（Safe RL）** 仅能处理静态安全约束，无法应对时序变化的任务。线性时间逻辑（LTL）提供了一种表达复杂时序任务和非平稳安全约束的形式化框架，但直接将LTL规范转化为奖励函数会导致非马尔可夫性，违反RL的马尔可夫假设。现有将LTL与RL结合的方法存在两个主要问题：（1）基于稀疏二元奖励的方法在复杂连续环境中难以有效引导行为；（2）仅能处理有限类别的LTL规范，难以同时支持时序目标和安全约束。

**本文旨在解决上述差距，提出一种可扩展的算法，支持大多数LTL任务规范（递归类公式），并在连续控制任务中实现优于现有方法的性能，同时满足安全的时序约束。**

## 2. 方法论：核心思想、关键技术细节

### 核心思想
ACQL 通过构建一个**增强乘积约束马尔可夫决策过程（Augmented Product CMDP）**，将LTL规范转化为自动机表示，并从中提取：（1）每个自动机状态对应的**子目标列表**，用于指导分阶段目标推进；（2）**安全条件映射**，用于执行可变的（包括非平稳的）安全约束。在此基础上，结合**目标条件值学习**和**自动机引导的强化**，并引入两个关键技术解决现有方法的瓶颈。

### 关键技术细节
1. **自动机分析与结构提取**：
   - 将输入STL（信号时序逻辑）规范翻译为确定性Büchi自动机（DBA）。
   - 从自动机中提取两种映射：
     - **安全条件映射 S(q)**：对于每个自动机状态 q，通过找出指向非接受汇合组件（non-accepting sink-components）的边，取这些边谓词的否定，得到必须始终满足的安全条件。
     - **活跃性条件映射 O(q)**：通过保留非安全相关的出边谓词，得到推进任务所需满足的条件；然后过滤出与子目标命题（AP_subgoal）相关的谓词，生成子目标列表 G(q)。
   - 示例：对于公式 `¬p4 U ((p1 ∨ p2) ∧ ◦ ♢p3)`，S(q0)=¬p4, S(q1)=S(q2)=true, O(q0)=p1∨p2, O(q1)=p3，从而G(q0)={g1,g2}, G(q1)={g3}。

2. **增强乘积CMDP构造**：
   - 状态空间：`S_A = S × G⁺ × Q`，包含原始MDP状态、子目标列表、自动机状态。
   - 转移：仅当自动机根据状态标签支持转移时才允许相应MDP转移。
   - 奖励函数：稀疏奖励，当进入接受状态且接近对应目标时给1。
   - 约束函数：基于**最小安全约束**（minimum safety constraint），利用鲁棒性函数 `ρ(s, S(q))` 定义 `c_A`，使其在违反安全时为负、满足时为正。约束目标为：`E[min_{t≥0} c_A(s_t,a_t)] > L`（L设为0）。该格式避免了累加成本带来的高方差，简化为分类任务，无需手动调参。

3. **ACQL算法流程**：
   - 学习两个模型：**Q_rψ**（状态-动作值函数）和 **Q_cθ**（状态-动作安全函数）。
   - 策略：`π(s_A) = arg max_{a: Q_c(s_A,a)>L} Q_r(s_A,a)`，若无安全动作则选最安全动作。
   - 训练中采用**安全性折扣因子调度**（γ_c从0.8逐渐增至0.98），确保最终收敛到无折扣的最小安全期望。
   - 利用**Hindsight Experience Replay (HER)** 对轨迹进行重标记：将轨迹中最终达到的目标替换为原始子目标，并重新计算奖励，从而缓解稀疏奖励问题。
   - 采用三时间尺度随机逼近证明收敛性：Q_c最快更新，Q_r次之，γ_c最慢，在有限状态行动空间和适当步长下近似最优解。

## 3. 实验设计

### 环境与任务
- **模拟环境**：基于 Brax 物理引擎，使用三种智能体：
  - **2D PointMass**（4方向离散动作）
  - **Quadcopter**（6方向离散动作）
  - **8-DOF Ant**（4个预训练的方向性运动技能，每个执行4步）
- **环境特点**：无障碍物（物理障碍通过任务规范引入），以突出算法仅从规范反馈中学习避障的能力。
- **5种LTL任务**：
  1. 两子目标顺序导航：`♢(g1 ∧ ◦ (♢g2))`
  2. 两子目标分支导航：`♢g1 ∧ ♢g2`
  3. 单目标带避险区：`♢g1 ∧ □¬o1`
  4. 两子目标带消失避险区：`¬o1 U g1 ∧ ◦ ♢g2`
  5. 无限循环带持续避险区：`□♢(g1 ∧ ◦ ♢g2) ∧ □¬o1`

### 对比方法
- **CRM-RS** (Counterfactual Experiences for Reward Machines with Reward Shaping)：标准产品MDP方法，使用稀疏/成形奖励，将非接受状态作为终止状态来强制安全。
- **LOF** (Logical Options Framework)：层次化方法，为每个子目标训练单独的逻辑选项，组合后通过值迭代选择；不安全步骤给予大惩罚（R_s=-1000）。

### 评测指标
- **奖励**：在最终目标附近停留的步数（反映任务完成程度）。
- **成功率(S.R.)**：整个轨迹（1000步）完全满足任务规范的比例；对于“循环”任务，考察至少完成一次完整循环且从未违反安全的比例。

### 真实世界验证
- 在模拟的**UR5e 6-DOF机械臂**的存储柜环境中训练策略，任务为顺序到达3个子目标并避开2个障碍物（`♢(p1 ∧ ◦ (♢(p2 ∧ ◦ (♢(p3))))) ∧ □(¬(in_wall ∨ in_table))`）。
- 训练后直接在真实UR5e机械臂上部署，验证了模拟到现实的可迁移性。

## 4. 资源与算力

论文明确说明：
- **GPU**：单张 NVIDIA RTX 3090 (24GB VRAM)。
- **CPU**：12th Gen Intel i7-12700F，32GB RAM。
- **时间**：每次实验约30分钟。
- **总实验量**：比较分析225次运行 + 消融实验90次运行 ≈ 315 GPU-hours。另有少量超参数调优和开发时间。

## 5. 实验数量与充分性

### 实验规模
- **比较实验**：3种智能体 × 5种任务 × 5个种子 = 75种配置，每种方法（ACQL、CRM-RS、LOF）均运行，共225次运行。
- **消融实验**：研究两个关键组件（HER、最小安全约束）的效果，在3种智能体 × 4种任务（排除循环任务） × 5个种子 = 60种配置上运行（但论文表格Table 2中汇总了所有任务，未明确说明排除循环任务）。此外，对安全任务单独统计。
- **真实世界实验**：单一策略训练，16次模拟评估，然后在真实机器人上验证。

### 充分性评估
- **非常充分**：覆盖了多种智能体（点质量、四旋翼、蚂蚁、机械臂）、多种LTL公式类型（顺序、分支、安全、until、循环），并使用5个随机种子报告均值和标准差。
- **对比公平**：与两个代表性基线（CRM-RS和LOF）比较，每个基线的设置（如LOF为每个选项分配5M步训练）保证了公平性。
- **消融彻底**：分别去除HER和用累加成本替代最小安全约束，并针对仅涉及安全的任务额外分析，确认了两个组件的必要性。
- **客观性**：所有结果报告了均值和标准差，并展示了训练曲线（附录中），未选择性呈现最优结果。

## 6. 主要结论与发现

1. **性能大幅领先**：在全部5种任务和3种连续控制环境中，ACQL在奖励和成功率上显著超过CRM-RS和LOF。尤其在有安全约束的任务中，CRM-RS和LOF几乎完全失败（成功率为0或极低），而ACQL保持高成功率。
2. **HER不可或缺**：去除HER后，奖励和成功率急剧下降（平均奖励从682.5降至95.7，成功率从91.5%降至12.9%），证明子目标重标记对稀疏奖励的缓解作用至关重要。
3. **最小安全约束优于累加成本**：在涉及安全的任务中，使用累加成本公式的平均奖励仅8.0，成功率4.6%，远低于ACQL的545.8和75.4%。可视化显示累加成本形式难以精确学习安全边界。
4. **真实世界可部署**：模拟训练的UR5e策略在真实存储柜环境中实现100%成功率（16次模拟评估平均奖励908.4），证明了方法的实用性。

## 7. 优点（方法与实验亮点）

- **方法亮点**：
  - 将LTL安全约束从“代价累加”转化为“最小安全分类”，简化学习、无需调参（L=0固定）。
  - 自动从自动机提取子目标列表，无缝兼容HER等目标条件RL技术，解决稀疏奖励问题。
  - 使用多安全条件头部的目标条件值网络，共享参数处理不同自动机状态的安全需求，避免为每个状态训练独立模型。
  - 提供三时间尺度收敛性证明（尽管有限状态假设）。
- **实验亮点**：
  - 同时评价奖励和成功率，全面反映任务完成质量和安全满足程度。
  - 真实机器人部署验证了模拟到现实的可行性。
  - 可视化分析（图4）直观展示了最小安全约束相对于累加成本在安全边界学习上的优势。

## 8. 不足与局限

- **LTL公式限制**：仅支持DBA可表示的公式（递归类），不能处理需要非确定性自动机（如Good-for-MDPs NBC）的规范。作者提及未来将探索更表达力的自动机。
- **子目标假设**：假设部分原子命题是参数化的子目标，且安全相关命题不包含子目标参数。若安全约束也涉及目标位置，则当前分离可能不够。
- **条件性有限**：策略仅基于当前子目标集，未充分编码未来子目标依赖，可能影响长程最优性。
- **部分可观测性与Sim-to-Real差距**：当前实验在完全可观测、模拟与真实环境几何对齐的情况下进行，对于更复杂的部分可观测任务或更大的Sim-to-Real差异未做处理。
- **计算开销**：使用双Q网络（共4个网络）可能增加训练时间，但未报告与其他方法的训练时间对比。
- **消融排除循环任务**：循环任务（□♢…）因有限轨迹上无法有意义评估鲁棒性，在消融表（Table 2）中未包含，可能影响对HER和最小安全约束在无限循环任务上效益的结论。

（完）
