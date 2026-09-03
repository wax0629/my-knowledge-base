---
type: wiki
updated_at: 2026-09-03
topics:
  - Claude Code
  - CLAUDE.md
  - Skills
  - Subagents
  - MCP
  - Hooks
  - Plugins
---

# Claude Code 工程化六件套

## 摘要

专栏把 Claude Code 的工程化能力归纳为六个互补机制：`CLAUDE.md` 管稳定规则，Skills 管按需知识，Subagents 管分工与上下文隔离，MCP 管外部连接，Hooks 管生命周期门禁，Plugins 管能力打包与分发。它们共同把一次性提示变成可复用、可审查的工作环境。

## 核心内容

| 机制 | 主要职责 | 典型内容 |
| --- | --- | --- |
| `CLAUDE.md` | 稳定项目规则 | 技术栈、命令、目录规范、安全禁区 |
| Skills | 专项知识与流程 | 评审清单、发布流程、参考资料、模板 |
| Subagents | 独立上下文与任务分工 | 探索、实现、测试、审查、并行调研 |
| MCP | 仓库外系统连接 | GitHub、工单、数据库、云文档、监控 |
| Hooks | 固定时机的自动动作 | 格式化、测试、敏感文件保护、审计 |
| Plugins | 组合、安装和共享能力 | 规则、Skill、Agent、MCP 与 Hook 的打包 |

### 组合关系

一个典型流程可以由 `CLAUDE.md` 提供项目背景，Skill 提供步骤和检查清单，Subagent 负责独立探索或 Review，MCP 读取/更新外部工单，Hook 在工具或任务生命周期上做门禁，最后通过 Plugin 把这套实践分发给团队。每一层的责任应清楚，避免把所有内容复制进规则文件。

### 工程边界

六件套扩大了 Agent 的能力，也扩大了权限、认证、成本和外部副作用。只读与写入连接器应区分，破坏性工具需要确认，Hook 失败要有明确的阻断或恢复策略，Plugin 引入的规则和脚本要经过来源审查。

## 与已有知识的关系

这是 [[Harness Engineering]] 的 Claude Code 产品化视图，与 [[Codex 工程化能力]] 的规则、Skills、Subagents、MCP、Hooks 五类机制形成跨产品对照；[[Loop Engineering]] 把其中的自动化、worktree、Skill、连接器、子 Agent 和状态组合成持续循环。

## 我的理解

六件套的价值在于职责分离：规则解决“默认遵守什么”，Skill 解决“专项任务怎么做”，Subagent 解决“谁来做”，MCP 解决“能接触哪些外部系统”，Hook 解决“什么时候强制检查”，Plugin 解决“如何复制给别人”。实际落地要先从一个可验证的高频流程开始，再逐步扩张权限。

## 相关主题

- [[Harness Engineering]]
- [[Claude Code 项目规则与 CLAUDE.md]]
- [[Agent Skills 与渐进式披露]]
- [[Claude Code 多智能体协作]]
- [[Loop Engineering]]
- [[Codex 工程化能力]]

## 来源

- 来源文件：`raw/articles/2026-09-03-Claude-Code六件套.md`
- 补充来源：`raw/articles/2026-09-03-CLAUDE-md维护.md`、`raw/articles/2026-09-03-Claude-Skills实践.md`
- 原始文章：https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247560334&idx=1&sn=8c72a7c80d6b65425686e33425d62651&chksm=f98ca824cefb2132abd2e974fde38227c68ef4160d3e0bb2d75e38f724e5eccaeb325dd1d4c6#rd&scene=21#wechat_redirect
- 作者/日期：小林coding，2026-07-28

## 待核实

- Claude Code 六件套的实际配置路径、版本支持、Hook 事件和 Plugin 安装方式需要当前文档核对。
- 与 Codex 同名能力的配置语义、权限模型和生命周期不一定相同。
