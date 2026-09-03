---
type: source
ingested_at: 2026-09-03
published_at: 2026-05-22
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247557838&idx=1&sn=c4bc3f0537ef2b1fdd3b26e2c9c8d3ae&chksm=f98ca664cefb2f72d9fdbb65753dda2d2fa99ef3e089c53814da23eb7a043cf8d6f96f80fd41#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 11
author: 小林coding
topics:
  - Claude Code
  - 大型代码库
  - Harness Engineering
  - Agentic Search
  - LSP
  - 团队协作
status: processed
capture: webpage_summary
---

# 面试官皱眉：“公司项目几百万行代码，Claude Code 怎么扛得住？”我：“换 Opus 4.7”，他叹气：模型是地板，harness 才是天花板

## 保存说明

公众号页面已读取。本文件保存文章对大型代码库实践的结构化摘要，不替代原文全文；产品版本和外部博客结论需独立核对。

## 来源信息

- 原文标题：面试官皱眉：“公司项目几百万行代码，Claude Code 怎么扛得住？”我：“换 Opus 4.7”，他叹气：模型是地板，harness 才是天花板
- 作者/账号：小林coding
- 页面发布时间：2026-05-22 14:12

## 内容摘要

文章认为大型代码库的问题首先不是“换更大的模型”，而是要把 Harness 搭好：用分层规则、Agentic Search、LSP、任务拆分、独立会话和团队共享机制控制上下文与变更范围。模型是能力底座，工程化环境决定可用上限。

## 关键内容

- 大型仓库不应试图一次性塞进上下文；文章推荐以清晰入口、目录和符号线索启动搜索，让模型逐步定位当前代码。
- `CLAUDE.md` 根文件只保留跨模块约定和关键陷阱，模块细节放入子目录；文章引用“控制在约 200 行以内”的经验建议，但该数字需独立验证。
- Agentic Search 通过 `Glob`、`Grep`、`Read` 逐步探索；LSP 可补充符号定义、引用和跳转信息，减少单纯文本搜索的误判。
- 跨几十个文件的修改应该分阶段实施：先调查和计划，再按边界执行，持续运行测试，并把独立检查交给干净上下文的子 Agent。
- 团队推广可以从高频操作做成 Skill，再用 Plugin 分发，用 MCP 连接内部系统，并指定维护者持续更新规则与流程。
- 文章提醒不适合把高风险架构、鉴权、支付和生产部署完全交给无人值守的 Agent；权限、审查和人工接管仍是必要边界。

## 与专栏其他文章的关系

本篇把 [[Harness Engineering]] 落到大型仓库实践，连接 [[Claude Code 代码检索策略]]、[[Claude Code 项目规则与 CLAUDE.md]] 和 [[Claude Code 多智能体协作]]。

## 待核实

- 文章引用的模型上下文规模、团队实践、LSP 具体接入方式和产品功能需回到原始资料或当前版本核对。
- “模型是地板、Harness 是天花板”是文章的观点性总结，不是可量化定律。
