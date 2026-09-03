---
type: source
ingested_at: 2026-09-03
published_at: 2026-04-06
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247556000&idx=1&sn=01e3a55e22467c677af3e75f9a6d7c62&chksm=f98d5f0acefad61c6ea9c227ebbc65356eb14007cb66d09ac40e50a5a7538446060c61e5fefa#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 3
author: 小林coding
topics:
  - Claude Code
  - Agent 架构
  - Tool-Use Loop
  - System Prompt
  - 记忆
  - 上下文管理
status: processed
capture: webpage_summary
---

# 面试官：“简历写着用过 Claude Code，那源码看过吗？”，我怼回去：“没看过，又能怎？”

## 保存说明

公众号页面已读取。本文件只保存基于文章的结构化摘要；文章把网传的 Claude Code 客户端源码作为分析材料，其真实性、版本和完整性没有在本次入库中独立确认。

## 来源信息

- 原文标题：面试官：“简历写着用过 Claude Code，那源码看过吗？”，我怼回去：“没看过，又能怎？”
- 作者/账号：小林coding
- 页面发布时间：2026-04-06 15:36

## 内容摘要

文章从所谓 Claude Code 客户端源码出发，试图说明一个编程 Agent 如何通过分层、工具治理、上下文压缩和记忆系统获得可靠性。作者把它概括为“不是让模型更聪明，而是给模型加一套可控的执行系统”。

## 关键内容

- 文章描述四层结构：引擎层负责协调上下文、分发工具和决定继续/结束；工具层承载文件、Shell、搜索和子 Agent 等能力；服务层提供模型 API、上下文压缩和 MCP；安全与治理层横跨各层，处理权限、Hook、Shell 风险与用户确认。
- 文章认为 Claude Code 的核心不是经典的显式 ReAct 文本，而是由模型输出工具请求、运行时执行工具、把结果写回上下文并继续请求的 Tool-Use Loop；同时讨论了 Plan Mode 对任务规划的影响。
- System Prompt 被描述为多个约束的集合：角色、安全红线、工具使用、Git 安全、输出风格、环境信息和缓存/分段策略。
- 文章把记忆归纳为分类、索引、独立文件和按需召回，把上下文管理归纳为大结果落盘、旧消息裁剪、工具结果压缩、读时投影和全量摘要；这些细节与专栏后续文章分开展开。

## 与专栏其他文章的关系

这是 Claude Code 系列的总览，具体机制见 [[Claude Code 多智能体协作]]、[[Claude Code 代码检索策略]]、[[Claude Code 记忆与上下文管理]]、[[Claude Code 主循环与 Query 流程]] 和 [[Claude Code 工程化六件套]]。

## 待核实

- 所谓客户端源码泄漏、行数、四层目录、工具数量和类型系统约束均应回到可确认的源码版本核对。
- “没有使用 ReAct”是文章对实现范式的判断，不代表所有 Claude Code 版本或内部模型推理过程。
