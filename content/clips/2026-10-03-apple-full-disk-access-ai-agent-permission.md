---
title: "苹果突然收紧Mac权限，为了防AI变得更像iOS"
slug: "apple-full-disk-access-ai-agent-permission"
date: 2026-10-03T09:00:00+08:00
draft: false
tags: ["苹果", "macOS", "Full Disk Access", "全盘访问权限", "AI Agent", "Meta Muse", "APPSO（ID：appsolution）", "剪藏"]
categories: ["产品、产业与资本"]
description: "苹果于 2026-10-02（周五） 在开发者网站发布《Updates to Full Disk Access in macOS》，宣布将为 macOS 的全盘访问权限加设额外控制：真正想授予这份权限的用户，今后也只能通过非常明确的用户操作才能给出。⭐ APPSO 这篇说苹果没有明着说、只是暗…"
showToc: false
---

> **来源**：APPSO（ID：appsolution）（APPSO） · 2026-10-03 · [原文链接](https://mp.weixin.qq.com/s/WnFcL0r67sqnQPdKheyyJQ)

> **分类**：主线强相关（Agent 权限治理这篇把我 #37 那条「运行时控制强制它实际被允许做什么」从一家公司的产品扩成了操作系统层 + 模型厂商 + Agent 厂商三层同时在做的同一件事；且带来了可以直接搬到具身接口上的框架——Simon Willison 的「致命三要素」，以及一条可操作的评测法：在更小的授权范围里再做一次同样的工作）

---

## 一句话概括

苹果于 **2026-10-02（周五）** 在开发者网站发布《Updates to Full Disk Access in macOS》，宣布将为 macOS 的**全盘访问权限**加设额外控制：真正想授予这份权限的用户，今后也只能"通过非常明确的用户操作"才能给出。**⭐ APPSO 这篇说苹果"没有明着说、只是暗示是 AI Agent 的锅"——这是错的，苹果是明说的**：原文写的是"随着 AI agent 的能力与自主性不断增强，这种级别的访问权限所附带的风险将大幅上升（As AI agents become increasingly capable and autonomous, the risks associated with this level of access will grow substantially）"。导火索是 Meta 的个人 Agent **Muse** 被 Inc. 专栏作家 Jason Aten 指控读了其私人消息（Meta 否认，称必须同时开启 Full Disk Access 与 Messages connector）。**我在原文基础上补到的、而中文稿完全没有的三件事才是重点：① Simon Willison 的「致命三要素」（接触私人数据 + 读取不可信内容 + 向外部通信，三者同时存在即致命）；② 10-02 同日 WIRED 披露 ChatGPT Mac 应用一个已修复漏洞可让攻击者取走聊天记录，Patrick Wardle 把 Agent 比作"掌握各房间钥匙的楼宇管理员"；③ Meta 的 Muse 架构里，Agent 跑在隔离环境、不接触真实凭证，连接器操作与对外网络请求由独立的 Sentinel 系统管理——"模型可以提出动作，但不能自行决定是否获得执行许可"。这第三条与 #37 黄仁勋的 OpenShell/Sentry 是同一个设计原则的第二个实例，而且现在它已经在操作系统层、模型厂商、Agent 厂商三层同时出现。**

## 核心要点



## 金句

> this is why we can't have nice things（这就是为什么我们没法拥有好东西）。

> Mac 本来就是一台「危险但强大」（dangerously powerful）的 Unix 工作站。

> 开发者认为用户完成了授权，用户却认为自己没有委托这件事。

> Agent 就像掌握各房间钥匙的楼宇管理员：访问越广，被攻破后的影响也越大。（Patrick Wardle）

> 允许模型规划任务，同时把权限判断放在模型无法自行改写的边界上。

> 完整权限下的演示能说明能力上限，受限环境中的表现则更接近部署后的价值。

## 质疑与核查

**1. ⭐ 中文稿说苹果"没有明着说、只是暗示"——这是错的。** 苹果原文白纸黑字写了 "As AI agents become increasingly capable and autonomous, the risks associated with this level of access will grow substantially." **是明示，不是暗示。**（已核 The Verge / Mashable / CNA 均引用同一段原文。）

**2. 中文稿说 Gruber「矛头直指 Meta Muse、Grok」——苹果公告没有点名任何应用。** Muse 与苹果公告的关联是**时间上的前后**（Reuters/CNA 报道），不是苹果点名；**Grok 我核不到任何与本次全盘权限相关的具体材料，APPSO 这个并列缺乏依据。**

**3. 中文稿把措施写成"更明确（也更繁琐）的手动操作"——"更繁琐"是推断。** 苹果只说 "very explicit user action"，**没有说会增加几步、会是什么交互**。备份类工具的授权流程会不会被迫改版，目前没有说法。

**4. ⭐ 中文稿漏掉了苹果原文里最关键的一句半**：「For communication apps, this can also compromise the privacy of the people users are communicating with」（通信类应用会连带影响**与你通信的那一方**的隐私）——这是"隐私不只是个人的"这一层；以及"Full Disk Access largely sidesteps these controls"这个对自身隐私体系的承认。

**5. 中文稿是纯评论转述，零技术内容。** 没有 lethal trifecta、没有 WIRED 那条漏洞、没有 Meta Sentinel 架构、没有苹果原文——**以上四处全部是我回英文源补的**（Reuters/CNA、The Verge、Mashable、新浪/腾讯转载的中文深度稿）。

**6. Muse 事件本身仍是各执一词，不能当作"绕过权限"的定论。** Aten 说自己没授权，Meta 说必须两个开关同时开。**在没有第三方复现之前，这只能算"授权语义存在鸿沟"的证据，不能算"Muse 越权"的证据。**

**7. 「致命三要素」是 Simon Willison 2025 年提出的分析框架，不是实验结论。** 它描述的是能力组合带来的风险结构，不是某个具体攻击的实测。**引用时按框架处理，不要当成已发生的事件。**

**8. 苹果的措施目前只有方向没有规则。** 未披露机制、版本、时间，也没有禁止 Agent 使用该权限。**任何"苹果封死了 Agent"的说法都过度解读。**

---

> 本文为阅读剪藏（摘要 + 摘录 + 评论），非原文转载。[查看原文](https://mp.weixin.qq.com/s/WnFcL0r67sqnQPdKheyyJQ)
