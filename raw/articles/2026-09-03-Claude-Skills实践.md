---
type: source
ingested_at: 2026-09-03
published_at: 2026-06-18
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247558967&idx=1&sn=bb508feae2a5a5cfd28a12f4ab4130df&chksm=f98ca39dcefb2a8b9152a7c25587ce1dabb4044f290670ffbeec49fbff66859c5c10fc87bf4a#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 15
author: 小林coding
topics:
  - Claude Code
  - Skills
  - Agent 工程化
  - 团队知识
  - 可观测性
status: processed
capture: webpage_summary
---

# 面试官皱眉：“Claude Code 你用了半年，你懂 Skills 吗？”我反问：“不就是写了步骤的 markdown 吗”，他：今天就到这吧

## 保存说明

公众号页面已读取。本文件保存文章摘要和实践建议，不替代原文全文；文章引用的 Anthropic 内部经验没有在本次入库中独立验证。

## 来源信息

- 原文标题：面试官皱眉：“Claude Code 你用了半年，你懂 Skills 吗？”我反问：“不就是写了步骤的 markdown 吗”，他：今天就到这吧
- 作者/账号：小林coding
- 页面发布时间：2026-06-18 14:12

## 内容摘要

文章反驳“Skill 只是写步骤的 Markdown”这一理解，强调 Skill 的真正载体是一个可发现、可探索的文件夹。除了 `SKILL.md`，还可以包含参考资料、脚本、数据和输出模板；好的 Skill 还要解决触发、坑点、记忆、团队共享和使用反馈。

## 关键内容

- `SKILL.md` 是入口，frontmatter 负责名称和描述，正文负责操作指引；其余文件按需读取，不应把所有细节常驻上下文。
- 文章引用 Anthropic 对内部数百个 Skill 的归类，认为高价值 Skill 通常围绕库/API 参考、产品验证、数据分析和高频业务流程等重复工作沉淀。
- Skill 的描述要让模型知道“什么时候用我”，而不是只罗列“我是什么”；触发词、适用条件、输入输出和明确的反例会影响触发质量。
- 最有价值的内容往往是失败案例和坑点清单：前置条件、容易误用的参数、失败后的恢复方式和必须人工确认的边界。
- Skill 可以携带持久记忆、执行脚本或只在激活期间生效的 Hook；复杂计算交给脚本，模型负责理解任务与编排，减少重复推理。
- 项目级 Skill 可随仓库共享，Plugin 可打包分发；通过调用次数、成功率、失败类型和使用反馈判断 Skill 是否真正有价值。

## 与专栏其他文章的关系

本篇是 [[Agent Skills 与渐进式披露]] 的实践篇，也与 [[Claude Code 工程化六件套]] 的团队分发和 [[Loop Engineering]] 的知识复利相连。

## 待核实

- Anthropic 内部 Skill 数量、九类划分、使用数据和最佳实践属于文章转述，需要原始博客或公开资料验证。
- Skill 记忆、脚本和临时 Hook 的可用接口随 Claude Code 版本变化。
