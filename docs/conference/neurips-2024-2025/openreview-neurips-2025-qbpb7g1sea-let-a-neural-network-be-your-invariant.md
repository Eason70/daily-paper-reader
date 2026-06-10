---
title: Let a Neural Network be Your Invariant
title_zh: 让神经网络成为你的不变量
authors: "Mirco Giacobbe, Daniel Kroening, Abhinandan Pal, Michael Tautschnig"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=qBPb7g1SEa"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 用神经网络学习安全验证中的归纳不变量
tldr: 形式验证中安全属性需要归纳不变量，而现有神经模型检查仅关注活性的排名函数。本文扩展了神经模型检查，使其同时学习排名函数和归纳不变量，从而能够用神经网络验证安全属性。该方法为自动化安全验证提供了数据驱动的新途径。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-qbpb7g1sea/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1371, \"height\": 921, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-qbpb7g1sea/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1395, \"height\": 575, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-qbpb7g1sea/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1455, \"height\": 945, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-qbpb7g1sea/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1424, \"height\": 427, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-qbpb7g1sea/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1318, \"height\": 257, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-qbpb7g1sea/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1331, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-qbpb7g1sea/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1207, \"height\": 973, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-qbpb7g1sea/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1474, \"height\": 996, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-qbpb7g1sea/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1477, \"height\": 964, \"label\": \"Table\"}]"
motivation: 现有的神经模型检查只能验证活性，不能验证安全性。
method: 扩展神经模型检查，使其同时学习排名函数和归纳不变量。
result: 能够用神经网络验证安全属性。
conclusion: 为安全验证提供了基于神经网络的数据驱动方法。
---

## Abstract
Safety verification ensures that a system avoids undesired behaviour. 
Liveness complements safety, ensuring that the system also achieves its
desired objectives.  A complete specification of functional correctness must
combine both safety and liveness.  Proving with mathematical
certainty that a system satisfies a safety property demands presenting an
appropriate inductive invariant of the system, whereas proving liveness
requires showing a measure of progress witnessed by a ranking function. 
Neural model checking has recently introduced a data-driven approach to the
formal verification of reactive systems, albeit focusing on ranking
functions and thus addressing liveness properties only.  In this paper, we
extend and generalise neural model checking to additionally encompass
inductive invariants and thus safety properties as well.  Given a system and
a linear temporal logic specification of safety and liveness, our approach
alternates a learning and a checking component towards the construction of a
provably sound neural certificate.  Our new method introduces a neural
certificate architecture that jointly represents inductive invariants as
proofs of safety, and ranking functions as proofs of liveness.  Moreover,
our new architecture is amenable to training using constraint solvers,
accelerating prior neural model checking work otherwise based on gradient
descent. We experimentally demonstrate that our method is orders of
magnitude faster than the state-of-the-art model checkers on pure liveness
and combined safety and liveness verification tasks written in
SystemVerilog, while enabling the verification of richer properties than was
previously possible for neural model checking.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：形式验证中，完整的功能正确性规范必须同时包含安全属性（“坏事永不发生”）和活性属性（“好事终将发生”）。安全属性需要归纳不变量来证明，活性属性需要排名函数来证明。传统符号模型检查器（如基于BDD或SAT/IC3）在处理大规模算术电路时面临可扩展性问题；神经模型检查此前仅能处理活性属性（通过神经网络学习排名函数），无法处理安全属性。
- **核心问题**：如何将神经模型检查扩展到同时处理安全与活性，即让神经网络既能表示归纳不变量（证明安全），又能表示排名函数（证明活性），从而验证任意线性时态逻辑（LTL）规范。
- **整体含义**：本文提出一种新的神经证书架构，统一表示不变量与排名函数，并采用基于约束求解器（MILP）的训练方法，显著提升效率与数值稳定性，首次实现用神经网络验证完整的LTL性质，并在多个基准上超越现有符号工具。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将模型检查问题规约为公平空性（fair emptiness）问题，通过构造一个神经部分排名函数（Neural Partially-Ranking Function） \(\bar{V}(\text{reg } s; \theta_q)\) 联合表示归纳不变量和排名函数。该函数满足：
  - **初试条件**（公式6）：所有初态 \(s \in S_0\) 满足 \(\kappa \geq \bar{V}(\text{reg } s; \theta_{q_0})\)。
  - **排名条件**（公式7）：对任意转移 \((s,q) \to (s',q')\)，若 \(\kappa \geq \bar{V}(\text{reg } s; \theta_q)\)，则 \(\bar{V}(\text{reg } s; \theta_q) \geq \bar{V}(\text{reg } s'; \theta_{q'}) + \mathbf{1}_F(q)\)（在公平状态下降1，否则非增）。
  - 由此可定义不变量 \(I = \{(\text{reg } s, q) \mid \kappa \geq \bar{V}(\text{reg } s; \theta_q)\}\)，排名函数 \(V = \bar{V}\)。
- **架构**：双分支网络（图2b）。左分支：L层全连接层（符号激活函数 + 输出层步进函数），输出二进制掩码 \(\alpha \in \{0,1\}^m\)；右分支：m个线性函数 \(\beta = A^{(q)}r + c^{(q)}\)。最终输出 \(\bar{V} = \alpha \cdot \beta\)，即分段线性函数。
- **学习算法**：反例引导的归纳合成（CEGIS）循环。初始化空数据集 \(D_{\text{init}}, D_{\text{trans}}\)；学习阶段使用MILP求解器（Gurobi）求解公式(11)的约束（初试与排名条件在样本上成立）；检查阶段用SMT求解器（Bitwuzla）验证公式(14)是否在全状态空间上成立，若不成立则添加反例继续循环。网络结构失败时逐步增加一层或扩大宽度。
- **关键技术**：使用整数决策变量和线性约束编码（公式15-18），避免双线性项，使得学习阶段可转化为混合整数线性规划（MILP），从而用高效稳定的MILP求解器训练。

### 3. 实验设计：数据集、基准、对比方法

- **基准（Benchmark）**：基于Prior NMC'24的10个参数化SystemVerilog设计，新增第11个设计，并为每个设计构造纯安全性、纯活性、安全+活性三类LTL性质，共634个任务。具体设计包括Delay、LCD Controller、Blink、Thermocouple、7-Segment、i2c Stretch、PWM、VGA Controller、UART Transmitter、Load-Store、Gray Counter（附录A详述）。
- **对比方法**：
  - NMC'24：梯度下降的神经模型检查（仅活性）
  - nuXmv 2.1.0：符号模型检查器
  - rIC3 1.5.1：基于IC3的硬件模型检查器
  - ABC/Super-Prove：AIG电路上的模型检查器
- **翻译流程**：SystemVerilog → SMT (EBMC) → SMV (nuXmv) → AIG (ABC/rIC3) 自动转换。

### 4. 资源与算力

- **硬件**：AWS m6a.4xlarge实例（16 vCPU，64 GB RAM，Ubuntu 24.04）。未使用GPU。
- **时间**：每个任务超时5小时；所有实验总计耗时9083小时（约378天）。
- **工具版本**：Spot 2.11.6（LTL转Büchi自动机）、EBMC 5.6、Bitwuzla 0.7.0、Gurobi 12.0.1，以及CVC5 1.1.2、MathSAT 5.6.10、Z3 4.13.0（用于学习引擎对比）。

### 5. 实验数量与充分性

- **实验数量**：634个任务 × 4个对比工具 + 多个消融实验（线性架构、随机数据初始化、不同学习引擎），总实验次数可观。
- **充分性**：
  - 覆盖三类LTL性质（安全、活性、组合），每个设计多种性质。
  - 消融实验验证了神经网络表达力（纯线性模型仅完成48%任务，自动增量架构完成87%）；随机初始化未提升性能；MILP引擎（Gurobi/Z3）优于梯度下降和部分SMT求解器。
  - 采用标准竞赛工具（HWMCC获奖者）并统一翻译流程，保证公平。
  - 但未进行统计显著性检验（形式验证工具确定性运行，误差条无意义）。

### 6. 论文的主要结论与发现

- **纯活性任务**：新方法完成88%任务（nuXmv 82%，NMC’24 79%，rIC3 50%，ABC 36%），速度比最快对比工具快10×以上占46%，最高10^5×。
- **安全+活性组合任务**：完成82%（nuXmv 74%，rIC3 61%，ABC 46%），速度显著领先：61%任务快于其他工具，其中27%快10^4×以上。
- **纯安全任务**：完成92%（与ABC/nuXmv/rIC3的95%+接近），但多任务在1秒内完成，表明可匹配成熟的符号工具。
- **消融实验显示**：仅线性模型（无隐藏层）无法解决大部分任务，说明神经网络增加了必要表达力；随机数据集无益；MILP求解器（Gurobi/Z3）优于其他学习引擎。
- **主要贡献**：首次用神经网络同时证明安全与活性；提出MILP可训练的架构，比梯度下降更快更稳定；大规模实验验证了有效性。

### 7. 优点

- **方法创新**：将归纳不变量与排名函数统一到单一神经网络中，扩展了神经模型检查的能力范围。
- **训练高效**：采用MILP求解器（而非梯度下降），避免超参调优和数值不稳定问题，训练速度快且可证明最优。
- **架构紧凑**：双分支结构产生天然分段线性函数，整数类型自然量化，输出可解释。
- **实验全面**：634任务覆盖典型硬件设计，对比多个最强基线，包含消融和引擎对比，结论可靠。
- **开源**：代码和基准将公开，便于复现。

### 8. 不足与局限

- **表达局限**：架构仅支持符号激活函数和线性右分支，无法处理更复杂的非线性函数或深度网络。
- **应用范围**：仅限于有限状态硬件（无数组、字符串、过程调用），无法直接处理软件或无限状态系统。
- **纯安全性任务**：虽与符号工具相当，但未超越；在简单安全性质上可能不如专用工具快。
- **计算资源**：总耗时大（9083小时），但每个任务通常秒级完成；个别任务因Gurobi内存段错误或无解而失败（13%）。
- **泛化性**：基准主要来自教材级设计，可能不代表工业级大规模电路；未来需评估扩展到更大设计的能力。
- **无统计显著性**：由于工具确定性，未报告误差条，但通过大量任务分布图（cactus/scatter）展示了趋势。

（完）
