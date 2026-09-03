---
type: source
ingested_at: 2026-09-03
published_at: 2026-07-28
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247560334&idx=1&sn=8c72a7c80d6b65425686e33425d62651&chksm=f98ca824cefb2132abd2e974fde38227c68ef4160d3e0bb2d75e38f724e5eccaeb325dd1d4c6#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 20
author: 小林coding
topics:
  - Claude Code
  - CLAUDE.md
  - Skills
  - Subagents
  - MCP
  - Hooks
  - Plugins
status: processed
capture: webpage_summary
---

# 面试官皱眉：“你懂 Claude Code？” 我笑了：“何止懂？CLAUDE.md、Skills、Subagents、MCP、Hooks、Plugins样样都懂”

## 保存说明

公众号页面已读取。本文件保存文章对 Claude Code 工程化六件套的结构化摘要，不替代原文全文；具体能力和配置格式需要按当前版本核验。

## 来源信息

- 原文标题：面试官皱眉：“你懂 Claude Code？” 我笑了：“何止懂？CLAUDE.md、Skills、Subagents、MCP、Hooks、Plugins样样都懂”
- 作者/账号：小林coding
- 页面发布时间：2026-07-28 14:12

## 内容摘要

文章把 Claude Code 的工程化配置归纳为六件套：`CLAUDE.md`、Skills、Subagents、MCP、Hooks 和 Plugins。它们分别承担项目规则、按需知识、任务分工、外部连接、生命周期门禁和能力打包，不应把所有职责都堆进一份 Prompt 或规则文件。

## 关键内容

- `CLAUDE.md`：保存项目技术栈、命令、目录约定和不可触碰的边界，作为会话的稳定基础。
- Skills：把低频但复杂的流程、参考资料和模板按需加载，减少规则文件和常驻上下文膨胀。
- Subagents：为探索、实现、测试和审查提供独立上下文与职责边界，主 Agent 负责协调和合成。
- MCP：以统一协议连接 GitHub、Issue、数据库、云文档和其他外部系统，让 Agent 能获取信息或执行受控操作。
- Hooks：把格式化、测试、敏感文件保护、审计和结果记录绑定到工具或任务生命周期节点，减少依赖模型自觉。
- Plugins：把规则、Skill、Subagent、MCP 配置和 Hook 组合成可安装/共享的能力包，便于团队复制实践。
- 文章用一个 code review/修复流程展示组合方式：规则提供背景，Skill 提供清单，Subagent 分工，MCP 读写协作系统，Hook 做门禁，Plugin 负责分发。

## 与专栏其他文章的关系

本篇是专栏后半段的总览，统一连接 [[Claude Code 项目规则与 CLAUDE.md]]、[[Agent Skills 与渐进式披露]]、[[Claude Code 多智能体协作]]、[[Harness Engineering]] 和 [[Loop Engineering]]。

## 待核实

- 六件套各自的目录、事件、权限和安装方式可能随 Claude Code 版本变化。
- MCP 写操作、Hook 失败行为和 Plugin 分发边界应按实际配置逐项验证。
