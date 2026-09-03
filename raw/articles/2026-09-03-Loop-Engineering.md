---
type: source
ingested_at: 2026-09-03
published_at: 2026-06-14
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247558717&idx=1&sn=1b7e118a44b39ff3fff33c392f784897&chksm=f98ca297cefb2b81c617ca2d0ff862e65af3bc6fdfe9485a8ca0208e478016d33ea34e6abaf4#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 14
author: 小林coding
topics:
  - Loop Engineering
  - 自动化
  - Worktree
  - Skill
  - Connector
  - Subagent
  - Agent 记忆
status: processed
capture: webpage_summary
---

# 面试官坏笑：“你怎么看 Loop Engineering？”我反问：“不就是 /loop 吗？让 Agent 循环干活”，他摇了摇头...

## 保存说明

公众号页面已读取。本文件保存文章对 Loop Engineering 的概念和案例摘要，不替代原文全文。

## 来源信息

- 原文标题：面试官坏笑：“你怎么看 Loop Engineering？”我反问：“不就是 /loop 吗？让 Agent 循环干活”，他摇了摇头...
- 作者/账号：小林coding
- 页面发布时间：2026-06-14 15:36

## 内容摘要

文章把 Loop Engineering 解释为围绕一个能持续运行的 Agent 循环设计完整工作环境，而不只是增加一个 `/loop` 命令。它是 Prompt → Context → Harness 之后的瓶颈迁移：模型可以连续工作后，自动触发、隔离、连接、验证和记忆成为关键。

## 关键内容

- 一个完整 loop 由自动化触发、Git worktree、Skill、Connector、Subagent 和磁盘记忆/状态组成。
- 自动化是循环的心跳；worktree 为并行 Agent 提供独立目录和分支；Skill 保存项目知识；Connector（文章以 MCP 为例）连接 Issue、监控、消息和 PR；Subagent 把写代码与检查代码分开；状态文件让下一次循环接上上一次进度。
- 文章给出的示例是定时读取 CI、Issue 和提交，生成待处理项，为每项创建隔离 worktree，派 Agent 修复，再由独立 Agent 检查，最后自动开 PR、更新工单并记录状态；无法自动处理的问题进入人工待办。
- 自动化程度越高，验证责任、Token 预算、理解债和认知投降风险越高。Loop 适合高频、可验证、可回滚的工作，不应默认接管架构、鉴权、支付和生产部署。

## 与专栏其他文章的关系

[[Harness Engineering]] 解释 loop 的组成零件为何需要存在；[[Graph Engineering]] 进一步将一个 loop 扩展成有依赖关系的多节点图；[[Claude Code 工程化六件套]] 提供 Skill、Subagent、MCP、Hook 和 Plugin 的具体机制。

## 待核实

- Loop Engineering 的术语、外部博客引用和示例是否已经形成统一定义，需要回查原始资料。
- 文章提出的“理解债”“认知投降”是风险分析框架，不是现成的工程度量指标。
