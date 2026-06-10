---
title: Learning Safe Control via On-the-Fly Bandit Exploration
title_zh: 通过在线Bandit探索学习安全控制
authors: "Alexandre Capone, Ryan Kazuo Cosner, Aaron Ames, Sandra Hirche"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=X6nIBckemw"
tags: ["query:safe-rl-cbf"]
score: 9.0
evidence: 基于CBF的安全控制与bandit探索
tldr: 针对模型不确定性高时安全过滤器可能无效的问题，提出一种结合控制屏障函数（CBF）和高斯过程bandit算法的在线探索方法。当安全过滤器无可行解时，算法动态收集额外数据以改进模型，从而恢复可行性。理论证明安全证书在可行时保证安全，实验验证了在不确定系统中维持安全的有效性，为安全控制提供了一种无需备份控制器的实用方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-x6nibckemw/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1756, \"height\": 656, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x6nibckemw/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 805, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x6nibckemw/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 807, \"height\": 377, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x6nibckemw/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 516, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x6nibckemw/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 808, \"height\": 490, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x6nibckemw/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 808, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-x6nibckemw/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1718, \"height\": 574, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-x6nibckemw/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 864, \"height\": 1320, \"label\": \"Table\"}]"
motivation: 高模型不确定性下基于学习的安全过滤器可能无可行控制输入。
method: 结合控制屏障函数与高斯过程bandit算法，在过滤器无效时在线收集数据以改进模型。
result: 在多种不确定系统中维持安全，避免了备份控制器的需要。
conclusion: 为模型不确定下的安全控制提供了实用且可证安全的探索方法。
---

## Abstract
Control tasks with safety requirements under high levels of model uncertainty are increasingly common. Machine learning techniques are frequently used to address such tasks, typically by leveraging model error bounds to specify robust constraint-based safety filters. However, if the learned model uncertainty is very high, the corresponding filters are potentially invalid, meaning no control input satisfies the constraints imposed by the safety filter. While most works address this issue by assuming some form of safe backup controller, ours tackles it by collecting additional data on the fly using a Gaussian process bandit-type algorithm. We combine a control barrier function with a learned model to specify a robust certificate that ensures safety if feasible. Whenever infeasibility occurs, we leverage the control barrier function to guide exploration, ensuring the collected data contributes toward the closed-loop system safety. By combining a safety filter with exploration in this manner, our method provably achieves safety in a general setting that does not require any prior model or backup controller, provided that the true system lies in a reproducing kernel Hilbert space. To the best of our knowledge, it is the first safe learning-based control method that achieves this.

---

## 论文详细总结（自动生成）

# 论文总结：Learning Safe Control via On-the-Fly Bandit Exploration

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在控制任务中，当模型不确定性较高时，基于约束的安全过滤器（如控制屏障函数CBF）可能变得“不可行”（infeasible），即不存在任何控制输入能满足安全约束。现有大多数方法假设存在一个安全的备份控制器（backup controller）来应对这种情况，但该假设在许多实际场景中难以满足。
- **背景**：安全关键系统（如自动驾驶、医疗机器人）对安全性要求极高。控制屏障函数（CBF）是一种常用的保证约束满足的工具，但在系统动力学部分未知时，需要结合学习模型（如高斯过程GP）来构建鲁棒安全过滤器。然而，若模型误差过大，鲁棒约束可能无解。
- **研究动机**：提出一种无需备份控制器的方法，通过在线探索（on-the-fly exploration）主动收集数据来降低不确定性，从而恢复安全过滤器的可行性，并严格保证安全性。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：将控制屏障函数（CBF）与高斯过程（GP）bandit探索算法结合。当安全过滤器（一个基于LCB的鲁棒约束二阶锥规划SOCP）可行时，应用该过滤器输出安全控制；当不可行时，切换至探索模式，通过最大化UCB（上置信界）来选择控制输入，收集数据以改进模型，从而尽快恢复可行性。
- **关键技术细节**：
  - 系统模型：仿射控制系统 \( \dot{x} = f(x) + g(x)u \)，其中 \(f,g\) 部分未知。
  - 安全集： \( C = \{x \mid h(x) \ge 0\} \)，其中 \(h\) 是已知的CBF。
  - 鲁棒安全过滤器（SOCP）：
    \[
    \pi_{N,\text{safe}}(x) = \arg\min_{u\in U} \|u - \pi_{\text{nom}}(x)\|^2 \quad \text{s.t.} \quad \text{LCB}_N(x,u) \ge -\alpha(h(x)) + \epsilon/2.
    \]
    其中 \(\text{LCB}_N(x,u) = \frac{\partial h}{\partial x} \mu_N(x,u) - L_h \beta_N \sqrt{\operatorname{tr}(\Sigma_N(x,u))}\)。
  - 探索策略：当过滤器不可行（\(\max_u \text{LCB}_N = -\alpha(h(x)) + \epsilon/2\)）时，选择 \(u^{(N+1)} = \arg\max_{u} \text{UCB}_N(x,u)\)，然后应用该控制输入固定时间 \(\Delta t\)，收集测量数据并更新GP模型。
  - 理论保证：定理3.2表明，如果采样时间 \(\Delta t\) 足够大（满足不等式(16)），则系统以高概率保持安全，且在有限次数据收集后安全过滤器将永久可行。
- **算法流程**（Algorithm 1）：
  1. 初始化GP先验、CBF \(h\)、类-\(\mathcal{K}\)函数 \(\alpha\)。
  2. 在每个时间步，若当前未在探索模式，则检查鲁棒SOCP是否严格可行。若可行，应用安全过滤器输出；否则进入探索模式，记录时间 \(t_N\)，计算 \(u^{(N)}\) 并设置探索标志。
  3. 探索期间：在 \([t_N, t_N+\Delta t]\) 内应用一个局部Lipschitz控制器（如常值 \(u^{(N)}\)），并收集测量数据。
  4. 在 \(t=t_N+\Delta t\) 时，更新GP模型，清除探索标志。

## 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法

- **场景**：
  - **巡航控制（Cruise Control）**：一个自适应巡航控制系统的仿真，状态为车速和与前车的距离，CBF用于维持安全车距。动力学为仿射形式，部分未知（滚动阻力参数未知）。无先验模型，使用零均值GP先验，初始10个数据点用于学习超参数。
  - **四旋翼（Quadrotor）**：带地面效应的四旋翼动力学仿真，状态包括位置、速度、姿态（四元数）。使用两个CBF（一个针对高度，一个针对微分平坦性约束）。同样无先验模型，仅知动力学的一部分（不含控制输入影响）。
- **Benchmark**：论文未明确列出标准benchmark，但比较了**随机探索**作为基线：在过滤器不可行时，随机从控制空间均匀采样一个控制输入，而非使用UCB引导的探索。
- **对比方法**：主要对比了“随机探索”与“本文提出的UCB引导探索”在不同采样频率（\(\Delta t\)）下的失败率（failure rate）。未与其他现有安全学习方法（如基于备份控制器的方法）对比，因为论文声称那些方法在零先验、无备份控制器设定下无法工作。
- **无监督学习/预训练**：所有仿真均从零开始，无预训练模型。

## 4. 资源与算力

- **文中未明确提及**使用的GPU型号、数量或训练时长。所有实验为数值仿真，可能仅使用CPU进行在线计算（GP更新和SOCP求解）。由于是控制仿真，算力需求相对较低。未提供详细信息。

## 5. 实验数量与充分性

- **实验数量**：
  - 巡航控制：单次仿真时长100秒，展示了CBF值和LCB的时序图。
  - 四旋翼：单次仿真时长50秒，展示了轨迹和CBF/LCD图。
  - 比较实验：对每种方法（本文方法与随机探索）在不同采样频率下分别进行了**100次**模拟（不同初始条件均匀采样），统计失败率。
- **充分性评价**：
  - **积极方面**：比较实验覆盖了多个采样频率，定量评估了方法对采样时间的敏感性；失败率在100次重复下具有统计意义。
  - **不足**：
    - 仅与随机探索对比，未与其他主流安全探索方法（如SafeOpt、GoSafeOpt等）比较。
    - 未在多种不同系统上验证（只有两个仿真案例），缺乏对高维系统或实际硬件的验证。
    - 消融实验不完整：未单独分析CBF选择、GP核函数、超参数学习等的影响。
    - 未展示探索期间的控制输入平滑性、能耗或性能指标（安全性之外的指标）。
  - **客观性**：比较中，随机探索的失败率明显更高，作者声称本文方法更好，结果可信，但缺乏统计显著性检验（如t检验或置信区间）。

## 6. 论文的主要结论与发现

- **主要结论**：本文提出的将CBF安全过滤器与GP bandit探索相结合的方法，能够在无需备份控制器和零先验动力学模型的前提下，高概率地保证系统安全性。理论上证明了安全过滤器在有限步探索后必然恢复可行性，实验验证了该方法在两种非线性系统中的有效性，且优于随机探索。
- **关键发现**：采样频率 \(\Delta t\) 是影响安全性的关键因素——更高的采样频率（更短的采样间隔）导致更低的失败率。本文方法在所有测试频率下均优于随机探索，表明UCB引导的探索能更高效地收集有利于恢复可行性的数据。

## 7. 优点：方法或实验设计上有哪些亮点

- **方法创新**：首次将“在线bandit探索”与“CBF鲁棒安全过滤器”结合，解决了高不确定性下过滤器无解的根本问题，而非依赖备份控制器假设。
- **理论严谨**：提供了完整的概率安全性证明（定理3.2），分析了采样时间、模型不确定度、测量噪声等关键参数之间的量化关系。
- **算法实用性**：不需要预先知道任何动力学模型（零均值先验），也不需要安全备份控制器，对实际部署非常友好。
- **实验设计亮点**：通过改变采样频率进行参数敏感性分析，展示了方法在不同时间尺度下的鲁棒性；与随机探索的对比有效地说明了引导探索的优势。

## 8. 不足与局限：包括实验覆盖、偏差风险、应用限制

- **实验覆盖有限**：仅两个仿真案例，且均为低维系统（巡航控制2状态，四旋翼3D但简化）。未在更高维系统（如6自由度机械臂）、实际物理平台或涉及环境干扰的场景中验证。
- **偏差风险**：论文可能选择了有利于自身方法的基准（随机探索），未与同样可用于在线安全探索的现有方法（如SafeOpt、Cautious MPC等）进行公平对比。此外，仿真中可能对系统动力学、噪声分布等做了理想化假设。
- **应用限制**：
  - 需要已知CBF \(h(x)\)，这依赖于专家知识或严格建模；对于复杂任务，设计有效的CBF本身就有挑战。
  - 探索阶段使用的控制输入（由UCB最大化得到）可能引起系统剧烈运动或高频激励，在现实中可能超出物理约束或导致执行器退化（虽然论文声称“合理”预期）。
  - 理论要求系统属于RKHS且核函数选择合适，实际中核函数超参数未知可能影响性能（论文虽提及有方法处理，但未在实验中使用）。
  - 采样时间 \(\Delta t\) 的下界依赖于与信息增益相关的复杂不等式(16)，实际中难以精确计算，可能过于保守。
- **其他不足**：
  - 未讨论探索与控制性能（如跟踪误差）的权衡，仅保证安全性。
  - 算法假设每次探索收集一个新数据点立刻更新GP，但在高维系统或大数据量时，GP更新可能成为计算瓶颈。

（完）
