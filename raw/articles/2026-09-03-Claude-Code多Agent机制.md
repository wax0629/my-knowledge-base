---
type: source
ingested_at: 2026-09-03
published_at: 2026-05-09
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247557309&idx=1&sn=db872d9df4336797d2c364b5c4e4e880&chksm=f98ca417cefb2d01139bdb082b2a6b862a217371c71c53658800ca253cf615600e654cd36d00#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 7
author: 小林coding
topics:
  - Claude Code
  - Multi-Agent
  - Subagent
  - Coordinator-Worker
  - 异步通信
  - 上下文隔离
status: processed
capture: webpage_summary
---

# 面试官皱眉：“你知道 Claude Code 多Agent实现机制吗？” 我：“何止知道？我还看过源码”，他愣了…

## 保存说明

公众号页面已读取。本文件保存文章对多 Agent 机制的结构化摘要；涉及 Claude Code 内部源码的细节均应视为文章描述，未在本次入库中独立验证。

## 来源信息

- 原文标题：面试官皱眉：“你知道 Claude Code 多Agent实现机制吗？” 我：“何止知道？我还看过源码”，他愣了…
- 作者/账号：小林coding
- 页面发布时间：2026-05-09 15:26

## 内容摘要

文章将 Claude Code 的多 Agent 形态归纳为父子型、平级协作型和 Coordinator-Worker 型，并重点分析 Subagent 的工具/上下文隔离、消息驱动通信、Fork 优化和协调者并行调度。

## 关键内容

- 常规 Subagent 由主 Agent 通过工具派出，拥有自己的工具池、上下文和生命周期；例如 Explore 类型的子 Agent 更适合只读探索。
- 隔离不是简单给一个空上下文，而是按字段决定继承、克隆或关闭：工具权限、读缓存、全局状态、任务注册、深度计数等分别处理，以防污染父 Agent 或递归失控。
- 父子通信采用消息驱动模型：父 Agent 把消息放入子任务的信箱，子任务异步运行；完成、失败、被终止等状态通过通知回到父 Agent。这样可以避免同步阻塞并支持并行。
- Fork Subagent 复用尽量相同的提示词前缀和缓存，降低重复渲染、延迟和成本；适合需要相同上下文基础的分支任务。
- Coordinator 模式让协调者只负责拆分、派发、收集和合成，Worker 之间不直接通信；文章强调并行优先、工具权限分级、合成不转发和限制递归深度。

## 与专栏其他文章的关系

本篇是 [[Harness Engineering]] 中“编排、分工与失败恢复”的具体案例，也与 [[Graph Engineering]] 的节点间调度相连；主循环与工具执行细节见 [[Claude Code 主循环与 Query 流程]]。

## 待核实

- 文章声称的源码类型名、工具名、XML 通知和缓存节省比例需要对应版本源码核对。
- 平级协作型是否被产品直接支持，不能仅凭文章的分类推断。
