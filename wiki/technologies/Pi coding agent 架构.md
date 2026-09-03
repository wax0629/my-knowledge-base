---
type: wiki
updated_at: 2026-09-02
topics:
  - Pi
  - coding agent
  - 软件架构
---

# Pi coding agent 架构

## 摘要

Pi 是 `earendil-works/pi` 项目中的 coding agent。根据胖小天对 `v0.84.3` 源码的解析，它由产品层、运行时层和模型层组成，并用终端 UI、RPC、会话存储、遥测和评估等包提供支撑。它的关键架构特征是：interactive、print、rpc 三种入口共享同一个 `AgentSession` 核心。

## 核心内容

### 分层和依赖

文章记录的构建顺序为：

`tui → telemetry → ai → agent → session-backends → protocol → client → server → coding-agent`

这条顺序可以作为阅读项目依赖图的入口：底层能力先构建，产品层最后构建。主干三层分别是：

- 产品层 `pi-coding-agent`：命令行入口、三种运行模式、内置工具、扩展系统和会话持久化。
- 运行时层 `pi-agent-core`：agent 主循环、工具调度、会话状态和上下文压缩；模型调用、文件系统和 shell 通过接口替换。
- 模型层 `pi-ai`：统一多模型服务商的 SDK，可以脱离产品层单独使用。

支撑能力包括 `pi-tui`、CBOR RPC 的 `protocol/client/server`、SQLite 会话后端 `session-backends/sqlite-node`、`pi-telemetry`，以及文章提到的 `pi-evals`。

### 一个核心、三种入口

- `interactive`：TTY 环境中的完整终端 UI。
- `print`：`--print` 或管道输入的一次性模式，适合脚本。
- `rpc`：stdin/stdout 上的 JSONL 协议，供其他程序调用。

三种模式不各自实现一套 agent，而是共享 `AgentSession`。因此会话状态、上下文压缩、模型管理和持久化可以保持一致，模式之间主要改变 I/O 适配方式。

### 请求链路

一次交互大致经过以下步骤：

1. `AgentSession` 接收并追加用户消息。
2. `runAgentLoop` 组装上下文。
3. `pi-ai` 的 `Models.stream()` 调用具体服务商适配器。
4. 流式 delta 转换为统一事件，交给当前入口呈现。
5. 如果需要工具，主循环执行工具，把结果写回上下文，再发起下一轮。
6. 消息、模型切换和工具结果追加到 `~/.pi/agent/sessions/` 下的 JSONL 会话文件。

### 工程约束

文章称 Pi 支持编译成 Bun 单文件原生二进制，直接依赖使用精确版本，依赖包需满足 `min-release-age=2`，发布 CLI 通过 shrinkwrap 固定传递依赖。这些措施意在降低高权限工具的供应链风险。

## 与已有知识的关系

当前知识库之前没有 Pi 或 coding agent 主题。本条目是本次材料新建的具体项目架构主题，并从中抽取了一个更通用的设计概念：[[Agent 运行时与多入口模式]]。

## 我的理解

Pi 的可复用性主要来自边界设计：模型层、运行时层和 I/O 层可以分别替换或嵌入。阅读类似项目时，先看构建顺序和包依赖，通常比先从产品入口逐行阅读更快建立全局模型。

这篇文章的架构描述只代表其声明的源码基线，不能直接当作当前版本的 API 合同。包数量、版本和具体入口仍应以目标 commit 或最新源码为准。

## 相关主题

- [[Agent 运行时与多入口模式]]

## 来源

- 来源文件：`raw/articles/2026-09-02-Pi架构解析二.md`
- 原始文章：https://mp.weixin.qq.com/s/WB24MCub0fosrhZOlEiSAQ
- 作者/日期：胖小天，2026-09-01
- 源码基线：2026-08-28，commit `56700d4`，版本 `v0.84.3`

## 待核实

- “九个包”和支撑层包列表的计数口径存在疑点。
- 当前 Pi 源码是否仍保持相同的包划分、构建顺序和 `AgentSession` API，尚未独立核对。
- `min-release-age=2` 的单位和配置位置尚未核对。
