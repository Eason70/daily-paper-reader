---
title: Safety through feedback in Constrained RL
title_zh: 约束强化学习中的反馈安全
authors: "Shashank Reddy Chirra, Pradeep Varakantham, Praveen Paruchuri"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=WSsht66fbC"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 从反馈中学习代价函数用于安全约束强化学习
tldr: 安全关键强化学习中设计代价函数昂贵且困难。本文提出从离线反馈中学习代价函数的框架，反馈可由系统生成或人类观察提供。该方法在迭代训练中利用反馈调整成本，避免了手动设计。实验表明在多种安全场景中有效降低了违反约束率，提升了安全性。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1430, \"height\": 398, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1423, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 506, \"height\": 765, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 467, \"height\": 769, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 317, \"height\": 1164, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 315, \"height\": 1145, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1042, \"height\": 2143, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1429, \"height\": 789, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1425, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1155, \"height\": 472, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 576, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1356, \"height\": 531, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1422, \"height\": 1218, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1370, \"height\": 1093, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2024-wssht66fbc/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1142, \"height\": 574, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2024-wssht66fbc/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1452, \"height\": 967, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-wssht66fbc/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1448, \"height\": 271, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-wssht66fbc/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1445, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2024-wssht66fbc/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1445, \"height\": 615, \"label\": \"Table\"}]"
motivation: 安全强化学习代价函数设计复杂且昂贵。
method: 从离线反馈中学习代价函数，结合强化学习迭代优化。
result: 有效降低约束违反率，减少人工干预。
conclusion: 为安全强化学习提供了实用的成本学习框架。
---

## Abstract
In safety-critical RL settings, the inclusion of an additional cost function is often favoured over the arduous task of modifying the reward function to ensure the agent's safe behaviour. However, designing or evaluating such a cost function can be prohibitively expensive. For instance, in the domain of self-driving, designing a cost function that encompasses all unsafe behaviours (e.g., aggressive lane changes, risky overtakes) is inherently complex, it must also consider all the actors present in the scene making it expensive to evaluate. In such scenarios, the cost function can be learned from feedback collected offline in between training rounds. This feedback can be system generated or elicited from a human observing the training process. Previous approaches have not been able to scale to complex environments and are constrained to receiving feedback at the state level which can be expensive to collect. To this end, we introduce an approach that scales to more complex domains and extends beyond state-level feedback, thus, reducing the burden on the evaluator. Inferring the cost function in such settings poses challenges, particularly in assigning credit to individual states based on trajectory-level feedback. To address this, we propose a surrogate objective that transforms the problem into a state-level supervised classification task with noisy labels, which can be solved efficiently. Additionally, it is often infeasible to collect feedback for every trajectory generated by the agent, hence, two fundamental questions arise: (1) Which trajectories should be presented to the human? and (2) How many trajectories are necessary for effective learning? To address these questions, we introduce a \textit{novelty-based sampling} mechanism that selectively involves the evaluator only when the the agent encounters a \textit{novel} trajectory, and discontinues querying once the trajectories are no longer \textit{novel}. We showcase the efficiency of our method through experimentation on several benchmark Safety Gymnasium environments and realistic self-driving scenarios. Our method demonstrates near-optimal performance, comparable to when the cost function is known, by relying solely on trajectory-level feedback across multiple domains. This highlights both the effectiveness and scalability of our approach. The code to replicate these results can be found at \href{https://github.com/shshnkreddy/RLSF}{https://github.com/shshnkreddy/RLSF}

---

## 论文详细总结（自动生成）

# 论文总结：Safety through feedback in Constrained RL

## 1. 核心问题与整体含义（研究动机和背景）

在安全关键的强化学习场景中，传统方法需要手动设计代价函数（cost function）来惩罚不安全行为，但这一过程极其复杂且昂贵。例如，在自动驾驶中，需要定义所有可能的危险行为（如激进变道、危险超车）并考虑所有交通参与者，设计成本高，评估也耗时。为此，论文提出从离线反馈中学习代价函数，以替代手工设计。反馈可由系统生成或由人类观察者提供，从而降低人工负担。现有方法局限于状态级反馈且无法扩展到复杂环境。本文旨在解决：  
- 如何从轨迹级反馈中推断代价函数？  
- 如何选择最需要反馈的轨迹，以减少查询量？  

最终目标是实现安全策略学习，且性能接近已知代价函数的情况。

## 2. 方法论

### 2.1 核心思想
提出**RLSF（Reinforcement Learning from Safety Feedback）**算法，由两个交替阶段组成：  
1. **数据/反馈收集**：使用当前策略滚动收集轨迹，从中选取子集向评估者请求反馈。反馈方式为将轨迹分段，每个段标记为“安全”或“不安全”（只要段内任一状态不安全，则整个段标记为不安全）。  
2. **代价推断与策略改进**：利用反馈数据学习一个二元分类器（安全/不安全概率），再用推断出的代价函数配合PPO-Lagrangian算法更新策略。

### 2.2 关键技术细节

#### 2.2.1 代价函数推断
- 假设存在真实二元代价函数 $c_{gt}(s,a) \in \{0,1\}$，定义安全概率 $p_{\text{safe}}(s,a)$。  
- 轨迹段安全概率为 $p_{\text{safe}}(\tau_{i:j}) = \prod_{t=i}^{j} p_{\text{safe}}(s_t,a_t)$。直接最大化似然会导致长段时梯度不稳定。  
- **替代损失函数**：将轨迹级问题转化为状态级带噪声标签的二元分类问题：  
  $$L_{\text{sur}} = - \mathbb{E}_{(s,a)\sim d_g} \log p_{\text{safe}}(s,a) - \mathbb{E}_{(s,a)\sim d_b} \log(1-p_{\text{safe}}(s,a))$$  
  其中 $d_g$ 和 $d_b$ 分别是安全段与不安全段中状态-动作对的分布。理论证明 $L_{\text{sur}}$ 是原似然损失的上界，且优化该损失得到的估计 $c^*(s,a)$ 具有**非负偏差**，即推断的期望代价真实代价的上界，从而保证安全。

#### 2.2.2 高效轨迹抽样
- 提出**新颖性采样**：将状态空间通过 SimHash 离散化为桶，维护状态访问计数。一条轨迹若包含至少 $e$ 个新颖状态（即计数为零的状态），则被选中请求反馈。这自然形成随时间递减的查询计划，减少人工负担。

#### 2.2.3 策略优化
- 使用 PPO-Lagrangian 算法，将推断的代价 $c_\theta(\tau)$ 作为约束项进行优化。算法详细流程见论文 Algorithm 1。

## 3. 实验设计

### 3.1 环境与场景
- **Safety Gymnasium**：包含 Point Circle、Car Circle、Biased Pendulum、Blocked Swimmer、HalfCheetah、Hopper、Walker2d（硬约束 $c_{\max}=0$）以及 Point/Car Goal、Point/Car Push（软约束 $c_{\max}>0$）。  
- **Safe Driver 模拟器**：三种场景（阻塞道路、变道、双车道超车），代价基于速度、位置、与车辆距离等。

### 3.2 对比方法
- 已知代价：PPO-Lagrangian（PPOLag）与 SIM with known costs（SIMKC）作为上界。  
- 未知代价基线：SIM（自模仿安全强化学习）、SDM（安全分布匹配）。  
- 抽样方法比较：均匀采样、递减调度、随机采样、熵采样 vs 新颖性采样。

### 3.3 评估指标
- 回报（Return）与代价违反率（Cost Violation Rate）。硬约束环境要求违反率尽量低，软约束环境要求代价不超过阈值。

## 4. 资源与算力

论文在附录 D.1 中说明：实验在配有 **4 块 NVIDIA RTX A5000 GPU** 和 **96 核 CPU** 的集群上进行，总计算时长约 **两周**。每种子设置重复 6 个独立种子（部分为 3 个）。未提供每步 GPU 小时数等更细粒度数据。

## 5. 实验数量与充分性

- 共在 **9 个 Safety Gymnasium 环境**（含 7 个硬约束 + 4 个软约束）及 **3 个 Safe Driver 场景**上进行实验。  
- 进行了**消融实验**：  
  - 不同抽样方法对比（Figure 2、Figure 9）。  
  - 不同段长度对性能影响（Figure 12）。  
  - 反馈缓冲区大小影响（Figure 13）。  
  - 替代损失 vs 原始似然损失的梯度稳定性（Figure 14）。  
- 还进行了**代价函数迁移实验**：将 Point 场景学到的代价函数迁移到 Doggo 智能体（不同形态）上训练，结果显示性能与已知代价相近。  
- 实验设计较为全面，对比基线包含了已知代价和未知代价两类方法，且评估指标明确。但所有反馈均由自动脚本基于真实代价函数模拟，缺乏真实人类实验。

## 6. 主要结论与发现

1. **RLSF 在绝大多数环境中显著优于 SIM 和 SDM 基线**，在 7/11 个环境中达到 PPOLag（已知代价）最佳性能的 ≈80%。  
2. **新颖性采样方式在最少的反馈量下达到最佳性能**，优于固定预算下的均匀采样、递减调度、熵采样等。  
3. **推断的代价函数与真实代价高度相关**，在状态级反馈时几乎一致，在轨迹级反馈时存在轻微高估偏差，但该偏差保证安全性（上界性）。  
4. **代价迁移**：不同形态的智能体（Point → Doggo）使用迁移的代价函数仍可训练出安全策略。  
5. **偏差校正**：通过增大 $c_{\max}$ 可缓解过度保守，但 δ 需要手动调节。

## 7. 优点

- **方法创新**：首次将反馈扩展到轨迹级别，替代损失有效解决了长段信用分配问题；新颖性采样隐式降低查询量且无需预设预算。  
- **理论支撑**：证明了替代损失是似然损失的上界，推断的代价函数偏差非负，从而保证安全的充分性。  
- **实验覆盖广**：包含多种类型的环境（位置约束、速度约束、障碍物规避、驾驶场景），迁移实验验证了泛化性。  
- **代码开放**：提供了可复现的 GitHub 仓库。

## 8. 不足与局限

- **反馈模拟**：实验中使用真实代价函数的自动脚本模拟人类反馈，未在真实人类受试者上验证，存在噪声与不一致性风险。  
- **环境依赖**：在部分环境（如 Safety Goal/Push）仍需状态级反馈（段长 k=1），这会增加人工负担。  
- **偏差调节**：高估偏差只能通过手动调整阈值缓解，缺乏自动校正方案。  
- **反馈量**：虽然优于基线，但在复杂场景中仍可能需上千条查询（如 Point Goal 约 7892 条），实际部署成本仍不低。  
- **缺少与最新方法的对比**：例如与 Inverse Constrained RL 等方法（依赖专家演示）的对比未涉及，但论文已说明目标场景不同。

（完）
