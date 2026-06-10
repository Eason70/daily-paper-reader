---
title: Constrained Diffusers for Safe Planning and Control
title_zh: 约束扩散模型用于安全规划与控制
authors: "Jichen Zhang, Liqun Zhao, Antonis Papachristodoulou, Jack Umenberger"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=tahkGZjjWA"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 通过约束扩散模型实现安全规划与控制
tldr: 本文针对扩散模型在规划与控制中的安全性挑战，提出约束扩散模型框架，无需重新训练即可将分布级约束集成到预训练扩散模型中。通过约束朗之万采样方法，联合优化轨迹并满足约束。实验表明该方法在多个安全控制任务上有效，为安全规划提供了新的扩散模型范式。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-tahkgzjjwa/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1458, \"height\": 388, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tahkgzjjwa/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1438, \"height\": 445, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tahkgzjjwa/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1405, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tahkgzjjwa/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 450, \"height\": 362, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tahkgzjjwa/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1371, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tahkgzjjwa/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1371, \"height\": 291, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tahkgzjjwa/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1370, \"height\": 291, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tahkgzjjwa/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1370, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tahkgzjjwa/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1369, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tahkgzjjwa/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1370, \"height\": 291, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-tahkgzjjwa/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1269, \"height\": 593, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tahkgzjjwa/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1444, \"height\": 479, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tahkgzjjwa/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1442, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tahkgzjjwa/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1469, \"height\": 1250, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tahkgzjjwa/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1336, \"height\": 300, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tahkgzjjwa/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1123, \"height\": 532, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tahkgzjjwa/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1403, \"height\": 899, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tahkgzjjwa/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1368, \"height\": 611, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tahkgzjjwa/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1055, \"height\": 649, \"label\": \"Table\"}]"
motivation: 扩散模型在规划控制中表现优异，但确保安全性仍是一个关键挑战。
method: 提出约束扩散模型，使用投影法、原始-对偶法和增广拉格朗日法等迭代算法实现约束朗之万采样。
result: 在安全规划与控制任务上验证了约束满足能力。
conclusion: 约束扩散模型为安全控制提供了有效的框架。
---

## Abstract
Diffusion models have shown remarkable potential in planning and control tasks due to their ability to represent multimodal distributions over actions and trajectories. However, ensuring safety under constraints remains a critical challenge for diffusion models. This paper proposes Constrained Diffusers, an extended framework for planning and control that incorporates distribution-level constraints into pre-trained diffusion models without retraining or architectural modifications. Inspired by constrained optimization, we apply a constrained Langevin sampling method for the reverse diffusion process that jointly optimizes the trajectory and achieves constraint satisfaction through three iterative algorithms: projected method, primal-dual method and augmented Lagrangian method. In addition, we incorporate discrete control barrier functions as constraints for constrained diffusers to guarantee safety in online implementation, following a receding-horizon control that we generate a short-horizon plan and execute only the first action before replanning. Experiments in Maze2D, locomotion, and PyBullet ball running tasks demonstrate that our proposed methods achieve constraint satisfaction with less computation time, and are competitive with existing methods in environments with static and time-varying constraints.

---

## 论文详细总结（自动生成）

# 论文结构化总结

## 1. 核心问题与整体含义（研究动机与背景）
- **核心问题**：扩散模型在规划与控制任务中表现出色，能够建模多模态轨迹分布，但其直接部署于安全关键系统时面临严峻挑战——如何在无需重训练或修改架构的前提下，将约束（尤其是时变的、非凸的约束）有效地集成到扩散采样过程中，同时保证计算效率。
- **研究背景**：现有方法如分类器引导、分类器无关引导在图像生成中有效，但直接用于规划/控制会导致严重违反约束；SafeDiffuser 需在每一步扩散中求解二次规划（QP），计算代价高；Projected Diffusion 可处理样本级约束但无法处理分布级期望约束，且硬投影可能破坏轨迹平滑性。
- **整体含义**：本文提出 **Constrained Diffusers** 框架，将扩散生成重新解释为分布层面的约束优化问题，通过修改逆向扩散采样过程（无需重训练）来满足安全约束，并结合离散控制屏障函数（DCBF）和逆动力学模型（IDM）实现在线安全执行。

## 2. 方法论
### 核心思想
- 将轨迹生成视为**分布约束优化**：在最小化 KL 散度（与原扩散分布）的同时，满足期望约束 \( \mathbb{E}_{x\sim q}[g(x)] \le 0 \)。
- 连接 DDPM 逆向过程与随机梯度朗之万动力学（SGLD），将每一步更新看作梯度下降+噪声，从而自然地融入约束梯度。
- 引入三种约束采样算法，均仅需约束函数的梯度，无需求解 QP。

### 关键技术细节
1. **投影法（Projected Method）**  
   - 在每一步朗之万更新后，将样本投影到约束集 \( \mathcal{C} \) 上：  
     \[
     x_{t-1} = \Pi_{\mathcal{C}}\left( x_t + \frac{\beta_t}{2}\nabla_{x_t}\log p(x_t) + \sqrt{\beta_t}z \right)
     \]
   - 保证每步样本严格可行，但硬投影可能偏离专家分布。

2. **原始-对偶法（Primal-Dual, PD）**  
   - 将原始约束问题转化为 max-min 问题，通过交替更新原始变量（轨迹）和对偶变量（拉格朗日乘子）：
     \[
     x_{t-1} = x_t + \frac{\beta_t}{2}(\nabla\log p(x_t) - \lambda_t^\top \nabla g(x_t)) + \sqrt{\beta_t}z
     \]
     \[
     \lambda_{t-1} = [\lambda_t + \eta_\lambda g(x_t)]_+
     \]
   - 无需 QP，仅需一阶梯度；可处理分布级期望约束。

3. **增广拉格朗日法（Augmented Lagrangian Method, ALM）**  
   - 在拉格朗日函数中加入二次罚项以提升稳定性：
     \[
     x_{t-1} = x_t + \frac{\beta_t}{2}\left[\nabla\log p(x_t) - (\lambda_t + \rho_t \mathbb{E}[g(x_t)])^\top \nabla g(x_t)\right] + \sqrt{\beta_t}z
     \]
     \[
     \lambda_{t-1} = \lambda_t + \rho_t \mathbb{E}[g(x_t)]
     \]
     \[
     \rho_{t-1} = c\cdot\rho_t,\ c>1
     \]
   - 相比 PD，约束满足程度更高。

### 在线安全实现
- **离散控制屏障函数（DCBF）**：将安全性转化为相邻状态间的约束 \( h(x_{\tau+1}) \ge (1-\alpha)h(x_\tau) \)，直接施加于规划轨迹上。
- **逆动力学模型（IDM）**：用专家数据训练神经网络，将状态转移 \( (x_\tau, x_{\tau+1}) \) 映射为动作 \( u_\tau \)，避免动作不可行。
- **滚动时域控制**：每次只规划短时域轨迹，执行第一个动作后根据新观测重新规划，类似 MPC。

## 3. 实验设计
### 数据集/场景
| 场景 | 环境 | 任务描述 |
|------|------|----------|
| 规划 | Maze2D (umaze, large) | 从起点到终点避障，障碍物由线性或二次不等式定义 |
| 运动控制 | MuJoCo Hopper, Swimmer | 限制关节角速度（Hinge 或 Rotor） |
| 时变约束 | PyBullet SafetyBallRunning | 避让运动障碍物（红色球），约束随时间变化 |
| 高维动作 | Adroit Relocate (操纵) | 30维动作空间，限制臂平移和俯仰 |

### Benchmark 对比方法
- **Diffuser**（基线，无约束）
- **Conditional Diffuser**（约束作为条件，需重训练）
- **SafeDiffuser**（每步 QP 求解 DCBF）
- **Projected Diffusion**（[10] 投影法，但仅处理样本硬约束）
- **本文方法**：Projected（扩展版）、Primal-Dual、ALM

### 评估指标
- 规划/实施阶段约束违反次数（总违反量、违反率）
- 累计奖励
- 每步计算时间

## 4. 资源与算力
- **实验硬件**：Intel Core i7-14700 × 28 核，32GB 内存，NVIDIA GeForce RTX 4060，Ubuntu 24.04。
- **训练细节**：所有扩散模型均从头训练，使用 D4RL 或 Minari 数据集；每个环境的具体规划步长、扩散步数、超参数在附录 C 中详列。**论文未明确报告总训练时长或 GPU 小时数**。

## 5. 实验数量与充分性
- **实验组数**：涵盖 4 种场景（规划+3 种控制），每组至少 10 个随机种子重复。
- **消融与敏感性分析**：
  - α 参数对 DCBF 的影响（附录 E）
  - IDM 预测误差敏感性（2%, 10%, 25%）（附录 F）
  - 极端初始条件最坏情况分析（附录 G）
  - 执行步数（1/2/3 步）的影响（附录 H）
- **公平性**：所有对比方法均在相同环境、相同预处理、相同评价指标下进行；使用与 SafeDiffuser/Projected Diffusion 相同的 U-Net 架构和训练流程。结论客观。

## 6. 主要结论与发现
- **约束满足**：PD 和 ALM 方法将规划阶段违反减少 96%~99%，且计算时间仅增加 ~10%，远低于 SafeDiffuser（~100 倍）和 Projected（~10 倍）。
- **在线安全**：结合 DCBF 后，实施阶段违反率大幅降低（Swimmer 上 PD/ALM 达 98% 降幅，PyBullet 上 99%）。
- **时变约束适应性**：Dynamic 障碍物场景下，PD/ALM 获得最高奖励同时违反率仅 1.6%~2.2%，优于投影法。
- **高维扩展性**：Adroit Relocate（30 维动作）中，PD/ALM 维持近零违反，计算时间接近 Diffuser。
- **理论保证**：给出了投影法和原始-对偶法的局部收敛性分析（附录 I、J、K）。

## 7. 优点
- **无需重训练**：直接利用预训练扩散模型，适合迁移部署。
- **计算高效**：仅需一阶梯度更新，避免 QP 求解，适合实时控制。
- **分布级约束**：与投影法等只能处理样本硬约束的方法不同，可处理期望约束。
- **DCBF 集成**：通过状态耦合约束保证系统正向不变性，提高在线安全性。
- **理论分析**：提供收敛性和约束满意度的证明，虽为局部收敛但仍具指导意义。
- **实验充分**：涵盖静态与动态约束、低维与高维动作空间、消融研究、敏感性分析。

## 8. 不足与局限
- **理论假设较强**：需要准确的分数函数估计、Lipschitz 连续、耗散性等条件，实际中可能无法严格满足；收敛保证仅为局部，全局最优性未证明。
- **约束需已知可微**：要求约束函数 \( g(x) \) 显式且可求梯度；对于黑箱或复杂环境约束难以直接应用。
- **缺乏鲁棒性分析**：未考虑环境不确定性（传感器噪声、模型误差）对约束满足的影响。
- **IDM 依赖**：逆动力学模型需要专家数据训练，可迁移性受限；对于欠驱动系统，可能存在状态转移不可行但 IDM 仍输出错误动作的情况。
- **100% 安全性无保证**：尽管违反率极低，但 PD/ALM 仍可能产生轻微违反，不适用于需绝对安全的关键系统。
- **计算资源描述不充分**：未报告完整训练时长，难以评估大规模部署成本。

（完）
