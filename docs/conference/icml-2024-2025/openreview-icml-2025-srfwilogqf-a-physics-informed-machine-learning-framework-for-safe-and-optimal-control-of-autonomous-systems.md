---
title: A Physics-Informed Machine Learning Framework for Safe and Optimal Control of Autonomous Systems
title_zh: 面向自主系统安全与最优控制的物理信息机器学习框架
authors: "Manan Tayal, Aditya Singh, Shishir Kolathaya, Somil Bansal"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=SrfwiloGQF"
tags: ["query:safe-rl-cbf"]
score: 9.0
evidence: 结合约束强化学习与控制屏障函数以实现安全最优控制
tldr: 自主系统安全与性能常相互竞争：CRL性能好但缺乏形式化安全保证，CBF等方法提供严格保证但过于保守。本文提出物理信息机器学习框架，联合优化CRL与CBF，在保持性能的同时获得形式化安全保证，实验表明在多种自主系统中实现了更优的安全-性能权衡。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-srfwilogqf/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1478, \"height\": 796, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-srfwilogqf/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1764, \"height\": 734, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-srfwilogqf/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 847, \"height\": 676, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-srfwilogqf/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 837, \"height\": 680, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-srfwilogqf/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1769, \"height\": 461, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-srfwilogqf/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1781, \"height\": 688, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-srfwilogqf/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1738, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-srfwilogqf/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1757, \"height\": 850, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-srfwilogqf/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1201, \"height\": 887, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-srfwilogqf/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1770, \"height\": 463, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-srfwilogqf/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1773, \"height\": 466, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-srfwilogqf/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1770, \"height\": 466, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-srfwilogqf/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1075, \"height\": 860, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-srfwilogqf/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 544, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-srfwilogqf/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1072, \"height\": 643, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-srfwilogqf/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1074, \"height\": 646, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-srfwilogqf/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1077, \"height\": 990, \"label\": \"Table\"}]"
motivation: 现有方法顾此失彼：CRL性能好但无安全保证，形式方法保守。
method: 提出物理信息框架，联合优化约束强化学习与控制屏障函数，实现安全与性能协同。
result: 在多个自主系统任务中取得了较低保守性的形式安全保证和良好性能。
conclusion: 该框架有效弥合了学习与形式方法在安全控制中的鸿沟。
---

## Abstract
As autonomous systems become more ubiquitous in daily life, ensuring high performance with guaranteed safety is crucial. However, safety and performance could be competing objectives, which makes their co-optimization difficult. Learning-based methods, such as Constrained Reinforcement Learning (CRL), achieve strong performance but lack formal safety guarantees due to safety being enforced as soft constraints, limiting their use in safety-critical settings. Conversely, formal methods such as Hamilton-Jacobi (HJ) Reachability Analysis and Control Barrier Functions (CBFs) provide rigorous safety assurances but often neglect performance, resulting in overly conservative controllers. To bridge this gap, we formulate the co-optimization of safety and performance as a state-constrained optimal control problem, where performance objectives are encoded via a cost function and safety requirements are imposed as state constraints. 
We demonstrate that the resultant value function satisfies a Hamilton-Jacobi-Bellman (HJB) equation, which we approximate efficiently using a novel physics-informed machine learning framework. In addition, we introduce a conformal prediction-based verification strategy to quantify the learning errors, recovering a high-confidence safety value function, along with a probabilistic error bound on performance degradation. Through several case studies, we demonstrate the efficacy of the proposed framework in enabling scalable learning of safe and performant controllers for complex, high-dimensional autonomous systems.

---

## 论文详细总结（自动生成）

# 中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：自主系统要求同时满足高性能（如高效导航、任务完成）和严格安全（避免碰撞、保护设备）。然而，安全和性能经常作为竞争目标存在，它们的协同优化非常困难。
- **现有方法局限**：
  - **约束强化学习（CRL）** 如 SAC-Lag、PPO-Lag、CPO 等虽能提升性能，但安全约束仅作为软约束（soft constraint）引入，缺乏形式化安全保证，在安全关键场景中不可信。
  - **形式化方法** 如 Hamilton-Jacobi (HJ) 可达性分析、控制屏障函数（CBF）提供严格安全保证，但往往忽略性能，导致过度保守的控制器（如 MPPI-CBF 安全率100%但成本极高）。
- **本文目标**：弥合上述两类方法的鸿沟，设计一种能同时提供 **形式化安全保证** 和 **接近最优性能** 的控制器，且能扩展到高维系统。

## 2. 方法论
### 核心思想
将安全–性能联合优化问题建模为 **状态约束最优控制问题（SC-OCP）**，并通过 **epigraph（上境图）重构** 转化为无约束形式，进而利用 **物理信息机器学习（Physics-Informed Machine Learning, PIML）** 高效求解相应的 Hamilton-Jacobi-Bellman（HJB）偏微分方程，最后通过 **共形预测（Conformal Prediction）** 提供高置信度的安全验证和性能退化量化。

### 关键技术细节
1. **SC-OCP 建模**：
   - 系统动力学：\(\dot{x}=f(x,u)\)；性能由成本 \(C(\cdot)\) 刻画（运行成本+终端成本）；安全由状态约束 \(g(x)\le 0\) 定义（失败集 \(F=\{x: g(x)>0\}\)）。
   - 原始问题：\(\min_u \int_t^T l(x)ds + \phi(x(T))\)，s.t. \(\dot{x}=f(x,u),\; g(x(s))\le 0,\;\forall s\)。

2. **Epigraph 重构**：
   - 引入辅助变量 \(z\)（可视为允许的最小成本）和辅助值函数 \(\hat{V}(t,x,z)=\min_u\max\{C(t,x,u)-z,\;\max_{s\in[t,T]}g(x(s))\}\)。
   - 原始值函数 \(V(t,x)=\min_{z\ge 0} z\) s.t. \(\hat{V}(t,x,z)\le 0\)。
   - 将 \(z\) 视为扩展状态（动态 \(\dot{z}=-l(x)\)），得到增广系统 \(\hat{x}=[x,z]^T\)。辅助值函数满足 HJB-PDE：
     \[
     \min\left\{-\partial_t\hat{V} - \min_u \langle\nabla_{\hat{x}}\hat{V},\hat{f}(\hat{x},u)\rangle,\; \hat{V}-g(x)\right\}=0
     \]
     边界条件：\(\hat{V}(T,\hat{x})=\max(\phi(x(T))-z,\;g(x))\)。

3. **物理信息机器学习求解**：
   - 用神经网络 \(\hat{V}_\theta\) 近似 \(\hat{V}\)，训练损失包括 PDE 残差损失 \(L_{\text{pde}}\) 和边界条件损失 \(L_{\text{bc}}\)，采用课程学习（先学习终止时间再向后传播）。
   - 通过自适应损失平衡（Wang et al., 2021）减少超参数 \(\lambda\) 的影响。

4. **安全验证（共形预测）**：
   - 学习误差可能导致 \(\hat{V}_\theta\) 判定为安全但实际轨迹不安全。引入一致性校正裕量 \(\delta\)，使得子 \(\delta\)-水平集内的状态在诱导策略下保持安全。
   - 共形预测定理（Theorem 3.1）：给定样本 \(N_s\)、允许违规率 \(\epsilon_s\)、置信度 \(\beta_s\)，可计算出 \(\delta\)，使得以概率至少 \(1-\beta_s\)，任意状态在 \(\hat{V}_\theta(0,\hat{x})\le\delta\) 时安全概率 \(\ge 1-\epsilon_s\)。

5. **性能量化（共形预测）**：
   - 定义归一化误差分数 \(p_i=|V_\theta(0,x_i)-V_{\pi_\theta}(0,x_i)|/C_{\max}\)。
   - 共形预测定理（Theorem 3.2）：以高置信度给出性能退化上界 \(\psi\)。

6. **策略生成**：通过二分搜索求解 epigraph 优化 \(V_\theta(t,x)=\min_z z\) s.t. \(\hat{V}_\theta(t,x,z)\le\delta\)，最优策略 \(\pi_\theta(t,x)=\arg\min_u\langle \nabla_{\hat{x}}\hat{V}_\theta(t,\hat{x}^*),\hat{f}(\hat{x}^*,u)\rangle\)。

## 3. 实验设计
### 场景与数据集
- **2D 船导航（Boat Navigation）**：2维状态，在带漂移的河流中避开两个圆形障碍物到达目标岛。成本为距离目标距离。
- **追车跟踪避障（Pursuer-Evader）**：8维状态（加速驱动追车+线性运动逃逸车），避开5个圆形障碍物同时逼近逃逸车。成本为追车与逃逸车距离。
- **多智能体导航（Multi-Agent Navigation）**：5个智能体（20维状态），各自到达指定目标点，避免相互碰撞（半径R安全距离）。成本为各智能体距离各自目标距离的均值。

### Benchmark 与对比方法
- **MPPI**（模型预测路径积分）：安全作为软约束。
- **MPPI-CBF**（MPPI + 控制屏障函数-QP）：安全过滤，硬约束。
- **CRL 方法**：SAC-Lagrangian、PPO-Lagrangian、CPO。
- 对于2D船导航，还对比了 Level Set Toolbox 计算的 **Ground Truth** 值函数。

### 评估指标
- **累计成本**（Cumulative Cost）
- **安全率**（Safety Rate）：轨迹从未进入失败集的百分比。
- **计算时间**：离线训练时间和在线推理时间。

### 超参数与配置
- 神经网络：3隐藏层 MLP，每层256神经元，Sine激活，Adam优化器，学习率 \(2\times10^{-5}\)。
- 训练样本：65,000点，预训练50–60K epoch，正式训练200K–400K epoch。
- 共形预测：\(N_s=N_p=300K\)，\(\epsilon_s=0.001\) 或 0.01，\(\beta_s=10^{-10}\)。

## 4. 资源与算力
- **文中明确提及**（附录 C.1）：
  - CPU：11th Gen Intel Core i9-11900K @ 3.50GHz × 16
  - 内存：128GB RAM
  - GPU：NVIDIA GeForce RTX 4090（用于训练）
- **训练时长**：
  - 2D 船导航：约122分钟（相比 Level Set 网格解法390分钟更少）
  - 追车和智能体系统未具体给出数值，但提到训练时间随维度增长呈次线性增加（从2D→8D增加很少，8D→20D略有增加）。
- **在线推理**：所有系统约2ms，适合实时应用。

## 5. 实验数量与充分性
- **三大类实验**：低维(2)、中高维(8)、超高维(20)，覆盖不同复杂度。
- **对比基线全面**：包括软约束(CRL)、硬约束过滤(MPPI-CBF)、采样优化(MPPI)，以及基于 Lagrange 的多种方法。
- **额外分析**：
  - 2D 任务有 ground truth 对比（MSE=0.36）。
  - 验证共形预测的理论-经验关系（图9），证实保守性。
  - 计算时间对比（离线/在线）。
- **充分性与公平性**：所有实验在同一硬件和相近超参数下运行，基线使用各自推荐设置。实验设计客观，结果清晰支持方法优越性。

## 6. 主要结论与发现
- **安全率**：本文方法在所有实验中保持 **100% 安全率**，而基线（如 SAC-Lag 仅 66%–76%，MPPI 约 72%–90%）安全率明显较低；MPPI-CBF 虽 100% 安全但成本极高。
- **性能（成本）**：本文方法累计成本在所有场景中最低，比最接近的基线（MPPI）低 18%–148%；尤其在多智能体场景中优势巨大（成本仅为 MPPI 的约 1/2.5）。
- **可扩展性**：从 2D 到 20D，PIML 方法计算时间呈次线性增长，而网格法指数级爆炸（8D以上不可行）。
- **共形预测的有效性**：经验安全违规率始终低于理论保证，验证了形式化安全界限的保守性和可靠性。
- **结论**：本文提出的框架成功弥合了学习型方法与形式化方法之间的鸿沟，实现了高性能与形式化安全保证的联合优化。

## 7. 优点
- **创新性**：首次将物理信息神经网络（PINN）与状态约束最优控制的 epigraph 重构结合，并集成共形预测提供可量化保证。
- **安全+性能兼顾**：同时提供高置信度的形式化安全保证和接近最优的性能，优于所有基线。
- **可扩展性**：适用于高维系统（20维），规避了传统动态规划维数灾难。
- **理论完善**：提供两个共形预测定理（安全验证、性能量化），并有理论推导和实验验证。
- **实时可用**：在线推理仅需2ms，适合实际机器人控制。

## 8. 不足与局限
- **依赖模型已知**：论文假设动力学已知（但指出可学习），实际系统中模型误差可能影响性能。
- **离线训练耗时**：虽然比网格法快，但仍需数小时训练（122–数小时），可能不适合需要快速部署的场景。
- **共形预测样本需求**：需要大量校准样本（\(N_s=N_p=300K\)），在某些资源受限环境中可能难以满足。
- **未考虑动态环境**：目前假设环境固定，未来工作提到需探索环境或安全约束变化时的快速适应。
- **缺乏真实机器人实验**：全部基于仿真，实际硬件中的传感器噪声、执行误差等未验证。
- **性能量化界限依赖于 \(C_{\max}\)**：该最大值可能在实际场景中难以严格计算或上界过高导致界限宽松。

---

（完）
