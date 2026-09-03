---
type: source
ingested_at: 2026-09-03
published_at: 2026-04-15
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247556454&idx=1&sn=ad92c367b10877933f4556d0aceb497c&chksm=f98d59cccefad0da61a2a320741f5a2d2c181aefa407c702a84bb2b578bbcd49fd75a895f214#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 5
author: 小林coding
topics:
  - Harness Engineering
  - Context Engineering
  - Agent 工程化
  - 评估与恢复
status: processed
capture: webpage_summary
---

# 鹅厂面试官：“你怎么看 Harness Engineering？” 我：“就是给大模型套缰绳” 他拍桌：终于有人说明白了

## 保存说明

公众号页面已读取。本文件保存文章摘要和概念归纳，不替代原文全文。

## 来源信息

- 原文标题：鹅厂面试官：“你怎么看 Harness Engineering？” 我：“就是给大模型套缰绳” 他拍桌：终于有人说明白了
- 作者/账号：小林coding
- 页面发布时间：2026-04-15 10:47

## 内容摘要

文章把 Prompt Engineering、Context Engineering 和 Harness Engineering 看成瓶颈逐步外移的三个阶段：先解决“怎么说”，再解决“喂什么”，最终解决 Agent 如何在真实环境里稳定、可验证地完成一串任务。Harness 不是某个单一组件，而是围绕模型构建的执行系统。

## 关键内容

文章把 Harness 拆成六层：

1. 上下文精细管理：选择、裁剪、分层和恢复模型所需信息。
2. 工具系统治理：明确工具的能力、参数、权限和调用边界。
3. 任务全局编排：安排步骤、并行、依赖、暂停和恢复。
4. 记忆与状态分层：区分会话上下文、长期记忆、任务状态和外部事实。
5. 评估与观测：记录过程与结果，用独立评估判断是否真的完成。
6. 约束、校验与失败恢复：把安全规则和可重试/人工接管路径落到系统中。

文章还讨论长任务漂移、自评偏乐观、规范文件过长、代码技术债和“老技术更稳”等问题，主张把可确定的约束交给代码、工具和测试，不把可靠性全部寄托在 Prompt 上。

## 与专栏其他文章的关系

[[Loop Engineering]] 是 Harness 走向持续自动运行的延伸；[[Claude Code 工程化六件套]] 给出规则、Skill、Subagent、MCP、Hook 和 Plugin 的具体落点；[[Graph Engineering]] 则进一步处理多个执行节点之间的依赖关系。

## 待核实

- Harness Engineering 的术语来源、边界和行业共识仍在演进，本文主要是作者的解释框架。
- 文章提到的外部人物、案例和方法需要回查原始文章或公开实现。
