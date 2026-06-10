---
title: "Lyapunov-stable Neural Control for State and Output Feedback: A Novel Formulation"
title_zh: 状态和输出反馈的李雅普诺夫稳定神经网络控制：一种新公式
authors: "Lujie Yang, Hongkai Dai, Zhouxing Shi, Cho-Jui Hsieh, Russ Tedrake, Huan Zhang"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=3xPMW9JURD"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 李雅普诺夫稳定神经网络控制
tldr: 针对神经网络控制器缺乏形式化稳定性保证的问题，提出一种结合经验反证和正则化的学习框架。该方法同时学习控制器和李雅普诺夫函数，通过快速反证和策略正则化扩大可验证吸引域。在非线性动力系统上验证了方法的有效性，为神经网络控制提供了一种可扩展的稳定性认证途径。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-3xpmw9jurd/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 854, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-3xpmw9jurd/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 689, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-3xpmw9jurd/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 554, \"height\": 343, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-3xpmw9jurd/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 855, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-3xpmw9jurd/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 844, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-3xpmw9jurd/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 762, \"height\": 696, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-3xpmw9jurd/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 763, \"height\": 655, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-3xpmw9jurd/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 856, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-3xpmw9jurd/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1702, \"height\": 388, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-3xpmw9jurd/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 652, \"height\": 363, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-3xpmw9jurd/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 764, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-3xpmw9jurd/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 857, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-3xpmw9jurd/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1765, \"height\": 325, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-3xpmw9jurd/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 697, \"height\": 279, \"label\": \"Table\"}]"
motivation: 学习型神经网络控制器难以获得形式化李雅普诺夫稳定性保证，现有方法依赖昂贵求解器。
method: 提出新框架，通过快速经验反证和策略正则化同时学习控制器和李雅普诺夫函数。
result: 获得比现有方法更大的可验证吸引域，且计算开销低。
conclusion: 为神经网络控制提供了可扩展的稳定性认证方法。
---

## Abstract
Learning-based neural-network (NN) control policies have shown impressive empirical performance in a wide range of tasks in robotics and control. However, formal (Lyapunov) stability guarantees over the region-of-attraction (ROA) for NN controllers with nonlinear dynamical systems are challenging to obtain, and most existing approaches rely on expensive solvers for sums-of-squares (SOS), mixed-integer programming (MIP), or satisfiability modulo theories (SMT). In this paper, we demonstrate a new framework for learning NN controllers together with Lyapunov certificates using fast empirical falsification and strategic regularizations. We propose a novel formulation that defines a larger verifiable region-of-attraction (ROA) than shown in the literature, and refines the conventional restrictive constraints on Lyapunov derivatives to focus only on certifiable ROAs. The Lyapunov condition is rigorously verified post-hoc using branch-and-bound with scalable linear bound propagation-based NN verification techniques. The approach is efficient and flexible, and the full training and verification procedure is accelerated on GPUs without relying on expensive solvers for SOS, MIP, nor SMT. The flexibility and efficiency of our framework allow us to demonstrate Lyapunov-stable output feedback control with synthesized NN-based controllers and NN-based observers with formal stability guarantees, for the first time in literature.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：基于学习的神经网络（NN）控制器在机器人控制中表现优异，但缺乏形式化的李雅普诺夫稳定性保证，尤其是在非线性动力系统中。现有的获得形式化保证的方法（如SOS、MIP、SMT）计算代价高昂，难以扩展到复杂控制器和输出反馈场景。
- **整体含义**：论文旨在提出一种高效、可扩展的框架，能够同时学习神经网络控制器、观测器（输出反馈下）和李雅普诺夫函数，并事后用严格的验证工具（α,β-CROWN）给出形式化稳定性保证，首次实现了输出反馈控制下的神经网络李雅普诺夫稳定控制的形式化认证。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
### 核心思想
- 利用**快速经验反证（PGD攻击）** 代替昂贵的求解器来指导训练，仅在训练后使用一次昂贵的验证器（α,β-CROWN）进行严格验证。
- 引入**新公式**：定义可验证吸引域（ROA）为**“感兴趣区域B”与李雅普诺夫函数子水平集V(ξ) < ρ的交集**，显式保证该集合的不变性，并放松了传统方法在整个B上强制李雅普诺夫导数约束的苛刻条件。
- 提出**新的可验证条件**（Theorem 3.3）：将原定义在隐式集合S上的导数条件转化为显式域B上的条件：
  `(−F(ξ_t) ≥ 0 ∧ ξ_{t+1} ∈ B) ∨ (V(ξ_t) ≥ ρ), ∀ξ_t ∈ B`，
  其中`F(ξ_t)=V(f_cl(ξ_t))-(1-κ)V(ξ_t)`，ρ为子水平集阈值。

### 关键技术细节
- **参数化**：控制器π、观测器φ_obs和李雅普诺夫函数V均可用神经网络参数化；也可使用二次型李雅普诺夫函数（通过可学习矩阵R保证正定性）。
- **训练框架**：采用CEGIS（反例引导归纳合成）框架，但反例由**PGD攻击**生成（最大化损失`L̇V`），而非昂贵的SMT/MIP求解器。损失函数包含：
  - `L̇V`：导数条件与集不变性违背；
  - `L_roa`：覆盖候选状态的代理损失；
  - `L1正则化`：降低Lipschitz常数；
  - `L_obs`（输出反馈）：观测器预测误差。
- **验证**：使用α,β-CROWN（一种基于线性界传播的分支定界验证器）事后验证条件（14），并通过二分搜索寻找最大可验证ρ。

### 算法流程（文字说明）
1. 初始化参数θ（控制器、观测器、李雅普诺夫函数）。
2. 循环迭代：
   - 在边界∂B上取样点，通过PGD最小化V以更新ρ（ρ = γ · min V(∂B)）。
   - 在B内取样点，通过PGD最大化L̇V生成反例，加入数据集D。
   - 在D上优化整体损失函数L(θ; D, ρ)更新θ。
3. 训练后，使用α,β-CROWN验证条件（14），通过二分搜索求最大ρ_max。

## 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法
- **场景/系统**：
  - **状态反馈**：倒立摆、路径跟踪、2D四旋翼、小车-杆系统（Cartpole）、PVTOL（平面垂直起降飞行器）。
  - **输出反馈**：倒立摆（仅角度观测）、2D四旋翼（6束截断激光雷达观测）。
- **基准方法**：
  - DITL（Wu et al., 2023）：使用MIP进行验证和反例生成。
  - NLC（Chang et al., 2019）：使用SMT求解器。
  - UNL（Zhou et al., 2022）：针对未知系统的神经李雅普诺夫控制。
- **对比指标**：可验证ROA大小（2D切片可视化）、验证运行时间、训练收敛性。

## 4. 资源与算力
- 论文明确提到**全部训练和验证过程在GPU上加速**，利用了PGD在GPU上的高效计算。
- 具体GPU型号、数量、训练时长**未明确给出**。验证运行时在正文表1和表2中有记录（例如倒立摆状态反馈验证11.3s，四旋翼输出反馈8.9小时），但未说明硬件规格。

## 5. 实验数量与充分性：大概做了多少组实验，是否充分、客观、公平
- **实验组数**：
  - 验证对比：在4个状态反馈系统（倒立摆、路径跟踪、Cartpole、PVTOL）上比较了验证运行时和ROA大小。
  - 训练对比：在倒立摆和路径跟踪上与DITL、NLC、UNL对比ROA（图5）。
  - 新训练模型：在倒立摆、路径跟踪、2D四旋翼（状态反馈）上展示了ROA；在输出反馈下展示了两个系统（倒立摆、四旋翼）。
  - 消融实验：没有显式的消融实验，但通过对比传统公式（13）与新公式（14/16b）说明了新公式的优势。
- **充分性**：实验覆盖了多个常见非线性系统，维度从2到8，包含状态反馈和输出反馈。与SOTA方法进行了公平对比（使用相同的动力学和区域B），并指出了DITL在PVTOL上的实现错误（附录B.6）。整体实验设计较充分，但缺少对更高维系统（如>10维）的验证。

## 6. 论文的主要结论与发现
- 提出的**新公式**（将ROA定义为B与子水平集的交集）比传统方法（在整个B上强制导数条件）得到**更大可验证ROA**，且更容易训练和验证。
- **仅使用PGD反例进行训练**即可获得可验证的控制器，无需昂贵的求解器，训练后仅用α,β-CROWN一次性验证。
- **首次实现**输出反馈下带形式化稳定性保证的神经网络控制器和观测器（倒立摆和2D四旋翼）。
- 验证器α,β-CROWN比MIP求解器在更复杂系统（如Cartpole、PVTOL）上**快几倍到几十倍**，且支持GPU并行。

## 7. 优点：方法或实验设计上的亮点
- **效率**：用低成本PGD反例代替昂贵求解器进行训练，大幅降低训练开销；验证仅需一次，且α,β-CROWN可高效利用GPU。
- **灵活性**：支持状态反馈和输出反馈；支持二次型或神经网络李雅普诺夫函数；支持任意连续动力学（包括三角函数等非线性，通过α,β-CROWN支持）。
- **新颖公式**：通过放宽不必要约束，扩大可验证ROA；引入H(ξ_{t+1})确保不变性，使训练和验证一致。
- **可解释性**：给出正式的李雅普诺夫证书和可验证的ROA边界。
- **完整性**：开源代码和详细的附录（网络结构、区域参数等），便于复现。

## 8. 不足与局限
- **维度限制**：虽然扩展到8维（输出反馈），但更高维系统（如带图像观测的机器人）仍未解决，论文明确指出这是未来方向。
- **观测函数限制**：仅处理了截断型激光雷达等较简单的观测函数，图像/点云等复杂观测未涉及。
- **训练依赖PGD**：PGD可能无法找到所有关键反例，导致训练后验证失败，但论文通过增大PGD步数和随机采样缓解。
- **缺乏消融实验**：未系统分析各损失项（L1正则化、L_obs等）的贡献。
- **硬件未明确**：无法评估算力需求是否普遍可接受。
- **输出反馈仅考虑初始状态不确定性**：未处理过程噪声或模型误差，实际应用有限。

（完）
