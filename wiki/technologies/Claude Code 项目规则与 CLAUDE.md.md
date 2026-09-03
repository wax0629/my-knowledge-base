---
type: wiki
updated_at: 2026-09-03
topics:
  - Claude Code
  - CLAUDE.md
  - 项目规则
  - Context Engineering
  - 团队协作
---

# Claude Code 项目规则与 CLAUDE.md

## 摘要

`CLAUDE.md` 在专栏文章中被定位为 Claude Code 的项目级入职手册：它保存技术栈、命令、目录约定、修改边界和验证要求，让每次会话从同一组前提开始。高质量规则的标准不是长度，而是具体、稳定、可验证并且确实会改变 Agent 行为。

## 核心内容

### 分层放置

文章描述了全局、项目根目录和子目录等层级：全局文件适合个人偏好，项目文件适合团队共享的技术和流程约定，子目录文件适合模块特有规则。分层可以让根上下文只承载跨模块的关键约束。

### 有效规则

值得保留的规则通常说明：使用什么构建/测试命令、哪些目录或数据不可触碰、代码应遵守什么兼容性要求、提交或发布前必须通过什么检查。已经由代码、工具或常识保证的内容不必重复；模糊的“注意质量”无法成为可靠约束。

### 维护方式

维护应由实际错误驱动：记录 Agent 反复犯的、可以通过规则预防的问题；同时定期删除不会改变行为的条目。文章介绍 `/init` 作为起步工具、`/memory` 作为维护辅助，但具体命令行为要按版本确认。

## 与已有知识的关系

[[Claude Code 记忆与上下文管理]] 把 `CLAUDE.md` 放在静态记忆层；[[Claude Code 大型代码库实践]] 讨论根文件长度、子目录规则与代码检索的配合；[[Claude Code 工程化六件套]] 将它与 Skill、Subagent、MCP、Hook 和 Plugin 组合。[[Codex 工程化能力]] 中的 `AGENTS.md` 是另一种产品的相近规则机制，不能假设配置完全相同。

## 我的理解

规则文件应像接口契约，而不是项目百科全书。每条规则都应该能回答“什么时候适用、具体要做什么、如何验证”，并且有明确的所有者和淘汰机制。对高风险操作，规则只能提供上下文，真正的阻断应放在权限、工具参数、Hook 或测试门禁中。

## 相关主题

- [[Claude Code 记忆与上下文管理]]
- [[Claude Code 大型代码库实践]]
- [[Claude Code 工程化六件套]]
- [[Codex 工程化能力]]
- [[Harness Engineering]]

## 来源

- 来源文件：`raw/articles/2026-09-03-CLAUDE-md维护.md`
- 补充来源：`raw/articles/2026-09-03-Claude-Code大型代码库实践.md`、`raw/articles/2026-09-03-Claude-Code六件套.md`
- 原始文章：https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247557733&idx=1&sn=dbb3a9a9c6103c2d5dc1506b21f6b2ef&chksm=f98ca6cfcefb2fd9e3821b37b57cc78cb979395313a4bb3b35909b08a3d78623f6c42952cb26#rd&scene=21#wechat_redirect
- 作者/日期：小林coding，2026-05-20；补充文章发表于 2026-05-22、2026-07-28

## 待核实

- `CLAUDE.md` 的实际加载顺序、文件路径、长度建议、`/init` 和 `/memory` 行为需要当前版本文档或源码验证。
- 文章引用的 Anthropic 团队维护经验不是本地项目的强制规范。
