---
type: source
ingested_at: 2026-09-03
published_at: 2025-02-07
accessed_at: 2026-09-03
source_type: research_paper
source_url: "https://arxiv.org/abs/2502.05171"
pdf_url: "https://arxiv.org/pdf/2502.05171"
html_url: "https://arxiv.org/html/2502.05171"
authors:
  - Jonas Geiping
  - Sean McLeish
  - Neel Jain
  - John Kirchenbauer
  - Siddharth Singh
  - Brian R. Bartoldson
  - Bhavya Kailkhura
  - Abhinav Bhatele
  - Tom Goldstein
topics:
  - 循环深度
  - 潜在推理
  - 测试时计算
  - 语言模型架构
  - Huginn
status: processed
source_version: v2
version_updated_at: 2025-02-17
capture: full_text_read_and_summary
---

# Scaling up Test-Time Compute with Latent Reasoning: A Recurrent Depth Approach

## 保存说明

本文件根据 arXiv v2 摘要、架构、训练、评测、推理效率和结论章节整理。论文把模型称为 proof-of-concept，并不声称复现任何 OpenAI 产品。

## 方法

论文训练一个带 recurrent depth 的 decoder-only 语言模型，把网络分成三段：

1. `prelude` 将输入 token 编码到潜在状态。
2. `core recurrent block` 接收输入表示和上一轮隐藏状态，重复运行 r 次。
3. `coda` 将最终潜在状态解码成下一个 token 的概率。

训练时为每个序列随机采样循环次数，并用截断反向传播控制显存。这样模型在训练时见过不同深度，推理时可以通过增加循环次数使用更多计算，而不必生成更长的语言 CoT。

## 规模与实验

- 主模型约 3.5B 参数，使用约 800B token 训练；模型和代码/数据配方通过论文页面提供。
- 模型在标准、数学和代码基准上评测。循环次数增加时，多个推理任务持续改善，较容易的任务较早饱和，较难的任务能利用更多循环。
- 在相同训练设置下与非循环 twin 比较时，循环模型在 ARC Challenge、GSM8K 等需要推理的任务上优势明显；在 SciQ 等偏事实记忆的任务上差距较小。
- 论文的准确表述是：测试时可以扩展到接近 50B 固定深度 Transformer 的计算负载，性能有时显著改善。它不等于证明 3.5B 模型在所有指标上达到 50B 模型水平。

## 推理时能力

论文报告了一些不需要额外专门训练的原型能力：

- **自适应计算**：根据相邻循环步骤输出分布的 KL 散度，在每个 token 上提前退出；示例阈值为 `5 x 10^-4`。
- **KV cache 共享**：让不同循环步骤复用有限的 KV cache，降低缓存占用。
- **连续 CoT**：生成下一个 token 时用前一个 token 的最终潜在状态热启动，而不是每次从随机状态开始。
- **自投机解码**：用少量循环快速草拟 token，再用更多循环验证，不需要单独 draft model。

这些结果说明循环深度可以同时影响表达能力、测试时扩展和推理效率，但它们是该原型上的实验，不是通用保证。

## 潜空间中的轨迹

研究者通过 PCA 等方法观察循环状态，看到不同 token 可能表现为收敛到固定点、在潜空间中形成 orbit，或沿某个方向漂移的 slider。更难的问题和关键 token 往往使用更多循环。论文把这些几何轨迹视为模型组织计算的线索，而不是已经完成的可解释性证明。

## 论文结论与限制

论文认为 latent recurrent depth 是一种有潜力的测试时扩展轴，可以与参数规模扩展、语言 CoT 扩展互补。它的优势是可以使用标准语言建模数据、小上下文和连续潜变量；代价是计算变重、训练稳定性要求高，且相比可读 CoT 更难直接监督和审计。

作者明确把模型定位为 proof-of-concept：主训练运行只有一个大规模模型，数据混合和学习率方案未充分优化，结果不能直接代表成熟生产系统。

## 来源

- arXiv 摘要页：`https://arxiv.org/abs/2502.05171`
- arXiv HTML 全文：`https://arxiv.org/html/2502.05171`
- DOI：`https://doi.org/10.48550/arXiv.2502.05171`
- 首次提交：2025-02-07；v2：2025-02-17
- 模型：`https://huggingface.co/tomg-group-umd/huginn-0125`
- 代码与数据：`https://github.com/seal-rg/recurrent-pretraining`
- 关联文章：`raw/articles/2026-09-03-OpenAI-Astra与循环Transformer.md`

## 待核实

- 50B 是论文使用的计算负载对照，不应直接当成参数等价或通用能力等价。
- 自适应退出、KV cache 共享和自投机解码的收益需要在更多模型、硬件和服务负载上复现。
- 潜空间轨迹与真正因果推理步骤之间的对应关系仍未完全确定。
