---
type: wiki
updated_at: 2026-09-03
topics:
  - LLM
  - Agent
  - Workflow
  - ReAct
  - Function Call
  - MCP
  - Skills
  - A2A
---

# Agent 基础概念与协议

## 摘要

Agent 可以理解为以 LLM 为推理核心、通过工具、记忆、规划和循环与外部世界交互的任务执行系统。Workflow 更偏代码预先控制流程，Agent 更偏模型根据上下文选择下一步；Function Call、MCP、Skills 和 A2A 分别解决调用能力、连接工具、承载方法知识和 Agent 间协作的问题。

## 核心内容

### LLM、Agent 与 Workflow

- LLM 负责语言理解、推理和生成，但不会因为能生成文本就天然拥有外部执行、持久记忆或长期规划能力。
- Agent 在 LLM 外围增加工具、状态/记忆、规划和循环，使任务可以经过多轮“观察—决策—行动”完成。
- Workflow 通常由程序显式规定步骤；Agent 把部分步骤选择交给模型。真实系统可以混合两者：确定性路径由代码控制，需要语义判断的节点再交给模型。

### 常见 Agent 模式

- ReAct：每轮根据当前观察决定下一步行动。
- Plan-and-Execute：先形成计划，再按计划执行并处理偏差。
- Reflection：执行后引入检查或批评步骤。
- Multi-Agent：把任务分给多个职责明确的 Agent，再协调或合成结果。

### 四个能力/协议层

| 名称 | 主要解决的问题 | 在系统中的位置 |
| --- | --- | --- |
| Function Call | 模型如何结构化地请求外部函数 | 能力调用层 |
| MCP | Agent 如何发现和连接工具、资源、提示 | 工具连接层 |
| Skills | Agent 如何获得一套可复用的做事方法 | 知识与流程层 |
| A2A | Agent 如何发现、通信和协作 | Agent 间协作层 |

这些层互补而非互斥：Function Call 可以是 MCP 工具的底层调用形式，Skill 可以编排多个工具，A2A 可以把一个 Agent 暴露为另一个 Agent 可协作的执行单元。

## 与已有知识的关系

[[OpenClaw 本地自主 Agent]] 是本概念地图的本地执行案例；[[Claude Code 工程化六件套]] 展示规则、Skill、Subagent、MCP、Hook 和 Plugin 的工程化组合；[[Graph Engineering]] 将 Workflow 与 Agent 的混合控制具体化为节点、边和状态。

## 我的理解

判断一个系统是不是 Agent，不能只看它有没有 LLM 或工具，而要看谁在控制任务状态和下一步路径。Function Call 解决“能不能调用”，MCP 解决“如何接入”，Skill 解决“按什么方法做”，A2A 解决“如何让多个执行单元合作”；评估时应该分别测这四个边界。

## 相关主题

- [[OpenClaw 本地自主 Agent]]
- [[Agent Skills 与渐进式披露]]
- [[Claude Code 多智能体协作]]
- [[Graph Engineering]]
- [[RAG 检索与评估]]

## 来源

- 来源文件：`raw/articles/2026-09-03-Agent核心概念与协议.md`
- 原始文章：https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247555560&idx=1&sn=6b5f198acf46009effeb4235efdb638d&chksm=f98d5d42cefad4542071ba75ef5d36311f4d60bc0f9cd2408239a03a28d6e61159665c1e3ebc#rd&scene=21#wechat_redirect
- 作者/日期：小林coding，2026-03-29

## 待核实

- MCP、A2A 的正式规范、版本与生态状态需要回查官方资料。
- ReAct、Plan-and-Execute、Reflection 和 Multi-Agent 的适用性不能只依据文章的定性归纳。
