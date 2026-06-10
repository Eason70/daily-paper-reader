---
title: Safety Certificate against Latent Variables with Partially Unidentifiable Dynamics
title_zh: 针对部分不可识别动力学的潜变量安全证书
authors: "Haoming Jing, Yorie Nakahira"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=AMB11zS6kg"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 针对含潜变量系统的概率安全证书设计
tldr: 本文针对实际系统中存在潜变量导致动力学部分不可识别或分布偏移、从而破坏传统安全证书的问题，提出了一种概率安全证书设计技术，能够在仅部分可观测的统计量下保证系统前向不变性。该方法通过保守的概率界限补偿不可识别性，在仿真实验中展示了鲁棒性，为安全关键系统提供了更实用的安全保证。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-amb11zs6kg/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 737, \"height\": 474, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-amb11zs6kg/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 738, \"height\": 476, \"label\": \"Figure\"}]"
motivation: 潜变量导致动力学不可识别，现有安全证书方法失效。
method: 提出概率安全证书技术，利用保守概率界处理不可识别性。
result: 在多个含潜变量的系统上验证了证书的可行性。
conclusion: 概率方法可有效应对部分可观测性，扩展安全证书适用范围。
---

## Abstract
Existing control techniques often assume access to complete dynamics or perfect simulators with fully observable states, which are necessary to verify whether the system remains within a safe set (forward invariance) or safe actions are persistently feasible at all times. However, many systems contain latent variables that make their dynamics partially unidentifiable or cause distribution shifts in the observed statistics between offline and online data, even when the underlying mechanistic dynamics are unchanged. Such “spurious” distribution shifts can break many techniques that use data to learn system models or safety certificates. To address this limitation, we propose a technique for designing probabilistic safety certificates for systems with latent variables. A key technical enabler is the formulation of invariance conditions in probability space, which can be constructed using observed statistics in the presence of distribution shifts due to latent variables. We use this invariance condition to construct a safety certificate that can be implemented efficiently in real-time control. The proposed safety certificate can persistently find feasible actions that control long-term risk to stay within tolerance. Stochastic safe control and (causal) reinforcement learning have been studied in isolation until now. To the best of our knowledge, the proposed work is the first to use causal reinforcement learning to quantify long-term risk for the design of safety certificates. This integration enables safety certificates to efficiently ensure long-term safety in the presence of latent variables. The effectiveness of the proposed safety certificate is demonstrated in numerical simulations.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：现有安全控制技术通常假设系统动力学完全已知或拥有完美模拟器，且状态完全可观测，从而能够验证前向不变性或安全动作的持续可行性。然而，实际系统中常存在潜变量（latent variables），导致动力学部分不可识别，并引起离线数据与在线数据之间观测统计量的分布偏移（即使底层机械动力学未改变）。这种“虚假”分布偏移会破坏依赖数据学习系统模型或安全证书的方法。
- **核心问题**：如何在存在潜变量（导致分布偏移和部分不可观测动力学）的情况下，高效地保证随机系统的长期安全性？特别是要保证安全证书的持续可行性（persistent feasibility），即始终存在满足安全约束的控制动作。
- **整体含义**：论文首次将因果强化学习引入安全证书设计，以量化长期风险，从而在潜变量存在时仍能确保持续安全。这项工作弥补了随机安全控制与因果强化学习之间的鸿沟，为实际系统中的安全关键控制提供了更实用的方法。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

### 核心思想
- 在概率空间中制定不变性条件（invariance conditions），该条件可以仅利用观测统计量构建，不受潜变量引起的分布偏移影响。
- 将长期安全概率表示为某个马尔可夫决策过程的边值函数（value function），进而利用Q函数来构造安全条件，且该条件可以通过因果强化学习方法从离线数据中学习。

### 关键技术细节
1. **系统模型**：考虑含潜变量的混杂马尔可夫决策过程（confounded MDP），状态 \(X_t\) 可观测，潜变量 \(W_t\) 不可观测，动作 \(U_t\) 可观测。假设 \(W_t\) 仅依赖于 \(X_t\)，且 \(X_t\) 具有马尔可夫性。
2. **分布偏移**：离线数据由行为策略 \(\pi_b\) 生成，该策略依赖于潜变量；而在线策略不依赖于潜变量，因此离线统计量 \(P_{\text{offline}}(X_{t+1}|X_t,U_t)\) 与在线统计量 \(P_{\text{online}}(X_{t+1}|X_t,U_t)\) 不同。
3. **安全目标**：保证长期安全概率 \(P^{\hat\pi,\pi}(C(X_t)\cap\cdots\cap C(X_H)|X_0)\ge 1-\epsilon\)，其中 \(\hat\pi\) 是实际在线策略，\(\pi\) 是用于计算风险的名义策略。
4. **安全性条件**：定义边值函数 \(V^\pi(\hat Y_t)\) 和Q函数 \(Q^\pi(\hat Y_t,U_t)\)，其中 \(\hat Y_t\) 是增强状态（含剩余时间）。安全条件为：
   \[
   S(X_t,U_t,t) = Q^\pi(\hat Y_t,U_t) - \mathbb{E}_{U\sim\pi(\cdot|\hat Y_t)}[Q^\pi(\hat Y_t,U)|\hat Y_t] \ge 0.
   \]
   该条件等价于概率空间中的不变性条件，且满足后则能保证长期安全概率不降低。
5. **持续可行性**：定理3.4证明，总存在一个动作（使Q值最大的动作）满足该条件，因此安全证书可持久可行。
6. **因果强化学习集成**：利用前门调整（front-door adjustment）消除潜变量的混杂偏差，从而从离线数据中无偏估计 \(Q^\pi\)。具体算法使用可观测的媒介变量 \(M_t\)，通过迭代求解最小二乘问题（公式44）来学习 \(Q^\pi_M\)，进而得到 \(Q^\pi\)。

### 算法流程（文字描述）
1. **预处理**：利用离线数据集 \(D\)（包含状态和动作序列），按照算法1生成增强状态数据集 \(\tilde D\)，其中状态在安全时按真实转移更新，不安全时保持不动，时间索引递减。
2. **学习Q函数**：采用因果强化学习方法（如Shi et al. 2024），通过前门调整公式，迭代学习条件Q函数 \(Q^\pi_M\)，并利用它计算 \(Q^\pi\)。
3. **在线控制**：在每个时间步，观测当前状态 \(X_t\)，获取名义策略的动作 \(U_n\)，再通过优化问题（公式55）选择满足安全条件 \(S(X_t,u,t)\ge 0\) 且尽量接近 \(U_n\) 的动作执行。

## 3. 实验设计

- **场景**：一个简化的驾驶场景，状态 \(X_t\) 为二维离散值（位置和速度），潜变量 \(W_t\) 表示道路湿滑程度（影响加速/刹车效果），还有噪声项。安全要求为车辆遵守可变速度限制（取决于位置模10）。
- **数据集**：离线数据由行为策略 \(\pi_b\) 生成，该策略会根据道路湿滑程度施加更重的刹车（但湿滑程度未被传感器记录）。即离线数据存在分布偏移。
- **Benchmark / 对比方法**：离散时间控制障碍函数（DTCBF）方法（Cosner et al. 2023），该方法直接使用离线数据统计量来评估安全条件，不能利用无偏的Q函数。
- **参数设置**：\(H=10\)，\(\epsilon=0.2\)，初始状态 \(X_0=[0,0]^T\)。名义策略为均匀随机动作。
- **实验内容**：进行了100次模拟，每次模拟100条轨迹，对比两种方法的安全概率和长期安全概率随时间的变化。

## 4. 资源与算力

论文中**未明确说明**使用了何种GPU、数量或训练时长。仅提及数值模拟为离散状态空间、小规模场景（H=10），因此可以推断算力需求较低，可能使用CPU即可完成。

## 5. 实验数量与充分性

- **实验数量**：100次模拟，每次100条轨迹，总共10000条轨迹。结果给出了安全性概率随时间曲线及95%置信区间。
- **充分性**：实验较为充分，展示了统计稳定性（置信区间较窄），并且清楚地展示了所提方法满足安全目标（概率始终高于1-ϵ），而DTCBF方法失败。但**没有进行消融实验**（如不同ϵ、不同H、不同分布偏移程度下的性能），也未测试更复杂或连续状态空间。实验仅在一个特定离散场景上验证，泛化能力尚需更多证据。
- **客观性**：实验设计相对客观：对比了已有方法，且所提方法的Q函数被假设为无偏估计（未讨论学习误差的影响）。DTCBF的失败原因在理论部分已解释，实验结果与理论一致。

## 6. 论文的主要结论与发现

- 所提出的概率安全证书能够在潜变量存在且动力学部分不可识别的情况下，保证长期安全概率不低于给定阈值 \(1-\epsilon\)，并且具有持续可行性。
- 与基线DTCBF相比，所提方法在安全性能上显著更优：其安全概率始终在阈值以上，而DTCBF的安全概率随时间迅速下降，无法满足安全目标。
- 因果强化学习可以有效用于安全证书设计，即使离线数据存在分布偏移，也能量化长期风险。

## 7. 优点

- **理论创新**：首次将因果强化学习与安全证书结合，解决了潜变量引起分布偏移这一被忽视的问题。提出了概率空间中的不变性条件，该条件仅需观测统计量，无需完整动力学。
- **可行性保证**：定理3.4证明了控制动作总能满足安全条件，即安全证书具有持续可行性，这是一个很强的实用性优点。
- **算法高效**：安全条件的评估仅需Q函数，无需在线模拟或复杂优化，可实现实时控制。
- **扩展性**：作者指出该框架可推广至其他因果推断技术，具有较好的通用性。

## 8. 不足与局限

- **实验覆盖有限**：仅在单个离散小规模场景上验证，未测试连续状态/动作空间、高维系统、更复杂分布偏移模式等，因此实际应用潜力需进一步验证。
- **未考虑Q函数学习误差**：文中假设可以利用因果RL得到无偏Q函数，但实际学习可能存在偏差和方差，实验中未分析学习误差对安全保证的影响。
- **假设较强**：系统模型要求潜变量满足特定的独立性假设（Assumption 2.1），并且在某些方法中要求离散状态空间和媒介变量（Assumption 3.5），限制了方法的适用范围。
- **计算效率分析缺失**：虽然声称适用于实时控制，但未给出具体的在线计算时间或复杂度分析。
- **缺乏消融实验**：没有对安全阈值ϵ、时间长度H、行为策略偏移程度等参数进行敏感性分析，对方法的鲁棒性理解不够深入。

（完）
