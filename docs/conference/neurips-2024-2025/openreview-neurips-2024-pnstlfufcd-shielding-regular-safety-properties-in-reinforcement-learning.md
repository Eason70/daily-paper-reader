---
title: Shielding Regular Safety Properties in Reinforcement Learning
title_zh: 强化学习中正则安全属性的屏蔽
authors: "Alex Goodall, Francesco Belardinelli"
date: 2024-05-15
pdf: "https://openreview.net/pdf?id=PnSTlFUfcd"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 具有可证明安全保证的强化学习屏蔽元算法
tldr: 现实部署强化学习需考虑安全约束。本文研究具有正则安全属性的强化学习，提出一种具有可证明安全保证的屏蔽元算法，在训练和部署期间防止智能体违反安全属性。在表格和深度强化学习设置中验证了有效性和可扩展性，为实际应用提供了可靠安全保障。
source: NeurIPS-2024-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-pnstlfufcd/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 426, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pnstlfufcd/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 720, \"height\": 707, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pnstlfufcd/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 719, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pnstlfufcd/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 388, \"height\": 388, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pnstlfufcd/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1087, \"height\": 1028, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pnstlfufcd/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 504, \"height\": 311, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pnstlfufcd/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1088, \"height\": 722, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pnstlfufcd/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 721, \"height\": 704, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pnstlfufcd/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 720, \"height\": 704, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pnstlfufcd/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 720, \"height\": 706, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pnstlfufcd/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 721, \"height\": 709, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pnstlfufcd/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 720, \"height\": 708, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-pnstlfufcd/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 491, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-pnstlfufcd/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 691, \"height\": 226, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-pnstlfufcd/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1378, \"height\": 258, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-pnstlfufcd/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1378, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-pnstlfufcd/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1380, \"height\": 766, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-pnstlfufcd/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1382, \"height\": 1581, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-pnstlfufcd/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1281, \"height\": 518, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-pnstlfufcd/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1384, \"height\": 707, \"label\": \"Table\"}]"
motivation: 现有强化学习忽略安全属性，难以在真实世界部署。
method: 提出基于屏蔽的元算法，确保强化学习满足正则安全属性。
result: 在表格和深度强化学习环境中均实现了可证明的安全保证。
conclusion: 该框架为强化学习部署提供了有效的安全保障方法。
---

## Abstract
To deploy reinforcement learning (RL) systems in real-world scenarios we need to consider requirements such as safety and constraint compliance, rather than blindly maximizing for reward. In this paper we study RL with regular safety properties. We present a constrained problem based on the satisfaction of regular safety properties with high probability and we compare our setup to the some common constrained Markov decision processes (CMDP) settings. We also present a meta-algorithm with provable safety-guarantees, that can be used to shield the agent from violating the regular safety property during training and deployment. We demonstrate the effectiveness and scalability of our framework by evaluating our meta-algorithm in both the tabular and deep RL setting.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究动机**：现实世界中的强化学习（RL）部署需要满足安全性与约束要求，而传统的 RL 一味追求最大化奖励，忽略了安全风险。现有的约束马尔可夫决策过程（CMDP）框架存在局限性：约束违规仅在期望意义上得到保证，而非高概率；约束阈值缺乏语义含义且难以调节；成本函数通常是马尔可夫的，无法表达非马尔可夫的正则安全属性。
- **整体含义**：论文旨在提出一种可证明安全保证的 RL 框架，使智能体在训练和部署过程中不违反正则安全属性（regular safety properties）。正则安全属性通过确定性有限自动机（DFA）定义坏前缀，能够表达丰富的时态逻辑约束，如“永远避免绿色状态”或“到达目标后必须在10步内到达蓝色状态”。

## 2. 方法论：核心思想、关键技术细节与算法流程

### 核心思想
- 采用**屏蔽（Shielding）** 方法：在运行时使用模型检查（model checking）评估当前状态的有限步内违反安全属性的概率，若超过阈值则启用一个“备份策略”（backup policy）来代理动作，从而保证安全。
- 将安全属性与奖励目标分离为两个独立策略：**任务策略**（task policy）最大化奖励，**备份策略**最小化成本（即违反安全属性的概率）。

### 关键技术细节
1. **问题定义（Problem 4.1）**：  
   - 最大化期望累积奖励，同时约束每一步的有限步可达安全违规概率不超过 \(p_1\)，即 \(\Pr(\langle s_t, q_t\rangle \models \Diamond^{\le H} \text{accept}) \le p_1\)。
   - 通过产品马尔可夫链（Product Markov Chain）将安全属性的满足概率转化为有界可达概率。

2. **模型检查过程**：
   - **精确模型检查**：当已知真实转移概率时，可通过解线性方程或矩阵乘法计算。（时间复杂度为 O(poly(size)×H)）
   - **蒙特卡洛模型检查**：当仅有黑箱模拟器时，通过采样路径估计概率，并使用 Hoeffding 不等式保证误差（样本量 \(m \ge \frac{1}{2\epsilon^2}\log\frac{2}{\delta}\)）。
   - **近似模型检查**：使用学习得到的近似动力学模型（如最大似然估计），结合上述两种方法。

3. **屏蔽元算法**（Algorithm 1）：
   - 初始化：任务策略 \(\pi_{\text{task}}\)、备份策略 \(\pi_{\text{safe}}\)、近似模型 \(\hat{P}\)。
   - 每个时间步：采样动作 \(a \sim \pi_{\text{task}}\)，若 \(\Pr(\langle s,q\rangle \models \Diamond^{\le H}\text{accept}) > p_1\) 则改用 \(\pi_{\text{safe}}\)；否则执行 \(a\)。
   - 更新：用 RL 更新任务策略和备份策略，更新近似模型。

4. **安全保证（Theorem 6.5）**：
   - 在假设存在非临界状态与不可恢复状态、备份策略满足安全阈值的前提下，若每个状态-动作对被访问足够多次（涉及样本复杂度 \(O\left(\frac{H^2 |S|^2}{\epsilon^2}\log\frac{|A||S|^2}{\delta}\right)\)），则系统以高概率满足约束。

## 3. 实验设计

### 场景与数据集
1. **表格强化学习（Tabular RL）**：  
   - 环境：“颜色网格世界”（9×9 网格），智能体从一角出发到达另一角获取奖励，状态包含颜色标记（绿色、蓝色、紫色）。
   - 安全属性（3种）：
     - (1) \(\square \lnot \text{green}\)：永远避免绿色状态。
     - (2) \(\square(\text{goal} \rightarrow \Diamond^{\le 10}\text{blue})\)：到达目标后10步内必须到达蓝色。
     - (3) \(\square(\text{goal} \rightarrow \Diamond^{\le 10}\square^{\le 5}\text{purple})\)：到达目标后10步内到达紫色并保持5步。
   - 环境随机性：以概率 \(p\) 随机覆盖动作（\(p\) 值分别为 0.25、0.25、0.1）。

2. **深度强化学习（Deep RL）**：  
   - 环境：Atari Seaquest（ALE 平台），部分可观测像素输入。
   - 安全属性：
     - (1) 避免在水面下无潜水员时上浮、避免缺氧、避免被击中。
     - (2) 一旦有潜水员，必须在30步内上浮。

### 对比方法
- **Baseline 1**：普通 Q-learning / DreamerV3（无安全惩罚）。
- **Baseline 2**：带惩罚的 Q-learning（在成本函数上惩罚违规，使用反事实经验加速学习）。
- **Baseline 3**：带增广拉格朗日法的 DreamerV3（Lagrangian DreamerV3）。

### 评估指标
- 累积奖励（reward）
- 违规次数或违反率（cost/violation rate）

## 4. 资源与算力

- **硬件**：2 块 NVIDIA Tesla A30（24GB RAM）GPU；24 核 / 48 线程 Intel Xeon CPU；32GB RAM。
- **训练时长**：
  - 表格实验：每个运行从几分钟到约 1.5 天（取决于安全属性复杂度）。
  - Deep RL Seaquest 实验：每运行约 8 小时到 1 天；屏蔽方法比普通 DreamerV3 慢约 2 倍。
- **显存要求**：使用 DreamerV3 xlarge 配置时，需约 32GB GPU 显存。
- **说明**：附录 E 提供了完整细节。

## 5. 实验数量与充分性

- **实验数量**：每组实验均报告 5 个随机种子的结果（误差带为 95% 自助法置信区间）。
- **覆盖范围**：
  - 表格环境：3 种安全属性，每种对比 3 种方法（共 3×3=9 组主要实验）。
  - 附录 F 包含大量消融实验：反事实经验、精确模型检查 vs 蒙特卡洛、成本系数 C、模型检查地平线 H、环境随机性 p 的影响。
  - Deep RL 环境：2 种安全属性 × 3 种方法 = 6 组主要实验。
- **公平性与客观性**：方法超参数通过前期统计确定（如最大满足概率）；基线方法使用常见配置；消融实验充分探讨了关键超参数的敏感性；实验设计合理，数据充分。

## 6. 主要结论与发现

1. 所提出的屏蔽元算法在表格和深度 RL 设置中均能有效平衡奖励最大化与安全属性满足。
2. 相比普通无安全考虑的 RL 和有惩罚的 RL，屏蔽方法在安全性能上显著优越，同时保持了相当的任务奖励。
3. 将奖励与安全分离为两个策略是有效的，备份策略能够快速引导系统回到安全状态。
4. 安全属性越复杂（如含时间约束），屏蔽方法的优势越明显。
5. 理论安全保证在合理假设下成立，且实验验证了实际接近理论预测。

## 7. 优点

- **理论扎实**：给出了有限步正则安全属性的概率约束定义，并建立了与多种 CMDP 约束（期望累积、概率累积、即时约束）的等价关系（Theorem 4.7 及附录 G）。
- **可证明安全**：提出了在表格设置下具有高概率安全保证的样本复杂度上界（Theorem 6.5）。
- **灵活模型检查**：支持精确、蒙特卡洛、近似模型检查，适应不同场景（已知/未知/近似动力学）。
- **可扩展性**：在深度 RL 中结合 DreamerV3 世界模型成功应用于 Atari Seaquest，表明框架可扩展到高维视觉输入环境。
- **消融实验充分**：对关键超参数（H, p1, C, 随机性）进行了系统分析，验证了方法的稳健性。

## 8. 不足与局限

- **收敛性与分离问题**：完全分离任务策略与备份策略可能导致二者争夺控制权，损失渐进收敛保证（类似分层 RL 问题）。作者提及可能需要轻度耦合策略。
- **对模型检查地平线 H 敏感**：H 设置过大可能导致过度保守，牺牲奖励；附录 F.4 提出了可恢复性改进，但仍有性能下降。
- **假设较强**：理论保证依赖不可恢复状态存在、备份策略满足阈值等假设，实际中可能难以严格满足。
- **计算开销**：在深度 RL 中屏蔽方法使训练时间翻倍；对状态空间较大或 DFA 复杂时，模型检查可能成为瓶颈。
- **实验场景有限**：表格环境仅为一个简单的网格世界；深度 RL 仅测试了 Atari Seaquest，缺乏更复杂连续控制或多智能体场景。
- **随机性处理**：实验环境随机性较低（\(p\le0.25\)），更高随机性下方法表现未充分验证。

（完）
