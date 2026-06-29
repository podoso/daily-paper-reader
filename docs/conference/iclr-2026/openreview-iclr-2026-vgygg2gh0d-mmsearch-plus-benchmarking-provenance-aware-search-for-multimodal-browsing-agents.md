---
title: "MMSearch-Plus: Benchmarking Provenance-Aware Search for Multimodal Browsing Agents"
title_zh: MMSearch-Plus：面向多模态浏览代理的溯源感知搜索基准
authors: "Xijia Tao, Teng Yihua, Xinxing Su, Xinyu Fu, Jihao Wu, Chaofan Tao, Ziru Liu, Haoli Bai, Rui Liu, Lingpeng Kong"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=VGYgG2GH0d"
tags: ["query:multimodal"]
score: 4.0
evidence: 多模态浏览基准，需要视觉线索提取
tldr: 现有浏览基准缺乏真正的多模态推理。MMSearch-Plus提出311个任务，强制要求从图像中提取细粒度视觉线索，并通过迭代检索和交叉验证来推理，确保视觉信息的端到端使用。该基准和代理框架有助于评估多模态理解能力。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1437, \"height\": 783, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 859, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1464, \"height\": 730, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 719, \"height\": 611, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1442, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 736, \"height\": 522, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 847, \"height\": 1209, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1433, \"height\": 804, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 367, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 665, \"height\": 398, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 666, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 663, \"height\": 400, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1441, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1441, \"height\": 765, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1442, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1445, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1441, \"height\": 426, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1375, \"height\": 1293, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 683, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 283, \"height\": 748, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 812, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 810, \"height\": 488, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 283, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 283, \"height\": 267, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-iclr-2026-vgygg2gh0d/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 286, \"height\": 735, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-iclr-2026-vgygg2gh0d/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 674, \"height\": 718, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vgygg2gh0d/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1479, \"height\": 1088, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vgygg2gh0d/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1301, \"height\": 588, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vgygg2gh0d/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 637, \"height\": 416, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vgygg2gh0d/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1297, \"height\": 1086, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vgygg2gh0d/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1344, \"height\": 2030, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-iclr-2026-vgygg2gh0d/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1342, \"height\": 2264, \"label\": \"Table\"}]"
motivation: 现有多模态基准任务可被文本启发式解决，缺乏真正的视觉推理。
method: 构建311个需要视觉线索提取和传播的任务，并提供模型无关的代理框架和Set-of-Mark模块。
result: 提出的基准强制要求多模态理解，并通过迭代图像-文本检索和交叉验证实现。
conclusion: 该工作为多模态浏览代理提供了更严格的评估标准。
---

## Abstract
Existing multimodal browsing benchmarks often fail to require genuine multimodal reasoning, as many tasks can be solved with text-only heuristics without vision-in-the-loop verification. We introduce MMSearch-Plus, a 311-task benchmark that enforces multimodal understanding by requiring extraction and propagation of fine-grained visual cues through iterative image–text retrieval and cross-validation under retrieval noise.
Our curation procedure seeds questions whose answers require extrapolating from spatial cues and temporal traces to out-of-image facts such as events, dates, and venues.
Beyond the dataset, we provide a model-agnostic agent framework with standard browsing tools and a set-of-mark (SoM) module, which lets the agent place marks, crop subregions, and launch targeted image/text searches. SoM enables provenance-aware zoom-and-retrieve and improves robustness in multi-step reasoning.
We evaluated closed- and open-source MLLMs in this framework. The strongest system achieves an end-to-end accuracy of 36.0%, and integrating SoM produces consistent gains in multiple settings, with improvements up to +3.9 points.
From failure analysis, we observe recurring errors in locating relevant webpages and distinguishing between visually similar events. These results underscore the challenges of real-world multimodal search and establish MMSearch-Plus as a rigorous benchmark for advancing agentic MLLMs.

---

## 论文详细总结（自动生成）

以下是基于论文《MMSearch-Plus: Benchmarking Provenance-Aware Search for Multimodal Browsing Agents》的中文详细总结。

---

# 论文总结：MMSearch-Plus：面向多模态浏览代理的溯源感知搜索基准

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **现有问题**：现有的大规模多模态浏览基准（如MMSearch）虽然结合了图像与网页浏览，但许多任务仅需文本启发式即可解决，无需真正的多模态推理。例如，强大的图像搜索引擎往往能直接返回包含答案的页面，使得纯语言模型也能表现良好。
- **差距**：文本浏览基准（如BrowseComp）强调长程、多步推理，但当前多模态浏览基准远不如文本浏览基准困难，反映了真实世界多模态搜索需求与现有评估之间的鸿沟。
- **目标**：设计一个需要**真正的、细粒度视觉推理**的基准，要求代理从图像中提取微弱空间/时间线索，并通过迭代搜索和溯源验证（provenance）来回答不在图或文中的事实（如事件、日期、地点）。

## 2. 论文提出的方法论：核心思想与关键技术

### 2.1 核心思想：空间-时间外推（Spatial-Temporal Extrapolation）

- 构建问题时，要求模型从图像中的**局部空间线索**（如微文字、标志、布局）和**时间线索**（如界面变化、广播叠加）推断出图像外的事实。
- 问题类型分为：
  - **空间外推**：推断画面外的未显示实体（如背对的人、遮挡的标牌）。
  - **时间外推**：推断显示瞬间之前或之后的事件（如下一场比赛、下一集内容）。
- 这迫使代理必须先定位源事件，再检索并整合外部知识。

### 2.2 数据收集与过滤

- **数据来源**：公共视频平台、arXiv 学术论文。视频由人工选取关键帧，论文提取图表截图。
- **筛选条件**：截图包含模糊/嘈杂信息，识别困难；缺乏常见实体；无法通过直接图像搜索解决。
- **对抗性过滤**：移除可被现有闭源模型（如 GPT-4o, Gemini-2.5-Pro）直接回答的问题；对关键区域进行模糊或遮挡；迭代优化。

### 2.3 基准统计

- **总任务数**：311 个（含图像），分为 8 个主类别（地理、体育、学术、影视、科技、游戏、Vlog、音乐）。
- **难度分布**：易 94(30.2%)，难 217(69.8%)。“易”定义为无搜索或仅图像搜索即可由 o3 或 Gemini-2.5-Pro 正确回答。
- **答案长度**：平均 3.7 词，短答案为主。

### 2.4 代理框架

- **模型无关**：提供标准工具（文本搜索、图像搜索、缩放裁剪）。
- **Set-of-Mark (SoM)**：提供人类标注的边界框，代理可调用 `zoom_in(index)` 返回裁剪子图，然后对该子图进行图像搜索。这实现了溯源感知的缩放检索（provenance-aware zoom-and-retrieve）。
- **状态管理**：维护多轮对话上下文（工具调用、裁剪结果、假设），支持长程推理。
- **缓存与总结**：图像搜索结果被缓存并由 MLLM 总结为 `web info` 和 `related info` 两个字段，以压缩历史。

## 3. 实验设计

### 3.1 基准与评估

- **数据集**：MMSearch-Plus（311 任务）。另有一个子集 MMSearch-Plus-lite（239 个任务，所有模型无搜索解答率为 0），用于消除内部知识影响。
- **评估指标**：准确率（accuracy），使用 LLM-as-judge（GPT-4o）与人工验证一致。

### 3.2 对比方法

- **人类基线**：专家使用 Chrome 浏览器，每任务 10–20 分钟。
- **搜索模式**：
  1. **无搜索**：仅凭图像和问题。
  2. **仅图像搜索**：使用预缓存的前 10 个图像搜索结果。
  3. **仅文本搜索**：最多 20 轮，每轮 3–5 个查询。
  4. **完整部署（Full Rollout）**：自由使用文本/图像搜索，最多 20 轮。
  5. **完整部署 + SoM**：增加缩放裁剪和子图搜索功能。
- **评估模型**：
  - 闭源：Gemini-2.5-Pro、o3、GPT-5。
  - 开源：Qwen-2.5-VL-72B-Instruct。

### 3.3 实验数量与充分性

- **主要实验**：表 1 报告了 5 种搜索模式下各模型的准确率，共约 30 组结果。
- **消融实验**：比较 Full Rollout 与 Full Rollout + SoM，分析 SoM 增益。
- **内部知识影响分析**：MMSearch-Plus-lite 上的结果（表 4）和图 4 显示趋势稳定。
- **误差分析**：图 6 分类错误类型（无相关信息、幻觉等），定性案例图 7。
- **行为分析**：工具使用分布（图 5）、过渡矩阵（图 12）、缩放行为（图 13,14）、轨迹长度统计（图 15）。
- **充分性**：实验覆盖了主要模型、搜索模式、消融、误差和工具行为，较为充分。但对比模型数量有限，且仅有一个开源模型（Qwen-72B）。

## 4. 资源与算力

论文 **未明确说明** 训练或评估所使用的具体 GPU 型号、数量、训练时长或计算成本。评估阶段涉及多个 MLLM 的 API 调用（闭源模型）和本地模型（Qwen-72B）的推理，但未报告其部署环境（如 A100、H100 数量等）。仅提及使用 SerpApi 进行搜索，以及使用 Gemini 进行网页摘要。**资源细节缺失**，可能是论文的一个局限。

## 5. 主要结论与发现

1. **现有模型表现较低**：最强系统（o3）在完整部署下仅 36.0% 准确率；开源模型 Qwen-72B 仅 13.5%；人类专家为 22.8%。
2. **SoM 带来一致提升**：Full Rollout + SoM 相比 Full Rollout 在 o3 上 +1.6，Gemini +3.9，Qwen +1.0。
3. **工具使用不足**：在 Easy 子集上，完整部署准确率反而不如仅图像搜索，原因是模型省略了必要的图像搜索（过度依赖文本搜索或内部知识）。
4. **错误类型**：主要错误为“无相关信息”（51.1%）和“幻觉”（11.5%），反映检索失败或视觉错误归因。
5. **场景文字处理方式**：模型主要将图像文字转换为文本查询，而不是使用子图图像搜索。
6. **不同模型策略差异**：o3 倾向于多次缩放但不常跟随图像搜索；Gemini 更常使用缩放后图像搜索；Qwen 工具调用不稳定（421 次无效图像搜索）。
7. **图像搜索与文本搜索各有优势**：图像搜索在影视类表现更好，文本搜索在地理类更有效。

## 6. 优点

- **真正的多模态推理需求**：设计原则强制要求细粒度视觉推理，避免纯文本捷径，填补了现有基准的空白。
- **空间-时间外推方法**：创新性地从空间和时间维度设计问题，使问题更贴近真实世界挑战。
- **模型无关的代理框架与 SoM**：提供标准化工具和人类标注的边界框，使缩放和子图检索成为可能，提升了可重复性。
- **全面的消融与分析**：不仅报告准确率，还深入分析内部知识影响、工具行为模式、错误类型，为后续研究提供了洞察。
- **动态维护**：承诺定期刷新基准以防止模型记忆污染。
- **多类别覆盖**：8 个主类别，43 个子类别，分布平衡。

## 7. 不足与局限

- **数据偏差**：数据主要来自公共视频平台和 arXiv，可能偏向英语、高视觉密度内容；非英语或低视觉密度页面代表性不足。
- **模型评估范围有限**：仅评估了 4 个模型（3 闭源 +1 开源），开源模型仅一个（Qwen-72B），未能覆盖更多开源大模型（如 LLaVA 系列、CogVLM 等）。
- **计算资源未报告**：不知复现实验的成本，难以评估可重复性。
- **SoM 依赖人工标注**：边界框由人类提供，自动生成标记尚不可靠，限制了框架的全自动扩展。
- **动态内容未探索**：仅处理静态图像/截图，未涉及视频、交互式界面或实时直播。
- **内部知识干扰**：尽管做了过滤，但部分闭源模型仍能通过记忆回答少数问题，导致“易”子集准确率波动。
- **代理框架局限性**：工具调用决策受限于模型能力，未能探索更丰富的 UI 控制（如点击、滚动）。
- **评估指标单一**：仅使用准确率，未包括检索效率、路径长度、工具调用次数等细粒度指标。

---

（完）
