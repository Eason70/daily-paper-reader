---
title: Safe Time-Varying Optimization based on Gaussian Processes with Spatio-Temporal Kernel
title_zh: 基于时空高斯过程的时变安全优化
authors: "Jialin Li, Marta Zagorowska, Giulia De Pasquale, Alisa Rupenyan, John Lygeros"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=yKvHJJE9le"
tags: ["query:safe-rl-cbf"]
score: 4.0
evidence: 面向时变安全约束的贝叶斯优化方法
tldr: 针对时变环境下安全优化问题，提出TVSAFEOPT算法，利用时空核的高斯过程建模未知时变安全约束，无需显式变化检测即可安全跟踪时变安全区域，在静态问题上具有最优性保证，仿真实验验证了有效性。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-ykvhjje9le/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1416, \"height\": 1431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-ykvhjje9le/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1337, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-ykvhjje9le/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 486, \"height\": 368, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-ykvhjje9le/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 494, \"height\": 379, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-ykvhjje9le/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 774, \"height\": 580, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-ykvhjje9le/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1443, \"height\": 450, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-ykvhjje9le/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1446, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-ykvhjje9le/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 879, \"height\": 172, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-ykvhjje9le/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 877, \"height\": 170, \"label\": \"Table\"}]"
motivation: 时变系统的安全优化面临未知奖励与约束的挑战，传统方法难以处理。
method: 提出TVSAFEOPT算法，结合贝叶斯优化与时空核函数，在线学习安全区域。
result: 算法能安全跟踪时变安全区域，在静态情形下提供最优性保证。
conclusion: 为时变安全优化提供了一种无需变化检测的实用方法。
---

## Abstract
Ensuring safety is a key aspect in sequential decision making problems, such as robotics or process control. The complexity of the underlying systems often makes finding the optimal decision challenging, especially when the safety-critical system is time-varying. Overcoming the problem of optimizing an unknown time-varying reward subject to unknown time-varying safety constraints, we propose TVSAFEOPT, a new algorithm built on Bayesian optimization with a spatio-temporal kernel. The algorithm is capable of safely tracking a time-varying safe region without the need for explicit change detection. Optimality guarantees are also provided for the algorithm when the optimization problem becomes stationary. We show that TVSAFEOPT compares favorably against SAFEOPT on synthetic data, both regarding safety and optimality. Evaluation on a realistic case study with gas compressors confirms that TVSAFEOPT ensures safety when solving time-varying optimization problems with unknown reward and safety functions.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：在机器人、过程控制等安全关键的顺序决策问题中，系统常具有未知且时变的奖励函数和安全约束。传统的安全贝叶斯优化（如 SAFEOPT）仅适用于静态环境，无法处理安全区域随时间变化的情形；而现有的一些时变安全方法（如 ETSAFEOPT）依赖显式变化检测，可能漏检连续缓慢变化导致不安全。
- **整体含义**：本文提出 TVSAFEOPT 算法，利用带有时空核的高斯过程（GP）建模未知时变奖励与安全约束，在不依赖显式变化检测的前提下，安全地跟踪时变安全区域，并在问题变为静态时提供最优性保证。这为时变安全优化提供了一种理论完备且实用的新方案。

## 2. 论文提出的方法论

- **核心思想**：基于贝叶斯优化框架，将时间和决策空间联合建模为时空核函数，利用时间 Lipschitz 常数描述函数随时间变化的上界。通过递归地构造交叠置信区间，并在更新安全集时考虑时间变化导致的“安全裕度”，从而在每一时间步保守地缩小安全集，避免因过时信息而做出不安全决策。
- **关键技术细节**：
  - 定义辅助函数 \(h(x,t,i)\) 统一表示奖励（\(i=0\)）和约束（\(i\in I_c\)）。
  - 使用零均值 GP 和时空核 \(\kappa((x,t,i),(x',t',i'))\)，并假设 \(h\) 在空间和时间上均满足 Lipschitz 连续，且有界 RKHS 范数。
  - 构建置信区间 \(Q_k(x,i)\)，并通过 Minkowski 和加入时间 Lipschitz 常数得到递归交叠区间 \(C_k(x,i)\)，利用其下界 \(l_k\) 更新安全集 \(S_k = \bigcap_{i\in I_c} \bigcup_{x'\in S_{k-1}} \{x\in X \mid l_k(x',i)-L_x d(x,x')-L(t)\ge 0\}\)。
  - 定义潜在最大化者 \(M_k\) 和潜在扩展者 \(G_k\)，选择不确定性最大的点进行采样（\(x_k = \arg\max_{x\in G_k\cup M_k, i\in I} w_k(x,i)\)），实现探索与利用的平衡。
  - 安全保证（Theorem 2.5）基于引理 2.4 证明置信区间以高概率包含真实函数，从而确保所有被选决策满足约束。
  - 近最优性保证（Theorem 2.6）针对问题变为静态的情形，证明在有限步内能找到接近最优的解。

## 3. 实验设计

- **数据集/场景**：
  - **合成数据**：二维空间 \([-2,2]^2\) 上的时变优化问题，奖励函数含时间线性项，约束为随时间平移的椭圆区域。离散化为 100×100 网格点。
  - **真实案例**：燃气压缩机站负荷分配问题，包含 3 台并联压缩机，目标是最小化功率，约束包括时变需求、压缩机的运行边界（喘振、阻塞等），时变输入包括需求、压头和退化参数（来自文献 [40]）。搜索空间为 60×60×60 网格点。
- **Benchmark 与对比方法**：
  - **SAFEOPT**：经典静态安全贝叶斯优化。
  - **ETSAFEOPT**：基于事件触发的时变安全贝叶斯优化。
  - **Approximate Optimization**：对约束进行线性近似后求解的近似优化方法。
- **评价指标**：安全集基数、安全集中不安全决策占比、安全集覆盖真实安全区域比例、累计遗憾、奖励值等。

## 4. 资源与算力

- 论文明确说明实验使用 **Intel i7-11370H CPU**，Python 3.8.5，GPy 1.12.0，NumPy 1.22.0，Matplotlib 3.5.0。
- **未提及 GPU 或分布式训练**，所有实验均在单 CPU 上完成，未提供训练时长等具体算力消耗。

## 5. 实验数量与充分性

- **实验数量**：
  - 合成数据：5 次独立运行（不同初始安全集）。
  - 压缩机案例：10 次独立运行（不同初始安全集）。
  - 无单独消融实验，仅与三种 baseline 进行比较。
- **充分性与公平性**：
  - 所有算法均使用相同的初始安全集和噪声设置，超参数在附录中列出。
  - 结果以平均值和标准差呈现，图表包含误差棒，统计显著性可评估。
  - 但仅针对两个场景（合成+真实案例），且真实案例仅有一个压缩机站数据，泛化性验证有限；未进行参数敏感性分析或对更多不同时变模式的测试。

## 6. 论文的主要结论与发现

- TVSAFEOPT 能安全适应时变安全区域，在合成数据中安全决策占比显著高于 SAFEOPT 和 ETSAFEOPT，几乎无违规（-99.99% 违规减少）。
- 在压缩机案例中，TVSAFEOPT 保持最低的违规比例（-96.8%），但覆盖真实安全区域比例低于 SAFEOPT，且累计遗憾更高（+178.3%），体现了安全与最优性之间的权衡。
- 理论部分提供了时变情形下的一般安全保证，以及静态情形下的近最优性保证，是主要贡献点。

## 7. 优点

- **理论贡献**：首次在时变安全贝叶斯优化中同时给出安全保证和（静态时的）最优性保证。
- **方法创新**：利用时空核与时间 Lipschitz 常数构建递归置信区间，无需显式变化检测即可自适应安全集收缩，避免过时不安全决策。
- **实验设计**：既包含可直观验证的合成数据，也包含具有实际意义的燃气压缩机案例，增强了方法的可信度。
- **实用性**：提供了 Lipschitz 常数未知时的实用修改版本，降低了应用门槛。

## 8. 不足与局限

- **最优性受限**：在非静态（时变未停止）情形下，TVSAFEOPT 过度保守，累计遗憾显著高于 SAFEOPT，理论仅有静态最优性保证，非静态情形缺乏理论分析。
- **依赖 Lipschitz 常数**：虽然提供了免 Lipschitz 的实用版本，但原始算法需要精确的时间 Lipschitz 常数和空间 Lipschitz 常数，实际中难以获取。
- **实验覆盖有限**：仅两个场景，且真实案例中 ETSAFEOPT 因频繁触发事件而无法运行，对比不够全面；未在更高维、更多样化的时变任务上测试。
- **资源与可扩展性**：未讨论算法在高维决策空间上 GP 计算的可扩展性问题；时变维度增加导致核矩阵增长，可能面临计算瓶颈。

（完）
