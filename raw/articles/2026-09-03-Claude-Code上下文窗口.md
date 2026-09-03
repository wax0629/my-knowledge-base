---
type: source
ingested_at: 2026-09-03
published_at: 2026-05-18
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247557638&idx=1&sn=81cbd4fa599c9664a7eb6100cc26a3b2&chksm=f98ca6accefb2fba5c3d19f7e8d6d8413f2d595733a218337df211f9e583f82c2fbc2e5f0157#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 9
author: 小林coding
topics:
  - Claude Code
  - 上下文窗口
  - Context Compact
  - Auto-Compact
  - Prompt Cache
status: processed
capture: webpage_summary
---

# 面试官皱眉：“你知道 Claude Code 的上下文窗口管理吗？”我：“何止知道？我还看过源码”，他愣了…

## 保存说明

公众号页面已读取。本文件保存文章对上下文压缩的结构化摘要，不替代原文全文；阈值和实现细节均属于文章描述，未独立验证。

## 来源信息

- 原文标题：面试官皱眉：“你知道 Claude Code 的上下文窗口管理吗？”我：“何止知道？我还看过源码”，他愣了…
- 作者/账号：小林coding
- 页面发布时间：2026-05-18 14:12

## 内容摘要

文章把 Agent 的上下文管理描述为从轻到重的五层压缩金字塔，目标是“能不做全量摘要就不做”。它先用本地、零 API 开销的办法处理大工具结果和过时消息，只有接近窗口上限时才执行代价最高的 Auto-Compact。

## 关键内容

1. 大工具结果落盘：超大的 `Read` 或命令结果保存到磁盘，消息里只保留预览，需要时再读取。
2. Snip：删除已经失去价值的早期探索消息，加入边界标记，并把释放空间的信息交给后续压缩层。
3. Micro-Compact：在缓存可能失效或工具结果已过时后，清理可重复获取的旧结果，保留最近结果和不可重复的子任务状态。
4. Context Collapse：接近阈值时不改动本地原始消息，只在调用模型时生成压缩后的“读时投影”。
5. Auto-Compact：前四层仍不够时，把历史重写成结构化摘要，并通过重新注入文件、记忆和异步任务状态恢复关键事实。

文章还讨论绝对 token 阈值、手动/自动触发、递归守卫、摘要 Prompt、文件恢复和压缩后的无缝续接。其核心工程原则是把可恢复内容放在外部，把当前目标、进度、错误和下一步保留在摘要中。

## 与专栏其他文章的关系

本篇展开 [[Claude Code 记忆与上下文管理]] 的上下文部分，与 [[Claude Code 主循环与 Query 流程]] 的错误恢复和 [[Harness Engineering]] 的状态治理直接相关。

## 待核实

- 文中提到的 50KB/200KB、60 分钟、90%/95% 等阈值，以及默认输出 token 上限，需要结合实际版本核对。
- “上下文压缩五层”是文章对实现的归纳，不能直接当成所有 Agent 的通用协议。
