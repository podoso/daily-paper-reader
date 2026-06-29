---
title: "ProactiveBench: Benchmarking Proactiveness in Multimodal Large Language Models"
title_zh: ProactiveBench：多模态大语言模型主动性的基准测试
authors: "Thomas De Min, Subhankar Roy, Stéphane Lathuilière, Elisa Ricci, Massimiliano Mancini"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=e5a1ZlVcjN"
tags: ["query:multimodal"]
score: 4.0
evidence: 评估多模态大语言模型主动性的基准
tldr: 当前缺少评估多模态大语言模型主动性的基准。本文提出ProactiveBench，利用七个数据集评估MLLM在遮挡物体识别等任务中主动询问用户的能力。实验发现多数MLLM缺乏主动性。
source: ICLR-2026-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1288, \"height\": 989, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1437, \"height\": 382, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 487, \"height\": 300, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 456, \"height\": 330, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 489, \"height\": 308, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 487, \"height\": 316, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 480, \"height\": 308, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 490, \"height\": 302, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 491, \"height\": 307, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1452, \"height\": 256, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1451, \"height\": 286, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 573, \"height\": 315, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 708, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1452, \"height\": 287, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 692, \"height\": 351, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1444, \"height\": 425, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 719, \"height\": 327, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1457, \"height\": 206, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1449, \"height\": 206, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1448, \"height\": 574, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1444, \"height\": 400, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1486, \"height\": 673, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 415, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 557, \"height\": 320, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 413, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 394, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 561, \"height\": 321, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-e5a1zlvcjn/fig-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 226, \"height\": 462, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-e5a1zlvcjn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1452, \"height\": 704, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-e5a1zlvcjn/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1459, \"height\": 523, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-e5a1zlvcjn/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1461, \"height\": 523, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-e5a1zlvcjn/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1454, \"height\": 700, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-e5a1zlvcjn/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1455, \"height\": 674, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-e5a1zlvcjn/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1453, \"height\": 502, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-e5a1zlvcjn/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1455, \"height\": 700, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-e5a1zlvcjn/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1454, \"height\": 390, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-e5a1zlvcjn/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1457, \"height\": 414, \"label\": \"Table\"}]"
motivation: 现有基准未关注多模态大语言模型的主动提问能力。
method: 构建高质量基准ProactiveBench，包含7个数据集和多种主动任务。
result: 评估21个MLLM，发现它们普遍缺乏主动性。
conclusion: ProactiveBench填补了主动性评估空白，揭示了MLLM的重要缺陷。
---

## Abstract
How do multimodal large language models (MLLMs) handle images where the object of interest is partially or fully occluded? While a human would naturally ask follow-up questions or seek additional visual cues before answering, do MLLMs exhibit similar “proactive” behavior by prompting the user for more information? Despite their growing use in collaborative settings, no benchmark currently evaluates the proactiveness of MLLMs. To fill this gap, we introduce ProactiveBench, a benchmark built from seven repurposed datasets to evaluate proactiveness across tasks such as recognizing occluded objects, enhancing image quality, and interpreting coarse sketches, to name a few. We evaluated 21 MLLMs on ProactiveBench and found that they generally lack proactiveness. Model capacity shows no clear correlation with proactiveness, and adding “hints” in the query to elicit proactive suggestions yields only marginal gains. Surprisingly, conversation histories and in-context learning introduce negative biases, hindering performance. Overall, our results highlight the challenge of instilling proactiveness in MLLMs, with ProactiveBench being a first step toward building more proactive models.

---

## 论文详细总结（自动生成）

# ProactiveBench：多模态大语言模型主动性基准测试——详细中文总结

## 1. 论文的核心问题与整体含义

当前多模态大语言模型（MLLMs）在用户查询中遇到部分或完全遮挡、模糊、草图等不完整视觉信息时，通常直接作答（可能错误或拒绝回答），而缺乏人类那种主动向用户询问额外视觉线索（如“请移开遮挡物”、“请旋转物体”、“请提高图像质量”）的能力。这种“主动性”（proactiveness）在协作场景中至关重要，然而现有基准完全忽略了这一维度。论文提出了**ProactiveBench**，这是首个系统性评估MLLMs主动性的基准，旨在推动模型从“被动反应”（reactive）向“主动寻求信息”（proactive）转变。

## 2. 方法论

- **核心思想**：将评估建模为**马尔可夫决策过程（MDP）**：
  - **状态** \(s_t\)：当前图像帧 \(I_t\) 和当前可行动作集合 \(A_t\)。
  - **动作** \(a_t\)：模型从选项中选择一项，选项包括：
    - 若干“主动性建议”（例如“移动左边的积木”、“等待遮挡消失”、“去模糊图像”等）。
    - 一个“拒绝回答”选项。
    - 四个候选类别（仅一个正确）。
  - **策略** \(\pi_\theta(a_t \mid q, s_t)\)：MLLM根据问题 \(q\) 和当前状态选择动作。
  - **转移函数** \(T\)：如果选择主动性建议，环境返回下一帧（如遮挡物移动后的图像）；否则终止。
  - **奖励** \(R\)：最终正确预测类别得1分，否则0分。
- **关键技术细节**：
  - 基于**选择题（multiple-choice）** 评估，避免自由生成带来的解析困难。
  - 多轮互动：模型可以多次建议，直到获得足够信息或达到最大步数。
  - 每个样本包含：开始的模糊帧、中间帧、参考帧（完整信息）。
  - 数据集经过**过滤**：去掉那些在首轮就能被大多数模型正确回答的样本（首轮正确率≥25%的样本被移除），确保真正需要主动性才能答对。
- **数据集来源**：复用七个现有数据集，构造不同主动性场景（详见实验设计部分）。

## 3. 实验设计

- **数据集/场景（共7个）**：
  1. **ROD**：移动遮挡物以识别被遮物体（88个样本，14帧/样本，2个主动动作）。
  2. **VSOD**：等待或回放视频以处理时间性遮挡（63个样本，~230帧/样本，2个主动动作）。
  3. **MVP-N**：旋转物体以获取信息视角（4.2k样本，~4帧/样本，1个主动动作）。
  4. **ImageNet-C (IN-C)**：改善图像质量（去模糊、降噪等）以分类（5k样本，5帧/样本，8个主动动作）。
  5. **QuickDraw (QD)**：要求添加细节以识别潦草画（3.4k样本，~5帧/样本，1个主动动作）。
  6. **ChangeIt (CIT)**：在长视频中等待或回放以捕捉目标对象/动作（1.1k样本，~20帧/样本，2个主动动作）。
  7. **MS-COCO**：移动摄像机以获取更完整视图（4.8k样本，~3帧/样本，5个主动动作）。
- **Benchmark**：ProactiveBench，过滤后共7,557个样本。
- **对比方法（共21个MLLMs）**：包括开源模型（LLaVA-1.5/NeXT/OV系列、SmolVLM2、Idefics3、InstructBLIP、Qwen2.5-VL系列、InternVL3系列、Phi-4-Multimodal）和闭源模型（GPT-4.1、o4-mini）。
- **指标**：准确率（acc）和平均主动性建议次数（ps）。

## 4. 资源与算力

论文未明确说明训练阶段（因为ProactiveBench是评估基准，不需要训练模型）。实验阶段：
- 大部分实验使用**单个NVIDIA A100 GPU + 32GB RAM + 8 CPU核**，每个数据集大约1小时。
- 会话历史条件和少样本实验使用**两块A100 GPU**，约2小时，最长8小时。
- 对于Phi-4-Multimodal的少样本实验，为防显存溢出，对ROD图像缩放到512×512，MVP-N序列长度减为2。
- 会话历史条件实验中，将所有图像短边缩放到224px。

## 5. 实验数量与充分性

- **主要实验**：在7个数据集上评估21个模型，获得准确率和主动性建议次数（表1）。
- **消融与拓展实验**：
  - 3组关键分析实验：
    1. 用无效主动性选项替换有效选项（检测真正的主动性 vs. 单纯避免拒绝回答）。
    2. 在提示中加入主动性提示（hint）。
    3. 保持对话历史（multi-turn 上下文）。
    4. 提供1-shot和3-shot示例（ICL）。
  - **自由生成实验（附录A）**：在6个模型上进行开放生成评估，使用LLM-as-a-judge（o4-mini）。
  - **未过滤数据实验（附录B.8）**：展示过滤效果。
- **充分性评价**：实验覆盖面广，涵盖了多个场景、多种模型规模、多个控制变量（hint、历史、少样本、随机建议）。所有实验都公平对比了零样本基线。实验设计客观、控制得当，结论有强支撑。

## 6. 主要结论与发现

1. **普遍缺乏主动性**：在ProactiveBench上，MLLMs平均准确率仅17.5%，远低于oracle（无模糊时）的79.8%，差距超60%。
2. **模型大小与主动性不相关**：例如InternVL3 1B（27.1% acc）优于InternVL3 8B（12.7%），LLaVA-1.5 7B（24.8%）优于LLaVA-OV 72B（13.0%）。
3. **有些模型“看似主动”实则只是不拒绝回答**：将有效性建议替换为随机建议后，某些模型仍高概率选择建议，说明它们并非真正理解问题，只是倾向于不拒绝。
4. **提示（hint）能增加主动性建议次数，但准确率提升有限**：平均acc从17.5%升至25.8%，仍远低于随机基线，且部分模型会“过度探索”忽略最终分类。
5. **对话历史与少样本示例会引入负面偏差**：历史条件下，平均acc下降至10.2%（ vs 17.2%），建议次数增多但正确率降低；少样本条件下类似，ROD准确率甚至下降。
6. **闭源模型（GPT-4.1、o4-mini）在MS-COCO上异常高分（~94%），可能源于训练数据污染**。

## 7. 优点

- **首创性**：首次定义并提出MLLM主动性评估基准，填补空白。
- **场景丰富**：覆盖7个不同视觉场景（遮挡、模糊、草图、时间模糊等），具有良好泛化性。
- **评估框架严谨**：采用MDP形式化多轮互动，支持结构化的选择题评估，避免开放生成歧义。
- **实验设计全面**：包含多种控制实验（hint、历史、ICL、随机建议），深入分析主动性来源，区分“真主动”与“假主动”。
- **开源性**：代码和基准公开，利于后续研究。

## 8. 不足与局限

- **评估限于选择题**：虽然结构化，但可能限制模型自然表达（自由生成附属实验支持主要结论，但未完全覆盖所有模型）。
- **数据集构建人工性强**：主动建议集合预定义，可能无法涵盖所有现实主动行为。
- **闭源模型结果可能受数据污染**：MS-COCO上的异常高分无法解释，影响可比性。
- **过滤标准（25%首轮正确率）** 可能删除部分有意义的样本，且依赖多个模型聚合，过滤公平性需进一步验证。
- **实际应用场景差异**：基准中用户干预（如移物、旋转）被预先定义且可执行；真实场景中模型可能提出不可操作的请求，该情况未考虑。
- **计算资源消耗大**：虽然论文注明算力，但对普通研究者复现全部实验有门槛。

（完）
