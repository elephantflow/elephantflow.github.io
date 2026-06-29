---
title: "ArXiv 每日精选 · 2026-06-29"
date: 2026-06-30T06:00:00+08:00
draft: false
tags: ["ArXiv", "论文精选", "AI研究", "扩散模型", "世界模型", "视频生成", "具身智能", "机器人"]
categories: ["ArXiv 每日精选"]
description: "精选 7 篇 ArXiv 最新 AI 论文，涵盖扩散模型、世界模型、视频生成、具身AI等核心方向深度分析。"
showToc: true
tocopen: true
---

> 📅 本期精选来自 2026-06-29 ArXiv 最新论文，聚焦扩散模型、世界模型、视频生成、具身AI等核心方向，共 7 篇。

---

## 📄 论文精选

### TempAct: Advancing Temporal Plausibility in Autoregressive Video Generation via Planner-Executor RL

**链接：** https://arxiv.org/abs/2606.28016

**一句话总结：** 提出 Planner-Executor 强化学习框架，解决自回归视频扩散模型中 chunk-wise 生成的时序指令跟随问题，显著提升长视频的时间一致性。

**研究问题：** 自回归（AR）视频扩散模型以分块方式逐段生成视频，但全局文本 prompt 无法精确指定每个 chunk 应实现的子事件，导致延迟反应、语义混合以及跨 prompt 转换时的误差累积——这些问题用 SFT 或蒸馏方法难以有效解决。

**核心方法：** TempAct 引入双层 RL 框架：LLM Planner 探索 span-aware 的逐步 prompt，AR 扩散 Executor 在自身生成历史下学习遵循这些 prompt。关键机制是分层群组探索（hierarchical group exploration）：候选计划构成规划组，每个计划在共享视觉上下文下产生执行组，实现计划级和执行器级的信用分配。

**技术亮点：**
- 分层奖励设计：Planner 获得计划质量和全视频时序反馈，Executor 获得转换级步骤跟随奖励、美学正则化和 KL 约束
- 层次化群组探索机制，支持长视程时序结果的信用分配
- 基于 Self-Forcing 和 LongLive 两种 AR 视频框架验证，在保持视觉质量的同时提升时序一致性

**实验结果：** 在 Self-Forcing 和 LongLive 两个 AR 视频生成基线上验证，时序一致性显著改善，视觉质量不降。

**应用场景：** 长视频生成、文本驱动视频创作、视频世界模型的时序规划控制。

**研究价值：** ⭐⭐⭐⭐⭐（5/5）— 将 RL 引入 AR 视频生成的时序规划，解决的是 chunk-wise 扩散模型的核心痛点，方法新颖，对视频生成和世界模型研究均有直接意义。

---

### PhysisForcing: Physics Reinforced World Simulator for Robotic Manipulation

**链接：** https://arxiv.org/abs/2606.28128

**一句话总结：** 提出 PhysisForcing 训练框架，通过像素级轨迹对齐和语义关系对齐两项损失，强化视频生成模型中物理一致性，使其作为机器人操作世界模拟器更可靠。

**研究问题：** 视频生成模型作为具身世界模拟器时，普遍存在物理不合理现象（运动轨迹不连续、机器人-物体接触时空关系异常），限制了其作为机器人训练数据源的可靠性。

**核心方法：** 通过大量实验定位物理不一致的两大根源：运动物体形变和接触区域的时空关联不合理。PhysisForcing 提出可扩展训练框架，在物理信息密集区域聚焦监督：（1）像素级轨迹对齐损失——利用参考点轨迹监督 DiT 特征；（2）语义级关系对齐损失——对齐 DiT 特征以保持接触实体间的时空关联一致性。

**技术亮点：**
- 精准定位视频生成物理失真的两大根源，提供可解释的改进路径
- 联合优化像素级和语义级特征，双重监督互补
- 框架可扩展，适配 DiT 架构的视频生成模型（如 Wan2.1 等）
- 作者包含 NVIDIA Ming-Yu Liu 和 Enze Xie，团队背景强

**实验结果：** 在机器人操作视频生成任务上，物理一致性（轨迹连续性、接触合理性）显著优于基线；定量评估覆盖物理合理性专项指标。

**应用场景：** 机器人操作视频生成、合成训练数据生成、具身 AI 世界模型构建。

**研究价值：** ⭐⭐⭐⭐⭐（5/5）— 精准攻击视频生成模型在机器人场景中最核心的物理不一致问题，方法可解释、可扩展，对世界模型和具身AI方向有直接推动价值。

---

### DEFAR: Exposure Bias Can Alleviate Itself via Directional and Frequency Rectification in Flow Matching

**链接：** https://arxiv.org/abs/2606.28226

**一句话总结：** 发现 Flow Matching 中 exposure bias 本身携带可用于自矫正的动态信号，提出 DEFAR 框架通过方向性和频率自适应反馈实现 bias 的自我修复。

**研究问题：** Flow Matching 在训练与推理间存在分布偏差（exposure bias），现有缓解方案依赖静态约束或外部启发式方法，未能充分利用 bias 本身携带的信息。

**核心方法：** DEFAR（DirEctional-Frequency Adaptive Rectification）框架包含两个核心组件：（1）Anti-Drift Rectification（ADR）——在训练时模拟单步推理过程识别 bias，将推理时的漂移视为信号学习方向性矫正，赋予模型主动自矫正能力；（2）Frequency Compensation（FC）——观察到高噪声阶段累积 bias 源于低频成分缺失，利用 bias 本身作为自反馈权重因子补偿缺失频率。

**技术亮点：**
- 核心洞见：exposure bias 不仅是噪声，而是包含可利用的动态矫正信号
- 无需外部数据或额外模型，完全自监督方式实现 bias 矫正
- 方向性和频率双维度互补覆盖 bias 的不同表现
- 理论上适用于所有 Flow Matching 模型，泛化性强

**实验结果：** 在图像/视频生成标准 benchmark 上，生成质量（FID/FVD）相比基线 Flow Matching 模型有明显提升；频率分析实验验证了低频补偿的有效性。

**应用场景：** 图像生成、视频生成、任意基于 Flow Matching 的生成模型推理优化。

**研究价值：** ⭐⭐⭐⭐（4/5）— 对 Flow Matching 训练-推理一致性问题提出了优雅的自反馈解决方案，理论分析深入，但最终效果增益大小仍依赖具体模型规模和任务。

---

### RS-Diffuser: Risk-Sensitive Diffusion Planning with Distributional Value Guidance

**链接：** https://arxiv.org/abs/2606.27766

**一句话总结：** 提出 RS-Diffuser，将分布式值函数批评家引入扩散规划框架，实现推理时可灵活调控风险偏好的离线 RL 决策，同时提升平均收益和最坏情况鲁棒性。

**研究问题：** 现有扩散规划方法（如 Diffuser）是风险中性的，无法感知极端坏结果，在安全关键的机器人导航等任务中存在隐患。

**核心方法：** RS-Diffuser 由三部分组成：（1）扩散规划器——生成未来状态轨迹的多模态分布；（2）独立逆动力学模型——从轨迹解码动作；（3）Monte Carlo 分布式批评家——通过分位数回归估计候选轨迹的完整回报分布。在去噪采样时，利用 CVaR（条件风险价值）等尾部感知目标的梯度作为风险敏感引导信号，无需重新训练即可通过调整推理时风险参数切换风险规避/中性/偏好行为。

**技术亮点：**
- 单一训练模型，推理时通过风险参数灵活控制行为模式
- 分布式批评家捕捉完整回报分布（不仅均值），从而能够评估尾部风险
- CVaR 引导与扩散去噪过程的优雅结合
- ICIC 2026 Oral，同时适用于安全机器人导航和标准 D4RL 任务

**实验结果：** 在风险敏感 D4RL 和危险机器人导航 benchmark 上达到 SOTA，在提升整体收益的同时显著降低安全违规率，最坏情况性能明显优于风险中性基线。

**应用场景：** 安全关键机器人导航、离线 RL 决策、自动驾驶轨迹规划。

**研究价值：** ⭐⭐⭐⭐（4/5）— 扩散规划遇上分布式 RL，解决了实际部署中不可忽视的风险敏感性问题，方法简洁而有效，对 Embodied AI 安全性研究有参考价值。

---

### EMOSH: Expressive Motion and Shape Disentanglement for Human Animation

**链接：** https://arxiv.org/abs/2606.28026

**一句话总结：** 提出 EMOSH 框架，通过显式解耦人体形状与运动参数，从根本上消除驱动主体体型泄露问题，实现高保真的表情-动作-身份三维一致可控人体视频生成（ECCV 2026）。

**研究问题：** 可控人体动画面临"运动-形状纠缠"难题：2D pose 驱动方法导致驱动主体体型泄露，而依赖 SMPL 等 3D 先验的方法难以捕捉表情和复杂手势，生成结果僵硬。

**核心方法：** EMOSH 提出三个核心设计：（1）Expressive Human Model（EHM）——显式分离形状和姿态参数的控制表示，配合鲁棒运动追踪器从视频估计 EHM 参数；（2）Coarse-to-Fine Hybrid Motion Injection——渐进注入策略实现对表情和手势的细粒度控制；（3）Spatially-Aligned Conditioning——空间对齐条件化机制，弥合训练-推理域差距，提升身份一致性。

**技术亮点：**
- 首次在单一框架内同时解决体型泄露、表情精度和手势控制三大难题
- EHM 作为统一控制表示，兼具 3D 几何精度和 2D 表达力
- 空间对齐条件化有效缓解训练-推理分布偏差
- ECCV 2026 收录，自驱和跨人驱动场景均有强表现

**实验结果：** 在自驱（self-driven）和跨人驱动（cross-driven）场景均优于现有方法，身份保持、表情真实度和体型一致性均有量化提升。

**应用场景：** 数字虚拟人动画、影视内容制作、AR/VR 化身、人体行为数据增强。

**研究价值：** ⭐⭐⭐⭐（4/5）— 将运动生成和视频生成的核心挑战（形状-运动解耦）推进到新水平，EHM 表示设计有独到之处，但泛化到极端体型或遮挡场景的能力仍待评估。

---

### LLawCo: Learning Laws of Cooperation for Modeling Embodied Multi-Agent Behavior

**链接：** https://arxiv.org/abs/2606.28182

**一句话总结：** 提出 LLawCo 框架，让具身智能体从历史失败中提炼高层行为法则（如"必要时才交流"），通过 SFT 内化到推理链中，显著提升去中心化多智能体协作效率（ICML 2026）。

**研究问题：** 基于 LLM 的具身智能体在去中心化、部分可观测环境中协作时，行为常与伙伴或任务目标不对齐，导致低效协作和任务失败。

**核心方法：** LLawCo 包含两个关键步骤：（1）反思失败——从历史失败轨迹中提取不对齐的行为模式；（2）法则推导——将这些模式上升为高层行为法则（如"Talk when necessary"、"Wait for partner"），通过 SFT 显式嵌入智能体的思维链，对齐其推理与任务需求及伙伴行为。同时引入 PARTNR-Dialog 大规模多智能体通信协作规划 benchmark。

**技术亮点：**
- 从失败中自动提炼可解释的高层行为法则，无需人工设计规则
- 法则以自然语言形式嵌入 CoT，可解释且可迁移
- PARTNR-Dialog 新 benchmark 覆盖通信+协作双重维度
- 跨 4 种 LLM backbone 均有稳定提升，方法鲁棒性强

**实验结果：** 在 PARTNR-Dialog（+4.5%）和 TDW-MAT（+6.8%）benchmark 上，相比 SOTA 开源通信智能体框架取得平均成功率提升，跨 4 种 LLM backbone 一致性强。ICML 2026 收录。

**应用场景：** 多机器人协作任务、具身多智能体系统、家庭服务机器人、协作任务规划。

**研究价值：** ⭐⭐⭐⭐（4/5）— 将"从失败中学习"的思路延伸到多智能体行为对齐，法则提炼机制新颖，新 benchmark 对领域有贡献，但法则的自动提炼质量对下游性能影响的分析仍可深化。

---

### StructSplat: Generalizable 3D Gaussian Splatting from Uncalibrated Sparse Views

**链接：** https://arxiv.org/abs/2606.28321

**一句话总结：** 提出 StructSplat，无需相机参数的前馈式可泛化 3D Gaussian 重建框架，在 DL3DV 上以 28.045 PSNR 大幅超越 AnySplat（+5.67 dB），跨数据集泛化性能同样显著领先。

**研究问题：** 现有可泛化 3D Gaussian 方法或依赖已知相机姿态，或在单一骨干网络中混合几何与外观建模，限制了重建保真度和泛化能力。

**核心方法：** StructSplat 采用结构化表示，将几何、语义、纹理线索赋予明确角色：（1）像素对齐特征注入机制——从 2D 观测精确建模纹理；（2）语义感知先验——提升全局一致性；（3）相机对齐策略——防止信息泄露，提升跨场景泛化。整个框架为 feed-forward，无需每场景优化，也无需相机参数输入。

**技术亮点：**
- 无需相机标定即可重建高质量 3D Gaussian，极大降低使用门槛
- 结构化解耦设计（几何/语义/纹理各司其职）比端到端单骨干更有效
- 跨数据集泛化能力突出：ACID +1.94 dB、RealEstate10K +1.72 dB over AnySplat
- 代码已开源

**实验结果：** DL3DV 上 PSNR 28.045（AnySplat 22.377，+5.67 dB），ACID +1.94 dB，RealEstate10K +1.72 dB，跨数据集全面领先当前 SOTA。

**应用场景：** 从野外图片快速 3D 重建、AR/VR 场景生成、机器人环境感知、具身AI场景理解。

**研究价值：** ⭐⭐⭐⭐（4/5）— 无相机参数约束下的大幅 PSNR 提升令人信服，结构化表示的设计哲学有一定启发性；但泛化至室外大场景或极稀疏视图（<3 帧）的鲁棒性仍是开放问题。

---

## 📊 今日研究趋势

2026-06-29 ArXiv AI 领域呈现多条活跃研究线索：**视频生成与时序控制**持续升温，TempAct 展示了将 RL 引入 AR 视频扩散的新范式，预示着视频生成向长时程、可控方向演进；**世界模型与具身AI**交叉方向强势，PhysisForcing 专注物理一致性、ReScene 关注场景重建、LLawCo 攻坚多智能体协作，形成从感知到规划的完整技术栈；**扩散模型理论**方面，DEFAR 对 Flow Matching exposure bias 的深度分析和 RS-Diffuser 对风险敏感规划的探索，反映了社区对生成模型可靠性和安全性的关注；**3D 生成**方向 StructSplat 的突破性 PSNR 提升显示 feed-forward Gaussian Splatting 仍有巨大空间。整体来看，今日论文质量较高，ECCV 2026、ICML 2026 收录论文集中出现，是重要会议论文提前公开的一批。

---

## 🏆 最值得关注的 3 篇

1. **TempAct** — 首次将 Planner-Executor RL 引入 AR 视频扩散模型，精准解决 chunk-wise 生成的时序一致性难题，对视频生成和世界模型研究方向均有重要参考价值。
2. **PhysisForcing** — 物理增强的机器人操作世界模拟器，从根源定位视频生成物理失真，双重对齐损失设计简洁有效，是具身AI数据飞轮的关键基础设施。
3. **StructSplat** — 无相机参数 3D Gaussian 重建实现 +5.67 dB PSNR 的大幅超越，跨数据集一致领先，feed-forward 范式进一步降低 3D 生成门槛。

---

*数据来源：ArXiv 2026-06-29 | 分析生成时间：2026-06-30 06:00 (北京时间)*
