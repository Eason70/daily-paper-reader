---
title: Robust Inverse Constrained Reinforcement Learning under Model Misspecification
title_zh: 模型误设下的鲁棒逆约束强化学习
authors: "Sheng Xu, Guiliang Liu"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=pkUl39b0in"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 用于安全关键决策的鲁棒逆约束强化学习
tldr: 逆约束强化学习从专家演示中推断约束，但忽略训练与部署环境差异会导致不安全动作。AR-ICRL通过将动力学偏差建模为对手策略，学习鲁棒策略，并在模型失配下保持约束可靠性，从而提升安全关键决策的鲁棒性。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-pkul39b0in/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 854, \"height\": 324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-pkul39b0in/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 831, \"height\": 578, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-pkul39b0in/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 815, \"height\": 523, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-pkul39b0in/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 781, \"height\": 282, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-pkul39b0in/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 696, \"height\": 384, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-pkul39b0in/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1028, \"height\": 349, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-pkul39b0in/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1025, \"height\": 942, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-pkul39b0in/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 768, \"height\": 880, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-pkul39b0in/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 796, \"height\": 915, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2024-pkul39b0in/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 809, \"height\": 944, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-pkul39b0in/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1774, \"height\": 584, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-pkul39b0in/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1754, \"height\": 718, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-pkul39b0in/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1066, \"height\": 1067, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-pkul39b0in/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1062, \"height\": 741, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-pkul39b0in/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1766, \"height\": 592, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-pkul39b0in/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1767, \"height\": 567, \"label\": \"Table\"}]"
motivation: 训练与部署环境差异严重损害推断约束的可靠性，导致不安全行为。
method: 提出自适应鲁棒逆约束RL，将动力学误设建模为对手策略，学习鲁棒策略。
result: 在模型失配环境中显著降低了约束违反，并保持了较高的任务性能。
conclusion: AR-ICRL提高了逆约束RL在实际部署中的安全鲁棒性。
---

## Abstract
To solve safety-critical decision-making problems, Inverse Constrained Reinforcement Learning (ICRL) infers constraints from expert demonstrations and seeks to imitate expert preference by utilizing these constraints. While prior ICRL research commonly overlooks the discrepancy between the training and deploying environments, we demonstrate that such a discrepancy can significantly compromise the reliability of the inferred constraints and thus induce unsafe movements. Motivated by this finding, we propose the Robust Constraint Inference (RCI) problem and an Adaptively Robust ICRL (AR-ICRL) algorithm to solve RCI efficiently. Specifically, we model the impact of misspecified dynamics with an opponent policy and learn a robust policy to facilitate safe control in a Markov Game. Subsequently, we adjust our constraint model to align the learned policies to expert demonstrations, accommodating both soft and hard optimality in our behavioral models. Empirical results demonstrate the significance of robust constraints and the effectiveness of the proposed AR-ICRL algorithm under continuous and discrete domains. The code is available at https://github.com/Jasonxu1225/AR-ICRL.

---

## 论文详细总结（自动生成）

# 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：在安全关键决策问题中，逆约束强化学习（ICRL）从专家演示中推断潜在约束，并利用这些约束指导智能体行为。然而，现有ICRL方法普遍假设训练与部署环境相同，忽略了实际应用中常见的环境动力学差异（如风、噪声、模型误设）。论文通过理论和实验证明，这种差异会严重损害推断约束的可靠性，导致智能体在执行时违反安全约束，产生危险行为。
- **整体含义**：为了解决这一问题，论文定义了**鲁棒约束推断（RCI）**问题，要求学习到的约束能在一定不确定性集内的所有环境中均保证安全。在此基础上提出了**自适应鲁棒逆约束强化学习（AR-ICRL）**算法，通过将动力学偏差建模为对手策略，在马尔可夫博弈中学习鲁棒策略，并自适应地调整约束模型以匹配专家演示，从而在模型失配下仍能实现安全控制。

# 2. 论文提出的方法论

## 核心思想
将ICRL中的环境动力学不确定性问题转化为一个**两玩家的零和马尔可夫博弈**，其中玩家（agent）追求在约束下最大化奖励，对手（opponent）则通过选择最坏情况下的动作来破坏安全性（即最大化成本）。通过交替优化玩家策略和对手策略，学习到一个既能模仿专家又能抵御环境扰动的鲁棒策略，并从中蒸馏出鲁棒约束。

## 关键技术细节
- **安全鲁棒策略优化**：将约束满足视为安全目标，利用拉格朗日对偶将原问题转化为优化目标，并用对手策略的上界（Proposition 4.1）将最小化问题转化为两玩家博弈。具体实现上，离散环境采用Q-learning风格的鲁棒策略迭代（Algorithm 2）；连续环境采用基于PPO的算法（Algorithm 3），其中对手策略最大化成本，玩家策略最大化带熵的奖励并受成本约束。
- **自适应约束推断**：在博弈框架下，通过最大化专家轨迹的（因果）对数似然来更新可允许性函数 ϕω(s,a)=exp(-c(s,a))。论文考虑两种情形：
  - **硬最优对手**（Assumption 4.3）：假设专家不会选择成本最大化动作，得到梯度更新式(12)，仅需专家数据和玩家策略采样。
  - **软最优对手**：两者均为软最优策略，利用AM-GM不等式推导出似然的下界，得到梯度更新式(15)，包含专家、玩家和对手的采样。
- **鲁棒约束蒸馏**：博弈收敛后，将玩家策略作为专家，用标准ICRL方法（如MEICRL）在训练环境中蒸馏出鲁棒成本函数 c∀，使该约束下的最优策略在不确定性集内均安全。

## 算法流程（Algorithm 1）
1. 输入专家轨迹、对手强度 1-α、学习环境 ML。
2. 初始化玩家和对手策略，设初始可允许性 ϕ=1（无约束）。
3. 重复：
   - 用目标(8)更新玩家和对手策略。
   - 用混合策略 απ_pl + (1-α)π_op 在 ML 中 rollout 收集轨迹。
   - 用梯度(12)或(15)更新成本函数 cω。
   - 直到轨迹占有率与专家相近。
4. 以玩家策略为专家，用标准ICRL提取鲁棒成本 c∀。

# 3. 实验设计

## 使用场景/数据集
- **离散环境**：三种不同布局的Gridworld，智能体从起点（红）到终点（蓝），需避开不可观测的黑格（约束）。训练时无风，测试时引入随机向上的风（概率pw控制强度）。
- **连续环境**：基于公开ICRL基准（Liu et al., 2023）的三个机器人控制任务：
  - **Blocked Half-Cheetah**：约束 X ≥ -3，最大步长1000。
  - **Blocked Ant**：约束 X ≥ -3，最大步长500。
  - **Crippled Walker**：约束大腿角度 |θ| ≤ 0.6，最大步长500。
- **噪声类型**：三种测试环境下的动力学失配：
  - **全随机噪声**：对全部状态转移加高斯噪声 η~N(μ,σ)。
  - **部分随机噪声**：仅对约束相关特征（如X坐标、大腿角度）加噪声。
  - **攻击噪声**：故意推动智能体违反约束的噪声。

## Benchmark 与对比方法
- **MEICRL** (Malik et al., 2021)：最大熵ICRL + PPO-Lagrange。
- **BC2L** (Binary Classifier Constraint Learning)：简单二分类器作为约束模型。
- **VICRL** (Liu et al., 2023)：用贝塔分布捕捉认知不确定性。
- **IRCO** (Inverse Reachable Constrained Optimization)：结合可达性分析与最大熵约束推断。

# 4. 资源与算力

论文中**未明确说明**所使用的GPU型号、数量、训练时长等具体算力信息，也未提及资源消耗细节。

# 5. 实验数量与充分性

- **实验数量**：
  - 离散环境：3种Gridworld，每种测试不同风强（pw）下的约束违反率和可行奖励。
  - 连续环境：3个任务，每种任务测试3种噪声类型 × 3种噪声规模（共9种测试条件），每个实验重复4个随机种子，报告均值±标准差。
- **消融实验**：论文未单独设计消融实验，但通过调整对手强度 α 间接分析了鲁棒性影响（离散环境中对比 α=0.99和0.9）。
- **充分性与公平性**：
  - 实验覆盖了离散和连续空间，多种噪声类型和规模，对比了主流ICRL方法，评价指标包括约束违反率、可行奖励、累计成本等，较为全面。
  - 但缺乏与直接鲁棒RL方法的对比（如RARL、RCRL等），也未在更多实际场景（如自动驾驶、医疗）中验证。对手强度 α 仅在Gridworld中变化，连续环境固定为0.95，缺乏系统性调参分析。总体而言，实验设计较充分，但仍有进一步提升空间。

# 6. 论文的主要结论与发现

1. **环境动力学失配会严重破坏ICRL的可靠性**：即使推断出真实约束，在扰动环境中策略仍频繁违反约束（Proposition 3.3 及实验证据）。
2. **AR-ICRL显著提升鲁棒性**：在三种连续任务和Gridworld中，AR-ICRL的约束违反率均低于所有对比方法（尤其在大噪声下），同时可行奖励保持较高水平。
3. **对手强度 α 控制鲁棒程度**：较小的 α（更强的对手）使策略更保守，在匹配大的环境扰动时更安全，但可能牺牲部分任务奖励。
4. **鲁棒约束更保守**：可视化显示AR-ICRL恢复的约束比传统方法更保守，使智能体与危险区域保持更大距离，从而在扰动下不易触发约束。

# 7. 优点

- **问题定义合理且实用**：首次系统研究ICRL中的环境动力学失配问题，提出了RCI问题，切合实际部署需求。
- **方法创新**：将安全鲁棒策略优化与逆约束推断有机结合，利用两玩家博弈框架统一处理不确定性和约束学习，理论推导严谨（包括硬/软最优对手的梯度公式）。
- **算法通用性**：支持离散和连续动作空间，兼容软硬最优性假设，有明确的算法流程（Algorithm 1）及子算法（Algorithm 2, 3）。
- **实验验证充分**：在多任务、多噪声类型和规模下验证，对比多个强基线，指标全面。

# 8. 不足与局限

1. **需要在线环境交互**：AR-ICRL是online RL框架，需与训练环境交互收集数据，不适合交互成本高昂或危险的真实场景。论文虽在Limitation中提及，但未给出离线扩展方案。
2. **假设不确定性集有界**：方法假设训练与部署环境的差异是有限的（由α控制），但实际中环境变化可能完全超出预设范围，此时鲁棒性无法保证。
3. **缺乏消融实验**：未单独分析各组件（对手策略、约束蒸馏等）的贡献；对手强度 α 的选择缺乏准则，连续环境中固定为0.95可能并非最优。
4. **基准对比不全**：未与鲁棒RL方法（如RARL、RCRL）或离线ICRL方法对比，也未验证在更复杂环境（如多智能体、高维视觉）中的表现。
5. **计算资源未报告**：缺乏GPU型号、训练时长等细节，影响可复现性和效率评估。
6. **理论分析局限性**：Proposition 4.6的证明依赖较强假设（如专家环境与学习环境相同），实际中专家演示可能来自不同环境，此时结论可能不成立。

（完）
