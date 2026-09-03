---
type: wiki
updated_at: 2026-09-03
topics:
  - 图解Agent
  - Agent
  - Claude Code
  - Agent 工程化
---

# 图解 Agent 专栏

## 摘要

“图解Agent”是小林coding 的公众号连载专栏，本次读取到 22 篇文章。专栏从 OpenClaw 和 Agent 基础概念开始，经过 RAG、GraphRAG/LightRAG 与 Claude Code 源码解析，逐步转向记忆、上下文、Skill、Harness、Loop 和 Graph Engineering。它适合作为 Agent 工程化主题的阅读索引，但其中关于快速迭代产品、泄漏源码和网传系统提示词的内容需要单独核验。

## 核心内容

### 阅读路径

1. 基础：[[OpenClaw 本地自主 Agent]]、[[Agent 基础概念与协议]]。
2. 检索：[[RAG 检索与评估]]、[[GraphRAG 与 LightRAG]]、[[Claude Code 代码检索策略]]。
3. 运行时：[[Claude Code 源码与架构]]、[[Claude Code 主循环与 Query 流程]]、[[Claude Code 多智能体协作]]。
4. 状态与规则：[[Claude Code 记忆与上下文管理]]、[[Claude Code 项目规则与 CLAUDE.md]]。
5. 工程化：[[Harness Engineering]]、[[Agent Skills 与渐进式披露]]、[[Claude Code 工程化六件套]]、[[Loop Engineering]]、[[Graph Engineering]]。
6. 争议材料：[[Claude 系统提示词与工具治理]]。

### 专栏内部演进

- 文章 1–2 建立本地 Agent 和基础协议的词汇表。
- 文章 3–6 从 coding agent 架构扩展到 RAG 和图检索。
- 文章 7–13 以 Claude Code 为案例拆解多 Agent、代码搜索、上下文、规则、记忆和主循环。
- 文章 14–21 讨论如何把单次 Agent 变成可持续、可分工、可验证的工程系统。
- 文章 22 的 Codex 工程化能力与后半段主题形成跨产品对照，原料已存在于 `raw/articles/2026-09-02-Codex工程化能力.md`。

## 与已有知识的关系

本篇是专栏导航，不替代各主题文章。[[Pi coding agent 架构]] 和 [[Agent 运行时与多入口模式]] 是知识库中另一条 coding agent 运行时架构线；[[Codex 工程化能力]] 可用于比较不同 Agent 产品的规则、技能、子任务、连接和 Hook 机制。

## 我的理解

专栏最有价值的主线不是某个产品名称，而是瓶颈从模型能力逐步外移：先是 Prompt，再是 Context，然后是 Harness、Loop 和 Graph。读这些文章时应把“文章对某实现的描述”和“可迁移的工程原则”分开保存，并用源码、官方文档和可复现实验验证具体数字。

## 相关主题

- [[Agent 基础概念与协议]]
- [[Claude Code 源码与架构]]
- [[Harness Engineering]]
- [[Loop Engineering]]
- [[Graph Engineering]]
- [[Claude 系统提示词与工具治理]]

## 来源

- 来源文件：`raw/articles/2026-09-03-图解Agent专栏.md`
- 专栏链接：https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect
- 作者：小林coding
- 读取日期：2026-09-03

## 待核实

- 本条目反映 2026-09-03 读取到的 22 篇目录，专栏后续可能继续更新。
- 文章所引产品版本、源码、论文数字和网传系统提示词均不应在未验证前作为确定事实。
