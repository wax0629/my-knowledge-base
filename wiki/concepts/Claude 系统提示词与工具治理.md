---
type: wiki
updated_at: 2026-09-03
topics:
  - 系统提示词
  - Agent 安全
  - 工具治理
  - 长期记忆
  - 并发控制
  - Claude
---

# Claude 系统提示词与工具治理

## 摘要

专栏中两篇文章以网传的 Claude Fable 5 和 Claude Opus 5 系统提示词为材料，讨论系统提示词如何描述工具使用时机、文档优先、用户确认、安全红线、记忆读写和思考深度。由于材料真实性和版本均未确认，本条目保留的是可迁移的工程思想，而不是 Claude 的已证实内部规格。

## 核心内容

### Prompt 负责意图，接口负责约束

文章用 `ask_user_input`、`create_file` 和 `message_compose` 等示例说明：提示词可以告诉模型何时询问、先解释什么、何时给方案；工具的参数顺序、权限检查、版本号和返回结构则可以强制“必须带什么”。能由接口保证的要求，不应只写成自然语言提醒。

### 记忆与并发

网传 Opus 5 材料被文章描述为文件化长期记忆：先看索引，再按需读取正文；写入区分覆盖、追加和局部替换，并携带版本号。多个客户端同时修改时，使用类似乐观锁的版本检查，冲突后读取最新内容、合并并重试。

### 隐私与使用边界

文章强调长期记忆应少记、慎用：政治、健康、证件、金融账号和实时位置等敏感信息不应随意保存；即使某条事实可以保存，也只有在真正改变当前回答时才应注入。旧记忆、文件路径和配置状态都应在行动前重新验证。

### 工具路由与思考深度

工具数量增加后，模型需要根据任务目标、工具描述和调用前置条件做路由；任务复杂度还可以影响思考深度、预算和是否先做计划。工具说明书、文档和外部状态必须分层，避免把全部能力和细节无差别地塞进每次上下文。

## 与已有知识的关系

[[Claude Code 记忆与上下文管理]] 记录文件化记忆、索引和老化验证；[[Claude Code 源码与架构]] 讨论工具元数据和安全治理层；[[Harness Engineering]] 将 Prompt、接口、测试和恢复机制放入更大的系统边界；[[Claude Code 工程化六件套]] 提供 Hook、MCP 和 Plugin 等可执行落点。

## 我的理解

系统提示词最有价值的部分不是神秘措辞，而是把“何时做、为何做、何时停”说清楚，并把“必须携带的版本、ID、授权和证据”做进工具接口。长期记忆一旦可被多个端读写，就已经是有并发、隐私和过期问题的状态系统，必须像数据库一样设计和测试。

## 相关主题

- [[Claude Code 记忆与上下文管理]]
- [[Claude Code 源码与架构]]
- [[Harness Engineering]]
- [[Claude Code 工程化六件套]]
- [[Agent Skills 与渐进式披露]]

## 来源

- 来源文件：`raw/articles/2026-09-03-Claude-Fable-5系统提示词.md`、`raw/articles/2026-09-03-Claude-Opus-5系统提示词.md`
- 原始文章：https://mp.weixin.qq.com/s?__biz=MzUxODAzNDg4NQ==&mid=2247559033&idx=1&sn=1679aad1869bed534723c98da1549eb1&chksm=f98ca3d3cefb2ac52e2e27e619fa71d298906c7e9c2f3a06f22b2f8203570d1717d1a198e3fc#rd&scene=21#wechat_redirect
- 补充文章日期：2026-06-21、2026-08-05
- Opus 5 文章引用材料：https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/OPUS-5.md

## 待核实

- Claude Fable 5、Claude Opus 5 及相关系统提示词材料的真实性、官方性、完整性和版本均未确认。
- `memory_read`、`memory_write`、`memory_append`、`memory_str_replace`、`if_version` 等名称不能当作公开 Claude 产品 API。
