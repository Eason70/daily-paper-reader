---
title: Learning Dynamics under Environmental Constraints via Measurement-Induced Bundle Structures
title_zh: 通过测量诱导的束结构学习环境约束下的动力学
authors: "Dongzhe Zheng, Wenjie Mei"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=mwSBIlNLdQ"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 提出测量感知的控制屏障函数用于约束下的安全控制
tldr: 该文针对环境约束下的动力学学习问题，提出一种基于纤维束结构的几何框架，将测量、约束与动力学学习统一。框架自然导出测量感知的控制屏障函数，使其能适应局部传感条件，为安全控制提供几何基础。该方法有望为无人系统在不确定环境中的安全控制提供新思路。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-mwsbilnldq/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 830, \"height\": 281, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mwsbilnldq/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1757, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mwsbilnldq/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 820, \"height\": 499, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-mwsbilnldq/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1521, \"height\": 580, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mwsbilnldq/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 765, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mwsbilnldq/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1183, \"height\": 463, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mwsbilnldq/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1112, \"height\": 405, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mwsbilnldq/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1470, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mwsbilnldq/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1454, \"height\": 274, \"label\": \"Table\"}]"
motivation: 现有方法需要全局约束信息或概率滤波，未能充分利用局部测量的几何结构，导致控制屏障函数设计不够灵活。
method: 提出基于纤维束结构的几何框架，将状态空间上的局部测量、约束与动力学学习统一，并由此导出测量感知的控制屏障函数。
result: 该方法能够让控制屏障函数根据局部传感条件自适应调整，在仿真中展示了比传统方法更好的约束满足性能。
conclusion: 所提几何框架有效融合了局部测量与约束结构，为环境约束下的安全控制提供了新的工具。
---

## Abstract
Learning unknown dynamics under environmental (or external) constraints is fundamental to many fields (e.g., modern robotics), particularly challenging when constraint information is only locally available and uncertain. Existing approaches requiring global constraints or using probabilistic filtering fail to fully exploit the geometric structure inherent in local measurements (by using, e.g., sensors) and constraints. This paper presents a geometric framework unifying measurements, constraints, and dynamics learning through a fiber bundle structure over the state space. This naturally induced geometric structure enables measurement-aware Control Barrier Functions that adapt to local sensing (or measurement) conditions. By integrating Neural ODEs, our framework learns continuous-time dynamics while preserving geometric constraints, with theoretical guarantees of learning convergence and constraint satisfaction dependent on sensing quality. The geometric framework not only enables efficient dynamics learning but also suggests promising directions for integration with reinforcement learning approaches. Extensive simulations demonstrate significant improvements in both learning efficiency and constraint satisfaction over traditional methods, especially under limited and uncertain sensing conditions.

---

## 论文详细总结（自动生成）

# 中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在环境约束未知且仅能通过局部、不确定的传感器测量获取信息时，如何学习系统动力学并同时保证安全约束满足。
- **背景与动机**：传统控制屏障函数（CBF）将测量视为外部观测，未充分利用其几何结构；全局约束知识在现实场景中难以获得；概率滤波方法无法有效利用局部测量的固有几何信息。论文旨在通过微分几何中的纤维束结构，统一测量、约束和动力学学习，使安全控制能够自适应局部传感条件。

## 2. 论文提出的方法论

### 核心思想
- 利用测量不确定性在状态空间上自然诱导的纤维束结构（fiber bundle），将状态空间 \(M\) 与测量空间 \(Y\) 构成总空间 \(E = M \times Y\)，并定义连接（connection）来描述状态与测量之间的几何关系。
- 在纤维束上定义测量自适应的控制屏障函数（mCBFs），自动根据局部测量质量调整安全裕度。
- 结合神经常微分方程（Neural ODEs）学习连续时间动力学，同时利用束结构保持物理约束。

### 关键技术细节
1. **系统模型与测量结构**：状态 \(x \in M\)，控制 \(u \in U\)，动态 \(\dot{x} = f(x,u) + g(x)w\)，测量 \(y = h(x) + v\)，噪声有界。
2. **纤维束框架**：投影 \(\pi: E \to M\)，纤维 \(\pi^{-1}(x) = \{(x,y): y = h(x)+v, \|v\|\le \delta_v\}\)。连接 \(\nabla\) 耦合状态与测量微分。
3. **束上的安全证书**：光滑映射 \(\Phi: E \to \mathbb{R}\) 满足：在名义安全集上正值、束导数正定、与测量不确定性相关。
4. **测量自适应CBF（mCBF）**：函数 \(b: E \to \mathbb{R}\) 需满足：\(b(x,y)\ge 0 \Rightarrow x\in S_0\)；李导数条件下 \(\inf_u (L_f b + (L_g b)w + \alpha(b)) \ge 0\)；对测量Lipschitz连续。
5. **安全保证定理（Theorem 3.1）**：若初始mCBF非负，则对任何有界噪声，保持安全集的概率 \(\ge 1 - \exp(-c/\delta_v^2)\)。
6. **学习框架**：定义束值学习算子，通过梯度下降更新动力学估计 \(\hat{f}\) 和安全证书 \(\Phi\)，损失函数用测量不确定性加权。策略更新时投影到安全集。

## 3. 实验设计

### 场景与任务
- **三个机器人控制任务**：
  - **软体蠕虫导航**：0.1m长蠕虫，用物质点法（MPM）模拟，四个肌肉信号控制，躲避障碍到达目标。
  - **Franka 7-DOF机械臂操作**：关节空间运动，需要避免关节限位和障碍物。
  - **四旋翼无人机3D导航**：位置、速度、姿态、角速度动力学，深度传感器测量障碍距离。

### 基准方法
- 学习安全认证：Neural-CBF, SafeLearn, SafetyNet, SafeTrack, StructCBF。
- 物理信息/几何方法：PNDS, GEM, GeoPath。
- 鲁棒与自适应控制：RobustSafe, DataFilter, AdaptSafe。
- 不确定性预测控制：GPMPC, ALMPC, SafeRL。

### 评估指标
- 成功率(SR)、路径长度(PL)、步数(GRS)、最终状态误差(FSE)、最小安全距离(MMC)、平均安全裕度(AMC)、约束满足率(CSR)、控制幅度(ACM)、控制平滑度(CS)。

### 实验设置
- 网格：2m×2m×2m工作空间，随机障碍物位置。
- 蠕虫：500次试验；Franka臂：400次；四旋翼：300次。
- 每个条件重复10次试验（不同随机种子）。

## 4. 资源与算力

- **硬件**：Intel Xeon CPU, NVIDIA RTX 3090 GPU (24GB GDDR6X), 64GB RAM。
- **软件**：Python 3.9, PyTorch 1.12.0, CUDA 11.7, cuDNN 8.5。
- **训练时间**：本文方法约5小时（在RTX 3090上），Neural-CBF约4小时，GPMPC约3小时。
- **未说明**：未提及使用的GPU数量（推测为单卡），也未提及分布式训练或集群细节。

## 5. 实验数量与充分性

- **总实验数量**：三个任务共约1200次完整试验（蠕虫500+臂400+无人机300），每次试验对应一条轨迹。此外，每个条件重复10次以统计均值和标准差。
- **消融实验**：三个关键组件（束结构、mCBF、李群对称性）的消融，每个组件10次独立运行，跨三个任务（共约90次消融运行）。
- **扩展领域实验**：额外在建筑气候控制、批反应控制、电网频率控制三个领域验证（各1000 episode，10次重复）。
- **噪声鲁棒性实验**：不同噪声水平（σ=0.1-0.3）下对比成功率。
- **不确定性模式消融**：高斯噪声、固定偏置、时变偏置、延迟、传感器故障等。
- **束结构变体消融**：固定/自适应维度、简单/复杂连接。
- **几何表示比较**：纤维束 vs 积流形、向量丛、主丛。
- **充分性评估**：实验覆盖了多种任务类型、噪声模式、组件变体，并使用了统计重复。基线比较全面，消融为每组件贡献提供了定量证据。实验设计较为充分、客观。

## 6. 论文的主要结论与发现

- 提出的纤维束几何框架统一了测量、约束和动力学学习，使安全证书能根据局部测量质量自适应调整。
- 方法在三个机器人任务中**成功率96.3%**，显著优于传统方法（最高89.7%），同时路径更短（18.5m vs 21.7-26.9m），控制更平滑。
- 约束满足率（99.3%）与最优基线持平或更高，但控制幅度更小（0.17 vs 0.20-0.29），表明更高效。
- 收敛速度快，训练波动小。
- 在不同噪声水平下保持稳健性（成功率>91%），而基线方法在高噪声时显著下降。
- 消融表明：束结构、mCBF是核心组件（移除后成功率分别降至62.7%和45.7%），李群对称性作为增强（移除后仍达85.7%）。

## 7. 优点

- **理论创新**：将微分几何的纤维束引入安全学习控制，为测量不确定性与安全约束提供了统一几何框架，定理提供了概率安全保证。
- **方法设计**：mCBF自动适应测量质量，无需全局约束知识，实用性强。
- **实验全面**：覆盖三种不同机器人（软体、刚体臂、无人机）、多种基线（10+种）、多种不确定性模式、消融实验、跨领域验证。
- **性能卓越**：在成功率、路径效率、控制平滑度等多维度领先。
- **开源可复现**：代码公开，实验细节充分（超参数、网络结构、训练流程）。

## 8. 不足与局限

- **实验局限**：
  - 仿真环境（Genesis物理引擎），未在真实机器人上验证，实际传感器噪声、延迟、非线性可能更复杂。
  - 每个任务的具体障碍物数量及采样方式未详细说明，难以完全复现。
  - 跨领域扩展实验（建筑、化工、电网）虽然覆盖广，但模型简化较多，与真实工业场景存在差距。
- **理论局限**：
  - 假设测量噪声为次高斯且状态空间光滑，对非光滑、非高斯噪声或强非线性系统适用性未验证。
  - 安全概率下界与测量噪声方差相关，在高噪声环境下保守性可能过强，但未讨论自适应调整策略。
- **计算复杂性**：纤维束结构增加了维度，虽然论文提到效率可接受，但未与轻量级方法（如简单CBF）比较计算耗时。
- **偏差风险**：基线方法的选择偏向于传统方法，未包含较新的几何深度学习模型（如等变网络），论文在附录F中说明了原因（目标不同），但可能遗漏了有竞争力的近期工作。
- **可扩展性**：方法依赖于光滑流形和连接，对于离散或混合状态系统可能不直接适用。

（完）
