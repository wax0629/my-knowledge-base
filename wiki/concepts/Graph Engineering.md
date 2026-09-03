---
type: wiki
updated_at: 2026-09-03
topics:
  - Graph Engineering
  - Agent 编排
  - 任务依赖
  - 并行执行
  - 状态机
  - LangGraph
---

# Graph Engineering

## 摘要

Graph Engineering 是用节点、边和状态表达复杂任务依赖的编排方法。它不是 Loop Engineering 的替代品：loop 关注单个 Agent 节点内部如何思考、调用工具和修正，graph 关注多个执行单元如何串并行、分支、汇合、重试和恢复。

## 核心内容

### Node、Edge、State

- Node 是一个职责明确、可独立测试和替换的执行单元，可以是 Agent、普通代码、数据库查询或人工审批。
- Edge 决定下一步走向。确定性边由代码规则决定；模型决策边把需要语义判断的路由交给模型；条件边根据结果选择分支。
- State 是字段固定的结构化对象，记录当前阶段、节点产出、错误、重试次数、成本和需要传给后续节点的事实。

能写死的路径应尽量写死，把模型判断留给真正需要理解语义的分支。通过显式状态和边，流程可以定位失败节点、只重跑局部并保留审计记录。

### 与 Loop 的关系

一个 loop 可以视为只有一个节点和一条指回自身的边的最小 graph。将调研、实现、测试、审查拆成多个节点后，可以并行执行互不依赖的部分，在汇合节点统一合成结果；失败节点可以回到返工节点，不必整条流程重来。

### 与 LangGraph 的关系

LangGraph 是实现图式 Agent 编排的一种框架；Graph Engineering 是更宽的架构和流程设计思想。即使不用特定框架，也可以用任务表、状态机、队列、工作树和 CI 组合出类似的显式依赖。

### 多 Bot 管理案例

Grok Bot 的产品报道把管理 Bot、多个职责型 Worker Bot、定期汇报和最终摘要描述成一个多节点任务图。这个案例可以帮助理解管理者分派、Worker 并行、消息边和汇合节点，但报道没有提供足够实现细节，不能据此确认产品内部真的采用某个图框架。

## 与已有知识的关系

[[Loop Engineering]] 记录单个持续循环的触发、隔离、知识、连接和记忆；[[Harness Engineering]] 记录节点内部的工具、状态、评估和恢复；[[Claude Code 多智能体协作]] 提供 Coordinator-Worker、Fork 和并行通信案例；[[Grok Bot 与云端多 Agent]] 提供云端常驻多 Bot 的产品报道案例；[[Agent 运行时与多入口模式]] 提供单一核心循环的运行时视角。

## 我的理解

Graph 的价值是把“下一步为什么是这一步”从隐含在 Prompt 里的模型行为，部分变成可检查的依赖图。实践时可先画出节点的输入输出、可并行关系、失败分支和人工门禁，再选择框架。不要为了形式化而把简单任务复杂化；当任务存在多个独立角色、条件分支或局部重试需求时，显式 graph 才有明显收益。

## 相关主题

- [[Loop Engineering]]
- [[Harness Engineering]]
- [[Claude Code 多智能体协作]]
- [[Agent 基础概念与协议]]
- [[GraphRAG 与 LightRAG]]

## 来源

- 来源文件：`raw/articles/2026-09-03-Graph-Engineering.md`
- 补充来源文件：`raw/articles/2026-09-03-Grok-Bot与云端多Agent.md`
- 补充来源：`raw/articles/2026-09-03-Loop-Engineering.md`、`raw/articles/2026-09-03-Loop-Engineering实操.md`
- 原始文章：https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247560325&idx=1&sn=2d8aff16200b26fe1802c555c83b0618&chksm=f98ca82fcefb2139ba39c5e80c4ff33e65c6fd4e7e59cf5dd2bb1c6adadf84a24959b9af15ce#rd&scene=21#wechat_redirect
- 补充文章：https://mp.weixin.qq.com/s/VOMprzcbm93k6QqgoYJ5ZA
- 作者/日期：小林coding，2026-07-24

## 待核实

- Graph Engineering 是否已形成统一行业术语和最佳实践尚待观察。
- LangGraph 当前 API、Claude Code 可实现的编排方式和外部文章观点需要独立核对。
- Grok Bot 报道中的管理 Bot、Worker Bot 和群聊协商机制需要产品资料或实测确认。
