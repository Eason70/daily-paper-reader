---
title: Provably Safe Neural Network Controllers via Differential Dynamic Logic
title_zh: 通过微分动态逻辑实现可证明安全的神经网络控制器
authors: "Samuel Teuber, Stefan Mitsch, Andre Platzer"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=SiALFXa0NN"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 使用微分动态逻辑验证神经网络控制器的安全性
tldr: 本文提出VerSAILLE框架，将微分动态逻辑与神经网络验证工具相结合，为信息物理系统提供可证明安全的神经网络控制器。该方法利用控制理论中的安全包络，通过逻辑推理实现无穷时域的安全性验证，在多种基准上证明了其有效性。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-sialfxa0nn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1379, \"height\": 328, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-sialfxa0nn/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 518, \"height\": 105, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-sialfxa0nn/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1029, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-sialfxa0nn/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 346, \"height\": 288, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-sialfxa0nn/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1011, \"height\": 223, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-sialfxa0nn/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1201, \"height\": 523, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-sialfxa0nn/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1430, \"height\": 447, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-sialfxa0nn/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1433, \"height\": 445, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-sialfxa0nn/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1432, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-sialfxa0nn/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1430, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-sialfxa0nn/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1433, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-sialfxa0nn/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1433, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-sialfxa0nn/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1433, \"height\": 447, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-sialfxa0nn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 580, \"height\": 387, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-sialfxa0nn/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1425, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-sialfxa0nn/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1451, \"height\": 105, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-sialfxa0nn/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1451, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-sialfxa0nn/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 870, \"height\": 385, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-sialfxa0nn/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1458, \"height\": 803, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-sialfxa0nn/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1453, \"height\": 485, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-sialfxa0nn/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1030, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-sialfxa0nn/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1467, \"height\": 310, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-sialfxa0nn/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1430, \"height\": 464, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-sialfxa0nn/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 910, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-sialfxa0nn/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1444, \"height\": 465, \"label\": \"Table\"}]"
motivation: 神经网络控制器的安全验证在无穷时域上具有极大挑战。
method: 基于微分动态逻辑的安全包络推导，结合NN验证工具进行形式化验证。
result: 在多个CPS基准上实现了可证明的安全性。
conclusion: VerSAILLE为神经网络控制器的安全验证提供了通用框架。
---

## Abstract
While neural networks (NNs) have a large potential as autonomous controllers for Cyber-Physical Systems, verifying the safety of neural network based control systems (NNCSs) poses significant challenges for the practical use of NNs— especially when safety is needed for unbounded time horizons. One reason for this is the intractability of analyzing NNs, ODEs and hybrid systems. To this end, we introduce VerSAILLE (Verifiably Safe AI via Logically Linked Envelopes): The first general approach that allows reusing control theory literature for NNCS verification. By joining forces, we can exploit the efficiency of NN verification tools while retaining the rigor of differential dynamic logic (dL). Based on a provably safe control envelope in dL, we derive a specification for the NN which is proven with NN verification tools. We show that a proof of the NN’s adherence to the specification is then mirrored by a dL proof on the infinite-time safety of the NNCS.

The NN verification properties resulting from hybrid systems typically contain nonlinear arithmetic over formulas with arbitrary logical structure while efficient NN verification tools merely support linear constraints. To overcome this divide, we present Mosaic: An efficient, sound and complete verification approach for polynomial real arithmetic properties on piece-wise linear NNs. Mosaic partitions complex NN verification queries into simple queries and lifts off-the-shelf linear constraint tools to the nonlinear setting in a completeness-preserving manner by combining approximation with exact reasoning for counterexample regions. In our evaluation we demonstrate the versatility of VerSAILLE and Mosaic: We prove infinite-time safety on the classical Vertical Airborne Collision Avoidance NNCS verification benchmark for some scenarios while (exhaustively) enumerating counterexample regions in unsafe scenarios. We also show that our approach significantly outperforms the State-of-the-Art tools in closed-loop NNV

---

## 论文详细总结（自动生成）

# 论文结构化总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：神经网络控制器（NNCS）在信息物理系统（CPS）中的**无穷时域安全性**验证难以实现。现有方法存在根本性局限：
  - **开环NNV**：忽略物理环境动力学，无法证明系统闭环安全。
  - **闭环NNV**：仅能分析有限时间窗口（秒/分钟级），无法提供无限时间保证。
  - **屏障证书方法**：对连续时间系统，需要验证非线性神经网络特性，难以扩展到中等规模网络。
- **背景**：微分动态逻辑（dL）可对抽象控制策略（控制包络）进行**无穷时域安全证明**，但无法直接处理神经网络。反之，NN验证工具擅长数值推理，但缺乏无穷时域和精确推理能力。论文旨在**结合两者优势**，实现可证明安全的NNCS。

## 2. 论文提出的方法论

### 核心思想
- **VerSAILLE**（Verifiably Safe AI via Logically Linked Envelopes）：基于dL中已验证的安全控制包络，通过**ModelPlex**合成控制器监视器公式（ζc），再将其转化为开环NNV查询。若NN满足该查询，则其行为被证明是控制包络的精化，从而继承无穷时域安全保证。
- **Mosaic**：将VerSAILLE生成的非线性、非归一化开环NNV查询，高效分解为线性归一化查询，并保持完备性。

### 关键技术细节
- **VerSAILLE流程**：
  1. 在dL中验证安全控制包络（例如ACC模型），得到有效公式 `ϕ → [(αctrl; αplant)*] ψ`。
  2. 使用ModelPlex合成控制器监视器公式 ζc，描述允许的状态转移。
  3. 结合系统不变式 ζs，构造开环NNV查询：`ζs → ζc`（即检查NN输出是否始终符合 ζc）。
  4. 若开环NNV工具对该查询返回unsat，则NNCS的无穷时域安全成立（定理2）。
- **Mosaic算法**（算法1）：
  1. **线性化（LINEARIZE）**：对公式中的非线性原子，使用OVERT工具进行分段线性近似（上近似和下近似），并作为蕴含条件加入原公式，保持等价性。
  2. **输入空间马赛克（MOSAIC）**：基于DPLL(T)思想，但先枚举输入空间的线性约束组合（azulejos），再针对每个azulejo枚举输出约束组合，生成线性归一化查询（ql）和残差非线性约束（qn）。避免经典DPLL(T)中多次重复探索相同输入区域。
  3. **反例枚举（ENUM）**：使用开环NNV工具（如nnenum）对线性查询进行可达性分析，并将每个反例点**泛化为反例区域**（输入多面体ι及局部仿射映射ω），利用分段线性NN的性质保证区域覆盖。
  4. **反例过滤（FILTER）**：对每个反例区域，用SMT求解器检查是否存在满足非线性约束的具体反例。由于局部仿射映射ω仅涉及输入变量（I维），编码规模极小，远小于编码整个NN。
- **理论保证**：定理3证明Mosaic**完备且可靠**——返回safe当且仅当不存在反例。

## 3. 实验设计

### 数据集/场景
- **自适应巡航控制（ACC）**：ego车跟随前车，避免碰撞。训练了两个PPO网络（2层64 ReLU、4层64 ReLU），以及第二轮训练后的safe网络。
- **垂直空中碰撞避免（VCAS）**：基于ACAS X的NN控制器（6层45 ReLU），输出9种规避建议。分析水平飞行入侵者场景（|h|≤8000 ft, |v|≤100 ft/s, 6s≤τ≤40s）。对比8种先前建议类型（DNC、DND、DES1500等）。
- **齐柏林飞艇转向**：在随机风扰动下学习避障，使用差分混合博弈的形式化安全包络。

### Benchmark与对比方法
- **开环NNV工具**：nnenum（作为Mosaic底层）。
- **闭环NNV工具**：NNV、JuliaReach、CORA、POLAR（仅测试ACC小部分状态空间）。
- **SMT求解器**：Z3、dReal、Mathematica、cvc5、MathSAT、Z3++（对比非线性查询求解能力）。
- **其他方法**：DNNV（比较归一化查询生成效率）、Genin et al.（手动近似方法）。

### 对比结果
- 闭环工具：仅NNV能在0.1秒内证明0.009%状态空间安全，远弱于N3V的无穷时域全覆盖。
- SMT求解器：均超时（12小时）或返回unknown，只有N3V能成功验证。
- DNNV：对VCAS查询可能产生高达39万亿个可满足析取子句，而Mosaic仅产生约1.9万个查询，效率提升巨大。

## 4. 资源与算力

- **硬件**：AMD Ryzen 7 PRO 5850U CPU（16核），N3V使用单线程，底层nnenum使用多线程。
- **未使用GPU**：所有实验在CPU上完成。
- **训练信息**：ACC NN使用PPO训练，但未报告具体训练时长、GPU型号或数量。VCAS NN来自公开数据集（Julian et al.），无需训练。
- **运行时间**：ACC验证47-300秒；VCAS每个网络0.28-5.45小时；齐柏林飞艇4.1小时。

## 5. 实验数量与充分性

- **实验数量**：
  - ACC：3个网络（原始、大、再训练）× 不同近似粒度（线性、N=1/2/3），共约12组。
  - VCAS：8种先前建议类型，每种完整运行。
  - 齐柏林飞艇：1组。
  - 对比实验：闭环比对4个工具×多种配置（表6），SMT对比6个求解器（表8），DNNV对比（表7）。
- **充分性判断**：
  - **优点**：覆盖了连续/离散控制、不同NN规模、多种对比工具，且结果呈**定性差异**（其他方法根本无法完成相同任务），无需统计显著性。
  - **不足**：未进行消融实验（如去除线性化或反例枚举的影响）；未提供多次运行的标准差；对比实验中未调优其他工具到最佳性能（可能不公平，但论文已尽力尝试多种配置）；仅限于ReLU NN（但理论支持更广）。

## 6. 论文的主要结论与发现

- VerSAILLE+Mosaic**首次实现**对NNCS的**无穷时域安全验证**，同时保持完备性（可详尽枚举不安全区域）。
- 在VCAS基准上，DNC和DND两种网络在水平飞行条件下被证明安全，其余6种不安全，并给出了首次发现的可避免NMAC轨迹（反例区域）。
- 在ACC案例中，通过循环验证-重训练可以逐步缩小不安全区域，最终获得可证明安全的NN（除极小区间外）。
- 对比显示，现有闭环比与SMT方法在无穷时域问题上**完全无法竞争**——要么只能限时，要么超时。
- 齐柏林飞艇案例暴露了经验评估的局限性：一个在模拟中表现良好的NN实际上存在大量不安全区域，仅通过验证才能发现。

## 7. 优点

- **理论创新**：首次将dL的形式化验证与NNV工具无缝结合，利用控制理论已有的安全结果，避免学习屏障函数。
- **完备性**：Mosaic通过反例区域泛化和SMT过滤，在不牺牲效率的前提下保持完备性，这是许多近似方法缺失的。
- **可解释性**：详尽枚举不安全区域，有助于故障分析、重训练指导或备份控制器设计。
- **通用性**：VerSAILLE理论上支持任意分段Noetherian激活函数，Mosaic支持任意分段线性NN，不仅限于ReLU。
- **工程实现**：N3V工具开源，支持标准VNNLIB接口，便于未来集成更优的底层NNV工具。
- **实验说服力**：在多个经典CPS基准上验证，与多种现有方法对比，结果具有压倒性优势。

## 8. 不足与局限

- **可扩展性限制**：最大验证的NN具有270个ReLU节点（VCAS），对于更大规模的NN（如卷积网络或深度ResNet）可能难以处理。论文承认全局属性验证的规模天花板远低于局部鲁棒性验证。
- **依赖dL安全包络**：VerSAILLE要求存在已证明安全的控制包络，对于没有现成包络的新系统，需要额外工作量（dL建模与证明）。
- **仅支持ReLU实现**：虽然理论更通用，但工具N3V仅支持ReLU。其他激活函数（如tanh、sigmoid）需要扩展Mosaic的线性化与SMT部分。
- **对比实验公平性**：闭环比工具未能充分发挥性能（如开环工具无法直接处理非线性），但论文已尽力通过近似使其适用；SMT求解器超时后未报告统计信息。
- **缺少消融研究**：未单独分析线性化精度、马赛克粒度、反例枚举超参数对结果的影响，也未提供多次运行的方差。
- **VCAS仅分析水平飞行**：非水平飞行入侵者已被发现有反例，但未做详尽分析。
- **训练计算资源未报告**：无法复现训练过程。

（完）
