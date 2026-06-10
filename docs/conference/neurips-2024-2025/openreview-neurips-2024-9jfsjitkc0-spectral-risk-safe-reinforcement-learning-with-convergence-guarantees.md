---
title: Spectral-Risk Safe Reinforcement Learning with Convergence Guarantees
title_zh: 具有收敛保证的谱风险安全强化学习
authors: "Dohyeong Kim, Taehyun Cho, Seungyub Han, Hojun Chung, Kyungjae Lee, Songhwai Oh"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=9JFSJitKC0"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 基于谱风险度量的安全强化学习，具有收敛保证
tldr: 风险约束强化学习因风险度量的非线性而难以收敛。本文提出谱风险约束策略优化（SRCPO），利用风险度量的对偶性质构建双层优化，外层优化对偶变量，内层求策略。理论证明了收敛性，实验表明该方法在控制最坏场景风险方面优于传统方法。为安全关键场景提供了一种理论健全的风险敏感RL方案。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-9jfsjitkc0/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 484, \"height\": 339, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-9jfsjitkc0/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1447, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-9jfsjitkc0/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1445, \"height\": 427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-9jfsjitkc0/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1442, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-9jfsjitkc0/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1447, \"height\": 294, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-9jfsjitkc0/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1403, \"height\": 347, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-9jfsjitkc0/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1414, \"height\": 611, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-9jfsjitkc0/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1415, \"height\": 563, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-9jfsjitkc0/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 740, \"height\": 552, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-9jfsjitkc0/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1452, \"height\": 928, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-9jfsjitkc0/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1445, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-9jfsjitkc0/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1454, \"height\": 318, \"label\": \"Table\"}]"
motivation: 解决风险度量非线性导致的安全强化学习收敛困难。
method: 提出谱风险约束策略优化，采用双层优化框架分离对偶变量和策略优化。
result: 在多个基准任务上实现了更好的风险回报权衡。
conclusion: 为风险敏感安全强化学习提供了有收敛保证的实用算法。
---

## Abstract
The field of risk-constrained reinforcement learning (RCRL) has been developed to effectively reduce the likelihood of worst-case scenarios by explicitly handling risk-measure-based constraints.
However, the nonlinearity of risk measures makes it challenging to achieve convergence and optimality.
To overcome the difficulties posed by the nonlinearity, we propose a spectral risk measure-constrained RL algorithm, spectral-risk-constrained policy optimization (SRCPO), a bilevel optimization approach that utilizes the duality of spectral risk measures.
In the bilevel optimization structure, the outer problem involves optimizing dual variables derived from the risk measures, while the inner problem involves finding an optimal policy given these dual variables.
The proposed method, to the best of our knowledge, is the first to guarantee convergence to an optimum in the tabular setting.
Furthermore, the proposed method has been evaluated on continuous control tasks and showed the best performance among other RCRL algorithms satisfying the constraints.
Our code is available at https://github.com/rllab-snu/Spectral-Risk-Constrained-RL.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

安全强化学习（Safe RL）旨在避免智能体在交互过程中产生不可逆的损害。传统方法通常使用期望形式的成本约束，但期望无法捕捉成本分布的尾部信息，因而难以有效抑制最坏情况（worst-case scenarios）的发生。为此，研究者引入风险度量（如条件风险价值 CVaR 及其推广形式——谱风险度量）来定义约束，构成风险约束强化学习（RCRL）问题。然而，风险度量固有的非线性导致现有 RCRL 算法难以保证收敛到全局最优，大多只能实现局部收敛。本文旨在解决这一难题，提出首个在表格设置下保证收敛到最优的谱风险约束强化学习算法。

## 2. 方法论

### 核心思想
利用谱风险度量的对偶形式，将原始 RCRL 问题转化为一个双层优化问题：
- **外层问题**：优化由风险度量对偶形式导出的对偶变量（即函数 \(g\) 的参数化表示 \(\beta\)）；
- **内层问题**：在给定对偶变量的条件下，寻找满足子风险度量约束的最优策略。

### 关键技术细节
1. **谱风险度量的对偶表示**  
   \[
   R_\sigma(X) = \inf_g \mathbb{E}[g(X)] + \int_0^1 g^*(\sigma(u))\,du
   \]
   其中 \(g\) 为递增凸函数。通过参数化 \(g\)（采用分段线性函数 \(g_\beta\)），将外问题的搜索空间从函数空间转化为有限维参数空间 \(\mathcal{B} \subset \mathbb{R}^{M-1}\)。

2. **内问题：策略梯度更新**  
   定义新的风险值函数 \(V^\pi_{i,g}(\bar{s})\) 和风险优势函数 \(A^\pi_{i,g}(\bar{s},a)\)，并证明其满足性能差分的线性形式。在此基础上提出策略更新规则：满足约束时同时优化奖励和约束的梯度方向，违反约束时优先降低违反的约束。在软max参数化下，证明了该更新规则在表格设置下收敛到内问题最优策略。

3. **外问题：对偶变量优化**  
   由于外问题可能非凸，直接梯度下降无法保证全局收敛。为此，引入一个分布（称为 sampler）\(\xi\) 来建模 \(\beta\) 的最优性概率。通过最小化当前策略与目标分布之间的交叉熵损失，并采用自然梯度更新，证明该 sampler 收敛到仅在最优 \(\beta^*\) 处非零的分布。

4. **实用实现**  
   使用分位数分布评论家（quantile distributional critic）估计风险值函数；使用截断正态分布参数化 sampler；采用条件策略网络 \(\pi_\theta(a|\bar{s};\beta)\) 同时处理多个 \(\beta\)。

## 3. 实验设计

### 任务场景
- **Safety Gymnasium**：点机器人（point）和车机器人（car）在 goal 和 button 任务中避障，单约束（碰撞代价）。
- **足式机器人 locomotion**：双足和四足机器人跟踪目标速度，多约束（身体平衡、高度、足地接触时序）。

### Baseline 方法
按风险估计方式分为三类：
- **使用辅助变量估计 CVaR**：CVaR-CPO、CPPO
- **使用分布评论家估计状态级风险**：WCSAC-Dist、SDPO
- **假设高斯近似**：SDAC

所有方法均在同一超参数设置下，每个任务使用 5 个随机种子进行训练和评估。

### 对比指标
- 奖励总和（reward sum）
- 成本率（cost rate）
- 约束满足情况

## 4. 资源与算力

论文明确说明实验硬件：
- **CPU**：Intel Xeon E5-2680
- **GPU**：NVIDIA TITAN Xp（单卡）
- **平均训练时间**（以 point goal 任务为例）：
  - SRCPO：约 9 小时 51 分钟
  - 其他基线：4–14 小时不等

## 5. 实验数量与充分性

- 共涵盖 6 个连续控制任务（Safety Gymnasium 4 个 + 足式机器人 2 个）。
- 每个算法在所有任务上各运行 5 个随机种子。
- 额外进行了针对不同风险度量（CVaR、Pow、Wang）及不同风险水平的消融实验。
- 实验设计覆盖单约束和多约束场景，结果展示了训练曲线、最终性能分布和统计误差（标准差）。
- **充分性评价**：实验较为充分，对比方法覆盖了主流的 RCRL 算法，且控制了网络结构和超参一致，公平性较好。唯一可改进的是缺少在高维或离散动作空间的实验。

## 6. 主要结论与发现

- **理论贡献**：SRCPO 是首个在表格设置下保证收敛到 RCRL 问题全局最优的算法。
- **实验性能**：在所有连续控制任务中，SRCPO 在满足成本约束的前提下取得了最高的平均奖励。
- **风险度量适用性**：SRCPO 能够灵活处理多种风险度量（CVaR、Pow、Wang），且风险水平越高，对极端成本的抑制越明显。
- **与基线对比**：多数基线（如 WCSAC-Dist）因风险估计近似方式导致约束违反，而 SRCPO 始终满足约束。

## 7. 优点

- **理论完备性**：首次为 RCRL 问题提供全局收敛证明，填补了该领域的理论空白。
- **双层框架的巧妙性**：利用谱风险度量的对偶性，将非线性问题转化为可分离的内外优化，内问题保持线性性，外问题通过分布更新避免非凸困境。
- **通用性**：提出的策略更新规则可以泛化到多种现有 primal-based 安全 RL 算法（如 CPO、PCPO、P3O），为其提供收敛性分析。
- **实用性能**：在标准基准上超越 SOTA 基线，且支持多约束和多种风险度量，工程实现完整（开源代码）。

## 8. 不足与局限

- **理论假设限制**：收敛证明仅在表格设置（有限状态动作空间、softmax 参数化）下成立，未扩展到线性 MDP 或函数近似，实用性受限于理论范围。
- **外问题离散化误差**：对谱函数的离散化（M 个分点）引入近似误差，虽然给出了误差界，但实际选择 M 时需平衡精度与计算量。
- **计算开销**：内问题需要为每个 \(\beta\) 维护策略，且 outer loop 涉及多次内问题求解，训练时间较长（9h+），可能不适合实时或样本效率要求极高的场景。
- **实验覆盖有限**：未在复杂视觉任务或高维状态空间（如 Atari）上验证，也缺少与最优风险敏感 RL 方法（如 Bäuerle & Glauner 的谱风险 MDP 算法）的直接对比。
- **风险度量选择主观**：实际使用中谱的选取（如 CVaR、Pow、Wang）需要先验知识，缺乏自适应机制。

（完）
