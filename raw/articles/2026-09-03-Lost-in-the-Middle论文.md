---
type: source
ingested_at: 2026-09-03
published_at: 2023-07-06
accessed_at: 2026-09-03
source_type: research_paper
source_url: "https://arxiv.org/abs/2307.03172"
authors:
  - Nelson F. Liu
  - Kevin Lin
  - John Hewitt
  - Ashwin Paranjape
  - Michele Bevilacqua
  - Fabio Petroni
  - Percy Liang
topics:
  - Lost in the Middle
  - 长上下文
  - 注意力机制
  - 信息检索
  - Transformer
status: processed
capture: webpage_summary
---

# Lost in the Middle: How Language Models Use Long Contexts

## 保存说明

本文件保存论文的结构化摘要和机制分析，不替代论文全文。论文证明的是长上下文任务中的位置敏感性，并对架构、查询位置和指令微调做了初步分析；它没有证明某一个单独的注意力头或公式项就是唯一原因。

## 来源信息

- 论文：Lost in the Middle: How Language Models Use Long Contexts
- 作者：Nelson F. Liu 等
- arXiv 首次提交：2023-07-06；页面显示 v3 修订于 2023-11-20
- 论文状态：arXiv 页面标注已被 TACL 2023 接收

## 主要结论

- 在多文档问答和合成 key-value 检索中，相关信息位于上下文开头或结尾时表现通常较好，位于中间时明显下降，形成 U 形曲线。
- 该现象不仅出现在显式扩展上下文窗口的模型，也出现在基础模型，因此不能简单归因于指令微调。
- 打乱干扰文档顺序后仍能观察到 U 形趋势，因此也不只是搜索结果排序先验造成的。
- Encoder-decoder 模型在不超过训练时长度的输入上相对更稳健，但超过训练长度后也出现中间位置退化。
- 把查询同时放在数据前后，对合成 key-value 检索有显著帮助；对多文档问答的整体趋势改善有限。

## 与注意力机制的关系

Transformer 的注意力在形式上可以访问上下文中的位置，但访问能力不等于模型会稳定地选中并使用目标信息。对 decoder-only 模型，如果文档在前、问题在后，文档位置的隐藏表示不能读取未来的问题；最终生成位置虽然可以回看文档，却只能从未针对当前问题编码的表示中检索。

论文第 6.3 节也指出，Transformer 的 self-attention 在技术上能够检索任意 token，但模型仍表现出类似心理学“系列位置效应”的首尾优势。这说明现象是训练分布、位置表示、架构和任务负载共同作用的结果，而不是注意力可达性本身的硬限制。

## 待核实

- 论文的实验对象主要是 2023 年前后的模型，不能直接代表所有当前长上下文模型。
- “softmax 竞争导致注意力稀释”“中间位置缺少边界锚点”等是基于架构的机制解释或研究假设，不是论文已证明的唯一因果机制。
- 注意力权重图不能单独等同于模型实际使用了哪些信息，还需要结合残差流、MLP、层间路由和最终输出做机制分析。
