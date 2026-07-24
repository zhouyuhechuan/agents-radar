# AI CLI 工具社区动态日报 2026-07-24

> 生成时间: 2026-07-24 01:59 UTC | 覆盖工具: 9 个

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

好的，作为专注于 AI 开发工具生态的资深技术分析师，我将根据您提供的 2026-07-24 各主流 AI CLI 工具的社区动态数据，为您呈现一份横向对比分析报告。

---

### AI CLI 工具生态横向对比分析报告 (2026-07-24)

#### 1. 生态全景

当前 AI CLI 工具生态呈现出 **“群雄逐鹿，聚焦可靠性”** 的态势。各工具在基础能力趋同后，社区重心正从“功能堆叠”转向 **“稳定性、安全性与平台兼容性”**。连接中断、会话管理、计费透明度成为跨工具的普遍痛点，而 **MCP 协议集成**与 **Agent 的沙箱安全控制**则是当前最关键的差异化竞争点。整体市场处于快速迭代期，社区对 Bug 的容忍度降低，对 “开箱即用” 的稳定体验要求显著提高。

#### 2. 各工具活跃度对比

| 工具 | 热点 Issues (数量) | 重要 PR (数量) | 版本发布 | 社区活力判断 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 极高 (10条，累计数百评论) | 低 (4条) | 无 | **高**，虽新PR少，但Issue讨论激烈，用户基数大，问题反馈集中。 |
| **OpenAI Codex** | 高 (10条，累计百条评论) | 极高 (10条) | `v0.146.0-alpha` x2 | **极高**，版本迭代频繁，PR合并活跃，Windows相关问题集中爆发。 |
| **Gemini CLI** | 高 (10条，Agent稳定性相关) | 高 (10条，含基础设施建设) | 无 | **高**，PR关注基础设施（PR Generator），社区Bug反馈集中在Agent核心行为。 |
| **GitHub Copilot CLI** | 中 (10条) | 极低 (2条，无效) | `v1.0.74` | **中**，发布新版（支持Open Plugin Spec），但PR停滞，社区关注点在于会话管理和MCP继承。 |
| **Kimi Code CLI** | 低 (6条) | 高 (10条，大部分同一贡献者) | 无 | **高**，代码贡献活跃，主要由核心开发者在推动大量Bug修复和优化。 |
| **OpenCode** | 极高 (50条更新) | 极高 (50条更新) | 无 | **极高**，社区最活跃，Issues和PR数量均领先，用户对功能、UI、计费讨论热度高。 |
| **Pi** | 中 (10条) | 高 (10条) | 无 | **中**，社区讨论相对技术化，聚焦于模型配置、扩展生态和终端UI细节打磨。 |
| **Qwen Code** | 中 (10条) | 高 (10条) | `v0.20.1-nightly` | **高**，问题类型多样（外部记忆、MCP、TUI体验），PR产出丰富，迭代速度快。 |
| **DeepSeek TUI** | 高 (10条) | 中 (4条) | 无 (v0.9.1审查中) | **高**，处于重大版本发布前夜，社区聚焦在安全审查、并发可靠性和启动崩溃等关键问题上。 |

#### 3. 共同关注的功能方向

多个工具的社区需求呈现出显著的趋同性：

- **MCP 生态融合与继承**: **Claude Code** (#41836)、**GitHub Copilot CLI** (#4143)、**Kimi Code CLI** (#2548) 和 **OpenCode** (#38579) 的社区都在讨论 MCP 会话标识、工具继承、以及 CLI 与 IDE 之间 MCP 能力互通的问题。这表明 MCP 协议的标准化和跨平台一致性是下一阶段的关键。
- **会话管理与连接稳定性**: **Claude Code** (ECONNRESET, #5674)、**OpenCode** (重连风暴, #36285)、**Gemini CLI** (Shell执行卡死, #25166) 均在抱怨连接中断、会话挂起、状态不同步等问题。这是当前最影响用户体验的“卡脖子”问题。
- **计费透明度与策略优化**: **Claude Code** (Fable 5计费冲突, #79337)、**OpenCode** (内容过滤器误报收费, #35475) 和 **Gemini CLI** (状态显示矛盾) 都突出了计费逻辑不透明、误扣费、配额显示不一致等矛盾，用户对成本的可预测性要求提高。
- **权限与安全控制**: **Claude Code** (路径权限拒绝, #80736) 和 **DeepSeek TUI** (子代理沙箱, #4042) 都聚焦于细粒度权限控制。这反映了随着 Agent 能力增强，其操作权限的“安全护栏”建设成为刚需。
- **Windows 平台兼容性**: **OpenAI Codex** (CPU饱和, #34879)、**Kimi Code CLI** (插件崩溃, #2553)、**GitHub Copilot CLI** (WSL2剪贴板失效, #3534) 等大量 Windows 专属 Bug 涌现，说明跨平台稳定性是该生态普遍面临的严峻挑战。

#### 4. 差异化定位分析

- **Claude Code & OpenAI Codex**: 作为 **“第一梯队”**，背靠最强大的模型公司。社区讨论集中在 **计费策略、模型切换 (Fable vs Opus) 和深层 IDE 集成**。它们的挑战不是“能不能做”，而是“如何优化体验和成本”。
- **Gemini CLI & Qwen Code**: 强调 **“Agent 行为可预测性”**。社区大量Issue指向子代理决策不透明、技能未主动调用等核心逻辑问题（如 #22323）。这表明它们在追求 Agent 自主性的同时，也在努力解决“自主”带来的不确定性。
- **Kimi Code CLI & Pi**: 侧重于 **“用户体验打磨”**。Kimi 的 PR 集中在 Shell 补全、Windows 乱码、插件管理等细节修复；Pi 则专注于 TUI 局部重绘、模型配置热重载等终端交互优化。它们的竞争点在开发者的“手感和工作流流畅度”。
- **GitHub Copilot CLI & DeepSeek TUI (CodeWhale)**: 聚焦 **“插件与扩展生态”**。Copilot CLI 的新版本核心是支持 Open Plugin Spec；DeepSeek TUI 发布前的核心议题是安全检查、数据库并发、MCP 服务器启动等基础设施问题。它们的成败将取决于其生态繁荣度和基础设施的健壮性。
- **OpenCode**: 作为 **“社区驱动的功能试验田”**，其功能需求最广（模型自动发现、UI自定义、MCP转发），Bug类型也最丰富（计费、子进程残留、渲染器崩溃）。社区更像一个大型众测平台，功能和 Bug 的多样性远超其他工具。

#### 5. 社区热度与成熟度

- **社区最活跃**: **OpenCode** 在 Issue 和 PR 数量上远超其他工具，社区参与度最高，功能讨论和 Bug 反馈空前活跃。
- **迭代速度最快**: **OpenAI Codex** 和 **Qwen Code** 保持着较快的发版和 PR 合并节奏，产品迭代周期短。
- **风险与声量并存**: **Claude Code** 虽 Issue 数量不多，但每个 Issue 的评论量和“👍”数极高（如 #29006 获 114 赞），且屡现“P0”级别致命 Bug，说明其用户基数巨大，对产品稳定性高度敏感。
- **处于发布前冲刺期**: **DeepSeek TUI** 处于 v0.9.1 发布前的密集审查期，社区活动围绕安全、稳定、数据完整性展开，显示出维护者对软件质量负责任的态度。
- **功能同质化风险**: 多个工具的 PR 内容高度重合（如修复 MCP、编码兼容性、Shell 交互），表明核心功能已趋同，差异化空间正在缩小。

#### 6. 值得关注的趋势信号

1.  **“稳定性”成为新护城河**: 当工具都能“做出”AI Coding Agent时，谁能 “稳定地不出错” 将成为核心竞争力。社区对连接断开、会话挂起、背景进程残留等问题的容忍度极低。
2.  **“安全与信任”是下沉市场敲门砖**: 从 DeepSeek TUI 的沙箱审查到 Claude Code 的权限规则，社区不再满足于“能干活”，开始要求 “干得安全”。这将是企业级采纳的最后一道门槛。
3.  **“多模型/多提供商”不再是优势，而是默认配置**: 几乎所有工具都面临模型切换、模型配置、模型兼容性的 Bug 挑战。这已经从一个“卖点”变成了一个必须解决好的“基础运维问题”。
4.  **“MCP 协议”是生态之战的制高点**: 谁能原生、丝滑地支持 MCP 标准，并解决好跨应用（CLI vs IDE）的工具继承，谁就可能成为开发者的“中心控制台”，锁定用户生态。
5.  **“远程协作”需求从可选变为必需**: Claude Code (#29006) 和 Kimi Code CLI (#1282) 的远程控制功能需求都获得了极高的社区点赞。这表明 AI 编程工具正在从个人生产力工具向“单人多端”或“多人协作”平台演进。

**对开发者的建议**: 在选择 AI CLI 工具时，**请优先考虑其在稳定性和安全性上的硬伤修复记录**，而非功能数量。对于 Windows 用户，建议重点关注 **OpenAI Codex** 和 **Kimi Code CLI** 的近期更新日志，以评估其在您工作环境下的表现。对于深度依赖插件生态的开发者，**GitHub Copilot CLI** 的 Open Plugin Spec 支持值得密切关注。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，这是针对 `anthropics/skills` 仓库数据（截止 2026-07-24）的社区热点分析报告。

---

### Claude Code Skills 社区热点报告 (2026-07-24)

#### 1. 热门 Skills 排行 (Top 5-8 PRs)

以下为社区讨论最热烈、关注度最高的 Pull Requests，代表了社区最关心的 Skill 功能和待解决的问题。

1.  **`fix(skill-creator): run_eval.py always reports 0% recall` (PR #1298)**
    *   **功能**: 修复 `skill-creator` 工具链的核心组件 `run_eval.py`，该组件在评估 Skill 描述时始终报告 0% 的召回率，导致开发者无法有效优化 Skill 描述。
    *   **社区热点**: 这是当前社区讨论的绝对焦点。该 PR 引用了多个复现此 Bug 的 Issue（#556, #1099, #1061），并集成了多项修复，包括 Windows 兼容性、触发器检测和并行工作进程。它直接触及了 Skill 开发体验的核心痛点。
    *   **状态**: **OPEN**
    *   **链接**: [PR #1298](https://github.com/anthropics/skills/pull/1298)

2.  **`Add document-typography skill` (PR #514)**
    *   **功能**: 提供一个用于文档排版质量控制的 Skill，专门解决 AI 生成文档中的常见排版问题，如孤行（orphan）、寡段（widow）和编号错位。
    *   **社区热点**: 这是一个高度实用、解决普遍痛点的 Skill。社区讨论肯定了这类问题在 AI 生成文档中的普遍性，反映出用户对“即用型”高质量微调工具的需求。
    *   **状态**: **OPEN**
    *   **链接**: [PR #514](https://github.com/anthropics/skills/pull/514)

3.  **`feat(skills): add self-audit — mechanical verification + four-dimension reasoning quality gate (v1.3.0)` (PR #1367)**
    *   **功能**: 引入一个全新的“自我审计”Skill，在输出交付前进行“机械验证”（文件是否存在）和“四维推理质量审查”（按损害严重性排序）。
    *   **社区热点**: 概念新颖且全面，试图解决 AI 输出质量难以保证的核心问题。这代表了社区对 LLM 输出“可信度”和“可靠性”的更高要求。
    *   **状态**: **OPEN**
    *   **链接**: [PR #1367](https://github.com/anthropics/skills/pull/1367)

4.  **`Add pyxel skill for retro game development` (PR #525)**
    *   **功能**: 为 `pyxel-mcp`（一个 Pyxel 复古游戏引擎的 MCP 服务器）添加专用 Skill，支持创建像素/复古风格 8-bit 游戏。
    *   **社区热点**: 展示了 Skill 与 MCP（Model Context Protocol）服务器生态结合的潜力。它不仅是 Skill，更是一个特定工具的使用代理，体现了社区对“专业知识+工具调用”组合的兴趣。
    *   **状态**: **OPEN**
    *   **链接**: [PR #525](https://github.com/anthropics/skills/pull/525)

5.  **`Add ODT skill — OpenDocument text creation and template filling and parse ODT to HTML` (PR #486)**
    *   **功能**: 增加对 OpenDocument (.odt, .ods) 格式的支持，包括创建、填写模板和转换为 HTML。
    *   **社区热点**: 反映了社区对 **多格式支持和企业级办公自动化** 的强烈需求。对于使用 LibreOffice 或需要严格遵循开源标准的用户来说，此 Skill 价值巨大。
    *   **状态**: **OPEN**
    *   **链接**: [PR #486](https://github.com/anthropics/skills/pull/486)

6.  **`feat: add testing-patterns skill` (PR #723)**
    *   **功能**: 提供一个全面的测试模式 Skill，涵盖单元测试（AAA 模式）、React 组件测试、集成测试和 E2E 测试的最佳实践。
    *   **社区热点**: 软件测试是开发者社区的永恒主题。此 PR 旨在让 Claude 遵循成熟的测试框架和模式，提升 AI 编写代码的可靠性和可维护性，需求非常实际。
    *   **状态**: **OPEN**
    *   **链接**: [PR #723](https://github.com/anthropics/skills/pull/723)

7.  **`fix(skill-creator): warn on unquoted description with YAML special characters` & `Detect unquoted YAML special characters in description fields` (PR #539 & #361)**
    *   **功能**: 这两个 PR 都旨在改进 `skill-creator` 的验证功能，避免因 YAML 格式问题导致 Skill 描述解析错误。
    *   **社区热点**: 属于“开发者体验”优化。这类基础性验证工具的缺失会给 Skill 编写者带来迷惑的 Bug。社区对此类问题的积极反馈和重复提交，表明开发者需要一个更健壮、容错性更高的 Skill 开发环境。
    *   **状态**: **OPEN**
    *   **链接**: [PR #539](https://github.com/anthropics/skills/pull/539) [PR #361](https://github.com/anthropics/skills/pull/361)

---

#### 2. 社区需求趋势 (来自 Issues)

从 Issues 中可以看出社区最迫切的需求和期待方向：

1.  **安全与可信度核心诉求**: **#492** 是目前最受关注的 Issue，它尖锐地指出了社区 Skill 分发机制中的信任问题：在 `anthropic/` 命名空间下分发社区 Skill 可能造成“官方授权”的假象，导致用户无意中授予过高的权限。这说明社区不仅追求功能，更关注安全和信任基础设施的构建。

2.  **组织级协作与共享**: **#228** 期望能有原生的组织内 Skill 分享机制，而非手动下载和传输文件。这表明 Skills 已经从个人工具向团队协作资产演进，需要一个中心化的库或共享链接来简化工作流。

3.  **基础的开发者工具体验**: 多个高票 Issue (**#556**, **#1061**, **#1169**) 都指向 `skill-creator` 工具包自身的问题，特别是 `run_eval.py` 在各种环境下（尤其是 Windows）无法正常工作，导致优化循环失效。这表明 **社区对“用来创建 Skill 的工具”本身的稳定性和跨平台兼容性** 有非常强烈的诉求，这是 Skill 生态繁荣的基石。

4.  **Context 窗口与性能优化**: **#1329**（紧凑型记忆 Skill）和 **#1175**（处理 SPO 文档时的安全问题与上下文占用）反映了用户开始关注 Skill 本身对 Token 的消耗和对 Context 窗口的占用，追求更“轻量”的 Skill。

---

#### 3. 高潜力待合并 Skills

以下 PR 是评论活跃、尚未合并，但概念或技术价值极高，有望近期落地的 Skill：

1.  **skill-creator 修复套件 (PR #1298, #1099, #1050)**: 尽管它们是修复，但修复的是最核心的工具。一旦合并完成并发布，将极大改善 Skill 开发者的体验，释放整个生态的创作潜力。

2.  **self-audit (PR #1367)**: 这个 Skill 的概念非常超前且全面，将“质量审计”内化为一种 Skill，代表了 AI 应用的未来方向。其实现思路可能成为后续 Skill 开发的标准范式。

3.  **color-expert (PR #1302)**: 这是典型的“专业知识”加持型 Skill。它将复杂的色彩系统、色彩空间和调色板知识注入 Claude，对于设计师和前端开发者有极高价值。实用性很强，逻辑相对封闭，合并难度不高。

4.  **pyxel retro game (PR #525)**: 作为连接第三方 MCP 服务器的范例，其成功合并将证明 Skill 作为“O 型插件”连接外部工具的可行性，具有很强的示范效应。

---

#### 4. Skills 生态洞察

**一句话总结**: 当前社区的焦点正在从“创造各种花哨的 Skill”，**迅速转向解决 Skill 创作流程中的稳定性和可靠性问题**，并开始严肃关注生态的安全信任与协作共享机制。`skill-creator` 工具链的故障已成为阻碍社区发展的最大瓶颈。

---

# Claude Code 社区动态日报 | 2026-07-24

---

## 📋 今日速览

Fable 5 模型的计费与可用性问题成为社区焦点，多个 issue 指出 Max 计划用户被错误提示需要“usage credits”。同时，macOS 和 WSL 平台的连接中断（ECONNRESET / mid-response）问题持续困扰开发者，累计评论超 80 条。功能方面，远程控制会话和 VS Code 语法高亮的呼声依然高涨。

---

## 📦 版本发布

过去 24 小时内无新版本发布。

---

## 🔥 社区热点 Issues（10 条）

### 1. Fable 5 计费/可用性冲突（#79337）
- **评论 40 · 👍 12**
- **描述**：Max 计划用户在 7 月 20 日（Fable 5 成为 Max 标配首日）被强制降级至 Opus 4.8，并提示“Fable requires usage credits”。
- **链接**：[#79337](https://github.com/anthropics/claude-code/issues/79337)

### 2. macOS 持久 ECONNRESET 错误（#5674）
- **评论 50 · 👍 47**（24h 内更新）
- **描述**：macOS 下网络连接频繁断开，导致任务中断；Windows/Linux 无此问题。
- **链接**：[#5674](https://github.com/anthropics/claude-code/issues/5674)

### 3. 请求：支持远程控制 Claude Code 会话（#29006）
- **评论 35 · 👍 114**
- **描述**：要求在 Claude Desktop 应用中远程操控 CLI 会话，支持多设备协作。
- **链接**：[#29006](https://github.com/anthropics/claude-code/issues/29006)

### 4. VSCode/WSL 连接中段导致不可用（#69415）
- **评论 33 · 👍 65**
- **描述**：API 错误“Connection closed mid-response”频繁发生，任何任务都无法完成。
- **链接**：[#69415](https://github.com/anthropics/claude-code/issues/69415)

### 5. 权限规则拒绝特定路径（#80736）
- **评论 1 · 👍 0**（今日新开）
- **描述**：`Read`/`Grep`/`Edit` 对 `src/main/java/**` 路径被拒绝，但同一模块下其他路径正常。
- **链接**：[#80736](https://github.com/anthropics/claude-code/issues/80736)

### 6. MCP 服务器无法区分并发会话（#41836）
- **评论 14 · 👍 24**
- **描述**：Claude Code 连接 MCP 时未传递会话标识，服务端无法维护 per-conversation 状态。
- **链接**：[#41836](https://github.com/anthropics/claude-code/issues/41836)

### 7. 自动更新器无跨会话锁，重复下载 265MB（#79942）
- **评论 1 · 👍 0**
- **描述**：每个运行中的会话独立下载完整更新包，且失败后残留 0 字节版本文件。
- **链接**：[#79942](https://github.com/anthropics/claude-code/issues/79942)

### 8. VS Code 扩展聊天面板缺少语法高亮（#64968）
- **评论 7 · 👍 21**
- **描述**：代码块以纯文本显示，不识别语言标签，与 IDE 主题不匹配。
- **链接**：[#64968](https://github.com/anthropics/claude-code/issues/64968)

### 9. Fable 5 安全误报干扰人文/安全工作（#80741）
- **评论 0 · 👍 0**（今日新开）
- **描述**：94 次误报事件，在合法人文研究场景中被拦截，导致降级至 Opus 4.8。
- **链接**：[#80741](https://github.com/anthropics/claude-code/issues/80741)

### 10. 无关网页内容被注入助手响应（#80739）
- **评论 0 · 👍 0**（今日新开）
- **描述**：中文 AI 提示站点页脚及 JS 错误文本拼接到流式输出中，会话随后显示中断。
- **链接**：[#80739](https://github.com/anthropics/claude-code/issues/80739)

---

## 🔧 重要 PR 进展（全部 4 条）

### 1. [#41611] 为 Claude Code 补充缺失的 source
- **作者**：tornikeo｜**状态**：Open (2026-03-31 创建，24h 内更新)
- **描述**：添加缺失的源代码引用。
- **链接**：[PR #41611](https://github.com/anthropics/claude-code/pull/41611)

### 2. [#42604] 移除前端设计技能中的“复古未来主义”建议
- **作者**：TechyHaroon｜**状态**：Closed (2026-04-02 创建，24h 内更新)
- **描述**：删除过时的设计推荐。
- **链接**：[PR #42604](https://github.com/anthropics/claude-code/pull/42604)

### 3. [#80508] 修复自动关闭重复 Issue 脚本的分页问题
- **作者**：Serhii-Leniv｜**状态**：Open (2026-07-23 创建)
- **描述**：`auto-close-duplicates.ts` 在读取评论和 reactions 时未分页，只获取了前 30 条。
- **链接**：[PR #80508](https://github.com/anthropics/claude-code/pull/80508)

### 4. [#80495] 修复 `/ralph-loop` 将提示文本解析为 shell 代码的问题
- **作者**：Serhii-Leniv｜**状态**：Open (2026-07-23 创建)
- **描述**：`$ARGUMENTS` 直接替换到 shell 命令中，导致普通提示被当作代码执行。
- **链接**：[PR #80495](https://github.com/anthropics/claude-code/pull/80495)

---

## 📈 功能需求趋势

根据过去 24 小时更新的 Issues，社区最关注的功能方向包括：

1. **IDE 深度集成**：VS Code 语法高亮（#64968）、会话重命名同步至终端标签（#37628）、Spinner 动词自定义（#80742）。
2. **远程协作与多会话管理**：远程控制桌面 <-> CLI 会话（#29006）、MCP 会话标识传递（#41836）、更新器跨会话锁（#79942）。
3. **模型/计费优化**：Fable 5 可用性与计费策略（#79337, #79341, #80382）、PDF 读取时减少图片渲染 token（#80449）。
4. **权限与安全**：更细粒度的路径权限规则（#80736）、AutoMode 授权绕过修复（#73739）、Fable 5 安全引擎误报（#80741）。

---

## 👨‍💻 开发者关注点

| 痛点 / 高频反馈 | 相关 Issue | 严重程度 |
|----------------|------------|----------|
| 连接中断（ECONNRESET / mid-response） | #5674, #69415, #69336 | 🔴 严重 |
| Fable 5 计费误判导致无法使用 | #79337, #79341, #80382 | 🔴 严重 |
| 权限配置失效（允许规则仍被拦截） | #80736, #62135 | 🟠 较高 |
| 自动更新器重复下载 & 文件残留 | #79942 | 🟠 较高 |
| VS Code 扩展功能缺失（重命名同步、语法高亮） | #37628, #64968, #80742 | 🟡 中 |
| 会话内容异常（重复渲染、被删除、注入垃圾） | #49985, #80740, #80739 | 🟡 中 |
| MCP 协议不足（无会话标识、$ref 解析失败） | #41836, #76040 | 🟡 中 |

---

*数据来源：[GitHub - anthropics/claude-code](https://github.com/anthropics/claude-code) | 更新至 2026-07-24 23:59 UTC*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 | 2026-07-24

## 今日速览
- 发布两个 Rust 运行时 alpha 版本（`0.146.0-alpha.3.1` 和 `0.146.0-alpha.5`），累计合并多项基础设施和代理逻辑改进。
- Windows 平台性能问题集中爆发：`WmiPrvSE` CPU 占用全核饱和、长期线程上下文压缩失效、`apply_patch` 间歇性挂起等 Bug 获得高度关注。
- 社区对 `Conversation Compaction Telemetry`、多聊天窗口支持、官方 ChatGPT 对话导入等增强功能的呼声持续升高，超过 30 个 Issues 进入活跃讨论。

---

## 版本发布

### rust-v0.146.0-alpha.5
发布 `0.146.0-alpha.5`，包含近期多项基础设施优化和 Bug 修复。
- [发布链接](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.5)

### rust-v0.146.0-alpha.3.1
发布 `0.146.0-alpha.3.1`，为前序版本的补丁发布。
- [发布链接](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.3.1)

---

## 社区热点 Issues

### 1. #20214 – Codex App 在 Windows 11 Pro 上频繁卡顿/冻结
- **重要性**：75 条评论、72 个 👍，社区高度共鸣。用户反馈即便拥有充足系统资源（Ryzen 5 5600 + 32GB RAM），应用仍间歇性无响应。
- **社区反应**：多用户确认复现，讨论涉及 Electron 渲染线程、GPU 加速、以及视频编解码组件冲突。
- [Issue 链接](https://github.com/openai/codex/issues/20214)

### 2. #4003 – Windows 上修补文件出现混合换行符
- **重要性**：27 条评论、71 个 👍 的长期 Bug（2025 年 9 月开启），影响跨平台协作。
- **社区反应**：用户期望 Codex 自动识别源文件换行风格并保持一致，目前仅能手动修复。
- [Issue 链接](https://github.com/openai/codex/issues/4003)

### 3. #35032 – 桌面端自动压缩后上下文仪表仍显示 ~80%，导致重复压缩
- **重要性**：新增 Bug（2026-07-23），13 条评论，严重消耗配额和性能。
- **社区反应**：用户描述在长线程中压缩声称完成但上下文几乎未释放，进一步引发反复压缩循环。
- [Issue 链接](https://github.com/openai/codex/issues/35032)

### 4. #34879 – [P0 回归] Windows 桌面启动立即导致 WmiPrvSE 占用全部 CPU
- **重要性**：标记为 P0 回归，5 条评论但影响极大——32 逻辑核心 100% 饱和，应用完全不可用。
- **社区反应**：用户发现关闭 Codex 是唯一恢复方式，怀疑与 Windows Management Instrumentation 查询风暴有关。
- [Issue 链接](https://github.com/openai/codex/issues/34879)

### 5. #28074 – WSL 集成在全新安装后仍损坏
- **重要性**：11 条评论，Pro 订阅用户报告。WSL 是 Windows 开发者的核心特性，反复无法使用。
- **社区反应**：用户已尝试完全卸载重装、重置 WSL 内核，问题依然存在。
- [Issue 链接](https://github.com/openai/codex/issues/28074)

### 6. #33786 – Windows 26.715：完成的大线程每隔几秒完全重放，导致系统输入卡顿
- **重要性**：4 条评论，2 个 👍，但描述问题清晰——线程已完成后仍在后台全量回放，引起鼠标/键盘延迟。
- **社区反应**：回放频率约数秒一次，疑似渲染引擎缓存失效或状态管理 Bug。
- [Issue 链接](https://github.com/openai/codex/issues/33786)

### 7. #34290 – Windows 上 `apply_patch` 间歇性多分钟挂起
- **重要性**：4 条评论，影响频繁使用 patch 工具的开发者。挂起期间无反馈，只能强制结束。
- **社区反应**：用户提到挂起发生在中等规模文件应用补丁时，疑似与沙箱权限或文件锁定相关。
- [Issue 链接](https://github.com/openai/codex/issues/34290)

### 8. #22220 – 对话压缩遥测 / 上下文健康仪表板
- **重要性**：19 条评论、12 个 👍，长期需求（2026 年 5 月）。用户希望获得压缩何时发生、损失了多少上下文、压缩后可用的 token 数等透明信息。
- **社区反应**：获得 ChatGPT Pro/Max 用户支持，认为这是提升长会话可控性的关键特性。
- [Issue 链接](https://github.com/openai/codex/issues/22220)

### 9. #13036 – 支持多聊天窗口同时显示
- **重要性**：12 条评论、8 个 👍。当前 macOS App 仅支持单一活跃聊天窗口，无法多任务或多代理并行。
- **社区反应**：用户期望类似终端多标签页或分屏体验，以同时对比不同会话或协调子代理。
- [Issue 链接](https://github.com/openai/codex/issues/13036)

### 10. #31973 – Windows 远程控制卡在“正在重连...”，无恢复手段
- **重要性**：10 条评论，1 个 👍。QR 配对后远程连接丢失并永久卡住，只能关闭应用重新启动。
- **社区反应**：用户指出该问题在 Windows 11 + ChatGPT Mobile 远程控制场景下频繁触发。
- [Issue 链接](https://github.com/openai/codex/issues/31973)

---

## 重要 PR 进展

### 1. #35056 – 将 exec-server WebSocket 路由通过配置的代理
- **功能**：远程环境连接现在会遵循 Codex 的出站代理策略，包括断线重连时也使用配置的 HttpClientFactory。
- [PR 链接](https://github.com/openai/codex/pull/35056)

### 2. #35054 – 允许禁用 `update_plan` 工具
- **功能**：新增配置项 `tools.update_plan.enabled`，默认开启；关闭后模型将无法使用该工具，适用于需要控制计划更新行为的场景。
- [PR 链接](https://github.com/openai/codex/pull/35054)

### 3. #35049 – 注册 Guardian V2 特性标志
- **功能**：添加 `GuardianV2` 到特性注册表，暴露为 `features.guardianv2`，默认关闭。为下一代自动审查机制做准备。
- [PR 链接](https://github.com/openai/codex/pull/35049)

### 4. #35065 – 避免在工具搜索中重复列出延迟源
- **修复**：`DeferredToolWorldState` 已申明可用工具源，移除 `tool_search` 描述中的重复上下文，节省 token 并减少混淆。
- [PR 链接](https://github.com/openai/codex/pull/35065)

### 5. #35063 – 在全局状态中跟踪延迟工具命名空间
- **功能**：增加 `deferred_tool_world_state` 特性（默认禁用），向模型暴露延迟工具的命名空间和描述，支持动态工具可用性事件。
- [PR 链接](https://github.com/openai/codex/pull/35063)

### 6. #35029 – 保留跨命令审批的插件归属信息
- **功能**：在执行审批和 Guardian 评估事件中添加 `plugin_id` 和 `script_path` 字段，保证审计链路中插件来源可追溯。
- [PR 链接](https://github.com/openai/codex/pull/35029)

### 7. #35028 – 在 MCP 运行时更新后保留刷新的 Apps 工具
- **修复**：远程插件安装刷新工具目录后，新的 MCP 运行时不会因旧连接恢复而还原之前的工具列表。
- [PR 链接](https://github.com/openai/codex/pull/35028)

### 8. #35067 – 修复 Bazel 测试中平台特定数据配置
- **修复**：将 CLI 快照文件纳入 Bazel 测试运行时文件，限制 Windows 沙箱二进制测试仅运行在 Windows，标记受影响的 CLI 测试的布尔/可选参数。
- [PR 链接](https://github.com/openai/codex/pull/35067)

### 9. #35036 – 在 Guardian 会话中保留 Windows 沙箱代理设置
- **修复**：Guardian 审查命令运行时缺少父会话的代理端口环境变量，导致沙箱网络配置丢失。此 PR 保证代理设置正确继承。
- [PR 链接](https://github.com/openai/codex/pull/35036)

### 10. #35031 – 对线程归档和删除强制写入者所有权
- **修复**：分页线程只允许一个 app-server 进程写入。归档/删除操作必须获取分页写入锁，防止多个进程同时修改线程状态。
- [PR 链接](https://github.com/openai/codex/pull/35031)

---

## 功能需求趋势

根据过去 24 小时活跃的 Issues 分析，社区最关注的功能方向包括：

- **上下文透明化与压缩控制**：`Conversation Compaction Telemetry` (#22220) 获得持续支持，用户要求清晰显示压缩时机、压缩量、剩余上下文 token 和压缩后可用空间。
- **多聊天窗口/多会话管理**：`Support Display of Multiple Chats` (#13036) 呼声高，开发者希望同时查看和操作多个线程，特别是多代理协作场景。
- **官方 ChatGPT 对话与项目导入**：`Official ChatGPT transcript/project import connector` (#30636) 代表了一类跨平台无缝迁移数据的需求。
- **Windows 稳定性与性能修复**：从大量 Windows 相关 Bug（#20214、#34879、#33786、#34290 等）可看出，社区强烈期望优先解决桌面应用卡顿、CPU 耗尽、WSL 集成失效等问题。
- **插件/技能管理持久化**：`Plugins from built-in marketplace are deleted after restart` (#29103) 和 `skills/.system` 间歇性丢失 (#19265) 表明插件和技能的状态持久化是一大痛点。
- **远程控制与移动端配对可靠性**：iPad Pro 配对失败 (#30750)、Windows 远程控制卡住 (#31973) 等报告表明远程工作流程稳定性亟需提升。

---

## 开发者关注点

综合 Issue 反馈，开发者当前最突出的痛点与高频需求如下：

1. **Windows 性能瓶颈**：多个 P0/P1 级别的 CPU 饱和、应用卡顿、输入延迟问题直接阻碍日常使用。
2. **上下文压缩不透明且低效**：压缩后仍余 80% 上下文、反复压缩浪费配额，且缺乏任何可视监控。
3. **WSL 集成反复失效**：Windows 下 WSL 是主流的 Linux 开发环境，但整合体验频繁损坏，影响前后端全栈开发者。
4. **子代理/技能缓存泄漏**：`stale subagents` 无法关闭、`~/.codex/skills/.system` 被误删，导致模型失去可用技能，影响自动化工作流。
5. **代理与工具执行的“幻觉”**：Codex 在后台完成配置变更后即宣称功能可用，但用户在前台未看到实际变化（#35041、#35043），降低信任度。
6. **配额与状态显示矛盾**：不同的计费池（周额度 vs 模型额度、学分）显示不一致，且无全局错误提示（#35047、#35037），造成困惑和额外费用。

以上问题表明，Codex 团队应优先加强 Windows 平台的稳定性测试、完善上下文压缩的监控透明性、以及提升远程与 WSL 场景的鲁棒性。同时，社区对多会话和插件生态持久化的需求正在快速增长。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 | 2026-07-24

## 今日速览
今日社区无新版本发布，但围绕 Agent 核心稳定性涌现多个高优 Bug：子代理在达到最大轮次时误报成功（#22323）、通用代理执行简单任务时永久挂起（#21409）、以及 Shell 命令执行完成后“等待输入”死锁（#25166）。另一方面，项目团队在持续推动 PR 生成管道（PR Generator）的 Firestore 并发锁、容器编排和提示优化等大型基础设施代码合并。安全与认证修复也是今日 PR 的重点，包括无限认证循环、OAuth 令牌刷新和 HTTPS 强制等。

---

## 社区热点 Issues（10 条）

### 1. #22323 - 子代理在达到最大轮次后误报成功
- **重要性**：核心 Agent 行为 Bug，子代理 `codebase_investigator` 在超时后错误返回 `status: "success"` 和 `Termination Reason: "GOAL"`，实际是中断而非完成，导致用户被误导。
- **社区反应**：12 条评论，2 👍 ，已标记 `priority/p1` 但尚需重新测试。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/22323

### 2. #21409 - 通用代理在执行简单命令时永久挂起
- **重要性**：影响所有用户的基础功能，创建文件夹等操作都会导致无限等待，用户反馈等待长达一小时。
- **社区反应**：8 条评论，8 👍（今日最高赞），优先级 p1，持续关注。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/21409

### 3. #25166 - Shell 命令执行完成后仍显示“等待输入”并卡住
- **重要性**：核心交互 Bug，简单 CLI 命令完成后界面卡死，严重影响日常使用。
- **社区反应**：4 条评论，3 👍，优先级 p1，定性为 effort/medium。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/25166

### 4. #24353 - 组件级评估系统（EPIC）
- **重要性**：提升 Agent 可靠性的重要内部工程，已有 76 个行为评估测试，覆盖 6 个 Gemini 模型，未来将大幅减少回归。
- **社区反应**：7 条评论，仅 maintainer 可见，但影响深远。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/24353

### 5. #22745 - AST 感知的文件读取/搜索/映射评估
- **重要性**：探索通过抽象语法树提升工具调用精准度、减少 Token 消耗，可能显著改善大规模代码库下的表现。
- **社区反应**：7 条评论，1 👍，标记为 feature。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/22745

### 6. #21968 - Gemini 未充分使用自定义技能和子代理
- **重要性**：用户反馈模型几乎不主动调用已配置的技能或子代理，需强制指示才执行，违反用户预期。
- **社区反应**：6 条评论，标记为 bug，需重新测试。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/21968

### 7. #26522 - Auto Memory 无限重试低信号会话
- **重要性**：内存系统效率问题，低价值会话不断被重新提取，浪费 Token 和计算资源。
- **社区反应**：5 条评论，由 Maintainer 提出并推动修复。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/26522

### 8. #26525 - 自动内存未在前端确定性脱敏且日志泄漏
- **重要性**：安全缺陷，内容在发送模型前未脱敏，且日志可能记录技能内容。
- **社区反应**：4 条评论，优先级 p2，安全相关。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/26525

### 9. #22232 - 浏览器代理会话锁定恢复能力增强
- **重要性**：浏览器代理在持久模式下遇到锁定的配置文件即失败退出，缺少自动接管机制。
- **社区反应**：4 条评论，标记为 feature，社区期待改进。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/22232

### 10. #21983 - 浏览器子代理在 Wayland 下失败
- **重要性**：Linux Wayland 环境兼容性问题，浏览器代理报错后终止。
- **社区反应**：4 条评论，1 👍，需重新测试。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/21983

---

## 重要 PR 进展（10 条）

### 1. #28519 - 修复无限认证循环
- **内容**：在凭证保存后强制等待并添加 consent 参数，解决 #28430 的无限重定向。
- **状态**：OPEN，size/s，优先级 p1。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28519

### 2. #28523 - 强制文件密钥库的标签长度验证
- **内容**：为文件凭证存储配置显式的 128 位身份验证标签，提升加密健壮性。
- **状态**：OPEN，size/m，标记 need-issue。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28523

### 3. #28524 - Caretaker 分拣提示优化 + 编排器更新
- **内容**：引入 3 周提示爬山结果，新增 `code_explorer` 技能，分拣质量显著提升。
- **状态**：OPEN，size/m。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28524

### 4. #28433 - PR 生成器：迭代 Bug 修复状态机与容器入口
- **内容**：实现 Firestore 并发锁、AI 编码-评估循环、ESLint 分析等核心编排逻辑。
- **状态**：OPEN，size/xl。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28433

### 5. #28432 - PR 生成器：Firestore 双锁与测试工具
- **内容**：数据库接口层，提供事务锁、文档 ID 解析、生命周期状态枚举等。
- **状态**：OPEN，size/xl。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28432

### 6. #28509 - 过滤历史记录中的思考痕迹（thought parts）
- **内容**：当上下文管理关闭时，从 `getHistoryTurns` 中彻底移除内部思维/思考部分，防止重复推理块泄漏。
- **状态**：OPEN，size/m。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28509

### 7. #28481 - 修复 MCP OAuth 令牌刷新时使用存储的 client ID
- **内容**：解决动态客户端注册场景下刷新失败并删除凭据的问题，避免每次重新授权。
- **状态**：OPEN，size/m，优先级 p1。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28481

### 8. #28446 - 使用原生 fetch 进行 OAuth 令牌交换，避免“Premature close”
- **内容**：修复无头 VPS 上 `gemini login` 因 `Premature close` 失败的问题。
- **状态**：OPEN，size/m，优先级 p1。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28446

### 9. #28485 - 将 gemini-3.5-flash 加入模型选择器
- **内容**：解决 v0.51.0 用户无法选择新模型的问题（#28483）。
- **状态**：OPEN，size/m，优先级 p2。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28485

### 10. #28469 - 模型回退时轮换会话 ID 防止有状态 API 错误
- **内容**：当永久回退至 gemini-2.5-flash 时自动生成新 session ID，避免 `[API Error: Please submit a new query]`。
- **状态**：已合并（CLOSED）。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28469

---

## 功能需求趋势

从过去 24 小时更新的 Issues 中，社区最关注的功能方向包括：

1. **Agent 行为可预测性**：大量 issue 围绕子代理决策不透明（如超时误报）、技能未自动调用、浏览器代理状态恢复等，用户期望更可控、更可解释的 Agent 行为。
2. **内存系统的健壮性与安全性**：Auto Memory 的重试逻辑、日志脱敏、无效补丁处理等问题表明社区对长期记忆功能既期待又担心隐私泄漏。
3. **新模型与工具链支持**：gemini-3.5-flash 模型选择、AST 感知代码工具、Symlink 识别等，反映社区希望 CLI 紧跟模型更新并增强底层分析能力。
4. **终端/UI 体验优化**：Shell 执行后假死、VSCode 集成后的焦点丢失、终端 resize 闪烁等，开发者对交互流畅度要求高。
5. **安全与认证**：MCP OAuth 刷新、HTTPS 强制、凭证加密等是近期 PR 和 Issue 的密集区，安全基线正在加固。

---

## 开发者关注点

- **常见痛点**：Agent 挂起（尤其是通用代理和浏览器代理）、命令执行后状态不同步导致用户误操作、子代理配置被忽略、以及自动更新引入的意外行为（如子代理绕过权限设置）。
- **高频请求**：
  - 提供更详细的 Subagent 轨迹记录与分享（#22598）。
  - `settings.json` 配置能被所有 Agent 正确读取（#22267）。
  - 减少破坏性操作（如 `git reset --force`）的自动执行（#22672）。
  - 终端 resize 时实现高性能无闪烁重绘（#21924）。
- **反馈情绪**：整体积极但有挫败感，尤其是阻塞性 Bug（挂起、无限循环）反复出现。开发者希望团队优先修复 P1 稳定类问题，再推进新功能。

---

*数据来源：[github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报  
**2026-07-24** | 数据来源：github.com/github/copilot-cli

---

## 今日速览

昨天（2026-07-23）Copilot CLI 发布了 **v1.0.74 / v1.0.74-4**，重点支持 **Open Plugin Spec v1 插件清单和 MCP JSON 配置**，并修复了 IDE 集成在 MCP 服务器重载时的断连问题。社区热度集中在 **会话过大导致 CAPI 5 MB 限制** 带来的永久性卡死（#3767、#4097）以及 **MCP 工具继承与订阅** 等议题。另有大量 triage 状态的 bug 提交，涉及中断控制、剪贴板、代理指令等细节。

---

## 版本发布

### v1.0.74 / v1.0.74-4 （2026-07-23）

**新增**
- 支持 **Open Plugin Spec v1 插件清单**（plugin manifests）和 **mcp.json 配置文件**，允许插件通过标准格式声明 MCP 服务器。
- 子代理时间线可标识提示来自主代理或另一子代理（改进调试可见性）。

**修复**
- IDE 集成在 CLI 重新加载 MCP 服务器或切换目录后**可靠重连**，不再出现断连后无法恢复的问题。
- `/search` 栏打开时输入 `?` 不再被当作文本，而是正确弹出快速帮助。
- 其他稳定性修复。

> **注意**：v1.0.74-4 是 v1.0.74 的补充发布，变更内容基本一致。

---

## 社区热点 Issues（10 条最值得关注）

### 1. [#3767] 附件过大永久卡死会话（CAPI 5MB 限制，无恢复机制）  
🔗 [链接](https://github.com/github/copilot-cli/issues/3767)  
- **状态**：已关闭（但问题依然存在）  
- **重要性**：当附件（图片/文档）导致请求超过 CAPI 原生 5MB 限制时，会话直接报错且无法恢复，严重影响大文件场景。  
- **社区反应**：12 条评论，用户呼吁加入自动压缩或分块机制。

### 2. [#4097] apply_patch 删除二进制文件时将整个文件存入历史，永久超限  
🔗 [链接](https://github.com/github/copilot-cli/issues/4097)  
- **状态**：打开  
- **重要性**：`apply_patch` 删除大二进制文件时，`result.detailedContent` 存储了完整的文本 diff，导致后续请求始终超 5MB 限制，`/compact` 也无法解决。  
- **社区反应**：4 条评论，用户反馈这是触发 #3767 的常见原因。

### 3. [#3534] WSL2 ARM64：`/copy` 因 `cmd.exe` 引号错误失败  
🔗 [链接](https://github.com/github/copilot-cli/issues/3534)  
- **状态**：打开  
- **重要性**：影响 ARM64 版 WSL2 用户，clipboard 操作完全失效。  
- **社区反应**：5 条评论，4 个 👍，用户尝试各种 workaround 无效。

### 4. [#4143] CLI 应从已连接的 VS Code 实例继承 MCP 工具  
🔗 [链接](https://github.com/github/copilot-cli/issues/4143)  
- **状态**：打开（triaged）  
- **重要性**：当 CLI 接入 VS Code 后，无法使用 VS Code 中安装的 MCP 插件，导致工具分裂。  
- **社区反应**：5 个 👍，是 MCP 生态融合的核心需求。

### 5. [#4206] 环境页脚在 GitHub MCP 握手时永久显示“Loading:”  
🔗 [链接](https://github.com/github/copilot-cli/issues/4206)  
- **状态**：打开（triaged）  
- **重要性**：企业用户受组织 MCP 策略影响，页面假死，无法感知实际加载完成。  
- **社区反应**：2 个 👍，影响 Mac 用户。

### 6. [#4165] Windows 上 `copilot --resume` 在冷启动时挂起  
🔗 [链接](https://github.com/github/copilot-cli/issues/4165)  
- **状态**：打开  
- **重要性**：Windows 下从 PowerShell 恢复会话无限卡在“Resuming session...”。  
- **社区反应**：1 个 👍，用户指出先进入交互模式再手动 resume 可绕过。

### 7. [#2650] 应通知用户等待输入（阻塞提示不可见问题）  
🔗 [链接](https://github.com/github/copilot-cli/issues/2650)  
- **状态**：已关闭  
- **重要性**：长时间任务中，用户不知道 CLI 正在等待输入，导致无操作超时。  
- **社区反应**：5 条评论，提议增加视觉或声音提示。

### 8. [#4233] ACP 模式应发射 `usage_update` 以显示上下文窗口/AI 信用  
🔗 [链接](https://github.com/github/copilot-cli/issues/4233)  
- **状态**：打开  
- **重要性**：Zed 等 ACP 客户端无法展示 Copilot 上下文窗口和信用消耗，影响用户体验。  
- **社区反应**：2 个 👍，开发者期待快速实现。

### 9. [#4235] Ctrl+C 不再中断活跃的代理运行（回归）  
🔗 [链接](https://github.com/github/copilot-cli/issues/4235)  
- **状态**：打开（triage）  
- **重要性**：严重打断工作流，用户无法取消误操作，属于关键交互回归。  
- **社区反应**：刚刚提交，暂无评论。

### 10. [#3696] Alpine/musl 环境自动更新错误下载 linux-x64 包  
🔗 [链接](https://github.com/github/copilot-cli/issues/3696)  
- **状态**：已关闭  
- **重要性**：导致 musl 用户完全无法启动，影响容器/Docker 使用者。  
- **社区反应**：1 条评论，已发布修复但仍有残留问题。

---

## 重要 PR 进展

昨日仅 2 个 PR，且均无实质内容：

- **#4228**（已关闭）：撤回——因修改了文档而非私有 clipboard 运行时实现，源分支已删除。  
- **#3163**（打开）：内容为“ViewSonic monitor”，无实质性代码变更，疑似 spam。

**结论**：昨日无重要的代码合并或功能 PR 提交。社区活跃度主要体现在 Issue 讨论和版本发布。

---

## 功能需求趋势

从过去 24 小时更新的 Issues 中，社区最关注的功能方向为：

| 方向 | 代表 Issue | 需求概述 |
|------|------------|----------|
| **MCP 工具继承与同步** | #4143、#3125、#3073 | CLI 与 VS Code 共享 MCP 工具；MCP 工具变更应即时生效；支持资源订阅通知 |
| **会话大小管理与恢复** | #3767、#4097、#4214 | 附件/删除文件导致超限的自动恢复、压缩提示、透明降级 |
| **Windows 及跨平台兼容性** | #3534、#4165、#4235 | WSL2 剪贴板、Windows resume 挂起、Ctrl+C 中断回归 |
| **企业 / ACP 客户端体验** | #3161、#4233、#4206 | 企业认证、ACP 使用指标推送、MCP 握手状态透明 |
| **插件与 MCP 配置标准化** | v1.0.74 新功能、#4234 | 支持 Open Plugin Spec v1、插件 MCP 服务器工作目录问题 |
| **用户交互改进** | #2650、#4135、#4230、#4237 | 等待输入提示、hook 决策渲染优化、$EDITOR 编辑支持、静默丢弃 steering 消息 |
| **性能与内存** | #4199 | 会话更新后旧版本依然运行、空闲会话不释放内存 |

---

## 开发者关注点

1. **会话膨胀与限制**：  
   - 多位开发者遭遇“5MB CAPI 限制”导致会话永久卡死，且 `/compact` 无法清理删除二进制文件留下的历史。这是当前最痛的体验问题。  
   - 用户强烈建议实现自动压缩、分段发送或更优雅的降级提示。

2. **MCP 生态割裂**：  
   - CLI 和 VS Code 之间的 MCP 工具不互通，用户需重复配置；MCP 工具变更后模型无法立即感知，导致幻觉或错误调用。  
   - 企业用户的 MCP 策略（如 GitHub 内置 MCP）导致页面假死，缺乏加载超时或手动跳过机制。

3. **跨平台稳定性**：  
   - WSL2 (ARM64) 的 `/copy` 失效、Windows 下 `--resume` 挂起、Ctrl+C 中断回归——这些平台特定问题严重影响日常使用。  
   - Alpine musl 用户下载错误包导致完全无法启动的问题虽已关闭，但社区担心类似自动更新逻辑仍有隐患。

4. **插件和 agent 配置灵活性不足**：  
   - 子代理解析相对路径时以 CWD 为基准而非代理文件所在目录，导致引用文档失败。  
   - 插件 MCP 服务器的工作目录被设置为插件安装根目录，无法访问项目文件。

5. **交互体验细节**：  
   - 用户希望等待输入时有明确提示（#2650）；hook 返回“ask”时显示 JSON 而非 diff 视图（#4135）；Ctrl+G 编辑功能在 ask_user 模式中损坏（#4230）。  
   - 这些虽非致命，但暴露了 CLI 在复杂交互路径中的测试盲区。

---

**总结**：v1.0.74 的发布为插件和 MCP 标准化迈出重要一步，但社区更期待解决会话超限、MCP 继承和平台兼容性等核心痛点。建议开发者密切关注 #4097 和 #4143 的进展，这两个 issue 可能影响未来 2-3 个版本的路线图。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 ｜ 2026-07-24

## 今日速览
今日社区活跃度集中在 Bug 修复与性能优化上，贡献者 `lihailong00` 一口气提交了 10+ 个涉及 MCP 会话管理、Shell 补全、Windows 兼容性等关键模块的 PR。功能讨论方面，多会话远程控制（#1282）和 A 股量化 Agent 实践（#2555）成为社区关注热点，后者由用户主动分享金融领域对 Kimi Agent 框架的落地思考。

## 版本发布
过去 24 小时内无新版本发布。

## 社区热点 Issues（共 6 条，全部收录）

1. **[#1282] Feature Request: Remote Control - Continue local sessions from any device**  
   - 作者: CatKang | 更新: 2026-07-23 | 👍: 16 | 评论: 6  
   - **摘要**：建议增加远程控制功能，允许用户从手机、平板或浏览器继续本地 Kimi CLI 会话，实现工作流无缝切换。  
   - **观察**：16 个 👍 表明该功能需求强烈，属于“高呼声”特性，可能影响未来产品路线。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/issues/1282)

2. **[#2555] 讨论：A股量化+AI Agent 实践 —— 从 Kimi 的 Agent 思路学到什么**  
   - 作者: yupeng012 | 创建: 2026-07-24 | 更新: 2026-07-24 | 评论: 0  
   - **摘要**：分享使用 Hermes Agent 框架做金融交易 Agent 的实践经验，强调必须以真实 PnL 作为学习反馈闭环，并采用贝叶斯优化自动搜索参数。  
   - **观察**：虽然刚发布，但内容深度高，可能引发对 Agent 落地金融场景的讨论。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/issues/2555)

3. **[#2553] /plugins crashes with TypeError when 2+ plugins are installed (v0.29.0, Windows)**  
   - 作者: tovipy-png | 更新: 2026-07-23 | 评论: 0 | 👍: 0  
   - **摘要**：在 Windows 上安装 2 个及以上插件后，`/plugins` 管理界面因 `TypeError: Cannot read properties of undefined (reading 'value')` 崩溃。  
   - **观察**：严重影响插件用户，属于高优先级 Bug，需要尽快修复。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/issues/2553)

4. **[#2552] [Kimi Desktop] Poor font kerning for Cyrillic text in chat markdown**  
   - 作者: Serg2000Mr | 更新: 2026-07-23 | 评论: 0 | 👍: 0  
   - **摘要**：Windows 版 Kimi Desktop 聊天面板中，西里尔字母在 Markdown 块内字间距异常，影响俄语用户可读性。  
   - **观察**：国际化体验问题，影响非英语用户群体。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/issues/2552)

5. **[#2545] Synchronize queued prompts to backend to improve phone user experience with Kimi Web**  
   - 作者: vilicvane | 更新: 2026-07-23 | 评论: 0 | 👍: 0  
   - **摘要**：浏览器切到后台后，排队中的提示不会被发送，建议同步到后端以改善手机用户频繁切屏的体验。  
   - **观察**：移动端体验优化点，与 #1282 的远程控制有部分重叠诉求。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/issues/2545)

6. **[#2538] kimi-datasource plugin worker pool blocks all sessions on timeout**  
   - 作者: cloxichjc | 更新: 2026-07-23 | 评论: 0 | 👍: 0  
   - **摘要**：`kimi-datasource` 插件的 worker 池在某个会话超时后阻塞所有其他会话，导致多会话卡死。  
   - **观察**：插件体系的多会话隔离问题，影响并发使用体验。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/issues/2538)

## 重要 PR 进展（精选 10 条）

1. **[#2548] fix(mcp): reuse initialized client sessions**  
   - 作者: lihailong00 | 更新: 2026-07-23  
   - **摘要**：保持每个 MCP 客户端会话在工具集生命周期内复用，避免每次工具调用都重复初始化，提升性能。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/pull/2548)

2. **[#2551] fix(shell): search past file completion limit**  
   - 作者: lihailong00 | 更新: 2026-07-23  
   - **摘要**：修复非 Git 目录下 `@` 文件补全仅搜索前 1000 条的问题，优化扫描预算（上限 10000 条），提升大型目录补全准确性。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/pull/2551)

3. **[#2550] fix(kosong): propagate message serialization options**  
   - 作者: lihailong00 | 更新: 2026-07-23  
   - **摘要**：透传 Pydantic 序列化选项，确保调用 `model_dump(exclude_none=True)` 时不会遗漏 `null` 字段，修复媒体消息兼容性问题。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/pull/2550)

4. **[#2547] fix(windows): configure stdio as utf-8**  
   - 作者: lihailong00 | 更新: 2026-07-23  
   - **摘要**：在 Windows 上启动时配置 stdout/stderr 为 UTF-8 编码，解决 cp936 终端下中文/特殊字符乱码。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/pull/2547)

5. **[#2546] fix(print): escape markup in echoed stdin prompts**  
   - 作者: lihailong00 | 更新: 2026-07-23  
   - **摘要**：修复标准输入提示中包含 `[/login]` 等 Rich 标记语法时被错误解析的问题，确保原样传递。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/pull/2546)

6. **[#2543] fix(hooks): notify on permission prompts**  
   - 作者: lihailong00 | 更新: 2026-07-23  
   - **摘要**：在需要手动审批权限提示时，发出对应的 `Notification` 钩子，避免遗漏通知。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/pull/2543)

7. **[#2541] fix(mcp): continue after deferred startup failure**  
   - 作者: lihailong00 | 更新: 2026-07-23  
   - **摘要**：防止后台 MCP 启动失败中止交互轮次，仅捕获 `MCPRuntimeError`，保持其他异常可见。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/pull/2541)

8. **[#2542] fix(logging): isolate Windows process log files**  
   - 作者: lihailong00 | 更新: 2026-07-23  
   - **摘要**：Windows 下日志文件使用 `kimi.<pid>.log` 格式，避免多进程共享同一日志文件导致轮转冲突。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/pull/2542)

9. **[#2540] fix(media): normalize ICO images to PNG**  
   - 作者: lihailong00 | 更新: 2026-07-23  
   - **摘要**：将 ICO 图像转为 PNG 后再发送给模型，保持元数据完整，修复图标文件兼容性。  
   - [链接](https://github.com/MoonshotAI/kimi-cli/pull/2540)

10. **[#2537] fix(shell): support numeric keypad input**  
    - 作者: lihailong00 | 更新: 2026-07-23  
    - **摘要**：识别 Windows Terminal 发送的 DEC 应用小键盘序列，使数字小键盘输入（0-9）在提示符中生效。  
    - [链接](https://github.com/MoonshotAI/kimi-cli/pull/2537)

## 功能需求趋势
- **远程/跨设备连续性**：Issue #1282 的远程控制功能获 16 个 👍，叠加 #2545 的队列同步建议，表明移动端和跨设备工作流是社区最关注的方向。  
- **插件系统稳定性**：#2553（多插件崩溃）和 #2538（worker 池阻塞）反映出插件承载越来越多第三方能力后，资源隔离与错误处理成为痛点。  
- **国际化和编码兼容**：#2552（西里尔文字间距）、#2547（Windows UTF-8）说明非英语用户和 Windows 平台的体验改进需求持续存在。  
- **Agent 落地实践**：#2555 的量化交易讨论虽刚出现，但侧面证明开发者对 Kimi Agent 框架在非编程领域的二次开发感兴趣。

## 开发者关注点
- **Windows 环境 Bug 集中**：昨日 PR 中有半数与 Windows 相关（UTF-8、进程日志、数字小键盘、进程组隔离），说明 Windows 用户基数增长带来适配挑战。  
- **MCP 会话管理**：PR #2548（复用会话）、#2541（后台启动失败不阻断）显示 MCP 协议集成正被重点打磨，以提升工具调用的稳定性和性能。  
- **文件补全性能**：PR #2551 和 #2549 分别优化 `@` 补全的扫描范围与 vendor 目录索引，反映出开发者对大项目文件操作效率的重视。  
- **安全与权限通知**：PR #2543 修复权限提示通知遗漏，表明自动审批流程的透明性受到关注，需要明确钩子机制。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-07-24

---

## 📰 今日速览

今日社区活跃度高涨，共产生 50 条 Issue 和 50 条 PR 更新。**模型自动发现功能（#6231）以 187 个赞持续位列最受期待需求**，而 V2 版本的多项性能与稳定性修复（#36285、#38590）正在密集合并。此外，**计费争议（#35475、#38255）和子进程残留风险（#38564）** 成为开发者最关心的两类 Bug。

---

## 🚀 版本发布

过去 24 小时内无新版本发布。当前稳定版为 **Desktop v1.18.4**，CLI 版本 1.18.4。

---

## 🔥 社区热点 Issues（精选 10 条）

### 1. 自动发现 OpenAI 兼容提供商模型  
**#6231** - `[OPEN] Auto-discover models from OpenAI-compatible provider endpoints`  
👍 187 | 💬 30 | 创建: 2025-12-27 | 更新: 2026-07-23  
👉 https://github.com/anomalyco/opencode/issues/6231  
**为什么重要**：用户需手动配置 LM Studio、Ollama 等本地提供商的模型列表，模型频繁变更时极其繁琐。这是社区最强烈的功能需求，有望大幅降低配置成本。

### 2. 保留旧版布局选项  
**#37012** - `[OPEN] [FEATURE]: keep legacy layout option`  
👍 30 | 💬 29 | 创建: 2026-07-15 | 更新: 2026-07-23  
👉 https://github.com/anomalyco/opencode/issues/37012  
**为什么重要**：新版 UI 将许多操作深埋导航中，旧版布局的“一站式”体验更受欢迎。该 Issue 体现了用户对 UI 自定义的强烈诉求。

### 3. 内容过滤器误报且仍收费  
**#35475** - `[OPEN] False positive content-filter on claude-fable-5 — charged ~$20 for blocked output`  
👍 0 | 💬 10 | 创建: 2026-07-05 | 更新: 2026-07-23  
👉 https://github.com/anomalyco/opencode/issues/35475  
**为什么重要**：良性查询被拦截，用户仍需支付完整缓存写入费用（约 $6.69/次），累计损失 $20。计费逻辑引发公正性质疑，与 #35643 形成关联。

### 4. V2 服务重启引发重连风暴  
**#36285** - `[CLOSED] [bug, perf, 2.0] 2.0: managed-service restart causes reconnect herd and resource spikes`  
👍 0 | 💬 5 | 创建: 2026-07-10 | 更新: 2026-07-24  
👉 https://github.com/anomalyco/opencode/issues/36285  
**为什么重要**：自动更新后管理服务被替换，所有 TUI 断开连接并批量冷启动位置图，导致资源峰值和新 TUI 缓慢。该问题已关闭，相关修复 PR 正在验证。

### 5. 使用量仪表盘数据不一致  
**#38255** - `[OPEN] Discrepancy between different opencode go usage dashboard`  
👍 0 | 💬 5 | 创建: 2026-07-22 | 更新: 2026-07-24  
👉 https://github.com/anomalyco/opencode/issues/38255  
**为什么重要**：月度限额显示 100% 用量，但明细仪表盘仅显示 $10 消费。用户因误判被服务拒绝，严重影响计费透明度。

### 6. 子代理终止后子进程未杀死（磁盘 I/O 滥用风险）  
**#38564** - `[OPEN] Subagent termination does not kill spawned child processes (disk abuse risk)`  
👍 0 | 💬 2 | 创建: 2026-07-23 | 更新: 2026-07-23  
👉 https://github.com/anomalyco/opencode/issues/38564  
**为什么重要**：取消子代理后，PowerShell 子进程仍在后台以 100% I/O 持续运行，只能强制终止 opencode。存在资源泄露隐患。

### 7. Windows 上 @ 符号无法引用文件  
**#29859** - `[CLOSED] @ symbol completely fails to reference files in any directory on Windows (v1.15.12)`  
👍 0 | 💬 4 | 创建: 2026-05-29 | 更新: 2026-07-24  
👉 https://github.com/anomalyco/opencode/issues/29859  
**为什么重要**：Windows 用户无法使用最基础的上下文引用功能，影响面广。虽已关闭，但根本原因仍需关注。

### 8. 桌面端渲染器崩溃（1.18.4）  
**#38577** - `[CLOSED] Desktop 1.18.4 renderer crash: TypeError on data.lsp (data shape mismatch)`  
👍 0 | 💬 2 | 创建: 2026-07-23 | 更新: 2026-07-24  
👉 https://github.com/anomalyco/opencode/issues/38577  
**为什么重要**：最新版桌面应用启动即崩溃，影响 macOS M 系列用户。快速关闭说明修复已上线。

### 9. 数学公式无法渲染  
**#37326** - `[OPEN] math equations not rendered`  
👍 1 | 💬 7 | 创建: 2026-07-16 | 更新: 2026-07-24  
👉 https://github.com/anomalyco/opencode/issues/37326  
**为什么重要**：模型输出的 LaTeX / 数学公式在 UI 中显示为纯文本，影响学术和科学场景使用。

### 10. Always Allow 权限选择不生效  
**#37880** - `[OPEN] [Desktop] 'Always Allow' permission selection not respected - acts like 'Allow Once' and resets immediately`  
👍 1 | 💬 2 | 创建: 2026-07-20 | 更新: 2026-07-23  
👉 https://github.com/anomalyco/opencode/issues/37880  
**为什么重要**：用户选择“始终允许”后权限立即重置，逐次确认非常干扰工作流。UI 行为违背用户预期。

---

## 🛠️ 重要 PR 进展（精选 10 条）

### 1. 为自定义提供商添加推理与 Token 限制配置  
**#38594** - `[OPEN] [needs:compliance] feat(app): add reasoning and token limits to custom providers`  
作者: cppcoffee | 更新: 2026-07-24  
👉 https://github.com/anomalyco/opencode/pull/38594  
**内容**：支持在自定义提供商中配置“启用推理”、“上下文长度”等参数，解决 #38593 中的配置缺失问题。

### 2. 修复会话变更面板永远为空  
**#38592** - `[OPEN] [needs:issue, needs:compliance] fix: session changes panel always empty — restore session-level diff computation`  
作者: oguzeray | 更新: 2026-07-24  
👉 https://github.com/anomalyco/opencode/pull/38592  
**内容**：TUI 右侧“Session Changes”面板和 Desktop 审查面板始终显示“无更改”，即使代理已编辑大量文件。此 PR 重新实现了 diff 计算，影响所有平台。

### 3. 转发父级附件给子代理  
**#32302** - `[OPEN] [contributor] fix(opencode): forward parent attachments to subagents`  
作者: 21pounder | 更新: 2026-07-24  
👉 https://github.com/anomalyco/opencode/pull/32302  
**内容**：修复 `@mention` 子代理时无法继承父会话附件的问题，提升多代理协作场景的能力。

### 4. 稳定工具定义排序提高缓存命中率  
**#38590** - `[CLOSED] [contributor] fix(core): stabilize tool definition ordering`  
作者: kitlangton | 更新: 2026-07-24  
👉 https://github.com/anomalyco/opencode/pull/38590  
**内容**：按规范名称排序工具定义，确保相同注册集合产生字节一致的数组，从而稳定提供商的 prompt 缓存前缀，减少请求成本。

### 5. 保留 Grep 符号链接路径  
**#38581** - `[OPEN] fix(opencode): preserve grep symlink paths`  
作者: remixz | 更新: 2026-07-24  
👉 https://github.com/anomalyco/opencode/pull/38581  
**内容**：修复 `grep` 工具将符号链接路径规范化后，后续工具调用因路径不匹配而失败的问题。

### 6. CodeMode 目录增量渲染  
**#38183** - `[OPEN] feat(core): render CodeMode catalog deltas from structured snapshots`  
作者: rekram1-node | 更新: 2026-07-24  
👉 https://github.com/anomalyco/opencode/pull/38183  
**内容**：将 Code Mode 目录的模型提示信息从全量替换升级为技能风格的语义增量，开发者仅需关注变更部分。

### 7. 改进 Patch 错误提示  
**#38369** - `[CLOSED] fix(core): improve patch errors`  
作者: rekram1-node | 更新: 2026-07-23  
👉 https://github.com/anomalyco/opencode/pull/38369  
**内容**：识别格式错误的 add/delete/move hunk，移除冗余前缀，并包含稳定的文件系统原因，帮助开发者快速定位错误。

### 8. 转发插件元数据到 MCP 工具调用  
**#38579** - `[OPEN] feat(mcp): forward plugin request metadata`  
作者: dialupdisaster | 更新: 2026-07-23  
👉 https://github.com/anomalyco/opencode/pull/38579  
**内容**：允许插件设置可选的 `_meta` 字段，并将其与 session ID 等一并传递给 MCP 服务器，增强 MCP 生态可观测性。

### 9. 保留原始 finish 原因  
**#38423** - `[CLOSED] feat(ai): preserve raw finish reasons`  
作者: rekram1-node | 更新: 2026-07-23  
👉 https://github.com/anomalyco/opencode/pull/38423  
**内容**：将模型终结原因（如 `stop`、`length`）拆为标准化+原始两个字段，支持 OpenAI、Anthropic、Gemini 等主流提供商，便于用户诊断输出截断等问题。

### 10. 阶段文件编辑避免重复写入  
**#38198** - `[OPEN] fix(acp): stage file edits for native review instead of writing twice`  
作者: anthony-furman | 更新: 2026-07-23  
👉 https://github.com/anomalyco/opencode/pull/38198  
**内容**：修改 ACP 协议，先暂存文件编辑再原生审查，而不是直接写入两次，提升文件操作性能并减少磁盘写入。

---

## 📈 功能需求趋势

从近期 Issue 和 PR 中可以提炼出以下社区关注方向：

- **模型自动发现与统一配置**：减少手动列模型，支持对 OpenAI 兼容本地提供商的自发现（#6231），同时要求自定义提供商支持推理和 Token 限制（#38594）。
- **UI 灵活性与可定制性**：旧版布局保留（#37012）、子代理输出独立视图（#37267）、移动端远程控制（#33163）等，反映用户对界面自主权的高期望。
- **多平台兼容性**：Windows 路径/符号引用问题（#29859）、FreeBSD 平台支持（#38591）、Intel macOS 兼容等，社区覆盖范围不断扩大。
- **MCP 生态扩展**：转发 session ID 和 plugin meta 到 MCP 工具（#38579、#21624），推动第三方工具集成能力。
- **Agent 内省与调试**：子代理推理级别显示（#26266）、CodeMode 目录增量渲染（#38183），帮助开发者理解 Agent 内部决策。

---

## 👨‍💻 开发者关注点

结合

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# 🥧 Pi 社区动态日报 | 2026-07-24

---

## 📋 今日速览

社区在 **模型配置 & 扩展生态** 两个方向修复了多个关键 bug（如 llama.cpp 输出上限硬编码、`models.json` 热重载回归、`wl-copy` 误报成功等），并合入了多项新功能（受限采样、bash 执行事件、TUI 局部重绘等）。此外，关于 **Anthropic 的 Fable→Opus 降级**、**SiiconFlow 内置 Provider** 等需求仍有持续讨论。

---

## 📦 版本发布

**无**（过去 24 小时内未发布新的 Release）

---

## 🔥 社区热点 Issues（Top 10）

### 1. [OPEN] Qwen 推理强度 (reasoning effort) 映射错误  
**#6951** — Qwen3.8-max-preview 的 API 要求 `low/medium/xhigh`，而 Pi 内部使用了 `minimal/low/medium/high`，导致调用时参数无效。已有 1 个 👍，开发者已确认并开始处理。  
🔗 [GitHub Issue](https://github.com/earendil-works/pi/issues/6951)

### 2. [OPEN] `models.json` 热重载在 0.80.8+ 后失效  
**#6999** — 用户希望能在不重启会话的情况下通过 `/model` 重新加载 `models.json` 中的自定义 Provider。新版本移除了该能力，社区呼声较高（3 条评论）。  
🔗 [GitHub Issue](https://github.com/earendil-works/pi/issues/6999)

### 3. [OPEN] llama.cpp 默认模型在启动时未自动应用  
**#6948** — 即使 `settings.json` 中配置了 `defaultProvider: "llama.cpp"` 和 `defaultModel`，启动后仍使用空模型，触发了异步竞争条件。影响新用户入门体验。  
🔗 [GitHub Issue](https://github.com/earendil-works/pi/issues/6948)

### 4. [OPEN] `/copy` 命令在 `wl-copy` 失败时误报成功  
**#6872** — 在 bwrap 沙箱或无 Wayland 环境的用户中，`wl-copy` 执行失败但 exit code 未被 await，导致误报并跳过 fallback（xclip）。已有 3 条评论，发现者提供了复现步骤。  
🔗 [GitHub Issue](https://github.com/earendil-works/pi/issues/6872)

### 5. [OPEN] GitHub Copilot Provider 因使用 Plugin 而非 OAuth 导致 Token 失效  
**#6970** — 当用户在多设备同时使用 `github-copilot` 时，Pi 使用的 `GitHub Copilot Plugin` 认证方式会被服务器认为是滥用，从而快速过期。社区建议改用 OAuth 流程。  
🔗 [GitHub Issue](https://github.com/earendil-works/pi/issues/6970)

### 6. [OPEN] Extension 注册 `resource_discover` 后导致所有 skill/prompt scope 坍缩  
**#6968** — 安装一个注册了 `resource_discover` 的扩展后，所有已安装包的 source 元数据丢失，自动补全标签从 `[npm]` 等变成 `[t]`。严重影响扩展开发者。  
🔗 [GitHub Issue](https://github.com/earendil-works/pi/issues/6968)

### 7. [OPEN] DeepSeek 通过阿里云（通义 Token 计划）使用时需设置 `thinkingFormat: "qwen"`  
**#6998** — 社区查明阿里云提供的 DeepSeek 模型应该使用通义系的 thinking 格式，但当前 generate-models 覆盖了 `compat` 和 `thinkingLevelMap`，导致配置冲突。  
🔗 [GitHub Issue](https://github.com/earendil-works/pi/issues/6998)

### 8. [CLOSED] CJK/宽字符导致光标上下移动列位置错误  
**#7021** — `Up/Down` 光标移动时按 UTF-16 code units 计算列宽，而 CJK 字符占 2 个显示列，导致视觉错位。该问题已通过 PR 修复并关闭。  
🔗 [GitHub Issue](https://github.com/earendil-works/pi/issues/7021)

### 9. [CLOSED] 安装损坏的 `package.json` 导致会话启动循环崩溃  
**#7033** — 若某个包的 `pi` 字段中 `skills` 是字符串而非数组，会导致 `entries.filter is not a function`，且因坏包持久化在 settings 中，每次启动均立即崩溃。已快速修复。  
🔗 [GitHub Issue](https://github.com/earendil-works/pi/issues/7033)

### 10. [NEW] 新增 per-provider 范围的模型刷新 API  
**#7040** — 由 lethe-code 提交的需求：当前 `Models.refresh()` 强制刷新所有动态 Provider，但某些场景只需刷新一个 Provider（例如 model-miss 后）。希望提供按 Provider ID 刷新的接口。  
🔗 [GitHub Issue](https://github.com/earendil-works/pi/issues/7040)

---

## 🔧 重要 PR 进展（Top 10）

### 1. [OPEN] 修复 `/model` 选择器中的模型配置热重载  
**#7036** — 由 mitsuhiko 提交，直接回应 #6999。在打开 `/model` 时重新加载 `models.json`，但作者指出更好的方案是让 `reloadConfig` 直接返回 `refresh` 的结果，避免双重刷新。  
🔗 [GitHub PR](https://github.com/earendil-works/pi/pull/7036)

### 2. [CLOSED] 移除 llama.cpp 最大输出 token 硬编码（16,384）  
**#7034** — 改为从每个模型的实际 context window 动态推导输出限制，修复 #6994。通过了测试和 check。  
🔗 [GitHub PR](https://github.com/earendil-works/pi/pull/7034)

### 3. [CLOSED] TUI 编辑区域实验性局部重绘支持  
**#7017** — 加入 `repaint` 设置，避免长会话时每次重绘整个 transcript，显著提升大会话下的终端性能。虽为实验性功能，但社区反馈积极。  
🔗 [GitHub PR](https://github.com/earendil-works/pi/pull/7017)

### 4. [OPEN] 暴露不可用的 scoped 模型并提供移除入口  
**#7032** — 当之前配置的模型模式（pattern）不再匹配任何可用模型时，现在会在 `/scoped-models` 中显示为 `no-match` 类型条目，并允许用户删除。增强模型管理透明性。  
🔗 [GitHub PR](https://github.com/earendil-works/pi/pull/7032)

### 5. [CLOSED] 修复 `/resume` 嵌套自引用导致选择器坍缩  
**#7028** — 在已通过 `/resume` 打开的会话中再次使用 `/resume`，选择器只显示当前会话自身，违背直观。修复后恢复到完整列表。  
🔗 [GitHub PR](https://github.com/earendil-works/pi/pull/7028)

### 6. [CLOSED] 为 `AssistantMessage` 添加 `hiddenThinkingLabel` 字段  
**#7018** — 允许每条思考块单独展示标签（如“思考了 3 秒”），替代全局标签。扩展可以设置 per-message 的思考标签，提升用户对模型状态的感知。  
🔗 [GitHub PR](https://github.com/earendil-works/pi/pull/7018)

### 7. [CLOSED] 发出 `bash_execution_update` 事件（供编辑器/客户端使用）  
**#6971** — 新增事件，携带执行 ID，支持并行 shell 执行跟踪。此 PR 修复了 #6703，并已被 pimacs 等编辑器客户端采用。  
🔗 [GitHub PR](https://github.com/earendil-works/pi/pull/6971)

### 8. [CLOSED] 使 Provider 重试可被 abort 取消  
**#6980** — 替换 Anthropic/OpenAI SDK 内部重试逻辑为统一 helper，支持 `abortSignal` 中断，并强制 `maxRetryDelayMS`。避免用户等待不可取消的重试。  
🔗 [GitHub PR](https://github.com/earendil-works/pi/pull/6980)

### 9. [CLOSED] 修复 `wl-copy` 退出码检查与 fallback 逻辑  
**#7009** — 现在会正确 await `wl-copy` 的 exit code，若失败则 fallback 到 xclip 和 OSC 52。直接修复了 #6872 及同类问题。  
🔗 [GitHub PR](https://github.com/earendil-works/pi/pull/7009)

### 10. [OPEN] 共享宿主模块给原生 ESM 扩展  
**#7011** — 解决 Jiti 在原生 import 时绕过别名和虚拟模块的问题，防止扩展与宿主加载不同版本的 Pi 包。扩展开发者关注的重要兼容性修复。  
🔗 [GitHub PR](https://github.com/earendil-works/pi/pull/7011)

---

## 📈 功能需求趋势

从过去 24 小时的讨论中，社区关注度较高的功能方向包括：

- **模型 / Provider 支持**  
  - 新增 SiliconFlow 内置 Provider (#7013)  
  - 修复 Aliyun / DeepSeek 兼容 (#6998)  
  - 支持 Anthropic 服务端 Fable→Opus 降级 (#6886

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 (2026-07-24)

## 📰 今日速览
昨夜发布的 `v0.20.1-nightly` 版本主要修复了遥测初始化顺序并优化了性能；社区核心讨论集中在 **外部记忆集成** 和 **MCP 服务器兼容性** 问题上，两项新提案（企业级外部内存集成、直接外部上下文提供者）引起广泛关注；此外，🎯 微信频道和 Telegram 主题回复的 Bug 已快速修复，CI 稳定性也成为近期开发者热议话题。

---

## 🚀 版本发布
### v0.20.1-nightly.20260724.7d17c44a3
- **What's Changed**
  - `test(telemetry):` 增加守护进程指标初始化顺序测试，并修复 metricReader 不对称问题
  - `perf:` 性能优化（具体细节未在 release note 中展开）
- 发布链接：[GitHub Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.20.1-nightly.20260724.7d17c44a3)

---

## 🔥 社区热点 Issues（Top 10）

1. **#7449 [OPEN] proposal(memory): 定义企业级外部内存集成方案**  
   - 由 @doudouOUC 提出，文档优先、兼容性测试渐进，不影响 Core API。5条评论，P3 但社区反馈积极。  
   - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/7449)

2. **#7485 [OPEN] TUI: 恢复会话后最后一条消息与输入框之间出现大片空白**  
   - Bug 导致界面错乱，影响日常使用。P2，已获 4 条评论，社区希望尽快修复。  
   - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/7485)

3. **#7147 [CLOSED] MCP 服务器始终无法获取工具和资源列表**  
   - 用户尝试 Fastmail MCP 时认证成功但工具获取超时。6 条评论，已关闭但问题典型。  
   - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/7147)

4. **#7264 [OPEN] 冷启动后续：ACP 子进程仍存在大量懒加载候选**  
   - 针对 #4748 的跟进，esbuild 审计发现冷启动时仍要加载 2420 个模块。P2，4 条评论，性能敏感用户关注。  
   - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/7264)

5. **#7599 [CLOSED] bug(artifacts): record_artifact 创建的工件缺少 managedId**  
   - 工作区生成的 HTML 等文件无法正确上报 managedId，影响 SSE 事件流。5 条评论，已关闭但值得注意。  
   - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/7599)

6. **#7585 [OPEN] proposal: 添加直接外部上下文提供者**  
   - 允许一个 Qwen CLI 进程从外部知识服务获取上下文，不改变 Core。4 条评论，与 #7449 相辅相成。  
   - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/7585)

7. **#7590 [CLOSED] 微信频道无法使用**  
   - 配置微信频道后发送消息导致 `session/cancel` 内部错误。中文用户反馈，已关闭（推测快速修复）。  
   - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/7590)

8. **#7568 [OPEN] 安装扩展失败**  
   - 安装 dotnet 扩展时版本冲突，错误提示不明确。P2，2 条评论，影响扩展生态。  
   - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/7568)

9. **#7543 [CLOSED] getNpmCliPath 返回 mise bash wrapper 而非 npm-cli.js，导致更新检查失败**  
   - 多用户反馈 v0.20.1 后 `qwen update` 总是报 registry 错误，经排查为路径解析 bug。3 条评论。  
   - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/7543)

10. **#7575 [OPEN] bug(serve): 通道/ACP 模式下不加载用户级 skills**  
    - 运行 `qwen serve --channel` 时 `~/.qwen/skills/` 不被加载，仅加载项目级和内置 skills。P2，2 条评论。  
    - [查看 Issue](https://github.com/QwenLM/qwen-code/issues/7575)

---

## 🛠️ 重要 PR 进展（Top 10）

1. **#7268 [OPEN] feat(serve): 热加载工作区信任变更**  
   - 无需重启守护进程即可应用信任策略变更，引入语义快照与监控。由 @doudouOUC 贡献，已获多项跟进。  
   - [查看 PR](https://github.com/QwenLM/qwen-code/pull/7268)

2. **#7497 [OPEN] feat(cli): 支持 /learn 原生视频输入**  
   - 允许直接上传 MP4/WebM 等本地视频文件或 HTTP 视频链接，自动检查模型模态兼容性。  
   - [查看 PR](https://github.com/QwenLM/qwen-code/pull/7497)

3. **#7632 [OPEN] feat(channels): GitHub 轮询适配器（通知即唤醒架构）**  
   - 基于 @mentions 的 GitHub Issue/PR 回复渠道，采用不同于 #7266 的异步唤醒模式。  
   - [查看 PR](https://github.com/QwenLM/qwen-code/pull/7632)

4. **#7607 [OPEN] feat(core): 可配置的图像生成模型**  
   - 允许用户选择专用图像生成模型（通过 `/model --image`），提供内置审批工具。  
   - [查看 PR](https://github.com/QwenLM/qwen-code/pull/7607)

5. **#7589 [OPEN] fix(cli): 多工具紧凑摘要中显示工具描述**  
   - 之前同类工具合并后只显示数量（如“Read 2 files”），现在显示具体路径/模式。  
   - [查看 PR](https://github.com/QwenLM/qwen-code/pull/7589)

6. **#7594 [OPEN] perf(cli): 向 ACP 子进程传播编译缓存**  
   - 通过环境变量传递 Node 模块编译缓存，减少冷启动编译开销。  
   - [查看 PR](https://github.com/QwenLM/qwen-code/pull/7594)

7. **#7302 [OPEN] feat(cli): 通过 @ 引用历史会话并增加补全标签**  
   - 在交互式 `@` 补全中加入先前会话，插入 `@session:<id>` 并生成只读摘要。  
   - [查看 PR](https://github.com/QwenLM/qwen-code/pull/7302)

8. **#7471 [OPEN] feat(web-shell): 新建会话时增加 Git 模式选择**  
   - 在 Web Shell 的会话创建流程中嵌入分支/新分支/fork 三种 Git 工作流选择。  
   - [查看 PR](https://github.com/QwenLM/qwen-code/pull/7471)

9. **#7603 [OPEN] fix(sdk-java): 加固守护进程传输可靠性**  
   - 适配重启安全的事件光标契约，修复 `X-Qwen-Event-Epoch` 头传递。  
   - [查看 PR](https://github.com/QwenLM/qwen-code/pull/7603)

10. **#7542 [OPEN] feat(cli): 添加版本升级提示**  
    - 启动时展示“What's New”通知，按版本记录已读状态，不影响现有提示系统。  
    - [查看 PR](https://github.com/QwenLM/qwen-code/pull/7542)

---

## 📈 功能需求趋势
- **外部记忆与上下文集成**（#7449、#7585）：社区连续提出两项关于外部内存/知识服务的提案，期望在不改动 Core API 的前提下实现企业级记忆共享与上下文注入。
- **通道适配器扩展**（#7632、#7590、#7609）：微信、Telegram 主题回复等渠道 Bug 与新适配器（GitHub 通知）齐发，说明多平台接入是持续热点。
- **视频/多模态输入**（#7497、#7607）：/learn 支持原生视频、可配置图像生成模型，表明开发者希望 Qwen Code 更好利用多模态能力。
- **CI 与测试优化**（#7616、#7605）：E2E 测试频繁因非确定性模型表现失败，社区开始反思测试策略，提出 “真的需要这么多 E2E 测试吗？”。
- **TUI/UI 交互改进**（#7485、#6806、#7138）：空白区域、状态栏刷新、取消输入恢复等细微体验问题被频繁提出，说明用户对交互体验要求提高。

---

## 🔧 开发者关注点
- **更新检查失败**（#7543、#7520、#7515）：多个用户报告 v0.20.1 后 `qwen update` 或 `/update` 报 “registry error”，根源是 npm 12 兼容性及路径解析问题，已有多项修复 PR 在途。
- **工作区与扩展管理**（#7575、#7568）：通道模式下用户级 skills 不加载、扩展安装时版本冲突提示不友好，影响自定义扩展生态。
- **会话恢复与状态同步**（#7485、#6806、#7287）：TUI 空白区、状态栏压缩后不刷新、auto-memory 未注册 FileReadCache 导致写文件被拒，反映内部 cache 与 UI 同步仍有死角。
- **MCP 兼容性**（#7147、#7195）：非标准 MCP 服务器（如 Fastmail）集成时超时 / 认证后无响应，社区期待更健壮的传输层支持。
- **CI 可靠性**（#7516、#7559、#7605、#7616）：E2E 测试频繁因模型输入非确定性、Docker 沙箱慢等原因误报失败，开发者呼吁减少此类测试或增加超时/重试机制。

---

*数据来源：GitHub QwenLM/qwen-code，采集时间 2026-07-24。*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，我将根据您提供的 GitHub 数据，为您生成 2026-07-24 的 DeepSeek TUI（现更名为 CodeWhale）社区动态日报。

***

# DeepSeek TUI (CodeWhale) 社区动态日报 | 2026-07-24

## 今日速览

今日社区动态集中在 **v0.9.1 版本的发布前安全审查**和**大量可靠性 Bug 的集中提交与修复**。核心关注点是**子代理（Sub-agent）的沙箱安全性**、**数据并发写入损坏**以及 **TUI 启动崩溃**等影响用户体验的关键问题。此外，**MCP 服务器功能失效**和**配置静默失败**等深层问题也被揭露，构成了 v0.9.1 发布前的最后一道防线。

## 社区热点 Issues

以下挑选了今日更新中最值得关注的 10 个 Issues：

1.  **[#4042] feat: Environment-level tool sandboxing for sub-agents** (已关闭)
    *   **重要性**: 这是 v0.9.0 中一个关键的安全增强功能，确保子代理不能调用父会话未授权的工具。该 issue 跟踪了 CodeWhale（原 DeepSeek TUI）不同执行上下文（会话、子代理、Fleet 工作节点、MCP 服务器）中工具限制的运行时强制执行情况。核心价值在于将权限控制下沉到环境级别，提升多代理场景下的系统安全。
    *   **社区反应**: 讨论热烈，共 19 条评论，深入探讨了实现细节和边界情况。
    *   **链接**: [Issue #4042](https://github.com/Hmbown/CodeWhale/issues/4042)

2.  **[#4713] v0.9.1 security gate: deep scan and dependency alert disposition** (开放中)
    *   **重要性**: **发布前的最后一道安全关卡**。该 issue 要求在进行 v0.9.1 版本标记和发布前，完成全仓安全审查，并明确处理 17 个 GitHub 依赖警报（7 个高危，10 个中危）。这直接关系到新版本的发布进程和用户系统的安全。
    *   **社区反应**: 作为一个里程碑式的任务，它聚合了其他安全相关的 issue。
    *   **链接**: [Issue #4713](https://github.com/Hmbown/CodeWhale/issues/4713)

3.  **[#4716] [stop-ship] TUI exits immediately on launch** (开放中)
    *   **重要性**: **最高优先级的 Bug**。在 macOS 的纯新终端中，运行 `codew` 命令后 TUI 立即退出，用户无法使用。这是一个关键的启动崩溃问题，会完全阻止新用户入门。
    *   **社区反应**: 被标记为 “stop-ship”，意味着该问题必须在发布前解决。
    *   **链接**: [Issue #4716](https://github.com/Hmbown/CodeWhale/issues/4716)

4.  **[#4727] codewhale mcp-server never spawns configured MCP servers** (开放中)
    *   **重要性**: **核心功能失效**。`codewhale mcp-server` 子命令旨在运行用户配置的 MCP 服务器，但目前只返回伪造的模拟响应。这意味着所有依赖 MCP 服务器的第三方工具集成完全不可用，影响面巨大。
    *   **社区反应**: 虽然暂无评论，但其严重性不言而喻。
    *   **链接**: [Issue #4727](https://github.com/Hmbown/CodeWhale/issues/4727)

5.  **[#4733] malformed project config.toml is silently treated as "no project config"** (开放中)
    *   **重要性**: **隐蔽的安全与配置问题**。项目配置文件 (`config.toml`) 解析出错时，系统会静默忽略该错误并返回“无项目配置”。用户可能在一个错误或老旧配置下运行，而意识不到自己的自定义设置（如安全策略、工具限制）已全部失效。
    *   **社区反应**: 暂无评论，但此类“静默失败”是开发者的噩梦。
    *   **链接**: [Issue #4733](https://github.com/Hmbown/CodeWhale/issues/4733)

6.  **[#4741/4739] JsonlHookSink has no write synchronization** (部分已关闭)
    *   **重要性**: 这是两个高度相似的问题，指出 `JsonlHookSink` 的 `emit` 方法在**并发写入**时没有同步机制（锁），会导致 **JSONL 日志文件损坏**。对于调试和审计至关重要，日志损坏将严重影响问题追踪。
    *   **社区反应**: #4741 已被快速关闭并合并（fix），显示出维护者的高度重视。
    *   **链接**: [Issue #4741](https://github.com/Hmbown/CodeWhale/issues/4741) | [Issue #4739](https://github.com/Hmbown/CodeWhale/issues/4739)

7.  **[#4723] AltGr+Q on Brazilian ABNT2 layout opens help overlay** (开放中)
    *   **重要性**: **跨平台键盘布局兼容性**问题。对于使用巴西 ABNT2 键盘布局的 Windows 用户，输入 `/` 的快捷键 `AltGr+Q` 被错误地映射为 `Ctrl+Alt+Q`，导致触发了帮助菜单，而非输入字符。这是一个影响非英语母语者使用体验的典型问题。
    *   **社区反应**: 由社区用户 `nicolassmotta` 提交，代表了特定地区用户的痛点。
    *   **链接**: [Issue #4723](https://github.com/Hmbown/CodeWhale/issues/4723)

8.  **[#4734] SQLite connection has no busy_timeout/WAL** (开放中)
    *   **重要性**: **并发可靠性问题**。SQLite 连接未设置 `busy_timeout` 和 WAL 日志模式，多个进程并发访问数据库时会直接失败。对于需要高并发或后台任务（如 Fleet）运行的场景，这是一个严重的稳定性隐患。
    *   **社区反应**: 暂无评论，是典型的“看不见的定时炸弹”。
    *   **链接**: [Issue #4734](https://github.com/Hmbown/CodeWhale/issues/4734)

9.  **[#4719] Composer: large pasted prompts get byte-corrupted** (开放中)
    *   **重要性**: **影响核心输入体验**。在 Composer 中粘贴长提示词会被截断或字符损坏，导致模型接收到的指令是错误的。这不仅令人沮丧，还可能导致 AI 输出完全不符合预期，浪费用户时间和资源。
    *   **社区反应**: 由作者亲自提交，说明问题已经过复现，确认存在。
    *   **链接**: [Issue #4719](https://github.com/Hmbown/CodeWhale/issues/4719)

10. **[#4738] in-flight stdio thread/message turns cannot be cancelled** (开放中)
    *   **重要性**: **系统响应性问题**。Stdio JSON-RPC 循环是顺序执行的，正在处理的消息无法被中断，甚至无法通过关闭事件来取消。这会导致在调用耗时工具时，整个服务器都无响应，影响用户体验和系统优雅关闭。
    *   **社区反应**: 暂无评论，但问题描述清晰，是架构层面的优化点。
    *   **链接**: [Issue #4738](https://github.com/Hmbown/CodeWhale/issues/4738)

## 重要 PR 进展

1.  **[#4724] fix(tui): archive completed background shell output** (开放中)
    *   **内容**: 修复了 TUI 中后台 Shell 任务完成后的输出归档问题。当后台任务结束后，其最终的可见输出会被归档到原始的执行单元格 (`ExecCell`)中，并清除实时输出流，冻结显示时长。
    *   **重要性**: 提升了多任务并发的可视性，使用户能回溯已结束后台任务的输出，改善调试和工作流追踪体验。
    *   **链接**: [PR #4724](https://github.com/Hmbown/CodeWhale/pull/4724)

2.  **[#4346] fix: sanitize tool input_schema for Anthropic adapter** (已关闭)
    *   **内容**: 修复了在使用 Anthropic 作为提供商时，工具的 `input_schema` 包含顶层 `oneOf`/`anyOf`/`allOf` 时，API 会返回 400 错误的问题。通过对模式进行清理，确保兼容 Anthropic 的 API 要求。
    *   **重要性**: 解决了与 Anthropic 模型核心功能的兼容性问题，确保用户可以使用 Anthropic 支持的复杂工具参数。
    *   **链接**: [PR #4346](https://github.com/Hmbown/CodeWhale/pull/4346)

3.  **[#4722] fix(tui): show complete edit previews in details** (开放中)
    *   **内容**: 改进了 `edit_file` 工具的审批 UI。在卡片预览中保持紧凑，但通过 `Alt+V` 快捷键可以懒加载查看完整的搜索/替换差异对比，并增加了回归测试。
    *   **重要性**: 解决了代码编辑预览信息密度问题，既保证了主界面的简洁，又提供了深入审查完整变更的能力，提升了开发效率。
    *   **链接**: [PR #4722](https://github.com/Hmbown/CodeWhale/pull/4722)

4.  **[#4610] feat(tui): add configurable session token header** (开放中)
    *   **内容**: 引入了一个可配置的 `tui.header_items` 功能，允许用户在 TUI 头部添加累积的会话 Token 统计信息（包括输入、缓存命中、输出计数）。
    *   **重要性**: 满足高级用户和开发者跟踪 API 消耗的强需求，提供更高的透明度和成本控制能力。
    *   **链接**: [PR #4610](https://github.com/Hmbown/CodeWhale/pull/4610)

## 功能需求趋势

*   **安全与沙箱是绝对核心**：从子代理环境级别的工具沙箱（#4042），到 MCP 服务器权限隔离（#4729），再到工作流命令权限审计（#4730），社区对安全加固的需求极为迫切。这反映了 TUI 工具在多人协作或复杂工作流中，权限控制是首要考虑因素。
*   **数据持久化与并发可靠性**：大量 Issue 集中在状态存储（SQLite `busy_timeout` #4734）、日志写入（`JsonlHookSink` 并发 #4741）、索引文件操作（会话索引未锁定 #4736）等方面。这表明用户对 TUI 在长时间、多任务运行下的数据一致性和稳定性有较高要求。
*   **配置系统健壮性**：配置文件的静默失败（#4733）、配置更新后运行时未正确重置（#4737）等问题显示，社区希望配置系统更加健壮和透明。用户期望修改配置后能获得即时、明确的反馈，而非静默的错误。
*   **模型提供商切换透明化**：用户（#4720）对于运行时自动切换模型提供商（`deepseek -> zai`）感到困惑，希望切换的时机、原因和后果能更清晰地呈现给用户，并要求切换行为是“有意的 (deliberate)”。

## 开发者关注点

*   **“静默失败”是最大的痛点**：无论是配置解析错误（#4733）、路径解析失败（#4719），还是 MCP 服务器不工作（#4727），不少问题都以静默方式失败或返回错误结果。开发者普遍希望系统能提供清晰的错误提示和告警，而不是在用户浑然不觉时默默出错。
*   **快捷键与键盘布局冲突**：来自社区用户的反馈（#4723）表明，对于非英语用户，全局快捷键（如 `Ctrl+Alt+Q`）与本地布局的输入冲突是一个显著的使用障碍。TUI 工具需要更精细地处理键盘事件，避免与操作系统层的快捷键产生冲突。
*   **启动问题影响首要印象**：macOS 上的启动即崩溃问题（#4716）被标记为 `stop-ship`，说明任何阻碍用户首次启动的问题都是最高优先级。一个稳定、可靠的启动流程是所有后续功能得以被使用的基础。
*   **并发场景下的数据损坏**：多个 Issue（#4741， #4736， #4734）指向了并发操作下的数据损坏风险。这表明开发者在编写并发代码时，对竞态条件和锁的考虑仍需加强，尤其是在涉及文件 I/O 和数据库操作的核心组件中。

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*