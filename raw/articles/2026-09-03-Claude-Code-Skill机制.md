---
type: source
ingested_at: 2026-09-03
published_at: 2026-07-21
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247560206&idx=1&sn=880058483b49b10dd082e07bed9fdc80&chksm=f98ca8a4cefb21b2e9255dd748b7b7eb5f2bec59dbd81fef2b3214f86c2f108223b0ceecda94#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 18
author: 小林coding
topics:
  - Claude Code
  - Skill
  - 渐进式披露
  - Slash 命令
  - 动态内容
  - MCP
status: processed
capture: webpage_summary
---

# 面试官皱眉：“你知道 Claude Code 的 skill 机制吗？” 我：“何止知道？我还看过源码”，他又愣了…

## 保存说明

公众号页面已读取。本文件保存文章对 Claude Code Skill 源码机制的摘要，不替代原文全文；源码路径和行为属于文章所述版本，未独立确认。

## 来源信息

- 原文标题：面试官皱眉：“你知道 Claude Code 的 skill 机制吗？” 我：“何止知道？我还看过源码”，他又愣了…
- 作者/账号：小林coding
- 页面发布时间：2026-07-21 14:12

## 内容摘要

文章把 Skill 的核心价值归结为渐进式披露（Progressive Disclosure）：常驻上下文只放名称和描述，模型判断可能有用后才读取 `SKILL.md`，更深的参考资料、脚本和模板再按需展开。Skill 因此既是知识容器，也是知识加载策略。

## 关键内容

- 一个最小 Skill 是包含 `SKILL.md` 的文件夹；`references/`、`scripts/`、`assets/` 等目录可选，用于承载长文档、可执行脚本和输出模板。
- 渐进式披露分为三层：常驻的 frontmatter/描述、触发后的主文档、主文档进一步指向的附录和资源。这样安装大量 Skill 时不会把全部正文塞进上下文。
- 触发匹配主要依赖 Skill 的名称、描述、当前用户任务和可用来源；描述应写清适用时机与任务边界，而不是只写功能名。
- 用户输入的 `/命令` 和模型自主选择 Skill 可以落到同一套加载机制；Skill 可接收 `$ARGUMENTS`，把命令后面的参数带入正文。
- 文章还描述正文中的 `!\`命令\`` 动态展开：本地 Skill 激活时先执行嵌入命令，再把输出填回 Prompt；来自 MCP 的远程 Skill 被视为不可信内容，不执行这类嵌入命令。
- Skill 来源包括内置、用户级、项目级、Plugin 和 MCP 等；项目级 Skill 随仓库共享，来源冲突和优先级需要以实现为准。

## 与专栏其他文章的关系

本篇是 [[Agent Skills 与渐进式披露]] 的机制篇，与 [[Claude Skills 实践]] 的团队实践互补；[[Claude Code 工程化六件套]] 记录 Skill 如何与规则、Hook、MCP 和 Plugin 配合。

## 待核实

- Skill 的真实扫描目录、来源优先级、触发算法和动态命令限制需要回到当前 Claude Code 版本核对。
- 文章中的源码文件名和代码片段不应直接作为稳定 API 使用。
