---
title: Efficient Policy Optimization in Robust Constrained MDPs with Iteration Complexity Guarantees
title_zh: 具有迭代复杂度保证的鲁棒约束MDP高效策略优化
authors: "Sourav Ganguly, Kishan Panaganti, Arnob Ghosh, Adam Wierman"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=3MiADMHY62"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 鲁棒约束马尔可夫决策过程用于安全策略优化
tldr: 本文研究鲁棒约束马尔可夫决策过程，代理在模型不确定性下最大化累积奖励同时满足约束。提出高效的原始-对偶算法并给出迭代复杂度保证，为安全策略优化提供了理论基础。实验表明该方法在鲁棒性方面优于现有方法。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-3miadmhy62/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1290, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3miadmhy62/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1288, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3miadmhy62/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1390, \"height\": 570, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3miadmhy62/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1379, \"height\": 516, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3miadmhy62/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1390, \"height\": 571, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3miadmhy62/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1398, \"height\": 569, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3miadmhy62/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 649, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3miadmhy62/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1370, \"height\": 562, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3miadmhy62/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1365, \"height\": 567, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3miadmhy62/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1365, \"height\": 559, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-3miadmhy62/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1111, \"height\": 305, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3miadmhy62/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 964, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3miadmhy62/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 585, \"height\": 303, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3miadmhy62/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1073, \"height\": 468, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3miadmhy62/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1059, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3miadmhy62/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 765, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3miadmhy62/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1534, \"height\": 553, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3miadmhy62/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 758, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3miadmhy62/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1075, \"height\": 467, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3miadmhy62/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1075, \"height\": 467, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3miadmhy62/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1599, \"height\": 350, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3miadmhy62/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1126, \"height\": 269, \"label\": \"Table\"}]"
motivation: 现实控制系统中模拟环境与真实环境存在差距，需要鲁棒的安全决策。
method: 采用原始-对偶方法处理鲁棒约束MDP，并分析迭代复杂度。
result: 在多个基准问题上验证了算法的高效性和鲁棒性。
conclusion: 该方法为鲁棒安全策略学习提供了理论保证。
---

## Abstract
Constrained decision-making is essential for designing safe policies in real-world control systems, yet simulated environments often fail to capture real-world adversities. We consider the problem of learning a policy that will maximize the cumulative reward while satisfying a constraint, even when there is a mismatch between the real model and an accessible simulator/nominal model. In particular, we consider the robust constrained Markov decision problem (RCMDP) where an agent needs to maximize the reward and satisfy the constraint against the worst possible stochastic model under the uncertainty set centered around an unknown nominal model.  Primal-dual methods, effective for standard constrained MDP (CMDP), are not applicable here because of the lack of the strong duality property. Further, one cannot apply the standard robust value-iteration based approach on the composite value function, either, as the worst-case models may be different for the reward value function and the constraint value function. We propose a novel technique that effectively minimizes the constraint value function--to satisfy the constraints; on the other hand, when all the constraints are satisfied, it can simply maximize the robust reward value function. We prove that such an algorithm finds a policy with at most $\epsilon$ sub-optimality and a feasible policy after $O(\epsilon^{-2})$ iterations. In contrast to the state-of-the-art method, we do not need to employ a binary search; thus, we reduce the computation time and achieve a better performance, especially for continuous state-space.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：现实控制系统（如自动驾驶）对安全性要求极高，强化学习（RL）策略需在模拟器中训练后部署到真实环境。然而，模拟器（标称模型）与真实环境之间存在模型失配（sim-to-real gap），导致在模拟中满足安全约束的策略在真实环境中可能违反约束。因此，需要一种**鲁棒约束马尔可夫决策过程（RCMDP）**，使得策略在最坏情况下的随机模型（位于以未知标称模型为中心的 uncertainty set 内）下仍能最大化累积奖励并满足约束。
- **挑战**：标准约束MDP（CMDP）可通过原始-对偶方法求解，但RCMDP因占据测度非凸、最坏模型随策略变化，导致强对偶性不成立，原始-对偶方法失效。同时，复合值函数的鲁棒值迭代也不可行。现有方法（EPIRC-PGS）采用epigraph形式与二分搜索，但需要大量计算（尤其是折扣因子γ大时），且二分搜索对噪声敏感，不适用于大状态空间。
- **目标**：提出一种无需二分搜索、迭代复杂度更优（O(ϵ⁻²)）的算法，同时保证策略的可行性（严格满足约束）与近最优性。

### 2. 方法论：核心思想、关键技术细节、公式与算法流程

- **核心思想**：将RCMDP问题转化为一个新的优化形式：
  \[
  \min_{\pi} \max\left\{ \frac{J^{c_0}_\pi}{\lambda},\ \max_{n} (J^{c_n}_\pi - b_n) \right\}
  \]
  其中 \( J^{c_0}_\pi \) 为目标值函数，\( J^{c_n}_\pi \) 为第n个约束值函数，\( b_n \) 为阈值，λ为缩放因子。当约束满足时，第二项为负，优化聚焦于最小化目标；当约束违反时，第二项主导，优化转向减小约束违反。该形式避免了二分搜索，且通过选择合适的λ（如λ=2H/ξ，其中ξ为严格可行性参数），可保证最终策略的可行性。
- **算法流程（RNPG）**：
  1. 初始化策略为均匀分布。
  2. 每轮迭代中，利用鲁棒策略评估器（Robust Policy Evaluator，基于KL散度等不确定性集）计算当前策略下各值函数及其梯度。
  3. 选择当前要优化的 index：\( i_t = \arg\max\{ J^{c_0}_\pi/\lambda,\ \{J^{c_n}_\pi - b_n + \xi\} \}\)。
  4. 使用自然策略梯度（Natural Policy Gradient，基于KL散度正则项）更新策略：
     \[
     \pi_{t+1,s} = \arg\min_{\pi_s \in \Delta_A} \{ \langle Q^{i_t}_{\pi_t,p_t}, \pi_s\rangle + \frac{1}{\alpha_t} \text{KL}(\pi_s \| \pi_{t,s}) \},\ \forall s
     \]
     其中 \( p_t \) 为最坏情形转移概率，\( Q^{i_t} \) 为对应的鲁棒Q值。
  5. 迭代T步后输出使得 surrogate objective \(\max\{J^{c_0}_\pi/\lambda,\ \max_n(J^{c_n}_\pi - b_n + \xi)\}\) 最小的策略。
- **理论保证**：在严格可行性假设（Assumption 1）、协方差支撑假设（Assumption 2）及均匀最小化假设（Assumption 3）下，RNPG经 \( O(\epsilon^{-2}\xi^{-2}(1-\gamma)^{-2}(1-\beta)^{-2}S\log|A|) \) 次迭代得到ϵ-最优且可行的策略（Theorem 4.1）。若未知ξ，则经 \( O(\epsilon^{-4}) \) 次迭代得到ϵ-最优且ϵ-违反策略（Theorem 6.1）。
- **扩展至函数逼近**：提出鲁棒约束Actor-Critic（RCAC），利用积分概率度量（IPM）不确定性集，引入鲁棒Bellman算子中的正则项，适用于连续状态空间。

### 3. 实验设计：数据集/场景、benchmark、对比方法

- **场景与数据集**：
  - 有限状态-动作空间：**Garnet(15,20)**（15状态20动作）、**Constrained River-swim (CRS)**（6状态）、**Modified Frozenlake**（4×4网格）、**Garbage collector**（4×4网格，动态障碍物）。
  - 连续状态空间：**Cartpole-v1**（gymnasium库）。
- **Benchmark**：主要对比 **EPIRC-PGS**（[Kitamura et al., 2024]），以及 **RPPG**（本文提出的ℓ₂正则化版本）、**Robust CRPO**（鲁棒版本的CRPO）、**CAC**（标准约束Actor-Critic，非鲁棒）。
- **评估指标**：累积奖励（目标函数值）、累积约束成本、壁钟时间（wall-clock time）、可行性和违反程度。

### 4. 资源与算力

- 文中未明确说明使用的GPU型号、数量或具体训练时长。仅在Table 1和文本中给出了各环境在不同算法下的壁钟时间（秒），但未提供硬件配置细节（除脚注1提到：Intel Core i7-14700 2.10GHz, 32GB RAM, 64位操作系统，无GPU）。因此，**算力资源仅涉及CPU，未使用GPU**。

### 5. 实验数量与充分性

- **实验覆盖**：在4个有限状态环境（CRS, Garnet, Frozenlake, Garbage collector）和1个连续状态环境（Cartpole）上进行了测试。每个环境均比较了RNPG、RPPG、EPIRC-PGS，并在Cartpole上额外对比了Robust CRPO和CAC。
- **参数与配置**：统一设置γ=0.99，RNPG中λ固定为50（无需调参），EPIRC-PGS使用内外循环（K=10, T=100）。提供了完整的超参数表（附录E）。
- **充分性**：实验覆盖了不同规模（小至6状态，大至15状态）和不同特性（随机障碍、动态环境）的任务，并比较了多种基线。但缺少“多次运行取平均”的误差棒或置信区间（文中提到“single run”），可能影响统计显著性。此外，仅对RNPG进行了λ敏感性分析（图4），未对学习率等关键参数进行系统的消融实验。

### 6. 论文的主要结论与发现

- RNPG在**所有有限状态环境中均能学到可行（满足约束）且奖励更优的策略**，而EPIRC-PGS在CRS和Garbage collector中违反约束，在Garnet和Frozenlake中虽可行但奖励低于RNPG。
- RNPG的**计算时间远快于EPIRC-PGS**：在CRS上，γ=0.99时快约4.7倍；在Garnet上快约3.7倍；且随着γ增大（接近1），EPIRC-PGS时间急剧增加，RNPG受影响较小。
- **KL正则化的自然梯度优于ℓ₂正则化的投影梯度**：RNPG比RPPG更稳定、约束违反更小、奖励更高。
- 连续状态空间的RCAC在Cartpole测试中，**在模型失配环境下唯一能同时保持可行性和高奖励**，而CAC（非鲁棒）约束违反严重，Robust CRPO轻微违反且奖励较低，EPIRC-PGS无法收敛。

### 7. 优点

- **理论创新**：提出新的surrogate优化形式，避免了二分搜索，给出严格的迭代复杂度界（O(ϵ⁻²)），优于前人工作的O(ϵ⁻⁴)。
- **算法简洁高效**：RNPG无需调参λ（固定较大值即可），计算效率显著提升。
- **鲁棒性**：理论保证在严格可行性条件下得到**零违反**策略，实验也验证了其在不确定性环境下的可行性。
- **扩展性强**：方法可推广至IPM不确定性集和函数逼近，提出实用的RCAC算法，且实验成功。

### 8. 不足与局限

- **理论假设较强**：Assumption 1（严格可行性且ξ已知）在现实中难以获取；Assumption 2（转移概率支撑包含）可能不满足；Assumption 3（均匀最小化）进一步限制了适用范围。
- **实验局限性**：所有实验仅执行单次运行，缺乏统计误差分析；未对学习率、KL正则化系数等超参数进行系统性消融研究；连续状态实验（Cartpole）中的扰动仅为均匀噪声，缺乏更复杂的对抗性不确定性。
- **实际应用距离**：当前工作仍限于中等规模离散状态或简单连续控制问题，未验证在大规模复杂任务（如机器人、自动驾驶）上的可扩展性。
- **鲁棒策略评估器假设**：算法依赖高效鲁棒评估器，虽然对于常见不确定性集（KL、TV等）已有研究，但在实际部署中仍需额外的样本和计算开销。

（完）
