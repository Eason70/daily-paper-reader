---
title: Safe and Stable Control via Lyapunov-Guided Diffusion Models
title_zh: 基于李雅普诺夫引导扩散模型的安全稳定控制
authors: "Xiaoyuan Cheng, Xiaohang Tang, Yiming Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=aY97JGello"
tags: ["query:safe-rl-cbf"]
score: 9.0
evidence: 基于李雅普诺夫引导扩散模型的安全控制，等价于控制屏障函数方法
tldr: 现有基于扩散模型的控制策略往往忽略安全与稳定性。本文提出S^2Diff框架，从李雅普诺夫角度利用扩散模型学习证书函数以同时保证安全与稳定。该方法避免了复杂梯度求解器（如二次规划）和控制仿射结构需求，生成全局有效控制策略。实验表明其在多个控制任务上优于现有安全控制方法。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-ay97jgello/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 729, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ay97jgello/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1451, \"height\": 308, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ay97jgello/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1432, \"height\": 267, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ay97jgello/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1415, \"height\": 284, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ay97jgello/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 617, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ay97jgello/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 653, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ay97jgello/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1451, \"height\": 508, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ay97jgello/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1207, \"height\": 635, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ay97jgello/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1205, \"height\": 634, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ay97jgello/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1426, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ay97jgello/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 982, \"height\": 553, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ay97jgello/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1349, \"height\": 462, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ay97jgello/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1428, \"height\": 841, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-ay97jgello/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1327, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ay97jgello/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1329, \"height\": 1282, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ay97jgello/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1134, \"height\": 138, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ay97jgello/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1433, \"height\": 150, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ay97jgello/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1455, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ay97jgello/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 874, \"height\": 1093, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ay97jgello/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1037, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ay97jgello/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1445, \"height\": 521, \"label\": \"Table\"}]"
motivation: 扩散模型在控制中多关注奖励最大化，忽略安全与稳定性。
method: 提出S^2Diff框架，利用李雅普诺夫证书函数引导扩散模型生成安全稳定策略。
result: 无需梯度求解器，实现全局有效安全控制，性能优于现有方法。
conclusion: 为基于学习的安全控制提供了无需显式CBF的替代方案，方法通用性强。
---

## Abstract
Diffusion models have made significant strides in recent years, exhibiting strong generalization capabilities in planning and control tasks. However, most diffusion-based policies remain focused on reward maximization or cost minimization, often overlooking critical aspects of safety and stability. In this work, we propose Safe and Stable Diffusion ($S^2$Diff), a model-based framework that explores how diffusion models can ensure safety and stability from a Lyapunov perspective. We demonstrate that $S^2$Diff eliminates the reliance on both complex gradient-based solvers (e.g., quadratic programming, non-convex solvers) and control-affine structures, leading to globally valid control policies driven by the learned certificate functions. Additionally, we uncover intrinsic connections between diffusion sampling and almost Lyapunov theory, enabling the use of trajectory-level control policies to learn better certificate functions for safety and stability guarantees. To validate our approach, we conduct experiments on a wide variety of dynamical control systems, where $S^2$Diff consistently outperforms both certificate-based controllers and model-based diffusion baselines in terms of safety, stability, and overall control performance.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：扩散模型在规划和控制任务中表现出强大的泛化能力，但现有扩散策略大多聚焦于奖励最大化或成本最小化，**严重忽视了安全性和稳定性**这两个实际控制系统（如机器人、航空航天）中的关键要求。
- **问题背景**：
  - 模型预测控制（MPC）虽能处理约束，但计算复杂且易陷入局部最优；基于控制李雅普诺夫函数（CLF）/控制屏障函数（CBF）的二次规划（QP）方法需要**控制仿射结构**，引入松弛变量会导致全局不一致，且联合学习证书函数与策略时可能出现不可行QP。
  - 现有模型扩散规划（MBD）无法保证安全与稳定；手设计CBF难度大。
- **核心目标**：探索扩散模型如何从李雅普诺夫角度同时保证安全与稳定，摆脱对控制仿射结构和复杂梯度求解器的依赖。

### 2. 论文提出的方法论

- **核心思想**：提出 **S²Diff（Safe and Stable Diffusion）** 框架，将扩散采样与 Almost Lyapunov 理论相结合，迭代地学习证书函数（CLBF）并生成安全稳定的轨迹级策略。
- **关键技术细节**：
  - **概率公式化**：将控制问题建模为对目标分布 \( p(U) \propto p_{\text{safe}} p_{\text{stable}} p_{\text{cost}} \) 的采样，其中：
    - \( p_{\text{safe}} \)：指示函数，要求 \( V(x_t) \le c \)
    - \( p_{\text{stable}} \)：采用**软约束**（公式8），用指数惩罚 \( \exp\left(-\frac{1}{\gamma_2}\sum_t [L_f V(x_t) + \lambda V(x_t)]_+^2 \right) \) 替代严格指示函数，避免松弛变量。
    - \( p_{\text{cost}} \)：指数形式的累积成本或与名义策略的 \( \ell_2 \) 距离。
  - **扩散采样**：使用蒙特卡罗得分上升（公式10）进行逆向扩散，无需训练得分网络，仅利用已知动力学模型。
  - **CLBF 更新**：利用采样轨迹，通过损失函数（公式11）联合最小化多个约束项，包括平衡点、正性、安全子/超集、连续与离散时间李导数条件，并引入缓冲项 \( \epsilon \) 容忍小违规。
  - **迭代交替**：每轮先由当前 CLBF 引导扩散采样生成轨迹，再用该轨迹更新 CLBF。
- **理论贡献**：定理3.1 建立了**Almost Lyapunov 几乎必然安全稳定保证**——即使局部存在李导数违规区域（体积 \( < \epsilon \)），整体仍保持指数衰减，提供 \( O(\epsilon^{1/n}) \) 的附加缓冲项。

### 3. 实验设计

- **场景与任务**：涵盖 8 个动力学系统：
  - **稳定性任务**：倒立摆（n=2）、汽车运动学跟踪（n=5）、汽车侧滑跟踪（n=7）
  - **安全+稳定任务**：Segway（n=4）、神经着陆器（n=6）、2D四旋翼（n=6）、3D四旋翼（n=9）、**F-16（n=16，非控制仿射）**
- **基准方法**：
  - **rCLBF-QP**：基于二次型 CLBF 的 QP 方法 [Dawson et al., 2022]
  - **MPC**：鲁棒 MPC [Löfberg, 2012]
  - **MBD**：模型扩散规划 [Pan et al., 2024]
- **评估指标**：安全率（20个初始状态的平均百分比）、稳定性（终端状态与平衡点距离）、推理效率（ms）。
- **结果**（表2）：S²Diff 平均安全率 98.75%，终端误差 0.226，推理时间 45.64ms，**在所有任务上均优于或持平最佳基线**（rCLBF-QP 安全率 78.75%，误差 0.384；MPC 66.25%，0.501；MBD 73.75%，0.954）。在非控制仿真的 F-16 上，S²Diff 是唯一能同时保证安全与稳定的方法。

### 4. 资源与算力

- 文中**未明确说明** GPU 型号、数量或训练总时长。
- 附录 F 提及：所有推理时间在 **Intel i9-13900 CPU + 单块 RTX 4090 GPU** 上评估。
- 训练细节未公开量化，但可推测单 GPU 能在合理时间内完成（因为任务规模不大）。

### 5. 实验数量与充分性

- **数量**：在 **8 个不同系统**上进行了完整对比实验，每个系统报告 20 个初始状态下的均值和标准差。
- **消融实验**（附录 F.1）：
  - 稳定性温度 \( \gamma_2 \)（5 个值）
  - 损失函数中连续/离散李导数权重 \( \alpha_1, \alpha_2 \)（6 种组合）
  - 轨迹长度（5 种长度）
- **附加分析**：CLBF 等高线图、违反率表（表3，4个任务）、轨迹可视化（图4、9-12）。
- **充分性评价**：实验覆盖多种复杂度（低维到16维非仿射）、多种约束类型（凸/非凸），对比方法均为领域内代表性算法，结果有统计误差，消融全面。但**缺乏真实硬件实验**，且未与其他如 SafeDiffuser 等最近安全扩散方法比较（可能在时间上不可用）。

### 6. 论文的主要结论与发现

1. **扩散采样可有效学习证书函数**：相比 QP 方法，S²Diff 学到的 CLBF 具有更大的收缩区域（倒立摆等高线图），且能直接处理非凸、非仿射系统（F-16）。
2. **CLBF 引导的扩散策略优于单纯扩散或 QP 策略**：在安全率、稳定性和全局一致性上显著提升，尤其是在起始状态远离目标时。
3. **Almost Lyapunov 理论在实验中得以验证**：违反李导数条件的频率很低（< 2.4%），CLBF 值几乎单调下降，符合定理3.1的保证。
4. **方法的通用性**：无需控制仿射假设、无需松弛变量，适用于一般可微动力学系统。

### 7. 优点

- **创新性融合**：首次将扩散采样与 Almost Lyapunov 理论结合，实现端到端的安全稳定控制。
- **理论扎实**：提供了违反区域体积可控下的几乎必然收敛保证，并给出样本复杂度分析（定理 C.4）。
- **实用性强**：摆脱了对控制仿射结构和 QP 求解器的依赖；软约束设计避免了硬指示函数的高拒绝率。
- **实验全面**：覆盖低维到高维、仿射/非仿射系统，消融深入，对比基线均为当前最佳方法。
- **代码开源**：论文附带代码和实验配置，可复现。

### 8. 不足与局限

- **推理速度**：虽然优于 MPC，但比纯 QP 方法慢（45.64ms vs 10ms），在高实时性场景中可能需要策略蒸馏。
- **模型依赖性**：S²Diff 基于已知动力学模型（model-based），当模型不准确或未知时需额外学习。
- **计算开销**：训练阶段需要多次扩散采样并更新 CLBF，整体训练时间可能较长（文中未披露）。
- **违反区域假设**：理论要求违规区域体积足够小，实际中若初始状态集中在大违规区域，性能可能下降。
- **基准覆盖**：未与近期其它安全扩散方法（如 SafeDiffuser）对比，可能影响全面性。
- **应用限制**：CLBF 的网络参数化可能对极端复杂约束（如高维非凸障碍）仍面临收敛困难。

（完）
