---
title: Provably Efficient RL under Episode-Wise Safety in Constrained MDPs with Linear Function Approximation
title_zh: 线性函数逼近下每回合安全约束的CMDP中可证明高效的强化学习
authors: "Toshinori Kitamura, Arnob Ghosh, Tadashi Kozuno, Wataru Kumagai, Kazumi Kasaura, Kenta Hoshino, Yohei Hosoe, Yutaka Matsuo"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=rgoSyTCTkn"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 线性MDP中每回合零违反的安全强化学习
tldr: 线性函数逼近下的安全强化学习理论结果稀少。本文提出首个针对线性CMDP的RL算法，实现每回合零违反保证并达到O(√K)遗憾界，计算复杂度与状态空间大小无关，填补了理论空白。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-rgosytctkn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1412, \"height\": 1356, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-rgosytctkn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1421, \"height\": 277, \"label\": \"Table\"}]"
motivation: 线性CMDP中安全RL的理论保证研究不足。
method: 设计一种线性CMDP算法，同时保证每回合零违反和次线性遗憾。
result: 算法实现O(√K)遗憾且每回合零违反，计算高效。
conclusion: 为线性函数逼近下的安全RL提供了首个可证明高效的解决方案。
---

## Abstract
We study the reinforcement learning (RL) problem in a constrained Markov decision process (CMDP), where an agent explores the environment to maximize the expected cumulative reward while satisfying a single constraint on the expected total utility value in every episode. While this problem is well understood in the tabular setting, theoretical results for function approximation remain scarce. This paper closes the gap by proposing an RL algorithm for linear CMDPs that achieves $\widetilde{\mathcal{O}}(\sqrt{K})$ regret with an episode-wise zero-violation guarantee. Furthermore, our method is computationally efficient, scaling polynomially with problem-dependent parameters while remaining independent of the state space size. Our results significantly improve upon recent linear CMDP algorithms, which either violate the constraint or incur exponential computational costs.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究问题**：在约束马尔可夫决策过程（CMDP）中，智能体需要在每一回合满足预期累计效用的单个约束（每回合零违反），同时最大化累计奖励。  
- **背景**：该问题在表格型状态空间（tabular）中已有完善的理论结果（如 $\widetilde{\mathcal{O}}(\sqrt{K})$ 遗憾和零违反），但在大规模函数逼近场景（如线性MDP）中理论结果极少。  
- **动机**：现有线性CMDP算法要么违反约束（如Ghosh et al. 2024），要么产生指数级计算成本。因此，核心挑战是设计一个**计算高效**且**每回合零违反**的线性CMDP算法，并证明其**次线性遗憾**。

### 2. 论文提出的方法论：核心思想、关键技术细节、算法流程（文字说明）

- **核心思想**：采用**乐观-悲观（Optimistic-Pessimistic）探索框架**，结合 **softmax策略** 与 **安全策略 $\pi_{\text{sf}}$ 的智能部署** 实现约束满足和高效探索。
- **关键技术细节**：
  - **线性CMDP假设**：状态-动作对通过已知特征映射 $\phi(s,a) \in \mathbb{R}^d$ 表示，奖励和效用是 $\phi$ 的线性函数，转移概率也是线性形式。
  - **安全策略 $\pi_{\text{sf}}$ 部署规则**：仅当对 $\pi_{\text{sf}}$ 的安全性不自信时（即 $V^{\pi_{\text{sf}}, \beta}_{P,1}(s_1) > \xi/(4C_u)$）才部署 $\pi_{\text{sf}}$；否则使用乐观-悲观策略。定理证明部署次数为对数级 $O(d^3 H^4 \xi^{-2} \ln(K))$。
  - **复合softmax策略**：定义 $\pi^{(k),\lambda}$，通过控制参数 $\lambda$ 调节乐观与悲观程度：  
    $\pi^{(k),\lambda}_h(\cdot|s) = \text{SoftMax}\left( \frac{1}{\kappa} [Q^{(k),\dagger}_{h} + Q^{(k),r}_{h}[\kappa] + \lambda Q^{(k),u}_{h}] \right)$。
  - **算法流程（Algorithm 2 - OPSE-LCMDP）**：
    1. 每轮 $k$，构造乐观惩罚函数与悲观值函数（clipped value functions）。
    2. 若 $\pi^{(k),C_\lambda}$ 的悲观效用估计低于阈值 $b$，则部署 $\pi_{\text{sf}}$。
    3. 否则，通过**二分搜索**在 $[0, C_\lambda]$ 中寻找最小的可行 $\lambda$，使得 $V^{(k),\lambda,u}_1(s_1) \geq b$。
    4. 部署得到的 softmax 策略 $\pi^{(k)}$ 并收集轨迹。
  - **计算效率**：二分搜索仅需 $T = \widetilde{O}(H)$ 次迭代，单次策略与值函数计算复杂度与 $A, H, d$ 多项式相关，独立于状态空间大小 $|S|$。
- **理论结果**：在此主文中未证明，但附录有完整推导，主要贡献是定理4：以概率 $1-\delta$ 实现每回合零违反，且 $\text{Regret}(K) = \widetilde{O}\left(H^2 \sqrt{d^3 K} + d^3 H^4 \xi^{-2} + H^4 \xi^{-1} \sqrt{d^5 K}\right)$。

### 3. 实验设计：数据集/场景、benchmark、对比方法

- **实验环境**（Appendix F）：
  - **合成表格型环境**：$|S|=5, |A|=3, H=4$，随机转移概率（Dirichlet分布）、随机奖励与效用。
  - **Media Streaming 环境**：无线基站传输媒体，快/慢服务策略，缓冲区长度 $L=5, H=4$，状态为缓冲区占用。
  - **合成线性环境**：$|S|=100, |A|=3, d=5, H=4$，随机线性MDP构建。
- **Benchmark**：每种场景计算最优策略 $\pi^*$ 以得到真实遗憾。
- **对比方法**：
  - **Ghosh et al. (2024)**：之前最先进的线性CMDP算法，允许约束违反。
  - **DOPE (Bura et al., 2022)**：表格型CMDP算法，可实现零违反但状态空间依赖。
  - **Uniform Policy**：均匀随机策略，作为下界参考。
- **评估指标**：累计遗憾（Regret）、违反遗憾（Violation Regret）、安全策略 $\pi_{\text{sf}}$ 部署次数。

### 4. 资源与算力

- **文中明确说明**：所有实验在 **30分钟** 内完成，使用 **8个 Intel Core i7 CPU** 和 **32 GiB RAM**。未使用GPU。
- 未提及具体模型训练或大规模并行计算需求，实验规模小且计算要求低。

### 5. 实验数量与充分性

- **实验组数**：每个环境运行 **10个随机种子**，取平均结果。共3个场景，每个场景比较4种方法（但线性环境中DOPE因计算不可行未运行），即总共约3×3=9组实验曲线。
- **是否充分**：实验覆盖了表格型、结构化环境和线性环境，验证了方法在**小规模**和**中规模**线性MDP上的有效性。但缺乏更大尺度（如 $d$ 较大或 $H$ 较长）的测试，也未提供消融实验（如不同 $\kappa, C_\lambda$ 的敏感性）。
- **公平性**：对比方法均使用作者发布的官方或合理复现，超参数经启发式调整。但未报告方差或置信区间（仅平均曲线），可能掩盖性能波动。

### 6. 论文的主要结论与发现

- **算法性能**：OPSE-LCMDP 在所有三种环境下均实现**每回合零违反**（Violation Regret 始终为0），且累计遗憾呈次线性增长（$\widetilde{O}(\sqrt{K})$）。
- **与现有方法对比**：
  - 相比 Ghosh et al. (2024)（违反约束），本算法在安全保障上有本质提升。
  - 相比 DOPE（仅适用于表格型），本算法可扩展至状态空间较大的线性MDP且保持计算高效。
- **安全策略部署**：实验表明，$\pi_{\text{sf}}$ 仅在初始阶段被部署，之后部署次数迅速下降（支持理论对数界），验证了高效探索的设计。

### 7. 优点

- **理论突破**：首次同时实现线性CMDP的**每回合零违反**和**次线性遗憾**，填补了函数逼近场景下的理论空白。
- **计算高效**：二分搜索和软性策略设计导致计算复杂度与状态空间大小无关，多项式依赖于 $d, H, A$，相较先前指数级复杂度有巨大提升。
- **分析技巧**：将乐观-悲观方法从表格推广到线性MDP，通过混合策略分析与椭圆势验证，解决非平凡技术挑战。
- **实验验证**：提供了从简单到中等复杂度的多样化环境，直观展示零违反和次线性遗憾。

### 8. 不足与局限

- **实验覆盖不足**：仅测试了 $d \leq 5$、$H=4$ 的小规模环境，未验证大规模特征维度（如 $d=100$）或更长时域的真实应用。
- **缺乏消融研究**：未分析关键超参数（如 $\xi, C_\lambda, \kappa$）对性能的影响。
- **较弱公平性**：未报告误差条（error bar），仅显示均值，削弱统计可靠性。
- **理论遗憾界中的 $\xi^{-1}$ 项**：虽然不可避免，但可能导致在安全裕度很小 $\xi$ 时遗憾退化，文中未讨论。
- **多约束限制**：方法限于单约束，扩展到多约束需要向量化单调性引理，目前未解决。
- **对抗初始状态不可扩展**：分析依赖于固定初始状态 $s_1$，对抗性初始状态会破坏关键保证。
- **应用假设**：线性MDP假设强，现实中特征映射可能未知或近似线性，未讨论模型误指定问题。

（完）
