---
type: wiki
updated_at: 2026-09-03
topics:
  - Agent Skills
  - Claude Code
  - 渐进式披露
  - 知识加载
  - 工具编排
---

# Agent Skills 与渐进式披露

## 摘要

Skill 不只是写步骤的 Markdown，而是一个可发现、可探索的知识与工具文件夹。它的关键机制是渐进式披露：常驻上下文只保留描述，匹配任务后再读取主文档，需要更深细节时才打开参考资料、脚本或模板，从而把可复用能力与上下文成本分离。

## 核心内容

### 文件夹形态

最小 Skill 需要 `SKILL.md`，通常包含 frontmatter、适用时机、输入输出、操作步骤和坑点。可选资源包括 `references/`、`scripts/`、`assets/` 或输出模板。模型可以根据当前步骤继续探索这些资源，而不是启动时全部加载。

### 三层加载

1. 描述层：名称和 description 常驻，用于触发匹配。
2. 主文档层：任务匹配后加载 `SKILL.md` 的流程和边界。
3. 资源层：主文档指向的参考资料、脚本和模板在真正需要时读取或执行。

这种结构让 Skill 同时成为知识容器和加载策略；`/命令` 与模型自主选 Skill 可以复用同一套加载逻辑。文章还描述 `$ARGUMENTS` 参数替换，以及本地 Skill 正文中 `!\`命令\`` 的动态内容展开。

### 写作与安全

description 应写清“什么时候应该使用”，正文应包含前置条件、失败案例、参数陷阱、验证方法和人工确认边界。脚本适合负责确定性计算与编排，模型负责理解与决策。文章指出，来自 MCP 的远程 Skill 属于不可信内容，不应执行正文里嵌入的本地命令。

### 共享与反馈

Skill 可以放在项目仓库中随代码共享，也可以通过 Plugin 分发。调用次数、成功率、失败类型和用户反馈可用于判断它是否真的减少了重复工作，而不是只增加了文档数量。

## 与已有知识的关系

[[Claude Code 项目规则与 CLAUDE.md]] 适合放每次都要遵守的稳定规则；Skill 适合低频、专项、需要较多步骤的知识。[[Claude Code 工程化六件套]] 记录其与 Subagent、MCP、Hook 和 Plugin 的组合；[[Claude Code 记忆与上下文管理]] 使用了相同的索引常驻、正文按需思想。

## 我的理解

把所有方法都塞进 system prompt 会让模型“知道很多但分不清什么时候用”。Skill 的价值在于把触发条件、流程、资源和验证绑定起来，并把上下文加载延迟到真正需要的时刻。写 Skill 时首先应收集失败样本，而不是先写一篇完整教程。

## 相关主题

- [[Claude Code 项目规则与 CLAUDE.md]]
- [[Claude Code 工程化六件套]]
- [[Claude Skills 实践]]
- [[Claude Code 记忆与上下文管理]]
- [[Harness Engineering]]

## 来源

- 来源文件：`raw/articles/2026-09-03-Claude-Skills实践.md`、`raw/articles/2026-09-03-Claude-Code-Skill机制.md`
- 补充来源：`raw/articles/2026-09-03-Claude-Code六件套.md`
- 原始文章日期：2026-06-18、2026-07-21、2026-07-28
- 原始链接：<https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247558967&idx=1&sn=bb508feae2a5a5cfd28a12f4ab4130df&chksm=f98ca39dcefb2a8b9152a7c25587ce1dabb4044f290670ffbeec49fbff66859c5c10fc87bf4a#rd&scene=21#wechat_redirect>

## 待核实

- Skill 的扫描目录、触发匹配、来源优先级和远程内容安全规则需要按当前 Claude Code 版本核对。
- 文章引用的 Anthropic 内部 Skill 数量、分类和使用数据尚未独立验证。
