---
type: wiki
updated_at: 2026-09-03
topics:
  - Claude Code
  - 大型代码库
  - Harness Engineering
  - Agentic Search
  - LSP
  - 团队协作
---

# Claude Code 大型代码库实践

## 摘要

大型代码库的 Agent 问题通常不是单纯换更大模型，而是如何控制上下文、精准检索、分阶段改动和持续验证。专栏文章建议用短而分层的规则、Agentic Search、LSP、独立会话、子 Agent 和团队共享的 Skill/Plugin/MCP 组成适合大仓库的 Harness。

## 核心内容

### 上下文与检索

不能把整个仓库塞进上下文。根目录规则只保留跨模块约定和关键陷阱，模块细节放到子目录；代码定位从目录和清晰入口开始，再用 `Glob`、`Grep`、`Read` 和必要的 LSP 逐步缩小范围。这样可以让每一步都基于当前工作树，而不是依赖可能过期的索引。

### 跨文件实施

跨几十个文件的修改应拆成调查、计划、实现、测试和 Review 阶段。独立上下文的子 Agent 适合做探索或挑错，主 Agent 负责合成和最终决策；每个阶段都要运行与目标匹配的编译、测试和静态检查。

### 团队推广

高频操作可以先沉淀成 Skill，再用 Plugin 分发；需要访问 Issue、监控或代码托管平台时接入 MCP，并指定维护者持续更新规则和流程。工具的成功率、失败类型和人工反馈应成为迭代依据。

### 适用边界

文章提醒，高风险架构、鉴权、支付和生产部署不适合默认无人值守。即使模型具备较大上下文，也不能替代权限隔离、回滚能力、独立 Review 和人工接管。

## 与已有知识的关系

[[Claude Code 代码检索策略]] 详细解释 Agentic Search 与代码 RAG 的取舍；[[Claude Code 项目规则与 CLAUDE.md]] 记录规则分层；[[Claude Code 多智能体协作]] 记录子 Agent 隔离和并行；[[Harness Engineering]] 是本篇实践背后的系统框架。

## 我的理解

大仓库的核心优化目标是减少无效上下文和错误修改，而不是追求一次请求覆盖更多文件。最小可行的做法是先让 Agent 稳定找到正确入口并通过小范围测试，再逐步增加跨文件和并行能力；任何自动化扩张都要同步增加可观察性和人工复核。

## 相关主题

- [[Claude Code 代码检索策略]]
- [[Claude Code 项目规则与 CLAUDE.md]]
- [[Claude Code 多智能体协作]]
- [[Harness Engineering]]
- [[Loop Engineering]]

## 来源

- 来源文件：`raw/articles/2026-09-03-Claude-Code大型代码库实践.md`
- 原始文章：https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247557838&idx=1&sn=c4bc3f0537ef2b1fdd3b26e2c9c8d3ae&chksm=f98ca664cefb2f72d9fdbb65753dda2d2fa99ef3e089c53814da23eb7a043cf8d6f96f80fd41#rd&scene=21#wechat_redirect
- 作者/日期：小林coding，2026-05-22

## 待核实

- 文中引用的模型上下文规模、根规则长度建议、LSP 集成和 Anthropic 团队实践需要独立验证。
- 文章对“不适合 Claude Code”的项目边界是经验判断，应按具体风险模型调整。
