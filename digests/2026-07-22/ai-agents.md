# OpenClaw 生态日报 2026-07-22

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-07-22 01:56 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我根据您提供的 OpenClaw 项目数据，为您生成 2026-07-22 的项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-07-22

### 1. 今日速览

项目今日保持极高的社区活跃度，Issues 和 PR 更新均达 500 条，显示出庞大的用户基础和维护压力。然而，高活跃度背后存在显著积压：PR 合并率仅约 33%（164/500），Issue 关闭率仅 21%（105/500），维护团队响应能力面临挑战。同时，多个 P0/P1 级别的严重 Bug（如数据库损坏、401 认证失败）仍处于“待审查”或“有待复现”状态，项目稳定性风险较高。尽管如此，有数个针对关键问题的修复 PR 已经提交并进入审核流程，项目核心功能仍在正向迭代。

### 2. 版本发布

**无新版本发布。**

---

### 3. 项目进展

尽管合并率不高，但今日仍有数个关键 PR 被合并，推动了项目在安全、UI 和稳定性方面的进展。

- **`[agents] fix(agents): enforce Claude CLI cron tool policies`** (PR #112457)
    - **状态**：已合并。
    - **内容**：此 PR 增强了 Claude CLI 后端的运行沙箱，通过强制实施 `toolsAllow` 策略，隔离受限任务与用户/项目/插件等上下文，防止授权滥用。
    - **意义**：提升了子进程和第三方 CLI 集成的安全边界，是近期安全强化工作的重要一步。

- **`[gateway] fix(gateway): read control-UI descriptors from the pinned session-extension registry`** (PR #112471)
    - **状态**：已合并。
    - **内容**：修复了插件小部件在控制 UI 中首次交互后消失的问题。之前，插件 widget 的注册信息读取自错误的内存副本，导致丢失。此 PR 修复了这个问题。
    - **意义**：解决了影响插件生态和用户仪表盘体验的严重 UI Bug。

- **`[docs, cli, maintainer] Install ClawHub packages for new Claw agents`** (PR #102228)
    - **状态**：已关闭（合并）。
    - **内容**：实现了从 ClawHub 安装包到新创建 Agent 的完整链路，包括包解析、信任确认、安装和校验。
    - **意义**：标志着 Claw 包管理系统和插件生态的关键流程打通，是“Claw”功能集成的重大进展。

- **其他合并修复**：
    - `fix(agents): cap sessions_list tool limit before gateway dispatch` (PR #110739)
    - `fix(plugins): deep-clone registry elements in transaction snapshot` (PR #112461)
    - `fix(config): add compaction.enabled to agent defaults schema` (PR #112460)
    - `fix(session): gate contextTokens persistence on actual usage data` (PR #112462)
    - `fix(macos): prevent AppKit automatic termination in menu bar app` (PR #112463)
    - `refactor(line,mattermost): declare single-account config promotion keys` (PR #112474)
    - `fix(hooks): kill gog process tree on gmail-watcher shutdown` (PR #112452)
    - `fix(qa): run isolated Matrix evidence partitions in parallel` (PR #112465)

**项目推进总结**：修复了多个与插件注册、配置验证、会话状态显示和客户端稳定性相关的关键问题，确保了核心功能的正常运行。

---

### 4. 社区热点

本周最活跃的讨论集中在**安全性与数据完整性**两大痛点。`clawsweeper` 标签系统显示这些议题正在接受跨团队审查。

- **🔥 #10659 [Feature Request: Masked Secrets]** (评论: 15, 👍: 4)
    - **链接**: https://github.com/openclaw/openclaw/issues/10659
    - **背景**：该请求要求实现“蒙版密钥”系统，允许 Agent 使用 API 密钥但无法直接查看或泄露它们。这是防止提示注入盗取凭证的核心手段。
    - **分析**：获得 15 条评论，社区反响强烈。这表明用户对 Agent 工作流中的**安全风险**认知度极高，且对当前 `~/.openclaw/.env` 文件的明文存储方式存在普遍担忧。安全是当前社区最关注的核心议题之一。

- **🔥 #101290 [CLI startup preflight can corrupt the live state DB]** (评论: 13, 👍: 1)
    - **链接**: https://github.com/openclaw/openclaw/issues/101290
    - **背景**：报告了一个 P0 级别的回归 Bug，即 CLI 启动时的健康检查会损坏正在运行中的 SQLite 数据库。
    - **分析**：评论数高，反映了该问题的**严重性**和**普遍性**（macOS 单主机环境多次触发）。用户面临数据丢失风险，对项目稳定性产生质疑。

- **🔥 #86996 [Active Memory + Codex app-server path causes long response latency]** (评论: 11, 👍: 2)
    - **链接**: https://github.com/openclaw/openclaw/issues/86996
    - **背景**：报告在特定配置（Active Memory + Codex 模型）下，简单消息回复也会产生高延迟和超时。
    - **分析**：此问题关联了多个核心组件（Active Memory, Honcho, Codex），是性能瓶颈的代表。用户希望获得更流畅、响应更快的体验，这对 Agent 作为实时助手至关重要。

- **🔥 #85030 [MCP tools not injected into subagent sessions]** (评论: 11, 👍: 5)
    - **链接**: https://github.com/openclaw/openclaw/issues/85030
    - **背景**：报告了一个配置完全被忽略的 Bug，即 MCP 工具无法注入到 `sessions_spawn` 创建的**子代理**会话中。
    - **分析**：获得 5 个👍（最多之一），表明这是一个**高需求**且**严重阻碍工作流**的功能缺陷。用户期望构建多 Agent 协作系统（如 DMZ 隔离搜索），该 Bug 使得整个子代理生态的 MCP 工具集成完全失效。`clawsweeper:needs-product-decision` 标签暗示该问题的修复方向需要产品决策。

---

### 5. Bug 与稳定性

今日报告的 Bug 数量多且严重，涵盖数据损坏、认证失败、核心功能异常等多个方面。`P0` 和 `P1` 级问题依然占据主导，且大多仍未修复。

- **P0 (Critical)**
    - **#101290 [CLI startup preflight can corrupt the live state DB]**: 最严重的 Bug。SQLite 数据库损坏。已有备用 PR #108287 尝试修复，但仍在审核。强烈建议维护者优先处理。
        - **链接**: https://github.com/openclaw/openclaw/issues/101290

- **P1 (High)**
    - **#106779 [Issue with 2026.7.1]**: 最新版本与本地 `llama.cpp` provider 不兼容，导致 `400 Unable to generate parser` 错误。严重影响自托管用户。
        - **链接**: https://github.com/openclaw/openclaw/issues/106779
    - **#95612 [cli-backend agent runs against anthropic return 401 authentication_failed]**: Claude CLI 认证失败，且无法重现于原生 CLI。严重影响使用 Anthropic 后端的用户。
        - **链接**: https://github.com/openclaw/openclaw/issues/95612
    - **#88562 [models.json generator writes apiKey as plain string]**: 安全漏洞，`models.json` 文件会写入明文密钥。已有 PR 修复。
        - **链接**: https://github.com/openclaw/openclaw/issues/88562
    - **#90840 [Subagent run completion is delivered to chat user as raw worker output]**: 回归 Bug，子代理的输出直接发送给用户，而不是由父代理处理后再总结发送。
        - **链接**: https://github.com/openclaw/openclaw/issues/90840
    - **#95441 [github-copilot/gpt-5.5 still persists/replays thinkingSignature encrypted_content]**: 与 GitHub Copilot 模型的兼容性问题，残留的加密内容导致请求失败。
        - **链接**: https://github.com/openclaw/openclaw/issues/95441
    - **#111498 [Main agent blocked by persistent workspace-state migration]**: 回归 Bug，Agent 被持久的迁移状态阻塞，无法进行任何调用。
        - **链接**: https://github.com/openclaw/openclaw/issues/111498
    - **#108473 [cron tool schema breaks llama.cpp tool-calling]**: 回归 Bug，`cron` 工具的 schema 定义不规范（无锚点正则），导致本地模型出错。
        - **链接**: https://github.com/openclaw/openclaw/issues/108473
    - **#53408 [Write/exec tool parameters silently dropped after long conversations]**: 行为 Bug，长时间对话后，`write` 和 `exec` 工具参数被静默丢弃，导致操作失败。
        - **链接**: https://github.com/openclaw/openclaw/issues/53408

---

### 6. 功能请求与路线图信号

社区对**安全**和**可观测性**的需求尤为突出。同时，也有若干与路线图强相关的功能请求浮现。

- **高潜力路线图信号：安全强化**
    - `#10659 Masked Secrets`, `#7722 Filesystem Sandboxing`, `#12678 Capability-based permissions` 等议题共同构成了一个强烈的“安全护城河”路线图。用户不再满足于基础功能，而是要求一个**默认安全**的 Agent 平台。今天合并的 PR #112457 和待审核的 #105884 (`fix(vydra): apply request policy`) 表明项目已经在朝这个方向努力。`clawsweeper:needs-product-decision` 标签在这些议题上的频繁出现，暗示产品团队可能需要优先决策“安全”的优先级。

- **备受关注的开发者体验改进：**
    - `#14438 [Plugin hot-reload without container restart]` (👍: 4, 评论: 5)：插件开发者对漫长的开发循环感到痛苦。这直接关系到开发生态的健康度。

- **“Claw” 包管理系统推进**：
    - 尽管今日数据中无相关 Issue，但 PR #102228 (已合并) 完成了包安装的闭环。这是“Claw”生态系统的里程碑，预计未来将有更多围绕包管理、版本控制和依赖的 Issues/PRs 涌现。

---

### 7. 用户反馈摘要

从今日的 Issues 讨论中，可以提炼出以下几类核心用户反馈：

- **安全焦虑是普遍现象**：用户对 `~/.openclaw/.env` 的明文密钥存储感到不安，害怕被提示注入攻击窃取。`Masked Secrets` 功能呼声极高，是用户心中“Agent 安全”的基本要求。
- **稳定性是第一生产力**：用户频繁报告导致**数据丢失**（DB 损坏）、**完全不可用**（认证失败、版本不兼容）和**任务失败**（参数静默丢弃）的 Bug。用户期望一个“开箱即用”的稳定系统，而非频繁遭遇故障的“实验性”项目。
- **对多模态和本地模型的支持需求强烈**：如 #85030 (MCP子代理)、#108473 (llama.cpp 兼容性) 和 #106779 (版本不兼容) 所示，用户正积极构建复杂的多 Agent 系统和依赖本地模型的私有化部署方案。兼容性和可靠性是他们最大的痛点。
- **插件开发者体验有待提升**：来自 Issue #14438的请求表明，插件开发者在热重载方面存在显著痛点。漫长的编译-重启-测试循环拖慢了开发

---

## 横向生态对比

好的，作为 AI 智能体与个人 AI 助手领域开源项目的资深技术分析师，我根据您提供的 2026-07-22 各项目日报，为您生成一份横向对比分析报告。

---

### 跨项目横向对比分析报告 | 2026-07-22

#### 1. 生态全景

个人 AI 助手 / 自主智能体开源生态正处于“**功能爆发与稳定性巩固**”的并行阶段。一方面，以 **IronClaw** 发布候选版、**OpenClaw** 生态打通、**ZeroClaw** 密集推进新功能为代表，头部项目正在完成从原型到可用、可扩展平台的蜕变。另一方面，**数据损坏、安全漏洞、性能回归**等“成长的烦恼”几乎在所有活跃项目中同步出现，表明社区在追求功能上限的同时，对**安全性、数据持久性和系统可靠性**提出了严苛要求。生态已从“能否做到”全面转向“**能否做得安全、稳定、流畅**”。

#### 2. 各项目活跃度对比

| 项目 | Issues 更新数 | PR 更新数 | 今日版本发布 | 健康度评估 |
|:---|:---|:---|:---|:---|
| **OpenClaw** | 500 (高) | 500 (高) | 无 | ⚠️ **高活跃、高积压**：合并率约33%，关闭率21%，积压严重；多个P0/P1 Bug待修复，风险较高。 |
| **NanoBot** | 10 (中) | 33 (高) | 无 | ✅ **高产出、高效率**：PR合并率高(22/33)，Bug修复与安全加固密集，交付能力强。 |
| **Hermes Agent** | 50 (高) | 50 (高) | 无 | ⚠️ **高度并行**：PR和Issue数量均高，但待合并PR积压(46条)，需核心团队加速审查。 |
| **PicoClaw** | 8 (低) | 8 (低) | 无 | ✅ **稳定推进**：活跃度适中，有明确的修复和目标推进，社区讨论有深度。 |
| **NanoClaw** | 1 (低) | 12 (中) | 无 | ⚡ **贡献者热情高，审查瓶颈**：PR合并率低(3/12)，社区贡献多，但维护者响应需加强。 |
| **IronClaw** | 41 (高) | 50 (高) | **v1.0.0-rc.1** | 🔥 **密集冲刺**：发布候选版，进入架构重构（Reborn）最后阶段，大量XL尺寸PR活跃，健康度最高。 |
| **LobsterAI** | 1 (低) | 10 (中) | 无 | ✅ **迭代有序**：合并率高(5/10)，聚焦特定功能与用户体验优化，团队效率高。 |
| **Moltis** | 1 (低) | 1 (低) | 无 | 💤 **低活跃**：开发节奏放缓，社区讨论停留在旧有功能请求上，缺乏新进展。 |
| **CoPaw** | 21 (高) | 30 (高) | **v2.0.1-beta.1** | ✅ **高产出、高闭合**：Issues和PR关闭率高，补丁发布及时，社区讨论质量高，健康度好。 |
| **ZeroClaw** | 50 (高) | 50 (高) | 无 | 🔥 **高活跃、高风险**：功能密集推进，但也报告了S0级安全漏洞和S1级阻塞Bug，需平衡速度与安全。 |

*注：项目按报告顺序排列。健康度评估综合考虑活跃度、合并效率、Bug严重程度和版本发布节奏。*

#### 3. OpenClaw 在生态中的定位

- **优势**：作为核心参照，**OpenClaw 拥有最庞大的用户基础和维护压力**，象征着“全能平台”的路线。其正在推进的“Claw”包管理系统（PR #102228）力图构建一个闭环的插件生态，类似于移动端的应用商店，这是其他项目尚未涉足的**生态壁垒**。
- **技术路线差异**：与 **ZeroClaw**（Rust 重写，强调安全与性能）和 **IronClaw**（全新架构 Reborn，追求根本性重构）相比，OpenClaw 更像是在现有架构上不断修补和功能堆叠，导致**合并率低、Bug 多、维护负担重**。它的技术演进路径更偏向于“**渐进式改良**”，而非“**颠覆式创新**”。
- **社区规模对比**：OpenClaw 的 Issues 和 PR 数量远超其他项目（日均 500 条），表明其社区规模是**指数级领先**的。但这同时也暴露了其维护能力的瓶颈。相比之下，**IronClaw** 和 **ZeroClaw** 虽然活跃度极高，但其问题讨论更具深度，PR 的“尺寸”（如 XLarge）表明其变更更偏向架构级，而非大量零散的小修小补。

#### 4. 共同关注的技术方向

1.  **安全加固与凭据管理** (OpenClaw, NanoBot, PicoClaw, ZeroClaw, Hermes Agent)：
    - **具体诉求**：要求“蒙版密钥”（Masked Secrets）、环境变量引用替代明文存储、沙箱化执行、Shell 执行前用户确认、子进程隔离和权限策略控制。用户对明文密钥和提示注入攻击的担忧已成为普遍现象。
2.  **性能优化与低延迟体验** (OpenClaw, NanoBot, Hermes Agent, CoPaw, ZeroClaw)：
    - **具体诉求**：抱怨“每次对话额外增加60秒延迟”、“v2.0引入2秒固定开销”、“长对话后工具参数静默丢弃”、“会话消息无限增长导致内存泄漏”。**用户对 Agent 作为“实时助手”的流畅性有苛刻要求**。
3.  **多模态与本地模型支持** (OpenClaw, Hermes Agent, LobsterAI, CoPaw, ZeroClaw)：
    - **具体诉求**：要求在切换视觉/非视觉模型时图片附件能自动同步（状态同步 Bug）、修复与 Qwen 和 `llama.cpp` 等本地模型的兼容性问题、提供更灵活的模型切换能力。**本地化和多模态是除云端大模型之外的核心竞争力**。
4.  **可观测性与 Debug 工具** (OpenClaw, IronClaw, Hermes Agent)：
    - **具体诉求**：用户需要理解决策过程，要求提供 LLM 调用链追踪（IronClaw）、更清晰的工具调用状态反馈、以及“计划模式”下避免重复操作。**Agent 的“黑箱”问题是用户信任受损的主要原因**。

#### 5. 差异化定位分析

| 维度 | OpenClaw (全能平台) | ZeroClaw (安全与高性能) | IronClaw (架构探索者) | CoPaw (应用与协作) | LobsterAI (企业协作) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | 包生态、全能插件、多LLM后端 | 协议兼容(OpenAI)、多Agent协作(Goal Mode)、渠道丰富度 | 全新架构(Reborn)、Agent运行时重写、错误恢复 | 工作流集成(OMP)、桌面端体验(Tauri)、技能市场 | Artifact分享、代码审查协作(Cowork)、Windows静默更新 |
| **目标用户** | 高级开发者、插件生态贡献者 | 对安全性、Rust性能有要求的技术团队 | 核心开发者、架构研究者、追求极致底层的用户 | 个人用户、桌面端重度用户、AI应用开发者 | 企业内开发者团队、需协作功能的专业用户 |
| **技术架构** | 模块化，渐进式演进 | Rust 原生，类型安全 | 根本性重写，追求终局 | Python后端，Tauri桌面壳 | Electron/React，注重UI/UX |
| **核心优势** | 用户基数大、生态潜力大 | 安全性高、性能好、协议兼容性强 | 架构先进、错误处理能力优秀 | 迭代快、社区响应快、实用性强 | 垂直场景深度优化、协作功能强大 |
| **核心风险** | 维护负担重、Bug积压 | 功能推进快、安全风险并存 | 重构稳定性、与旧版兼容性问题 | 性能回归、核心架构稳定性 | 社区活跃度一般，依赖核心团队 |

#### 6. 社区热度与成熟度

- **第一梯队（高速迭代与架构重塑）**：**IronClaw**、**ZeroClaw**。两者都以发布候选版或密集架构整合的形式，处于从“能做”到“做好”的关键冲刺阶段。社区讨论深度高，开发者热情高涨，但风险也最高。
- **第二梯队（成熟运营与巩固质量）**：**OpenClaw**、**CoPaw**。拥有庞大的用户基础和频繁的反馈，但此阶段的主要矛盾是从“能用”到“好用、稳定、安全”的转化。它们在补丁发布和修复效率上表现出色。
- **第三梯队（稳定增长与功能迭代）**：**NanoBot**、**Hermes Agent**、**PicoClaw**。处于健康的迭代节奏，社区贡献活跃，有明确的功能和修复方向，维护团队能有效管理任务。NanoBot 和 PicoClaw 在安全加固上的快速响应值得称赞。
- **第四梯队（探索或静默期）**：**LobsterAI**、**Moltis**、**NanoClaw**。NanoClaw 虽贡献者多但审查慢，Moltis 则处于相对静默期。它们或聚焦于特定垂直场景，或正等待核心团队的决策。

#### 7. 值得关注的趋势信号

1.  **“安全即特性”时代已到来**：社区对 Agent 安全的关注已从“可选”变为“核心功能”。任何不支持蒙版密钥、沙箱执行或权限控制的项目，都将在未来竞争中处于劣势。**对于 AI 智能体开发者，将安全能力作为架构的一等公民（first-class citizen）是项目能否走向生产环境的关键。**
2.  **性能是用户体验的“生死线”**：来自 **NanoBot** (提到60秒延迟) 和 **CoPaw** (提到2秒固定开销) 的强烈抱怨表明，即使是毫秒级的额外开销也会被用户放大。开发者需将性能基线作为 CI/CD 的一部分，并构建可量化的 Agent 性能仪表盘。
3.  **多模态与本地化是必争之地**：从 **LobsterAI** 的图片状态 Bug 到 **OpenClaw**、**Hermes Agent** 对本地模型兼容性的修复，可以看到生态正在快速拥抱多模态和本地部署。**支持模型能力动态适配**，以及对 Ollama、`llama.cpp` 等主流本地推理引擎的深度优化，是面向未来市场的核心竞争力。
4.  **生态兼容性是护城河**：**ZeroClaw** 对 OpenAI API 的兼容与 **OpenClaw** 的“Claw”包管理系统，代表了两种不同的生态策略。前者是将自己插入现有成熟生态（如 Open WebUI），后者是构建专属应用生态。**对开发者而言，选择哪个项目，意味着选择与哪个生态绑定。**

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据NanoBot项目2026年7月22日的GitHub数据生成的日报。

---

### NanoBot 项目动态日报 | 2026年7月22日

#### 1. 今日速览

今日项目动态呈现出极高的活跃度和开发效率。在24小时内，共有33个PR被更新，其中22个已完成合并/关闭，显示出强劲的交付能力。同时，10个Issues中有9个得到解决或关闭，项目净新增活跃议题（1个）控制在低位。团队重点聚焦于安全性（API密钥存储、子进程管理）、稳定性（工具结果、文件读取）和平台扩展（ModelScope提供商支持）。整体来看，项目正处于一个高强度的Bug修复、安全加固和可靠性提升阶段，社区贡献者参与度很高。

#### 2. 版本发布

**无**。过去24小时内无新版本发布。

#### 3. 项目进展

今日团队高效地合并/关闭了多个关键PR，显著推进了项目在安全性、稳定性和扩展性上的进展。

-   **安全加固**:
    -   **API密钥凭据安全**：PR [#4989](https://github.com/HKUDS/nanobot/pull/4989) 修复了语音转录功能中API密钥和环境变量引用未正确解析的问题。PR [#5010](https://github.com/HKUDS/nanobot/pull/5010) 更新了安全文档，强烈建议用户使用环境变量代替明文存储API密钥，这是对 [#4803](https://github.com/HKUDS/nanobot/issues/4803) 问题的直接响应。
    -   **子进程管理**：PR [#4984](https://github.com/HKUDS/nanobot/pull/4984) 通过原子写入（temp+replace）方式，防止了配置写入时崩溃导致的文件损坏。这虽非直接安全管理，但增强了配置系统的健壮性。

-   **稳定性与Bug修复**:
    -   **核心Agent逻辑修复**：PR [#4663](https://github.com/HKUDS/nanobot/pull/4663) 修复了工具调用结果的隔离检疫问题，防止无效/重复的工具结果破坏模型推理，修复了 [#4058](https://github.com/HKUDS/nanobot/issues/4058)。
    -   **数据边界处理**：PR [#4952](https://github.com/HKUDS/nanobot/pull/4952) 在提供商请求边界处对UTF-16代理项进行消毒，解决了因表情符号等富文本内容导致请求失败的 `UnicodeEncodeError` 问题。
    -   **Cron定时任务修复**：PR [#4983](https://github.com/HKUDS/nanobot/pull/4983) 修复了 `jobs.json` 文件中时间字段因被读取为字符串而导致的类型错误。

-   **新功能与平台扩展**:
    -   **新提供商支持**：PR [#4965](https://github.com/HKUDS/nanobot/pull/4965) 正式将ModelScope作为内置模型提供商，支持其兼容OpenAI的API端点，扩展了用户对Qwen、DeepSeek等开源模型的接入方式。
    -   **用户体验改进**：PR [#5020](https://github.com/HKUDS/nanobot/pull/5020) 在WebUI中为已发送消息中的技能引用（`$skillname`）添加高亮，提升了交互反馈。

#### 4. 社区热点

-   **热点讨论：Ollama缓存问题** `#4867` [CLOSED]
    -   **链接**: [HKUDS/nanobot Issue #4867](https://github.com/HKUDS/nanobot/issues/4867)
    -   **热度**: 22条评论，是当日讨论最热烈的议题。
    -   **分析**: 该议题报告了一个严重性能退步：NanoBot在使用Ollama时，每次对话回合都会额外增加约60秒的延迟，长达两周都被用户认为“完全不可用”。尽管最终被关闭，但其22条评论揭示了用户对本地模型推理性能的极高敏感度和苛刻要求。此问题也被标记为`enhancement`，核心诉求是希望保留精确的`prompt prefix`以利用Ollama等工具的缓存机制。这反映出社区对高性能，尤其是本地模型的低延迟体验有着强烈期待。

-   **高反应议题：工具网关** `#4911` [CLOSED]
    -   **链接**: [HKUDS/nanobot Issue #4911](https://github.com/HKUDS/nanobot/issues/4911)
    -   **热度**: 获得1个👍，1条评论。
    -   **分析**: 该议题提出了一个架构层面的功能请求：为Channel提供一个“受保护的”工具网关接口，使得Channel（如实时语音通道）也能调用Agent的工具。这代表社区对NanoBot的应用场景正从纯文本交互向更丰富、更实时的多模态交互（如语音）拓展，对架构的可扩展性提出了更高要求。

#### 5. Bug 与稳定性

当日报告的Bug主要集中在安全、资源管理和数据一致性方面。大多数问题已有对应修复PR。

-   **严重 (P0/P1)**:
    -   **API密钥明文存储** (`#4803` [CLOSED]): 报告API密钥在配置文件中以明文存储，存在安全风险。已有文档更新PR [#5010](https://github.com/HKUDS/nanobot/pull/5010) 和代码原子写入PR [#4984](https://github.com/HKUDS/nanobot/pull/4984) 来缓解。
    -   **文件读取导致OOM** (`#4785` [CLOSED]): `read_file` 在读取多GB文件时未做截断检查，直接加载到内存导致OOM崩溃。有报告但无明确对应的fix PR，状态为已关闭，可能已通过其它方式修复。
    -   **子进程成为孤儿** (`#4794` [CLOSED]): `Exec session` 关闭时未杀死子进程，导致进程泄露。有修复需求的PR `#5021` 正在开放状态，旨在解决此问题。
    -   **Qwen模型暴露思考内容** (`#4934` [OPEN]): 使用Qwen模型时，其内部“思考/推理”内容被错误地暴露在聊天响应中，影响用户体验。已有修复PR `#5023` 正在开放。

-   **中等 (P2)**:
    -   **会话消息无限增长** (`#4787` [CLOSED]): `Session.messages` 列表无界增长，导致内存泄漏。关闭状态，可能已有内部方案或尚未解决。
    -   **捕获 `BaseException`** (`#4788` [CLOSED]): `AgentRunner` 误捕获了 `KeyboardInterrupt`、`SystemExit` 等不应被捕获的异常。关闭状态，可能已修复。

#### 6. 功能请求与路线图信号

今日的功能请求议题和PR揭示了项目潜在的演进方向：

-   **安全与用户控制**:
    -   **Shell执行前用户确认** (`#5013` [CLOSED]): 用户提出在执行Shell命令前需要增加“Human in the Loop”的确认机制，降低安全风险。这一需求很可能会在未来版本中实现。
    -   **环境变量引用** (`#5010` [CLOSED]): 社区有强烈需求转向更安全的凭据管理方式，推荐使用环境变量引用。

-   **增强的Agent控制**:
    -   **子进程级联终止** (`#5021` [OPEN]): `/stop` 命令将能级联终止子Agent的子进程，提升了系统资源管理的可控性。
    -   **取消长期目标命令** (`#5022` [OPEN]): 提出 `/cancel-goal` 命令，用于打破Agent陷入的“持续目标”循环，这是对Agent行为控制上的一次重要补充。

-   **架构与体验改进**:
    -   **模型预设绑定会话** (`#4866` [OPEN]): 允许将模型预设绑定到会话，提供更灵活、持久的模型选择能力。
    -   **支持显式技能加载** (`#5018` [OPEN]): 允许直接调用者显式加载所需技能，而非仅依赖 `always: true` 的自动注入，提升了架构的灵活性。

#### 7. 用户反馈摘要

-   **痛点**:
    -   **性能瓶颈**: 用户`The-Markiteck`强烈抱怨NanoBot与Ollama组合时性能极差（每次请求增加60秒），称其“完全不可用”，对本地推理性能提出了严苛要求。
    -   **安全风险**: 用户`xiakj`明确提出了Shell命令执行缺乏用户确认的安全风险。
    -   **兼容性问题**: `celanwang`用户报告了Qwen模型在NanoBot中暴露思考内容的问题，这可能引发用户对数据隐私和模型行为的困惑。
-   **使用场景与满意点**:
    -   **安全改进受赞**: 对API密钥存储安全问题的报告和相应文档更新，体现了社区对安全性的重视和积极反馈。
    -   **稳定性修复**: 多个针对无效工具结果、类型错误等Bug的修复，预计将提升用户在日常使用中的稳定性体验。

#### 8. 待处理积压

-   **PR: WebUI隐藏配置（`#4399`）**: 旨在为WebUI添加“隐藏设置项”功能，使管理员能简化非技术用户的界面。已开放超过一个月，并存在合并冲突（`conflict`），需要维护者关注和处理。

    -   **链接**: [HKUDS/nanobot PR #4399](https://github.com/HKUDS/nanobot/pull/4399)

-   **PR: Shell防护路径提取（`#4594`）**: 修复Shell工作区防护中 `=` 号后未提取绝对路径的绕过漏洞。此PR为安全修复，虽优先级为P1，但已开放近三周，建议维护者尽快评审与合并。

    -   **链接**: [HKUDS/nanobot PR #4594](https://github.com/HKUDS/nanobot/pull/4594)

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下为您呈上基于 2026-07-22 数据的 Hermes Agent 项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-07-22

## 今日速览

今日 Hermes Agent 项目社区活跃度极高，过去 24 小时内产生了 50 条 Issue 和 50 条 PR 更新，显示出社区高度的参与度和开发热情。虽然无新版本发布，但项目在稳定性、安全性和功能扩展方面有大量并行推进。值得注意的是，P1/P2 级别的 Bug 报告较多，社区对用户体验和系统稳定性有迫切诉求，同时，也有多个高质量的 PR 正在尝试解决这些痛点。当前项目处于“**高活跃、高产出、高关注**”的状态，但任务积压情况（46 条待合并 PR）也需要核心团队关注。

## 项目进展

### 今日已合并/关闭的 PR
过去 24 小时内，共有 4 个 PR 被合并或关闭，表明有重要的修复和功能已落地：
- **`#68999` [CLOSED] - fix(ui-tui): widget-grid hardening**：一个快速跟进 PR，解决了 TUI 中 `widget-grid` 的多个问题，特别是修复了 MCP 组件在未加载完成时就被确认（acked）的严重问题，并增强了网格的健壮性。
- 此外，还有 3 个 Issue 因重复、已修复或已被其他 PR 覆盖而关闭，标志着这些问题的闭环。

### 今日活跃的 PR（待合并状态）
超过 40 个 PR 处于开放和待合并状态，社区贡献者正集中火力解决多个关键问题，涵盖桌面端、TUI、Kanban 模块、安全等方方面面。以下为重点 PR：
- **`#69037` - fix(kanban): re-probe DB health**：旨在解决 Kanban 模块数据库健康检查的缓存问题，提升其可靠性。
- **`#69036` - fix(kanban): harden auto-triage and worker process cleanup**：强化自动分类和工作者进程的清理逻辑，防止僵尸进程和资源泄漏。
- **`#69035` / `#69034` - fix(tui/kanban/codex)**：这些由同一位贡献者提交的 PR 组成了一套组合拳，旨在修复 Kanban 功能在 TUI 和桌面端的持久性、交付和运行时连续性。
- **`#68994` - fix: Copilot ACP weak spots**：增强 Copilot ACP 协议的健壮性，包括长连接复用、会话/更新流处理和故障转移。
- **`#69011` - fix(agent): delimit continuation prompts**：修复 agent 在截断或中断后发送的提示信息（continuation prompts）被模型误解的问题，通过将其标注为系统指令来提升交互正确性。
- **`#69032` / `#69024` - fix(tui): preserve Thai combining marks**：社区贡献者分别提交了两个 PR 来解决 TUI 中泰文字符显示异常的 Bug，体现了对不同语言用户的关注。

这表明项目整体在**Kanban协作模块、桌面端稳定性和国际化显示**等方面迈出了实质性的一步。

## 社区热点

社区讨论最为集中的议题主要集中在记忆系统、技能管理和工具过滤等关键功能的设计上。

- **🎯 话题 1：可配置的内存后端 (`#47349`)**
  - **评论数：13**
  - 这是目前最受关注的话题。用户 `TechFlipsi` 提出了一个重大功能请求：将 `memory.md` 重命名为 `rules.md`，并支持可配置的内存后端。核心诉求是希望摆脱硬编码的文件系统，使用 `honcho` （一个记忆管理库）或 `fact_store` 等专业工具来管理 Agent 的记忆，从而解决长对话中系统提示词臃肿和记忆管理僵化的问题。这反映了社区对“**更聪明、更高效、更可扩展的记忆管理**”的强烈需求。
  - [View Issue #47349](https://github.com/NousResearch/hermes-agent/issues/47349)

- **💡 话题 2：不可变/受保护技能 (`#25083`)**
  - **评论数：7**
  - 社区对 Agent 安全性提出了更高要求。用户 `spiky02plateau` 希望为关键技能（如安全规则）添加“不可变”保护，防止 Agent 在自主运行时无意或恶意地修改它们。这暴露出当前“**技能全可变**”设计的安全风险，社区期待引入类似“权限控制”或“文件锁定”的机制。
  - [View Issue #25083](https://github.com/NousResearch/hermes-agent/issues/25083)

- **🔧 话题 3：Per-function 工具过滤 (`#68964`)**
  - **评论数：1（新开）**
  - 尽管是新建 Issue，但它切中了用户的精细化控制需求。目前只能对整个“技能工具集”执行启用/禁用，而无法单独控制 `skills_list`、`skill_manage` 等具体工具。社区希望获得更细粒度的控制权，以应对复杂的自动化场景。
  - [View Issue #68964](https://github.com/NousResearch/hermes-agent/issues/68964)

## Bug 与稳定性

过去 24 小时报告了多个高优先级 Bug，尤其集中在桌面端、终端工具和会话管理模块，并有修复 PR 同步跟进。

#### 🚨 P1 紧急
- **`#68915` - Worker deadlocks**：Agent 在后台通过 shell `&` 启动服务时（如 `node server.js &`），工作者进程会永久死锁。这是开发人员使用 Agent 进行自动化测试和开发时的核心痛点，严重影响可用性。**目前暂无对应修复 PR。**
  - [View Issue #68915](https://github.com/NousResearch/hermes-agent/issues/68915)
- **`#68474` - state.db zeroed on Windows**：Windows 平台桌面应用更新至 v0.19.0 时，会话数据库被破坏为全空字节（95MB），导致所有历史会话丢失。这是一个影响数据安全的严重故障。**暂无对应修复 PR。**
  - [View Issue #68474](https://github.com/NousResearch/hermes-agent/issues/68474)

#### ⚠️ P2 严重
- **`#68920` - Session leaks**：桌面版/TUI 未正确释放会话租约，导致 `max_concurrent_sessions` 限制阻塞新会话。多个活跃 PR （如 `#69035`）正在修复类似问题。
  - [View Issue #68920](https://github.com/NousResearch/hermes-agent/issues/68920)
- **`#69033` - Orphaned child processes on Windows**：终端工具在 Windows 上无法正确分离子进程组，导致 Agent 退出后留下大量孤儿进程。**暂无对应修复 PR。**
  - [View Issue #69033](https://github.com/NousResearch/hermes-agent/issues/69033)
- **`#68979` - Long-thread rendering issue**：长会话经过压缩后，用户消息显示顺序混乱，严重影响桌面端的使用体验。**暂无对应修复 PR。**
  - [View Issue #68979](https://github.com/NousResearch/hermes-agent/issues/68979)
- **`#69008` - OpenRouter continuation failure**：使用特定模型时，工具调用后的延续推理会因格式问题被 API 拒绝。**暂无对应修复 PR。**
  - [View Issue #69008](https://github.com/NousResearch/hermes-agent/issues/69008)

#### 🐞 P3 低优先级/待复现
- **`#68990` - Thai combining marks dropped**：TUI 中泰文字符显示异常，但存储内容正确。已有修复 PR `#69032` 和 `#69024` 提交。
- **`#68911` - Phone numbers redacted**：网关强制删除 E.164 格式电话号码，影响依赖号码显示的聊天工具。
- **`#68474` / `#65868` - Desktop crash**：桌面应用在 macOS 上因 Rust→V8 IPC 桥问题反复崩溃。

## 功能请求与路线图信号

除了“社区热点”中提及的热门请求外，以下功能请求也反映出用户对项目未来的期望：

- **插件系统扩展 (`#64900` - Feature)**：用户希望允许插件扩展 `send_message` 工具，以为不同平台添加自定义参数。这指向一个**更开放、更易扩展的插件架构**。
  - [View Issue #64900](https://github.com/NousResearch/hermes-agent/issues/64900)
- **桌面端体验增强 (`#69025`, `#68970` - Feature)**：用户连续提交了两个关于桌面端搜索的功能请求，一个是“设置搜索栏”（`#69025`），另一个是“可搜索的时区下拉框”（`#68970`）。这表明随着桌面端功能日益丰富，**提升配置和发现效率**成为社区强需求。对应的 PR `#69023` 和 `#68969` 已经提交。
  - [View PR #69023](https://github.com/NousResearch/hermes-agent/pull/69023)
  - [View PR #68969](https://github.com/NousResearch/hermes-agent/pull/68969)
- **跨表面主题SDK (`#68857` - Feature)**：贡献者提出了一个雄心勃勃的“主题 SDK”，旨在一套主题定义同时应用于 CLI、TUI 和桌面 GUI。这是一个**高价值、高复杂度**的功能，代表着项目在用户界面统一性上的愿景，它将在 v0.20 或更高版本中产生重大影响。
  - [View PR #68857](https://github.com/NousResearch/hermes-agent/issues/68857)

这些诉求表明，社区不再满足于功能堆砌，而是希望项目在**核心架构的灵活性、安全边界和用户交互的智能化**上做出更深层次的改进。

## 用户反馈摘要

从 Issues 评论中，可以提炼出用户对 Hermes Agent 的真实感受：

- **积极反馈**：用户对项目的进展非常关注，并积极参与讨论。多个高质量的功能提案（如记忆系统、主题SDK）由社区成员提出，显示了他们对项目未来的深度思考。用户 `DavidMetcalfe` 连续为桌面端提交搜索功能改进，体现了对提升日常使用体验的满意和期待。
- **核心痛点**：
  - **稳定性灾难**：`#68474` 中用户描述“`state.db` 被彻底破坏”，Windows 用户在更新后丢失了所有会话和配置，这是最严重的不稳定情况。用户对“更新即失去一切”的风险感到沮丧。
  - **死锁与阻塞**：`#68915` 中的“永久死锁”和 `#68920` 中因会话泄漏导致无法开启新会话，这些不可恢复的错误从根本上破坏了用户对 Agent 可靠性的信任。
  - **体验下降**：`#68979` 中描述的“用户需要向上滚动寻找最新回复”，这是一种令人困惑的 UI 倒退，严重影响了长对话场景下的使用流畅度。
  - **配置困难**：时区配置等细节问题上，用户抱怨“必须知道确切的IANA标识符”，这表明某些配置入口对普通用户不友好。

## 待处理积压

以下为长期未得到有效响应或解决的重要 Issue/PR，请核心团队关注：

- **`#23207` (Feature, P3)**：关于“如何使用 Ollama 的 Web 搜索”的问题。从 5 月 10 号起一直处于开放状态，这是一个关系到核心功能集成的痛点，可能需要文档或功能上的支持。
  - [View Issue #23207](https://github.com/NousResearch/hermes-agent/issues/23207)
- **`#61042` (Feature, P3)**：建议 `/compress` 命令支持输入缓存，以便在压缩过程中输入下一条消息。这是一个成熟的用户体验改进建议，已有一个月未更新。
  - [View Issue #61042](https://github.com/NousResearch/hermes-agent/issues/61042)
- **`#65868` (Bug, P3)**：一个关于桌面应用在 macOS 上反复崩溃的报告，社区贡献者提供了非常详细的技术分析（Rust→V8 IPC bridge）。虽然优先级设为 P3，但这是一项影响特定平台高价值用户群的严重问题，值得优先评估。
  - [View Issue #65868](https://github.com/NousResearch/hermes-agent/issues/65868)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目日报 | 2026-07-22

## 今日速览

项目过去24小时保持中等活跃度：共产生 **8 条 Issues 更新**（新开/活跃 4，关闭 4）和 **8 条 PR 更新**（待合并 5，合并/关闭 3），未发布新版本。社区关注点集中在 **Matrix 同步断连后无自动重连**（#3203）、**Google OAuth 2.0 合规性阻断**（#3278）以及 **Web UI 聊天输入卡顿**（#3281）等稳定性问题；同时 **Antigravity 提供商**的两项回归或阻塞 bug 已被快速定位并提交修复 PR。功能侧，**可配置默认 fallback 链**（#3200）和 **策略管控的系统命令执行**（#3282）两项 PR 已合并或进入审阅尾声，项目核心能力稳步推进。

## 版本发布

过去24小时无新版本发布。

## 项目进展

今日合并/关闭了 3 个重要 PR，涵盖功能、修复与合规性：

- **#3282 [已合并] feat(nodes): add policy-gated system exec**  
  作者：bogdanovich  
  新增 `system.exec.v1` 节点能力，允许在严格策略（可执行文件路径、工作目录、环境变量、超时、输出大小）限制下执行系统命令，全程避免 shell 注入，并记录执行结果类型。该功能对需要安全自动化任务的用户场景至关重要。  
  链接：[#3282](https://github.com/sipeed/picoclaw/pull/3282)

- **#3233 [已关闭] Fix pr 3222 backward compat**  
  作者：yaotukeji  
  修复了 #3222 引入的向后兼容性问题，确保旧配置无需修改即可正常工作，属于稳定性增强。  
  链接：[#3233](https://github.com/sipeed/picoclaw/pull/3233)

- **#303 [已关闭] fix: make bot greeting name configurable via bot_name setting**  
  作者：AtharvaGurao  
  允许通过 `bot_name` 配置项自定义 Telegram 和钉钉频道中的欢迎语，解决用户自定义 bot 身份后仍显示固定“PicoClaw”的体验问题。该 PR 实际创建于 2 月，今日合并，标志着长达半年的社区诉求落地。  
  链接：[#303](https://github.com/sipeed/picoclaw/pull/303)

## 社区热点

过去24小时讨论最活跃的议题如下：

- **#3088 [开放] [help wanted] 建议用 vodozemac 替换 libolm**  
  评论数：9 | 👍：2  
  社区持续呼吁弃用未维护且存在安全风险的 libolm，转向官方替代库 vodozemac。该 issue 已标记 `priority: high` 且停滞超过一个月（stale），但仍有较高关注度，是头部安全诉求。  
  链接：[#3088](https://github.com/sipeed/picoclaw/issues/3088)

- **#3203 [开放] Matrix sync 循环缺少重连逻辑**  
  评论数：4 | 👍：1  
  用户报告 Matrix `/sync` 长轮询在网络中断或服务器重启后永久静默死亡，且因主进程存活导致 systemd 无法自动重启。这是 Matrix 信道稳定性的关键短板，社区期待尽快引入指数退避重连逻辑。  
  链接：[#3203](https://github.com/sipeed/picoclaw/issues/3203)

- **#3256 [开放] fix(feishu) 飞书音视频原生类型发送**  
  评论数：0（但被标记为 stale）  
  PR 将飞书渠道上传的音频/视频从通用文件类型改为原生可播放消息，改善飞书用户使用体验。虽无实时评论，但属于提升渠道完备性的实用贡献。  
  链接：[#3256](https://github.com/sipeed/picoclaw/pull/3256)

## Bug 与稳定性

按严重程度排列今日报告的 Bug：

1. **#3278 [已关闭] Antigravity OAuth 被 Google 阻止：不符合 OAuth 2.0 安全政策**  
   用户尝试登录 Antigravity 提供商时，Google 拒绝授权，提示应用不满足其安全策略。该问题直接阻断 Antigravity 提供商的使用，紧急程度高。目前已有关联修复 PR #3280（见下文 PR 部分）。  
   链接：[#3278](https://github.com/sipeed/picoclaw/issues/3278)

2. **#3203 [开放] Matrix sync 无重连逻辑**  
   如上文所述，网络中断后永久死亡，影响 Matrix 通道的可用性。目前无直接修复 PR，但该 issue 已有 4 条讨论，社区可能正在推进方案。  
   链接：[#3203](https://github.com/sipeed/picoclaw/issues/3203)

3. **#3274 [已关闭] Antigravity 提供商在 main 分支回归：`INVALID_ARGUMENT` 错误**  
   用户从 v0.3.1 升级到 `main@85dcfcc` 后 Antigravity 提供商报错，`tool_schema_transform "simple"` 不再有效。该回归已通过后续 commit 修复（issue 已被关闭），但提示主干分支需加强回归测试。  
   链接：[#3274](https://github.com/sipeed/picoclaw/issues/3274)

4. **#3281 [开放] Web UI 聊天输入在历史较长时严重卡顿**  
   刚创建，无评论，但描述清晰：当会话内聊天历史较长时，输入框变得非常卡顿。属性能退化，影响核心交互，优先级应较高。  
   链接：[#3281](https://github.com/sipeed/picoclaw/issues/3281)

5. **#3153 [已关闭] Volcengine Doubao 工具调用偶发泄漏为原始文本**  
   虽然已关闭，但用户报告了在特定模型下工具调用文本被暴露的问题，属于底层交互 bug。关闭可能不代表完全修复（需确认）。  
   链接：[#3153](https://github.com/sipeed/picoclaw/issues/3153)

## 功能请求与路线图信号

- **#3088 用 vodozemac 替代 libolm**：高优先级的核心安全依赖替换，社区呼声高，虽未进入近期发布计划，但有望成为下一个里程碑的关键项。
- **#3200 [待合并] 可配置默认 fallback 链**：允许用户在 Web UI 中配置默认模型及 fallback 链，并通过后端 API 持久化。这直接回应了 #3232（未配置 fallback 时限流失效）等用户痛点，预计会在下一版本中合并。
- **#3282 策略控管系统命令执行**：已合并，将在下一个 release 中提供更安全的命令执行节点，适合自动化工作流。
- **#3228 [待合并] Anthropic Messages 支持 `SystemParts` 与 `cache_control`**：实现 Anthropic 提示缓存能力，对希望利用 Anthropic 模型成本优势的用户至关重要。
- **#3256 飞书音视频原生类型发送**：提升渠道体验的实用功能。

## 用户反馈摘要

从今日 Issues 评论中可提炼出以下真实痛点：

- **Matrix 通道可靠性不足**（#3203）：用户 @weissfl 反馈“silent death”，表明当前 Matrix 实现难以在生产环境落地，需要主动重连机制。
- **Antigravity 提供商频繁受阻**（#3274、#3278）：连续两天出现回归和 OAuth 策略问题，反映出该提供商维护投入不足或上游政策变化应对滞后。
- **限流配置对单模型用户无效**（#3232）：**@VictorSu000** 指出未设置 fallback 模型时，即使配置了 RPM 限流也不生效，这降低了速率限制的实际价值。
- **钉钉聊天列表预览显示固定文本**（#3255）：**@MrTreasure** 抱怨“PicoClaw”占位符破坏了品牌自定义体验，尽管 PR #303 已合并同名问题，但 DingTalk 部分的修复可能尚需额外工作。
- **Web UI 长会话卡顿**（#3281）：**@xpader** 反映历史越长输入越卡顿，可能涉及前端状态管理或消息渲染性能，需要优化。

## 待处理积压

以下 Issue/PR 长期未响应或停滞，建议维护团队关注：

| 编号 | 类型 | 标题 | 创建/最后更新 | 原因 |
|------|------|------|---------------|------|
| #3088 | Issue | 用 vodozemac 替代 libolm（高优先级） | 2026-06-09 / 2026-07-21 | 已 stale 30+天，社区持续讨论但无进展；安全替换依赖决策层推动 |
| #3255 | Issue | 钉钉聊天列表预览固定文本 | 2026-07-14 / 2026-07-21 | 仅 1 条评论，未分配；PR #303 合并后可能已部分修复，但需确认 |
| #3256 | PR | 飞书音视频原生发送 | 2026-07-14 / 2026-07-21 | 标记 stale，无 reviewer 活动；属于低风险增强，可快速合入 |
| #3200 | PR | 可配置默认 fallback 链 | 2026-07-01 / 2026-07-21 | 开放 21 天，无 review；功能请求热度高（对应 issue #3232），建议加速评审 |
| #3228 | PR | Anthropic Messages 支持 SystemParts/cache_control | 2026-07-06 / 2026-07-21 | 开放 16 天，无 activity；对 Anthropic 用户是刚需，可减少 token 开销 |

*注：标记 stale 的 Issue/PR 均已被自动检测为长期未活动，维护者应优先排查是否可关闭或安排 reviewer。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据NanoClaw项目最新数据生成的2026年7月22日项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-07-22

## 1. 今日速览

今日项目提交活跃度较高，但合并速度相对放缓。过去24小时内共产生12个Pull Requests，其中3个已合并/关闭，但仍有9个待处理，表明社区贡献热情高涨，但维护者需要集中精力进行审查。Issues方面相对平静，仅有一个关于新增LINE渠道技能的新功能请求，社区关注度较高。整体来看，项目正处于功能请求和密集修复期，社区贡献者与核心团队的协作模式良好，项目健康度较高。

## 2. 版本发布

本日无新版本发布。

## 3. 项目进展

今日合并/关闭了3个Pull Requests，主要涉及文档优化和自动化流程同步，项目在文档规范性和工具链方面有所推进。

- **文档指南重写**：`#3095` [CLOSED] 对分支维护指南进行了重写，以适应新的注册表分支模型。该工作由核心团队成员完成，有助于提升协作效率。
    - 链接：[PR #3095](https://github.com/nanocoai/nanoclaw/pull/3095)

- **引导流程同步**：`#3116` [CLOSED] 和 `#3114` [CLOSED] 两个PR均为对GitHub自动引导（guidelines）流程的同步操作，确保了贡献者提交模板与项目规范保持同步。
    - 链接：[PR #3116](https://github.com/nanocoai/nanoclaw/pull/3116)
    - 链接：[PR #3114](https://github.com/nanocoai/nanoclaw/pull/3114)

## 4. 社区热点

今日最受关注的议题是 `Issue #3096`，该议题提议为NanoClaw增加LINE官方账号渠道支持。

- **诉求分析**：提案者指出，LINE是日本、台湾和泰国最主要的即时通讯软件，目前项目支持的渠道列表中没有覆盖。这反映了社区对**扩展项目在多地区、多文化背景下适用性**的强烈需求。该议题已产生3条评论，说明有多个用户对此表示关注或参与了讨论，认为这是一个有价值的“技能”贡献。
    - 链接：[Issue #3096](https://github.com/nanocoai/nanoclaw/issues/3096)

此外，`PR #3111` 关于修复Telegram中URL因包含下划线(`_`)导致消息发送失败的问题，获得了较多关注。这是一个典型的“边缘案例”Bug，暴露出用户在实际使用中面临的深层痛点，修复它的呼声很高。
    - 链接：[PR #3111](https://github.com/nanocoai/nanoclaw/pull/3111)

## 5. Bug 与稳定性

今日提交的Bug与修复主要围绕已有功能的稳定性及环境兼容性：

- **严重** - **WhatsApp 媒体文件读取失败** (`PR #3113`)：修复了WhatsApp渠道中，容器无法读取收到的媒体文件的问题。这是一个影响核心功能的Bug，已提交修复PR。
    - 链接：[PR #3113](https://github.com/nanocoai/nanoclaw/pull/3113)

- **严重** - **Telegram URL解析错误** (`PR #3111`)：修复了URL中包含下划线导致的解析失败，该问题会导致消息永久丢失。此修复对于使用GitLab等URL含有`-`的服务的用户至关重要。
    - 链接：[PR #3111](https://github.com/nanocoai/nanoclaw/pull/3111)

- **中等** - **WhatsApp 媒体失败通知回归** (`PR #2896`)：是在之前一个已合并PR (`#2895`) 的基础上进行修复，解决了在处理待批准回复时，Media Failure通知应用的逻辑错误。
    - 链接：[PR #2896](https://github.com/nanocoai/nanoclaw/pull/2896)

- **低** - **OneCLI 工具未阻止旧版Gmail API路由** (`PR #3115`)：通过增加阻断规则，提升了系统的安全性和稳定性。
    - 链接：[PR #3115](https://github.com/nanocoai/nanoclaw/pull/3115)

## 6. 功能请求与路线图信号

- **LINE渠道支持** (`Issue #3096`)：这是一个明确的功能请求。考虑到LINE在东亚市场的占有率和提案者的积极性，此功能很可能被纳入后续开发计划，特别是如果社区能提供一个`@chat-adapter/line`的包或实现方案。
    - 链接：[Issue #3096](https://github.com/nanocoai/nanoclaw/issues/3096)

- **新增Dial频道** (`PR #3050`)：一个由社区提交、旨在增加“Dial”频道的功能PR，显示了项目渠道拓展的多元化趋势。
    - 链接：[PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050)

- **文档国际化** (`PR #2950`)：关于添加繁体中文README的PR，与LINE渠道请求形成呼应，强烈地表明项目正在吸引**非英语**地区的用户群体。国际化将成为项目发展的重要信号。
    - 链接：[PR #2950](https://github.com/nanocoai/nanoclaw/pull/2950)

## 7. 用户反馈摘要

从`Issue #3096` 的讨论中可以提炼出用户的真实痛点：

- **用户痛点**：目前项目不支持的LINE渠道，使得在日本、台湾和泰国的用户或企业无法将NanoClaw部署为本地化的AI助手，限制了其应用场景。用户需要的是一个“开箱即用”的集成。

- **使用场景**：用户期望通过在README中提到的“技能请求”流程，来推动项目方向，使其更符合实际业务需求。这表明社区用户正在积极地利用项目机制来表达诉求。

- **满意度**：新功能请求获得较多关注，侧面反映出用户对项目潜力抱有期待，但不满于当前渠道覆盖的不足。

## 8. 待处理积压

以下PRs已打开较长时间，建议维护者关注并进行处理：

- **`#1530`**：修复Docker volume mounts在SELinux-enforcing系统下的权限问题。该PR自2026年3月29日开启，已有近4个月。对于在Fedora、RHEL等系统上部署的用户而言，这是一个高优先级的修复。
    - 链接：[PR #1530](https://github.com/nanocoai/nanoclaw/pull/1530)

- **`#2236`**：修复容器`WORKDIR`与实际挂载路径不一致问题。同样是一个重要的容器稳定性修复，自5月3日开启后至今未合并。
    - 链接：[PR #2236](https://github.com/nanocoai/nanoclaw/pull/2236)

- **`#2896`**：WhatsApp媒体失败通知的回归问题修复，作为前一个重要PR的跟进，需要及时合并。
    - 链接：[PR #2896](https://github.com/nanocoai/nanoclaw/pull/2896)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，以下是为您生成的 IronClaw 项目日报。

---

# IronClaw 项目动态日报 | 2026-07-22

## 今日速览

项目今日重现高度活跃状态，过去24小时内产生了41条Issue更新和50条PR更新，并迎来了**v1.0.0-rc.1**这一里程碑式的版本发布。核心开发团队正围绕“Reborn”架构落地进行最后的冲刺，多个“XL”尺寸的关键PR（如#6438、#6441）正处于开放和密集审查阶段。项目健康度良好，社区讨论集中于架构整合和产品化上线前的稳定性保障。

## 版本发布

- **`ironclaw-v1.0.0-rc.1` (v1.0.0-rc.1)**
  - 发布日期: 2026-07-20
  - **核心特性**: 这是对IronClaw进行**根本性重构**后的第一个候选发布版本。它不是对0.29.x系列的增量更新，而是对Agent运行时、存储、扩展主机和Web UI的完全重写。
  - **破坏性变更**: 该版本宣布了架构重建，`ironclaw`二进制文件已被替换为新的CLI。这意味着旧的配置文件、命令和API可能不兼容。从之前的 `0.29.x` 版本升级的用户需要参照新的文档进行完整的迁移。
  - **迁移注意事项**: 强烈建议所有用户在进行生产环境部署前，先在测试环境中验证此版本的兼容性。旧的插件、技能或通道可能需要按照新的“Reborn”架构进行适配。

## 项目进展

今日合并/关闭了17个PR，项目在以下关键领域取得了明确进展：

- **核心架构精简 (Reborn)**: 成功合并了多个核心架构重构的PR，标志着“Reborn”落地进入最后阶段。
  - **[#6430] 移除内存存储 (Remove in-memory ratchet stores)**: 该PR移除了最后一个内存态存储，将所有持久化用例迁移到文件系统支持的存储上，这是对稳定性和数据持久性的重要提升。
  - **[#6432] 见证者与路由 (witness always-present + dispatch-through-witness)**: 合入了“见证者模式”的核心代码，将授权和调度路由统一管理，为后续删除旧有的“CapabilityDispatchRequest”等临时DTO对象铺平了道路。

- **集成与兼容性**: 长期分支的整合工作取得突破。
  - **[#6116] (CLOSED) 统一泛型扩展运行时**: 一个大型的集成PR（包含92个commit）成功关闭，将“统一泛型扩展运行时”的特性合并回主分支，解决了长期存在的分支不一致问题。

- **质量与测试**: 测试基础架构得到增强。
  - **[#6422] 全场景LLM追踪 (harvest full per-case LLM trace catalog)**: 开放了用于记录和捕获完整LLM调用链的测试框架，为后续的回归测试和模型行为分析提供了关键能力。

## 社区热点

今日讨论热度最高、最能体现社区焦点的问题是关于“Reborn”架构的终局整合与产品化。

- **#2987 [EPIC] Track Reborn architecture landing strategy and grouped PR plan**
  - 链接: [Issue #2987](https://github.com/nearai/ironclaw/issues/2987)
  - 热度分析: 共有 **44条评论**，为今日之最。作为追踪“Reborn”架构如何分阶段落地的Epic，它持续受到核心贡献者和关注者的高度关注。今日的讨论很可能围绕最新合并的PR和剩余的落地计划展开，反映了社区对架构重构最终状态的强烈关切。

- **#6389 Phase 4 (§5.11): collapse build_local_runtime + build_production_shaped into one build_runtime(cfg)**
  - 链接: [Issue #6389](https://github.com/nearai/ironclaw/issues/6389)
  - 热度分析: 仅一天就获得了 **10条评论**。该Issue直接指向“Reborn”架构路线图中关于统一运行时构建路径的明确目标，其高关注度表明开发者对简化配置、消除环境间的行为差异有着迫切需求。

- **PR #6436, #6438, #6441, #6442**: 多个来自核心贡献者 `ilblackdragon` 的“XL”尺寸PR在今日大量涌现并被更新，涉及命名边界、运行时图选择、密封进程调度等核心问题。这表明项目的核心架构整合工作正在高效且集中地进行，架构师正在高强度推动“Reborn”落地。

## Bug 与稳定性

今日报告的Bug多与“Dogfooding（内部试用）”和稳定性相关，且有对应的修复PR在跟进。

- **Epic #6394: Dogfooding & QA bug fixing 07/20 - 07/24**
  - 链接: [Issue #6394](https://github.com/nearai/ironclaw/issues/6394)
  - **严重程度: 高 (Epic)**。这表明项目已进入密集的内部试用和Bug修复周，旨在**Release前消灭已知问题**。

- **PR #6437: fix(reborn): make model-visible failures recoverable**
  - 链接: [PR #6437](https://github.com/nearai/ironclaw/pull/6437)
  - **严重程度: 高**。该PR直接应对**Epic #6284**中提出的“模型能从它看到的100%错误中恢复”这一终局目标。它确保了模型可见的请求失败、沙盒计划失败等不再是运行时异常，而是可恢复的模型可见反馈，对提升Agent体验至关重要。

- **PR #6425: fix(webui): restore SSE streams across navigation**
  - 链接: [PR #6425](https://github.com/nearai/ironclaw/pull/6425)
  - **严重程度: 中**。修复了Web UI在页面导航时SSE流中断的问题，直接影响了用户使用体验的流畅性。

## 功能请求与路线图信号

- **#6433 Feature: Dedicated custom instructions / master prompt section**
  - 链接: [Issue #6433](https://github.com/nearai/ironclaw/issues/6433)
  - **信号强度：高**。这是一个直接对标ChatGPT和Claude的用户功能请求，意图添加一个专用的“主提示词”设置区域。鉴于v1.0.0-rc.1已发布，此功能很可能被纳入v1.1或更早的补丁版本。

- **#6284 [EPIC] error-recoverability endgame**
  - 链接: [Issue #6284](https://github.com/nearai/ironclaw/issues/6284)
  - **信号强度：极高**。虽然这是内部设立的工程目标，但它直接关系Agent的鲁棒性。今日合并的**PR #6437**正是对此Epic的直接响应，说明开发团队正在将此类基础能力作为**上线前的必备条件**来执行。

## 用户反馈摘要

- **配置复杂性与一致性**: 从Epic #3036、#6389等讨论可以看出，用户和运维人员渴望一种更统一、声明式的配置方式，而不是在多种配置文件和运行时标志之间手动切换。社区对`build_runtime(cfg)`这类简化配置的提案反响热烈，表明简化操作是当前最强烈的用户痛之一。

- **对“Reborn”架构的期待**: 从Issue #2987等热点问题可以看出，社区对即将到来的根本性架构升级既充满期待又保持谨慎。开发者们非常关注API的稳定性、迁移路径以及新旧版本的兼容性。

## 待处理积压

- **#5598 [PR] chore: release**
  - 链接: [PR #5598](https://github.com/nearai/ironclaw/pull/5598)
  - **状态**: 开放已 **19天**。
  - **分析**: 该PR涉及`ironclaw_common`和`ironclaw_skills`等核心库的版本发布。虽然它可能因为等待更关键的架构变更落地而被挂起，但持续的积压可能会阻塞其他依赖新版本的开发工作。建议维护团队检查此PR的阻塞项，并评估其优先级。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，以下是基于您提供的 LobsterAI (netease-youdao/LobsterAI) 项目数据生成的 2026-07-22 项目动态日报。

---

## LobsterAI 项目动态日报 | 2026年07月22日

### 1. 今日速览

过去24小时，LobsterAI 项目整体活跃度较高，主要体现在 Pull Request 的密集提交与合并上。项目共收到 10 条 PR，其中 5 条已被合并或关闭，表明维护团队对代码库的迭代和修复效率较高。Issues 方面仅更新 1 条，整体社区讨论热度相对平稳。团队重点推进了**图片附件与视觉模型同步**、**Artifact 分享/部署权限流优化**和**Windows 客户端静默更新**等功能，同时修复了多个与浏览器注释状态相关的 Bug。项目未发布新版本。

### 3. 项目进展

今日项目完成了 5 项重要的功能迭代与问题修复，主要聚焦于提升用户体验、优化协作流程和完善系统配置。

- **【已合并】Windows 静默更新机制** ([#2368](https://github.com/netease-youdao/LobsterAI/pull/2368))：优化了 Windows 平台的更新流程。现在更新包将通过 PowerShell 后台静默安装，避免了交互式安装向导，更新完成后自动重启应用。同时，对 UAC 权限拒绝等常见错误提供了本地化的错误提示，提升了 Windows 用户的无感更新体验。

- **【已合并】浏览器注释与会话状态修复** ([#2371](https://github.com/netease-youdao/LobsterAI/pull/2371))：针对协作（Cowork）功能，修复了多个浏览器注释相关的问题。现在支持无评论但包含样式修改的注释，并会在 Prompt 和附件中展示元素修改的细节。同时，清空草稿注释会自动停止 Webview 标注会话，避免了页面状态残留。

- **【已合并】Artifact 分享访问权限优化** ([#2369](https://github.com/netease-youdao/LobsterAI/pull/2369))：优化了 Artifact 文件分享的交互流程，区分了“创建分享”和“更新访问权限”两种状态，避免打开弹窗时自动创建分享。改进了本地服务部署的权限设置逻辑，并增加了停止服务提示、权限更新成功反馈等，使操作路径更清晰。

- **【已合并】Artifact 统一订阅拦截弹窗** ([#2370](https://github.com/netease-youdao/LobsterAI/pull/2370))：为 Artifact 的文件分享和本地部署功能增加了统一的订阅权限校验和提示弹窗组件。这一改动确保用户在执行付费操作前会收到明确的引导，有助于规范化商业功能的转化路径。

- **【已合并】依赖更新** ([#1279](https://github.com/netease-youdao/LobsterAI/pull/1279))：由 Dependabot 自动化机器人提交的依赖更新（cross-env）被合并，项目基础依赖的健康度得到微小提升。

### 4. 社区热点

今日社区讨论的核心聚焦在**多模态模型切换时的图片附件状态同步问题**上。

- **最活跃 Issue: #1861 - 图片附件不随模型切换重新处理**
  【[链接](https://github.com/netease-youdao/LobsterAI/issues/1861)】
  该 Issue 是今日最受关注的讨论点，虽然点赞数不多（0），但其详尽的描述揭示了用户在切换支持/不支持图片的模型时的核心痛点。问题指出了三种具体的失败场景，包括视觉模型看不到图片、非视觉模型错误处理Base64数据以及界面提示不更新。这暴露了当前模型能力状态与附件处理逻辑之间的“状态不同步”问题，是一个影响用户流畅使用多模态功能的明显断点。

- **关联 PR: #2373 - fix(cowork): sync image attachments with model capability**
  【[链接](https://github.com/netease-youdao/LobsterAI/pull/2373)】
  与 Issue #1861 直接相关的是这条处于开放状态的 PR。这明显是社区和维护团队最关心的核心修复。该 PR 明确旨在解决当会话在视觉模型和非视觉模型之间切换时，图片附件状态不同步的问题。这说明维护团队已经意识到并开始着手修复此问题，社区期待其尽快合并。

### 5. Bug 与稳定性

今日无新 Bug 报告，但 Issue #1861 揭示了一个重要的逻辑 Bug，影响日常对话的多模态体验。

- **【严重】图片附件状态不随模型切换同步** ([#1861](https://github.com/netease-youdao/LobsterAI/issues/1861))
  - **现象**：用户手动切换模型后，已添加的图片附件处理方式（Base64编码 vs 文件路径引用）未更新，导致视觉模型“看”不到图片，或非视觉模型发送了无意义的 Base64 数据。
  - **影响范围**：所有在多模态和非多模态模型间进行切换的用户。
  - **修复状态**：已有对应的修复 PR #2373 处于 **OPEN（待合并）** 状态，预计将很快被合入。

此外，今日已合并的 PR 也修复了另一稳定性问题：
- **【中】协作模式下浏览器注释状态残留** ([#2371](https://github.com/netease-youdao/LobsterAI/pull/2371))：修复了清空草稿注释后，Webview 页面仍会残留标注状态的问题。

### 6. 功能请求与路线图信号

今日主要功能请求信号来自 Issue #1861，它本质上是一个对“动态适配”功能的需求：即对话系统应根据当前选择的模型能力，实时调整所有上下文元素（如图片附件）的处理方式。

- **模型感知状态同步**：用户期望模型切换后，整个会话的上下文能自动、无缝地适配。这不仅是 Bug，更是对产品核心交互逻辑的完善需求。结合已提交的修复 PR (#2373)，该功能很可能在下一轮更新中被纳入。

- **商业化功能闭环**：已合并的 PR #2369 和 #2370 显示，项目正在加强 Artifact 功能（如分享、本地部署）的订阅管理。这暗示项目 4.0 版本（或近期版本）的路线图中，**完善商业功能的基础设施和用户引导流程**是优先度较高的方向。

- **更细致的 UI 偏好控制**：PR #2374 提出在设置中添加“永久隐藏侧边栏广告”的开关，尽管尚未合并，但反映了社区对于广告体验的负面反馈，以及对更细粒度用户控制权的需求。

### 7. 用户反馈摘要

从 Issue #1861 的详细描述中，可以提炼出以下真实用户痛点：

- **多模态体验的“断点”**：用户在使用不同模型（视觉/非视觉）时，原本流畅的添加图片-发送消息流程被“模型切换”操作打断。用户需要手动重新处理附件，这破坏了用户体验的一致性。
- **对“所见即所得”的期待落空**：用户在切换模型后，界面上的附件看似还在，但实际上“对不起，你的模型变了，我需要重新处理你”。用户对这部分状态的感知是缺失的，导致发送后才发现模型“看不到”图片，造成了困惑和操作成本的浪费。
- **操作路径复杂**：描述中提到了三种场景，每种都需要用户理解不同的失败模式并手动调整。这并非用户期望的操作方式，他们希望系统能智能处理。

### 8. 待处理积压

以下两条由 Dependabot 提交的依赖更新 PR 已标记为 `[stale]`（陈旧），长期未获响应，存在依赖风险，建议维护者予以关注。

- **[STALE] chore(deps): bump react-dom from 18.3.1 to 19.2.4** ([#1280](https://github.com/netease-youdao/LobsterAI/pull/1280))
  - 状态：OPEN | 创建于：2026-04-02
  - 风险：等待近4个月，React 19 版本较老，后续若有安全更新可能不会自动覆盖此 PR，需手动处理并测试兼容性。

- **[STALE] chore(deps-dev): bump vite from 5.4.21 to 8.0.9** ([#1281](https://github.com/netease-youdao/LobsterAI/pull/1281))
  - 状态：OPEN | 创建于：2026-04-02
  - 风险：更新跨度极大（Vite 5 -> 8），合并后可能引入构建或兼容性问题，需要仔细审查变更日志。

此外，核心 Bug 修复 PR #2373 处于开放状态，是当下最重要的待合并项。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报（2026-07-22）

---

## 1. 今日速览

过去24小时内，项目活跃度处于较低水平。仅产生1条新Issue讨论和1条自动化依赖更新PR，无新版本发布，也无任何PR被合并或关闭。社区讨论集中于#574“按主题进行模型路由”的功能请求，该Issue在沉寂数月后于今天获得更新，表明用户对该需求仍有持续关注。整体来看，项目今日以社区讨论和常规依赖维护为主，核心开发推进不明显。

- Issue 新开/活跃：1 条
- PR 待合并：1 条
- 版本发布：0 个

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日无任何PR被合并或关闭。暂无功能推进或Bug修复的记录。唯一待处理的PR #1161 为依赖更新，尚未通过审查。

- [#1161 (OPEN) chore(deps): bump astro from 7.0.9 to 7.1.3 in /docs](https://github.com/moltis-org/moltis/pull/1161) —— 由 Dependabot 自动提交，升级文档站点的Astro框架版本，旨在修复潜在安全或兼容性问题，等待维护者合并。

---

## 4. 社区热点

今日最受关注的议题为 Issue #574，该Issue于2026-04-06创建，今天获得最后一次更新（可能是回复或标签变化），共获5条评论、1个👍。

- [#574 [Feature] Model Routing Per topic](https://github.com/moltis-org/moltis/issues/574)  
  **作者**：azharkov78  
  **诉求**：用户希望Moltis能够根据对话主题（topic）实现模型路由，即不同话题自动分配不同的后端模型（如OpenAI、Claude等），从而优化资源利用与回答质量。  
  **分析**：该请求提出了一个较为高级的编排能力，涉及多模型调度与策略管理。虽然评论数量不多，但Issue存在超过3个月仍未被关闭，说明社区对此功能存在真实需求，且维护团队尚未明确表态是否采纳。今日的更新可能源于用户再次发声或维护者标记为“考虑中”。

---

## 5. Bug 与稳定性

今日未报告任何Bug、崩溃或回归问题。项目稳定性方面暂无负面信号。

---

## 6. 功能请求与路线图信号

今日唯一的功能请求即#574（Model Routing Per Topic），该提议与Moltis作为AI智能体编排平台的核心定位高度契合。结合目前PR#1161仅为依赖更新，暂无其他与模型路由相关的开发分支，因此该功能短期内进入开发的可能性较低。但若社区反馈持续升温，可能被纳入下一个小版本或中间版本（如v0.x）的路线图。

---

## 7. 用户反馈摘要

从#574的评论（共5条）来看（摘要中未包含具体评论内容），用户**azharkov78**在创建Issue时已按照预检清单确认未重复提交，并强调该请求来自聊天会话场景。整体语气正面，属于建设性功能建议。目前暂无用户表达对现有功能的不满或使用障碍。

---

## 8. 待处理积压

以下Issue因创建时间较长且长期未得到正式回应或关闭，值得维护者关注：

- **#574 [Feature] Model Routing Per topic**  
  创建于2026-04-06，至今已逾3个月。虽今日有更新，但仍处于Open状态且未关联任何PR或里程碑。建议维护者评估是否纳入路线图，或给予明确反馈（如“暂不考虑”），以避免社区期待落空。

- （今日无其他明显积压）

---

**总结**：Moltis项目今日运行平稳但开发节奏放缓。社区对高级路由功能保持期待，而依赖更新等待合并。建议维护者尽快处理待合并PR #1161，并针对#574给出明确态度，以维持社区参与度。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，遵照您的指示。以下是根据 CoPaw (github.com/agentscope-ai/CoPaw) 项目数据生成的 2026-07-22 项目动态日报。

---

# CoPaw 项目动态日报 | 2026-07-22

## 今日速览

项目今日活跃度极高，Issues 和 PR 的更新数量均处于近期高位，呈现“高产出、高闭合”的健康状态。过去24小时内，项目成功关闭了21个 Issues 和30个 PR，同时有20个新 PR 正在等待合并。新发布的 `v2.0.1-beta.1` 主要聚焦于 Bug 修复。社区讨论热情高涨，关于会话数据污染和旧版性能回归的问题引发了大量关注。整体来看，项目正通过高密度的社区反馈和快速的补丁迭代，稳步向 v2.0 正式版的成熟稳定迈进。

## 版本发布

**v2.0.1-beta.1**

此版本为补丁发布，主要修复了以下问题：
- **核心修复：** 修复了 Tauri 桌面端入口文件使用相对路径导入导致的问题，增强了桌面端稳定性。
- **内存修复：** 修复了 `MemorySpace` 组件在保存工具引用时可能因 `OSError` 而崩溃的问题，提升了工具调用场景下的健壮性。

该版本不包含破坏性变更，建议所有 v2.0.x 用户升级。

## 项目进展

今日有多个关键 PR 被合并，标志着项目在治理、安全性和用户体验方面取得了实质性进展：

- **治理与安全（Governance & Security）**：一系列由 `weidankong` 和 `XiuShenAl` 贡献的 PR 被合并，标志着项目在“治理”和“沙箱”模式上迈出了关键一步。这些 PR 引入了新的工具注册机制（`@tool_descriptor`），统一了内置工具和插件工具的注册与权限控制，并修复了 `ToolGuard` 与安全基元的集成问题，显著增强了 Agent 执行的安全性。
- **OMP工作流集成（OMP Workflow Integration）**：`XiuShenAl` 提交的关于集成 OMP 工作流模式的 PR (#5882) 已被标记为待合并，这是项目功能上的一个重要进展。它引入了多种预设工作流模式并扩展了子 Agent 能力。
- **用户体验优化**：PR #6262 添加了“一键复制Agent配置”功能，方便用户快速创建类似配置的Agent，提升了配置管理效率。同时，PR #6296 修复了从市场安装技能后，前端配置未能即时刷新的问题。

## 社区热点

今天社区讨论的热点集中在以下几个方面，相关 Issues 和 PR 均获得了大量关注：

1.  **会话数据污染（Critical）**：**Issue #6299** `[Bug]: Deleted session records persist in history.db...` 是今日最受关注的 Bug 之一。用户反馈删除会话后数据并未完全清除，导致新会话出现序列冲突和上下文污染。这直接触及了数据一致性和用户隐私的核心痛点，得到了3条评论。关联的 **PR #6068** 正在对此问题进行修复。
2.  **v2.0 性能回归（High）**：**Issue #6307** `[Performance]: v2.0 introduces ~2s fixed overhead...` 报告了一个严重的性能回归问题。用户指出从 v1.x 升级到 v2.0.0.post3 后，每次简单回复都会凭空多出约2秒的固定开销。该问题直指 v2.0 核心架构变化，可能影响多数用户的升级意愿，目前已有2条评论，等待项目组确认和修复。
3.  **计划模式下的反复读取文件（Medium）**：**Issue #5759** `[Bug]: QwenPaw_计划模式反复读取文件` 在今日依然有讨论，用户抱怨在 Plan Mode 下，同一文件被不必要的多次读取，增加了 Token 消耗和等待时间。这反映了用户对 Agent 执行效率和智能性的高要求。

**链接：**
- [Issue #6299: Deleted session records persist in history.db...](https://github.com/agentscope-ai/QwenPaw/issues/6299)
- [Issue #6307: v2.0 introduces ~2s fixed overhead...](https://github.com/agentscope-ai/QwenPaw/issues/6307)
- [Issue #5759: QwenPaw_计划模式反复读取文件](https://github.com/agentscope-ai/QwenPaw/issues/5759)

## Bug 与稳定性

今日报告的 Bug 数量较多，主要集中在稳定性和数据一致性上。

**严重：**
1.  **[Bug] 会话数据污染 (Issue #6299)**：删除的会话数据残留导致新会话错乱。**已有修复PR** (#6068)。
2.  **[Bug] v2.0 简单回复~2s固定开销 (Issue #6307)**：v2.0 存在性能回归。**暂无修复PR**。
3.  **[Bug] 模型输出截断 (Issue #6324)**：使用 MiniMax-M3 模型时，响应被意外截断。
4.  **[Bug] 对话进度丢失与无限循环 (Issue #5860)**：v2.0 中频繁出现上下文混淆和 Agent 死循环的问题，对可用性影响大。

**中等：**
5.  **[Bug] 多次工具调用产生相同思考过程 (Issue #6257)**：当 Agent 单轮调用多个工具时，思考过程内容完全一致，缺乏独立性。
6.  **[Bug] LaTeX公式无法正确渲染 (Issue #6320)**：渲染器在处理带根号的公式时出现错误。
7.  **[Bug] 模型最大输出token不生效 (Issue #6258)**：用户设置的最大输出 Token 参数对流式API无效。
8.  **[Bug] 多工具调用死循环 (Issue #6241)**：Agent 在多次调用 `memory_search` 后陷入死循环，缺乏重复检测机制。

**链接：**
- [Issue #6324: MiniMax-M3 响应截断](https://github.com/agentscope-ai/QwenPaw/issues/6324)
- [Issue #5860: v2.0 对话进度丢失与无限循环](https://github.com/agentscope-ai/QwenPaw/issues/5860)
- [Issue #6257: 多次工具调用重复思考](https://github.com/agentscope-ai/QwenPaw/issues/6257)

## 功能请求与路线图信号

用户今日提出了多项有意义的功能请求，部分可能与项目未来路线图方向一致：

- **工作区文件快捷访问**：用户希望可直接在 Desktop 客户端内访问Agent产出的文件，而不是跳出应用去文件夹里翻找。**PR #6083 (OPEN)** 探讨了此功能。
- **可配置皮肤与主题**：新贡献者提交了首个关于可配置主题模块的 Draft PR (**PR #6312**)，这可能呼应了社区对个性化界面的潜在需求。
- **自定义命令终端**：用户希望在 Coding 模式中拥有一个可输入自定义命令的终端，以增强开发灵活性 (**Issue #6308**)。
- **AGENTS.md 中支持前置条件规则**：用户提出在任务规则中定义工具调用的前置条件，例如在修改文件前必须先查询记忆，以提升Agent执行任务的准确性 (**Issue #6321**)。
- **支持更多云模型**：用户要求更新内置模型列表，以支持阿里云新发布的 `qwen3.8-max-preview` 模型 (**Issue #6285**)。

这表明社区不仅关注稳定性，也对“增强Agent行为的可控制性”和“提升端到端用户体验”有强烈需求。**PR #6083 (工作区访问)** 和 **PR #5992 (会话模型覆盖)** 等开放性 PR 很可能是下一版本的重点考虑方向。

## 用户反馈摘要

- **痛点与失望**：v2.0 的性能回归（#6307）和对历史会话数据处理不当（#6299）是用户最强烈的负面反馈点，尤其是在从 v1.x 升级的场景下，用户对“开倒车”的体验非常失望。
- **场景与需求**：用户以实际工作场景（如合同审核 #6297）和开发场景为主，期望Agent能直接处理更多文件类型，并更智能、高效地执行任务（避免重复读取文件 #5759）。
- **积极信号**：社区中已有新贡献者提交了主题模块 (#6312) 等增强功能，说明项目有良好的社区吸引力和扩展潜力。用户对高度定制化（如分离工具调用信息、自定义模型列表）的需求也表明项目正被深度使用。

## 待处理积压

- **Issue #6083 (增强)**：关于“Desktop窗口增加工作区产出物快捷访问按钮”的讨论，已开放一周，有3条评论。此功能对用户体验提升显著，建议项目组关注。
- **PR #5992 (功能)**：关于“添加会话级模型覆盖”的 PR，已开放10天，允许用户为不同会话指定不同模型。这是一个常见且实用的需求，需要推动审查和合并流程。
- **PR #6203 (Bug修复)**：关于“修复Windows tasklist探针”的 PR，涉及跨平台稳定性，由新贡献者提交且已标记为“待人工审查”，建议尽快安排审查。

**链接：**
- [Issue #6083: Desktop 窗口增加工作区产出物快捷访问按钮](https://github.com/agentscope-ai/QwenPaw/issues/6083)
- [PR #5992: Add per-session model overrides](https://github.com/agentscope-ai/QwenPaw/pull/5992)
- [PR #6203: fix(utils): bound and hide the Windows tasklist liveness probe](https://github.com/agentscope-ai/QwenPaw/pull/6203)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-07-22

**数据来源**：GitHub (zeroclaw-labs/zeroclaw)  
**统计区间**：2026-07-21 ~ 2026-07-22（过去24小时）  
**分析机构**：AI 智能体与个人 AI 助手开源项目分析师

---

## 1. 今日速览

ZeroClaw 在过去24小时内保持了极高的社区活跃度：**50 条 Issue 更新**（其中 47 条新开/活跃，3 条关闭）和 **50 条 PR 更新**（41 条待合并，9 条合并/关闭）。项目未发布新版本，但多个重量级功能（OpenAI 兼容端点、目标模式控制器、Matrix 流模式）正在密集推进。安全相关议题（delegate 绕过允许列表、Shell 工作区逃逸）引发高度关注，两个 S0 级漏洞被报告。整体而言，项目处于快速迭代期，贡献者协作热情高涨，但积压的 `needs-author-action` PR 数量较多（约 13 条），需维护方加速审核。

---

## 3. 项目进展

过去24小时共有 **3 个 Issue 关闭**、**9 个 PR 合并/关闭**（具体列表未完全展示）。从已知关闭项可看出重要推进：

- **RFC #9086**（Structured Security Audit Pipeline）已关闭，标志着安全审计管线设计取得阶段性共识，后续可进入实现阶段。
- **Bug #9120**（SOP 路由错误地在 false `when` 后执行 switch）已修复，提升 SOP 引擎可靠性。
- **Feat #7082**（Mattermost WebSocket 监听模式）已合并，增强了渠道实时性。

在活跃 PR 方面，多个大型 PR 处于持续审查或等待作者响应状态：

- **PR #8486**：OpenAI Chat Completions 兼容端点 (size:XL) — 这是社区期待已久的功能，直接关联 Issue #8603。当前状态 `needs-author-action`，需作者解决冲突。
- **PR #8687 – #8689 系列**：目标模式（Goal mode）控制器、工具、渠道接入 — 由 @vrurg 主导的三大 PR 构成完整 feature 栈，合并后将补齐“有界自主会话”核心能力。
- **PR #8443**：Matrix 单消息进度草稿 (size:XL) — 解决 Matrix 渠道流模式体验问题，已持续近一个月。
- **PR #8949**：Webhook GET + challenge-echo 插件验证 (size:XL) — 打通渠道插件验证流程，预计将提升第三方插件接入能力。

项目整体在 **渠道体验优化**、**安全边界加固**、**协议兼容性** 三个方向迈出了扎实步伐。

---

## 4. 社区热点

过去24小时讨论最活跃的 Issue 和 PR 如下：

| 编号 | 标题 | 评论数 | 核心诉求 |
|------|------|--------|----------|
| [#8226](https://github.com/zeroclaw-labs/zeroclaw/issues/8226) | [Feature]: Add typed per-agent git identity | 6 | 为内建 git 操作提供多租户身份隔离，`runtime_context` / `runtime_secrets` 设计引发深入讨论 |
| [#8505](https://github.com/zeroclaw-labs/zeroclaw/issues/8505) | [Bug]: Telegram channel cannot be configured | 6 | Telegram 渠道配置失败，bot 无响应，被标记为 S1 阻塞级 Bug |
| [#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) | RFC: Goal mode for bounded autonomous session work | 4 | 目标模式是当前最被期待的功能之一，社区对预算/暂停/续传机制讨论热烈 |
| [#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) | RFC: OpenAI Chat Completions compatibility adapter | 4 | 用户强烈要求能接入 Open WebUI / LobeChat 等客户端，已有 PR #8486 跟进 |

**分析**：这四个议题覆盖了 **身份管理（多租户）**、**渠道稳定性**、**自主任务框架**、**生态兼容性**，是用户当前最痛点。其中 #8505 的严重性为 S1（工作流阻塞），且被标记为 `quickstart`，对新手用户影响极大，社区要求尽快修复。

---

## 5. Bug 与稳定性

过去24小时报告的 Bug 按严重程度分级如下：

### S0 — 数据丢失 / 安全风险
1. **#8279** ([delegate 绕过父级工具允许列表](https://github.com/zeroclaw-labs/zeroclaw/issues/8279))：子代理可调用父策略排除的工具，已确认影响安全边界。**尚未有关联修复 PR**。
2. **#9247** ([Shell 工具工作区边界绕过](https://github.com/zeroclaw-labs/zeroclaw/issues/9247))：符号链接可逃逸工作区目录，导致任意文件读写。**刚刚报告，无 PR**。

### S1 — 工作流阻塞
3. **#8505** ([Telegram 渠道无法配置](https://github.com/zeroclaw-labs/zeroclaw/issues/8505))：`zeroclaw channels doctor` 报告未配置，bot 不能回复。影响快速入门体验。**无直接修复 PR**，但社区猜测可能与启动顺序或配置解析有关。

### S2 — 行为退化
4. **#8642** ([MCP 工具模式克隆导致 RSS 无限增长](https://github.com/zeroclaw-labs/zeroclaw/issues/8642))：已在 #8633 中缓解重启风暴，但内存增长根源仍在排查。
5. **#8731** ([Stdio MCP 服务器僵尸进程累积](https://github.com/zeroclaw-labs/zeroclaw/issues/8731))：子进程未正确回收，长期运行导致进程表溢出。**无直接 PR**。
6. **#8615** ([Compatible 提供者静默删除 `<think>` 标签内容](https://github.com/zeroclaw-labs/zeroclaw/issues/8615))：内容丢失但无报错，用户体验差。PR #8838 修复了 SSE 空闲超时，但标签剥离问题需额外修复。
7. **#8718** ([`zeroclaw config init` 生成无效配置](https://github.com/zeroclaw-labs/zeroclaw/issues/8718))：静默禁用本地语音转录，影响 voice pipeline。**无直接 PR**。
8. **#9120**（[SOP 开关路由错误](https://github.com/zeroclaw-labs/zeroclaw/issues/9120)）**已关闭**，经由 #8771 修复。

此外，#9240 ([`save_dirty` 对包含点的键名静默丢弃](https://github.com/zeroclaw-labs/zeroclaw/issues/9240)) 为配置基础组件的隐蔽 bug，可能导致特定模型 ID 配置无法持久化。

**建议**：社区应优先关注 #8279 和 #9247 这两个安全漏洞，特别是 #8279 已在 Issue 中持续近一个月，应尽快安排 fix PR。

---

## 6. 功能请求与路线图信号

过去24小时提出的 Enhancement 类 Issue 共约 20+ 条（含 RFC），凸显社区的多样性需求。以下按优先级和关联 PR 进行分类：

### 很可能纳入下一版本（已有对应 PR 或活跃实现）
| Issue | 标题 | 对应 PR | 状态 |
|-------|------|---------|------|
| #8603 | OpenAI Chat Completions 适配 | #8486 | `needs-author-action`，等待作者 |
| #8303 | Goal mode RFC | #8687/#8688/#8689 | 三大 PR 密集推进 |
| #8541 | Matrix 线程级会话历史 | #8443 | `needs-author-action` |
| #8226 | 每代理 Git 身份 | 暂无直接 PR，但设计讨论完成 | 预计近期会有实现 |
| #8288 | SOP 控制面 milestone | 已有多个小 PR 合入 | 正在按 roadmap 推进 |

### 路线图信号较强的需求
- **#8568** (Mixture-of-Agents 虚拟提供者)：反映了用户对多模型协作的迫切需求。
- **#8780** (Gemini Live 实时语音渠道)：前瞻性需求，已有 RFC，但实现成本较高，预计列为 0.9.x 目标。
- **#8396** (协议优先的提供者构建)：架构层面 RFC，意图统一 provider 实现，减少碎片化。
- **#8309** (SkillForge 废弃或重新激活)：社区存在分歧，需维护者决策。

### 跟踪器 (Tracker)
- **#8583** (渠道/共享边界清理)：包括多个子任务，旨在统一渠道生命周期、流模式、信任模型等。

**趋势判断**：项目正向“平台化”演进，重点补齐**第三方客户端兼容 (OpenAI API)**、**自主会话 (Goal)**、**渠道丰富度 (Matrix/Telegram/QQ)**，同时对安全与内存稳定性投入显著提高。

---

## 7. 用户反馈摘要

从评论区提炼的真实用户声音（匿名化处理）：

- **Telegram 渠道配置失败** (#8505)：用户按 quickstart 和 ZeroCode 设置后，bot 在 Telegram 中无响应，CLI 正常。反馈“Probably related: another...”表明该问题可能与其他配置解析 bug 耦合，新手入门场景严重受损。
- **文档错误** (#8810)：用户尖锐指出“slop remains slop”，批评部分命令输出与文档不符，影响新用户信任。该 Issue 被标记为 `priority:p2`，但 `risk:low`，建议提升优先级。
- **条件渠道任务不应回复** (#8410)：用户期望“有新邮件通知，否则静默”，但当前设计仍会发送空回复。社区讨论确认需要 `intentional no-reply` 语义。
- **模型切换不灵活** (#8600)：从 Moltis 迁移的用户抱怨 ZeroClaw 只能使用 provider 的默认模型，无法像 Moltis 一样自由切换同一 provider 下的全量模型。已提出 `easy per-chat model switching` 需求。
- **配置模板静默损坏** (#8718)：用户发现 `zeroclaw config init` 生成的配置中 `local_whisper` 参数值超出运行时可接受范围，导致语音转录无声失败。用户情绪：“silently disabling transcription for local_whisper”。
- **Bedrock Nova 2 Lite 缓存错误** (#8720)：用户试图禁用缓存点，但找不到配置途径。支持请求。

**整体满意度**：社区对 ZeroClaw 的技术架构（Rust 安全、类型系统）认可度高，但在渠道稳定性、文档质量、配置一致性方面出现较多抱怨。快速入门体验是当前短板。

---

## 8. 待处理积压

以下为长期未响应或停滞的关键 Issue/PR，需维护者关注：

### 长期未关闭的 Issue（创建超20天）
| Issue | 标题 | 创建时间 | 最后更新 | 严重度 | 状态 |
|-------|------|----------|----------|--------|------|
| [#8226](https://github.com/zeroclaw-labs/zeroclaw/issues/8226) | Typed per-agent git identity | 2026-06-23 | 2026-07-21 | P2 | `accepted, no-stale` |
| [#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) | Goal mode RFC | 2026-06-24 | 2026-07-21 | P2

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*