---
title: "Motus2：面向灵巧操作的自进化通用世界模型"
slug: "motus2-self-evolving-world-model"
date: 2026-09-01T09:00:00+08:00
draft: false
tags: ["世界模型", "具身智能", "触觉智能", "灵巧操作", "第一视角数据", "Scaling", "Motus2", "剪藏"]
categories: ["世界模型与具身智能"]
description: "Motus2 把策略、模拟器、评估器三件事塞进同一套权重（只用改注意力掩码来切换），让模型能自己生成候选动作、想象后果、给结果打分、再用打分回传更新策略——形成闭环自我进化，配合 13 万小时第一视角人类数据金字塔，把双臂灵巧手的真机成功率从 0% 拉到 84%。"
showToc: false
---

> **来源**：Motus2 · 2026-09-01 · [原文链接](https://mp.weixin.qq.com/s/2EbruvHr_uU_lbYgLmKLiA)

> **分类**：技术报告

---

## 一句话概括

Motus2 把策略、模拟器、评估器三件事塞进**同一套权重**（只用改注意力掩码来切换），让模型能自己生成候选动作、想象后果、给结果打分、再用打分回传更新策略——形成闭环自我进化，配合 13 万小时第一视角人类数据金字塔，把双臂灵巧手的真机成功率从 0% 拉到 84%。

## 核心要点

- **一套权重，三个接口**：world-action model 当策略（输出 action chunking）、action-conditioned world model 当模拟器（预测动作后果）、value model 当评估器（估计任务推进程度）。三者不是三个独立网络，而是同一参数在不同注意力掩码与训练模式下的三种条件函数。
- **action-first 分解 + 基于轨迹的监督路由**：action token 不能读未来视频和 value；未来的视频能读 action；value query 能读 action 和视频但对其他 token 不可见。更关键的是，**只有筛选过的成功轨迹才开启 action 监督**——失败和次优轨迹的 action 只当条件变量、不当模仿目标，让它们去喂动力学建模和 value learning。这一步把"垃圾数据"变成了有用证据。
- **推理时默认不走完整链路**：普通控制只查询 action 因子，只有做规划（Best-of-N）和策略优化（DiffusionNFT 的 model-based RL）时才完整跑策略-模拟器-评估器。既保留了视频-动作联合训练的好处，又不用每一步都做未来 rollout。
- **数据金字塔**：约 13 万小时 egocentric 数据，单目（低分辨率 500K 步 → 高分辨率 340K 步）→ 双目联合训练 450K 步 → 机器人轨迹 + human-robot alignment 数据做 mid-training。并验证了双目人类数据在 2k–20k 小时区间内 human action 预测误差与数据量的对数-线性 scaling。
- **长上下文与触觉两个扩展**：长历史对比了 global-autoregressive（全历史保留）和 hybrid working memory（anchor + 近期帧 + memory token），前者在两个探测任务上都明显更好；轻量化 Tactile Expert（30 层、hidden 128）复用骨干 KV cache，每 0.2 秒用最新触觉窗口修正一个子分块，同时预测下一窗口的力信号。
- **关键数字**：主套件 macro-average SR 从 WAN-SFT 的 0% → Pretrain-SFT 51% → Motus2 84%；MBRL 单独 +7.5 个点、Best-of-N 规划 +2.5 个点、叠加 +10 个点；触觉 Expert 让两个接触敏感任务平均 +12.5 个点（60% → 72.5%）。

## 金句

> Motus2 不把 action 生成、action-conditioned 未来仿真、结果评估当作互相独立系统，而是看作共享物理世界模型上不同条件函数。

> 规划只改变从现有策略分布中的选择结果；model-based RL 直接更新后续采样所依赖的策略分布。

> 失败样本并不全部一开始就很低；曲线形态更有信息。……共同模式：前期执行正确 value 上升；一旦任务推进停止，value 开始下降。

---

> 本文为阅读剪藏（摘要 + 摘录 + 评论），非原文转载。[查看原文](https://mp.weixin.qq.com/s/2EbruvHr_uU_lbYgLmKLiA)
