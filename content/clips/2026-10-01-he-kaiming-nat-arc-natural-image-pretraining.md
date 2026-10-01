---
title: "何恺明团队新作：看猫片就能学会 ARC 挑战"
slug: "he-kaiming-nat-arc-natural-image-pretraining"
date: 2026-10-01T09:00:00+08:00
draft: false
tags: ["何恺明", "NAT-ARC", "VARC", "ARC", "ARC-AGI", "MAE", "量子位（ID：QbitAI）", "剪藏"]
categories: ["世界模型与具身智能"]
description: "何恺明团队（MIT CSAIL，一作 Xiaoman Delores Ding，也是 CVPR 2026 的 VARC 一作）新论文 NAT-ARC（*Natural Image Pretraining Improves Abstract Reasoning*，ECCV 2026）在 VARC…"
showToc: false
---

> **来源**：量子位（ID：QbitAI）（克雷西 发自 凹非寺） · 2026-10-01 · [原文链接](https://mp.weixin.qq.com/s/IQH3easn93wPN_cXtbUzMw)

> **分类**：主线强相关（表面上是一篇 ARC 刷榜稿，真正值钱的是两件事：①「没有预训练时模型越大反而越差」这条小数据下的 scaling 负收益诊断；②自然图像上学到的前景/背景分离与连通区域能力能零成本迁移到完全非自然的离散格子——这两条直接打到触觉「没有 ImageNet」这个缺口上）

---

## 一句话概括

何恺明团队（MIT CSAIL，一作 Xiaoman Delores Ding，也是 CVPR 2026 的 VARC 一作）新论文 **NAT-ARC**（*Natural Image Pretraining Improves Abstract Reasoning*，ECCV 2026）在 VARC 的纯视觉流程前面插了一步 **ImageNet MAE 预训练**，直接沿用公开 checkpoint、零额外预训练成本，让在猫狗花草上学到的视觉表征迁移到抽象彩色格子推理上：**ARC-1 pass@2 单模型 63.4%（huge，6.6 亿参数），三路集成 70.2%**，逼近 8B 专用 LLM 系统 The ARChitects 的 71.6%。**但我读完整篇 + 回论文表后，这篇中文稿有两个必须打的折：① ARC-2 上只有单模型 8.6% / 集成 13.1%，中文稿一个字没提，标题「就能学会 ARC 挑战」严重夸大；② 70.2% 的集成里包含用 RE-ARC 40 万对 + NVARC 150 万对合成数据做的「ARC 风格格子 MAE 预训练」那一路，并不全是「看猫片」的功劳。真正让我留下这篇的是另外一条：没有预训练时模型从 large 到 huge 反而掉点，加上预训练后三个尺度才单调上升——这是小数据任务上「容量增长先带来过拟合」的直接诊断，而触觉恰好就是这样一个小数据、且连个 ImageNet 都没有的模态。**

## 核心要点



## 金句

> 视觉路线依然有一个结构性短板：多数视觉 ARC 方案的模型从随机初始化开始训练，没有吃到预训练的红利。

> 没有预训练时，模型从 base 到 large 性能还能涨，但从 large 到 huge 反而掉点了。模型变大，效果变差，这在深度学习里不是常见现象。

> 在 ImageNet 上看猫学到的「把猫从草地背景里分出来」，到了 ARC 里变成了「把这块连通的彩色区域从格子里认出来」。

> 从猫猫中来，到猫猫中去。

## 质疑与核查

**1. ⭐ 标题"看猫片就能学会 ARC 挑战"夸大，ARC-2 数字被完全略去。** 论文表 2 明写 ARC-2 单模型 8.6±0.8%、集成 13.1±0.7%。ARC-2 才是当前真正的难点，且在 ARC-1 上人类平均 60.2%、Gemini 3 Pro 98.0%——"逼近 LLM 水平"只在"ARC 专用微调 LLM 系统"这个窄口径下成立，离通用前沿模型差近 28 个点。**读这篇时不要把 70.2% 当成通用推理能力的刻度。**

**2. 70.2% 不全是"看猫片"的功劳。** 集成的三路里有一路是 **ARC 风格格子 MAE 预训练**：用原始 ARC-1 的 400 道训练题 + RE-ARC 约 40 万对 + NVARC 150 万对合成网格，75% 掩码训 500 轮。这路的 patch/位置编码与下游一致、可以整体保留，单模型表现比 ImageNet 路更好（只是 large→huge 不再涨）。把 70.2% 讲成"纯自然图像迁移"是归因过度简化。

**3. "参数量比 LLM 方案小了几个数量级"只对 VARC 成立。** VARC 是 18M（vs 8B，约两个数量级）；但 NAT-ARC huge 是 6.64 亿、集成约 2B，对比 8B 只有 4 倍，中文稿自己写的也是"四分之一的参数量"。同一段里两个说法互相打架。

**4. 单模型 63.4% 其实低于同赛道已有的视觉方法。** 中文稿前文自己列出 LoopViT 65.8%（18M）、Loop-OWM 68.5%（10.6M）。所以"首次逼近专用 LLM 系统"是**集成后 70.2%、且仍略低于 The ARChitects 71.6%**。口径是否完全一致（pass@2 vs pass@1）需要回论文确认，在此之前不要把 63.4% 当作 SOTA。

**5. "共享同一套表征空间"是概念验证不是证明。** autoencoder 的离散符号未与 ARC 颜色语义对齐，作者自己标为定性分析；15 道题的筛选条件（≤30% vs ≥70%）本身也是 cherry-pick 后的描述性统计，不能读成因果。

**6. 可信的部分**：论文真实存在（ECCV 2026 poster 5527，作者 Xiaoman Delores Ding, Keya Hu, Katelyn Gan, Victor Yin, Kaiming He，MIT）；VARC 确实被 CVPR 2026 接收（pp. 2537–2546，集成 60.4%）；"零额外预训练成本"成立（用的就是公开 ImageNet-1K MAE checkpoint）。

**7. 一点小保留**：中文稿把测试时逐题 LoRA 微调写成"用这几组示范试图从中'学会'这道题的规则"——更准确的说法是 TTT（test-time training），每题都要单独跑一轮优化，推理成本远高于一次性前向。比较参数量时不比较测试时计算量，本身就是不公平的（论文自己也提醒了各系统在测试时算力上差别很大）。

---

> 本文为阅读剪藏（摘要 + 摘录 + 评论），非原文转载。[查看原文](https://mp.weixin.qq.com/s/IQH3easn93wPN_cXtbUzMw)
