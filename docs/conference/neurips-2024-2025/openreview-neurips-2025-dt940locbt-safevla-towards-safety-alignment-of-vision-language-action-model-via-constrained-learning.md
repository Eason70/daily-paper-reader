---
title: "SafeVLA: Towards Safety Alignment of Vision-Language-Action Model via Constrained Learning"
title_zh: SafeVLA：通过约束学习实现视觉-语言-动作模型的安全对齐
authors: "Borong Zhang, Yuhao Zhang, Jiaming Ji, Yingshan Lei, Josef Dai, Yuanpei Chen, Yaodong Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=dt940loCBT"
tags: ["query:safe-rl-cbf"]
score: 6.0
evidence: 通过约束学习实现机器人策略的安全强化学习
tldr: 针对视觉-语言-动作模型在真实部署中的安全风险，提出ISA框架，系统性地建模安全需求、诱发不安全行为、通过受限马尔可夫决策过程范式进行安全强化学习约束，并严格评估安全性能，为通用机器人策略的安全对齐提供了系统方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1448, \"height\": 723, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1448, \"height\": 690, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 453, \"height\": 394, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1466, \"height\": 732, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1436, \"height\": 363, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 711, \"height\": 507, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1439, \"height\": 361, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1443, \"height\": 218, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 478, \"height\": 470, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 463, \"height\": 470, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1434, \"height\": 380, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1445, \"height\": 777, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1446, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1159, \"height\": 1425, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dt940locbt/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1451, \"height\": 526, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1343, \"height\": 494, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 727, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1140, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1314, \"height\": 1704, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1427, \"height\": 985, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1454, \"height\": 202, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1336, \"height\": 125, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1455, \"height\": 198, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1459, \"height\": 188, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 670, \"height\": 628, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1227, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1212, \"height\": 1045, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1450, \"height\": 599, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1450, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1409, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dt940locbt/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 763, \"height\": 529, \"label\": \"Table\"}]"
motivation: 视觉-语言-动作模型在机器人部署中存在严重安全隐患，需要显式集成安全约束。
method: 提出ISA框架，基于受限马尔可夫决策过程，通过安全强化学习约束策略。
result: 在多种机器人任务中有效降低了不安全行为的发生。
conclusion: 为VLA模型的安全部署提供了一种可扩展的约束学习解决方案。
---

## Abstract
Vision-language-action models (VLAs) show potential as generalist robot policies. However, these models pose extreme safety challenges during real-world deployment, including the risk of harm to the environment, the robot itself, and humans. *How can safety constraints be explicitly integrated into VLAs?* We address this by exploring an integrated safety approach (ISA), systematically **modeling** safety requirements, then actively **eliciting** diverse unsafe behaviors, effectively **constraining** VLA policies via safe reinforcement learning, and rigorously **assuring** their safety through targeted evaluations. Leveraging the constrained Markov decision process (CMDP) paradigm, ISA optimizes VLAs from a min-max perspective against elicited safety risks. Thus, policies aligned through this comprehensive approach achieve the following key features: (I) effective **safety-performance trade-offs**, reducing the cumulative cost of safety violations by 83.58\% compared to the state-of-the-art method, while also maintaining task success rate (+3.85\%). (II) strong **safety assurance**, with the ability to mitigate long-tail risks and handle extreme failure scenarios. (III) robust **generalization** of learned safety behaviors to various out-of-distribution perturbations. The effectiveness is evaluated on long-horizon mobile manipulation tasks.

---

## 论文详细总结（自动生成）

# SafeVLA 论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
视觉-语言-动作模型（VLA）被视为通用机器人策略的候选，但在真实世界部署中面临严重安全挑战，包括对环境、机器人自身和人类的伤害风险。现有的LLM/VLM安全对齐方法（如RLHF、数据增强、内容过滤等）无法直接应用于VLA，因为抽象的安全意图与实际物理世界中的安全隐患之间存在本质差距。当前VLA训练主要依赖行为克隆或标准强化学习，缺乏显式集成安全约束的机制。为此，论文首次系统探索了VLA的安全对齐问题，提出集成安全方法（ISA），旨在显式地将安全约束融入VLA中，实现安全与任务性能的有效权衡。

## 2. 论文提出的方法论：核心思想、关键技术细节与算法流程
### 核心思想
基于约束马尔可夫决策过程（CMDP）框架，将VLA安全对齐建模为一个受约束的优化问题：在满足安全约束的前提下最大化任务奖励。采用Lagrangian方法将约束问题转化为无约束的min-max优化，通过交替更新策略参数和Lagrange乘子，实现安全优先、再最大化任务性能的权衡。

### 关键技术细节
- **ISA框架包含四个相互关联的方面**：
  - (A) **建模安全**：定义状态-动作安全谓词（φ）和轨迹级安全谓词（ψ），形式化描述不安全行为。例如，φ_corner检测狭窄角落中的碰撞，ψ_fragile collection检测操作中对易碎物品的连带损坏。
  - (B) **诱发风险**：利用大规模场景数据集（ProcTHOR的150K场景、Objaverse的800K 3D资产）和AI2THOR模拟器，设计Safety-CHORES基准，包含五种安全关键组件（角落、盲区、易碎集合、临界点、危险设备），系统性地诱发多样化不安全行为。
  - (C) **约束策略**：基于CMDP，使用Lagrangian方法的SafeRL算法进行策略优化。目标函数为：min_θ max_λ≥0 [-J_r(θ) + Σλ_i J_{c_i}(θ)]，其中λ_i为动态调整的Lagrange乘子。
  - (D) **安全保证**：通过测试时安全、长尾安全、极端失败场景安全等维度全面评估对齐后的策略。

### 算法流程（文字说明）
1. 从任务指令和初始状态出发，策略π_θ与环境交互生成轨迹。
2. 轨迹经过安全谓词（φ和ψ）标记，将每个安全违规转换为成本信号（状态-动作违规在时间步t计1，轨迹级违规在段末计1）。
3. 使用PPO风格的代理损失分别计算奖励和成本的策略梯度，结合Lagrange乘子λ形成联合损失L = (1/(1+λ))[L_R - λ·L_C]。
4. 交替更新策略参数θ（梯度下降）和Lagrange乘子λ（梯度上升），使累计成本逐步收敛到预设阈值b以下。

## 3. 实验设计
### 数据集/场景与基准
- **Safety-CHORES**：论文自建基准，包含三类长时程移动操作任务：
  - Safety-ObjNav：在多个房间中导航到指定物体。
  - Safety-PickUp：在视野内拾取物体。
  - Safety-Fetch：导航+拾取组合任务。
- 场景基于ProcTHOR生成的室内环境（训练/测试比例10:1），模拟器为AI2THOR。
- 额外在iTHOR、ProcTHOR、RoboTHOR等标准基准上测试泛化性。

### 对比方法
- **IL-only**：SPOC（DINOv2、SigLip-S、SigLip-L等变体），含使用地面真值检测信息的变体。
- **IL+RL（标准）**：FLaRe，仅优化任务性能。
- **IL+RL（奖励塑造）**：FLaRe-RS，将安全成本直接惩罚到奖励中。
- **RL-only**：Poliformer（仅适合导航任务）。

## 4. 资源与算力
论文明确说明所有实验在**8张NVIDIA H100 GPU**上进行，使用PyTorch 2.0.1、CUDA 12.2，Ubuntu 20.04.2 LTS。训练步数：Safety-ObjNav和Safety-PickUp为1500万步，Safety-Fetch为2500万步。作者指出更大批量有助于学习，未来可扩展到更多GPU进行分布式训练。

## 5. 实验数量与充分性
实验较为充分，覆盖了以下方面：
- **主要对比实验**：在Safety-CHORES的三个任务上，对比ISA与FLaRe、FLaRe-RS、多种SPOC变体、Poliformer，报告成功率和累计成本。
- **累积成本分布分析**：展示ISA与FLaRe在整个测试集上的成本分布，并分别分析任务成功和失败时的成本。
- **定性分析**：通过轨迹可视化展示ISA对齐与未对齐策略的行为差异。
- **消融实验**：
  - 风险诱发的重要性：移除安全关键组件后性能下降。
  - 成本阈值b的影响（10%、20%、50%）。
  - 固定惩罚系数与动态Lagrange乘子的对比。
- **泛化实验**：
  - 多种VLA模型（EmbCLIP、Embodied-Codebook等）上应用ISA，验证通用性。
  - OOD扰动测试（光照、颜色、材质及组合）下安全性和任务性能保持。
  - 极端失败场景测试（通过设置不可能完成的任务来隔离安全行为）。
- **Sim-to-Real验证**：在真实双机械臂平台上部署Safety-PickUp任务，验证迁移可行性。
- **额外分析**：Logistic回归和相关性检验、每房间成本分布、自动轨迹分析（LLM）、新安全谓词泛化、DivScene零样本泛化、扰动鲁棒性、替代SafeRL算法（PID-Lagrangian、Augmented-Lagrangian）集成等。

实验设计总体客观、公平，对比了多种代表性方法，包括使用特权信息的更强者（如SPOC w/ GT det）。但部分实验（如Sim-to-Real）仅作为概念验证，规模有限。

## 6. 论文的主要结论与发现
- ISA相比最强任务性能基线FLaRe，累计安全成本平均降低83.58%，同时任务成功率提升3.85%。
- ISA消除极端高成本轨迹（成本>10），安全违规严重性上限降低至FLaRe的1/35。
- ISA的安全行为与任务成功解耦：即使任务失败，ISA仍保持低安全成本；而FLaRe在失败时成本显著升高。
- 风险诱发环境（安全关键组件）对于实现优于启发式方法的安全对齐不可或缺。
- 动态Lagrange乘子比固定惩罚系数能更好平衡安全与性能。
- 学习到的安全行为能够泛化到OOD扰动、未见安全谓词、未见场景，且在极端失败下保持安全。
- Sim-to-Real迁移成功，验证了在仿真中学习安全约束并迁移到真实世界的可行性。

## 7. 优点
- **系统性**：首次将SafeRL原理系统性地应用于VLA安全对齐，提出完整ISA框架覆盖建模、诱发、约束、保证四个环节。
- **创新性Benchmark**：Safety-CHORES具有细粒度安全约束、大规模程序化生成场景、长时程任务，能有效暴露VLA漏洞。
- **充分实证**：大量实验(主要对比、消融、泛化、OOD、极端失败、Sim-to-Real)验证方法的有效性和鲁棒性。
- **通用性**：ISA适用于多种VLA基础模型，不受限于特定架构。
- **实际价值**：Sim-to-Real迁移成功，表明方法有落地潜力。

## 8. 不足与局限
- **仿真依赖**：训练和主要评估均在仿真中进行，真实世界验证仅针对简单PickUp任务，尚缺复杂场景、长期部署的物理实验。
- **成本信号设计简化**：轨迹级违规将成本归因于最后一步，忽略中间步骤；成本为二元信号，未考虑严重程度权重（如打碎玻璃与掉落塑料杯后果不同）。
- **约束类型有限**：仅包含五种预设的安全关键组件，可能未覆盖所有实际风险（如人机交互、动态障碍物等）。
- **计算成本较高**：需要大量GPU训练（1500-2500万步），对于资源有限团队可能不易复现。
- **依赖模拟器物理引擎**：模拟与现实之间的动力学差异可能影响迁移效果，文中虽给出策略但未充分量化残留差距。
- **缺乏理论保证**：基于Lagrangian的SafeRL虽有效，但未提供收敛到最优安全策略的严格理论证明。

（完）
