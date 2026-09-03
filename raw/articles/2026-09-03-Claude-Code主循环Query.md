---
type: source
ingested_at: 2026-09-03
published_at: 2026-06-03
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247558351&idx=1&sn=0a6580a9fb22474bb2cf2d6cabf8977f&chksm=f98ca065cefb2973783e3bfb742f86f19ba5785898bcfbd0a4905ef62313cf628f3b00baf6e4#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 13
author: 小林coding
topics:
  - Claude Code
  - Query Loop
  - 异步生成器
  - 工具调用
  - 错误恢复
status: processed
capture: webpage_summary
---

# 面试官皱眉：“你懂 Claude Code 主循环 Query 流程吗？” 我说：“就是一个 while 循环，调模型、跑工具、再调模型”，他：就这？？

## 保存说明

公众号页面已读取。本文件保存文章对主循环的结构化摘要，不替代原文全文；源码行数、函数名和具体错误处理属于文章所述版本。

## 来源信息

- 原文标题：面试官皱眉：“你懂 Claude Code 主循环 Query 流程吗？” 我说：“就是一个 while 循环，调模型、跑工具、再调模型”，他：就这？？
- 作者/账号：小林coding
- 页面发布时间：2026-06-03 16:36

## 内容摘要

文章把 Claude Code 的一次任务抽象为“接受消息、请求模型、判断是否调用工具、执行工具、把结果写回、继续或结束”的 Query Loop，并进一步拆出 `ask → QueryEngine.submitMessage → query → queryLoop` 四层调用。重点不在正常路径，而在流式事件、跨轮状态和异常恢复。

## 关键内容

- `ask` 是 SDK 入口；`QueryEngine` 维护会话消息、缓存、权限拒绝等跨轮状态；`query` 负责流式包装；`queryLoop` 是真正的主循环。
- 异步生成器通过 `yield*` 把最内层的模型 delta、工具开始/结束和状态事件逐层传递给外部调用者，使界面可以边执行边展示。
- Agent 是否继续取决于模型返回的文本与工具请求：没有待执行工具时结束，有工具时执行并把 `tool_result` 加入下一轮上下文。
- 工具异常、中断或协议不完整时，文章描述系统会补造与 `tool_use_id` 对应的错误结果，避免出现孤立 `tool_use` 导致下一次 API 请求被拒收。
- 输出被截断时，文章描述主循环先静默调整上限并重试，仍超长则向下一轮加入续写提示；上下文过长、取消、失败和循环不收敛也属于生产级主循环必须处理的分支。

## 与专栏其他文章的关系

本篇是 [[Claude Code 源码与架构]] 的执行链细化，与 [[Agent 运行时与多入口模式]] 的“入口 → 核心循环 → 事件”模型相互印证；多 Agent 的异步任务和上下文压缩分别见相关主题。

## 待核实

- `ask`、`QueryEngine`、`queryLoop` 的准确 API、源码文件、输出上限和恢复函数名需要回到可确认版本核对。
- 文章中的“1729 行”“80% 异常路径”等数字属于作者统计，不能未经复现直接引用。
