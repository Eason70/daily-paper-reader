---
title: Neural Event-Triggered Control with Optimal Scheduling
title_zh: 具有最优调度的神经事件触发控制
authors: "Luan Yang, Jingdong Zhang, Qunxi Zhu, Wei Lin"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=djVlAgkRFO"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 具有稳定证书的神经事件触发控制器
tldr: 本文针对学习使能控制器在实际部署中通信资源消耗大的问题，提出神经事件触发控制框架，通过路径积分和蒙特卡洛算法实现最小化触发次数的调度，在保证稳定性的前提下显著降低通信负担，为资源受限的安全控制场景提供了有效方法。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-djvlagkrfo/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 844, \"height\": 313, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-djvlagkrfo/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1090, \"height\": 529, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-djvlagkrfo/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 709, \"height\": 377, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-djvlagkrfo/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 791, \"height\": 295, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-djvlagkrfo/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1767, \"height\": 403, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-djvlagkrfo/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 852, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-djvlagkrfo/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 854, \"height\": 246, \"label\": \"Table\"}]"
motivation: 现有神经控制器持续更新消耗过多通信资源，亟需高效事件触发机制。
method: 提出Neural ETC框架，包含路径积分和蒙特卡洛两种实用算法来自动学习最优触发调度。
result: 在多个控制基准上验证了该方法能实现极低触发次数同时保持稳定性能。
conclusion: 事件触发控制与稳定性证书结合可有效节约通信资源，适用于实际数字平台。
---

## Abstract
Learning-enabled controllers with stability certificate functions have demonstrated impressive empirical performance in addressing control problems in recent years. Nevertheless, directly deploying the neural controllers onto actual digital platforms requires impractically excessive communication resources due to a continuously updating demand from the closed-loop feedback controller. We introduce a framework aimed at learning the event-triggered controller (ETC) with optimal scheduling, i.e., minimal triggering times, to address this challenge in resource-constrained scenarios. Our proposed framework, denoted by Neural ETC, includes two practical algorithms: the path integral algorithm based on directly simulating the event-triggered dynamics, and the Monte Carlo algorithm derived from new theoretical results regarding lower bound of inter-event time. Furthermore, we propose a projection operation with an analytical expression that ensures theoretical stability and schedule optimality for Neural ETC. Compared to the conventional neural controllers, our empirical results show that the Neural ETC significantly reduces the required communication resources while enhancing the control performance in constrained communication resources scenarios.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：近年来，基于稳定性证书函数（如 Lyapunov 函数）的学习型神经控制器在控制复杂非线性系统中表现出色。然而，这类控制器在实际部署时需要持续更新控制信号，导致通信资源消耗过高，尤其在资源受限的无线嵌入式控制系统中难以实现。
- **核心问题**：如何设计一种事件触发控制器，使其在保证系统指数稳定性的前提下，实现最优调度（即最小的触发次数和最大的事件间隔时间），从而大幅降低通信负担。
- **整体含义**：本文提出名为 **Neural ETC** 的框架，通过学习一个事件触发控制器，将控制更新限制在极少数的触发时刻，在保持稳定性的同时显著节约通信资源。这是首次在连续动力学系统中研究事件触发控制的调度优化问题。

## 2. 方法论：核心思想、关键技术细节与公式/算法流程

### 核心思想
- 将事件触发控制建模为闭环误差增广系统，设计具有指数稳定保证的事件函数，并通过神经网络参数化控制器和 Lyapunov 函数，优化触发间隔。

### 关键技术细节
- **事件函数设计**：基于 Lyapunov 函数的导数条件，构造事件函数  
  `h = ∇V·(f(x,u(x+e)) - f(x,u(x))) - σV(x)`（σ∈(0,1)），保证在两次触发之间满足指数衰减率 `1-σ`。
- **两种训练算法**：
  1. **路径积分法 (Neural ETC-PI)**：利用神经事件 ODE 求解器 (`ODESolveEvent`) 和根求解器计算触发时间 `tk`，并通过隐函数定理求导，将触发间隔目标纳入损失函数 `L = L_stab + λ1 L_lip + λ2 L_event`。
  2. **蒙特卡洛法 (Neural ETC-MC)**：理论上界定了最小事件间隔的下界（定理3.2, 3.3），从而避免直接求解 ODE 的昂贵反向传播，仅通过正则化控制器和类K函数逆的 Lipschitz 常数来最大化间隔。损失函数为 `L = ˜L_stab + λ1 L_lip + λ2 L_α⁻¹`。
- **投影操作**：提出投影算子 `π(u, U(V)) = u - max(0, L_fu V - V)/‖∇V‖² · ∇V`，确保任意学习到的控制器经过投影后满足 Lyapunov 稳定性条件，且 Lipschitz 连续（有界域上），从而提供理论稳定性保证（定理4.1）和最优性必要条件（定理4.2）。
- **参数化**：Lyapunov 函数用输入凸神经网络（ICNN）加二次项构造；控制器用谱归一化前馈网络构造；类K函数通过单调神经网络积分构造。

### 算法流程（文字描述）
- **Neural ETC-PI**：① 预热训练（仅包含稳定性损失和 Lipschitz 正则）；② 主训练：从数据集中采样初始状态，通过 ODESolveEvent 求解第一次触发时间，计算包含触发间隔的损失，更新网络参数。
- **Neural ETC-MC**：直接从分布中采样状态和误差样本，计算稳定性损失、控制器 Lipschitz 正则、类K函数逆正则，更新参数，无需 ODE 求解。

## 3. 实验设计

### 使用的基准系统（场景）
1. **基因调控网络 (GRN)** – 2维，用于控制蛋白表达水平，从低表达吸引子切换到高表达吸引子。
2. **Lorenz 系统** – 3维混沌系统，镇定到零解。
3. **Michaelis–Menten 子细胞模型 (Cell)** – 100维高维系统，从凋亡状态调控到活跃状态。

### Benchmark 方法
- **经典控制**：LQR（线性二次型调节器）、BALSA（基于贝叶斯学习的自适应QP控制）
- **基于证书的神经控制**：NLC（神经 Lyapunov 控制）、Quad-NLC（二次型 Lyapunov 改进）、PGDNLC（最新SOTA）、ETS（事件触发镇定）
- **强化学习类 ETC**：IRL ETC（积分强化学习）、Critic-Actor ETC
- **本文方法**：Neural ETC-PI（路径积分法）、Neural ETC-MC（蒙特卡洛法）

### 评估指标
- 触发次数（越少越好）
- 最小事件间隔时间（越大越好）
- 有限触发（≤10次）下的均方误差 (MSE)（越小越好）

### 对比公平性
- 所有学习模型的总参数数保持一致；事件函数类型按各自方法定义；超参数经调优。

## 4. 资源与算力

- 论文中明确指出：所有实验在**单台 i7-10870 CPU（16GB 内存）**上完成。
- **未明确说明 GPU 型号或数量**，也未给出具体训练时长（仅有相对比较，如 Neural ETC-PI 在 GRN 上训练时间 1230 秒，在 Lorenz 上 503 秒，而 Neural ETC-MC 对应 32 秒和 29 秒）。高维 Cell 任务也未给出训练时间数值。

## 5. 实验数量与充分性

- **主要对比实验**：在 3 个不同维度（2/3/100）和不同类型的系统上，对比了 8 种方法 + 本文 2 种变体，每种方法重复 5 次取平均和标准差。覆盖了低维到高维、线性到混沌、单输入到全驱动场景。
- **消融实验**：
  - σ 参数（指数衰减率）的影响（图3a/b），测试了两个值 0.1 和 0.9。
  - 事件损失权重 λ2 的影响（表3），测试了 0.005/0.05/0.5（PI）和 0.01/0.1/1.0（MC）。
- **关键因素分析**（图4）：在训练过程中观察 V 的凸性（Hessian 迹）、控制器梯度范数 ‖∇u‖ 与触发次数的演化关系。
- **充分性评价**：实验覆盖了不同维度、不同控制难度、多种对比方法，且做了参数敏感性分析和机制解释实验，整体较为充分客观。但 σ 和 λ2 的取值范围不够密集（仅少数离散值），可能未完全揭示最优配置。

## 6. 主要结论与发现

- **Neural ETC 显著优于现有方法**：在所有三个基准系统上，Neural ETC-PI 和 Neural ETC-MC 均取得了**最少触发次数**和**最大最小事件间隔**，同时有限触发下的 MSE 远低于对比方法。
- **通信资源大幅节省**：例如在 Lorenz 系统中，Neural ETC-PI 仅触发约 20 次，而 NLC 需要 1602 次；在 Cell 系统中，Neural ETC-MC 仅触发 2 次，而其他方法动辄数十到数百次。
- **稳定性和最优性有理论保证**：投影操作确保了经投影后的控制器满足 Lyapunov 条件，并给出最小事件间隔的正下界；正则化 Lipschitz 常数是实现最优调度的关键。
- **两种算法互补**：Neural ETC-PI 轨迹方差小、鲁棒性强，但训练慢（需 ODE 求解）；Neural ETC-MC 训练速度快，适合高维系统，但轨迹方差稍大。
- **关键因素**：控制器梯度范数 ‖∇u‖ 与触发次数呈强负相关，是优化调度的主要驱动因素，而 Lyapunov 函数的凸性影响较小。

## 7. 优点

- **理论创新**：首次给出事件触发控制下最小事件间隔的下界估计（定理3.2, 3.3），并设计投影操作保证稳定性（定理4.1）及最优调度的必要条件（定理4.2）。
- **方法实用**：同时提出两种训练算法，可根据任务需求（精度优先 vs. 效率优先）灵活选择；蒙特卡洛法避免了 ODE 反向传播的高计算开销，适合高维系统。
- **实验设计全面**：涵盖 2D、3D、100D 三种维度的代表性应用，与多种基线（包括经典控制、神经证书控制、RL 控制等）对比，且验证了消融和关键因素分析。
- **开源代码**：提供了可复现实验的 GitHub 仓库。

## 8. 不足与局限

- **ODEs 求解器依赖**：路径积分法依赖固定步长 ODE 求解器，对刚性方程效果可能不佳，自适应求解器可改善但计算资源要求更高。
- **未扩展到随机系统**：当前框架只适用于确定性 ODE，对于随机微分方程（SDEs），因为触发时间成为停时、具有随机性，无法直接套用 ODESolveEvent 方法。
- **高维任务训练效率**：在 100 维 Cell 任务中，Neural ETC-PI 的训练计算成本极高（只用了 10 次迭代和 batch size 5），难以扩展到更大规模系统；蒙特卡洛法虽然快，但轨迹方差大，可能影响稳定性。
- **超参数调优有限**：σ 和 λ2 仅测试了少数离散值，没有系统扫描，最佳配置可能不唯一；σ=0.8 的建议来自 Lorenz 系统，未必迁移到其他系统。
- **实验数量**：虽然覆盖 3 个系统，但缺少对更多真实机器人或工程系统的验证，结论的通用性有限；消融实验的粒度较粗（σ 只测了两个极端值）。
- **偏差风险**：本文方法在低触发次数下 MSE 极低，但在某些场景下（如 LQR 线性化系统）LQR 也能有低触发，但作者未详细讨论为何 LQR 在 GRN 上触发高达 1816 次（可能是由于非线性强）；对比方法的实现细节（事件函数、超参数）可能存在偏差，尽管尽量保持公平。

（完）
