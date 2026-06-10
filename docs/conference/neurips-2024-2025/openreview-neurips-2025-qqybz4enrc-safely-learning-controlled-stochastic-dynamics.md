---
title: Safely Learning Controlled Stochastic Dynamics
title_zh: 安全学习受控随机动力学
authors: "Luc Brogat-Motte, Alessandro Rudi, Riccardo Bonalli"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=QQybz4enRc"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 确保安全域内受控动力学的安全学习
tldr: 在训练和部署过程中确保系统轨迹始终处于预设安全区域是安全关键应用的核心。本文提出一种基于核函数置信界的方法，从初始安全控制集出发迭代扩展，实现安全探索和高效动力学估计，仅需平滑性假设和初始安全集。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-qqybz4enrc/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1436, \"height\": 575, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-qqybz4enrc/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1448, \"height\": 362, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-qqybz4enrc/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1444, \"height\": 266, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-qqybz4enrc/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1454, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-qqybz4enrc/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1035, \"height\": 239, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-qqybz4enrc/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1460, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-qqybz4enrc/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1329, \"height\": 366, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-qqybz4enrc/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 729, \"height\": 452, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-qqybz4enrc/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 832, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-qqybz4enrc/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1453, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-qqybz4enrc/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1411, \"height\": 886, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-qqybz4enrc/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1493, \"height\": 708, \"label\": \"Table\"}]"
motivation: 需要一种方法在安全限制下学习随机动力学，同时保证探索的安全性。
method: 利用核函数置信界迭代扩展初始安全控制集，进行安全探索和模型估计。
result: 学习到的模型能预测系统动力学并验证任意控制的安全性。
conclusion: 为受控随机动力学的安全学习与验证提供了通用框架。
---

## Abstract
We address the problem of safely learning controlled stochastic dynamics from discrete-time trajectory observations, ensuring system trajectories remain within predefined safe regions during both training and deployment. Safety-critical constraints of this kind are crucial in applications such as autonomous robotics, finance, and biomedicine. We introduce a method that ensures safe exploration and efficient estimation of system dynamics by iteratively expanding an initial known safe control set using kernel-based confidence bounds. After training, the learned model enables predictions of the system's dynamics and permits safety verification of any given control. Our approach requires only mild smoothness assumptions and access to an initial safe control set, enabling broad applicability to complex real-world systems. We provide theoretical guarantees for safety and derive adaptive learning rates that improve with increasing Sobolev regularity of the true dynamics. Experimental evaluations demonstrate the practical effectiveness of our method in terms of safety, estimation accuracy, and computational efficiency.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在训练和部署过程中，如何安全地学习受控随机动力系统的动力学模型？即，在收集轨迹数据以估计系统状态概率密度时，必须保证所有执行的轨迹以高概率始终处于预设的安全区域内，并能够在训练前或训练后验证任一控制输入的安全性。
- **背景和动机**：许多实际应用（如自主机器人导航、金融投资组合管理、生物医学）中，系统动力学仅部分已知，且存在随机扰动（风、传感器噪声、市场波动等）。传统的数据收集方法可能因“盲目探索”导致不安全的轨迹，造成系统损坏或违反安全要求。因此，需要一种在探索过程中能同时保证安全并高效估计系统动力学的方法。
- **整体含义**：论文提出了一种基于核函数置信边界（kernel-based confidence bounds）的安全探索与学习框架，能够在不牺牲安全性的前提下，逐步扩展已知的安全控制集，并在训练后提供对任意控制输入的安全验证能力。该方法仅需系统动力学具有足够的光滑性（Sobolev正则性）以及一个初始非空的安全控制集，适用范围广泛。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：借鉴 Safe UCB（安全上置信界）框架，将学习与安全约束耦合。通过迭代地选择能使模型不确定性最大化的控制参数，同时确保所选控制满足安全概率和重置概率的下界，逐步扩展已知的安全-可重置控制集。训练过程中联合学习三个模型：动力学模型（状态密度）、安全模型（安全概率）和重置模型（重置概率），均使用核岭回归（kernel ridge regression）并辅以置信区间。
- **关键技术细节**：
  - **问题形式化**：系统由随机微分方程（SDE）描述，状态密度 \( p_\theta(t, x) \) 依赖于控制参数 \(\theta\)。安全定义为状态落入预设安全区域的概率 \( s(\theta, t) \)，重置定义为轨迹末端可复位到初始分布的概率 \( r(\theta, t) \)。
  - **三个核心模型**：
    - 动力学模型：通过核密度估计（Nadaraya–Watson型）和核岭回归估计状态密度 \(\hat{p}_\theta(t, x)\)。
    - 安全/重置模型：基于观测数据估计安全概率 \(\hat{s}_N(\theta, t)\) 和重置概率 \(\hat{r}_N(\theta, t)\)。
    - 不确定性：预测不确定性 \(\sigma_N(\theta, t)\) 由核函数的条件方差给出。
  - **安全采样**：定义下置信界（LCB）：\( \text{LCB}^s_N(\theta, T) = \inf_{t \in [0,T]} (\hat{s}_N(\theta, t) - \beta^s_N \sigma_N(\theta, t)) \)，类似定义 \( \text{LCB}^r_N \)。只有当两者均不低于预设阈值 \(1-\varepsilon\) 和 \(1-\xi\) 时，控制才被选为可行。
  - **迭代扩展**：初始已知安全-可重置集 \(\Gamma_0\) 给定后，每轮选择使 \(\sigma_N(\theta, t)\) 最大的可行点（即当前不确定性最大的地方）进行采样，收集轨迹数据，更新三个模型和不确定性，重复直至不确定性低于阈值 \(\eta\)。
  - **算法流程**（见论文附录B）：包括密度估计、概率计算、核映射拟合、安全采样（含局部区域增长策略）等步骤，支持并行化。
- **公式/算法**：核岭回归形式为 \(\hat{p}_\theta(t, x) = \hat{P}(x)(K + N\lambda I)^{-1}k(\theta, t)\)，类似定义 \(\hat{s}_N\) 和 \(\hat{r}_N\)。置信参数 \(\beta^s_N\) 和 \(\beta^r_N\) 基于RKHS范数的上界设定。

## 3. 实验设计：数据集/场景、benchmark、对比方法

- **场景**：一个二维二阶随机动力系统，位置 \(X(t) \in \mathbb{R}^2\)，速度 \(V(t) \in \mathbb{R}^2\)，受控加速度和空间相关噪声（高斯型）。安全区域为 \((-10,10)^2\)，重置区域为原点半径2.5的圆盘。初始状态为 \(\mathcal{N}(0, 0.1 I)\)，时间上限 \(T_{\max}=20\)。
- **控制空间**：参数化控制 \(\theta = (\theta_1, \theta_2)\)，表示两个加速度方向，每个方向施加固定时长，附带阻尼项使速度收敛，探索阶段后由一个反馈控制器引导至初始分布。
- **数据集**：无外部数据集，所有轨迹由 SDE 模拟生成。训练时对每个选定的控制参数重复采样 Q=200 条轨迹用于估计。
- **Benchmark**：论文未设置外部 benchmark，也未与现有方法进行对比。实验主要考察自身方法在不同安全/重置阈值 \((\varepsilon, \xi) \in \{0.1, 0.3, 0.5, \infty\}\) 下的表现，评估安全保证、探索效率、预测精度和计算成本。
- **无对比方法**：论文明确指出“据我们所知，目前没有工作在连续时间连续状态设定下提供联合安全探索和密度估计的保证”。因此实验仅展示本方法的效果，无基线对比。

## 4. 资源与算力

- **硬件**：Apple M3 Pro 芯片，18 GB 内存（见附录B.4）。
- **运行时间**：每次迭代约 \(1.92 \pm 0.02\) 秒，1000 次迭代总时长约 \(31.77 \pm 0.38\) 分钟（基于20次重复运行）。密度预测在 2500 点的网格上约需 10 秒。
- **标注**：论文没有使用 GPU，也未提及大规模计算集群。所有实验在单台个人电脑上完成，算力需求合理。作者指出可以通过近似方法（如 sketching、并行化）进一步加速。

## 5. 实验数量与充分性

- **实验数量**：主要实验为一组：在不同安全/重置阈值（4个设置）下各运行1000次迭代。给出了：
  - 安全/重置概率随迭代变化的曲线（图3）。
  - 控制覆盖散点图（图4）。
  - 安全/重置预测误差的均值和标准差（表1）。
  - 动力学预测的定性可视化（图7）。
  - 信息增益曲线（图8，附录C.2）。
- **消融实验**：无正式的消融实验，仅通过调整阈值展示了安全-探索权衡。
- **充分性评价**：
  - **优点**：覆盖了安全、重置、动力学预测、计算时间等多个维度，且提供了多次运行的标准差，具有一定统计意义。
  - **不足**：
    - 缺乏与任何基线方法的定量比较（如 Safe BO、Safe RL 等），无法评估本方法的相对优势。
    - 实验仅在一个低维（2D）系统上进行，未验证高维或更复杂系统。
    - 控制参数空间为2维，探索空间有限。
    - 未对核函数、置信参数 \(\beta\)、正则化系数 \(\lambda\) 等超参数进行系统的敏感性分析。
    - 没有测试不同噪声强度或不同初始安全集大小的影响。
    - 安全保证仅在模拟中验证，未在真实物理系统上测试。

## 6. 论文的主要结论与发现

- **安全保证**：提出的方法能够在整个学习过程中保证所有执行轨迹以高概率 (≥1-ε) 处于安全区域，且轨迹终点以高概率 (≥1-ξ) 落入可重置区域。训练结束后，ΓN 可作为已认证的安全控制集用于部署。
- **估计精度**：在满足采样条件（如 \(Q \gtrsim N^{(2\nu+n)/(2\nu-n)}\)）时，动力学、安全概率、重置概率的估计误差均可由不确定性阈值 \(\eta\) 线性控制，即 \(\|\hat{p} - p\|_\infty \leq c_3 \eta\)，\(|\hat{s} - s| \leq c_4 \eta\)，\(|\hat{r} - r| \leq c_5 \eta\)。
- **样本复杂度**：算法在最多 \(N = O(\eta^{-2/(1-\alpha)})\) 次迭代后停止，其中 \(\alpha > (m+1)/(m+1+2\nu)\) 反映信息增益的次线性增长，且学习率随 Sobolev 正则性 \(\nu\) 的增加而改善（适应性的）。
- **安全-探索权衡**：阈值 \((\varepsilon, \xi)\) 越宽松（接近 ∞），控制覆盖越大、信息增益越快，但安全风险增加；反之，严格阈值限制了探索，尤其在安全/重置概率接近阈值的区域形成瓶颈。
- **计算可行性**：在标准个人电脑上 1000 次迭代约需 32 分钟，计算成本可接受。

## 7. 优点：方法或实验设计上的亮点

- **理论保证完整**：同时提供了学习过程中的安全保证（所有轨迹安全）和估计误差的收敛率，且对 Sobolev 光滑性具有自适应性。
- **假设弱且实际**：仅要求系统动力学足够光滑（Sobolev正则性）和初始存在一个已知安全控制，无需已知动力学模型、安全预评估或特殊控制结构。
- **统一框架**：同时学习动力学、安全概率、重置概率，并利用共享核函数和置信边界进行安全探索，实现了“边学习、边探索、边保证安全”。
- **实验设计合理**：通过调整安全/重置阈值直观展示了安全-探索权衡；给出了预测误差的统计量和多次运行的标准差，具有一定说服力。
- **开源实现**：提供了完整的 Python 代码，便于复现和后续应用。

## 8. 不足与局限

- **缺乏基线对比**：未与 Safe BO、Safe RL、模型预测安全滤波等现有方法在相同设定下进行定量比较，难以评估本方法的相对有效性。
- **实验场景单一**：仅在一个 2D 二次系统上验证，未测试更高维系统、非高斯噪声、强非线性或实际机器人平台。虽然理论分析表明在高维下收敛率仍成立，但实验支撑不足。
- **超参数敏感性未分析**：核类型、正则化 \(\lambda\)、置信参数 \(\beta\)、带宽 \(R\) 等均需人工设定，论文仅给出了调参建议，缺乏系统性实验说明方法的鲁棒性。
- **初始化依赖**：要求事先知道至少一个安全控制点和重置点（即 \(\Gamma_0\)），在完全未知的系统启动时可能难以满足。
- **重置假设较强**：假设可重置区域存在并能实际执行复位操作，对于某些实时系统（如连续运行的化学过程）可能不现实。
- **计算复杂度**：尽管实验时间可接受，但算法复杂度为 \(O(N^3 + M N^2)\)（\(N\) 为迭代次数，\(M\) 为候选点数目），随着 \(N\) 增大可能成为瓶颈，虽然可用近似方法缓解。
- **安全概率的保守性**：使用下置信界可能导致探索过于保守，特别是在安全函数非凸或边界不规则时，可能长时间停滞在初始安全区域附近。

（完）
