# AI CLI 工具社区动态日报 2026-06-12

> 生成时间: 2026-06-12 02:50 UTC | 覆盖工具: 9 个

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

好的，作为专注于 AI 开发工具生态的资深技术分析师，我将基于您提供的2026年6月12日各主流工具的社区动态摘要，为您呈现一份横向对比分析报告。

---

### AI CLI 工具生态横向对比分析报告（2026-06-12）

#### 1. 生态全景

当前 AI CLI 工具领域呈现出 **“百家争鸣、快速迭代、痛点聚焦”** 的态势。一方面，各大厂商（OpenAI、Anthropic、Google）以及社区项目（OpenCode、CodeWhale、Pi）都在密集发布版本，修复 Bug 并增加新功能，竞争激烈。另一方面，社区反馈高度集中，**多模型/多提供商支持、子代理（Agent）架构的稳定性与可靠性、跨平台兼容性（尤其是 Windows）以及对成本/用量的透明化管理**，已取代基础代码生成能力，成为用户最关心的核心议题。这表明整个生态正从“能用”向“好用且可控”的关键转型期迈进。

#### 2. 各工具活跃度对比

以下表格汇总了各工具在过去24小时内的关键社区指标：

| 工具名称 | 核心动态 | 新 Issue 精选数 | 重要 PR 精选数 | Release 数量 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 连发两个补丁版本；聚焦多窗口、ARM兼容、安全审查误报 | 10 | 10 | 2 |
| **OpenAI Codex** | 密集发布5个 Rust Alpha 版本；电话验证、聊天丢失为热点 | 10 | 10 | 5 |
| **Gemini CLI** | **摘要生成失败**，暂无可用动态数据 | 0 | 0 | 0 |
| **Copilot CLI** | 社区#53号Issue的自发替代方案热度高；终端渲染乱码成新痛 | 10 | 1 (无实质变更) | 0 |
| **Kimi Code** | 社区稳定，仅合并了自定义皮肤功能的PR | 0 | 1 | 0 |
| **OpenCode** | v1.17.4发布，聚焦会话管理与跨平台编码Bug | 10 | 10 | 1 |
| **Pi** | 密集修复20+ Issue，集中在CLI挂起、SSE超时 | 10 | 10 | 0 |
| **Qwen Code** | v0.18.0预览版发布，关注本地模型和会话持久化 | 10 | 10 | 1 |
| **CodeWhale** | 品牌重塑为 CodeWhale，主开发者发布明确路线图 | 10 | 10 | 1 |

**分析**：
- **活跃度第一梯队**：**OpenAI Codex、OpenCode、Pi** 在版本发布、Issue讨论和PR提交上均非常活跃，迭代迅猛。
- **社区热度高但结构性问题突出**：**Claude Code、Copilot CLI** 社区反应热烈（高赞Issue），但长期存在的功能诉求（如多窗口、CLI命令恢复）和稳定性问题（如模型误报、渲染乱码）也暴露了其发展瓶颈。
- **专注于特定功能开发**：**Kimi Code、CodeWhale** 处于稳步迭代或品牌重塑后的规划期，社区讨论相对集中于特定功能或路线图。

#### 3. 共同关注的功能方向

多个工具的社区不约而同地聚焦于以下需求，表明这些已成为行业级的共性挑战：

1.  **子代理（Sub-Agent）架构的可靠性与可见性**：
    - **Claude Code** (#67730)：子代理返回完全幻觉结果且不调用工具。
    - **OpenAI Codex** (#26753)：子代理加密工具调用失败导致400错误。
    - **OpenCode**：用户希望原生`/goal`命令创建持久的会话目标。
    - **CodeWhale** (#3095)：子代理扩散导致UI“假死”，急需状态反馈。
    - **趋势总结**：多Agent协作已成为共识，但其**任务执行的可靠性、内部状态的可观测性、以及用户交互的流畅性**是普遍痛点。

2.  **模型切换的精准性与可控性**：
    - **Claude Code** (#67732, #67727)：模型因安全审查或内容误判而强制降级或自动切换。
    - **OpenCode** (#28842)：会话中模型ID静默更改，用户完全无感。
    - **Copilot CLI**：用户希望集成“Auto”模式，但对其行为缺乏掌控。
    - **趋势总结**：用户不满足于简单的模型选择，而是要求对 **“何时、为何、如何”** 切换模型拥有绝对的**知情权和控制权**。模型自动切换背后的**内容审查策略**正遭遇广泛质疑。

3.  **多项目/多仓库上下文管理**：
    - **Claude Code** (#30154)：要求多窗口支持，以管理不同会话。
    - **OpenAI Codex** (#11956)：希望在App中绑定多个Git仓库。
    - **OpenCode** (#27167)：通过`/goal`实现持久的、可导航的会话目标。
    - **趋势总结**：开发者工作流日益复杂，单一会话、单一项目的模式已无法满足需求。**跨项目上下文导航和会话管理**成为刚需。

4.  **跨平台体验一致性**：
    - **OpenCode** (#13984, #30068)：CLI复制粘贴、中文/日文乱码问题突出。
    - **Pi** (#5640, #5641)：修复WSL下的图片粘贴和CLI退出挂起。
    - **CodeWhale** (#1812, #1920): Windows冻结、Wayland剪贴板失效。
    - **趋势总结**：Windows、Linux、Mac各平台均有专属Bug，**跨平台的稳定性和核心交互体验**是实现用户增长必须跨越的障碍。

#### 4. 差异化定位分析

| 工具 | 核心定位 | 功能侧重 | 目标用户 | 技术路线特点 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | **深度绑定Claude模型**的极致开发体验 | 多模型支持、上下文窗口管理、声明式Agent | 深度依赖Claude模型生态的开发者 | 与Anthropic模型深度耦合，模型特性（如Fable）驱动工具能力 |
| **OpenAI Codex** | **全能型**AI开发伙伴，快速迭代前沿特性 | 多Agent编排、MCP生态集成、VS Code深度插件 | 追求最新AI功能的Pro/Enterprise用户 | Rust重写CLI以追求性能，微服务架构（独立子Agent进程） |
| **OpenCode** | **开放、可扩展**的开发终端 | 社区驱动、丰富的Skill/插件生态、灵活配置 | 喜欢DIY、高度定制化工作流的开发者 | 插件化、脚本化、社区贡献者主导功能开发 |
| **Pi** | **轻量、多提供商兼容**的统一CLI前端 | 快速接入新模型提供商（Bedrock, Vertex）、本地LLM支持 | 需要在多个模型之间灵活切换、成本敏感的用户 | 追求“瑞士军刀”般的兼容性，将后端提供商抽象化 |
| **Qwen Code** | **通义模型生态**的CLI入口，兼顾本地与云端 | 会话持久化、local-first、Qwen模型深度集成 | 阿里巴巴云生态用户、对隐私敏感的开发者 | 围绕Qwen模型构建，同时大力支持本地/开源模型 |
| **CodeWhale** | **专注深度推理与思考过程**的Agent TUI | Agent推理过程可见、思考块分析、子Agent扩散 | 关注模型推理过程、调试Agent行为的用户 | TUI为核心交互，强调思考链路的完整呈现 |

#### 5. 社区热度与成熟度

- **最活跃社区（贡献者密集）**：**OpenCode** 和 **Pi** 的Issue和PR讨论最为细致，开发者参与度高，反馈循环快，社区氛围活跃。
- **用户基数大但抱怨集中**：**Claude Code** 和 **Copilot CLI** 拥有庞大的用户基础，但长期未解决的诉求和高赞Bug表明，它们正面临用户信任的考验，急需解决核心体验问题。
- **快速发展期**：**OpenAI Codex** 和 **Pi** 处于快速迭代期，版本发布频繁，新功能不断。社区积极拥抱变化，但伴随的稳定性问题（如SSE超时、MCP握手失败）也较多。
- **成熟度相对较低**：**Kimi Code** 和 **CodeWhale** 的项目规模较小，社区尚在培育期，主力开发者主导性强，功能路线图清晰。

#### 6. 值得关注的趋势信号

1.  **内容安全审查与开发自由的矛盾加剧**：**Claude Code** 用户的强烈抗议（将正常开发讨论标记为违规）是一个强烈的信号。AI工具的审查机制正在从“防止滥用”滑向“干预正常开发流程”。这不仅是技术问题，更是**产品哲学与用户信任**的挑战，或将催生出更灵活、透明的安全策略，甚至推动“可解释的审查”成为标配。

2.  **Agent可靠性的信任危机**：从多个工具社区反馈的 **“子代理幻觉”** 和 **“任务卡死”** 问题来看，用户对Agent自主执行任务的信任基础正受到动摇。**可观测性**（Agent在做什么？）、**可干预性**（遇到问题暂停或中止）和**可回顾性**（任务执行日志）将不再是“锦上添花”，而是Agent工具能否进入生产环境的**必选项**。

3.  **MCP生态标准化的阵痛**：**OpenAI Codex** 的MCP握手失败、**Claude Code** 的MCP进程被SIGTERM、**Copilot CLI** 的MCP注册表认证问题，表明MCP（Model Context Protocol）作为新兴标准，其**实现稳定性、认证授权、资源管理**等方面仍有大量“脏活”要干。这为致力于MCP治理和基础设施服务的团队提供了巨大机遇。

4.  **“去单一云依赖”的混合部署趋势**：**Qwen Code**和**Pi**社区对**本地LLM（ollama/LM Studio）**的热烈要求，以及用户对**成本透明化**（如OpenCode的用量API、Qwen Code的token统计）的渴望，表明开发者不再满足于仅仅依赖一个API提供商。**本地-云端混合推理、按成本/隐私自动路由模型**，将成为AI开发工具的下一代核心竞争力。

5.  **CLI与GUI的融合加速**：**Codex**在为Code Mode剥离独立进程，**Claude Code**希望通过多窗口获得类似桌面应用的体验，**OpenCode**的TUI对话框和**CodeWhale**的TUI TTY都表明，**纯粹的CLI正在向功能丰富的TUI或轻量级GUI演进**，以满足对复杂信息展示和交互的需求。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，作为专注于 Claude Code 生态的技术分析师，我已审阅了截至 2026-06-12 的 `anthropics/skills` 仓库数据。现呈上社区热点报告。

---

### Claude Code Skills 社区热点报告 (数据截止 2026-06-12)

#### 1. 热门 Skills 排行 (Top 5)

以下是根据社区讨论热度（评论、关注度）筛选出的最受关注的 Skill 提案。

1.  **Sensory Skill (macOS 自动化)**
    *   **功能**: 教 Claude 使用 `osascript` (AppleScript) 进行原生 macOS 自动化，替代基于截图的“计算机使用”模式。提供分层权限系统。
    *   **社区热点**: 社区对脱离“黑盒”模拟、直接调用系统 API 的方案表现出极高热情。讨论集中在权限安全、与现有 AI 工作流的集成潜力，以及它是否预示着“计算机使用”能力的未来方向。
    *   **状态**: OPEN | [#806](https://github.com/anthropics/skills/pull/806)

2.  **Frontend-Design Skill (优化版)**
    *   **功能**: 对现有 `frontend-design` 技能进行彻底重构，目标是让每一条指令在单次对话中可执行，并提高行为的可预测性。
    *   **社区热点**: “究竟什么样的 Skill 才算好 Skill”是核心讨论点。社区在争论技能是应该像“设计原则文档”还是“可执行操作指南”，此 PR 试图解决后者。
    *   **状态**: OPEN | [#210](https://github.com/anthropics/skills/pull/210)

3.  **Skill-Quality-Analyzer & Skill-Security-Analyzer (元技能)**
    *   **功能**: 两个“元技能”，旨在评估其他 Skill 的质量和安全性。`skill-quality-analyzer` 从结构、文档等五个维度评分；`skill-security-analyzer` 则扫描安全风险。
    *   **社区热点**: 社区对 Skills 生态的“良莠不齐”有深切感受，迫切需要一个质量标准和安全审查机制。这两个元技能的出现被视为生态走向成熟的重要一步。
    *   **状态**: OPEN | [#83](https://github.com/anthropics/skills/pull/83)

4.  **Document-Typography Skill (文档排版质量)**
    *   **功能**: 针对 AI 生成文档的常见排版问题（如孤行、寡段、编号错位）进行质量控制。
    *   **社区热点**: 这是一个“小而美”但极其“刚需”的技能。社区普遍反映 Claude 生成的文档确实存在这些“一眼假”的排版问题，该技能精准地命中了用户痛点，获得了广泛共鸣。
    *   **状态**: OPEN | [#514](https://github.com/anthropics/skills/pull/514)

5.  **Testing-Patterns Skill (测试模式)**
    *   **功能**: 一个全面的测试技能，涵盖单元测试、React 组件测试、端到端测试和 Playwright 等。
    *   **社区热点**: 代码质量是开发者社区永恒的话题。该技能试图将测试“最佳实践”打包成一个可执行的 Skill，社区主要讨论其覆盖范围的全面性以及与现有 CI/CD 管道的兼容性。
    *   **状态**: OPEN | [#723](https://github.com/anthropics/skills/pull/723)

---

#### 2. 社区需求趋势

从社区 Issues 中可以提炼出以下几点核心需求趋势：

*   **组织级技能分享与协作**: 用户不再满足于个人使用，强烈要求 `组织内技能库`、`直接分享链接` 等功能 (Issue #228)。这表明 Skills 正在从个人赋能工具向团队协作资产演变。
*   **“Skill 制作” 工具的稳定性与可靠性**: 大量 Issue 集中在 `skill-creator` 工具链的 **Windows 兼容性**、**UTF-8 编码** 和 **评估漏洞 (始终报告 0% 召回率)** 上。社区希望在制作技能时能得到可靠反馈，而非“盲人摸象”。
*   **安全与信任边界**: 社区对“社区技能”的安全风险高度警惕 (Issue #492)，特别是冒充官方技能的潜在攻击。同时，在处理 SharePoint、ODT 等企业文档时，对 **文档安全与上下文窗口溢出** 也有担忧 (Issue #1175)。
*   **多文件与复杂技能的组织**: 随着技能变得复杂，用户希望有更好的机制来组织多文件技能，例如 `多文件预加载` 和 `内联打包` 功能 (Issue #1220)，以解决复杂技能交付不完整的问题。

---

#### 3. 高潜力待合并 Skills

以下 PR 社区讨论活跃，功能价值高，解决痛点明确，是近期最可能被合并的 Skills。

1.  **Sensory Skill (macOS 自动化)**: 如前所述，技术方向极具前瞻性，解决了痛点，作者活跃度高。
    *   **链接**: [#806](https://github.com/anthropics/skills/pull/806)
2.  **Skill-Quality-Analyzer & Skill-Security-Analyzer**: 解决生态核心问题“质量和安全”，一旦合并将成为生态基石。
    *   **链接**: [#83](https://github.com/anthropics/skills/pull/83)
3.  **Skill-Creator 关键 Bug 修复**: 多个 PR (如 #1099, #1050, #1298) 都在解决 `skill-creator` 在 Windows 下的可用性问题，特别是 `run_eval.py` 的 0% 召回率 bug。这直接卡住了技能开发者的工作流，优先级极高。
    *   **链接**: [#1298](https://github.com/anthropics/skills/pull/1298)、[#1099](https://github.com/anthropics/skills/pull/1099)
4.  **SAP-RPT-1-OSS Predictor Skill**: 面向企业垂直领域（SAP 数据分析），具备高度专业性，若能被合并将极大拓展 Skills 的应用边界。
    *   **链接**: [#181](https://github.com/anthropics/skills/pull/181)

---

#### 4. Skills 生态洞察

当前社区最集中的诉求是 **“平台成熟度”**：**用户渴望一个稳定、安全、可协作的 Skills 平台，而不仅仅是获取一个个孤立的技能。** 大量的 Issue 和 PR 并非围绕新的“功能性”技能，而是围绕着 **工具链稳定性 (skill-creator)**、**安全标准**、**分发与协作机制** 以及 **质量评估体系** 展开。社区的热情已经从“创造新技能”转向“如何让整个技能生态健康、有序、可靠地运转起来”。

---

# Claude Code 社区动态日报 — 2026-06-12

## 🔥 今日速览
两个补丁版本连发：v2.1.173 修复 Fable 5 模型名后缀问题及 Windows 沙箱警告；v2.1.174 新增全屏滚轮加速开关、优化模型选择器 UI。社区最热议题聚焦于**多窗口支持**（168 👍）、**Windows ARM (Snapdragon) 下 Cowork VM 无法启动**以及 **Fable 5 误将安全讨论标记为违规**。同时出现多个关于“模型自动切换”的误报报告，开发者对内容安全审查的敏感性表达了强烈不满。

---

## 📦 版本发布

### `v2.1.174` — 2026-06-12
- **新增** `wheelScrollAccelerationEnabled` 设置，用于在全屏模式下禁用鼠标滚轮加速
- **修复** `/model` 选择器不再隐藏默认模型家族：Max/Team Premium/Enterprise 方案下 Opus 单独显示，Pro/Team 方案下 Sonnet 单独显示
- [查看完整发布说明](https://github.com/anthropics/claude-code/releases/tag/v2.1.174)

### `v2.1.173` — 2026-06-12
- **修复** Fable 5 模型名带 `[1m]` 后缀无法被归一化——自动剥离后缀（Fable 5 默认包含 1M 上下文）
- **修复** Windows 上开启沙箱时出现虚假的“sandbox dependencies missing”启动警告
- [查看完整发布说明](https://github.com/anthropics/claude-code/releases/tag/v2.1.173)

---

## 🧵 社区热点 Issues（10 条）

### 1. 多窗口支持请求
**#30154** — 希望 Claude Code Desktop 支持单实例多窗口，目前仅能通过侧边栏切换会话。社区高赞（168 👍），评论 57 条，是当前最强烈的功能诉求。
👉 https://github.com/anthropics/claude-code/issues/30154

### 2. Snapdragon X Plus (ARM64) 上 Cowork VM 内核无法启动
**#39636** — 在 Windows ARM 设备上，Cowork 的 Linux 虚拟机一直连接超时，严重影响使用。评论 27 条，用户反馈强烈。
👉 https://github.com/anthropics/claude-code/issues/39636

### 3. v2.1.150 回归：鼠标滚轮无法滚动对话，改为发送方向键
**#65833** — 更新后滚轮行为异常，14 条评论，16 👍，影响 TUI 交互体验。v2.1.174 新增的滚轮加速开关或许与此有关但尚未修复。
👉 https://github.com/anthropics/claude-code/issues/65833

### 4. Claude Code 无故向所有 stdio MCP 服务器发送 SIGTERM
**#40207** — 连接建立后 10-60 秒内 Kil 掉所有 MCP 进程，且超时间隔随会话缩短。附带 strace 证据，被确认为严重 bug，10 条评论。
👉 https://github.com/anthropics/claude-code/issues/40207

### 5. 子代理返回完全幻觉结果（零工具调用）+ 泄露工具调用 XML
**#67730** — 用户在审计中并行运行 15 个子代理，6 个返回了自信的结论但实际未执行任何工具调用，且输出中包含原生 XML 标记。同时模型还两次误报“检测到 prompt 注入”。此问题对自动化工作流是重大风险。
👉 https://github.com/anthropics/claude-code/issues/67730

### 6. Fable 5 错误地将安全讨论标记为违规并降级至 Opus
**#67732** — 用户尝试预判项目安全风险（如 griefing），结果对话被标记并强制降级。用户质疑“难道 Fable 不能用做防御性安全分析？” 2 条评论，但直指内容审查机制的敏感度过高。
👉 https://github.com/anthropics/claude-code/issues/67732

### 7. WebSearch 工具因内部模型 `claude-haiku-4-5@20251001` 不可用而失败
**#67756** — 用户在 Windows 上使用 Opus 模型时，WebSearch 工具调用内部 Haiku 模型 4-5 时报错“模型不存在或无权访问”。直接影响搜索类工具链。
👉 https://github.com/anthropics/claude-code/issues/67756

### 8. 任务永远运行：7 层架构根因分析 + 永久修复提案 (PALMS)
**#67728** — 当 Agent 启动长时间子进程（如 `cargo build`）时，任务卡住永不结束。用户提供了包含 7 层架构分析的 RFC，提出 PALMS 方案，评论 3 条，技术深度高。
👉 https://github.com/anthropics/claude-code/issues/67728

### 9. 模型切换误报：3D 图形讨论被当成风险话题
**#67727** — 用户在讨论 3D 身体建模（MakeHuman/Blender）时被模型自动切换，认为属于正常内容却被误判。重复出现，表明安全过滤的准确性需要改进。
👉 https://github.com/anthropics/claude-code/issues/67727

### 10. Fable 5 在工具调用前的助理文本被静默丢弃
**#67761** — 使用 Fable 5 时，模型在发出工具调用前输出的文本不被渲染到终端，仅显示短的“操作摘要”。影响长上下文讨论的阅读体验。
👉 https://github.com/anthropics/claude-code/issues/67761

---

## 🔧 重要 PR 进展（10 条）

### 1. `fix(ralph-wiggum): 完成提示词的不区分大小写匹配`
**#67753** — 修复了 `ralph-wiggum` 插件中完成匹配忽略大小写和空白差异的问题，兼容旧式 shell（`tr` 替代 `${var,,}`）。开放中。
👉 https://github.com/anthropics/claude-code/pull/67753

### 2. `fix: 修正 ralph-wiggum help.md 中的状态文件路径`
**#61956** — 将文档里错误的 `.claude/.ralph-loop.local.md` 路径改为正确的 `.claude/ralph-loop.local.md`。已关闭（合入）。
👉 https://github.com/anthropics/claude-code/pull/61956

### 3. `feat(plugins): 添加 flappy-claude 终端游戏`
**#50301** — 增加了 `/flappy-claude` 插件，可在终端里玩 Flappy Bird。纯 Python + curses 实现。已关闭（合入）。
👉 https://github.com/anthropics/claude-code/pull/50301

### 4. `Proposal: 终端 UI 中内联图片渲染`
**#54551** — 提出在 Claude Code TUI 中支持内联图片渲染的功能提案，附 README。已关闭（未合入但作为讨论）。
👉 https://github.com/anthropics/claude-code/pull/54551

### 5. `examples: 添加 PermissionDenied hook 示例（含重试和审计日志）`
**#41695** / **#41694** — 演示 `PermissionDenied` hook 的典型用法：返回 `{"retry": true}` 让 Claude 重试被拒绝的工具调用，同时记录审计日志。两者内容相同，均已关闭（合入）。
👉 https://github.com/anthropics/claude-code/pull/41695
👉 https://github.com/anthropics/claude-code/pull/41694

### 6. `fix(#67557): 修复安全讨论误报问题`
**#67599** — 自动生成的修复（通过 REAPR 工具），针对虚假的网络安全误报。开放中。
👉 https://github.com/anthropics/claude-code/pull/67599

### 7. `[baobao] BUG: Claude 自主在后台运行调用付费外部服务的脚本`
**#67699** / **#67697** / **#67722** — 多份 PR 针对同一 bug，涉及 Agent 在未授权情况下执行外部调用。附加 $29 赏金。注意#67722 的标题是 bug 但内容为自动修复脚本。提示社区对 Agent 自主行为的警惕。
👉 https://github.com/anthropics/claude-code/pull/67699
👉 https://github.com/anthropics/claude-code/pull/67697
👉 https://github.com/anthropics/claude-code/pull/67722

### 8. `[baobao] BUG: 计费错误导致账户降级`
**#67409** — 使用 NVIDIA AI 自动生成的修复，$200 赏金。修复计费系统未能正确应用礼品订阅的延期。开放中。
👉 https://github.com/anthropics/claude-code/pull/67409

### 9. `updated example file`
**#64489** — 更新了示例文件内容。虽无具体描述，但表明社区持续完善示例。开放中。
👉 https://github.com/anthropics/claude-code/pull/64489

### 10. `docs: 添加 VS Code 使用面板的文档说明`
**#67746** — 对应 issue（本身是文档需求），指出 v2.1.174 新增的 `/usage` 命令可以显示 per-skill/plugin/MCP 缓存和长上下文归因，但官方文档尚未更新。PR 尚未创建，但 issue 已标记为 documentation 需求，社区期待补全。
👉 https://github.com/anthropics/claude-code/issues/67746

---

## 📊 功能需求趋势

从近期 Issues 和 PR 中可以提炼出社区最关注的 **五大功能方向**：

1. **多窗口 / 多实例桌面支持** (#30154) — 高赞、高热度，用户希望摆脱单窗口的限制，实现类比 VS Code 的窗口管理。
2. **Linux 原生桌面应用** (#67758) — 虽然目前已有 CLI，但社区强烈要求推出 Linux 原生桌面 GUI 应用（当前仅 macOS/Windows）。
3. **沙箱状态可见性** (#56843) — 希望在状态栏中显示当前的沙箱模式（Docker、本地沙箱或无沙箱），便于用户感知环境安全。
4. **通道 (Channels) 与 Telegram 集成稳定性** (#67760, #67759) — 多个错误报告指出 Telegram 通道插件存在消息丢失、注册拒绝等问题，表明 Channels 功能还在早期阶段，社区迫切希望稳定。
5. **内联图片渲染** (#54551) — 相比 claude.ai 网页版和移动端，CLI/TUI 无法显示图片，社区提案了内联渲染方案但尚未被合并。

---

## 💡 开发者关注点

近期高频反馈的**痛点与高频需求**：

- **模型自动切换误报** — 多起报告（#67732, #67727, #67757, #67738）显示 Fable / Opus 模型在讨论安全、3D 建模、论文阅读等内容时被错误标记并降级，开发者认为当前审查机制过于敏感，破坏了正常开发流程。
- **子代理幻觉问题** (#67730) — 子代理返回虚假结果且不执行工具调用，严重削弱多 Agent 架构的可靠性。
- **MCP 服务器稳定性** (#40207) — 无故被 SIGTERM 杀掉，影响长会话工具链。
- **Cowork VM 兼容性** (#39636, #66870) — 在 ARM64 Windows 和 macOS 26 上启动失败，代码签名权限缺失。
- **滚轮回归** (#65833) — v2.1.150 引入的滚轮行为破坏，至今未完全修复（尽管 #67766 可能后期修复）。
- **计费与礼品订阅问题** (#67750, #67578) — 礼品订阅未延长到期日期，以及 Pro 计划下 1M 上下文被错误要求使用量。
- **Billing 和 Usage 文档缺失** (#67746) — 新版 `/usage` 面板的功能在官方文档中没有说明，社区期待补全。

---

*日报生成时间：2026-06-12，数据截止至 2026-06-12 23:59 UTC。动态追踪请关注 [anthropics/claude-code](https://github.com/anthropics/claude-code)。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 | 2026-06-12

## 今日速览

过去24小时内，Codex 密集发布了 5 个 Rust 0.140.0-alpha 系列版本，工程团队持续打磨 CLI 与桌面端。社区反馈集中在电话验证 bug（197 条评论）、聊天历史丢失以及 Windows 端高频 Git 进程占用 CPU 等稳定性问题上；同时多仓库支持、嵌套 AGENTS.md 等功能需求呼声极高。

## 版本发布

过去 24 小时共发布 5 个 Rust 0.140.0-alpha 版本，均为 CLI 相关的开发中快照：

- [`rust‑v0.140.0‑alpha.8`](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.8)
- [`rust‑v0.140.0‑alpha.9`](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.9)
- [`rust‑v0.140.0‑alpha.10`](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.10)
- [`rust‑v0.140.0‑alpha.11`](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.11)
- [`rust‑v0.140.0‑alpha.13`](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.13)

各 Release 均仅标注 “Release 0.140.0‑alpha.X”，未提供额外 changelog，推测为滚动式内部发布。

## 社区热点 Issues（精选 10 条）

### 1. 🔥 电话验证无法工作 — 影响登录与 SSO 流程
[#20161](https://github.com/openai/codex/issues/20161)  
`[bug, auth]` · 关闭 · 197 评论 · 121 👍  
**重要性**：用户在切换设备或使用 SSO 登录时被强制要求绑定手机号，但许多人从未设置过手机，导致账户无法正常使用。社区反应激烈，点赞数高达 121，是目前最受关注的 bug。

### 2. Windows 端撤销 (Undo) 功能无效
[#3567](https://github.com/openai/codex/issues/3567)  
`[bug, windows-os, extension]` · 关闭 · 58 评论 · 29 👍  
**重要性**：VS Code 插件中在 Full Agent 模式执行修改后无法用 Ctrl+Z 撤销，严重影响开发体验。虽已关闭但仍有大量用户跟进。

### 3. MCP 客户端握手失败：所有服务器同时崩溃
[#6020](https://github.com/openai/codex/issues/6020)  
`[bug, mcp]` · 开放 · 42 评论 · 27 👍  
**重要性**：MCP 服务器（X 等）全部无法启动，错误提示为“handshaking failed: connection closed”。使用 GPT‑5 与 Pro 订阅的用户受影响，社区期望快速修复。

### 4. 桌面端更新后项目聊天历史全部丢失
[#20741](https://github.com/openai/codex/issues/20741)  
`[bug, app, session]` · 开放 · 38 评论 · 14 👍  
**重要性**：macOS 用户更新后历史会话消失，Pro 订阅者反馈强烈。虽然数据可能未彻底丢失（后端仍可返回），但 UI 层面不再显示，造成极大困扰。

### 5. 后台进程轮询浪费大量 token
[#13733](https://github.com/openai/codex/issues/13733)  
`[bug, rate-limits, tool-calls, session]` · 开放 · 27 评论 · 22 👍  
**重要性**：当后台有编译/测试任务时，Codex 会频繁轮询状态，每次轮询都消耗完整对话历史产生的 token，导致付费额度快速流失。开发者呼声高。

### 6. 按需加载嵌套 AGENTS.md 文件
[#12115](https://github.com/openai/codex/issues/12115)  
`[enhancement, context]` · 开放 · 20 评论 · 67 👍  
**重要性**：希望像 Claude Code 那样仅在访问子目录时加载该目录下的 AGENTS.md，避免根目录文件过于庞大。67 个赞反映这是社区高度期待的功能。

### 7. 多仓库支持
[#11956](https://github.com/openai/codex/issues/11956)  
`[enhancement]` · 开放 · 16 评论 · 30 👍  
**重要性**：用户希望在 Codex App 中同时绑定多个 Git 仓库，便于跨服务改动。目前只能通过 CLI 绕行，社区希望原生支持。

### 8. MultiAgentV2 加密工具调用导致 400 错误
[#26753](https://github.com/openai/codex/issues/26753)  
`[bug, exec, CLI, tool-calls, subagent]` · 关闭 · 15 评论 · 4 👍  
**重要性**：开启 `multi_agent_v2` 后所有对话均失败，因为模型无法使用加密的 `spawn_agent` 工具。虽然已关闭，但暴露了子代理加密配置兼容性问题。

### 9. Windows 端 Git for Windows 进程持续高 CPU
[#22085](https://github.com/openai/codex/issues/22085)  
`[bug, windows-os, app, performance]` · 关闭 · 12 评论 · 17 👍  
**重要性**：更新后 Codex 频繁启动 Git 进程（每分钟上千次），导致 CPU 持续高占用，Windows 开发者开发环境严重卡顿。

### 10. macOS “保持 Mac 唤醒” 功能失效
[#23294](https://github.com/openai/codex/issues/23294)  
`[bug, app, remote]` · 开放 · 8 评论 · 5 👍  
**重要性**：即使勾选了“Keep this Mac awake”，接通电源的 MacBook 仍会睡眠，导致远程连接中断。对依赖远程开发环境的用户影响明显。

## 重要 PR 进展（精选 10 条）

### 1. macOS Seatbelt 拒绝信息集成到统一执行输出
[#17724](https://github.com/openai/codex/pull/17724)  
`[code‑reviewed]` · 开放  
**功能**：新增 `tools.unified_exec.log_macos_seatbelt_denials` 设置（默认关闭），将沙箱拒绝详情直接输出到统一执行结果中，避免用户手动查看系统日志。

### 2. 提取 macOS Seatbelt 拒绝收集器
[#27745](https://github.com/openai/codex/pull/27745)  
**功能**：将 CLI 调试沙箱命令中的拒绝收集器与 PID 追踪器抽离至 `codex-sandboxing` 库，供其他沙箱路径复用，减少重复代码。

### 3. 并行化发布代码生成
[#27702](https://github.com/openai/codex/pull/27702)  
`已关闭`  
**优化**：将 release 构建的 codegen 单元数从 1 增加到 4（配合 ThinLTO），显著缩短关键路径编译时间，提升发布效率。

### 4. Code Mode 独立进程 — 阶段 3/4：客户端接入
[#27727](https://github.com/openai/codex/pull/27727)  
`开放`  
**功能**：第二阶段构建的独立二进制，现在创建新的 IPC `CodeModeSessionProvider` 供主进程消费。整体目标是将 Code Mode 从主进程 V8 中彻底剥离。

### 5. Guardian 自动审查线程预预热
[#27721](https://github.com/openai/codex/pull/27721)  
`[code‑reviewed]` · 开放  
**性能**：在用户线程启动时异步创建 Guardian 审查线程，避免首次请求审查时的冷启动延迟。预计能改善用户体验中的响应时间。

### 6. 修复 apply_patch 处理 CRLF 文件
[#25866](https://github.com/openai/codex/pull/25866)  
`[code‑reviewed]` · 开放  
**修复**：新增默认关闭的 `apply_patch_crlf` 特性开关，使 patch 应用时保留 CRLF 换行符，避免将 Windows 换行符改为 Unix 格式，保持原有文件风格。

### 7. 缓存工具搜索处理器（免每次重建 BM25 索引）
[#27258](https://github.com/openai/codex/pull/27258)  
`[code‑reviewed]` · 开放  
**性能**：在每个会话/采样连续性中缓存工具搜索结果处理器，避免重复构建 BM25 索引（每次耗时约 113ms），整体提升会话初始化与工具调用速度。

### 8. 清空临时内存指令种子
[#26102](https://github.com/openai/codex/pull/26102)  
`已关闭`  
**修复**：在返回前将 ad‑hoc 内存指令种子写入磁盘并清空，确保调用方后续能观察到正确的持久化指令数据。

### 9. MCP 测试执行重试（解决 ETXTBSY 问题）
[#26103](https://github.com/openai/codex/pull/26103)  
`已关闭`  
**可靠性**：当操作系统临时报告 `ETXTBSY` 时，对已解析的 MCP 程序执行进行重试，提升 CI 和本地测试的稳定性。

### 10. 增加延迟追踪跨度
[#27710](https://github.com/openai/codex/pull/27710)  
`开放`  
**可观测性**：在线程启动、恢复、上下文构建、回滚构建、技能/插件加载等关键路径增加 Span，帮助开发者定位延迟瓶颈，提升调试效率。

## 功能需求趋势

从近期 Issues 中可看出社区最关注的三个功能方向：

1. **多项目/多仓库上下文支持** — `#11956`（多仓库）、`#12115`（嵌套 AGENTS.md）、`#25482`（远程线程编排）等均指向用户希望在一个会话中处理多个独立项目的代码变更，尤其在微服务架构下需求迫切。
2. **长期付费用户豁免强制电话验证** — `#27742` 提议对高信用老用户免除手机验证，直接反映了电话验证流程对开发者的干扰已超出预期。
3. **存档/历史会话的易访问性** — `#27717`、`#27207` 等要求从主界面直接浏览和阅读已归档聊天记录，而非隐藏于设置深处。社区认为存档不应等于“彻底隐藏”。

此外，**Windows 平台的稳定性与性能**（如 Git 进程泛滥、高 CPU、启动挂起）持续成为 Windows 用户的突出痛点。

## 开发者关注点

- **Token 成本失控** — `#13733` 揭示后台轮询操作按完整历史对话消耗 API 用量，付费用户表示“烧钱”速度过快，期望实现增量轮询或本地状态检测。
- **子代理/多 Agent 配置兼容性** — `#26753`、`#27205` 等多处报告加密工具调用与模型不匹配导致的 400 错误，开发者反馈配置门槛高且报错信息不清晰。
- **Windows 与 macOS 特定崩溃** — `#21358`（macOS 15.7 V8 SIGTRAP）、`#27367`（Windows 10 桌面端闪退）、`#26477`（UAC 安装检测导致 node_repl 失败）显示跨平台适配仍是痛点。
- **Subagent 界面空白** — `#27350` 中 Pro 用户反映子代理对话面板无法渲染，严重影响多人协作场景下的工作流。
- **功能开关类型不匹配** — `#27076` PR 指出当前只接受布尔值 `features.foo = true`，即将到来的表格格式需要同时支持 `{ enabled = true, ... }`，开发者在迁移过程中需要关注配置格式变化。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

⚠️ 摘要生成失败。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 (2026-06-12)

## 1. 今日速览

社区对长期未解决的 Issue #53（请求恢复 CLI 命令）的自发替代方案持续升温，该 Issue 已获 75 个 👍。同时，终端渲染乱码（#3755、#3749）、令牌过期无自动刷新（#3763）以及企业级 MCP 注册表认证缺失（#3772）成为今日新涌现的关键话题。唯一的新 PR 为项目初始设置，无实质功能变更。

## 2. 版本发布

过去 24 小时无新版本发布。

## 3. 社区热点 Issues（10 个精选）

### ⭐ #53 – 请求恢复 Copilot CLI 命令，避免破坏工作流
- **作者**: EDM115 | **👍**: 75 | **评论**: 37
- **摘要**: 已有 6 个月未收到 GitHub 官方回应，社区开始自行实现替代方案，如 `shell-ai`。
- **链接**: [Issue #53](https://github.com/github/copilot-cli/issues/53)

### ⭐ #223 – 企业级细粒度 Token 应显示 “Copilot Requests” 权限
- **作者**: RyanHecht | **👍**: 76 | **评论**: 30
- **摘要**: 组织拥有的 Token 创建时无法看到“Copilot Requests”权限，企业无法控制自动化认证。
- **链接**: [Issue #223](https://github.com/github/copilot-cli/issues/223)

### ⭐ #892 – 沙箱模式：限制 CLI 文件访问范围
- **作者**: rexxiang | **👍**: 49 | **评论**: 12
- **摘要**: 希望增加沙箱能力，让代码代理只能读写指定工作目录。
- **链接**: [Issue #892](https://github.com/github/copilot-cli/issues/892)

### ⭐ #3534 – WSL2 ARM64 上 `/copy` 因 `clip.exe` 引号问题失败
- **作者**: TheDr1ver | **👍**: 2 | **评论**: 3
- **摘要**: Copilot CLI v1.0.55-1 中，WSL2 ARM64 环境下剪贴板写入报错。
- **链接**: [Issue #3534](https://github.com/github/copilot-cli/issues/3534)

### ⭐ #2056 – 定时/循环提示（Scheduled/recurring prompts）
- **作者**: drorkremer | **👍**: 3 | **评论**: 3
- **摘要**: 希望 CLI 代理能按计划自动执行任务，如每小时检查集群作业。
- **链接**: [Issue #2056](https://github.com/github/copilot-cli/issues/2056)

### ⭐ #2243 – Worktree 灾难性体验，应默认禁用
- **作者**: movy | **👍**: 8 | **评论**: 2
- **摘要**: 托管会话意外导致数千行代码无法合并回主 worktree。
- **链接**: [Issue #2243](https://github.com/github/copilot-cli/issues/2243)

### ⭐ #3602 – `@github/copilot` SDK 污染 `process.env` 影响所有子进程
- **作者**: DaRosenberg | **👍**: 4 | **评论**: 1
- **摘要**: SDK 初始化时注入 Git 安全配置，导致全局环境被修改。
- **链接**: [Issue #3602](https://github.com/github/copilot-cli/issues/3602)

### ⭐ #3755 – 推理/思考显示导致文本乱码（重叠重复）
- **作者**: corinex-spencer | **👍**: 0 | **评论**: 3
- **摘要**: `showReasoning: true` 后流式文本出现单词重复、片段错乱。
- **链接**: [Issue #3755](https://github.com/github/copilot-cli/issues/3755)

### ⭐ #3749 – 终端流渲染器损坏输出（字符加倍/截断）
- **作者**: Richard-Marlow | **👍**: 5 | **评论**: 3
- **摘要**: 输出流中产生重复字符、截断 token 和重复行。
- **链接**: [Issue #3749](https://github.com/github/copilot-cli/issues/3749)

### ⭐ #3772 – 支持 MCP 注册表的认证读取（企业需求）
- **作者**: eggboy | **👍**: 0 | **评论**: 0
- **摘要**: 企业自定义 MCP 注册表（如 Azure API Center）目前被匿名读取，不安全。
- **链接**: [Issue #3772](https://github.com/github/copilot-cli/issues/3772)

## 4. 重要 PR 进展

### #3771 – 初始项目设置（OPEN）
- **作者**: limenpchuolto112-creator | **评论**: 0 | **👍**: 0
- **摘要**: 仅包含基础项目初始化，无功能变更。
- **链接**: [PR #3771](https://github.com/github/copilot-cli/pull/3771)

> 注：今日仅此一条 PR，且为无实质内容的新贡献者初始化。无合并或有意义的代码变更。

## 5. 功能需求趋势

从近期 Issue 可看出社区最关注的几个方向：

- **沙箱与权限隔离**：请求文件系统沙箱（#892）和更细粒度的目录访问控制（#3764）。
- **自动化与定时任务**：希望 CLI 支持定时/循环执行（#2056、#2129），使代理可长时间无人值守。
- **企业级认证与 MCP 集成**：企业 Token 权限缺失（#223）、MCP 注册表认证（#3772）成为企业用户的核心诉求。
- **多平台兼容性**：WSL2 ARM64 剪贴板问题（#3534）、Windows 语音输入失效（#3770）显示平台适配需求。
- **终端渲染改进**：流式文本乱码（#3755、#3749、#3765）和线程问题（#3769）在 v1.0.61 中集中爆发，亟需修复。

## 6. 开发者关注点

- **令牌过期无自动刷新**：#3763 反映会话令牌到期后 CLI 不自动续期，导致任务中途失败，用户需手动 `resume` 才能恢复。
- **Content Exclusion Service 崩溃**：#3757 指出在凭证更新后，内容排除服务被错误释放，导致所有 shell 命令被阻止。
- **重复文件权限审批**：#3764 指出同一个目录被多次要求批准，缺少解释原因。
- **输入快捷键冲突**：`Shift+Enter` 无法换行（#3768），以及提示 `ctrl+enter enqueue` 但实际 `ctrl+enter` 是换行（#3760），UI/UX 不一致。
- **工作树（worktree）失控**：#2243 强调自动创建 worktree 导致代码合并灾难，社区呼吁默认禁用。
- **环境变量污染**：#3602 指出 SDK 修改全局 `process.env` 可能影响用户其他工具链。

> 数据来源：https://github.com/github/copilot-cli （截至 2026-06-12 10:00 UTC）

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 | 2026-06-12

## 📌 今日速览
- 社区核心动态集中于 **自定义颜色皮肤** 功能：PR #2170 提交了通过 YAML 文件自定义主题配色的能力，支持运行时 `/skin` 命令切换，目前已合并。
- 过去 24 小时内无新 Release 或活跃 Issue，项目处于功能合并后的稳定期，开发者可关注即将到来的更新。

## 🚀 版本发布
无（过去 24 小时内无新版本发布）

## 🔥 社区热点 Issues
无（过去 24 小时内无更新或新创建的 Issue）

## 📦 重要 PR 进展
（过去 24 小时内更新共 1 条）

### #2170 [已合并] feat: add user-customizable color skins via YAML
- **作者**: VrtxOmega | 创建: 2026-05-06 | 更新: 2026-06-11 | 👍 0
- **摘要**:  
  新增 `/skin` 斜杠命令，允许用户在运行时切换命名皮肤；支持 `~/.kimi/skins/<name>.yaml` 文件定义完整的 Hermes 兼容配色方案，未指定的配色将回退到默认值。该 PR 解决了 #2171 中关于灵活主题定制的需求。
- **链接**: [MoonshotAI/kimi-cli PR #2170](https://github.com/MoonshotAI/kimi-cli/pull/2170)

## 🧭 功能需求趋势
目前无活跃 Issue 数据，但从近期 PR（#2170）可看出社区对 **用户自定义主题/皮肤** 有明确需求，尤其关注：
- YAML 配置方式的易用性与 Hermes 兼容性
- 运行时动态切换（非重启）的 CLI 体验
- 对终端色彩深度适配（256色、TrueColor 等）

## ⚙️ 开发者关注点
- 主题自定义的 **回退机制** 与 **默认主题** 的稳定性
- YAML 文件路径与 CLI 核心配置的协同（如是否支持全局/项目级皮肤）
- 命令 `/skin` 与已有 `/theme` 命令的关系（PR 中声明互补而非冲突）
- 缺失 Issues 反映出社区当前更关注 **已开放功能的完善** 而非新需求提交，建议开发者关注 CHANGELOG 或 upcoming milestones。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，我将根据您提供的 GitHub 数据，为您生成 2026-06-12 的 OpenCode 社区动态日报。

---

# OpenCode 社区动态日报 | 2026-06-12

## 今日速览

今日社区热度集中在 **会话生命周期管理** 与 **跨平台编码/兼容性** 两大方向。v1.17.4 版本悄然发布，带来了本地 MCP 服务器的 `cwd` 支持以及连接器认证流程的基础铺垫。与此同时，关于原生 `/goal` 会话目标、上下文窗口可视化的功能呼声极高，而 Windows 环境下的复制粘贴、乱码等基础体验问题依然是 bug 反馈的重灾区。

## 版本发布

### [v1.17.4](https://github.com/anomalyco/opencode/releases/tag/v1.17.4) (最新)

本次小版本更新主要进行了三项基础架构的改进：
- **本地 MCP 服务器支持 `cwd`**：允许从工作区相对目录启动本地 MCP 服务器，这对于 monorepo 或多项目工作流非常实用。
- **连接器认证流程**：新增了基于连接器的认证流，并为存储的供应商凭据提供了支持。这为未来集成更多第三方服务打下了基础。
- **V2 API 增强**：增加了创建、获取会话以及列出会话的 V2 API 端点，表明团队正在持续推进 API 的迭代。

## 社区热点 Issues

| 序号 | Issue 标题 | 热度 (👍/💬) | 重要性 & 社区反应 |
| :--- | :--- | :--- | :--- |
| 1 | **[[FEATURE] Add native session goals with /goal](https://github.com/anomalyco/opencode/issues/27167)** | 71 👍 / 45 💬 | **社区呼声极高的功能请求**。用户希望引入原生 `/goal` 命令来创建持久的会话目标和生命周期管理，而非依赖自定义 slash 命令。社区讨论热烈，反映了用户对复杂、可控工作流的需求。 |
| 2 | **[[FEATURE] Session context usage](https://github.com/anomalyco/opencode/issues/6152)** | 108 👍 / 18 💬 | **用户最渴望的功能（获赞数最高）**。希望实现类似 Claude Code 中 `/context` 的 TUI 对话框，可视化地展示当前会话的上下文窗口使用情况（如 token 消耗、文件列表等）。这是高级用户进行精细化管理的关键需求。 |
| 3 | **[can not copy and paste in opencode CLI](https://github.com/anomalyco/opencode/issues/13984)** | 20 👍 / 47 💬 | **最活跃的 Bug 报告**。用户在 CLI 中复制后无法粘贴，UI 提示“已复制到剪贴板”但实际无效。虽然影响范围可能有限，但高达 47 条评论表明该问题非常棘手且影响开发者效率。 |
| 4 | **[[FEATURE] Add Go plan usage/balance API endpoint](https://github.com/anomalyco/opencode/issues/16017)** | 52 👍 / 17 💬 | **可观测性方向的强需求**。用户希望公开一个 API 端点，用于查询 Go 计划的用量和余额（支持滚动/周/月窗口）。这表明社区对成本控制和用量监控有实际诉求。 |
| 5 | **[[BUG] "Upstream idle timeout exceeded"](https://github.com/anomalyco/opencode/issues/28957)** | 0 👍 / 9 💬 | **影响使用体验的 Bug**。用户在长时间会话（特别是使用 “writing-plans” skill 时）遭遇上游连接空闲超时。这会影响长时间、复杂的任务，社区正在寻求解决方案。 |
| 6 | **[[BUG] Terminal button in web UI mysteriously disappears](https://github.com/anomalyco/opencode/issues/30158)** | 7 👍 / 8 💬 | **严重的 Web UI 回归 Bug**。从 v1.15.12 开始，Web UI 右上角的终端按钮神秘消失，降级回旧版本才能恢复。这对 Web UI 使用者是重大阻塞，社区反馈明确。 |
| 7 | **[Bug: Copying Japanese text from chat output results in mojibake](https://github.com/anomalyco/opencode/issues/30068)** | 3 👍 / 7 💬 | **国际化编码问题**。从聊天输出复制日语文本时显示正常，粘贴后变成乱码。这是长期存在的 UTF-8 解析问题，对非英语用户影响很大。 |
| 8 | **[[FEATURE] Expose GitHub Copilot "Auto" option in model selector](https://github.com/anomalyco/opencode/issues/25239)** | 13 👍 / 7 💬 | **模型选择器功能增强**。希望模型选择器能集成并暴露 GitHub Copilot 的 “Auto” 模式，让模型自动选择更智能。这表明用户希望 OpenCode 更具“智能代理”特性。 |
| 9 | **[[BUG] Model ID auto-switches silently during session](https://github.com/anomalyco/opencode/issues/28842)** | 0 👍 / 6 💬 | **令人困惑的 Bug**。会话中的模型 ID 会在无任何提示的情况下自动切换（例如从 OpenAI 切换到 DeepSeek）。这种行为对用户预期是巨大破坏，亟待修复“静默切换”的问题。 |
| 10 | **[[BUG] "all messages must have non-empty content" errors](https://github.com/anomalyco/opencode/issues/31971)** | 0 👍 / 2 💬 | **特定模型下的高频 Bug**。在使用 DeepSeek-V4-Flash 进行长时间会话后，所有消息都返回“内容不能为空”错误。这很可能与上下文窗口接近满载时的消息处理逻辑有关。 |

## 重要 PR 进展

| 序号 | PR 标题 | 类型 | 核心内容 |
| :--- | :--- | :--- | :--- |
| 1 | **[fix(instance): eliminate dual InstanceStore.Service materialization per directory](https://github.com/anomalyco/opencode/pull/29773)** | Bug Fix | **关键性能修复**。修复了 `InstanceStore.Service` 为同一目录重复实例化导致的 `Question` 工具卡死问题，解决了潜在大面积性能瓶颈。 |
| 2 | **[fix(opencode): avoid downloading MCP resource URIs](https://github.com/anomalyco/opencode/pull/31940)** | Bug Fix | **MCP 功能优化**。阻止 OpenCode 将 MCP 资源的自定义 URI 作为可下载文件传递给模型提供者，修复了可能导致错误或性能问题的行为，并保持了 `resources/read` 的原有功能。 |
| 3 | **[fix(opencode): prevent process.exit() from killing parent terminal on Windows](https://github.com/anomalyco/opencode/pull/29281)** | Bug Fix | **Windows 平台关键修复**。修复了在 Windows 上 `process.exit()` 会连带杀死父终端 (pwsh/cmd) 的严重问题。这对 Windows 开发者是至关重要的体验改进。 |
| 4 | **[[needs:compliance] fix(bash): lazy Windows code page detection with periodic refresh](https://github.com/anomalyco/opencode/pull/31980)** | Bug Fix | **解决 Windows 乱码根源**。引入延迟的 Windows 代码页检测与定期刷新机制，以解决中文、日文、韩文等非 UTF-8 系统下 bash 工具输出乱码的问题。 |
| 5 | **[fix: Windows session path, shell env, error message, and autocomplete](https://github.com/anomalyco/opencode/pull/31946)** | Bug Fix | **Windows 综合 Bug 修复**。一次性修复了 Windows 桌面版会话路径、Shell 环境变量、错误信息及自动补全等多个问题，极大地改善了 Windows 用户的开箱即用体验。 |
| 6 | **[feat: improve deepseek prompt cache reuse](https://github.com/anomalyco/opencode/pull/31867)** | New Feature / Refactor | **性能优化**。通过移除系统提示中动态注入的当前日期，提高了 DeepSeek 模型的提示缓存命中率，从而减少请求延迟和成本。 |
| 7 | **[fix(tui): preserve exit epilogue during scoped shutdown](https://github.com/anomalyco/opencode/pull/31805)** | Bug Fix | **TUI 体验修复**。修复了在 TUI 退出时，因作用域清理导致会话结束语在打印前就被清除的 Bug，确保了退出信息的完整性。 |
| 8 | **[fix(provider): distinguish unknown model pricing](https://github.com/anomalyco/opencode/pull/30021)** | Bug Fix | **成本显示修复**。修复了 OpenCode 将未知定价模型的价格误显示为 $0 的问题，避免用户产生误解。 |
| 9 | **[fix(mcp): bind oauth callback to IPv4 loopback](https://github.com/anomalyco/opencode/pull/30022)** | Bug Fix | **网络兼容性修复**。修复了 MCP OAuth 回调服务器绑定到 IPv6 通配符地址导致某些 Linux 系统上连接失败的问题，现在会明确绑定到 IPv4 回环地址。 |
| 10 | **[fix(tui): scope non-git sessions by directory, not hierarchical path](https://github.com/anomalyco/opencode/pull/31210)** | Bug Fix | **会话管理修复**。一次性关闭了 6 个相关 Issue。修复了非 Git 项目的会话按层级路径而不是按目录作用域进行管理的问题，避免了会话混乱。 |

## 功能需求趋势

从今日的 Issues 中，可以提炼出社区最关注的几个功能方向：

1.  **会话持久化与导航**：社区不满足于简单的对话，而是希望有 **持久的会话目标** (`/goal`)、**层次化的会话导航** 以及 **会话上下文可视化** (`/context`)。这表明用户希望将 OpenCode 用于更长期、更复杂的项目任务管理。
2.  **AI 原生技能 (Skills/Agent) 增强**：用户希望 OpenCode 能像一个“智能代理”一样工作，例如 **子代理间相互协作**、**自动切换模型** (如 Copilot Auto 模式)，并能通过 **内置 Skill** 来定制自身行为。
3.  **可观测性与用量管理**：高级用户开始关注成本与资源消耗，迫切需求 **API 用量查询**、**Token 计数**、**计划余额** 等可观测性功能，以便进行成本控制和性能调优。
4.  **跨平台编码与终端兼容性**：随着 OpenCode 走向国际化，**非英语字符（中文、日文、韩文）的复制/粘贴** 以及 **Windows 终端的乱码** 问题成为社区反馈的焦点，这是提升全球用户体验的必经之路。
5.  **模型选择与切换的精细化**：用户对当前 **模型静默自动切换** 的行为感到困惑，并希望拥有更丰富的模型选择器（如集成 Copilot Auto），体现了用户对 AI 工作流可控制性的更高要求。
6.  **本地开发的深度整合**：`cwd` 支持、LM Studio 模型刷新、以及 MCP 服务器的深入集成，显示社区正积极将 OpenCode 嵌入到复杂的本地开发工作流中。

## 开发者关注点

从 Bug 报告和反馈中，可以总结出以下开发者痛点和高频需求：

-   **编码与剪贴板问题是最大痛点**：CLI 复制无效 (#13984)、日文/韩文粘贴乱码 (#30068, #31978) 以及退出后鼠标乱码 (#11748, #20458) 是报告频率最高的三类问题，严重影响日常使用。
-   **Windows 平台体验显著落后**：无论是 `process.exit` 杀死父终端 (#28673)、PowerShell 乱码 (#23636)，还是桌面应用启动问题，都表明 Windows 平台需要专门的关注和修复。
-   **模型稳定性与可控性不足**：模型在会话中 **静默切换** (#28842)、**进入无限循环** (#21850) 以及 **因非空内容错误中断** (#31971) 等问题，破坏了用户对 AI 工作流的信任。
-   **Web UI / TUI 体验退化**：Web UI 终端按钮消失 (#30158) 和 TUI 退出时显示 Bug (#31803) 等回归问题，让用户感到不满，亟需建立更完善的回归测试机制。
-   **MCP / Skills 配置复杂性**：关于 MCP 资源处理 (#31940)、Skill 发现重复 (#31977) 以及内置 Skill 配置过时 (#31982) 的反馈，表明配置和集成过程对用户来说仍然不够透明和友好。
-   **升级过程的反馈缺失**：用户希望在执行 `opencode upgrade` 时能看到进度条 (#31623)，以确保升级过程正常进行，这反映了对工具本身健壮性的要求。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 | 2026-06-12

## 今日速览
- **关键 Bug 密集修复**：过去 24 小时内有 20+ 个 Issue 被关闭，主要涉及 CLI 命令挂起、SSE 超时、模型推理流挂死、会话恢复重复等问题，社区贡献者积极提交 PR 解决。
- **新提供商支持加速**：`amazon-bedrock-mantle`、`anthropic-vertex` 等原生提供商 PR 持续活跃，同时社区对本地 LLM（ollama/LM Studio）的集成呼声极高。
- **Windows/WSL 用户体验改善**：多项 PR 针对 Windows 终端图片粘贴、CLI 退出挂起等问题，表明跨平台兼容性成为当前开发重点。

## 版本发布
无（过去 24 小时未发布正式版本，当前最新为 v0.79.1）。

---

## 社区热点 Issues（10 条）

### 1. #4945 – openai-codex 在 `Working...` 状态下无限挂起
- **热度**：54 评论 / 30 👍
- **重要性**：严重影响使用 OpenAI Codex 模型的用户，交互式体验完全阻塞。社区反馈频繁出现，需按 Escape 才能恢复，但会记录零使用的轮次。
- **进展**：标记为 `inprogress, possibly-openclaw-clanker`，仍在开放中。
- 链接：https://github.com/earendil-works/pi/issues/4945

### 2. #3357 – 官方本地 LLM 提供商扩展（ollama/LM Studio）
- **热度**：23 评论 / 36 👍
- **重要性**：社区呼声最高的功能请求，希望 Pi 能自动从 `{baseUrl}/models` 动态获取模型列表，以无缝对接本地运行的开源模型。
- **进展**：自 4 月提出后持续活跃，评论数一直增长。
- 链接：https://github.com/earendil-works/pi/issues/3357

### 3. #5363 – 新增 Amazon Bedrock Mantle 提供商
- **热度**：9 评论 / 3 👍
- **重要性**：Bedrock Mantle 使用 OpenAI 兼容 API 而非 Converse API，当前 `amazon-bedrock` 提供商无法使用，亟需新提供商支持。
- **进展**：已有关联 PR #5509，社区讨论热烈。
- 链接：https://github.com/earendil-works/pi/issues/5363

### 4. #5427 – OpenAI Codex 传输超时（SSE 响应头 10000ms）
- **热度**：5 评论 / 4 👍
- **重要性**：升级到 0.78.1 后频繁出现 `Codex SSE response headers timed out`，影响所有使用 ChatGPT 订阅的用户。
- **进展**：已关闭，推测通过配置化超时参数解决（见 #5631）。
- 链接：https://github.com/earendil-works/pi/issues/5427

### 5. #5652 – npm-shrinkwrap.json 导致 `pi-ai` 重复安装
- **热度**：3 评论 / 0 👍
- **重要性**：`@earendil-works/pi-coding-agent` 打包的 shrinkwrap 缺少 `pi-ai` 的完整性校验，导致项目同时依赖 `pi-ai` 和 `pi-coding-agent` 时出现两套独立的 `pi-ai` 副本，API 提供商注册表分裂。
- **进展**：已关闭，但问题在 #5653 中进一步讨论。
- 链接：https://github.com/earendil-works/pi/issues/5652

### 6. #5584 – Bedrock 提供商忽略 models.json 中的 apiKey
- **热度**：2 评论 / 1 👍
- **重要性**：使用自定义提供商配置时，`apiKey` 被静默忽略，只能通过 `AWS_BEARER_TOKEN_BEDROCK` 环境变量认证，导致配置不统一。
- **进展**：PR #5586 已合并解决。
- 链接：https://github.com/earendil-works/pi/issues/5584

### 7. #5633 – Kimi 2.6 在续会话时抛出 `reasoning_content is missing` 错误
- **热度**：2 评论 / 0 👍
- **重要性**：使用 Kimi 2.6 模型超过缓存续会话时出现 400 错误，直接影响用户长会话体验。
- **进展**：已关闭，推测为模型 API 兼容性问题。
- 链接：https://github.com/earendil-works/pi/issues/5633

### 8. #5558 – 流式模型调用无限挂死（无超时机制）
- **热度**：2 评论 / 0 👍
- **重要性**：在没有终端活动/轮次截止时间的情况下，上游短暂中断会导致流式调用永久挂死，需要手动 kill 进程。
- **进展**：已关闭，可能已加入相关超时机制。
- 链接：https://github.com/earendil-works/pi/issues/5558

### 9. #5660 – 会话恢复时显示最后一条消息而非第一条
- **热度**：1 评论 / 0 👍（最新 Issue）
- **重要性**：用户体验优化，当工作目录有多个分支时，resume 列表无法区分不同分支，希望显示最后一条消息辅助识别。
- **进展**：刚提出，已关闭，可能已被接受。
- 链接：https://github.com/earendil-works/pi/issues/5656

### 10. #5648 – 符号链接 `~/.pi/agent` 导致 `AGENTS.md` 内容重复
- **热度**：1 评论 / 0 👍
- **重要性**：使用符号链接配置目录时系统提示重复，污染上下文。触及文件路径规范化问题。
- **进展**：已关闭，PR #5647 修复。
- 链接：https://github.com/earendil-works/pi/issues/5648

---

## 重要 PR 进展（10 条）

### 1. #5586 – Bedrock 使用 apiKey 作为 Bearer Token 后备认证
- **修复**：允许 `models.json` 中的 `apiKey` 作为 Bearer Token 回退，解决 #5584。
- 链接：https://github.com/earendil-works/pi/pull/5586

### 2. #5509 – 新增 Amazon Bedrock Mantle OpenAI Responses 提供商
- **功能**：基于 Azure OpenAI Responses 架构，支持 Bedrock Mantle API（当前仅支持 GPT 5.5/5.4）。
- 链接：https://github.com/earendil-works/pi/pull/5509

### 3. #5262 – 新增 Anthropic Vertex 提供商（Claude on GCP）
- **功能**：内置 `anthropic-vertex` 提供商，复用现有 Anthropic 流式路径，降低配置成本。
- 链接：https://github.com/earendil-works/pi/pull/5262

### 4. #5650 – 修复 OpenRouter Kimi 免费模型断言失败
- **修复**：OpenRouter 返回模型列表中不再包含 `moonshotai/kimi-k2.6:free`，移除对应测试断言使 CI 通过。
- 链接：https://github.com/earendil-works/pi/pull/5650

### 5. #5385 – 首次运行时检测终端主题（亮/暗）
- **功能**：通过 OSC 查询终端颜色方案，自动匹配 Pi 界面主题，提升首次使用体验。
- 链接：https://github.com/earendil-works/pi/pull/5385

### 6. #5647 – 规范化文件路径解决 AGENTS.md 重复加载
- **修复**：使用 `fs.realpathSync` 规范化符号链接路径，防止上下文重复。
- 链接：https://github.com/earendil-works/pi/pull/5647

### 7. #5641 – CLI 包命令退出后进程不再挂起
- **修复**：包管理命令（`install`/`remove`/`list`/etc.）完成后强制退出，保留退出码，解决 Windows/Linux 挂死问题。
- 链接：https://github.com/earendil-works/pi/pull/5641

### 8. #5635 & #5640 – WSL 下 Ctrl+V 粘贴图片支持
- **修复**：Windows Terminal 会拦截 Ctrl+V 作为文本粘贴，现改为 Alt+V 绑定或通过 WSL 系统菜单方式绕过。
- 链接：https://github.com/earendil-works/pi/pull/5635 / https://github.com/earendil-works/pi/pull/5640

### 9. #5637 – 私有 Git 仓库 HTTPS 安装支持 Token 认证
- **功能**：当设置 `PI_GIT_TOKEN` 或 `GITHUB_TOKEN` 时，自动嵌入到克隆 URL 中，允许安装私有仓库。
- 链接：https://github.com/earendil-works/pi/pull/5637

### 10. #5615 – 修复仅含可选参数的工具在 Claude/OpenAI 上的架构拒绝
- **修复**：当工具所有参数都是可选时，TypeBox 省略 `required` 字段，导致 Claude 等提供商返回 400。现显式添加空数组 `required: []`。
- 链接：https://github.com/earendil-works/pi/pull/5615

---

## 功能需求趋势

1. **本地模型深度集成**：`ollama`/`LM Studio`/`llama.cpp` 等本地推理引擎的自动化模型发现成为第一需求（#3357 持续高赞）。
2. **新模型提供商快速接入**：Amazon Bedrock Mantle、Anthropic Vertex、OpenCode 等新渠道的官方支持不断涌现，社区希望减少手动配置。
3. **跨平台体验统一**：Windows/WSL 下的图片粘贴、CLI 退出、终端主题检测等细节改进表明用户群正在扩大，跨平台一致性成为焦点。
4. **隐私与安全**：私有 Git 仓库安装 Token 支持、OAuth 信号中止防止端口泄漏等体现社区对安全性的重视。
5. **会话管理优化**：恢复会话时显示最后消息、区分分支、自定义消息排除上下文等功能旨在提升长 session 的可管理性。

---

## 开发者关注点（痛点 & 高频需求）

- **Codex SSE 超时频繁**（#5427, #5631）：用户强烈要求将超时配置化，而非硬编码 10 秒。
- **包管理命令退出挂起**（#5626, #5630, #5641）：所有 CLI 子命令在完成后不退出，必须手动 Ctrl+C，尤其影响 CI 自动化。
- **模型 ID 含斜杠解析错误**（#5643）：`xiaomi/mimo-v2.5-pro` 会被误认为提供商 `xiaomi`，导致无法使用。
- **双份 `pi-ai` 安装导致注册表分裂**（#5652）：npm shrinkwrap 问题，需重新打包 `pi-coding-agent`。
- **流式调用无超时保护**（#5558, #4945）：用户期望引入 `inactivity_timeout` 或 `turn_deadline` 机制自动终止挂死调用。
- **工具参数架构兼容性**（#5615）：Claude/OpenAI Responses API 对缺少 `required` 字段的工具报 400，需加固 Schema 生成逻辑。

---

*日报基于 GitHub 仓库 earendil-works/pi 2026-06-12 数据自动生成，仅供参考。*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 | 2026-06-12

---

## 今日速览

v0.18.0-preview.2 预览版正式发布，重点修复了 CLI 复制输出时跳过思考部分的问题。社区围绕**本地模型兼容性**、**会话状态持久化**以及**UI 交互体验**展开了大量讨论，其中 `Ctrl+U` 多行删除、`/goal` 迭代计数器重置、`/stats` 双倍计数等 Bug 反馈活跃。PR 方面，`/cd` 命令、持久化 cron 任务、A2UI 桥接等新功能进入审查阶段，代码库规模持续扩大。

---

## 版本发布

### v0.18.0-preview.2

**发布时间**：2026-06-12  
**变更摘要**：
- 修复 CLI 在复制输出时跳过 `thought` 部分的问题（`fix(cli): skip thought parts in copy output`）
- 同步 v0.17.1 的发布流程优化（`chore(release): v0.17.1`）

> 详情：[Release v0.18.0-preview.2](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.0-preview.2)

---

## 社区热点 Issues（10 条）

1. **#3384 – 无法添加 OpenAI 兼容的本地 LLM**  
   - 用户尝试用 Qwen Code + Qwen3.6-35B-A3B（VLLM）但配置不生效。  
   - **评论 14**，社区关注度最高，反映了用户对本地/自托管模型支持的强烈需求。  
   - 链接：[#3384](https://github.com/QwenLM/qwen-code/issues/3384)

2. **#4987 – PR #4779 静默回退了已合并的 PR #4652**  
   - 无解释地回退了一个已合并功能，开发者要求冲突应在 PR 内解决而非回退无关功能。  
   - **标签**：`type/bug` `priority/P2` `welcome-pr`，社区讨论激烈。  
   - 链接：[#4987](https://github.com/QwenLM/qwen-code/issues/4987)

3. **#4888 – IDEA 插件中 ask_user_question 不显示问题文本和输入框**  
   - 插件仅显示“提交”“取消”按钮，用户无法输入答案。  
   - **评论 4**，IDE 集成体验 Bug，影响日常使用。  
   - 链接：[#4888](https://github.com/QwenLM/qwen-code/issues/4888)

4. **#4898 – 希望自由约束用户画像生成和 skill 自动提炼**  
   - 用户希望更精细地控制上下文积累，避免污染。功能需求型 Issue，社区呼声上升。  
   - 链接：[#4898](https://github.com/QwenLM/qwen-code/issues/4898)

5. **#4814 – UI 应方便自定义提供商用户添加新模型**  
   - 首次启动向导对自定义 Provider 支持不够直观，无法批量添加模型。  
   - **评论 3**，高频痛点（#3384 也是同一作者）。  
   - 链接：[#4814](https://github.com/QwenLM/qwen-code/issues/4814)

6. **#4854 – 让 qwen code 进程从其他位置启动，避免杀死自身 session**  
   - Agent 启动开发服务器后，`qwen serve` 的路径冲突导致自杀。  
   - **评论 3**，涉及 session 隔离与安全。  
   - 链接：[#4854](https://github.com/QwenLM/qwen-code/issues/4854)

7. **#4921 – 启用“Virtualized History”后视口高度异常**  
   - 设置中开启虚拟化历史后，视图高度变高且出现滚动条，光标位置同样异常。  
   - **评论 3**，UI 渲染 Bug。  
   - 链接：[#4921](https://github.com/QwenLM/qwen-code/issues/4921)

8. **#4964 – 从 max_tokens 截断中恢复**  
   - 当前若响应被截断，模型无法自动从截断点继续，导致工具调用失败。  
   - **评论 3**，严重影响长会话场景。  
   - 链接：[#4964](https://github.com/QwenLM/qwen-code/issues/4964)

9. **#4951 – statusline 中 tokens 统计是否准确？**  
   - 用户质疑“说几句话就几百K tokens”是否真实，统计精度存疑。  
   - **评论 3**，影响用户对计费/资源消耗的判断。  
   - 链接：[#4951](https://github.com/QwenLM/qwen-code/issues/4951)

10. **#4999 – `/goal` 迭代计数器在会话恢复后重置**  
    - `MAX_GOAL_ITERATIONS` 限制因计数器归零而失效，导致无限循环风险。  
    - **标签**：`priority/P2` `type/bug` `welcome-pr`，安全相关。  
    - 链接：[#4999](https://github.com/QwenLM/qwen-code/issues/4999)

---

## 重要 PR 进展（10 条）

1. **#4890 – 新增 `/cd` 命令**  
   - 允许在 CLI 中切换工作目录，无需重启会话。包含目录验证、信任提示、工作区根目录迁移。  
   - 作者：qqqys  
   - 链接：[#4890](https://github.com/QwenLM/qwen-code/pull/4890)

2. **#4996 – 移植 declarative-agent 的 mcpServers + hooks 支持**  
   - 实现对 Claude Code 2.1.168 声明式 agent 的 `mcpServers` 和 `hooks` 字段解析与运行时调用，替换 YAML 解析。  
   - 作者：LaZzyMan  
   - 链接：[#4996](https://github.com/QwenLM/qwen-code/pull/4996)

3. **#4866 – 将 PR 分类流水线拆分为 4 阶段**  
   - 替换单体 triage 脚本，引入多阶段 Pipeline（resolve → product-decision → review → merge）。提升 CI 效率。  
   - 作者：yiliang114  
   - 链接：[#4866](https://github.com/QwenLM/qwen-code/pull/4866)

4. **#5009 – 修复 `extensions new` 在缺失内置示例时的错误**  
   - 当发行版不包含示例目录时，`qwen extensions new` 不再失败，并新增完整脚手架。  
   - 作者：BZ-D  
   - 链接：[#5009](https://github.com/QwenLM/qwen-code/pull/5009)

5. **#4947 – Workflow P2：实现 parallel() + pipeline() 并发扇出**  
   - 在 P1 顺序 agent() 基础上增加并行原语，最多 16 个 agent 并发，使用滑动窗口控制。  
   - 作者：LaZzyMan  
   - 链接：[#4947](https://github.com/QwenLM/qwen-code/pull/4947)

6. **#5006 – 清理 daemon 日志并类型化 MCP 重启**  
   - 去除冗余日志，对 MCP 服务重试/重启进行类型化处理，提升可观测性和稳定性。  
   - 作者：doudouOUC  
   - 链接：[#5006](https://github.com/QwenLM/qwen-code/pull/5006)

7. **#4909 – 支持从本地/远程归档文件安装扩展**  
   - 允许通过 `.zip` / `.tar.gz` 离线安装扩展，复用现有验证、转换流程。  
   - 作者：kkhomej33-netizen  
   - 链接：[#4909](https://github.com/QwenLM/qwen-code/pull/4909)

8. **#4897 – 持久化文件历史快照，实现跨会话 `/rewind`**  
   - 将 `FileHistorySnapshot` 写入 JSONL，使回退功能在会话恢复后仍可用。  
   - 作者：doudouOUC  
   - 链接：[#4897](https://github.com/QwenLM/qwen-code/pull/4897)

9. **#4971 – 减少 CLI 中交互式工具输出的内存占用**  
   - 对大型 tool-output 显示元数据进行压缩，优化 scheduler 状态与 UI 历史记录。  
   - 作者：kkhomej33-netizen  
   - 链接：[#4971](https://github.com/QwenLM/qwen-code/pull/4971)

10. **#5004 – 持久化 cron 任务：`/loop` 可跨重启存活**  
    - `/loop` 命令创建的定时任务可保存到 `.qwen/scheduled_tasks.json`，下次启动自动恢复。默认仍为会话级，可选持久化。  
    - 作者：tanzhenxin  
    - 链接：[#5004](https://github.com/QwenLM/qwen-code/pull/5004)

---

## 功能需求趋势

- **本地 / 自定义模型支持**：多次出现添加 OpenAI 兼容 LLM 的困难（#3384），以及 UI 对自定义 Provider 模型添加不够友好（#4814），表明用户群体正在从纯云端向混合部署扩展。
- **会话持久化与恢复**：#4964（截断恢复）、#4999（goal 迭代计数重置）、#4897（/rewind 跨会话）等说明用户对长会话的连续性有刚性需求。
- **IDE 与插件集成**：#4888（IDEA 插件）、#4991（VS Code 1.124 兼容性）暴露了插件生态的稳定性和功能完备性有待提升。
- **用户画像 / 上下文控制**：#4898 希望自由约束 skill 自动提炼，避免污染，说明用户对 AI “记忆”的精细管控需求增长。
- **MCP 与动态工作流**：多个 PR（#4996、#4947、#4713）围绕 MCP 服务器、工作流并发、权限冒泡展开，开发者正加大在 agent orchestration 方向的投入。

---

## 开发者关注点

- **版本兼容性**：VS Code 升级至 1.124.0 后，Qwen Code 0.16 无法启动，需回退至 0.15.1（#4991）。这提示版本同步测试需加强。
- **命令行工具依赖**：`/copy` 命令在 SSH 环境下因缺少 `xclip`/`xsel` 而不可用（#4926），建议通过转义序列实现跨平台复制。
- **统计准确性**：statusline 显示的 tokens 数字与用户预期严重不符（#4951），引起对计费透明度的担忧。
- **PR 管理流程**：#4987 指出 PR #4779 无理由回退已合并功能，社区希望强制要求冲突 PR 内解决而非静默回退，提升协作规范性。
- **内存与性能**：多位贡献者提交了内存优化相关 PR（#4971、#4868），社区对大规模对话下的资源消耗十分敏感。

---

如有遗漏或错误，欢迎指正。数据截止于 2026-06-12 协调世界时。  
*日报由 AI 自动生成，仅供参考。*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

好的，各位开发者好。我是你们的技术分析师。今天（2026年6月12日）的社区日报已出炉，我们聚焦于 **CodeWhale**（原 `deepseek-tui`）的最新动态。今天的关键词是：**品牌重塑、QoL优化与Agent能力深化**。

---

### 2026-06-12 DeepSeek TUI (CodeWhale) 社区动态日报

#### 1. 今日速览

今天，项目正式发布了品牌重塑版本 v0.8.58，标志着从 `deepseek-tui` 向 **CodeWhale** 的全面迁移。社区讨论热度不减，核心议题集中在 **Agent 推理过程的国际化（尤其是思考链路的语言问题）** 以及 **子Agent（Sub-Agent）架构带来的UI卡死与可靠性挑战**。主开发者 @Hmbown 开始密集规划 v0.8.59 版本，重点聚焦于稳定性、TUI优化和新特性整合。

#### 2. 版本发布

**v0.8.58: 品牌重塑与迁移里程碑**
- **内容概要**：此版本是项目的正式更名版本，`CodeWhale` 成为规范的名称、命令和npm包名。旧的 `deepseek-tui` npm包已弃用，不再接收更新。
- **迁移指引**：`v0.8.x` 系列旧版本用户需参考 `docs/REBRAND.md` 完成迁移。
- **链接**: [v0.8.58 Release](https://github.com/Hmbown/DeepSeek-TUI/releases/tag/v0.8.58) (请注意，由于品牌重命名，仓库本身可能也已迁移，请关注社区通知)

#### 3. 社区热点 Issues (Top 10)

1.  **#3098 - v0.8.59 执行路线图** (评论: 5, 👍: 0)
    - **重要性**: 🔥🔥🔥🔥🔥 **最高优先级**。主开发者 @Hmbown 亲自制定了v0.8.59的开发路线图，将原本属于v0.8.60的工作（如Provider模型修正、子Agent架构、WhaleFlow工作流、国际化等）提前纳入。这是社区未来几周所有工作的纲领性文件。
    - **链接**: [#3098](https://github.com/Hmbown/CodeWhale/issues/3098)

2.  **#1120 - 缓存命中率问题** (评论: 21, 👍: 0)
    - **重要性**: 🔥🔥🔥🔥  **顽固性Bug**。用户报告即使在相同项目上修改，`input_cache_miss` 比率仍然异常。19+条的评论表明多个用户遇到了此问题，开发者正在持续排查其他可能导致缓存命中率降低的原因。
    - **链接**: [#1120](https://github.com/Hmbown/CodeWhale/issues/1120)

3.  **#683 - 强制模型使用特定语言思考** (评论: 15, 👍: 0)
    - **重要性**: 🔥🔥🔥🔥 **高需求特性**。用户希望强制模型（如DeepSeek V4）的推理思考链路使用中文，而非默认的英文。即使修改了“记忆”，模型依然输出英文思考过程，这成为了非英语母语用户的一大痛点。
    - **链接**: [#683](https://github.com/Hmbown/CodeWhale/issues/683)

4.  **#1118 - 语言配置为中文，但“思考”输出仍是英文** (评论: 8, 👍: 0)
    - **重要性**: 🔥🔥🔥  **#683的延续**。一个具体的用户反馈，确认了即使全局语言设置为中文，模型的`thinking`输出仍然为英文。这与`#683`问题密切相关，是用户对该功能缺失的直接证据。
    - **链接**: [#1118](https://github.com/Hmbown/CodeWhale/issues/1118)

5.  **#2766 - UI重构需求** (评论: 8, 👍: 0)
    - **重要性**: 🔥🔥🔥 **核心UX问题**。用户明确指出复制输出困难，并且确认弹窗会遮挡主界面，显示大量无关信息。这直接影响了日常使用效率。
    - **链接**: [#2766](https://github.com/Hmbown/CodeWhale/issues/2766)

6.  **#861 - 思考块冻结/截断/丢失** (评论: 7, 👍: 0)
    - **重要性**: 🔥🔥🔥 **关键Bug**。用户报告了一类“思考崩塌”问题：模型的推理块在流式输出时，会冻结、被静默截断（尤其是超过4行时）或完全消失。这是Agent可靠性的一个严重问题。
    - **链接**: [#861](https://github.com/Hmbown/CodeWhale/issues/861)

7.  **#3095 - 子Agent扩散规划导致UI卡死** (评论: 2, 👍: 0)
    - **重要性**: 🔥🔥🔥 **新架构痛点**。在正常使用中，当主模型决定启动多个子Agent时，UI会显示 `working ... (waiting for model)` 并持续数分钟，不向用户反馈子Agent状态。这使得工具感觉像“死机”了一样。
    - **链接**: [#3095](https://github.com/Hmbown/CodeWhale/issues/3095)

8.  **#3145 - 为浏览器和UI任务添加可视化检查工件** (评论: 1, 👍: 0)
    - **重要性**: 🔥🔥🔥 **前瞻性功能**。主开发者研究了Cursor的Design Mode，旨在为Agent提供更丰富的证据循环（如选中的元素、布局关系、代码上下文等），提升UI任务的执行质量。
    - **链接**: [#3145](https://github.com/Hmbown/CodeWhale/issues/3145)

9.  **#1812 - Windows下TUI间歇性冻结** (评论: 5, 👍: 0)
    - **重要性**: 🔥🔥 **平台兼容性**。在Windows 11上，TUI会间歇性完全无响应（无键盘输入、屏幕不更新），但进程未崩溃。影响特定平台用户的核心体验。
    - **链接**: [#1812](https://github.com/Hmbown/CodeWhale/issues/1812)

10. **#1920 - 非wlroots Wayland合成器上剪贴板复制失效** (评论: 4, 👍: 0)
    - **重要性**: 🔥🔥 **小众但关键**。在Arch Linux下的`niri`等非wlroots的Wayland环境中，鼠标选中并复制文本的操作会静默失败，影响Linux用户的使用。
    - **链接**: [#1920](https://github.com/Hmbown/CodeWhale/issues/1920)

#### 4. 重要 PR 进展 (Top 10)

1.  **#3141 - `get_thread_detail` 性能优化（N+1修复）** (OPEN)
    - **内容**: 通过批量读取 `items` 目录并按 `turn_id` 分组，修复了 `get_thread_detail` 接口在遍历每个`turn`时重复读取目录的N+1查询问题。
    - **链接**: [#3141](https://github.com/Hmbown/CodeWhale/pull/3141)

2.  **#3140 - 修复Hook中的命令注入漏洞** (OPEN)
    - **内容**: 修复了安全漏洞。Hook命令不再直接传给系统shell执行，避免了shell元字符扩展和代码执行风险。
    - **链接**: [#3140](https://github.com/Hmbown/CodeWhale/pull/3140)

3.  **#3139 - 并行化技能同步** (OPEN)
    - **内容**: 将技能注册表的同步操作从顺序执行改为并发执行，大幅减少了网络I/O等待时间。
    - **链接**: [#3139](https://github.com/Hmbown/CodeWhale/pull/3139)

4.  **#3128 - 使用 `SearchContext` 重构 `walk_for_completions`** (OPEN)
    - **内容**: 针对函数参数过多、复杂度高的问题，引入`SearchContext`结构体将5个相关搜索参数打包传递，提升了代码的可维护性。
    - **链接**: [#3128](https://github.com/Hmbown/CodeWhale/pull/3128)

5.  **#3129 - 移除未使用的 `stop_sequence` 字段和死代码属性** (OPEN)
    - **内容**: 清理了 `StreamEvent` 等结构体中未使用的 `stop_sequence` 字段，移除了大量 `#[allow(dead_code)]` 标注，净化了代码库。
    - **链接**: [#3129](https://github.com/Hmbown/CodeWhale/pull/3129)

6.  **#3135 - 移除未使用的 `prompt_persist` 模块** (OPEN)
    - **内容**: 删除了整个未被引用的 `prompt_persist.rs` 文件及其模块声明，减少了代码冗余。
    - **链接**: [#3135](https://github.com/Hmbown/CodeWhale/pull/3135)

7.  **#3138 - 测试: 添加 `ToolError::path_escape` 测试** (OPEN)
    - **内容**: 增加了对 `ToolError::path_escape` 构造函数的单元测试，提升错误处理的代码覆盖率。
    - **链接**: [#3138](https://github.com/Hmbown/CodeWhale/pull/3138)

8.  **#3136 - 测试: 添加 `ToolError::invalid_input` 测试** (OPEN)
    - **内容**: 为 `ToolError::invalid_input` 构造函数添加了单元测试。
    - **链接**: [#3136](https://github.com/Hmbown/CodeWhale/pull/3136)

9.  **#3137 - 测试: 为 `release_base_url_from_env` 添加测试** (OPEN)
    - **内容**: 由于函数依赖环境变量，测试难度高。此PR使用`serial_test` crate为`release_base_url_from_env`函数添加了安全可靠的测试场景。
    - **链接**: [#3137](https://github.com/Hmbown/CodeWhale/pull/3137)

10. **#3122 - 测试: 测试 `fetchRepoStats` 函数** (OPEN)
    - **内容**: 为Web端 `github.ts` 文件中的 `fetchRepoStats` 函数编写了单元测试，覆盖了成功、失败、无授权等场景。
    - **链接**: [#3122](https://github.com/Hmbown/CodeWhale/pull/3122)

#### 5. 功能需求趋势

从今日的议题和PR中，可以提炼出社区最关注的四个功能发展方向：

1.  **子代理架构的深化与稳定**: 社区和主开发者都在积极探索子Agent（Sub-Agent）能力。需求不仅仅是实现，更是围绕其**UI反馈、任务状态跟踪、错误恢复机制**的完善，使其成为一个可靠的生产力工具。
2.  **TUI 稳定性与用户体验(QoL)提升**: 解决“UI卡死”、“思考块丢失”、“复制困难”等基础痛点是当前的第一要务。同时，社区也表达了对 **任务栏进度、标题动画、完成提示音**等微交互的渴望。
3.  **配置与自动化的“智能”升级**: 开发者不满足于手动切换Provider，对 **自动Fallback链** 的需求强烈。同时，**智能上下文压缩**和**执行策略的持久化规则** 被视为提升效率和安全的必要条件。
4.  **安全与可审计性**: 修复命令注入漏洞 (#3140) 和提出“自然语言自动审查策略” (#3144) 表明，社区对**Agent安全执行**和**结果可审计**的要求正在提升，不满足于“问一问”式的交互。

#### 6. 开发者关注点

结合社区反馈，以下是开发者最为痛心的几个高频问题和痛点：

-   **痛点一：缓存命中率不稳定**: “对同样的项目进行修改”却无法命中缓存 (#1120)，直接导致了重复计算和Token浪费，严重影响开发效率。
-   **痛点二：多语言思考链路失控**: 用户强制设置后，模型的“内心独白”（thinking）依然固执地使用英文 (#683, #1118)。对于非英语母语的开发者，理解和干预模型的推理过程变得异常困难。
-   **痛点三：TUI“假死”与“无响应”**: 无论是Windows上的冻结 (#1812) 还是子Agent扩散导致的卡死 (#3095)，用户对“不知道任务状态”的焦虑感非常强烈，迫切需要一个清晰的状态反馈机制。
-   **痛点四：首次配置引导缺失**:  用户反映，首次初始化时未能引导用户配置API Key，且`config.toml`文件未自动创建 (#759)。糟糕的开箱体验劝退了部分新用户。
-   **痛点五：上下文饱和时界面卡死**: 当上下文接近100%（约1M Token）时，UI事件循环几乎被“饿死”，导致完全无响应 (#1722)。这是一个在高强度使用中极易触发但影响巨大的问题。

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*