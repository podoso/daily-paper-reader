---
title: "MDocAgent: A Multi-Modal Multi-Agent Framework for Document Question Answering"
title_zh: MDocAgent：面向文档问答的多模态多智能体框架
authors: "Siwei Han, Peng Xia, Ruiyi Zhang, Tong Sun, Yun Li, Hongtu Zhu, Huaxiu Yao"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=05SHW9ai9e"
tags: ["query:multimodal"]
score: 7.0
evidence: 面向文档问答的多模态多智能体框架
tldr: 本文提出MDocAgent，一种多模态多智能体框架用于文档问答。系统包含通用、关键、文本、图像和摘要五个智能体，通过RAG和多智能体协作充分融合文本和视觉信息。在复杂文档推理任务上表现优异。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-05shw9ai9e/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 489, \"height\": 718, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-05shw9ai9e/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1373, \"height\": 651, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-05shw9ai9e/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1411, \"height\": 750, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-05shw9ai9e/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1416, \"height\": 782, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-05shw9ai9e/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1432, \"height\": 779, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-05shw9ai9e/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1375, \"height\": 684, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-05shw9ai9e/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1441, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-05shw9ai9e/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1470, \"height\": 846, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-05shw9ai9e/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1084, \"height\": 142, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-05shw9ai9e/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1411, \"height\": 919, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-05shw9ai9e/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1296, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-05shw9ai9e/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1010, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-05shw9ai9e/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 898, \"height\": 262, \"label\": \"Table\"}]"
motivation: 现有DocQA方法未能有效整合文本和视觉线索，多模态推理能力不足。
method: 设计五个专门智能体，分别处理文本、图像和决策，通过多智能体交互实现多模态融合。
result: 在文档问答任务上改善了多模态推理性能。
conclusion: MDocAgent为多模态文档理解提供了有效的多智能体框架。
---

## Abstract
Document Question Answering (DocQA) is a very common task. Existing methods using Large Language Models (LLMs) or Large Vision Language Models (LVLMs) and Retrieval Augmented Generation (RAG) often prioritize information from a single modal, failing to effectively integrate textual and visual cues. These approaches struggle with complex multi-modal reasoning, limiting their performance on real-world documents. We present MDocAgent (A Multi-Modal Multi-Agent Framework for Document Question Answering), a novel RAG and multi-agent framework that leverages both text and image. Our system employs five specialized agents: a general agent, a critical agent, a text agent, an image agent and a summarizing agent. These agents engage in multi-modal context retrieval, combining their individual insights to achieve a more comprehensive understanding of the document's content. This collaborative approach enables the system to synthesize information from both textual and visual components, leading to improved accuracy in question answering. Preliminary experiments on five benchmarks like MMLongBench, LongDocURL demonstrate the effectiveness of our MDocAgent, achieve an average improvement of 12.1% compared to current state-of-the-art method. This work contributes to the development of more robust and comprehensive DocQA systems capable of handling the complexities of real-world documents containing rich textual and visual information.

---

## 论文详细总结（自动生成）

# MDocAgent 论文中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **问题**：现有文档问答（DocQA）方法（如基于 LLM/LVLM 的纯文本或纯图像 RAG）往往只优先考虑单一模态的信息，未能有效整合文本和视觉线索。面对需要跨模态推理（例如同时依赖图表及其文字说明）的复杂真实文档时，这些方法表现不佳。
- **背景**：大语言模型只能处理文本，大视觉语言模型虽能处理图像，但在关键信息主要为文本或需精细结合文本与视觉时仍受局限。此外，文档信息量大，直接全篇处理不现实，因此检索增强生成（RAG）常被用作辅助工具，但现有 RAG 多分别检索文本或图像，缺失跨模态信息合成能力。
- **整体含义**：本文旨在通过构建一个多模态多智能体协作框架，实现文本与图像信息的深度融合与协同推理，提升复杂文档问答的准确性和全面性。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：采用并行的文本 RAG 和图像 RAG 分别检索相关上下文，然后利用五个专门智能体（通用、关键、文本、图像、总结）分阶段进行信息提取、细粒度分析及最终答案合成。
- **多阶段流程**（见论文 Algorithm 1 和 Algorithm 2）：
    1. **文档预处理**：使用 OCR 和 PDF 解析提取文本段，同时保留页面原始图像。
    2. **多模态上下文检索**：
        - 文本检索：利用 ColBERT 从文本段中检索 top-k 相关片段 \(T_q\)。
        - 图像检索：利用 ColPali 从页面图像中检索 top-k 相关页面 \(I_q\)。
    3. **初步分析与关键提取**：
        - 通用智能体 \(A_G\) 接收 \(T_q\) 和 \(I_q\)，生成初步答案 \(a_G\)。
        - 关键智能体 \(A_C\) 基于 \(q, T_q, I_q, a_G\) 提取关键文本信息 \(T_c\) 和关键视觉信息 \(I_c\)（以文字描述关键图像内容）。
    4. **专门智能体处理**：
        - 文本智能体 \(A_T\) 结合 \(T_q\) 和 \(T_c\) 生成基于文本的答案 \(a_T\)。
        - 图像智能体 \(A_I\) 结合 \(I_q\) 和 \(I_c\)（关键图像描述）生成基于图像的答案 \(a_I\)。
    5. **答案合成**：总结智能体 \(A_S\) 整合 \(a_G, a_T, a_I\) 产生最终答案 \(a_S\)。
- **关键技术细节**：智能体均基于预训练 LVLM（主要使用 Qwen2-VL-7B-Instruct，文本智能体使用 Llama-3.1-8B-Instruct）；检索器为 ColBERTv2（文本）和 ColPali（图像）；关键信息以字典格式传递。

## 3. 实验设计
- **数据集与场景**：
    - MMLongBench（长文档，多模态，1091问）
    - LongDocURL（多模态长文，含理解、推理、定位，2325问）
    - PaperTab（论文表格问答，393问）
    - PaperText（论文文本问答，2804问）
    - FetaTab（维基百科表格问答，1023问）
- **Benchmark 与对比方法**：
    - 纯 LVLM 基线：Qwen2-VL-7B、Qwen2.5-VL-7B、LLaVA-v1.6、Phi-3.5、LLaVA-One-Vision、SmolVLM。
    - RAG 方法：ColBERTv2+LLaMA-3.1-8B（仅文本）、M3DocRAG（ColPali+Qwen2-VL-7B，仅图像）。
    - 对比设置：top-1 和 top-4 检索。
- **消融实验**：分别移除文本智能体（MDocAgent_i）、图像智能体（MDocAgent_t）、通用+关键智能体（MDocAgent_s）。
- **细粒度分析**：按 MMLongBench 中的证据模态（图表、表格、纯文本、图文、图形）分解性能。
- **兼容性分析**：使用 ColQwen2-v1.0 替换 ColPali 作为图像 RAG 骨干。
- **其他实验**：不同 LVLM 骨干（Qwen2.5-VL、GPT-4o）、不同文档长度、检索模块准确率。

## 4. 资源与算力
- **明确说明**：“All experiments are conducted on 4 NVIDIA H100 GPUs。”文中未提供训练时长或总 GPU 小时数，也未说明具体推理时间。实验均使用预训练模型，无从头训练，因此算力主要用于推理和评估。

## 5. 实验数量与充分性
- **实验组数**：
    - 主实验：2 种检索设置（top-1, top-4）× 5 个数据集 × 9 种方法（包括自身）→ 约 90 组结果。
    - 消融实验：4 种变体 × 5 个数据集。
    - 细粒度分析：5 种模态 × 5 种方法（含自身）在 MMLongBench 上。
    - 兼容性分析：2 种图像 RAG × 5 个数据集。
    - 其他：2 种骨干 × 2 种检索在 5 个数据集上；文档长度分类 3 类 × 3 种方法；检索准确率 2 种 Top-k × 2 个数据集。
- **充分性与公平性**：实验覆盖多类型文档、多模态场景、多种基线（包括最先进方法）；所有结果均采用 GPT-4o 自动评估二元正确性，避免人工偏倚；消融和兼容性分析系统验证了每个组件的贡献。实验设计较为充分、客观、公平。

## 6. 论文的主要结论与发现
- **性能提升**：MDocAgent 在所有五个 benchmark 上均超越所有纯 LVLM 和现有 RAG 方法。top-1 检索平均提升 12.1% 对比最强 RAG 方法（M3DocRAG），top-4 提升 10.9%（对比 M3DocRAG）和 6.9%（对比 ColBERTv2+LLaMA）。
- **消融验证**：任何智能体（文本、图像、通用+关键）的移除都会导致性能下降，证明每个智能体及跨模态协作的必要性。
- **细粒度优势**：MDocAgent 在各类证据模态（图表、表格、纯文本、图文）上均表现出色，尤其在需要跨模态或细粒度信息时优势明显。
- **兼容性**：更换图像 RAG 骨干（ColQwen2-v1.0）平均性能持平，表明框架鲁棒且不依赖特定检索器。
- **骨干增强**：使用更强 LVLM（如 GPT-4o）可进一步提升框架性能，证明框架可受益于更强的底层模型。

## 7. 优点
- **方法论亮点**：首次将多智能体协作系统性地融入多模态 RAG 流程，设计五类专门智能体实现“检索→初步理解→关键提取→专注分析→综合”的流水线，有效解决信息过载和跨模态推理难题。
- **实验设计亮点**：覆盖多个长文档、不同模态、不同领域的公开数据集；消融、细粒度、兼容性等分析全面；自动评估流程保证可重复性和客观性。
- **实用性与扩展性**：框架不依赖特定检索器或 LVLM，易于替换更强骨干；代码已随附匿名提交（声称）。

## 8. 不足与局限
- **实验覆盖局限**：
    - 主要基于 7B 参数量级 LVLM（Qwen2-VL-7B、LLaMA-3.1-8B），仅附录中测试了 GPT-4o，未系统性研究更大模型（如 70B+）下的性能与计算成本。
    - 数据集均为英文，未评估多语言或低资源场景的泛化能力。
- **评估偏差风险**：
    - 使用 GPT-4o 作为自动评判，可能对 GPT-4o 自身或其他类似模型有偏向（但所有方法统一使用同一评判器，相对公平）。
    - 未报告人类一致率，且二元正确性评估可能忽略部分匹配或语义等价答案。
- **技术局限**：
    - 框架依赖两轮检索（文本+图像）和五个智能体的顺序调用，推理延迟和计算开销较大，未与实时性要求高或资源受限场景对比。
    - 未深入讨论检索完全失败时的应对策略（如关键信息缺失）或对 OCR 错误的鲁棒性。
    - 消融实验中移除通用+关键智能体（MDocAgent_s）后性能下降明显，表明这两阶段对最终结果至关重要，但也增加了系统复杂度。
- **实际应用限制**：
    - 未在现实业务文档（如扫描件、手写体、混合排版）上验证性能。
    - 未提供开源代码或模型权重（论文声称已提交但未正式公开），可复现性待验证。

（完）
