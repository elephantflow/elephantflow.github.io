---
title: "Anthropic接受OpenAI标准，智能体从此共用一份AGENTS.md"
slug: "claude-code-agents-md-convergence"
date: 2026-09-19T09:00:00+08:00
draft: false
tags: ["AGENTS.md", "CLAUDE.md", "Claude Code", "Anthropic", "OpenAI Codex", "MCP", "机器之心", "剪藏"]
categories: ["产品、产业与资本"]
description: "Claude Code 从 2.1.277 版本开始支持 AGENTS.md：如果项目目录里没有 CLAUDE.md，就沿目录树查找并使用 AGENTS.md，可在 `/config` 里切换行为；能力建在 Claude Code 的 mods 机制上，Anthropic 把 agents-m…"
showToc: false
---

> **来源**：机器之心 · 2026-09-19 · [原文链接](https://mp.weixin.qq.com/s/u3oTtbEFuTUAPWsEYZSXkw)

> **分类**：主线相关（不是 AI coding 工具新闻，而是**接口层如何收敛**的又一个样本：MCP（模型↔软件）/ AGENTS.md（模型↔项目指令）/ MHS（模型↔仪器）三层同时在收敛，而触觉连第一层都没有。另：中文标题「接受 OpenAI 标准」是错的，见核查第 1 条）

---

## 一句话概括

Claude Code 从 **2.1.277** 版本开始**支持 AGENTS.md**：如果项目目录里没有 CLAUDE.md，就沿目录树查找并使用 AGENTS.md，可在 `/config` 里切换行为；能力建在 Claude Code 的 **mods 机制**上，Anthropic 把 agents-md 做成了**内置 mod 并公开源码**。Claude Code 此前是这个标准"最大的缺席者之一"，它加入后主流 AI Coding 工具围绕「Agent README」收敛的趋势明显得多。**⭐ 但我把它留下的理由不是工具新闻，而是两件事：① 中文标题「Anthropic 接受 OpenAI 标准」是错的——AGENTS.md 早在 2025 年 12 月就捐给了 Linux Foundation 旗下的 Agentic AI Foundation，与 Anthropic 自己的 MCP、Block 的 goose 同为三个 anchor project，Anthropic 本身就是基金会白金成员。这不是"投降"，是两家把自己各自发明的接口层捐进了同一个中立池子。② 由此得到一条我认为很有用的判断：这三层接口能收敛，是因为它们承载的内容是**无争议、低风险、不需要专有技术**的（工具清单、项目说明、设备读数）；而触觉的接口层之所以没人定义，可能恰恰是因为"接触状态是什么"本身还没有共识——**接口层的标准化发生在共识之后，不是之前。我们一直在等一个先于共识出现的标准，顺序反了。**

## 核心要点



## 金句

> 「AGENTS.md 就像是项目写给 AI Agent 看的说明书……官方把它称为『README for agents』。」

> 「团队不应该长期承担这类同步工作。」（Tobi Lütke）—— 他把这种负担称为「复杂性税」。

> 「太好了！这就对了。欢迎来到光明的一边。」（OpenAI Codex 负责人 Tibo）

> 「不同模型家族具有不同的行为特点，system prompt 会显著影响模型表现。」（Thariq Shihipar，解释 Anthropic 为何坚持 CLAUDE.md）

> 「项目指令文件正在从工具偏好变成代码库基础设施。」

> 「如果两份文件存在差异，不同 Agent 获得的项目规则也会不同。」

> 「具体可执行的命令胜过含糊的描述——Agent 能执行 `npm test`，不能对『确保一切正常』采取行动。」（GitHub 对 2,500+ 仓库的分析）

## 质疑与核查

1. **⚠️⚠️ 标题「Anthropic 接受 OpenAI 标准」是错的，这是全篇最需要纠正的一处**。AGENTS.md 于 **2025 年 12 月捐给 Linux Foundation 旗下的 Agentic AI Foundation（AAIF）**，与 **Anthropic 自己的 MCP**、Block 的 goose 并列为三个 anchor project；**白金成员含 AWS、Anthropic、Block、Bloomberg、Cloudflare、Google、Microsoft、OpenAI**。所以准确的说法是：**两家公司各自发明的接口层都捐进了同一个中立池子，Anthropic 本身就是这个池子的成员和受益者（MCP 在里面）。** 另外，AGENTS.md 也并非 OpenAI 单独发明——Codex、Amp、Jules、Cursor、Factory 是**各自独立收敛后协调成一个格式**的。中文标题把一个"中立治理后的生态位补齐"讲成了"竞争对手投降"。

2. **⚠️ "支持"是回退，不是替换，也不是合并**。默认模式下**只有路径上没有 CLAUDE.md 时才读 AGENTS.md**；要同时加载需手动在 `/config` 改。机器之心正文写清楚了，但**标题"从此共用一份 AGENTS.md"会让人误以为 CLAUDE.md 被取代**——没有。

3. **⚠️ 不能说 AGENTS.md "已成为标准"**。它是**开放格式**，但**背后没有经过批准的、带版本号的规范**；采用格式与加入基金会是两件事（Cursor 读了但不是成员）。**准确措辞是"正在收敛的惯例"。** 中文稿说"跨厂商的项目指令标准"，偏重了。

4. **60,000+ 仓库、23.7k stars、OpenAI monorepo 88 个 AGENTS.md** 这些数字来自官方站点与 GitHub code search，**是自报数据**，且"用了 AGENTS.md"的统计口径（是否含 fork、是否含空文件）不明。

5. **发布日期有小出入**：机器之心与部分英文源说 Thariq **9 月 18 日**发帖，IT之家说 **9 月 19 日**发布的 2.1.277 版本。版本号 2.1.277 各家一致，日期差一天可能是时区或"宣布 vs 发布"，**引用时用版本号更稳**。

6. **⚠️ mods 机制本身还没被文档化**：Anthropic **未发布 mods 的正式文档、API 边界或 GA 时间**。中文稿说"这项能力建立在 mods 机制上"给人感觉 mods 已成熟，实际**AGENTS.md 支持看起来更像 mod 概念的示范**。"未来开发者也可以围绕项目指令构建自定义版本"是 Thariq 的意向表述，不是已交付能力。

7. **Shopify 那条是二手转述**：机器之心引用自己此前的报道，称 Tobi Lütke **"曾考虑"**禁用 Claude Code。**"曾考虑"与"已实施"差别很大**，且我未核到 Lütke 本人的原始表态。**"复杂性税"这个词的原始出处也值得再确认。**

8. **⚠️ 别把网站根目录的 /agents.md 混进来**：Shopify 在推的**网站根 /agents.md 是给 AI 购物代理看的**（agentic commerce），与本文的仓库级编码 Agent 指令文件**只是同名**。网上大量"AGENTS.md 取代 llms.txt"的说法说的是前者。

9. **评论区"终于统一了"是社区情绪，不是事实陈述**。统一的是**文件读取入口**，`.agents/skills` 与 `.claude/skills` 仍是两套目录，语义层的统一远未完成。

10. **⚠️ 与我主线的关系要克制**：接口层的**收敛机制与推广手法**可以借，**具体形态不能借**——编码指令是静态文本，接触状态是流式高维信号。**不要因为"一个 Markdown 文件赢了"就推断触觉也能靠一个约定文件赢。**

11. **一条我未能核实的**：有来源称 A2A 协议 2026 年 8 月加入 AAIF、AAIF 白金成员名单如上——**来自单一二手来源，未逐一核实，引用时注明。**

---

> 本文为阅读剪藏（摘要 + 摘录 + 评论），非原文转载。[查看原文](https://mp.weixin.qq.com/s/u3oTtbEFuTUAPWsEYZSXkw)
