---
type: wiki
updated_at: 2026-09-03
topics:
  - 循环 Transformer
  - 循环深度
  - 潜在推理
  - 连续思维链
  - 测试时计算
  - Astra
---

# 循环 Transformer 与潜在推理

## 摘要

循环 Transformer 通过重复使用同一组网络层，把参数量和有效计算深度解耦；潜在推理则把部分中间计算保留在连续隐藏状态中，而不是每一步都生成可读 token。三篇论文表明，这条路线可以改善部分需要迭代、搜索或多步组合的推理任务，但它们是不同的架构和训练方案，不能直接作为 OpenAI Astra 内部实现的证据。

## 核心内容

### 一句话理解

普通 Transformer 通常把输入从固定深度的层堆栈中走一遍；循环 Transformer 让核心层重复处理隐藏状态。若基础块有 k 层、循环 L 次，独立参数仍接近 k 层，但有效计算深度约为 k x L。潜在推理进一步允许这些循环或隐藏状态在向量空间里完成中间计算，只有需要对外表达时才解码成语言。

### 三条相关但不同的路线

| 路线 | 核心机制 | 训练方式 | 论文证据 |
| --- | --- | --- | --- |
| Looped Transformer | k 层块在深度方向共享权重并循环 L 次 | 直接训练或比较循环/非循环模型 | 合成推理和语言模型中，循环结构对推理的收益高于对记忆的收益 |
| Recurrent Depth | prelude、共享 recurrent core、coda；推理时改变循环次数 | 训练时随机采样循环深度，并用截断反向传播 | 3.5B 原型在增加测试时计算后改善推理任务，报告的对照上限是 50B 级计算负载 |
| Coconut | 将最后隐藏状态直接作为下一步输入 embedding | 先 CoT，再逐阶段替换成 continuous thoughts 的课程训练 | 在需要搜索的逻辑任务上减少 token 并提高准确率，但课程训练很重要 |

三者的共同点是“把更多计算放到内部状态”；差别在于共享层的方式、计算发生在深度还是序列位置、以及是否依赖 CoT 监督。

### 论文给出的主要证据

#### Google：Reasoning with Latent Thoughts

`Reasoning with Latent Thoughts: On the Power of Looped Transformers`（ICLR 2025）在加法、p-hop induction 和 i-GSM 上发现，较浅的循环模型可以接近相同有效深度的非循环模型，并显著优于同参数量的浅层模型。语言模型实验还显示，循环模型的困惑度和闭卷记忆不一定占优，但开放问答、数学问题和 reasoning primitives 的表现相对更好。论文用理论构造说明循环模型可以表达迭代算法，并可以模拟多步 CoT。

#### Recurrent Depth：Scaling up Test-Time Compute

`Scaling up Test-Time Compute with Latent Reasoning: A Recurrent Depth Approach`（arXiv 2502.05171）训练了约 3.5B 参数、约 800B token 的 Huginn 原型。推理时增加 recurrent core 的循环次数，多个数学、常识和代码任务会继续改善；论文还展示了按 token 提前退出、KV cache 共享、连续 CoT 和自投机解码等原型能力。论文把 50B 表述为可用计算负载的对照，不是“3.5B 在所有任务上等于 50B”。

#### Coconut：连续思维链

`Training Large Language Models to Reason in a Continuous Latent Space`（Coconut，COLM 2025）把隐藏状态反馈为后续输入，在连续潜空间中延迟语言化。论文在 ProsQA 上观察到潜在状态可以保留多个候选路径，行为类似 BFS，从而减少 CoT 早期贪心承诺带来的错误。在 GSM8K 上它没有超过语言 CoT，但用更少输出 token 获得了较好的准确率/效率折中；直接去掉课程训练则效果明显下降。

### 文章与论文的关系

公众号文章《刚刚，OpenAI新Transformer火了！Astra架构首次曝光》把上述研究路线串成“循环深度让 Astra 安静地思考”的叙事。这个叙事在技术方向上有研究依据，但产品归因仍需单独验证：OpenAI 2026-09-01 官方页面确认 Astra 是即将推出的模型，并公开了网络安全能力和监控措施，却没有公布 recurrent depth 或具体 Transformer 结构。文章引用的 The Information 正文本次无法在不订阅的情况下读取。

因此，当前最稳妥的结论是：循环/潜在推理是可信且已有论文支持的研究方向；Astra 是否采用、如何采用，以及 GPT-6 是否是正式产品名，仍属于外部报道或待核实信息。

### “思考隐身”到底意味着什么

潜在推理并不意味着模型没有中间状态，而是中间状态不再以人类可读 token 的形式完整暴露。这样做可能节省序列长度、带来更自由的搜索和迭代，但也减少了直接审阅 CoT 的机会。隐藏状态轨迹、输出概率和行为测试可以提供部分证据，却不能自动等同于完整、忠实的思维过程。

### 工程与安全含义

- 可以把参数扩展、token 级 CoT 和循环深度看成不同的测试时/训练时扩展轴，实际部署应分别测算显存、FLOPs、延迟和带宽。
- 不能只看“输出 token 少”判断效率；循环次数、KV cache、并行度和硬件利用率同样决定成本。
- 任务难度可能需要自适应循环次数，简单任务早停，复杂任务继续迭代；但退出判据需要独立评估，不能只依赖模型自评。
- 文字 CoT 变少后，安全审计不能简单消失。需要结合状态轨迹、工具调用、输出行为、红队测试、监控和人工门禁建立新的观测链。
- 与 [[Lost in the Middle 与长上下文]] 的关系是互补的：潜在推理可以减少外显 token 和上下文压力，但不自动解决长上下文检索、位置偏差或状态错误传播。

## 与已有知识的关系

本条目记录“模型内部循环”，而 [[Loop Engineering]] 记录“Agent 外部持续执行循环”，两者都需要明确状态、预算、停止条件和验证，但不应混为同一架构。[[Harness Engineering]] 提供对循环计算和不可读中间状态进行约束、观测与恢复的工程框架；[[Claude Code 上下文窗口管理]] 和 [[Claude Code 记忆与上下文管理]] 则说明如何减少上下文负担、保存可恢复状态。

## 我的理解

这组论文真正改变的不是“模型突然拥有了神秘思维”，而是把“能力来自更多独立参数”改写成一个可拆分的问题：有些任务更需要更深的迭代计算，有些任务更需要更大的记忆容量。循环结构可能用较少参数获得更深计算，潜在状态可能比逐 token 语言化更适合搜索和规划；但代价是训练稳定性、可解释性、验证和服务成本都变得更难。

## 相关主题

- [[Loop Engineering]]
- [[Harness Engineering]]
- [[Lost in the Middle 与长上下文]]
- [[Claude Code 上下文窗口管理]]
- [[Claude Code 记忆与上下文管理]]
- [[Agent 基础概念与协议]]

## 来源

- 原始公众号文章：`raw/articles/2026-09-03-OpenAI-Astra与循环Transformer.md`
- Google Research 论文：`raw/papers/2026-09-03-Reasoning-with-Latent-Thoughts.md`
- Recurrent Depth 论文：`raw/papers/2026-09-03-Scaling-up-Test-Time-Compute-with-Latent-Reasoning.md`
- Coconut 论文：`raw/papers/2026-09-03-Coconut连续潜在空间推理.md`
- OpenAI 官方：`https://openai.com/index/path-to-astra/`
- The Information：`https://www.theinformation.com/articles/secret-technique-behind-openais-astra-model-sparks-security-concerns`

## 待核实

- Astra 是否使用循环深度、循环块如何组织、是否采用 latent reasoning，等待官方技术报告、系统卡、API 文档或复现实验。
- 三篇论文的结果来自不同模型、数据和训练方案，不能直接横向比较准确率或成本。
- 连续状态是否忠实表达“推理过程”、潜在轨迹中的 orbit/slider 是否具有稳定因果功能，需要更多干预式机制研究。
- 生产环境中不可读中间计算的安全监控、审计和人工接管机制仍需公开案例验证。
