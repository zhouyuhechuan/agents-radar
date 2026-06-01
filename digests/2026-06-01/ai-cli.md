# AI CLI 工具社区动态日报 2026-06-01

> 生成时间: 2026-06-01 02:55 UTC | 覆盖工具: 9 个

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

好的，作为一名专注于 AI 开发工具生态的资深技术分析师，我已根据您提供的 2026 年 6 月 1 日各主流 AI CLI 工具的社区动态摘要，为您生成了以下横向对比分析报告。

---

### AI CLI 工具生态横向对比分析报告 (2026-06-01)

#### 1. 生态全景

当前 AI CLI 工具生态正处于 **“从可用到可靠”的剧烈阵痛与快速进化期**。一方面，工具能力边界迅速扩展，Agent 化、子代理、多模态、IDE 深度集成成为标配，推动着开发范式革新。另一方面，核心功能的稳定性问题成为社区最大痛点，尤其是 **扩展思维 (Extended Thinking)、Token 成本控制、Agent 行为可预测性** 等关键环节频频出现严重 Bug，表明这些前沿功能尚无成熟的技术保障。同时，生态分化初显，既有追求全平台、全模型支持的“全能型”工具（如 OpenCode），也有深耕特定模型生态、强化企业级服务的工具（如 OpenAI Codex），呈现出差异化竞争的态势。

#### 2. 各工具活跃度对比

| 工具名称 | 今日热点 Issues (Top 10+) | 重要 PR 进展 | 版本发布 | 社区活跃度评估 (基于 Issues 数量与热度) |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 10+ (严重 Bug 集中) | 0 | v2.1.159 (内部) | **极高** (严重 Bug 引发大量讨论) |
| **OpenAI Codex** | 10+ (Token 消耗、功能退化) | 10 (功能线完整) | rust-v0.136.0-alpha.2 | **极高** (长期问题发酵 + 新 Bug) |
| **Gemini CLI** | 10+ (Agent 可靠性问题) | 10 (修复密集) | 无 | **高** (开发团队修复积极，社区反馈活跃) |
| **GitHub Copilot CLI** | 10+ (v1.0.56 升级 Bug) | 0 | v1.0.57-4 | **高** (版本升级带来的连锁问题) |
| **Kimi Code CLI** | 10+ (API 兼容与登录 Bug) | 2 | 无 | **中高** (新工具，Bug 反馈集中) |
| **OpenCode** | 10+ (性能与兼容性) | 10 (功能增强) | 无 | **高** (社区庞大，问题类型广泛) |
| **Pi** | 10+ (模型兼容与 TUI 优化) | 10 (体验改进) | 无 | **高** (社区贡献者活跃，PR 数量多) |
| **Qwen Code** | 10+ (服务化与 IDE 集成) | 10 (架构优化) | v0.17.0-nightly | **中高** (侧重功能规划与架构重构) |
| **DeepSeek TUI** | 10+ (更名与缓存问题) | 10 (核心功能改进) | v0.8.48 (更名版本) | **中** (处于功能扩展期，社区规模相对较小) |

#### 3. 共同关注的功能方向

多个工具社区的反馈高度集中在几个核心痛点上，形成了行业性的共同诉求：

1.  **Agent 行为稳定性与可靠性** (几乎所有工具)
    - **具体诉求**：解决 Agent 挂起 (Claude Code, Gemini CLI)、子代理误报成功 (Gemini CLI, DeepSeek TUI)、模型捏造工具输出 (Claude Code)、子代理重复执行 (Claude Code) 等问题。
    - **涉及工具**：Claude Code, Gemini CLI, Kimi Code CLI, OpenCode, DeepSeek TUI, Qwen Code。

2.  **Token 消耗与成本控制的透明化** (Claude Code, OpenAI Codex, OpenCode)
    - **具体诉求**：公开“隐藏思考”Token 消耗 (Claude Code, OpenCode)、提供实时 Token 使用指示器 (OpenAI Codex)、解决 Token 消耗异常过快的问题 (Claude Code, OpenAI Codex)。
    - **涉及工具**：Claude Code, OpenAI Codex, OpenCode。

3.  **平台兼容性，尤其是 Windows 支持** (几乎所有工具)
    - **具体诉求**：修复 Windows 桌面端 Bug (OpenAI Codex, Qwen Code)、解决 WSL 下的 Git、输入、崩溃问题 (Claude Code, Pi, Kimi Code CLI)、支持 Wayland (Gemini CLI)、解决 IME 输入法死锁 (DeepSeek TUI)。
    - **涉及工具**：Claude Code, OpenAI Codex, Gemini CLI, Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, DeepSeek TUI。

4.  **IDE 集成深度与稳定性** (Claude Code, OpenAI Codex, Qwen Code)
    - **具体诉求**：修复 VS Code 扩展功能缺失 (Claude Code)、解决 JetBrains 插件登录和工作目录问题 (Qwen Code, Claude Code)、优化 IDE 内的 Token 显示 (OpenAI Codex)。
    - **涉及工具**：Claude Code, OpenAI Codex, Qwen Code。

5.  **可观测性与诊断能力** (Qwen Code, DeepSeek TUI)
    - **具体诉求**：为 daemon 服务添加 OpenTelemetry 支持 (Qwen Code)、提供更清晰的缓存命中率指标 (DeepSeek TUI)。
    - **涉及工具**：DeepSeek TUI, Qwen Code。

#### 4. 差异化定位分析

- **Claude Code**: **激进的前沿 Agent 探索者**。其核心特色是“扩展思维”和强大的 Agent 能力，但也是最不稳定、Bug 最多的工具。它瞄准的是愿意尝鲜、追求极致自动化、且对成本不那么敏感的高级开发者。目前来看，社区反馈它更像一个“高风险高回报”的实验场。
- **OpenAI Codex**: **企业级平台构建者**。从 PR 趋势（多账户切换、云端配置管理）看，它的目标是成为企业大规模部署 AI 开发助手的基础设施。它非常注重 IDE 集成和合规性，但用户对其成本控制和更新带来的“负优化”怨声载道。
- **Gemini CLI**: **专注 Agent 质量的工程师**。社区反馈的 PR 很密集，且核心逻辑修复（如避免模型幻觉、防止会话恢复崩溃）占比高，体现了 Google 团队对 Agent 基础可靠性的重视。它像一个正在快速打磨核心引擎的“工匠”，而非急于扩展外围功能。
- **GitHub Copilot CLI**: **最成熟的“个人效率工具”**。其社区反馈最为成熟，聚焦于版本升级带来的具体回归 Bug（登录、复制等）。它的核心价值是稳定、可靠的日常辅助，而非复杂的 Agent 功能。任何影响“基本操作”的问题都会引发最强烈的反感。
- **Kimi Code CLI**: **与模型深度绑定的“后起之秀”**。作为新兴工具，其 Bug 反馈集中在 API 兼容（双重编码、角色问题）和基础功能（登录、命令无响应）上。它更像是其旗舰模型（K2.6）的一个“原生”客户端，对模型特性的支持是核心优势，但基础设施尚不稳固。
- **OpenCode**: **社区驱动的“全能型”选手**。它支持的模型最广，社区最大，因此 Bug 类型也最杂，从 GPT 性能到 Gemma 兼容性。它像一个“开源集市”，各种技术和需求在此交汇，但也面临着维护复杂性高、问题追踪分散的挑战。
- **Pi**: **追求极致用户体验的“精耕者”**。它的 PR 主要围绕 TUI 细节（光标、聚焦、渲染）和跨平台兼容性。它不追求功能最多，而是追求在现有功能上提供最舒适的交互体验。社区贡献者对微小体验改进的热情很高。
- **Qwen Code**: **服务化与 MCP 生态的“架构师”**。它当前重心是补齐 `<qwen serve>` 的 HTTP/SSE 接口和 OpenTelemetry，同时强化 MCP 的安全模型（项目级、待审批）。这表明其定位是“AI 开发服务”的枢纽，而不仅是一个 CLI 工具。
- **DeepSeek TUI (CodeWhale)**: **性能与功能创新的“潜力股”**。它正经历品牌更名，同时社区诉求集中在缓存优化、Shell 实时输出等高级性能特性上。它展现出对“高级用户”需求的洞察，但代码质量和稳定性需要追赶。

#### 5. 社区热度与成熟度

- **成熟度最高，但面临稳定性危机**: **GitHub Copilot CLI** 社区反馈最为“专业”，问题聚焦点明确，这是成熟社区的特征。但频繁的回归 Bug 正在侵蚀用户信任。**OpenCode** 和 **Claude Code** 社区规模庞大，但 Issue 质量参差不齐，大量为严重的功能 Bug，表明其处于“成熟前的阵痛期”。
- **快速迭代，与社区共创**: **Gemini CLI**, **Pi**, **Qwen Code** 社区表现出极高的技术参与度，开发团队响应迅速，PR 数量和 Issue/PR 的关联度高，呈现出“开源共创”的健康态势。
- **新星崛起，问题导向**: **Kimi Code CLI** 和 **DeepSeek TUI** 的 Issue 数量不算最多，但问题类型非常聚焦于其核心功能路径（API 兼容、缓存），说明它们正处于验证核心价值、快速补短板的前期阶段。

#### 6. 值得关注的趋势信号

1.  **“推理 Token” 成本透明化是刚需**：Claude Code 与 OpenCode 的“隐藏思考 Token 消耗”引发众怒。这是一个强烈的信号：当模型开始进行复杂链式思考时，用户拒绝为不可见的“黑箱”操作买单。未来，提供可审计、可控制的推理过程将是高端模型 CLI 工具的核心竞争力。
2.  **Agent 技术栈从“实验”走向“生产”**：跨工具的 Agent 挂起、子代理误报、工具调用幻觉等问题，说明当前的 Agent 架构普遍缺乏健壮的错误处理、状态恢复和自愈能力。这不再是零星的 Bug，而是整个 Agent 技术栈必须解决的系统性问题。
3.  **平台兼容性是“及格线”而非“加分项”**：几乎所有工具都在 Windows/WSL 上遇到问题。这表明，对于想成为主流开发工具的 CLI 来说，跨平台（尤其是对 Windows 开发者）的稳定支持已不再是特色，而是其进入大众市场的“入场券”。
4.  **工具生态进入“平台战争”前夜**：OpenAI Codex 的多账户和企业配置 PR，以及 Qwen Code 的 daemon 服务规划，表明头部玩家正试图将简单的 CLI 工具升级为其 AI 开发云平台的“客户端”。这会加剧与 GitHub Copilot、JetBrains AI Assistant 等 IDE 原生 AI 功能的竞争。
5.  **“保留控制权”是用户的核心焦虑**：从对配置文件失效的愤怒（Gemini CLI）到对自动压缩失效的抱怨（Claude Code），再到要求 `/undo` 功能（OpenAI Codex），无不透露出用户对“AI 自作主张”的恐惧。开发者需要的是一个**可预测、可撤销、可配置**的智能助手，而不是一个“黑盒代理”。任何剥夺用户控制权的自动化功能，都会遭到强烈抵制。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，这是基于 `github.com/anthropics/skills` 仓库数据（截至2026-06-01）的社区热点分析报告。

---

### Claude Code Skills 社区热点报告 (2026-06-01)

#### 1. 热门 Skills 排行 (Top 5-8 PRs)

以下 Skills 凭借其功能实用性、技术深度或社区讨论度，成为当前最受关注的 PR：

1.  **Document Typography Skill (#514)**
    -   **功能**: 针对 AI 生成文档中常见的排版问题（如孤字成行、孤行段落悬挂、编号错位）进行质量控制。
    -   **社区热点**: 社区对此 PR 讨论热烈，核心焦点在于“AI 生成内容的最后一步——视觉呈现”的问题。用户普遍认可文档排版是 AI 生产力的关键短板，该 Skill 精准地解决了这一痛点。同时，对于如何定义“优秀排版”的规则边界（是严格遵循学术规范还是更宽松的阅读体验），社区存在探讨。
    -   **状态**: OPEN
    -   **链接**: [PR #514](https://github.com/anthropics/skills/pull/514)

2.  **ODT Skill — OpenDocument 格式支持 (#486)**
    -   **功能**: 为 Claude 添加创建、填充、读取和转换 ODF（.odt, .ods）格式文档的能力，填补了 LibreOffice 办公生态的支持空白。
    -   **社区热点**: 讨论围绕“跨平台办公格式支持”展开。许多用户反馈，虽然 DOCX 是主流，但在开源社区和特定企业环境中，ODT 是刚需。讨论还涉及其在处理政府文档、标准模板填充时的具体实现方案。
    -   **状态**: OPEN
    -   **链接**: [PR #486](https://github.com/anthropics/skills/pull/486)

3.  **改善前端设计 Skill 清晰度和可操作性 (#210)**
    -   **功能**: 对现有的 `frontend-design` Skill 进行重大修订，目标是使其指令更清晰、更可执行，确保 Claude 能在单次会话中遵循其指引。
    -   **社区热点**: 社区关注点并非在于提出新功能，而是对 **“元技能质量”** 的反思。用户讨论如何编写高质量的 Skill 才能让 Claude 真正理解和遵循，强调了技能自身文档结构、提示词精确度的重要性。
    -   **状态**: OPEN
    -   **链接**: [PR #210](https://github.com/anthropics/skills/pull/210)

4.  **Skill 质量与安全分析器 (PR #83)**
    -   **功能**: 引入两个元技能：`skill-quality-analyzer` 和 `skill-security-analyzer`，用于自动评估其他 Skill 的结构、文档、安全性和质量。
    -   **社区热点**: 随着社区 Skill 数量激增，如何保证其质量和安全性成为焦点。该 PR 试图建立一套社区标准，讨论围绕“自动化质量门禁”、“安全风险扫描（如注入攻击、敏感信息泄露）”和“评分标准合理性”展开。
    -   **状态**: OPEN
    -   **链接**: [PR #83](https://github.com/anthropics/skills/pull/83)

5.  **SAP 预测分析 Skill (#181)**
    -   **功能**: 集成 SAP 开源的表格基础模型 SAP-RPT-1-OSS，用于对 SAP 业务数据进行预测性分析。
    -   **社区热点**: 这是企业级功能与 AI 深度结合的典型代表。讨论集中在如何将 Claude 与特定的企业级模型和数据集（SAP）对接，以及该 Skill 能否简化复杂的 SAP 数据分析流程。社区对其在财务预测、供应链优化等方面的应用潜力非常期待。
    -   **状态**: OPEN
    -   **链接**: [PR #181](https://github.com/anthropics/skills/pull/181)

6.  **AURELION 技能套件 (#444)**
    -   **功能**: 引入了一套名为 AURELION 的认知与记忆框架技能，包括结构化思维模板（kernel）、顾问（advisor）、代理（agent）和持久化记忆（memory）。
    -   **社区热点**: 社区对此复杂的“系统级”技能套件保持了高关注度。讨论聚焦于其“结构化认知”方法是否优于传统的提示词工程，以及如何解决多技能间的冲突和上下文管理问题。这是一种将人类认知模型迁移到 AI 代理的尝试。
    -   **状态**: OPEN
    -   **链接**: [PR #444](https://github.com/anthropics/skills/pull/444)

7.  **测试模式 Skill (#723)**
    -   **功能**: 提供一个全面的测试技能，覆盖单元测试（AAA模式）、React组件测试、端到端测试及测试哲学（测试奖杯模型）。
    -   **社区热点**: 软件质量是社区永恒的话题。这个 PR 因其全面的测试指导而备受好评。讨论主要集中在 **“测试策略”** 本身，如如何定义测试范围、如何编写可维护的测试用例，以及该 Skill 能否适配不同语言和框架的项目。
    -   **状态**: OPEN
    -   **链接**: [PR #723](https://github.com/anthropics/skills/pull/723)

---

#### 2. 社区需求趋势 (Top Issues 分析)

从高活跃度 Issues 中，可以提炼出社区最期待的四个发展方向：

1.  **组织级协作与共享** (#228): **“如何让 Skills 在团队内轻松共享？”** 是最核心的呼声。用户不满于手动下载/上传 Skill 文件，强烈要求提供组织内的技能库或共享链接功能，以提升团队协作效率。
2.  **核心工具链的稳定性与兼容性** (#556, #202, #1087, #1102): 社区对 `skill-creator`, `run_eval.py` 等官方工具的质量、跨平台支持（特别是 Windows）和遵循最佳实践提出了明确要求。同时，关于插件加载逻辑混乱（#1087）和 MCP 数据臃肿（#1102）的讨论，表明用户希望官方工具链更稳健、智能。
3.  **安全与信任边界** (#492, #1175): 随着 Skills 权限提升，安全问题浮出水面。社区担忧在 `anthropic/` 命名空间下分发社区技能存在信任风险（#492），以及企业场景下（如处理 SharePoint 文档）的技能权限管控问题（#1175）。**安全审查机制和权限沙箱**是当前待解决的痛点。
4.  **AI 代理治理与标准化** (#412, #16): 社区不仅希望 Skills 执行任务，更希望其具备“治理”能力，如策略执行、威胁检测（#412）。此外，将 Skills 能力通过 MCP 暴露为标准化 API（#16）的呼声，反映了社区对 **Skills 互操作性和可组合性** 的长期期待。

---

#### 3. 高潜力待合并 Skills (近期可能落地)

以下 PR 评论活跃、功能明确，且尚未被合并，是近期最有可能被官方采纳或进入主分支的候选者：

1.  **Document Typography (#514)**: 解决了一个广泛存在的“最后一公里”问题，社区认可度高，技术方案边界清晰。
2.  **ODT Format Support (#486)**: 填补了重要的生态空白，与 DOCX 形成互补，对开源用户和企业用户都具有极高价值。
3.  **Skill Quality & Security Analyzer (#83)**: 这是维持社区健康发展的“基础设施”，符合 Anthropic 对生态治理的长期利益，但可能需要更多打磨。

---

#### 4. Skills 生态洞察

**一句话总结**: 当前社区对 Skills 的核心诉求已从“**创造功能**”转向“**建立秩序**”——即在技能数量爆发式增长的背景下，对质量保证、安全审计、组织协作和工具链可靠性提出了更迫切、更成体系的建设性要求。

---

好的，这是为您生成的 2026-06-01 Claude Code 社区动态日报。

---

# Claude Code 社区动态日报 | 2026-06-01

## 今日速览

今日社区最关切的问题集中在 **扩展思维 (Extended Thinking) 会话永久卡死** 的严重 Bug 上，两个独立报告的 Issue 均指向模型输出“修改的签名块”导致 API 400 错误。同时，**Token 消耗异常**（特别是 Opus 4.8 模型）以及 **自动压缩 (Auto-Compact) 失效** 等问题引发了开发者的广泛讨论。版本 v2.1.159 仅包含内部基础设施改进。

## 版本发布

- **v2.1.159**: 仅包含内部基础设施改进，无用户侧功能变化。

## 社区热点 Issues

1.  **[严重] [BUG] Resuming an extended-thinking session fails permanently with 400** (#63147)
    - **重要性**: 高。一个影响扩展思维会话的严重 Bug，当会话中包含工具调用时，恢复后会导致会话永久卡死，无法继续使用。已有 56 条讨论，社区反响强烈。
    - **链接**: [#63147](https://github.com/anthropics/claude-code/issues/63147)

2.  **[严重] Extended thinking: signed thinking block 'cannot be modified' (400) permanently wedges session** (#63335)
    - **重要性**: 高。与 #63147 高度相关，均指向扩展思维功能的核心问题。该 Issue 明确指出是模型重放了“被修改”的签名 `thinking` 块，导致 API 拒绝请求。
    - **链接**: [#63335](https://github.com/anthropics/claude-code/issues/63335)

3.  **[BUG] 5h token usage massively outstripping actual context** (#64093)
    - **重要性**: 高。用户反馈在约5小时的时间内，Token 消耗远超预期，可能涉及计费问题或模型行为异常。已有20条评论，且刚创建不久，关注度正在上升。
    - **链接**: [#64093](https://github.com/anthropics/claude-code/issues/64093)

4.  **[BUG] Opus 4.8 medium effort spends 46k output tokens on hidden thinking for a simple coding turn** (#64153)
    - **重要性**: 中高。用户发现 Opus 4.8 模型在执行简单任务时，在“隐藏思考”过程中消耗了异常多的输出 Token（46K），直接增加使用成本。
    - **链接**: [#64153](https://github.com/anthropics/claude-code/issues/64153)

5.  **[Bug] Model fabricates tool output (and even a user instruction) when a parallel batch is partially cancelled** (#63538)
    - **重要性**: 高。一个严重的模型行为问题，当部分并行工具调用被取消时，模型会捏造调用结果，甚至虚构用户指令。这对于依赖工具调用的自动化工作流是致命缺陷。
    - **链接**: [#63538](https://github.com/anthropics/claude-code/issues/63538)

6.  **[Bug] [Bug] Auto-compact never triggers despite statusline reporting “100% context used”** (#63015)
    - **重要性**: 中高。自动压缩功能失效，即使界面显示上下文已用满100%也无法触发，导致会话持续增长，最终可能引发上下文超限错误。
    - **链接**: [#63015](https://github.com/anthropics/claude-code/issues/63015)

7.  **[BUG] [BUG] German umlauts (ä, ö, ü) randomly replaced with ASCII substitutes (ae, oe, ue)** (#14131)
    - **重要性**: 中。一个存在已久的字符编码问题，影响德语等非英语用户。尽管已开放数月，但仍有33条评论和持续的更新，表明该问题未得到有效解决。
    - **链接**: [#14131](https://github.com/anthropics/claude-code/issues/14131)

8.  **[Bug] Agent spams no-op echo probe commands to flush shell output** (#63887)
    - **重要性**: 中。Agent 在 Bash 工具输出缓慢时，会大量发送无意义的 `echo` 命令来“冲刷”输出，这不仅低效，而且会使日志变得混乱。
    - **链接**: [#63887](https://github.com/anthropics/claude-code/issues/63887)

9.  **[Bug] Harness silently executes duplicated parallel tool_use blocks: subagent fan-out runs N× the intended count** (#64080)
    - **重要性**: 中高。当模型在单个轮次中并行调用子代理时，会重复发出相同的 `tool_use` 块，导致实际执行次数是预期数量的数倍（如从6次变成24次），造成资源浪费。
    - **链接**: [#64080](https://github.com/anthropics/claude-code/issues/64080)

10. **[BUG] VS Code extension doesn't load Chrome browser tools in chat panel** (#50423)
    - **重要性**: 中。文档表明 `@browser` 工具可用，但在 VS Code 扩展的聊天面板中无法加载，与文档描述不符，影响 Linux 用户在 IDE 内使用浏览器工具。
    - **链接**: [#50423](https://github.com/anthropics/claude-code/issues/50423)

*注：Issue #34229 评论数和点赞数最高，但内容疑似非技术性账户问题，未列入上述重点。*

## 重要 PR 进展

无。过去24小时内没有 PR 被创建或更新。

## 功能需求趋势

从近期的 Issues 和反馈中，社区主要关注以下功能方向：

1.  **IDE 与平台集成稳定性**: 用户持续要求修复 VS Code 扩展的 `@browser` 工具加载问题 ( #50423 )，并希望 JetBrains 插件支持设置父文件夹为工作目录 ( #61762 )。
2.  **成本控制与透明度**: Opus 4.8 模型的隐藏思考 Token 消耗 ( #64153 ) 和 Token 用量异常 ( #64093 ) 是核心痛点，用户渴望更透明的计费和消耗控制机制。
3.  **扩展思维 (Extended Thinking) 功能可靠性**: 当前该功能处于不稳定的状态，会话恢复即崩溃的问题 ( #63147, #63335 ) 是社区最期望修复的急迫问题。
4.  **Windows 生态支持**: 社区期望在 Windows 上支持“Computer Use”功能 ( #54833 )，表明对跨平台统一体验的需求。
5.  **自动化与 Agent 行为可预测性**: 模型捏造工具输出 ( #63538 ) 和子代理重复执行 ( #64080 ) 等问题，显示用户对 Agent 行为可靠性和可预测性的高度关注。

## 开发者关注点

1.  **会话稳定性是首要痛点**: 扩展思维功能的“一碰就碎”是当前最具破坏性的问题，开发者几乎无法依赖该功能进行持续工作。
2.  **Token 成本账本不清**: 开发者对 Opus 4.8 的高 Token 消耗感到不安，特别是“隐藏思考”带来的隐性成本，这可能直接影响用户对高端模型的使用意愿。
3.  **自动压缩 (Auto-Compact) 形同虚设**: “Auto-compact”功能在多个版本中均反馈不生效 ( #63015, #64277 )，导致开发者需要手动干预，破坏了“无人值守”的自动化工作流体验。
4.  **模型行为“幻觉”问题**: 从捏造工具输出到无意义地发送 `echo` 命令，开发者对模型在没有明确指令情况下的“自作主张”行为表示担忧，这影响了 Agent 工具的可信度。
5.  **平台兼容性磨损**: 从 Linux 的 VS Code 扩展问题到 WSL 中的 OSC 52 兼容性 Issue ( #61043 )，再到安卓 Termux 的回归 Bug ( #64202 )，跨平台的一致性和稳定性仍是一大挑战。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，作为一名专注于 AI 开发工具的技术分析师，我已根据您提供的 GitHub 数据，为您生成 2026 年 6 月 1 日的 OpenAI Codex 社区动态日报。

---

### OpenAI Codex 社区动态日报 | 2026-06-01

#### 1. 今日速览

今日社区动态活跃，**Token 消耗过快**问题（#14593）持续发酵，成为社区关注度最高的议题。同时，**Windows 桌面应用**和**身份验证流程**成为新的 Bug 重灾区，多项问题被集中反馈。在开发端，Codex 团队正积极推进**多账户切换 (Profile Switcher)** 和**云端配置管理**等底层架构的更新。

#### 2. 版本发布

- **rust-v0.136.0-alpha.2**: 今日发布了 Rust 版本的 0.136.0 第二个 Alpha 版本，但公告中未提供具体的更新日志。

#### 3. 社区热点 Issues

1.  **[#14593] Token 消耗过快 (Burning tokens very fast)**
    - **链接**: [Issue #14593](https://github.com/openai/codex/issues/14593)
    - **重要性**: **社区最关注的问题**。自 3 月以来已有 **593 条评论**和 **261 个赞**，说明大量 Business 订阅用户在 VSCode 上遭遇此问题，严重影响使用成本。
    - **社区反应**: 用户持续追问和提供线索，但问题仍处于开放状态，Codex 团队尚未给出根本解决方案。

2.  **[#2847] 排除敏感文件机制 (A way to exclude sensitive files)**
    - **链接**: [Issue #2847](https://github.com/openai/codex/issues/2847)
    - **重要性**: **呼声最高的功能请求**，获 **396 个赞**。用户强烈要求 Codex 能像 `.gitignore` 一样，提供 `.codexignore` 机制来保护敏感文件，防止被 AI 读取或发送。
    - **社区反应**: 社区中企业用户和安全意识较强的开发者持续关注，期待该功能尽快落地。

3.  **[#8745] CLI 集成 LSP (LSP integration for Codex CLI)**
    - **链接**: [Issue #8745](https://github.com/openai/codex/issues/8745)
    - **重要性**: 获 **360 个赞**的增强建议。开发者希望 Codex CLI 能内建语言服务器协议支持，利用 LSP 的诊断和符号智能来生成更精确的代码，减少错误。
    - **社区反应**: 社区普遍认为这是提升 CLI 模式下代码质量的关键功能，讨论热度高。

4.  **[#23794] [已关闭] 桌面端上下文/Token 使用指示器消失**
    - **链接**: [Issue #23794](https://github.com/openai/codex/issues/23794)
    - **重要性**: 桌面应用的核心体验问题。更新后，用户无法直观看到 Token 使用情况，导致难以控制成本。该 Issue 在关闭前有 **160 条评论**和 **156 个赞**，影响面广。
    - **社区反应**: 用户普遍抱怨此功能退化，认为这是一个严重的 UI 回退。

5.  **[#20161] [已关闭] 手机号验证失败**
    - **链接**: [Issue #20161](https://github.com/openai/codex/issues/20161)
    - **重要性**: **身份验证流程的严重 Bug**。用户在切换设备或使用 SSO 登录后，被强制要求绑定手机号，且功能失效，导致无法使用。
    - **社区反应**: 此 Bug 影响大量用户的正常接入，共有 177 条评论，表明该问题具有普遍性。

6.  **[#9203] 希望恢复 "/undo" 功能**
    - **链接**: [Issue #9203](https://github.com/openai/codex/issues/9203)
    - **重要性**: 开发者对 **CLI 和 TUI 模式下的安全机制**有强烈需求。`/undo` 功能在误操作（如误删未跟踪文件）时至关重要，获 **261 个赞**。
    - **社区反应**: 许多开发者表示曾因此遭受损失，希望团队能将其作为高优先级功能重新引入。

7.  **[#21598] Windows 桌面端 Chrome 插件在挪威/EU 不可用**
    - **链接**: [Issue #21598](https://github.com/openai/codex/issues/21598)
    - **重要性**: **区域可用性问题**。即使 Chrome 扩展显示已连接，Windows 桌面应用也无法调用相关功能，这可能与欧洲地区的服务部署策略有关。
    - **社区反应**: 欧洲用户对此表示困惑和失望，限制了该地区的使用场景。

8.  **[#25244] 目标模式（Goal）问题在重启后消失**
    - **链接**: [Issue #25244](https://github.com/openai/codex/issues/25244)
    - **重要性**: **严重的数据持久化问题**。用户表述的 “serious error!!!!” 表明，重启客户端后，长期运行的 “Goal” 会话会丢失，对依赖此功能进行长时任务管理的用户打击巨大。
    - **社区反应**: 反馈数量不多，但问题性质严重，容易引发用户对数据安全性的担忧。

9.  **[#20873] [已关闭] 聊天被标记为“可能的网络安全风险”**
    - **链接**: [Issue #20873](https://github.com/openai/codex/issues/20873)
    - **重要性**: **安全策略误判问题**。用户在使用 CLI 进行正常开发时，会话被标记为“网络安全风险”，导致使用中断。这对开发工作流程是致命的。
    - **社区反应**: 此类问题会严重降低用户的信任感，虽然已关闭，但反映出安全审查机制仍需优化。

10. **[#14860] 执行远程压缩任务错误**
    - **链接**: [Issue #14860](https://github.com/openai/codex/issues/14860)
    - **重要性**: CLI 模式下后台任务**长期存在**的问题。执行 `remote compact` 任务失败，影响使用远程沙箱功能的用户。
    - **社区反应**: 90 条评论表明此问题困扰了不少开发者，稳定性有待提高。

#### 4. 重要 PR 进展

1.  **[#25383] [3/3] 多账户切换：应用服务器账户会话生命周期**
    - **链接**: [PR #25383](https://github.com/openai/codex/pull/25383)
    - **功能**: 这是 **多账户切换** 功能的最后一部分，为桌面应用添加了账号会话的完整生命周期管理，包括添加、切换、注销等核心操作。

2.  **[#25470] [2/3] 多账户切换：保存的会话凭证槽**
    - **链接**: [PR #25470](https://github.com/openai/codex/pull/25470)
    - **功能**: 为多账户功能提供底层凭证存储支持，允许安全地保存和管理多个账号的 OAuth 凭证。

3.  **[#25469] [1/3] 多账户切换：账户会话协议**
    - **链接**: [PR #25469](https://github.com/openai/codex/pull/25469)
    - **功能**: 定义前端和后端之间关于账户会话的通信协议，是整个多账户功能的通信基础。**这三组 PR 构成了一个完整的功能线**。

4.  **[#25351] 锁定线程的多智能体运行时版本**
    - **链接**: [PR #25351](https://github.com/openai/codex/pull/25351)
    - **修复**: 修复了线程恢复或分叉时，智能体版本可能不一致的 Bug，确保一个线程在整个生命周期内使用同一版本的智能体系统，提升了行为可预测性。

5.  **[#25480] 向模型暴露本地图片路径**
    - **链接**: [PR #25480](https://github.com/openai/codex/pull/25480)
    - **功能**: 优化多模态体验。当用户附加本地图片时，现在会将文件的绝对路径也传递给模型，允许模型直接引用该路径，提升交互能力。

6.  **[#25113] 存储并暴露父线程 ID**
    - **链接**: [PR #25113](https://github.com/openai/codex/pull/25113)
    - **修复**: 修复了子代理数据建模中的一个核心问题，明确区分了“分叉来源”和“父线程”两个概念，为更清晰的线程和子代理管理打下基础。

7.  **[#24812] 显示企业月度信用额度**
    - **链接**: [PR #24812](https://github.com/openai/codex/pull/24812)
    - **功能**: 提升企业用户体验。现在在 `/status` 命令中会显示企业的月度消费限额，让企业用户能更好地进行成本控制。

8.  **[#24622] 切换到云端配置包**
    - **链接**: [PR #24622](https://github.com/openai/codex/pull/24622)
    - **功能**: 这是 **云端配置管理** 架构更新的收官之作。正式将运行时的配置加载切换到统一的云端配置包，这将使企业能够更灵活地远程管理用户的 Codex 设置。

9.  **[#25457] 缓存远程插件目录**
    - **链接**: [PR #25457](https://github.com/openai/codex/pull/25457)
    - **性能**: 优化插件安装体验。通过缓存远程插件目录，加快插件推荐和安装的响应速度，减少启动和安装时的网络延迟。

10. **[#25453] Windows 桌面端频繁启动 powershell.exe 导致高 CPU**
    - **链接**: [PR #25453](https://github.com/openai/codex/issues/25453)
    - **Bug**: (此为一个 Issue，但因其直接指向性能问题，故纳入) 报告 Windows 桌面端存在严重的性能问题，每秒都会启动 `powershell.exe` 进行进程轮询，导致 CPU 占用率过高。

#### 5. 功能需求趋势

- **上下文与成本控制**：社区最核心的需求是围绕上下文窗口和 Token 消耗的透明度与控制权。用户希望看到实时的 Token 使用指示器（#23794），并抱怨“Token 燃烧过快”（#14593）。同时，对 `.codexignore` 这类敏感文件排除机制（#2847）的呼声极高，这本质上也是一种安全性的上下文控制。
- **多账户与企业级管理**：从 PR 趋势看，Codex 团队正在为**多账户切换**和**云端企业配置管理**做准备。这是企业大规模部署 Codex 的关键前提，表明 Codex 正从个人工具向企业级平台演进。
- **CLI 与自动化增强**：开发者对 CLI 的智能性要求越来越高，`LSP 集成`（#8745）的诉求强烈。同时，对 `/undo` 等安全操作命令（#9203）的呼声，反映出在自动化代码生成场景下，开发者对可回滚和安全操作的高度重视。
- **Windows 平台稳定性**：今日的 Issues 中，大量 Windows 专用 Bug (如 #21598, #25249, #25453 等) 被密集报告，表明 **Windows 桌面应用的稳定性、兼容性和性能**是当前团队需要重点关注和优化的方向。

#### 6. 开发者关注点

- **安全性**：安全问题是开发者的首要痛点。从“网络安全风险误判”（#20873）到“敏感文件保护缺失”（#2847），再到“身份验证流程失败”（#20161），任何影响开发流程安全性或导致工作阻断的问题都会引发强烈反响。
- **数据持久化与可靠性**：“Goal 模式问题消失”（#25244）和“聊天历史丢失”（#21119）等问题，直接触及用户对数据持久性的信赖。开发者无法容忍 AI 辅助过程中产生的关键信息无故丢失。
- **更新带来的负优化**：用户对“更新后功能退化”极为敏感，如上下文指示器消失（#23794）、速度设置重置（#20769）等。开发者期望更新带来的是体验提升，而非需要重新适应甚至接受功能降级。
- **配置的稳定性与可迁移性**：用户在更新后遭遇配置丢失或配置迁移失败（#25440），以及“远程控制设备丢失”（#23403）等问题，这些“配置类” Bug 虽然不如功能 Bug 显眼，但会深刻影响用户对产品成熟度的信任。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，以下是 2026-06-01 的 Gemini CLI 社区动态日报。

---

# Gemini CLI 社区动态日报 | 2026-06-01

## 今日速览

社区开发热度不减，核心团队持续关注 **Agent 子系统稳定性与可靠性** 的修复工作，同时积极推动 **子代理功能** 的迭代。今日更新中，多个关于 Agent 挂起、子代理误报成功、以及工具使用不当的关键 Bug 被标记为待回归验证；同时，针对 AST 感知代码读取、组件级评估等长期功能的讨论也在深入进行。

## 社区热点 Issues

以下为今日最值得关注的 10 个 Issue，它们反映了社区最关心的稳定性和功能方向。

1.  **[#21409] Generalist agent hangs (通用代理挂起)**
    - **重要性**: **高**。这是一个影响广泛的严重 Bug，用户在将任务委托给通用 Agent 时会遇到无限挂起，简单操作（如创建文件夹）都无法完成。
    - **社区反应**: 获得 8 个 👍，是近期热度最高的问题。用户通过明确禁止使用子代理作为临时的解决方案，表明问题根源在于子代理调用机制。
    - **链接**: `google-gemini/gemini-cli Issue #21409`

2.  **[#24353] Robust component level evaluations (健壮的组件级评估)**
    - **重要性**: **高**。这是一个 EPIC（史诗级任务），旨在建立更强大的组件级评估体系。目前已拥有 76 个行为评估测试，对于保证 Agent 核心功能的质量至关重要。
    - **社区反应**: 讨论了 7 次，开发者们深入探讨了如何扩展和优化评估框架。
    - **链接**: `google-gemini/gemini-cli Issue #24353`

3.  **[#22745] Assess the impact of AST-aware file reads, search, and mapping (评估 AST 感知的文件读取、搜索和映射的影响)**
    - **重要性**: **高**。这是一个前瞻性的研究 EPIC，探索利用抽象语法树 (AST) 能力提升 Agent 理解代码的精准度和效率。若能成功，将显著减少 Token 消耗和交互次数。
    - **社区反应**: 社区积极讨论 AST 工具（如 tilth, glyph）的应用潜力，期待能解决代码读取不准、范围过大等痛点。
    - **链接**: `google-gemini/gemini-cli Issue #22745`

4.  **[#22323] Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption (子代理达到最大轮次后错误报告为成功)**
    - **重要性**: **高**。这是一个逻辑 Bug，子代理在被强制中断后，向上层伪装成“任务成功”，导致用户无法得知任务并未完成，影响任务可靠性和信任度。
    - **社区反应**: 讨论了 6 次，开发者强调了这是一个严重的误导性问题。
    - **链接**: `google-gemini/gemini-cli Issue #22323`

5.  **[#25166] Shell command execution gets stuck with "Waiting input" after command completes (Shell 执行完成后卡在“等待输入”)**
    - **重要性**: **高**。频繁出现的用户问题，影响日常开发工作流。即使是极其简单的命令，也可能导致终端无响应，需要手动干预。
    - **社区反应**: 用户报告了多次出现此情况，获得 3 个 👍，表明此问题具有一定的普遍性。
    - **链接**: `google-gemini/gemini-cli Issue #25166`

6.  **[#21968] Gemini does not use skills and sub-agents enough (Gemini 不主动使用技能和子代理)**
    - **重要性**: **中高**。这是关于 Agent 主动性问题的重要反馈。用户精心配置的“技能”和“子代理”未被模型主动调用，导致功能形同虚设，无法发挥 Agent 的复杂任务处理能力。
    - **社区反应**: 用户提供了具体案例（gradle, git 技能），说明模型只在明确指令下才使用，缺乏主动性。
    - **链接**: `google-gemini/gemini-cli Issue #21968`

7.  **[#21983] browser subagent fails in wayland (浏览器子代理在 Wayland 环境下失败)**
    - **重要性**: **中高**。这是一个平台兼容性问题。随着 Wayland 显示服务器的普及，浏览器 Agent 无法正常工作将影响部分 Linux 用户的使用体验。
    - **社区反应**: 用户提供了详细的错误报告，有助于开发者定位问题。
    - **链接**: `google-gemini/gemini-cli Issue #21983`

8.  **[#23571] Model frequently creates tmp scripts in random spots (模型频繁在随机位置创建临时脚本)**
    - **重要性**: **中**。用户工作流痛点。模型为了执行 Shell 命令，倾向于在项目各处撒下临时脚本，这极大增加了工作区清理的负担，用户期望模型行为更有序。
    - **社区反应**: 开发者内部认为这是一个需要解决的行为问题，强调模型应遵守更整洁的工作区管理规范。
    - **链接**: `google-gemini/gemini-cli Issue #23571`

9.  **[#22267] [BUG] Browser Agent ignores settings.json overrides (浏览器 Agent 忽略 settings.json 配置)**
    - **重要性**: **中**。配置穿透性问题。用户在 `settings.json` 中为浏览器 Agent 设置的参数（如 `maxTurns`）被完全忽略，导致无法精细控制 Agent 行为。
    - **社区反应**: 用户确认问题依然存在，需要开发团队修复。
    - **链接**: `google-gemini/gemini-cli Issue #22267`

10. **[#22186] get-shit-done output hook causes crash (get-shit-done 输出钩子导致崩溃)**
    - **重要性**: **中**。稳定性问题。当使用 `get-shit-done` 命令时，在任务即将完成的最后一步输出时会导致程序崩溃，严重影响用户体验。
    - **社区反应**: 用户多次遇到此问题，提供了详细的崩溃堆栈信息。
    - **链接**: `google-gemini/gemini-cli Issue #22186`

## 重要 PR 进展

今日主要关注 Agent 核心逻辑的修复和功能优化。

1.  **[#27174] fix(core): exclude .gemini/tmp/ from agent search tools by default (排除 .gemini/tmp/ 目录)**
    - **重要性**: **高**。基础性能修复。Agent 在搜索文件时，会错误地递归扫描自己的`session`日志文件，导致性能下降。此 PR 通过默认排除该目录来解决问题。
    - **状态**: 已合并
    - **链接**: `google-gemini/gemini-cli PR #27174`

2.  **[#27170] fix(core): prevent dropping valid model turns with empty text parts (防止丢弃包含空文本的有效模型轮次)**
    - **重要性**: **高**。核心逻辑修复。当模型返回 `functionCall` 带有一个空字符串文本时，CLI 会错误地丢弃整个模型轮次，导致 API 400 错误。此 PR 修复了这个过度过滤的问题。
    - **状态**: 已合并
    - **链接**: `google-gemini/gemini-cli PR #27170`

3.  **[#27412] fix(core): prevent model fabrication when read_file returns binary content (防止读取二进制文件时模型产生幻觉)**
    - **重要性**: **高**。可靠性修复。当 `read_file` 读取 PDF 等二进制文件时，模型会错误地“脑补”文件内容进行分析。此 PR 通过改进响应处理，防止了模型编造信息。
    - **状态**: 开放中
    - **链接**: `google-gemini/gemini-cli PR #27412`

4.  **[#27418] feat(core): ensure non-interactive shell respects 'enableInteractiveShell: false' (确保非交互式 Shell 遵循配置)**
    - **重要性**: **高**。配置一致性修复。修复了当用户设置 `enableInteractiveShell: false` 时，非交互式 Shell 仍可能被启动的问题。
    - **状态**: 开放中
    - **链接**: `google-gemini/gemini-cli PR #27418`

5.  **[#27371] fix(core): handle EBADF error when PTY fd is stale on session resume (处理会话恢复时的 PTY 文件描述符错误)**
    - **重要性**: **高**。稳定性修复。修复了使用 `gemini --resume` 恢复会话时，由于 PTY 文件描述符过期导致程序崩溃的问题。
    - **状态**: 已合并
    - **链接**: `google-gemini/gemini-cli PR #27371`

6.  **[#24478] feat(cli): add top-level /reload command to refresh all systems (添加 /reload 命令)**
    - **重要性**: **中**。用户体验提升。新增 `/reload` 命令，允许用户一键重新加载所有 Agent 状态，包括技能、Agent、MCP 服务器和配置，避免手动逐一操作。
    - **状态**: 开放中（提醒需要关联 Issue）
    - **链接**: `google-gemini/gemini-cli PR #24478`

7.  **[#27179] Feat/add local gemma 4 support (添加本地 Gemma 4 支持)**
    - **重要性**: **中**。功能扩展。尝试扩展模型支持。虽然为“本地 Gemma 4”支持修改了超时设置，但 PR 已被合并，可能意味着初步支持就绪。
    - **状态**: 已合并
    - **链接**: `google-gemini/gemini-cli PR #27179`

8.  **[#27409] Fix/performance test timeout (修复性能测试超时)**
    - **重要性**: **中**。工程优化。修复了性能测试中可能出现的超时问题，确保 CI/CD 流程的稳定性。
    - **状态**: 开放中
    - **链接**: `google-gemini/gemini-cli PR #27409`

9.  **[#24429] Add a failing behavioral eval for parallel replace (添加失败的并行替换行为评估测试)**
    - **重要性**: **中**。质量保障。新增了一个能够复现“并行写入同一文件”问题的自动化测试，这有助于开发者定位并修复潜在的资源竞争Bug。
    - **状态**: 开放中
    - **链接**: `google-gemini/gemini-cli PR #24429`

10. **[#27505] Prevent extra spaces on width-0 CJK continuation cells (修复 CJK 字符渲染问题)**
    - **重要性**: **中**。国际化修复。修复了 CJK（中日韩）字符在终端输出时因为字符宽度计算问题导致的多余空格，提升国际化用户的使用体验。
    - **状态**: 开放中
    - **链接**: `google-gemini/gemini-cli PR #27505`

## 功能需求趋势

从本周的 Issues 中，可以提炼出社区最关注的几大功能方向：

- **Agent 子代理系统优化**：这是当前最核心的议题。社区强烈要求解决子代理的 **主动性不足**（不主动调用）、**行为不准确**（误报成功、忽视配置）以及**稳定性问题**（挂起、崩溃）。
- **基础能力增强**：用户期望 Agent 拥有更强的**代码理解能力**，例如通过 **AST 感知** 来更精准地读取、搜索和映射代码库，而不是依赖简单的文本匹配。
- **可配置性与可控性**：用户明确要求 Agent 行为能通过 `settings.json` 等配置文件进行精确控制，例如代理的**最大轮次、是否启用交互式Shell、以及对特定子代理的权限控制**。Browser Agent 忽略配置的 Bug 是当前焦点。
- **安全与隐私**：随着 Auto Memory 等功能的出现，社区开始关注**敏感信息（如密钥）的删改与日志安全**，以及如何防止 Agent 执行**破坏性操作**。
- **本地模型支持**：对类似 **Gemma 4** 等本地模型的支持需求开始出现，预示着社区对离线或私有化部署的潜在兴趣。

## 开发者关注点

社区开发者的反馈集中体现了以下几个主要痛点和高频需求：

- **Agent 自动决策机制频繁误判**：用户普遍反映 Agent 在“是否使用子代理”、“使用什么工具”、“在哪里创建文件”等决策上表现不佳，常常选择错误的路径或不听话，导致用户需要频繁手动干预或进行指令微调。
- **回收流程质量不完整**：子代理在任务被中断或达到上限后，其状态报告机制存在缺陷，导致“任务成功”的假象，这严重影响了用户对 Agent 完成度的信任。
- **基础设施兼容性滞后**：在较新的技术栈（如 Wayland 显示服务器）和特定使用场景（如从外部编辑器退出、终端尺寸变化）下，Agent 的兼容性和渲染表现不佳，影响了日常开发的流畅体验。
- **安全机制滞后**：当前的 Auto Memory 等功能的“安全”措施是在内容进入模型上下文之后才执行的（如删改密钥），开发者认为这种“事后处理”的方式不够安全，期望能在内容摄入前就进行确定性删改。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 – 2026-06-01

## 📌 今日速览

- **v1.0.57-4 发布**：新增鼠标点击 diff 行选中功能，修复了 tmux 中 Ctrl+C 等组合键失效、@-mention 文件搜索忽略大小写等问题。
- **社区集中反馈 v1.0.56 升级后连续登录失效、复制无法正常工作**，多个 Issue 获得高关注，开发者正积极排查。
- **新功能提案活跃**：插件技能支持子文件夹、图片粘贴到对话、Esc 中断模型响应等需求热度上升。

## 🚀 版本发布

**v1.0.57-4**（最新版）

- **Added**: 鼠标点击 diff 行即可选中该行（diff mode）。
- **Improved**: `preToolUse` hook 报错时，现在会拒绝工具调用，而不再静默允许执行。
- **Fixed**:  
  - tmux 环境下 Ctrl+C 等组合键恢复正常。  
  - @-mention 文件搜索不再因大小写混合而区分大小写。

## 🔥 社区热点 Issues（Top 10）

### 1. #1632 – [area:plugins] 支持技能子文件夹以更好地组织
- **作者**: cathysull | 👍14 | 评论6
- **摘要**: 用户有超过 10 个自定义技能，平铺在 skills 目录下难以管理，希望支持子文件夹。
- **意义**: 点赞数最高，反映插件生态扩展后组织管理的刚需。  
- **链接**: [Issue #1632](https://github.com/github/copilot-cli/issues/1632)

### 2. #3529 – [triage] Copilot 无法审查 PR，报“encountered an error”
- **作者**: bellaura | 👍1 | 评论2
- **摘要**: 用户付费后，无论 CLI 还是 GitHub UI 请求 Copilot Review 均报错，无法使用。
- **意义**: 可能影响付费用户的体验，属于服务端问题，需紧急排查。  
- **链接**: [Issue #3529](https://github.com/github/copilot-cli/issues/3529)

### 3. #3600 – [area:sessions] [Critical Bug] 无法移除运行了近两个月的孤儿会话
- **作者**: erbanku | 评论2
- **摘要**: 会话列表出现无法清除的“孤儿”会话（已运行约2个月），影响正常使用。
- **意义**: Critical 标签，直接暴露会话管理缺陷。  
- **链接**: [Issue #3600](https://github.com/github/copilot-cli/issues/3600)

### 4. #2675 – [area:input-keyboard] 支持从剪贴板粘贴图片到对话
- **作者**: CaioFML | 👍5 | 评论2
- **摘要**: 希望能够在 CLI 对话中粘贴截图，提升交互效率。
- **意义**: 需求认可度高，体现用户对多模态输入的需求。  
- **链接**: [Issue #2675](https://github.com/github/copilot-cli/issues/2675)

### 5. #3605 – [area:input-keyboard, area:terminal-rendering] 多行复制时空格被截断
- **作者**: qwaz | 评论1
- **摘要**: 在新版 v1.0.57-4 中，鼠标拖拽多行文本后右键复制，行首行尾空格被丢失。
- **意义**: 直接影响日常复制操作，用户反馈精确且可复现。  
- **链接**: [Issue #3605](https://github.com/github/copilot-cli/issues/3605)

### 6. #3597 – [area:authentication] v1.0.56 升级后需反复登录
- **作者**: zhuzeyuan | 评论1
- **摘要**: 24 小时内被要求登录 8 次以上，两台电脑均遇到，恢复会话也需重新登录。
- **意义**: 严重影响工作流，且与版本升级强相关，属高优先级回归缺陷。  
- **链接**: [Issue #3597](https://github.com/github/copilot-cli/issues/3597)

### 7. #3586 – [area:platform-linux, area:input-keyboard] v1.0.49 起复制功能异常
- **作者**: zhzy0077 | 评论1
- **摘要**: Linux 下复制功能在 v1.0.49 后失效，回退到 v1.0.48 正常，附有截图。
- **意义**: 明确回归点，协助开发定位问题。  
- **链接**: [Issue #3586](https://github.com/github/copilot-cli/issues/3586)

### 8. #3609 – [triage] v1.0.56 起“已复制”但实际未复制
- **作者**: zhuzeyuan | 评论0
- **摘要**: 点击复制按钮提示“copied to clipboard”，但粘贴无内容，同样始于 v1.0.56。
- **意义**: 与 #3586 类似，同为复制相关回归，可能为同一根因。  
- **链接**: [Issue #3609](https://github.com/github/copilot-cli/issues/3609)

### 9. #3606 – [area:plugins] 新安装的插件技能需手动 `/skills reload` 才可用
- **作者**: billxc | 评论0
- **摘要**: 安装插件后，技能列表能显示但无法实际调用，必须执行 `/skills reload`。
- **意义**: 用户体验断点，预期应有自动刷新机制。  
- **链接**: [Issue #3606](https://github.com/github/copilot-cli/issues/3606)

### 10. #3607 – [area:input-keyboard] Esc 不能中断模型响应
- **作者**: billxc | 评论0
- **摘要**: 模型在流式输出时，按 Esc 无效，只能杀掉 CLI 进程才能停止。
- **意义**: 基本交互缺失，影响大模型使用中的控制体验。  
- **链接**: [Issue #3607](https://github.com/github/copilot-cli/issues/3607)

## 🔄 重要 PR 进展

过去 24 小时内无新合并或更新的 Pull Request。

## 🧭 功能需求趋势

从近期 Issue 中提炼出社区最关注的几个方向：

- **插件与技能管理**  
  支持子文件夹（#1632）、自动加载新插件（#3606）——反映插件生态扩展后的组织需求。
- **输入与终端交互增强**  
  图片粘贴（#2675）、Esc 中断（#3607）、多行复制保留空格（#3605）——用户期望更接近图形界面的操作体验。
- **会话与认证稳定性**  
  孤儿会话清理（#3600）、频繁重新登录（#3597）、会话恢复时模型加载失败（#3596）——稳定性问题突出。
- **编码与国际化支持**  
  文件编码被改为 UTF-8（#3604）、非 ASCII 字符被丢弃（#3601）——对非英语用户影响大。
- **平台兼容性与基础功能**  
  Linux 下复制失效（#3586）、tmux 组合键修复（v1.0.57-4）、Windows 1252 编码——多平台场景需持续优化。

## 🎯 开发者关注点

- **v1.0.56 升级后的连锁故障**  
  多个用户报告升级后出现重复登录、复制功能失效、会话无法加载等问题，开发者已发布 v1.0.57-4 修复部分，但复制相关 Issue 仍开放。
- **插件技能使用门槛**  
  安装插件后需手动 reload、缺少自动刷新，社区期望即装即用。
- **终端内模型控制**  
  无法用 Esc 中断模型生成、鼠标选中复制体验不佳，影响快速迭代工作流。
- **环境变量污染**  
  #3602 指出 SDK 注入 Git 安全配置到全局 `process.env`，可能导致用户项目构建异常，需关注潜在风险。
- **工作树（worktree）支持**  
  #2653 获得 4 个 👍，用户希望 CLI 能原生支持多工作树以并行处理多个任务。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 | 2026-06-01

## 今日速览
过去 24 小时，Kimi Code CLI 社区活跃度显著上升，共产生 11 个新 Issue 和 2 个 Pull Request。最受关注的是 **OpenAI 兼容 API 需求**（#2208）和 **v1.46 版本登录失败 Bug**（#2403），同时多项针对 Tool Call 参数编码、子 Agent 超时等问题正在修复中。社区对增强 `thinking` 窗口大小、增加 `/goal` 自主任务命令等期望强烈。

---

## 社区热点 Issues（10 条最值得关注）

### 1. #2208 [enhancement] 希望能提供 OpenAI 兼容 API 以便在 Cursor 中使用
- **作者**：janeza2  
- **更新**：2026-05-31  
- **评论**：4 👍0  
- **链接**：[Issue #2208](https://github.com/MoonshotAI/kimi-cli/issues/2208)  
- **重要性**：用户希望在 Cursor 等 IDE 中直接使用 Kimi K2.6 模型，但需要 OpenAI 兼容接口。这是目前社区呼声最高的功能需求，对扩展生态至关重要。

---

### 2. #2403 [bug] 升级到 v1.46 后登录失败
- **作者**：AmooEbrahim  
- **更新**：2026-05-31  
- **评论**：2 👍0  
- **链接**：[Issue #2403](https://github.com/MoonshotAI/kimi-cli/issues/2403)  
- **重要性**：影响刚升级用户的正常使用，可能为回归 Bug。发生在 Linux 6.14 系统上，需紧急排查。

---

### 3. #2410 [bug] Linux 下 CLI 输入异常
- **作者**：scchy  
- **更新**：2026-05-31  
- **评论**：1 👍0  
- **链接**：[Issue #2410](https://github.com/MoonshotAI/kimi-cli/issues/2410)  
- **重要性**：v1.46.0 在 Linux 6.8 上执行需要 sudo 的命令时出现异常，可能涉及终端交互兼容性。

---

### 4. #2384 [bug] 大 Context 下频繁 ConnectTimeout，且 httpx 超时不可配置
- **作者**：1690834643  
- **更新**：2026-05-31  
- **评论**：1 👍0  
- **链接**：[Issue #2384](https://github.com/MoonshotAI/kimi-cli/issues/2384)  
- **重要性**：当 session context 超过 120k tokens 后，每个请求都可能超时。用户期望能自定义 connect_timeout 参数，影响长会话场景。

---

### 5. #2413 [bug] 重启 kimi cli 后自动发送历史图片，污染会话
- **作者**：d951092367  
- **更新**：2026-06-01  
- **评论**：0 👍0  
- **链接**：[Issue #2413](https://github.com/MoonshotAI/kimi-cli/issues/2413)  
- **重要性**：新发现的会话污染 Bug，重启后 Web 端发送的历史图片被自动带入 CLI 会话，导致上下文混乱。

---

### 6. #2412 [bug] `kimi acp` 命令无响应
- **作者**：HYPERVAPOR  
- **更新**：2026-05-31  
- **评论**：0 👍0  
- **链接**：[Issue #2412](https://github.com/MoonshotAI/kimi-cli/issues/2412)  
- **重要性**：v1.46.0 在 WSL2 上执行 `kimi acp` 后程序卡死，需要 Ctrl+C 中断，严重影响 Git 集成工作流。

---

### 7. #2411 [enhancement] 增加 thinking 行数窗口大小
- **作者**：dkhokhlov  
- **更新**：2026-05-31  
- **评论**：0 👍0  
- **链接**：[Issue #2411](https://github.com/MoonshotAI/kimi-cli/issues/2411)  
- **重要性**：当前 thinking 窗口仅显示 2 行，用户难以跟踪模型推理过程。建议改为 5-10 行或提供配置选项，属于体验优化需求。

---

### 8. #2408 [bug] 前台子 Agent 超时默认 120s，但 schema 声称“无默认超时”
- **作者**：morphishk  
- **更新**：2026-05-31  
- **评论**：0 👍0  
- **链接**：[Issue #2408](https://github.com/MoonshotAI/kimi-cli/issues/2408)  
- **重要性**：文档与实现不一致，导致生产环境中子 Agent 意外提前超时。影响可靠性。

---

### 9. #2406 [bug] Tool Call 参数双重编码导致数组/字典参数解析失败
- **作者**：wintrover  
- **更新**：2026-05-31  
- **评论**：0 👍0  
- **链接**：[Issue #2406](https://github.com/MoonshotAI/kimi-cli/issues/2406)  
- **重要性**：影响 `SetTodoList`、`ExitPlanMode`、`StrReplaceFile` 等多个工具的正常调用，属于 API 兼容性 Bug。已有 PR #2407 提出修复方案。

---

### 10. #2405 [bug] 400 错误：包含 tool_calls 的消息后缺少对应的 tool 响应
- **作者**：thoughtworld  
- **更新**：2026-05-31  
- **评论**：0 👍0  
- **链接**：[Issue #2405](https://github.com/MoonshotAI/kimi-cli/issues/2405)  
- **重要性**：使用 K2.6 模型时，`tool_calls` 消息的后续没有跟上对应的 tool 响应，导致 API 400 错误。可能为模型生成错误或底层通信 Bug。

---

## 重要 PR 进展（2 条）

### #2409 [fix] 为 create_openai_client 添加默认 120s 超时
- **作者**：wintrover  
- **更新**：2026-05-31  
- **链接**：[PR #2409](https://github.com/MoonshotAI/kimi-cli/pull/2409)  
- **内容**：`create_openai_client()` 未传递 timeout 参数，使 SDK 默认使用 600s，在代理超时（如 300s）时造成客户端额外等待。PR 添加 120s 默认超时，提升失败响应速度。

---

### #2407 [fix] 修复 Moonshot API 中 Tool Call 参数双重编码问题
- **作者**：wintrover  
- **更新**：2026-05-31  
- **链接**：[PR #2407](https://github.com/MoonshotAI/kimi-cli/pull/2407)  
- **内容**：针对 Issue #2406，Moonshot API 返回的 `function.arguments` 中嵌套对象被双重 JSON 编码，导致 Pydantic 校验失败。PR 在解析外层 JSON 后，对仍为字符串的嵌套值进行二次解析，影响 `SetTodoList` 等工具。

---

## 功能需求趋势

从近期 Issue 中可以提炼出社区最关注的三个功能方向：

1. **第三方 IDE 集成**  
   - #2208 明确要求提供 OpenAI 兼容 API，以便在 Cursor 等工具中直接调用 Kimi 模型。社区希望能像使用 OpenAI API 一样无缝接入。

2. **用户体验与自定义能力**  
   - #2411 要求增大 thinking 窗口行数（或可配置）。  
   - #2384 要求 `connect_timeout` 等网络超时可配置。  
   - #2404（未在热点列出）提出 `/goal` 命令，用于实现无需重复确认的自主任务完成，类似 Codex 的 mission 模式。

3. **工具调用与模型稳定性**  
   - #2406、#2405、#2408 均涉及 tool_calls 和子 Agent 的可靠性问题，反映出社区对 Agent 工作流稳定性的高要求。预期后续版本将重点修复这些边缘情况。

---

## 开发者关注点

- **升级后的回归 Bug**：v1.46.0 带来的登录失败（#2403）、`acp` 命令无响应（#2412）、Linux 输入异常（#2410）成为开发者最头疼的痛处，建议团队尽快针对 WSL2 和特定 Linux 内核做兼容性测试。
- **较长 Session 的性能瓶颈**：大 Context 下 ConnectTimeout 频繁（#2384），且缺乏可调超时机制，直接影响深度任务体验。开发者希望 CLI 能提供更细粒度的网络控制。
- **会话状态污染**：重启 CLI 后自动发送历史图片（#2413）是合理但易被忽略的 Bug，可能导致敏感信息泄露或上下文混乱，需要优先修复。
- **Tool Call 兼容性**：双重编码和缺失 tool 响应等错误（#2406、#2405）影响 Code Agent 的可用性，尤其是与 Moonshot API 配合使用时，开发者依赖这些工具完成文件操作和计划模式，修复需求紧迫。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-06-01

## 今日速览
GPT 模型响应耗时波动、内存问题集中讨论持续升温；Gemma 4 工具调用在多引擎下仍存在兼容问题。  
PR 方面，MiniMax M3 支持、会话状态聚合、Windows 存储路径修复等多项修复已进入合并流程。  
社区对权限交互卡死、工具执行中断、SQLite 启动崩溃等问题反馈集中，开发者体验改善成为当前焦点。

---

## 社区热点 Issues

### 1. #29079 GPT Models 响应时间过长
- **评论/点赞**: 114 / 48  
- **重要性**: 用户报告 GPT-5.4 等模型响应时间从秒级到数分钟波动，影响日常使用。  
- **链接**: [Issue #29079](https://github.com/anomalco/opencode/issues/29079)

### 2. #20695 内存问题集中讨论（Memory Megathread）
- **评论/点赞**: 83 / 60  
- **重要性**: 项目方设立此议题统一收集内存泄漏报告，号召用户提供堆快照，社区参与度高。  
- **链接**: [Issue #20695](https://github.com/anomalco/opencode/issues/20695)

### 3. #20995 Gemma 4 (e4b) 通过 Ollama 调用时工具调用失败
- **评论/点赞**: 19 / 45  
- **重要性**: 模型返回 `tool_calls` 但 OpenCode 无法识别，导致流式工具调用完全失效。  
- **链接**: [Issue #20995](https://github.com/anomalco/opencode/issues/20995)

### 4. #21034 Gemma 4 系列（26B/31B）交互循环/失败
- **评论/点赞**: 17 / 18  
- **重要性**: 即使使用最新 tokenizer 和引擎补丁，`gemma-4-26b/31b` 仍无法在 OpenCode 中正常使用。  
- **链接**: [Issue #21034](https://github.com/anomalco/opencode/issues/21034)

### 5. #29786 Opus 4.8 在 dev 分支出现 bug
- **评论/点赞**: 16 / 3  
- **重要性**: 子代理返回异常消息，影响 dev 分支开发测试。  
- **链接**: [Issue #29786](https://github.com/anomalco/opencode/issues/29786)

### 6. #25940 TUI 终端启动即崩溃
- **评论/点赞**: 9 / 2  
- **重要性**: 打开 OpenCode 后整个终端会话崩溃，即使非 git 目录也出现，严重影响基础体验。  
- **链接**: [Issue #25940](https://github.com/anomalco/opencode/issues/25940)

### 7. #27436 权限请求无法正常选择
- **评论/点赞**: 8 / 2  
- **重要性**: 点击“Allow once”无反应，“Allow always”循环弹窗，“Reject”后无法提交反馈，会话卡死。  
- **链接**: [Issue #27436](https://github.com/anomalco/opencode/issues/27436)

### 8. #30070 Desktop MCP 面板显示为 0/0
- **评论/点赞**: 6 / 8  
- **重要性**: CLI 可正常列出 MCP 服务器，但桌面端实时同步状态为空，猜测为 sidecar 同步问题。  
- **链接**: [Issue #30070](https://github.com/anomalco/opencode/issues/30070)

### 9. #28011 编辑工具连续调用后频繁中断
- **评论/点赞**: 5 / 0  
- **重要性**: v1.15.x 升级后，对同一文件连续执行 `edit` 工具出现 `[Tool execution was interrupted]`，回归问题。  
- **链接**: [Issue #28011](https://github.com/anomalco/opencode/issues/28011)

### 10. #22813 思考块签名丢失导致多轮对话 API 错误
- **评论/点赞**: 3 / 10  
- **重要性**: 使用启用扩展思考的 Anthropic 模型时，多轮后因 `thinking` block 签名被修改而触发 API 错误。  
- **链接**: [Issue #22813](https://github.com/anomalco/opencode/issues/22813)

---

## 重要 PR 进展

### 1. #30162 新增 MiniMax M3 模型支持
- **状态**: OPEN  
- **内容**: 为 MiniMax 提供商添加 M3 模型（上游目录未收录前）。  
- **链接**: [PR #30162](https://github.com/anomalco/opencode/pull/30162)

### 2. #30155 修复子目录会话状态聚合
- **状态**: OPEN  
- **内容**: `GET /session/status` 之前只返回选中实例的状态，现在聚合子项目目录的运行状态。  
- **链接**: [PR #30155](https://github.com/anomalco/opencode/pull/30155)

### 3. #29666 强制存储路径格式一致（修复 Windows 会话列表为空）
- **状态**: OPEN  
- **内容**: 所有 session/project 路径统一为前向斜杠，解决 Windows 下 `\` 与 `/` 不匹配导致的列表空。  
- **链接**: [PR #29666](https://github.com/anomalco/opencode/pull/29666)

### 4. #30153 模型处理前保存文件附件到磁盘
- **状态**: OPEN  
- **内容**: 用户上传图片/PDF 且模型不支持该模态时，附件不会被丢失，先存盘再通知用户。  
- **链接**: [PR #30153](https://github.com/anomalco/opencode/pull/30153)

### 5. #30051 新版 TUI 子代理行显示优化
- **状态**: OPEN  
- **内容**: 完成的子代理渲染为紧凑 `✓` 行，保留进行中的 spinner 和活动子行，提升可读性。  
- **链接**: [PR #30051](https://github.com/anomalco/opencode/pull/30051)

### 6. #29901 新增 Snowflake Cortex 提供商
- **状态**: OPEN  
- **内容**: 提供 OpenAI 兼容接口的完整集成，包括工具调用支持与文档。  
- **链接**: [PR #29901](https://github.com/anomalco/opencode/pull/29901)

### 7. #29928 修复桌面端 Git Diff 全文件上下文折叠
- **状态**: OPEN  
- **内容**: 桌面端 Git Changes 收到的补丁包含全文件上下文，导致 diff 视图渲染整个文件，现改为折叠。  
- **链接**: [PR #29928](https://github.com/anomalco/opencode/pull/29928)

### 8. #30145 修复 ACP 协议中 session/cancel 被拒绝
- **状态**: OPEN  
- **内容**: ACP 代理之前错误返回 `UnsupportedOperationError`，导致客户端无法取消正在运行的 turn。  
- **链接**: [PR #30145](https://github.com/anomalco/opencode/pull/30145)

### 9. #26861 修复长会话中旧消息消失
- **状态**: OPEN  
- **内容**: 引入懒加载滚动，滑动到顶部时自动加载更多历史消息，防止消息丢失。  
- **链接**: [PR #26861](https://github.com/anomalco/opencode/pull/26861)

### 10. #12633 TUI 自动接受编辑权限模式
- **状态**: OPEN  
- **内容**: 新增 `permission_auto_accept_toggle` 快捷键（默认 Shift+Tab），自动接受编辑请求，其他权限仍提示。  
- **链接**: [PR #12633](https://github.com/anomalco/opencode/pull/12633)

---

## 功能需求趋势

- **模型兼容扩展**：社区持续要求支持新模型（MiniMax M3、Snowflake Cortex），同时对 Gemma 4、GPT、Opus 的兼容性修复呼声很高。  
- **权限交互体验**：多个 Issue 和 PR 聚焦权限提示的易用性，包括 YOLO 模式（#9070）、自动接受编辑（#12633）、以及当前权限 UI 卡死（#27436）的修复。  
- **性能与稳定性**：GPT 响应耗时、内存泄漏、工具执行中断、SQLite 启动崩溃成为高频关注点。  
- **MCP 集成**：桌面端 MCP 面板与 CLI 不同步（#30070）、配置后会话丢失（#30151）暴露出 MCP 状态同步机制的不足。  
- **UI 改进**：新版 TUI 重写后，社区要求恢复“在外部编辑器中打开”功能（#30135），并希望优化子代理展示、长会话消息加载等。  
- **全局规则（Glob-based rules）**：Issue #4716 提议类似 `.gitignore` 的文件选择规则，已有 16 👍，但进展较慢。

---

## 开发者关注点

- **响应时间不可控**：GPT 模型有时秒级有时数分钟，严重影响信任度，社区希望 OpenCode 能提供超时或进度反馈。  
- **内存问题持续困扰**：虽然设立了集中讨论，但缺乏自动化堆快照采集工具，开发者需要手动操作。  
- **Gemma 4 系列兼容性差**：即使引擎打上补丁，工具调用和交互循环仍无法正常工作，社区期待官方提供官方的内测支持。  
- **v1.15.x 回归问题**：编辑工具频繁中断（#28011）、多轮思考块签名丢失（#22813）等回归让部分用户考虑回退版本。  
- **权限交互卡死**：点击“Allow once”无反馈、“Reject”无法提交原因，会话陷入死锁，影响所有用户。  
- **Windows 端问题**：存储路径格式（#29666）、终端崩溃（#25940）、Brew 构建失败（#29846）让 Windows 开发者体验较差。  
- **MCP 配置导致数据丢失**：多位用户报告配置 MCP 后重启桌面端，会话和项目全部消失（#30151、#30150），引发信任危机。  
- **新 TUI 缺失功能**：外部编辑器打开、输入框交互等尚未完善，部分老用户呼吁尽快补回。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

好的，这是为您生成的 Pi 社区动态日报。

---

# 2026-06-01 Pi 社区动态日报

## 今日速览

今日社区活跃度极高，主要集中在模型兼容性修复和核心 TUI 体验优化上。`openai-codex` 的“假死”问题 (#4945) 成为社区讨论焦点，同时多项针对 WSL、iTerm2 等特定环境的 Bug 修复也取得了进展。在功能方向上，社区对会话内模型切换的“临时性”以及跨平台兼容性的呼声日益高涨。

## 社区热点 Issues

1.  **`openai-codex` 交互式 TUI 假死问题** [#4945](https://earendil-works/pi Issue #4945)
    - **重要性：** 社区最热 Issue（50条评论），直接影响核心交互体验。用户在使用 `openai-codex` / `gpt-5.5` 时，TUI 界面会卡死在“Working...”状态，无任何输出或错误，只能强制退出。
    - **社区反应：** 大量用户确认遇到此问题，开发者已标记为 `inprogress` 并指派相关人员。这很可能是由于流式响应中断或资源释放不当导致。

2.  **Anthropic Opus 4.8 自适应思考模式请求失败** [#5223](https://earendil-works/pi Issue #5223)
    - **重要性：** 核心 API 兼容性问题。多轮对话中，使用 Claude Opus 4.8 的高推理强度模式时，会因 `thinking` 或 `redacted_thinking` 块处理不当导致 400 错误。
    - **社区反应：** 开发者正积极处理，这关系到对高端模型特性的支持，可能需要对 Anthropic SDK 的流式解析进行修复。

3.  **Qwen 3.7 Max 在 OpenRouter 上不可用** [#5117](https://earendil-works/pi Issue #5117)
    - **重要性：** 热门模型适配问题。用户反馈使用 Qwen 3.7 Max 模型时，OpenRouter 返回 400 错误，原因是 `developer` 角色未被 API 识别。
    - **社区反应：** 该 Issue 已关闭，表明开发者已意识到此问题，并可能通过修改消息角色（例如回退到 `system` 角色）来解决。

4.  **Windows 下 `bash` 工具会创建名为 `nul` 的文件** [#4920](https://earendil-works/pi Issue #4920)
    - **重要性：** 平台兼容性 Bug。在 Windows 上，`bash` 工具错误地将重定向目标 `nul` 创建为普通文件，而不是重定向到空设备。这会导致无法删除的垃圾文件。
    - **社区反应：** 该问题已修复并关闭。这体现了 Pi 在跨平台（特别是 WSL/Windows）方面的持续改进。

5.  **TUI 渲染 `web_search` 结果时崩溃** [#5266](https://earendil-works/pi Issue #5266)
    - **重要性：** 新版本（v0.78.0）的回归性 Bug。当 `web_search` 工具返回的结果缺少 `content` 数组时，TUI 直接崩溃。
    - **社区反应：** 该问题迅速被关闭，说明已得到快速修复。这提醒开发者在处理外部 API 响应时需加强数据健壮性校验。

6.  **429 重试策略忽略 `maxRetryDelayMs` 配置** [#4666](https://earendil-works/pi Issue #4666)
    - **重要性：** 用户体验和配置生效性问题。用户设置的 `retry.provider.maxRetryDelayMs` 上限被忽略，导致长时间静默等待。`Esc` 和 `/new` 命令也无法干净地恢复。
    - **社区反应：** 用户对此感到困扰，这是一个影响比较广泛的配置 Bug，可能导致工具在特定情况下“假死”。

7.  **贡献提案：自动检测亮/暗模式** [#1436](https://earendil-works/pi Issue #1436)
    - **重要性：** 经典的需求，虽已关闭但仍有参考价值。用户期望 Pi 能跟随系统主题自动切换亮暗色模式，无需手动设置。
    - **社区反应：** 虽然历史久远，但这种对细微用户体验的追求在开发者社区中很受欢迎，是提升工具“精致感”的重要方向。

8.  **MiniMax 在 OpenRouter 上不可用** [#5229](https://earendil-works/pi Issue #5229)
    - **重要性：** 与 Qwen 类似，是模型提供商适配问题。`developer` 角色在 MiniMax 模型上同样不被支持。
    - **社区反应：** 该问题已被识别，可能表明需要统一处理 OpenRouter 上部分模型对 `developer` 角色的兼容性问题。

9.  **贡献提案：多选列表 UI 组件** [#5025](https://earendil-works/pi Issue #5025)
    - **重要性：** 核心能力扩展。用户需要一个 `multi-select-list` 组件，以便在自定义扩展中实现多选操作（如选择多个模型）。
    - **社区反应：** 虽然处于关闭状态，但这反映了社区对增强 Pi 扩展系统 UI 能力的需求，使其能开发更复杂的交互逻辑。

10. **Git 分支名在 WSL `/mnt` 目录下不刷新** [#5052](https://earendil-works/pi Issue #5052)
    - **重要性：** 极其影响开发流的小问题。在 WSL 中操作 Windows 目录下的仓库时，页脚的 Git 分支名不更新。
    - **社区反应：** 用户已自行提出修复 PR，表明该问题对 WSL 用户群体影响较大，社区贡献者已主动介入解决。

## 重要 PR 进展

1.  **PR #5270：模型与思考等级切换改为“临时”** [查看](https://earendil-works/pi PR #5270)
    - **功能：** 默认将 `setModel()` 等操作改为仅对当前会话有效，而非覆盖全局配置。
    - **重要性：** 满足了社区长期以来的诉求，使 /new、/fork 等操作后的模型切换更加灵活，避免意外更改全局设置，是本次日报中最重要的体验改进之一。

2.  **PR #5269：为 Coding Agent 添加 `ctx.isInteractive` API** [查看](https://earendil-works/pi PR #5269)
    - **功能：** 允许扩展程序区分自身运行在 TUI 模式还是 RPC 模式。
    - **重要性：** 解决了扩展开发中的一个关键痛点。修复了RPC模式下的回归Bug，让扩展能根据运行环境做出不同表现。

3.  **PR #5268：修复 TUI 光标在窗口失焦时不“空心”** [查看](https://earendil-works/pi PR #5268)
    - **功能：** 默认启用硬件光标，使得当终端窗口失去焦点时，光标会变为空心。
    - **重要性：** 一个细小的用户体验改进，但对多窗口工作的开发者来说非常有意义，能让用户直观感知当前窗口是否活跃。

4.  **PR #5264：修复 WSL `/mnt` 仓库的 Git 分支脚标** [查看](https://earendil-works/pi PR #5264)
    - **功能：** 通过间隔轮询来解决 WSL 下 Git 分支名不更新的问题。
    - **重要性：** 社区贡献者为报告已久的 WSL 特定 Bug 提供了解决方案，体现了社区的积极作用。

5.  **PR #5235：修复 TUI 覆盖层聚焦问题** [查看](https://earendil-works/pi PR #5235)
    - **功能：** 当一个覆盖层（overlay）打开时，确保输入焦点正确停留在覆盖层上，而非背后的编辑器。
    - **重要性：** 修复了一类常见的 TUI 交互 Bug，提升了大量使用弹窗和菜单的交互稳定性。

6.  **PR #4651：在 Windows 上自动下载便携版 Git Bash** [查看](https://earendil-works/pi PR #4651)
    - **功能：** 实验性地为 Windows 环境自动下载 Git Bash，但会占用约 350MB 空间。
    - **重要性：** 这是一个仍在讨论中的重大改动，旨在改善 Windows 开箱即用体验，但下载大小成为潜在的分歧点，开发者持审慎态度。

7.  **PR #5254：用 `util.styleText` 替换 `chalk` 库** [查看](https://earendil-works/pi PR #5254)
    - **功能：** 移除第三方依赖 `chalk`，改用 Node.js v20+ 内置的 `util.styleText` 来实现终端颜色。
    - **重要性：** 符合当前前端工具链去重型化的趋势（如 e18e 运动），有助于减少依赖数量和包体积。

8.  **PR #5233：修复 Kitty 图像在 WezTerm 中的渲染** [查看](https://earendil-works/pi PR #5233)
    - **功能：** 修复了 Kitty 图像协议在 WezTerm 下只显示顶部一条的 Bug。
    - **重要性：** 解决了特定终端模拟器的兼容性问题，体现了对多平台支持的一贯重视。

9.  **PR #5262：新增 `anthropic-vertex` 提供商** [查看](https://earendil-works/pi PR #5262)
    - **功能：** 为 Google Cloud Vertex AI 平台上的 Claude 模型提供了一个原生内置提供商。
    - **重要性：** 扩展了 Pi 对 Claude 模型访问的渠道，为使用 GCP 的企业用户提供了更便捷、更合规的选项。

10. **PR #5221：修复 OpenRouter 推理指令角色** [查看](https://earendil-works/pi PR #5221)
    - **功能：** 解决 OpenRouter 在处理推理模型时，系统提示消息角色错误的问题，将其改为 `system`。
    - **重要性：** 修复了影响多个模型可用性的关键 Bug，与 Issue #5117 和 #5229 直接相关，是本次更新中最核心的兼容性修复之一。

## 功能需求趋势

- **模型兼容性与适配：** 社区对于新模型（如 Qwen 3.7 Max, MiniMax）和高端模型（如 Opus 4.8）的快速适配有极高要求，尤其关注 OpenAI、Anthropic、OpenRouter 等主要提供商的兼容性修复。
- **用户体验与界面优化：** 除了 Bug 修复，微小的交互改进（如光标状态、快捷键配置、主题跟随系统）受到高度关注，体现了用户对“精致感”的追求。
- **平台兼容性：** WSL 和 Windows 环境的特定问题持续成为热点。开发者正通过社区贡献和官方修复双管齐下，努力解决跨平台体验不一致的问题。
- **性能与资源管理：** 大型会话的加载性能（`--resume` 时的 OOM 问题）和资源占用（如 Git Bash 的大小）被反复提及，表明用户群正面临更复杂的项目场景。
- **安全与鲁棒性：** 对无限循环的保护（Agent Loop）、扩展加载失败不崩溃、错误重试策略等问题开始得到更多关注，表明工具正在从“可用”向“可靠”演进。

## 开发者关注点

- **错误处理不友好：** 多个 Issue 提到，当工具遇到问题时（如 API 400 错误、工具调用超时），缺乏清晰、可操作的错误提示，导致用户困惑。
- **配置管理混乱：** 模型、思考等级等配置的作用域（全局 vs 会话）不明确，是用户反馈中的高频痛点。同时，部分配置项（如 `retry.provider.maxRetryDelayMs`）未按预期工作。
- **跨平台体验割裂：** WSL、原生 Windows、不同终端模拟器（如 iTerm2, WezTerm) 之间，核心体验和功能表现存在显著差异，开发者需要在多种环境下不断进行兼容性调试。
- **缺乏监控与诊断工具：** 用户希望有类似会话活动热力图、Token 消费统计等功能，以更好地理解和管理自己的使用情况和工作流程。
- **文档与沟通缺失：** 有 Issue 抱怨，即使提交了详细的 Bug 报告和修复方案（如 PR），也未得到维护者的回应。这表明社区贡献流程和沟通渠道有待优化。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

好的，以下是为您生成的 2026-06-01 Qwen Code 社区动态日报。

---

# Qwen Code 社区动态日报 — 2026-06-01

## 今日速览

今日 Qwen Code 发布了 v0.17.0-nightly 版本，并修复了对话压缩（rewind）中的一个 Bug。社区焦点主要集中在 **<qwen serve> daemon 服务** 的 HTTP/SSE 接口补齐、**MCP 稳定性**以及 **OpenTelemetry 可观测性** 的全面增强上。此外，新模型支持（MiniMax-M3）和 **OOM 自动诊断** 的 PR 也引发了广泛关注。

## 版本发布

- **v0.17.0-nightly.20260601.1c48e4121**
  - **主要内容**: 常规 nightly 版本发布。
  - **修复**: 修复了 `fix(rewind)` 中一个在对话中途压缩时可能误报“compressed turn”错误的问题。
  - [查看发布详情](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.0-nightly.20260601.1c48e4121)

## 社区热点 Issues

1.  **[#4514] `<qwen serve>` daemon 能力缺口与优先级规划**
    - **摘要**: 详细列举了 `qwen serve` 中 HTTP/SSE 接口（如 `POST /session/:id/prompt`）需要补齐的功能，涉及 ACP 兼容性、会话生命周期管理等。
    - **重要性**: 这是决定 `qwen serve` 能否成为生产级服务的关键文档，为后续社区贡献提供了路线图。
    - **社区反应**: 10 条评论，社区开发者正在积极参与讨论技术方案。
    - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/4514)

2.  **[#4493]** **JetBrains Rider IDE 无法登录 Qwen Code**
    - **摘要**: 用户报告在 Rider 中通过 OAuth 登录时，页面无限重定向，无法绑定阿里云 Token。
    - **重要性**: 影响了 JetBrains IDE 用户的核心使用体验，属于严重的集成问题。
    - **社区反应**: 9 条评论，问题已被标记，社区和开发者正在排查重定向逻辑。
    - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/4493)

3.  **[#3881]** **本地部署 Qwen3.6-27B 模型首次提问持续返回 `/` 直到 Token 耗尽**
    - **摘要**: 用户在调用本地模型时，模型持续输出 `/` 符号，直至达到 Token 上限。
    - **重要性**: 严重阻碍了用户使用本地模型的体验，可能与模型采样参数或客户端预处理逻辑有关。
    - **社区反应**: 7 条评论，问题已关闭，但讨论中提供了多种排查思路。
    - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/3881)

4.  **[#4663]** **请求增加 MiniMax-M3 模型支持并优化选择 UI**
    - **摘要**: 用户希望在 API Key 配置流程中，增加 MiniMax-M3 模型选项，并将文本输入改为复选框多选界面。
    - **重要性**: 反映了社区对新模型和更友好 UI 的实时需求。
    - **社区反应**: 6 条评论，社区对该提议表示支持。
    - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/4663)

5.  **[#4554]** **功能请求：为 `<qwen serve>` daemon 添加 OpenTelemetry 支持**
    - **摘要**: 提议为 `qwen serve` 的 daemon 进程添加端到端的 OpenTelemetry 追踪，覆盖 HTTP 路由、会话生命周期、桥接队列等。
    - **重要性**: 补全了服务模式下的可观测性缺口，对运维和调试至关重要。
    - **社区反应**: 4 条评论，开发者已提出具体实现方案。
    - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/4554)

6.  **[#4609]** **运行本地模型时出现 DOMException 错误**
    - **摘要**: 用户在 v0.16.2 版本中，连接本地 Ollama 模型进行提问时，报错 `[API Error: Value of "this" must be of DOMException]`。
    - **重要性**: 阻止用户正常使用本地模型，属于关键 Bug。
    - **社区反应**: 4 条评论，问题已关闭，可能已通过其他修复解决。
    - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/4609)

7.  **[#4641]** **Windows 环境下 MCP 连接不稳定**
    - **摘要**: 用户在 Windows 10 上每次启动 Qwen Code 后，已配置的 8 个 MCP Server 可用数量不定（3-5 个），连接不稳定。
    - **重要性**: MCP 是 Qwen Code 的核心扩展能力，其稳定性问题在 Windows 上尤为突出。
    - **社区反应**: 1 条评论，这是一个需要优先解决的环境兼容性问题。
    - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/4641)

8.  **[#4476] [PR]** **为 AUTO 模式添加拒绝原因可见性和上限**
    - **摘要**: 该 PR 为 AUTO 模式增加了结构化的拒绝原因边界、用于分类器拦截的 PermissionDenied Hook，以及累积拒绝上限。
    - **重要性**: 提升 AUTO 模式的安全性和可解释性，帮助用户理解模型为何拒绝操作。
    - **社区反应**: 这是一个活跃的 PR，社区正在跟进讨论。
    - [查看 Pull Request](https://github.com/QwenLM/qwen-code/pull/4476)

9.  **[#4650] [PR]** **修复 `/memory` 开关状态持久化问题**
    - **摘要**: 该 PR 修复了 `/memory` 对话框关闭后重新打开，之前设置的开关状态会恢复默认的问题。
    - **重要性**: 解决了影响用户配置体验的直观问题。
    - **社区反应**: 作为一个 Bug 修复，受到用户关注。
    - [查看 Pull Request](https://github.com/QwenLM/qwen-code/pull/4650)

10. **[#4494]** **侧边查询忽略用户配置的输出语言**
    - **摘要**: 报告指出侧边查询（如 recap、title 等）会忽略用户设置的输出语言偏好（例如中文），使用英语输出。
    - **重要性**: 影响多语言用户的使用体验细节。
    - **社区反应**: 1 条评论，问题描述清晰。
    - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/4494)

## 重要 PR 进展

1.  **[#4655]** **Web Shell UI 重大改进与虚拟滚动**
    - **内容**: 对 Web Shell 进行全方位 UI 改进，包括修复子 Agent 渲染，并引入 `@tanstack/react-virtual` 虚拟滚动技术以优化长会话性能。
    - **链接**: [查看 Pull Request](https://github.com/QwenLM/qwen-code/pull/4655)

2.  **[#4545]** **改进钩子匹配器信息展示**
    - **内容**: 更新钩子管理视图，先展示匹配器（Matcher）分组，再显示分组内的处理器，使逻辑更清晰。
    - **链接**: [查看 Pull Request](https://github.com/QwenLM/qwen-code/pull/4545)

3.  **[#4654]** **核心功能：内存压力自动诊断转储**
    - **内容**: 当检测到内存压力时，自动将诊断信息写入磁盘，以便在 OOM 崩溃后定位问题。
    - **链接**: [查看 Pull Request](https://github.com/QwenLM/qwen-code/pull/4654)

4.  **[#4656]** **添加项目级 MCP 配置及待审批状态**
    - **内容**: 新增项目级 `.mcp.json` 发现和待审批（pending-approval）状态，增强 MCP 的安全管理。
    - **链接**: [查看 Pull Request](https://github.com/QwenLM/qwen-code/pull/4656)

5.  **[#4572]** **强化 AUTO 模式的自我修改检查**
    - **内容**: 加强对 AUTO 模式下修改配置、指令等高危操作的权限检查，防止绕过分类器。
    - **链接**: [查看 Pull Request](https://github.com/QwenLM/qwen-code/pull/4572)

6.  **[#4647]** **修复 Linux 下粘贴图片问题**
    - **内容**: 使用系统原生工具（wl-paste/xclip）替换 Node.js 原生模块，以修复在 WSL2+Wayland 环境下的图片粘贴 Bug。
    - **链接**: [查看 Pull Request](https://github.com/QwenLM/qwen-code/pull/4647)

7.  **[#4563]** **重构 `<qwen serve>` 服务，提取工作区服务**
    - **内容**: 将 `HttpAcpBridge` 重命名为 `AcpSessionBridge`，并提取出 `DaemonWorkspaceService`，分离会话和工作区职责，优化架构。
    - **链接**: [查看 Pull Request](https://github.com/QwenLM/qwen-code/pull/4563)

8.  **[#4653]** **核心功能：支持可配置的 Agent 忽略文件**
    - **内容**: 新增支持 `.agentignore` 和 `.aiignore` 等配置文件，让用户更方便地控制 AI 可以访问的文件。
    - **链接**: [查看 Pull Request](https://github.com/QwenLM/qwen-code/pull/4653)

9.  **[#4662]** **修复：将子模块包含进文件搜索**
    - **内容**: 修复了 Git 子模块中的文件无法被文件爬虫找到的问题，现在 `git ls-files` 会递归搜索子模块。
    - **链接**: [查看 Pull Request](https://github.com/QwenLM/qwen-code/pull/4662)

10. **[#4661] / [#4659]** **Telemetry: 为每次交互生成独立的 TraceId**
    - **内容**: 为每次用户提示（prompt）生成全新的 TraceId，替代之前基于会话 ID 推导的固定 TraceId，使链路追踪更清晰准确。
    - **链接**: [查看 Pull Request](https://github.com/QwenLM/qwen-code/pull/4661)

## 功能需求趋势

- **Daemon 服务能力完善**: 围绕 `<qwen serve>`，社区强烈要求补齐 HTTP/SSE 接口、完善 OpenTelemetry 可观测性、日志功能和更全面的会话管理能力。
- **IDE 集成与 OAuth 认证**: JetBrains IDE（特别是 Rider）的登录和认证问题频发，是当前社区最痛点的集成问题，对认证流程的稳定性需求极高。
- **新模型与 API Key UI**: 对 MiniMax-M3 等新模型的需求旺盛，同时用户渴望更现代化、更易用的 API Key 配置界面（如复选框代替文本输入）。
- **可观测性与 Telemetry**: OpenTelemetry 的实现和对齐工作持续进行，社区和开发者都在致力于让 Qwen Code 的运行状态可视化、可调试。
- **内存与性能优化**: 长对话和模型调用导致的 OOM 问题是核心痛点，推动社区提出自动内存诊断转储等实用方案。

## 开发者关注点

- **IDE 登录认证**：JetBrains Rider 等 IDE 的 OAuth 登录流程存在死锁，严重影响了开发者的正常使用，是最急需解决的认证问题。
- **MCP 稳定性**: 特别是 Windows 平台下，MCP Server 连接不稳定、跨会话不一致的问题，是开发者在扩展功能时遇到的首要障碍。
- **模型兼容性与 Token 错误**：本地部署的模型（如通过 Ollama）容易出现各种 Token 耗尽或不合理的输出（如连续输出 `/`），说明客户端与本地模型的交互容错性有待提升。
- **任务/UI 残留**: 部分 UI 上完成的任务状态未能及时清除，影响界面整洁度，虽不严重但干扰了日常使用体验。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报 | 2026-06-01

## 📋 今日速览

项目正式更名为 **CodeWhale**，v0.8.48 版本已发布，旧二进制名称进入淘汰过渡期。社区围绕**缓存命中率**、**Windows 输入崩溃**、**更名后配置迁移**等话题讨论热烈。同时，多个关键 PR 正在推进子代理 MCP 权限、i18n、TLS 自定义等基础设施改进。

## 🚀 版本发布

### v0.8.48 – “CodeWhale” 更名版本
- **主要内容**：项目正式从 `deepseek` / `deepseek-tui` 重命名为 **CodeWhale**。新版本同时提供 `codewhale` 和 `codewhale-tui` 二进制文件，旧名称作为兼容占位符（打印一行警告后转发），将在 v0.9.0 移除。
- **包含修复**：子代理存活性修复、前缀缓存稳定性、提供商/模型显示对齐、设置/测试隔离、Windows 发布启动器资产等。
- **🔗** [GitHub Release](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.48) | [更名文档](https://github.com/Hmbown/CodeWhale/blob/main/docs/REBRAND.md)

## 🔥 社区热点 Issues（10 条）

1. **#1120 缓存命中问题**（评论 21）
   - 用户反馈对同一项目修改后 `input_cache_miss` 比率存在问题，怀疑未在 v0.8.17 修复。
   - **🔗** [Issue #1120](https://github.com/Hmbown/CodeWhale/issues/1120)

2. **#1757 Ctrl+C 取消后恢复输入内容**（评论 11）
   - 请求在取消 API 请求后将已发送内容自动回填到输入框，减少终端复制粘贴不便。
   - **🔗** [Issue #1757](https://github.com/Hmbown/CodeWhale/issues/1757)

3. **#1969 更名后会话/技能是否保留**（评论 8）
   - 核心迁移问题：用户担心从 deepseek-tui 升级到 CodeWhale 后原有会话、技能丢失，文档未明确手动迁移方式。
   - **🔗** [Issue #1969](https://github.com/Hmbown/CodeWhale/issues/1969)

4. **#2261 TUI 崩溃导致输入泄漏到 PowerShell**（评论 4）
   - Windows 环境下进程崩溃后输入焦点丢失，后续按键被 PowerShell 当作命令执行，属严重安全性问题。
   - **🔗** [Issue #2261](https://github.com/Hmbown/CodeWhale/issues/2261)

5. **#1835 Windows IME 死锁**（评论 2，👍 1）
   - 使用中文输入法（搜狗）时输入框完全无响应，疑似 IME 组合事件死锁。
   - **🔗** [Issue #1835](https://github.com/Hmbown/CodeWhale/issues/1835)

6. **#2369 配置路径碎片化与静默迁移 Bug**（评论 2）
   - CodeWhale 在不同 OS 和 Cygwin 下配置文件路径不一致，且旧路径 `.deepseek` 到 `.codewhale` 的迁移逻辑有缺陷。
   - **🔗** [Issue #2369](https://github.com/Hmbown/CodeWhale/issues/2369)

7. **#2362 子代理无法访问 MCP 工具**（评论 4）
   - 通过 `agent_open` 启动的子代理无法使用父会话配置的 MCP 工具（Brave Search、Tavily 等），需增强工具继承机制。
   - **🔗** [Issue #2362](https://github.com/Hmbown/CodeWhale/issues/2362)

8. **#1681 中国用户无法使用网页搜索**（评论 2，👍 3）
   - 当前默认搜索提供商 Bing 在中国不可用，请求支持区域感知的搜索提供商配置。
   - **🔗** [Issue #1681](https://github.com/Hmbown/CodeWhale/issues/1681)

9. **#2309 `/statusline` 选择器未显示未配置项**（评论 5）
   - Picker 只显示已在 `config.toml` 中列出的状态项，无法在 UI 中发现所有可用芯片，降低可发现性。
   - **🔗** [Issue #2309](https://github.com/Hmbown/CodeWhale/issues/2309)

10. **#2264 系统性前缀缓存稳定性**（评论 2，👍 1）
    - 建议从最佳实践升级为系统性不变性约束，参考 deepseek-reasonix 的 99%+ 缓存命中架构，属 v0.9 规划。
    - **🔗** [Issue #2264](https://github.com/Hmbown/CodeWhale/issues/2264)

## 🔧 重要 PR 进展（10 条）

1. **#2476 修复 fork 迁移父级链接确定性**（Open）
   - 修复遗留迁移中因 `created_at` 相同而丢失父链接的 bug，并移除 `test_fork` 中的残留 `dbg!`。
   - **🔗** [PR #2476](https://github.com/Hmbown/CodeWhale/pull/2476)

2. **#2318 允许 `message_submit` Hooks 修改提交文本**（Open）
   - 实现 #1364 第一阶段：通过结构化 stdin/stdout 让 hooks 可以替换提交文本或阻止提交。
   - **🔗** [PR #2318](https://github.com/Hmbown/CodeWhale/pull/2318)

3. **#1865 新增 Pro Plan 模式**（Open）
   - 使用 deepseek-v4-pro 进行规划/审查，deepseek-v4-flash 执行，保留现有确认门控。
   - **🔗** [PR #1865](https://github.com/Hmbown/CodeWhale/pull/1865)

4. **#1893 可配置 TLS 证书验证**（Open）
   - 新增 `insecure_skip_tls_verify` 选项（默认 false），允许用户在有自签名证书的环境中禁用验证。
   - **🔗** [PR #1893](https://github.com/Hmbown/CodeWhale/pull/1893)

5. **#2048 TUI 实时显示 Shell 输出**（Open）
   - 在命令执行过程中实时增量输出，而不是等执行完成后才显示全部结果。
   - **🔗** [PR #2048](https://github.com/Hmbown/CodeWhale/pull/2048)

6. **#2113 独立滚动区域：对话与工具输出**（Open）
   - 将聊天区域拆分为上下两个独立滚动区域，支持各自滚动状态和缓存，避免干扰。
   - **🔗** [PR #2113](https://github.com/Hmbown/CodeWhale/pull/2113)

7. **#2239 i18n Phase 1-4b 集成**（Open）
   - 将 MessageId 翻译绑定到 47 个 UI 文件，修复 109 个编译错误，新增 1059 行本地化代码。
   - **🔗** [PR #2239](https://github.com/Hmbown/CodeWhale/pull/2239)

8. **#2242 类型化持久化工具权限规则**（Open）
   - 实现端到端类型化权限系统，支持按工具名/命令前缀/工作区路径等维度做 allow/deny/ask。
   - **🔗** [PR #2242](https://github.com/Hmbown/CodeWhale/pull/2242)

9. **#2256 工作空间 crate 合并：14→11**（Open）
   - 删除废弃的 `tui-core` crate，合并 `hooks` 与 `agent`，零行为变化，减小维护面。
   - **🔗** [PR #2256](https://github.com/Hmbown/CodeWhale/pull/2256)

10. **#2416 三层前缀缓存类型基础（Phase 1）**（已关闭）
    - 引入 `PinnedPrefix / FrozenPrefix / PrefixDrift` 类型词汇，为 v0.9 缓存最大化奠基。
    - **🔗** [PR #2416](https://github.com/Hmbown/CodeWhale/pull/2416)

## 📈 功能需求趋势

从近 30 条高活跃 Issue 中可提炼出社区最关注的四大方向：

1. **缓存与性能优化**（#1120、#2264、#2127、#2132）
   - 用户对缓存命中率、前缀缓存稳定性有强烈诉求，期望系统性地提升并可视化缓存状态。
2. **Windows 稳定性与输入体系**（#2261、#1835、#1779、#2369）
   - 频繁出现 TUI 崩溃导致输入泄漏、IME 死锁、shell 硬编码 cmd.exe 等问题，Windows 用户反馈集中。
3. **工具继承与权限模型**（#2362、#2303、#1186、#2328）
   - 子代理缺乏 MCP 工具访问、`allow_shell` 权限不一致、执行策略无法持久化，社区希望有更精细的权限体系。
4. **配置标准化与迁移**（#1224、#1969、#2369、#1901）
   - 更名后配置文件路径碎片化、遗留 `.deepseek` 迁移不透明、货币单位显示不一致，用户期望统一配置管理。

## 💡 开发者关注点

- **输入安全漏洞**：TUI 崩溃后输入泄漏到终端（#2261）是最严重问题，应优先修复。
- **中文输入法兼容性**：多个 Windows 用户报告 IME 死锁（#1835），需在事件循环中正确处理组合键。
- **子代理功能缺失**：高级用户通过 `agent_open` 构建复杂工作流，但子代理缺少父级工具和 hooks，降低了自动化能力。
- **缓存命中可观测性**：社区希望看到更多缓存指标（如#2264提出的可视化仪表），以便优化 prompt 结构。
- **更名后迁移文档不足**：用户担心升级后数据丢失，需要清晰的手动迁移指南和自动迁移工具。

---

*日报数据来源：GitHub Hmbown/CodeWhale Issues & PRs（截至 2026-06-01 12:00 UTC）*

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*