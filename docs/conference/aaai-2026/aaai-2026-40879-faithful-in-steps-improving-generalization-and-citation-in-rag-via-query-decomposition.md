---
title: "Faithful in Steps: Improving Generalization and Citation in RAG via Query Decomposition"
title_zh: 逐步忠实：通过查询分解改进RAG的泛化与引用
authors: "Yue Liu, Zhongying Ru, Shimin Di, Jipeng Zhang, Ruiyuan Zhang, Xiaofang Zhou"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40879/44840"
tags: ["query:ie"]
score: 6.0
evidence: 通过查询分解解决RAG中的实体识别问题，与命名实体识别相关
tldr: 本文提出QDRAG框架，针对多跳和多模态问题中隐式实体识别失败的问题，将输入问题分解为原子子问题以识别隐式实体，并通过重排序优化上下文。实验证明该方法有效减少过度引用，提升答案可验证性和泛化能力，同时展示了实体识别在RAG中的关键作用。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有可归因RAG在多跳推理和多模态问题中面临隐式实体识别失败和过度引用问题。
method: 将问题分解为原子子问题以识别隐式实体，并通过重排序消除上下文干扰。
result: 在多个问答基准上，QDRAG在引用准确性和答案质量上均优于基线。
conclusion: 实体识别是增强RAG可靠性的重要组件。
---

## Abstract
Retrieval-augment generation is a prevalent strategy to mitigate hallucinations of LLMs. The attributable RAG (RAGQ) generates quotes for its answers. The quotes indicate which input contexts support the RAG to derive the answers, enhancing the answer's verifiability and trustworthiness. However, existing RAGQs exhibit significant degradation when dealing with questions that require multi-hop reasoning and multi-modal understanding, suffering from over-citation, implicit entity identification failure, and poor generalization. In this paper, we propose a novel RAGQ framework, namely QDRAG. QDRAG breaks down the input question into atomic subquestions to identify the implicit entities. Then, the reranker prunes context distractors to eliminate the downstream over-citation. To facilitate query decomposition, we propose two zero-shot approaches: QD-C and QD-R, which guide the QD MLLM to decompose the question based on context knowledge and retrieval rewards, respectively. One interesting finding is that finetuning on the QD task shows better generalizability compared to directly finetuning on the downstream RAGQ task. Experiments on four multi-modal QA benchmarks demonstrate QDRAG's efficacy in grounding answers and generating faithful citations. The framework significantly outperforms all the baselines on both in-domain and out-of-domain tests, even surpassing Gemini-Pro.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：现有可归因检索增强生成（RAG with Quotes, RAGQ）在多跳推理和多模态问答任务中面临三大挑战：
  - **过度引用错误上下文**：RAGQ引用了局部匹配但整体不相关的多模态上下文。
  - **隐式实体检索失败**：多跳问题中关键实体未显式出现在查询中，导致检索不到支持上下文。
  - **泛化能力差**：对RAGQ任务进行指令微调后，面对动态多媒体知识难以保持引用准确性。
- **背景**：RAG通过外部知识减少LLM幻觉，但多跳和多模态场景下现有方法表现严重退化。稀疏上下文有助于提升引用质量，但现有稀疏RAG（如重排序）处理多跳问题时可能丢弃关键上下文。
- **整体含义**：提出QDRAG框架，通过查询分解（将复杂问题拆解为原子子问题）识别隐式实体，结合重排序过滤干扰上下文，从而提升引用的忠实性和答案质量，并显著改善模型的跨域泛化能力。

## 2. 方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：将输入的多跳问题分解为多个单跳子问题，每个子问题对应一个可被单一上下文回答的知识点；对每个子问题进行独立重排序，保留最相关的上下文；最终由MLLM基于稀疏上下文生成答案和引用。
- **关键技术细节**：
  - **查询分解**：提出两种零样本方法：
    - **QD-C（上下文引导分解）**：定义两个操作符——实体替换（将指代表达替换为具体实体）和开放式分解（将实体分配给多个独立子问题）。单轮MLLM推理完成，即插即用。
    - **QD-R（检索引导分解）**：进行多轮检索，用特殊token `<Ans_of_Q_i>` 表示子问题依赖前序答案；提出**QDARF**（从检索反馈对齐MLLM），以黄金上下文的召回率作为奖励，使用DPO对分解计划进行偏好优化，使子问题召回率更高。
  - **上下文重排序**：对每个子问题，计算上下文的相关性分数 $S(C|Q_i) = P(\text{“Yes”} | Q_i, C, R)$，保留top-k上下文。
  - **自适应预算分配**：基于熵分配总保留上下文数量N给各子问题，熵越高的子问题保留更多上下文。
- **公式**：DPO损失函数：
  $$L = -\mathbb{E}_{(x,y_w,y_l)\sim \mathcal{D}} \left[ \log \sigma \left( \beta \log \frac{\pi_\theta(y_w|x)}{\pi_{\text{ref}}(y_w|x)} - \beta \log \frac{\pi_\theta(y_l|x)}{\pi_{\text{ref}}(y_l|x)} \right) \right]$$
- **算法流程**：输入问题 → 查询分解得到子问题集合 → 对每个子问题检索并重排序 → 分配预算 → 合并上下文 → MLLM生成带引用的答案。

## 3. 实验设计

- **数据集**：四个多模态QA基准：
  - **MMQA**（1196条测试查询）、**WebQA**（4967条测试查询）——纯文本查询，需图像或文本片段。
  - **InfoSeek**、**E-VQA**——需实体识别与文本信息检索。
  - 训练数据来自MMQA和WebQA的训练集，测试时InfoSeek和E-VQA属于**跨域**（out-of-domain）场景。
- **评估指标**：
  - 答案质量：精确匹配（EM）和LLM-judge评分（正确性和全面性）。
  - 引用忠实性：AutoAIS（用Qwen2.5VL-32B判断引用是否支持答案）。
- **基线方法**分为四类：
  - 密集RAG：Gemini-Pro、Qwen2.5VL、InternVL3（含post-hoc检索）。
  - 检索-重排序-生成：CLIP、MMEmbed、Sparse-RAG、RagVL。
  - 检索-QD-重排序-生成：LlamaIndex、QDRAG-C（单轮检索）。
  - QD-检索-重排序-生成：Self-Ask、SearChain、QDRAG-R（多轮检索）。
- **实现细节**：
  - 7B模型：Qwen2.5-VL-7B；14B模型：InternVL3-14B。
  - 重排序保留top-5上下文，使用LoRA微调，vLLM v0.9.2推理。
  - 检索器默认CLIP-ViT-L/14@336px。

## 4. 资源与算力

- **硬件**：Ubuntu服务器配备**2块A100 80GB GPU**。
- **框架**：vLLM v0.9.2，LoRA微调。
- **训练反馈成本**（表5）：
  - 传统RAGQ方法（如Front）使用LLM-judge构建训练数据耗时约**28小时**。
  - QDRAG-R使用检索反馈（召回率）构建数据仅需约**2小时**。
- **整体训练时长**：文中未明确说明完整训练耗时，但指出反馈成本大幅降低。

## 5. 实验数量与充分性

- **实验组数**：包含主实验（表1，跨四个数据集、多个基线）、消融实验（表3、6、7）、跨任务微调对比（表4）、单轮检索对比（表2）、失败案例分析（图6）、效率与成本分析（图8、表5）、注意力可视化（图9）等，共计**超过10组核心实验**。
- **充分性**：
  - 覆盖了in-domain（MMQA, WebQA）和out-of-domain（InfoSeek, E-VQA）场景，验证泛化性。
  - 消融实验细化到分解算符（D/R/S）、训练数据大小、是否使用DPO、自适应预算等。
  - 与最新方法（包括商业模型Gemini-Pro）对比，结果统计显著。
- **公平性**：所有模型使用相同检索器（CLIP），重排序/生成模型规模一致（7B/14B），对比条件控制较好。

## 6. 主要结论与发现

- **QDRAG-R显著优于所有基线**：在MMQA和WebQA上QDRAG-R-7B/14B在所有指标（EM、LLM、Cite）上均获得最佳或次佳；在out-of-domain的InfoSeek和E-VQA上同样大幅领先，甚至超越Gemini-Pro。
- **稀疏上下文提升引用质量**：重排序（稀疏RAG）比密集RAG引用更准确，但多跳下直接使用稀疏RAG会降低答案质量，而QDRAG通过子问题重排序解决了这一问题。
- **QD任务微调比直接RAGQ微调更泛化**：在QD任务上微调（QDRAG）在out-of-domain上优于在RAGQ任务上微调的模型（Front）。
- **检索反馈比LLM反馈更高效**：QD-R的反馈成本仅为2小时，而传统LLM-judge反馈需28小时。
- **查询分解优于查询重写**：QD-reranking方案全面优于重写方案（RaFe）。

## 7. 优点

- **创新性**：首次将查询分解与重排序结合用于RAGQ，提出两种零样本分解方法（QD-C/QD-R），并引入基于检索奖励的DPO对齐。
- **实用性**：QD-C即插即用、成本低（单次MLLM调用$0.019/查询）；QD-R在性能提升的同时时间增加可控。
- **泛化性**：跨域测试表现优异，证明分解逻辑的通用性，不受具体领域知识束缚。
- **消融充分**：对每个设计组件（分解算子、DPO、预算分配、训练数据量）进行了全面验证，因果明确。
- **公平对比**：与多种前沿方法（包括商业模型）在同一检索器和硬件下对比，结果可靠。

## 8. 不足与局限

- **依赖初始检索质量**：QD-C在轻量级检索器下表现一般，仅在强大检索器（如MMEmbed）下效果提升显著（表2）。
- **多轮检索增加成本**：QD-R虽然性能更好，但需要多轮检索和重排序，时间成本仍高于简单RAG（尽管优于其他分解方法）。
- **实验覆盖有限**：仅评估了多模态QA场景，未在纯文本多跳QA（如HotpotQA）或更复杂的跨模态推理任务上验证。
- **模型选择局限**：主要基于Qwen2.5VL和InternVL3系列，未测试其他主流MLLM（如LLaVA, GPT-4V）。
- **未讨论失败模式**：虽然进行了失败案例分析（图6），但未深入分析QDRAG自身的失败案例（如分解错误或重排序错误）。
- **潜在偏差**：AutoAIS评估使用Qwen2.5VL-32B作为评判，可能存在裁判模型偏好；且仅使用二值标签（True/False），粒度较粗。

（完）
