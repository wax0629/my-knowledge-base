---
type: source
ingested_at: 2026-09-03
published_at: 2026-06-21
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247559033&idx=1&sn=1679aad1869bed534723c98da1549eb1&chksm=f98ca3d3cefb2ac52e2e27e619fa71d298906c7e9c2f3a06f22b2f8203570d1717d1a198e3fc#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 16
author: 小林coding
topics:
  - Claude Fable 5
  - 系统提示词
  - 工具治理
  - Agent 安全
status: processed
capture: webpage_summary
---

# 面试官皱眉：“你看过 Claude Fable 5 系统提示词吗？”，我笑了：“刚看过，需要向我请教什么？”，他：“来，开始你的表演”

## 保存说明

公众号页面已读取。本文件保存文章对网传 Claude Fable 5 系统提示词的解析，不保存或复述所谓提示词全文；其真实性、来源和版本均未在本次入库中独立确认。

## 来源信息

- 原文标题：面试官皱眉：“你看过 Claude Fable 5 系统提示词吗？”，我笑了：“刚看过，需要向我请教什么？”，他：“来，开始你的表演”
- 作者/账号：小林coding
- 页面发布时间：2026-06-21 15:42

## 内容摘要

文章以一份网传的 Claude Fable 5 系统提示词为样本，讨论如何通过工具说明、参数结构、文档优先、行为约束和安全红线塑造 Agent 行为。它的重点不是某个模型的秘密文字，而是“提示词说明意图，工具和系统约束行为”的工程思路。

## 关键内容

- 系统提示词被拆为角色、工具说明、使用时机、输出风格、文档/知识获取方式和安全边界等部分。
- `ask_user_input` 被文章用来说明何时应该停下来向用户确认；`create_file` 被用来说明参数顺序和先解释目的再创建文件如何减少误操作；`message_compose` 则体现面向任务方案而不是只生成文案的工具设计。
- 文章强调“先查说明书再行动”：当工具、外部系统或规范存在文档时，模型应先读取并遵循文档，而不是凭记忆猜参数。
- 行为设计既要让 Agent 说话自然，也要避免通过过度迎合、无关闲聊或持续诱导制造不必要的依赖。
- 安全红线应写清楚权限边界、用户确认、敏感操作、不可伪造的外部状态以及遇到不确定性时的停机/询问路径。

## 与专栏其他文章的关系

本篇为 [[Claude 系统提示词与工具治理]] 提供案例；[[Claude Code 主循环与 Query 流程]] 说明这些规则如何进入工具执行循环，[[Harness Engineering]] 则把规则扩展到系统级验证和恢复。

## 待核实

- “Claude Fable 5”及其系统提示词是否为真实公开材料、是否对应正式产品版本，尚未确认。
- 文中工具名称、参数顺序和提示词片段不应直接作为 Claude 产品 API 合同。
