---
title: "FESSNC: Fast Exponentially Stable and Safe Neural Controller"
title_zh: FESSNC：快速指数稳定且安全的神经控制器
authors: "Jingdong Zhang, Luan Yang, Qunxi Zhu, Wei Lin"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=cVp8blEw2i"
tags: ["query:safe-rl-cbf"]
score: 9.0
evidence: 神经网络控制器同时保证指数稳定性和安全性
tldr: 本文提出快速指数稳定安全神经控制器，针对随机非线性系统同时实现严格指数稳定性和几乎必然安全性。通过启发式学习和投影算子确保学习控制器的稳定与安全，为基于神经网络的安全控制提供了新范式。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-cvp8blew2i/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 839, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-cvp8blew2i/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 669, \"height\": 333, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-cvp8blew2i/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 844, \"height\": 330, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-cvp8blew2i/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 836, \"height\": 323, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-cvp8blew2i/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 847, \"height\": 337, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-cvp8blew2i/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 838, \"height\": 324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-cvp8blew2i/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1508, \"height\": 587, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-cvp8blew2i/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 856, \"height\": 510, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-cvp8blew2i/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 714, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-cvp8blew2i/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1636, \"height\": 521, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-cvp8blew2i/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1618, \"height\": 524, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-cvp8blew2i/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1787, \"height\": 563, \"label\": \"Table\"}]"
motivation: 现有方法难以同时保证随机非线性系统的指数稳定性和安全性。
method: 设计启发式方法学习稳定和安全控制器，并开发投影算子严格确保稳定性和安全性。
result: 在随机动态上实现快速学习，同时满足指数稳定和几乎必然安全。
conclusion: FESSNC为神经网络安全控制提供了理论严谨且实用的方法。
---

## Abstract
In order to stabilize nonlinear systems modeled by stochastic differential equations, we design a Fast Exponentially Stable and Safe Neural Controller (FESSNC) for fast learning controllers. Our framework is parameterized by neural networks, and realizing both rigorous exponential stability and safety guarantees. Concretely, we design heuristic methods to learn the exponentially stable and the safe controllers, respectively, in light of the classical theory of stochastic exponential stability and our established theorem on guaranteeing the almost-sure safety for stochastic dynamics. More significantly, to rigorously ensure the stability and the safety guarantees for the learned controllers, we develop a projection operator, projecting to the space of exponentially-stable and safe controllers. To reduce the highly computational cost for solving the projection operation, approximate projection operators are delicately proposed with closed forms that map the learned controllers to the target controller space. Furthermore, we employ Hutchinson's trace estimator for a scalable unbiased estimate of the Hessian matrix that is used in the projection operator, which thus allows for reducing computational cost and, therefore, can accelerate the training and testing processes. More importantly, our approximate projection operations are applicable to the nonparametric control methods, improving their stability and safety performance. We empirically demonstrate the superiority of the FESSNC over the existing methods.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：如何为随机微分方程（SDE）描述的非线性系统设计一个控制器，既能保证系统的**指数稳定性**（解以指数速度几乎必然收敛到平衡点），又能保证**几乎必然安全性**（所有轨迹始终位于预定义的紧致安全区域内），同时控制器可以**快速学习**（训练和推理阶段计算高效）。
- **背景动机**：现有神经控制器（如Neural Lyapunov Control, Neural Stochastic Control）通常基于有限样本训练，缺乏在整个状态空间上严格满足稳定性条件的保证；安全性方面，大多数安全控制方法（如二次规划QP、和（Sum-of-Squares SOS）方法）计算代价高，或仅能以概率小于1保证安全，不能满足安全关键应用中的“几乎必然”要求。因此，需要一种既有理论严谨性又计算高效的框架。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **整体框架（FESSNC）**：两阶段流程。
  1. **启发式训练**：使用神经网络参数化控制器 \(u_\theta\)、势函数 \(V_\theta\) 和类K函数 \(\alpha_\theta\)，通过设计包含稳定性损失和安全损失的总损失函数 \(L(\theta)=L_{es}(\theta)+L_{sf}(\theta)\) 进行训练。
  2. **后训练投影**：利用近似投影算子 \(\hat{\pi}_{es}\) 和 \(\hat{\pi}_{sf}\) 将学习到的控制器投影到指数稳定控制器空间和安全控制器空间，从而获得严格的理论保证。

- **关键技术细节**：
  - **指数稳定性损失**（定义3.1）：
    \[
    L_{es}(\theta)=\frac{1}{N}\sum_i\left[u_\theta(x_i)^T R u_\theta(x_i) + \lambda_1 \max(0, L_{u_\theta}V_\theta(x_i)-c V_\theta(x_i))\right]
    \]
    其中 \(L_{u}V = \nabla V^T f_u + \frac{1}{2}\mathrm{Tr}(g^T H_V g)\)。
  - **安全性损失**（定义4.2）：
    \[
    L_{sf}(\theta)=\frac{1}{N}\sum_i\left[u_\theta(x_i)^T R u_\theta(x_i) + \lambda_2 \max(0, -L_{u_\theta}h(x_i)-\alpha_\theta(h(x_i)))\right]
    \]
    其中 \(h\) 为零阻碍函数（Zeroing Barrier Function）。
  - **近似投影算子**：
    - 稳定性投影：\(\hat{\pi}_{es}(u,U_{es}) = u - \frac{\max(0, L_u V - c V)}{\|\nabla V\|^2} \nabla V\)（定理3.1）。要求状态空间有界才能保证Lipschitz连续性。
    - 安全性投影：\(\hat{\pi}_{sf}(u,U_{sf}) = u + \frac{\max(0, -L_u h - \alpha(h))}{\|\nabla h\|^2} \nabla h\)（定理4.2）。要求 \(C\) 有界且 \(\nabla h(0)=0\)。
  - **复合保证**：先应用 \(\hat{\pi}_{sf}\) 获得安全控制器，此时状态空间限制在紧集 \(C\) 内，再应用 \(\hat{\pi}_{es}\) 获得指数稳定性保证（定理4.4证明交集非空）。
  - **加速计算**：
    - 当扩散项 \(g\) 为矩阵（\(r>1\)）时：使用Hutchinson迹估计 \(\mathrm{Tr}[g^T H_V g] \approx \frac{1}{M}\sum_{i=1}^M (\nabla(\xi_i^T \nabla V))^T g g^T \xi_i\)，复杂度从 \(O(Nd^2)\) 降至 \(O(NMd)\)，通常取 \(M=1\)。
    - 当 \(g\) 为向量（\(r=1\)）时：利用恒等式 \(\mathrm{Tr}[g^T H_V g] = g^T \nabla((g.\mathrm{detach}())^T \nabla V)\)，复杂度降至 \(O(Nd)\)。
  - **算法流程**（Algorithm 1）：采样子数据 → 计算损失 → 更新参数 → 后处理投影。

## 3. 实验设计：数据集/场景、benchmark、对比方法

- **实验场景**：
  1. **双摆（Double Pendulum）**：4维系统（2角度+2角速度），加性乘性噪声。目标：将摆稳定到倒立位置，同时保证内摆角度在 \([-\pi/6, 7\pi/6]\) 内。
  2. **平面运动自行车模型（Kinetic Bicycle）**：4维系统（位置x,y、方向θ、速度v），噪声扰动。目标：使自行车到达目标点（0,0），安全区域为半径2的圆内。
  3. **耦合FHN振荡器同步（FitzHugh-Nagumo）**：50个节点的随机耦合网络，100维状态。目标：同步到同步流形，安全约束为每个节点模值不超过5。
  4. **三连杆摆（3-link Pendulum）**：6维系统，用于验证非参数控制器扩展。

- **Benchmark**：使用 Euler–Maruyama 方法近似SDE的流映射得到MDP，进行模型评估。

- **对比方法**：
  - 经典方法：GP-MPC（高斯过程模型预测控制）、BALSA（贝叶斯自适应安全控制，基于QP）。
  - 学习型方法：SYNC（基于网格的安全神经控制）、NNDMC（神经网络动态模型安全控制）、RSMC（基于超鞅的随机稳定验证）、RSMC+ICNN（将RSMC中的势函数替换为ICNN）。
  - 非参数方法：基于核方法的控制器（Kernel），以及应用投影算子后的FESS+Kernel。

## 4. 资源与算力

- 论文中明确说明计算设备为“single i7-10870 CPU with 16GB memory”，**未使用GPU**。
- 训练时长：双摆任务约10.35秒，自行车任务约6.39秒；与对比方法相比（如GP-MPC 146.64/26.68秒，BALSA 3.08/2.18秒），FESSNC介于两者之间。
- 对于学习型方法对比（表2），FESSNC训练时间14秒，低于其他方法（SYNC 125秒，NNDMC 209秒，RSMC 435秒，RSMC+ICNN 987秒）。
- 所有参数使用Adam优化器训练。

## 5. 实验数量与充分性

- **实验组数**：
  - 每个场景（双摆、自行车）进行**5次独立实验**（不同随机种子：{1,4,6,8,9} 和 {3,5,6,9,10}），绘制均值曲线和方差区域。
  - 与学习型方法对比时，使用**10个种子** {3,6,9,10,11,12,14,15,16,28}。
  - 耦合FHN实验使用**5个种子** {1,4,5,9,15}。
  - 消融实验：对超参数 \(\{k, \lambda_1, \lambda_2\} \in \{0.1, 0.5, 1.0\}^3\) 共27种组合，每种用10条轨迹测试。
- **公平性**：所有方法使用相同的训练步数（500步）和batch大小（500），测试条件一致（20秒仿真时间）。对比方法使用其原文推荐设置。
- **充分性**：涵盖了2个经典控制基准、1个高维同步任务、1个非参数扩展、以及详细的消融分析。实验设计比较全面，但缺乏在更高维系统（如>100维）上的规模扩展测试。

## 6. 论文的主要结论与发现

- FESSNC在所有任务中均能以**100%安全率**和**100%成功率**完成任务，而GP-MPC和BALSA在稳定性或安全性上存在缺陷（例如GP-MPC无法长期平衡摆，BALSA因预定义势函数不合理导致性能差）。
- 与学习型方法对比（表2）：FESSNC是唯一同时提供**指数稳定性**和**几乎必然安全性**理论保证的方法，且计算复杂度仅为 \(O(d)\)（线性），避免其他方法的维度灾难（\(O(k d d^2)\) 或 \(O(k d d^3)\)）。
- 近似投影算子能提升非参数控制器（Kernel）的性能，表明框架通用性。
- 消融实验显示：FESSNC对超参数选择不敏感，不同组合下均能保持良好表现（误差<0.11，最大半径<2，安全）。

## 7. 优点

- **理论严谨**：首次为神经控制器同时提供指数稳定性（a.s.）和安全性（a.s.）的严格数学保证，而非数值近似。
- **计算高效**：通过Hutchinson迹估计和向量雅可比积技巧，将训练和投影阶段的复杂度从 \(O(d^2)\) 降至 \(O(d)\) 或 \(O(Md)\)，可扩展至高维系统。
- **离线策略**：一旦训练完成，投影操作可在后训练阶段一次完成，实际部署时无需在线求解优化问题，速度快。
- **通用性**：投影算子可应用于非参数控制方法，拓宽了适用范围。
- **清晰的数学框架**：理论完整地证明了稳定与安全控制器空间的交集非空，并给出了构造性证明。

## 8. 不足与局限

- **有界状态空间假设**：指数稳定性投影要求状态空间有界，这依赖安全性约束提供紧集，若安全区域无界则不能直接应用。
- **确定性控制假设**：论文仅考虑确定性控制器 \(u(x)\)，未扩展到随机控制（如反馈增益自适应），因为难以构造随机控制的近似投影算子。
- **完全驱动假设**：实验中假设执行器可直接驱动所有状态（全驱动），而许多实际系统是欠驱动的（如仅能控制一部分状态），该情况未探讨。
- **扩散项限制**：Hutchinson迹估计仅适用于 \(r>1\) 且 \(g\) 与 \(x\) 无关的情况，对于更一般的扩散项（如状态依赖的随机矩阵）可能需要更复杂的加速手段。
- **实验范围局限**：虽包含高维同步任务（100维），但未在更高维（如>500维）系统上测试计算可扩展性。对比方法中GP-MPC、BALSA仅在2个基准上测试，学习型方法对比只在一个系统（自行车）上进行。
- **安全指标风险**：尽管理论保证“几乎必然”安全，但实际数值仿真中因离散化误差和随机抽样，仍可能存在极小概率边界违反。
- **缺少在线适应**：框架本质是离线学习+后处理投影，未考虑系统动态变化或分布偏移时的在线调整。

（完）
