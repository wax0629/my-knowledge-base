---
type: wiki
updated_at: 2026-09-03
topics:
  - Harness Engineering
  - Context Engineering
  - Agent 工程化
  - 评估
  - 失败恢复
---

# Harness Engineering

## 摘要

Harness Engineering 是围绕模型构建可持续执行环境的工程方法。专栏把它放在 Prompt Engineering 和 Context Engineering 之后：模型越能连续工作，瓶颈越从“怎么问”转向上下文、工具、编排、状态、评估、约束和恢复。Harness 不是一个单独组件，而是一套把 Agent 约束在可验证轨道上的系统。

## 核心内容

### 从 Prompt 到 Harness

- Prompt Engineering 解决如何表达任务。
- Context Engineering 解决在正确时机提供哪些代码、文档、工具和历史。
- Harness Engineering 解决 Agent 如何在真实环境中执行多步任务、处理权限和失败、持续被验证。

### 六个层面

1. 上下文管理：分层注入、裁剪、压缩和恢复。
2. 工具治理：明确能力、参数、权限、破坏性和并行属性。
3. 任务编排：处理步骤、依赖、并行、暂停和恢复。
4. 记忆与状态：区分会话历史、长期记忆、任务状态和外部事实。
5. 评估与观测：记录过程和结果，用独立判定而非模型自评确认完成。
6. 约束与恢复：设置权限门禁、测试、重试、止损和人工接管。

### 主要难题

长任务会发生上下文漂移，Agent 的自评往往偏乐观，规则文件可能越写越长，自动生成代码可能积累技术债。文章的共同答案是把能由代码、接口、测试和流程保证的要求固化下来，不把可靠性全部寄托在 Prompt 上。

### 常驻多 Bot 的额外边界

Grok Bot 的产品报道提供了一个高风险案例：云端计算机可以在后台登录网站、操作界面并让多个 Bot 继续协作。这样的系统把“工具治理”和“失败恢复”从代码仓库扩展到凭证、网页副作用、事件触发、任务预算和人工审批；“能继续执行”本身不能作为“应该继续执行”的依据。

## 与已有知识的关系

[[Claude Code 工程化六件套]] 是 Harness 的产品化落点；[[Grok Bot 与云端多 Agent]] 展示常驻云端、多 Bot 和浏览器操作带来的治理问题；[[Loop Engineering]] 把 Harness 扩展为有触发器和持久状态的持续循环；[[Graph Engineering]] 处理多个执行节点之间的依赖和汇合；[[Codex 工程化能力]] 提供另一个产品中的规则、技能、子任务、连接和 Hook 对照。

## 我的理解

Harness 的核心产物不是一段更长的系统提示词，而是“模型能做什么、何时能做、如何证明做对、失败后如何恢复”的可执行边界。设计 Agent 时应先列出不可接受的失败，再决定哪些交给模型、哪些交给工具参数、哪些交给测试或人工审批。

## 相关主题

- [[Loop Engineering]]
- [[Graph Engineering]]
- [[Claude Code 工程化六件套]]
- [[Claude Code 多智能体协作]]
- [[Codex 工程化能力]]

## 来源

- 来源文件：`raw/articles/2026-09-03-Harness-Engineering.md`
- 补充来源文件：`raw/articles/2026-09-03-Grok-Bot与云端多Agent.md`
- 补充来源：`raw/articles/2026-09-03-Claude-Code大型代码库实践.md`、`raw/articles/2026-09-03-Loop-Engineering.md`、`raw/articles/2026-09-03-Loop-Engineering实操.md`
- 原始文章：https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247556454&idx=1&sn=ad92c367b10877933f4556d0aceb497c&chksm=f98d59cccefad0da61a2a320741f5a2d2c181aefa407c702a84bb2b578bbcd49fd75a895f214#rd&scene=21#wechat_redirect
- 补充文章：https://mp.weixin.qq.com/s/VOMprzcbm93k6QqgoYJ5ZA
- 作者/日期：小林coding，2026-04-15；补充文章发表于 2026-05-22、2026-06-14、2026-06-24

## 待核实

- Harness Engineering 的术语来源和行业边界仍在演进，本条目主要记录专栏的解释框架。
- 外部博客中的案例、人物观点和实践效果需要分别回查原始来源。
- Grok Bot 的具体权限、审批、凭证隔离和错误恢复机制需要官方资料或实测确认。
