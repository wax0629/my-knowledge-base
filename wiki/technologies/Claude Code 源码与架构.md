---
type: wiki
updated_at: 2026-09-03
topics:
  - Claude Code
  - Agent 架构
  - Tool-Use Loop
  - System Prompt
  - 安全治理
---

# Claude Code 源码与架构

## 摘要

专栏文章把 Claude Code 客户端描述为由引擎、工具、服务和安全治理组成的分层 Agent 系统：引擎负责上下文、工具分发和循环决策，工具层提供能力，服务层提供模型/协议/压缩基础设施，治理层横跨所有层。文章的主要启示是，可靠性更多来自边界、工具元数据和异常处理，而不是某个神奇 Prompt。

## 核心内容

### 四层模型

按文章的归纳：

- 引擎层：组合用户输入、系统指令和历史，调用模型，分发工具并决定继续还是结束。
- 工具层：承载文件、Shell、搜索、子 Agent 等能力；工具同时声明读写性质、破坏性和是否可以并行等安全属性。
- 服务层：统一模型 API、上下文压缩和 MCP 等共享基础设施。
- 安全与治理层：处理权限确认、Hook、Shell 命令分析、路径逃逸和敏感操作边界。

### Tool-Use Loop 与 Plan Mode

文章将实现概括为模型输出工具请求，运行时执行工具，把结果写回上下文，再发起下一次模型请求的循环。它认为这种 Tool-Use Loop 不必要求模型把每一步内部推理都显式写成 ReAct 文本；Plan Mode 则是在执行前增加规划和边界确认，适合较大的修改任务。

### System Prompt 的职责

文章把系统提示词拆成角色定义、安全红线、工具使用指南、Git 安全协议、输出风格、环境信息以及上下文/缓存相关约束。提示词负责告诉模型什么时候做、为什么做和何时停下，工具参数、权限检查和 Hook 则负责把部分要求变成可执行门槛。

## 与已有知识的关系

[[Claude Code 主循环与 Query 流程]] 是本篇架构的执行链细化；[[Claude Code 多智能体协作]]、[[Claude Code 记忆与上下文管理]] 和 [[Claude Code 代码检索策略]] 分别展开工具隔离、状态管理和代码探索。[[Pi coding agent 架构]] 提供另一个 coding agent 的分层和共享核心案例。

## 我的理解

阅读 Agent 源码时，优先找状态对象、工具协议、事件流和错误恢复点，比只看“调模型”的正常路径更有价值。一个可扩展的引擎不应该知道每种业务工具的细节；安全属性如果能进入类型、参数或执行器，就不应只留在自然语言规则里。

## 相关主题

- [[Claude Code 主循环与 Query 流程]]
- [[Claude Code 多智能体协作]]
- [[Claude Code 记忆与上下文管理]]
- [[Claude Code 代码检索策略]]
- [[Claude 系统提示词与工具治理]]
- [[Pi coding agent 架构]]

## 来源

- 来源文件：`raw/articles/2026-09-03-Claude-Code源码与架构.md`
- 原始文章：https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247556000&idx=1&sn=01e3a55e22467c677af3e75f9a6d7c62&chksm=f98d5f0acefad61c6ea9c227ebbc65356eb14007cb66d09ac40e50a5a7538446060c61e5fefa#rd&scene=21#wechat_redirect
- 作者/日期：小林coding，2026-04-06

## 待核实

- 文章分析的 Claude Code 客户端源码泄漏、完整性、版本、行数、工具数量和类型约束尚未独立核对。
- “未采用 ReAct”是文章对实现范式的判断，不应理解为模型内部没有推理。
