---
title: "SampurNER: Fine-Grained Named Entity Recognition Dataset for 22 Indian Languages"
title_zh: SampurNER：22种印度语言的细粒度命名实体识别数据集
authors: "Prachuryya Kaushik, Ashish Anand"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40405/44366"
tags: ["query:ie"]
score: 8.0
evidence: 22种印度语言的细粒度命名实体识别数据集
tldr: 针对印地语等22种语言细粒度命名实体资源稀缺且远程监督噪声大的问题，构建SampurNER数据集并提出实体锚定机器翻译框架（EaMaTa），通过锚定实体进行翻译对齐，有效降低了标注噪声，为多语言NER研究提供了高质量资源。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40405/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1819, \"height\": 390, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40405/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1844, \"height\": 2160, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40405/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1838, \"height\": 375, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40405/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1671, \"height\": 228, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40405/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1835, \"height\": 430, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40405/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1808, \"height\": 1022, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40405/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1832, \"height\": 1059, \"label\": \"Table\"}]"
motivation: 印度语言细粒度NER资源稀缺且远程监督数据噪声大。
method: 提出实体锚定机器翻译框架（EaMaTa），利用锚定实体进行翻译对齐，降低噪声。
result: 构建了覆盖22种语言的高质量细粒度NER数据集。
conclusion: 该数据集将促进多语言NER研究。
---

## Abstract
We introduce SampurNER, a fine-grained named entity recognition (FgNER) dataset encompassing all 22 scheduled Indian languages spoken by more than two billion people across various countries. While manual annotation for FgNER resources is often labor-intensive and expensive, distant supervision methods have been employed as a viable solution. However, such datasets are often noisy, with entity mentions tagged with multiple types, requiring computationally intensive noise-aware models for effective FgNER. Moreover, resources for both coarse-grained and fine-grained named entity recognition tasks in Indian languages remain scarce. To address this, we propose an entity-anchored machine translation (EaMaTa) framework that leverages the largest manually annotated English FgNER dataset, FewNERD, to create a large-scale FgNER dataset in 22 languages. On average, the dataset comprises over 153k sentences, 354k entities, and 3.3M tokens in each language. The languages covered are: Assamese (as), Bengali (bn), Bodo (brx), Dogri (doi), Gujarati (gu), Hindi (hi), Kannada (kn), Kashmiri (ks), Konkani (gom), Maithili (mai), Malayalam (ml), Manipuri (mni), Marathi (mr), Nepali (ne), Odia (or), Punjabi (pa), Sanskrit (sa), Santali (sat),  Sindhi (sd), Tamil (ta), Telugu (te), and Urdu (ur). Various rigorous analyses and human evaluations confirm the high quality of the dataset and demonstrate the effectiveness of the entity-anchored machine translation framework with up to 9% increase in F1-score against the current state-of-the-art. Additionally, we extend our analysis to zero-shot, multilingual, and cross-lingual settings, investigating the influence of language family and script similarity on cross-lingual FgNER performance.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：印度有22种官方语言，使用者超过20亿，但现有细粒度命名实体识别（FgNER）资源极其匮乏。手动标注FgNER数据集成本高、劳动密集；而远程监督方法生成的噪声数据集（如TAFSIL）需要复杂的噪声感知模型，且质量有限。粗粒度NER在印度语言中已有一定进展（如Naamapadam等），但FgNER资源几乎空白。
- **核心问题**：如何高效、高质量地为22种印度语言构建大规模细粒度命名实体识别数据集。
- **整体意义**：填补印度语言FgNER资源空白，为多语言NER研究、零样本跨语言迁移等提供基础数据支撑，推动低资源语言NLP发展。

## 2. 方法论：核心思想、关键技术细节、算法流程

- **核心思想**：提出**实体锚定的机器翻译（Entity-Anchored Machine Translation, EaMaTa）** 框架，利用现有大规模人工标注英文FgNER数据集FewNERD，通过翻译和清洗，将标注信息无损失地迁移到目标语言，生成高质量的多语言FgNER数据集。
- **关键技术细节**：
  - **预处理**：将源语言（英语）的BIO格式NER数据集转换为两种格式：纯文本句子（plain sentence）和实体锚定句子（entity-anchored sentence）。在实体锚定句子中，每个实体mention用一对特殊的锚点符号（开始锚点αⱼ和结束锚点βⱼⁱ，其中i表示实体类型）包裹。
  - **翻译**：分别将纯文本句子和实体锚定句子通过机器翻译服务翻译成目标语言。
  - **清洗（三个阶段的过滤）**：
    - **阶段1（句子不匹配检测）**：移除实体锚定翻译句（去除锚点符号后）与纯文本翻译句不一致的句子。
    - **阶段2（实体锚点不匹配检测）**：移除翻译后的实体锚定句子中起始锚点与结束锚点不配对（缺少任一端）的句子。
    - **阶段3（实体总数不匹配检测）**：移除翻译后实体mention总数与源句子不一致的句子。
  - **锚点设计**：通过评估不同翻译系统（Google Translate、Bing Translator、IndicTrans2）对锚点符号的保留能力，为每种语言选择最优翻译服务，确保锚点不被破坏。
- **算法流程**（Algorithm 1用文字描述）：
  1. 输入：源FgNER数据集Ssrc（BIO格式）；机器翻译服务M。
  2. **预处理**：对每个句子s，生成纯文本版本s_plain和实体锚定版本s_anchor（将实体mention替换为αⱼ mention βⱼⁱ）。
  3. **翻译**：分别用M翻译s_plain和s_anchor，得到目标语言版本的sT_plain和sT_anchor。
  4. **清洗**：对每个sT_anchor：
     - 去除锚点后与sT_plain比较，不一致则丢弃。
     - 检查锚点对是否完整，不完整则丢弃。
     - 比较源句与目标句的实体总数（表示为∑(e∈s_anchor)与∑(e∈sT_anchor)），不一致则丢弃。
  5. 输出：清洗后的目标语言FgNER数据集ST_clean。

## 3. 实验设计：数据集、Benchmark、对比方法

- **使用的数据集**：
  - **源数据集**：FewNERD（最大规模人工标注英文FgNER数据集，18.8万句子，8个粗粒度、66个细粒度实体类型）。
  - **目标数据集**：SampurNER（使用EaMaTa将FewNERD翻译成22种印度语言）。平均每种语言超过15.3万句子、35.4万实体、330万token。
  - **对比数据集**：
    - MultiCoNER2（针对印地语和孟加拉语的FgNER远程监督数据集）。
    - TAFSIL（针对印地语、马拉地语、梵语、泰米尔语、泰卢固语、乌尔都语的噪声FgNER数据集）。
  - **人工标注黄金测试集**：从SampurNER的银测试集中随机选取10种语言各1000句，由至少两名母语标注者进行人工标注，IAA大于0.8。
- **Benchmark与对比方法**：
  - **模型**：mBERT（bert-base-multilingual-cased）和IndicBERTv2。
  - **对比基线**：state-of-the-art噪声感知模型DECENT（RoBERTa-large → XLM-RoBERTa-large + IndicBERTv2），对比MultiCoNER2和TAFSIL数据集性能。
  - **评估指标**：Macro F1、Micro F1（SeqEval工具）。
- **实验场景**：
  - **单语FgNER**：在22种语言上分别微调mBERT和IndicBERTv2，评估银测试集和黄金测试集。
  - **与SOTA对比**：将EaMaTa生成的印地语、孟加拉语等7种语言数据集与MultiCoNER2和TAFSIL在同一种模型（DECENT）下对比F1。
  - **交叉语言零样本分析**：对每种语言（包括英语）微调mBERT/IndicBERTv2，然后测试所有其他语言的测试集，生成零样本性能矩阵（图2）。
  - **多语言与脚本相似性分析**：构建不同语言组合的训练集（全部22种、印欧语系、达罗毗荼语系、同种脚本等），评估零样本性能。
  - **错误分析**：计算边界错误、实体类型错误、虚假实体错误百分比；对Santali语言进行共现混淆分析。
  - **消融实验**：评估Stage 2和Stage 3过滤对F1的提升效果。

## 4. 资源与算力

- 论文明确提到：使用**NVIDIA A100 GPU**进行模型微调。
- **具体数量与时长**：未明确说明使用了多少张A100 GPU以及训练时长。仅提及batch size、epoch等超参数（mBERT/IndicBERTv2：batch size=64, epochs=6；DECENT：batch size=16, epochs=2）。因此无法知道总计算成本。
- 翻译服务使用了Google Translate（19种语言）、Bing Translator（Bodo和Kashmiri）、IndicTrans2（Santali），但未提及翻译阶段的计算资源。

## 5. 实验数量与充分性

- **实验数量丰富**：
  - 单语微调实验：22种语言 × 2种PLM = 44组主要结果（表4）。
  - SOTA对比：7种语言 × DECENT模型 × 3种训练集（MultiCoNER2/TAFSIL/EaMaTa），共约14组对比（表2）。
  - 零样本分析：22×22种语言对（图2），包含mBERT和IndicBERTv2两种模型，共968个零样本性能点。
  - 多语言/脚本分析：多个组合（All22、Indo-European、Dravidian等）。
  - 消融实验：21种语言验证了Stage2+Stage3的F1提升（图3）。
  - 人工评估：XSTS评分（每语言100句×2标注者）。
- **充分性评估**：实验设计全面，覆盖了单语、跨语言、零样本、消融、错误分析等多种角度，对比了现有SOTA数据集和模型，结论具有说服力。但黄金测试集仅覆盖10种语言，银测试集用于主要分析，可能引入微小偏差（作者指出±5%差异）。

## 6. 主要结论与发现

1. **数据集质量高**：EaMaTa框架生成的数据集在SOTA对比中，F1分数提升最高达9%（梵语4.2→44.2，提升9%）；人工XSTS评分均在3.5-4.2之间，表明语义保留良好。
2. **模型性能**：IndicBERTv2在22种语言上均优于mBERT，尤其是对mBERT未预训练的语言（如曼尼普尔语、桑塔利语）提升显著。
3. **零样本迁移的关键因素**：脚本相似性比语言家族更重要；包含目标语言的预训练（如IndicBERTv2预训练了所有22种语言）显著提升零样本性能。
4. **异常发现**：
   - 只使用波斯-阿拉伯语系语言微调IndicBERTv2，对桑塔利语的零样本性能优于All22模型（尽管All22包含桑塔利样本）。
   - 曼尼普尔语（汉藏语系）在达罗毗荼语系微调下零样本性能优于All22。
5. **消融有效性**：阶段2（锚点不匹配过滤）平均提升F1 2.8%，阶段3（实体总数过滤）平均提升2.4%。
6. **错误类型**：最常混淆的细粒度类型为`actor/artist/author/politician`与`person-other`，以及`location-GPE`与`location-other`，其他类型学习较好。

## 7. 优点（方法或实验设计的亮点）

- **方法创新**：EaMaTa框架通过锚点符号保护实体边界，结合三阶段清洗策略，有效减少机器翻译引入的噪声，无需额外人工标注即可生成高质量FgNER数据集。
- **规模宏大**：一次性覆盖22种印度语言（包括两种濒危语言：Bodo和Manipuri），平均数据量超过15万句子，远超现有资源。
- **实验设计严谨**：包含人工黄金测试集（IAA>0.8）、多种对比基线、全面的零样本/跨语言/多语言分析，以及消融实验和错误分析，证明数据集的有效性和方法的通用性。
- **开源贡献**：数据集和扩展版本公开提供（huggingface和tinyurl），促进后续研究。
- **翻译服务评估**：对三种翻译服务（Google、Bing、IndicTrans2）进行系统对比（BLEU/TER/chrF/COMET），为每种语言选择最佳翻译器，体现工程优化。

## 8. 不足与局限

- **翻译引入的偏差**：即使经过清洗，翻译过程仍可能丢失源语言的文化、地理和语言细微差别，造成实体类型误判或边界偏移。论文承认“缺乏印度次大陆特有语言和文化的细微差别”。
- **依赖源语言数据集**：SampurNER完全基于FewNERD，受限于FewNERD的领域覆盖（尽管多域）和实体类型定义（66种细粒度），无法覆盖所有印度语境下的实体类型。
- **黄金测试集覆盖不全**：仅10种语言有人工标注黄金测试集，其余12种语言仅依赖银测试集（自动翻译+清洗），可能高估或低估质量。
- **计算成本未报告完整**：虽然指出了A100 GPU，但未给出训练总时长、GPU数量等，不利于复现和算力估算。
- **未与人类标注基线对比**：没有提供完全人工标注的FgNER数据集作为上界，难以判断“EaMaTa vs. 纯人工”的质量差距。
- **翻译服务的选择依赖启发式**：仅基于小样本（1000句）部分语言的翻译质量指标选择翻译器，可能未覆盖所有语言的真实情况。
- **未评测大型语言模型（LLM）**：论文提到“未来计划系统评估LLM的FgNER能力”，表明当前实验未包括GPT等模型，限制了与最新范式的对比。

（完）
