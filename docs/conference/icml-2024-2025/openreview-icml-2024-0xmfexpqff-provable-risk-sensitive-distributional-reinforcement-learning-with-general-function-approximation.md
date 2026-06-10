---
title: Provable Risk-Sensitive Distributional Reinforcement Learning with General Function Approximation
title_zh: 基于一般函数逼近的可证明风险敏感分布强化学习
authors: "Yu Chen, XiangCheng Zhang, Siwei Wang, Longbo Huang"
date: 2024-05-02
pdf: "https://openreview.net/pdf?id=0xmfExPqFf"
tags: ["query:safe-rl-cbf"]
score: 5.0
evidence: 风险敏感分布强化学习
tldr: 该论文提出风险敏感分布强化学习通用框架，采用静态Lipschitz风险度量，设计了模型基与模型无关的元算法，可捕捉决策中的风险与安全，虽未涉及控制屏障函数，但方法可迁移至安全控制场景。
source: ICML-2024-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2024-0xmfexpqff/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1685, \"height\": 1252, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2024-0xmfexpqff/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 885, \"height\": 539, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-0xmfexpqff/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1770, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2024-0xmfexpqff/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1772, \"height\": 394, \"label\": \"Table\"}]"
motivation: 在强化学习中考虑风险因素以提升决策安全性。
method: 提出风险敏感分布强化学习框架及两种元算法。
result: 理论分析了估计函数对策略效果的影响及样本复杂度。
conclusion: 为风险敏感RL提供了理论基础。
---

## Abstract
In the realm of reinforcement learning (RL), accounting for risk is crucial for making decisions under uncertainty, particularly in applications where safety and reliability are paramount. In this paper, we introduce a general framework on Risk-Sensitive Distributional Reinforcement Learning (RS-DisRL), with static Lipschitz Risk Measures (LRM) and general function approximation. Our framework covers a broad class of risk-sensitive RL, and facilitates analysis of the impact of estimation functions on the effectiveness of RSRL strategies and evaluation of their sample complexity. We design two innovative meta-algorithms: RS-DisRL-M, a model-based strategy for model-based function approximation, and RS-DisRL-V, a model-free approach for general value function approximation. With our novel estimation techniques via Least Squares Regression (LSR) and Maximum Likelihood Estimation (MLE) in distributional RL with augmented Markov Decision Process (MDP), we derive the first $\widetilde{\mathcal{O}}(\sqrt{K})$ dependency of the regret upper bound for RSRL with static LRM, marking a pioneering contribution towards statistically efficient algorithms in this domain.

---

## 论文详细总结（自动生成）

# 论文总结：《基于一般函数逼近的可证明风险敏感分布强化学习》

## 1. 核心问题与整体含义

- **研究动机**：在安全攸关的场景（如金融投资、医疗决策、自动驾驶）中，强化学习需要明确考虑风险。传统的风险中性RL仅优化期望回报，无法捕捉回报分布的风险特征；而风险敏感RL（RSRL）旨在优化某种风险度量（如条件风险价值CVaR、熵风险度量ERM）。然而，现有RSRL理论工作大多局限于表格MDP或特定风险度量，缺乏在一般函数逼近框架下处理静态Lipschitz风险度量（LRM）的样本效率分析。
- **整体含义**：论文首次提出了一个通用的风险敏感分布强化学习（RS-DisRL）框架，覆盖了包括ERM、CVaR、谱风险度量在内的广泛静态LRM，并给出了基于一般函数逼近（模型基与模型无关）的亚线性遗憾上界，填补了该方向的理论空白。

## 2. 方法论

- **核心思想**：利用分布强化学习（DisRL）的分布特性，结合增强MDP（augmented MDP）将历史依赖策略转化为马尔可夫策略，从而在增强状态空间上应用分布贝尔曼方程。通过最小二乘回归（LSR）或最大似然估计（MLE）构建置信集，并采用乐观规划（optimistic planning）实现探索与利用的平衡。
- **关键技术细节**：
    - **增强MDP**：将原始MDP的状态扩展为包含当前累积回报的状态对 $(s_h, y_h)$，使得历史依赖策略等价于增强MDP中的马尔可夫策略。
    - **分布贝尔曼方程**：定义累积回报的CDF/PDF满足的分布贝尔曼算子，用于估计值分布。
    - **模型基元算法 RS-DisRL-M**：利用模型类 $\Theta$，通过LSR或MLE估计转移模型，并构造置信集 $\hat{\Theta}_k$；在每轮执行乐观计划 $(\pi_k, \hat{\theta}_k) = \arg\max_{\pi,\theta\in\hat{\Theta}_k}\rho(Z^\pi_\theta)$。
    - **模型无关元算法 RS-DisRL-V**：给定值函数类 $\mathcal{Z}$，通过LSR或MLE估计回报分布并构造版本空间 $\hat{\mathcal{Z}}_{k,\pi}$，同样采用乐观规划。
    - **估计方法**：
        - **LSR方法**：对CDF进行回归，利用混合分布函数和贝尔曼误差的平方和构造置信半径 $\beta_{\text{LSR}}$。
        - **MLE方法**：对转移概率或密度函数进行最大似然估计，利用TV距离与似然比的关系，结合增广仿真引理（Lemma D.2）和证人秩（witness rank）或贝尔曼eluder维数控制复杂度。
    - **理论保证**：在各自假设下，两种元算法的遗憾上界均为 $\widetilde{\mathcal{O}}(L_\infty(\rho) \cdot \text{poly}(H) \cdot D \cdot \sqrt{K})$，其中 $D$ 为结构复杂度（如eluder维数、证人秩、贝尔曼eluder维数）。

## 3. 实验设计

- **实验场景**：论文**未在正文中设计大规模实验**，仅在附录I.6中提供了一个简单的数值例子：一个零均值MDP（期望回报为0，因此风险中性算法无法学习），状态数 $S=3$、动作数 $A=2$、特征维数 $d=2$、回合长度 $H=6$、固定回报网格点数 $M=3$。
- **Benchmark**：对比了风险中性LSVI-UCB（Jin et al., 2020）和模型基乐观MDP算法（Bastani et al., 2022）。
- **对比方法**：包括风险中性和另一种风险敏感基线。
- **结果**：风险中性算法失败，模型基算法收敛慢，而本文提出的线性CVaR算法（RSRL-Linear-CVaR）收敛更快，且风险参数 $\tau$ 越小（风险厌恶程度越高）遗憾越大，与理论一致。

## 4. 资源与算力

- 论文**未明确提及**使用的GPU型号、数量、训练时长或任何计算资源。数值实验规模极小（MDP简单，迭代轮数较少），可以推断所用算力极低，未涉及大规模深度学习训练。

## 5. 实验数量与充分性

- **实验数量**：仅一个简单合成MDP上的数值验证，包含4种不同的 $\tau$ 值（0.2, 0.3, 0.5, 0.7），每个场景绘制了不同算法的累积遗憾曲线。无消融实验、无多环境对比、无统计显著性检验。
- **充分性与公平性**：实验规模非常有限，不足以全面验证算法在复杂场景下的性能；但论文定位于理论贡献，数值实验仅用于展示可计算、可实现的例子，并非实验驱动。因此，在理论论文语境下，实验是合理的补充，但不足以支持实际部署结论。

## 6. 主要结论与发现

- 提出了RS-DisRL的通用框架，覆盖静态LRM与一般函数逼近，设计了模型基与模型无关两种元算法。
- 首次为静态LRM下的RSRL证明了 $\widetilde{\mathcal{O}}(\sqrt{K})$ 的遗憾上界，达到了表格MDP下已知最优的 $K$ 依赖。
- 在风险中性特例下，结果退化为已有最优值（如Ayoub et al.，Liu et al.，Jin et al.），且在CVaR和低秩MDP等具体情形下比先前工作（如Zhao et al.）有更优或相当的依赖。
- 数值实验验证了算法在零均值MDP中能有效学习CVaR，风险中性算法失败，且本文算法优于模型基基线。

## 7. 优点

- **理论深度**：首次将分布RL与静态LRM结合，并统一了模型基与模型无关框架，分析技巧（如增广仿真引理、CDF的LSR回归、分布性能差分解）具有创新性。
- **通用性**：框架覆盖ERM、CVaR、谱风险等多种风险度量，且函数类可扩展至线性、低秩、eluder维数有界等常见结构。
- **结果最优性**：在 $K$ 的依赖上达到 $\sqrt{K}$，符合信息论下界；风险中性时与已知最优结果一致。
- **可计算性**：在离散线性MDP和CVaR特例下，给出了高效可实现算法（RSRL-Linear-CVaR），并进行了数值验证。

## 8. 不足与局限

- **实验覆盖严重不足**：仅一个合成MDP的数值例子，缺乏在标准RL基准（如Atari、MuJoCo）或实际风险敏感场景上的验证，无法证明算法的实际可用性。
- **理论假设较强**：
    - 需要模型可实现性（model realizability）或分布贝尔曼完备性（distributional Bellman completeness），这在复杂环境中可能难以满足。
    - 对LRM要求Lipschitz连续性及律不变性，部分风险度量（如VaR）不满足Lipschitz条件，因此不直接适用。
    - 在线学习框架假设MDP是episodic且回合数已知，未考虑离线或无限视域设置。
- **计算复杂性**：通用元算法（RS-DisRL-M和RS-DisRL-V）涉及在整个版本空间上的乐观规划，这是NP-hard的，仅在线性等特例下可高效实现。
- **风险度量限制**：仅考虑静态风险度量，未覆盖动态/迭代风险度量（如迭代CVaR），后者在长时间序列风险控制中更常见。
- **偏差风险**：理论证明依赖于高概率事件，隐藏常数及poly(log)项可能较大，实际性能可能与上界有显著差距。

（完）
