---
title: "From Uncertain to Safe: Conformal Adaptation of Diffusion Models for Safe PDE Control"
title_zh: 从不确定到安全：扩散模型的共形自适应用于安全PDE控制
authors: "Peiyan Hu, Xiaowei Qian, Wenhao Deng, Rui Wang, Haodong Feng, Ruiqi Feng, Tao Zhang, Long Wei, Yue Wang, Zhi-Ming Ma, Tailin Wu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=XGJ33p4qwt"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 使用扩散模型实现偏微分方程控制的安全约束，涉及安全控制
tldr: 本文提出SafeDiffCon，结合扩散模型和不确定性分位数，在偏微分方程约束控制中确保安全性。通过后训练和推理阶段引入安全约束，实现最优控制。为工程系统中的安全控制提供了新方法。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-xgj33p4qwt/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1153, \"height\": 505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-xgj33p4qwt/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 856, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-xgj33p4qwt/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1314, \"height\": 282, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-xgj33p4qwt/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 955, \"height\": 1550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-xgj33p4qwt/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1633, \"height\": 1704, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 838, \"height\": 467, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 647, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 687, \"height\": 424, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 703, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1496, \"height\": 151, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 740, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 895, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 670, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 576, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 499, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1766, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 950, \"height\": 195, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 642, \"height\": 461, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 712, \"height\": 720, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1232, \"height\": 848, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1122, \"height\": 848, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 914, \"height\": 419, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 915, \"height\": 419, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 704, \"height\": 631, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 748, \"height\": 630, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-xgj33p4qwt/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 556, \"height\": 416, \"label\": \"Table\"}]"
motivation: 现有深度学习方法在PDE约束控制中很少考虑安全要求。
method: 后训练扩散模型生成满足安全约束的控制序列，并引入不确定性分位数加权损失。
result: 在安全约束下实现更优的控制目标，同时提高安全性。
conclusion: SafeDiffCon为安全关键控制提供了结合不确定量化的新范式。
---

## Abstract
The application of deep learning for partial differential equation (PDE)-constrained control is gaining increasing attention. However, existing methods rarely consider safety requirements crucial in real-world applications. To address this limitation, we propose Safe Diffusion Models for PDE Control (SafeDiffCon), which introduce the uncertainty quantile as model uncertainty quantification to achieve optimal control under safety constraints through both post-training and inference phases. Firstly, our approach post-trains a pre-trained diffusion model to generate control sequences that better satisfy safety constraints while achieving improved control objectives via a reweighted diffusion loss, which incorporates the uncertainty quantile estimated using conformal prediction. Secondly, during inference, the diffusion model dynamically adjusts both its generation process and parameters through iterative guidance and fine-tuning, conditioned on control targets while simultaneously integrating the estimated uncertainty quantile. We evaluate SafeDiffCon on three control tasks: 1D Burgers' equation, 2D incompressible fluid, and controlled nuclear fusion problem. Results demonstrate that SafeDiffCon is the only method that satisfies all safety constraints, whereas other classical and deep learning baselines fail. Furthermore, while adhering to safety constraints, SafeDiffCon achieves the best control performance. The code can be found at https://github.com/AI4Science-WestlakeU/safediffcon.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：现有深度学习方法在偏微分方程（PDE）约束控制中表现优秀，但几乎完全忽略了安全约束。在流体控制、核聚变等高危实际场景中，违反安全约束可能导致灾难性后果。因此，急需一种既能优化控制目标又能严格满足安全约束的算法。
- **核心问题**：离线控制面临分布偏移（训练数据包含次优甚至不安全样本），且安全与性能之间存在固有矛盾。现有方法（如行为克隆、MPC、RL）难以同时满足安全与最优性。
- **整体含义**：论文提出 **SafeDiffCon**，首次将**共形预测（Conformal Prediction）** 引入扩散模型的安全控制，通过量化不确定性（不确定性分位数）并应用于后训练和推理微调，实现了在多个PDE控制任务中**零安全违规**且**最优控制性能**。

## 2. 方法论：核心思想、关键技术、公式流程
- **核心思想**：利用共形预测为扩散模型估计一个**不确定性分位数**，基于该分位数构造一个“安全置信区间”。在模型分布偏移时，该区间能以概率(1-\alpha)覆盖真实安全得分。然后将此分位数融入损失函数和引导过程，迫使模型产出既安全又高效的控制序列。
- **关键技术**：
  1. **不确定性量化（Uncertainty Quantile）**：  
     - 划分校准集 \(D_{cal}\)，计算每个样本的预测误差 \(\Delta s_i = |s(u_\theta(w_i)) - s(u_i)|\)。  
     - 考虑分布偏移，对误差进行加权：\(\tilde{S} = \{\omega_{\text{norm}}(u_i,w_i)\Delta s_i\}\)，权重 \(\omega \propto e^{-W(u,w)}\)。  
     - 取加权误差集的 \((1-\alpha)(1+1/|D_{cal}|)\) 分位数作为**不确定性分位数** \(Q\)。  
     - 得到共形区间 \(CI = [s(u_\theta(w))-Q,\; s(u_\theta(w))+Q]\)，保证真实 \(s\) 落入的概率 \(\ge 1-\alpha\)。
  2. **后训练（Post-training）**：  
     - 定义惩罚项 \(W(u,w) = \max[s(u)+Q - s_0,\,0] + \gamma J(u,w)\)。  
     - 使用**重加权扩散损失** \(L_{\text{post-train}} = \mathbb{E}[e^{-W(u,w)} \|\epsilon - \epsilon_\theta\|^2]\) 对预训练模型进行微调，使模型分布偏移至安全和更优的区域。
  3. **推理时微调（Inference-time Fine-tuning）**：  
     - 在生成过程中，用相同的 \(W\) 作为引导（Guidance）逐步调整输出。  
     - 同时对模型参数进行少量梯度更新（保留最后一步计算图），损失函数为 \(\sum W(u_\theta,w_\theta)\)，进一步提升特定任务下的安全性和性能。
- **算法流程**（文字说明）：
  1. 用原始训练数据预训练扩散模型 \(\theta\)（学习联合分布 \(p(u,w)\)）。
  2. 基于校准集计算不确定性分位数 \(Q\)。
  3. 执行后训练（重加权损失），更新 \(\theta\) 多次。
  4. 针对具体控制任务，循环执行：采样（含引导）→ 计算微调损失 → 更新 \(\theta\)，若干轮后输出最终控制序列。

## 3. 实验设计
- **数据集/场景**（三个任务，覆盖不同物理系统）：
  - **1D Burgers 方程**：控制最终状态与目标状态一致，安全得分 \(s = \sup u^2\)，阈值 \(s_0 = 0.64\)。训练集约 39000 条（89.7% 不安全），校准集 1000 条，测试集 50 条全不安全。
  - **2D 不可压缩流体**（Navier-Stokes）：控制烟雾通过目标桶，同时避开红色危险区域，安全得分 \(s\) 为进入危险区的烟雾比例，\(s_0 = 0.1\)。训练集 53.1% 不安全。
  - **托卡马克聚变**（Tokamak）：控制等离子体参数 \(\beta_p\) 和 \(l_i\) 达到目标，安全约束 \(q_{95} > 4.98\)，训练集 71.18% 不安全。
- **Benchmark**：所有实验均使用真实物理模拟器（数值求解器）评估控制结果，安全指标包括样本不安全率（\(R_{\text{sample}}\)）、时间步不安全率（\(R_{\text{time}}\)）、空间点不安全率（\(R_{\text{point}}\)）以及安全违规幅度（**SVM**）。
- **对比方法**：BC、BC-Safe（仅用安全数据）、PID、SL-Lag（监督学习+拉格朗日）、MPC-Lag（模型预测控制+拉格朗日）、CDT（约束决策Transformer）、TREBI（扩散模型规划）。其中 CDT 为离线安全 RL 最强基线。

## 4. 资源与算力
- 论文**未明确说明**训练所使用的 GPU 型号、数量及总训练时长。仅在附录 B.1 给出推理时间对比：在 **A800 单卡 + 8 CPU** 上，SafeDiffCon 推理 50 条轨迹约需 **2.36 分钟**，远快于 TREBI（13.55 分钟），但慢于 BC（0.14 分钟）等轻量方法。训练算力需求未披露。

## 5. 实验数量与充分性
- **实验数量**：共 3 个物理场景，每个场景均报告了方法对比表。此外还有：
  - **消融实验**（第 5.4 节及附录 B.2）：在 2D 流体上移除后训练、推理微调、不确定性分位数；在 Burgers 和 Tokamak 上也做了补充消融。
  - **参数敏感性分析**（附录 B.3）：对覆盖率 \(\alpha\)、训练/校准分裂比例、目标权重 \(\gamma\) 进行实验，显示结果相对稳健。
- **充分性**：实验覆盖了不同维度和复杂度的 PDE 问题，对比基线包括了经典控制、模仿学习、离线安全 RL、扩散规划等主流方法。消融实验清晰展示了各组件的必要。
- **客观性与公平性**：所有方法使用相同的数据划分和评估规程；对于 CDT，进行了返回/成本参数扫描以寻找最佳超参数（附录 I.1）；对于 TREBI，在 Burgers 上采用了多步规划（允许交互）这种不利优势进行分析，但结果仍不如 SafeDiffCon。因此实验设计较为严谨。

## 6. 主要结论与发现
- **安全唯一性**：在三个任务中，**SafeDiffCon 是唯一在所有测试轨迹上满足安全约束的方法**（\(R_{\text{sample}}=0\)），且同时获得了**最低的控制目标值 J**（性能最优）。
- **组件必要性**：消融实验表明，去除后训练、推理微调或不确定性分位数任一组件均会导致安全违规，证明三者各有不可或缺的作用。
- **参数鲁棒性**：覆盖概率 \(\alpha\)、训练/校准分割比例、目标权重 \(\gamma\) 在一定范围内变化时，模型仍保持安全且性能稳定。

## 7. 优点
- **方法创新**：首次将共形预测框架融入安全控制，提供了**有理论保证**的安全区间，有效应对离线设置下的分布偏移。
- **双阶段优化**：后训练（全局分布迁移）+ 推理微调（任务特定精确调整）结合，兼顾了安全与最优性。
- **广泛的实证验证**：在三个具有代表性的物理系统（一维/二维流体、核聚变）上进行实验，结果一致证明其有效性。
- **可复现性**：开源代码，并提供详细的超参数和网络结构（附录 F-H）。

## 8. 不足与局限
- **实验覆盖局限**：仅测试了中低维系统（1D/2D），未涉及更高维度（如 3D）或实时控制场景。令牌环聚变任务中的状态维度较低。
- **算力开销**：推理时间（2.36 分钟）仍显著高于传统方法（BC 0.14 分钟），限制了实时应用潜力。训练算力未报告，但可推断需要较大资源。
- **理论假设**：共形预测的覆盖保证依赖于弱交换性。虽然论文考虑了协变量偏移，但在更强的对抗性分布偏移或非平稳环境下，理论保证可能弱化。
- **基线对比不足**：未与近期的安全离线 RL 方法（如 **FISOR**、**CPQ**）进行比较，仅与 CDT 和 TREBI 对比。且 TREBI 的实现与原始论文略有不同（多步规划可能具有不公平优势），但论文已承认并处理。
- **安全与性能的权衡**：在 2D 流体任务中，SafeDiffCon 的 J（-0.3548）比未安全约束的 BC（-0.7104）明显更高，说明为了安全牺牲了部分性能，未给出理论最优权衡。

（完）
