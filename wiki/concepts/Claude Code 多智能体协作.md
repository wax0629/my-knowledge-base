---
type: wiki
updated_at: 2026-09-03
topics:
  - Claude Code
  - Multi-Agent
  - Subagent
  - Coordinator-Worker
  - 上下文隔离
  - 异步通信
---

# Claude Code 多智能体协作

## 摘要

专栏文章把 Claude Code 的多 Agent 机制归纳为父子型、平级协作型和 Coordinator-Worker 型，并强调四个工程问题：工具权限隔离、上下文隔离、消息驱动通信和并行结果合成。Fork Subagent 用于复用相同的提示词前缀与缓存，Coordinator 则把主 Agent 退化为调度和合成角色。

## 核心内容

### 三种形态

- 父子型：主 Agent 遇到子问题时派出 Subagent，收回结果后继续主任务。
- 平级协作型：职责对等的 Agent 通过共享状态或消息协作，状态同步较难。
- Coordinator-Worker：协调者拆分、派发、收集和合成，Worker 之间不直接通信，适合并行任务。

### 两类隔离

工具隔离不是简单复制父 Agent 的全部工具，而是按 Agent 身份提供工具子集，阻止递归派生、越权写入或污染主任务状态。上下文隔离也不是粗暴清空，而是逐字段决定继承、克隆或关闭，同时保留任务注册、状态回收和必要的通信通路。

### 消息驱动通信

文章将每个子任务描述为有状态和消息队列的执行单元。父 Agent 写入任务消息后可以继续工作；子 Agent 完成、失败或被终止时，通过异步通知把结果交回。相较同步函数调用，这种方式更适合长任务、并行和可持久化事件流。

### Fork 与 Coordinator

Fork Subagent 适合需要同样基础上下文的分支，通过复用提示词缓存降低重复成本。Coordinator 模式中，协调者只做任务流水线，Worker 按职责执行；文章提出扁平、不递归、权限分级、并行优先和协调者亲自合成等原则。

### 与云端多 Bot 的对照

另一篇产品报道把 Grok Bot 描述为云端常驻、多 Bot 通信和管理 Bot 分配 Worker 的系统，并提到不同会话之间可以传递任务摘要。它与本主题中的异步消息和 Coordinator-Worker 在结构上相似，但运行环境、权限模型和是否支持这些功能需要分别以产品实现为准，不能因为概念相似就视为同一协议。

## 与已有知识的关系

[[Claude Code 源码与架构]] 提供引擎/工具/服务/治理的宏观层次；[[Claude Code 主循环与 Query 流程]] 说明工具结果如何回到主循环；[[Grok Bot 与云端多 Agent]] 提供云端常驻多 Bot 的跨产品对照；[[Graph Engineering]] 把类似 Coordinator-Worker 的依赖、分支和汇合抽象成图；[[Harness Engineering]] 记录隔离、评估和恢复的更大边界。

## 我的理解

多 Agent 的难点不在“开几个模型实例”，而在于决定每个状态字段、工具权限和消息是否应该共享。设计时可用三个问题检查：子任务是否能独立验证、父子之间是否需要同步阻塞、结果由谁负责最终解释和验收。协调者不能只当传话筒，否则并行只增加成本，不增加可靠性。

## 相关主题

- [[Claude Code 源码与架构]]
- [[Claude Code 主循环与 Query 流程]]
- [[Graph Engineering]]
- [[Harness Engineering]]
- [[Agent 基础概念与协议]]

## 来源

- 来源文件：`raw/articles/2026-09-03-Claude-Code多Agent机制.md`
- 补充来源文件：`raw/articles/2026-09-03-Grok-Bot与云端多Agent.md`
- 原始文章：https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247557309&idx=1&sn=db872d9df4336797d2c364b5c4e4e880&chksm=f98ca417cefb2d01139bdb082b2a6b862a217371c71c53658800ca253cf615600e654cd36d00#rd&scene=21#wechat_redirect
- 补充文章：https://mp.weixin.qq.com/s/VOMprzcbm93k6QqgoYJ5ZA
- 作者/日期：小林coding，2026-05-09

## 待核实

- 文章中的 Claude Code 工具名、状态类型、XML 通知、Fork 缓存行为和成本比例需要对应版本源码核对。
- 平级协作是否由产品直接提供，不能仅凭文章的概念分类判断。
- Grok Bot 报道中关于会话间通信和多 Bot 协作的描述，不能直接证明 Claude Code 或 Grok Bot 采用同一实现。
