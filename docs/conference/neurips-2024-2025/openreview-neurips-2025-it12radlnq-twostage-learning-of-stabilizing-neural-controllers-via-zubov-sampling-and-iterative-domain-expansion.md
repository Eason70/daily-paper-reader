---
title: Two‑Stage Learning of Stabilizing Neural Controllers via Zubov Sampling and Iterative Domain Expansion
title_zh: 基于Zubov采样和迭代域扩展的两阶段稳定神经网络控制器学习
authors: "Haoyu Li, Xiangru Zhong, Bin Hu, Huan Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=IT12Radlnq"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 使用Lyapunov函数保证稳定性的神经网络控制
tldr: "该论文针对神经网络控制器稳定性保证问题，提出两阶段训练框架联合综合控制器和Lyapunov函数。利用Zubov吸引域特征直接估计稳定边界，并通过迭代域扩展减小保守性。方法在连续时间系统上成功获得更大吸引域估计。该工作与需求中的'神经网络'直接相关，且其稳定性方法可辅助安全控制，但未涉及安全强化学习或控制屏障函数。"
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-it12radlnq/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 600, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-it12radlnq/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1431, \"height\": 500, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-it12radlnq/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1436, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-it12radlnq/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1429, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-it12radlnq/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1429, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-it12radlnq/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1435, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-it12radlnq/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1450, \"height\": 1960, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-it12radlnq/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1454, \"height\": 981, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-it12radlnq/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1452, \"height\": 372, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-it12radlnq/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1451, \"height\": 151, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-it12radlnq/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1314, \"height\": 407, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-it12radlnq/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1451, \"height\": 491, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-it12radlnq/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1170, \"height\": 384, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-it12radlnq/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1084, \"height\": 381, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-it12radlnq/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1172, \"height\": 410, \"label\": \"Table\"}]"
motivation: 现有学习型神经网络控制器难以获得稳定性保证和吸引域估计，且框架保守性大。
method: 提出两阶段训练：第一阶段基于Zubov采样估计吸引域边界，第二阶段迭代扩展域并联合优化控制器和Lyapunov函数。
result: 在多个连续时间系统上，方法合成的不稳定控制器具有更大的吸引域估计，且验证了稳定性。
conclusion: 该框架为神经网络控制提供了可扩展的稳定性保证，可与CBF等方法互补用于安全控制。
---

## Abstract
Learning-based neural network (NN) control policies have shown impressive empirical performance. However, obtaining stability guarantees and estimates of the region of attraction of these learned neural controllers is challenging due to the lack of stable and scalable training and verification algorithms. Although previous works in this area have achieved great success, much conservatism remains in their frameworks. In this work, we propose a novel two-stage training framework to jointly synthesize a controller and a Lyapunov function for continuous-time systems. By leveraging a Zubov‑inspired region of attraction characterization to directly estimate stability boundaries, we propose a novel training-data sampling strategy and a domain-updating mechanism that significantly reduces the conservatism in training. Moreover, unlike existing works on continuous-time systems that rely on an SMT solver to formally verify the Lyapunov condition, we extend state-of-the-art neural network verifier $\alpha,\beta$-CROWN with the capability of performing automatic bound propagation through the Jacobian of dynamical systems and a novel verification scheme that avoids expensive bisection. To demonstrate the effectiveness of our approach, we conduct numerical experiments by synthesizing and verifying controllers on several challenging nonlinear systems across multiple dimensions. We show that our training can yield region of attractions with volume $5 - 1.5\cdot 10^{5}$ times larger compared to the baselines, and our verification on continuous systems can be up to $40-10{,}000$ times faster compared to the traditional SMT solver dReal. Our code is available at https://github.com/Verified-Intelligence/Two-Stage_Neural_Controller_Training.

---

## 论文详细总结（自动生成）

# 论文总结：Two‑Stage Learning of Stabilizing Neural Controllers via Zubov Sampling and Iterative Domain Expansion

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：学习型神经网络控制器在复杂系统中表现优异，但缺乏稳定性保证，尤其在安全关键应用中。现有方法难以获得可扩展的稳定性训练和验证算法，且普遍存在保守性问题。
- **背景**：传统方法（如SOS技术）限于线性或多项式系统；数据驱动方法（如CEGIS）依赖良好的初始化，且训练域和数据采样策略导致吸引域（ROA）估计偏小。本文旨在为连续时间系统联合合成神经网络控制器及其Lyapunov函数，最大化可验证的ROA。

## 2. 方法论：核心思想、关键技术细节、公式/算法流程

### 核心思想
- **两阶段训练**：第一阶段（ROA估计阶段）利用Zubov定理的吸引域表征，通过新颖的数据采样和动态域扩展机制获得工作良好的控制器和Lyapunov函数；第二阶段（CEGIS精炼阶段）通过反例引导学习消除Lyapunov条件违规，获得可验证的证书。
- **基于Zubov的采样**：混合从当前ROA内部和边界附近采样，解决高维空间中ROA占比极小导致的样本不平衡。
- **动态训练域扩展**：从初始小域开始，利用收敛轨迹扩展示训练域，消除固定域引入的保守性。
- **验证方面**：扩展α,β-CROWN以处理连续时间系统Jacobian相关算子（如Tanh、Sigmoid的导数），并设计自适应验证方案避免二分法搜索c1、c2。

### 关键技术细节
1. **参数化**：控制器 \(u_\theta(x) = c \cdot \tanh(NN_c(x) - NN_c(x^*) + \tanh^{-1}(u^*/c))\) 保证平衡点；Lyapunov函数 \(V_\theta(x) = \text{sigmoid}(NN_v(x))\) 确保值在[0,1]。
2. **Zubov引导采样**：使用投影梯度下降（PGD）分别从V≤c（内部）和V接近1（外部）采样，损失函数分别为 \(L_{\text{interior}} = \text{ReLU}(V_\theta(x)-c)\) 和 \(L_{\text{outside}} = |V_\theta(x)-1|\)。
3. **动态域扩展**：定期从当前ROA内采样初始点，模拟轨迹，将域扩展至收敛轨迹可达的最远点，并均匀放大以处理单调收敛。
4. **损失函数**：包括零损失（\(L_{\text{zero}}\)）、PDE残差损失（\(L_{\text{pde}}\)）、数据损失（基于Bellman型重写，仅需短时模拟）、控制器损失（\(L_{\text{controller}}\)）、边界损失（\(L_{\text{boundary}}\)）。
5. **CEGIS精炼**：使用PGD寻找违规反例，损失为\(L_{\text{cegis}} = \text{ReLU}(\nabla V_\theta(x_{\text{cex}}) f(x_{\text{cex}}))\)，并加入正则化项稳定水平集。
6. **验证方案**：提出定理3.1，在带域中验证Lyapunov条件及边界逃逸条件；扩展α,β-CROWN处理Jacobian算子，自适应更新c1、c2避免二分法。

### 算法流程（文字描述）
- **第一阶段（ROA估计）**：初始化小域Ω，每γ步执行域更新（算法2）。采样N个数据点（来自内部和外部），N个边界点，计算总损失并更新参数θ。循环至M1次。
- **第二阶段（CEGIS）**：从Ω采样P个点，进行P步PGD攻击获得反例，存入有限缓冲区。对缓冲区数据，交替进行K轮CEGIS精炼和正则化。若连续n步无反例则终止。

## 3. 实验设计

### 数据集/场景
- 连续时间非线性系统，包括2D系统（Van-der-Pol, Double-Integrator, Inverted Pendulum, Path Tracking）、4D系统（Cartpole）、6D系统（PVTOL, 2D Quadrotor, Ducted Fan）、12D系统（3D Quadrotor）。部分系统设大/小扭矩两种设置。
- Benchmark场景：遵循先前工作DITL、Yang et al.、Shi et al.的设置。

### 对比方法
- Fossil 2.0（连续时间方法，仅部分系统可比）、DITL（离散时间）、Yang et al.（离散时间）、Shi et al.（离散时间）。文中说明因现有连续时间方法在平衡点处理上有问题，因此主要对比离散时间基线。

### 评估方案
- 三种评估等级：形式验证（α,β-CROWN）、PGD攻击评估、轨迹评估（随机轨迹收敛性）。随着维度增加，依赖更经验的评估。

## 4. 资源与算力

- **训练**：使用NVIDIA V100 GPU，16GB内存。训练时间在附录C.7给出：2D系统约15-30分钟，4D系统约2小时，6D系统约3-5小时，12D系统约1.3小时（仅第一阶段，CEGIS未完成）。
- **验证**：使用NVIDIA 5090 GPU，32GB内存。验证时间：2D系统α,β-CROWN约3-4秒，dReal约100-40000秒；Cartpole约76443秒；2D Quadrotor约104614秒。
- 未明确说明使用的GPU数量，推测单卡。

## 5. 实验数量与充分性

- **实验数量**：每个方法在每种系统上以5个不同随机种子运行。共涉及12种系统（含扭矩设置），对比4种基线方法。
- **消融实验**：在Cartpole和2D Quadrotor上进行了三种训练方案对比：1）两阶段+随机采样；2）仅第一阶段；3）仅CEGIS。结果显示仅完整管道能在形式验证或强PGD攻击下成功。
- **充分性**：实验覆盖了从2D到12D的多种非线性系统，结果以均值和标准差报告，成功率列于表中。对比方法也运行5次。实验设计较全面，但基线方法均为离散时间，且仅部分系统可比，可能存在公平性偏差。验证时间对比仅列了几种系统的示例。

## 6. 主要结论与发现

- **ROA体积提升**：相比于现有基线，本文方法在2D系统上获得5倍~1500倍更大的ROA（例如倒立摆大扭矩：2946 vs 487）；在4D Cartpole上获得330倍以上；在6D系统上获得高达1.5×10^5倍（2D Quadrotor）。
- **成功率**：在所有2D和4D系统上，本文方法均100%成功（部分基线仅有20%-80%）。在高维6D和12D系统中，本文是唯一能给出可行ROA估计的方法。
- **验证速度**：在可形式验证的系统中，α,β-CROWN比dReal快40~10,000倍。
- **消融结果**：单独的第一阶段ROA估计已能通过轨迹评估，但需要CEGIS才能通过形式验证或强PGD评估。

## 7. 优点

- **新颖的训练策略**：结合Zubov定理的物理信息损失和动态域扩展，有效减少保守性，且无需精细调整初始域。
- **数据采样机制**：通过PGD从当前ROA内部和边界附近采样，解决了高维空间中样本不平衡问题。
- **验证扩展**：首次将α,β-CROWN扩展到连续时间系统Jacobian相关算子，设计了更紧的线性松弛，并提出避免二分法的自适应验证方案。
- **经验性能突出**：在多种维度系统上均显著优于现有基线，ROA体积提升2~5个数量级。

## 8. 不足与局限

- **形式验证可扩展性**：尽管验证速度快于dReal，但高维系统（6D以上）仍难以完成完整形式验证，仅能依赖经验评估（PGD或轨迹）。
- **基线对比公平性**：主要对比的是离散时间方法，连续时间基线因处理不当被排除，可能导致评价不够全面。
- **对系统类型的限制**：仅适用于连续时间系统，且需要平衡点已知、控制输入满足特定形式。
- **训练参数敏感**：超参数（如损失权重、c的选择）仍需一定手动调整，在更高维系统上可能需要更多调优。
- **理论保证有限**：虽然Lyapunov函数形式化保证可在低维系统上验证，但高维系统只能提供经验性收敛保证，缺乏严格安全性证明。

（完）
