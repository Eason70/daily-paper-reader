---
title: "Analytical Lyapunov Function Discovery: An RL-based Generative Approach"
title_zh: 解析李雅普诺夫函数发现：基于强化学习的生成式方法
authors: "Haohan Zou, Jie Feng, Hao Zhao, Yuanyuan Shi"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=rqOlUTnKWh"
tags: ["query:safe-rl-cbf"]
score: 5.0
evidence: 使用强化学习生成解析李雅普诺夫函数，可辅助安全验证
tldr: 本文提出基于Transformer的解析李雅普诺夫函数生成框架，结合风险寻求策略梯度进行验证与优化。该方法避免了神经网络黑箱特性，提供可解释的稳定性分析工具，对安全控制验证有价值。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-rqolutnkwh/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 734, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rqolutnkwh/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1581, \"height\": 836, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rqolutnkwh/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1701, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rqolutnkwh/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1461, \"height\": 850, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rqolutnkwh/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1675, \"height\": 523, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rqolutnkwh/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 756, \"height\": 529, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rqolutnkwh/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 752, \"height\": 527, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rqolutnkwh/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1662, \"height\": 531, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-rqolutnkwh/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1779, \"height\": 862, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rqolutnkwh/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1706, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rqolutnkwh/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1623, \"height\": 235, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rqolutnkwh/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 674, \"height\": 192, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rqolutnkwh/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1516, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rqolutnkwh/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1103, \"height\": 438, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rqolutnkwh/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1255, \"height\": 275, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rqolutnkwh/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1241, \"height\": 234, \"label\": \"Table\"}]"
motivation: 神经网络李雅普诺夫函数难以扩展验证且缺乏可解释性。
method: 使用Transformer生成候选解析李雅普诺夫函数，并利用风险寻求策略梯度优化。
result: 在非线性系统上成功发现解析李雅普诺夫函数，验证效率高于现有方法。
conclusion: 该工作为控制系统的形式化验证提供了新途径，间接支持安全控制。
---

## Abstract
Despite advances in learning-based methods, finding valid Lyapunov functions for nonlinear dynamical systems remains challenging. Current neural network approaches face two main issues:  challenges in scalable verification and limited interpretability. To address these, we propose an end-to-end framework using transformers to construct analytical Lyapunov functions (local), which simplifies formal verification, enhances interpretability, and provides valuable insights for control engineers. Our framework consists of a transformer-based trainer that generates candidate Lyapunov functions and a falsifier that verifies candidate expressions and refines the model via risk-seeking policy gradient. Unlike Alfarano et al. (2024), which utilizes pre-training and seeks global Lyapunov functions for low-dimensional systems, our model is trained from scratch via reinforcement learning (RL) and succeeds in finding local Lyapunov functions for *high-dimensional* and *non-polynomial* systems. Given the symbolic nature of the Lyapunov function candidates, we employ efficient optimization methods for falsification during training and formal verification tools for the final verification. We demonstrate the efficiency of our approach on a range of nonlinear dynamical systems with up to ten dimensions and show that it can discover Lyapunov functions not previously identified in the control literature. Full implementation is available on [Github](https://github.com/JieFeng-cse/Analytical-Lyapunov-Function-Discovery).

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究动机**：传统的李雅普诺夫函数构造依赖专家经验，称为“艺术”；基于神经网络的方法虽然自动化，但面临**可扩展验证困难**（如SMT/MIP求解器受限于网络规模）和**缺乏可解释性**（黑箱特性无法为控制工程师提供直观见解）。因此，论文旨在直接发现**解析形式**（符号表达式）的局部李雅普诺夫函数，以同时满足可验证性与可解释性。
- **整体含义**：提出一个端到端框架，利用符号Transformer生成候选解析李雅普诺夫函数，并通过强化学习（风险寻求策略梯度）针对特定系统从头训练，无需大规模预训练数据集，能处理高达10维的非线性系统（包括非多项式动力学），并首次为有损电力系统找到已知文献中未知的局部李雅普诺夫函数。

### 2. 论文提出的方法论

- **核心思想**：将李雅普诺夫函数发现建模为符号回归问题，使用**符号Transformer**作为条件生成器（输入系统动力学的符号序列，输出候选解析表达式的token序列）。采用**风险寻求策略梯度**（Risk-Seeking Policy Gradient）优化Transformer参数，以最大化候选表达式在“最好情况”下的性能（即找到至少一个有效解），而非平均性能。训练过程中，通过**全局优化（SHGO）** 进行数值验证，识别违反李雅普诺夫条件的反例，并反馈到训练集中。此外，整合**遗传编程（GP）** 作为专家引导，对Transformer生成的候选进行进一步演化，并通过专家引导损失（加权交叉熵）加速收敛。
- **关键技术细节**：
  - **符号Transformer**：编码器将系统ODE（如`\dot{x}_1 = x_2`）token化为前序遍历序列，并编码为潜在向量；解码器自回归生成候选函数的token序列（采用层次树状态表示增强上下文）。
  - **风险寻求策略梯度**：目标函数 `J_risk(ϕ, α)` 仅对位于奖励分布前 `(1-α)` 分位的样本计算梯度，避免平均性能目标与“找到至少一个有效解”之间的不匹配（实验中α=0.1）。
  - **全局优化数值验证**：对每个候选 `V_φ`，使用SHGO找到 `V_φ` 和 `-L_f V_φ` 在状态空间内的全局极小点，在极小点邻域及全局随机采样共约2400个点检查条件；违反点加入训练集。该验证提供对抗性反馈，加速策略改进。
  - **遗传编程引导**：GP将Transformer输出的候选作为初始种群，以李雅普诺夫风险奖励为适应度进行演化，取精英集计算专家引导损失，使Transformer学习GP探索到的好解特征。
- **公式/算法流程**（文字说明）：
  - 初始化Transformer参数ϕ，随机采样训练集X；
  - 每轮迭代：解码器采样Q个候选函数；用GP改进得到精英集；数值验证全部候选，若无违反则返回有效解，否则收集反例X_ce；
  - 计算所有候选的奖励（基于李雅普诺夫风险映射到[0,1]）；
  - 计算风险寻求策略梯度更新ϕ；同时计算专家引导损失更新ϕ；
  - 将反例X_ce加入训练集，继续下一轮。

### 3. 实验设计

- **测试场景/数据集**：涵盖11个非线性系统，分为多项式系统（2-D至10-D，包括Van Der Pol振荡器、高次多项式、耦合线性子系统等）和非多项式系统（简单摆、3-D三角函数系统、四旋翼、3母线无损电力系统、2母线有损电力系统、9-D合成系统等）。大多数系统为局部渐近稳定，部分为全局渐近稳定。
- **基准对比方法**：
  - **神经网络方法**：Augmented Neural Lyapunov Control (ANLC) 和 FOSSIL 2.0，两者均训练神经网络李雅普诺夫函数并采用CEGIS循环。
  - **解析方法**：Alfarano et al. (2024) 的预训练Transformer（全局搜索，仅适用于低维全局稳定系统）；Sum-of-Squares (SOS) 方法（使用SOSTOOLS，适用于多项式系统及经重铸的非多项式系统）。
- **对比指标**：成功发现有效李雅普诺夫函数的**成功率**（每个系统5个随机种子）、**训练/求解时间**、**最终验证时间**（SMT求解器dReal，容差e-3，精度e-12）。

### 4. 资源与算力

- 论文在“Computation Resources”部分说明：所有实验使用一台工作站，配备 AMD Ryzen Threadripper 2920X 12核CPU、Nvidia RTX 2080Ti 11GB GPU 和 Nvidia RTX 2080 8GB GPU。
- 未给出每个实验精确的GPU使用时长，但提供了整体不同系统的训练时间（如2-D系统约68-288秒，10-D系统约64223秒），训练可在单GPU上完成，算力需求不高。

### 5. 实验数量与充分性

- **数量**：主实验在11个系统上测试，每个系统5个随机种子报告成功率。此外，设计了三个消融实验：①风险寻求分位数 α 的影响（α=0.1, 0.5, 1）；②验证方法比较（SHGO vs. 根查找 vs. SMT vs. 随机采样）；③遗传编程及专家引导的影响（Transformer-only, GP-only, Transformer+GP, 全套）。
- **充分性与客观性**：
  - 覆盖维度从2到10，包含多项式与非多项式、全局与局部稳定、以及未知李雅普诺夫函数的真实挑战系统（有损电力系统），具有代表性。
  - 与四种基线比较，包括当前最先进的神经网络方法和解析方法，对比全面。
  - 消融实验从不同角度验证了核心组件（风险寻求策略、SHGO验证、GP引导）的有效性。
  - 但也存在局限：仅与ANLC和FOSSIL 2.0比较了部分系统（低维至6-D/8-D），更高维度下未展示基线结果（因为基线无法收敛或超时），对比不完整；SOS方法仅在多项式系统上测试，且高维局部稳定性下SOS超时，未给出失败时的详细数据。

### 6. 论文的主要结论与发现

- 所提方法能在众多非线性系统（最高10维）上成功发现有效的解析局部李雅普诺夫函数，成功率在多数系统上达到80%-100%。
- 与神经网络方法相比，虽然训练时间较长（低维系统ANLC/FOSSIL 2.0训练更快），但解析候选函数的验证效率极高（毫秒级），且可解释性强；神经网络方法在高维、非多项式系统上失败率较高。
- 与预训练Transformer（Alfarano et al. 2024）相比，该方法不需要大规模预训练数据集，且能处理非全局稳定系统。
- 与SOS方法相比，该方法能处理非多项式动力学的局部稳定性验证，且在高维局部稳定系统上SOS无法扩展。
- 首次为**2母线有损电力系统**发现了两个有效的解析局部李雅普诺夫函数，此前文献中未知。

### 7. 优点

- **创新性**：首次将风险寻求策略梯度与符号Transformer结合，实现从零开始直接搜索解析李雅普诺夫函数，无需预训练数据集。
- **可解释性与验证高效性**：输出解析表达式，结构简单；最终形式化验证时间极短（毫秒级），而神经网络需要数小时。
- **可扩展性**：成功应用于10维系统，以及非多项式真实系统（四旋翼、电力系统）。
- **发现未知函数**：在电力系统稳定性分析领域有实际贡献。
- **消融实验设计充分**：验证了风险寻求策略、SHGO验证、GP引导各自的作用，支撑了方法设计的合理性。

### 8. 不足与局限

- **实验覆盖**：与神经网络基线（ANLC、FOSSIL 2.0）的对比仅局限于低-中维系统（2-D至6-D），更高维度下基线超时或失败，缺乏直接的性能可比性；与SOS方法的对比也限于低维系统，高维局部稳定性SOS失败未给出失败原因细节。
- **偏差风险**：所有实验仅使用5个随机种子，成功率波动可能较大（如6-D Quadrotor成功率80%、9-D系统60%），尚需更多重复验证。
- **算力资源利用不明确**：未报告每个实验的具体GPU使用时间、超参数调优过程等，可复现性细节不足。
- **应用限制**：目前只能处理自治系统（或已知反馈律的闭环系统），未扩展至控制李雅普诺夫函数（CLF）或控制障碍函数（CBF）；最终验证依赖SMT求解器，对容差参数敏感（ϵ, δ），存在数值误差导致的误判风险。
- **训练稳定性**：SHGO验证提供对抗性反馈可能导致训练不稳定（如消融实验H.2中提到可能过拟合“硬”违反），需要结合随机采样平衡。

（完）
