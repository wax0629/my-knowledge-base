---
type: source
ingested_at: 2026-09-03
published_at: 2025-02-24
accessed_at: 2026-09-03
source_type: research_paper
source_url: "https://arxiv.org/abs/2502.17416"
pdf_url: "https://arxiv.org/pdf/2502.17416"
html_url: "https://arxiv.org/html/2502.17416"
authors:
  - Nikunj Saunshi
  - Nishanth Dikkala
  - Zhiyuan Li
  - Sanjiv Kumar
  - Sashank J. Reddi
topics:
  - 循环 Transformer
  - 潜在推理
  - 测试时计算
  - 推理与记忆
status: processed
source_version: v1
publication: ICLR 2025
capture: full_text_read_and_summary
---

# Reasoning with Latent Thoughts: On the Power of Looped Transformers

## 保存说明

本文件根据 arXiv HTML 正文、摘要、实验章节和理论章节整理。论文研究的是循环 Transformer 的一般能力，不是对 OpenAI Astra 的技术披露。

## 核心问题

论文提出：很多推理任务需要的是较大的计算深度，而不一定需要同等规模的独立参数。若把一个 k 层 Transformer 的函数重复 L 次，并让这些循环共享权重，可以用大约 k 层的参数获得接近 k×L 层非循环模型的有效深度。

论文用 `(k x L)` 表示 k 层模型循环 L 次，用 `(k x 1)` 表示同参数规模的浅层基线，用 `(kL x 1)` 表示独立参数、相同有效深度的基线。

## 实验结论

### 合成推理任务

- 在多位数加法、p-hop induction 和 i-GSM（符号化的小学数学问题）上，循环模型明显优于同参数量的浅层模型，并接近或达到同 FLOPs 的深层非循环模型。
- 在加法任务中，一个 1 层模型循环 12 次就能达到接近 12 层基线的效果，但参数量约为后者的 1/12。这支持“任务更依赖深度而非参数量”的判断。
- p-hop induction 需要反复回溯和检索上下文。论文理论上给出只用常数层、循环约 log(p) 次即可解决该问题的构造，与非循环模型的深度下界相符。

### 语言模型实验

- 论文在 Pile 上训练约 1B 参数的语言模型，并比较 24 层非循环模型、不同层数的循环模型及同参数量基线。
- 循环模型的验证集困惑度和闭卷问答通常较差，说明它的记忆容量不占优。
- 在开放式问答、数学文字题和 reasoning primitives 上，循环模型在相同困惑度下表现更好，部分任务甚至超过独立参数更多的深层基线。
- 研究者把这种差异称为对推理的归纳偏置：循环结构把更多容量放在反复加工上下文和执行迭代算法上，而不是单纯记忆事实。
- 有效深度增加时，任务准确率大致可用 `accuracy = alpha * log(depth) + beta` 描述；推理任务中循环带来的深度收益相对更明显。

### 循环启发的正则化

论文还尝试在普通深层模型中加入正则项，使相邻 k 层的参数余弦相似度更高，得到“近似循环”的模型。实验显示，在基本不损害困惑度的情况下，开放问答和推理任务可以改善。这是一个独立的训练方法，不等同于真正的权重共享。

## 理论结论

- 循环模型可以表达许多适合用迭代算法解决的推理任务。
- 循环 Transformer 可以模拟某些非循环 Transformer，说明参数共享不必然意味着表达深度不足。
- 论文给出理论构造，说明循环模型可以模拟另一模型的多步 CoT；在这个意义上，每轮循环可以在隐藏空间中产生多个 latent thoughts，而不必每步都解码成词。

## 关键边界

- 论文证明的是表达能力和特定任务上的实验结果，不是“循环模型在所有推理任务上都更强”。
- 理论模拟使用了特定的掩码、虚拟 token 和模型构造，不能直接等同于现实产品的训练和推理实现。
- 语言建模实验规模、数据和任务覆盖有限；论文结论支持研究方向，但不能据此推断某个商业模型的内部架构。

## 来源

- arXiv 摘要页：`https://arxiv.org/abs/2502.17416`
- arXiv HTML 全文：`https://arxiv.org/html/2502.17416`
- DOI：`https://doi.org/10.48550/arXiv.2502.17416`
- 首次提交：2025-02-24；arXiv 页面备注：ICLR 2025
- 关联文章：`raw/articles/2026-09-03-OpenAI-Astra与循环Transformer.md`

## 待核实

- 论文实验主要基于 2025 年前后的模型规模，循环结构在当前闭源模型上的收益需要逐模型复测。
- “推理归纳偏置”是实验归纳，具体由优化、数据、权重共享还是有效深度造成的比例仍需机制研究。
