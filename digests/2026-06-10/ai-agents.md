# OpenClaw 生态日报 2026-06-10

> Issues: 442 | PRs: 488 | 覆盖项目: 13 个 | 生成时间: 2026-06-10 02:43 UTC

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

# OpenClaw 项目日报 — 2026-06-10

## 今日速览
项目持续保持极高活跃度：过去 24 小时处理 **442 条 Issue**（新开/活跃 314 条，关闭 128 条）和 **488 条 PR**（待合并 355 条，合并关闭 133 条），发布两个版本（正式版 + 预览版）。社区围绕工具调用文本泄漏、Codex 会话回归、Matrix 线程回复等关键问题展开了激烈讨论。多场重要修复（iMessage 传输加固、Codex 压缩所有权等）已完成合并，同时涌现一批面向语音通话和 UI 改进的大型特性 PR。

## 版本发布

### v2026.6.5（正式版）& v2026.6.5-beta.6
两个版本包含相同的更新亮点：

- **QQBot**：现在会在原生推送前剥离模型推理/思考框架，防止原始 `<thinking>` 内容泄露到频道回复中（#89913, #90132，感谢 @openperf）。
- **MCP 工具结果**：强制对 `resource_link`、`resource`、`audio`、畸形图片及未来未定义类型进行合规化处理，避免非法载荷传递到渠道。
- 无破坏性变更记录，升级前建议查阅 `CHANGELOG.md` 确认完整改动。

> 发布链接：[v2026.6.5](https://github.com/openclaw/openclaw/releases/tag/v2026.6.5) | [v2026.6.5-beta.6](https://github.com/openclaw/openclaw/releases/tag/v2026.6.5-beta.6)

## 项目进展
今日合并/关闭的重要 PR 集中在核心稳定性与渠道支持上：

- **Codex 会话压缩所有权修复**（[PR #91590](https://github.com/openclaw/openclaw/pull/91590)）— 修正 Codex 与本地上下文引擎同时活跃时压缩冲突的问题，确保预算压缩由拥有引擎主导，Codex 仅作有限次生调用。
- **iMessage 发送传输加固**（[PR #91783](https://github.com/openclaw/openclaw/pull/91783)）— 新增 `sendTransport` 配置（auto / bridge / applescript），停止监控线程复用长连接发送回复，避免连接泄漏。
- **iMessage 启动诊断**（[PR #91785](https://github.com/openclaw/openclaw/pull/91785)）— 为回显/自聊天丢弃的行添加安全级别日志，便于排查入站消息丢失。
- **Cron 单次任务禁用唤醒回退**（[PR #91811](https://github.com/openclaw/openclaw/pull/91811)）— 当 `runHeartbeatOnce()` 返回 `skipped: disabled` 时，改为队列心跳请求而非直接标记跳过，确保单次任务不会意外被禁用。
- **WebChat 延迟思考重载**（[PR #91810](https://github.com/openclaw/openclaw/pull/91810)）— 修复运行结束时会话已包含推理内容但最终回复仅含可渲染文本导致的重绘丢失。

整体而言，项目在 **渠道兼容性**、**会话状态正确性**、**OOM/超时弹性** 方面迈出了稳健一步。

## 社区热点
评论数最多的 Issue 揭示了用户的两个核心关注点：

| Issue | 标题 | 评论数 | 核心诉求 |
|-------|------|--------|----------|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | Text between tool calls leaks to messaging channels | 29 | 代理在工具调用间产生的内部处理、错误处理等文本被直接路由到用户频道，严重破坏 UX。 |
| [#88312](https://github.com/openclaw/openclaw/issues/88312) | [Regression] Codex app-server turn-completion stall | 15 | 2026.5.27 版本后 Codex 会话卡死，回退至 5.26 正常，属于已修复回归的再次出现。 |
| [#87307](https://github.com/openclaw/openclaw/issues/87307) | Matrix thread replies sent as normal replies | 14 | 升级至 2026.5.22 后 Matrix 线程回复变为普通回复，/status 和 /model 命令静默。 |

PR 方面，虽然评论数显示为 undefined，但以下 PR 因规模大、影响广而备受关注：

- [PR #91438](https://github.com/openclaw/openclaw/pull/91438) — Microsoft Teams 语音/视频通话提供者（XL 规模，兼容性风险高）。
- [PR #91557](https://github.com/openclaw/openclaw/pull/91557) — iPad/iPhone 控制界面全面改进（视频证明，XL 规模）。

**分析**：文本泄漏和会话卡死直接影响了生产环境可用性，社区情绪紧张但反馈积极；Matrix 和 iMessage 渠道的回归问题表明多渠道维护是持续挑战。

## Bug 与稳定性
按严重程度排列的今日重点 Bug（附 fix PR 跟踪）：

| 严重度 | Issue | 标题 | 状态 | Fix PR 状态 |
|--------|-------|------|------|-------------|
| P1/回归 | [#88312](https://github.com/openclaw/openclaw/issues/88312) | Codex 会话卡死 | 开放，需复现 | 无关联 PR |
| P1 | [#86508](https://github.com/openclaw/openclaw/issues/86508) | 嵌入式会话 takeover 错误（Discord） | 开放 | 无关联 PR |
| P1 | [#89315](https://github.com/openclaw/openclaw/issues/89315) | 网关内存无限增长导致 OOM 杀死 | 开放 | 无关联 PR |
| P1/阻塞 | [#86599](https://github.com/openclaw/openclaw/issues/86599) | 本地模型调用阻塞 Windows 事件循环 | 已关闭 | 已关闭（可能已修复） |
| P2 | [#53486](https://github.com/openclaw/openclaw/issues/53486) | 飞书卡片 JSON 渲染为纯文本（回归） | 开放 | 无关联 PR |
| P2 | [#50442](https://github.com/openclaw/openclaw/issues/50442) | 备份大 .tmp 文件残留导致磁盘耗尽 | 开放 | 无关联 PR |

值得关注的 **修复进展**：  
- [PR #89721](https://github.com/openclaw/openclaw/pull/89721) 为 cron 会话回收增加了回归测试，防止基会话被误删。  
- [PR #91801](https://github.com/openclaw/openclaw/pull/91801) 修复了在清空中止后释放卡住会话通道的问题，覆盖 `queuedCount=0` 但 `queueDepth>0` 的楔形状态。  
- [PR #89017](https://github.com/openclaw/openclaw/pull/89017) 修复 WebChat 会话在网络断开后重置为 `.jsonl.reset.*` 的问题。

## 功能请求与路线图信号
今日社区提出的新功能需求（结合已有 PR 判断路线图方向）：

- **持久化任务状态面板**（[#52640](https://github.com/openclaw/openclaw/issues/52640)）— 为长运行频道交互（如 Discord）提供权威状态表面。已有相关 PR 改进 WebChat 进度条（[#91215](https://github.com/openclaw/openclaw/pull/91215)），但抽象层尚未落地。
- **MathJax/LaTeX 支持**（[#42840](https://github.com/openclaw/openclaw/issues/42840), 👍6）— 用户强烈希望 Control UI 可渲染数学公式，目前无关联 PR。
- **预压缩内存刷新的有界追加语义**（[#90354](https://github.com/openclaw/openclaw/issues/90354)）— 防止模型追加过大或噪声内容。该方向与 [#53638](https://github.com/openclaw/openclaw/issues/53638)（通道级模型覆盖）等一起暗示项目正在提升配置细粒度控制。
- **通道/群组/DM 模型覆盖**（[#53638](https://github.com/openclaw/openclaw/issues/53638)）— 允许在配置中按对话指定模型，无需运行时可选。

路线图信号：**语音渠道**（Teams CVI 和 WebSocket 路由改进 [PR #91784](https://github.com/openclaw/openclaw/pull/91784)）和 **内存/上下文管理**（如 PR #91091 修复扫描失败时错误裁剪索引）是当前的中期投入方向。

## 用户反馈摘要
从 Issue 评论中提炼的真实反馈：

- **“内部处理泄漏到频道是灾难性的”** — [#25592](https://github.com/openclaw/openclaw/issues/25592) 用户描述在 Slack 频道中看到 `“let me check…”` 及其它 debug 输出，影响品牌形象。
- **“5.27 开始 Codex 会话完全不可用”** — [#88312](https://github.com/openclaw/openclaw/issues/88312) 用户报告即使回退到 5.26 仍稳定，表明是近期合并引入的回归。
- **“Matrix 升级后线程全部变成普通回复，用户很困惑”** — [#87307](https://github.com/openclaw/openclaw/issues/87307) 用户同时指出 `/status` 和 `/model` 命令静默，需要手动重启解决。
- **“备份超时后磁盘被 .tmp 文件占满”** — [#50442](https://github.com/openclaw/openclaw/issues/50442) 用户发现 50GB 空间在 3 小时内耗尽，建议增加自动清理。
- **“RISC-V64 上安装成功但请求失败”** — [#54253](https://github.com/openclaw/openclaw/issues/54253) 用户对跨架构支持表达兴奋，但希望修复 LLM 请求失败问题。

整体满意度：多数用户对功能广度表示认可，但对 **回归频率** 和 **渠道一致性** 提出批评，特别是 Matrix、Discord 和 iMessage 渠道。

## 待处理积压
以下重要 Issue/PR 长期未响应，需维护者关注：

- **[Issue #25592](https://github.com/openclaw/openclaw/issues/25592)** — P1，工具调用文本泄漏，创建于 2 月 24 日，已标记 `stale` 和 `clawsweeper:needs-maintainer-review`，目前无进展。
- **[Issue #54253](https://github.com/openclaw/openclaw/issues/54253)** — P2，RISC-V64 架构 LLM 请求失败，创建于 3 月 25 日，需社区或架构专家介入。
- **[Issue #53628](https://github.com/openclaw/openclaw/issues/53628)** — P2，`$XDG_CONFIG_HOME` 未解析导致技能安装失败，创建于 3 月 24 日，有 linked PR 但未合并。
- **[Issue #44905](https://github.com/openclaw/openclaw/issues/44905)** — P1，Discord 泄漏内部工具调用痕迹，严重安全影响，无 PR 关联。
- **[PR #55851](https://github.com/openclaw/openclaw/pull/55851)** — 长期开放（3 月 27 日），为超载/限流错误添加上下文信息，状态为 `waiting on author`，需作者回应。
- **[PR #79982](https://github.com/openclaw/openclaw/pull/79982)** — 引入 `group:core` 工具组，状态为 `waiting on author`，已停止更新。

**建议**：优先解决 P1 级别的文本泄漏和回归问题，清理 `stale` 标记的议题以保持积压健康。Matrix 和 Discord 渠道的回归应在下一个小版本中处理。

---

*数据统计时间：2026-06-10 17:00 UTC | 数据源：GitHub issues & PRs*

---

## 横向生态对比

好的，作为资深技术分析师，我已详细审阅了您提供的2026年6月10日各开源项目的社区动态摘要。基于这些数据，现为您呈上一份横向对比分析报告。

---

# 开源个人AI助手生态横向分析报告 (2026-06-10)

## 1. 生态全景

2026年6月，个人AI助手/自主智能体开源生态呈现出 **“一超多强、分化加速”** 的鲜明态势。以OpenClaw为核心的生态系依然占据社区活跃度的绝对主导，其巨大的Issue和PR吞吐量（单日近千条）是其生态规模的直接体现。与此同时，以ZeroClaw、IronClaw为代表的新一代项目正快速崛起，它们不再满足于功能堆叠，而是将焦点转向**企业级安全（RBAC）、核心运行时稳定性（上下文管理、高并发）、以及架构重构（如AgentScope 2.0迁移）**。这种从“功能扩展”到“质量与安全巩固”的范式转变，标志着整个赛道正告别野蛮生长，进入精细化打磨的关键阶段。社区的核心诉求从“还能做什么”转向了“怎么做才可靠、安全、可溯源”。

## 2. 各项目活跃度对比

以下表格汇总了各项目在2026-06-10的核心活跃度指标：

| 项目名称 | 今日Issues (新开/活跃) | 今日PRs (新开/合并) | 版本发布 | 健康度评估 | 核心活动特征 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 314 新开，128 关闭 | 355 待合并，133 合并 | ✅ v2026.6.5 (正式版+beta) | ⭐⭐⭐⭐⭐ | 生态核心，**极高吞吐量**，渠道修复与核心稳定性并重 |
| **ZeroClaw** | ~50 | ~50 (仅合并1) | ❌ | ⭐⭐⭐ | **高度活跃**，但PR合并率极低，处于大规模特性提交与审核博弈期 |
| **IronClaw** | 46 | 50 (合并2) | ❌ | ⭐⭐⭐⭐ | **极度活跃**，聚焦于“Reborn”架构的生产就绪冲刺 |
| **Hermes Agent** | 50 | 50 (合并6) | ❌ | ⭐⭐⭐⭐ | **极高活跃度**，社区贡献积极，围绕重大Bug和架构改进深度讨论 |
| **PicoClaw** | 16 (安全相关) | 5 (合并) | ✅ nightly | ⭐⭐⭐ | **安全事件驱动**，因集中安全漏洞报告活跃度飙升 |
| **NanoBot** | 6 (全开放) | 13 (待合并) | ❌ | ⭐⭐⭐ | **稳步推进**，聚焦于会话隔离、Provider兼容性等中级问题 |
| **CoPaw** | >30 | >30 | ✅ v1.1.11-beta.2 | ⭐⭐⭐ | **活跃**，模型兼容性与前端性能是主要矛盾点 |
| **NullClaw** | 1 (新开) | 1 (新开) | ❌ | ⭐⭐⭐⭐ | **健康高效**，7个PR中修复了5个用户报告的问题，修复率高 |
| **NanoClaw** | 低 (1个老Issue更新) | 40 (合并, 多为清理) | ❌ | ⭐⭐⭐ | **内部清理期**，大量关闭历史积压提案，为下一阶段做准备 |
| **LobsterAI** | 2 | 5 (合并4) | ❌ | ⭐⭐⭐ | **方向明确**，专注于任务通知和数据备份的痛点功能 |
| **TinyClaw / Moltis / ZeptoClaw** | 0 | 0 | ❌ | - | **静默期**，过去24小时无公开活动 |

## 3. OpenClaw在生态中的定位

- **绝对核心与参照物**: OpenClaw以其**428条活跃Issue、488条PR**的巨量社区活动，毫无悬念地成为整个生态的“引力中心”。其它项目在功能设计、问题讨论（如文本泄漏、会话管理）上往往以OpenClaw为参照。
- **成熟度与广度**: 作为最成熟的项目，OpenClaw的更新已超越功能添加，进入**深度渠道兼容性优化**（如iMessage传输加固）和**复杂状态管理修复**（如Codex会话压缩所有权）。每日稳定发布正式版+预览版的节奏，显示了其工程化水平之高。
- **社区规模最大，痛点也最典型**: 其社区痛点（如#25592工具调用文本泄漏、#88312 Codex回归）代表了该生态下最普遍、最影响生产环境的“大项目病”。其它小项目能更灵活地避免或修复类似问题。
- **定位差异**: 与侧重于**企业级安全**的ZeroClaw、**架构革新**的IronClaw相比，OpenClaw更像一个 **“全能型选手”** ，它试图覆盖最广泛的渠道和功能，但这同时也意味着需要解决最复杂的系统耦合问题。其庞大的积压和回归问题就是这种复杂性的代价。

## 4. 共同关注的技术方向

多项目不约而同地涌现出以下共同需求，指明了当前的核心技术挑战：

1.  **工具调用文本泄漏与安全 (涉及: OpenClaw, NanoBot, ZeroClaw, PicoClaw)**
    - **具体诉求**: 代理在工具调用间产生的内部推理、错误信息、甚至密码等敏感数据，被意外路由到用户可见的频道，严重影响UX和信息安全。这是当前**最普遍、最严重**的问题。

2.  **会话管理与上下文隔离 (涉及: OpenClaw, NanoBot, ZeroClaw, IronClaw)**
    - **具体诉求**: 修复会话卡死、回归、历史记录跨会话污染、上下文预算被系统提示耗尽、压缩机制不合理等。这直接关系到AI助手的**可靠性与一致性**。

3.  **渠道兼容性碎片化 (涉及: OpenClaw, NullClaw, ZeroClaw, CoPaw)**
    - **具体诉求**: 几乎所有主流渠道（Discord, Matrix, Telegram, iMessage, Slack, 微信）都存在回归或不一致问题。用户对“在某个平台上特定功能失效”的抱怨非常普遍。

4.  **内存与上下文管理 (涉及: OpenClaw, ZeroClaw, Hermes Agent)**
    - **具体诉求**: 优化内存占用防止OOM、实现更智能的上下文预算和压缩、支持长上下文模型、清理备份残留文件。这是保证服务长期稳定运行的基础。

5.  **安全加固 (涉及: PicoClaw, ZeroClaw, NanoClaw)**
    - **具体诉求**: 引入RBAC、修复SSRF/CSRF/授权绕过漏洞、使用加密安全的随机数生成。尤其针对PicoClaw，一日内报告数十个安全漏洞，将安全问题的紧迫性推至顶峰。

## 5. 差异化定位分析

| 维度 | OpenClaw | ZeroClaw | IronClaw | Hermes Agent | CoPaw | NanoBot / NullClaw |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | 全渠道、全能型AI助手 | 企业级安全、MCP、多租户 | Reborn架构、生产就绪、通用附件 | 桌面端体验、学习循环、架构创新 | 国内用户友好、模型兼容、前端易用 | 轻量级、专注单一平台、高修复效率 |
| **目标用户** | 广泛开发者、社区 | 企业、安全敏感团队 | 寻求最新架构和第三方集成的开发者 | 桌面重度用户、追求PBT的团队 | 国内中文用户、对性能有要求的用户 | 特定平台（Telegram/custom Dev）用户 |
| **技术架构** | 高度模块化，但对渠道适配投入极大 | 强调安全分层和权限模型 | 彻底重写(Reborn)，追求干净的设计和可观测性 | 强调“学习循环”和互动式UI | 基于AgentScope生态，存在迁移计划 | 架构简洁，启动快，配置灵活 |
| **当前阶段** | 质量巩固期（处理回归和长期积压） | 功能与安全并行推进期 | 架构冲刺期 (Reborn生产就绪) | 核心功能打磨期 | 模型兼容性与前端性能攻坚期 | 稳步迭代期 |

## 6. 社区热度与成熟度

- **第一梯队 (超级活跃、生态核心)**: **OpenClaw**。其数据量一骑绝尘，是生态的绝对中心。
- **第二梯队 (极高活跃、快速迭代)**: **ZeroClaw, IronClaw, Hermes Agent**。这些项目在特定领域（安全、架构、体验）进行深度耕耘，社区讨论质量高，是下一阶段创新的主要来源。
- **第三梯队 (活跃、稳步推进)**: **NanoBot, NullClaw, CoPaw, LobsterAI**。这些项目社区规模相对较小，但修复效率高，方向明确，在产品打磨上表现稳健。
- **成熟度分层**:
    - **质量巩固阶段**: OpenClaw（处理回归）、CoPaw（模型兼容）。
    - **架构/质量并行阶段**: ZeroClaw（安全与功能）、IronClaw（架构冲刺与功能）。
    - **功能快速迭代阶段**: Hermes Agent, NanoBot, NullClaw。
- **值得注意**: PicoClaw因24小时内集中涌入16个安全漏洞报告，其活跃度是**事件驱动型**的，反映了项目在安全实践上可能存在的短板，并不代表其成熟度。

## 7. 值得关注的趋势信号

1.  **安全不再只是“选项”，而是“硬约束”**: PicoClaw一天内数十个安全漏洞，加上ZeroClaw对RBAC的强烈呼声，强烈表明社区对AI Agent的安全要求已从“最好有”变为“必须有”。任何面向生产环境的AI Agent项目，**安全审计和权限模型**必须从设计阶段就开始考虑。

2.  **Agent自主性与“学习循环”成为新战场**: Hermes Agent社区对“学习循环”的热议，CoPaw采纳“技能自我进化”功能，都指向了同一个方向：用户不再满足于被动执行指令的Agent，而是希望Agent具备**从交互中学习、自我迭代能力**。这可能成为下一代Agent架构的核心竞争力。

3.  **“多模型/多Provider”路由成为刚需**: 用户期望在不同的模型（快速付费 vs. 私密本地）之间灵活切换，甚至在同一工作流中编排多个模型。这要求项目必须提供**统一、健壮、可配置的模型路由层**，而不仅仅是简单的API封装。

4.  **企业级多租户与管理功能浮出水面**: ZeroClaw对RBAC和多租户的讨论，IronClaw对管理员共享工具和角色的规划，标志着这一生态正从**个人爱好者工具**向**团队生产力平台**演化。能够提供团队协作、权限管理、审计追踪的项目将获得先发优势。

5.  **“调试与可观测性”重要性凸显**: IronClaw投入大量精力构建操作员命令平面、生产图验证；ZeroClaw关注turn metadata；甚至连CoPaw也在集成AgentScope Tracing。这表明，随着Agent系统日趋复杂，**如何诊断问题、监控状态**已成为与功能开发同等重要的基础能力。

**总结**: 当前AI Agent开源生态正处于一个关键转折点。项目间的竞争已从“功能有无”转向“品质高低”。**可靠性、安全性、可管理性**，而非单纯的功能数量，将成为决定项目未来走向的关键因素。对于开发者而言，选择项目时，除了功能列表，更应仔细审查其**Issue修复率、安全响应速度、以及对核心运行时稳定性的投入**。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# 🤖 NanoBot 项目动态日报 | 2026-06-10

## 今日速览
过去24小时项目保持 **高活跃度**：共处理6个新Issues（全部开放，0关闭）和23个PR（其中10个已合并/关闭，13个待合并）。核心贡献者针对历史上下文污染、会话隔离、模型API兼容性等关键问题提交了修复PR，同时社区发起了多项改进建议（如按会话覆盖模型预设、启动时使用自定义图标等）。测试基础设施持续加强（如内存生命周期测试脚本）。无新版本发布，但代码库正稳步向更健壮、更用户友好的方向演进。

---

## 版本发布
*无新版本发布。*

---

## 项目进展
今日合并/关闭的10个PR中，重要的功能推进与修复如下：

- **PR #4208** — [feat(webui): 添加助手回复的“从此处派生”功能](https://github.com/HKUDS/nanobot/pull/4208)。用户可从任意助手回复处派生新对话，保留前缀、打开空白输入框。增强了WebUI的对话管理灵活性。
- **PR #4177** — [docs: 优化新手入门文档](https://github.com/HKUDS/nanobot/pull/4177)。重构了文档入口，为不同背景用户提供清晰路径（零基础、CLI快速、WebUI、Provider食谱等），降低上手门槛。
- **PR #4265** — [feat(english-read): 将定时任务从每天改为每2天](https://github.com/HKUDS/nanobot/pull/4265)。调整内建的英语阅读技能调度频率。
- **PR #3434** — [feat(lateX): 飞书通道LaTeX渲染](https://github.com/HKUDS/nanobot/pull/3434)。通过CodeCogs API将LaTeX公式转为图片并在飞书频道展示，默认关闭，需配置开启。
- **PR #3400** — [feat(dream): 允许用户控制Dream是否可编辑USER.md和SOUL.md](https://github.com/HKUDS/nanobot/pull/3400)。增加`allow_edit_identity_files`配置项，默认true；设为false时Dream仅编辑memory文件，保护核心人格设定。
- **PR #4034** — [feat: 添加GitAgent Protocol支持](https://github.com/HKUDS/nanobot/pull/4034)（标记为duplicate，但已合并内容）。增加`agent.yaml`和`SOUL.md`文件支持，提升与其他AI Agent标准的互操作性。
- **PR #4190** — [enhancement: 加强工具调用参数验证严格性](https://github.com/HKUDS/nanobot/pull/4190)。不再静默修复非对象参数为空对象，强制要求参数解析为JSON对象后再进行Schema校验。

> 此外，多项长期待审查的PR（#3983、#3982、#4053、#4119等）在今日获得更新，表明测试基础设施和安全性增强工作仍在持续推进。

---

## 社区热点
今日讨论最活跃的Issues（按评论数排序）：

1. **#4253** — [enhancement: 支持按会话覆盖模型预设](https://github.com/HKUDS/nanobot/issues/4253)（3条评论）  
   **诉求**：用户经常在“快速但需付费的OpenRouter”和“私密但缓慢的本地llamacpp”之间切换，希望能在每个会话中独立指定模型，而非依赖全局设置。这表明高级用户对多模型工作流有强烈的需求。

2. **#4259** — [bug: `history.jsonl`跨会话注入导致上下文污染](https://github.com/HKUDS/nanobot/issues/4259)（2条评论）  
   **诉求**：`ContextBuilder.build_system_prompt()`在注入#Recent History时未做会话隔离，导致某会话的历史摘要混入其他会话的system prompt。社区已给出详细的数据流分析，并正在等待维护者确认。该问题对会话隔离的破坏性严重。

3. **#4061** — [bug: OpenAI兼容的文本格式工具调用未被解析为结构化tool_calls](https://github.com/HKUDS/nanobot/issues/4061)（1条评论）  
   **诉求**：部分OpenAI兼容provider以纯文本markup形式返回工具调用，而NanoBot只执行结构化的`LLMResponse.tool_calls`，导致用户看到原始标记且无法调用工具。该Issue已存在12天，社区期待修复。

---

## Bug 与稳定性
按严重程度排列今日报告的Bug：

| 等级 | Issue # | 描述 | 状态 |
|------|---------|------|------|
| 🔴 严重 | [#4259](https://github.com/HKUDS/nanobot/issues/4259) | **历史记录跨会话注入**：`history.jsonl`中所有会话的未进入Dream处理的条目被混入当前会话system prompt，导致隐私泄露和上下文污染。 | 开放，无关联PR |
| 🟠 中等 | [#4264](https://github.com/HKUDS/nanobot/issues/4264) | **`idleCompact`未覆盖最后8条消息**：若用户纠正模型错误的过程发生在最后8条消息中，压缩时这些纠正内容会被跳过，导致`history.jsonl`留下错误结论。 | 开放，无关联PR |
| 🟠 中等 | [#4261](https://github.com/HKUDS/nanobot/issues/4261) | **GPT-5/o-series模型使用`max_tokens`而非`max_completion_tokens`**：Azure上部署GPT-5.4时请求被拒。已有两个修复PR（#4263、#4268）。 | 开放，已有PR |
| 🟡 轻微 | [#4262](https://github.com/HKUDS/nanobot/issues/4262) | **Agent模式启动未使用自定义`botIcon`**：首次显示默认图标"puppy"，后续才显示配置的图标。 | 开放，无关联PR |

**稳定性信号**：今日无崩溃类问题报告，但上下文污染和压缩机制缺陷属于中等严重性。两个关于`max_completion_tokens`的PR（#4263、#4268）正在竞争解决同一问题，需合并一种方案。

---

## 功能请求与路线图信号

| 功能 | Issue/PR | 社区热度 | 可能纳入下一版本的迹象 |
|------|----------|----------|------------------------|
| **按会话覆盖模型预设** | [#4253](https://github.com/HKUDS/nanobot/issues/4253) | 3条评论，无反对 | 当前无对应PR，但该需求与多Provider工作流紧密相关，预计会成为未来增强方向。 |
| **启动时使用自定义图标** | [#4262](https://github.com/HKUDS/nanobot/issues/4262) | 0评论 | 微小改进，实现简单，可能很快被采纳。 |
| **飞书频道LaTeX渲染** | PR [#3434](https://github.com/HKUDS/nanobot/pull/3434) | 已合并 | 已进入主分支，下一版本将包含。 |
| **Dream可控制是否编辑身份文件** | PR [#3400](https://github.com/HKUDS/nanobot/pull/3400) | 已合并 | 同上，已合并。 |
| **按需版本检查（Settings > About）** | PR [#4255](https://github.com/HKUDS/nanobot/pull/4255) | 开放待审 | 关闭了实时轮询和WebSocket推送，符合轻量化设计，预计会合并。 |
| **分段消息支持fenced代码块感知** | PR [#4257](https://github.com/HKUDS/nanobot/pull/4257) | 开放待审 | 修复了因分割消息导致代码块渲染错误的问题，实用性高，很可能合并。 |
| **StepFun ASR SSE转录Provider** | PR [#4260](https://github.com/HKUDS/nanobot/pull/4260) | 开放待审 | 新增语音转录提供商，扩展了多模态能力。 |
| **保持历史cursor单调递增** | PR [#4256](https://github.com/HKUDS/nanobot/pull/4256) | 开放待审 | 修复`MemoryStore`中cursor分配非单调的问题，影响数据一致性，应被积极审查。 |

**路线图信号**：项目明显在强化 **会话隔离** 和 **Provider兼容性** 两条主线，同时通过测试覆盖和安全性增强提升代码健壮性。社区对 **多模型工作流** 和 **跨会话上下文污染** 的呼声较高，预期会成为下一个版本的核心改进点。

---

## 用户反馈摘要
从Issues评论中提炼的典型用户痛点与场景：

- **多模型混合使用**（#4253）：用户`rombert`表示日常使用OpenRouter（快速、付费）和本地llamacpp（私密、慢速、免费）两种预设，希望每个会话能独立选择，且不丢失对话历史。当前无此功能，只能手动切换全局设置。
- **会话隐私与上下文隔离**（#4259）：用户`chxuan`通过分析代码指出，`history.jsonl`中其他会话的历史摘要被直接注入当前会话的system prompt，导致“上下文污染”。用户强烈要求按会话隔离，避免敏感信息泄露。
- **模型纠正闭环丢失**（#4264）：用户`imkuang`描述了一个典型场景：用户请求任务→模型错误→用户纠正→模型正确执行。但`idleCompact`只压缩除最后8条之外的消息，若纠正过程在最后8条内，则压缩后历史记录会遗漏纠正，保留错误结论。用户认为“这对于基于token预算的压缩方式也是一样的，但那些通常发生在会话进行中，记录仍在更新”。
- **GPT-5模型API不兼容**（#4261）：用户`mraad`在使用Azure部署GPT-5.4时遇到`max_tokens`参数被拒绝的问题，指出需要改用`max_completion_tokens`。另一位用户`axelray-dev`和`04cb`已分别提交修复PR。
- **Starting代理模式显示默认图标**（#4262）：用户`mraad`反馈首次进入agent模式时显示“puppy”而非配置的`botIcon`，后续正确。属于小但影响体验的问题。

**满意度**：用户对文档改进（#4177）和飞书LaTeX渲染（#3434）等已合并功能表示满意。但对核心漏洞（#4259）和产品体验（#4253）的反馈显示仍有改进空间。

---

## 待处理积压
以下为长时间未响应的重要Issue或PR，建议维护者优先关注：

| 标识 | 描述 | 创建时间 | 上次更新 | 备注 |
|------|------|----------|----------|------|
| **Issue #4061** | [OpenAI兼容provider的文本格式工具调用未解析](https://github.com/HKUDS/nanobot/issues/4061) | 2026-05-29 | 2026-06-09 | 已存在12天，仅1条评论，无修复PR。影响使用非结构化tool_calls provider的用户。 |
| **PR #3983** | [test: 覆盖runner中blocked tool-call finish reasons](https://github.com/HKUDS/nanobot/pull/3983) | 2026-05-24 | 2026-06-09 | 来自核心贡献者`yu-xin-c`，测试覆盖率增强，等待审查合并。 |
| **PR #3982** | [test: 添加脚本化 agent runner 测试 harness](https://github.com/HKUDS/nanobot/pull/3982) | 2026-05-24 | 2026-06-09 | 同上，提供可复用测试框架，有助于自动化质量保证。 |
| **PR #4053** | [fix(tools): 保持只读根目录不出现在写入路径中](https://github.com/HKUDS/nanobot/pull/4053) | 2026-05-29 | 2026-06-09 | 安全性修复，防止只读目录被写入。已积累较多更改，建议尽快合并。 |
| **PR #4119** | [fix(exec): 阻止通过相对符号链接逃逸工作区](https://github.com/HKUDS/nanobot/pull/4119) | 2026-05-31 | 2026-06-09 | 安全漏洞修复，允许通过symlink逃逸工作区执行命令。建议优先审查。 |
| **PR #4193** | [test: 添加内存生命周期测试脚本](https://github.com/HKUDS/nanobot/pull/4193) | 2026-06-04 | 2026-06-09 | 测试覆盖记忆系统核心流程，与上下文污染问题相关，重要性高。 |

> 以上PR均来自多次贡献的维护老手（如`yu-xin-c`），且多与安全性、测试基础设置相关，长期未合并可能引入技术债务和安全隐患。建议维护者集中审查。

---

*数据来源：GitHub API 更新于 2026-06-10 10:00 UTC | 日报自动生成*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，我已根据您提供的Hermes Agent GitHub数据，生成了以下2026年6月10日的项目动态日报。

---

# Hermes Agent 项目日报 | 2026-06-10

## 今日速览

项目今日保持极高活跃度，24小时内产生了50条Issue和50条PR，社区贡献热情持续高涨。尽管无新版本发布，但多个关键Bug的修复PR（如Stale Stream回退、Kanban锁超时）和大量新技能捆绑包的提交，表明项目正处于密集的“功能完善与稳定性加固”阶段。值得一提的是，社区对桌面客户端（Hermes Desktop）的集成体验和Cron作业的可用性提出了大量反馈，是当前关注的焦点。整体项目健康度良好，但合并率（6/50）相对较低，可能预示着代码审查的精细度或复杂性较高。

## 项目进展

今日没有合并或关闭的重大PR。以下为当前开放的关键PR，它们代表了项目正在积极推进的方向：

- **修复模块阴影 (`sys.path`)** [PR #43090](https://github.com/nousresearch/hermes-agent/pull/43090): 修复了当当前目录存在同名文件时，Python导入系统会错误地优先加载该文件而非Hermes包的问题。这是一个重要的环境兼容性修复，能避免许多因命名冲突导致的诡异错误。
- **Kanban锁超时** [PR #41058](https://github.com/nousresearch/hermes-agent/pull/41058): 为Kanban数据库添加了文件锁超时机制，解决因进程意外持有锁导致后续命令无限期阻塞的问题，是提升Kanban可靠性的关键一步。
- **Stale Stream回退** [PR #43222](https://github.com/nousresearch/hermes-agent/pull/43222) & [PR #43231](https://github.com/nousresearch/hermes-agent/pull/43231): 针对流式API中断后在同个不健康提供商上无脑重试的问题，两个PR分别提出了不同的解决方案（单轮内升级与连续中断升级）。这显示了社区对提升LLM调用鲁棒性的高度重视。
- **移除红队技能** [PR #43221](https://github.com/nousresearch/hermes-agent/pull/43221): 为避免`godmode`等红队技能的定义触发Anthropic等高级LLM的输出分类器，导致无关任务失败，贡献者主动移除了这些内容。这体现了项目在策略层面对模型治理规则的适应性调整。
- **Cron会话渲染** [PR #43233](https://github.com/nousresearch/hermes-agent/pull/43233): 修复了Hermes Desktop上查看Cron作业执行详情时，工具调用和模型回复不可见的核心问题。这直接提升了Desktop客户端的核心“调度记录查看”功能可用性。

## 社区热点

1.  **Telegram AI Bot新功能集成** [Issue #21587](https://github.com/nousresearch/hermes-agent/issues/21587) **(9条评论)**
    - **诉求**: Telegram 5月7日发布了重大AI Bot更新（访客机器人、机器人间通信等），社区成员`Editorenbici`提议Hermes Agent应集成这些新API，以支持更复杂的多智能体协作和团队聊天工作流。
    - **分析**: 该Issue虽然评论最多，但创建时间较早。今日的“更新”使其重回视野，表明社区对利用最新平台能力、拓展Agent应用场景（如作为来宾机器人加入群聊）有强烈愿望。这是项目保持平台前沿性的重要信号。

2.  **密码被星号替换导致工具调用失败** [Issue #43083](https://github.com/nousresearch/hermes-agent/issues/43083) **(6条评论，P1优先级)**
    - **诉求**: 出于安全考虑，工具调用中的密码被替换为`***`。但这导致模型在读取自身对话历史时，看到的是`***`而非真实密码，进而在第二次工具调用时提交错误的参数（`***`导致认证失败），产生“自残式”功能失效。
    - **分析**: 这是一个典型的“安全vs可用性”权衡问题。现有的防御性编码策略虽然保护了日志安全性，却破坏了Agent作为自主实体的核心交互闭环。该Issue被标记为 **P1** 优先级，社区不仅指出了问题，还提供了在持久化前擦除凭证的详细代码建议，是高质量反馈的典范。

3.  **macOS launchd重启失败** [Issue #42006](https://github.com/nousresearch/hermes-agent/issues/42006) **(5条评论，P2优先级)**
    - **诉求**: 在macOS上执行`hermes update`后，`launchd_restart()`函数因未先执行`bootout`就直接尝试`bootstrap`新任务，导致Gateway重启失败，进程与launchd注册状态不同步。
    - **分析**: 这是一个平台特定的回归问题，直接影响了macOS用户的更新体验。社区不仅复现了问题，还深入分析了launchd的`bootstrap`和`bootout`指令行为差异，并提出了“先bootout再bootstrap”的标准macOS服务管理模式解决方案。这显示了社区对底层平台机制的深刻理解。
    - **关联**: 该Issue的讨论热度也说明macOS平台用户群体庞大，且对网关稳定性有较高要求。

## Bug与稳定性

以下为今日报告的严重Bug，按优先级排列：

- **[P1] Passwords replaced by `***` cause tool call failure** [Issue #43083](https://github.com/nousresearch/hermes-agent/issues/43083): 如上所述，核心交互闭环被破坏，严重性高。**已有明确的代码修复建议**。
- **[P1] Cron: `deliver=origin` fails to resolve target** [Issue #43014](https://github.com/nousresearch/hermes-agent/issues/43014): Cron作业的递送目标解析失败，导致作业结果无法交付。这是核心Cron功能的阻断性Bug。
- **[P2] `launchd_restart` fails on macOS** [Issue #42006](https://github.com/nousresearch/hermes-agent/issues/42006): 影响macOS用户的升级体验。
- **[P2] Stale stream errors don't trigger fallback** [Issue #43211](https://github.com/nousresearch/hermes-agent/issues/43211): 流中断后在同个提供商上无脑重试，浪费资源且延迟恢复。**已有两个Fix PR** ([PR #43222](https://github.com/nousresearch/hermes-agent/pull/43222), [PR #43231](https://github.com/nousresearch/hermes-agent/pull/43231))。
- **[P3] `auxiliary.title.enabled` config ignored** [Issue #41744](https://github.com/nousresearch/hermes-agent/issues/41744): 配置项不生效，标题生成功能不受控。
- **[P3] File browser ENOENT in remote gateway mode** [Issue #43042](https://github.com/nousresearch/hermes-agent/issues/43042): 桌面应用文件浏览器在远程模式下间歇性显示`ENOENT`错误，影响用户文件操作体验。

## 功能请求与路线图信号

- **Volcengine (火山引擎) 内置支持** [Issue #29331](https://github.com/nousresearch/hermes-agent/issues/29331): 用户提议将字节跳动的火山引擎作为内置提供商。该项目已在其文档中有官方集成指南，说明这是一个有明确用户基础和官方支持的需求，被纳入正式版本的可能性很高。
- **每工具开关** [Issue #31375](https://github.com/nousresearch/hermes-agent/issues/31375): 用户要求比“工具集”更精细的“工具”级别开关，例如允许禁用`web_search`而保留`web_extract`。这反映了用户对Agent行为进行更精细化控制的普遍需求。
- **上下文选择/路由作为一等公民** [Issue #36765](https://github.com/nousresearch/hermes-agent/issues/36765): 一个 **RFC** 级别的提案，主张将上下文引擎的职责从“压缩”扩展为“选择/路由”，以支持检索、主题切换等场景。这是一个重要的架构设计方向讨论，若被采纳，将对后续版本产生深远影响。
- **`delegated_role`字段** [Issue #41554](https://github.com/nousresearch/hermes-agent/issues/41554): 提议在委派会话中添加`delegated_role`字段，用于记录子Agent被指派扮演的角色或人格。这有助于完善多智能体溯源和工作流管理。
- **YOLO模式下仍需确认`execute_code`** [Issue #42921](https://github.com/nousresearch/hermes-agent/issues/42921): 用户报告即使启用了所有自动确认配置，`execute_code`工具仍会弹出确认提示。这表明“完全自主执行代码”是部分用户的核心需求，但项目在安全和自主性之间设置的最后一道防线可能过于严格。

## 用户反馈摘要

- **macOS更新痛点** ([Issue #42006](https://github.com/nousresearch/hermes-agent/issues/42006)): 用户`rjbudzynski`在尝试更新后，Gateway进程分离，无法无缝重启。该反馈深入分析了launchd行为，提供了高质量的诊断信息。
- **桌面端与网关不同步** ([Issue #42962](https://github.com/nousresearch/hermes-agent/issues/42962)): 用户发现，Desktop应用在已经打开的会话中，不会同步显示来自Telegram等其他前端产生的新消息。这是一个破坏“多端同步”核心体验的Bug，用户需要手动刷新才能看到最新内容。
- **慢速本地提供商体验不佳** ([Issue #43028](https://github.com/nousresearch/hermes-agent/issues/43028)): 用户`AlphonsoGit`指出，使用Ollama等慢速本地模型时，进度指示器（spinner）会超时并在Agent实际完成思考前报错，建议为慢速模型默认启用安静模式或使超时可配置。这反映了本地模型用户特有的痛点。
- **桌面端新会话工作目录问题** ([Issue #43234](https://github.com/nousresearch/hermes-agent/pull/43234)): 一个PR揭示了`设置 -> 默认项目目录`配置不生效的回归问题，新会话总是从用户主目录启动。这表明桌面端用户体验的细节打磨仍需加强。

## 待处理积压

- **长期未响应的配置功能请求** [Issue #13107](https://github.com/nousresearch/hermes-agent/issues/13107) (2026-04-20创建): 用户请求支持通过`config.yaml`覆盖命令描述，以便为Telegram、Discord等平台提供本地化描述。该Issue已有1个月无人评论或分配，属于“有痛点但未获重视”的长期功能请求。考虑到社区对多语言和自定义UI的潜在需求，建议维护者评估其优先级。
- **Matrix群聊引用设置** [Issue #7507](https://github.com/nousresearch/hermes-agent/issues/7507) (2026-04-11创建): 请求为Matrix群聊添加可配置的回复引用功能。这是最早的未关闭feature request之一，反映了早期用户对平台适配的精细化需求，至今仍未获得分配或实现。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 PicoClaw (github.com/sipeed/picoclaw) 数据，现为您呈上 2026 年 6 月 10 日的项目动态日报。

---

## PicoClaw 项目动态日报 | 2026-06-10

### 1. 今日速览

今日 PicoClaw 项目活跃度极高。一方面，社区功能需求（特别是流式 HTTP 请求支持）持续获得高度关注；另一方面，项目遭遇了大规模安全漏洞报告，一天内有超过 10 个安全问题被集中提交，涵盖 SSRF 绕过、授权绕过、CSRF 等多个方面，这成为今日最重大的事件。虽然项目发布了新的 nightly 版本，并推进了多项关键修复与功能 PR，但维护者可能需要在安全审查上投入更多精力。

### 2. 版本发布

**Nightly 构建 (v0.2.9-nightly.20260610.b9a8fad6)**

- 内容: 这是一个自动化构建版本，包含了自 v0.2.9 以来的所有最新改动。
- 警告: 官方明确指出此版本可能不稳定，建议谨慎使用。
- 完整变更日志: [查看 v0.2.9...main 的变更](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

### 3. 项目进展

今日有 5 个 PR 被合并或关闭，推动了项目和修复与优化：

- **核心稳定性修复**
  - **PR #3064 (已关闭)**：修复了 `pkg/config/migration.go` 中一个可能导致程序崩溃的未检查类型断言问题。当配置文件中的 `model_name` 字段类型异常时，此修复可避免 panic。[查看 PR](https://github.com/sipeed/picoclaw/pull/3064)
  - **PR #2942 (已关闭)**：修正了默认 `claude-sonnet-4.6` 模型 ID 的格式问题，将点号 `.` 更正为连字符 `-`，解决了新安装用户首次对话即失败的问题。[查看 PR](https://github.com/sipeed/picoclaw/pull/2942)
  - **PR #2940 (已关闭)**：修复了 `claude-opus-4-7` 模型因 `temperature` 参数被弃用而导致请求失败的问题。现在，针对该模型及其升级版（如 `claude-sonnet-4.7`），将不再发送该字段。[查看 PR](https://github.com/sipeed/picoclaw/pull/2940)

- **新功能探索**
  - **PR #2937 (已关闭)**：这是一个大型功能 PR，引入了“Agent 协作总线”，实现了 Agent 间通信的持久化邮件系统和权限感知的消息传递。尽管已合并，但它标志着项目在 Agent 协同能力上迈出了重要一步。[查看 PR](https://github.com/sipeed/picoclaw/pull/2937)

- **文档更新**
  - **PR #3086 (已关闭)**：更新了项目 README 中的微信二维码。[查看 PR](https://github.com/sipeed/picoclaw/pull/3086)

### 4. 社区热点

- **🔥 最活跃 Issue：添加流式 HTTP 请求支持** ([Issue #2404](https://github.com/sipeed/picoclaw/issues/2404))
  - 该 issue 已存在超过两个月，累积了 11 条评论和 1 个赞，是目前讨论最热烈的话题。
  - 用户核心诉求是：让 PicoClaw 在向 LLM 后端发送请求时，能够像 OpenAI 的 Python 客户端一样，通过配置 `"streaming": true` 来启用流式传输，从而获得更好的实时响应体验。这个需求反映了用户对更流畅、更接近原生 LLM 使用体验的强烈渴望。

- **用户痛点 Bug：历史记录中多轮对话用户消息显示不全** ([Issue #2796](https://github.com/sipeed/picoclaw/issues/2796))
  - 该 bug 在过去一个月内获得了 6 条评论，并被关闭。
  - 用户指出，当一个对话包含多条用户消息时，从历史记录中只能看到最后一条，前面的用户消息全部丢失。用户认为，用于上下文压缩的消息裁剪不应影响前端展示。

- **其他高关注度 Issue**
  - **PR #2984**: 提议为 Pico WebSocket 客户端添加明确的对话“轮次完成”信号，以解决客户端无法确定 Agent 是否已完全结束处理的问题。[查看 Issue](https://github.com/sipeed/picoclaw/issues/2984)
  - **PR #2983**: 修复 Agent 核心循环中，当 OpenAI 兼容提供商返回语义上空的响应（如 `content: null`）时无法触发重试的问题。[查看 PR](https://github.com/sipeed/picoclaw/pull/2983)

### 5. Bug 与稳定性

今日最突出的是由用户 **YLChen-007** 集中提交的一批 **安全漏洞报告**，风险极高，影响面广。

- **🔴 严重安全风险 (16个新提交)**
  - **SSRF 绕过**：报告了 `web_fetch` 工具可以被多个手段绕过 SSRF 保护，包括：
    - 通过环境配置的 HTTP 代理 ([#3078](https://github.com/sipeed/picoclaw/issues/3078))
    - 利用特殊用途 IPv4 地址段 `198.18.0.0/15` ([#3077](https://github.com/sipeed/picoclaw/issues/3077))
    - 利用 ISATAP IPv6 字面量嵌入私有 IPv4 地址 ([#3074](https://github.com/sipeed/picoclaw/issues/3074))
    - 已有对应修复 PR [#3085](https://github.com/sipeed/picoclaw/pull/3085) 提交。
  - **授权绕过**：报告了多个通道存在 `allow_from` 配置可被绕过的问题，包括飞书 (Feishu, [#3082](https://github.com/sipeed/picoclaw/issues/3082))、MQTT ([#3068](https://github.com/sipeed/picoclaw/issues/3068))、WeCom ([#3076](https://github.com/sipeed/picoclaw/issues/3076))。
  - **控制面/提权风险**：
    - Launcher 的 `allowed_cidrs` 可通过同主机反向代理绕过 ([#3069](https://github.com/sipeed/picoclaw/issues/3069), [#3080](https://github.com/sipeed/picoclaw/issues/3080))
    - 首次设置的密码端点存在 CSRF 漏洞 ([#3072](https://github.com/sipeed/picoclaw/issues/3072))
    - 已认证的 WebSocket 客户端可通过 `/reload` 端点触发未授权的配置重载 ([#3071](https://github.com/sipeed/picoclaw/issues/3071))
  - **其他**：`approval hook` 的目录绑定存在符号链接竞争条件 ([#3081](https://github.com/sipeed/picoclaw/issues/3081))，`exec` 命令白名单可通过 `jq` 环境变量泄露信息 ([#3079](https://github.com/sipeed/picoclaw/issues/3079))，OneBot 频道任意媒体 URL 获取 ([#3070](https://github.com/sipeed/picoclaw/issues/3070))，LINE 签名 webhook 重放攻击 ([#3073](https://github.com/sipeed/picoclaw/issues/3073))，以及从工作目录自动加载不可信的 `skills/` 元数据 ([#3075](https://github.com/sipeed/picoclaw/issues/3075))。

- **其他 Bug 修复 PR (待合并)**
  - **PR #2987**: 修复流式会话期间，`tool_calls` 消息被错误过滤的问题。[查看 PR](https://github.com/sipeed/picoclaw/pull/2987)
  - **PR #2988**: 修复 `/context` 命令始终显示固定压缩 Token 数，无视 `summarize_token_percent` 配置的问题。[查看 PR](https://github.com/sipeed/picoclaw/pull/2988)
  - **PR #2990**: 修复 Web UI 历史记录中只能看到最后一条用户消息的问题，与 Issue #2796 对应。[查看 PR](https://github.com/sipeed/picoclaw/pull/2990)
  - **PR #3067**: 修复可配置页面的“会话隔离范围”设置无法保存的问题。[查看 PR](https://github.com/sipeed/picoclaw/pull/3067)

### 6. 功能请求与路线图信号

结合今日动态，以下需求与未来版本方向高度相关：

- **✨ 高优先级: 流式 HTTP 请求** ([#2404](https://github.com/sipeed/picoclaw/issues/2404))
  - 这是社区呼声最高的功能，虽然已有数月但热度不减。预计会被排入近期开发计划。
- **✨ 网络与安全层加强** (多个安全 PR/Issue)
  - 今日集中爆发的大量安全问题，几乎都围绕着 SSRF、授权、命令注入等网络安全边界。这将成为项目接下来最优先修复和加固的方向。
- **✨ 新 Provider/平台集成**:
  - **NEAR AI Cloud** ([#2917](https://github.com/sipeed/picoclaw/pull/2917)): 增加了对 NEAR AI Cloud 的开源 LLM 支持。虽然标记为 [stale]，但表明项目持续扩展 LLM 生态。
  - **Delta Chat Gateway** ([#3063](https://github.com/sipeed/picoclaw/pull/3063)): 新增对基于邮件协议的 Delta Chat 即时通讯的支持，显示项目在消息渠道上的扩展尝试。

- **🔧 内部优化**:
  - **加密库替换** ([#3088](https://github.com/sipeed/picoclaw/issues/3088)): 提议用更安全、维护中的 `vodozemac` 库替换已不再维护的 `libolm`。这是提升安全基础的重要信号。
  - **Agent 协作** ([#2937](https://github.com/sipeed/picoclaw/pull/2937)): 已合并的 Agent 协作总线，为未来更复杂的多 Agent 任务编排奠定了基础。

### 7. 用户反馈摘要

- **痛点**:
  - **模型兼容性**: 使用 `claude-sonnet-4.6` 和 `claude-opus-4-7` 模型的新用户遇到了开箱即崩溃的问题，尤其是模型 ID 格式错误和参数弃用问题，影响了首次体验。
  - **功能缺失**: 用户迫切需要流式响应，这表明当前非流式体验已无法满足其对实时性的要求。
  - **配置Bug**: 会话隔离范围设置无法保存，说明配置系统的某些部分存在持久化问题，影响用户配置管理的可信度。
  - **Workspace路径限制**: PR #3087 修复了 `exec` 工具在 `restrict_to_workspace` 模式下，因为路径包含 `/` 而被误判为绝对路径从而被拦截的问题。这表明用户在使用复杂的工作区脚本时遇到了障碍。

- **满意点**:
  - 社区对 PR #2937（Agent 协作）的合并感到乐观，这被视为迈向复杂自动化的重要一步。

### 8. 待处理积压

以下为长期未更新的重要 Issue 或 PR，提醒维护者关注：

- **功能请求**:
  - `[Feature] Add in config to send streaming HTTP request` ([#2404](https://github.com/sipeed/picoclaw/issues/2404)): 高需求，已开放超过两个月，建议优先推进。
- **待审阅 PR**:
  - **`feat: add deltachat gateway`** ([#3063](https://github.com/sipeed/picoclaw/pull/3063)): 新网关支持，已提交两天，建议审阅。
  - **`feat(provider): add NEAR AI Cloud provider`** ([#2917](https://github.com/sipeed/picoclaw/pull/2917)): 新 LLM 提供商，已开放三周，标记为 `[stale]`，如无冲突应考虑合并或关闭。
  - **`fix(agent): retry empty llm response`** ([#2983](https://github.com/sipeed/picoclaw/pull/2983)): 修复核心推理循环中的重试问题，已开放 9 天，应尽快审核。
  - **`fix(web): read full session history for Web UI display`** ([#2990](https://github.com/sipeed/picoclaw/pull/2990)): 对应一个用户反馈强烈的 UI Bug ，已开放 8 天。
- **【重点】安全问题**:
  - 报告的十几个安全问题 ([#3068 - #3082](https://github.com/sipeed/picoclaw/issues?q=is%3Aissue+is%3Aopen+label%3ASecurity+created%3A2026-06-09)) 是项目的重大安全风险，必须立即组织 Review 并制定修复计划。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为一名 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 NanoClaw 项目数据，我为您生成了 2026 年 6 月 10 日的项目动态日报。

---

### NanoClaw 项目日报 | 2026-06-10

**项目名称:** NanoClaw
**数据来源:** github.com/qwibitai/nanoclaw
**分析日期:** 2026-06-10
**分析师:** AI 开源项目分析师

---

### 1. 今日速览

今日 NanoClaw 项目整体**非常活跃**，但表现形式偏向于内部维护和大量历史 PR 的收尾工作，而非新的重大功能讨论。具体表现为：(1) **PR 合并量巨大**：过去 24 小时内合并/关闭了 40 个 PR，虽然其中大部分是带有 `[Status: Pending Closure]` 标签的早期提案，但这标志着项目正在积极清理历史积压；(2) **New Issue 活跃度低**：仅有一个新 Issue 更新，且为四月份创建的老议题，社区新功能讨论氛围暂时平静；(3) **Bug 修复与安全增强**：今日合并的 PR 中包含了对飞书交互卡片僵尸状态和 Telegram 配对码安全性的重要修复，显示了项目对稳定性的关注。综合来看，项目正处于**高强度“清理”和“打磨”阶段**，为下一阶段的功能迭代奠定了坚实基础。

### 2. 版本发布

**无**

### 3. 项目进展

今日项目在**代码清理、安全修复、文档完善**方面取得了显著进展。虽然合并的 40 个 PR 多为截止今日关闭的历史提案，但这有效降低了项目 Issues/PRs 的积压量，提升了项目健康度。关键进展包括：

- **安全与稳定性修复合并**：
    - **PR #2718** ([链接](https://github.com/qwibitai/nanoclaw/pull/2718))：修复了飞书渠道在 `agent-runner` 异常退出后，交互卡片卡在“运行中”状态的 **Bug**。这是一个重要的生产环境稳定性修复。
    - **PR #2722** ([链接](https://github.com/qwibitai/nanoclaw/pull/2722))：将 Telegram 配对码生成从 `Math.random` 替换为 `crypto.randomInt`，**增强了安全性**，防止序列被预测。
    - **PR #2723** ([链接](https://github.com/qwibitai/nanoclaw/pull/2723))：新增了一个“金融尽职调查 Agent”的技能（Finance dd agent），丰富了项目的生态技能库。

- **大量历史 PR 收尾**：项目今日关闭了大量自 2 月以来创建、带有 `[Status: Pending Closure]` 标签的 PR（如 #212、#337、#357、#379 等）。这些 PR 提案了 `WebUI控制面板`、`Prompt链条日志记录`、`外部Markdown种子文件`、`JSDoc文档完善` 等丰富功能。虽然最终未被合并，但清理这些长期未决的提案使项目路线图更加清晰。

### 4. 社区热点

- **最受关注 Issue：#1690** ([链接](https://github.com/qwibitai/nanoclaw/issues/1690))：该 Issue 提出了一个“多运行时 Agent SDK 抽象层”，主张允许不同的 Agent SDK（如 Claude、Codex）像频道一样作为模块化技能安装。虽然创建于 4 月，但今日仍有更新，收获了 3 个 👍 和 5 条评论。这反映了社区对**打破单一运行时限制、拥抱多元化模型接入**的强烈诉求，是 NanoClaw 未来向 Agent 中心化平台演进的关键信号。

- **活跃讨论 PR：#2722** ([链接](https://github.com/qwibitai/nanoclaw/pull/2722))：修复 Telegram 配对码安全漏洞的 PR 引起了社区关注。尽管评论数未明确，但安全相关议题通常能引发开发者对项目安全实践的讨论。其关切的本质是：**开源项目的安全性设计，尤其是在身份验证这类关键环节，必须恪守最佳实践**。

### 5. Bug 与稳定性

今日报告并修复了 1 个生产环境 Bug，另有 1 个安全漏洞被修复。

| 严重程度 | Bug / 问题描述 | Issue / PR 链接 | 状态 |
| :--- | :--- | :--- | :--- |
| **严重** | **飞书交互卡片状态“僵尸”问题**：`agent-runner` 进程因超时被杀死后，飞书的交互式卡片会永久显示“运行中”（运行中），无法更新状态。 | [PR #2718](https://github.com/qwibitai/nanoclaw/pull/2718) | **已合并** |
| **严重** | **Telegram 配对码可预测性**：`generateCode` 函数使用 `Math.random()` 生成用于注册和提升拥有者权限的配对码，码值可被预测，存在安全风险。 | [PR #2722](https://github.com/qwibitai/nanoclaw/pull/2722) | **开放中（待合并）** |

### 6. 功能请求与路线图信号

- **核心信号：多运行时支持（抽象层）**：Issue **#1690** ([链接](https://github.com/qwibitai/nanoclaw/issues/1690)) 提出的“Multi-runtime agent SDK abstraction”是当前最重要的路线图信号。虽然尚未被正式接受，但其设计思想与社区对灵活集成的需求高度契合，有望成为下一个里程碑的核心特性。
- **可能的演进方向**：
    - **WebUI 控制面板**：PR #212 提案的 WebUI 虽已关闭，但随着 #1202 中“Agent Trace”的轻量级 UI 以及 #1285 的“直接运行器模式”等组件的成熟，一个更成熟的 WebUI 可能会被重新提上议程。
    - **文档与开发体验**：PR #2721 ([链接](https://github.com/qwibitai/nanoclaw/pull/2721)) 新增的关于自定义、技能模型和指南的文档，表明项目正在强化“基于技能（Skills-based）的开发模式”。这预示着未来的版本将更加强调模块化和易于定制的开发体验。

### 7. 用户反馈摘要

- **对模块化集成的渴望**：在 Issue **#1690** 中，用户 `chiptoe-svg` 明确表达了希望将不同 Agent SDK 像“/add-telegram”一样作为技能无缝集成的需求。这表明高级用户不满足于单一模型，希望构建更复杂的、利用不同模型优势的 Agent 工作流。
- **对安全实践的重视**：PR #2722 的修复，直接回应了安全意识较强的用户的担忧。社区认可将随机数生成从 `Math.random` 迁移到密码学安全的 `crypto.randomInt`，这能增强用户对项目安全性的信任感。
- **对文档质量的认可**：PR #379、#380 等合并的文档类 PR，虽然规模小，但反映了社区正在积极完善项目文档，这是一个成熟和健康社区的标志。

### 8. 待处理积压

- **开放中的安全修复 PR**：
    - **PR #2722** ([链接](https://github.com/qwibitai/nanoclaw/pull/2722))：Telegram 配对码安全漏洞修复。此 PR 已提交且逻辑清晰，应尽快审查并合并，以弥合安全缺口。
- **阻碍项目进度的开放性提案**：
    - **Issue #1690** ([链接](https://github.com/qwibitai/nanoclaw/issues/1690))：多运行时抽象层。该提案已存在两月，且代表了核心演进方向。维护者**应该在此 Issue 中给出明确反馈**，是接受并纳入路线图，还是指出其与现有架构的冲突而予以拒绝，以避免社区投入错误的贡献方向。
- **长期未响应的高价值 Issue**：
    - 未发现。但请关注所有标记为 `Status: Blocked` 的历史 PR，虽然今日已大量清理，但确保它们被正确标记和归档，避免信息孤岛。

---
*本日报由 AI 自动生成，数据来源于指定时间段的 GitHub 活动。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-06-10

---

## 1. 今日速览

过去 24 小时项目保持高活跃度：共处理 **5 条 Issue**（新开 1 条、关闭 4 条）和 **8 条 PR**（新开 1 条、合并/关闭 7 条）。修复集中在 Telegram 交互细节（缺少打字指示器、自定义 provider 回退、PII 误报）、Agent 配置死标志以及 cron 任务交付问题。社区贡献者 raskevichai、vernonstinebaker、DonPrus 等积极参与，跨内存同步特性（#711）也已合并落地。整体项目健康度良好，但仍有一个 **待合并的修复 PR（#948）** 需要维护者关注。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 7 个 PR 主要推动了以下修复与功能增强：

| PR | 内容 | 状态 |
|----|------|------|
| #945 | **修复 PII 误报**：在 `matchPhone` 中添加 `isDateLike()` 守卫，拒绝将 ISO 日期/时间模式（如 `2026-06-02 20:17`）误判为电话号码。对应 Issue #944。 | ✅ 已合并 |
| #946 | **Agent 系统提示工具过滤**：新增 `filterToolsForPromptText`，仅将 `always` 组的工具包含在文本提示中，动态 MCP 工具通过原生 API tool-calling 传递，减少提示噪声。 | ✅ 已合并 |
| #947 | **新增 Evolink 提供商**：将 Evolink（多模型网关）作为一等 OpenAI 兼容提供商加入，支持 GPT-5、Gemini、DeepSeek 等。配置便捷，直接使用 Bearer token 认证。 | ✅ 已合并 |
| #943 | **Telegram 打字指示器修复**：按下内联按钮（如 `callback_query`）时，现在会显示“正在输入…”指示器，消除 5~30 秒的静默等待。对应 Issue #942。 | ✅ 已合并 |
| #940 | **自定义 provider 模型列表查询**：修复当用户选择自定义 OpenAI 兼容提供商时，NullClaw 不再回退到硬编码的 Claude 模型列表，而是真实查询 `base_url/v1/models`。对应 Issue #936。 | ✅ 已合并 |
| #939 | **`compact_context` 死标志修复**：Agent 配置中的 `compact_context` 标志现在被运行时正确读取，之前始终执行上下文压缩。对应 Issue #937。 | ✅ 已合并 |
| #711 | **跨内存同步（跨实例记忆）**：为 Agent 添加确定性内存事件流，允许在不同 Agent 实例间同步用户偏好等记忆。该特性为长期功能，今日正式合并。 | ✅ 已合并 |

**总结**：项目今日修复了 5 个用户报告的问题，新增 1 个第三方提供商支持，并落地了跨内存同步这一重要基础能力，整体向前迈进较大。

---

## 4. 社区热点

**最活跃 Issue / PR 组合**  
- **#941（Open）**：Agent 类型定时任务不启动子进程，导致 Telegram 消息从未发送。该 Issue 于 5 月 31 日创建，6 月 9 日迎来社区贡献者 DonPrus 提交修复 PR #948（当前为 Open 待合并状态）。  
  → Issue 链接：https://github.com/nullclaw/nullclaw/issues/941  
  → PR 链接：https://github.com/nullclaw/nullclaw/pull/948

**背后诉求**：用户希望 cron job 的 agent 子进程能正确继承交付元数据，将结果送达指定渠道。这是一个影响核心定时任务功能的 Bug，社区关注度最高。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue # | 描述 | 当前状态 |
|----------|---------|------|----------|
| 🔴 严重 | #941 | Agent 定时任务不启动子进程，Telegram 消息永不到达。已提交修复 PR #948 | 待合并 |
| 🟠 中等 | #944 | PII 脱敏器误将 `date` 命令输出中的时间格式标记为电话号码，导致时间戳被替换为 `[PHONE_X]`。已修复（#945） | 已关闭 |
| 🟠 中等 | #942 | Telegram 内联按钮无打字指示器，用户无法感知处理进行中。已修复（#943） | 已关闭 |
| 🟡 低 | #936 | 自定义 OpenAI 兼容 provider 在 `/models` 菜单中回退到硬编码 Claude 模型。已修复（#940） | 已关闭 |
| 🟡 低 | #937 | `compact_context` 配置项是死标志，所有 Agent 强制压缩上下文。已修复（#939） | 已关闭 |

**回归情况**：无明确回归问题被报告。

---

## 6. 功能请求与路线图信号

- **#947**（已合并）新增 Evolink 提供商：表明项目有意扩展对多模型网关的官方支持，类似合作可能在未来版本继续出现。
- **#711**（已合并）跨内存同步：标志着项目开始构建多 Agent 协作的基础设施，后续可能围绕记忆同步、Agent 间通信展开更多特性。
- **#948**（待合并）cron 交付归属修复：虽为 Bug 修复，但其中对 `once-agent` 处理逻辑的调整（保持交付路由标记）可视为对 cron 功能可用性的增强。

暂无来自 Issue 或 PR 的新增功能请求（Feature Request），上述两项修复本身已包含功能增强。

---

## 7. 用户反馈摘要

从 Issue 描述中可以提炼以下用户痛点与使用场景：

- **定时任务可靠性**（#941）：用户 `weissfl` 报告配置了 `job_type: "agent"`、`delivery_mode: "always"` 和 `delivery_channel: "telegram"` 的定时任务，但子进程从未启动。用户期望 cron agent 能像手动执行一样正常工作。
- **自定义 provider 兼容性**（#936）：用户 `weissfl` 尝试使用自定义 OpenAI 兼容API时，NullClaw 完全不查询其模型列表，而是使用硬编码的 Claude 模型。用户希望获得真正的 BYOM（自带模型）体验。
- **PII 脱敏误伤可用性**（#944）：用户 `vernonstinebaker`（同时也是修正者）指出系统日期输出被错误脱敏，导致 Agent 获取的时间不可用。用户认为脱敏应针对真正的电话号码，而非通用数字序列。
- **交互体验缺失**（#942）：用户 `weissfl` 抱怨内联按钮没有打字指示器，在模型处理期间（5~30 秒）体验“死寂”，影响使用流畅度。
- **配置死字段**（#937）：用户 `weissfl` 发现 `compact_context` 配置项虽被解析但从未被使用，使配置中对历史压缩的控制无效。

**满意方面**：上述 bug 大部分已快速修复（日期 5/27~6/02 报告的 Issues 在本日或之前关闭），社区响应积极。

---

## 8. 待处理积压

| 项目 | 状态 | 创建日期 | 最后更新 | 说明 |
|------|------|----------|----------|------|
| #948 | PR Open | 2026-06-10 | 2026-06-10 | 修复 #941（cron agent 交付归属），需要维护者审查与合并 |
| #941 | Issue Open | 2026-05-31 | 2026-06-09 | 等待修复 PR 合并后自动关闭，建议尽快合并 #948 |

**提醒**：#941 是用户报告的严重功能缺陷，对应修复 PR #948 已由社区贡献者提交，建议维护者优先审核合并，以恢复 cron agent 任务的正常交付。

---

*日报基于 GitHub 数据自动生成，数据截止 2026-06-10 06:00 UTC。*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我根据您提供的 IronClaw 项目 GitHub 数据，生成了以下 2026-06-10 的项目动态日报。

---

# IronClaw 项目动态日报 | 2026-06-10

## 1. 今日速览

项目今日处于**极度活跃**状态。核心团队正围绕 **Reborn 生产就绪 (Production Cutover Readiness)** 这一关键里程碑进行密集冲刺，同时社区贡献也相当积极。24 小时内共产生 46 条 Issue 和 50 条 PR，其中大部分为新提交的待处理项，反映了团队在并行推进多项功能开发、Bug 修复和测试覆盖方面的强劲势头。虽然存在少量关键 Bug，但项目整体健康度较高，正处于功能大幅迭代和稳定性加固并行的关键阶段。

## 2. 项目进展

今日无新版本发布，但核心团队在多个关键功能线上取得了重大进展，尤其是在 **Reborn 架构的“生产就绪”** 和 **通用附件支持** 两大方向。

**已合并/关闭的重要 PR 与 Issue (今日关闭 2 个 PR，5 个 Issue):**

-   **Close: #4447, #4446 – Reborn OpenAI 兼容 API 迁移结束**：这组 Issue 的关闭标志着 Reborn 对 OpenAI 兼容 API 的支持（包括流式传输）已通过兼容性和安全性测试，迁移工作完成。这为开发者提供了更通用的接入方式。
-   **Close: #4604 – Reborn WebUI v2 缺乏浏览器驱动 E2E 测试**：作为任务关闭，表明团队已识别到测试覆盖缺口，并通过 #4632 等系列 Issue 开始了系统性构建。
-   **Close: #4609 – Reborn WebUI v2 认证审计**：认证审计任务已完成，保障了新 WebUI 的身份验证安全。
-   **Close: #4591 – Reborn 操作员命令平面基础**：为 Reborn 设置/配置/诊断/生命周期管理建立了基础 API 层，是提升运维能力的关键一步。
-   **Close: #4447, #4446 (前述)**：如上所述。

**项目整体迈进的步伐：**
项目重心已从简单的功能添加转向 **系统集成、安全生产和架构清理**。大量 PR 围绕“Reborn 生产就绪” (#3026) 展开，包括就绪诊断、生产图验证、PostgreSQL 生产配置等，表明项目正从实验性阶段迈向准生产级。同时，对“通用附件”支持的重构 (#4644) 也已启动，并有多项 PR 被创建，这是提升用户体验的关键功能。

## 3. 社区热点

今日讨论最活跃的 Issue 和 PR 主要集中在 **Reborn 生产就绪**和 **关键 Bug** 根因分析上。

-   **最活跃 Issue：** **[#3026] Epic: Reborn production wiring and cutover readiness** [链接](https://github.com/nearai/ironclaw/issues/3026)
    -   **热度分析**：作为 Reborn 生产就绪的核心史诗，它汇集了大量子 Issue（如 #4551, #4621, #4620）的讨论。社区和核心贡献者围绕如何构建、验证生产图，避免服务缺失或配置不当导致流量问题进行了深度交流。这是当前项目稳定的“北极星”。

-   **最活跃 Bug Issue：** **[#4642] Strict-mode providers' null-for-unset-optionals rejected by capability-port validation** [链接](https://github.com/nearai/ironclaw/issues/4642)
    -   **热度分析**：该 Bug 影响面极广（most first-party tools）。社区用户和开发者对“严格模式 LLM 提供者发送 `null` 给可选参数却被 Reborn 验证器拒绝”这一行为表达了强烈关注，因为这是生产环境中 `DeepSeek` 等提供者的标准行为。此 Issue 的修复优先级预计会非常高。

-   **最受关注的 PR (因评论数较少，按重要性判断)：** **[#4600] Add Slack personal DM outbound targets** [链接](https://github.com/nearai/ironclaw/pull/4600)
    -   **热度分析**：这是一项大型 PR，它不仅仅是一个 Bug 修复，而是实现了 Slack 个人 DM 的出站目标支持。这是构建 Slack 频道路由个人/团队代理 (#4625) 功能的基础，标志着 Reborn 在渠道能力上的重要扩展，社区对此功能期待已久。

## 4. Bug 与稳定性

今日报告的 Bug 问题影响面较广，覆盖了核心功能、工具链和用户界面。

| 严重程度 | Issue / PR | 标题 | 简述 | 是否有 Fix PR |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | [#4642](https://github.com/nearai/ironclaw/issues/4642) | Strict-mode providers' null-for-unset-optionals rejected by capability-port validation | 严格模式 LLM 提供者（如 DeepSeek）发送的 `null` 值被 Reborn 验证器拒绝，导致部分工具调用失败，影响大部分第一方工具。 | 无 |
| **严重** | [#4548](https://github.com/nearai/ironclaw/issues/4548) | Chat completion request serializes duplicate top-level `model` field when tools are included | 当请求包含工具时，序列化会产生重复的 `model` 字段，导致 DeepSeek API 返回 400 错误。 | 无 |
| **中等** | [#4640](https://github.com/nearai/ironclaw/issues/4640) | [bug] Reborn gsuite google-calendar list_events returns oldest/unordered events | `google-calendar` 扩展的 `list_events` 在无排序和时间下限时，返回了最旧的事件，导致“查询我接下来的会议”返回错误结果。 | 无 |
| **轻微** | [#4673](https://github.com/nearai/ironclaw/issues/4673) | [Reborn] NEAR AI provider configuration cannot be saved after successful Test connection | 在 Reborn 中配置 NEAR AI 提供者时，“测试连接”成功但“保存”按钮无效，配置无法持久化，影响用户体验。 | 无 |

## 5. 功能请求与路线图信号

今日涌现了大量与 **Reborn 生产就绪** 和 **用户体验增强** 相关的功能请求，部分已有对应 PR 在执行，预计将进入下一阶段开发。

-   **高优先级：**
    -   **[#4644] Universal attachments across all channels** [链接](https://github.com/nearai/ironclaw/issues/4644) - 这是一个重要的功能 Epic，旨在统一跨渠道的附件处理。它获得了多项 PR（#4654, #4655, #4668, #4670, #4672）的直接支持，涉及格式注册、传输线集成和字节存储，说明团队正集中力量攻克此功能。

-   **中优先级：**
    -   **[#4625] Slack channel-routed personal and team agents** [链接](https://github.com/nearai/ironclaw/issues/4625) - 增强 Slack 渠道，支持个人和团队代理通过不同路由交互。相关 PR #4600 已提交，该功能是提升协作体验的关键。
    -   **[#4628] Admin-shared tools and skills with per-user auth** [链接](https://github.com/nearai/ironclaw/issues/4628) - 多租户场景下的核心需求，允许管理员统一配置共享工具和技能，并按用户授权。与 PR #4544 (Scoped lifecycle admin) 目标一致，是 Reborn 走向企业级应用的重要功能。
    -   **[#4647] Unified (omni) search** [链接](https://github.com/nearai/ironclaw/issues/4647) - 提升 Reborn WebUI v2 可用性的关键功能，实现跨线程、文件、扩展的全域搜索。
    -   **[#4667] Support Ask-gated capability approvals in Reborn REPL** [链接](https://github.com/nearai/ironclaw/issues/4667) - 提升开发体验，允许在 REPL 中处理需要用户授权的能力（Ask-gated capabilities），这在调试和开发时会非常有用。

## 6. 用户反馈摘要

从当日的 Issue 和 PR 评论中，可以提炼出以下真实的用户痛点与诉求：

-   **与特定 LLM 提供者的兼容性是关键痛点**：用户指出使用 `DeepSeek` 等提供者时遇到两个关键 Bug（重复 `model` 字段、`null` 值校验失败）。这表明用户对可切换多种主流模型有强烈需求，项目对非 OpenAI 标准的适配需要更加谨慎和健壮。
-   **工具的稳定性和准确性直接影响信任**：`google-calendar` 返回错误顺序的会议信息 (#4640) 和配置无法保存 (#4673) 这类 Bug 会严重削弱用户对 AI 助手功能的信任和日常使用意愿。
-   **对生产环境运维能力的关注**：大量关于 Reborn 生产就绪 (#3026) 和运维管理 (#4591) 的讨论表明，用户（或潜在的企业用户）不仅需要好的功能，更关心如何安全、可控地将项目部署到生产环境中。
-   **对新协作和集成功能的期待**：Slack 渠道的增强 (#4625)、管理员权限管理 (#4628) 等功能的提出，反映了用户期望 IronClaw 从一个个人工具向团队协作平台演进的趋势。

## 7. 待处理积压

以下 Issue 和 PR 存在较长时间，且在当前冲刺周期内尚未获得足够关注，建议维护者关注。

-   **[#88] feat: Security hardening (device pairing, elevated mode, safe bins, media URL validation)** [链接](https://github.com/nearai/ironclaw/issues/88)
    -   **状态**：P2-P3 优先级，创建于 4 个月前，至今仍在开放状态。
    -   **提醒**：涉及到设备配对、提升模式、安全库等核心安全功能。随着 Reborn 走向生产就绪，这些安全加固项的重要性将日益凸显，建议分配资源评估和推进，以避免成为后续的潜在风险点。

-   **长期未响应的工作：** `#4666` 和 `#4665`
    -   **提醒**：这两条是关于代码文件大小超过架构规定阈值（`slack_host_state.rs` 和 `slack_host_beta.rs`）的追踪 Issue。虽然不直接影响功能，但代码膨胀是技术债务的典型信号，长期不处理会导致可维护性下降，阻碍新功能开发。建议在 Sprint 规划中安排重构任务。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

## LobsterAI 项目日报 – 2026-06-10

### 1. 今日速览
- 过去24小时项目保持较高活跃度：共处理2条新Issue、5条Pull Request（其中4条已完成合并/关闭），无新版本发布。
- 团队重点推进**任务完成通知机制**与**数据备份迁移**两大功能，相关PR已全部合并，标志着Cowork协作流程和用户体验的显著提升。
- 社区反馈聚焦于**跨模型子任务协作**（Issue #2132）与**支持Hermes Agent**（Issue #2131），反映出用户对多模型编排和Agent扩展性的强烈需求。
- 一项关键Bug修复（导出与代码复制问题）目前处于待合并状态，预计近期将进入主干。

### 3. 项目进展
今日共合并/关闭4条重要PR，推动以下功能或修复落地：

- **任务完成通知**（PR #2130、#2134）：  
  - [PR #2130](netease-yandao/LobsterAI PR #2130) 实现了隐私安全的任务完成提醒，当LobsterAI不在前台时，通过系统通知、macOS Dock角标、Windows任务栏闪烁等方式告知用户，并可在设置中开关。  
  - [PR #2134](netease-yandao/LobsterAI PR #2134) 在此基础上完善了主窗口关闭/销毁后的恢复机制，确保渲染进程通知处理器就绪后再打开目标Cowork会话，同时保持macOS通知中心的点击有效。  
  - **意义**：解决了用户执行长任务时不得不保持应用在前台的痛点，提升了多任务场景的可用性。

- **数据备份与迁移**（PR #2136）：  
  - [PR #2136](netease-yandao/LobsterAI PR #2136) 增加了数据备份与迁移功能，涵盖renderer、docs、main等模块。  
  - 同时[PR #2135](netease-yandao/LobsterAI PR #2135) 临时关闭了数据备份功能（chore），推测为配合后续优化或防止冲突。  
  - **意义**：为数据持久化和跨环境迁移奠定基础，是项目迈向生产级稳定性的重要一步。

### 4. 社区热点

- **Issue #2131 – 支持Hermes Agent**  
  [链接](netease-yandao/LobsterAI Issue #2131)  
  用户询问是否有计划支持Hermes Agent。Hermes Agent是近期开源的通用智能体框架，LobsterAI若能集成可显著扩展Agent生态。该Issue获得1条评论，反映出社区对“插件式Agent”的期待。

- **Issue #2132 – 跨模型子任务调用**  
  [链接](netease-yandao/LobsterAI Issue #2132)  
  用户描述了主任务（M3模型规划+验收）与子任务（DeepSeek快速执行）的协作场景，并指出当前跨模型子任务存在会话不匹配（gateway function call而非sessions_spawn）问题。  
  该Issue详细分析了根因并提出了修复方案（同模型子任务通知机制可借鉴至跨模型场景，以及子任务主动通知主任务的机制）。**暂无评论**，但问题描述专业、方案完整，是当前社区最受关注的功能请求之一。

### 5. Bug 与稳定性

- **PR #2133 – 导出与代码复制Bug修复**（待合并）  
  [链接](netease-yandao/LobsterAI PR #2133)  
  涉及renderer和cowork模块，修复了导出和代码复制时可能出现的错误。该Bug未在Issue中单独报告，但PR已提交，目前处于Open状态，预计近期会合并。  
  **严重程度**：中等，影响用户体验，但无崩溃或数据丢失风险。

- 其余已合并的PR未发现新增Bug。

### 6. 功能请求与路线图信号

| 功能请求 | 来源 | 关联PR / 信号 |
|----------|------|----------------|
| 支持Hermes Agent | Issue #2131 | 暂无PR，属用户新需求 |
| 跨模型子任务协作 | Issue #2132 | 用户已给出详细修复方案，可能被纳入下一版本 |
| 任务完成通知（已实现） | PR #2130 / #2134 | 已合并，下个版本可用 |
| 数据备份与迁移（已实现） | PR #2136 | 已合并，但临时关闭，等待后续稳定 |

**路线图信号**：从社区反馈和PR趋势看，下阶段可能优先处理“跨模型协作”相关需求，并进一步完善通知系统与数据持久化。

### 7. 用户反馈摘要

- **正向反馈**：用户对Cowork任务完成通知功能的实现表示肯定（PR #2130、#2134未直接显示用户评论，但从Issue活跃度看，该功能是社区长期诉求）。
- **痛点**：  
  - 跨模型子任务调用中会话管理不清晰（Issue #2132）；  
  - 希望支持更多Agent框架（Issue #2131）；  
  - 导出和代码复制偶发Bug（PR #2133）。
- **建议**：用户“woxinsj”在Issue #2132中提出的“子任务完成后主动通知主任务”机制，以及“同模型子任务通知机制可借鉴”的思路，对设计扩展性架构有参考价值。

### 8. 待处理积压

| 条目 | 类型 | 创建时间 | 最后更新 | 状态 | 备注 |
|------|------|----------|----------|------|------|
| [Issue #2131](netease-yandao/LobsterAI Issue #2131) – 支持Hermes Agent | 功能请求 | 2026-06-09 | 2026-06-09 | OPEN | 待确认是否纳入路线图 |
| [Issue #2132](netease-yandao/LobsterAI Issue #2132) – 跨模型子任务调用 | 功能请求/Bug | 2026-06-09 | 2026-06-09 | OPEN | 已有用户方案，等待维护者回应 |
| [PR #2133](netease-yandao/LobsterAI PR #2133) – 导出和代码复制Bug修复 | Bug修复 | 2026-06-09 | 2026-06-09 | OPEN | 建议尽快合并以修复用户问题 |

**提醒维护者**：Issue #2132 提供了详细分析，若采纳可大幅提升跨模型编排体验；PR #2133 如无冲突应优先合并，避免Bug积累。

---

*本日报基于 GitHub 公开数据生成，数据截止时间 2026-06-10 00:00 UTC。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，以下是为您生成的 CoPaw 项目动态日报：

---

## CoPaw 项目动态日报 | 2026-06-10

### 1. 今日速览

今日 CoPaw 项目社区活跃度极高，Issue 与 PR 的更新量均超过 30 条，显示出强劲的开发与讨论势头。`v1.1.11-beta.2` 版本已发布，主要修复了浏览器控制相关 Bug。社区讨论焦点集中在模型兼容性、前端性能优化以及借鉴外部项目（如 Hermes Agent）功能特性上。项目方面，多个重要 Bug 修复和功能增强的 PR 已合并，同时一项涉及后端架构升级的**破坏性变更**（迁移至 AgentScope 2.0）正在推进中。

### 2. 版本发布

- **[v1.1.11-beta.2](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.11-beta.2)**
  - **更新内容**：此版本为小型的 Beta 更新。
    - **新功能**：为 `browser_control` 增加了页面坐标点击支持。
    - **Bug 修复**：修复了跨浏览器切换时的 CDP 超时参数和浏览器配置文件隔离问题。
  - **破坏性变更**：无。
  - **迁移注意事项**：无特殊迁移需求，建议所有 Beta 版本用户升级以获取最新修复。

### 3. 项目进展

- **Bug 修复**：修复了多个影响稳定性的关键 Bug，包括：
  - 解决了会话文件名在 Windows 上因用户 ID 重复而导致溢出，以及**桌面端 Agent 间调用失败**的问题 ([PR #5036](https://github.com/agentscope-ai/QwenPaw/pull/5036))。
  - 修复了 `/compact` 命令及自动压缩功能在未设置 `active_model` 时，**忽略模型自身 `max_input_length` 配置**的问题 ([PR #5021](https://github.com/agentscope-ai/QwenPaw/pull/5021))。
  - 修复了 Tauri 桌面版**无法打开外部链接**及**文件下载被阻止**的问题 ([PR #5044](https://github.com/agentscope-ai/QwenPaw/pull/5044))。
  - 处理了 DeepSeek API 因工具函数名包含点号（`.`）而**拒绝调用**的兼容性问题 ([PR #5045](https://github.com/agentscope-ai/QwenPaw/pull/5045))。
  - 修复了 OpenAI 兼容流式解析器中，多个 `thinking/text` 块内的工具调用**互相覆盖**的问题 ([PR #5039](https://github.com/agentscope-ai/QwenPaw/pull/5039))。
  - 解决了 DingTalk 频道在 Agent 输出为空时，**发送空白“处理中”卡片**的问题 ([PR #5061](https://github.com/agentscope-ai/QwenPaw/pull/5061))。
  - 修复了 `WeChatChannel` 在定时任务投递时，返回 `session_id` 而非 `user_id` 导致**微信推送失败**的问题 ([Issue #5060](https://github.com/agentscope-ai/QwenPaw/issues/5060))。

- **新功能与增强**：
  - 新增 **OpenSandbox 插件**，支持 MCP 协议，用于在隔离环境中安全执行代码/命令，增强 Agent 安全性 ([PR #5043](https://github.com/agentscope-ai/QwenPaw/pull/5043))。
  - 增强了 `make-skill` 流程，支持**技能自我进化**，Agent 可在后台自动创建并迭代技能 ([PR #4857](https://github.com/agentscope-ai/QwenPaw/pull/4857))。
  - 为 CloudPaw 插件新增从 **AgentHub 导入 Agent** 的能力，并增强了 A2A（Agent-to-Agent）能力 ([PR #5033](https://github.com/agentscope-ai/QwenPaw/pull/5033))。

- **代码质量与基础设施**：
  - 为 `local_models`、`providers`、`tunnel`、`utils` 等模块新增 **129 个单元测试**，显著提升了测试覆盖率 ([PR #4973](https://github.com/agentscope-ai/QwenPaw/pull/4973))。
  - 新增了覆盖频道层和多 Agent 管理的 **60 个集成测试** ([PR #5058](https://github.com/agentscope-ai/QwenPaw/pull/5058))。

### 4. 社区热点

- [#5017 [Feature]: 建议关注 Hermes Agent 的发展，借鉴其"学习循环"等优势特性](https://github.com/agentscope-ai/QwenPaw/issues/5017)
  - **热度**：10 条评论，3 个 👍，已关闭。
  - **分析**：这是今日社区讨论最热烈的话题。用户高度认可 CoPaw 的本地化体验，但强烈建议团队关注新兴的 Hermes Agent 项目，尤其是其“学习循环”和“分层记忆系统”等核心创新。这反映了社区对 Agent 自主进化能力的迫切需求，并希望 CoPaw 能集百家之长，保持技术领先。该 Issue 已被关闭，可能意味着项目组已注意到或已有内部规划。

- [#5003 [Bug]: 使用阿里 coding plan qwen3.7-plus 会一直卡住](https://github.com/agentscope-ai/QwenPaw/issues/5003)
  - **热度**：8 条评论，已关闭。
  - **分析**：用户报告了与特定阿里云模型集成时出现的严重问题，即 Agent 在处理编码任务时完全无响应。此问题获得了较多关注，说明用户对主流通用模型的兼容性要求很高，尤其是在使用特定厂商的“编程计划”模型时。

### 5. Bug 与稳定性

- **严重 Bug**：
  - **使用本地千问 3.6-27B 模型对话无响应**：`v1.1.9` 和 `v1.1.10` 版本中，配置本地部署的 Qwen 模型后，提交问题无任何回复。影响面较大，需要紧急排查 ([Issue #4989](https://github.com/agentscope-ai/QwenPaw/issues/4989))。
  - **新建会话后模型配置丢失**：新建会话导致 Models 配置页面加载失败，只能重启应用解决，严重影响用户体验 ([Issue #4666](https://github.com/agentscope-ai/QwenPaw/issues/4666))。

- **中等 Bug**：
  - **工具调用多次后报错**：会话进行若干次工具调用后，所有工具都报 `got an unexpected keyword argument 'arguments'` 错误，疑似代理状态出现问题 ([Issue #5052](https://github.com/agentscope-ai/QwenPaw/issues/5052))。
  - **`/compact` 命令忽略模型配置**：`/compact` 命令进行上下文压缩时，未使用模型实际的 `max_input_length`，而是默认 128K，导致长上下文模型能力被浪费 (已修复，见 [PR #5021](https://github.com/agentscope-ai/QwenPaw/pull/5021))。
  - **WeChat 定时任务推送失败**：定时任务结果无法推送到微信，根源是 `channel.py` 对用户 ID 的处理逻辑错误 (已修复，见 [Issue #5060](https://github.com/agentscope-ai/QwenPaw/issues/5060))。
  - **前端加载与性能瓶颈**：Windows Desktop 端前端加载不流畅，聊天数据多时切换卡顿、CPU 激增；此外，流式输出长文本时整个电脑异常卡顿。这些问题集中在 Console 前端渲染性能上 ([Issue #5015](https://github.com/agentscope-ai/QwenPaw/issues/5015)， [Issue #4917](https://github.com/agentscope-ai/QwenPaw/issues/4917)， [Issue #4792](https://github.com/agentscope-ai/QwenPaw/issues/4792))。

- **低等 Bug**：
  - 图片预览放大后拖动抖动，影响浏览体验 ([Issue #4993](https://github.com/agentscope-ai/QwenPaw/issues/4993))。
  - Tauri 桌面版启动过慢，从 Python 打包切换后问题明显 ([Issue #5047](https://github.com/agentscope-ai/QwenPaw/issues/5047))。

### 6. 功能请求与路线图信号

- **学习循环与记忆系统**：社区对 Agent 的“学习循环”和“分层记忆系统”呼声很高。`#5017` 与 `#4994` 反映了用户希望 CoPaw 能够像 Hermes Agent 一样，实现技能的自我创造和迭代。项目已合并 `#4857` PR 开始支持技能自我进化，这与该方向一致。
- **独立视觉模型配置**：用户 `#4992` 建议增加独立的视觉模型配置项，当主模型不支持多模态时，自动调用视觉模型处理图片。这是一种实用的“视觉中转站”方案，可能成为即将推出的功能。
- **支持 OpenSandbox**：`#4951` 建议增加安全沙箱支持，已被采纳并合并 ([PR #5043](https://github.com/agentscope-ai/QwenPaw/pull/5043))，已纳入 `v1.1.11` 版本。
- **迁移至 AgentScope 2.0**：`#4727` 是一个**破坏性变更**的 Issue，计划将后端从 AgentScope 1.x 迁移到 2.0。这是一项重大架构升级，预计将影响后续版本的 API 和运行时模型。
- **接入 AgentScope Tracing**：`#4057` 请求在应用启动时集成 AgentScope 的链路追踪（Tracing）功能，建议统一初始化入口，便于用户接入监控平台。

### 7. 用户反馈摘要

- **满意点**：
  - 用户 `tecgic` 在 `#5017` 中盛赞 CoPaw“国内用起来特别舒服”、“本地化做得很到位，设置清晰无门槛，开箱即用”，这是对产品体验的高度认可。
- **痛点与不满**：
  - **模型兼容性问题频发**：用户在 `#4989`、`#5003`、`#4962`、`#5013`、`#5045`、`#5052` 等多个 Issue 中报告了与不同模型（本地 Qwen、阿里、DeepSeek、Kimi、MiniMax）集成的各类问题，包括无响应、思考内容显示异常、工具调用失败等。这表明模型兼容层仍然是稳定性的主要挑战。
  - **前端性能问题突出**：多名用户（`#5015`、`#4917`、`#4792`、`#5047`）抱怨 Console 前端加载卡顿、CPU 激增、切换延迟，甚至在流式输出时导致整个系统卡死。这已成为影响日常使用的核心障碍。
  - **桌面端体验退步**：用户 `#5047` 抱怨自打包方式切换为 Tauri 后，启动速度严重下滑（从“一两分钟变成十几分钟”），并经常无响应，体验明显降级。
  - **微信渠道不稳定**：`#5030` 和 `#4878` 反映了微信频道在主动模式下出现重复回复和推送失败的问题，影响了核心 IM 通道的可靠性。
  - **会话管理不便**：`#4971` 提出切换会话需要多次点击，操作繁琐，建议增加侧边栏直接切换。

### 8. 待处理积压

- **Issue #4057**：[Support AgentScope tracing initialization](https://github.com/agentscope-ai/QwenPaw/issues/4057)，提出已超过一个月，目前处于开放状态且未分配。该功能对于希望监控和优化 Agent 行为的高级用户非常重要，建议优先排期。
- **PR #4669**：[feat(desktop): add tauri auto updater](https://github.com/agentscope-ai/QwenPaw/pull/4669)，已开放超过两周，目前状态为`OPEN`。Tauri 桌面端的自动更新功能是提升用户体验的关键，应加快审查和合并进度。
- **PR #4975**：[feat(console): implement customizable column order in sessions page](https://github.com/agentscope-ai/QwenPaw/pull/4975)，处于“Under Review”状态。此功能是社区用户 `#4770` 的直接需求，应尽快完成审查以改善会话管理体验。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，以下是基于您提供的 ZeroClaw 项目数据生成的 2026-06-10 项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-06-10

**分析师观点：** 项目处于高度活跃期，日均 Issue/PR 更新量（50条）处于高位。社区对 **安全模型（RBAC、MCP、技能权限）** 和 **核心运行时稳定性（上下文预算、Cron、消息丢失）** 的反馈极为强烈，表明项目正从功能扩展阶段进入稳定性与安全合规的深水区。虽然合并率较低（24h内仅 1 PR 合并），但大量高质量 PR 处于待审核状态，可能预示着一次大型版本迭代即将到来。

---

### 1. 今日速览
- **整体状态：** 高度活跃。过去24小时内，社区提交了50条Issue和50条PR，主要集中在 Bug 修复与功能增强两大方向。
- **活跃度评估 (A级):** 社区参与度极高，新 Issue 平均评论数超过 4 条，反映出用户遇到实际困难后积极寻求解决方案的态度。
- **健康度提示：** 代码合并速度（24h内仅1条合并/关闭）低于提交速度，可能导致维护者审核压力增大，建议关注积压 PR 的合并进程。
- **关键矛盾点：** 社区强烈要求引入 **细粒度安全控制** (RBAC、技能权限隔离) 和 **运行时稳定性改进**（上下文预算、Cron 防抖、Telegram 工具调用），但部分高价值 PR 仍处于 `needs-author-action` 或 `blocked` 状态。

### 2. 版本发布
无新版本发布。当前最新版本稳定版为 `v0.7.5`，Beta 版为 `v0.8.0-beta-1`。多个严重 Bug（如 Issue #6646, #6862）仅在 `v0.8.0-beta-1` 中报告，建议关注 `v0.8.0` 的正式发布。

### 3. 项目进展
24小时内合并/关闭的 PR 极少（仅 1 条），但大量在途 PR 标志着关键模块即将得到重大改进。虽然没有合并，但多个重要 PR 进入可接受状态，值得关注：
- **核心运行时优化：** `#7442 [OPEN]` **fix(runtime): make parallel SubAgents and Delegates return reliably** 修复了并行子智能体无法可靠返回的问题，这对复杂任务拆解至关重要。
- **文档与配置：** `#7365 [OPEN]` **docs(book): rework the book and derive provider/config surfaces from source** 计划重写官方文档，并从源码自动生成配置项文档，将极大改善开发者体验。
- **可观测性：** `#7385 [OPEN]` **feat(observability): add turn metadata to observer events** 增加了回合元数据，为调试和监控提供了关键数据支持。
- **网关能力增强：** `#7367 [OPEN]` **feat(gateway): route inbound webhooks per channel alias** 支持按通道别名路由 webhook，是实现多租户的重要一步。

项目整体向 **安全性、可观测性、多租户** 的方向演进，但推进速度受审核流程影响。

### 4. 社区热点
- **#6721 [Bug, 4评论, 高热度]:** **工具搜索 (tool_search) 在延迟加载且启用 webhook 时静默挂起120秒后自动拒绝。** 这是当前影响 MCP（Model Context Protocol）工具链的核心问题，用户 `nick-pape` 指出配置默认情况下会导致生产环境工作流阻塞。社区对 MCP 工具的可用性极为关注。
    - 链接: [Issue #6721](https://zeroclaw-labs/zeroclaw/issues/6721)
- **#5982 [Feature, 9评论, 高热度]:** **为多租户代理部署添加按发送者角色访问控制 (RBAC)。** 用户 `metalmon` 提出的需求得到广泛讨论，反映了社区从个人使用向企业级部署的转变需求。这是安全方向最受关注的功能请求。
    - 链接: [Issue #5982](https://zeroclaw-labs/zeroclaw/issues/5982)

### 5. Bug 与稳定性
今日报告的 Bug 主要集中在以下 **P1 (严重)** 和 **P2 (高)** 级别问题，部分已有修复 PR：

| 严重级别 | Issue / 标题 | 问题摘要 | 修复状态 |
| :--- | :--- | :--- | :--- |
| **S1 (Workflow Blocked)** | [#6034](https://zeroclaw-labs/zeroclaw/issues/6034) 单轮对话以及多轮对话会出现丢失 user message的现象 | 用户消息丢失，导致工作流完全阻塞。 | 未关联PR |
| **S1 (Workflow Blocked)** | [#6721](https://zeroclaw-labs/zeroclaw/issues/6721) tool_search not in default_auto_approve → deferred_loading+webhook silently hangs | MCP 工具在 Webhook 模式下无响应，静默失败。 | 未关联PR |
| **S1 (Workflow Blocked)** | [#5808](https://zeroclaw-labs/zeroclaw/issues/5808) Default 32k context budget is exceeded by system prompt | 默认上下文预算被系统提示和工具定义耗尽，导致循环修剪。 | 未关联PR |
| **S2 (Degraded Behavior)** | [#5844](https://zeroclaw-labs/zeroclaw/issues/5844) Too much emphasis on memory | 系统提示过分强调记忆，导致当前Cron任务或其他任务偏离预期。 | 未关联PR |
| **S2 (Degraded Behavior)** | [#7376](https://zeroclaw-labs/zeroclaw/issues/7376) zerocode Dashboard hides unavailable/error states | 仪表盘隐藏了错误状态，误导用户。 | PR #7444 |
| **S2 (Degraded Behavior)** | [#6584](https://zeroclaw-labs/zeroclaw/issues/6584) OpenAI-Compatible provider ignores `reasoning` field | 不兼容OpenRouter等提供者的`reasoning`字段。 | PR #7423 |
| **S2 (Degraded Behavior)** | [#7377](https://zeroclaw-labs/zeroclaw/issues/7377) zerocode dark themes can inherit unreadable foreground text | TUI主题可读性问题。 | 未关联PR |

**关键发现：** 运行时稳定性（消息丢失、上下文溢出）依然是阻塞开发者的首要问题。

### 6. 功能请求与路线图信号
- **安全性与多租户 (强烈信号):**
    - **RBAC (Issue #5982)** 是社区最强烈的呼声，可能会被纳入 v0.9.0 规划。
    - **按技能权限隔离 (Issue #5775)** 和 **Per-sender RBAC** 共同指向了企业级部署需求。
    - **Composio 工具动作范围过滤 (Issue #6917)** 是集成第三方服务时的必要安全控制。
- **可配置性与用户体验:**
    - **Discord 频道白名单 (Issue #6378)** 和 **Config UX 一致性 (Issue #7117)** 表明社区希望更精细、统一的配置体验。
    - **持久化缓存 Token 成本核算 (Issue #7248)** 反映了对成本透明度的需求。
- **即将纳入的特性：**
    - **按渠道别名路由 Webhook (PR #7367)** 已在 PR 阶段，很可能进入 v0.8.0 正式版。
    - **对 MCP 工具的安全限制 (Issue #6876)** 已被标记为 `accepted`，将澄清或修复 `allowed_tools` 对 MCP 无效的问题。

### 7. 用户反馈摘要
- **痛点：**
    - **“Zeroclaw 不知道它能添加 Cron。”** (Issue #5862) - 这是一个严重的可用性缺陷，用户认为模型缺乏对自身工具的了解，导致无法执行定时任务。
    - **“过分强调记忆。”** (Issue #5844) - 用户 `databillm` 指出在 Cron 任务中，系统提示中对记忆的优先级过高，导致智能体行为偏离了当前指令。
    - **“在Telegram上使用搜索工具时完全不触发。”** (Issue #6646) - 用户 `icemann521` 反馈在 `v0.7.5` 的 Telegram 频道上，两个核心工具（web_search_tool, web_fetch）无法工作，严重影响了用户体验。
- **满意点：**
    - **社区对安全功能扩展的积极响应：** 从多个安全相关的 Issue（如 #5982, #5775, #6876）看，用户愿意主动参与讨论并提出详细方案，表明对项目未来安全能力的信心。
    - **活跃的 Bug 复现与反馈：** 尽管问题多，但用户提供了详细的日志和复现步骤（如 #6034, #6646），展现了高度的社区协作精神。

### 8. 待处理积压
以下 Issue 和 PR 长期未得到维护者响应或进展缓慢，可能成为项目瓶颈：
- **#5844 [Bug, 2026-04-17]:** “Too much emphasis on memory” - 严重性为 **S2**，已有一个月未有关键回复，无关联 PR。这是用户最常抱怨的 AI 行为不一致问题之一。
    - 链接: [Issue #5844](https://zeroclaw-labs/zeroclaw/issues/5844)
- **#6037 [Bug, 2026-04-23]:** “Cron jobs can be launched repeatedly while still running” - 严重的 Cron 任务失控问题，标记为 `status:in-progress` 但近两个月无更新。
    - 链接: [Issue #6037](https://zeroclaw-labs/zeroclaw/issues/6037)
- **#6916 [Feature, 2026-05-25]:** “process-memory limits on shell/skill_tool subprocess execution” - 这是防止 OOM 的关键安全特性，已 `accepted` 但尚未有关联 PR。
    - 链接: [Issue #6916](https://zeroclaw-labs/zeroclaw/issues/6916)
- **#6973 [PR, 2026-05-27]:** “fix(channels/whatsapp-web): pass LID JIDs unchanged to whatsapp-rust 0.6+” - 关键 WhatsApp 通道的兼容性修复 PR，已等待近两周未合并。
    - 链接: [PR #6973](https://zeroclaw-labs/zeroclaw/pull/6973)

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*