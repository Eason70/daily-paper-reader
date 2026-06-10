---
title: "ABNet: Adaptive explicit-Barrier Net for Safe and Scalable Robot Learning"
title_zh: ABNet：用于安全可扩展机器人学习的自适应显式屏障网络
authors: "Wei Xiao, Tsun-Hsuan Wang, Chuang Gan, Daniela Rus"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=ymlwqfxuUc"
tags: ["query:safe-rl-cbf"]
score: 8.0
evidence: 显式屏障网络用于安全控制
tldr: 针对机器人安全学习中可扩展性和鲁棒性问题，提出自适应显式屏障网络（ABNet）。该网络在模型中显式包含屏障函数，以闭式形式保证安全性；通过多头架构学习不同特征的安全策略，避免直接构建大型模型。在噪声输入下仍保持稳定，实验证明其可扩展至复杂任务且训练高效。为安全基础模型提供了新范式。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-ymlwqfxuuc/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1248, \"height\": 426, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ymlwqfxuuc/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 877, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ymlwqfxuuc/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 629, \"height\": 976, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ymlwqfxuuc/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 625, \"height\": 955, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ymlwqfxuuc/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 614, \"height\": 892, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ymlwqfxuuc/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 608, \"height\": 988, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ymlwqfxuuc/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1645, \"height\": 582, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ymlwqfxuuc/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 822, \"height\": 269, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ymlwqfxuuc/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 757, \"height\": 575, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ymlwqfxuuc/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 619, \"height\": 264, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ymlwqfxuuc/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1674, \"height\": 593, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ymlwqfxuuc/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1677, \"height\": 818, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ymlwqfxuuc/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1660, \"height\": 597, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ymlwqfxuuc/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 863, \"height\": 799, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ymlwqfxuuc/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1762, \"height\": 597, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ymlwqfxuuc/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1761, \"height\": 589, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ymlwqfxuuc/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1764, \"height\": 571, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ymlwqfxuuc/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1754, \"height\": 564, \"label\": \"Table\"}]"
motivation: 现有安全学习方法不可扩展、低效且对噪声敏感，难以在机器人上部署。
method: 提出ABNet，在模型中以闭式显式屏障函数保证安全，通过多头架构学习不同特征的安全策略。
result: 在多个机器人任务中展示了比基线更好的可扩展性和对噪声的鲁棒性。
conclusion: ABNet为构建安全基础模型提供了高效且可扩展的方法。
---

## Abstract
Safe learning is central to AI-enabled robots where a single failure may lead to catastrophic results. Existing safe learning methods are not scalable, inefficient and hard to train, and tend to generate unstable signals under noisy inputs that are challenging to be deployed for robots. To address these challenges, we propose Adaptive explicit-Barrier Net (ABNet) in which barriers explicitly show up in the closed-form model that guarantees safety. The ABNet has the potential to incrementally scale toward larger safe foundation models.  Each head of ABNet could learn safe control policies from different features and focuses on specific part of the observation. In this way, we do not need to directly construct a large model for complex tasks, which significantly facilitates the training of the model while ensuring its stable output. Most importantly, we can still formally prove the safety guarantees of the ABNet. We demonstrate the efficiency and strength of ABNet in 2D robot obstacle avoidance, safe robot manipulation, and vision-based end-to-end autonomous driving, with results showing much better robustness and guarantees over existing models.

---

## 论文详细总结（自动生成）

# ABNet 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有安全机器人学习方法（如基于可微 QP 的 BarrierNet、可微 MPC 等）存在以下缺陷：
  - **不可扩展（not scalable）**：难以构建大型安全模型；
  - **训练低效且不稳定**：求解批量 QP 耗时且易产生劣化解，恶化模型质量；
  - **对输入噪声敏感**：输出控制信号不稳定，无法在真实机器人上部署。
- **整体含义**：需要一种能够融合多个安全关键模型、同时保持安全保证的方法，以实现安全、可扩展、鲁棒的机器人学习，为构建安全基础模型奠定基础。

## 2. 论文提出的方法论

### 核心思想
- 提出 **Adaptive explicit-Barrier Net (ABNet)**，将屏障函数（Barrier Function）显式地以闭式形式融入模型，保证安全。
- 采用 **多头（multi-head）架构**，每个头可关注不同的观测特征（如左车道边界、右车道边界），学习各自的局部安全控制策略。
- 通过 **线性融合**（带权重可训练）组合各头的安全控制输出，融合后仍能证明全局安全。

### 关键技术细节
- **显式屏障（Explicit-Barrier）**：将原始可微 CBF 问题转化为仅含两个约束（通过取最危险的两个安全规范或对数凸组合）的 QP，从而推导出闭式解：
  - 控制律：`u_k = -λ1 H⁻¹ L_g ψ_I - λ2 H⁻¹ L_g ψ_II - H⁻¹ F`
  - 其中 λ1, λ2 是门控函数（由安全约束激活），H, F 来自上一网络层。
  - 该闭式解避免了求解批量 QP，显著提升训练效率和稳定性。
- **多头显式屏障**：每个头独立计算一个安全控制 `u_k`。
- **交叉连接（Cross connection）**：所有头共享低阶 HOCBF 参数（`θ_p`），确保安全构造的一致性，并实现信息共享。
- **融合机制**：`u = Σ w_k u_k`，权重 `w_k ≥ 0` 且和为 1，可训练或通过测试损失确定。
- **安全证明**：定理 3.1 证明 ABNet 输出保证安全性（若初始安全）；定理 3.2 证明多个 ABNet 再次融合仍安全。
- **自然噪声滤波器**：权重均在 0-1 之间，多头平均可平滑输出，增强鲁棒性。

### 算法流程（文字说明）
1. 为每个头构造显式屏障（公式 4）。
2. 通过共享参数 `θ_p` 建立交叉连接。
3. 融合所有头的输出（公式 5）。
4. 可选：增量训练（先单独训练每个头，再确定权重）或一次性端到端训练。

## 3. 实验设计

### 使用数据集 / 场景
1. **2D 机器人避障**：自行车模型，避障约束（圆形障碍物）。
2. **安全机器人操作**：两连杆平面机械臂，末端执行器避障。
3. **视觉端到端自动驾驶**：使用 VISTA 模拟器（基于真实驾驶数据），数据集包含约 40 万图像-控制对，障碍物为静态/停泊车辆。

### Benchmark
- **MPC**：用于生成标签的模型预测控制器（非线性 MPC）。
- **对比方法**：
  - 无安全保障：E2E（端到端）、E2Es-MCD（Monte Carlo Dropout 集成）、E2Es-DR（Deep Resembles 集成）。
  - 有安全保障：DFB（深度前向后向随机微分方程）、BNet（BarrierNet，基于可微 QP）、BNet-UP（BarrierNet 带不确定性传播）。
  - 自己的 ABNet 变体：ABNET-10-SC（增量训练 10 头）、ABNET-10（一次性训练 10 头）、ABNET-100（100 头）、ABNET-ATT（注意力图像多头）、ABNET-SC（可扩展融合）。

### 评估指标
- 安全性（SAFETY）：所有运行中安全约束的最小值（≥0 表示安全）。
- 保守性（CONSER.）：均值±标准差。
- 控制不确定性（u1/u2 UNCERTAINTY）：输出标准差。
- MSE（均方误差）、障碍物碰撞率（CRASH）、通过率（PASS）。

## 4. 资源与算力

- **训练硬件**：RTX-3090 GPU。
- **训练时长**：
  - 2D 避障：约 1 小时（20 epoch）。
  - 机器人操作：约 2 小时（10 epoch）。
  - 视觉自动驾驶：约 15 小时（5 epoch）。
- **未明确说明**：GPU 数量未提及（推测单卡）；模型参数量未给出。

## 5. 实验数量与充分性

- **实验数量**：包含三大类任务，每类任务对比 6-8 种方法，并报告 100 次闭环测试的统计结果。
- **消融实验**：自动驾驶任务中对 ABNet 进行了注意力输入变体（ABNET-ATT）和可扩展训练（ABNET-SC）的消融；还进行了高噪声（50% 图像噪声）的鲁棒性消融。
- **充分性判断**：
  - 实验覆盖不同复杂度任务（低维状态输入、高维图像输入）。
  - 使用公开数据集（VISTA）和标准协议，可复现。
  - 方法对比充分（baseline 包括无安全方法、安全方法、集成方法）。
  - 不足之处：未在真实机器人上验证；未涉及多机器人或动态障碍物场景。

## 6. 论文的主要结论与发现

- ABNet 的计算和训练效率显著优于基于可微 QP 的 BarrierNet，且训练更稳定。
- 多头融合可提升性能（降低 MSE、减小控制不确定性），且不确定性随头数增加而降低。
- 在保证理论安全的前提下，ABNet 在噪声输入下仍能保持安全（自动驾驶 0% 碰撞率），而其他安全方法（BNet、DFB）会出现碰撞或过度保守。
- 显式屏障的闭式解使模型更易训练、更可解释，且支持增量式构建安全基础模型。

## 7. 优点

- **高效率**：避免求解批量 QP，训练速度与普通 NN 相近。
- **可扩展**：可通过增加头部数量增量式训练，易于集成新技能。
- **强鲁棒性**：多头平均自然滤除噪声，输出平滑。
- **保留安全证明**：融合后仍可形式化证明安全。
- **直观可解释**：屏障函数显式出现在解中，比隐式 BarrierNet 更透明。

## 8. 不足与局限

- **安全约束同质**：所有头必须使用相同的安全约束，无法融合不同约束下的模型（作者列为未来工作）。
- **依赖安全规范**：需要预定义安全约束（如障碍物位置），可能不适用于完全未知环境（可结合学习安全规范的方法）。
- **输出空间融合**：仅在输出层融合，未在参数空间融合，可能限制表达力。
- **实验局限性**：
  - 未在真实机器人平台上部署，仅仿真。
  - 未涉及接触操作（如抓取）或动态障碍物场景。
  - 高噪声消融仅做了图像噪声，未测试控制噪声或传感器噪声组合。
- **未报告不确定性量化**：虽然降低控制不确定性，但未与贝叶斯方法（如 MCD）在不确定性校准上直接比较。

（完）
