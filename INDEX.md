# 知识库索引

这是知识库的总入口。每个主题一行，随着 `wiki/` 更新。

## 概念

- [[Agent Skills 与渐进式披露]]：把 Agent Skill 视为可发现的知识与工具文件夹，并用渐进式披露控制上下文加载。
- [[Agent 运行时与多入口模式]]：将交互式终端、单次打印和 RPC 入口统一到同一个 Agent 运行时核心的架构模式。
- [[语言与思维]]：区分语言处理、逻辑推理和非语言表征，记录相关神经科学研究及其对 LLM 的启发边界。
- [[Claude Code 多智能体协作]]：Claude Code 多 Agent 的父子、Coordinator-Worker、隔离、异步通信与并行设计。
- [[Claude Code 记忆与上下文管理]]：静态规则、动态记忆和五层上下文压缩如何共同管理 Agent 状态。
- [[Claude Code 上下文窗口管理]]：从结果落盘、消息裁剪到 Auto-Compact 的上下文治理策略。
- [[Lost in the Middle 与长上下文]]：解释长上下文中首尾高、中间低的位置偏差及其注意力机制边界。
- [[Claude 系统提示词与工具治理]]：从网传 Claude 提示词材料中提炼工具路由、记忆并发和安全边界设计。
- [[Claude Skills 实践]]：围绕触发条件、坑点、脚本、共享和使用反馈沉淀可执行 Skill。
- [[Graph Engineering]]：用节点、边和状态编排复杂任务的依赖、分支、并行和恢复。
- [[Grok Bot 与云端多 Agent]]：记录云端常驻计算机、浏览器操作、工作流录制和多 Bot 协作的产品报道。
- [[Harness Engineering]]：围绕上下文、工具、编排、状态、评估和恢复构建可靠 Agent 环境。
- [[Loop Engineering]]：通过自动化、隔离、连接、子 Agent 和持久状态让 Agent 持续运行。
- [[循环 Transformer 与潜在推理]]：整理循环 Transformer、循环深度、Coconut 和潜在推理的论文证据，并区分 Astra 传闻与已验证事实。

## 技术

- [[Claude Code 主循环与 Query 流程]]：从 ask 到 queryLoop 的流式工具执行、状态管理和异常恢复。
- [[Claude Code 代码检索策略]]：用 Glob、Grep、Read、LSP 和子 Agent 进行实时、可验证的代码探索。
- [[Claude Code 大型代码库实践]]：在大型仓库中通过分层规则、Agentic Search、分阶段修改和团队共享控制上下文。
- [[Claude Code 工程化六件套]]：CLAUDE.md、Skills、Subagents、MCP、Hooks、Plugins 的职责分工与组合。
- [[Claude Code 源码与架构]]：从文章描述中整理 Claude Code 的引擎、工具、服务和安全治理分层。
- [[Claude Code 项目规则与 CLAUDE.md]]：项目规则文件的分层、写法、维护和验证边界。
- [[Codex 工程化能力]]：围绕项目规则、专项技能、子任务协作、外部连接和生命周期检查组织 Agent 工作。
- [[GraphRAG 与 LightRAG]]：用知识图谱、社区摘要或双层检索改善多跳与全局问题，并比较更新成本。
- [[OpenClaw 本地自主 Agent]]：把模型、工具、设备节点、消息通道和长期记忆组合成本地常驻 Agent。
- [[Pi coding agent 架构]]：Pi 项目的分层依赖、三种运行模式、请求链路和工程约束。
- [[RAG 检索与评估]]：从文档切分、召回、精排到生成评估和幻觉抑制的完整 RAG 链路。
- [[世界模型与空间智能]]：记录 World Labs Atlas 报道中的多模态空间重建、相机控制和 Real-to-Sim 路线。

## 人物

暂无主题。

## 项目

暂无主题。

## 主题

- [[Agent 基础概念与协议]]：梳理 LLM、Agent、Workflow、ReAct、Function Call、MCP、Skills 和 A2A。
- [[图解 Agent 专栏]]：小林coding“图解Agent”公众号专栏 22 篇文章的目录、阅读路径和证据边界。

## 最近更新

- 2026-09-03：读取 Astra/循环 Transformer 文章及其中三篇论文，新增循环 Transformer 与潜在推理主题、论文原料和外部核查记录。
- 2026-09-03：新增语言与思维、Atlas 世界模型/空间智能、Grok Bot 云端多 Agent 三篇来源摘要，更新相关 Agent 工程化主题。
- 2026-09-03：读取“图解Agent”专栏 22 篇文章，新增 21 篇来源摘要、专栏总览和 Agent/RAG/Claude Code 工程化主题。
- 2026-09-02：入库 Pi 架构解析文章，新增两个相关 wiki 主题并建立相互链接。
- 2026-09-02：入库 Codex 工程化能力文章，新增技术主题并与现有 Agent 架构主题关联。
