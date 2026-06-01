# OpenClaw 生态日报 2026-06-01

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-01 02:55 UTC

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

# OpenClaw 项目日报 — 2026-06-01

## 1. 今日速览

过去 24 小时内，OpenClaw 社区活动极为活跃：**500 条 Issue 更新**（新开/活跃 284 条，关闭 216 条），**500 条 PR 更新**（待合并 204 条，已合并/关闭 296 条），同时发布了 **4 个 Beta 版本**。项目在代理运行时恢复、跨通道消息投递稳定性以及多槽记忆架构等关键方向上有显著推进。整体健康度较高，但 P1/P2 级 Bug 仍较多，社区对会话上下文混乱、通道回复回归等问题反映集中。

---

## 2. 版本发布

### v2026.5.31-beta.1 ~ beta.4

连续发布 4 个 beta 版本（[beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.5.31-beta.1) / [beta.2](https://github.com/openclaw/openclaw/releases/tag/v2026.5.31-beta.2) / [beta.3](https://github.com/openclaw/openclaw/releases/tag/v2026.5.31-beta.3) / [beta.4](https://github.com/openclaw/openclaw/releases/tag/v2026.5.31-beta.4)），核心改进一致：

- **Agent & CLI 运行时**：更稳健地从中断的工具调用、过期会话绑定、压缩移交、媒体投递重试中恢复（参考 #88129、#88136、#88141、#88162、#88182）
- **通道稳定性**：Telegram、WhatsApp、iMessage、Slack 渠道的消息投递更加稳定

**破坏性变更 / 迁移注意事项**：无特别说明，建议用户升级至最新 beta 以获得上述修复。

---

## 3. 项目进展

今日合并/关闭的关键 PR（基于已展示数据）：

| PR | 标题 | 状态 | 说明 |
|----|------|------|------|
| [#88873](https://github.com/openclaw/openclaw/pull/88873) | fix(agent-os): harden full-local substrate | ✅ 已合并 | 强化 Docker 本地部署环境，包括回环发布、隔离数据库、包包含等 |
| [#88504](https://github.com/openclaw/openclaw/pull/88504) | feat(memory): add multi-slot memory role architecture | 🔄 开放中 | 多槽记忆角色架构，允许内存插件组合而非覆盖，已进入审核（feature: ✨ showcase） |
| [#88859](https://github.com/openclaw/openclaw/pull/88859) | fix(mattermost): route send attachments through upload | 🔄 开放中 | Mattermost 附件上传支持，修复文件丢失问题（P1, 待维护者查看） |
| [#88820](https://github.com/openclaw/openclaw/pull/88820) | fix(diagnostics): clear embedded-run activity when recovery declares lane idle | 🔄 开放中 | 修复卡住会话恢复后诊断信息持续报错的问题（P1, 待维护者查看） |
| [#88294](https://github.com/openclaw/openclaw/pull/88294) | fix(cron): include job name when reading single-job run history | 🔄 开放中 | 修复 Cron 历史记录中显示原始 jobId 的问题 |

项目已合并 296 个 PR，整体修复方向集中在**会话状态管理、通道消息投递、诊断正确性、Cron 与子代理**等领域。

---

## 4. 社区热点

以下 Issue / PR 讨论最为活跃，反映社区核心关切：

### 🔥 [Issue #32296](https://github.com/openclaw/openclaw/issues/32296) — Agent 回复上一消息而非当前消息（会话上下文混乱）
- **评论数**：13 | 👍：1
- **影响**：P1、涉及会话状态丢失、消息混乱
- **背景**：用户报告 agent 总是回复前一条用户消息，造成对话错位。该问题自 3 月以来持续活跃，至今仍标注 `needs-maintainer-review`，社区对修复进度关注度高。

### 🔥 [Issue #87307](https://github.com/openclaw/openclaw/issues/87307) — Matrix 线程回复退化（2026.5.22）
- **评论数**：11 | 👍：1
- **背景**：升级后 Matrix 线程回复变为普通回复，`/status`、`/model` 命令无响应。用户强调这是回归问题，社区希望尽快回滚或修复。

### 🔥 [Issue #13583](https://github.com/openclaw/openclaw/issues/13583) — 强制工具调用钩子（硬门控）
- **评论数**：11 | 👍：2
- **背景**：安全/金融场景用户要求在最终回复前**机械强制**必须调用某个工具，而非依赖软提示。这是一个功能请求，已被标记为 `enhancement`，讨论热烈，可能影响未来版本路由。

### 🔥 [PR #88873](https://github.com/openclaw/openclaw/pull/88873) — 强化 Agent OS 本地 Docker 基底
- 已合并，社区反馈积极，认为是提升自托管稳定性的重要一步。

---

## 5. Bug 与稳定性

按严重程度排列（P1 > P2 > P3），标注是否已有 fix PR：

| 严重级 | Issue | 简述 | 有无 Fix PR |
|--------|-------|------|-------------|
| **P1** | [#32296](https://github.com/openclaw/openclaw/issues/32296) | Agent 回复错乱（会话上下文混乱） | 无（`needs-maintainer-review`） |
| **P1** | [#87307](https://github.com/openclaw/openclaw/issues/87307) | Matrix 线程回复退化 | 无（`needs-info`） |
| **P1** | [#83959](https://github.com/openclaw/openclaw/issues/83959) | Codex 应用服务器启动重试耗尽 | 无（`needs-live-repro`） |
| **P1** | [#86047](https://github.com/openclaw/openclaw/issues/86047) | Nextcloud Talk 会话中审批停顿导致超时 | 无（`needs-maintainer-review`） |
| **P1** | [#86996](https://github.com/openclaw/openclaw/issues/86996) | Active Memory + Codex 路径导致高延迟/超时 | 无（`needs-product-decision`） |
| **P1** | [#88020](https://github.com/openclaw/openclaw/issues/88020) | Anthropic thinking 签名无效导致硬失败（已关闭，疑似已修复） | ✅ 已关闭 |
| **P1** | [#45494](https://github.com/openclaw/openclaw/issues/45494) | Cron 任务在 LLM API 持续 500 时超时而非快速失败 | 无（`needs-maintainer-review`） |
| **P2** | [#88788](https://github.com/openclaw/openclaw/issues/88788) | 2026.5.28 镜像中 Discord 进度评论配置 schema 过期 | 无（`needs-maintainer-review`） |
| **P2** | [#85251](https://github.com/openclaw/openclaw/issues/85251) | Codex app-server 发出 turn/started 后静默，会话卡住 360s | 无（`queueable-fix`） |
| **P2** | [#85888](https://github.com/openclaw/openclaw/issues/85888) | Cron 任务在 MiniMax 高峰时段 503，手动触发成功 | 无（`linked-pr-open`） |
| **P2** | [#87616](https://github.com/openclaw/openclaw/issues/87616) | GatewayClientRequestError: LLM请求3秒超时（LM Studio） | 无（`needs-live-repro`） |

大部分 P1 问题尚未有明确修复 PR，社区期望维护者优先处理。

---

## 6. 功能请求与路线图信号

### 可能纳入下一版本的功能请求

- **[#13583](https://github.com/openclaw/openclaw/issues/13583) Pre-response enforcement hooks**：强制的工具调用/策略硬门控，已有初步讨论，被标记 `needs-product-decision` 和 `needs-security-review`，可能进入下一版本。
- **[#78308](https://github.com/openclaw/openclaw/issues/78308) Channel-mediated approval for MCP tool calls**：允许 MCP 工具通过渠道审批管道，已有 `linked-pr-open`，表明正在实现中。
- **[#8441](https://github.com/openclaw/openclaw/issues/8441) 技能配置中增加 thinking 和 model 字段**：社区长期需求，已有多处关联 PR（如 #88504 多槽记忆架构同样涉及技能配置扩展）。

### 已进入审查阶段的新功能 PR

- **[#88504](https://github.com/openclaw/openclaw/pull/88504) multi-slot memory role architecture**：改变记忆插件组织方式，支持 `memory.recall`、`memory.compaction` 等独立槽位，是记忆子系统重构的重要里程碑。
- **[#87072](https://github.com/openclaw/openclaw/pull/87072) Telegram 可选交错进度车道**：将推理文本以单独消息展示在 Telegram 中，模仿 CLI 体验，标记为 showcase。
- **[#88830](https://github.com/openclaw/openclaw/pull/88830) dreaming 候选评分层**：为 shadow trial 结果添加评分（不自动写入 MEMORY.md），是 #83719 的延续。
- **[#84758](https://github.com/openclaw/openclaw/pull/84758) 子代理执行后端placement**：允许 `sessions_spawn` 指定执行后端（如 local process），为多后端执行铺路。

### 路线图信号

- 记忆子系统的模块化（多槽）、子代理执行后端的扩展性、以及强安全门控（硬钩子）是当前三大亮点方向。
- 通道侧重视 Telegram/WhatsApp/Mattermost 的消息投递准确性，Mattermost 附件上传修复 (#88859) 正在推进。

---

## 7. 用户反馈摘要

从 Issue 评论中提炼的真实用户声音：

### 正面反馈
- **性能改进**：Beta 版本的恢复能力被部分用户肯定，特别是 CLI 运行时的中断处理（#88129 相关评论）。
- **文档更新**：PR [#88875](https://github.com/openclaw/openclaw/pull/88875) 补充 markdown 渲染器文档，社区认为“填补了空白”。

### 负面反馈 / 痛点
- **稳定性的持续担忧**：多名用户表示“每升级一个版本都担心某个通道会坏掉”（如 #87307 Matrix、#79308 Telegram 错发 chat_id）。
- **配置复杂度**：用户抱怨“插件加载静默失败消耗数小时调试时间”（[#78301](https://github.com/openclaw/openclaw/issues/78301)），希望插件加载时能给出明确错误信息。
- **性能衰减**：Codex 运行时延迟高（[#78947](https://github.com/openclaw/openclaw/issues/78947)），明明只返回“OK”却耗时 25 秒且消耗 33k tokens。
- **会话历史截断矫枉过正**：聊天历史对超过 12k 字符的助理消息强制截断（[#53242](https://github.com/openclaw/openclaw/issues/53242)），即使预算仍有富余。
- **自托管本地模型体验不佳**：LM Studio 用户反映请求极快超时（[#87616](https://github.com/openclaw/openclaw/issues/87616)），尽管已调大所有超时参数。
- **多账户场景支持不足**：Discord 多 bot 账户时斜杠命令注册缺失（[#77359](https://github.com/openclaw/openclaw/issues/77359)）。

---

## 8. 待处理积压

以下 Issue / PR 长期未获响应或处于 stale 状态，需维护者关注：

### 关键 Issue
| Issue | 创建时间 | 最后更新 | 状态 | 备注 |
|-------|----------|----------|------|------|
| [#78308](https://github.com/openclaw/openclaw/issues/78308) MCP 工具渠道审批 | 2026-05-06 |

---

## 横向生态对比

好的，作为资深技术分析师，以下是基于您提供的2026-06-01各项目动态摘要生成的横向对比分析报告。

---

### AI智能体与个人AI助手开源生态横向对比分析报告 (2026-06-01)

#### 1. 生态全景

当前，个人AI助手与自主智能体开源生态呈现出 **“繁荣与分化”** 的态势。一方面，以OpenClaw、ZeroClaw、IronClaw为代表的核心项目社区极度活跃，代码迭代和架构讨论（如统一路由、多槽记忆、定时任务管道化）频繁，表明技术正从“能跑就行”的早期阶段向体系化、稳定化、可扩展的企业级能力演进。另一方面，项目间的差异化定位愈发明显，既有追求全功能、大而全的“旗舰”框架，也有专注于特定场景（如TUI、硬件IoT）或极致稳定的“小而美”项目。社区对**会话稳定性**、**生产级部署可靠性**、**精细化的控制与安全门控**以及**更佳的交互体验**（WebUI、多模态输入）的诉求已成为普遍共识，推动整个生态向更成熟的方向发展。

#### 2. 各项目活跃度对比

| 项目名称 | Issues 更新 (新开/活跃) | Issues 关闭 | PRs 总数 | PRs 合并/关闭 | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 284 | 216 | 500 | 296 | 4个Beta | **高**：修复与演进并行，P1/P2 Bug多但修复力度大 |
| **IronClaw** | 3 | - | 25 | 7 | 0 | **高**：架构推进有力（Reborn），测试基建完善 |
| **CoPaw** | 21 | 6 | 9 | 1 | 0 | **中**：社区活跃反馈多，但PR积压与Bug修复滞后 |
| **ZeroClaw** | - | - | 93 (总) | - | 0 | **高**：架构级RFC讨论热烈，TUI与硬件拓展并进 |
| **Hermes Agent** | - | - | 50 (总) | 8 | 0 | **中高**：模型跟进快，但核心Codex稳定性问题突出 |
| **NanoBot** | 2 | - | 18 | 7 | 0 | **高**：高效的“反馈-修复”闭环，聚焦安全与稳定性 |
| **PicoClaw** | 4 | 3 | 10 | 3 | 1个Nightly | **高**：关键Bug修复迅速，社区对版本节奏有期待 |
| **Moltis** | 0 | 0 | 1 | 0 | 0 | **稳定**：单点突破，专注于会话历史管理优化 |
| **NanoClaw** | 3 | 0 | 8 | 2 | 0 | **中高**：社区挖掘出架构级稳定性风险，响应迅速 |
| **LobsterAI** | 0 | 0 | 1 | 1 | 0 | **低**：活跃度低，关键Bug修复停滞 |
| **NullClaw** | 2 | 0 | 0 | 0 | 0 | **低**：项目活跃度陷入低谷，需关注 |
| **TinyClaw** | - | - | - | - | - | **停滞**：24小时内无任何活动 |
| **ZeptoClaw** | 1 | 1 | 0 | 0 | 0 | **静默**：仅进行安全维护，开发活动停滞 |

*注：“-”表示摘要中未提供该精确数据*

#### 3. OpenClaw 在生态中的定位

- **核心参照与生态标杆**：OpenClaw是当前生态中**社区规模最大、迭代速度最快、功能最全面**的项目，其500条PR/日的活跃度无人能及。它在会话管理、通道投递、记忆架构等多条战线上同时推进，扮演着整个生态技术风向标的角色。
- **技术路线差异**：与CoPaw侧重Windows桌面、ZeroClaw探索IoT等不同，OpenClaw走的是**“全栈通用平台”**路线。其推出的“多槽记忆架构”（PR #88504）和“强制工具调用钩子”（Issue #13583）等尝试，旨在解决通用AI助手最核心、最复杂的问题，技术深度和广度领先。
- **优势与挑战**：优势在于**强大的社区驱动力和快速的功能迭代**。挑战在于，高度的活跃伴随着**P1/P2级Bug积压**（如会话上下文混乱、Matrix通道退化），部分用户已对升级后稳定性产生担忧。相比之下，NanoBot虽功能较少，但通过高效的Bug修复循环赢得了“稳定可靠”的口碑。

#### 4. 共同关注的技术方向

| 技术方向 | 涉及项目与具体诉求 |
| :--- | :--- |
| **会话与记忆管理** | **OpenClaw**（多槽记忆）；**CoPaw**（对话版本化、会话隔离）；**Moltis**（会话历史容量控制）；**ZeroClaw**（统一输出路由）；**NanoBot**（消息重复归档）；**PicoClaw**（上下文压缩显示）。**诉求**：更精细、可配置、稳定、高效的上下文管理，避免“串话”、“遗忘”和资源膨胀。 |
| **通道稳定性与交互体验** | **OpenClaw**（Telegram/Matrix通道退化）；**PicoClaw**（QQ渠道重启循环、Telegram Typing Indicator）；**Hermes Agent**（Codex集成不稳定）；**NanoBot**（WebUI白屏崩溃）。**诉求**：多平台消息投递准确、稳定，并提供良好的终端用户反馈（Visual Feedback）。 |
| **安全与权限控制** | **OpenClaw**（强制工具调用钩子）；**ZeroClaw**（MCP工具风险管控盲区、内存限制）；**NanoBot**（WebSocket Token安全、Azure AAD认证）；**CoPaw**（企业微信内存隔离）。**诉求**：引入更严格的、可编程的安全门控和精细的权限管理，以支撑企业级和多租户部署。 |
| **本地模型支持与自托管** | **PicoClaw**（LM Studio一键集成诉求强烈）；**OpenClaw**（Docker本地部署强化）；**Hermes Agent**（LM Studio用户遭遇超时问题）。**诉求**：降低本地模型使用门槛，优化自托管体验，确保在非云端环境下的可靠、高性能运行。 |
| **开发与部署体验** | **CoPaw**（技能注册困惑、文档与实际不符）；**NanoClaw**（生产环境静默故障、配置不生效）；**ZeroClaw**（TUI重连卡死）。**诉求**：更清晰准确的文档、更强的故障诊断能力、更平滑的配置和部署流程。 |

#### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 关键架构差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全功能通用平台 | 开发者、高级用户、社区维护者 | 全栈、模块化、高扩展性，侧重通用场景 |
| **ZeroClaw** | 架构探索 + IoT硬件扩展 | 创新开发者、IoT爱好者 | 重视架构RFC讨论，具备硬件（ESP32）扩展能力 |
| **IronClaw** | 企业级产品认证与集成 | 关注认证流程、企业级部署用户 | 以“Reborn”架构重构，强调第三方认证与产品化 |
| **CoPaw** | 桌面体验 + 技能生态 | Windows桌面用户、知识工作者 | 聚焦桌面端流畅度（WebUI、性能）、技能易用性 |
| **Hermes Agent** | 前沿模型（Codex）快速集成 | 紧跟模型前沿的开发者 | 紧跟OpenAI等前沿模型API，但对稳定性问题反应不够快 |
| **NanoBot** | 稳定性与安全性 | 追求稳定部署的开发者、企业用户 | 高效的“小步快跑”修复模式，以安全和Bug修复为优先 |
| **PicoClaw** | 轻量级、快速迭代 | 追求新功能、易用性的用户 | 功能相对精简，发布节奏快（Nightly），积极采纳社区反馈 |
| **Moltis** | 会话历史管理 | 深度使用、关注长对话体验的用户 | 专注单点突破，优化会话历史的存储、加载和生命周期 |

#### 6. 社区热度与成熟度

- **快速迭代与技术探索阶段（高活跃度）**：
    - **OpenClaw、ZeroClaw、IronClaw**：社区贡献、Issue讨论、PR数量均处于高位。项目处于向更成熟架构（模块化、标准化、可观测性）演进的过程中，新功能、新RFC层出不穷，但也伴随着较多的不稳定性。
- **质量巩固与优化阶段（中高活跃度）**：
    - **Hermes Agent、NanoBot、PicoClaw、NanoClaw**：社区反馈与Bug修复形成良性循环。项目主要精力投入到**修复核心Bug、提升稳定性、打磨交互体验**上。版本迭代（如有）趋于理性和稳健，是值得信赖的“中坚力量”。
- **平稳或蓄力阶段（低活跃/停滞）**：
    - **CoPaw、LobsterAI、NullClaw、TinyClaw、ZeptoClaw**：这些项目要么PR积压严重（CoPaw）、关键Bug搁置（LobsterAI），要么开发活动基本停滞（TinyClaw、ZeptoClaw）。对于潜在用户而言，选择这些项目需评估维护风险。

#### 7. 值得关注的趋势信号

1.  **AI Agent的“确定性”与“可解释性”需求增长**：从OpenClaw的“强制工具调用钩子”到ZeroClaw的“统一输出路由”，社区不再满足于“黑盒”式回复，而是要求对Agent的**行为决策和输出进行精细控制与预期管理**。这对开发者意味着在设计Agent时，需要设计明确的、可执行的控制流和策略节点。
2.  **从“功能堆叠”到“体系化重构”的演进**：ZeroClaw的RFC讨论（将Cron纳入消息管道）、OpenClaw的多槽记忆架构，都表明项目在解决复杂问题时，正从“打补丁”转向**底层架构的重新设计**。这提示开发者，当Agent应用复杂度达到一定程度后，架构上的“根因修复”比“临时规避”更具长期价值。
3.  **交互体验的“精细化”竞争**：WebUI白屏崩溃、Telegram无打字提示、cmd窗口闪烁等不再被视为小问题。用户对**UI/UX的容错性和反馈机制**提出了更高要求。AI Agent开发者应投资于提升终端用户使用的前端体验与交互反馈，这将是产品差异化的关键。
4.  **安全与合规成为核心瓶颈**：Azure AAD认证、MCP工具风险管控、企业微信内存隔离等诉求，暴露出AI Agent在**企业级部署中的安全短板**。对于任何希望拓展B端市场的项目，建立完善的身份认证、权限管理和数据隔离机制是必须攻克的关卡。
5.  **生态的“长尾”与“互操作性”**：PicoClaw等轻量级项目依然拥有忠实用户，表明市场存在**对特定场景或低资源消耗方案的长期需求**。同时，MCP协议（如NanoClaw的HTTP/SSE MCP支持）的普及，将推动不同Agent项目间的工具和插件共享，生态的互操作性将成为未来的重要竞争力。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 NanoBot 项目数据，现为您生成 2026-06-01 的项目动态日报。

---

### **NanoBot 项目动态日报 | 2026年6月1日 (周一)**

#### 1. 今日速览

今日 NanoBot 项目呈现 **中等偏高活跃度**，但核心进展主要集中于 Bug 修复与功能补全，而非突破性新功能。过去 24 小时内，共有 18 个 PR 被提交或处理，其中 **7 个已合并/关闭**，这表明贡献者团队的协作效率较高。社区在 Issues 中反馈了两个核心问题（Azure AAD 认证支持、WebUI 白屏崩溃）和一个关键 Bug（消息重复归档），均已迅速得到拉取请求的响应，形成了高效的“反馈-修复”闭环。项目健康度良好，稳定性与安全性是今日的主旋律。

#### 2. 版本发布

*   **无新版本发布。** 今日无新的 Release 产出，上述 Fix 内容预计将在下个版本中合并。

#### 3. 项目进展

今日合并/关闭的 PR 主要集中在 **安全性、会话管理、WebUI 稳定性及核心 Agent 调度** 四个方面，显著提升了项目的健壮性。

*   **安全性与漏洞修复：**
    *   `#4103` **【已合并】** 修复了 WebSocket Token 签发未授权的问题，防止短生命周期 Token 被未认证生产。 ([PR #4103](https://github.com/HKUDS/nanobot/pull/4103))
    *   `#4112` & `#4114` **【已合并】** 修复了 Heartbeat 定时任务在无任务时错误发送 “All clear.” 通知的问题，并优化了内部检查逻辑。([PR #4112](https://github.com/HKUDS/nanobot/pull/4112), [PR #4114](https://github.com/HKUDS/nanobot/pull/4114))
    *   `#4117` **【已合并】** 修复了 WebUI 中无语言标识符的代码块 (` ``` `) 导致白屏崩溃的问题。([PR #4117](https://github.com/HKUDS/nanobot/pull/4117))
*   **核心调度与业务逻辑优化：**
    *   `#4127` **【已合并】** 扩展了 `/goal` 指令的持续目标（Sustained Goal）迭代预算，优化了长任务场景下的 Agent 循环。([PR #4127](https://github.com/HKUDS/nanobot/pull/4127))
    *   `#4121` **【已合并】** 对 WebUI 聊天渲染和宿主运行时进行了整体打磨，稳定了流式输出和推理块展示。([PR #4121](https://github.com/HKUDS/nanobot/pull/4121))

这些合并推进了项目向 **更安全、更稳定、体验更流畅** 迈进，解决了数天前报告的关键问题。

#### 4. 社区热点

*   **讨论最活跃：`#4125` - Azure AAD 认证支持请求**
    *   **诉求分析：** 该 Issue (已有一个对应 [PR #4126](https://github.com/HKUDS/nanobot/pull/4126)) 讨论了关键的企业级需求：支持 Azure 基于身份的认证（托管身份、Azure CLI、服务主体）。用户痛点在于无法在启用 AAD 安全策略的 Azure 订阅中部署 NanoBot。这反映了社区对 **企业级部署和安全性** 的强烈需求，是项目从个人工具向企业服务演进的关键信号。

*   **技术讨论焦点：`#4122` - 集成本地语音识别**
    *   **诉求分析：** 这是一个功能增强 PR，提议在 WebUI 中加入录音功能，并通过 FunASR 实现本地语音转文字。虽然被打上了 `[enhancement, invalid]` 标签（可能因实现复杂度或不兼容），但引发了社区对 **多模态交互**（输入方式多样化）的兴趣，是未来路线图的一个潜在方向。

#### 5. Bug 与稳定性

以下为今日报告的 Bug，按严重程度排列：

*   **高 (High):** `#4116` **WebUI 白屏崩溃**。用户加载含有无语言标识符代码块的会话时，WebUI 完全崩溃。**已有修复 PR `#4117` 并已合并。**
*   **中 (Medium):**
    *   `#4128` **用户消息重复归档**。`retain_recent_legal_suffix` 方法存在逻辑缺陷，当尾部消息全是 assistant/tool 消息时，会将用户消息同时归档到 archive 和 kept 中，可能导致 LLM 上下文不一致。**已有修复 PR `#4129` (待合并)。**
    *   `#4111` **Heartbeat 错误通知**。在无任务时，Heartbeat 定时任务向飞书错误发送 “All clear.” 消息，造成用户困扰。**已有修复 PR `#4112` / `#4114` 并已合并。**
*   **低 (Low):** `#4077` **安全漏洞：WebSocket Token 签发缺陷**。当 `tokenIssueSecret` 为空时，Token 签发接口可被未授权访问。**已有修复 PR `#4103` 并已合并。**

#### 6. 功能请求与路线图信号

*   **高优先级信号：** **Azure AAD 认证** (`#4125`)。不仅是功能请求，更直接反映了企业级用户的需求，对应 PR `#4126` 已经就绪，极有可能被纳入下一版本。
*   **新颖的功能增强：** **WebUI 语音录制与转录** (`#4122`)。尽管 PR 被标记为 `invalid`，但它揭示了社区对“更便捷输入”的渴望，可能促使维护者探索更成熟的 WebRTC 或第三方语音 SDK 方案。
*   **安全增强：** **拒绝 MCP 不安全的 HTTP URL** (`#4123`)。这是一个待合并的防御性增强 PR，体现了项目对 **SSRF 攻击防护** 的重视，是安全路线图上的重要一环。
*   **架构演进：** **提取 `GatewayHTTPHandler`** (`#4115`)。这是一个长期运行的 PR，旨在解耦 WebUI、WebSocket 和 AgentLoop，为未来“热加载”等功能铺路。这表明项目正在为 **更模块化、更易于扩展的架构** 做准备。

#### 7. 用户反馈摘要

*   **企业用户痛点：** `#4125` 评论者明确指出，“Azure 订阅的安全策略强制禁用 API Key，转而要求 Azure Identity 认证”，这是用户在 **企业环境部署** 中面临的核心阻碍。
*   **普通用户使用体验：** `#4116` 的反馈直指 **WebUI 的基础渲染容错性不佳**，导致部分会话完全无法查看，严重影响了体验。好在已被快速修复。
*   **高级用户逻辑困惑：** `#4128` 报告者详细分析了一个微妙的 Bug，揭示了会话管理逻辑在边缘情况下的缺陷，可能导致模型“记忆错乱”。这表明核心用户对会话上下文一致性有 **很高的期望和敏锐的洞察力**。
*   **外围功能干扰：** `#4111` 反馈了 Heartbeat 功能“乱报”的问题，虽非核心功能，但错误的推送消息对用户造成了不必要的干扰。

#### 8. 待处理积压

*   **PR `#1443` (feat: decouple heartbeat reasoning from notification)**
    *   **创建时间：** 2026-03-02 ｜ **最后更新：** 2026-05-31
    *   **状态：** **待合并 (OPEN)**
    *   **分析：** 这是一个已有 **3 个月** 的老 PR，与近期修复 Heartbeat 的 PR (`#4112`) 在目标上高度相关（都是让 Heartbeat 更安静、更可控）。它提供了一个更优雅的配置方案 (`sendReasoning` 字段)。鉴于近期对 Heartbeat 的持续关注，该 PR 应被优先评估并考虑合并，以避免功能演进出现分叉。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是为您生成的 Hermes Agent 项目日报。

---

### **Hermes Agent 项目动态日报 | 2026年6月1日**

---

### **1. 今日速览**

今日项目社区活跃度极高，Issues 和 PR 的更新数量均达到 50 条，其中新议题和待合并 PR 占主导，显示项目处于快速迭代和用户密集反馈期。主要焦点集中在修复 `openai-codex`/`gpt-5.5` 的稳定性问题、增强多平台支持（如飞书、Discord、Telegram），以及围绕 Docker 环境和路径处理的 Bug 修复。尽管新版本未发布，但大量针对核心组件（`comp/agent`）和网关（`comp/gateway`）的修复与功能提案已经形成，项目健康度良好，社区参与积极。

### **2. 版本发布**

*无。*

### **3. 项目进展**

今日共有 8 个 PR 被合并/关闭，其中几个重要进展值得关注：

- **模型支持更新**：PR [#36191](https://github.com/NousResearch/hermes-agent/pull/36191) 已合并，将 OpenRouter 和 Nous 列表中的 MiniMax 模型从 `minimax-minimax-m2.7` 更新至 `minimax/minimax-m3`，并已合并相关模型列表演示。PJ [#86205](https://github.com/NousResearch/hermes-agent/pull/36205) 已打开，进一步支持最小化区域的 `minimax-m3`，包括1M上下文。

- **模型能力钩子**：PR [#23014](https://github.com/NousResearch/hermes-agent/pull/23014) 已合并，该 PR 为提供商添加了模型能力标签钩子，这是一个底层的架构改进，允许未来更灵活地声明模型能力。

- **文档与架构更新**：PR [#36203](https://github.com/NousResearch/hermes-agent/pull/36203) 已合并，增加了看板架构的文档，为项目协同子系统提供了更清晰的解释。

- **关键 Bug 修复**：PR [#36200](https://github.com/NousResearch/hermes-agent/pull/36200)、[#36199](https://github.com/NousResearch/hermes-agent/pull/36199)、[#36193](https://github.com/NousResearch/hermes-agent/pull/36193)、[#36197](https://github.com/NousResearch/hermes-agent/pull/36197) 等正在处理文件路径、模型切换、终端清理、飞书视频顺序等多项重要的 Bug 修复，项目整体稳定性和用户体验正在向前迈进。

### **4. 社区热点**

今日最热的讨论集中在 `openai-codex`/`gpt-5.5` 的稳定性问题上，引发社区广泛共鸣。

- **#33075 [CLOSED]**: [openai-codex/gpt-5.5 still unstable in Hermes v0.14.0: subagents almost always hit APIConnectionError/TTFB timeout while Codex CLI works](https://github.com/NousResearch/hermes-agent/issues/33075)
    - **热度**: 评论 14，赞 11。这是今日讨论最激烈的问题。
    - **分析**: 用户报告在 Windows 上使用 v0.14.0 版本时，`openai-codex` 子代理几乎总是出现 `APIConnectionError`/`TTFB` 超时，而官方 Codex CLI 却工作正常。该问题的广泛关注（11个赞）表明，官方工具与开源实现之间的稳定性差异是许多用户的核心痛点。社区迫切希望 Hermes 能追赶 Codex CLI 的可靠性，尤其是在网络、认证等基础连接层。

- **#13834 [OPEN]**: [Hermes openai-codex fails on same machine/network where official Codex CLI still works](https://github.com/NousResearch/hermes-agent/issues/13834)
    - **热度**: 评论 8。这是该长期问题的持续讨论，与 #33075 高度相关。
    - **分析**: 这进一步证实了 Codex 集成是社区的首要痛点。即使用户网络和机器环境无问题，Hermes 也无法成功调用 Codex。这不仅是一个 Bug，更是项目路由和认证处理上的一个信任赤字。

- **#31392 [OPEN]**: [RFC: Agent-native task relay with auto-forking subagents + async human approval gates](https://github.com/NousResearch/hermes-agent/issues/31392)
    - **热度**: 评论 7。
    - **分析**: 该 RFC 提出了增加原生任务中继系统，支持自动分支子代理和异步人工审批门。这是对现有功能（`spawn isolated subagents`）的增强，表明高级用户正在寻求更复杂、可控的执行流和工作批准机制。如果被采纳，将显著提升 Hermes 处理复杂多步骤任务的能力。

### **5. Bug 与稳定性**

今日报告的 Bug 主要集中在代理核心（`comp/agent`）、CLI 命令和 Docker 环境，按严重程度排列如下：

- **严重 (P1)**:
    - [#36151](https://github.com/NousResearch/hermes-agent/issues/36151): `bedrod_adapter` 在调用 Opus 4.8 时因发**`温度`**参数被拒绝（HTTP 400），而 `g ` 的 guard 并未应用于 Bedrock 路径。**已有相关修复讨论但无正式 PR。**
    - [#34554](https://github.com/NousResearch/hermes-agent/issues/34554) (已关闭): `claude-opus-4-8` 因 Anthropic 改变了 `thinking` 架构而 400 错误。**已作为已知问题关闭，但用户仍可能因此受影响。**

- **一般 (P2)**:
    - [#33961](https://github.com/NousResearch/hermes-agent/issues/33961): `/new`、`/clear`、`/reset` 等斜杠命令导致终端会话冻结，`Ctrl+C` 无法中断。
    - [#32423](https://github.com/NousResearch/hermes-agent/issues/32423) (已关闭): 上下文窗口在压缩中断并恢复后从 1M 错误变为 256K。
    - [#25281](https://github.com/NousResearch/hermes-agent/issues/25281): 仪表盘的“Update Hermes”按钮删除所有计划好的 cron 任务。
    - [#36201](https://github.com/NousResearch/hermes-agent/pull/36201), [#36188](https://github.com/NousResearch/hermes-agent/pull/36188): PR 正在处理 Docker 稳定性、网关优雅重启、飞书适配器、上下文窗口等问题。
    - [#36144](https://github.com/NousResearch/hermes-agent/issues/36144): 代理会话的 `HOME` 环境变量指向了 hermes 配置文件，导致工具在用户实际主目录之外查找路径。

- **内存与性能 (P3)**:
    - [#31263](https://github.com/NousResearch/hermes-agent/issues/31263): 全息内存上下文注入从未触发，导致代理记忆功能失效。
    - [#31158](https://github.com/NousResearch/hermes-agent/issues/31158) (已关闭): 看板调度器在多线程 + 子进程并发下卡死，因 SQLite WAL 缓存污染。**已标记关闭，但类似模式可能复现。**

### **6. 功能请求与路线图信号**

- **高潜力/可能纳入下一版本**:
    - **任务中继系统** ([#31392](https://github.com/NousResearch/hermes-agent/issues/31392)): 呼声很高，且与当前“子代理并行”功能互补，很可能成为下个大版本的核心特性。
    - **上下文窗口持久化** ([#36199](https://github.com/NousResearch/hermes-agent/pull/36199)): 修复 `/model` 切换后上下文窗口丢失的 PR (P2) 今日已提交。这是一个直接提升用户体验的修复，预计会被快速合并。
    - **Cron 安全** ([#36194](https://github.com/NousResearch/hermes-agent/pull/36194)): 对 cron 工具应用网关生命周期阻塞和脚本扫描，加强安全性。这在 cron 任务自动执行场景下非常重要。

- **长期或社区级需求 (P3)**:
    - **云同步** ([#20510](https://github.com/NousResearch/hermes-agent/issues/20510)): 跨设备同步配置和会话记忆的需求有 9 个赞，是许多用户期待的便利性功能，但实现复杂度高，可能被推迟到次要版本。
    - **Claude 订阅集成** ([#25267](https://github.com/NousResearch/hermes-agent/issues/25267)): 允许 Claude 订阅用户无需额外 API 密钥即可使用。若 Anthropic Codex 模式无法普及，这将是降低用户使用门槛的关键。
    - **原生移动应用** ([#11911](https://github.com/NousResearch/hermes-agent/issues/11911)): 提及度和评论数一般，但作为长期愿景，未来若移动设备使用量增长，可能被提上日程。

### **7. 用户反馈摘要**

- **痛点**:
    - **“官方行，我为什么不行？”**：用户对 `openai-codex` 的稳定性抱怨最多，尤其是在 Windows 上与官方 Codex CLI 对比时。这直接影响了核心体验，用户感觉“被抛弃”了。
    - **“Windows 适配是后妈生的”**：多个用户 (Kypc-ic、Koraji95-coder) 反馈 Windows 下的路径问题（MSYS 路径、环境变量 `%LOCALAPPDATA%`、`~/.hermes` 解析差异），表明 Windows 用户环境适配仍有显著缺口。
    - **“配置不一致”**：`env_loader` 与 `hermes config show` 读取的 `HERMES_HOME` 不一致（#31144），让用户很困惑，削弱了配置管理的可靠性。

- **满意点**:
    - **新模型支持迅速**：社区对快速跟进 MiniMax-M3 模型表示赞赏，表明项目对预发布模型的跟进速度是积极的。
    - **开发者社区活跃**：用户主动贡献 RFC ([#31392](https://github.com/NousResearch/hermes-agent/issues/31392)) 和修复 PR，证明了项目维护者与社区的良好互动。

### **8. 待处理积压**

- **超长期未响应的重要 Issue**:
    - [#19236](https://github.com/NousResearch/hermes-agent/issues/19236) (2026-05-03): Slack 发送消息无法打开 DM。已过去近一个月，虽评论不多，但功能缺失影响核心协作场景。
    - [#13142](https://github.com/NousResearch/hermes-agent/issues/13142) (2026-04-20): `execute_code` 在 Docker 后端静默失败 (`tool_calls_made: 0`)。这是一个严重的交互问题，用户将遭遇“无响应”体验而无法得知原因。长时间未修复可能影响 Docker 用户信心。
    - [#11911](https://github.com/NousResearch/hermes-agent/issues/11911) (2026-04-18): 原生移动 App 请求。尽管 P3，但这是项目路线图的重要信号，长期无响应可能挫伤移动端用户社区的积极性。

- **待合并的 PR**:
    - [#22064](https://github.com/NousResearch/hermes-agent/pull/22064) (2026-05-08): 避免启动拒绝时的 sweep 任务泄漏。PR 存在已近一个月，但作者 Warrenpoobear 的活跃度未知，可能需要维护者协助合并或重新评估。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-06-01

## 1. 今日速览
过去24小时项目保持高活跃度：新开 / 活跃 Issue 4 个，关闭 3 个；新提交 PR 10 个（待合并 7 个，已合并 / 关闭 3 个）；发布 `nightly` 构建版本一个。核心进展为 **Codex OAuth 空响应缺陷已通过 PR #2967 修复并合并**，同时 `message` 工具获得媒体附件与 Telegram 富文本投递能力（PR #2856 合并）。社区对客户端稳定性、上下文压缩显示及新提供商集成呼声较高。

## 2. 版本发布
- **nightly‑20260601**  
  `v0.2.9-nightly.20260601.ba806592`  
  自动从 `main` 分支构建，未包含破坏性变更。主要包含昨日合并的 Codex 流式文本 delta 修复（PR #2967）及其他累积改动。详见 [Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)。  
  ⚠️ 提示：此为夜间构建，可能不稳定，**生产环境请谨慎使用**。

## 3. 项目进展（已合并 / 关闭的重要 PR）
- **PR #2967** — [`fix(codex): preserve streamed output text deltas`](https://github.com/sipeed/picoclaw/pull/2967)  
  修复了 OpenAI/Codex OAuth 提供者因后端通过 `response.output_text.delta` 流式传输文本但在 `response.completed` 事件中将 `response.output` 置为 `null` 导致空响应的问题。**该 PR 已合并，对应 Issue #2674、#2953 应得到解决。**
- **PR #2856** — [`feat(message): support media attachments and Telegram rich delivery`](https://github.com/sipeed/picoclaw/pull/2856)  
  允许 `message` 工具携带单个语义化的外发负载（文本+媒体），消除 agent 必须拆分数次发送的尴尬，且 Telegram 渠道原生支持。对应 Issue #2855 已关闭。
- **PR #2980** — [`chore: gitignore debug output files`](https://github.com/sipeed/picoclaw/pull/2980)  
  清理 `.gitignore`，避免调试文件被误提交。已合并。

项目整体在 **稳定性修复**（Codex）、**消息工具增强**、**Telegram 交互优化** 三个方向取得了明确进展。

## 4. 社区热点
| 编号 | 标题 | 评论数 | 👍 | 链接 | 状态 |
|------|------|--------|----|------|------|
| #28 | Feat Request: LM Studio Easy Connect | 21 | 2 | [Issue](https://github.com/sipeed/picoclaw/issues/28) | 已关闭 |
| #2674 | Codex OAuth: empty assistant response | 7 | 4 | [Issue](https://github.com/sipeed/picoclaw/issues/2674) | 开放 |
| #2968 | /context always show Compress at: 76800 tokens | 3 | 1 | [Issue](https://github.com/sipeed/picoclaw/issues/2968) | 开放 |
| #2952 | 好久没发新版本了（含多个问题） | 3 | 0 | [Issue](https://github.com/sipeed/picoclaw/issues/2952) | 开放 |

**分析：**
- **#28** 虽然已关闭，但 21 条评论表明用户对 **一键接入本地模型（LM Studio）** 需求强烈，可能因难度较高未被实现，社区中仍有人希望接力。
- **#2674** 随着 PR #2967 合并应可关闭，但当前仍为 OPEN 状态，建议维护者尽快确认后关闭。
- **#2968** 和 **#2952** 反映了用户对 **上下文压缩显示** 和 **版本发布节奏** 的不满，后者更指出 QQ 渠道重启后循环重启的严重稳定性问题。

## 5. Bug 与稳定性
按严重程度排列（已标注是否有对应修复 PR）：

| 严重性 | Issue | 描述 | 状态 | Fix PR |
|--------|-------|------|------|--------|
| 🔴 高 | [#2674](https://github.com/sipeed/picoclaw/issues/2674) | Codex OAuth 空响应（模型实际有输出） | 开放 | ✅ PR #2967 已合并 |
| 🔴 高 | [#2952](https://github.com/sipeed/picoclaw/issues/2952) | QQ 渠道重启后再次向该渠道发消息会再次重启 | 开放 | ❌ 无 |
| 🟡 中 | [#2968](https://github.com/sipeed/picoclaw/issues/2968) | `/context` 始终显示“Compress at: 76800 tokens” | 开放 | ❌ 无 |
| 🟡 中 | [#2953](https://github.com/sipeed/picoclaw/issues/2953) | Codex 流式 delta 被忽略（与 #2674 重复） | 已关闭 | ✅ PR #2967 已合并 |

**注意**：`exec` 命令的 `actions:run` 问题在 #2952 中被提及，可能导致模型额外运行不必要命令，但细节尚不完整。

## 6. 功能请求与路线图信号
### 已明确进入路线图的特性（对应已合并/活跃 PR）
- **消息工具支持媒体附件** —— PR #2856 已合并，预计随下一版本发布。
- **Telegram 群聊回复触发 bot** —— PR #2975 开放中，`mention_only: true` 模式下回复 bot 消息视为 @提及。
- **Cron 工具增加 `get`/`update` 动作** —— PR #2977 开放，允许 agent 检查并部分更新定时任务，避免 `remove->add` 流程的副作用。

### 社区强烈需求但尚未实现
- **LM Studio“一键式”集成**（#28）：虽已关闭，但社区用户呼吁逐步简化配置。
- **OmniRoute 作为新提供商**（#2978）：刚提交 0 评论，但截图显示用户需要手动组合配置，希望官方支持。
- **技能自动跳过缺失二进制依赖**（PR #2936）：通过解析 `SKILL.md` 中的 `requires.bins` 过滤不可用技能，处于 stale 状态，但概念契合 Agent 可靠性提升。

### 版本节奏
Issue #2952 中用户表达“好久没发新版本了”，结合已有多个特性 PR 和修复 PR 待合并，下一正式版本 (v0.3.0?) 可能即将发布，建议维护者评估合并一批稳定 PR 后打标签。

## 7. 用户反馈摘要
- **Codex OAuth 用户**：对空响应非常困惑，重置 token、更换账号均无效，最终发现是流式事件处理遗漏。修复后社区表示感谢（#2953 关闭评论）。
- **MiniMax 用户（#2968）**：发现 `/context` 压缩数值始终固定为 76800，怀疑未正确读取模型 `max_tokens` 配置，期望获得动态显示。
- **QQ 渠道运维者（#2952）**：多次重启后触发无限重启，必须手动清除历史上下文才能恢复正常，严重影响生产使用。
- **版本等待者**：认为项目仍有较多待修 Bug（如 `exec` 默认不带 `actions:run`），希望维护者尽快发布新版本以解决累积问题。

## 8. 待处理积压
以下 Issue/PR 长期未获正面响应或进展，建议维护团队优先关注：

| 编号 | 类型 | 标题 | 最后更新 | 搁置天数 | 链接 |
|------|------|------|----------|----------|------|
| #2936 | PR | feat(skills): skip skills whose required binaries are missing on PATH | 2026-05-31 | 8天（stale） | [PR](https://github.com/sipeed/picoclaw/pull/2936) |
| #2906 | PR | Fix message bus backpressure handling and health visibility | 2026-05-31 | 12天（stale） | [PR](https://github.com/sipeed/picoclaw/pull/2906) |
| #2904 | PR | Fix agent loop reload and panic cleanup stability | 2026-05-31 | 12天（stale） | [PR](https://github.com/sipeed/picoclaw/pull/2904) |
| #2902 | PR | docs: add Android Termux guide | 2026-05-31 | 12天（stale） | [PR](https://github.com/sipeed/picoclaw/pull/2902) |
| #2674 | Issue | Codex OAuth empty response（fix 已合并但 Issue 未关闭） | 2026-05-31 | 36天 | [Issue](https://github.com/sipeed/picoclaw/issues/2674) |
| #2952 | Issue | 多个稳定性 & UI 问题（含 QQ 重启循环） | 2026-05-31 | 5天 | [Issue](https://github.com/sipeed/picoclaw/issues/2952) |

**提醒**：上述 stale PR 均涉及关键运行时稳定性（背压处理、agent 重载、panic 清理），长时间不合并可能积累技术债务。此外 #2674 应尽快关闭以保持 Issue 整洁。

---

*报告生成时间：2026-06-01 23:59 UTC。数据来源：PicoClaw GitHub 仓库。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 NanoClaw 开源项目分析师，根据您提供的 2026-05-31 日 GitHub 数据，我为您生成了 2026-06-01 日的项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-06-01

## 1. 今日速览

今日项目无新版本发布，但社区与开发活动异常活跃。过去 24 小时内涌现 3 个严重 Issues，均聚焦于单线程主机模型下的系统僵死与资源耗尽问题，暴露了核心架构的稳定性风险。社区对此反应迅速，贡献者提交了 8 个 Pull Requests (PRs)，其中 2 个已合并/关闭，6 个待合并。PR 内容主要针对上述稳定性问题提供了修复方案，并引入了多项新功能（如 MCP 服务器支持、技能注册等），显示了项目在主动解决生产环境痛点与拓展能力边界两方面的积极进展。总体评估：**高活跃度，重心转向稳定性加固与可靠性提升，具备较高的健康度但需紧急关注 Bug 修复。**

## 2. 版本发布

**无新版本发布。**

## 3. 项目进展

今日合入或关闭的 PR 较少，但解决的均为实际问题，体现了项目对部署和可用性的关注。

-   **已关闭 PR:** **#2658 [Actual deployment]** ，由 `cyber-chris` 提交。该 PR 虽然合并，但从标题和标签看更像是一个部署相关的操作记录。这表明项目可能正在进行针对实际部署环境的测试或配置工作。
-   **已合并 PR:** **#2648 [feat: add /upload-trace command to upload session trace to Hugging Face]** ，由 `gavrielc` 提交。此功能允许用户将会话追踪数据上传至 Hugging Face，这对于调试、模型行为分析以及社区知识共享具有重要价值，间接增强了项目的透明度和协作能力。

## 4. 社区热点

今日社区讨论的焦点不在评论数量，而在于问题的**严重性和集中度**。大多数新创建的 Issues 和 PRs 都围绕一个核心痛点展开：**系统在特定负载或并发情况下的脆弱性与不可靠性**。

-   **热点 Issue #2665 [Single-threaded host can be frozen by unbounded/synchronous ops]**：此问题揭示了项目核心架构（单线程 Node.js 事件循环）的一个根本性缺陷。如果发起一个无界的 `await` 操作或同步阻塞调用，整个主机将陷入僵死，且健康检查接口 `/health` 无法检测到这种状态。这引发了社区对系统**自恢复能力**和**监控盲区**的担忧。
-   **热点 Issue #2657 [Self-healing: supervise the OneCLI gateway dependency]**与**#2655 [OneCLI gateway hard-exits on fd exhaustion]**：这两者都与核心网关 **OneCLI** 有关，讨论了网关进程在容器内死亡或遭遇文件描述符耗尽时，外层监控和容器编排系统的失效问题，导致整个代理集群无声地瘫痪。

**分析背后的诉求：** 用户和贡献者不再仅仅满足于功能“跑得通”，而是强烈要求项目具备**生产级稳定性**。核心诉求包括：1) 避免单点故障导致全局不可用；2) 进程崩溃后应能自动恢复；3) 性能瓶颈（如文件描述符限制）需要预警和自动扩缩容机制。

## 5. Bug 与稳定性

今日报告的 Bug 均属于 **严重级别**，直接威胁生产环境的可用性。目前均有对应的修复 PR 提交，反应迅速。

| 严重程度 | Issue | 摘要 | 是否有修复 PR |
| :--- | :--- | :--- | :--- |
| **严重** | **[#2665] (Single-threaded host can be frozen)** | 单线程主机会被无界/同步操作冻结，且健康检查无法检测。这是架构级问题。 | 暂无直接 PR，但 **#2659 (fix: reap containers via host PID)** 解决的是类似主机层面的故障恢复问题，可视为间接缓解。 |
| **严重** | **[#2657] (Gateway worker dies silently)** | OneCLI 网关的 Worker 进程死在幕后，容器 `Up` 状态但 `unhealthy`，导致全服务不可用。 | 暂无直接对应 PR。但社区讨论热度高，预计将很快有提案。 |
| **严重** | **[#2655] (File descriptor exhaustion)** | OneCLI 网关因默认文件描述符限制，在突发流量下硬崩溃，导致代理服务完全中断。 | 暂无直接 PR，但问题明确，修复方式相对直接（修改 `ulimit`），预计是下一个紧急修复点。 |

此外，**PR #2659** 修复了一个重要问题：在 `docker stop/kill` 因权限问题失败时，系统会泄漏孤儿容器，此 PR 通过宿主 PID 来收割这些残留容器。

## 6. 功能请求与路线图信号

社区在修复 Bug 的同时，也在积极推动新功能，以下信号预示着近期版本可能包含的能力：

-   **PR #2662 [feat: add HTTP/SSE MCP server support]**：此功能请求将对标准 MCP 协议（Model Context Protocol）的支持从 stdio 扩展至 HTTP/SSE 传输。这表明 NanoClaw 正试图与更广泛的第三方托管服务或远程 AI 模型服务进行交互，向**开放互联**迈出重要一步，可能成为下个版本的核心特性。
-   **PR #2661 [feat: register per-group skills as Claude Code slash commands]**：此 PR 解决了组内技能无法在 Claude Code 中被自动发现为斜杠命令的问题。这显著**提升了开发者体验**，使技能的组织和使用更加直观，很可能被纳入下一次小版本更新。
-   **PR #2660 [feat: mount external symlink targets for per-group skills]**：此功能允许技能目录中的符号链接指向组目录外部的共享库，实现了技能资产的**模块化复用**，对复杂或大型项目团队尤为有用。

## 7. 用户反馈摘要

今日 Issues 和 PRs 的评论多为技术细节讨论，但从问题描述中可以提炼出真实的用户痛点：

-   **痛点一：生产环境“静默故障”，排查成本高。** 用户 @mshirel 在 **#2657** 中描述了网关 “Worker 进程默默死亡”且容器保持 `Up` 状态，这类“僵尸”状态导致监控报警失效，只能在用户大规模投诉后才能发现，运维成本极高。
-   **痛点二：默认配置脆弱，不适应生产负载。** 如 **#2655** 指出，OneCLI 网关使用默认的 1024 文件描述符限制，在稍微高一点的压力下就会崩溃。这说明默认配置偏保守，未考虑生产环境下的并发需求，用户期望开箱即用的生产级稳健性。
-   **痛点三：配置不生效，文档与实现脱节。** 如 **#2656** [fix(add-mnemon): run mnemon setup in index.ts main(), not entrypoint.sh] 所述，官方告诉用户在 `entrypoint.sh` 中添加配置，但主机实际运行时根本不会执行该文件，导致文档指导的配置根本无效。这直接反映了**文档与实际运行逻辑的不一致**，降低了用户对官方指南的信任度。

## 8. 待处理积压

目前没有发现明显被长期搁置的关键 Issue 或 PR。今日提出的 3 个严重 Issues 均是新开的，没有任何回复，属于**紧急待办**，需要项目维护者**优先关注**和回复，以稳定社区情绪并引导修复方向。

| 项目 | 链接 | 描述 | 建议行动 |
| :--- | :--- | :--- | :--- |
| **Issue #2665** | [链接](nanocoai/nanoclaw Issue #2665) | 单线程主机被冻结，无健康检查守护。 | **优先级最高**。回复社区，讨论架构评审或替代方案（如引入工作进程/看门狗）的必要性与时间表。 |
| **Issue #2657** | [链接](nanocoai/nanoclaw Issue #2657) | 依赖的网关进程死后，整个服务不可用。 | **高优先级**。需要决定是增强 Docker 的 `healthcheck` 和 `restart` 策略，还是在应用中实现更健壮的熔断机制。 |
| **Issue #2655** | [链接](nanocoai/nanoclaw Issue #2655) | 文件描述符耗尽，网关硬崩溃。 | **高优先级**。修复明确（提高软限制），需快速发布补丁，并考虑加入动态连接池管理。 |

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 NullClaw 项目数据，我为您生成了 2026 年 6 月 1 日的项目动态日报。

---

# NullClaw 项目日报 | 2026-06-01

## 1. 今日速览
今日项目活跃度较低，过去24小时内无新的Pull Request和版本发布，仅收到2个新Issue。项目核心贡献节奏有所放缓，但社区发现了两个明确的功能性Bug，涉及Telegram交互体验和核心任务调度机制。整体状态为**“稳定但需关注”**，团队应优先处理新出现的调度模块问题。

## 2. 版本发布
无

## 3. 项目进展
项目今日未合并或关闭任何重要PR，也无新代码提交。当前的核心进展集中在社区对两个新报告的Bug进行反馈与确认，尚无功能性的向前推进。

## 4. 社区热点
今日社区活跃度集中于报告Bug，暂无高讨论度的帖子。两个新Issue（#941 和 #942）虽然目前无评论，但由于其涉及Telegram核心交互和定时任务可靠性，预计会成为未来几天社区关注的焦点。
- **热点Issue分析**：用户 `weissfl` 连续提交了两个高质量Bug报告，反映出深度用户在精细使用场景（Inline Button交互、Agent定时任务）中遇到了体验断层。诉求集中于：**1）交互反馈缺失**（Typing Indicator）；**2）关键功能失效**（Agent子进程不启动）。这暴露了项目在非标准消息流和异步任务调度上的稳定性短板。

## 5. Bug 与稳定性
今日报告了2个Bug，按严重程度排列如下：

- **[高] Agent类型定时任务不触发子进程 (#941)**
    - **描述**：当创建`job_type: "agent"`的定时任务时，系统标记任务为“已完成”，但实际上从未启动Agent子进程，导致通过Telegram的交付完全失效。
    - **影响**：严重影响所有依赖定时Agent的自动化工作流，导致关键功能不可用。
    - **状态**：Open，无关联Fix PR。
    - **链接**：`nullclaw/nullclaw Issue #941`
- **[中] Telegram 内联按钮缺少“正在输入”提示 (#942)**
    - **描述**：用户在Telegram中按下`callback_query`（如`nc_choices`选择的Inline Button）时，在处理请求期间缺少Typing Indicator，导致用户无法感知系统正在工作。普通文本消息正常。
    - **影响**：影响交互体验和用户反馈，在请求处理时间较长时可能导致用户重复点击或困惑。
    - **状态**：Open，无关联Fix PR。
    - **链接**：`nullclaw/nullclaw Issue #942`

## 6. 功能请求与路线图信号
今日无新的功能请求。但Issue #941 (`Agent-type cron jobs don't spawn a subprocess`) 暴露了当前任务调度模块的潜在架构缺陷。这个问题可能成为**下一版本发布的阻塞项**，修复工作可能涉及对`schedule`模块的底层重构，并可能催生相关的回归测试。

## 7. 用户反馈摘要
今日反馈主要来自用户 `weissfl` 的两个Bug报告，反映了真实用户的使用痛点：
- **使用场景 & 痛点**：
    1.  **Telegram交互体验**：用户在使用Inline Button进行交互时，需要即时视觉反馈。当前缺失的“Typing”指示器破坏了会话连贯性。
    2.  **定时任务可靠性**：用户设置了配置正确的Agent定时任务（`delivery_mode: "always"`），并期望消息准时送达，但任务无声失败。这表明用户对“任务必须被可靠执行”有刚性需求，当前模块未能满足。
- **满意点**：无正面评论。
- **不满意点**：功能（Agent定时任务）未按预期工作，属于功能性Bug。

## 8. 待处理积压
今日无长期未响应的重要Issue或PR。两个新Issue (#941, #942) 均由同一用户贡献，且创建时间不足24小时。**建议维护者优先关注 #941**，因其属于功能失效类Bug，若长期无响应，将严重损害用户对项目调度功能的信任。
- **链接**：`nullclaw/nullclaw Issue #941`

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 | 2026-06-01

---

## 1. 今日速览

项目今日继续保持**高度活跃**状态：过去 24 小时内有 **3 条 Issues 更新** 和 **25 条 PR 更新**，其中 7 个 PR 已被合并或关闭，18 个仍处于开放待合并状态。核心团队持续推进“Reborn”架构的多项重要模块建设，包括 Slack 插件集成、触发器存储后端（PostgreSQL / libSQL）、产品认证流程迁移以及出站通信解析引擎等。同时，**夜间 E2E 测试出现失败**（#4108），需关注稳定性。依赖更新类 PR 数量较多，表明项目正积极维护生态兼容性。

---

## 2. 版本发布

**无新版本发布。**

---

## 3. 项目进展（今日合并/关闭的重要 PR）

| PR | 标题 | 状态 | 贡献者 | 关键进展 |
|----|------|------|--------|----------|
| #4263 | feat(triggers): add libsql repository | ✅ **已合并** | henrypark133 | 为 Reborn 触发器新增首个持久化后端（libSQL），标志着触发器子系统从原型走向持久化 |
| #4262 | feat(outbound): add resolution engine | ✅ **已合并** | henrypark133 | 出站通信解析引擎完成，实现候选投递对象的类型化选择逻辑 |
| #4257 | feat(reborn): wire AuthPromptView challenge enrichment + WebUI OAuth card | ✅ **已合并** | serrrfirat | 完成 GSuite OAuth、Notion MCP OAuth、GitHub PAT 三项认证流程的 UI + Rust 端打通 |
| #4033 | chore(deps): bump the everything-else group (45 updates) | ✅ **已合并** | dependabot | 大规模依赖更新，涵盖 agent-client-protocol、postgres-types 等 45 个包 |
| #4000 | chore(deps): bump serde_json | ✅ **已合并** | dependabot | serde_json 从 1.0.149 → 1.0.150 |

**项目整体推进方向：**
- **Reborn 架构**：Slack 集成、触发器持久化、产品认证流程迁移等核心模块均在本日取得实质性进展。
- **测试基建**：#4256 新增 WebUI v2 认证 E2E 测试夹具与 3 个测试场景，增强 QA 覆盖。

---

## 4. 社区热点

| 条目 | 类型 | 热度指标 | 核心诉求 |
|------|------|----------|----------|
| [#2923](https://github.com/nearai/ironclaw/issues/2923) | ISSUE（OPEN） | 💬 4 条评论 👍 1 | **stdio MCP 激活失败**：用户重新提交此前被误关闭的 Bug，强调 stdio 传输在 v0.25.0 已端到端就绪，仅激活前检查环节存在 Bug。社区对此架构边界非常敏感 |
| [#4035](https://github.com/nearai/ironclaw/pull/4035) | PR（OPEN） | 新回复 + 被依赖 | **Slack Reborn ProductAdapter 核心**：作为 #3857 的第一个可审查切片，定义了 adapter 骨架、入站标准化、出站回复渲染等，是社区关注度最高的功能 PR 之一 |

**分析**：
- #2923 反映出用户对 MCP 标准传输协议的强烈依赖，以及对 Non-maintainer 不当关闭 Issue 的不满，项目组应重视此流程问题。
- #4035 作为 Slack 集成的基石 PR，受到上下游 PR 的依赖，是近期最重要的功能推进之一。

---

## 5. Bug 与稳定性

| 严重程度 | Issue / PR | 描述 | 当前状态 |
|----------|------------|------|----------|
| **严重** | [#4108](https://github.com/nearai/ironclaw/issues/4108) | **Nightly E2E 失败** - 定时运行失败，涉及 extensions 测试 | ⚠️ 无关联 fix PR，待排查 |
| **中** | [#2923](https://github.com/nearai/ironclaw/issues/2923) | stdio MCP 激活失败 - 激活前检查环节存在 Bug | 🔄 重新打开中，无 fix PR 链接 |
| **低** | #4035, #4266, #4184 等开放 PR | 虽为功能 PR，但均标注 risk: low，代码审查尚未提出未解决 Bug | ✅ 正常审查中 |

> **特别关注**：#4108 的 E2E 失败未关联任何 Issue 或 fix PR，建议立即分配责任人排查。

---

## 6. 功能请求与路线图信号

| 功能/需求 | 相关 PR/Issue | 可能被纳入版本 | 说明 |
|-----------|----------------|----------------|------|
| **Slack Events API 主机入口** | [#4272](https://github.com/nearai/ironclaw/pull/4272) | v0.26+ | 新增 Slack 签名验证、URL 验证等，是 #3857 的一部分 |
| **GitHub 原生 SSO** | [#4229](https://github.com/nearai/ironclaw/pull/4229) | v0.26+ | WebUI v2 新增 GitHub OAuth，与已有的 Google SSO 对称 |
| **PostgreSQL 触发器仓库** | [#4270](https://github.com/nearai/ironclaw/pull/4270) | v0.26+ | 第二个触发器持久化后端，与 libSQL 并存 |
| **统一差异预览** | [#4184](https://github.com/nearai/ironclaw/pull/4184) | v0.26+ | 为 write_file / apply_patch 生成 diff 预览，改善用户反馈 |
| **产品认证账户投射到运行时** | [#4239](https://github.com/nearai/ironclaw/pull/4239) | v0.26+ | 关闭 #4238，确保 product-auth 与 runtime 两套凭证存储不漂移 |

**路线图信号**：大量 PR 聚焦“Reborn”架构下的**认证、触发器持久化、第三方集成（Slack/GitHub）**，表明 v0.26 可能是一个以产品认证与插件生态为核心的大版本。

---

## 7. 用户反馈摘要

从 #2923 的评论中提炼：

> **“Stdio is wired end-to-end in v0.25.0 — the bug is strictly in the activation pre-flight.”**  
> 用户明确指出 stdio 传输本身已完整实现，仅激活前检查环节存在逻辑 Bug。此前 Issue 被 Non-maintainer 以“stdio 不受支持”的评论错误关闭，引发了用户的流程不满。

**隐含诉求**：
- 希望维护团队对传输类型支持有更清晰、官方的文档说明。
- 希望 Issue 关闭的权限和审核流程更严谨，避免被非核心贡献者误操作。

---

## 8. 待处理积压

| 条目 | 类型 | 创建时间 | 最后更新 | 建议行动 |
|------|------|----------|----------|----------|
| [#2923](https://github.com/nearai/ironclaw/issues/2923) | ISSUE（OPEN） | 2026-04-24 | 2026-05-31 | 已重新打开，但无 fix PR。建议核心维护者评估 stdio 激活前检查的修复方案并指派 |
| [#4002](https://github.com/nearai/ironclaw/pull/4002) | PR（OPEN） | 2026-05-24 | 2026-05-31 | Actions 依赖更新（16个包）已搁置 8 天，建议关注合并冲突或审查风险 |
| [#4001](https://github.com/nearai/ironclaw/pull/4001) | PR（OPEN） | 2026-05-24 | 2026-05-31 | Tokio 生态依赖更新（7个包），同样搁置 8 天，建议合并 |
| [#4108](https://github.com/nearai/ironclaw/issues/4108) | ISSUE（OPEN） | 2026-05-27 | 2026-05-31 | Nightly E2E 失败，无任何关联 PR 或人，建议立即分配责任人 |

---

*本日报由 AI 自动生成，基于 github.com/nearai/ironclaw 公开数据。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，这是根据您提供的 LobsterAI 项目数据生成的 2026-06-01 项目动态日报。

---

# LobsterAI 项目日报 | 2026-06-01

## 1. 今日速览

项目今日整体活跃度较低，过去 24 小时无新 Issue 产生，也无新版本发布。社区贡献以代码清理和优化为主（PR #2080 已合并），但遗留一个已创建近两个月的定时任务幽灵会话 Bug（PR #1465）仍处于待合并的停滞状态，需要维护者介入评估。项目当前处于小幅迭代与积压清理的平稳期。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并/关闭的重要 PR：

- **[PR #2080] [CLOSED] chore: optimize kits and upload file ui**  
  作者：fisherdaddy  
  该 PR 涉及 `renderer`、`docs`、`main`、`cowork` 四个模块，主要对 kits（工具包）和文件上传界面进行了代码优化（chore）。已合并，无破坏性变更。  
  https://github.com/netease-youdao/LobsterAI/pull/2080

整体来看，项目在 UI/UX 细节和代码结构上有所改进，但欠缺核心功能或重大 bug 修复的推进。

## 4. 社区热点

今日无高互动、多评论的 Issue 或 PR。目前长期未响应的 PR #1465 是唯一可能引起社区关注的话题（见下文 Bug 部分），但尚未形成活跃讨论。

## 5. Bug 与稳定性

今日未报告新 Bug。但存在一个重要的 **待处理 Bug**（已由 PR 提出修复方案）：

- **[PR #1465] [OPEN] [stale] fix: 已删除的定时任务重启后作为幽灵会话重新出现**  
  严重程度：**高** – 影响数据一致性与用户信任。问题根因是删除定时任务时未清理本地 SQLite 中关联的会话记录，重启后任务以空内容的幽灵会话重现。PR 已创建 58 天，且标记为 stale，需维护者尽快评审合并。  
  https://github.com/netease-youdao/LobsterAI/pull/1465

## 6. 功能请求与路线图信号

今日无新提出的功能请求。从已关闭的 PR #2080 内容看，项目团队当前关注点仍在 UI 优化与代码清洁上，未透露下一版本的功能规划信号。

## 7. 用户反馈摘要

由于今日无新 Issue 评论，用户反馈主要来源于 PR #1465 的背景描述：用户删除定时任务后，重启应用发现任务以空会话形式再次出现，反复操作无效。该问题直接影响了定时任务功能的实用性，用户期待彻底的数据清理逻辑。这也是社区对数据持久化可靠性提出的明确诉求。

## 8. 待处理积压

需维护者重点关注以下长期未响应的重要 PR：

- **[PR #1465] [stale] fix(scheduled-tasks): 已删除的定时任务重启后作为幽灵会话重新出现**  
  创建时间：2026-04-04 | 最后更新：2026-05-31  
  持续 58 天未合并，已进入 stale 状态。若放任不管，该 Bug 将继续影响体验并增加后续回归风险。建议尽快评审、测试并合并。  
  https://github.com/netease-youdao/LobsterAI/pull/1465

当前无其他积压的高优先级 Issue 或 PR。

---

**项目健康度评估：** 3.5/5（代码优化持续推进，但关键 Bug 修复停滞，社区活跃度偏低）。建议维护者优先处理 PR #1465，并鼓励贡献者提交新 Issue 以维持项目活力。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 Moltis 项目 2026-06-01 日报。

---

### Moltis 项目日报 - 2026-06-01

#### 今日速览

项目今日活跃度中等偏静，24小时内无新 Issue 产生，也无 PR 被合并。项目的核心进展集中于一个针对会话历史处理的重要 PR（#1089），该 PR 旨在提升系统在面对大型会话历史时的稳定性和资源利用效率。开发者侧活跃度较低，但技术侧有明确推进，整体项目健康度稳定，处于蓄力阶段。

---

#### 项目进展

**核心进展：会话历史处理机制优化**

今日项目的主要推动来自一个开放中的 Pull Request。

- **[PR #1089] Cap persisted tool results before rehydration** （待合并）
    - **作者**: s-salamatov
    - **状态**: 开放中，24小时内创建
    - **摘要**: 该 PR 解决了在将持久化的会话历史“重新水合”（rehydrate）为 `ChatMessage` 对象时，`tool` 和 `tool_result` 内容可能无限增长的问题。
    - **意义**: 此改进对系统的**鲁棒性和内存管理**至关重要。它确保了包括常规对话、流式对话、压缩后重试、提示检查、记忆轮次以及基于 LLM 的压缩提示在内的多种场景下，历史消息不会因工具调用结果过大而导致性能下降或异常。这标志着项目在对大型复杂对话的支持上迈出了坚实的一步。

---

#### 社区热点

今日无活跃讨论的 Issues，社区讨论的焦点集中在唯一开放的 **PR #1089** 上。

- **PR #1089**（链接：moltis-org/moltis PR #1089）
    - **热点分析**: 虽然该 PR 尚无评论，但其技术内容触及了 AI Agent 系统的一个核心痛点：**会话历史的长期管理与性能平衡**。
    - **背后诉求**: 社区（尤其是重度用户）对项目能否处理长时间、高复杂度对话的能力存在潜在担忧。该 PR 直接回应了这种担忧，通过“容量限制”（Cap）机制，在不丢失核心信息的前提下，防止历史数据膨胀。这反映了用户对**稳定、高效、可扩展**的 AI 助手体验的深层需求。

---

#### Bug 与稳定性

今日未报告新的 Bug 或稳定性问题。值得关注的是， **PR #1089** 本质上是针对一个**隐性的、与长期稳定性相关的潜在 Bug 或性能瓶颈**的预防性修复。它虽未被报告为 Bug，但它所解决的问题（会话历史因工具结果过大导致性能问题）是用户在实际使用中可能遇到的稳定性和回归问题。

-   **严重程度**: 中等（长期使用后可能影响性能）
-   **修复状态**: 已有 Fix PR (#1089) 待合并。

---

#### 功能请求与路线图信号

今日无新的功能请求。然而， **PR #1089** 可被视为对“会话历史管理”这一长期路线图功能的**基础设施优化**。它不属于新增用户可见功能，但却是支撑未来更强大功能（如长上下文记忆、更复杂的工具调用链）的基础。该 PR 的合入将降低后续开发的风险，并可能为 **支持更大规模的记忆或对话容量** 奠定基础。

---

#### 用户反馈摘要

今日无直接的用户评论。但从 **PR #1089** 的摘要内容，我们可以推断出用户在使用过程中的潜在痛点：

-   **痛点**: 当与 AI 助手进行长时间、涉及多次工具调用的对话后，历史记录可能变得异常庞大，导致响应变慢或出现超时错误。
-   **使用场景**: 处理复杂数据报表、进行多步骤的代码调试、需要回顾历史工具调用结果的深度工作流。
-   **用户期望**: 对话历史应能自动进行“清洁”，在保留可用信息的同时，避免无意义的冗余数据拖慢系统。

---

#### 待处理积压

今日最需要维护者关注的积压项为 **PR #1089**。

-   **首要关注**: **[PR #1089] Cap persisted tool results before rehydration**（链接：moltis-org/moltis PR #1089）
    -   **重要性**: 高。该项目是提升生产环境下稳定性的关键补丁。
    -   **当前状态**: 已创建，需要 Code Review 和测试。
    -   **提醒**: 建议维护者尽快安排 review，确认其与现有压缩、记忆等机制的兼容性，并组织相关测试，以便尽早合并，避免后续社区用户遇到相关的性能问题。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 2026-06-01

## 1️⃣ 今日速览

过去 24 小时项目活跃度处于 **高位**。共处理 27 条 Issues（新开/活跃 21 条，关闭 6 条）和 9 条 PR（待合并 8 条，已合并/关闭 1 条）。无新版本发布。社区反馈集中在 **Windows 桌面端体验**（cmd 窗口闪烁、MCP 进程积累）、**定时任务/会话隔离**以及 **技能管理** 等方向。多个关键 Bug 已有对应修复 PR 提交，整体修复节奏尚可，但 PR 积压数量较大，需加快合并进度。

## 3️⃣ 项目进展（已合并/关闭的重要 PR）

- **PR #4810** `[Under Review] feat(console): improve chat slash skill suggestions` — **已合并/关闭**。优化了聊天输入框的斜杠技能提示：仅显示当前 Agent 可用技能、限制最多 5 项并支持滚动。该功能提升了技能发现效率。  
  链接：https://github.com/agentscope-ai/QwenPaw/pull/4810

## 4️⃣ 社区热点

| Issue / PR | 评论数 | 点赞 | 核心诉求 |
|------------|--------|------|----------|
| **#4789** [CLOSED] 希望对话可删除/回退 | 8 | 1 | 用户要求像 Trae 一样精细管理每次对话（含文件回退、二次确认），期望打通本地目录而非仅沙箱 |
| **#4653** [CLOSED] 定时任务与用户消息共享 session 导致中断 | 8 | 0 | 定时任务与用户消息同 session 时，用户新消息会打断定时脚本执行 |
| **#4808** [OPEN] Agent `person_stat_skill` 不存在 | 6 | 0 | 按照文档编写 SKILL.md 并命中后提示不可用，反馈配置正确但 Agent 无法加载 |

- **#4789** 虽已被关闭，但用户“照抄 Trae”的强烈诉求反映了社区对对话版本化管理的巨大期待，可能成为后续功能的重点方向。  
- **#4653** 暴露了定时任务的核心设计缺陷，已关闭但需防范类似问题再次出现。  
- **#4808** 的持续开放表明技能注册机制仍存在文档/实现不一致的问题，影响用户信任。

## 5️⃣ Bug 与稳定性（按严重程度排序）

| 严重程度 | Issue | 描述 | 关联修复 PR |
|----------|-------|------|-------------|
| **🔴 严重** | **#4842** | 配置 MCP 工具后每个 Agent 实例产生独立 MCP 服务进程，300+ Agent 时资源耗尽 | 无 |
| **🔴 严重** | **#4837** | v1.1.9 频繁返回系统级 fallback "无法处理您的问题"，非 Agent 真实回复 | 无 |
| **🟠 中等** | **#4835** | `jobs.json` 中一个无效 job 导致整个工作区无法启动 | 无 |
| **🟠 中等** | **#4834** | MCP 服务进程在重启后不清理，累计多余进程拖慢控制台加载 | 无 |
| **🟠 中等** | **#4824** | ACP 协议版本号格式不匹配，`delegate_external_agent` 报 Internal Error | 无 |
| **🟠 中等** | **#4811** | 消息中包含内联 `source` URL 时压缩失败，`AttributeError: 'str' object has no attribute 'get'` | **PR #4820** |
| **🟡 普通** | **#4818** | Cron agent 设置 `share_session=true` 时执行轨迹为空，实际未执行 | **PR #4822** |
| **🟡 普通** | **#4832** | Windows 下 shell 命令执行时 cmd 窗口闪烁（与 #4829 重复） | 无（但 #4829 已关闭） |
| **🟡 普通** | **#4839** | Windows pip 升级留下 `~` 前缀的陈旧技能目录，导致技能池脏数据 | 无 |
| **🟡 普通** | **#4666** | 新建会话后 Models 配置页面丢失且无法加载，需重启 | 无 |

- 已有修复 PR 的 Bug：**#4811**（PR #4820）、**#4818**（PR #4822）、**#4807**（PR #4847）。  
- **Windows 桌面端** 出现多个相关 Bug（#4832、#4834、#4839、#4842、#4844），建议维护者集中资源专项优化。

## 6️⃣ 功能请求与路线图信号

| Issue | 功能要点 | 潜力评估 |
|-------|----------|----------|
| **#4789** | 对话版本化管理（删除/回退副本地文件） | 需求强烈（8评论，1👍），但已关闭，可能需重新开启 |
| **#4830** | Desktop 输出路径自动生成可点击链接 | 体验优化，实现成本低 |
| **#4831** | Docker 镜像预装 `psycopg2-binary`、`pytz`、`mootdx` | 减少容器重建后脚本失效 |
| **#4836** | 工具按需加载，减少初始上下文 55-65% token 开销 | 对工具丰富场景有巨大价值，建议纳入下一版本 |
| **#4838** | 支持工具执行后抑制 Agent 最终文本回复（静默工具模式） | 适合需要纯工具输出的 Channel 场景 |
| **#4840** | 对话窗口添加思考强度等级选择器 | 借鉴 OpenClaw 设计，提升用户体验 |
| **#4841** | 第三方技能提案 "Before You Build" | 社区贡献，可丰富技能生态 |
| **#4843** | 可配置聊天模式：Interrupt / Queue / Insert | 细粒度控制并发消息，匹配企业级需求 |
| **#4845** | 企业微信频道内存隔离（防止 prompt 注入窃取聊天记录） | **安全相关**，亟需响应 |

- 当前已有 **PR #4821**（飞书群组会话共享）和 **PR #4822**（修复 cron share_session 问题）推进会话隔离方面的改进，但不完全覆盖 #4845 的安全隔离诉求。

## 7️⃣ 用户反馈摘要

- **频繁 cmd 窗口闪烁**：多位 Windows 用户（@yoDIan2、@felixphong）反映 Agent 执行 shell 命令时屏幕闪烁，严重影响连续操作场景。用户期望后台静默执行（#4832 / #4829）。
- **定时任务中断**：用户 @feng183043996 详细记录了定时任务被用户消息打断的日志，并提供复现步骤和日志证据，反馈质量较高（#4653、#4649、#4835、#4834 均由同一作者提出，显示该场景下的持续痛点）。
- **技能注册困惑**：用户 @jiadong696 严格按照文档编写 SKILL.md 但 Agent 报错 `person_stat_skill not exists`，其他用户也有类似困惑，说明技能发布/注册流程的文档或实现存在盲区（#4808）。
- **升级后 fallback 频率陡增**：用户 @Lukaschen1986 反馈 v1.1.9 升级后系统级 fallback 消息“无法处理您的问题”频繁出现，但 Agent 本身能正常回答。推测为后端超时或流式处理缺陷（#4837）。
- **ACP 协议版本不匹配**：用户 @jianchuan3 使用 QwenPaw 连接 Claude Code via ACP 时遇到格式冲突，提示内部错误，反映跨代理协议兼容性问题（#4824）。

## 8️⃣ 待处理积压

| Issue / PR | 创建时间 | 状态 | 原因 / 提醒 |
|------------|----------|------|-------------|
| **#4433** (PR) | 2026-05-15 | OPEN | 添加 token 使用信息输出，已审查 17 天未合并。涉及用户体验改进，建议尽快合并或给出反馈 |
| **#4737** (PR) | 2026-05-28 | OPEN | Telegram 频道工具审批交互卡，还有评论未合并；需要继续审查 |
| **#4808** (Issue) | 2026-05-29 | OPEN | 技能无法使用，4 天无维护者回复，用户困惑加剧 |
| **#4666** (Issue) | 2026-05-25 | OPEN | 新建会话后 Models 配置丢失，持续 7 天未修复，严重影响使用 |
| **#4841** (Issue) | 2026-05-31 | OPEN | 第三方技能提案，维护者尚未回应，可能影响社区贡献积极性 |
| **#4844** (Issue) | 2026-05-31 | OPEN | Windows 上浏览器进程和临时目录锁残留，还无修复计划 |
| **#4649** (Issue) | 2026-05-24 | CLOSED（但修复不彻底） | 孤儿 cron 作业清理问题，虽已关闭，但 #4835/#4834 显示相关隐患仍存在 |

---

_分析师备注：_ 项目社区反馈活跃，Bug 修复和功能请求并进。建议下一阶段优先处理 **Windows 桌面基础体验**（cmd 窗口、MCP 进程泄漏、浏览器残留）、**定时任务隔离** 以及 **技能注册可靠性**。同时关注 #4433（token 可见性）、#4841（社区技能）等长期未处理事项，以维持贡献者信任。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

## ZeptoClaw 项目动态日报 — 2026-06-01

### 1. 今日速览
过去 24 小时项目活动量极低，仅处理了 1 个安全扫描相关的 Issue，无新 Pull Request 提交或合并，亦无新版本发布。项目整体维护节奏趋缓，但安全类任务仍被及时关闭，表明代码合规流程仍在正常运行。  
**活跃度评估：** ⭐（低），仅限维护性操作。

### 2. 版本发布
无新版本发布。

### 3. 项目进展
- **无重要 PR 合并或关闭。** 今日没有任何 Pull Request 操作，项目核心功能推进停滞。

### 4. 社区热点
唯一活跃的 Issue 为 **#609**（已关闭），内容为全仓库 Codex 安全扫描，聚焦 webhook 身份路由的准入控制流程。该 Issue 由作者 `daneschneider-oai` 发起，获得 1 条评论，无明显社区讨论热度。  
- **链接：** [Issue #609](https://github.com/qhkm/zeptoclaw/issues/609)  
- **分析：** 该 Issue 系自动化安全扫描任务，非用户自发讨论，社区互动几乎为零。

### 5. Bug 与稳定性
今日无新 Bug 报告、崩溃或回归问题。项目稳定性未收到负面反馈。

### 6. 功能请求与路线图信号
今日未收到任何新功能请求。结合已有 PR 与 Issue，暂无明确信号指向下一版本规划。

### 7. 用户反馈摘要
今日无任何用户痛点或使用场景讨论。唯一 Issue 为维护性操作，未体现用户满意/不满意信息。

### 8. 待处理积压
当前无长期未响应的重要 Issue 或 PR。项目积压情况健康，无需要特别提醒维护者关注的项目。

---

**总体结论：** 项目在当日处于静默期，安全合规任务正常闭环，但开发活动陷入停滞。建议关注后续是否有新功能或社区讨论出现。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 ZeroClaw (github.com/zeroclaw-labs/zeroclaw) 数据生成的 2026年6月1日 项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-06-01

## 今日速览

过去 24 小时内，ZeroClaw 项目保持极高活跃度，累计处理 93 条 Issue 与 PR 更新。值得注意的是，社区讨论高度集中在架构性改善上，包括统一输出路由模型（RFC #6969）和将定时任务纳入消息管道（RFC #6954），预示着项目正从功能堆叠迈向体系化重构。同时，**zerocode TUI** 的集成作为 v0.8.0-beta-2 的核心预发布分支（PR #6848），合并了大量涉及核心、通道、提供方的改动，风险高但进展显著。此外，来自 @Rhoahndur 的硬件模块（ESP32 智能房间）多组 PR 的提交，展示了项目在物联网（IoT）领域的扩展尝试。

## 版本发布

- **无新版本发布。** 社区正密切关注 PR #6848，该分支将作为 **v0.8.0-beta-2** 预发布版本的基础。

## 项目进展

- **zerocode TUI 与 beta-2 集成进行时**：核心集成 PR **#6848**（[PR #6848](zeroclaw-labs/zeroclaw PR #6848)）在持续演进。今日合并了修复 PR **#7029**（[PR #7029](zeroclaw-labs/zeroclaw PR #7029)），修复了 `zerocode` 在设置完成后无法刷新空状态的问题。这表明 TUI 的打磨已进入细节完善阶段。
- **硬件能力拓展**：来自 @Rhoahndur 的多个 PR 被提交，标志着 ZeroClaw 的硬件控制能力取得阶段性进展。
  - 新增 **ESP32 模拟器示例**（PR #7048），为在没有实体硬件的情况下进行开发测试提供了基础。
  - 修复了 `hardware_capabilities` 工具中**丢失设备和描述信息**的问题（PR #7047）。
  - 引入了**开发模拟功能**（PR #7046），允许在 `/tmp/zc-sim-*` 路径下绑定串口进行模拟。
  - 新增 **“智能房间”具名设备工具**（`set_device`/`read_device`），并完善了外设工具的加载与注册逻辑（PR #7045）。
- **通道层优化与聚合**：PR **#7044**（[PR #7044](zeroclaw-labs/zeroclaw PR #7044)）被合并，将冗长的通道功能列表提取为 `channels-all` 聚合特性，简化了编译配置，是提升开发者体验的积极步骤。

## 社区热点

今日讨论最激烈的议题集中于项目架构设计，背后反映了用户对更精细控制能力和更稳定运行基线的迫切需求。

1.  **统一输出路由模型（RFC #6969）**：由 @mov-xound-glitch 提出的 RFC **#6969**（[Issue #6969](zeroclaw-labs/zeroclaw Issue #6969)）是今日最受关注的设计提案之一。该提案旨在解决用户无法控制“回复如何、在哪里被发送”的痛点。用户强烈渴望恢复类似 Letta 中基于用户指令或偏好的动态路由能力，例如“晨报发语音到Telegram，代码文本发到Slack”。
2.  **定时任务纳入消息管道（RFC #6954）**：同为 @mov-xound-glitch 提出的 RFC **#6954**（[Issue #6954](zeroclaw-labs/zeroclaw Issue #6954)），直指当前定时任务（Cron Job）绕过核心消息管道的根本性缺陷。该提案被提及可一举解决 #6037、#6105 等系列相关 Bug，显示了社区对系统性根因修复的期待。
3.  **状态性列表的 Bug（Issue #7043）**：最新用户 @singlerider 报告的 Bug **#7043**（[Issue #7043](zeroclaw-labs/zeroclaw Issue #7043)）指出，在守护进程关闭或重启后，`zerocode` TUI 会永久性卡死且无法重连。尽管评论数尚少，但其对 TUI 用户造成的严重阻塞（S1级），已被标记为亟待解决的问题。

## Bug 与稳定性

今日报告的 bug 主要集中在 **TUI 稳定性** 和 **工具控制精确性** 方面。

- **严重（S1 - Workflow Blocked）**：
  - **zerocode TUI 永久卡死**（Issue #7043）：Daemon 关闭后 TUI 无法重连。**尚无关联修复 PR。**
  - **context_aware_tools 配置字段失效**（Issue #6720）：该配置虽能解析，但代码中从未读取，功能完全无效。**尚无关联修复 PR。**

- **中等（S2/S3 - Degraded Behavior）**：
  - **风险配置无法限制 MCP 工具**（Issue #6876）：`risk_profile.allowed_tools` 设置对 MCP 工具无效，存在安全管控缺口。**尚无关联修复 PR。** 相关增强（Issue #6914）正在讨论。
  - **Telegram 群组中回复不响应**（Issue #5866）：当设为 `mention_only=true` 时，回复机器人消息不会触发响应，影响正常对话流程。**尚无关联修复 PR。**

## 功能请求与路线图信号

近期 RFC 和 Feature 请求指向了三大方向，其中 **统一输出路由** 和 **计算机使用支持** 呼声最高，最有可能进入下一个里程碑。

- **高优先级路线图候选**：
  - **计算机使用（Computer-Use）**（Issue #6909）：类似 OpenAI Codex 的屏幕截图与键鼠控制能力。该功能将极大拓宽 ZeroClaw 在自动化场景的应用，目前已有 RFC 提案，讨论积极。
  - **统一输出路由模型**（RFC #6969）: 已关联 PR #7020（静态输出模态偏好），显示出从讨论走向实现的可能性。
  - **技能作用域的工具激活**（Issue #6915）和 **Shell 子进程内存限制**（Issue #6916）：@alex-nax 的系列提案专注于安全性和运行时控制粒度，是实现企业级部署的关键。

- **等待维护者审阅**：
  - **解耦内存策略层**（Issue #6850）：引入 `MemoryStrategy` trait 以实现可插拔的策略，背后是希望获得更好的长期记忆管理。此 RFC 处于 `needs-maintainer-review` 状态，等待项目核心维护者的决策。

## 用户反馈摘要

- **向好趋势**：
  - 用户 @mov-xound-glitch 表示刚从 Letta 迁移到 ZeroClaw，这证明项目对前 Letta 用户具有吸引力。
  - 社区对 RFC 提案（#6954, #6969）的技术方案质量认可度高，讨论聚焦于实现细节而非否定提案本身。
- **核心痛点**：
  - **灵活性与控制力不足**：多位用户（@mov-xound-glitch, @databillm, @leonardorey1992）提出的诉求一致：希望获得更精细的控制能力，包括输出路由、模型推理参数、API Key 管理等。
  - **安全管控盲区**：用户 @perlowja 发现了 MCP 工具不受 `allowed_tools` 限制的安全隐患，这是企业级部署的关键顾虑。
  - **TUI 不稳定**：用户 @singlerider 遇到的 TUI 卡死问题是目前最直观的负面体验。

## 待处理积压

以下 Issue/PR 长期未获得核心维护者的有效响应或处于 Blocked 状态，可能导致社区贡献者流失或用户问题积压。

- **RFC: 共享回复消息构建器** (PR #6883)：此 RFC 旨在解决代码重复问题，逻辑清晰且实现成本低，但已提交9天仍无维护者回复。
- **Bug: Gemini CLI OAuth 不可用** (Issue #4879)：严重程度为 S1，影响了部分用户使用 Gemini 通道，且已有 2 个赞，但自 3 月底报告以来长期处于 OPEN 状态。
- **PR: 构建 ESP32 示例** (PR #6148)：作者 @Rhoahndur 从该大型 PR 中拆解出多个小 PR 提交，但原 PR 仍处于 OPEN 且标记为 `needs-author-action`。维护者需要关注并协调处理，避免贡献者的努力被搁置。
- **RFC: 解码内存策略层** (Issue #6850)：已被标记为 `needs-maintainer-review`，是重要的架构改进提案，需尽快确定是否纳入路线图。

---

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*