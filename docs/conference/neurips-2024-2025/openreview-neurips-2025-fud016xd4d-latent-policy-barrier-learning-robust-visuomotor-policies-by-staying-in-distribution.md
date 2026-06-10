---
title: "Latent Policy Barrier: Learning Robust Visuomotor Policies by Staying In-Distribution"
title_zh: 潜在策略屏障：通过保持分布内学习鲁棒的视觉运动策略
authors: "Zhanyi Sun, Shuran Song"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=FUd016XD4d"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 利用控制屏障函数概念通过潜在屏障实现鲁棒策略学习
tldr: 本文提出潜在策略屏障（LPB），受控制屏障函数启发，将专家演示的潜在嵌入视为隐式屏障，使策略保持分布内以避免协变量偏移。该方法无需额外数据收集或数据增强，在多种机器人任务中显著提升了策略的鲁棒性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-fud016xd4d/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 721, \"height\": 436, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fud016xd4d/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1440, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fud016xd4d/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1407, \"height\": 242, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fud016xd4d/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1440, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fud016xd4d/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1353, \"height\": 628, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fud016xd4d/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1360, \"height\": 335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fud016xd4d/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1350, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fud016xd4d/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1365, \"height\": 776, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fud016xd4d/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1363, \"height\": 825, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fud016xd4d/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1079, \"height\": 608, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fud016xd4d/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1076, \"height\": 499, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-fud016xd4d/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1419, \"height\": 301, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fud016xd4d/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1014, \"height\": 175, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fud016xd4d/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 850, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fud016xd4d/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1406, \"height\": 180, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fud016xd4d/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 733, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fud016xd4d/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 732, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fud016xd4d/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 460, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fud016xd4d/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 470, \"height\": 414, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fud016xd4d/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 419, \"height\": 292, \"label\": \"Table\"}]"
motivation: 行为克隆策略容易因协变量偏移而失败，现有方法成本高或降低模仿质量。
method: 借鉴控制屏障函数思想，在潜在空间中构建屏障以分离安全与不安全状态。
result: 在多个视觉运动任务中增强了策略鲁棒性。
conclusion: LPB为鲁棒模仿学习提供了高效屏障方法。
---

## Abstract
Visuomotor policies trained via behavior cloning are vulnerable to covariate shift, where small deviations from expert trajectories can compound into failure. Common strategies to mitigate this issue involve expanding the training distribution through human-in-the-loop corrections or synthetic data augmentation. However, these approaches are often labor-intensive, rely on strong task assumptions, or compromise the quality of imitation. We introduce Latent Policy Barrier, a framework for robust visuomotor policy learning. Inspired by Control Barrier Functions, LPB treats the latent embeddings of expert demonstrations as an implicit barrier separating safe, in-distribution states from unsafe, out-of-distribution (OOD) ones. Our approach decouples the role of precise expert imitation and OOD recovery into two separate modules: a base diffusion policy solely on expert data, and a dynamics model trained on both expert and suboptimal policy rollout data.  At inference time, the dynamics model predicts future latent states and optimizes them to stay within the expert distribution. Both simulated and real-world experiments show that LPB improves both policy robustness and data efficiency, enabling reliable manipulation from limited expert data and without additional human correction or annotation. More details are on our anonymous project website https://latentpolicybarrier.github.io.

---

## 论文详细总结（自动生成）

# 论文详细总结：Latent Policy Barrier

## 1. 核心问题与整体含义
- **研究动机**：视觉运动策略（visuomotor policies）通过行为克隆（behavior cloning）学习时极易受到**协变量偏移（covariate shift）** 的影响——细微的动作偏差会逐步累积，导致任务失败。
- **现有方法的不足**：传统缓解策略（如 DAgger 式人工交互修正、合成数据增强）要么**劳动成本高昂**，要么依赖**强任务假设**，且可能引入**不一致或次优的示范数据**，在提升鲁棒性的同时损害了模仿的精确性。
- **核心含义**：本文提出**潜在策略屏障（Latent Policy Barrier, LPB）**，借鉴控制理论中的**控制屏障函数（Control Barrier Functions, CBF）** 思想，将专家演示在潜在空间中的嵌入视为一个**隐式屏障**，用以区分安全（分布内）与不安全（分布外）状态，从而实现无需额外人工干预的鲁棒策略学习。

## 2. 方法论
### 核心思想
- 将**精确模仿**与**分布外恢复**两个目标解耦，分别用两个独立模块完成：
  - **基础扩散策略**：仅用高质量专家数据训练，保证模仿的准确性。
  - **视觉潜在动力学模型**：同时利用专家数据和**自动收集的次优 Rollout 数据**训练，用于检测偏离并引导策略回归专家分布。
- 在推理时，利用动力学模型预测未来潜在状态，并通过梯度导向（gradient guidance）优化动作去噪过程，使预测状态尽量靠近专家潜在流形。

### 关键技术细节
1. **训练阶段**
   - **基础策略**：采用扩散策略（Diffusion Policy），视觉编码器与噪声预测网络端到端训练，仅使用少量高质量专家演示。
   - **动力学模型**：由**冻结的视觉编码器**（与基础策略共享）和**可学习的动力学预测器**（decoder-only transformer）组成。输入当前观测的潜在表示和未来动作序列，输出未来时刻的潜在观测，训练损失为预测潜在与真实潜在之间的 MSE。
   - **Rollout 数据收集**：在基础策略训练过程中，以固定间隔保存中间检查点并自动执行完整 episode，无论任务成功与否均保留所有转移。该过程无需任何人工标注或奖励信号。

2. **测试时优化（论文 Algorithm 1）**
   - 定义**潜在 OOD 得分**：当前观测的潜在表示与其在专家潜在集合中的最近邻之间的 L2 距离 $\delta(z) = \|z - z_{NN}\|_2^2$。
   - 若 $\delta(z_t) > \tau$（预设阈值），则触发**分布内回退引导**：
     - 在扩散去噪的最后 $K_{guide}$ 步，通过动力学模型预测未来潜在状态 $ \hat{z}_{t+h} = d_\phi(z_t, A_t^k)$。
     - 计算 OOD 得分关于动作的梯度，修正噪声预测：$\hat{\epsilon}(A_t^k) = \epsilon_\theta(A_t^k) - \eta \sqrt{1-\bar{\alpha}_k} \nabla_{A_t^k} \delta(\hat{z}_{t+h})$。
   - 若 $\delta(z_t) \leq \tau$，则直接输出来自基础策略的动作。

## 3. 实验设计
### 基准与数据集
- **模拟环境**：
  - **Push-T**（20% 专家演示）
  - **Robomimic**：三个最具挑战性的任务——Square、Tool Hang、Transport（均使用 20% 演示）
  - **Libero10**：语言条件的多任务基准（使用全部 50 个演示/任务）
- **真实机器人**：
  - **Cup Arrangement**（ARX5 臂，腕部 GoPro 相机，任务三阶段）
  - **Belt Assembly**（UR5 臂，NIST 主板组装挑战）

### 对比方法
- **Expert BC**：仅用专家数据的扩散策略
- **Mixed BC**：混入 Rollout 数据训练
- **Filtered BC**：仅保留成功 Rollout 与专家数据合并后重新训练
- **CCIL**：连续性数据增强的纠正行为克隆
- **CQL**：离线强化学习方法（需奖励函数）

### 评估设置
- 限制专家演示数量（通常 20%），测试样本效率和鲁棒性。
- 推理时扰动测试：对输出动作以概率 $p \in \{0.0, 0.1, 0.2, 0.3, 0.4\}$ 加入高斯噪声。
- 真实机器人：Cup Arrangement 在分布内/分布外初始位姿下各 20 次；Belt Assembly 40 次（变化初始位姿和板位置）。

## 4. 资源与算力
- **模拟实验**：单个 NVIDIA L40S GPU（46 GB VRAM），基础策略训练约 24-48 小时，动力学模型约 24 小时。
- **真实实验**：动力学模型在 **6 块 NVIDIA L40S GPU** 上并行训练，约 36 小时收敛；基础策略为预训练模型，无额外训练成本。
- **附录 B** 提供了所有任务的超参数表（表 5-9），包括 batch size、learning rate、rollout 收集计划等。

## 5. 实验数量与充分性
- **主要结果**（表 1）：覆盖 5 个模拟任务，每个任务报告 3 个不同 checkpoints 的均值和标准差，对比 5 种基线。
- **消融实验**（附录 A）：
  - 梯度导向超参数（引导尺度 $\eta$、引导步数 $K_{guide}$）
  - OOD 阈值 $\tau$
  - 动力学模型数据来源（策略 Rollout vs. 加噪演示 vs. epsilon-greedy）
  - 动作优化策略（classifier guidance vs. MPC vs. 梯度下降）
  - 潜在表示选择（BC 编码器 vs. DINOv2 vs. 重建编码器）
- **额外分析**：
  - 推理时扰动下的鲁棒性（图 4a）
  - 专家演示数量的影响（图 4b）
  - Rollout 数据量的影响（图 4c）
  - 潜在 OOD 得分可视化（图 5）
- **真实实验**：两个任务，各 20-40 次评估，结果以成功率柱状图呈现。
- **结论**：实验覆盖多种任务、多个基线、充分消融，统计上报告误差棒，设计较为公平客观。

## 6. 主要结论与发现
- LPB 在**有限演示**（20%）下**匹配或超越所有基线**，尤其在长时程高精度任务（Tool Hang 提升至 0.39 vs. Expert BC 的 0.27；Transport 提升至 0.85 vs. 0.68）上优势显著。
- 推理时**鲁棒性**明显优于 FCBC、Expert BC 和 CCIL，噪声干扰下退化最小。
- **样本效率高**：随着专家演示数量增加，LPB 在低数据量（≤60%）区间优势最大；随 Rollout 数据增加性能持续提升，说明动力学模型能从次优数据中获益。
- **潜在 OOD 得分**能有效检测偏离，LPB 的导向使状态保持接近专家流形（见图 5 和 8 的可视化）。
- 在**真实机器人**上，LPB 可即插即用增强预训练策略，在分布外初始位姿下显著提升成功率（Cup Arrangement: 从 0 提升至约 0.55；Belt Assembly: 从 0.55 提升至 0.75），且不损失分布内性能。

## 7. 优点
- **方法创新**：将控制屏障函数的概念引入模仿学习，通过在潜在空间构建隐式屏障，**无需显式定义安全集或系统动力学**。
- **高效的数据利用**：自动收集策略训练过程中产生的 Rollout 数据（包括失败轨迹），避免额外人工成本。
- **解耦设计**：基础策略专注精确模仿，动力学模型专注偏离恢复，缓解了精确性与鲁棒性之间的冲突。
- **即插即用**：可与现有预训练策略（如 UMI 预训练策略）结合，无需重新训练或微调基础策略。
- **实验充分**：模拟+真实，多种任务，多种基线，多个消融，结果可靠且可视化清晰。
- **代码开源**：提供匿名项目网站和代码，促进复现。

## 8. 不足与局限
- **短期校正**：仅能纠正局部短期偏离，对于严重或长期的错误无法有效恢复（论文在 Limitations 中明确指出）。
- **任务特定性**：动力学模型为每个任务单独训练，无法跨任务泛化，在多任务或新环境前需重新收集数据。
- **依赖专家训练数据**：OOD 阈值计算需要访问原始专家演示数据；若只有预训练策略而无配对训练数据，则无法直接使用。
- **超参数敏感性**：OOD 阈值 $\tau$ 和引导尺度 $\eta$ 需针对任务手动调整（附录 A.2 显示性能随阈值波动）。
- **缺乏理论保证**：虽然借鉴 CBF，但没有提供严格的稳定性或安全性保证，仅是经验性方法。
- **真实实验规模较小**：每项任务 20-40 次试验，可能不足以完全评估分布偏移下的行为差异。
- **计算开销**：推理时需额外运行动力学模型并计算梯度，增加延迟（尤其在去噪的最后 K 步）；对于高频控制任务可能需要优化。

（完）
