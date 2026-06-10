---
title: Explainably Safe Reinforcement Learning
title_zh: 可解释安全强化学习
authors: "Sabine Rieder, Stefan Pranger, Debraj Chakraborty, Jan Kretinsky, Bettina Könighofer"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=l6hAqx4eoB"
tags: ["query:safe-rl-cbf"]
score: 7.0
evidence: 通过决策树屏蔽实现可解释安全强化学习
tldr: 安全强化学习中的屏蔽机制虽能保证安全，但自动合成的屏蔽难以解释。本文提出使用紧凑决策树表示屏蔽策略，解决传统屏蔽的非确定性和规模过大问题，实现可解释的安全强化学习，增强了对系统行为的理解。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1073, \"height\": 764, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1155, \"height\": 291, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1391, \"height\": 366, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1402, \"height\": 304, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1190, \"height\": 657, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 673, \"height\": 630, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1455, \"height\": 129, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 448, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1405, \"height\": 305, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1406, \"height\": 307, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 984, \"height\": 512, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1017, \"height\": 633, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1245, \"height\": 938, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 980, \"height\": 2226, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1219, \"height\": 1121, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1366, \"height\": 1354, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 436, \"height\": 289, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 469, \"height\": 267, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 598, \"height\": 260, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l6haqx4eob/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1385, \"height\": 1500, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-l6haqx4eob/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 712, \"height\": 336, \"label\": \"Table\"}]"
motivation: 现有安全RL中的屏蔽机制不可解释，且决策树表示面临非确定性挑战。
method: 将屏蔽策略转化为紧凑决策树表示，提出新方法控制规模并保持可解释性。
result: 获得了可解释且仍具安全保证的屏蔽策略。
conclusion: 为安全RL提供了兼顾可解释性和安全性的解决方案。
---

## Abstract
Trust in a decision-making system requires both safety guarantees and the ability to interpret and understand its behavior. This is particularly important for learned systems, whose decision-making processes are often highly opaque. Shielding is a prominent model-based technique for enforcing safety in reinforcement learning. However, because shields are automatically synthesized using rigorous formal methods, their decisions are often similarly difficult for humans to interpret. Recently, decision trees became customary to represent controllers and policies. However, since shields are inherently non-deterministic, their decision tree representations become too large to be explainable in practice. To address this challenge, we propose a novel approach for explainable safe RL that enhances trust by providing human-interpretable explanations of the shield's decisions. Our method represents the shielding policy as a hierarchy of decision trees, offering top-down, case-based explanations. At design time, we use a world model to analyze the safety risks of executing actions in given states. Based on this risk analysis, we construct both the shield and a high-level decision tree that classifies states into risk categories (safe, critical, dangerous, unsafe), providing an initial explanation of why a given situation may be safety-critical. At runtime, we generate localized decision trees that explain which actions are allowed and why others are deemed unsafe. Altogether, our method facilitates the explainability of the safety aspect in the safe-by-shielding reinforcement learning. Our framework requires no additional information beyond what is already used for shielding, incurs minimal overhead, and can be readily integrated into existing shielded RL pipelines. In our experiments, we compute explanations using decision trees that are several orders of magnitude smaller than the original shield.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **背景**：深度强化学习在安全关键系统中应用受限，因为智能体通过试错探索环境，存在采取不安全行为的风险。
- **已有方案**：屏蔽（Shielding）是保障强化学习安全的主流技术，它在运行时拦截不安全动作，提供形式化安全保证。但屏蔽通常由严格形式化方法自动合成，其决策（即允许/禁止哪些动作）对用户而言同样难以理解。
- **问题**：屏蔽策略本质上是非确定性的（每个状态下允许多个安全动作），直接将其表示为决策树会导致树过大、不可解释。同时，强化学习策略本身也是不透明的深度神经网络，导致整个系统的行为难以预测、理解和信任。
- **核心目标**：在保留屏蔽安全保证的前提下，提供人类可理解的解释，提升对安全强化学习系统的信任。

## 2. 方法论：核心思想、关键技术细节

### 2.1 整体框架

- **输入**：一个马尔可夫决策过程（MDP）世界模型 \(M\)，一个暂态逻辑（CTL）安全规约 \(\varphi\)。
- **输出**：一个分层决策树结构，提供三级解释：
  - **Level 1**：状态风险分类决策树，解释当前状态的风险类别（安全、临界、危险、不安全）。
  - **Level 2**：动作风险决策树，解释在当前状态下哪些动作被允许、哪些被禁止。
  - **Level 3**：执行树，解释为什么某个被禁动作会导致安全违规。

### 2.2 关键定义与计算

- **风险定义**：
  - 从状态 \(s\) 出发，在 \(h\) 步内违反安全规约的最小概率：\(\text{risk}_{M,\varphi}(s, h) = \mathbf{P}^{\min}_{M, \neg \varphi}(s, h)\)。
  - 在状态 \(s\) 执行动作 \(a\) 后的风险：\(\text{risk}_{M,\varphi}(s, a, h) = \sum_{s'} P(s,a,s') \cdot \text{risk}_{M,\varphi}(s', h-1)\)。
- **状态分类**（基于风险阈值 \(\epsilon\)）：
  - **安全状态**：所有动作风险 \(\le \epsilon\)。
  - **临界状态**：部分动作风险 \(\le \epsilon\)，部分 \(> \epsilon\)。
  - **危险状态**：所有动作风险 \(> \epsilon\)，但尚未违反安全。
  - **不安全状态**：已违反安全规约。
- **屏蔽策略**：在安全/临界状态允许风险 \(\le \epsilon\) 的动作；在危险状态只允许风险最小的动作（作为后备）；在不安全状态无动作。

### 2.3 Level 1 决策树

- 使用标准决策树学习算法，以状态特征和用户定义的谓词作为分裂条件，精确地将所有状态分类到四个风险类别。
- 树的叶子对应单个类别，路径上的谓词即为分类原因。

### 2.4 Level 2 决策树

- 针对 Level 1 树中某个叶节点对应的状态子集，学习一棵子决策树，解释该子集中哪些动作被允许。
- 对临界状态，树区分安全动作与不安全动作；对危险状态，树指出最安全动作。

### 2.5 Level 3 执行树

- 给定当前状态 \(s\) 和被禁动作 \(a\)，构造一个马尔可夫链：在 \(s\) 执行 \(a\)，之后在所有状态采取最安全动作。
- 从该链中提取一组概率质量超过阈值 \(\epsilon\) 的即将会进入不安全状态的轨迹，并将这些轨迹合并为执行树，直观展示 unsafe 后果。

## 3. 实验设计

- **场景**：
  1. **Frozen Lake**（Farama）：\(n \times n\) 网格，智能体需避开冰洞到达目标。盾牌防止掉入冰洞，风险阈值 \(\epsilon=0.075\)。
  2. **Highway Cruise Control**：自动驾驶汽车在高速公路上行驶，避免碰撞。两个参数：车道数（2或3）、速度是否可变。-f (fixed)、-c (changeable)。共4个场景：HW2-f, HW2-c, HW3-f, HW3-c。阈值 \(\epsilon=0\)。
  3. **Boeing TaxiNet**：飞机滑行时保持中心线对齐，避免超过最大航向误差和位置偏差。两种变体：确定性和湿滑（有滑移概率）。阈值 \(\epsilon=0\)。
- **Benchmark**：无外部基线对比，主要与原始盾牌（查找表）和直接用一个决策树表示盾牌的方法比较大小。
- **对比方法**：原始盾牌大小 \(|\pi_{\text{shield}}|\) vs 单棵决策树 \(|\mathcal{T}_{\text{shield}}|\) vs 分层决策树 \(|\mathcal{T}_{L1}|\) 和 \(|\mathcal{T}_{L2}|\)。
- **评价指标**：树的大小（节点数）作为可解释性代理。同时报告盾牌合成、决策树学习的耗时。

## 4. 资源与算力

- 文中明确说明：“All experiments were conducted on a laptop with an Intel® Core™i7-11800H CPU at 2.3 GHz with 32 GB of RAM.”
- 未使用GPU。所有模型检查用 Tempest 工具，决策树学习用 dtcontrol。未报告具体的训练轮数或总计算量。

## 5. 实验数量与充分性

- **Frozen Lake**：对 \(n=5,10,\dots,50\) 每种规模随机生成10个实例，共约50个实例，报告平均值和标准差（在附录图8、9中给出不同孔洞比例下的结果）。
- **Highway**：4个不同场景（HW2-f, HW2-c, HW3-f, HW3-c），每个场景给出盾牌大小和树的大小，并展示示例决策树。
- **TaxiNet**：2个变体（确定性和湿滑），给出盾牌和树的尺寸。
- **消融/变体**：在Frozen Lake中改变了孔洞比例（4%、15%、20%），验证对树大小的影响；在Highway中区分固定速度/可变速度。
- **总体评价**：实验覆盖了不同领域（网格导航、自动驾驶、飞机滑行），规模从几千到几十万状态不等，并展示了树大小比原始盾牌小几个数量级。但缺乏与其他可解释安全方法（如基于规则的方法）的对比，也没有用户研究评估解释的实用性。训练结果（Reward、违反次数）仅作为补充，未纳入主要可解释性评价。

## 6. 主要结论与发现

- 提出的分层决策树方法能够将盾牌大小压缩数数量级（例如 Frozen Lake 中 50×50 网格的盾牌约 16 万条规则，而 Level 1+2 树仅为几十个节点）。
- 用户定义的谓词（例如距离、相对速度）能显著提升树的紧凑性和可读性。
- 方法可无缝集成到现有屏蔽 RL 流水线，不需要额外输入，计算开销小（盾牌合成和树学习都在秒级或分钟级）。
- 通过三个不同领域的案例验证了方法的通用性和可扩展性。

## 7. 优点

1. **新颖性**：首次将可解释性与形式化安全保证系统性地结合在 RL 中。
2. **层次化解释**：从状态风险类别到动作允许性再到具体后果，提供由粗到细的因果追溯，避免了单一大型决策树难以阅读的问题。
3. **保持安全性与最优性**：仅解释盾牌，不干预 RL 策略的学习，保留其最优性。
4. **低开销**：仅依赖屏蔽已有的模型和规约，增加的计算成本可忽略。
5. **支持用户自定义谓词**：允许引入领域知识指导决策树学习，提升解释质量和紧凑性。

## 8. 不足与局限

1. **对谓词的依赖**：生成紧凑解释高度依赖用户提供良好的谓词。若谓词选择不当，树可能过大。作者提及未来需研究自动谓词生成。
2. **实验对比不足**：未与任何其他可解释安全方法（如基于规则、注意力机制等）进行对比，缺乏基准。
3. **缺乏用户研究**：虽然声称“可解释”，但没有通过人类实验验证解释的有效性和理解度。
4. **状态空间假设**：方法需要离散状态空间和完整的 MDP 模型。对连续状态/动作空间或部分可观环境，需额外抽象，可能影响精度。
5. **阈值依赖**：风险阈值 \(\epsilon\) 的选择影响状态分类和盾牌行为，但论文未探讨其敏感性或自动选取。
6. **可扩展性挑战**：对于极高维或巨量状态空间，盾牌计算和决策树学习可能成为瓶颈（例如 HW3-c 中 Level 1 树达 70 节点，且作者提到若谓词不当会更大）。
7. **概率保证**：盾牌给出的是概率安全保证，但 Level 3 执行树仅展示达到阈值的一组轨迹，未提供所有可能导致 unsafe 的完整覆盖。

（完）
