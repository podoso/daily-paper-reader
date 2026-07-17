---
title: Structured Semantic Information Helps Retrieve Better Examples for In-Context Learning Applied to Few-Shot Relation Extraction
title_zh: 结构化语义信息帮助在少样本关系抽取的上下文学习中检索更好的示例
authors: "Aunabil Chakma, Mihai Surdeanu, Eduardo Blanco"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1664.pdf"
tags: ["query:ie"]
score: 7.0
evidence: 利用结构化语义信息改进关系抽取的上下文示例选择
tldr: 针对少样本关系抽取，该论文提出自动获取额外示例的策略，通过基于句法-语义结构的示例选择方法，结合LLM生成示例，构建混合系统，实现对关系更全面的理解。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1664/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1378, \"height\": 737, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1634, \"height\": 943, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1306, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1632, \"height\": 1088, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1644, \"height\": 2150, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1632, \"height\": 681, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1439, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1631, \"height\": 621, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1633, \"height\": 943, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1651, \"height\": 2321, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1650, \"height\": 2316, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1650, \"height\": 2322, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1663, \"height\": 2328, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1522, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1186, \"height\": 741, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1346, \"height\": 401, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1664/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1445, \"height\": 324, \"label\": \"Table\"}]"
motivation: 少样本关系抽取中上下文学习的示例质量和多样性不足。
method: 提出基于句法-语义结构相似性的示例选择策略，并与LLM生成示例结合。
result: 混合方法在关系抽取上取得更全面的关系理解，且跨领域迁移性好。
conclusion: 结构化语义信息能有效提升上下文学习在关系抽取中的表现。
---

## Abstract
This paper presents several strategies to automatically obtain additional examples for in-context learning, effectively transforming relation extraction from a 1-shot to a few-shot setting. Specifically, we introduce a novel strategy for example selection, in which new examples are selected based on the similarity of their underlying syntactic-semantic structure to the provided 1-shot example. We show that our strategy results in complementary word choices and sentence structures compared to LLM-generated examples. When both strategies are combined, the resulting hybrid system achieves a more holistic picture of the relations of interest than either method alone. Our framework transfers well across datasets (FS-TACRED and FS-FewRel) and LLM families(Qwen and Gemma). Overall, our hybrid system consistently outperforms alternative strategies achieving state-of-the-art performance on FS-TACRED and strong gains on a customized FewRel subset.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **任务**：少样本关系抽取（Few-Shot Relation Extraction, FSRE），即只有1个标注示例（1-shot）时，判断句子中两个实体间是否存在给定关系。
- **挑战**：传统方法依赖大量标注或微调，而大语言模型（LLM）虽可通过上下文学习（In-Context Learning, ICL）处理，但如何自动获取并选择有效的附加示例仍待探索。
- **核心问题**：如何自动补充示例，将1-shot转换为5-shot或10-shot，并提升ICL的性能？关键是示例的相似性与多样性之间的平衡。
- **论文贡献**：提出基于**句法-语义结构表示**的示例检索方法，并与LLM生成示例混合，构建首个在该设定下达到新SOTA的混合系统。

## 2. 方法论：核心思想与技术细节
- **整体框架**：将5-way 1-shot任务分解为5个独立的二分类问题（每个关系是否成立）。先通过NER类型过滤去除不兼容的关系，再对每个关系进行ICL判断。
- **示例获取策略**：
  - **LLM生成式**：
    - **改写（Paraphrase）**：用LLM改写原始支持句，保持实体和关系不变。
    - **全新生成（Generate）**：根据关系名称和定义，用LLM生成多样化新示例。
  - **检索式（Retrieval）**：
    - **SBERT表示**：基于句子级语义嵌入检索最相似句子。
    - **句法-语义规则表示（核心创新）**：
      - 提取句中主语-宾语之间的最短句法依赖路径，形成“词汇-句法规则”（如 `[NATIONALITY] <amod group >acl:relcl lead >nmod_by [PERSON]`）。
      - 使用自监督训练得到的语义匹配器（SoftMatcher）将规则映射为语义向量，然后通过FAISS索引检索余弦相似度最高的候选。
      - **多样性增强**：对检索结果进行k-means聚类，从每个簇中选一个代表例（采用随机、最远/最近簇等多种策略）。
  - **混合策略（Hybrid）**：将LLM生成例与语义规则检索例混合，并用LLM按多样性排序选择最终示例集。
  - **示例摘要（Summarization）**：用LLM压缩示例，保留关系核心信息。
- **关键技术细节**：
  - 检索语料：UMBC WebBase子集（2.3M句子，含两个实体且类型兼容）。
  - 相似度阈值τ调至0.6（在开发集上优化）。
  - 整体流程：一个LLM统一用于NER过滤、生成、混合选择、推理，保证一致性。

## 3. 实验设计
- **数据集**：
  - FS-TACRED（主基准）：5-way 1-shot，每个episode 10k，3个查询，97%为no_relation。
  - FS-FewRel（自建子集）：从FewRel筛选与TACRED类型兼容的6个关系，同样构造5-way 1-shot。
  - 排除FS-NYT（LLM参数知识已足够，无需上下文）。
- **对比方法**：
  - 先前专用FSRE方法：MNAV（Sabo等）、OdinSynth、CKPT、Anchor+gen. rules、SoftRules（均为微调小模型）。
  - 基线：1-shot ICL（仅1个金标示例）。
  - 多个变体：LLM改写、LLM生成、SBERT检索、语义规则检索+聚类（多种簇选择）、混合、摘要等。
- **评估指标**：精确率、召回率、F1（排除no_relation），报告均值±标准差，使用bootstrap显著性检验。
- **LLM**：Qwen3-4B、Qwen3-14B、Gemma3-4B、Gemma3-12B（均使用HuggingFace）。

## 4. 资源与算力
- **未明确说明**：论文未提及使用的GPU型号、数量、训练时长等具体硬件信息（因为本文基于ICL，无需模型训练，仅需推理和检索）。检索通过FAISS离线计算，LLM推理在单卡上即可完成。未给出总计算消耗。

## 5. 实验数量与充分性
- **数量充足**：涉及2个数据集、4个LLM、多种策略（生成/检索/混合/聚类变体/摘要），每个设置重复5次（5个episode文件），主表（Table 1 / 5）和附录表格（Table 6-13）合计超过60组实验。
- **客观公平**：
  - 所有ICL使用相同prompt模板，仅示例集不同。
  - 超参数（阈值τ）在开发集上调优，且固定用于两个数据集以避免过调。
  - 统计显著性检验（bootstrap）标注了p<0.05和p<0.01。
- **消融实验**：包括NER过滤（Table 13）、多类vs二类（Table 12）、多样性分析（Table 11）、混合选择比例（Table 10）等，较为全面。

## 6. 主要结论与发现
- **结构化语义信息优势**：基于语义规则检索的示例（尤其与LLM生成混合）在多数设置下优于SBERT、改写、纯生成等方法。
- **混合系统最佳**：在Qwen3-4B上，混合策略在FS-TACRED达F1=27.6（超越先前SOTA 24.8），在FS-FewRel上也有提升（+1.6）。Qwen3-14B在FS-TACRED达37.8。
- **多样性平衡关键**：过度相似（改写）或过度多样（纯聚类）均不佳，混合恰好平衡。
- **小模型受益更大**：4B模型提升显著，12B/14B模型有时无提升甚至下降（Gemma3-12B全策略均不如1-shot基线）。
- **额外示例并非总是有益**：大模型已有足够理解时，额外示例可能有害。

## 7. 优点
- **方法创新**：首次将句法-语义规则表示用于ICL示例选择，捕捉关系核心结构而非表面相似。
- **实用性**：无需微调、无需额外标注，仅利用无标注语料和LLM，可直接应用到新关系或新领域。
- **稳健性**：在两个数据集、两个LLM家族上一致有效，且混合策略鲁棒。
- **分析深入**：提供了多样性、NER过滤、多类vs二类、混合选择比例等多角度分析，结论可靠。

## 8. 不足与局限
- **跨关系对齐限制**：仅测试了TACRED与FewRel中类型兼容的关系，非所有关系的通用性未验证。
- **LLM敏感性**：不同LLM对同一示例集反应差异大，示例选择未针对模型个性化。
- **检索噪声**：语义规则偶尔不准确，可能引入无关示例。
- **大模型失效**：Gemma3-12B上所有策略均不提升，说明大模型对不同策略的适应性需进一步研究。
- **计算隐含成本**：虽未训练，但LLM推理和检索（尤其是聚类）仍可能耗时，且未报告具体GPU时长。
- **实验数据集局限**：仅两个公开基准，且no_relation占比极高（>95%），结果是否能推广到更均衡场景存疑。

（完）
