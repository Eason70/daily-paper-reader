---
title: "VNN: Verification-Friendly Neural Networks with Hard Robustness Guarantees"
title_zh: VNN：具有硬鲁棒性保证的验证友好神经网络
authors: "Anahita Baninajjar, Ahmed Rezine, Amir Aminifar"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=gUFufRkzjV"
tags: ["query:safe-rl-cbf"]
score: 4.0
evidence: 面向安全关键应用的神经网络验证
tldr: 深度神经网络缺乏形式化正确性保证，验证面临可扩展性和精度挑战。VNN框架通过后训练优化生成验证友好的神经网络，提供硬鲁棒性保证，使形式化验证更为可行。该方法在保持精度的同时大幅降低了验证复杂度。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-gufufrkzjv/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1624, \"height\": 574, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-gufufrkzjv/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 658, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-gufufrkzjv/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 661, \"height\": 518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-gufufrkzjv/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1628, \"height\": 579, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-gufufrkzjv/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 658, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-gufufrkzjv/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 660, \"height\": 520, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-gufufrkzjv/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1701, \"height\": 380, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-gufufrkzjv/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1768, \"height\": 614, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-gufufrkzjv/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 591, \"height\": 307, \"label\": \"Table\"}]"
motivation: 深度学习缺乏形式化保证，现有验证技术可扩展性和精度不足。
method: 提出后训练优化框架，生成验证友好的神经网络，以降低验证复杂度。
result: 在多个数据集上实现了硬鲁棒性保证，同时保持模型精度。
conclusion: VNN提升了神经网络在安全关键应用中的可验证性。
---

## Abstract
Machine learning techniques often lack formal correctness guarantees, evidenced by the widespread adversarial examples that plague most deep-learning applications. This lack of formal guarantees resulted in several research efforts that aim at verifying Deep Neural Networks (DNNs), with a particular focus on safety-critical applications. However, formal verification techniques still face major scalability and precision challenges. The over-approximation introduced during the formal verification process to tackle the scalability challenge often results in inconclusive analysis. To address this challenge, we propose a novel framework to generate Verification-Friendly Neural Networks (VNNs). We present a post-training optimization framework to achieve a balance between preserving prediction performance and verification-friendliness. Our proposed framework results in VNNs that are comparable to the original DNNs in terms of prediction performance, while amenable to formal verification techniques. This essentially enables us to establish robustness for more VNNs than their DNN counterparts, in a time-efficient manner.

---

## 论文详细总结（自动生成）

### 中文总结：VNN: 具有硬鲁棒性保证的验证友好神经网络

#### 1. 核心问题与整体含义（研究动机和背景）
- **问题**：深度神经网络（DNN）在安全关键应用中缺乏形式化正确性保证，易受对抗样本攻击。现有形式化验证方法（如过近似技术）虽旨在提高可扩展性，但引入的近似误差常导致验证结果不明确（即无法判定鲁棒性）。
- **目标**：提出一种**后训练优化框架**，生成**验证友好神经网络（VNN）**，在保持预测性能的同时，使验证工具能更高效、更广泛地建立硬鲁棒性保证。

#### 2. 方法论：核心思想、关键技术细节、算法流程
- **核心思想**：通过**层间稀疏正则化**（L0→L1松弛）和**硬约束**（保持网络输出类别、神经元激活状态、输出变化范围）来降低验证时的过近似累积。
- **关键技术细节**：
  - **逐层优化**：针对第 \(l\) 层的权重 \(\tilde{W}^{(l)}\) 和偏置 \(\tilde{b}^{(l)}\)，最小化 \(\|\tilde{W}^{(l)}\|_{1,1} + \|\tilde{b}^{(l)}\|_{1}\)（L1松弛）。
  - **约束条件**：
    - 神经元激活状态不变：如果原始神经元活跃（\(f_{l,i}(x^{(l-1)})>0\)），则新权重应保持 \(\tilde{W}_{i,:}^{(l)} x^{(l-1)} + \tilde{b}_i^{(l)} \ge 0\)；否则 \(\le 0\)。
    - 后续层状态一致：保证优化后所有后续神经元的激活/非激活状态与原始网络一致（利用ReLU分段线性）。
    - 输出差异约束：\(\|\tilde{x}^{(l)} - x^{(l)}\|_\infty \le \epsilon\)，允许小幅变化。
    - 最终分类结果不变：\(\arg\max x^{(N)} = \arg\max \tilde{x}^{(N)} = y\)。
  - **算法流程**：
    1. 从输入层开始，对每个隐藏层依次求解线性规划（使用Gurobi求解器）。
    2. 固定已优化层的参数，继续优化下一层，直至输出层。
    3. 可选择不同 \(\epsilon\) 值（0, 0.1, 0.2, 0.3）来控制松弛程度。
- **形式化表述**：整体优化问题（式(11)）是一个线性规划，包含目标函数（L1范数）和线性/分段线性约束。

#### 3. 实验设计
- **数据集与场景**：
  - **MNIST**（手写数字）：经典图像分类，测试验证友好性。
  - **CHB-MIT**（癫痫脑电图）：真实安全关键医疗应用（癫痫检测）。
  - **MIT-BIH**（心电图心律失常）：另一安全关键医疗应用（心律异常检测）。
- **Benchmark与对比方法**：
  - **原始DNN**（未优化）。
  - **幅度剪枝（MBP）**：阈值法将最小权重置零。
  - **稀疏优化剪枝（SOP）**：训练中引入稀疏优化。
  - **对抗训练（PGD）**：使用PGD训练的网络。
  - **验证工具**：ERAN（基于抽象解释的过近似）和SafeDeep（增量细化凸近似）；部分实验使用精确验证工具Marabou（SMT求解）。
- **网络结构**：
  - MNIST：全连接网络（2×50, 2×100, 5×100, 5×200, 8×100, 8×200, 6×500, 7×200）。
  - CHB-MIT/MIT-BIH：小规模CNN（2-3个隐藏层）。
- **评估指标**：验证鲁棒性百分比（在不同扰动 \(\delta\) 下）、平均验证时间、模型准确率。

#### 4. 资源与算力
- **文中明确说明**：使用**Gurobi求解器**在 **MacBook Pro（8核CPU，32 GB RAM）** 上实现。**未使用GPU**。
- **时间成本**：VNN生成时间随层数线性增长（如2×50网络约40秒，8×200网络约618秒）。验证时VNN比原始DNN快至多3倍。

#### 5. 实验数量与充分性
- **实验数量**：覆盖3个数据集、多种网络结构（13种以上）、多组扰动 \(\delta\)（每数据集5-6个）、多组 \(\epsilon\) 值（0, 0.1, 0.2, 0.3）、多种对比方法（MBP, SOP, PGD）、消融实验（优化层数、超参数影响）。总计超过50组不同配置的鲁棒性验证结果。
- **充分性与公平性**：
  - 实验设计较全面，包括小/中/大规模网络、医疗实际场景。
  - 对比了多种剪枝方法，且考虑了不同剪枝率（MBP-10%~90%）。
  - 使用了两种不同验证工具（ERAN、SafeDeep）及精确验证（Marabou），增强结论可靠性。
  - 但**仅使用ReLU激活函数**，未测试其他非线性函数（如tanh, sigmoid）；验证集大小可能影响大规模网络（如8×200）的泛化。

#### 6. 主要结论与发现
- **验证友好性大幅提升**：VNN在多数扰动下验证鲁棒性样本数比原始DNN高**24~76倍**（MNIST）；医疗数据CHB-MIT高**24倍**，MIT-BIH高**34倍**。
- **验证时间效率**：VNN验证时间最多为原始DNN的**三分之一**。
- **精度保持**：VNN与原始DNN精度相当（差异通常在1-3%内），而剪枝方法（MBP/SOP）在高稀疏度下精度下降明显。
- **优于剪枝方法**：VNN比MBP和SOP验证友好度**高46倍以上**，且不依赖启发式阈值。
- **可与对抗训练结合**：VNN进一步提升PGD对抗训练网络的验证友好性。
- **Robustness增强**：VNN本身更鲁棒（在精确验证中，无任何情况VNN不鲁棒而原始DNN鲁棒）。

#### 7. 优点
- **方法论创新**：将“验证友好性”作为显式优化目标，并保证硬鲁棒性约束，而非仅通过剪枝/量化简单近似。
- **实用性强**：后训练阶段即可应用，不依赖修改训练过程，兼容现有验证工具。
- **迁移性**：可扩展到其他分段线性激活函数（如Leaky ReLU），且能结合对抗训练等防御手段。
- **实验全面**：覆盖不同规模网络、不同数据集（含医疗安全关键）、多种验证工具，消融分析充分。

#### 8. 不足与局限
- **激活函数限制**：仅针对ReLU设计，未验证其他非线性函数（如tanh、sigmoid）的适用性。
- **验证集规模依赖**：当网络较大而验证集较小时（如8×200，200个样本），增大 \(\epsilon\) 会导致精度下降（Fig.4b），表明泛化能力受限于验证集代表性。
- **计算开销**：优化过程本身需要求解线性规划，对超大规模网络（如ResNet-50）可能耗时较长（未实验）。
- **精确验证局限性**：即使VNN在精确验证（Marabou）中时延少于原始DNN，但仍有大量样本超时（>75%），说明完全精确验证仍不易。
- **仅限分类任务**：未讨论回归、目标检测等其他任务类型。

（完）
