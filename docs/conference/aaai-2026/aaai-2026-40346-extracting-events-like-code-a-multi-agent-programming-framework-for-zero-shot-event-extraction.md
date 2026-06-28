---
title: "Extracting Events Like Code: A Multi-Agent Programming Framework for Zero-Shot Event Extraction"
title_zh: 像编码一样抽取事件：面向零样本事件抽取的多智能体编程框架
authors: "Quanjiang Guo, Sijie Wang, Jinchuan Zhang, Ben Zhang, Zhao Kang, Ling Tian, Ke Yan"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40346/44307"
tags: ["query:ie"]
score: 9.0
evidence: 零样本事件抽取多智能体框架
tldr: 针对零样本事件抽取中直接提示导致输出不完整和结构无效的问题，本文提出Agent-Event-Coder，一种将事件抽取视为代码生成的多智能体框架，通过检索、规划、编码和验证子任务分解，利用LLM代理生成结构化事件输出，显著提升了抽取的完整性和准确性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 针对零样本事件抽取中直接提示导致输出不完整、结构无效的问题。
method: 提出Agent-Event-Coder框架，将事件抽取分解为检索、规划、编码和验证子任务，每个子任务由专用LLM代理处理，事件模式表示为可执行类定义。
result: 实验表明该方法能生成结构化事件输出，减少了触发词误分类、论元缺失等问题。
conclusion: 该框架通过将事件抽取建模为代码生成，有效提升了零样本事件抽取的性能和可靠性。
---

## Abstract
Zero-shot event extraction (ZSEE) remains a significant challenge for large language models (LLMs) due to the need for complex reasoning and domain-specific understanding. Direct prompting often yields incomplete or structurally invalid outputs—such as misclassified triggers, missing arguments, and schema violations. To address these limitations, we present Agent-Event-Coder (AEC), a novel multi-agent framework that treats event extraction like software engineering: as a structured, iterative code-generation process. AEC decomposes ZSEE into specialized subtasks—retrieval, planning, coding, and verification—each handled by a dedicated LLM agent. Event schemas are represented as executable class definitions, enabling deterministic validation and precise feedback via a verification agent. This programming-inspired approach allows for systematic disambiguation and schema enforcement through iterative refinement. By leveraging collaborative agent workflows, AEC enables LLMs to produce precise, complete, and schema-consistent extractions in zero-shot settings. Experiments across five diverse domains and six LLMs demonstrate that AEC consistently outperforms prior zero-shot baselines, showcasing the power of treating event extraction like code generation.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：零样本事件抽取（Zero-shot Event Extraction, ZSEE）面临两大挑战：
  - **上下文歧义**：候选触发词多义词常见，直接提示LLM会因注意力失败而误分类（如“strike”可指抗议或攻击）。
  - **结构保真度不足**：LLM直接输出时难以严格遵循预定义的事件模式（Schema），导致格式错误、论元缺失、角色幻觉等。
- **研究动机**：现有方法（如直接提示、对话式提取、代码结构化）在零样本场景下表现不佳，缺乏系统性的歧义消解和模式约束机制。
- **整体含义**：本文首次将ZSEE重新定义为**多智能体协作的代码生成过程**，通过编程范式融合结构约束与迭代推理，为结构化预测提供了新范式。

## 2. 论文提出的方法论
### 核心思想：Agent-Event-Coder (AEC)
将事件抽取视为软件工程中的**结构化、迭代代码生成任务**，通过四个专用LLM智能体协作完成：
- **检索智能体 (Retrieval Agent)**：利用类比提示（analogical prompting）自我生成k个高质量示例，弥合模式定义与文本上下文之间的鸿沟。
- **规划智能体 (Planning Agent)**：结合输入文本和检索示例，生成带置信度分数和自然语言解释的触发词-事件类型假设列表（Top-k）。
- **编码智能体 (Coding Agent)**：将最高置信度的假设转化为可执行Python代码，实例化预定义的事件类模板（图4所示固定输出模板）。
- **验证智能体 (Verification Agent)**：执行三阶段确定性测试套件（语义检查T1、类型检查T2、结构检查T3），返回二元结果和失败诊断信息。

### 关键技术细节
- **模式即代码 (Schema-as-Code)**：将事件模式编译为Python BaseModel，构造函数强制角色类型，实现运行时确定性验证。
- **双循环优化算法 (Dual-Loop Refinement Algorithm)**：
  - 外层：当当前假设的所有修补尝试用尽后，回溯到下一最佳假设（最多k个假设）。
  - 内层：对当前假设执行最多t次迭代修补，每次根据验证失败的诊断信息生成修正代码。
  - 算法复杂度O(k·t)，保证最终输出既语义正确又符合模式。

## 3. 实验设计
### 数据集与场景
- **5个领域数据集**：
  - FewEvent（通用领域，100种事件类型，仅触发词/事件识别）
  - ACE 2005（新闻，33种事件类型，含论元识别与分类）
  - GENIA（生物医学，9种事件类型）
  - SPEED（流行病学，7种事件类型，仅触发词/事件识别）
  - CASIE（网络安全，5种事件类型，含论元）
- **采样策略**：为避免分布偏差，每个数据集均匀采样250个测试实例（CASIE为50个），严格遵循TextEE评估协议。

### 基准方法 (Baselines)
- **DirectEE**：单步直接提示
- **CEDAR**：多阶段层级检测框架（仅事件检测，未报道论元指标）
- **DecomposeEnrichEE**：分解为事件检测和论元提取，结合动态模式感知检索
- **GuidelineEE**：将事件抽取转换为结构化Python代码生成任务
- **ChatIE**：多轮对话式抽取

所有基线均统一输出结构化事件对象，并集成了验证组件保证公平性。

### 基座LLM
- Llama3-8B-Instruct / Llama3-70B-Instruct
- Qwen2.5-14B-Instruct / Qwen2.5-72B-Instruct
- GPT-3.5-turbo / GPT-4o

### 评估指标
- 触发词识别 (TI)、事件识别 (EI)、论元识别 (AI)、论元分类 (AC) — 微平均F1分数。

## 4. 资源与算力
- **GPU型号**：NVIDIA RTX A800 (每个节点4张GPU)
- **数量**：未明确说明使用多少节点，但所有开源模型在本地A800集群上推理。
- **训练时长**：论文声明“AEC在LLM骨干网上实现，不进行任何额外微调”，因此仅涉及推理。文中未报告具体推理时间或算力消耗，仅说明使用4张GPU运行开源模型。
- **备注**：由于零样本方法无需训练，主要算力开销来自多智能体迭代推理（k=3, t=3），但论文未量化该开销。

## 5. 实验数量与充分性
### 实验组数量
- **主实验**：在2个LLM（Llama3-8B/70B）上对比5个基线，覆盖5个数据集，共2×5×5=50组（部分基线限于TI/EI指标）。
- **泛化实验**：在另外4个LLM（Qwen2.5-14B/72B, GPT-3.5/4o）上对比GuidelineEE和DecomposeEE，共4×2×5=40组。
- **消融实验**：在2个LLM（Llama3-70B, GPT-4o）上、2个数据集（FewEvent, ACE）上，去除5个组件（检索、规划理由、验证循环、结构检查），共2×2×4=16组。
- **超参数分析**：k和t的影响（5种组合），以及验证用例数量的影响（5个值），在GPT-4o上进行。
- **定性分析**：3个示例的逐组件对比。
- **总计约**：50+40+16+若干超参数实验 = 超过100组实验结果报告。

### 充分性与公平性
- **充分**：覆盖了多领域、多规模LLM、多种基线，消融实验全面，超参数分析细致，定性分析直观。
- **公平**：所有基线均统一输出格式并集成验证组件，采用TextEE基准框架，微平均F1，三次独立运行取平均。
- **客观**：公开代码、数据集采样标准流程，具有可复现性。

## 6. 论文的主要结论与发现
1. **AEC在所有基准上一致最优**：特别是在复杂模式的数据集（ACE 2005, GENIA）上提升显著，Llama3-70B在ACE上TI提升+5.5%（57.0 vs 51.5），EI提升+5.9%（54.6 vs 48.7）。
2. **跨LLM泛化能力强**：从8B到GPT-4o，AEC平均比最强基线DecomposeEE高3~5% TI、4~6% EI、2~4% 论元指标。
3. **各组件不可或缺**：消融实验显示去除验证循环导致性能下降最严重（Llama3-70B在ACE上TI下降9.9%），检索和规划理由同样关键。
4. **超参数敏感性低**：k=3, t=3即达到饱和，继续增加收益微弱。
5. **验证用例数量以3个为最优**：过多测试用例增加开销但提升有限。

## 7. 优点
- **方法论创新**：首次将ZSEE建模为多智能体代码生成，巧妙融合“模式即代码”的确定性验证与LLM的语义理解。
- **系统化消歧**：检索+规划+编码的逐步推理有效缓解上下文歧义。
- **结构保真保障**：双循环迭代+三阶段测试确保输出严格符合模式，避免格式错误和角色幻觉。
- **实验扎实**：覆盖5个领域、6个LLM、全面基线、深入消融和超参数分析，结果具有说服力。
- **可复现性强**：提供开源代码，采用标准TextEE基准框架。
- **零样本实用性强**：无需任何标注数据，可直接应用于新事件类型。

## 8. 不足与局限
- **计算开销**：多智能体迭代推理（k×t次LLM调用）比单步提示慢，文中未量化延迟和成本，实际部署可能需要权衡效率。
- **长文本处理能力未验证**：实验仅使用短文本片段（均基于TextEE采样），对于长文档或多事件嵌套场景效果未知。
- **论元抽取性能仍有限**：在ACE上最佳AC仅34.7%（Llama3-70B），远低于有监督方法，说明零样本论元抽取距离实用仍有差距。
- **依赖LLM推理能力**：基座LLM较强时效果更好（GPT-4o > Qwen2.5-72B > Llama3-70B），弱模型可能因规划或编码不准确而失效。
- **事件类型数量限制**：实验中最大事件类别为100（FewEvent），未验证千级类型场景的扩展性。
- **可能存在的偏差**：采样250个实例的随机性可能导致结果波动，虽取三次平均但未报告标准差。
- **未与有监督方法对比**：实验仅在零样本基线间比较，未说明与全监督方法的差距，因此读者难以判断“零样本性能是否够用”。

（完）
