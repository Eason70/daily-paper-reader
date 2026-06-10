---
title: Scalable Constrained Policy Optimization for Safe Multi-agent Reinforcement Learning
title_zh: 可扩展的约束策略优化用于安全多智能体强化学习
authors: "Lijun Zhang, Lin Li, Wei Wei, Huizhong Song, Yaodong Yang, Jiye Liang"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=pJlFURyTG5"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 面向无人机群的安全多智能体强化学习，具备可扩展性
tldr: 现有安全多智能体强化学习方法因全局耦合和状态空间爆炸难以扩展。本文提出一种可扩展的理论性多智能体约束策略优化方法，解决了通信和计算资源受限下的安全协作问题。在无人机群等场景中实验验证了方法的有效性和可扩展性，为实际多智能体系统安全控制提供了新思路。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-pjlfurytg5/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1405, \"height\": 728, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pjlfurytg5/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1407, \"height\": 684, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pjlfurytg5/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1413, \"height\": 692, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-pjlfurytg5/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1409, \"height\": 745, \"label\": \"Figure\"}]"
motivation: 为解决多智能体强化学习中全局安全约束导致的扩展性瓶颈。
method: 提出可扩展的多智能体约束策略优化算法，通过解耦安全约束实现分布式协作。
result: 在无人机群等任务中验证了安全性和可扩展性优于基线方法。
conclusion: 所提方法为资源受限的多智能体系统安全控制提供了有效方案。
---

## Abstract
A challenging problem in seeking to bring multi-agent reinforcement learning (MARL) techniques into real-world applications, such as autonomous driving and drone swarms, is how to control multiple agents safely and cooperatively to accomplish tasks. Most existing safe MARL methods learn the centralized value function by introducing a global state to guide safety cooperation. However, the global coupling arising from agents’ safety constraints and the exponential growth of the state-action space size limit their applicability in instant communication or computing resource-constrained systems and larger multi-agent systems. In this paper, we develop a novel scalable and theoretically-justified multi-agent constrained policy optimization method. This method utilizes the rigorous bounds of the trust region method and the bounds of the truncated advantage function to provide a new local policy optimization objective for each agent. Also, we prove that the safety constraints and the joint policy improvement can be met when each agent adopts a sequential update scheme to optimize a $\kappa$-hop policy. Then, we propose a practical algorithm called Scalable MAPPO-Lagrangian (Scal-MAPPO-L). The proposed method’s effectiveness is verified on a collection of benchmark tasks, and the results support our theory that decentralized training with local interactions can still improve reward performance and satisfy safe constraints.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

多智能体强化学习（MARL）在真实世界应用（如自动驾驶、无人机群）中面临一个关键挑战：如何在保证安全的前提下，让多个智能体协作完成任务。现有安全 MARL 方法（如 CMIX、MAPPO-L）通常采用集中式训练-分散式执行（CTDE）框架，通过引入全局状态来指导安全协作。然而，这些方法存在两个主要问题：
- **全局耦合**：智能体的安全约束相互耦合，导致全局状态-动作空间随智能体数量指数增长。
- **可扩展性瓶颈**：在通信或计算资源受限的系统以及大规模多智能体系统中，这些方法难以适用。

因此，本文旨在开发一种可扩展的、有理论保证的多智能体约束策略优化方法，使得每个智能体只需依赖局部邻居信息（κ-hop 邻域）进行决策，同时确保联合策略的性能提升和安全性满足。

## 2. 方法论

### 核心思想
利用环境动态和策略的空间相关性衰减性质（spatial correlation decay），将全局安全约束问题分解为每个智能体的局部优化问题。通过截断优势函数（truncated advantage function）估计，使得每个智能体仅需考虑其 κ-hop 邻居的状态和动作，从而大幅减少通信和计算开销。

### 关键技术细节
1. **空间相关性假设**：
   - **Assumption 2.1（动态的空间衰减）**：智能体 i 的转移概率对其他智能体 j 状态/动作的敏感性随距离指数衰减，满足 ∑_j e^{β d(i,j)} W_{ij} ≤ ζ。
   - **Assumption 2.2（策略的空间衰减）**：智能体 i 的策略对远处邻居状态的依赖性也呈指数衰减：sup |π_i(·|s_{N_i^κ}, s_{N_{-i}^κ}) - π_i(·|s_{N_i^κ}, s'_{N_{-i}^κ})| ≤ ξ e^{-βκ}。

2. **优势函数分解与截断**：
   - **Lemma 3.1**（多智能体优势分解）：联合优势函数 A^π(s,a) 可分解为各智能体顺序展开的优势之和：A^π(s,a) = Σ_i A_i^π(s, a_{<i}, a_i)。
   - **Proposition 3.3**（截断优势的误差界）：在假设下，截断优势函数与全局优势函数的差异以 η φ^κ 为界指数衰减。
   - **Corollary 3.4**：代理回报 L_{1:i}^π 与局部截断回报 L_i^{π_i^κ} 的误差也指数衰减。

3. **可扩展约束策略优化**：
   - **Proposition 3.5**：每个智能体顺序求解局部优化问题（式 13），可保证联合策略的期望回报改进下界：J(π̄) - J(π) ≥ Σ_i (L_i^{π_i^κ}(π̂_i^κ) - η'φ^κ - ν_i^κ D_max_KL(π_i^κ||π̂_i^κ))。
   - **Corollary 3.6**：给出了成本期望的上界。
   - **Theorem 3.7**：当每个智能体按式（16）顺序更新策略时，联合策略具有单调改进性，且安全约束均满足。该定理提供了理论保证。

4. **实际算法 Scal-MAPPO-L**：
   - 使用神经网络参数化局部策略 π_i^{θ_i^κ}。
   - 引入拉格朗日乘子 λ_i，将约束优化转化为 min-max 问题（式 17）。
   - 采用 PPO-clip 目标（式 20）简化 KL 约束，仅依赖自身动作和 κ-hop 邻居状态。
   - 算法伪代码见 Appendix C.8（Algorithm 1）。

## 3. 实验设计

### 数据集/场景
使用 Safe MAMuJoCo 基准（安全多智能体 MuJoCo），是 MAMuJoCo 的扩展，包含障碍物（墙壁、陷阱）。具体任务：
- Safe ManyAgent Ant 任务（2×3, 3×2, 6×1）
- Safe Ant 任务（2×4, 4×2, 8×1）
- Safe Coupled HalfCheetah 任务（2×6, 6×2, 12×1）

### benchmark 和方法对比
对比方法：
- **IPPO**：独立 PPO（无集中训练）
- **HAPPO**：多智能体信任域优化（Heterogeneous-Agent Trust Region Policy Optimisation）
- **MAPPO-L**：集中训练的安全 MAPPO（使用全局状态）
- **Scal-MAPPO-L（本文方法）**：仅使用 κ-hop 局部信息

### 实验内容
- 图1：在三个 ManyAgent Ant 任务上对比成本（越低越好）和奖励（越高越好）曲线，κ 设置为约一半智能体的邻域。
- 图2：在不同任务上测试不同 κ 值（1,2,3,5 等）对性能的影响，并与 MAPPO-L 对比。
- 附录 D 还提供了 Safe Ant 和 Safe Coupled HalfCheetah 的额外结果。

## 4. 资源与算力

论文在 Appendix D.2 明确了计算资源：
- GPU：NVIDIA GeForce RTX 4090
- CPU：Intel Core i9-13900K

运行时间示例（10^7 步）：
- Safe Manyagent Ant 6×1：平均 8.43 h
- Safe Ant 8×1：9.28 h
- Safe Coupled HalfCheetah 12×1：11.65 h

未提及使用的 GPU 数量（推测单卡），也未说明是否采用了并行训练。算力描述较为简洁。

## 5. 实验数量与充分性

### 实验数量
- 主要对比实验（图1）：3 种任务 × 4 种算法 = 12 条学习曲线。
- κ 敏感性实验（图2）：3 种任务 × 每个任务 4~5 个 κ 值 + MAPPO-L 基线 = 每组约 5-6 条曲线。
- 附录额外实验（图3-4）：6 种任务（Safe Ant 和 HalfCheetah variants），对比 HAPPO、MAPPO-L 和 Scal-MAPPO-L。
- 所有结果均采用 3 个以上随机种子平均，曲线平滑处理。

### 充分性评价
- **优点**：涵盖了不同任务规模（2~12 智能体）、不同机器人类型（Ant、HalfCheetah），并系统研究了 κ 参数影响。对比方法全面（独立学习、集中训练、安全 MARL）。
- **不足**：未提供与最新其他安全 MARL 方法（如 CMIX、Safe Dec-PG）的直接对比；仅使用 Safe MAMuJoCo 单一基准，缺乏 real-world 或更复杂环境（如自动驾驶模拟器）验证。消融实验只对 κ 进行，未对拉格朗日乘子更新、网络结构等进行消融。
- **公平性**：作者说明为公平比较，所有算法的网络架构和超参数（除 κ 外）与 MAPPO-L 保持一致。但 Scal-MAPPO-L 实际执行的近似（如 PPO-clip）可能使其理论保证不完全成立，论文在 3.3 末承认了这一点。

整体上实验设计合理，但覆盖面有限，客观性较好。

## 6. 主要结论与发现

1. **有效性与可扩展性**：Scal-MAPPO-L 仅需局部 κ-hop 信息，在多数任务上能达到与 MAPPO-L（使用全局状态）相近甚至更好的奖励和约束满足性能，验证了空间相关性衰减假设在实际问题中的有效性。
2. **κ 的影响**：当 κ 较小时（κ=1）性能最差，但随着 κ 增大（κ≥3），性能迅速提升，在某些场景下（如 Ant 8×1 中 κ=6）甚至超越 MAPPO-L，因为全局状态可能包含冗余噪声。
3. **理论支持**：提出的局部优化目标（式 16）在理论上保证了联合策略的单调改进和安全约束的满足，实验与之吻合。

## 7. 优点

- **理论深厚**：严格推导了截断优势函数的误差界、联合回报改进下界和安全约束上界，证明了顺序更新下的单调性和安全性保证。
- **方法新颖**：将空间相关性衰减性质与信任域方法有机结合，首次在安全 MARL 中实现理论上可扩展的分散式策略优化。
- **实践有效**：在多个基准任务上验证了方法，虽然使用近似（PPO-clip），但仍保持了良好的性能。
- **可解释性强**：κ 参数直观控制通信半径，便于在资源受限场景下权衡性能与开销。
- **开源代码**：提供了伪代码和补充材料，便于复现。

## 8. 不足与局限

- **假设依赖**：核心结果依赖动态和策略的空间相关性衰减假设（Assumption 2.1 & 2.2），在强耦合、非局部交互的环境中（如所有智能体必须全局协调），该方法可能失效。论文承认了这一点。
- **实验基准单一**：仅使用 Safe MAMuJoCo，未在真实机器人或更复杂模拟器（如 SUMO、SMARTS）上测试，泛化性有待验证。
- **理论与实现之间有差距**：实际算法中使用了 PPO-clip 和拉格朗日方法近似，可能违背严格的理论保证（论文明确指出了这一点）。
- **κ 选择缺乏自适应机制**：κ 是固定超参数，如何自动确定最优 κ 未讨论。
- **计算效率分析不充分**：虽然声称减少通信，但实际训练时间并未因 κ 减小而显著下降（论文解释为未考虑真实传递开销），需进一步优化。
- **未比较更多基线**：缺少与 Safe Dec-PG、CMIX 等方法的对比，说服力略有不足。

（完）
