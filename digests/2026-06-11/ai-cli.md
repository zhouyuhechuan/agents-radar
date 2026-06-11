# AI CLI 工具社区动态日报 2026-06-11

> 生成时间: 2026-06-11 02:53 UTC | 覆盖工具: 9 个

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

# AI CLI 工具横向对比分析报告（2026-06-11）

## 一、生态全景

当前 AI CLI 工具生态已进入 **“能力深水区”与“体验分化期”** 。一方面，主流工具普遍具备子代理、多模型支持、MCP 集成等基础能力，竞争焦点转向 **可靠性、可控性与协作效率**；另一方面，社区对 **模型行为幻构、Token 消耗失控、安全误报** 等核心痛点的反弹日益强烈，倒逼各团队加速修复与特性迭代。值得注意的是，**Windows 平台兼容性、终端 UI 渲染稳定性、以及 Provider 中立化** 成为跨工具的共性战场，而 **多智能体编排与自动化工作流** 正从概念验证走向工程落地。

---

## 二、各工具活跃度对比

| 工具 | 今日发布数量 | 热门 Issue（Top10） | 主要 PR 数（本文列出） | 核心动态 |
|------|------------|-------------------|----------------------|---------|
| **Claude Code** | 1（v2.1.172） | 10 | 10 | 子智能体递归（深5层）、Amazon Bedrock 区域对齐 |
| **OpenAI Codex** | 2（rust alpha） | 10 | 10 | Token 预算管理工具、TUI 目标增强（长文本+图片） |
| **Gemini CLI** | 0 | 10 | 10 | P1 Bug 修复（Shell 挂起、终端 resize 崩溃）、安全补 XSS |
| **GitHub Copilot CLI** | 0 | 10 | 0 | 模型列表不一致、MCP 策略误判、终端渲染退化 |
| **Kimi Code CLI** | 0 | 3 | 10（23个PR合入/更新） | YOLO 模式可靠性、会话恢复、Windows 兼容性 |
| **OpenCode** | 4（v1.17.0-3） | 10 | 10 | TUI 2.0、v2 Session API、图片粘贴需求高涨 |
| **Pi** | 0 | 10 | 10 | 信任门控（25条评论）、流处理超时、新 Provider 支持 |
| **Qwen Code** | 0 | 10 | 10 | 守护进程模式 alpha 合并、子代理团队协作、TUI 滚动冲突 |
| **DeepSeek TUI (CodeWhale)** | 2（v0.8.56-57） | 10 | 10 | 品牌重塑、Provider 中立化、Hooks v2 |

> **注**：活跃度不能仅看 Issue/PR 数量，还需结合评论热度。例如 Claude Code 的 #18435（多账户）有 109 条评论、580 👍，OpenAI Codex 的 #14593（Token 燃烧）有 604 条评论，远高于其他工具。

---

## 三、共同关注的功能方向

| 需求方向 | 涉及工具（具体诉求） | 说明 |
|---------|-------------------|------|
| **多账户/工作区管理** | Claude Code (#18435, 109评论)、OpenAI Codex (#26867 工作区迁移)、GitHub Copilot CLI (#223 细粒度Token) | 企业级用户强烈要求账户切换与权限继承 |
| **子代理/多智能体可靠性** | Claude Code (递归)、OpenAI Codex (MultiAgentV2 加密失败)、Gemini CLI (挂起/误报成功)、Kimi Code (YOLO模式)、Qwen Code (串行化领取任务) | 核心痛点：子代理超时、状态误报、并发竞争 |
| **安全策略误报与精细控制** | Claude Code (Fable5误报)、OpenAI Codex (Guardian超时回退)、Gemini CLI (IPI绕过修复)、GitHub Copilot CLI (MCP误判)、Kimi Code (路径遍历修复)、Pi (信任门控) | 社区普遍要求“安全但可用”的平衡 |
| **Windows 原生兼容性** | Claude Code (WSL集成)、OpenAI Codex (非ASCII用户名崩溃)、Kimi Code (子进程窗口、日志共享)、OpenCode (IP版本冲突)、Gemini CLI (Wayland) | 多家工具在 Windows 上出现闪退/UI卡顿/编码问题 |
| **终端 UI 渲染退化** | Claude Code (tmux滚动回归)、OpenAI Codex (桌面端UI卡顿)、GitHub Copilot CLI (字符错乱)、Qwen Code (resize碎片化)、DeepSeek TUI (紧凑日志) | 新版发布常破坏终端滚动、流式输出、复制粘贴 |
| **Provider 中立化/多模型支持** | Pi (新增Palantir/Mantle)、DeepSeek TUI (解除硬编码)、Qwen Code (同名模型区分)、GitHub Copilot CLI (Gemini缺失) | 用户希望自由切换 Provider，不被单一模型绑定 |
| **上下文窗口与 Token 管理** | OpenAI Codex (剩余上下文工具、自动压缩)、Claude Code (子Agent递归控制)、Qwen Code (auto memory控制) | Token 消耗过快是突出抱怨，社区要求模型自主感知预算 |

---

## 四、差异化定位分析

| 工具 | 核心定位 | 功能侧重 | 目标用户 | 技术路线 |
|------|---------|---------|---------|---------|
| **Claude Code** | 深度 Agent 编排 + 安全优先 | 子智能体递归（5层）、Amazon Bedrock 集成、模型行为可靠性 | 高级开发者、安全敏感企业 | 基于 Anthropic 模型生态，强调子智能体分层能力 |
| **OpenAI Codex** | Rust 后端 + TUI 协作增强 | Token 预算管理、TUI 目标（/goal）支持长文本/图片、Guardian 审查 | 跨平台开发者、团队协作 | Rust 重写跨平台 CLI，注重上下文窗口自动化 |
| **Gemini CLI** | 多模态 + 安全底座 | Shell 命令可靠性、终端 resize 稳定性、Auto Memory 脱敏 | Linux/安全研究型用户 | Google 生态，强调组件级评估与路径遍历防护 |
| **GitHub Copilot CLI** | GitHub 生态深度融合 | 模型列表与 VS Code 对齐、MCP 策略透明、git 工作树控制 | 企业 GitHub 用户、组织管理员 | 依赖 GitHub Copilot 后端，模型多样性受限于组织策略 |
| **Kimi Code CLI** | 快速迭代 + Windows 优先 | YOLO 模式自动化、会话持久化、MCP 失败降级 | 国内开发者、Windows 用户 | 高频修复，关注子进程管理、日志独立 |
| **OpenCode** | 开源/可扩展 + TUI 2.0 | 图片粘贴、TUI 内联技能、v2 Session API、MCP OAuth 修复 | 开源社区、自定义工作流用户 | 强调插件化与贡献友好，后台架构向守护进程演进 |
| **Pi** | Provider 中立 + 远程工作台 | 信任门控、流处理超时、Palantir Foundry 代理、远程 VPS 部署 | 多 Provider 用户、DevOps | 注重扩展系统兼容性，支持 Telegram 控制 |
| **Qwen Code** | 团队协作 + 守护进程模式 | 子代理串行化、统计持久化、Web-Shell 任务管理 | 团队开发、大型仓库 | 守护进程模式（alpha），强调会话级隔离与团队身份 |
| **DeepSeek TUI (CodeWhale)** | 品牌重塑 + Provider 中立化 | 宪法提示 YAML 化、Hooks v2、侧边栏面板、Voice 输入 | DeepSeek 用户迁移、多模型实验者 | 从 DeepSeek 专有走向通用，强调自动化故障转移 |

---

## 五、社区热度与成熟度

- **🔥 高热度（日活评论数高、Issue 飙速）**  
  - **Claude Code**：社区规模最大，#18435（多账户）580 个 👍，问题讨论深度高，但内存泄漏等顽固 Bug 仍在。  
  - **OpenAI Codex**：#14593（Token 燃烧）604 条评论，业务付费用户痛点反馈剧烈，但开发组响应迅速（TUI 目标三连发）。  
  - **GitHub Copilot CLI**：#53（命令稳定性）75 个 👍，但 GitHub 更新频率低，社区涌现第三方替代方案。

- **⚡ 快速迭代（发布密度高、PR 合入快）**  
  - **Kimi Code CLI**：今日 23 个 PR 更新/合并，Windows 修复密集，但 Issue 仅 3 个，社区规模较小但开发活跃。  
  - **OpenCode**：一日 4 个版本，TUI 2.0 与 v2 Session API 大规模 PR，社区贡献者活跃。  
  - **Qwen Code**：守护进程模式 386 文件变更，团队协作 PR 批量合入，属架构升级密集期。

- **📦 成熟度中等（功能趋于稳定，社区讨论分化）**  
  - **Gemini CLI**：P1 级别 Bug 修复高效（Shell 挂起、resize 崩溃），但社区反馈集中在安全误报与 Agent 通用挂起。  
  - **Pi**：信任门控引发 25 条评论，Provider 扩展持续，但流处理超时等稳定性问题存在。  
  - **DeepSeek TUI**：品牌重塑关键期，Provider 中立化推进，但原 DeepSeek 用户迁移成本高。

---

## 六、值得关注的趋势信号

### 1. 模型行为可靠性成为第一性原理
多个工具同时报告 **模型幻构用户意图**（Claude Code #64260）、**子代理误报成功**（Gemini CLI #22323）、**提前结束任务**（DeepSeek TUI #2989）。开发者对“模型可信度”的容忍度急剧下降——工具不仅要提供能力，还要确保输出可预测。这意味 **可追溯的推理过程、显式的错误码、以及用户可干预的断言机制** 将成为下一阶段差异化关键。

### 2. 安全策略的“人性化”迫在眉睫
Fable 5 安全误报（Claude Code）、Guardian 超时硬阻断（OpenAI Codex）、IPI 绕过（Gemini CLI #27472）、MCP 策略误判（GitHub Copilot CLI）——**“一刀切”的安全机制正在反噬用户**。社区呼唤 **可配置的 allowlist/denylist、可见的审查理由、以及失败时的手动降级通道**。安全，需要学会“建议”而非“命令”。

### 3. 终端 UI 不再是“锦上添花”，而是“核心体验”
tmux 滚动回归、流式输出乱码、resize 碎片化、复制粘贴失效——这些看似“小”的 Bug 在多个工具中高频出现，说明 **TUI 渲染层已成为稳定性薄弱的环节**。随着 Agent 输出越来越长、子代理并发对话越来越复杂，终端需要支持 **分屏、可折叠、超链接、侧边栏** 等高级交互。OpenCode 的 TUI 2.0、Qwen Code 的可折叠思考块、DeepSeek TUI 的紧凑日志，都指向同一方向。

### 4. “Provider 中立”从口号变为工程方案
Pi 在 PR 中新增 Palantir Foundry 代理，DeepSeek TUI 解除子代理模型硬编码，Qwen Code 修复同名模型混淆——**用户不想被单一模型或单一厂商绑定**。这要求 CLI 工具在抽象层支持 **模型能力动态发现、自动回退链、以及统一的计费/统计接口**。能够提供“一次配置、多模型透明调用”的工具将获得开发者忠诚度。

### 5. 守护进程模式成为“智能化底座”
Qwen Code 的守护进程模式（386 文件变更）OpenCode 的 v2 Session API、DeepSeek TUI 的远程工作台——**AI CLI 正在从“临时会话”走向“常驻服务”**。守护进程允许 **会话持久化、异步任务、团队共享上下文、以及与 Web/Desktop 端同步**。这标志着工具定位从“命令行对话”升级为“AI 操作系统接口”，对工程复杂度要求陡增。

### 6. Windows 用户正在“被迫容忍”
尽管多家工具在修复 Windows 兼容性，但问题依然高发：非 ASCII 用户名、子进程弹出控制台、IPC 超时、日志文件共享冲突等。Windows 开发者社区在抱怨中展现出惊人的耐心，但长期看，**无法提供原生体验的工具将失去快速增长的企业桌面用户群**。

---

**总结**：AI CLI 工具正处在一个 **功能膨胀后必须回归工程质量** 的关口。未来 3-6 个月，谁能最快解决“模型不可靠、安全误频繁、终端体验差”这三座大山，同时提供“多 Provider 自由、团队协作、持久化服务”等增量价值，谁就能在开发者心智中占据不可替代的位置。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，作为一名专注于 Claude Code 生态的技术分析师，我已审阅截止 2026 年 6 月 11 日 `anthropics/skills` 仓库的相关数据。

以下是基于社区 Issue 和 Pull Request 数据生成的 Claude Code Skills 社区热点报告。

---

### Claude Code Skills 社区热点报告 (数据截止: 2026-06-11)

#### 1. 热门 Skills 排行 (Top 8)

以下 Skills 是当前社区讨论热度最高、最受关注的 Pull Request，反映了社区的迫切需求或创新方向。

1.  **多功能文档生成与格式支持**
    -   **PR**: [#514 Add document-typography skill](https://github.com/anthropics/skills/pull/514), [#486 Add ODT skill](https://github.com/anthropics/skills/pull/486)
    -   **功能**: 前者专注于 AI 文档的排版质量控制（如孤行、寡段、编号对齐）；后者新增对 OpenDocument (.odt/.ods) 格式的原生创建、填充与转换支持。
    -   **热点**: 社区对 **AI 输出质量**（排版细节）和**格式兼容性**（开源、ISO 标准格式）的双重追求。用户期待 AI 生成的内容不仅正确，而且“美观”和“通用”。
    -   **状态**: 均为 `OPEN`

2.  **核心技能质量与工具箱完善**
    -   **PR**: [#83 Add skill-quality-analyzer and skill-security-analyzer](https://github.com/anthropics/skills/pull/83), [#210 Improve frontend-design skill](https://github.com/anthropics/skills/pull/210)
    -   **功能**: `skill-quality-analyzer` 是一种“元技能”，用于评估其他 SKILL.md 文件的质量；`frontend-design` 的优化则提升了现有热门技能的可执行性。
    -   **热点**: 社区开始从“创建技能”转向“**优化技能生态**”。用户关注技能本身的编写质量、可维护性和复用性，而非仅仅是功能的堆砌。
    -   **状态**: 均为 `OPEN`

3.  **AI Agent 的持久化记忆与上下文管理**
    -   **PR**: [#154 Add shodh-memory skill](https://github.com/anthropics/skills/pull/154)
    -   **功能**: 为 AI Agent 提供跨对话的持久化记忆系统，使其能够在长期交互中保持上下文和用户偏好。
    -   **热点**: **Agent 的长效记忆**是社区的刚需。围绕如何安全、高效地在文件系统中管理上下文信息，社区展开了深度讨论，这直接关系到 Agent 的实用性与智能化程度。
    -   **状态**: `OPEN`

4.  **专有系统与垂直领域集成**
    -   **PR**: [#181 Add SAP-RPT-1-OSS predictor skill](https://github.com/anthropics/skills/pull/181), [#806 Add sensory skill (macOS automation)](https://github.com/anthropics/skills/pull/806)
    -   **功能**: SAP 预测分析技能，针对企业级 ERP 数据；macOS 原生自动化技能，通过 AppleScript 绕开截图进行本地桌面控制。
    -   **热点**: 社区需求正从通用开发向**垂直领域**和**平台特定**的应用场景深入。企业集成（SAP）和平台原生能力（macOS）是社区探索的重点，显示了 Claude Code 作为“万能枢纽”的潜力。
    -   **状态**: 均为 `OPEN`

5.  **元技能与智能 Agent 编排**
    -   **PR**: [#1140 Implement agent-creator skill](https://github.com/anthropics/skills/pull/1140)
    -   **功能**: 一个创建“技能组合（agent sets）”的元技能，允许用户为特定任务动态组合一组 Agent。
    -   **热点**: **Agent 的自动编排与动态组合**。社区不满足于单技能运行，而是期望 Claude 能理解复杂任务，并自动激活一套最合适的技能链。这是实现高级自动化的重要一步。
    -   **状态**: `OPEN`

6.  **软件开发工具箱**
    -   **PR**: [#147 Add codebase-inventory-audit skill](https://github.com/anthropics/skills/pull/147), [#723 Add testing-patterns skill](https://github.com/anthropics/skills/pull/723)
    -   **功能**: 代码库审计与清理、全面测试模式指南。
    -   **热点**: **代码质量与工程规范**。用户正系统性地将 Claude Code 应用于DevOps 和软件工程全生命周期，从代码审计到测试，旨在建立标准化的 AI 辅助开发流程。
    -   **状态**: 均为 `OPEN`

#### 2. 社区需求趋势

从 Issues 来看，社区最期待的 Skill 方向呈现出明显的“基础设施”和“企业级”特性：

-   **组织级协作与共享**: **[#228 组织级技能分享](https://github.com/anthropics/skills/issues/228)** 是需求最强烈的 Issue。社区不再满足于个人使用，而是迫切需要一个官方的、在企业内共享和管理 Skills 的平台或机制，以替代手动传递 `.skill` 文件的低效方式。
-   **安全与信任治理**: **[#492 官方命名空间下的安全风险](https://github.com/anthropics/skills/issues/492)** 和 **[#1175 企业文档安全顾虑](https://github.com/anthropics/skills/issues/1175)** 表明，随着 Skills 生态的壮大，**安全、鉴权和信任边界**已成为社区核心焦虑点。用户需要明确的权限模型和安全性分析工具。
-   **评估与效率**: **[#556 run_eval.py 无法触发技能](https://github.com/anthropics/skills/issues/556)** 和 **[#1169 skill-creator 评估循环为 0%](https://github.com/anthropics/skills/issues/1169)** 揭示了开发者工具（skill-creator）本身存在严重缺陷，这阻碍了 Skills 的创作与优化。 **稳定、可用的开发者工具链** 是社区当前最急迫的基础需求。
-   **去重与模块化**: **[#189 插件包内容重复](https://github.com/anthropics/skills/issues/189)** 等问题表明，社区希望官方对 Skills 进行分类和模块化管理，避免混乱。
-   **MCP 化与标准化**: **[#16 将 Skill 暴露为 MCP](https://github.com/anthropics/skills/issues/16)** 老 Issue 仍然具有前瞻性，社区期望 Skills 能通过标准协议（如 MCP）对外提供 API 接口，实现更好的互操作性。

#### 3. 高潜力待合并 Skills

以下 PR 讨论活跃，且解决了社区的切肤之痛，预计将很快被合并或产生重大影响：

-   **[#1099 skill-creator: 修复 Windows 子进程崩溃](https://github.com/anthropics/skills/pull/1099)** & **[#1050 skill-creator: 修复 Windows 兼容性](https://github.com/anthropics/skills/pull/1050)**: 这两个 PR 直指社区“开发者工具”的硬伤——Windows 兼容性问题。它们直接解决了`run_eval.py`等核心脚本的可用性问题，**合并优先级极高**。
-   **[#538 修复 PDF SKILL.md 引用大小写敏感问题](https://github.com/anthropics/skills/pull/538)** & **[#539 修复 YAML 特殊字符未引用的解析问题](https://github.com/anthropics/skills/pull/539)**: 这些“修复”类 PR 虽然看起来小，但解决了**跨平台执行和技能文件解析**的根本性问题。它们是影响所有技能稳定性的关键底层修复，社区关注度极高。
-   **[#1140 实现 agent-creator 技能](https://github.com/anthropics/skills/pull/1140)**: 该 PR 不仅是功能创新，还包含了对 Windows 支持和评估器修复，一次性解决了多个痛点，表现出很高的技术成熟度。

#### 4. Skills 生态洞察

> **一句话总结**: 当前社区对 Skills 的诉求已从“创造新技能”全面转向 **“构建专业化、安全化、可共享的企业级生态系统”** ，而实现这一目标的**最大瓶颈在于官方提供的开发者工具链（特别是评估与调试工具）的稳定性与平台兼容性**。

---

好的，各位开发者，以下是基于 GitHub 上 Anthropics 官方仓库 `an anthropics/claude-code` 生成的 2026 年 6 月 11 日社区动态日报。

---

## 📰 Claude Code 社区动态日报 | 2026-06-11

### 1. 今日速览

**版本更新**：发布了 v2.1.172，引入了备受关注的**子智能体递归**能力，现在智能体可以创建自己的子智能体（最深5层），显著扩展了复杂任务编排的可能性。同时，Amazon Bedrock 的区域配置也进行了对齐优化。

**社区热议**：关于**多账户管理**的功能请求热度空前（109 条评论），反映了用户对多身份工作流管理的强烈需求。**Opus 4.8 模型幻构用户意图**的问题引发了新一轮关于模型可靠性的讨论。

**Bug 追踪**：**Fable 5 模型安全策略误报**成为新的焦点，多位用户反馈其在处理常规安全、生物信息或审计任务时被错误拦截，影响了该模型的可用性。

### 2. 版本发布

- **v2.1.172** | 2026-06-11
  - 🕸️ **子智能体递归**：子智能体现可以生成自己的子智能体，支持最多5层深度。这对于需要分层分析和处理的复杂项目是一大利好。
  - ☁️ **Amazon Bedrock 改进**：当未设置 `AWS_REGION` 环境变量时，Claude Code 现在会读取 `~/.aws/config` 文件中的区域配置，并与 AWS SDK 的行为保持一致。用户可以通过 `/status` 命令查看当前区域来源。
  - 📖 **Markdown 浏览体验优化**：在浏览 Markdown 文件时增加了搜索栏，方便快速定位内容。

### 3. 社区热点 Issues

以下是从过去24小时内有更新的Issue中精选出的10条，反映了社区最关注的痛点和需求：

1.  **[Feature] 在 Claude Desktop 中管理多个账户** (`#18435`)
    - **重要性**: 需求极其强烈，是近期评论数最高的Issue。用户需要在不反复登出的情况下，在不同 Claude 账号（如个人账号 vs 工作团队账号）之间快速切换。
    - **社区反应**: 109 条评论，580 个 👍，社区呼声极高。
    - [链接](https://github.com/anthropics/claude-code/issues/18435)

2.  **[Bug] 严重内存泄漏导致系统冻结** (`#11315`)
    - **重要性**: 一个非常严重且顽固的性能问题，消耗高达129GB虚拟内存，导致系统完全卡死，需要硬重启。
    - **社区反应**: 64 条评论，虽然已存在数月，但仍在持续讨论中，说明该问题影响深远。
    - [链接](https://github.com/anthropics/claude-code/issues/11315)

3.  **[Bug] Opus 4.8 幻构用户请求上下文** (`#64260`)
    - **重要性**: 一个新的模型行为问题。报告指出 Opus 4.8 会无中生有地“幻构”一个当前时态的用户请求，并固执地围绕这个虚构的上下文执行任务，这严重破坏了用户对模型输出可靠性的信任。
    - **社区反应**: 9 条评论，这是一个值得高度关注的模型可靠性问题。
    - [链接](https://github.com/anthropics/claude-code/issues/64260)

4.  **[Feature] 原生 WSL 远程集成** (`#49933`)
    - **重要性**: 针对在 Windows 上使用 WSL 的开发者的核心需求。目前缺少原生集成，导致开发体验割裂。该功能请求拥有很高的支持度。
    - **社区反应**: 9 条评论，55 个 👍。
    - [链接](https://github.com/anthropics/claude-code/issues/49933)

5.  **[Bug] Cowork 在 ARM64 (Snapdragon X) 上失败** (`#50674`)
    - **重要性**: 虽然被标记为重复，但这个问题关乎最新的 Arm Windows PC 生态。对于使用高通骁龙 X 系列芯片设备的用户来说，`cowork` 功能完全无法使用，是平台兼容性的痛点。
    - **社区反应**: 19 条评论。
    - [链接](https://github.com/anthropics/claude-code/issues/50674)

6.  **[Bug] Bash 工具 `ENOSPC` 错误，即使磁盘有空余** (`#63909`)
    - **重要性**: 一个奇怪的系统交互问题。Bash 工具在捕获子进程输出时报告磁盘空间不足，导致所有命令输出丢失，但磁盘本身空间充足。严重影响了需要处理大量输出的用户。
    - **社区反应**: 8 条评论，16 个 👍。
    - [链接](https://github.com/anthropics/claude-code/issues/63909)

7.  **[Bug] TUI 滚动回退回归 (tmux)** (`#67289`)
    - **重要性**: 最新版本 v2.1.172 中的一个新 Bug，破坏了在 tmux 中的滚动查看能力，对依赖终端回滚的开发者来说是一个可访问性降级。
    - **社区反应**: 刚提出的新问题，已有 2 条评论。
    - [链接](https://github.com/anthropics/claude-code/issues/67289)

8.  **[Bug] Fable 5 安全误报使其在防御性网络威胁情报中几乎不可用** (`#67305`)
    - **重要性**: 多个用户报告 Fable 5 在涉及网络安全和生物学的常规任务中，被错误地触发安全机制，自动降级到 Opus 4.8，严重影响了其在该领域的价值。
    - **社区反应**: 刚提出的新问题，1 条评论，但已有多个相关 Issue（如 `#67304`, `#67302`）集中爆发，表明这是一个严重的模型特性问题。
    - [链接](https://github.com/anthropics/claude-code/issues/67305)

9.  **[Bug] Edit 工具无声地将 Tab 转换为空格** (`#26996`)
    - **重要性**: 对于使用 Tab 缩进的代码库（如 Go、Python 的某些风格），此 Bug 会导致编辑匹配反复失败，因为工具悄无声息地改变了代码格式。
    - **社区反应**: 15 条评论，27 个 👍。
    - [链接](https://github.com/anthropics/claude-code/issues/26996)

10. **[Bug] 窗口 Homebrew 未检测到新版本** (`#67294`)
    - **重要性**: 虽然只是一个包管理问题，但它会阻碍 Homebrew 用户快速获取最新的 v2.1.172 版本。在每次发布时需要关注。
    - **社区反应**: 1 条评论，属于新的紧急问题。
    - [链接](https://github.com/anthropics/claude-code/issues/67294)

### 4. 重要 PR 进展

1.  **修复 `plugin-dev` 中的验证器脚本** (`#66416`)
    - **内容**: 解决了因为 `set -e` 导致验证器脚本在发现第一个问题时立即终止，无法完成全面检查的问题。
    - **重要性**: 提高插件开发工具链的实用性和用户体验。
    - [链接](https://github.com/anthropics/claude-code/pull/66416)

2.  **修复 `agentic_review` 子进程的环境变量传递** (`#65875`)
    - **内容**: 修复了在使用 OAuth/gateway 的场景下，`agentic_review` 子进程无法继承 `ANTHROPIC_BASE_URL` 变量导致认证失败的问题。
    - **重要性**: 解决了使用代理网关时的关键阻塞问题。
    - [链接](https://github.com/anthropics/claude-code/pull/65875)

3.  **延长 Issue 自动关闭时间** (`#63686`)
    - **内容**: 将 Issue 因不活跃而自动标记并关闭的时间从 14 天延长至 90 天。
    - **重要性**: 给高质量的技术讨论和尚未解决的难题提供了更宽裕的时间窗口，有利于社区反馈的沉淀。
    - [链接](https://github.com/anthropics/claude-code/pull/63686)

4.  **修复 Devcontainer Docker 检测逻辑** (`#66372`)
    - **内容**: 修复了在 PowerShell 中因错误处理不当，导致 Docker 守护进程未运行时无法正确报错并提示用户的问题。
    - **重要性**: 提升了开发容器环境的体验和错误反馈的准确性。
    - [链接](https://github.com/anthropics/claude-code/pull/66372)

5.  **为 SubAgent 添加 `${CLAUDE_PLUGIN_ROOT}` 限制文档** (`#65919`)
    - **内容**: 在文档中增加了一个已知限制：SubAgent 可能无法正确解析 `${CLAUDE_PLUGIN_ROOT}` 变量，导致无法访问插件文件。
    - **重要性**: 主动告知用户这一潜在问题，避免开发过程中出现意外错误。
    - [链接](https://github.com/anthropics/claude-code/pull/65919)

6.  **修复 `allowed-tools` 的文档歧义** (`#65916`)
    - **内容**: 明确区分了 `allowed-tools`（自动批准白名单）与 SubAgent 中 `tools:`（硬性限制）的不同用途。
    - **重要性**: 澄清了概念，防止用户错误地将 `allowed-tools` 视为权限边界，影响实际开发。
    - [链接](https://github.com/anthropics/claude-code/pull/65916)

7.  **修复 `ralph-wiggum` 插件的错误处理** (`#66573`)
    - **内容**: 修复了因 `set -euo pipefail` 导致的错误处理逻辑失效，使得某些错误能被正确捕获并处理。
    - **重要性**: 提升了内置插件的稳定性和健壮性。
    - [链接](https://github.com/anthropics/claude-code/pull/66573)

8.  **为 `plugin-dev` 添加 `plugin.json` 清单** (`#65286`)
    - **内容**: 为 `plugin-dev` 添加了缺失的 `plugin.json` 清单文件，使其便于通过标准插件机制发现和安装。
    - **重要性**: 完善了插件生态的基础设施。
    - [链接](https://github.com/anthropics/claude-code/pull/65286)

9.  **更新插件 README 中的 NPM 安装说明** (`#63460`)
    - **内容**: 将文档中已废弃的 `npm install -g` 安装方式更新为推荐的 `curl/irm` 方式。
    - **重要性**: 保持文档的时效性和准确性，降低新用户的入门门槛。
    - [链接](https://github.com/anthropics/claude-code/pull/63460)

10. **修复 `.mcp.json` 示例文档** (`#64607`)
    - **内容**: 修正了插件文档中 `.mcp.json` 文件的格式错误示例。
    - **重要性**: 纠正文档错误，避免误导开发者。
    - [链接](https://github.com/anthropics/claude-code/pull/64607)

### 5. 功能需求趋势

- **多账户与多平台支持**: 社区强烈要求更好的账户管理（`#18435`）和跨平台支持，特别是原生的 **WSL 集成** (`#49933`)。
- **模型行为可靠性**: 对模型“幻构”意图（`#64260`）、不遵循用户定义的规则/工作流（`#54117`, `#49259`）等问题越来越受关注。用户期望模型在各种场景下都表现出稳定且可预测的行为。
- **作为工具的核心能力增强**: 用户关注编辑器的代码操作透明性（`#26996` tab/空格问题），以及 Agent 编排能力的深度（子Agent递归）。
- **安全与合规性**: 引入 Fable 5 等强安全模型后，如何平衡**安全策略的严格性与实际使用场景的可用性**是新的挑战。频繁的误报（`#67305`, `#67304`）影响了其在安全、生物信息等领域的实用性。
- **IDE 与终端集成**: 除了丰富的终端（TUI）体验，社区也在关注**非阻断式后台审查**（如 agentic_review）和改善与 `tmux` 等工具的兼容性（`#67289`）。

### 6. 开发者关注点

- **核心痛点**: **内存泄漏** (`#11315`) 和**性能稳定性**依然是高优问题。**模型行为不符合预期**（如忽略规则、幻构上下文）带来的挫败感很强。
- **高频需求**: 支持**多账号管理**和**跨平台无缝协同**（特别是Windows/WSL）是呼声最高的功能诉求。
- **新版本适应**: v2.1.172 带来的 `tmux` 滚动回归 (`#67289`) 和 Homebrew 版本检测问题 (`#67294`) 提醒我们，新版本的引入需要充分考虑与开发者现有工作流的兼容性。
- **安全策略的精细化**: 开发者希望安全模型能更智能、更少误报，或者提供更精细的配置选项，以便在“安全”和“可用”之间找到平衡。Fable 5 的误报问题 (`#67305`) 是当前最热的新话题。
- **文档与教育**: 围绕插件开发、SubAgent 变量限制 (`#65919`) 和 Hook 系统 (`#63382`) 的文档需要有更多的实践指导和清晰的边界说明，以减少开发者的困惑。

---

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-06-11

## 今日速览

- **Token 消耗与窗口管理成为社区焦点**：Issue #14593（Token 燃烧过快）评论突破 600 条，社区持续关注计费与资源控制；同时多个 PR 引入“上下文剩余工具”和“comp_hash 变化时自动压缩”，旨在帮助模型自主管理上下文窗口。
- **Windows 桌面端崩溃/兼容性问题集中爆发**：至少 5 个新 Issue 报告 Windows 版 Codex Desktop 在更新后启动即闪退或 UI 异常，涉及非 ASCII 用户名、透明 UI 等场景，开发团队已通过多个 PR 开始增强跨平台文件系统测试。
- **TUI 目标功能增强三连发**：OpenAI 工程师提交了 3 个连续 PR（#27508-#27510），为 /goal 命令增加长文本粘贴和图片支持，极大提升终端用户的多人协作体验。

## 版本发布

- **[rust-v0.140.0-alpha.7](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.7)**：0.140.0-alpha.7 发布，未提供详细变更日志。
- **[rust-v0.140.0-alpha.4](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.4)**：0.140.0-alpha.4 发布，未提供详细变更日志。

（注：均为 Rust 后端 alpha 版本，可能包含底层库修复）

## 社区热点 Issues（Top 10）

1. **[#14593] [bug] Token 消耗极快**  
   - 评论 604 | 👍 265  
   - 用户持续反馈 Business 订阅下 token 燃烧速度异常，已有 604 条讨论，社区要求公开计费逻辑和实时消耗统计。  
   - [查看详情](https://github.com/openai/codex/issues/14593)

2. **[#26867] [bug] GitHub PR Review 仍使用已停用的工作区**  
   - 评论 13 | 👍 7  
   - 从 Business 迁移到 Personal Pro 账户后，GitHub PR 审查功能错误地引用旧工作区，导致“Workspace deactivated”错误。  
   - [查看详情](https://github.com/openai/codex/issues/26867)

3. **[#25463] [bug] Desktop 项目线程消失，但本地 JSONL 仍在**  
   - 评论 12 | 👍 1  
   - 用户报告对话记录在 UI 中消失，磁盘文件却完整，指向本地状态索引损坏或同步 Bug。  
   - [查看详情](https://github.com/openai/codex/issues/25463)

4. **[#17642] [bug] CLI 提示“gpt-5.3-codex-spark”模型不受 ChatGPT 账户支持**  
   - 评论 12 | 👍 0  
   - Pro 订阅用户在 CLI 中使用 `gpt-5.3-codex-spark` 模型被拒，暴露模型分级与认证之间的兼容性问题。  
   - [查看详情](https://github.com/openai/codex/issues/17642)

5. **[#23198] [bug] Windows Desktop 响应极其缓慢**  
   - 评论 12 | 👍 31  
   - 普遍反映 Codex Desktop 在 Windows 上拖拽、输入延迟严重，疑与前台渲染线程相关。  
   - [查看详情](https://github.com/openai/codex/issues/23198)

6. **[#13553] [bug] Windows 用户名含非 ASCII 字符时 Store 版无法启动**  
   - 评论 11 | 👍 9  
   - 韩文、中文用户名导致 Codex 启动即崩溃，社区期待 fast-fix。  
   - [查看详情](https://github.com/openai/codex/issues/13553)

7. **[#20833] [bug] Desktop 侧边栏隐藏旧工作区对话**  
   - 评论 9 | 👍 5  
   - 与 #25463 类似，但强调侧边栏而非项目视图，用户尝试通过反馈 ID 追踪无果。  
   - [查看详情](https://github.com/openai/codex/issues/20833)

8. **[#26753] [bug] MultiAgentV2 加密 spawn_agent 返回 400**  
   - 评论 9 | 👍 2  
   - 启用 `features.multi_agent_v2` 后每个回合都失败，因为函数模式被加密工具拒绝，严重影响子代理工作流。  
   - [查看详情](https://github.com/openai/codex/issues/26753)

9. **[#27175] [bug] Windows 26.602.71036 更新后崩溃**  
   - 评论 8 | 👍 2  
   - 继 #23198 后又一波 Windows 闪退报告，用户为 ChatGPT Pro $200/月 订阅者，影响面大。  
   - [查看详情](https://github.com/openai/codex/issues/27175)

10. **[#22796] [bug] Desktop 项目侧边栏显示“No chats”**  
    - 评论 7 | 👍 1  
    - 尽管 `session_index.jsonl` 仍然存在，UI 却误报空项目，属于状态不一致类 Bug。  
    - [查看详情](https://github.com/openai/codex/issues/22796)

## 重要 PR 进展（Top 10）

1. **[#27518] [feature] 添加“剩余上下文”工具**  
   - 作者 pakrym-oai | 状态 OPEN  
   - 为模型提供查询当前 Token 预算剩余量的工具，配合 token budget 特性使用。  
   - [查看详情](https://github.com/openai/codex/pull/27518)

2. **[#27510] [feature] TUI 目标支持图片输入**  
   - 作者 etraut-openai | 状态 OPEN（3/3 系列）  
   - 在 `/goal` 命令中允许粘贴图片，从底层支持多模态目标描述。  
   - [查看详情](https://github.com/openai/codex/pull/27510)

3. **[#27509] [feature] TUI 目标支持长粘贴文本**  
   - 作者 etraut-openai | 状态 OPEN（2/3 系列）  
   - 解决过去长文本被截断的问题，将 placeholder 机制引入目标定义。  
   - [查看详情](https://github.com/openai/codex/pull/27509)

4. **[#27508] [feature] TUI 目标支持长原始目标文本**  
   - 作者 etraut-openai | 状态 OPEN（1/3 系列）  
   - 将 `thread/goal/set` 的字符限制从 4000 提升，适配大型目标。  
   - [查看详情](https://github.com/openai/codex/pull/27508)

5. **[#27454] [test] 添加跨平台文件系统适配器测试覆盖**  
   - 作者 anp-oai | 状态 OPEN  
   - 将原本只在 Unix 上运行的测试扩展到 Windows，为 PathUri 迁移做准备。  
   - [查看详情](https://github.com/openai/codex/pull/27454)

6. **[#27488] [feature] 添加“新建上下文窗口”工具**  
   - 作者 pakrym-oai | 状态 OPEN  
   - 允许模型请求清空当前上下文并开始新窗口，避免因窗口沾满导致无用压缩。  
   - [查看详情](https://github.com/openai/codex/pull/27488)

7. **[#27520] [feature] comp_hash 变化时自动压缩历史**  
   - 作者 aibrahim-oai | 状态 OPEN  
   - 当模型配置（comp_hash）改变时，自动触发压缩，保护后续对话质量。  
   - [查看详情](https://github.com/openai/codex/pull/27520)

8. **[#27519] [feature] 为 ModelInfo 添加 comp_hash 元数据**  
   - 作者 aibrahim-oai | 状态 OPEN  
   - 为模型信息增加不透明标识，便于下游识别压缩兼容性。  
   - [查看详情](https://github.com/openai/codex/pull/27519)

9. **[#27266] [fix] 调整提示图片时保留元数据**  
   - 作者 fjord-oai | 状态 OPEN  
   - 保留 ICC 配置文件和 EXIF 方向信息，避免旋转或丢失色彩空间。  
   - [查看详情](https://github.com/openai/codex/pull/27266)

10. **[#27440] [fix] Guardian 超时后回退到手动审批**  
    - 作者 kbazzi | 状态 OPEN（标记 code-reviewed）  
    - 当 Guardian 自动审查因超时无结果时，不再硬性阻止，而是弹出手动审批框，提升可用性。  
    - [查看详情](https://github.com/openai/codex/pull/27440)

## 功能需求趋势

从过去 24 小时的 Issues 和 PR 中可以提炼出以下社区最关注的方向：

- **上下文窗口与 Token 管理**：多个 Issue 抱怨 Token 消耗过快，PR 同步增加“剩余上下文工具”和“新窗口工具”，表明社区迫切希望模型能自主感知并管理上下文预算。
- **Windows 原生兼容性**：大量 Windows 用户报告启动崩溃、UI 卡顿、非 ASCII 用户名冲突，开发团队已开始增加跨平台测试覆盖，但修复进度仍待加速。
- **子代理（Sub‑agent）与多智能体协同**：MultiAgentV2 加密模式问题、子代理关闭时“agent loop died”等 Bug 频繁出现，社区对多智能体工作流稳定性期望很高。
- **Desktop 状态同步一致性**：对话记录在本地存在但 UI 不显示的问题反复出现（#25463、#20833、#22796），说明本地索引（SQLite / JSONL）与渲染层同步逻辑存在缺陷。
- **认证与工作区迁移**：从 Business 迁移到 Personal Pro 后的权限残影问题，以及对新模型（gpt-5.3-codex-spark）的认证支持，反映用户对灵活账户切换和模型选择的需求。

## 开发者关注点

- **紧急痛点**：
  - Windows Desktop 在最新更新（26.602.71036 / 26.608.1337）后无法正常启动，回滚需求强烈。
  - Token 消耗不受控，Business 订阅用户反馈“每分钟几十美元”的消耗速度，需紧急审计计费逻辑。
  - GitHub PR Review 功能因工作区缓存错误而失效，影响团队协作流程。
  - 多代理加密模式直接导致所有请求失败，阻塞高级用户使用 MultiAgentV2。
- **高频请求**：
  - 提供 token 使用仪表板或实时配额警告。
  - 修复 Windows 用户名中的非 ASCII 支持——该问题已存在 3 个月（#13553）。
  - 改进上下文压缩策略，避免因压缩导致关键信息丢失（PR #21777 提议将压缩暴露给 agent）。
  - 统一 Desktop 与 CLI 的认证状态，减少“Workspace deactivated”类报错。
- **开发者提醒**：
  - 当前 Rust alpha 版本发布频繁，建议关注 changelog 以了解底层修复。
  - 如果使用 `/goal` 命令，请留意即将发布的新 PR 系列，将带来长文本和图片支持，可能影响现有工作流。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 | 2026-06-11

## 📌 今日速览

今天社区没有新版本发布，但多项高优先级 Bug 修复和安全补丁进入合并阶段：核心团队提交了解决 shell 命令挂起（#25166）和终端 resize 崩溃（#27502）的关键 PR；同时自动内存（Auto Memory）系统的安全与效率问题（#26525、#26522）持续引发讨论，社区对 Agent 通用化、子代理误报等稳定性问题的关注度依然最高。

---

## 🚀 版本发布

**无**（过去 24 小时内无新 Release）

---

## 🔥 社区热点 Issues（10 个）

1. **[Generalist agent 挂起] #21409**  
   `priority/p1` · 7 条评论 · 8 👍  
   用户反馈 Gemini CLI 在委托给通用代理时永久挂起，简单操作（如创建文件夹）也无法完成。临时解决方案是在提示中禁用子代理。  
   [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21409)

2. **[子代理达到 MAX_TURNS 后误报成功] #22323**  
   `priority/p1` · 6 条评论 · 2 👍  
   `codebase_investigator` 子代理在达到最大轮次数后仍返回 `status: "success"` 和 `Termination Reason: "GOAL"`，隐藏了实际中断，导致用户难以发现任务未完成。  
   [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22323)

3. **[Shell 命令执行后卡在“等待输入”] #25166**  
   `priority/p1` · 4 条评论 · 3 👍  
   大量用户报告简单 CLI 命令完成后界面依然显示“Awaiting user input”，shell 无法正常退出。该问题已有对应 PR #27842 进行修复。  
   [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/25166)

4. **[稳健的组件级评估] #24353**  
   `priority/p1` · 7 条评论  
   继 #15300 引入行为评估后，此 EPIC 跟踪组件级评估的建立，目前已生成 76 个行为评估测试，覆盖 6 个支持的 Gemini 模型。  
   [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/24353)

5. **[AST 感知的文件读取/搜索/代码库映射影响评估] #22745**  
   `priority/p2` · 7 条评论 · 1 👍  
   探索使用 AST 感知工具（如 AST grep）来精确读取方法边界、减少 token 噪音，从而提升 Agent 质量和效率。  
   [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22745)

6. **[Auto Memory：确定性脱敏与减少日志] #26525**  
   `priority/p2` · 5 条评论  
   自动记忆功能在读取本地转录时，将内容先送入模型后再进行脱敏，存在敏感数据泄露风险；同时服务可能记录现有技能数据，需加强确定性处理。  
   [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/26525)

7. **[Auto Memory：低信号会话无限重试] #26522**  
   `priority/p2` · 5 条评论  
   自动记忆在遇到低信号会话时不会标记为“已处理”，导致该会话被反复扫描和重试，造成不必要的计算消耗。  
   [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/26522)

8. **[Browser 子代理在 Wayland 下失败] #21983**  
   `priority/p1` · 4 条评论 · 1 👍  
   在 Wayland 显示服务器上，浏览器子代理无法正常启动，直接返回 `Termination Reason: GOAL` 但实际失败。影响 Linux 用户。  
   [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21983)

9. **[模型“思考太久，什么都不做”] #27785**  
   `priority/p2` · 3 条评论  
   用户反馈 Gemini CLI 在思考阶段停留过久且无任何输出，最终也不执行任何操作。社区请求用户提供聊天历史 JSON 以分析。  
   [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/27785)

10. **[超过 128 个工具时返回 400 错误] #24246**  
    `priority/p2` · 3 条评论  
    当可用工具数量超过 400（实际触发条件为 >128）时，API 返回 400 错误。期望 Agent 能更智能地限制工具范围。  
    [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/24246)

---

## 🛠 重要 PR 进展（10 个）

1. **[核心修复：防止 Shell 退出结果在输出排空时挂起] #27842**  
   `priority/p1` · 开放  
   修复 #25166，在 PTY 执行完成后果渲染管道无错误处理导致界面卡住的问题，为输出添加了超时和错误边界。  
   [查看 PR](https://github.com/google-gemini/gemini-cli/pull/27842)

2. **[核心修复：终端 resize 时的 ioctl EBADF 崩溃] #27502**  
   `priority/p1` · 已合并  
   解决 PTY 刚被销毁时 React resize 回调竞争条件导致的崩溃，属于 P1 级稳定性修复。  
   [查看 PR](https://github.com/google-gemini/gemini-cli/pull/27502)

3. **[安全修复：解析主机名后检查私有 IP] #27473**  
   `priority/p1` · 已合并  
   `isBlockedHost()` 此前仅验证 IP 字面量，主机名解析到私有 IP 会绕过安全检查，可能导致 SSRF 风险。  
   [查看 PR](https://github.com/google-gemini/gemini-cli/pull/27473)

4. **[核心修复：防止空 parts 误判为 FunctionCall] #27474**  
   `priority/p2` · 已合并  
   `Array.prototype.every([])` 返回 true，导致空 `parts` 消息被错误分类为函数调用或函数响应，影响消息处理。  
   [查看 PR](https://github.com/google-gemini/gemini-cli/pull/27474)

5. **[安全修复：工具确认 UI 实施截断锁定防止 IPI 绕过] #27472**  
   `priority/p1` · 已合并  
   通过要求用户展开并查看完整内容后才能确认工具执行，修复了 #23433 中描述的间接提示注入（IPI）绕过漏洞。  
   [查看 PR](https://github.com/google-gemini/gemini-cli/pull/27472)

6. **[功能增强：trustedFolders.json 支持列表格式] #27648**  
   `priority/p3` · 开放  
   允许 `trustedFolders.json` 使用 JSON 数组格式，方便手动维护简单目录列表；原有对象格式继续兼容。  
   [查看 PR](https://github.com/google-gemini/gemini-cli/pull/27648)

7. **[文档修复：修复遥测页面中的结构错误] #27649**  
   `priority/p1` · 开放  
   将 Traces 部分从 Metrics 子节中分离出来，修正了文档分类错误。  
   [查看 PR](https://github.com/google-gemini/gemini-cli/pull/27649)

8. **[安全修复：阻止技能安装中的路径遍历漏洞] #27767**  
   `size/m` · 开放  
   修复 `installSkill`、`linkSkill`、`uninstallSkill` 中的三个路径遍历漏洞，防止攻击者通过构造的 frontmatter 访问任意文件。  
   [查看 PR](https://github.com/google-gemini/gemini-cli/pull/27767)

9. **[CI 安全：验证 workflow_run 来源防止 Fork 投毒] #27753**  
   `size/s` · 开放  
   链式 E2E 管道通过检查 `repo.full_name` 确保只信任来自同一仓库的触发事件，阻止 fork PR 盗用 secrets。  
   [查看 PR](https://github.com/google-gemini/gemini-cli/pull/27753)

10. **[核心修复：使 read_background_output 延迟可被中止感知] #27839**  
    `size/s` · 开放  
    修复按 ESC 取消 `read_background_output` 后，spinner 仍然旋转且新提示被排队的问题。将 `setTimeout` 替换为 AbortSignal 感知版本。  
    [查看 PR](https://github.com/google-gemini/gemini-cli/pull/27839)

---

## 📈 功能需求趋势

从近期 Issue 和讨论中可以提炼出社区最关注的三个功能方向：

1. **Agent 智能化与鲁棒性**  
   - **AST 感知工具**：精准读取方法边界、搜索语法结构，减少 token 浪费（#22745、#22746）  
   - **自我意识**：Agent 能够准确描述自身 CLI 标志、热键和执行能力（#21432）  
   - **技能与子代理的主动调用**：即使不显式指令，Agent 也应自动使用自定义技能（#21968）

2. **安全与隐私增强**  
   - **Auto Memory 脱敏前置**：在内容送入模型前进行确定性脱敏（#26525）  
   - **工具确认截断锁定**：防止间接提示注入，要求用户展开完整内容（已通过 #27472 部分解决）  
   - **子代理权限控制**：用户报告 v0.33.0 后子代理在禁用状态下仍被调用（#22093）  
   - **路径遍历防护**：技能安装、链接等操作需要严格的路径校验（#27767）

3. **用户体验与稳定性**  
   - **Shell 命令执行可靠性**：解决命令完成后挂起、PTY 退出竞争条件等（#25166、#27502）  
   - **终端 resize 无闪烁**：迁移至 RenderStatic 并分批更新历史项（#21924）  
   - **工具数量限制优化**：当工具超过 API 上限（128/400）时应智能裁剪而非返回错误（#24246）  
   - **Auto Memory 重试机制**：低信号会话应被标记避免无限循环（#26522）

---

## 👥 开发者关注点

综合 Issue 评论和用户反馈，当前开发者使用 Gemini CLI 时主要遭遇以下痛点：

- **代理挂起**：通用代理在处理简单请求时无限等待（#21409），唯一缓解方式是指定不使用子代理，但牺牲了自动纠错能力。
- **子代理状态误报**：子代理达到最大轮次后仍报告“成功”，导致用户误以为任务完成（#22323），影响信任度。
- **Shell 命令卡住**：命令已执行完毕但终端界面显示“等待输入”，需要手动中断（#25166），日常开发中频繁出现。
- **浏览器代理 Wayland 兼容性**：部分 Linux 桌面环境下浏览器子代理完全无法工作（#21983）。
- **模型思考超长**：屏幕显示“Thinking…”后无响应，用户无法判断是否正常运行（#27785）。
- **工具数量爆炸**：启用大量技能/MCP 工具后遇到 400 错误，且 Agent 不会自动缩小工具范围（#24246）。
- **Auto Memory 无限重试**：低信号会话无法被自动标记已处理，导致背景提取任务反复重试（#26522）。
- **配置覆盖失效**：`settings.json` 中的 `maxTurns` 等配置对浏览器子代理不生效（#22267）。

以上痛点说明开发者对 Agent 的可控性、可靠性和安全性有着极高的要求，Gemini CLI 团队正在通过近期

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-06-11

**数据来源**: [github/copilot-cli](https://github.com/github/copilot-cli) | 生成时间: 2026-06-11

---

## 今日速览

过去 24 小时内，Copilot CLI 仓库无新版本发布，但多个历史问题持续引发讨论。**模型可用性不一致**（CLI 缺少 Gemini 系列、GPT-5.5 子 Agent 挂起）与 **MCP 策略误判**（组织策略明明允许，却被 CLi 错误拦截）仍是两大核心痛点。此外，**终端渲染退化**（流式输出字符错乱）、**复制粘贴功能在 Linux/Windows 上失效** 等回归问题受到高频关注。

---

## 社区热点 Issues（10 条）

1. **[#53 – Bring back the GitHub Copilot in the CLI commands to not break workflows](https://github.com/github/copilot-cli/issues/53)**  
   🔥 评论 34 · 👍 75 · 开放  
   **为什么重要**: 社区长期最受关注的问题。GitHub 官方近半年未回应，社区已涌现 `shell-ai` 等第三方替代方案。反映了核心 CLI 命令稳定性缺失。

2. **[#1703 – Copilot CLI does not list all org-enabled models (e.g. Gemini 3.1 Pro) while VS Code Copilot does](https://github.com/github/copilot-cli/issues/1703)**  
   🔥 评论 31 · 👍 54 · 已关闭  
   **为什么重要**: 模型列表在不同 Copilot 客户端（CLI vs VS Code）间严重不一致，企业用户无法使用已启用模型，影响组织级部署。

3. **[#223 – "Copilot Requests" permission for fine-grained tokens should be visible for org-owned tokens](https://github.com/github/copilot-cli/issues/223)**  
   🔥 评论 29 · 👍 76 · 开放  
   **为什么重要**: 企业组织无法使用细粒度 Token 的“Copilot Requests”权限，导致自动化流程无法身份验证，是企业管理员的长期痛点。

4. **[#2082 – ctrl+shift+c no longer copies to clipboard on Linux](https://github.com/github/copilot-cli/issues/2082)**  
   🔥 评论 21 · 👍 8 · 开放  
   **为什么重要**: Linux 用户常用的复制快捷键失效，影响日常终端交互。社区期待回退或提供恢复方法。

5. **[#2334 – Please bring back no-alt-screen](https://github.com/github/copilot-cli/issues/2334)**  
   🔥 评论 7 · 👍 28 · 已关闭  
   **为什么重要**: `alt-screen` 模式导致无滚动条、无法查找历史，用户强烈要求恢复 `no-alt-screen` 选项。社区情绪激烈。

6. **[#2434 – Restore support for Gemini Pro](https://github.com/github/copilot-cli/issues/2434)**  
   🔥 评论 7 · 👍 10 · 已关闭  
   **为什么重要**: v1.0.14 意外移除 `gemini-3-pro-preview` 模型支持，社区认为这削弱了 CLI 的模型多样性优势。

7. **[#1707 – 3rd party MCP servers are disabled, despite no such policy](https://github.com/github/copilot-cli/issues/1707)**  
   🔥 评论 9 · 👍 0 · 已关闭  
   **为什么重要**: 组织策略明明允许，CLI 却错误拦截第三方 MCP 服务器。已有 follow-up [#3756](https://github.com/github/copilot-cli/issues/3756) 在 2026-06-11 重新报告。

8. **[#3596 – Error loading model list: Error: Not authenticated](https://github.com/github/copilot-cli/issues/3596)**  
   🔥 评论 5 · 👍 10 · 开放  
   **为什么重要**: 会话恢复后认证突然失效，导致无法切换模型。影响长时间会话的用户。

9. **[#3727 – Regression: userPromptSubmitted hook additionalContext no longer injected](https://github.com/github/copilot-cli/issues/3727)**  
   🔥 评论 3 · 👍 0 · 开放  
   **为什么重要**: v1.0.60 引入回归，插件钩子 `additionalContext` 失效。对依赖插件的开发工作流产生阻断。

10. **[#3749 – Terminal streaming renderer corrupts output – characters doubled/truncated](https://github.com/github/copilot-cli/issues/3749)**  
    🔥 评论 2 · 👍 2 · 开放  
    **为什么重要**: 流式渲染导致字符重复、截断，影响所有流式输出场景（思考过程、最终答案），是当前严重的终端 BUG。

---

## 重要 PR 进展

过去 24 小时无新 PR 更新。

---

## 功能需求趋势

从近期 Issues 中总结出社区最关注的 **五大功能方向**：

1. **模型支持扩展**  
   - 请求添加 Gemini 3.1 Pro、Gemini 3 Flash、GPT-5.5 等模型（[#1703](https://github.com/github/copilot-cli/issues/1703)、[#821](https://github.com/github/copilot-cli/issues/821)、[#3547](https://github.com/github/copilot-cli/issues/3547)）  
   - 期望 CLI 模型列表与 VS Code 完全对齐。

2. **MCP 策略透明与可控性**  
   - 要求修复组织策略误判（第三方 MCP 被错误禁用）([#1707](https://github.com/github/copilot-cli/issues/1707)、[#3756](https://github.com/github/copilot-cli/issues/3756)）  
   - 希望支持自定义 MCP 服务器权限覆盖（`/mcp enable` 永久生效）。

3. **终端体验优化**  
   - 恢复 `no-alt-screen` 选项（[#2334](https://github.com/github/copilot-cli/issues/2334)）  
   - 修复流式渲染乱码（[#3749](https://github.com/github/copilot-cli/issues/3749)）  
   - 改善 Linux/Windows 下的复制粘贴快捷键（[#2082](https://github.com/github/copilot-cli/issues/2082)、[#3622](https://github.com/github/copilot-cli/issues/3622)）。

4. **认证与权限简化**  
   - 企业级细粒度 Token 权限可见性（[#223](https://github.com/github/copilot-cli/issues/223)）  
   - 会话恢复时不丢失认证状态（[#3596](https://github.com/github/copilot-cli/issues/3596)）。

5. **Agent 与插件稳定性**  
   - 修复后台子 Agent 挂起（[#3547](https://github.com/github/copilot-cli/issues/3547)）  
   - 修复插件钩子回归（[#3727](https://github.com/github/copilot-cli/issues/3727)）  
   - 要求禁用工作树（Worktree）默认行为（[#2243](https://github.com/github/copilot-cli/issues/2243)）。

---

## 开发者关注点

- **模型可用性断层**：多个用户报告 CLI 中缺少 Gemini 系列模型，而 VS Code 中可用，降低 CLI 作为独立 AI 工具的价值。  
- **MCP 策略误判**：组织明明未设置禁用策略，CLI 却拦截第三方 MCP，导致开发者不得不用降级版本或 hack 绕过（如 [#2486](https://github.com/github/copilot-cli/issues/2486)）。  
- **终端渲染退化**：v1.0.60 后流式输出出现字符错乱（[#3749](https://github.com/github/copilot-cli/issues/3749)、[#3755](https://github.com/github/copilot-cli/issues/3755)），严重影响可读性。  
- **复制粘贴功能退步**：Linux Ctrl+Shift+C 和 Windows 复制均失效，迫使依赖旧版本。  
- **会话恢复认证问题**：恢复会话时 `Not authenticated` 错误提示不清晰，且无法绕开。  
- **插件钩子回归**：`userPromptSubmitted` 钩子 `additionalContext` 不再注入，打破部分团队自动化流程。  
- **工作树自动创建**：CLI 自动创建大量 Git 工作树，导致混乱，用户强烈要求默认禁用（[#2243](https://github.com/github/copilot-cli/issues/2243)）。  

---

> **说明**：本日报基于 2026-06-11 09:00 UTC 前的仓库数据生成，PR 进展部分无更新。所有链接均可直接访问对应 Issue/PR 页面。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-06-11）

## 📌 今日速览
过去24小时内未发布新版本，但社区十分活跃：**3个新Issue**报告了YOLO模式与任务终止的Bug，**23个PR**被更新或合并，其中大量修复涉及Windows兼容性、会话恢复、MCP启动及历史回放等关键场景。开发者对`yolo`模式下仍需手动确认、任务最终项无法完成等问题的反馈最为集中。

---

## 🐞 社区热点 Issues（共3条，全部列出）

| Issue | 状态 | 摘要 | 重要性 |
|-------|------|------|--------|
| [#2448](https://github.com/MoonshotAI/kimi-cli/issues/2448) | OPEN | **[Bug] YOLO模式下仍提示批准** – 用户在v0.12.0 + k2.6模型（Debian）启用`yolo`模式后，工具调用仍需手动确认。 | 直接影响“无监督”自动化流程，与核心模式期望冲突。 |
| [#2447](https://github.com/MoonshotAI/kimi-cli/issues/2447) | OPEN | **[Bug] 最终待办项永不完成** – Agent使用待办清单时，最后一项任务始终卡住无法标记完成。 | 严重干扰任务流程，导致会话无法自然结束。 |
| [#2173](https://github.com/MoonshotAI/kimi-cli/issues/2173) | CLOSED | 标题仅感叹号，无摘要，已于5月关闭。 | 无实际参考价值。 |

---

## 🔧 重要 PR 进展（精选10条）

| PR | 状态 | 核心内容 | 链接 |
|----|------|---------|------|
| #2355 | ✅ 合并 | **修复：MCP延迟启动失败后继续交互** – 避免因单个MCP服务器启动失败而中止整个交互回合，增加回归测试。 | [查看](https://github.com/MoonshotAI/kimi-cli/pull/2355) |
| #2354 | ✅ 合并 | **Windows日志文件不共享** – 为每个进程使用独立日志文件（`kimi.<pid>.log`），防止多进程并发旋转同一文件。 | [查看](https://github.com/MoonshotAI/kimi-cli/pull/2354) |
| #2334 | ✅ 合并 | **清理代理的孤立UTF-16代理对** – 在发送请求前移除系统提示和消息中的非法代理码点，避免被Kimi后端拒绝。 | [查看](https://github.com/MoonshotAI/kimi-cli/pull/2334) |
| #2327 | ✅ 合并 | **超时时终止Shell进程树** – 为前台Shell命令创建独立进程组，超时或取消时整树终止，修复残留子进程。 | [查看](https://github.com/MoonshotAI/kimi-cli/pull/2327) |
| #2289 | ✅ 合并 | **避免Windows控制台字体重置** – 子进程创建时传递`CREATE_NO_WINDOW`标志，避免弹出额外的控制台窗口。 | [查看](https://github.com/MoonshotAI/kimi-cli/pull/2289) |
| #2239 | ✅ 合并 | **继续最新持久会话** – `--continue`现在会回退到工作目录中最新的非空会话，而非因元数据丢失而报错。 | [查看](https://github.com/MoonshotAI/kimi-cli/pull/2239) |
| #2217 | ✅ 合并 | **后台自动触发冷却后恢复** – 连续3次后台失败后暂停10分钟，冷却后重置计数器，避免永久静默。 | [查看](https://github.com/MoonshotAI/kimi-cli/pull/2217) |
| #2387 | 🔄 OPEN | **保留Shell命令头部详情** – 修复终端中“Used Shell (...)”标题被过度截断的问题，保留更多命令原文。 | [查看](https://github.com/MoonshotAI/kimi-cli/pull/2387) |
| #2383 | 🔄 OPEN | **修复历史回放时的孤立tool_calls** – 会话在中间被杀时，持久化的`context.jsonl`可能包含无tool_call的assistant消息，现在会正确删除这些孤儿。 | [查看](https://github.com/MoonshotAI/kimi-cli/pull/2383) |
| #2386 | 🔄 OPEN | **映射undo的wire索引到context索引** – `/undo`和fork之前错误地使用wire索引进行截断，导致斜杠命令（如`/compact`）后无法正确回退。 | [查看](https://github.com/MoonshotAI/kimi-cli/pull/2386) |

---

## 📊 功能需求趋势

从近期Issue与PR中可提炼出社区关注的核心方向：

1. **YOLO模式的可靠性** – 用户期望`yolo`模式真正无需人工介入，但目前仍有“批准”弹窗。
2. **会话持久化与恢复** – 包括历史回放中的孤儿消息处理、undo上下文映射、`--continue`回退逻辑等。
3. **Windows原生支持** – 日志独立、控制台窗口管理、子进程进程组、编码兼容（非UTF-8文件名）依然是高频修复点。
4. **MCP（Multi-Component Pipeline）稳定性** – 延迟启动失败后继续运行、后台自动触发冷却机制。
5. **Shell命令体验优化** – 命令头部展示、超时进程树终止、执行前清理代理对。
6. **Web/Workers模式同步** – AFK模式向Worker传播、Web侧归档会话打开。

---

## 👨‍💻 开发者关注点

- **YOLO模式行为不符预期**（#2448）：用户明确表示在`yolo`模式下仍遇到“approval”提示，开发者需要重新检查模式判断逻辑。
- **任务终止卡死**（#2447）：最终待办项无法完成，可能涉及工具调用返回格式或状态机边缘情况。
- **Windows子进程创建控制台窗口**（#2197 / #2289 / #2199）：多用户在Windows上报告弹出黑色命令窗口，已有的修复需验证是否覆盖所有执行路径。
- **日志文件共享问题**（#2354）：Windows上并发进程争写同一日志，已修复但需关注是否有遗留。
- **非UTF-8文件名崩溃**（#1893）：中文GBK编码导致`git ls-files`异常，虽然已合并，但仍是Windows用户的常见痛点。
- **历史回放中的非法tool_calls**（#2383）：会话中途退出后产生的脏数据导致后续请求被拒绝，该修复对长期会话的可用性至关重要。
- **undo/fork索引不匹配**（#2386）：使用`/compact`等内置命令后undo行为异常，社区期待已久。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

好的，这是为你生成的 2026-06-11 OpenCode 社区动态日报。

---

# OpenCode 社区动态日报 | 2026-06-11

## 今日速览

今日社区迎来 **v1.17.3** 紧急修复版本，解决了桌面版闪退的严重问题。社区讨论热度集中在**图片粘贴支持**、**长命令挂起**以及**模型兼容性**等议题上。此外，**TUI 2.0** 和 **v2 Session API** 的重大 PR 正在推进，预示着 UI 和架构层面的重要升级。

---

## 版本发布

### v1.17.3 （最新）
**修复了 v1.17.2 桌面版闪退的问题**。
- 这是一个针对 `v1.17.2` 崩溃问题的紧急热修复。
- [查看发布说明](github.com/anomalyco/opencode/releases/tag/v1.17.3)

### v1.17.2
**核心** 修复了当 `remote config` 认证过期时，系统会提示重新登录而非崩溃的问题；并允许子代理使用自身配置的权限。
**桌面端** 修复了 Linux 启动器和图标，确保已固定的应用能继续正常工作。
- [查看发布说明](github.com/anomalyco/opencode/releases/tag/v1.17.2)

### v1.17.1
**核心** 改进了引用功能，支持为代理添加用法描述，并可选择性地在 `@` 自动补全中隐藏。同时，弃用的 `reference` 配置项仍可被正确加载。
- [查看发布说明](github.com/anomalyco/opencode/releases/tag/v1.17.1)

### v1.17.0
**核心** 引入了 `fff` 后端搜索工具，提升了大型项目中的文件搜索速度；添加了 `X-Session-Id` 头用于代理粘性路由；新增对 Cohere North 模型的支持。
- [查看发布说明](github.com/anomalyco/opencode/releases/tag/v1.17.0)

---

## 社区热点 Issues

1.  **#906：功能请求：支持粘贴图片**
    - **摘要**: 用户希望在聊天中直接粘贴（`Ctrl+V`）图片，以替代目前仅支持的拖拽方式，方便将 Excalidraw 等工具的截图直接引入。
    - **社区反应**: **36 条评论，22 个赞**，这是社区最受关注的功能需求之一，表明用户在视觉交互方面有强烈需求。
    - [查看 Issue](anomalyco/opencode/issues/906)

2.  **#450：支持在 UI 中配置 reasoning_effort 参数**
    - **摘要**: 建议为支持该参数的模型（如 OpenAI、Gemini、DeepSeek）在 UI 中提供一个可调节的推理努力程度旋钮。
    - **社区反应**: **12 条评论，26 个赞**，说明高级用户对深度控制 LLM 行为有明确诉求。
    - [查看 Issue](anomalyco/opencode/issues/450)

3.  **#25038：长命令（如 Gradle 构建）在成功后仍然卡住**
    - **摘要**: 执行 Gradle 等长命令时，即使终端显示 `BUILD SUCCESSFUL`，OpenCode 的进程仍然会挂起。
    - **社区反应**: **11 条评论**，这是一个影响开发流程的严重 Bug，尤其对 Java/Android 开发者造成困扰。
    - [查看 Issue](anomalyco/opencode/issues/25038)

4.  **#6330：功能请求：通用 UI 意图通道**
    - **摘要**: 提议在服务端-客户端协议中加入通用 “UI 意图” 事件类型，允许服务器和插件驱动更复杂的交互 UX。
    - **社区反应**: **17 条评论，8 个赞**，这是一个架构层面的提议，若实现将极大增强插件的 UI 能力。
    - [查看 Issue](anomalyco/opencode/issues/6330)

5.  **#18016：无法删除 Zen 账户**
    - **摘要**: 用户反馈无法在 Zen 平台删除账户，导致持续扣费问题，且客服联系无果。
    - **社区反应**: **4 条评论**，但这是关乎用户数据和资金安全的严重缺陷，已引起社区警觉。
    - [查看 Issue](anomalyco/opencode/issues/18016)

6.  **#24610：功能请求：DeepSeek-V4 需要“禁用思考”按钮**
    - **摘要**: 因 DeepSeek API 默认开启思考模式，用户需要一个按钮来关闭它，尤其是在执行翻译等不需要深度思考的任务时。
    - **社区反应**: **4 条评论，5 个赞**，与 #450 类似，体现了用户对模型行为精细控制的需求。
    - [查看 Issue](anomalyco/opencode/issues/24610)

7.  **#30086：新版 OpenCode 高 CPU 占用**
    - **摘要**: 用户反映新版 OpenCode 的 CPU 使用率飙升，导致系统卡顿，影响了多任务处理能力。
    - **社区反应**: **9 条评论**，性能退化是开发者最敏感的问题之一，需要开发团队重点关注。
    - [查看 Issue](anomalyco/opencode/issues/30086)

8.  **#28312：TUI 权限对话框状态过期**
    - **摘要**: 在 TUI 界面中，按回车确认权限时可能无响应，因为对话框状态已过期，但用户仍被卡住。
    - **社区反应**: **3 条评论**，这暴露了 TUI 状态管理中的一个竞态条件问题。
    - [查看 Issue](anomalyco/opencode/issues/28312)

9.  **#6490：Web UI 无法选择用户目录外的文件夹**
    - **摘要**: 在 Windows 上运行 Web UI 时，无法通过文件浏览器进入 D 盘等非用户目录，只能看到默认的下载、联系人等文件夹。
    - **社区反应**: **10 条评论，12 个赞**，对于非 C 盘开发项目的用户来说是个巨大的障碍。
    - [查看 Issue](anomalyco/opencode/issues/6490)

10. **#31824：MCP OAuth 在 Windows 上因 IP 版本冲突失败**
    - **摘要**: 在 Windows 上执行 MCP OAuth 认证时，本地回调服务器监听在 IPv6，而重定向 URI 使用了 IPv4（`127.0.0.1`），导致认证失败。
    - **社区反应**: **1 条评论**，这是一个新提交的、具体的跨平台 Bug，对 Windows 用户影响直接。
    - [查看 Issue](anomalyco/opencode/issues/31824)

---

## 重要 PR 进展

1.  **#31796：TUI 2.0**
    - **摘要**: 这是一个重大更新，预示着 TUI 界面将迎来新的版本。
    - [查看 PR](anomalyco/opencode/pull/31796)

2.  **#31822：增加 v2 Session API 端点**
    - **摘要**: 新版本 API 端点引入了位置解析、Session 创建与获取、Session 域待办问题列表等功能，是架构演进的重要一步。
    - [查看 PR](anomalyco/opencode/pull/31822)

3.  **#31798：修复快照：重复利用 Git 对象以加速大型仓库**
    - **摘要**: 修复了在 Chromium 级大型仓库中，由于 `git add --all` 导致首次快照过程长时间卡住的问题。
    - [查看 PR](anomalyco/opencode/pull/31798)

4.  **#29217：TUI 新增内联技能调用**
    - **摘要**: 在提示词输入框中支持输入 `$skill` 来调用技能，并具备自动补全和粘贴文本支持，提升了 TUI 的交互效率。
    - [查看 PR](anomalyco/opencode/pull/29217)

5.  **#31799：修复使用错误时的提示信息**
    - **摘要**: 当用户输错命令时，系统会显示具体的错误信息，而不是仅仅打印帮助文档，提高了用户体验。
    - [查看 PR](anomalyco/opencode/pull/31799)

6.  **#31745：显示内容过滤错误**
    - **摘要**: 当 LLM 因内容过滤（如 Anthropic 的 `stop_reason: refusal`）而终止响应时，系统将向用户展示明确的错误信息而非静默失败。
    - [查看 PR](anomalyco/opencode/pull/31745)

7.  **#31802：修复 MCP 认证和调试时 Header 丢失问题**
    - **摘要**: 确保在 MCP 的 OAuth 认证和 `mcp debug` 过程中，用户配置的 Headers 能够被正确传，解决了认证和调试的痛点。
    - [查看 PR](anomalyco/opencode/pull/31802)

8.  **#31329：优雅处理 PDF/图片读取失败**
    - **摘要**: 当代理尝试读取损坏的 PDF 或图片文件时，不再导致整个 Session 崩溃，而是进行优雅的错误处理。
    - [查看 PR](anomalyco/opencode/pull/31329)

9.  **#13610：桌面端新增快捷键切换项目**
    - **摘要**: 为桌面版增加了 `Cmd+1-9` 快捷键，用于在侧边栏项目之间快速切换。
    - [查看 PR](anomalyco/opencode/pull/13610)

10. **#31805：修复 TUI 退出时未打印结尾信息**
    - **摘要**: 修复了一个 Bug，即在作用域清理过程中，会话的结尾摘要（epilogue）会被错误清除，导致用户看不到最后的总结。
    - [查看 PR](anomalyco/opencode/pull/31805)

---

## 功能需求趋势

1.  **全面的图片支持**: 社区强烈要求不仅支持拖拽，更要支持**复制粘贴**图片（#906），并希望在 `question` 工具中也支持图片上传（#31791）。
2.  **模型行为精细控制**: 用户需要更细粒度的模型控制，例如在 UI 中提供 `reasoning_effort` 旋钮（#450），以及为 DeepSeek 等模型增加“禁用思考”的开关（#24610, #27555）。
3.  **跨客户端和插件集成**: 对更具扩展性的 UI 框架（#6330）和跨平台、跨客户端的自动化工作流（如 GitHub Actions 评论编辑 #30468, 微信桥接 #31820）表现出兴趣。
4.  **持久化和账户管理**: 用户对账户数据安全（#18016）和会话配置持久化（如 TUI 权限状态 #28312）提出了更高要求。
5.  **性能与稳定性**: 来自 IDE 化编辑工具的用户对**长命令挂起**（#25038）、**高 CPU 占用**（#30086）和**大型仓库支持**（#31798）等性能问题高度敏感。

---

## 开发者关注点

1.  **桌面端稳定性**: `v1.17.3` 的紧急发布以及 #31481 提到的桌面端启动崩溃，表明桌面版的稳定性仍是首要关注点。
2.  **权限与安全交互**: TUI 权限系统存在状态同步问题（#28312）；同时，V1 Shell 工具缺少对破坏性命令（如 `rm -rf /`）的保护（#31774），存在安全隐患。
3.  **本地化与跨平台兼容性**: Windows 用户在文件系统访问（#6490）和 OAuth 认证（#31824）方面遇到特殊问题，凸显了跨平台兼容性仍需打磨。
4.  **代理与子任务管理**: 复杂任务（如后台子代理 #31789）的管理和调试存在不足，容易产生无限循环或资源浪费。
5.  **慢速本地模型支持**: 桌面端在面对慢速本地推理时，存在固定的 5 分钟 Headers 超时限制（#26602），影响了本地模型的使用体验。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 | 2026-06-11

## 今日速览

Pi 项目今天迎来大量 bug 修复和新功能 PR 合入，社区讨论焦点集中在 **信任门控** 用户体验不佳、流处理超时与缓存计费错误等问题。PR 方面新增了 Palantir Foundry 代理、Amazon Bedrock Mantle 等新 provider 支持，同时 TUI 稳定性（CJK 文本、覆盖层合成、Markdown 渲染）得到明显改善。开发者需注意扩展系统与 Bun 的兼容性问题，以及多个 TUI 崩溃报告。

## 社区热点 Issues

### 1. [#5514 Project Trust Feature Feedback](https://github.com/earendil-works/pi/issues/5514)
- **评论: 25 | 👍: 13 | 已关闭**
- **摘要**：用户对刚上线的“信任门控”功能极度不满，认为每次打开项目/文件夹都需要确认信任非常烦人，且无法全局关闭。社区讨论热烈，要求提供可配置选项或移除该功能。

### 2. [#3715 `local-llm` streams terminate at 5 min](https://github.com/earendil-works/pi/issues/3715)
- **评论: 10 | 👍: 4 | 已关闭**
- **摘要**：使用本地 OpenAI 兼容后端（如 vLLM）时，Write 工具调用超过 5 分钟会因 undici 默认 `bodyTimeout` 而中断，且用户设置的 `retry.provider.timeoutMs` 无法覆盖该限制。影响长时间推理场景。

### 3. [#4160 pi extensions does not play nice with Bun](https://github.com/earendil-works/pi/issues/4160)
- **评论: 9 | 👍: 0 | 已关闭**
- **摘要**：在只安装 Bun 而无 Node/npm 的环境中，通过 `pi install` 安装扩展会因找不到 `npm` 而失败。Pi 自身生成的修复方案也不理想，暴露了扩展系统对运行时依赖的硬编码。

### 4. [#3372 pi can no longer work with Claude subscription](https://github.com/earendil-works/pi/issues/3372)
- **评论: 7 | 👍: 0 | 已关闭**
- **摘要**：用户反馈使用 Claude 订阅后 Pi 无法正常通信，怀疑是认证流或端点变更导致。曾一度影响付费用户使用。

### 5. [#5291 Sessions hang on "working" with Anthropic subscription](https://github.com/earendil-works/pi/issues/5291)
- **评论: 5 | 👍: 1 | 已关闭**
- **摘要**：使用 Anthropic Enterprise 订阅时，会话随机卡在“Working...”状态，中断/恢复操作有时无效。严重影响日常开发连贯性。

### 6. [#5611 GitLab Duo Anthropic streams hit ~90s cutoff](https://github.com/earendil-works/pi/issues/5611)
- **评论: 3 | 👍: 0 | 已关闭**
- **摘要**：GitLab Duo 通过 Anthropic 流式传输时，在 `message_stop` 之前约 90 秒就被关闭，导致 Pi 误判为重试条件，反复重发相同请求。导致重复输出和费用增加。

### 7. [#5536 Split-turn compaction sends parallel summarization requests causing 429](https://github.com/earendil-works/pi/issues/5536)
- **评论: 2 | 👍: 0 | 开放中**
- **摘要**：自动压缩选择 split-turn 策略时，会并发发送历史摘要和 turn-prefix 摘要请求，对单槽的本地后端（如 llama.cpp）造成 429 限流。目前尚无解决方案。

### 8. [#5605 MiniMax-M3: cache_control ignored on Anthropic endpoint](https://github.com/earendil-works/pi/issues/5605)
- **评论: 2 | 👍: 0 | 已关闭**
- **摘要**：MiniMax-M3 通过 Anthropic 兼容端点路由时，`cache_control` 被忽略导致 `cacheRead` 始终为 0，用户以全价 $0.60/Mtok 计费而非缓存价 $0.12/Mtok。同时通过 openai-completions 使用时 thinking 功能损坏。

### 9. [#5575 kimi-k2.6 via OpenCode Go fails with JSON Schema conflict](https://github.com/earendil-works/pi/issues/5575)
- **评论: 2 | 👍: 0 | 已关闭**
- **摘要**：通过 OpenCode Go 使用 Kimi K2.6 时，Pi 发送的工具定义与模型预期的 JSON Schema 冲突，导致 400 Bad Request。影响新兴模型兼容性。

### 10. [#5612 Switching models mid-session (DeepSeek V4 → Kimi K2.6) causes Connection error](https://github.com/earendil-works/pi/issues/5612)
- **评论: 1 | 👍: 0 | 开放中**
- **摘要**：在长会话中从 DeepSeek V4 Flash 切换到 Kimi K2.6 后，出现频繁连接错误且模型只输出单句不再调用工具。问题复现稳定，但 OpenCode 本身工作正常，疑似 Pi 内部状态混乱。

## 重要 PR 进展

### 1. [#5609 feat(providers): add Pal

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# 2026-06-11 Qwen Code 社区动态日报

## 今日速览

- **核心功能改进持续推进**：`daemon_mode` 批量合并 PR #4490 进入主分支，标志着守护进程模式进入 alpha 阶段；同时社区对 VP 模式滚动冲突、终端 resize 碎片化等 UI 缺陷反馈集中。
- **子代理与团队协作机制优化**：多个 PR 修复了队友身份保持、任务串行化以及权限提示冒泡等关键问题，为多智能体协作场景奠定基础。
- **开发者对统计持久化、MCP 安全策略和自动 memory 控制的呼声升高**，三项 feature request 均获得较多讨论，反映出社区对数据归因和可控性的重视。

## 社区热点 Issues（10 条）

1. **#4942 – VP 模式下 Composer 与滚动输入冲突**  
   [🔗](https://github.com/QwenLM/qwen-code/issues/4942)  
   **类别**：bug/UI  
   **重要性**：核心交互流程受阻塞，用户无法在 AI 回复后滚动历史记录。社区评论 4 条，已有 welcome-pr 标签，预计将尽快修复。

2. **#4597 – 增强 `/stats` 命令支持跨会话持久化用量统计**  
   [🔗](https://github.com/QwenLM/qwen-code/issues/4597)  
   **类别**：feature-request/telemetry  
   **重要性**：对标 Claude Code，社区广泛认为当前仅内存统计不可追溯。获得 4 条讨论与 1 个 👍，已在 roadmap 中标注 terminal-ux 和 export-data。

3. **#4876 – Subagent 读取图片文件返回非预期内容**  
   [🔗](https://github.com/QwenLM/qwen-code/issues/4876)  
   **类别**：bug/tools  
   **重要性**：主 agent 读取正常而 subagent 失败，暴露出子代理工具调用链路可能缺失图片预处理。已 closed，但值得关注修复方案。

4. **#4374 – 添加配置禁用自动 memory recall**  
   [🔗](https://github.com/QwenLM/qwen-code/issues/4374)  
   **类别**：feature-request/performance  
   **重要性**：用户反馈自动 memory recall 在高频对话中造成性能浪费，希望保持 extract/dream 功能的同时禁用 recall。3 条评论，期待配置项落地。

5. **#4877 – OpenWork 无法区分不同提供商下的同名模型**  
   [🔗](https://github.com/QwenLM/qwen-code/issues/4877)  
   **类别**：bug/UI  
   **重要性**：多模型提供商场景下，同一模型 ID 被不同源注册时 UI 无法区分，影响模型选择准确性。3 条讨论，涉及核心配置显示。

6. **#4882 – 为 Hook 添加 `terminalSequence` 字段**  
   [🔗](https://github.com/QwenLM/qwen-code/issues/4882)  
   **类别**：feature-request/CLI  
   **重要性**：借鉴 Claude Code 新特性，允许 Hook 触发桌面通知、标题更新等终端侧效果。3 条评论，已标记 roadmap/hooks-events。

7. **#4891 – 终端 resize 导致流式输出碎片化**  
   [🔗](https://github.com/QwenLM/qwen-code/issues/4891)  
   **类别**：bug/UI  
   **重要性**：高优先级（P2），在 macOS 下重现，回滚后内容呈现错位宽度。3 条讨论，welcome-pr 表明社区贡献者可以介入。

8. **#4864 – CI 缺少主分支保护状态检查**  
   [🔗](https://github.com/QwenLM/qwen-code/issues/4864)  
   **类别**：enhancement/CI  
   **重要性**：因未启用必选状态检查，PR #4798 合入时 CI 全红却未阻止，导致主分支引入 TypeScript 语法错误。已 closed，促成了防护策略改进。

9. **#4976 – 自动生成的 memory 干扰正常 CLI 调用**  
   [🔗](https://github.com/QwenLM/qwen-code/issues/4976)  
   **类别**：bug/tools  
   **重要性**：用户反馈自动 memory 在批量读取文档时插入无关上下文，浪费大量轮次。2 条评论，welcome-pr 标签，属于用户体验痛点。

10. **#4974 – SGR 鼠标滚轮序列泄漏为输入文本**  
    [🔗](https://github.com/QwenLM/qwen-code/issues/4974)  
    **类别**：bug/CLI  
    **重要性**：鼠标跟踪开启后，滚轮事件被 `KeypressContext` 双重消费，导致原始字节 `64;50;15M` 显示在输入框中。影响所有使用 SGR 模式的终端用户。

## 重要 PR 进展（10 条）

1. **#4598 – 可折叠思考块 + 耗时计时器（TUI）**  
   [🔗](https://github.com/QwenLM/qwen-code/pull/4598)  
   **状态**：OPEN  
   **概述**：将单行思考预览替换为可折叠历史块，流式推理展示在回答上方，完成后自动折叠并显示耗时。大幅提升推理过程可视化体验。

2. **#4979 – 修复审批后队友身份保持问题**  
   [🔗](https://github.com/QwenLM/qwen-code/pull/4979)  
   **状态**：OPEN（今日合建）  
   **概述**：默认审批模式下，队友发送的消息经审批后应正确归属给队友而非 leader。修复团队协作中的消息归属错乱。

3. **#4905 – 增加 Rewind 选择器降级状态测试**  
   [🔗](https://github.com/QwenLM/qwen-code/pull/4905)  
   **状态**：CLOSED  
   **概述**：为 RewindSelector 回退场景添加回归测试，覆盖文件恢复不可用、diff 统计数据加载失败等边界情况。

4. **#4981 – 串行化团队任务领取与邮箱锁一致性**  
   [🔗](https://github.com/QwenLM/qwen-code/pull/4981)  
   **状态**：OPEN（今日合建）  
   **概述**：防止同一 agent 在并发自动认领中被分配多个任务，同时将任务存储文件锁定与 team mailbox 机制对齐，提升并发稳定性。

5. **#4490 – 守护进程模式批量合并到主分支**  
   [🔗](https://github.com/QwenLM/qwen-code/pull/4490)  
   **状态**：OPEN（周期性合并）  
   **概述**：合并 `daemon_mode_b_main` 分支，包含 46 个提交、386 个文件变更（+115k / -12k LOC），覆盖守护进程核心功能集，标志 v0.16-alpha 的里程碑。

6. **#4952 – 修复 Web-Shell/WebUI 的 SSE 重连与错误路由**  
   [🔗](https://github.com/QwenLM/qwen-code/pull/4952)  
   **状态**：CLOSED  
   **概述**：实现 SSE delta 恢复，重连时发送 `Last-Event-ID` 避免重复数据；修复错误处理与 Toast API 渲染稳定性。

7. **#4954 – 在守护进程模式下隔离每个会话的统计**  
   [🔗](https://github.com/QwenLM/qwen-code/pull/4954)  
   **状态**：OPEN  
   **概述**：修复 `GET /session/:id/stats` 返回进程级累计数据的问题，引入 `Map<sessionId, SessionMetrics>` 双写模式，实现会话级 API/工具调用统计。

8. **#4894 – 修复 FIFO 启动阻塞（无读者时）**  
   [🔗](https://github.com/QwenLM/qwen-code/pull/4894)  
   **状态**：OPEN  
   **概述**：当 `--json-file` 指向 FIFO 且无读者时，改用 `O_RDWR | O_NONBLOCK` 非阻塞打开，避免启动卡死；增加 1MB 缓冲区高水位标记。

9. **#4856 – 为 Web-Shell 添加任务认证与目标工作流**  
   [🔗](https://github.com/QwenLM/qwen-code/pull/4856)  
   **状态**：OPEN  
   **概述**：扩展 Web-Shell 支持守护进程驱动的任务/认证/目标面板，提供结构化任务状态渲染以及新的 daemon/session API 消费。

10. **#4971 – 减少交互式 CLI 中工具输出内存占用**  
    [🔗](https://github.com/QwenLM/qwen-code/pull/4971)  
    **状态**：OPEN（今日合建）  
    **概述**：对大工具输出在存储到调度器状态、实时 UI 历史、聊天录制元数据和子代理摘要时进行压缩，降低终端资源消耗。

## 功能需求趋势

从近期 Issues 中可以观察到社区最关注的四个方向：

- **统计与数据持久化**：`/stats` 命令的跨会话持久化（#4597）、会话级 API 调用统计（#4954）以及 token 数据准确性验证（#4951）是持续热点，用户希望得到与 Claude Code 同等级的可追溯性。

- **子代理与团队协作能力**：子代理权限冒泡（#4928）、默认启用 fork subagent（#4956）、任务串行化（#4981）以及队友身份保持（#4979）表明多智能体协作架构正在快速成型，社区期待更高的自动化和可靠性。

- **MCP 安全与配置策略**：新增 `deniedMcpServers` 黑名单策略（#4940）、SchemaValidator 缺少数字字符串转换（#4966）反映出开发者对 MCP 工具调用安全的重视，以及需要更灵活的 allow/deny 机制。

- **终端 UI 与交互体验**：VP 模式滚动冲突（#4942）、终端 resize 碎片化（#4891）、可折叠思考块（#4598）、可选时间戳（#4899）以及 git 分支在桌面端的突出显示（#4769）等需求，说明社区对界面沉浸感和信息的可读性有更高要求。

## 开发者关注点

- **VP（Virtualized History）模式的兼容性**：多个 Issue（#4942、#4974、#4921）指向 VP 模式下终端滚动、鼠标事件和视口高度异常，是当前反馈最密集的痛点。
- **自动 memory 的不可控性**：用户抱怨自动生成的 memory 干扰正常工具调用流程（#4976），希望获得更精细的控制（#4374）。
- **模型切换与提供商管理**：无法区分同名模型（#4877）及绑定模型的版本限制（#4904）阻碍了多后端实验。
- **性能与内存泄漏**：`MaxListenersExceededWarning` 多出现于长会话（#4423），hook continuations 跳过了微压缩（#4838），以及终端 resize 导致的渲染碎片化（#4891）均影响长期使用稳定性。
- **工具调用规范性问题**：LLM 经常将数字参数作为字符串传递给 MCP 工具（#4966），下游严格校验时失败；同时 grep 等命令不能满足“读前编辑”检查（#4939），限制了编辑流程的自动推理。

以上日报基于 GitHub 公开数据自动整理，供技术社区快速掌握 Qwen Code 项目动态。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

好的，这是 2026 年 6 月 11 日的 DeepSeek TUI（CodeWhale）社区动态日报。

---

# CodeWhale 社区日报 | 2026-06-11

## 今日速览

1.  **品牌重塑进入深水区**：`v0.8.57` 发布，彻底废弃 `deepseek-tui` npm 包名，所有官方资产统一为 `CodeWhale`。社区大量 Issues 和 PR 围绕路径、文档、提示中的旧名称清理展开。
2.  **多模型与 Provider 中立化加速**：`v0.8.58` 分支异常活跃，大量 PR 正致力于解除对 DeepSeek 模型的硬编码，目标是在子代理、自动路由器、能力报告中支持任意 Provider 的模型 ID。
3.  **Agent 稳定性与体验仍是核心痛点**：Windows 下的 SSE 超时、子代理在多种场景下的失败、低信息密度 UI 以及缺乏自动故障转移机制，是社区最集中反馈的问题。

## 版本发布

- **v0.8.57**: **品牌重塑收尾版本。** 旧的 `deepseek-tui` npm 包已废弃，不再接收更新。所有新发布均以 `codewhale` 为官方名称。建议所有仍在使用旧名称的用户按照 `docs/REBRAND.md` 文档进行迁移。
- **v0.8.56**: **社区丰收版。** 集成了社区贡献的**国际化支持**、**更多 AI 服务商（Provider）接入**、**前缀缓存稳定性修复**以及其他杂项修复。

## 社区热点 Issues

1.  **[#3031] v0.8.58: 默认折叠工具调用日志** (@Hmbown)
    **重要性**: 显著提升终端用户交互体验。当前日志中充斥着“无输出”、毫秒级计时等低价值信息，该 Issue 提议默认折叠这些信息，仅在需要时展开。
    **链接**: [Issue #3031](https://github.com/Hmbown/CodeWhale/issues/3031)

2.  **[#2369] CodeWhale 配置路径在各类 OS 和 Cygwin 中碎片化** (@buko)
    **重要性**: 品牌重塑后，配置文件路径仍存在旧名称和跨平台不一致问题，影响用户迁移和日常使用。属于基础体验问题。
    **链接**: [Issue #2369](https://github.com/Hmbown/CodeWhale/issues/2369)

3.  **[#1679] Windows 11 下 SSE 多智能体并行超时 & UI 错乱** (@xaviertung)
    **重要性**: 持续存在的 Windows 平台兼容性问题，严重限制了该平台下高级功能（多智能体）的使用。
    **链接**: [Issue #1679](https://github.com/Hmbown/CodeWhale/issues/1679)

4.  **[#1806] 子代理 120s API 超时使 agent_open 几乎不可用** (@qiyuanlicn)
    **重要性**: 核心功能的严重 Bug。用户报告在批量处理任务时，子代理因 API 超时全部失败，与宣传的并行处理能力不符。
    **链接**: [Issue #1806](https://github.com/Hmbown/CodeWhale/issues/1806)

5.  **[#2574] 功能请求：Provider 自动故障转移链** (@hsdbeebou)
    **重要性**: 一个非常实用的增强功能。用户希望在一个 Provider（如 DeepSeek）因配额、错误码不可用时，系统能自动切换到后备 Provider（如 OpenAI），避免手动干预。
    **链接**: [Issue #2574](https://github.com/Hmbown/CodeWhale/issues/2574)

6.  **[#1990] 远程工作台：评估美国优先的云服务路径** (@Hmbown)
    **重要性**: 项目维护者主导的架构讨论，旨在为全球用户（尤其是非中国内地用户）提供基于廉价 VPS 和 Telegram 控制的安全远程运行环境。
    **链接**: [Issue #1990](https://github.com/Hmbown/CodeWhale/issues/1990)

7.  **[#3004] api_key 应支持通过脚本动态获取** (@ndzuki)
    **重要性**: 安全性和密码管理优化。用户希望避免明文存储 API Key，支持通过外部脚本（如从密码管理器）获取，符合安全最佳实践。
    **链接**: [Issue #3004](https://github.com/Hmbown/CodeWhale/issues/3004)

8.  **[#2989] 使用 Ollama + qwen3-coder:30b 时，Agent 提前报告“完成”** (@and7ey)
    **重要性**: 暴露了非标准 Provider 下的兼容性问题。Agent 未完成任务便返回成功状态，严重误导用户。
    **链接**: [Issue #2989](https://github.com/Hmbown/CodeWhale/issues/2989)

9.  **[#2964] v0.8.56：发布 DigitalOcean + Telegram 远程工作台搭建文档** (@Hmbown)
    **重要性**: 继 #1990 讨论后的实际行动。提供了可复现的、15分钟内搭建远程工作台的方案。
    **链接**: [Issue #2964](https://github.com/Hmbown/CodeWhale/issues/2964)

10. **[#2934] 功能：侧边栏会话面板，支持自动恢复和浏览历史** (@cy2311)
    **重要性**: 社区贡献的全新 UI 功能。解决当前会话管理不直观、切换流程繁琐的问题。
    **链接**: [Issue #2934](https://github.com/Hmbown/CodeWhale/issues/2934)

## 重要 PR 进展

1.  **[#3034] v0.8.58: 宪法提示词重构、Codex 修复、侧边栏改进** (@Hmbown)
    **进展**: v0.8.58 主干分支，集成了宪法提示词 YAML 化、TUI 侧边栏模式选择、Agent 配置界面等多个重要改变。
    **链接**: [PR #3034](https://github.com/Hmbown/CodeWhale/pull/3034)

2.  **[#3037] TUI 修复：紧凑型工具调用日志渲染** (@Hmbown)
    **进展**: 修复了 Issue #3031 的核心部分，默认视图下折叠“(no output)”和亚秒级计时信息。
    **链接**: [PR #3037](https://github.com/Hmbown/CodeWhale/pull/3037)

3.  **[#3045] 修复子代理模型验证：解除对 DeepSeek 的硬编码** (@Hmbown)
    **进展**: 允许子代理角色使用非 DeepSeek 的模型 ID（如 Moonshot, Ollama），是实现 Provider 中立化的关键一步。
    **链接**: [PR #3045](https://github.com/Hmbown/CodeWhale/pull/3045)

4.  **[#3048] 功能：参数化模型特定信息（上下文窗口、价格、思考能力）** (@Hmbown)
    **进展**: 取代原来硬编码的“DeepSeek V4”系统提示，现在可以动态注入当前模型的实际能力。解决 Issue #3025。
    **链接**: [PR #3048](https://github.com/Hmbown/CodeWhale/pull/3048)

5.  **[#3049] 功能: Hooks v2 — JSON 决策合约、文件匹配器、项目级配置** (@Hmbown)
    **进展**: 大幅提升 Hook 系统的灵活性和确定性，提供更精细的模型无关的控制。允许 Hook 返回 JSON 来自定义审批行为。
    **链接**: [PR #3049](https://github.com/Hmbown/CodeWhale/pull/3049)

6.  **[#3046] 修复推理内容：添加 Moonshot/Kimi 支持** (@Hmbown)
    **进展**: 修复 Kimi 模型思考内容在流式输出时无法正确显示的问题。
    **链接**: [PR #3046](https://github.com/Hmbown/CodeWhale/pull/3046)

7.  **[#3038] TUI 修复：使 Ctrl+B 直接后台当前前台 Shell** (@Hmbown)
    **进展**: 简化用户交互，将两步菜单操作改为一步快捷键。
    **链接**: [PR #3038](https://github.com/Hmbown/CodeWhale/pull/3038)

8.  **[#3051] 功能：添加 /voice 语音输入命令** (@HUQIANTAO)
    **进展**: 社区贡献的语音输入支持，实现了一次性录音、AI 转写和插入对话的功能。
    **链接**: [PR #3051](https://github.com/Hmbown/CodeWhale/pull/3051)

9.  **[#3044] 功能：远程烟雾测试提升至 v0.8.57，添加 gh CLI、swapfile 等** (@Hmbown)
    **进展**: 为远程工作台（DigitalOcean Droplet）的自动化运行提供更完善的基础设施支持。
    **链接**: [PR #3044](https://github.com/Hmbown/CodeWhale/pull/3044)

10. **[#3052] 功能：实现 verbosity 设置，支持 normal 和 concise 模式** (@cyq1017)
    **进展**: 社区贡献的体验优化，允许用户在`exec`等非交互模式启用简洁输出，减少不必要的提示词。
    **链接**: [PR #3052](https://github.com/Hmbown/CodeWhale/pull/3052)

## 功能需求趋势

1.  **Provider 中立化与多模型支持**：这是当前最明确的技术方向。从子代理、自动路由、能力报告到系统提示词，都在努力摆脱对 DeepSeek 模型的硬编码依赖，以支持 Moonshot、Ollama、OpenAI 等更多 Provider。
2.  **TUI 交互体验升级**：社区对 UI 细节要求越来越高。包括**可点击/可检查的低信息量行**、**默认折叠的紧凑日志**、**侧边栏会话管理面板**、**OSC 8 超链接**等，旨在让终端交互更信息化和高效。
3.  **Agent 鲁棒性与可靠性**：对 Agent 在执行过程中因超时、网络错误、模型限制等导致的失败非常敏感。社区强烈需要**自动故障转移**、**可配置的重试/退避策略**以及更**稳定的并行执行**。
4.  **远程与无人值守工作流**：开发者正积极构建**基于廉价 VPS 的“远程工作台”**（DigitalOcean + Telegram），这暗示了 CodeWhale 可能被用作一个持久的、可远程控制的 AI 代理服务，而不仅仅是一个对话式 TUI。
5.  **安全与密钥管理**：对 API Key 等敏感信息的管理提出了更高要求，希望支持**从外部脚本动态获取**，而非明文存储。

## 开发者关注点

-   **命名迁移阵痛**：从 `deepseek-tui` 到 `codewhale` 的迁移过程存在多个“坑”，包括配置文件路径不统一、旧 npm 包已废弃但用户不知、`/config` 页面仍显示旧名称等。
-   **错误提示信息质量**：用户反馈某些错误信息不准确或缺乏指导性，例如 TUI 错误地指责用户传递了 `--provider` 标志，或者子代理失败时没有提供有效的恢复建议。
-   **Windows 平台兼容性**：SSE 超时和 UI 错乱问题在 Windows 11 上反复出现，影响了该平台用户的信任。
-   **标准 Provider（如 Ollama）的稳定性**：使用非 DeepSeek 模型（如 Qwen）时，Agent 行为不可预测（如提前结束），表明 CodeWhale 的核心 Agent 逻辑对模型能力变化敏感。
-   **执行控制与 CICD 特性**：对于脚本化和自动化使用场景，开发者迫切需要 `--allowed-tools`、`--max-turns` 等更丰富的 `exec` 命令参数，以确保在 CI 管道或无人值守循环中的安全可控。

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*