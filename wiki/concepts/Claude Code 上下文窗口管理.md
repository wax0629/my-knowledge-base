---
type: wiki
updated_at: 2026-09-03
topics:
  - Claude Code
  - 上下文窗口
  - Context Compact
  - Auto-Compact
  - Prompt Cache
---

# Claude Code 上下文窗口管理

## 摘要

Agent 的上下文会同时累积系统提示、工具描述、用户消息、工具调用和工具结果，因此比普通聊天更容易接近窗口上限。专栏文章把 Claude Code 的处理概括为五层策略：先落盘和裁剪，再做读时投影，最后才进行代价更高的全量摘要。

## 核心内容

### 五层压缩策略

1. 大工具结果落盘，消息中只保留预览，需要时重新读取。
2. Snip 删除失去价值的早期探索消息，插入边界标记。
3. Micro-Compact 清理可重复获取的旧工具结果，保留最近结果和不可重建的子任务状态。
4. Context Collapse 在调用模型时生成压缩视图，不修改本地原始消息。
5. Auto-Compact 在前四层仍无法腾出空间时，把历史重写成可接续的摘要，并重新注入关键文件、记忆和异步任务状态。

### 触发与恢复

文章还讨论按 token 缓冲而非简单轮数触发、手动和自动压缩的区别、递归/熔断保护、摘要 Prompt 的结构，以及压缩后如何恢复文件和状态。核心恢复原则是：可以重新读取的原文不要全部塞进摘要；目标、进度、关键决策、失败原因和下一步必须留下。

## 与已有知识的关系

[[Claude Code 记忆与上下文管理]] 把本篇与动态记忆、静态 `CLAUDE.md` 放在同一个状态模型中；[[Lost in the Middle 与长上下文]] 说明即使没有超过窗口，模型也可能对中间位置的信息使用不稳健；[[Claude Code 主循环与 Query 流程]] 说明压缩发生在模型/工具循环的哪里；[[Claude Code 代码检索策略]] 说明减少无效读取是控制上下文的上游手段。

## 我的理解

上下文治理的优先级应是：减少无效输入，保留可恢复状态，最后才压缩不可避免的历史。所有压缩都应有可观测指标，例如丢弃了什么、是否能重新读取、摘要后任务成功率是否下降；否则“节省 Token”可能换来隐性错误。

## 相关主题

- [[Claude Code 记忆与上下文管理]]
- [[Lost in the Middle 与长上下文]]
- [[Claude Code 主循环与 Query 流程]]
- [[Claude Code 代码检索策略]]
- [[Harness Engineering]]
- [[Claude Code 源码与架构]]

## 来源

- 来源文件：`raw/articles/2026-09-03-Claude-Code上下文窗口.md`
- 原始文章：https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247557638&idx=1&sn=81cbd4fa599c9664a7eb6100cc26a3b2&chksm=f98ca6accefb2fba5c3d19f7e8d6d8413f2d595733a218337df211f9e583f82c2fbc2e5f0157#rd&scene=21#wechat_redirect
- 作者/日期：小林coding，2026-05-18

## 待核实

- 50KB/200KB、60 分钟、90%/95% 等阈值、缓存行为和 Auto-Compact 细节需要对应版本源码核对。
- 五层模型是文章归纳，不是 Claude Code 或 Agent 的通用标准。
