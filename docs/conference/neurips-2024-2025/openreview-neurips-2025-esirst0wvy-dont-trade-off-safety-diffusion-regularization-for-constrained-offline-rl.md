---
title: "Don’t Trade Off Safety: Diffusion Regularization for Constrained Offline RL"
title_zh: 不要牺牲安全性：扩散正则化用于约束离线强化学习
authors: "Junyu Guo, Zhi Zheng, Donghao Ying, Ming Jin, Shangding Gu, Costas Spanos, Javad Lavaei"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=eSIRst0WVy"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 使用扩散正则化满足约束的离线安全强化学习
tldr: 本文提出扩散正则化约束离线强化学习（DRCORL），利用扩散模型提取行为策略，并通过梯度操作平衡奖励目标与约束满足。该方法在固定数据集上无需探索即可学习安全策略，实验表明其在多个安全任务中优于现有方法。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 600, \"height\": 569, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1433, \"height\": 569, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 862, \"height\": 736, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1261, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1266, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1404, \"height\": 374, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 619, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 619, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 620, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 617, \"height\": 413, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 616, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 614, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 617, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 616, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 619, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 617, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 616, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 616, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 616, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 617, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 617, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 615, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 616, \"height\": 418, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 614, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 615, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 615, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 616, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 616, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-029.webp\", \"caption\": \"\", \"page\": 0, \"index\": 29, \"width\": 616, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-esirst0wvy/fig-030.webp\", \"caption\": \"\", \"page\": 0, \"index\": 30, \"width\": 615, \"height\": 407, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-esirst0wvy/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1452, \"height\": 589, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-esirst0wvy/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1459, \"height\": 714, \"label\": \"Table\"}]"
motivation: 离线强化学习中需要在不安全探索的情况下学习安全策略。
method: 使用扩散模型拟合行为策略，结合梯度操作调整策略以符合安全约束。
result: 在离线安全控制基准上取得了高性能与约束满足的平衡。
conclusion: DRCORL为离线安全强化学习提供了一种有效方案。
---

## Abstract
Constrained reinforcement learning (RL) seeks high-performance policies under safety constraints. We focus on an offline setting where the agent learns from a fixed dataset—a common requirement in realistic tasks to prevent unsafe exploration. To address this, we propose Diffusion-Regularized Constrained Offline Reinforcement Learning (DRCORL), which first uses a diffusion model to capture the behavioral policy from offline data and then extracts a simplified policy to enable efficient inference. We further apply gradient manipulation for safety adaptation, balancing the reward objective and constraint satisfaction. This approach leverages high-quality offline data while incorporating safety requirements. Empirical results show that DRCORL achieves reliable safety performance, fast inference, and strong reward outcomes across robot learning tasks. Compared to existing safe offline RL methods, it consistently meets cost limits and performs well with the same hyperparameters, indicating practical applicability in real-world scenarios. We open-source our implementation at https://github.com/JamesJunyuGuo/DRCORL.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：离线强化学习中，智能体只能从固定数据集学习，无法与环境交互，这避免了不安全探索，但带来了两大挑战：**分布偏移**（学习策略偏离数据集分布导致价值高估）和**奖励-安全权衡**（高回报与严格约束冲突）。现有在线安全RL方法不适用离线设置。
- **目标**：在不收集额外数据的前提下，同时最大化累积奖励并满足成本约束（软约束，期望总成本低于阈值）。
- **总体含义**：提出**DRCORL（扩散正则化约束离线强化学习）**，利用扩散模型拟合行为策略，通过逆KL散度正则化防止策略偏离，并采用梯度操纵动态平衡奖励与安全目标。

## 2. 方法论

### 核心思想
1. **扩散模型学习行为策略**：使用扩散模型（先验分布到高斯噪声的逆向去噪）从离线数据集中学习行为策略 π_b(a|s) 的分布。
2. **简化策略提取**：将学习到的扩散策略蒸馏为一个简单的高斯策略 π_θ(a|s)，利用扩散模型的**得分函数**（score function）计算逆KL散度梯度，实现高效推理（无需多次采样）。
3. **安全适应**：通过**梯度操纵**（gradient manipulation）动态协调奖励最大化与成本约束。引入松弛变量 h⁻, h⁺，根据当前策略成本是否接近阈值，选择只优化奖励、只优化成本，或在两者间进行梯度投影以缓解冲突。

### 关键技术与公式
- **扩散模型训练**：最小化噪声预测损失：
  \[
  L(\psi)=\mathbb{E}_{t,(s,a)}\left[w(t)\|\epsilon_{\psi}(a_t,t|s)-\epsilon_t\|^2\right]
  \]
- **逆KL正则化梯度**：利用扩散模型得分函数 \(\nabla_a\log \mu_\psi(a|s)\approx -\frac{1}{\sqrt{\bar{\beta}_t}}\epsilon_\psi(a_t,t|s)\) 计算：
  \[
  \nabla_\theta D_{\text{KL}}(\pi_\theta\|\mu_\psi)=-\mathbb{E}_{z}\left[\nabla_a\log\mu_\psi\cdot\nabla_\theta(m_\theta+\Sigma_\theta^{1/2}z)\right]-\frac{1}{2}\nabla_\theta\log\det\Sigma_\theta
  \]
- **梯度操纵**（式12）：根据梯度夹角 ϕ 选择最终梯度 g：
  - 若 ϕ ∈ (0,90°)：取均值 \(g=(g_r+g_c)/2\)
  - 若 ϕ ∈ [90°,180°]：投影到彼此零空间后取均值 \(g=(g_r^++g_c^+)/2\)
- **算法流程**（Algorithm 1）：
  1. 预训练扩散模型及奖励/成本评论家（奖励使用IQL，成本使用悲观TD学习）。
  2. 循环中采样小批量，更新评论家，通过安全适应步骤（Algorithm 2）计算梯度更新策略参数。
- **理论保证**：在表格设定下，给出最优性间隙和约束违反的上界（Theorem 3.1）；成本上界保证（Proposition 3.1）。

## 3. 实验设计

- **数据集/场景**：使用离线安全RL基准 **DSRL**，涵盖**Safety-Gymnasium**（如CarGoal, PointGoal, AntVel等）和**Bullet-Safety-Gym**（如HalfCheetahVel, HopperVel等），共13个任务。
- **评价指标**：归一化累积奖励（↑）和归一化累积成本（≤1视为安全）。
- **对比方法**：BC-Safe、BEARL、BCQ-Lag、CPQ、COptiDICE、CDT、CAPS、CCAC等8种基线（还包括TREBI和FISOR用于推理速度比较）。
- **实验配置**：每个任务5个随机种子，每个种子20个评估回合，结果取平均。

## 4. 资源与算力

- **文中说明**：仅提到使用Cuda设备，批量大小为256/512等（见表2），未明确给出GPU型号、数量或训练时长。
- **大致规模**：每个任务预训练步数约2050（策略提取阶段），预训练扩散模型和评论家需要额外步数，但总体比扩散策略推理成本低。
- **不足**：缺乏对算力消耗的具体量化描述。

## 5. 实验数量与充分性

- **实验数量**：13个任务 × 5种子 = 65个独立训练；含4组消融实验（成本限制、温度参数、松弛变量、推理速度对比）。
- **充分性**：覆盖多种机器人任务（导航、速度控制等），比较了主流离线安全RL方法；消融实验探究关键参数影响；提供了训练曲线。设计较为充分。
- **公平性**：所有方法在相同基准上评估，超参数公开（表2）。但未报告标准差/置信区间（仅平均），可能掩盖方差。

## 6. 主要结论与发现

- DRCORL在**多数任务上同时实现高奖励和安全约束满足**，归一化成本常接近0或远低于1。
- 相比基线，在CarGoal、PointGoal、BallCircle等任务中表现突出；在Walker2dVel等少数任务上BCQ-Lag奖励略高但违反安全。
- **推理速度**：比扩散模型方法（TREBI、FISOR）快10倍以上，接近轻量MLP方法（BCQ、CPQ）。
- **理论分析**给出了成本上界和收敛性保证，说明算法可保持与行为策略相近的安全性能。

## 7. 优点

- **方法创新**：将扩散模型作为行为先验并提取简单策略，兼顾表达能力和推理效率；梯度操纵机制无需手动调整Lagrange乘子，自适应平衡奖励与安全。
- **理论贡献**：提供了成本上界（Proposition 3.1）和表格设定下最优性/违反界（Theorem 3.1），增加了方法的可信度。
- **实验全面**：覆盖多类型任务和多组消融，与其他离线安全RL方法对比充分。
- **实用性强**：开源代码，且统一超参数在不同任务上表现良好，便于实际部署。

## 8. 不足与局限

- **计算开销**：预训练阶段（扩散模型+评论家）仍需要一定算力，虽推理快但训练成本未与基线详细对比。
- **零违规保证困难**：在离线设置下，由于数据集质量和覆盖有限，无法保证严格零成本违规。
- **数据集依赖**：方法有效性依赖于离线数据的表征质量；稀疏或偏差严重的数据集可能导致扩散模型欠表示安全模式，影响最终性能。
- **实验报告细节**：未报告每次实验的标准差/置信区间，削弱了统计显著性表述；算力资源信息缺失。
- **理论限制**：分析中忽略了反向KL项，假设策略始终在行为策略邻域内（Assumption A.1），实际中该假设未必总能满足。
- **软约束设置**：仅考虑软约束（期望成本低于阈值），未实验硬约束（每一步无违规）场景。

（完）
