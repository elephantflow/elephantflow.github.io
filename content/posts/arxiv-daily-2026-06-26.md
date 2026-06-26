---
title: "ArXiv 每日精选 · 2026-06-26"
date: 2026-06-27T06:00:00+08:00
draft: false
tags: ["ArXiv", "论文精选", "AI研究", "扩散模型", "世界模型", "视频生成", "具身智能", "生成模型"]
categories: ["ArXiv 每日精选"]
description: "精选 7 篇 ArXiv 最新 AI 论文，涵盖扩散模型、世界模型、视频生成、动作生成、具身AI等核心方向深度分析。"
showToc: true
tocopen: true
---

> 📅 本期精选来自 2026-06-26 ArXiv 最新论文，聚焦扩散模型、世界模型、视频生成、具身AI等核心方向，共 7 篇。

---

## 📄 论文精选

### World Action Models Enable Continual Imitation Learning with Recurrent Generative Replays

**链接：** https://arxiv.org/abs/2606.27374

**一句话总结：** 利用世界动作模型（WAM）的视频生成能力合成伪回放轨迹，实现无需存储历史演示数据的持续机器人模仿学习。

**研究问题：** 持续学习（Continual Learning）中机器人在学习新任务时往往遗忘旧任务（灾难性遗忘），而传统 Experience Replay 方法依赖存储大量历史真实轨迹，存储成本高且隐私风险大。

**核心方法：** 提出 REGEN（Recurrent Generative Replay），利用 World Action Model（WAM）的视频生成能力，在持续适应新任务期间递归地合成伪回放轨迹（pseudo-replay trajectories）。WAM 仅凭借历史任务的语言指令与当前任务观测，即可生成逼真的历史任务演示视频，用于策略排演。

**技术亮点：**
- 零历史数据存储：无需保留任何原始人类演示，靠生成伪轨迹解决遗忘问题
- 递归查询机制：WAM 递归地以前序任务指令为条件生成合成演示，可跨多个任务持续叠加
- 现实瓶颈分析：实验系统地指出了长视野视觉退化与动作-观测不一致性是当前生成回放的主要限制

**实验结果：** 在仿真与真实机械臂操控任务上验证，REGEN 相对顺序微调最多减少 50% 的灾难性遗忘，并接近需要访问真实回放数据的上界方法。

**应用场景：** 机器人持续学习、多任务操控、无数据存储的终身学习系统。

**研究价值：** ⭐⭐⭐⭐⭐（5/5）— 将世界模型与持续学习打通，思路颠覆传统范式；无需历史数据存储这一特性在实际部署中意义重大，且对 WAM 能力边界的分析具有较强指导价值。

---

### Not All Actions Are Equal: Rethinking Conditioning for Dexterous World Model

**链接：** https://arxiv.org/abs/2606.27325

**一句话总结：** 针对高自由度灵巧手操控场景，提出结构化动作条件化框架 DexAC-WM，解决传统世界模型在 high-DoF 控制下动作建模失真问题。

**研究问题：** 现有动作条件化世界模型将整个动作序列压缩为单一表示，在低自由度控制下尚可，但在高自由度（如灵巧手）场景中，不同动作维度的量级差异悬殊，均匀聚合导致优化失衡，细粒度效果难以建模。

**核心方法：** DexAC-WM 将动作条件化重新定义为结构化过程：
- 动作 Tokenization：保留维度级别语义
- 局部精化（local refinement）+ 全局调制（global modulation）：在视觉动态层面对齐动作信号
- 语义分支（semantic branch）：引入丰富的物体-场景先验，辅助世界模型捕捉精细视觉动态

**技术亮点：**
- 明确指出 high-DoF 动作的异质性问题，并从优化角度分析失衡根因
- 结构化动作 Tokenization 保留了维度级别语义，不同关节的运动贡献被正确区分
- 语义分支提供 object-level 先验，弥补现有世界模型语义能力不足

**实验结果：** 在 EgoDex 和 EgoVerse 数据集上，结合语义分支的 DexAC 显著改善 FID、FVD 和 PCK，视觉时序真实性和动作一致性均有提升；DexAC 也在其他骨干网络上验证了可扩展性。

**应用场景：** 灵巧手操控世界模型、高自由度机器人控制、具身智能动作条件化视频预测。

**研究价值：** ⭐⭐⭐⭐⭐（5/5）— 精准定位到 high-DoF 世界模型的核心痛点，结构化动作条件化设计具有较强的通用性，对机器人世界模型研究方向有直接推进作用。

---

### In-Context Model Predictive Generation: Open-Vocabulary Motion Synthesis from Language Models to Physics

**链接：** https://arxiv.org/abs/2606.26981

**一句话总结：** 将 Model Predictive Control 范式引入文本驱动动作生成，通过 LLM 规划与物理仿真反馈的闭环机制，实现语义忠实且物理合理的开放词汇动作合成。

**研究问题：** LLM 驱动的动作生成语义理解强但物理约束违反严重；物理感知模型真实性高但无法处理复杂语义指令和新概念。二者存在根本性的能力鸿沟。

**核心方法：** ICMPG（In-Context Model Predictive Generation）将动作合成重构为 MPC 过程：
- CAMG 模块：LLM 作为规划器，分解文本指令并从动作 token 生成候选动作序列
- MPG 模块：通过物理仿真与语义对齐评估候选，估计复合奖励，选择最优序列指导下一步生成
- 闭环精化：无需任务特定策略重训练即可适应物理环境变化

**技术亮点：**
- 首次将 MPC 的闭环控制逻辑引入动作生成领域，理论框架新颖
- LLM 作为语义规划器，解耦了语义理解与物理可行性评估两个模块
- 支持零样本开放词汇设置，泛化能力强

**实验结果：** 在标准及零样本开放词汇 benchmark 上，ICMPG 相比代表性基线在物理可信度和语义忠实度两项指标上均有明显提升。

**应用场景：** 角色动画、游戏 NPC 动作生成、人形机器人运动规划、影视数字人合成。

**研究价值：** ⭐⭐⭐⭐（4/5）— MPC 与语言驱动动作生成的结合思路新颖；闭环反馈机制理论上可解决 LLM 幻觉导致的物理违反问题，但具体性能增益需进一步量化验证。

---

### DanceOPD: On-Policy Generative Field Distillation

**链接：** https://arxiv.org/abs/2606.27377

**一句话总结：** 提出基于 on-policy 生成场蒸馏的框架 DanceOPD，统一文生图、局部编辑、全局编辑多种能力，解决多能力间的冲突与退化问题。

**研究问题：** 现代图像生成模型需要在单模型中统一 text-to-image、局部编辑和全局编辑等多种能力，但这些能力往往相互冲突——编辑能力会降低 T2I 质量，全局与局部编辑之间也相互干扰。

**核心方法：** DanceOPD 是一个针对 flow-matching 模型的 on-policy 生成场蒸馏框架：
- 将每个能力定义为共享流状态空间上的速度场（velocity field）
- 每个样本被路由到一个能力场，查询 student 自身生成的低噪声状态
- 使用简单 velocity MSE 目标训练，student 在自己的 rollout 状态上向各专家场学习
- 该框架同时可吸收 classifier-free guidance 等算子定义的场

**技术亮点：**
- on-policy 蒸馏设计：student 从自己的轨迹而非 teacher 轨迹学习，分布对齐更准确
- 将 CFG 统一纳入生成场框架，理论自洽
- 多能力组合不互相干扰，各能力的专家质量得到保留

**实验结果：** 在 T2I、编辑、真实感场吸收和 CFG 吸收等任务上全面实验，展示了多能力组合的提升效果。

**应用场景：** 统一图像生成与编辑模型训练、多能力 diffusion 模型蒸馏。

**研究价值：** ⭐⭐⭐⭐（4/5）— 生成场蒸馏框架理论优雅，on-policy 特性是关键创新点；对解决多能力统一模型的"能力冲突"难题提供了新思路。

---

### Don't Settle at the Mode! Mitigating Diversity Collapse in Pretrained Flow Models via Feature Self-Guidance

**链接：** https://arxiv.org/abs/2606.27371

**一句话总结：** 无需额外奖励模型，通过特征自引导（Feature Self-Guidance）机制缓解预训练 flow 模型在同一条件下多次采样时的多样性坍塌问题。

**研究问题：** 最先进的 flow 模型（如 DiT 类文生图模型）在同一条件下批量生成时存在 diversity collapse 现象——样本间相似度过高，缺乏多样性。现有方法要么依赖有限效果的 latent guidance，要么需要外部奖励模型带来大量推理开销。

**核心方法：** 训练无关的 plug-and-play 自引导机制：
- 特征自引导（FSG）：在批量生成时，在 flow 模型内部特征空间中分散各样本的内部表示，鼓励生成多样化
- 流形正则化（Manifold Regularization）：将分散后的特征投影回数据流形，确保多样性提升的同时不偏离条件对齐
- 无需训练，直接插入预训练 flow 模型，额外推理成本极低

**技术亮点：**
- 零训练开销，即插即用
- 流形正则化保证了多样性和保真度的平衡，避免 naive 分散导致的质量下降
- 适用于多步和 few-step 模型，以及 text-to-image、depth-to-image 等多种任务

**实验结果：** 在多个条件 flow 模型上显著提升多样性，同时保持生成保真度；已被 ECCV 2026 接收。

**应用场景：** 创意内容生成、需要多样输出的图像/视频生成应用、flow 模型推理加速配合使用。

**研究价值：** ⭐⭐⭐⭐（4/5）— 即插即用特性使其实用价值极高；diversity collapse 是 flow 模型落地应用中的实际痛点，该方案零训练成本的特点使其极易被业界采纳。已被 ECCV 2026 接收。

---

### ABC: Scalable Behavior Cloning with Open Data, Training, and Evaluation

**链接：** https://arxiv.org/abs/2606.27375

**一句话总结：** 发布迄今最大开源机器人遥操作数据集 ABC-130K（3500 小时，130K episodes，195 任务），并提供完整开源训练与评估栈，系统比较 DiT 和 VLA 模型的设计选择。

**研究问题：** 机器人操控领域缺乏大规模、多样化的开源训练数据，且不同模型架构（DiT vs VLA）的系统性比较研究缺失，导致社区难以高效推进。

**核心方法：** ABC 开源栈包含：
- ABC-130K：3500 小时遥操作数据，130K episodes，195 个多样化任务
- 仿真遥操作数据（400 小时）+ sim-to-real 协同训练方案
- 完整训练基础设施 + 仿真评估流水线
- 系统比较 Diffusion Transformer（DiT）与 Vision-Language-Action（VLA）多种架构和训练策略

**技术亮点：**
- 数据规模为现有开源数据集中最大，显著填补社区空白
- sim-to-real 联合训练方案提供可靠的仿真-真实相关性，降低昂贵真实评估需求
- Pieter Abbeel、Jitendra Malik、Angjoo Kanazawa 等顶尖研究者参与

**实验结果：** 通过大规模消融实验系统比较了各种架构选择；仿真评估结果与真实机器人评估高度相关，验证了替代评估可靠性。

**应用场景：** 机器人操控基础模型预训练、行为克隆研究、sim-to-real 迁移基准。

**研究价值：** ⭐⭐⭐⭐（4/5）— 大规模开源数据集对整个具身智能社区的研究加速意义重大，有望成为领域标准 benchmark；系统化的架构比较研究也为后续工作提供清晰的参考基线。

---

### RayPE: Ray-Space Positional Encoding for 3D-Aware Video Generation

**链接：** https://arxiv.org/abs/2606.27345

**一句话总结：** 提出 RayPE，将 6D Plücker 坐标作为位置编码注入视频 DiT 的注意力机制，仅增加 <0.1% 参数即可显著提升视频生成的相机可控性与跨帧 3D 一致性。

**研究问题：** 现代视频 Diffusion Transformer 使用 (u,v,t) 轴上的 RoPE 进行 token 位置编码，这种描述方式对 3D 场景结构一无所知，导致生成视频中相机控制精度差、跨帧 3D 一致性不足。

**核心方法：** RayPE 将 6D Plücker 坐标加性注入到 self-attention 的 queries 和 keys 中：
- 利用 Plücker 互积与 Transformer 注意力的 dot product 在代数形式上的同构性
- Query/key flip 排布确保对称身份配置与互积精确重合
- 加性注入使注意力分数可分解为内容项、几何项及交叉项——实验证明各项均必要
- 针对异质相机平移尺度（SfM、深度 SLAM、metric），解耦 ray 方向与 moment 幅度，用 learned 函数对 log-magnitude 门控，并用 RMSNorm 对齐内容分支

**技术亮点：**
- 优雅利用 Plücker 几何与注意力机制的代数同构，理论基础扎实
- Zero-initialization 确保从预训练权重出发，零 degradation 起步
- 参数量增加 <0.1%，实用性极强

**实验结果：** 在四数据集混合训练上改善相机可控性、跨帧 3D 一致性和整体视频质量。

**应用场景：** 相机轨迹可控视频生成、3D 一致性视频生成、世界模型中的多视角场景生成。

**研究价值：** ⭐⭐⭐⭐（4/5）— Plücker 几何与视频 DiT 位置编码的结合是真正的方法创新，且实现代价极低（<0.1%参数），对视频生成领域的相机控制问题提供了优雅解法。

---

## 📊 今日研究趋势

2026-06-26 的 ArXiv 呈现出几个鲜明趋势。**世界模型与机器人的深度融合**是当天最突出的主题——REGEN 和 DexAC-WM 分别从持续学习和高自由度动作建模两个维度推进了世界模型在具身智能中的应用，预示着世界模型正从"视频预测"向"机器人基础设施"方向演进。**视频生成的 3D 感知**方向也持续升温，RayPE 尝试将显式几何先验（Plücker 几何）注入生成模型，代表了该领域的一种理论驱动路线。**统一多模态模型（Unified LMM）**的热度依然不减，多篇论文（REGEN 的前置 WAM、DanceOPD、ABC）都涉及理解与生成统一建模。**数据规模化**方向（ABC-130K）也显示出具身智能领域开始进入大数据飞轮阶段。整体来看，今日论文质量普遍较高，cs.RO 与 cs.CV 跨领域交叉成果尤为集中。

---

## 🏆 最值得关注的 3 篇

1. **World Action Models Enable Continual Imitation Learning with Recurrent Generative Replays** — 世界模型的生成能力被创造性地用于解决持续学习中的灾难性遗忘，零存储演示的设计彻底改变了机器人学习范式，是世界模型走向实用化的重要一步。

2. **Not All Actions Are Equal: Rethinking Conditioning for Dexterous World Model** — 精准定位 high-DoF 世界模型的核心瓶颈，结构化动作条件化设计对灵巧操控世界模型研究具有直接指导价值，方法设计简洁有力。

3. **RayPE: Ray-Space Positional Encoding for 3D-Aware Video Generation** — 将 Plücker 几何与视频 DiT 优雅融合，仅 <0.1% 参数开销即可显著提升相机可控性，理论扎实、代价极低，有望成为视频生成模型的标准组件。

---

*数据来源：ArXiv 2026-06-26 | 分析生成时间：2026-06-27 06:00 (北京时间)*
