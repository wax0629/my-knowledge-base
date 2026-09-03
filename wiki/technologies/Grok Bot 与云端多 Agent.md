---
type: wiki
updated_at: 2026-09-03
topics:
  - Grok Bot
  - 云端 Agent
  - Multi-Agent
  - 浏览器操作
  - 工作流自动化
  - Agent 治理
---

# Grok Bot 与云端多 Agent

## 摘要

一篇 APPSO 文章把 Grok Bot 描述为“云端常驻计算机 + 浏览器界面操作 + 工作流录制 + 多 Bot 协作”的 Agent 产品形态。它与 [[OpenClaw 本地自主 Agent]] 的本地优先路线、[[Claude Code 多智能体协作]] 的会话级协作形成对照。由于本条目主要来自产品报道，开放范围、价格、内部架构和功能边界均应视为待核实信息。

## 核心内容

### 产品形态

按文章描述，每个 Bot 拥有一台持续运行的云端小型计算机，可以在用户设备离线时执行任务。Bot 可以登录用户已在使用的网站和应用，打开浏览器、填写表单、点击按钮并继续推进流程，因此理论上不要求目标软件提供 API 或 MCP。

### 多 Bot 与任务编排

- 用户可以创建销售、招聘、费用、Bug 复现等职责明确的 Bot，并让它们并行运行。
- Bot 之间可以通信、汇报进度、传递任务，并在群聊中协商分工。
- 文章还声称 Bot 可以创建新的 Bot，形成具有名称、头像和职位的层级化团队。
- 这种管理 Bot—Worker Bot 结构可以抽象为 [[Graph Engineering]] 中的节点、消息边和汇合节点；它也涉及 [[Harness Engineering]] 所关注的权限、状态、验证和恢复。

### 工作流录制

文章描述一种类似 Record & Replay 的工作流：用户先演示一遍任务，Bot 保存步骤；之后可以按时间计划或 Slack/GitHub 事件触发。用户在执行中纠正 Bot 后，修正可能被吸收进后续例程。该模式降低重复提示成本，但也会把错误步骤固化为自动化副作用，因此需要版本、审计、回滚和人工审批。

### 与其他 Agent 的对照

| 维度 | Grok Bot（文章描述） | OpenClaw / Claude Code 对照 |
| --- | --- | --- |
| 运行位置 | 云端专属计算机，支持后台常驻 | OpenClaw 强调本地优先；Claude Code 文章重点是会话与任务上下文 |
| 操作方式 | 可通过浏览器界面操作传统软件 | OpenClaw 连接工具、设备和消息通道；Claude Code 以代码和工具执行为主 |
| 协作方式 | 多 Bot 通信、管理者分配和群聊协商 | OpenClaw 文章以单个常驻 Agent 为主；Claude Code 有父子、Coordinator-Worker 和会话通信案例 |
| 模型选择 | 文章称绑定 Grok 系列模型 | OpenClaw 文章称可切换多家模型；Claude Code 依赖其产品支持 |

这张表是不同公众号材料之间的归纳，不是对各产品当前版本的官方承诺。

### 成本与治理

文章声称的开放订阅包括 SuperGrok Heavy 每月 300 美元、Cursor Ultra 每月 200 美元和 Cursor Teams Premium 每席位每月 120 美元，并称桌面端与 iOS 可用、Android 尚未上线。价格、地区和客户端状态变化快，应直接核对产品页面。

常驻、多 Bot 和界面自动化的主要风险包括：凭证泄露、误提交、权限越界、错误沿任务链扩散、无法回滚以及供应商/模型锁定。“不必等待下一条指令”必须配合高风险操作审批、沙箱、最小权限、预算、超时和审计。

## 与已有知识的关系

[[OpenClaw 本地自主 Agent]] 是本地常驻 Agent 的对照案例；[[Claude Code 多智能体协作]] 记录上下文隔离、异步消息和 Coordinator-Worker；[[Loop Engineering]] 关注持续触发和持久状态；[[Graph Engineering]] 关注多节点依赖与汇合；[[Harness Engineering]] 提供工具治理、验证和失败恢复的系统边界。

## 我的理解

这类产品的新增能力不只来自模型，而来自一个可持续运行的执行环境。判断它是否值得使用，应把任务完成率与副作用控制放在同一张验收表中，重点检查凭证隔离、审批触发、可回滚性、事件去重、错误传播、成本上限和模型迁移路径。演示中“会操作网页”不等于生产环境中“可以安全代办事务”。

## 相关主题

- [[OpenClaw 本地自主 Agent]]
- [[Claude Code 多智能体协作]]
- [[Harness Engineering]]
- [[Loop Engineering]]
- [[Graph Engineering]]
- [[Agent 基础概念与协议]]

## 来源

- 来源文件：`raw/articles/2026-09-03-Grok-Bot与云端多Agent.md`
- 原始公众号文章：`https://mp.weixin.qq.com/s/VOMprzcbm93k6QqgoYJ5ZA`
- 文章提供的体验入口：`https://x.ai/bot`

## 待核实

- Grok Bot 的正式发布状态、可用地区、客户端、订阅价格和企业申请方式。
- xAI、SpaceX、Cursor/Anysphere 的并购、更名和产品基础设施关系。
- 多 Bot 通信、Bot 创建 Bot、工作流录制、事件触发和浏览器自动化的实际产品边界。
- 凭证存储、权限沙箱、人工审批、审计、回滚机制和可用模型范围。
