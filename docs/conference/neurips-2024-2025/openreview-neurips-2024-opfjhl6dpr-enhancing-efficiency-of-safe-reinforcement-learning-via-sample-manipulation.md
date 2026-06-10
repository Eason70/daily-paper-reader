---
title: Enhancing Efficiency of Safe Reinforcement Learning via Sample Manipulation
title_zh: 通过样本操作提升安全强化学习效率
authors: "Shangding Gu, Laixi Shi, Yuhao Ding, Alois Knoll, Costas Spanos, Adam Wierman, Ming Jin"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=oPFjhl6DpR"
tags: ["query:safe-rl-cbf"]
score: 4.0
evidence: 通过样本操作提升安全强化学习效率
tldr: 该论文针对安全强化学习样本效率低的问题，提出高效安全策略优化（ESPO）框架，通过检测奖励与安全梯度冲突并动态调整采样模式，在三个模式间切换以平衡回报和约束。理论保证收敛性，实验表明在多个安全RL任务上以更少交互达到同等安全性。该工作属于安全RL方法改进，未涉及控制屏障函数或特定无人平台。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-opfjhl6dpr/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 617, \"height\": 285, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-opfjhl6dpr/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1249, \"height\": 734, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-opfjhl6dpr/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1247, \"height\": 728, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-opfjhl6dpr/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1246, \"height\": 731, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-opfjhl6dpr/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1246, \"height\": 731, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-opfjhl6dpr/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1242, \"height\": 373, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-opfjhl6dpr/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 863, \"height\": 185, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-opfjhl6dpr/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 869, \"height\": 141, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-opfjhl6dpr/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 811, \"height\": 172, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-opfjhl6dpr/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 992, \"height\": 442, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-opfjhl6dpr/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1217, \"height\": 298, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-opfjhl6dpr/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1477, \"height\": 298, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-opfjhl6dpr/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1067, \"height\": 1711, \"label\": \"Table\"}]"
motivation: 安全强化学习需要大量环境交互才能收敛到安全策略，样本效率低下。
method: 提出ESPO，根据奖励梯度与安全梯度的冲突程度，自适应在奖励最大化、成本最小化和平衡模式间切换采样分布。
result: 在安全RL基准任务上，ESPO用更少的样本实现了与最先进方法相当的安全回报。
conclusion: ESPO为安全RL的样本效率提供了有效优化手段，但未与控制屏障函数结合。
---

## Abstract
Safe reinforcement learning (RL) is crucial for deploying RL agents in real-world applications, as it aims to maximize long-term rewards while satisfying safety constraints. However, safe RL often suffers from sample inefficiency, requiring extensive interactions with the environment to learn a safe policy. We propose Efficient Safe Policy Optimization (ESPO), a novel approach that enhances the efficiency of safe RL through sample manipulation. ESPO employs an optimization framework with three modes: maximizing rewards, minimizing costs, and balancing the trade-off between the two. By dynamically adjusting the sampling process based on the observed conflict between reward and safety gradients, ESPO theoretically guarantees convergence, optimization stability, and improved sample complexity bounds. Experiments on the Safety-MuJoCo and Omnisafe benchmarks demonstrate that ESPO significantly outperforms existing primal-based and primal-dual-based baselines in terms of reward maximization and constraint satisfaction. Moreover, ESPO achieves substantial gains in sample efficiency, requiring 25--29\% fewer samples than baselines, and reduces training time by 21--38\%.

---

## 论文详细总结（自动生成）

# 论文总结：Enhancing Efficiency of Safe Reinforcement Learning via Sample Manipulation

## 1. 核心问题与整体含义
- **研究动机**：安全强化学习（Safe RL）旨在最大化长期回报的同时满足安全约束，但其样本效率低下，需要大量环境交互才能学到安全策略。现有方法（如 CRPO、PCRPO、CPO 等）使用固定样本大小，在简单场景中浪费样本，在复杂场景（高不确定性或目标冲突）中探索不足。
- **整体含义**：该论文提出通过动态调整样本大小来提升安全 RL 的样本效率，同时保证收敛性和安全约束，为安全 RL 提供更实用的优化框架。

## 2. 方法论
- **核心思想**：基于奖励梯度（gr）与成本梯度（gc）之间的冲突程度，动态调整每轮迭代使用的样本数量，并在三种优化模式间切换：
  - **安全违规模式**（成本值 > b + h⁺）：只优化成本。
  - **软约束违规模式**（成本值在 [b + h⁻, b + h⁺] 内）：根据梯度夹角 θr,c 决定更新策略：
    - 梯度冲突（θr,c > 90°）：增加样本量，采用梯度投影法平衡回报与成本。
    - 梯度一致（θr,c ≤ 90°）：减少样本量，直接加权求和更新。
  - **无违规模式**（成本值 < b + h⁻）：只优化回报，减少样本量。
- **关键技术细节**：
  - 样本量调整公式：  
    - 当 θr,c > 90°：\( X_{t+1} = X + X \zeta^+_t \)（增大样本）  
    - 当 θr,c ≤ 90°：\( X_{t+1} = X + X \zeta^-_t \)（减小样本）
  - 使用 Softmax 参数化策略，采用自然策略梯度（NPG）更新。
  - 算法流程（Algorithm 1）：在每个时间步判断当前成本状态，选择对应模式，调整样本量，执行相应更新。
- **理论保障**：提供了收敛率 \( \tilde{O}\left(\sqrt{\frac{|S||A|}{(1-\gamma)^3 T}}\right) \)，证明了减少振荡和样本效率提升。

## 3. 实验设计
- **数据集/场景**：
  - **Safety-MuJoCo**：包含 SafetyReacher-v4、SafetyWalker2d-v4、SafetyHumanoidStandup-v4 等任务，安全约束包括速度限制和机器人健康。
  - **Omnisafe**：包含 SafetyHopperVelocity-v1、SafetyAntVelocity-v1 等任务，主要约束机器人速度。
- **Benchmark**：Safety-MuJoCo（2024年发布，侧重 primal 方法）和 Omnisafe（侧重 primal-dual 方法）。
- **对比方法**：
  - Primal 基线：CRPO、PCRPO
  - Primal-dual 基线：PPOLag、CUP、PCPO

## 4. 资源与算力
- **文中说明**：
  - Safety-MuJoCo 实验在 Ubuntu 20.04.3 LTS 系统，AMD Ryzen-7-2700X CPU，NVIDIA GeForce RTX 2060 GPU 上运行。
  - Omnisafe 实验在 Ubuntu 20.04.6 LTS 系统，2×AMD EPYC-7763 CPU，6×NVIDIA RTX A6000 GPU 上运行。
  - 训练时间在图表中给出（例如 SafetyReacher-v4：ESPO 50 min vs CRPO 57 min vs PCRPO 67 min；其他任务类似）。
- **未明确说明**：未提供每次实验的种子数或总 GPU 小时数，仅提及至少 3 个随机种子。

## 5. 实验数量与充分性
- **实验数量**：
  - 在 Safety-MuJoCo 上进行了 3 个任务（Reacher、Walker、HumanoidStandup）的对比实验。
  - 在 Omnisafe 上进行了 2 个任务（HopperVelocity、AntVelocity）的对比实验。
  - 消融实验包括：不同成本限制、不同样本大小、不同梯度权重（xr,xc）、不同学习率、更新风格分析（表 3）。
  - 总共约 5 个主实验+多组消融实验，覆盖多种设定。
- **充分性与公平性**：
  - 对比方法均为 SOTA，参数使用官方推荐或调优后设置。
  - 每个实验至少 3 个随机种子，结果图显示均值曲线（可能包含阴影，但文中未明确声明误差棒形式）。
  - 实验覆盖了 primal 和 primal-dual 两大范式，且跨两个不同 benchmark，较为充分。
  - 消融实验验证了超参数鲁棒性，但缺少对样本调整参数 ζ⁺、ζ⁻ 的敏感性分析。

## 6. 主要结论与发现
- **样本效率**：ESPO 在 Safety-MuJoCo 上比 CRPO 和 PCRPO 节省 25-29% 的样本（例如 Reacher 任务 ESPO 5.7M vs 基线 8M），训练时间减少 21-38%。
- **回报与安全**：ESPO 在几乎所有任务上获得更高的累计回报，同时保证安全约束（成本低于阈值），而部分基线（如 CUP、PPOLag）无法维持安全。
- **理论支持**：收敛率与 CRPO 同级，且证明了减少振荡和样本效率优势。
- **更新风格**：ESPO 有更多步骤同时优化回报和成本（199 步 vs CRPO 的 0 步），仅有 3 步纯成本优化，而 CRPO 有 322 步纯成本优化，表明 ESPO 更有效地平衡了目标。

## 7. 优点
- **方法新颖**：首次将基于梯度冲突的样本自适应调整引入安全 RL，结合三模式优化，既提升效率又保证安全。
- **理论完整**：提供了收敛性、振荡减少和样本效率的严格证明，填补了 PCRPO 等方法的理论空白。
- **实验扎实**：在两种主流 benchmark 上对比了 primal 和 primal-dual 两类基线，并进行了多组消融实验，验证了方法的鲁棒性。
- **实用性**：训练时间显著减少，且无需调优对偶参数或依赖初始化（如 primal-dual 方法），更易于部署。

## 8. 不足与局限
- **实验覆盖有限**：仅在仿真环境（MuJoCo 和 Omnisafe）中验证，缺乏真实机器人或现实世界应用。
- **超参数依赖**：样本调整参数 ζ⁺、ζ⁻、软约束边界 h⁺、h⁻ 需要手动设置，文中虽提供了不同任务的默认值，但敏感性分析不足。
- **偏差风险**：结果图中未显示误差棒或置信区间，仅依赖至少 3 个随机种子，统计显著性未量化。
- **应用限制**：算法假设策略为 Softmax 参数化和表格设置（理论分析），扩展到深度网络和复杂状态空间时，理论保证可能不直接适用；且对大规模任务的计算开销未详细讨论。
- **未涉及 Control Barrier Function (CBF)**：论文未将方法与 CBF 或安全控制理论结合，适用范围限于 RL 优化框架。

（完）
