---
type: source
ingested_at: 2026-09-03
published_at: 2026-06-02
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247558299&idx=1&sn=cf16eb429a2c530589b31b80c2ded866&chksm=f98ca031cefb2927c43ad5dcfee1cb810fc1f1374455b5041b75c38d1159293d5614c8b5915c#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 12
author: 小林coding
topics:
  - Claude Code
  - 记忆系统
  - CLAUDE.md
  - 结构化记忆
  - 渐进式披露
status: processed
capture: webpage_summary
---

# 面试官皱眉：“你知道 Claude Code 记忆机制吗？” 我：“何止知道？我还看过源码”，他又愣了…

## 保存说明

公众号页面已读取。本文件保存文章对记忆机制的结构化摘要，不替代原文全文；源码路径、类型和阈值需要对应版本核验。

## 来源信息

- 原文标题：面试官皱眉：“你知道 Claude Code 记忆机制吗？” 我：“何止知道？我还看过源码”，他又愣了…
- 作者/账号：小林coding
- 页面发布时间：2026-06-02 14:12

## 内容摘要

文章把 Claude Code 的记忆分成静态层和动态层。静态层是分级加载的 `CLAUDE.md`，用于稳定规则；动态层是从互动中抽取的结构化记忆文件，用于偏好、项目事实和外部指针。两层都采用按需加载，避免把所有历史内容常驻在上下文中。

## 关键内容

- 动态记忆被分为 `user`、`feedback`、`project`、`reference` 四类，存储采用独立文件加索引，而不是不断变长的一份聊天摘要。
- 文章描述的写入流程由独立的 Extract Memories 代理在一轮主循环结束后执行；它与主对话分离，比较现有记忆、去重后再分类写入，并可复用主对话缓存。
- 检索先扫描记忆文件的头部信息，再让模型根据标题和描述挑选少量候选；文章描述为用 Sonnet 选择 top-5，而不是默认建立 Embedding/向量索引。
- 记忆注入使用 `system-reminder` 一类的系统标记，并附带老化提醒；若记忆包含文件、函数或 flag，使用前应回到当前工作树验证。
- 文章将结构化 schema、索引常驻/正文按需、廉价模型做选择题、时间感知与主动验证列为可迁移的设计原则。

## 与专栏其他文章的关系

本篇与 [[Claude Code 项目规则与 CLAUDE.md]] 组成“静态规则 + 动态记忆”双层模型；上下文压缩见 [[Claude Code 上下文窗口管理]]，更长远的工具与记忆治理见 [[Claude 系统提示词与工具治理]]。

## 待核实

- 四类记忆、文件路径、Extract Memories、Sonnet top-5 和老化阈值是否属于特定版本实现，尚未独立核对。
- 文章对“结构化文件优于向量检索”的评价是案例经验，不是普遍适用的检索结论。
