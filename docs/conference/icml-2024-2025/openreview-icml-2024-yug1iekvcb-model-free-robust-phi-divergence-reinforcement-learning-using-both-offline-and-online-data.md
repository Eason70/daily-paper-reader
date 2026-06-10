---
title: Model-Free Robust $\phi$-Divergence Reinforcement Learning Using Both Offline and Online Data
title_zh: 利用离线和在线数据的无模型鲁棒phi-散度强化学习
authors: "Kishan Panaganti, Adam Wierman, Eric Mazumdar"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=Yug1IEkvcb"
tags: ["query:safe-rl-cbf"]
score: 4.0
evidence: 无模型鲁棒强化学习
tldr: 该论文提出基于phi-散度的无模型鲁棒强化学习算法，利用离线和在线数据学习鲁棒策略，有效应对模型参数不确定性，在安全控制领域具有潜力，但未直接结合控制屏障函数。
source: ICML-2024-Public
selection_source: conference_retrieval
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-yug1iekvcb/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1746, \"height\": 407, \"label\": \"Table\"}]"
motivation: 解决模拟器与真实环境参数不匹配导致的策略不鲁棒问题。
method: 提出鲁棒phi-正则化拟合Q迭代算法。
result: 在理论证明下首次实现高维系统的鲁棒最优策略。
conclusion: 为鲁棒RL提供统一分析框架。
---

## Abstract
The robust $\phi$-regularized Markov Decision Process (RRMDP) framework focuses on designing control policies that are robust against parameter uncertainties due to mismatches between the simulator (nominal) model and real-world settings. This work makes *two* important contributions. First, we propose a *model-free* algorithm called *Robust $\phi$-regularized fitted Q-iteration* for learning an $\epsilon$-optimal robust policy that uses only the historical data collected by rolling out a behavior policy (with *robust exploratory* requirement) on the nominal model. To the best of our knowledge, we provide the *first* unified analysis for a class of $\phi$-divergences achieving robust optimal policies in high-dimensional systems of arbitrary large state space with general function approximation. Second, we introduce the *hybrid robust $\phi$-regularized reinforcement learning* framework to learn an optimal robust policy using both historical data and online sampling. Towards this framework, we propose a model-free algorithm called *Hybrid robust Total-variation-regularized Q-iteration*. To the best of our knowledge, we provide the *first* improved out-of-data-distribution assumption in large-scale problems of arbitrary large state space with general function approximation under the hybrid robust $\phi$-regularized reinforcement learning framework.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：实际强化学习训练环境（模拟器/标称模型）与真实部署环境之间存在参数不匹配，导致学习到的策略在真实环境中性能显著下降甚至失败。现有在线、离线、混合RL方法都无法从根本上解决模型失配问题。
- **整体背景**：鲁棒马尔可夫决策过程（RMDP）框架通过考虑一组围绕标称模型的可能转移概率（不确定性集合）来设计在集合内表现均匀良好的鲁棒策略。但已有模型无关算法多局限于特定散度（如TV、KL）或有限状态动作空间，缺乏对一般$\phi$-散度的统一处理；同时离线鲁棒RL面临数据分布外（OOD）问题，而混合RL（同时利用离线和在线数据）在鲁棒场景下尚未被充分探索。
- **核心问题**：如何在任意大状态空间、使用一般函数逼近的条件下，设计模型无关的鲁棒RL算法，实现对一大类$\phi$-散度的统一分析，并利用混合学习缓解离线鲁棒RL的OOD问题。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

### 2.1 RRMDP框架与对偶形式

- 论文基于鲁棒$\phi$-正则化MDP（RRMDP）框架，该框架等价于带惩罚项的RMDP（用$\lambda$控制鲁棒性强度）。
- 核心思想：将原始鲁棒贝尔曼算子中的内层最小化问题（在不确定性集合中搜索最坏情况转移概率）通过Fenchel对偶转化为仅依赖于标称模型期望的形式（Proposition 1），从而避免了对每个状态-动作对单独求解内部优化，使得利用单一离线数据集成为可能。
- 进一步，通过对偶变量函数$g(s,a)$的引入，将点态最小化转化为函数空间的最小化（Proposition 2），便于使用函数逼近。

### 2.2 RPQ算法（离线鲁棒$\phi$-正则化拟合Q迭代）

- **输入**：离线数据集$D_{P_o}$（标称模型下的i.i.d.数据）、函数类$F$（Q值函数）和$G$（对偶变量函数）。
- **迭代过程**（以文字说明）：
  1. 初始化$Q_0\equiv 0$。
  2. 对于$k=0,\dots,K-1$：
     - **对偶变量函数最小化**：$g_k = \arg\min_{g\in G} \hat{L}_{\text{dual}}(g; Q_k)$，其中$\hat{L}_{\text{dual}}$是基于数据的经验对偶损失（包含$\phi^*$）。
     - **鲁棒Q更新**：$Q_{k+1} = \arg\min_{Q\in F} \hat{L}_{\text{robQ}}(Q; Q_k, g_k)$，其中$\hat{L}_{\text{robQ}}$是经验平方鲁棒贝尔曼误差。
  3. 输出：贪婪策略$\pi_K(s)=\arg\max_a Q_K(s,a)$。
- **关键技术**：利用两个函数类分别表示Q值和对偶变量，通过经验风险最小化和最小二乘回归进行两步更新，避免了求解每个状态-动作的内层优化。

### 2.3 HyTQ算法（混合鲁棒TV-正则化Q迭代）

- **输入**：离线数据集$D^\mu_h$（每个时间步$h$有$m_{\text{off}}$个样本）、在线交互能力（每轮收集$m_{\text{on}}$个样本）、函数类$F_h$和$G_h$（总变差TV散度）。
- **迭代过程**（以文字说明）：
  1. 初始化$Q^0_h\equiv 0$。
  2. 对于$k=0,\dots,K-1$：
     - 计算贪婪策略$\pi^k$。
     - 收集在线数据集$D^k_h\sim d^{\pi^k}_{h,P_o}$（每个时间步$h$）。
     - 聚合自适应数据集$D^k_h = D^\mu_h \cup \bigcup_{\tau=0}^{k} D^\tau_h$。
     - 从$h=H-1$到$0$进行反向迭代：
       - **对偶变量函数最小化**（TV散度下有简化形式）：$g^{k+1}_h = \arg\min_{g\in G_h} \hat{L}_{\text{dual}}(g; Q^{k+1}_{h+1}, D^k_h)$。
       - **鲁棒Q更新**：$Q^{k+1}_h = \arg\min_{Q\in F_h} \hat{L}_{\text{robQ}}(Q; Q^{k+1}_{h+1}, g^{k+1}_h, D^k_h)$。
- **关键技术**：利用在线数据改善离线数据分布覆盖假设，从全策略覆盖（all-policy）降低到单策略覆盖（single-policy via transfer coefficient）；利用双线性模型（bilinear models）进行在线部分的分析，获得改进的样本复杂度。

## 3. 实验设计

- **实验设置**：论文**不包含任何实验**。全部内容为理论分析与证明。
- **Benchmark与对比方法**：在理论层面与已有工作进行了对比，包括Panaganti et al. (2022, TV散度), Zhang et al. (2024, KL散度), Yang et al. (2023, 卡方散度)等，对比项包括：算法类型、数据覆盖要求、数据集类型、次优性界等（参见论文Table 1）。
- **评估指标**：理论上给出$\epsilon$-最优策略的次优性界（suboptimality）和样本复杂度。

## 4. 资源与算力

- **未提及**：论文为纯理论工作，没有进行任何实际训练或仿真实验，因此未涉及任何GPU型号、数量、训练时长等算力信息。

## 5. 实验数量与充分性

- **实验数量**：无。
- **充分性评价**：作为理论论文，其贡献在于提出新算法并提供严格的理论证明（包括定理、引理、推论），而非实验验证。因此，不适用实验充分性的评判标准。理论贡献本身是充分的：给出了次优性界、样本复杂度、以及统一的$\phi$-散度分析。

## 6. 论文的主要结论与发现

1. **离线鲁棒RL方面**：提出RPQ算法，首次对一类$\phi$-散度（包括TV、KL、卡方、CVaR等）提供了统一的次优性界和样本复杂度分析（Theorem 1）。次优性为$\tilde{O}\left(\frac{\sqrt{C}\log(|\mathcal{F}||\mathcal{G}|)}{(1-\gamma)^3\sqrt{N}}\right)$（忽略近似误差和常数因子）。
2. **混合鲁棒RL方面**：提出HyTQ算法（针对TV散度），首次在鲁棒RL中使用离线和在线数据，将数据覆盖假设从全策略覆盖改进为仅需覆盖最优鲁棒策略（通过鲁棒贝尔曼误差传递系数$C(\pi^*)$），累积次优性界为$\tilde{O}\left(\max\{C(\pi^*),1\}\sqrt{d}H^2(\lambda+H)\sqrt{K\log(|\mathcal{F}||\mathcal{G}|/\delta)}\right)$。
3. **理论贡献**：统一了$\phi$-散度鲁棒RL的分析，为混合鲁棒RL提供了首个改进数据分布假设的分析。

## 7. 优点

- **理论深度与统一性**：首次对一大类$\phi$-散度进行统一分析，涵盖常见散度（TV、KL、卡方、CVaR），避免了针对每种散度的独立推导。
- **模型无关性**：算法不需要显式估计标称模型，仅使用离线数据（或离线和在线数据），适用于高维、大状态空间，配合一般函数近似（神经网络、核函数等）。
- **改进的数据假设**：HyTQ算法通过在线交互将覆盖条件从“所有策略的全覆盖”降低到“最优策略的单覆盖”，极大放宽了离线鲁棒RL的假设。
- **计算可行性**：两步更新（经验风险最小化+最小二乘回归）避免了求解每个状态-动作的内部优化，便于扩展到高维问题。
- **与现有理论对比**：在TV散度下取得了与专门算法Panaganti et al. (2022)相同的次优性界；在KL散度下与Zhang et al. (2024)相当；在卡方散度下优于Yang et al. (2023)中的随机近似方法（后者仅得到$N^{-1/3}$率，且依赖于表格设置）。

## 8. 不足与局限

- **缺乏实验验证**：纯理论论文，没有在标准基准环境（如MuJoCo、Atari等）中进行仿真实验，因此读者无法直观评估算法在实际问题中的表现、收敛速度和数值稳定性。
- **强假设依赖**：离线RPQ算法依赖全策略覆盖假设（Assumption 1）和近似鲁棒贝尔曼完备性（Assumption 2），这些假设在实际高维系统中可能难以满足。混合HyTQ算法依赖双线性模型假设（Assumption 7）和故障状态假设（Assumption 8），同样较为严格。
- **仅TV散度实现了混合算法**：混合鲁棒RL框架仅针对TV散度给出了具体算法和分析（HyTQ），对一般$\phi$-散度（如KL、卡方）的混合算法尚未解决，作者指出因缺乏双线性结构而存在分析困难。
- **常数的未知性**：理论界中的常数（如$c_\phi(\lambda,\gamma)$）依赖于具体散度，虽然给出了不同散度下的具体表达式（Proposition 3），但这些常数可能很大（如KL散度下指数依赖$1/(\lambda(1-\gamma))$）。
- **多轮在线数据消耗**：HyTQ算法每轮迭代都需采集$H$步在线数据，总样本数与迭代次数$K$和$H$有关，实际中可能需要较多在线交互才能达到理论保证。
- **未考虑奖励不确定性**：论文仅关注转移概率的不确定性，假设奖励函数已知且确定，但实际场景中奖励也可能有不确定性。

（完）
