---
title: Fully Autonomous Neuromorphic Navigation and Dynamic Obstacle Avoidance
title_zh: 全自主神经形态导航与动态避障
authors: "Xiaochen Shang, Luo Pengwei, Xinning Wang, Jiayue Zhao, Huilin Ge, Bo Dong, Xin Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=11fe8wKkmk"
tags: ["query:safe-rl-cbf"]
score: 4.0
evidence: 无人机神经形态导航与动态避障
tldr: 针对无人机依赖外部控制实现导航与避障的局限，提出全神经形态框架，利用事件相机和脉冲神经网络实现端到端动态避障，延迟仅2.3毫秒，无需目标识别和轨迹计算，在真实环境中验证了自主避障能力。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-11fe8wkkmk/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1382, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-11fe8wkkmk/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1362, \"height\": 769, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-11fe8wkkmk/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1414, \"height\": 875, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-11fe8wkkmk/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1439, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-11fe8wkkmk/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 592, \"height\": 340, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-11fe8wkkmk/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1264, \"height\": 573, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-11fe8wkkmk/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 864, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-11fe8wkkmk/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 938, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-11fe8wkkmk/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 771, \"height\": 263, \"label\": \"Table\"}]"
motivation: 无人机在机载计算和感知下实现实时导航与动态避障面临延迟和能耗挑战。
method: 提出全神经形态框架，结合脉冲神经网络和事件相机实现端到端避障。
result: 实现了2.3毫秒的低延迟动态避障，无需目标识别。
conclusion: 为无人机自主导航提供了一种高效仿生解决方案。
---

## Abstract
Unmanned aerial vehicles could accurately accomplish complex navigation and obstacle avoidance tasks under external control. However, enabling unmanned aerial vehicles (UAVs) to rely solely on onboard computation and sensing for real-time navigation and dynamic obstacle avoidance remains a significant challenge due to stringent latency and energy constraints. Inspired by the efficiency of biological systems, we propose a fully neuromorphic framework achieving end-to-end obstacle avoidance during navigation with an overall latency of just 2.3 milliseconds. Specifically, our bio-inspired approach enables accurate moving object detection and avoidance without requiring target recognition or trajectory computation. Additionally, we introduce the first monocular event-based pose correction dataset with over 50,000 paired and labeled event streams. We validate our system on an autonomous quadrotor using only onboard resources, demonstrating reliable navigation and avoidance of diverse obstacles moving at speeds up to 10 m/s.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
当前无人机（UAV）在执行复杂导航与动态避障任务时，通常依赖外部辅助（如GPS、地面站）或高功耗传感器（如LiDAR），这使得无人机在GPS拒止环境（如城市峡谷、洞穴、战场）中难以实现完全自主。此外，传统视觉方法（如SLAM、基于目标识别的轨迹估计）计算和内存开销巨大（数百MB至数GB、数百GFLOPs），不适合小型无人机机载平台。本文受生物系统（尤其是青蛙视觉系统）高效处理动态信息的启发，提出了一种**全神经形态框架**，仅依靠机载资源（一个单目事件相机和一个惯性测量单元IMU）实现实时导航与动态避障，延迟仅2.3毫秒，且无需目标识别和轨迹计算。该工作旨在突破小型无人机自主飞行的能耗与延迟瓶颈。

## 2. 方法论：核心思想与关键技术细节

### 2.1 整体架构
- 框架部署在 **Speck 神经形态 SoC** 上（具有327,000个神经元，最多支持8层SNN），组成一个小型四旋翼无人机（总重856g，直径240mm）。
- 任务分为两个阶段：
  - **出航飞行**：可手动或任意控制，同时记录IMU数据和事件流（用于后续归航）。
  - **归航飞行**：完全自主，使用IMU信息进行里程计导航，并在飞行中执行动态避障；同时周期性地通过**事件视觉归航算法**校正IMU漂移误差。

### 2.2 视觉归航导航
- **问题**：IMU误差随时间呈近似三次方漂移（公式1给出误差传播模型）。
- **方案**：采用 **视觉归航（Visual-homing）** 思想，模仿蜜蜂回巢行为。无人机在出航时定期在**快照点**记录事件流（每7.5米一个快照，每个240KB）。归航时，利用脉冲卷积神经网络（SCNN）的孪生结构（Siamese Network）比较当前事件流与存储的快照事件流，输出相对位置偏移（Δx, Δy, Δyaw），从而校正IMU漂移误差。
- **数据集**：首次构建**单目事件相机位姿校正数据集**，包含50,234对事件流，每对精确标注4自由度相对位姿（Δx, Δy, Δz, Δϕ）。数据采集使用DJI Ronin SC稳定云台（俯仰滚转误差±0.02°）和Vicon Vero 2.2动作捕捉系统（12个相机，2048×1088分辨率，330Hz）。四个室内场景，最大物距10m。

### 2.3 动态避障算法——生物启发的事件感受野模型
- **生物原理**：青蛙视网膜R3神经节细胞对运动物体敏感，对静止背景抑制。其感受野包含**兴奋性感受野（ERF）**和**抑制性感受野（IRF）**，且二者存在空间不对称性。
- **数学模型**：
  - 事件感受野模型（Event RF）公式（2）：
    \[
    F(x,y,e_n,t) = \min(A_1 K(t,\tau_e)G(x,y,e_n), E_{\text{th}}) - \min(A_2 K(t-\Delta t,\tau_i)G(x,y,e_n), I_{\text{th}})
    \]
  - 其中 \(K(t,\tau)=e^{-t/\tau}\) 为时间核函数，\(G\) 为二维椭圆高斯核（公式4）。ERF项增强动态事件，IRF项抑制静态事件。关键参数：ERF/IRF幅度比 \(A_1/A_2\)，延迟 \(\Delta t\)，时间常数 \(\tau_e, \tau_i\)，阈值 \(E_{\text{th}}, I_{\text{th}}\)，高斯标准差 \(\sigma_x, \sigma_y\)。
- **避障命令生成**：将RF模型输出的能量图转化为势场图，通过梯度下降生成运动指令；使用二值化、连通域检测和膨胀操作评估障碍物危险程度，产生逃避机动。

### 2.4 计算流程总结
- 全程数据流：事件相机→Speck SoC上的SCNN归航校正 + Event RF模型避障 → 输出平移和偏航指令 → 飞行控制器（Pixhawk）。
- 整个避障流水线延迟仅2.3毫秒。

## 3. 实验设计

### 3.1 数据集与场景
- **仿真实验**：Gazebo仿真环境，使用ESIM事件相机模拟器。构建三个难度递增的自定义地图（飞行距离40米至130米）。动态障碍物分为三种大小：硬币大小、网球大小、篮球大小；距离范围：0.2m以内（排除）、0.2-0.5m、0.5-1m、1-2m、2m以上。
- **真实世界实验**：
  - 室内实验：10m×10m飞行场地，三名实验人员投掷动态障碍物（如网球）。10次重复实验。
  - 复杂环境实验：室外广场（含静态箱子）和室内办公走廊，测试三种动态障碍物（投掷物、稀疏人群、密集人群）。
  - 极端光照实验：光照条件包括亮（10-100 lux）、闪烁（1-100 lux）、暗（1-10 lux）、极暗（0-1 lux）。

### 3.2 对比方法（Benchmark）
- 对比四种现有方法（表3）：
  - 方法1 [64]：基于RGB-D的检测跟踪，延迟19.12ms，位置误差0.11m，成功率96.3%。
  - 方法2 [13]：RGB-D实时跟踪，延迟39.49ms，位置误差0.11m，成功率89.1%。
  - 方法3 [26]：事件相机避障（无导航模块），延迟3.56ms，位置误差0.09m，成功率86.7%。
  - 方法4 [65]：LiDAR方法（GTX4090延迟14ms，机载延迟27ms），成功率95.75% / 86.5%。
- 本文方法：延迟2.34ms，位置误差0.02m，成功率94.5%。

### 3.3 消融与参数分析
- 对Event RF模型参数（\(A_1/A_2, \tau_e/\tau_i, \Delta t, \sigma, E_{\text{th}}/I_{\text{th}}\)）进行系统分析，在仿真中测试不同参数对低速/高速/超高速障碍物的成功率（表4）。
- 组合任务实验：在三个地图上各进行50次测试，成功率分别为100%、98%、94%。

## 4. 资源与算力
- **硬件平台**：Speck神经形态SoC（327K神经元，支持最多8层SNN）。机载计算机为Raspberry Pi或类似低功耗主板（未明确型号），配合Pixhawk飞行控制器。
- **训练算力**：文中未明确说明GPU型号、数量或训练时长。仅提到“训练细节见补充材料”，但主体文本未提及。因此**关键算力信息缺失**。
- **能耗对比**：神经形态芯片功耗比传统设备降低两个数量级；整个系统能耗降至传统架构的21%。主要能耗来自机载计算机操作、芯片与飞控的数据交换以及运动指令执行。

## 5. 实验数量与充分性
- **仿真实验**：
  - 归航导航：每个地图10次测试，全部成功。
  - 动态避障：300次测试（3种障碍物大小×4个距离段×25次）。
  - 组合任务：每个地图50次，总计150次。
- **真实实验**：
  - 室内：10次重复测试，全部成功。
  - 复杂环境：室外和走廊各测试多种障碍物（成功率表格给出，每项约30-50次？未精确说明）。
  - 极端光照：测试四种光照条件，仅极暗失败，其余表现稳定。
- **对比实验**：使用官方代码在相同仿真环境下复现对比方法（表3）。
- **总体评价**：实验数量充足，覆盖仿真和真实场景，包含消融分析和参数敏感性分析，对比方法公平。但真实环境实验次数较少（特别是复杂环境未给出具体次数），且部分结果缺少统计误差棒（除表1外）。

## 6. 主要结论与发现
1. 提出的全神经形态框架首次实现了无人机仅依靠机载计算和感知完成长距离导航与高速动态避障（障碍物速度最高10m/s），避障延迟仅2.3毫秒，较现有方法降低88.6%。
2. 生物启发的事件RF模型成功实现无需目标识别和轨迹计算的动态障碍物检测与躲避，性能接近甚至超过传统方法（成功率94.5% vs 最佳96.3%）。
3. 能耗显著降低：神经形态系统能耗仅为传统架构的21%。
4. 新构建的单目事件相机位姿校正数据集（50,234对事件流）为后续研究提供基准。
5. 框架在多种光照条件下表现鲁棒，仅在极暗（0-1 lux）下失效。

## 7. 优点
- **创新性**：首次将全神经形态流水线（感-算-控）用于无人机复杂导航与避障，不依赖外部基础设施。
- **生物启发算法**：Event RF模型直观简洁，通过数学模拟青蛙视网膜感受野实现动态/静态选择，绕过传统目标检测步骤，极大降低延迟。
- **数据集贡献**：首个大规模、标注精确的事件相机位姿校正数据集，推动事件相机在视觉归航方向的研究。
- **低延迟高成功率**：2.3ms延迟为无人机提供更长反应时间窗口，在高速障碍物场景下表现出显著优势。
- **实际部署验证**：在真实飞行中成功规避抛掷物，并在多种环境（室内外、不同光照）中验证鲁棒性。
- **开源承诺**：作者承诺论文接收后开源代码和数据集。

## 8. 不足与局限
- **单目深度缺失**：使用单目事件相机无法获取深度信息，导致远近障碍物在势场中危险程度相同，可能引发不必要的避障或误判。作者已将此列为未来工作。
- **依赖IMU归航**：导航基本依靠IMU，虽可周期校正，但在长时无校正段（如校正间隔7.5m内）仍需IMU积分，若环境发生动态变化（如快照点场景被遮挡）或IMU突然失效，则鲁棒性存疑。
- **数据集局限**：数据集仅涵盖室内环境（最大10m），且场景结构较为单一（四个室内场景）。是否适用于室外大尺度环境未见验证。
- **真实实验覆盖不足**：复杂环境实验（室外广场、办公走廊）未详细给出实验次数和统计误差，且密集人群场景成功率仅约55-62%，性能显著下降，说明算法在人流密集场景下不够鲁棒。
- **极端光照测试不完整**：仅在暗（1-10 lux）下成功，极暗（0-1 lux）失败，但未说明是否使用红外补光或其他措施。
- **对比实验偏差**：对比的方法中，方法3 [26] 仅做避障不含导航，而本文是导航+避障联合任务，资源分配不同，直接比较避障延迟可能不够公平。但作者也指出了这一点。
- **未知训练算力**：未提供训练SCNN所需的GPU型号、数量、时间，影响复现性评估。
- **硬件限制**：Speck芯片仅327K神经元，限制网络复杂度（最多8层SNN），未来更复杂任务可能超出硬件能力。

（完）
