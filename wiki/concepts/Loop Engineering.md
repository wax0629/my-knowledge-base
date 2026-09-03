---
type: wiki
updated_at: 2026-09-03
topics:
  - Loop Engineering
  - 自动化 Agent
  - Worktree
  - Skill
  - Connector
  - Subagent
  - Agent 状态
---

# Loop Engineering

## 摘要

Loop Engineering 关注如何让 Agent 从一次性执行变成可以按时间或事件持续运行的工作循环。一个可用的 loop 不只是反复调用模型，还需要自动化触发、并行隔离、专项 Skill、外部连接、独立检查、持久状态、预算和人工接管。

## 核心内容

### 六个组成部分

- 自动化：按时间或事件触发循环，提供“心跳”。
- Worktree：给并行 Agent 独立目录和分支，避免同时改文件互相覆盖。
- Skill：保存项目规则、流程和坑点，让每次循环不必从零推导。
- Connector：通过 MCP 等方式接入 Issue、监控、消息和代码托管系统。
- Subagent：把产出与检查分离，用干净上下文提供第二意见。
- 磁盘记忆/状态：记录已经完成、当前阻塞和下一步，让下一次运行可以接续。

### 典型流程

文章示例是定时读取 CI 失败、Issue 和近期提交，由分诊 Skill 形成待处理项；每个问题在独立 worktree 中由一个 Agent 起草修复，再由另一个 Agent 检查，之后自动开 PR、更新工单并写回状态。无法可靠自动化的问题进入人工待办。

### 实施门槛与风险

适合 loop 的任务应高频、边界清楚、结果可判定、可回滚且成本可控。第一版应从最小闭环开始，再逐步增加并行和外部连接。运行时要显式设置循环次数、重试、超时、Token 预算、停止条件和敏感操作确认，并保留可审计日志与人工 Review。

自动化会放大三类代价：验证责任不会消失，代码产出可能造成理解债，用户可能进入“认知投降”而停止判断。Loop 的目标是放大已有判断力，不是替代对工作的理解。

## 与已有知识的关系

[[Harness Engineering]] 是 loop 的系统底座；[[Graph Engineering]] 把多个 loop 或执行节点按依赖组织成图；[[Agent Skills 与渐进式披露]] 提供可复用知识；[[Claude Code 工程化六件套]] 提供 Skill、Subagent、MCP、Hook 和 Plugin 的产品化落点。模型内部的循环计算见 [[循环 Transformer 与潜在推理]]，它与本篇的 Agent 外部持续执行循环是不同层次的问题。

## 我的理解

持续运行的 Agent 本质上是一个有状态的自动化系统。设计重点应从“模型能否完成一次任务”转向“任务如何被触发、如何被隔离、如何被判定完成、失败如何停止、明天如何接着做”。只有把这些条件写成状态、测试和门禁，loop 才不会只是无限重试器。

## 相关主题

- [[Harness Engineering]]
- [[Graph Engineering]]
- [[Agent Skills 与渐进式披露]]
- [[Claude Code 工程化六件套]]
- [[Claude Code 多智能体协作]]
- [[循环 Transformer 与潜在推理]]

## 来源

- 来源文件：`raw/articles/2026-09-03-Loop-Engineering.md`、`raw/articles/2026-09-03-Loop-Engineering实操.md`
- 原始文章：https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247558717&idx=1&sn=1b7e118a44b39ff3fff33c392f784897&chksm=f98ca297cefb2b81c617ca2d0ff862e65af3bc6fdfe9485a8ca0208e478016d33ea34e6abaf4#rd&scene=21#wechat_redirect
- 补充文章：https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247559092&idx=1&sn=b9ce478f7d8c047b614afb8e0b696a66&chksm=f98ca31ecefb2a08ceff6426f5faf44eb7e2d13721bcbba627e2235558810eb399fddc830886#rd&scene=21#wechat_redirect
- 作者/日期：小林coding，2026-06-14、2026-06-24

## 待核实

- Loop Engineering 的术语、外部引用和最佳实践仍在演进，本条目记录的是专栏的工程化归纳。
- 自动循环在生产环境中的实际成功率、成本和人工接管比例需要用项目数据验证。
