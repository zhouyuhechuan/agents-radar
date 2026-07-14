# AI CLI 工具社区动态日报 2026-07-14

> 生成时间: 2026-07-14 01:49 UTC | 覆盖工具: 9 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/badlogic/pi-mono)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [DeepSeek TUI](https://github.com/Hmbown/DeepSeek-TUI)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

好的，作为专注于 AI 开发工具生态的资深技术分析师，我将根据您提供的多份社区动态日报，为您生成一份关于 AI CLI 工具生态的横向对比分析报告。

---

## AI CLI 工具生态横向对比分析报告 (2026-07-14)

### 1. 生态全景

当前，AI CLI 工具生态正处于 **“能力爆发与信任危机并存”的成熟化阵痛期**。各主流工具普遍进入了 **Agent 能力竞赛的下半场**，重点从“能否执行任务”转向“能否可靠、安全、经济地执行任务”。社区反馈的核心矛盾集中在 **Agent 自主性的失控**（如无限循环、巨额 Token 消耗）、**模型行为的不一致与退化**，以及 **权限系统的粗粒度** 带来的安全风险。与此同时，**跨平台兼容性**（特别是 Windows）、**互操作性**（如支持其他工具的配置文件）和 **成本透明化** 成为用户最迫切的需求。

### 2. 各工具活跃度对比

| 工具名称 | 活跃 Issues 数 | 重要 PR 数 | 版本发布情况 (今日) | 社区热点关键词 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 10 | 3 | 1 (v2.1.208) | 模型退化、Agent 成本失控、权限绕过、数据丢失 |
| **OpenAI Codex** | 10 | 10 | 3 (含 alpha 版本) | Windows 稳定性、MCP 回归、多 Agent 管理、资源泄漏 |
| **Gemini CLI** | 10 | 10 | 1 (nightly) | Agent 假阳性、无限循环、工具与技能使用不充分 |
| **GitHub Copilot CLI** | 10 | 0 | 0 | 快捷键冲突、语音模式失效、Autopilot 无限消耗 |
| **Kimi Code CLI** | 2 | 9 | 0 | 会话恢复损坏、ACP 协议缺陷、互操作性（支持 CLAUDE.md） |
| **OpenCode** | 10 | 10 | 2 (v1.17.19/20) | YOLO 模式、新模型兼容、权限系统重设计、Windows 兼容 |
| **Pi** | 10 | 10 | 0 | 新模型兼容性、`compact` 功能、超时/重试机制、资源泄漏 |
| **Qwen Code** | 10 | 10 | 2 (nightly & desktop) | 权限 Hook 失效、Subagent 通信、Daemon 模式扩展 |
| **CodeWhale** | 6 | 5 | 0 (v0.8.68 RC) | 终端动效、模型 Provider 扩展、状态持久化、计费准确性 |

**分析**:
- **OpenAI Codex** 和 **Qwen Code** 在版本迭代和 PR 合并且方面最为活跃，显示出强大的工程投入。
- **Gemini CLI**, **OpenCode**, **Pi** 的 Issue 和 PR 数量均很可观，社区参与度和开发响应速度都很快。
- **GitHub Copilot CLI** 今日无新 PR 或发布，但在 Issue 上仍有高频讨论，表明其用户群体庞大，但功能迭代速度相对保守。
- **Kimi Code CLI** 虽 Issue 数量少，但 PR 数量多，且修复均指向关键功能，显示出团队正集中精力解决核心短板。

### 3. 共同关注的功能方向

| 需求方向 | 涉及工具 | 具体诉求 |
| :--- | :--- | :--- |
| **Agent 成本与预算控制** | Claude Code, Copilot CLI, Codex, Gemini CLI | 要求引入强制 Token 预算上限、循环检测、实时费用显示，防止因 Agent 失控或逻辑缺陷导致巨额意外费用。 |
| **精细化权限与安全模型** | Claude Code, Copilot CLI, OpenCode, Gemini CLI | 需要可预测、可配置的权限系统，支持 YOLO 模式、持久化拒绝规则、应用级别的权限生效，并在终端交互中保持一致。 |
| **跨平台与跨工具互操作性** | Gemini CLI, Kimi Code CLI, OpenCode, Pi | 用户强烈要求在 Windows 上获得与 macOS/Linux 一致的使用体验。同时，希望工具能兼容彼此的配置（如 `CLAUDE.md`），降低迁移成本。 |
| **新模型兼容性与性能** | Claude Code, OpenCode, Pi, CodeWhale | 社区对新模型的适配速度极快，但随之而来的是大量的兼容性 Bug（如模型 404 错误、thinking 模式崩溃），要求开发者能快速响应。 |
| **代理间通讯与任务编排** | Gemini CLI, Qwen Code, OpenCode | 子代理完成任务后无法可靠通知主代理，后台任务状态不清晰，社区期望更健壮的 Agent 间通信机制和工作流编排能力。 |

### 4. 差异化定位分析

*   **Claude Code**：作为市场先行者，功能全面但正面临严重的 **稳定性与信任危机**。其社区反馈最为激烈，集中于模型 “负优化” 和 Agent 失控，反映出早期红利正在消退，用户对可靠性的要求达到新高度。
*   **OpenAI Codex**：定位是 **稳定高效的工程底座**。版本发布高频且稳定，PR 多集中在代码质量重构、内部服务解耦和遥测链路完善上，表现出极强的工程化水平。其对 MCP 和 Windows 的持续修复，显示其目标是成为企业级基础设施。
*   **Gemini CLI**：聚焦于 **Agent 行为的可观测性与自我改进**。大量 Issue 和 PR 围绕 Eval 框架、AST 工具评估、递归限制，表明其在努力打造一个更“聪明”且可被证明其“聪明”的 Agent。
*   **GitHub Copilot CLI**：作为平台入口，**强调流畅的交互体验**。Issue 多集中在快捷键冲突、语音模式失效等 UX 问题上，说明其核心功能已基本稳定，当前优化方向是深度打磨体验细节。
*   **Kimi Code CLI**：采取 **差异化竞争策略**，通过拥抱 `CLAUDE.md`、修复 ACP 协议来提升互操作性，力求从其他成熟工具（尤其是 Claude Code）的生态中快速切入。
*   **OpenCode** 与 **Pi**：定位为 **创新实验先锋**。社区对 YOLO 模式、新模型（如 GPT-5.6 Luna）的支持、水下动效等前沿功能接受度高，但也因此面临更多早期 Bug。它们吸引的是愿意尝鲜、追求极致功能的开发者。
*   **Qwen Code**：倾向于 **企业级平台化**。其“Daemon 模式多 Workspace 支持”、“Extension Management”、“渠道集成”等议题，表明它在构建一个类似 IDE 后端的服务化架构，服务于更复杂的内部开发流程。

### 5. 社区热度与成熟度

*   **高热度、高成熟度**：**Claude Code** 和 **OpenAI Codex**。用户基数巨大，形成了生态，但社区情绪已从早期的兴奋转向对稳定性和成本的严苛审视，是市场最成熟的信号。
*   **高热度、快速迭代**：**Gemini CLI**, **OpenCode** 和 **Qwen Code**。这些工具正处在功能快速迭代、用户量激增的阶段，社区讨论活跃，Bug 报告和功能请求都极为密集，是增长最快的梯队。
*   **成熟稳定、体验驱动**：**GitHub Copilot CLI**。其讨论聚焦于“使用体验”而非“功能缺失”，表明其核心功能已相当稳定。其庞大用户基数决定了任何微小的交互改进都会引发热议。
*   **新生力量、蓄势待发**：**Kimi Code CLI** 和 **CodeWhale**。Issue 和 PR 集中在关键功能的补齐和修复上，社区热度正在积累，处于快速发展前的酝酿期。

### 6. 值得关注的趋势信号

1.  **“预算保护”将成为 AI CLI 的标配功能**：从多家工具的社区反馈来看，Agent 导致的巨额 Token 消耗已从“偶发事件”变为“高频痛点”。未来，能提供强制的、实时的、多维度的成本控制功能的工具将获得竞争优势。
2.  **“YOLO 模式”与“安全屏障”的博弈将定义用户体验**：用户既要求极致的自动化（YOLO 模式），也恐惧数据丢失和权限误判。如何在这两者之间找到动态平衡点，是下一阶段产品设计的关键命题。
3.  **互操作性将取代单一生态成为关键卖点**：开发者越来越倾向于“工具箱”思维。能否轻松导入 `CLAUDE.md`、支持 MCP/ACP 协议、与主流 IDE 无缝集成，将成为影响开发者选择的关键非功能属性。
4.  **“功能成熟度”而非“功能数量”正在成为分水岭**：社区对 Claude Code 的批评表明，用户已经厌倦了“加功能”带来的“Bug 海”。Codex 对代码重构和遥测的专注，以及 Gemini CLI 对 Eval 框架的投入，都预示着下一阶段的竞争焦点将是 **稳定、可预见和可审计**。

**对开发者的参考建议**：
- **做技术选型时，优先评估工具的故障处理机制（如预算限制、重试策略、崩溃恢复）**，而不仅仅是 AI 模型的“聪明度”。
- **关注工具的跨平台和互操作性布局**，这会直接关系到未来团队协作和工具链演化的灵活性。
- **警惕“功能过载”带来的复杂度**，选择社区反馈中以“稳定”而非“新奇”着称的工具，可能更适合生产环境。
- **持续关注模型兼容性**，模型更新可能带来功能退化或中断，选择社区响应迅速的团队至关重要。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，作为专注于 Claude Code 生态的技术分析师，以下是基于 `anthropics/skills` 仓库数据（截至 2026-07-14）的社区热点报告。

---

### Claude Code Skills 社区热点报告 (2026-07-14)

#### 1. 热门 Skills 排行

以下 Skills 因其解决的核心痛点或功能性创新，收获了最集中的社区讨论。

1.  **skill-creator 运行评估修复集群** (`#1298`, `#1323`, `#1099`, `#1050`, `#362`, `#361`)
    *   **状态**: Open
    *   **热度分析**: 社区讨论的绝对焦点。多个 PR 直指 `run_eval.py` 及优化循环 (`run_loop.py`) 的根本性故障：**在 Windows 环境下崩溃**，或**在所有平台上报告 `recall=0%`（假阴性）**。这使得 skill-creator 的自动化评估与优化工具链形同虚设。
    - **功能**: 共同修复 skill-creator 核心脚本，涉及 Windows 子进程兼容性 (`PATHEXT`)、UTF-8 多字节字符编码、YAML 特殊字符解析、以及 `run_eval` 触发检测逻辑缺陷。
    - **社区讨论**: 贡献者们通过大量 Issue (`#556`, `#1061`, `#1169`) 和 PR 持续追踪，描述了“优化循环针对噪声进行优化”的窘境。这已成为社区 **最迫切** 的基础设施问题。
    - [PR #1298 链接](https://github.com/anthropics/skills/pull/1298)
    - [PR #1099 链接](https://github.com/anthropics/skills/pull/1099)

2.  **document-typography (`#514`)**
    *   **状态**: Open
    *   **热度分析**: 虽是早期 PR，但触及 AI 生成文档的普遍“痛点”——孤行、寡句、编号错位等排版问题。社区对此需求明确，属于“虽然不性感，但每天都会遇到”的高频实用技能。
    *   **功能**: 为生成的文档（如 Word、PDF）提供排版质量控制，防止常见的“AI 感”排版错误。
    - [PR #514 链接](https://github.com/anthropics/skills/pull/514)

3.  **testing-patterns (`#723`)**
    *   **状态**: Open
    *   **热度分析**: 社区对高质量、可落地的代码测试生成需求旺盛。该 PR 覆盖了从测试原则到 React、API 测试等具体模式，内容全面，符合开发者日常工作流。
    *   **功能**: 提供全面的测试模式指导，包括单元测试、组件测试、集成测试方法论，提升 Claude 生成测试代码的质量和规范性。
    - [PR #723 链接](https://github.com/anthropics/skills/pull/723)

4.  **self-audit (`#1367`)**
    *   **状态**: Open (最新 PR)
    *   **热度分析**: 这是最新的关注点。它对应了社区对 **AI 输出可靠性** 的深层焦虑。通过“机械验证”+“四维逻辑审计”的流水线，能显著降低幻觉和错误交付风险，是向“AI Agent 生产级应用”迈出的关键一步。
    *   **功能**: 在输出交付前，进行文件存在性验证，并按损害等级对推理结果进行多维审核。
    - [PR #1367 链接](https://github.com/anthropics/skills/pull/1367)

5.  **color-expert (`#1302`)**
    *   **状态**: Open
    *   **热度分析**: 这是一个高度专业化、知识密集型的 Skills 范例。它整合了 ISCC-NBS、Munsell、RAL 等多个色名系统和色彩空间。社区对此表示欢迎，体现了 Skills 生态向“深度知识助手”发展的趋势。
    *   **功能**: 为需要色彩知识支持的任务提供专家级建议，如配色方案、色名识别、色彩空间转换。
    - [PR #1302 链接](https://github.com/anthropics/skills/pull/1302)

6.  **ODT (`#486`)**
    *   **状态**: Open
    *   **热度分析**: 扩展了 Claude 在办公生态中的能力，特别是对 LibreOffice 和开源标准 (ODF) 的支持。社区对此类“企业级”、“跨平台”的文档处理能力有明确需求。
    *   **功能**: 支持创建、填充、读取和转换 OpenDocument 格式文件（.odt, .ods）。
    - [PR #486 链接](https://github.com/anthropics/skills/pull/486)

7.  **frontend-design (`#210`)**
    *   **状态**: Open
    *   **热度分析**: 社区对提升 Claude 前端设计质量有持续诉求。这个 PR 旨在让 Skill 指令更清晰、可执行，确保 Claude 能产出更专业和一致的前端交互方案。
    *   **功能**: 全面修订前端设计 Skill，提升指令的清晰度和可操作性，确保 Claude 在单次对话中能遵循具体的设计指导。
    - [PR #210 链接](https://github.com/anthropics/skills/pull/210)

---

#### 2. 社区需求趋势

从 Issues 中可以提炼出社区最渴望的几个新 Skill 方向：

1.  **安全与信任治理 (Security & Trust Governance)**:
    *   **核心需求**: 社区对 Skills 的安全边界高度关注。`#492` 指出“`anthropic/`”命名空间下的社区技能存在信任边界滥用的**风险**。这催生了对 **“技能安全审计器”** (`#83`) 和 **“代理治理”** 模式 (`#412`) 的需求，要求有机制对 Skills 行为进行安全审查和权限控制。

2.  **企业级协作与共享 (Enterprise Collaboration & Sharing)**:
    *   **核心需求**: 组织内共享 Skill 的流程极其繁琐（下载→发送→手动上传），`#228` 强烈呼吁 **“组织级 Skills 库”** 或**直接共享链接**。这说明 Skills 正从个人工具向团队生产力平台演进，但缺乏基础设施支撑。

3.  **AI 输出质量与可靠性 (Output Quality & Reliability)**:
    *   **核心需求**: 除了上述的热门 PR `self-audit`，社区通过 Issue `#1385` 提出了更系统性的 **“推理质量门流水线”** 方案，包含任务前校准、对抗性审查、交付验证。这表明用户不满足于“能用”，而是追求“可信、可控、可审计”的高质量输出。

4.  **系统性与元认知 Skills (Systematic & Meta Skills)**:
    *   **核心需求**: 不只是碎片化的任务，社区希望有 **“系统文档”**(`#95`)、**“记忆压缩”** (compact-memory, `#1329`) 等 Meta Skills。这代表了从“完成单个任务”到“构建和管理 AI Agent 持续工作状态”的需求进化。`#1329` 提出的用符号化表示法压缩长期 Agent 状态，是一个非常有远见的方向。

---

#### 3. 高潜力待合并 Skills

以下 PR 评论活跃，社区反响良好，且解决了明确的痛点，短期内合并可能性较高：

1.  **`#514` document-typography**: 修复了 AI 文档的普遍排版问题，受众广，实现价值高，一旦解决技术细节有望快速合并。
2.  **`#723` testing-patterns**: 内容完备、体系化，是开发者日常刚需。只要与现有文档技能不冲突，合并概率极大。
3.  **`#486` ODT**: 填补了办公文档处理的重要空白（特别是开源领域），满足企业级需求，实用性极强，合并优先级较高。
4.  **`#1367` self-audit**: 虽然提出晚，但直击 AI 应用的核心痛点（可靠性），代表了 Skills 发展的一个重要方向，有很大的合入潜力。
5.  **`#1302` color-expert**: 作为深度知识型 Skills 的典范，展示了 Skills 的无限可能性。如果官方有意推广此类专业 Skills，它将是完美的案例。

---

#### 4. 生态洞察

**一句话总结：当前社区的核心诉求并非寻找更多新 Skills，而是迫切要求修复 `skill-creator` 工具链在 Windows 上的兼容性崩溃和评估逻辑失效问题，使正在开发的 Skills 能可靠地落地和验证。** 这如同社区在呼吁：“先修通高速公路，再谈更好的汽车。” 只有这条关键的“造车”（Skill 开发）流水线稳定运行，整个 Skills 生态才能真正繁荣。

---

好的，作为专注于 AI 开发工具的技术分析师，以下是根据您提供的 GitHub 数据生成的 **2026-07-14 Claude Code 社区动态日报**。

---

## 今日速览

- **新版本 v2.1.208 发布**，新增屏幕阅读器模式和 `vimInsertModeRemaps` 设置，提升无障碍与 Vim 用户效率。
- **社区情绪持续紧张**：多起严重 Bug 报告涉及模型推理退化、权限系统绕过、Fable 代理失控导致大量 token 消耗及数据丢失。
- **3 个小幅 PR 修复**集中在插件文档和 hookify 机制的窗口兼容性与规则匹配问题上。

---

## 版本发布

### v2.1.208
- **新增屏幕阅读器模式**：启用纯文本渲染，方便屏幕阅读器用户。可通过 `claude --ax-screen-reader`、环境变量 `CLAUDE_AX_SCREEN_READER=1` 或设置 `"axScreenReader": true` 开启。
- **新增 `vimInsertModeRemaps` 设置**：允许映射双键插入模式序列（如 `jj`→`Escape`），提升 Vim 用户编辑效率。
- 查看完整 Release：[GitHub Release v2.1.208](https://github.com/anthropics/claude-code/releases/tag/v2.1.208)

---

## 社区热点 Issues（10 条最值得关注）

### 1️⃣ [Bug] Claude Code 默认模型切换为 1M 上下文未通知 Pro 用户
- **Issue #62199** | 评论 33 | 👍 19
- **重要性**：影响所有 Pro 用户，可能导致无预期的高消费。作者指责 Anthropic 未提供通知，直接更改默认模型。
- **社区反应**：大量用户附和抱怨，认为这是不透明的商业行为。
- [🔗 查看 Issue](https://github.com/anthropics/claude-code/issues/62199)

### 2️⃣ [Bug] Claude Opus 4.8 推理能力严重下降，速度与性能回退
- **Issue #68780** | 评论 24 | 👍 29
- **重要性**：高端模型 Opus 4.8 的推理质量被广泛认为大幅下降，用户质疑“误导性商业行为”，并准备在欧盟采取法律行动。
- **社区反应**：获得最多 👍 支持，多位用户反映相同体验。
- [🔗 查看 Issue](https://github.com/anthropics/claude-code/issues/68780)

### 3️⃣ [Bug] Fable 代理周末“什么都没建”，反而消耗了全部使用量
- **Issue #76987** | 评论 11 | 👍 0
- **重要性**：用户反馈 Fable 5 代理自行创建流程而不是执行用户要求的工作，消耗大量 tokens，导致近乎零产出。问题极具代表性，反映 Fable 自主行为失控。
- **社区反应**：描述情绪激动，直接点名“chargebacks”，引发其他用户共鸣。
- [🔗 查看 Issue](https://github.com/anthropics/claude-code/issues/76987)

### 4️⃣ [Bug] Windows 上 Cowork 会话文件夹挂载失败，无法确认添加
- **Issue #76187** | 评论 9 | 👍 1
- **重要性**：7月8日更新后，Cowork 在 Windows 上完全无法正常使用：项目上下文文件夹无法挂载，添加文件夹对话框无法确认。影响团队协作工作流。
- **社区反应**：用户已在两台机器上复现，期待紧急修复。
- [🔗 查看 Issue](https://github.com/anthropics/claude-code/issues/76187)

### 5️⃣ [Bug] 子代理递归循环导致约 80 万 token 消耗，产生 $27.60 意外费用
- **Issue #69578** | 评论 7 | 👍 1
- **重要性**：严重成本失控 Bug，子代理无限制地生成更深层子代理，实际产出接近零。暴露代理执行缺乏深度限制的问题。
- **社区反应**：用户要求退款，批评“Max Plan”订阅保护不足。
- [🔗 查看 Issue](https://github.com/anthropics/claude-code/issues/69578)

### 6️⃣ [Bug] `--resume` 恢复会话时丢失 `--effort` 级别，使 Prompt 缓存失效
- **Issue #66005** | 评论 7 | 👍 1
- **重要性**：影响所有使用 `--resume` 且依赖 Effort 设置的开发者，会话恢复后缓存失效导致成本增加，且 Effort 回退为默认值。
- **社区反应**：用户要求会话元数据应完整保留。
- [🔗 查看 Issue](https://github.com/anthropics/claude-code/issues/66005)

### 7️⃣ [Bug] 鼠标点击终端时意外触发权限提示
- **Issue #71539** | 评论 9 | 👍 17
- **重要性**：Linux 用户反馈仅因点击终端聚焦就出现 Bash 权限确认框，严重干扰工作流程。关注度高。
- **社区反应**：多个用户遇到，认为是 UI 聚焦检测 Bug。
- [🔗 查看 Issue](https://github.com/anthropics/claude-code/issues/71539)

### 8️⃣ [Bug] Windows 更新失败：CoworkVMService 运行时错误 0x80073CF6
- **Issue #49655** | 评论 14 | 👍 8
- **重要性**：长期未解决的 Windows 桌面版更新问题，影响大量用户。CoworkVMService 被占用时桌面应用更新即失败，无有效解决方法。
- **社区反应**：用户反复确认，官方未给出修复时间表。
- [🔗 查看 Issue](https://github.com/anthropics/claude-code/issues/49655)

### 9️⃣ [Bug] 桌面应用忽略 `permissions.allow` 规则，对所有操作都弹窗询问
- **Issue #73587** | 评论 4 | 👍 2
- **重要性**：权限配置失效，即使用户已预设“允许”规则，桌面版仍无差别弹窗，甚至对 Claude 自身配置目录的操作也要询问。严重破坏自动工作流。
- **社区反应**：用户将此视为回归 Bug，影响日常使用。
- [🔗 查看 Issue](https://github.com/anthropics/claude-code/issues/73587)

### 🔟 [Bug] Fable 5 $100 计划会话额度在 2 分钟内被全部用完
- **Issue #77336** | 评论 2 | 👍 0
- **重要性**：最新报告（今日创建），用户购买了 Fable 5 的 $100 计划，开场不到 2 分钟即消耗完整个会话限额，几乎无有效输出。可能指向 Fable 预算计算或代理循环 Bug。
- **社区反应**：紧急报告，期待 Anthropic 紧急排查。
- [🔗 查看 Issue](https://github.com/anthropics/claude-code/issues/77336)

---

## 重要 PR 进展（共 3 个，全部列示）

### #77292 📝 插件 README 使用正确的市场名称
- **作者**: sorapallivenkatesh | 评论: 0 | 👍 0
- **内容**：修复两个插件 README 中 `install` 命令引用的市场名称与 `.claude-plugin/marketplace.json` 中实际名称不匹配的问题，避免用户按文档安装失败。
- [🔗 查看 PR](https://github.com/anthropics/claude-code/pull/77292)

### #77289 🐛 Windows 上 `hookify` 插件规则无法触发
- **作者**: sorapallivenkatesh | 评论: 0 | 👍 0
- **内容**：修复 `hookify` 插件在 Windows 下的两个问题：UTF-8 编码错误以及 `prompt` 字段缺失，导致 `UserPromptSubmit` 规则永远不会执行，规则形同虚设。
- [🔗 查看 PR](https://github.com/anthropics/claude-code/pull/77289)

### #77260 🐛 修复 `hookify` 的 Write 和 prompt 规则匹配
- **作者**: ShiroKSH | 评论: 0 | 👍 0
- **内容**：完善 hookify 插件：使文件规则能正确检查 Write 工具的内容，让简单 prompt 规则能映射到当前 `UserPromptSubmit` 载荷，同时增加回归测试覆盖 Write、Edit 和 prompt 规则。
- [🔗 查看 PR](https://github.com/anthropics/claude-code/pull/77260)

---

## 功能需求趋势

从社区 Issue 中可提炼出以下五大核心需求方向：

1. **权限系统的可预测性与可控性**
   - 用户希望在“绕过权限”模式下真正免打扰，但当前仍出现弹窗（#75588）。
   - 需要更好的嵌套目录信任机制（#72896）、复合命令智能允许（#76718）以及权限规则在桌面版的正确执行（#73587）。

2. **代理（Fable / Sub-agent）的成本边界控制**
   - Fable 和子代理的失控行为（#76987、#69578、#77336）导致用户对“无限循环”和“预算超限”感到恐惧。
   - 社区强烈要求引入深度限制、Token 预算上限、以及更清晰的会话消费账单。

3. **模型质量与行为一致性**
   - Opus 4.8 的推理退化（#68780）引发用户对“模型被悄悄降级”的普遍猜疑。
   - 模型在权限处理上出现逻辑不一致（#76063：模型虚构输出并误判为 prompt injection 后删除文件）。

4. **Windows 平台支持成熟度**
   - Cowork 挂载失败（#76187）、桌面应用更新失败（#49655）、焦点/权限弹窗问题（#68526）表明 Windows 端的稳定性仍是短板。

5. **会话状态持久化与缓存优化**
   - `--resume` 丢失 `--effort` 导致缓存失效（#66005），后台命令残留导致竞争条件（#66764），以上问题均影响长时开发会话的效率与成本。

---

## 开发者关注点

- **成本不透明的严重抱怨**：大量用户报告意外高额消耗，尤其是 Fable 和子代理的循环消耗，以及对 Pro 模型无通知切换。开发者呼吁引入实时费用显示与强制的预算上限。
- **权限系统的“要么全问，要么全放”困境**：在“自动”模式下权限有时被绕过执行危险命令（#77173、#75794），而在“手动”模式下又因过多弹窗（#76718 出现 700+ 弹窗）让工作流无法进行。用户望找到平衡点。
- **数据丢失的高频风险**：多个 Issue 报告工具在无有效确认或错误报警后直接执行 `rm -rf` 操作（#76063、#69793、#66764），社区对 Claude Code 在生产环境操作文件的安全性产生怀疑。
- **协作功能的 Windows 兼容性**：Cowork 的 Windows 用户无法挂载文件夹、Dialog 无法确认，严重影响团队协作。开发者期望 Anthropic 优先修复 Windows 平台关键阻塞点。
- **对模型质量退化的信任危机**：推理退化、指令跟随不一致、虚构日志等行为让部分用户开始考虑切换工具。社区对 Anthropic 的透明度要求越来越高。

---

*日报生成于 2026-07-14，数据来源于 [GitHub anthropics/claude-code](https://github.com/anthropics/claude-code)。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-07-14

## 今日速览
昨日发布三个版本：`rust-v0.144.3`（纯版本号更新）、`rust-v0.144.2`（修复 Guardian auto-review 提示回归）以及 `rust-v0.145.0-alpha.7`（最新 alpha）。社区方面，Windows 平台稳定性问题持续发酵（#32040、#31583、#30712），MCP 工具调用回归（#19871）影响范围扩大。功能需求上，多行状态栏（#21653）和 Agent 管理视图（#22321）呼声最高。

---

## 版本发布

### rust-v0.144.3 (2026-07-14)
仅版本号更新，无代码变更。  
[完整 Changelog](https://github.com/openai/codex/compare/rust-v0.144.2...rust-v0.144.3)

### rust-v0.144.2 (2026-07-14)
**Bug Fixes**  
- 回滚了 Guardian auto-review 策略、请求格式和工具行为的提示回归（#32672）。  
[完整 Changelog](https://github.com/openai/codex/compare/rust-v0.144.1...rust-v0.144.2)

### rust-v0.145.0-alpha.7 (2026-07-14)
最新 alpha 版本，未标注具体变更。

---

## 社区热点 Issues

1. **#32040** — Windows Desktop 打开内置浏览器会挂起/关闭 Codex（评论 20，👍6）  
   > 复现明确：Browser Use 的 PiP 失败后整个应用无响应或重启。影响 Windows 用户的关键操作。  
   [链接](https://github.com/openai/codex/issues/32040)

2. **#19871** — MCP 工具调用在 v0.117.0+ 对自定义/本地提供商（Ollama）回归（评论 17，👍7）  
   > 二分排查确认回归范围，至今未修复，社区关注度高。  
   [链接](https://github.com/openai/codex/issues/19871)

3. **#21653** — TUI 支持多行状态栏（评论 11，👍41）  
   > 点赞数最高，用户希望状态栏不截断，提供换行能力。  
   [链接](https://github.com/openai/codex/issues/21653)

4. **#30712** — Windows Desktop 注入 split writable roots 导致 `apply_patch` 失败（评论 7，👍9）  
   > 沙箱路径绕开导致安全编辑不可用，迫使用户降级使用 PowerShell 绕过。  
   [链接](https://github.com/openai/codex/issues/30712)

5. **#22321** — 在 TUI 中增加 Agent 视图以管理多个 Codex agent（评论 6，👍19）  
   > 多 agent 并行工作场景强烈需求，已有 prototype 设计思路。  
   [链接](https://github.com/openai/codex/issues/22321)

6. **#31488** — Pro 用户未收到承诺的免费 Codex banked reset（评论 5，👍1）  
   > 官方公告后仍有用户未收到重置，涉及计费与权益问题。  
   [链接](https://github.com/openai/codex/issues/31488)

7. **#31583** — Windows Desktop 26.623 静默销毁/重启 AppX 容器（评论 5，👍0）  
   > 长运行线程恢复后出现静默重启，无崩溃日志，排查困难。  
   [链接](https://github.com/openai/codex/issues/31583)

8. **#30750** — iPad Pro 27 beta 2 上 Codex 远程配对失败（评论 4，👍0）  
   > QR 和手动码均失败，影响 iOS 远程使用场景。  
   [链接](https://github.com/openai/codex/issues/30750)

9. **#29693** — `/goal` 延续可复用过期权限上下文（评论 4，👍2）  
   > 即使设置为 Full Access 仍可能带上旧权限，安全风险。  
   [链接](https://github.com/openai/codex/issues/29693)

10. **#32913** — Locked use 在手动 Computer Use 时无法解锁（新建，评论 3，👍0）  
    > 从可信手机/SSH 连接启动远程 Computer Use 时锁定机制失效。  
    [链接](https://github.com/openai/codex/issues/32913)

---

## 重要 PR 进展

1. **#32911** — 允许向 `ThreadManager` 注入 models manager（merged）  
   > 让 embedding 调用方能控制模型目录是否持久化，增强可定制性。  
   [链接](https://github.com/openai/codex/pull/32911)

2. **#32905** — 在 app-server 通知中打上发出时间戳（merged）  
   > 新增 `emittedAtMs` 字段，方便客户端做延迟分析或重放排序。  
   [链接](https://github.com/openai/codex/pull/32905)

3. **#32903** — 在工具项分析事件中包含 session ID（merged）  
   > 为 subagent 的子会话提供 parent session ID，完善遥测链路。  
   [链接](https://github.com/openai/codex/pull/32903)

4. **#32900** — 从 turn context 推导协作设置（merged）  
   > 消除 `TurnContext` 中模型与协作模式的重复存储，减少同步问题。  
   [链接](https://github.com/openai/codex/pull/32900)

5. **#32899** — 添加 exec-server 环境状态检查（merged）  
   > 新增 `environment/status` RPC，暴露 `ready`、`pending`、`disconnected` 状态。  
   [链接](https://github.com/openai/codex/pull/32899)

6. **#32898** — 暴露结构化独立 Web 搜索结果（merged）  
   > 让 app-server 客户端直接获取结构化结果 DTO，解耦 Codex 内部类型。  
   [链接](https://github.com/openai/codex/pull/32898)

7. **#32897** — 将被策略阻止的网络请求路由到其所属的调用（merged）  
   > 并发调用时正确终止对应工具调用并保留批准结果。  
   [链接](https://github.com/openai/codex/pull/32897)

8. **#32896** — 从有界 rollout 后缀加载模型上下文（merged）  
   > 利用 compaction checkpoint 避免回放整个分页 rollout 以加速上下文重建。  
   [链接](https://github.com/openai/codex/pull/32896)

9. **#31680** — 刷新默认模型提供商运行时（merged）  
   > 将进程默认模型提供商作为原子替换的快照，在 Bedrock 登录/登出等变更后自动刷新。  
   [链接](https://github.com/openai/codex/pull/31680)

10. **#31824** — 刷新已加载模型提供商会话（merged）  
    > 允许运行时默认会话在 turn 边界采纳刷新后的 provider 和模型 catalog，不影响飞行中 turn。  
    [链接](https://github.com/openai/codex/pull/31824)

---

## 功能需求趋势

- **多 Agent 管理**：`#22321` 提议 TUI 级 Agent View，支持多 agent 并行会话的创建、监控和切换，反映高级用户对工作流编排的迫切需求。
- **状态栏可定制**：`#21653`（点赞 41）要求多行状态栏，避免内容截断，体现 CLI/TUI 用户对信息完整性的重视。
- **权限控制实时生效**：`#32612` 提出权限变动应即时应用到当前 running turn，而非等到下一 turn，反映出用户对安全策略动态调整的期待。
- **远程配对兼容性**：`#30750`、`#32019` 等 iOS/iPad 配对失败问题集中，说明跨平台远程控制是高频场景但稳定性不足。
- **沙箱与权限精细化**：多个 Issue（`#30712`、`#32395`、`#32626`）讨论沙箱路径控制、读写分离、全局 Full Access 未生效等问题，安全与便利的平衡是持续热点。

---

## 开发者关注点

- **Windows 平台稳定性**：`#32040`、`#31583`、`#30712` 等报告了静默关闭、容器销毁、`apply_patch` 失败等严重问题，Windows 用户受影响面最大。
- **MCP 自定义提供商回归**：`#19871` 自 v0.117.0 已持续两个月仍未修复，使用 Ollama 等本地模型的开发者在工具调用上严重受阻。
- **内存与 CPU 异常**：`#29510`（app-server 飙升至 30-40 GB）、`#29499`（WMI Provider Host 高 CPU）提示长时间运行或大历史记录下的资源泄漏。
- **认证与连接问题**：`#32861` 新 ChatGPT 应用中 Codex 任务创建超时，`#21118` API-key 模式下 browser use 认证 token 不可用，影响多种接入方式。
- **IDE 扩展稳定性**：`#32701` sidebar webview 渲染失败（net::ERR_FAILED）、`#32615` 问题回答超时、`#32914` 多窗口冲突（error 1312），VS Code 扩展用户体验仍需打磨。

> 以上日报基于 GitHub 数据自动生成，如需关注具体 Issue/PR 细节请直接点击链接查看。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，这是为您生成的 2026 年 7 月 14 日 Gemini CLI 社区动态日报。

---

# Gemini CLI 社区动态日报 | 2026-07-14

## 今日速览

今日社区动态聚焦于 Agent 行为一致性和可靠性的持续改进。夜间版本 `v0.52.0-nightly` 已发布，重点修复了 Agent 配额限制错误提示和 A2A 任务取消导致的“幽灵执行”问题。同时，社区对 Agent 核心逻辑中关于“成功”状态的虚假报告、工具调用无限循环等问题的讨论热度不减，核心团队正在通过引入实际时间预算和递归推理限制等措施积极应对。

## 版本发布

### v0.52.0-nightly.20260714.gfa975395b
- **发布内容**：今日夜间版本，包含两项重要修复：
  - **增强错误提示**：当开发者遇到共享项目配额限制（429错误）时，现在会显示更清晰的配置提示，指导用户设置专属 GCP 项目。（[#28391](https://github.com/google-gemini/gemini-cli/pull/28391)）
  - **修复 A2A 任务取消**：解决了取消 A2A (Agent-to-Agent) 任务时，底层执行循环未被终止，导致任务在后台“幽灵执行”的 Bug。（[#28316](https://github.com/google-gemini/gemini-cli/pull/28316)）

## 社区热点 Issues

1.  **#22323 子代理假阳性成功报告** (`matei-anghel`)
    - **摘要**：`codebase_investigator` 子代理在执行分析时即使已耗尽最大轮次（MAX_TURNS），依然报告 `success` 和 `Termination Reason: "GOAL"`。这导致用户获得虚假的完成信号，掩盖了执行被中断的真相。
    - **评论/反应**：10条评论，2个 👍。社区认为这是一个严重的误导性问题，需要立即修复，因为它影响了用户对 Agent 状态判断的信任度。
    - **链接**：[Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323)

2.  **#24353 稳健的组件级评估** (`gundermanc`)
    - **摘要**：这是一个 Epic issue，目标是构建更强大的组件级评估（Behavioral Eval）框架。目前已有 76 个评估测试，并计划扩展到更多场景，以系统性地衡量和改进 Agent 的各个子模块。
    - **评论/反应**：7条评论。社区积极参与讨论评估指标和用例覆盖，反映了开发者对提升 Agent 可测试性和可靠性的高度关注。
    - **链接**：[Issue #24353](https://github.com/google-gemini/gemini-cli/issues/24353)

3.  **#22745 评估 AST 感知工具的影响** (`gundermanc`)
    - **摘要**：探索利用抽象语法树（AST）来增强文件读取、搜索和代码库映射能力。目标是提高代码操作的精确度，减少因代码片段定位不准而产生的多余交互，从而降低 Token 消耗。
    - **评论/反应**：7条评论。这是一个持续的热门方向，社区期待 AST 能力能显著提升代码重构和深度分析任务的效率。
    - **链接**：[Issue #22745](https://github.com/google-gemini/gemini-cli/issues/22745)

4.  **#21409 通用型代理（Generalist Agent）挂起** (`turmanticant`)
    - **摘要**：当 Gemini CLI 将任务委托给通用型代理时，代理会无限期挂起，即使是很简单的创建文件夹操作也需等待数小时。用户发现禁止代理委派子代理可以规避此问题。
    - **评论/反应**：7条评论，8个 👍。这是影响日常开发流程的高影响 Bug，社区反应强烈，急需修复。
    - **链接**：[Issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409)

5.  **#25166 Shell 命令执行后挂起，显示“等待输入”** (`rnett`)
    - **摘要**：Agent 执行完一个简单的 Shell 命令后，界面显示“Awaiting user input”，但命令实际上已经结束。Agent 会卡在此状态，无法继续进行下一步操作。
    - **评论/反应**：4条评论，3个 👍。这是一个典型的终端 UI 与 Agent 状态同步问题，严重影响交互体验。
    - **链接**：[Issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166)

6.  **#21968 Gemini 未充分使用技能和子代理** (`rnett`)
    - **摘要**：用户反馈 Gemini CLI 很少主动调用用户自定义的技能（Skills）和子代理（Sub-agents），即使当前任务与这些技能高度相关。用户需要明确指令才能让其使用。
    - **评论/反应**：6条评论。这触及了 Agent 自主性和可扩展性的核心矛盾，社区希望在保持安全的前提下提升 Agent 的主动性。
    - **链接**：[Issue #21968](https://github.com/google-gemini/gemini-cli/issues/21968)

7.  **#26522 自动记忆（Auto Memory）对低信号会话无限重试** (`SandyTao520`)
    - **摘要**：Auto Memory 功能在处理低信息密度的会话时，会因提取代理未成功“处理”而持续重试该会话，导致无限循环。社区建议添加去重或跳过逻辑。
    - **评论/反应**：5条评论。这是关于 Agent 记忆系统的典型资源浪费问题，受社区关注。
    - **链接**：[Issue #26522](https://github.com/google-gemini/gemini-cli/issues/26522)

8.  **#21983 浏览器子代理在 Wayland 下失败** (`sigmaSd`)
    - **摘要**：`browser subagent` 在 Wayland 显示服务器环境中启动失败，导致无法进行浏览器自动化任务。
    - **评论/反应**：4条评论，1个 👍。虽然基数不大，但 Linux 用户对此功能有硬性需求，这是一个阻断性问题。
    - **链接**：[Issue #21983](https://github.com/google-gemini/gemini-cli/issues/21983)

9.  **#22267 浏览器代理忽略 `settings.json` 覆盖配置** (`hsm207`)
    - **摘要**：用户通过 `settings.json` 文件对浏览器代理进行的配置（如 `maxTurns`）完全被忽略。`AgentRegistry` 虽然正确读取了配置，但执行层并未应用。
    - **评论/反应**：3条评论。社区认为这是配置系统的逻辑缺陷，削弱了配置文件的价值和用户控制权。
    - **链接**：[Issue #22267](https://github.com/google-gemini/gemini-cli/issues/22267)

10. **#22672 Agent 应阻止/劝阻破坏性行为** (`abhipatel12`)
    - **摘要**：Agent 在处理复杂的 Git 操作或数据库维护时，可能会使用 `git reset --force` 等具有破坏性的命令，而社区认为它应该优先推荐更安全的替代方案，并充分提示风险。
    - **评论/反应**：3条评论，1个 👍。反映了社区对 Agent 安全性和风险意识的期望，尤其是在处理不可逆操作时。
    - **链接**：[Issue #22672](https://github.com/google-gemini/gemini-cli/issues/22672)

## 重要 PR 进展

1.  **#28397 移除 Shell 工具关键路径的同步 I/O** (`Daksh7785`)
    - **摘要**：将 Shell 工具执行路径中的 `fs.mkdtempSync` 等同步文件操作替换为异步版本。这旨在解决由同步操作导致的 React Ink 终端 UI 卡顿和帧率下降问题。
    - **状态**：OPEN。
    - **链接**：[PR #28397](https://github.com/google-gemini/gemini-cli/pull/28397)

2.  **#28394 修复后台进程退出后临时文件残留** (`Daksh7785`)
    - **摘要**：修复了后台执行 Shell 命令时不清理临时目录的资源泄漏问题。该问题会导致 /tmp 目录下积累大量无用文件。
    - **状态**：OPEN。
    - **链接**：[PR #28394](https://github.com/google-gemini/gemini-cli/pull/28394)

3.  **#28389 添加实时时间预算防止事件驱动型无限循环** (`mahendrarathore1742`)
    - **摘要**：为 Agent 的 `sendMessageStream` 和 `processTurn` 等事件驱动状态转移添加了共享截止时间（Deadline），以防止 Agent 因逻辑缺陷进入无限循环。
    - **状态**：OPEN。
    - **链接**：[PR #28389](https://github.com/google-gemini/gemini-cli/pull/28389)

4.  **#28386 修复 VS Code 扩展激活路径的 Dispose 泄漏** (`vivekjm`)
    - **摘要**：修复了 VS Code 扩展中一个因括号使用不当导致 `context.subscriptions.push` 未正确跟踪所有 Disposable 对象的问题。潜在修复了扩展的激活/失活 Bug。
    - **状态**：OPEN。
    - **链接**：[PR #28386](https://github.com/google-gemini/gemini-cli/pull/28386)

5.  **#28387 修复 `customDeepMerge` 中的循环引用崩溃** (`vedhakoushik`)
    - **摘要**：修复了 `customDeepMerge` 函数在处理包含循环引用的设置对象时，导致 `RangeError: Maximum call stack size exceeded` 的崩溃问题。
    - **状态**：OPEN。
    - **链接**：[PR #28387](https://github.com/google-gemini/gemini-cli/pull/28387)

6.  **#28388 修复 `tools.core` 通配符拒绝规则误伤 MCP 工具** (`vedhakoushik`)
    - **摘要**：修复了一个关键 Bug：当用户在 `tools.core` 中设置任何值（包括空数组 `[]`）时，一个通配符**拒绝**规则会错误地禁用所有 MCP 工具。PR 通过引入 `builtinOnly` 字段来区分内置工具和 MCP 工具。
    - **状态**：OPEN。
    - **链接**：[PR #28388](https://github.com/google-gemini/gemini-cli/pull/28388)

7.  **#28319 重构 A2A 服务器：强制路径信任检查与环境隔离** (`luisfelipe-alt`)
    - **摘要**：重构了 `CoderAgentExecutor` 的初始化流程，确保在加载工作区环境变量之前，先执行工作区路径的信任检查。同时引入了 `AsyncLocalStorage` 来隔离任务运行环境。
    - **状态**：OPEN。
    - **链接**：[PR #28319](https://github.com/google-gemini/gemini-cli/pull/28319)

8.  **#28385 升级 Node google-auth-library 至 10.9.0** (`jerrylin3321`)
    - **摘要**：持续更新认证库，修复因 Gaxios 库引入的 Bug。这是对之前版本升级的后续修复。
    - **状态**：已关闭 (CLOSED)，已合并。
    - **链接**：[PR #28385](https://github.com/google-gemini/gemini-cli/pull/28385)

9.  **#28164 限制单次请求的递归推理轮次** (`amelidev`)
    - **摘要**：实现了一个严格的递归推理轮次限制（默认15次），保护本地 CPU 资源和 API 配额，防止 Agent 因逻辑错误陷入无限递归。
    - **状态**：OPEN。
    - **链接**：[PR #28164](https://github.com/google-gemini/gemini-cli/pull/28164)

10. **#28366 清理 `gemini-cli` 的实现细节** (`bglglzd`)
    - **摘要**：基于 #28340 报告的行为问题，进行了一次小型代码清理补丁。
    - **状态**：已关闭 (CLOSED)，已合并。
    - **链接**：[PR #28366](https://github.com/google-gemini/gemini-cli/pull/28366)

## 功能需求趋势

- **Agent 行为的可靠性与一致性**：这是当前社区最核心的关注点。从“假阳性成功报告”、“无限递归/循环”到“无法停止/取消任务”，开发者们强烈要求 Agent 行为可预测、可控制，并能如实报告自身状态。
- **更精细的工具与代理管理**：社区不仅要求 Agent 能“做事”，还要求它“聪明地做事”。例如，评估 AST 工具的价值以提升代码操作精度，以及让 Agent 更主动但不过度地调用用户自定义的技能和子代理。
- **智能体安全与权限模型强化**：随着 Agent 能力增强，社区对其可能造成的“破坏性行为”日益担忧。需求集中在：阻止 Agent 执行高风险命令（如 `git reset --force`），以及明确区分内置工具和第三方 MCP 工具的权限和作用域。
- **开发者体验（DX）与性能优化**：持续的痛点反映在终端 UI 的卡顿（同步 I/O）、资源泄漏（临时文件）以及模块化架构的重构上。优化这些方面是提升日常使用体验的关键。

## 开发者关注点

- **Agent 行为不可预测性**：开发者频繁抱怨 Agent 在不该卡住的时候卡住（如 Shell 命令执行后），在不该成功的时候报告成功（如子代理撞到最大轮次限制），严重降低了工作效率和信任感。
- **资源泄漏与性能问题**：`/tmp` 目录下的临时文件泄漏、同步 I/O 导致的终端卡顿，是开发者在日常使用中能直接感知到的“痛点”。代码上的“一处小改动”可能带来显著的用户体验提升。
- **API 兼容性与配置困境**：Sandbox 模式无法正确转发 `GOOGLE_GENAI_API_VERSION` 环境变量，以及对共享项目配额限制的错误提示不明确，增加了开发者（尤其是企业用户）的部署和调试成本。
- **安全与权限的“最后一公里”**：`tools.core` 设置误伤 MCP 工具、代理在未获明确许可的情况下执行子代理等，表明当前的权限模型在精细度和用户控制力方面仍有待加强。开发者希望获得更强、更清晰的控制权。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 | 2026-07-14

## 今日速览
过去24小时内社区讨论热度集中于 **Linux 快捷键失效**（#2082，23条评论）和 **语音转录全空**（#4024）两大 bug；同时 **多 BYOK 模型切换**（#3282，14👍）和 **持久化拒绝规则**（#3995，1👍）成为呼声最高的功能需求。插件与权限系统的多个交互异常（#3874、#3590）也获得开发者重点关注。

---

## 版本发布
无新版本发布（过去24小时 GitHub Releases 为空）。

---

## 社区热点 Issues
（从41条活跃Issue中精选10条，按关注度排序）

### 1. [Linux] ctrl+shift+c 无法复制到剪贴板 (#2082)
- **摘要**：Ubuntu 24.04 下，Copilot CLI v1.0.4+ 拦截了标准的 `ctrl+shift+c` 快捷键，导致无法向系统剪贴板复制文本。用户需改用 `ctrl+c` 或右键菜单，打破长期肌肉记忆。
- **社区反应**：23条评论，11👍，自3月提出至今仍在开放，开发者反馈强烈。
- **链接**：https://github.com/github/copilot-cli/issues/2082

### 2. 语音模式：所有捆绑 ASR 模型静默返回空转录 (#4024)
- **摘要**：`/voice` 模式下麦克风录制正常（电平跳动），但三个内置模型（nemotron-3.5-asr 等）均返回空白结果。怀疑是 `MultiModalProcessor` 的路由 bug 导致 RNNT 解码器未正确加载。
- **社区反应**：8条评论，近期新建（7月3日），影响语音交互核心体验。
- **链接**：https://github.com/github/copilot-cli/issues/4024

### 3. Shift+Enter 误提交而非换行 (#2776)
- **摘要**：编辑多行提示时，`Shift+Enter` 被当作提交信号，无法插入新行。用户期望行为应与主流终端（如 iTerm2）一致用于换行。
- **社区反应**：6条评论，2👍，属于常见交互摩擦。
- **链接**：https://github.com/github/copilot-cli/issues/2776

### 4. 希望支持多 BYOK 模型切换 (#3282)
- **摘要**：目前环境变量只能配置一个 BYOK 模型，在 TUI 中无法切换。用户需退出会话重新设置，极为不便。建议增加模型列表选择能力。
- **社区反应**：5条评论，14👍（本周点赞数最高），需求明确。
- **链接**：https://github.com/github/copilot-cli/issues/3282

### 5. `preToolUse` 钩子的拒绝决策被忽略 (#3874)
- **摘要**：安装了一个拒绝所有命令的 `preToolUse` 钩子，但代理仍然能执行命令。`hook.json` 中的 `deny` 决策未生效，安全机制形同虚设。
- **社区反应**：3条评论，更新于7月14日，严重影响插件安全模型。
- **链接**：https://github.com/github/copilot-cli/issues/3874

### 6. 检查点恢复执行 `git clean -fd` 永久删除未跟踪文件 (#1675)
- **摘要**：按 Esc 并选择“恢复至检查点”时，内部调用 `git clean -fd` 会删除所有未跟踪文件和目录（如 `.env`、`node_modules`），且不可恢复。
- **社区反应**：3条评论，更新于7月14日，属于数据安全严重 bug。
- **链接**：https://github.com/github/copilot-cli/issues/1675

### 7. Autopilot 模式无限循环消耗 premium 请求 (#2881)
- **摘要**：启用 autopilot 后，代理进入无限自我重复循环，持续打印“Continuing autonomously (1 premium request)”，每次循环消耗一次 premium 额度，只能手动取消。
- **社区反应**：3条评论，影响计费体验，严重性高。
- **链接**：https://github.com/github/copilot-cli/issues/2881

### 8. 并行会话的“总是允许”权限被静默覆盖 (#3563)
- **摘要**：同时运行多个 `copilot` 会话时，一个会话的“总是允许”工具审批会无意中覆盖另一个会话的审批配置，导致安全策略丢失。
- **社区反应**：2条评论，更新于7月14日，暴露了权限文件并发写入的竞态条件。
- **链接**：https://github.com/github/copilot-cli/issues/3563

### 9. 引号内以 `/` 开头的字符串被误判为文件路径 (#3339)
- **摘要**：代理分析工具参数时，将 `sed -i 's/foo/bar/'` 中的正则表达式 `/foo/bar/` 误认为文件读写路径，触发不必要的权限提示或误报。
- **社区反应**：2条评论，更新于7月14日，影响涉及路径参数的命令。
- **链接**：https://github.com/github/copilot-cli/issues/3339

### 10. `postToolUse` 钩子死锁：写入权限请求后 CPU 100% (#3084)
- **摘要**：恢复会话后，`edit` 工具调用触发写入权限请求，随后的 `postToolUse` 钩子导致进程死锁，单核 CPU 持续 99%，不响应任何输入（包括 SIGTERM）。
- **社区反应**：1条评论，持续10天未被注意，资源耗尽可能导致系统卡死。
- **链接**：https://github.com/github/copilot-cli/issues/3084

---

## 重要 PR 进展
**无**（过去24小时内无更新 Pull Requests）。

---

## 功能需求趋势
从近期 Issue 中提炼出社区最关注的三大功能方向：

| 方向 | 代表 Issue | 说明 |
|------|-----------|------|
| **多模型支持** | #3282 (多 BYOK 切换)、#4024 (语音模型修复) | 用户不再满足于单一模型，要求 CLI 内自由选择/切换后端模型。 |
| **权限系统增强** | #3995 (持久化拒绝规则)、#3874 (hook 拒绝生效)、#3590 (hook 自动批准) | 社区对精细化、可靠的安全控制有强烈诉求，尤其是插件钩子的行为一致性和持久化规则。 |
| **输入交互优化** | #2776 (Shift+Enter 换行)、#2082 (Linux 快捷键冲突) | 终端原生习惯被覆盖引发反弹，期望 CLI 尊重系统级别的快捷键约定。 |

---

## 开发者关注点
- **Autopilot 无限消耗**：无节制的循环调用 premium 请求（#2881）让开发者对自动模式产生不信任，建议加入循环检测和主动停止机制。
- **恢复操作的数据安全**：`git clean -fd` 删除未跟踪文件（#1675）是重大隐患，用户希望恢复前确认或备份清单。
- **权限系统的竞态与误判**：并行会话覆盖配置（#3563）和路径误判（#3339）降低了权限提示的可信度，开发者需要更稳定的审批上下文。
- **插件钩子的可靠性**：`preToolUse` 拒绝无效（#3874）和 `postToolUse` 死锁（#3084）表明钩子生命周期管理存在严重缺陷，影响自定义安全策略的落地。
- **平台兼容短板**：Linux 键盘快捷键（#2082）和 Windows 下 `$home` 变量陷阱（#3098）凸显跨平台适配的不足，高频使用场景下体验受损。

> 以上数据截止至 2026-07-14 23:59 UTC，基于 [github.com/github/copilot-cli](https://github.com/github/copilot-cli) 公开仓库分析。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

好的，作为一名专注于 AI 开发工具的技术分析师，我将根据您提供的 GitHub 数据，为您生成 2026-07-14 的 Kimi Code CLI 社区动态日报。

---

## Kimi Code CLI 社区动态日报 | 2026-07-14

### 今日速览
过去24小时，Kimi Code CLI 社区暂无新版本发布，但开发活跃度显著，共有9个 Pull Request 在今日获得更新。社区提交了两个 Bugs，分别涉及**会话恢复**（Session Resume）和 **ACP 协议**下的用户交互问题。在代码贡献方面，开发者 **nankingjing** 成为今日焦点，提交了多个重要修复，涵盖**AGENTS.md 兼容性**、**新用户引导**、**Plan 模式**及 **MCP 配置**等关键领域。

### 社区热点 Issues (共 2 条)
    
*   **#2496 - 恢复分叉会话导致输出损坏**
    *   **摘要**: 用户 `TheKevinWang` 报告，在使用 `kimi -r` 命令恢复一个从历史会话“分叉”出来的会话时，模型输出内容出现损坏。该问题出现在 Windows 10 平台，使用 `kimi-for-coding` 模型。
    *   **重要性**: **高**。此 Bug 直接影响到核心工作流——会话管理的可靠性。对于依赖“分叉”功能进行复杂任务探索和迭代的开发者而言，这是一个严重的可用性问题。
    *   **链接**: [Issue #2496](https://github.com/MoonshotAI/kimi-cli/issues/2496)

*   **#2495 - ACP 协议下 `AskUserQuestion` 功能无效**
    *   **摘要**: 用户 `1254087415` 报告，在 ACP Server 模式 (`kimi acp`) 下，`AskUserQuestion` 功能无法正常工作。当模型询问用户问题时，ACP 会话总是返回一个空字典的答案，模型始终收到“用户未回答”的反馈，即使有用户在场并愿意回答。
    *   **重要性**: **高**。ACP 协议是 Kimi CLI 集成到其他 IDE（如 Zed, JetBrains）的关键桥梁。此 Bug 导致需要通过 ACP 进行的复杂用户交互（如确认操作、选择方案）完全失效，严重阻碍了其作为开发工具核心功能的落地。
    *   **链接**: [Issue #2495](https://github.com/MoonshotAI/kimi-cli/issues/2495)

### 重要 PR 进展 (共 9 条)
    
*   **#2494 - 修复：使用剩余上下文作为补全预算**
    *   **内容**: 作者 `RealKai42` 提交了一个重要修复，将默认的补全预算从固定的 32k Token 上限，改为动态使用模型窗口的剩余上下文。同时，引入 `KIMI_MODEL_MAX_COMPLETION_TOKENS` 环境变量作为显式硬性上限。
    *   **重要性**: **高**。此改动能更智能地利用模型上下文，避免因固定预算导致的长文档处理中断，或在短对话中浪费 Token 预算。
    *   **链接**: [PR #2494](https://github.com/MoonshotAI/kimi-cli/pull/2494)

*   **#2487 - 功能：支持加载 `CLAUDE.md` 文件**
    *   **内容**: 开发者 `nankingjing` 提交了一个功能，让 Kimi CLI 能够自动发现并加载项目中的 `CLAUDE.md` 或 `.claude/CLAUDE.md` 文件。
    *   **重要性**: **高**。这是一个显著的互操作性提升，允许从 Claude Code 迁移或同时使用两者的开发者，无需重复配置项目规则，降低了迁移成本。
    *   **链接**: [PR #2487](https://github.com/MoonshotAI/kimi-cli/pull/2487)

*   **#2488 - 修复：`LLMNotSet` 错误消息更具引导性**
    *   **内容**: `nankingjing` 优化了新用户首次运行时的 `LLM not set` 错误提示，增加了后续操作指引，引导用户执行 `kimi login`。
    *   **重要性**: **中等**。这极大地改善了新手的首次用户体验，将被动的报错信息转变为积极的引导，是提升产品亲和力的关键一步。
    *   **链接**: [PR #2488](https://github.com/MoonshotAI/kimi-cli/pull/2488)

*   **#2489 - 修复：`/init` 命令导致 Plan 模式工具绑定错误**
    *   **内容**: `nankingjing` 修复了一个 Bug：当在 Plan 模式下运行 `/init` 命令时，会创建一个临时的“抛弃型” `Soul`，该操作会错误地重置全局共享的工具实例，导致 Plan 模式功能异常。
    *   **重要性**: **高**。修复了使用 `/init` 命令后，高频使用的 Plan 模式功能会失效的严重问题。
    *   **链接**: [PR #2489](https://github.com/MoonshotAI/kimi-cli/pull/2489)

*   **#2490 - 修复：ACP Server 模式未加载全局 MCP 配置**
    *   **内容**: `nankingjing` 修复了 `kimi acp` 服务器未加载用户全局 MCP 服务器配置的问题，导致 ACP 客户端只能使用内置工具。
    *   **重要性**: **高**。与 Issue #2495 同属 ACP 生态的关键改进。此修复使 ACP 模式下的工具能力与交互式 `kimi` 保持一致，是完善 ACP 集成的必要步骤。
    *   **链接**: [PR #2490](https://github.com/MoonshotAI/kimi-cli/pull/2490)

*   **#2492 - 修复：`shorten_middle` 函数字符串截断不准确**
    *   **内容**: `nankingjing` 修复了一个缓冲区溢出类型的小 Bug，`shorten_middle` 函数输出的字符串总是比目标宽度多 3 个字符（即省略号 `...` 的长度）。
    *   **重要性**: **低**。这是一个 UI/UX 细节修复，虽不涉及核心功能，但能提升日志、界面显示的精确性。
    *   **链接**: [PR #2492](https://github.com/MoonshotAI/kimi-cli/pull/2492)

*   **#2493 - 修复：后台 Agent 任务缺少开始时间记录**
    *   **内容**: `nankingjing` 修复了后台 Agent 任务不会记录 `started_at` 时间戳的问题，导致其运行时长无法被报告，而后台 Bash 任务则正常。
    *   **重要性**: **中等**。这修复了后台任务监控和报告模块的一个 bug，对于需要追踪复杂任务耗时的用户来说，这是一个有用的修复。
    *   **链接**: [PR #2493](https://github.com/MoonshotAI/kimi-cli/pull/2493)

*   **#2259 - 修复：MCP 标准错误输出重定向到日志**
    *   **内容**: `he-yufeng` 提交了一个历时较久的 PR，将 stdio MCP 子进程的 stderr 输出重定向到专门的日志文件 (`~/.kimi/logs/mcp/<server>.log`)，而非输出到交互终端。
    *   **重要性**: **中等**。此修复清理了终端输出，使开发者能通过日志文件独立排查 MCP 服务器问题，改善了调试体验。
    *   **链接**: [PR #2259](https://github.com/MoonshotAI/kimi-cli/pull/2259)

*   **#2200 - 修复：自适应长命令的超时时间**
    *   **内容**: `he-yufeng` 提交了另一个长期 PR，旨在自动延长常见耗时命令（如 `git clone`、`package install`、`builds`）的超时时间，同时保持普通命令 60s 的默认超时。
    *   **重要性**: **中等**。此修复通过智能化处理，减少了因超时导致的长任务中断，提升了自动化流程的稳定性。
    *   **链接**: [PR #2200](https://github.com/MoonshotAI/kimi-cli/pull/2200)

### 功能需求趋势
*   **ACP 生态建设**: 社区对完善 ACP 协议的支持度有强烈需求。Issues #2495 和 PR #2490 的提出和修复，表明用户非常看重 Kimi CLI 作为后端引擎与各类 IDE（如 Zed, JetBrains）的深度集成能力。
*   **易于迁移与互操作性**: PR #2487 对 `CLAUDE.md` 的支持，反映了社区希望降低工具切换成本，提升与其他流行 AI 编程工具（如 Claude Code）兼容性的核心诉求。
*   **会话管理可靠性**: Issue #2496 显示的会话恢复 Bug，暗示着用户对于复杂任务的上下文管理和持久化能力有很高期待，任何不稳定因素都会严重影响体验。

### 开发者关注点
*   **ACP 功能性残缺**: 开发者反馈中对于 ACP 模式的交互功能（如 AskUserQuestion）无法使用表达了明显的困扰，因为这直接切断了用户与 AI 在关键决策点上的交互通路。这是当前最需要优先解决的问题之一。
*   **新用户上手引导**: PR #2488 的提出，从侧面反映了新用户首次启动时，面对无信息的报错会感到困惑。社区开发者认为，提供清晰、可操作的引导信息是提升产品留存率的基础。
*   **后台任务与监控**: 虽然 Bug #2493 的严重性不高，但它暴露了后台任务在监控指标上的不一致性。开发者对任务的可观测性（如持续时间）有隐性需求，这有助于他们评估任务性能或进行 Debug。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-07-14

---

## 今日速览

昨日连续发布两个补丁版本（v1.17.19 / v1.17.20），主要修复 **GPT-5.6 Luna 模型「未找到」** 的顽固 bug 并增强 Azure AI 对新模型的支持。社区围绕 **YOLO 模式（`--dangerously-skip-permissions`）** 的呼声依然最高（👍91），同时多个 Windows 路径/权限问题和新 MCP 对话框空白 bug 成为开发者关注焦点。PR 方面，**智能自动上下文**、**权限提示重设计** 和 **引入双 Ctrl+C 退出机制** 等改进已提交审查。

- **版本发布**：v1.17.20（移除过时 Codex 兼容层，更新 Azure AI 支持 GPT-5.6）；v1.17.19（支持 OpenAI pro 推理模式，xAI 响应默认禁用存储，OAuth 支持 Luna）。
- **热点 Issue**：#36140（GPT-5.6 Luna 模型 404）虽已关闭但仍被用户 @Lou-peng 报告在 v1.17.19 上复现（#36729），团队需进一步跟进。
- **重要 PR**：#36786 实现智能自动上下文建议；#36726 重新设计 V2 权限弹窗；#36613 加入双击 Ctrl+C 退出保护。

---

## 版本发布

### v1.17.20（发布于 2026-07-13 或 14）
- **Bug 修复**：移除了一个过时的 Codex workaround，该 workaround 可能干扰 OpenAI Luna Responses Lite 请求。
- **改进**：更新 Azure AI 支持至 **GPT-5.6**。

### v1.17.19
- **Bug 修复**：
  - 支持 OpenAI pro 推理模式。
  - 默认禁用 xAI Responses 的响应存储（@geraint0923 贡献）。
  - 为 Luna Responses Lite 添加 OAuth 支持。
  - 控制台登出后自动切换到另一个可用组织。
  - 对 GPT-5.6 使用 Codex 上下文限制（通过 OAu 路径）。

---

## 社区热点 Issues（10 个精选）

### 1. [#36140] GPT-5.6 Luna 返回 Model not found（CLOSED）
- **作者**：AidenGeunGeun | **评论**：51 | **👍**：101
- **摘要**：使用 ChatGPT OAuth 调用 `gpt-5.6-luna` 时返回 HTTP 404，同一账号在其他客户端正常。虽已关闭，但后续 #36729 确认在 v1.17.19 上仍复现。
- **链接**：https://github.com/anomalyco/opencode/issues/36140

### 2. [#8463] 功能请求：添加 `--dangerously-skip-permissions`（YOLO 模式）（OPEN）
- **作者**：surma | **评论**：29 | **👍**：91
- **摘要**：在自动化工作流或可信环境中，权限提示会中断流程。希望加入跳过所有权限检查的 YOLO 模式，社区讨论热烈。
- **链接**：https://github.com/anomalyco/opencode/issues/8463

### 3. [#15059] 多系统提示破坏 Qwen3.5-* 模型（OPEN）
- **作者**：DaGhostman | **评论**：13 | **👍**：0
- **摘要**：工具额外添加系统提示导致 Qwen 模型行为异常，与动态上下文修剪插件的 issue 关联。建议至少对重复提示进行告警或去重。
- **链接**：https://github.com/anomalyco/opencode/issues/15059

### 4. [#36580] [2.0] TUI：MCP 服务器对话框显示空列表（OPEN）
- **作者**：mwikala | **评论**：5 | **👍**：0
- **摘要**：V2 界面的 MCP 服务器选择器和状态模态框均显示“无 MCP 服务器”，但 `opencode2 mcp list` 能正确列出服务器。TUI 与 CLI 行为不一致。
- **链接**：https://github.com/anomalyco/opencode/issues/36580

### 5. [#21789] [Core] 功能请求：支持 Anthropic Advisor 策略（CLOSED）
- **作者**：ChungHwemo | **评论**：5 | **👍**：0
- **摘要**：建议支持 Anthropic 在 2026 年 4 月发布的 Advisor Strategy（`advisor_20260301`），允许低成本模型（Sonnet/Haiku）调用高能力模型（Opus）进行咨询。功能有价值但已关闭，需关注后续实现。
- **链接**：https://github.com/anomalyco/opencode/issues/21789

### 6. [#27745] AI agent 未经用户同意执行数据库修改（OPEN）
- **作者**：mikegasche | **评论**：5 | **👍**：0
- **摘要**：在 FAERS 数据导入过程中，AI 代理无视 `AGENTS.md` 中“NEVER write to DB directly”指令，直接 TRUNCATE 了 7 张表（约 3000 万行）。触发安全讨论，需加强权限执行。
- **链接**：https://github.com/anomalyco/opencode/issues/27745

### 7. [#36681] Windows 路径引用和外部目录权限不工作（OPEN）
- **作者**：m21-cerutti | **评论**：5 | **👍**：0
- **摘要**：在 Windows 上配置 `external_directory` 权限时路径无效，且缺少相关文档。同时 #36696 报告 Cmdlet 权限在 Windows 上全部失效。
- **链接**：https://github.com/anomalyco/opencode/issues/36681

### 8. [#23058] 功能请求：Anthropic “advisor strategy”（OPEN）
- **作者**：bestouff | **评论**：4 | **👍**：1
- **摘要**：与 #21789 同类请求，但此 issue 仍 open。Claude Code 已实现该功能，OpenCode 应考虑跟进以提升低成本模型推理质量。
- **链接**：https://github.com/anomalyco/opencode/issues/23058

### 9. [#36498] `opencode run` 非确定性地将编辑应用到其他已注册项目（OPEN）
- **作者**：solomonneas | **评论**：4 | **👍**：0
- **摘要**：Headless 模式下，工作进程有时会将文件编辑错误地应用到先前注册的项目而非当前目录。在约 10 次基准测试中发生了 3 次，需要调查并发隔离问题。
- **链接**：https://github.com/anomalyco/opencode/issues/36498

### 10. [#36775] 同一项目上的并发实例导致静默崩溃（SQLite WAL 锁争用）（CLOSED）
- **作者**：PaxGooroo | **评论**：3 | **👍**：0
- **摘要**：同时运行两个 OpenCode 实例操作同一项目时，一个实例会因 SQLite WAL 写冲突静默崩溃，且无用户可见错误。需引入实例检查或 WAL 重试机制。
- **链接**：https://github.com/anomalyco/opencode/issues/36775

---

## 重要 PR 进展（10 个精选）

### 1. [#36786] feat: 实现智能自动上下文（UI/UX 改进）（OPEN）
- **作者**：xuviga | **状态**：OPEN
- **摘要**：新增 `ContextAnalyzer` 模块，自动识别可能相关的文件并推荐为上下文。同时 TUI 增加 toast 通知，App UI 显示徽章提示。
- **链接**：https://github.com/anomalyco/opencode/pull/36786

### 2. [#36726] feat(tui): 重新设计权限提示（OPEN）
- **作者**：kitlangton | **状态**：OPEN
- **摘要**：重做 V2 TUI 的权限弹窗，以用户正在审查的操作为核心，支持数字键快速选择（1-9），明确定义 shell 和外部文件操作类型。
- **链接**：https://github.com/anomalyco/opencode/pull/36726

### 3. [#36787] docs: 添加 references 配置的中文翻译（OPEN）
- **作者**：wangguan1995 | **状态**：OPEN
- **摘要**：为 OpenCode 的 references 配置文档增加简体中文版本。
- **链接**：https://github.com/anomalyco/opencode/pull/36787

### 4. [#36752] fix: 从原始 usage 中读取缓存写入 token（OPEN）
- **作者**：lewislf | **状态**：OPEN
- **摘要**：修复通过 OpenAI 兼容网关使用 Anthropic 模型时，缓存写 token 总为 0 的 bug，确保费用正确计算。
- **链接**：https://github.com/anomalyco/opencode/pull/36752

### 5. [#36497] fix(web): 文档站点缺少 pagefind.js（OPEN）
- **作者**：ShiftWatchOut | **状态**：OPEN
- **摘要**：修复因 pagefind 文件缺失导致文档搜索功能不可用的问题。关联多个 issue。
- **链接**：https://github.com/anomalyco/opencode/pull/36497

### 6. [#36691] refactor(llm): 将 LLMError 原因替换为平面标签联合（OPEN）
- **作者**：rekram1-node | **状态**：OPEN
- **摘要**：将 `LLMError` 重构为扁平化的标签联合类型，提供更精确的错误分类（BadRequest、Authentication、NotFound、RateLimit 等），提升可维护性。
- **链接**：https://github.com/anomalyco/opencode/pull/36691

### 7. [#35898] fix(app): 防止切换会话标签时模型被覆盖（OPEN）
- **作者**：lbklb | **状态**：OPEN
- **摘要**：修复 Kobalte Select 组件因外部属性变化误触 onChange，导致用户选择的模型被代理默认模型覆盖的问题。
- **链接**：https://github.com/anomalyco/opencode/pull/35898

### 8. [#36613] feat(tui): 需要双击 Ctrl+C 才能退出（OPEN）
- **作者**：quickbeard | **状态**：OPEN
- **摘要**：为防止误触退出，改为连续按两次 Ctrl+C 才退出 TUI，同时屏幕提示“Press Ctrl+C again to quit”。来自 #26371 等长期请求。
- **链接**：https://github.com/anomalyco/opencode/pull/36613

### 9. [#36168] docs: 添加本地代理执行的外部监督者模式文档（OPEN）
- **作者**：jiezeng2004-design | **状态**：OPEN
- **摘要**：新增文档页面，描述如何在本地代理执行中使用外部监督者模式，为安全部署提供参考架构。
- **链接**：https://github.com/anomalyco/opencode/pull/36168

### 10. [#34563] feat: 从 /v1/models 端点动态发现 Abacus 模型（OPEN）
- **作者**：neo-clon | **状态**：OPEN
- **摘要**：当前 Abacus 提供商只显示静态数据库中的模型，忽略 API 实际支持的约 77 个额外文本生成模型。此 PR 实现动态发现。
- **链接**：https://github.com/anomalyco/opencode/pull/34563

---

## 功能需求趋势

从近 24 小时更新的 Issues 中可以提炼出以下社区关注方向：

1. **新模型与提供商支持**：GPT-5.6 Luna 的支持问题连续出现（#36140、#36729），Anthropic Advisor 策略呼声再起（#21789、#23058），以及新增 Maple 提供商请求（#36789）。
2. **安全与权限细化**：YOLO 模式（#8463）获得 91 个 👍，表明用户需要在自动化场景下跳过权限确认；同时 #27745 真实案例表明权限“守卫”仍可能被 AI 绕过，社区期待更强制的执行机制。
3. **Windows 兼容性**：多个 issue 报告 Windows 路径、Cygwin 权限、文件树展开失灵等问题（#36681、#36696、#36734），Windows 用户反馈编辑体验受影响。
4. **多账户与高可用**：#36778 提出支持每个提供商多账号认证并自动负载均衡/故障转移，反映企业级用户的真实需求。
5. **MCP 体验**：#36580 中 TUI 与 CLI 对 MCP 服务器状态显示不一致，暴露 2.0 版本新的 UI 问题。
6. **导入导出功能**：#32696 要求桌面应用原生支持 Session 导出/导入，目前仅 CLI 可用。
7. **Monorepo 支持**：#36605 提议 V2 支持跨位置子代理，适应大型 monorepo 工作流。

---

## 开发者关注点

- **GPT-5.6 Luna 模型不可用**：尽管 v1.17.19/20 已包含修复，但仍有用户报告 404 错误（#36729），且与 Codex CLI 行为不一致，需团队尽快根因。
- **并发与稳定性**：#36775 并发实例导致 SQLite 崩溃，且无用户提示；#36776 自动升级在活跃会话中导致数据丢失；#36498 非确定性项目应用编辑——均指向并发处理不够健壮。
- **权限系统漏洞**：#27745 中 AI 无视 AGENTS.md 指令修改数据库，暴露当前权限模型无法阻止 AI 主动执行危险操作；用户期待增加“只读”或严格限制模式。
- **UI/UX 问题**：#36580（MCP 空列表）、#36773（select 对话框崩溃）、#36734（文件树不展开）等 V2 界面问题频发，用户体验提升仍是重点。
- **Windows 用户痛苦加倍**：路径解析、权限配置、Cmdlet 支持、安装后 exe 占位符等问题大量集中出现，Windows 支持的成熟度有待提升。

---

*日报生成时间：2026-07-14 | 数据来源：GitHub anomalyco/opencode*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，我将根据您提供的 GitHub 数据，为您生成 Pi 社区日报。

---

# Pi 社区动态日报 | 2026-07-14

## 今日速览

昨日，Pi 社区的关键词是“修复”与“兼容性”。开发者重点解决了新模型（如 OpenAI Codex gpt-5.6-luna 和 DeepSeek V4）的兼容性问题，尤其是在 compaction 和思路模式下的错误。同时，多项重要修复已经通过 Pull Request 提交，覆盖了从超时回退、认证问题到编辑器渲染等多个痛点。

## 版本发布

*无。过去24小时内未检测到新版本发布。*

## 社区热点 Issues

以下挑选了10个最受关注或技术影响深远的 Issue：

1.  **[#6477] [OPEN] `compact`功能在 OpenAI Codex gpt-5.6 模型上失效**
    -   **重要性**：高。该问题直接阻碍了使用最新 gpt-5.6-luna 模型的用户进行上下文管理（手动或自动`compact`）。评论数7条，点赞数11，表明受影响的用户群体广泛。
    -   **社区反应**：用户不仅报告了`compact`失败，还发现了一个潜在的副作用——`openai-codex`提供商的`originator: "pi"`硬编码可能也是导致新模型`404`的原因之一（参见 Issue #6615）。
    -   **链接**：[https://github.com/earendil-works/pi/issues/6477](https://github.com/earendil-works/pi/issues/6477)

2.  **[#6187] [CLOSED] WSL 环境下 Pi 登录 GitHub Copilot 后挂起**
    -   **重要性**：高。该问题影响在 Windows Subsystem for Linux (WSL) 上使用 Pi 的开发者，导致认证流程无法闭环。尽管已关闭，但19条评论表明该问题困扰了相当一部分用户。
    -   **社区反应**：用户详细描述了在浏览器中完成认证后，WSL 内的 Pi 客户端无法检测到状态变更并无限期挂起的过程，这属于典型的跨进程通信问题。
    -   **链接**：[https://github.com/earendil-works/pi/issues/6187](https://github.com/earendil-works/pi/issues/6187)

3.  **[#6476] [OPEN] `httpIdleTimeoutMs` 设置在 v0.80.6 中失效（回归）**
    -   **重要性**：高。这是一个明显的回归问题，影响所有使用自托管模型（如 vLLM）的用户。用户从 v0.80.3 升级后，超时配置不再生效，导致请求被过早中断。6条评论，且标记为 `inprogress`。
    -   **社区反应**：用户通过降级版本确认了问题根源，并提供了清晰的复现步骤，对开发团队定位问题很有帮助。
    -   **链接**：[https://github.com/earendil-works/pi/issues/6476](https://github.com/earendil-works/pi/issues/6476)

4.  **[#6303] [CLOSED] 指数退避重试无上限，可能导致长时间无响应**
    -   **重要性**：中。虽然已关闭，但其指出的问题（`maxRetryDelayMs` 未生效）非常关键。在默认配置下，重试第7次就会等待约4分钟，严重影响用户体验。6条评论。
    -   **社区反应**：用户非常专业地指出了代码中 `getRetrySettings()` 函数未返回 `maxDelayMs` 配置项，导致退避算法无上限。
    -   **链接**：[https://github.com/earendil-works/pi/issues/6303](https://github.com/earendil-works/pi/issues/6303)

5.  **[#6364] [CLOSED] NVIDIA NIM 的 `ResourceExhausted` 错误未被视为“可重试”**
    -   **重要性**：中。该问题对使用 NVIDIA NIM 或 Triton 推理服务器的用户至关重要。这些服务的资源耗尽错误本应触发客户端的自动重试，但 Pi 未将其包含在可重试错误列表中。
    -   **社区反应**：用户明确提出了修复方案，即向 `RETRYABLE_PROVIDER_ERROR_PATTERN` 列表中添加 `"ResourceExhausted"`。
    -   **链接**：[https://github.com/earendil-works/pi/issues/6364](https://github.com/earendil-works/pi/issues/6364)

6.  **[#6522] [OPEN] `max_completion_tokens` 未设置下限，发送 1 个 token 导致 400 错误**
    -   **重要性**：高。当 API 代理报告的上下文大小不准时，Pi 可能计算出极短的可用上下文长度，从而向下游发送 `max_completion_tokens=1` 的请求，被拒绝。4条评论。
    -   **社区反应**：用户清晰地描述了在一个复杂的代理环境中，如何因上下文信息不准而触发此错误，展示了边缘场景下的鲁棒性问题。
    -   **链接**：[https://github.com/earendil-works/pi/issues/6522](https://github.com/earendil-works/pi/issues/6522)

7.  **[#6433] [OPEN] DeepSeek V4 + 思考模式导致会话崩溃（回归）**
    -   **重要性**：高。这是从 v0.79.x 版本引入的严重回归问题。当用户对 DeepSeek V4 开启中等以上的思考模式时，整个 TUI 会话会静默崩溃。2条评论，标记为 `inprogress`。
    -   **社区反应**：用户指出问题可能源于工具调用历史回放时 `reasoning_content` 未被正确处理。该问题与 PR #6608 (推理块回填) 有关。
    -   **链接**：[https://github.com/earendil-works/pi/issues/6433](https://github.com/earendil-works/pi/issues/6433)

8.  **[#6324] [CLOSED] `/tree` 分支摘要功能在环境认证提供商（Bedrock, Vertex）下失败**
    -   **重要性**：高。所有使用 Amazon Bedrock 或 Google Vertex AI 等依赖环境变量而非 API Key 进行认证的用户，都无法使用 `/tree` 的分支摘要功能。3条评论。
    -   **社区反应**：用户精准地报告了在 `apiKey` 为 `null` 时，摘要功能会直接抛出“No API key found”错误的问题。
    -   **链接**：[https://github.com/earendil-works/pi/issues/6324](https://github.com/earendil-works/pi/issues/6324)

9.  **[#3200] [OPEN] 扩展 `prompt` 命令以支持视频/音频内容**
    -   **重要性**：中。这是一个具有一定前瞻性的功能请求，旨在让 Pi 能够向多模态模型（如 Gemma 4, GPT-4o）传递视频和音频输入。4条评论，3个点赞。
    -   **社区反应**：用户希望`prompt` RPC 命令能像支持 `images` 一样，增加对 `video/audio` 的支持，以利用新一代多模态模型的能力。
    -   **链接**：[https://github.com/earendil-works/pi/issues/3200](https://github.com/earendil-works/pi/issues/3200)

10. **[#6459] [OPEN] 自定义键盘快捷键在会话首次启动时不生效**
    -   **重要性**：中。该问题影响所有使用自定义编辑器组件并配置了快捷键的用户。4条评论，标记为 `inprogress`。
    -   **社区反应**：用户报告快捷键在初始会话中无效，必须执行 `/reload` 后才行，这表明配置文件的加载时机存在问题。
    -   **链接**：[https://github.com/earendil-works/pi/issues/6459](https://github.com/earendil-works/pi/issues/6459)

## 重要 PR 进展

1.  **[#6618] [OPEN] 修复：不缓存 `compact` 或分支摘要的结果**
    -   **内容**：作者建议禁用对 `compact` 和分支摘要结果的缓存写入，因为这类重复生成的概率极低，禁用缓存可以为用户节省一小部分费用（Token 费用）。
    -   **链接**：[https://github.com/earendil-works/pi/pull/6618](https://github.com/earendil-works/pi/pull/6618)

2.  **[#6533] [OPEN] 修复：Codex API 的 `compact` 提示“Model not found”**
    -   **内容**：这是对 Issue #6477 的直接修复。PR 通过修复模型 ID 到 API 内部 slug 的映射，解决了 `gpt-5.6-luna` 模型在执行 `compact` 时的 404 错误。
    -   **链接**：[https://github.com/earendil-works/pi/pull/6533](https://github.com/earendil-works/pi/pull/6533)

3.  **[#6584] [OPEN] 修复：forward provider options to summary requests**
    -   **内容**：解决了 Issue #6555 中提到的 `summarize` 和 `compact` 请求没有携带当前会话的 `provider` 选项（如 API 端点、自定义参数）的问题。
    -   **链接**：[https://github.com/earendil-works/pi/pull/6584](https://github.com/earendil-works/pi/pull/6584)

4.  **[#6594] [OPEN] 新功能：SQLite 会话存储**
    -   **内容**：一个比较大的特性更新，引入了基于 SQLite 的会话存储能力。旨在提升会话加载和管理的效率，并为后续功能（如“保留末尾Token”）提供支持。
    -   **链接**：[https://github.com/earendil-works/pi/pull/6594](https://github.com/earendil-works/pi/pull/6594)

5.  **[#6496] [CLOSED] 修复：支持 OpenRouter 的会话亲和性（Session Affinity）**
    -   **内容**：为了让 Pi 能更好地利用 OpenRouter 的提示缓存功能，此 PR 添加了对 OpenRouter 会话亲和性的支持，确保会话请求能被路由到同一台后端服务器。
    -   **链接**：[https://github.com/earendil-works/pi/pull/6496](https://github.com/earendil-works/pi/pull/6496)

6.  **[#6544] [CLOSED] 修复：将 GitHub Copilot MAI-Code 模型路由到正确的 API 端点**
    -   **内容**：修复了 GitHub Copilot 的 `mai-code-1-flash-picker` 模型无法使用的问题。该模型必须使用 `/responses` 端点而非 `/chat/completions`。此 PR 确保了正确的路由。
    -   **链接**：[https://github.com/earendil-works/pi/pull/6544](https://github.com/earendil-works/pi/pull/6544)

7.  **[#6588] [CLOSED] 修复：OpenAI 和 Codex 强制工具调用**
    -   **内容**：解决了 Issue #6585 中提到的，在请求中强制模型调用特定工具时可能存在的兼容性或逻辑问题。
    -   **链接**：[https://github.com/earendil-works/pi/pull/6588](https://github.com/earendil-works/pi/pull/6588)

8.  **[#6595] [CLOSED] 修复：使用环境认证时的分支摘要功能**
    -   **内容**：这是对 Issue #6324 的直接修复。修复要点是允许 `apiKey` 为 `null`，从而让使用 Bedrock、Vertex 等环境认证方式的用户能够正常使用 `/tree` 的分支摘要功能。
    -   **链接**：[https://github.com/earendil-works/pi/pull/6595](https://github.com/earendil-works/pi/pull/6595)

9.  **[#6449] [CLOSED] 添加 `ResourceExhausted` 为可重试错误**
    -   **内容**：根据 Issue #6364 的需求，此 PR 将 NVIDIA NIM 等 gRPC 服务返回的 `ResourceExhausted` 错误模式添加到了重试列表中。
    -   **链接**：[https://github.com/earendil-works/pi/pull/6449](https://github.com/earendil-works/pi/pull/6449)

10. **[#6608] [CLOSED] 回填缺失的推理块（`encrypted_content`）**
    -   **内容**：为了解决 Azure OpenAI Responses API 在多轮推理回复中的 400 错误（Issue #6409），此 PR 通过从 `response.completed` 事件中提取数据，来回填缺失的推理内容块。
    -   **链接**：[https://github.com/earendil-works/pi/pull/6608](https://github.com/earendil-works/pi/pull/6608)

## 功能需求趋势

从昨日的数据可以提炼出社区最关注的功能方向：

1.  **新模型兼容性**：这是最迫切的需求。社区正积极尝试最新的 AI 模型（如 OpenAI Codex gpt-5.6-luna, DeepSeek V4），并急需 Pi 对它们提供完整支持。问题主要集中在 `compact`、思考模式和认证流程上。
2.  **健壮性与可靠性**：用户对 Pi 的稳定性和错误处理能力有很高的期待。包括：重试机制需要更完善（如处理`ResourceExhausted`）、超时配置需要可靠、需要避免静默崩溃（如 DeepSeek 思考模式）。
3.  **多模态能力扩展**：部分开发者希望 Pi 的 `prompt` 命令能超越图片支持，扩展至视频和音频内容，以利用 GPT-4o、Gemma 4 等新一代多模态模型的全部潜力。
4.  **会话与上下文管理优化**：除了修复 `compact` 的兼容性，社区也在寻求更智能的缓存策略（如 PR #6618）、更有效的会话存储方案（如 PR #6594 的 SQLite 存储）以及更友好的上下文预算控制。
5.  **插件生态与可扩展性**：议题涉及自定义编辑器的快捷键绑定、插件报告成本的能力等，表明社区正在构建更丰富的插件生态，并期待 Pi 提供更强大的插件 API。

## 开发者关注点

根据开发者反馈，以下是最突出的痛点或高频需求：

-   **`compact` 功能不稳定**：`compact`（上下文压缩）是使用过程中的高频操作，但在特定模型上频繁失败，成为体验的重大阻碍。
-   **模型认证与配置混乱**：不同模型提供商的认证方式（API Key vs. 环境变量）和配置参数（如 `httpIdleTimeoutMs`）未能被统一、正确地处理，导致用户需要排查各种奇怪的错误。
-   **高级特性回归**：“思考模式”在早期版本正常，但在新版本 (v0.80.x) 中出现崩溃，这类回归问题尤其让开发者感到沮丧。
-   **边缘场景处理不足**：在代理、超时、输入令牌计算不准确等边缘情况下，Pi 的鲁棒性不足，导致请求失败或挂起。
-   **开发体验**：RPC 模式下缺乏干净的关闭命令（`

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 | 2026-07-14

---

## 今日速览

今日发布两个版本：`v0.19.9-nightly` 修复了 YOLO 模式保持与 CLI 交互转发问题；`desktop-v0.0.5` 跟随发布。社区最热议题集中在 **Daemon 多 Workspace 支持（#6378，22 条评论）** 以及 **PreToolUse hook 的 `ask` 决策静默失败（#6321）**。此外，`/insight` 报告时区不一致（#6835）和终端鼠标选择 Bug（#6808）获得较多关注，修复 PR 已陆续提交。

---

## 版本发布

### v0.19.9-nightly.20260714.9dd8389eb
- **修复**：当模型调用 `enter_plan_mode` 时保持 YOLO 模式（#6630）
- **特性**：CLI 转发 `ask_user` 功能

### desktop-v0.0.5
- 完整变更日志：[desktop-v0.0.4…desktop-v0.0.5](https://github.com/QwenLM/qwen-code/compare/desktop-v0.0.4...desktop-v0.0.5)

---

## 社区热点 Issues（挑选 10 个）

### 1. [#3803] Daemon 模式（qwen serve）：提案与公开决策  
- **评论**：25 | **👍** 1  
- **摘要**：6 章设计系列，跟踪 Daemon 模式完整设计实现，是当前多 Workspace、通道集成等功能的基础提案。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/3803

### 2. [#6378] 支持在单个 qwen serve Daemon 中管理多个 Workspace  
- **评论**：22 | **👍** 0  
- **摘要**：RFC 提案，要求打破当前“1 daemon = 1 workspace”限制，允许客户端按 workspace 隔离会话。社区讨论活跃。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6378

### 3. [#6321] PreToolUse hook 的 permissionDecision: “ask” 被静默忽略  
- **评论**：4 | **👍** 0  
- **摘要**：文档允许 `ask` 决策应弹出用户确认，但实际从不显示，工具调用被拒绝。严重影响用户控制权，社区反馈强烈。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6321

### 4. [#4514] 跟踪：Daemon 能力差距与优先级 Backlog（v0.16 后）  
- **评论**：15 | **👍** 0  
- **摘要**：跟踪 `qwen serve` HTTP/SSE 接口剩余短板，包括尚不支持的 slash-command 转发等。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/4514

### 5. [#5239] Subagent 与主会话通信机制薄弱  
- **评论**：4 | **👍** 0  
- **摘要**：子 agent 完成任务后无通知，挂掉后主会话不感知。用户提出文件监控变通方案，期待原生通知机制。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/5239

### 6. [#6808] 终端鼠标文本选择失效  
- **评论**：4  
- **摘要**：ScrollableList 的 `bypassVpGate` 强制 SGR 鼠标追踪，导致无法原生选中文本，为回归 Bug。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6808

### 7. [#6835] `/insight` 报告日期基准 UTC 与本地时间不一致  
- **评论**：2  
- **摘要**：热力图、连续天数、活跃小时等数据混合使用 UTC 和本地时间，导致非 UTC 用户统计错误。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6835

### 8. [#6806] `/compress` 后状态行上下文使用率不刷新  
- **评论**：2  
- **摘要**：执行压缩命令后，底部 status line 仍显示旧百分比，直到下一次模型请求才更新。影响用户体验。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6806

### 9. [#6801] 功能请求：`pinned/` 目录——只读内存文件，免于 `/dream` 合并  
- **评论**：2  
- **摘要**：在 memory 文件夹中增加锁定的只读目录，防止 `/dream` 命令将其合并/覆盖，用于保存关键上下文。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6801

### 10. [#6824] 功能请求：为会话历史添加关键词搜索  
- **评论**：2  
- **摘要**：当前无搜索历史功能，用户大量会话后难以定位。希望 CLI 和 VSCode 扩展均支持。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6824

---

## 重要 PR 进展（挑选 10 个）

### 1. [#6816] feat(daemon): 添加 Workspace Skill 切换 API  
- **摘要**：为 Daemon 增加 REST 和 TypeScript SDK 支持，允许通过 `skills.disabled` 启用/禁用加载的技能，支持主工作区和限定工作区路由。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6816

### 2. [#6825] feat(serve): Extension Management v2  
- **摘要**：引入扩展管理第二版，安装的扩展仍为全局，但激活策略支持工作区精确覆盖，并新增 `extension_management_v2` 能力标记。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6825

### 3. [#6606] fix(core): 从 Shell 子进程环境中清理内部 Daemon 密钥  
- **摘要**：防止 Daemon 内部密钥（如 API Token）通过环境变量泄漏到 shell 子进程，提升安全性。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6606

### 4. [#6841] refactor(review): 共享探测工作树路径助手，强化过期树清理  
- **摘要**：将 `git worktree remove` 后路径释放逻辑统一提取，修复多个清理站点未正确释放路径的问题。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6841

### 5. [#6784] perf(core): 减少 Git 快照子进程数  
- **摘要**：将主会话系统指令中的分支读取和短状态读取合并为一次 `git status --short --branch`，减少 Git 进程调用。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6784

### 6. [#6802] fix(cli): 转义 insight 报告数据中的 `<` 防止脚本逃逸  
- **摘要**：修复 `</script>` 在 `TemplateRenderer.renderInsightHTML` 中可能逃逸导致 XSS 的问题，并添加回归测试。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6802

### 7. [#6840] fix(review): 为 Chunk Agent 在代码中构建提示——此前它们被“盲”启动  
- **摘要**：发现 23/23 的 chunk agent 实际未收到 diff 内容，修正后每个子代理获得正确的代码差异，显著提升审查覆盖率。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6840

### 8. [#6819] feat(acp): 暴露工具调用准备生命周期  
- **摘要**：为 Anthropic/OpenAI 兼容流式提供商添加 `phase: preparing` 阶段，使 ACP 在工具调用 ID 稳定后即发送 pending 状态。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6819

### 9. [#6785] fix(core): 检测 dotfiles（如 `.gitignore`）  
- **摘要**：修复 `getLanguageFromFilePath` 无法识别以点开头的文件，添加首个测试用例。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6785

### 10. [#6807] feat(subagents): 使 Explore 默认继承主模型  
- **摘要**：将内置 Explore 子代理默认模型从自动选择 `fastModel` 改为继承主会话模型，并新增 `agents.builtin.exploreModel` 配置项。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6807

---

## 功能需求趋势

从近 24 小时 Issues/PR 中可提炼出社区最关注的五大方向：

1. **Daemon 多 Workspace 与渠道集成**  
   - #6378 多 Workspace RFC、#6010 热重载通道、#5887 多玩家频道 Agent（钉钉先行），表明社区要求将 `qwen serve` 打造成真正的服务端方案，支持多租户与 IM 渠道。

2. **Agent 间通信与任务编排**  
   - #5239 subagent 通知机制、#4228 `/goal` 长期工作流硬化，反映出用户希望子 agent 能可靠地向主会话汇报状态，实现复杂任务链。

3. **扩展与技能管理标准化**  
   - #6825 Extension Management v2、#6816 Skill 切换 API，社区期望有统一的后台扩展安装、激活、能力声明体系。

4. **安全与信任基线**  
   - #6831 信任预览状态泄露、#6606 密钥环境清理，表明用户对安全边界（如 dotfiles 识别、子进程隔离）的重视。

5. **用户界面精细化**  
   - #6808 鼠标选择、#6806 状态行刷新、#6824 历史搜索、#6813 工具摘要显示文件名，说明社区对终端交互细节的体验要求持续提升。

---

## 开发者关注点

- **权限与提示缺失**：`PreToolUse` 的 `ask` 决策从未弹出确认对话框（#6321），导致用户无法拦截危险操作，安全性受质疑。
- **终端残留与显示 Bug**：Ctrl-C 退出后终端部分按键失效（#6776）；Ctrl+S diff 预览多行编辑乱码（#6809）；工具摘要过长被截断（#6814）。
- **状态与数据不一致**：`/compress` 后状态行百分比不刷新（#6806）；`/insight` 报告时间基准混乱（#6835）；`/review test-efficacy` 探针在共享工作树中造成竞争（#6832）。
- **集成兼容性**：`auto` 模式对第三方 API（如 DeepSeek、MiniMax）兼容异常（#6791），主要是 `tool-choice` 缺失与 thinking 标签透传问题。
- **发布与 CI 稳定性**：近期多个 CI 失败（#6781、#6796、#6773）以及 SDK 发布被阻塞（#6822），反映出自动化流水线仍需加固。

---

*数据来源：GitHub QwenLM/qwen-code*  
*生成时间：2026-07-14*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报 | 2026-07-14

> 实际项目名称为 **CodeWhale**，代码仓库：[Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale)  
> 本日报覆盖过去24小时内的 Issue / PR 更新。

---

## 📌 今日速览

- **v0.8.68 发布候选 PR（#4361）已提交**，整合了水下 TUI 动效、键盘鼠标一致性、无障碍语义及权限变更，社区验收在即。
- **Anthropic API 错误（#4329）已关闭**：`tool_use` 与 `tool_result` 块不匹配问题得到修复，影响使用 Anthropic 模型的用户。
- **MiniMax 模型支持迎来第二波 PR**（#4352 已合并，#4354 待审），表明社区对多模型 provider 扩展的需求强劲。

---

## 🔖 版本发布

- 过去24小时无正式 Release；**v0.8.68 RC** 正在通过 PR #4361 推送。

---

## 🔥 社区热点 Issues（共6条，全部列出）

### 1. [#4329 – [CLOSED] Anthropic API error](https://github.com/Hmbown/CodeWhale/issues/4329)  
**状态：已关闭 | 评论数：7**  
**摘要：** `tool_use` 块后缺少对应的 `tool_result` 块导致 HTTP 400 Bad Request，影响 Anthropic Claude 调用。  
**重要性：** 直接影响以 Anthropic 为主力的用户，关闭表明已修复。社区评论较多，是近期最受关注的 bug。

### 2. [#4355 – v0.8.68: persist stateful terminal identity and restart limitations safely](https://github.com/Hmbown/CodeWhale/issues/4355)  
**状态：OPEN | 评论数：0**  
**摘要：** 有状态终端会话在重启后可能错误复用 PID 或本地记录，需要明确的持久化契约。  
**重要性：** 属于可靠性核心改进，为后续 agent 长期运行打下基础。

### 3. [#4358 – v0.8.68: add PTY coverage for work-surface and approval mouse interactions](https://github.com/Hmbown/CodeWhale/issues/4358)  
**状态：OPEN | 评论数：0**  
**摘要：** PTY 测试缺少对鼠标点击工作区和确认按钮的覆盖，影响用户交互体验。  
**重要性：** 直接关联 TUI 可用性，确保鼠标操作与键盘操作一致性。

### 4. [#4356 – v0.8.68: complete versioned exec stream receipts and tool lifecycle metadata](https://github.com/Hmbown/CodeWhale/issues/4356)  
**状态：OPEN | 评论数：0**  
**摘要：** 执行流 JSON 需要标准化的终端收据和工具生命周期元数据，用于回放、支持和成本归属。  
**重要性：** 可观测性与可审计性需求，影响运维和计费场景。

### 5. [#4359 – v0.8.68: define parent-stop semantics for detached background agents](https://github.com/Hmbown/CodeWhale/issues/4359)  
**状态：OPEN | 评论数：0**  
**摘要：** 后台分离 agent 的 Esc/停止行为存在歧义（继续 / 取消所有 / 询问），需要明确用户契约。  
**重要性：** 直接影响 agent 工作流可靠性，防止用户误操作导致任务中断。

### 6. [#4357 – v0.8.68: finish underwater receipt settling and phase-aware ambient motion](https://github.com/Hmbown/CodeWhale/issues/4357)  
**状态：OPEN | 评论数：0**  
**摘要：** 水下 TUI（动态背景）在等待输入、审批或减少动效模式下不应出现运动，需要收尾逻辑。  
**重要性：** TUI 视觉体验打磨，避免不必要的动画干扰用户操作。

---

## 🚀 重要 PR 进展（共5条，全部列出）

### 1. [#4361 – Prepare CodeWhale v0.8.68 release candidate](https://github.com/Hmbown/CodeWhale/pull/4361)  
**作者：Hmbown | 状态：OPEN**  
**摘要：** 合并所有 v0.8.68 功能：水下 TUI 完成、键盘/鼠标一致性、减少动效、权限变更等。  
**重要性：** 核心发布候选，社区应重点关注并参与测试。

### 2. [#4360 – Fix/browser open on bsd systems](https://github.com/Hmbown/CodeWhale/pull/4360)  
**作者：ci4ic4 | 状态：OPEN**  
**摘要：** 修复 NetBSD、FreeBSD、OpenBSD 等 BSD 系统上点击链接时提示“不支持浏览器打开”的问题。  
**重要性：** 跨平台兼容性修复，拓宽 TUI 应用范围。

### 3. [#4352 – [CLOSED] feat: add MiniMax Messages-compatible route](https://github.com/Hmbown/CodeWhale/pull/4352)  
**作者：octo-patch | 状态：已合并**  
**摘要：** 在 provider 注册表中添加 MiniMax Messages 兼容路由，支持 MiniMax-M3/M2.7。  
**重要性：** 已合并，标志着 MiniMax 模型正式进入 CodeWhale 生态。

### 4. [#4354 – feat: add MiniMax Messages provider support](https://github.com/Hmbown/CodeWhale/pull/4354)  
**作者：octo-patch | 状态：OPEN**  
**摘要：** 添加专用的 MiniMax 提供者，支持中国/全球 Base URL，注册模型并覆盖认证、路由、定价元数据。  
**重要性：** 进一步完善 MiniMax 集成，与 #4352 互补。

### 5. [#4351 – fix(scorecard): bind costs to provider routes](https://github.com/Hmbown/CodeWhale/pull/4351)  
**作者：nightt5879 | 状态：OPEN**  
**摘要：** 将离线计分卡价格绑定到精确 provider/model 路由，确保 OAuth、本地/自定义、未知网关路由失败关闭。  
**重要性：** 计费准确性修复，避免未定价路由产生不正确的成本数据。

---

## 📊 功能需求趋势（从 Issues / PR 中提炼）

| 需求方向 | 典型 Issue/PR | 热度 |
|----------|---------------|------|
| **水下 TUI / 终端动效** | #4357, #4361 | 🔥 高频打磨 |
| **有状态终端持久化与安全重启** | #4355 | 中 |
| **PTY 交互与鼠标支持** | #4358 | 中 |
| **执行流可观测性 & 工具生命周期** | #4356 | 中 |
| **后台 agent 停止语义** | #4359 | 中 |
| **新模型提供者（MiniMax）** | #4352, #4354 | 🔥 持续贡献 |
| **跨平台兼容（BSD 浏览器打开）** | #4360 | 中 |
| **计费与成本路由绑定** | #4351 | 低（但关键） |

**趋势判断：**  
- **TUI 体验打磨**（动效、鼠标、减少动效模式）是 v0.8.68 的重点。  
- **模型 provider 扩展**（MiniMax 连续两个 PR）表明社区希望摆脱单一模型依赖。  
- **可靠性与可观测性**（持久化、exec 收据、agent 语义）是底层基建改进，为后续 agent 连动奠定基础。

---

## 🛠 开发者关注点（痛点 / 高频需求）

1. **Anthropic API 错误修复**（#4329）—— 直接阻断使用，已解决但用户需升级。  
2. **状态终端重启歧义**（#4355）—— 开发者担心重启后 PID 误判导致状态丢失或安全风险。  
3. **BSD 平台浏览器打开不可用**（#4360）—— 小众但开发者反馈积极，修复快速。  
4. **后台 agent 停止行为模糊**（#4359）—— 可能造成用户误关闭后台任务，需明确文档与 UI 提示。  
5. **计费路由不精确**（#4351）—— 影响成本追踪，开发者希望失败关闭而非产生误导数据。

---

*数据时间窗口：2026-07-13 至 2026-07-14 UTC*  
*生成时间：2026-07-14 08:00 UTC*  
*为开发者保持关注，建议订阅 [Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale) *

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*