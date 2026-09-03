---
type: source
ingested_at: 2026-09-03
published_at: 2026-05-16
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247557512&idx=1&sn=20e66b0bfde1564616291458f9f07a5e&chksm=f98ca522cefb2c3444573aec65a8ee4932ad84a6b5d4d480e3abd8d7e86343e80602f72c16c9#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 8
author: 小林coding
topics:
  - Claude Code
  - 代码检索
  - Agentic Search
  - Grep
  - Glob
  - RAG
status: processed
capture: webpage_summary
---

# 字节面试官：“为什么Claude Code不用RAG检索代码，而是用grep？”我："因为...省钱?" 他沉默了三秒

## 保存说明

公众号页面已读取。本文件保存文章摘要和适用边界，不替代原文全文；文章对 Claude Code 实现的描述需要对应版本源码核验。

## 来源信息

- 原文标题：字节面试官：“为什么Claude Code不用RAG检索代码，而是用grep？”我："因为...省钱?" 他沉默了三秒
- 作者/账号：小林coding
- 页面发布时间：2026-05-16 15:26

## 内容摘要

文章比较代码场景的 RAG 与 Claude Code 所谓的 Agentic Search。它认为代码是动态、结构化且经常需要精确匹配的对象，预先切块和向量化会引入索引过期、语义切断、冷启动和“相似但不是目标”的问题，因此更适合让模型在当前工作树上反复探索。

## 关键内容

- 代码 RAG 的基本流程仍是切块、Embedding、向量索引和 Top-K 召回，但函数边界、调用关系、符号精确匹配和频繁提交会放大其维护成本。
- Agentic Search 把代码检索分成三个基础动作：`Glob` 按文件名/路径模式定位候选，`Grep` 按内容或符号精确搜索，`Read` 按需读取文件和上下文。
- 三件套不是孤立工具：模型先查看目录和候选结果，再决定下一步搜索或读取；在复杂仓库中可以派只读子 Agent 做探索，主 Agent 只接收压缩后的结论。
- 独立工具比让模型直接用万能 Shell 更容易做权限控制、输出限制和审计；实时搜索能避免维护过期索引，但代价是依赖清晰的起点上下文并消耗多轮工具调用。
- 文章并不认为 RAG 应被淘汰：自然语言文档、跨库语义检索、知识库问答等场景仍可使用 RAG，代码检索应按查询目标和更新频率选型，必要时采用混合方案。

## 与专栏其他文章的关系

本篇是 [[RAG 检索与评估]] 在代码领域的反例与补充，也呼应 [[Claude Code 大型代码库实践]] 中“上下文爆炸首先是检索与 Harness 问题”的判断。

## 待核实

- Claude Code 是否完全不使用 Embedding/RAG、内置工具的精确参数和输出限制，需要回到目标版本核对。
- 文章中关于索引耗时、相似度召回效果和不同产品路线的比较缺少统一实验条件。
