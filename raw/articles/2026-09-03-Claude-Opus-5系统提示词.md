---
type: source
ingested_at: 2026-09-03
published_at: 2026-08-05
accessed_at: 2026-09-03
source_type: article
source_url: "https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247560495&idx=1&sn=344b0e50cba2655b5ab4771233628aea&chksm=f98ca985cefb20937df45398748335c4285d1acb214f71387904bc8ed0739e7967f8454cfb86#rd&scene=21#wechat_redirect"
collection_url: "https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzUxODAzNDg4NQ==&action=getalbum&album_id=4404340926102421504&scene=126&sessionid=1788402394390#wechat_redirect"
article_number: 21
author: 小林coding
topics:
  - Claude Opus 5
  - 系统提示词
  - 长期记忆
  - 乐观锁
  - 工具路由
  - 思考深度
status: processed
capture: webpage_summary
---

# 面试官皱眉：“你看过 Claude Opus 5 系统提示词吗？”，我笑了：“刚看过，需要向我请教什么？”，他：“来，开始你的表演”

## 保存说明

公众号页面已读取。本文件保存文章对网传 Claude Opus 5 系统提示词的解析和工程启示，不保存或复述所谓提示词全文；其真实性、版本和来源均未在本次入库中独立确认。

## 来源信息

- 原文标题：面试官皱眉：“你看过 Claude Opus 5 系统提示词吗？”，我笑了：“刚看过，需要向我请教什么？”，他：“来，开始你的表演”
- 作者/账号：小林coding
- 页面发布时间：2026-08-05 16:06
- 文章引用材料：<https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/OPUS-5.md>

## 内容摘要

文章把 Fable 5 与网传 Opus 5 提示词对比，关注点从“如何说明工具”扩展到“如何治理一个有状态、会长期协作的 Agent”。重点讨论文件化长期记忆、索引与正文分离、并发更新、敏感信息、工具路由和按任务难度分配思考深度。

## 关键内容

- 文章报告的对比是：Fable 5 对记忆的说明很短，而 Opus 5 的相关规则显著变长；工具数量也从文章所称的 18 个增加到 30 个。这些数字只代表文章对网传材料的统计。
- 长期记忆被描述为一个小型文件系统：常驻的是文件路径、单行摘要、别名和来源，只有当前问题相关时才用 `memory_read` 读取正文。
- 记忆写入区分整份覆盖、追加和局部替换，并要求携带当前版本号；多个客户端同时写入时使用乐观并发控制，冲突后读取最新内容、合并并重试。
- 文章强调“能由接口保证的事情不要只靠 Prompt”：写入工具强制 `if_version`，通过参数结构阻止模型绕过读取和版本检查。
- 记忆治理包括不保存政治/健康/证件/金融/实时位置等敏感信息，也不应为展示“记得用户”而注入与当前回答无关的个人资料；旧记忆使用前要验证。
- 工具变多后，系统提示词要帮助模型按任务目标和工具描述路由；模型还应先判断任务复杂度，再选择合适的思考深度和资源预算。

## 与专栏其他文章的关系

本篇补充 [[Claude Code 记忆与上下文管理]] 的并发、隐私和工具选择部分，也与 [[Claude 系统提示词与工具治理]]、[[Harness Engineering]] 的“Prompt + 接口 + 评估”三层约束相连。

## 待核实

- Claude Opus 5、Fable 5 及 GitHub 上的提示词材料是否真实、完整、官方，尚未确认。
- 文章报告的行数、工具数量和记忆 API（如 `memory_read`、`memory_write`、`if_version`）不能当作公开产品接口。
