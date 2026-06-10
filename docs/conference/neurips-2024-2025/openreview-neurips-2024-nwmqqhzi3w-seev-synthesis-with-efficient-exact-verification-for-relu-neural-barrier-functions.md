---
title: "SEEV: Synthesis with Efficient Exact Verification for ReLU Neural Barrier Functions"
title_zh: SEEV：面向ReLU神经屏障函数的合成与高效精确验证
authors: "Hongchao Zhang, Zhizhen Qin, Sicun Gao, Andrew Clark"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=nWMqQHzI3W"
tags: ["query:safe-rl-cbf"]
score: 9.0
evidence: 神经控制障碍函数的合成与精确验证
tldr: 针对基于ReLU神经网络的神经控制障碍函数（NCBF）验证计算成本高的问题，提出SEEV框架：合成阶段引入新正则化器减少安全边界激活区域，验证阶段利用网络分段线性结构进行高效精确验证，在非线性自主系统上显著降低验证计算开销。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-nwmqqhzi3w/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1077, \"height\": 355, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-nwmqqhzi3w/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1147, \"height\": 316, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-nwmqqhzi3w/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 990, \"height\": 481, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-nwmqqhzi3w/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1446, \"height\": 471, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-nwmqqhzi3w/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1422, \"height\": 394, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-nwmqqhzi3w/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1381, \"height\": 589, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-nwmqqhzi3w/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1450, \"height\": 564, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-nwmqqhzi3w/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1448, \"height\": 624, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-nwmqqhzi3w/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1454, \"height\": 730, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-nwmqqhzi3w/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 770, \"height\": 434, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-nwmqqhzi3w/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1090, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-nwmqqhzi3w/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1401, \"height\": 285, \"label\": \"Table\"}]"
motivation: 现有NCBF精确验证需枚举所有激活区域，计算成本过高。
method: 提出SEEV框架，包含减少安全边界激活区域的正则化合成算法和高效验证算法。
result: 在非线性自主系统上显著降低了验证时间，同时保证了安全约束。
conclusion: 为神经屏障函数的实际部署提供了可扩展的验证方案。
---

## Abstract
Neural Control Barrier Functions (NCBFs) have shown significant promise in enforcing safety constraints on nonlinear autonomous systems. State-of-the-art exact approaches to verifying safety of NCBF-based controllers exploit the piecewise-linear structure of ReLU neural networks, however, such approaches still rely on enumerating all of the activation regions of the network near the safety boundary, thus incurring high computation cost. In this paper, we propose a framework for Synthesis with Efficient Exact Verification (SEEV). Our framework consists of two components, namely (i) an NCBF synthesis algorithm that introduces a novel regularizer to reduce the number of activation regions at the safety boundary, and (ii) a verification algorithm that exploits tight over-approximations of the safety conditions to reduce the cost of verifying each piecewise-linear segment. Our simulations show that SEEV significantly improves verification efficiency while maintaining the CBF quality across various benchmark systems and neural network structures. Our code is available at https://github.com/HongchaoZhang-HZ/SEEV.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- 神经控制障碍函数（Neural Control Barrier Functions, NCBFs）利用ReLU神经网络表示安全约束，在非线性自主系统上展现出良好前景。
- 现有的精确验证方法虽然利用了ReLU网络的**分段线性结构**，但需要穷举安全边界附近的所有**激活区域（hyperplanes/hinges）**，导致计算成本极高，难以扩展到高维系统。
- 本文提出**SEEV（Synthesis with Efficient Exact Verification）**框架，旨在**协同设计NCBF的合成与验证**，通过减少边界激活区域数量并设计高效的验证流程，显著降低验证开销，同时保持安全性能。

### 2. 论文提出的方法论：核心思想、关键技术细节

#### 核心思想
- 将NCBF验证的计算瓶颈归结为**两个因素**：
  1. 安全边界上激活区域的数量；
  2. 验证每个分段线性段的计算复杂度。
- 针对这两个因素，SEEV分别设计：
  - **合成阶段**：引入边界激活正则化器，训练时惩罚边界附近激活模式的不一致性，从而减少边界超平面和铰链的数量。
  - **验证阶段**：采用分层策略，先使用**充分条件**（如线性规划或简单不等式）快速验证大部分区域，仅当充分条件失败时才调用**精确条件**（非线性优化），从而减少计算量。

#### 关键技术细节
1. **合成阶段（Synthesis）**：
   - 损失函数 \( \mathcal{L} = \lambda_B \mathcal{L}_B + \lambda_f \mathcal{L}_f + \lambda_c \mathcal{L}_c \)
     - \( \mathcal{L}_c \)：正确性损失，惩罚分类错误（安全样本应满足 \(b(x)\ge0\)，不安全样本应 \(b(x)<0\)）。
     - \( \mathcal{L}_f \)：验证损失，通过引入松弛变量 \(r\) 近似满足 Lie 导数条件。
     - \( \mathcal{L}_B \)：**边界激活正则化**，利用广义 sigmoid 函数平滑表示激活模式，然后对边界附近的样本进行聚类，惩罚同一聚类内激活向量的差异。
   - 通过**反例引导**：验证器返回的反例被加入训练数据集，迭代提升 NCBF 质量。

2. **验证阶段（Verification）**：
   - **激活区域枚举**：
     - 初始激活集 \(S_0\)：通过安全点与不安全点连线上的二分搜索+边界线性规划（BoundaryLP）获得。
     - NBFS（Neural Breadth-First Search）：从 \(S_0\) 出发，通过翻转每个神经元的激活状态（需满足 unstable neuron LP）扩散，寻找所有边界超平面。
     - 铰链（Hinges）枚举：通过求解线性规划识别相交于零水平面的多个超平面。
   - **分层验证**（从易到难）：
     - 正确性验证：检查 \(D \subseteq C\)，即 \(b(x)=0\) 时 \(h(x)\ge0\)。
     - 超平面验证：对于每个边界超平面，先尝试充分条件（例如若输入集为 \(\ell_\infty\)-球则转化为 L1 范数问题；若 \(U=\mathbb{R}^m\) 则需检查 \(W(S)^T g(x)=0\) 且 \(W(S)^T f(x)\ge0\) 等）。若充分条件失败，则求解非线性规划 (18) 或 (19)/(20)。
     - 铰链验证：类似地先尝试充分条件（如控制输入 \(u=0\) 即可满足，或存在可抵消所有项的控制方向），再求解精确非线性规划 (21)。
   - 完整性保证：枚举过程确保覆盖所有边界激活区域，且验证采用 dReal 求解器保证精确性（Theorem 2）。

### 3. 实验设计：数据集/场景、Benchmark、对比方法

- **系统/场景**（共4个）：
  1. **Darboux**：2维非线性开环多项式系统。
  2. **Obstacle Avoidance (OA)**：3维无人机避碰（位置+偏航角）。
  3. **Spacecraft Rendezvous (SR)**：6维航天器交会（线性化 Clohessy-Wiltshire-Hill 方程）。
  4. **hi-ord 8**：8维高阶线性系统（源自文献[21]）。
- **对比方法**：
  - Exact verification [23]：先前基于分段线性枚举的精确验证方法。
  - dReal：SMT-based 非线性求解器。
  - Z3：SMT solver。
- **评估指标**：
  - 边界超平面数量（\(N\)）、验证时间（超平面验证时间 \(t_h\)、铰链验证时间 \(t_g\)、总时间 \(T\)）。
  - 安全区域覆盖率 \(C\) 及正则化后覆盖率比值 \(\rho\)。
  - 合成成功率（Counterexample-guided training 的 success rate, 最小 epoch）。
- **消融实验**：
  - 边界正则化强度 \(r=0,1,10,50\) 的影响。
  - 超参数敏感性分析（\(\lambda_c, \lambda_f, k\) 等）。

### 4. 资源与算力

- 论文明确说明：实验运行在 **Intel i7-11700KF CPU** 和 **NVIDIA GeForce RTX 3080 GPU** 的工作站上。
- 未报告具体训练时长或总 GPU 小时数，但给出了验证时间（秒级别）和合成 epoch 数（最多 50 epoch）。
- 对于较大网络（如 SR 6维、4层16隐藏单元），验证时间达 60 秒左右，合成本身未报告耗时。

### 5. 实验数量与充分性

- **实验组数**：
  - 正则化效果（表1）：对OA和SR共10种网络结构（不同维度、层数、宽度），比较有无正则化的边界超平面数。
  - 验证效率（表2）：4个系统共13种配置，每个配置测量验证时间并与三个基线对比。
  - 合成反例引导（表3）：Darboux 和 hi-ord 8 各4种结构，每结构3个随机种子，比较有无CE的成功率。
  - 超参数消融（表5）：SR case (L=4, M=8) 对4个超参数各选4个值，每设置3随机种子。
- **充分性评估**：实验覆盖了不同维度（2~8）、不同网络结构（层数2~4，宽度8~512）、不同系统类型（非线性、线性高维）。但未在其他系统（如实际机器人平台）上验证。对比基线覆盖了当前主流方法，且消融实验较完整。整体较充分。

### 6. 论文的主要结论与发现

1. **边界正则化显著减少超平面数量**：例如SR系统（6维，4层，8隐藏单元）正则化后从6218减至627，安全覆盖率基本不变。
2. **验证效率大幅提升**：所有案例下SEEV验证时间远小于基线（如Darboux 2.5s vs 315s；OA 0.39s vs 16s；SR 9.8s vs 179s）；高维系统（hi-ord 8）基线超时，SEEV仅需22.4s。
3. **铰链验证通过充分条件即可完成，无需调用精确非线性求解**：所有实验中 \(t_g=0\)，说明充分条件已足够。
4. **反例引导合成提高了训练成功率**：不加CE训练几乎无法获得可证明安全的NCBF，加CE后大部分结构成功率达1/3以上。
5. 方法对超参数（\(\lambda_c, \lambda_f, k\)）具有一定鲁棒性，但需避免极端值。

### 7. 优点：方法或实验设计上的亮点

- **协同设计合成与验证**：从根源降低验证复杂度（减少边界激活区域），而非仅优化验证算法。
- **分层验证策略**：先充分条件后精确条件，充分条件下仅需求解LP，极大减少计算量；实验显示所有铰链验证只需充分条件。
- **验证流程完整**：NBFS 保证覆盖所有边界超平面和铰链，且利用 dReal 保证精确性（Theorem 2）。
- **正则化方法新颖**：通过平滑激活模式并聚类，实现可微的边界激活区域控制。
- **实验对比全面**：包含多个维度、多种网络结构，并与三种基线方法对比。

### 8. 不足与局限

- **高维系统仍具挑战**：对于10维以上系统，枚举所有超平面和铰链可能指数增长，文中未讨论极端情况。
- **仅适用于ReLU激活**：非ReLU（如tanh、sigmoid）缺乏分段线性结构，无法直接应用；作者在结论中明确此为开放问题。
- **系统模型限制**：假设控制仿射系统（\(\dot{x}=f(x)+g(x)u\)），且需已知 \(f,g\)；对更一般动力学不适用。
- **验证依赖dReal**：精确条件验证需调用dReal求解非线性规划，dReal本身对高维非线性优化可能效率低或不可判定。
- **实验规模有限**：仅在4个仿真系统上验证，未涉及真实机器人或噪声环境；安全区域形状简单（凸集或简单非凸）。
- **缺乏统计显著性报告**：验证时间仅给出单次测量（确定性过程），但合成成功率基于3次随机种子，未报告方差或置信区间。
- **潜在偏差风险**：正则化可能过度减少边界区域导致安全集收缩（文中用覆盖率比值 \(\rho\) 监控，但仅针对部分配置）。

（完）
