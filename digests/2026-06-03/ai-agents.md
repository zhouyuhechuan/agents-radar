# OpenClaw 生态日报 2026-06-03

> Issues: 429 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-03 03:26 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，现根据您提供的 GitHub 数据，为您呈现 **OpenClaw 项目 2026 年 6 月 3 日报**。

---

# OpenClaw 项目日报 | 2026-06-03

## 今日速览

过去 24 小时内，项目社区持续保持**极高活跃度**，共计产生 429 条 Issues 和 500 条 PR 的更新。核心焦点集中在**Session/Transcript 状态管理**、**消息投递可靠性**以及**平台回归问题**上。虽然有多个高优先级 Bug 被关闭，但大量 P1/P2 级别的稳定性和数据丢失问题仍处于待修复状态，社区的修复 PR 提交速度（尤其是针对 UI 和特定渠道的 Bug）非常迅速，体现了强大的社区自驱力。然而，新版本发布活动停滞，项目整体处于高强度的“维护与修复”攻坚期。

## 版本发布

- 无新版本发布。

## 项目进展

今日虽然没有重大功能合并，但多个关键修复和优化取得了进展，主要集中在解决高复现率的 Bug 和提升系统健壮性：

- **UI/UX 修复**：
    - `#89530` [合并待审核] 解决了 WebChat 中流式消息文本在特定情况下消失的回归问题，直接关联了近日多个 “message-loss” 类 Issue。
    - `#89681` [合并待审核] 修复了 Skills 面板中，切换技能开关后，开关状态会错误转移到列表中下一个技能的 UI 问题。这是一个用户感知极强的体验修复。
- **系统稳定性增强**：
    - `#89673` [合并待审核] 针对 `#87483` 报告的 Session 写锁长期持有问题，添加了“看门狗”机制，能自动回收超过持有者 `maxHoldMs` 的锁，防止请求被永久阻塞。
    - `#89669` [合并待审核] 增强了 Provider Schema 插件钩子的容错性，防止一个损坏的插件导致整个模型推理流程崩溃。
- **特定渠道修复**：
    - `#89659` [合并待审核] 为飞书（Feishu）渠道的消息发送增加了速率限制错误（230020/230006）的重试逻辑，提升消息投递的鲁棒性。
- **文档与协议**：
    - `#89613` [合并待审核] 记录了 Auth Profile 故障转移策略的契约，为开发者理解身份认证行为提供了更清晰的边界。

## 社区热点

今日社区讨论焦点主要集中在以下几个问题上，反映出用户对**Session 状态一致性**和**消息投递可靠性**的高度关注：

1.  **[Bug]：Session_send gives no session found (`#52875`)**
    - **热度**: 21 条评论
    - **分析**: 一个存在已久的回归问题，升级后主代理无法联系其他代理。用户认为核心的 Agent-to-Agent 通信机制出现了问题，这是构建复杂多代理系统的基石，因此引发了持续讨论。

2.  **[Feature/设计]：Track core session/transcript SQLite migration (`#88838`)**
    - **热度**: 17 条评论
    - **分析**: 社区正在激烈讨论如何通过“分支按抽象”（branch-by-abstraction）方法，将 Session 和 Transcript 的状态持久化迁移到 SQLite。这被视为解决 `sessions.json` 无限制增长（导致 OOM，见 `#55334`）和提升性能的关键一步，是项目未来的重要技术路线。

3.  **[Bug]：Windows chat UI regression: input text swallowed, streamed replies often invisible (`#67035`)**
    - **热度**: 14 条评论
    - **分析**: Windows 用户的强烈抱怨。UI 的回归问题严重影响了基础聊天体验，文本输入消失、回复不可见等问题迫使用户必须刷新页面，这被描述为“灾难性”的用户体验下降。

4.  **[Bug]：GHCR 2026.5.28 image emits stale config schema (`#88788`)**
    - **热度**: 12 条评论
    - **分析**: Docker 镜像配置 Schema 与实际代码不同步的问题，导致用户无法启用“Discord 进度评论”等已实现的功能。这暴露了构建和发布流程中的一致性问题。

## Bug 与稳定性

今日报告的 Bug 中有多个回归（Regression）问题，严重程度高，需警惕。

- **P1 (Critical/Highest) - 消息丢失/会话中断**
    - **[#88312]**: Codex 服务端 “turn-completion stall” 再次回归，导致多工具调用失败。这是 `#84076` 问题的复现，已被标记为高优先级。
    - **[#86047]**: Codex 插件批准流程卡顿，导致 Nextcloud Talk 中的 Agent 会话中断。用户被迫回滚版本。
    - **[#87646]**: 飞书频道升级后无法分发消息，报 `TypeError`。*[6月2日已关闭]*
    - **[#86519]**: Telegram 上 Agent 重复发送 2-10 条完全相同回复的回归问题，严重影响用户体验。
    - **[#80715]**: Slack 回复被“静默丢弃”，Agent 成功但消息从未发出，此 Bug 影响信任感。*已有相关 fix PR (#89590)*
- **P2 (High) - 功能/状态异常**
    - **[#55334]**: `sessions.json` 无限增长导致网关 OOM 的内存泄漏问题，根源在于 `skillsSnapshot` 被每个会话重复保存且无清理机制。
    - **[#52249]**: ACP 父子会话状态同步问题，父会话在等待子会话完成后会完全卡死，直到用户手动刷新 UI。
    - **[#72031]**: Bedrock 平台的 `image` 工具认证失败，即使 AWS SDK 凭证已就绪，`requireApiKey` 逻辑依然强制要求 API Key。

## 功能请求与路线图信号

- **[#39604]**: 要求为 `web_fetch` 工具添加 `allowPrivateNetwork` 配置以访问内网。这是一个强大的社区需求（9个👍），但涉及安全风险，维护者正在犹豫是否添加以及如何有效实施。已有相关 PR 在讨论中。
- **[#84216]**: 提议为 UI 侧边栏的 “Recent Sessions” 列表添加下拉式收起/展开功能，以优化小屏或低屏用户的界面体验。
- **[#81061]**: 提出需要一个 `before_route_inbound_message` 钩子，允许插件在消息路由决策之前进行拦截和代理，这为更复杂的渠道桥接和安全策略打开了空间。
- **[#77941]**: 社区提出了“孤儿转录清理”功能，即清理已经被删除，但其索引文件依然占用空间的情况，这是对 `sessions cleanup` 命令的重要补充。

## 用户反馈摘要

- **核心痛点**：UI 不稳定（尤其是 WebChat），消息状态不一致（消失、重复、被静默丢弃），Agent-to-Agent通信不可靠，以及升级后频繁出现的回归问题。许多用户表示被迫“回滚”到旧版本，这对一个追求前沿体验的项目是强烈的负面信号。
- **故障模式**：“白屏/闪断”、“消息丢失”、“无限循环/重复回复” 和 “Session 卡死” 是出现频率最高的关键词。用户对于“对话内容消失”的反应最为强烈，因为这直接影响到了他们对Agent的信任。
- **正面反馈**：飞书（Feishu）和 Realtime Talk 等功能虽然有其问题，但用户整体反馈是积极和喜爱的，表明这些特性是用户真正的兴奋点。特别是 Realtime Talk 被称赞为“感觉真正有用且低延迟”。
- **开发体验**：社区开发者正在积极参与讨论大型重构（如SQLite迁移），并主动提供大量修复PR，显示出极高的参与度。但对维护者响应速度（尤其在PR合并决策上）有一定期待。

## 待处理积压

以下为长期未得到有效修复或充分讨论的重要 Issue，提醒维护者关注：

1.  **`#39604`**: `web_fetch.allowPrivateNetwork` 功能请求，13条评论，9个 👍，已打开3个月，等待安全策略方面的最终决策。
2.  **`#55334`**: `sessions.json` 无限增长导致 OOM 的 P1 性能问题，已持续2个多月，虽已定位根因但尚无明确的修复方案。
3.  **`#41199`**: Agent-to-Agent 通信工具参数冲突，该 Issue 存在超过3个月，至今有 PR 但仍未关闭，表明解决复杂，可能需要架构层面的调整。

---

## 横向生态对比

好的，作为AI智能体与个人AI助手领域的资深技术分析师，现基于您提供的2026年6月3日各项目动态数据，为您呈上横向对比分析报告。

---

# 个人AI助手/自主智能体开源生态横向对比报告 (2026-06-03)

## 1. 生态全景

当前，个人AI助手与自主智能体开源生态正经历一场**高强度、大规模的“维护与修复”攻坚期**。多个头部项目的社区活跃度达到顶峰，但焦点已从新功能堆叠转向**系统稳定性、核心状态管理及安全性强化**。项目普遍面临因快速迭代导致的回归问题激增，尤其是会话（Session）状态一致性、消息投递可靠性及跨平台兼容性成为共同挑战。与此同时，MCP（Model Context Protocol）、高级子代理协作及TUI（终端用户界面）成为下半年的关键发展方向，标志着生态正从“能跑起来”向“跑得稳、用得爽、扩得开”迈进。

## 2. 各项目活跃度对比

| 项目名称 | Issues (更新/新开) | PRs (更新/合并关闭) | Release | 健康度评估 | 关键动态 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 429 | 500 | 无 | **高强度维护期** | Session状态、消息丢失、回归问题为绝对焦点；社区贡献极速。 |
| **NanoBot** | 9 (新) | 25 (新), 17 (合/关) | 无 | **快速迭代期** | 聚焦MCP稳定、子智能体权限、WebUI优化；QQ渠道、记忆RAG已合并。 |
| **Hermes Agent** | 50 (42新, 8关) | 50 (6合/关, 44待合) | 无 | **高活跃但积压严重** | Docker镜像、Discord网关P1级Bug未修复；44个PR待合并。 |
| **PicoClaw** | 3 (1关) | 14 (6合/关) | **1个** | **稳定推进期** | 修复智谱API、goroutine泄漏；流式请求和WebSocket协议需求浮现。 |
| **NanoClaw** | 1 (新) | 4 (合/关) | 无 | **中等活跃** | 合并插件钩子系统、安全修复；关键PR #2187积压超1个月。 |
| **NullClaw** | 1 (新) | 1 (新) | 无 | **低活跃，快速响应** | 仅一个PII误报问题，贡献者已提修复PR。 |
| **IronClaw** | 多个新开 | 30+ (合/关)，20待合 | 无 | **高强度重构期** | Reborn框架审计为主；修复OAuth、MCP及多项模型兼容性Bug。 |
| **LobsterAI** | 0 | 9 (6合/关) | 无 | **稳态优化期** | 聚焦MCP启动优化、MiniMax-M3模型支持、子代理批量删除。 |
| **Moltis** | 1 (新) | 1 (待合) | 无 | **温和演进期** | 核心PR#1089待合并，优化工具结果持久化；社区反馈平静。 |
| **CoPaw** | 36 | 29 | 无 | **爆发式修复期** | 安全漏洞、定时任务Bug、浏览器崩溃问题集中报告与修复。 |
| **ZeroClaw** | 33 (关) | 47 (关) | **1个 (v0.8.0-beta-2)** | **发布后密集修复期** | 发布TUI，快速修复安全、安装崩溃等S1级Bug。 |
| **TinyClaw, ZeptoClaw** | 0 | 0 | 无 | **静默** | 无任何活动。 |

## 3. OpenClaw 在生态中的定位

OpenClaw 作为生态的核心参照项目，今日的活跃度（429 Issues, 500 PRs）远超其他项目，其地位类似于一个 **“压力测试平台”**或 **“问题集散中心”**。

- **优势**：极高的人气意味着强大的社区修复能力和问题曝光度。大量的回归问题能得到快速识别和修复（如WebChat消息丢失的修复PR），体现了极高的社区自驱力。
- **技术路线差异**：相比NanoBot的RAG记忆与MCP集成、ZeroClaw的TUI创新，OpenClaw目前更聚焦于解决**Session/Transcript状态管理的根本性架构问题**（如SQLite迁移），这是所有项目的共性痛点，体现了其作为基础设施级项目的定位。
- **社区规模对比**：OpenClaw的社区规模（以日更Issues/PRs计）约是NanoBot和Hermes Agent的**5-10倍**，是PicoClaw、CoPaw等项目的**数十倍**。它汇聚了最多样化的用户场景和痛点，对其他项目有强烈的风向标作用。

## 4. 共同关注的技术方向

多项目在以下领域涌现出高度一致的诉求，标志着行业的共性挑战和下一阶段的攻坚方向：

1.  **Session/Transcript 状态管理与持久化**：
    - **项目**：OpenClaw (#88838), PicoClaw (#2404), Moltis (#1089), CoPaw (#4551), ZeroClaw。
    - **诉求**: 解决`sessions.json`无限增长、OOM、消息丢失。普遍期望采用SQLite进行结构化存储，并引入轻量级RAG或DAG压缩来管理长上下文，提升性能并避免信息丢失。

2.  **消息投递可靠性与渠道兼容性**：
    - **项目**：OpenClaw (#52875, #87646, #86519), Hermes Agent (#25495), CoPaw (#4878), ZeroClaw (#6246)，NullClaw (#944)。
    - **诉求**: 解决Agent间通信无响应、特定平台（Discord/Telegram/微信/WhatsApp）消息被丢弃、重复发送或无故失败。这暴露了网关层对第三方平台协议变更的脆弱性和自身路由逻辑的不健壮。

3.  **插件/钩子系统与MCP扩展**：
    - **项目**：NanoBot (#4168), NanoClaw (#1193), IronClaw (#4354), LobsterAI (#2091), CoPaw (#4804)。
    - **诉求**: 不仅要求MCP服务器稳定，更要求子Agent能访问MCP工具（NanoBot #4166）、插件能向系统Prompt注入内容（CoPaw #4804）、主机端提供完整的生命周期钩子（NanoClaw #1193）。这表明自动化工作流正变复杂，需要更强的可扩展性。

4.  **多模型兼容性与认证统一**：
    - **项目**：OpenClaw (#72031), NanoBot (#4167), PicoClaw (#2989), Hermes Agent (#14065), IronClaw (#4334)。
    - **诉求**: 解决特定模型（如Bedrock、小米MiMo、智谱）的认证、参数不兼容问题。用户期望模型切换与身份认证更加统一，减少因API差异带来的故障。

5.  **TUI/CLI与交互体验增强**：
    - **项目**：OpenClaw (#84216), ZeroClaw (v0.8.0-beta-2), NanoBot (#4163), CoPaw (#4904), PicoClaw (#2984)。
    - **诉求**: 用户不仅需要高级的WebUI，还要求高效的TUI、清晰的消息分支、可配置的侧边栏、以及更明确的WebSocket完成信号。这反映了专业用户对“界面可控性”和“操作效率”的更高追求。

## 5. 差异化定位分析

| 项目 | 功能侧重 | 典型目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全能型/基础设施 | 追求前沿、高度定制化的开发者 | 高复杂度主架构，社区驱动，问题集散地 |
| **NanoBot** | **易用性/开箱即用** | 想快速搭建个人助手的用户/开发者 | 轻量级RAG记忆，MCP生态桥接，快速合并社区功能 |
| **Hermes Agent** | 研究/前沿探索 | 学术研究、多代理协作的极客 | 聚焦自主子任务派发，部署稳定性问题较大 |
| **PicoClaw** | **Go语言&轻量级** | 偏好Go语言，追求性能和低资源消耗的开发者 | 采用Go构建，AI功能紧凑，社区规模较小但健康 |
| **IronClaw** | **企业级/平台化** | 关注SaaS集成、安全合规的团队 | 强OAuth/MCP/Slack集成，Reborn运行时为下一代平台 |
| **ZeroClaw** | **极致体验/创新** | 追求终端效率、喜欢尝鲜的专业开发者 | **TUI核心创新**，多智能体运行时，发布后快速迭代 |
| **CoPaw** | 生态集成/安全 | 注重安全、使用多平台IM（企微）的用户 | **安全漏洞发现与修复迅速**，插件生态活跃，中文社区友好 |
| **LobsterAI** | 稳健迭代/协作 | 需要稳定协作和分享功能的团队 | 侧重子Agent批量删除、分享弹窗等协作体验优化 |

## 6. 社区热度与成熟度分层

- **第一梯队（高强度迭代/维护）**：**OpenClaw**, **NanoBot**, **Hermes Agent**, **CoPaw**, **ZeroClaw**
    - **特征**：社区活跃度极高（日更Issues/PRs 30+），处于问题爆发和能力快速演进期，但伴随大量Bug和回归问题。这既是快速成长的标志，也是系统成熟度不足的体现。

- **第二梯队（快速迭代/发布）**：**PicoClaw**, **IronClaw**, **LobsterAI**
    - **特征**：活跃度中等偏高，修复和功能开发节奏清晰，有明确的发布/攻坚计划。Bug存在但不致命，项目健康度良好。

- **第三梯队（稳定/温和演进）**：**NanoClaw**, **Moltis**, **NullClaw**
    - **特征**：社区体量较小或处于稳态，新功能少，主要精力在解决特定痛点或积累待处理项，活跃度较低。

## 7. 值得关注的趋势信号

1.  **从“能跑”到“跑得稳”的范式转移**：当几乎所有项目的核心Bug都指向“消息丢失”、“Session卡死”时，说明开发者已不再满足于Agent能回答问题，而是要求其作为一项“通讯基础设施”拥有电信级可靠性。**可靠性将成为下一代AI助手的核心竞争壁垒**。

2.  **Session/Prompt 压缩技术将成为新“黑科技”**：OpenClaw的SQLite迁移、CoPaw的DAG无损压缩、NanoBot的轻量级RAG记忆，都指向一个核心问题：**如何在不丢失关键信息的前提下，将无限对话塞进有限的上下文窗口**。掌握高效、无损的上下文压缩技术，将是解决长链Agent和复杂自动化任务的关键。

3.  **“用户体验”回归，TUI/CLI成新增长点**：ZeroClaw的TUI发布和多个项目对CLI/WebUI的优化，表明社区开始认真对待开发者体验。专业的开发者和高级用户不再满足于简单的聊天框，他们需要**高效、可控、可脚本化的交互界面**。这预示着一波新的“Infrastructure for AI”工具浪潮。

4.  **渠道互联成为“阿喀琉斯之踵”**：微信、Discord、WhatsApp等第三方平台的协议变更是多项目稳定性问题的共同源头。生态的下一步发展必须解决如何建立稳健、透明的中间协议层，以解耦AI Agent与第三方平台的脆弱依赖关系。

5.  **安全不再是事后补救，而是基础架构**：CoPaw集中披露的API安全漏洞和IronClaw的零化凭证处理，标志着安全已从功能请求变为核心设计要求。**API密钥泄露、Session会话劫持、Prompt注入**等问题被系统性提出，将对Agent平台的架构设计产生深远影响。

*报告完毕。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 NanoBot (github.com/HKUDS/nanobot) GitHub 数据，我为您生成了 2026-06-03 的项目动态日报。

---

### NanoBot 项目动态日报 | 2026-06-03

---

#### 1. 今日速览

- **项目活跃度评估：极高**。过去24小时内，项目收到了9个新Issues和25个新PR，显示了非常强劲的社区参与度和开发节奏。虽然无版本发布，但PR的合并/关闭数量（17个）表明团队正在高效处理社区贡献，项目处于快速迭代期。从Issue内容看，社区关注的焦点已从基础功能搭建，转向了高度具体的稳定性、兼容性和功能增强（如MCP服务、Email通道、子智能体等）问题。

#### 2. 版本发布

- **无**。过去24小时无新版本发布。

#### 3. 项目进展

今日有 **17 个 PR 被合并或关闭**，项目在多个关键领域取得了显著进展：

- **新功能：QQ频道与邮件附件**：
    - **Q #4146** 合并了Napcat (QQ) 频道，为项目增加了对国内主流IM平台的支持，扩展了应用场景。
    - **Q #4162, #4160** 为Email通道添加了文件附件发送功能，提升了沟通的实用性。

- **核心架构优化：记忆检索与智能体流程**：
    - **Q #4109** 合并了轻量级RAG用于记忆检索，这可能显著提升智能体在长对话中的上下文理解能力和回答质量。
    - **Q #3990** 对“Dream”功能进行了重构，用更简单的 `cron + process_direct` 流程替代了旧的两阶段类，降低了复杂度和维护成本。

- **WebUI 与稳定性修复**：
    - 修复了多个关键WebUI问题，包括：**页面刷新后无法保持路由位置**（#4150）、**控制台回复复制功能在非安全环境下的降级处理**（#4149）、**侧边栏聊天分组排序混乱**（#4151）以及 **WebUI启动时的无限等待问题**（#4157）。

- **Bug 修复**：
    - **Q #4155** 修复了 `read_file` 工具在结果过大时陷入无限卸载循环的严重Bug。
    - **Q #4159** 通过自动修复脚本，初步解决了在 `uv tool` 环境下安装pip应用失败的问题。

#### 4. 社区热点

今日社区讨论热度集中在以下几个议题：

1.  **图像生成 API 兼容性问题** **(#4167)**
    - **链接**: HKUDS/nanobot Issue #4167
    - **诉求**: 用户 (gkd2323c) 在使用不兼容 `response_format` 参数的OpenAI兼容API（如Agnes AI）时，`generate_image` 工具直接失败。
    - **分析**: 这表明用户正在尝试将NanoBot接入多样化的第三方API生态，项目的通用性和兼容性成为关键痛点。用户对“开箱即用”的期望很高。

2.  **MCP 服务的稳定性与子智能体访问权限** **(#4168, #4166)**
    - **链接**: HKUDS/nanobot Issue #4168, #4166
    - **诉求**: 同一用户 (tjc0726) 连续提出了两个MCP相关问题：**稳定性问题**：MCP服务器在随机时间后无法连接。**功能缺失**：通过 `spawn()` 创建的子智能体无法访问MCP服务器提供的工具。
    - **分析**: MCP是NanoBot生态扩展的核心。这两个问题分别指向了MCP连接的健壮性和其与智能体模型的集成深度。特别是子智能体无法访问MCP工具，会严重限制复杂任务的自动化流程，是社区急需解决的重大痛点。

#### 5. Bug 与稳定性

| 严重程度 | Issue / PR 链接 | 描述 | 状态 | 对应修复 |
| :--- | :--- | :--- | :--- | :--- |
| **高** | Q #4168 | MCP服务器随机无响应，日志显示 `McpError: Session terminated`，重启可暂时修复。 | **Open** | 暂无 |
| **高** | Q #4167 | 与不支持 `response_format` 参数的OpenAI兼容图像API（如Agnes AI）不兼容。 | **Open** | 暂无 |
| **中** | Q #4153 (已关闭) | `read_file` 工具在恢复磁盘上持久化的超大工具结果时失败。 | **已修复** | Q #4155 已关闭 |
| **中** | Q #4158 | 在 `uv tool` 环境下安装WebUI CLI应用失败，因找不到 `pip` 模块。 | **已修复** | Q #4159, #4164 (待合并) |
| **中** | Q #4081 (已关闭) | `MemoryStore.append_history` 在高并发写入时可能分配重复游标。 | **已修复** | (通过 #4081 关闭) |
| **低** | Q #4066 (已关闭) | Session的 `last_consolidated` 偏移量超出范围导致历史消息被隐藏。 | **已修复** | Q #4169 (待合并) |

#### 6. 功能请求与路线图信号

今日提出的功能请求指向了项目下一阶段的几个重要方向：

- **子智能体（Subagent）能力增强** **(`#4166`)**: 允许子智能体访问MCP服务。这是实现复杂、可组合的自动化工作流的关键一步，很可能被纳入近期路线图。
- **自定义图像生成供应商支持** **(`#4132`)**: 允许用户在配置文件中自定义（如Agnes AI）生成图片的API。这与 `#4167` 的Bug报告相辅相成，说明用户有强烈的自定义第三方服务需求。
- **云平台一键部署** **(`#4139`)**: 一个大型PR，旨在为NanoBot提供在HuggingFace Spaces和ModelScope Studio等云平台上的第一方部署支持。这标志着项目开始关注降低用户的生产环境部署门槛，是走向成熟的重要信号。
- **WebUI 消息分支功能** **(`#4163`)**: 新增“从此处分支”（Fork from here）功能，允许用户在WebUI中对历史消息进行修改后发送。这增强了对话的灵活性和可控性。

#### 7. 用户反馈摘要

- **痛点与不满**:
    - **复杂API兼容性**: 用户 (gkd2323c) 在尝试使用非标准API时遇到直接失败，期望更好的兼容性或更清晰的错误提示。 ( #4167 )
    - **核心组件不稳定**: 用户 (tjc0726) 报告MCP服务会随机断开，且子智能体无法使用MCP工具，对工作流程影响极大。 ( #4168, #4166 )
- **使用场景与诉求**:
    - **跨国界MCP集成**: 用户 (silence-breaker) 尝试连接Notion的MCP但失败，虽然问题持续数月，但“Claude那边可以正常登录”的评论表明，用户期望NanoBot能像商业产品一样拥有广泛的MCP兼容性和清晰的配置文档。 ( #1168 )
    - **成本优化驱动**: 用户 (hamb1y) 在 #4142 中发起讨论，针对缓存未命中的输入Token优化API调用成本。这表明用户已进入深度使用阶段，开始关注大规模部署时的经济性。

#### 8. 待处理积压

- **长期未解决的基础设施问题**:
    - **Issues #1168**: “Nanobot 连接 Notion MCP失败！”，自2026-02-25起已持续三个多月，至今未有官方回复或解决方案。这可能是由于MCP协议早期的实现不完善或Notion MCP的特定兼容性问题，强烈建议项目维护者关注。

- **待审查的重要功能PR**:
    - **PR #4164**: `fix(cli): fall back to uv pip when pip is unavailable`，针对 #4158 的另一种更优雅的修复方案，已获得社区贡献，等待审核合并。
    - **PR #4165**: `fix(email): skip progress messages to prevent empty emails after tool calls`，一个明确的邮件通道Bug修复，逻辑清晰，建议尽快合并。
    - **PR #4169**: `fix(session): reset out-of-range last_consolidated to recover hidden history`，修复了一个可能导致历史消息丢失的严重问题，应优先合并。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

## Hermes Agent 项目日报 — 2026-06-03

---

### 1. 今日速览

昨日项目活跃度极高：共处理 50 条 Issue（新开/活跃 42 条，关闭 8 条）及 50 条 PR（待合并 44 条，合并/关闭 6 条），无新版本发布。社区讨论集中在 Docker 镜像中 Matrix/Synapse 网关损坏、Discord 网关对话过早终止等 P1 级 Bug，以及多项关于自主任务中继、多配置内存存储等 RFC 功能提议。修复 PR 覆盖了 Feishu 授权、浏览器凭据泄漏、Desktop 滚动回弹等多个领域，但仍有 44 条 PR 待合并，积压压力较大。

---

### 2. 版本发布

昨日无新版本发布。

---

### 3. 项目进展

昨日合并/关闭的 6 条 PR 中，两项关键修复已合入主分支：

- **`fix: pad empty content on tool-call-only assistant messages for MiMo compatibility`**（#37841）  
  修复小米 MiMo API 要求每条 assistant 消息必须有非空 `content` 而导致 HTTP 400 的问题。对使用小米私有模型的用户影响较大。

- **`fix(browser): scrub credentials from browser subprocess env`**（#37259）  
  阻止 agent-browser 子进程继承 Hermes 进程中的凭据（provider token、GitHub token 等），降低浏览器控制路径被攻击时的凭据泄露风险。

此外，另有一批修复 PR 处于 **待合并** 状态，详见下文 Bug 部分。

---

### 4. 社区热点

昨日讨论最活跃的 Issue 和 PR（按评论数排序）：

| 标题 | 类型 | 评论 | 链接 |
|------|------|------|------|
| [Bug]: Matrix / synapse broken in the official docker image | Issue | 10 | [#25495](https://github.com/NousResearch/hermes-agent/issues/25495) |
| RFC: Agent-native task relay with auto-forking subagents + async human approval gates | Issue | 8 | [#31392](https://github.com/NousResearch/hermes-agent/issues/31392) |
| entrypoint.sh misses chown for ui-tui/ and gateway/ when HERMES_UID is remapped | Issue | 6 | [#27221](https://github.com/NousResearch/hermes-agent/issues/27221) |
| Multi-profile shared memory store with on-demand capsule recall | Issue | 4 | [#31388](https://github.com/NousResearch/hermes-agent/issues/31388) |
| Expose model_switch as an agent-callable tool | Issue | 4 | [#16525](https://github.com/NousResearch/hermes-agent/issues/16525) |
| Discord Gateway: Premature conversation turn termination | Issue | 4 | [#27881](https://github.com/NousResearch/hermes-agent/issues/27881) |
| Named custom providers lose inline api_key | Issue | 4 | [#14065](https://github.com/NousResearch/hermes-agent/issues/14065) |

**分析**：  
- 社区注意力高度集中在 **Docker 部署稳定性**（#25495）和 **网关（Gateway）体验**（#27881 等）。  
- 两个 RFC（#31392、#31388）获得较多讨论，表明用户对 **自主子任务派发** 和 **多配置共享记忆** 有强烈需求。  
- `model_switch` 作为工具暴露（#16525）的呼声持续，用户希望 Agent 能根据任务复杂度自动切换模型。

---

### 5. Bug 与稳定性

昨日报告的 Bug 按严重程度排列（P1 最高）：

| 严重性 | 标题 | 状态 | 备注 |
|--------|------|------|------|
| P1 | Matrix / synapse broken in official docker image | OPEN | 最后正常版本 sha-1e01b25e76a9，之后日志卡在 "fixing ownership :1000"；无关联修复 PR |
| P1 | Discord Gateway: 对话过早终止 | OPEN | 自主工作流中频繁中断，反馈多 |
| P1 | Named custom providers 运行时丢失 api_key | OPEN | 影响 v12+ 配置，涉及 `runtime_provider.py` |
| P2 | entrypoint.sh 未 chown ui-tui/ 和 gateway/ | OPEN | 影响 Unraid/Synology 等 UID 重映射场景 |
| P3 | Hermes Desktop macOS DMG 仅 arm64，Intel Mac 无法运行 | OPEN | 新报告 |
| P3 | ACP 模式忽略 platform_toolsets，导致记忆工具被屏蔽 | OPEN | 已有 fix PR #37842 待合并 |
| P3 | Desktop 长线程鼠标滚轮向上滚动时回弹 | OPEN | 已有 fix PR #37831 待合并 |

**已有 fix PR 的 Bug**：
- ACP 模式工具集忽略 → PR #37842（OPEN）
- Desktop 滚动回弹 → PR #37831（OPEN）
- Feishu 授权回归 → PR #37849、#37847（OPEN）
- 浏览器子进程凭据泄露 → 已合并 #37259
- 小米 MiMo 空 content → 已合并 #37841

**注意**：仍有数个 P1 级 Bug 无修复 PR 关联，尤其是 Docker 和 Discord 网关问题亟需关注。

---

### 6. 功能请求与路线图信号

昨日新增多个功能请求，部分已有对应 PR 处于开发中：

- **Agent-native task relay**（#31392）：自动分叉子 Agent + 异步人工审批，是现有 Delegate 系统的补充。暂无关联 PR。
- **多配置共享记忆存储**（#31388）：类似 `capsule recall`，与现有 Honcho 集成并存。暂无 PR。
- **`compress_context` 作为原生 Tool**（#12213）：目前仅支持 `/compress` 命令，无法在 Skill 中调用。暂无 PR。
- **内部时钟感知**（#27742）：Agent 无自主时间感知，无法监控截止时间。暂无 PR。
- **谷歌工作区 Skill 服务账户认证**（#17272）：支持自主部署场景。暂无 PR。
- **Windows 中国用户一键安装脚本**（#37491）：考虑网络障碍。暂无 PR。
- **Mobile-first Mac chat hub**（#37835）：提出 PRD 文档。暂无 PR。

**已有对应 PR 的功能**：
- **Feishu 多应用支持** → PR #35911（OPEN）
- **Desktop i18n (zh-CN)** → PR #37276（OPEN）
- **Feishu 交互卡片 send_message** → PR #37830（OPEN）
- **Feishu 会议邀请处理** → PR #37826（OPEN）
- **自主编码技能消费中心 providers 配置** → #32537（需求，无 PR）

上述功能需求中，Feishu 增强和 i18n 最可能纳入近期版本。

---

### 7. 用户反馈摘要

从昨日 Issue 评论中提炼的用户痛点与使用场景：

1. **Docker 镜像 Matrix/Synapse 网关完全不可用**（#25495）：用户从某 commit 开始该功能中断，日志停滞，社区等待近三周无修复，挫败感强。
2. **Discord 网关频繁中断对话**（#27881）：即使用户执行简单同步工具调用，Agent 也会提前终止回复，严重影响交互体验。
3. **UID 重映射后 GUI/TUI 目录权限未修正**（#27221）：用户自行手动 `chown` 可绕过，但期望 entrypoint 自动处理。
4. **Intel Mac 用户无法启动 Hermes Desktop**（#37505）：新版 DMG 仅包含 ARM 切片，用户无法使用。
5. **ACP 模式无法使用记忆工具**（#37813）：用户需手动配置，与 `platform_toolsets` 设定冲突。
6. **Agent 在工具失败后盲目尝试未经验证的替代方案**（#24012）：导致大量 token 浪费，用户期望 Agent 先查历史记录。
7. **Windows 安装失败**（#37827）：`git checkout main` 报错，用户完全无法搭建环境。

总体来看，用户对 **网关稳定性** 和 **Docker/桌面部署兼容性** 的满意度较低，对 **自主 agent 路由与记忆** 的改进期待较高。

---

### 8. 待处理积压

以下为长期未响应或亟需维护者关注的重要 Issue/PR：

| 类型 | 标题 | 创建时间 | 最后更新 | 备注 |
|------|------|----------|----------|------|
| Issue | Matrix / synapse broken in official docker image (#25495) | 2026-05-14 | 2026-06-03 | P1，无响应 |
| Issue | entrypoint.sh misses chown for ui-tui/ and gateway/ (#27221) | 2026-05-17 | 2026-06-03 | P2，无修复 PR |
| Issue | Named custom providers lose inline api_key (#14065) | 2026-04-22 | 2026-06-03 | P1，影响范围大 |
| Issue | Discord Gateway premature termination (#27881) | 2026-05-18 | 2026-06-03 | P1，仅有一项用户评论转发 |
| PR | fix(tools): invalidate tool caches on dotenv reload (#33423) | 2026-05-27 | 2026-06-03 | 待合并近一周，修复工具热加载 |
| PR | feat(feishu): allow multiple Feishu/Lark apps (#35911) | 2026-05-31 | 2026-06-03 | 功能增强，待合并 |
| Issue | Hermes Desktop macOS DMG is arm64-only (#37505) | 2026-06-02 | 2026-06-03 | 新报告，需快速回应 |
| Issue | Agent autonomously tries unverified alternatives after tool failures (#24012) | 2026-05-11 | 2026-06-03 | 用户痛点明确，无 PR |

建议维护团队优先关注 P1 级 Docker 和 Discord 网关问题，并推进积压 PR 的 review 与合并。

---

*数据来源：Hermes Agent 官方 GitHub 仓库，统计时间窗口为 2026-06-02 至 2026-06-03 UTC。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-06-03

## 📊 今日速览
昨日项目活跃度较高：共处理 **3 条 Issues**（1 条关闭）、**14 条 PR**（6 条合并/关闭），并发布了一个 **nightly 版本**。合并的 PR 主要聚焦于稳定性修复（LLM 重试、goroutine 泄漏、智谱 API 错误处理），同时也有大量待合并的功能和修复 PR 积压。项目整体处于**稳定推进**状态，社区对流式请求和 WebSocket 协议完善的需求逐渐升温。

---

## 🚀 版本发布

### nightly: v0.2.9-nightly.20260603.a502aa7f
- 类型：自动构建（可能不稳定）
- 变更对比：[v0.2.9…main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- ⚠️ 无破坏性变更说明，但建议生产环境谨慎使用。该版本应包含近期合并的多个修复（如智谱 API 错误码、goroutine 泄漏等）。

---

## 📌 项目进展（今日合并/关闭的 PR）

| PR | 说明 | 状态 |
|---|---|---|
| [#2991](https://github.com/sipeed/picoclaw/pull/2991) | fix(agent): 使用 provider 错误分类器重试瞬时 LLM HTTP 错误，避免无后备模型时直接失败 | 已合并 |
| [#2986](https://github.com/sipeed/picoclaw/pull/2986) | fix(tools): 为 SessionManager 添加 `Stop()` 方法，防止 goroutine 泄漏 | 已合并 |
| [#2989](https://github.com/sipeed/picoclaw/pull/2989) | fix(providers): 将智谱 API 错误码 1210 加入格式错误分类，使微信图片请求触发 fallback | 已合并 |
| [#2994](https://github.com/sipeed/picoclaw/pull/2994) & [#2993](https://github.com/sipeed/picoclaw/pull/2993) | docs(skill): 添加 `picoclaw-agent` 技能说明文档，指导代理行为 | 已关闭（合并） |
| [#2239](https://github.com/sipeed/picoclaw/pull/2239) | modify docker compose with privileged（历史 PR 最终关闭） | 已关闭 |

**项目向前迈进**：修复了 3 个稳定性问题、完善了技能文档，进一步降低了运行时的资源泄漏风险，并增强了对智谱模型的兼容性。

---

## 🔥 社区热点

### 1. [#2404](https://github.com/sipeed/picoclaw/issues/2404) — 请求在配置中添加流式 HTTP 请求支持
- 评论数：10 | 👍 1 | 状态：OPEN（标记 stale）
- **诉求**：用户希望像 OpenAI Python 客户端那样通过配置文件 `"streaming": true` 启用流式请求，以降低等待时间、提升实时性。尽管已标记 stale，但讨论热度维持，表明这是广泛期待的功能。

### 2. [#2984](https://github.com/sipeed/picoclaw/issues/2984) — 为 WebSocket 客户端添加显式对话结束信号
- 评论数：0 | 👍 1 | 状态：OPEN（新开）
- **诉求**：外部 WebSocket 客户端目前只能通过 `message.create`、`typing.stop` 等事件推断代理是否完成，缺乏确定性信号。用户希望增加一个明确的 `turn.complete` 事件，提升协议可用性。

---

## 🐛 Bug 与稳定性

| 严重程度 | 问题描述 | 对应 PR 状态 |
|---|---|---|
| **高** | 微信发送图片触发智谱 GLM-5 API error 1210（参数错误），无法触发 fallback | [#2989](https://github.com/sipeed/picoclaw/pull/2989) **已合并** |
| **中** | Web UI 会话历史只显示最后一条用户消息（[#2796](https://github.com/sipeed/picoclaw/issues/2796)） | [#2990](https://github.com/sipeed/picoclaw/pull/2990) **待合并** |
| **中** | `/context` 命令始终显示固定压缩阈值，忽略 `summarize_token_percent` 配置（[#2968](https://github.com/sipeed/picoclaw/issues/2968)） | [#2988](https://github.com/sipeed/picoclaw/pull/2988) & [#2985](https://github.com/sipeed/picoclaw/pull/2985) **待合并** |
| **中** | 活跃流式会话中 tool_calls 消息被错误丢弃（[#2958](https://github.com/sipeed/picoclaw/issues/2958)） | [#2987](https://github.com/sipeed/picoclaw/pull/2987) **待合并** |
| **低** | 升级后新 Web UI 会话混入旧消息（[#2972](https://github.com/sipeed/picoclaw/issues/2972)） | [#2992](https://github.com/sipeed/picoclaw/pull/2992) **待合并** |
| **低** | `claude-opus-4-7` 模型因 `temperature` 参数被弃用导致 400 错误 | [#2948](https://github.com/sipeed/picoclaw/pull/2948) **待合并** |
| **低** | 原生 web_search 在部分 OpenAI 端点因工具类型不兼容报错 | [#2951](https://github.com/sipeed/picoclaw/pull/2951) **待合并** |

> 注意：上述“待合并” PR 均已创建于 2026-06-02，有望在近期合入。

---

## 💡 功能请求与路线图信号

| 功能 | 来源 | 可能纳入版本 |
|---|---|---|
| 流式 HTTP 请求（`"streaming": true`） | [#2404](https://github.com/sipeed/picoclaw/issues/2404) | 虽标记 stale，但呼声高，预计 v0.3.0 |
| WebSocket 显式完成信号（`turn.complete`） | [#2984](https://github.com/sipeed/picoclaw/issues/2984) | 新开需求，可能进入规划 |
| **picoclaw-tracer**（调试追踪 Web UI） | [#2945](https://github.com/sipeed/picoclaw/pull/2945) | **待合并**，亮点功能，可实时查看每轮 LLM 调用细节 |
| `/context` 显示双阈值（summarize & compress） | [#2985](https://github.com/sipeed/picoclaw/pull/2985) | 待合并，属于用户体验优化 |

---

## 🗣️ 用户反馈摘要

- **流式需求强烈**：[#2404](https://github.com/sipeed/picoclaw/issues/2404) 评论区可见用户希望快速获得实时响应，尤其对接 OpenAI 类 API 时，`stream=True` 是常用模式。
- **智谱兼容性**：用户 `weixshaw` 报告微信渠道调用 GLM-5-Turbo 视觉 API 失败后，开发者迅速定位并合并修复（[#2943](https://github.com/sipeed/picoclaw/issues/2943)），体现了对多模型支持的重视。
- **上下文管理困惑**：多位用户在 `/context` 命令的显示上存在疑惑（[#2968](https://github.com/sipeed/picoclaw/issues/2968)），开发者已提交 PR 添加软/硬双阈值显示，预计将提升透明度和可配置性。

---

## ⏳ 待处理积压（长期未响应的重要 Issue / PR）

| 类型 | 编号 | 创建时间 | 最新更新 | 原因 |
|---|---|---|---|---|
| Issue | [#2404](https://github.com/sipeed/picoclaw/issues/2404) | 2026-04-07 | 2026-06-02 | 已标记 `stale`，但社区讨论仍在持续，需评估优先级 |
| PR | [#2951](https://github.com/sipeed/picoclaw/pull/2951) | 2026-05-26 | 2026-06-02 | 修复 web_search 兼容性，标记 `stale`，需要 review |
| PR | [#2948](https://github.com/sipeed/picoclaw/pull/2948) | 2026-05-26 | 2026-06-02 | 修复 claude-opus-4-7 temperature 参数，标记 `stale` |
| PR | [#2945](https://github.com/sipeed/picoclaw/pull/2945) | 2026-05-26 | 2026-06-02 | 新增 tracer 功能，标记 `stale`，但功能价值高，建议尽快 review |

> **提醒维护者**：以上 3 个 stale PR 已近 8 天无更新，且对应阻塞性问题（模型兼容、调试工具），建议尽快安排 review 或与贡献者沟通。

---

*数据来源：GitHub (sipeed/picoclaw)，统计时段 2026-06-02 至 2026-06-03 UTC。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，根据您提供的NanoClaw项目数据，现为您呈上2026年6月3日的项目动态日报。

---

### **NanoClaw 项目动态日报 | 2026-06-03**

#### **1. 今日速览**

今日NanoClaw项目整体活跃度中等偏稳。核心亮点在于**合并/关闭了4个PR**，其中包含一个重要的安全漏洞修复和一个功能引入，显示出项目在安全加固和功能扩展上持续推进。然而，**一个关于平台ID的修复PR (#2187)已悬而未决超过一个月**，可能成为社区关注的焦点。同时，唯一新开的Issue描述较为特殊，可能为无效或测试提交，社区讨论活跃度相对有限。

#### **2. 项目进展**

今日项目核心进展体现在4个已合并/关闭的PR上，涵盖了功能、安全与基础设施标准化。

-   **[#1193] 主机端插件钩子系统 (Feat)**：该项目核心功能PR今日最终关闭，引入了主机端插件的 `onStartup`/`onShutdown` 钩子系统。这标志着NanoClaw的插件生态迈出了从“技能”到“平台级扩展”的关键一步，允许开发者编写在代理生命周期启动和关闭时运行的服务器或后台服务。该功能对构建更复杂的自动化工作流和集成至关重要。
    -   **链接**: [nanocoai/nanoclaw PR #1193](https://github.com/nanocoai/nanoclaw/pull/1193)

-   **[#2538] 容器运行器包名验证 (安全修复)**：该PR修复了`buildAgentGroupImage()` 函数中的一个命令注入漏洞 (CWE-78)。通过增加输入验证，有效阻止了攻击者通过恶意构造的包名执行系统命令。此安全更新对运行多租户或需要处理外部输入场景的用户至关重要。
    -   **链接**: [nanocoai/nanoclaw PR #2538](https://github.com/nanocoai/nanoclaw/pull/2538)

-   **[#2674] 标准化运行时状态消息 (Codex)**：此PR为Codex运行时消息提供了标准化格式，添加了元数据和内部通道防护，并整合了本地运行时的更新请求。这有助于提升系统的稳定性和可观测性，使运行时状态更易于理解和调试。
    -   **链接**: [nanocoai/nanoclaw PR #2674](https://github.com/nanocoai/nanoclaw/pull/2674)

-   **[#2069] Webchat 技能 (Feature Skill)**：该PR合并了一个新的Webchat技能，扩展了项目的通信渠道集成能力。这意味着用户现在可以通过web界面与代理进行交互，丰富了NanoClaw的部署和使用场景。
    -   **链接**: [nanocoai/nanoclaw PR #2069](https://github.com/nanocoai/nanoclaw/pull/2069)

#### **3. 社区热点**

今日社区讨论活跃度一般，但存在一个值得关注的长期悬而未决的PR。

-   **热点话题：平台ID命名空间修复 [#2187]**
    -   该PR致力于修复一个影响CLI渠道的bug，主要内容是防止对CLI平台的ID进行命名空间化。该PR于5月2日创建，**至今已过去一个月仍未合并**。这可能是社区关注的焦点，它直接关系到CLI用户在使用时的表现一致性问题。虽然今日有更新，但其长期未决的状态可能暗示了维护者与贡献者在解决方案上存在分歧，或维护者资源紧张。
    -   **链接**: [nanocoai/nanoclaw PR #2187](https://github.com/nanocoai/nanoclaw/pull/2187)

#### **4. Bug 与稳定性**

今日报告的Bug主要围绕平台兼容性和协议适配，严重程度均为中低级别。

-   **中等：CLI 平台 ID 命名规则不当 [#2187] (待合并)**：这是一个影响CLI用户的bug，可能导致平台ID在使用过程中出现不一致问题。虽不具灾难性，但会影响命令行工具的用户体验。目前已有对应的修复PR，但等待合并。
    -   **PR链接**: [nanocoai/nanoclaw PR #2187](https://github.com/nanocoai/nanoclaw/pull/2187)

-   **低等：容器运行器安全漏洞 [#2538] (已关闭)**：该命令注入漏洞在今天被成功修复。得益于贡献者的及时提交，该项目已消除了一个潜在的安全风险。
    -   **PR链接**: [nanocoai/nanoclaw PR #2538](https://github.com/nanocoai/nanoclaw/pull/2538)

-   **低等：Codex MCP 协议兼容性与 HTTP 代理问题 [#2672] (待合并)**：该PR报告了Codex提供者在与新的MCP（Model Context Protocol）配置格式（`stdio | http | sse`）缺乏兼容性，同时HTTP-only传输在代理后工作不正常。这些问题限制了Codex在某些特定网络环境下的使用。
    -   **PR链接**: [nanocoai/nanoclaw PR #2672](https://github.com/nanocoai/nanoclaw/pull/2672)

#### **5. 功能请求与路线图信号**

今日未从Issue中识别出明确的新功能请求。但通过合并的PR，可以判断项目的路线图方向：

-   **插件生态扩展**：**PR #1193** 的合并是一个强烈信号，表明项目正在积极构建更强大的生命周期钩子机制，为未来更复杂的集成场景（如与外部监控、数据库、API网关联动）铺平道路。
-   **交互渠道多元化**：**PR #2069** 的合并确认了团队在推进Web渠道集成，符合打造“全渠道”AI助手平台的趋势。
-   **协议标准化与兼容性**：**PR #2672** 专注于修复对MCP新版本协议的兼容性，表明项目正紧跟行业标准（如MCP协议）的演进，确保其核心组件不会落后。

#### **6. 用户反馈摘要**

今日来自Issue的评论极少，用户的直接反馈有限。Issue #2673 “Automated Student Grading System” 的描述中包含一个AI视频生成提示词模板，这更像是一个内容创作的示范或测试提交，而非真正的产品使用反馈。从唯一的PR #2187 “Fix: platform-id” 来看，背后反映了用户或贡献者在使用命令行界面时遇到了平台识别不一致的痛点，这可能影响了脚本自动化或与外部系统集成的可靠性。

#### **7. 待处理积压**

当前最值得关注的积压项是 **PR #2187**。该PR已悬而未决超过30天，且其内容是一次关键的Bug Fix。如果项目维护者有精力，应优先处理此PR，以避免社区贡献者的热情耗散，并尽快修复影响用户体验的bug。

-   **链接**: [nanocoai/nanoclaw PR #2187](https://github.com/nanocoai/nanoclaw/pull/2187)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-06-03

## 1. 今日速览

过去 24 小时项目整体活跃度中等偏低，仅触发了 1 个新 Issue 和 1 个对应的修复 PR。核心关注点是 **PII 脱敏组件（PII redactor）的误报问题**——系统 `date` 命令输出的 ISO 日期时间格式被错误地匹配为电话号码，导致代理无法获取正确时间戳。贡献者 `vernonstinebaker` 已同时提交 Issue 报告和修复 PR，反应迅速，表明社区对基础功能稳定性的敏感度较高。无新版本发布，项目处于快速响应 Bug 的阶段。

## 2. 版本发布

无新版本。上一稳定版本信息缺失，建议维护者近期考虑发布一个修复版本以解决 PII 误报问题。

## 3. 项目进展

- **PR #945 [待合并]** — `fix(redaction): reject ISO date/time patterns as false-positive phone matches`
  - 作者：`vernonstinebaker`
  - 内容：在 `src/redaction.zig` 的 `matchPhone` 函数中新增 `isDateLike()` 守卫，当原始文本匹配 ISO 日期时间模式（如 `YYYY-MM-DD hh` 或 `DD-MM-YYYY hh`）时，拒绝将其判定为电话号码。
  - 进展：该 PR 直接对应 Issue #944 的修复方案，一旦合并将彻底消除 `date` 命令输出被误脱敏的问题。但目前尚未被合并，也无人评论。

## 4. 社区热点

- **Issue #944 [OPEN]** — PII redactor falsely matches date/time output as phone numbers ([PHONE_X])
  - 作者：`vernonstinebaker` | 评论 0，👍 0
  - 链接：https://github.com/nullclaw/nullclaw/issues/944
  - 分析：这是今日唯一的社区讨论焦点。尽管没有评论和情绪标记，但该 Issue 精准指出了自 commit `41cdb493`（2026 年 5 月）起默认开启的 PII 脱敏功能的一个严重误报——使得代理执行 `date` 命令后看到的全是 `[PHONE_X]` 占位符。这直接干扰了代理对系统时间的获取，属于**功能回归**。用户提交 Issue 的同时也提交了修复 PR，说明该用户具备开发能力且希望社区快速修复。背后诉求：**PII 检测不应对标准系统工具的输出产生误判**，需要更精确的上下文模式识别。

## 5. Bug 与稳定性

| 严重程度 | Bug 描述 | Issue / PR | 是否有 fix PR |
|----------|----------|------------|---------------|
| **严重** | PII 脱敏组件将 `date` 命令输出的 ISO 日期时间（如 `2026-06-02 20:17`）误报为电话号码（`[PHONE_X]`），导致代理无法获取正确时间戳，影响依赖时间的智能体行为。 | #944 | 是（PR #945） |
| 低 | 无其他 Bug 报告 | — | — |

**评估**：该 Bug 直接影响核心功能（系统时间获取），但修复方案明确且已被提交，风险可控。建议维护者尽早合并 PR #945 并发布补丁版本。

## 6. 功能请求与路线图信号

当前无新的功能请求。但从 Issue #944 的反馈看，社区期望 PII 脱敏组件能引入**上下文感知的模式匹配**，即对于系统命令输出中常见的固定格式（如 `date`、`uptime` 等）进行白名单或模式豁免。类似思路可能被纳入下一个小版本的改进计划。

## 7. 用户反馈摘要

- **用户痛点**：`enable_pii_redaction` 默认开启后，代理无法显示实际时间戳，用户被迫手动禁用该功能或修改系统提示词（`appendDateTimeSection`）。该问题在 May 2026 commit 后出现，属于回归。
- **使用场景**：典型场景是智能体通过系统命令 `date` 获取当前时间以规划后续操作，脱敏后只能得到占位符，导致时间相关推理错误。
- **满意度**：用户 `vernonstinebaker` 积极提交 Issue 并附上修复方案，显示出对项目的关心，但暂时未获得维护者响应，情绪中性偏正面。

## 8. 待处理积压

- **Issue #944 / PR #945** — 虽然仅创建 1 天，但其修复方案清晰，且是当前唯一活跃的待处理项，可以视为**短期积压**。提醒维护者：该 Bug 影响所有使用默认 PII 脱敏的实例，建议在 24 小时内完成 Code Review 并合并。
- 此外，未发现超过 7 天无响应的其他重要 Issue 或 PR。

---

**项目健康度评估**：活跃度 ⭐⭐⭐（3/5），社区响应速度 ⭐⭐⭐⭐（4/5），代码质量风险 ⭐（1/5，仅单个轻度误报）。整体健康，只需快速合并补丁即可恢复稳定。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 GitHub 数据，为您生成 IronClaw 项目在 2026年6月3日 的动态日报。

---

# IronClaw 项目动态日报 | 2026-06-03

## 1. 今日速览

今日项目活跃度极高，尤其是在代码审查和缺陷修复方面。核心团队正集中精力对 **Reborn** 框架进行一次大规模的、系统性的审计与加固，密集提交了超过15个涉及正确性、安全性和可观测性的 “reborn-loop” 和 “reborn-subagent” 议题。与此同时，社区QA团队报告了多个 P2 级别的 Bug，主要集中在新模型兼容性（Qwen3.6-35B, MiniMax-M2.7）和 UI 交互体验上。PR 处理效率很高，超过 30 个 PR 被合并，但仍有约 20 个待合并，总体来看，项目正处于 “大版本内部重构 + 快速修复社区反馈” 的高强度迭代阶段。

## 2. 版本发布

**无**

昨日无新版本发布。当前版本活跃度主要由合并的 PR 和关闭的 Issue 推动。

## 3. 项目进展

今日项目有重大推进，核心团队在平台集成、安全性和模型兼容性上取得了关键进展。

- **强化平台集成 (OAuth & MCP):**
    - **PR #4354** [[链接]](https://github.com/nearai/ironclaw/pull/4354) 修复了托管 MCP 传输协商问题，并增强了 Notion/GSuite 的 OAuth 凭据复用能力。
    - **PR #4346** [[链接]](https://github.com/nearai/ironclaw/pull/4346) 和 **PR #4347** [[链接]](https://github.com/nearai/ironclaw/pull/4347) 修复了 Gmail OAuth 认证门控和权限范围问题，确保认证流程正确。
    - **PR #4345** [[链接]](https://github.com/nearai/ironclaw/pull/4345) 为 Notion 集成了 DCR OAuth 流程，这对 Reborn WebUI 的用户体验至关重要。

- **模型兼容性与功能修复:**
    - **PR #4315** [[链接]](https://github.com/nearai/ironclaw/pull/4315) 修复了引擎 v2 的视觉附件功能，现在图片内容可以在 LLM 请求中正确传递。
    - **PR #4374** [[链接]](https://github.com/nearai/ironclaw/pull/4374) 提高了 `memory_search` 工具的可用性，现在接受多种查询字段别名。
    - **PR #4371** [[链接]](https://github.com/nearai/ironclaw/pull/4371) 修复了 Codex ChatGPT Reborn 模式下可能返回空响应的问题。

- **安全与稳定性加固:**
    - **PR #4372** [[链接]](https://github.com/nearai/ironclaw/pull/4372) 实施了一项关键的安全改进：在 HTTP 凭据载体析构时进行零化处理，防止敏感信息泄露。
    - **PR #4373** [[链接]](https://github.com/nearai/ironclaw/pull/4373) 修复了子代理的安全和功能门控问题，防止安全提示被绕过。
    - **PR #4370** [[链接]](https://github.com/nearai/ironclaw/pull/4370) 解决了 Reborn 压缩摘要创建的重试幂等性问题，提升了系统稳定性。

## 4. 社区热点

今日社区讨论主要围绕由 `henrypark133` 发起的大规模 “Reborn” 代码审计系列议题。这些议题虽然尚未有大量评论，但它们数量庞大且高度结构化，代表了团队当前最核心的关注点和对社区未来的透明度。

- **热点 Issue 集群：** `#4358` 到 `#4368` [[链接]](https://github.com/nearai/ironclaw/issues?q=is%3Aissue+author%3Ahenrypark133+created%3A2026-06-02) 这一系列共计10个新开 Issue，系统性地审查了 Reborn 框架的各个模块。
- **背后诉求分析：** 这些议题并非来自用户，而是核心开发者在主导一个代号为 “Reborn-Loop” 和 “Reborn-Subagent” 的深度技术债务清理和架构加固行动。这表明社区（特别是核心团队）的诉求已从功能堆叠转向 **可靠性、安全性和架构合规性**。议题涵盖预算准确性 (L7)、取消传播 (L8)、数据持久化 (L5)、子代理安全性 (C4) 等关键领域，预示着一个强健的 v2 引擎即将到来。

## 5. Bug 与稳定性

今日报告了多个 **P2 级别** 的 Bug，主要影响用户体验，部分问题已有修复 PR。

- **严重 (Blocking):**
    - **#4334: Claude Opus 4.7/4.8 不可用** [[链接]](https://github.com/nearai/ironclaw/issues/4334)。因引擎始终发送已废弃的 `temperature` 参数，导致新模型请求被拒绝。这是严重的兼容性问题，**强烈建议 P0 优先级处理**。

- **中高 (P2 - QA Bug Bash):**
    - **#4341: 思维链暴露 & 卡死** [[链接]](https://github.com/nearai/ironclaw/issues/4341) (Qwen3.6)
    - **#4344: 消息回声** [[链接]](https://github.com/nearai/ironclaw/issues/4344) (Qwen3.6) - **已有修复 PR #4336** [[链接]](https://github.com/nearai/ironclaw/pull/4336) 待合并。
    - **#4343: MCP 驱动故障** [[链接]](https://github.com/nearai/ironclaw/issues/4343) (Qwen3.6)
    - **#4342: 认证模态框刷新后阻塞聊天** [[链接]](https://github.com/nearai/ironclaw/issues/4342) (Qwen3.6)
    - **#4340: 空白字段验证错误** [[链接]](https://github.com/nearai/ironclaw/issues/4340) (Qwen3.6)
    - **#4339: 工具调用被错误拒绝** [[链接]](https://github.com/nearai/ironclaw/issues/4339) (MiniMax-M2.7)
    - **#4338: 断开连接时显示误导性错误** [[链接]](https://github.com/nearai/ironclaw/issues/4338) (MiniMax-M2.7)

- **低 (P3):**
    - **#4108: Nightly E2E 测试失败** [[链接]](https://github.com/nearai/ironclaw/issues/4108)。持续多日的自动化测试失败，需排查根因。

## 6. 功能请求与路线图信号

今日无明确的新功能请求 Issue，但大量内部审计 Issue 和已合并的 PR 清晰指明了路线图方向。

- **Reborn 框架成熟度是核心方向：** 系列 `reborn-loop` 和 `reborn-subagent` Issue 表明，当前核心任务是让 Reborn 成为一个生产就绪的、坚固的运行时。这包括更精确的预算控制、可靠的补偿逻辑、安全的沙箱机制等。
- **平台集成进一步深化：** 今日合并的关于 Notion、Gmail、Slack 的 PR 表明，IronClaw 正在加速成为一个能够与外部 SaaS 服务深度协作的 AI 工作流平台。`trigger` 能力（由 `#4375` 引入）暗示了未来的自动化与定时任务功能。这些功能很可能被纳入下一个大版本（v2或Reborn正式版）。

## 7. 用户反馈摘要

由于今日数据主要来源于 QA Bug Bash，用户反馈集中在受控的测试环境中，而非真实用户自发的评论。

- **模型兼容性是最大痛点：** 从 `#4334`（Claude Opus 不可用）和多个针对 Qwen3.6/B 型号的 Bug 来看，用户对于不能在新模型上正常工作感到沮丧，这直接影响新模型的采用和用户体验。
- **交互反馈需改进：** 多个 Bug 涉及用户交互的模糊性，如 `#4344` 消息回声、`#4338` 断开连接时的误导性错误、`#4342` 模态框阻塞。这表明系统在处理异步状态（加载、错误、认证）时，未给用户提供足够清晰和一致的反馈，导致困惑。
- **MCP 集成期望高但门槛也高：** `#4343` 指出 MCP 功能虽被认可（acknowledged）但不稳定（unusable），这表明用户对扩展功能的期望很高，但当前实现的稳定性未能满足其应用需求。

## 8. 待处理积压

以下是一些重要的、长期未响应的 Issue/PR，可能阻碍关键功能或影响系统健康。

- **PR #3548: 添加 DISABLE_TOOLS_LIST 功能** [[链接]](https://github.com/nearai/ironclaw/pull/3548)
    - **状态：** 自5月12日起处于 Open 状态，已有安全和功能测试覆盖。
    - **影响：** 这是一个重要的安全性和可配置性功能，允许管理员禁用特定工具。长期未合并可能阻碍企业级部署。建议维护者评估并尽快决策。

- **PR #3669: engine v2 暴露线程/响应 ID 给工具** [[链接]](https://github.com/nearai/ironclaw/pull/3669)
    - **状态：** 自5月14日起处于 Open 状态，被视为一个 XL 大小的 PR。
    - **影响：** 恢复 engine v1 的核心契约，对工具做相关性回调至关重要。今日 Issue #4355 已为此 PR 进行了后续的类型封装，表明这是一个需要谨慎推进的架构变更。

- **Issue #3806: [Reborn] Lane 6: 实现 GitHub WASM 读写能力路径** [[链接]](https://github.com/nearai/ironclaw/issues/3806)
    - **状态：** 5月19日创建，已标记为 CLOSED，但关闭原因未说明（可能是被更高优先级的任务取代或暂缓）。
    - **影响：** 这是 Reborn WASM 能力目录扩展的关键一步。若其关闭意味着路线图变更，应及时告知社区；若只是暂时搁置，建议更新其状态和标签，避免混淆。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 LobsterAI 项目的 AI 智能体与个人 AI 助手领域开源项目分析师，这是为您生成的 2026 年 6 月 3 日项目动态日报。

---

# LobsterAI 项目日报 | 2026-06-03

## 1. 今日速览

今日项目活跃度较高，团队主要聚焦于 Bug 修复与功能优化。虽然新 Issue 更新量为零，但 Pull Request 活动频繁，共计 9 条，其中 6 条已合并/关闭，3 条仍在开放中。这表明项目维护效率高，侧重于解决近期问题。核心进展包括优化了 MiniMax-M3 模型的图像输入支持、修复了内部插件可见性问题，并对分享弹窗和子代理批量删除等交互细节进行了打磨。项目整体处于稳步迭代、持续优化的健康状态。

## 2. 项目进展

今日多项重要修复与功能优化已合并入主分支，主要推进了以下方面的工作：

- **模型与AI核心能力**
    - **[已合并] #2093 fix: enable image input support for MiniMax-M3**：修复了 MiniMax-M3 模型不支持图像输入的硬编码问题。此前该功能因配置继承自旧版模型而被错误禁用，现在用户可以为该模型启用图像输入功能。 *链接: [PR #2093](https://github.com/netease-youdao/LobsterAI/pull/2093)*

- **插件与系统集成**
    - **[已合并] #2096 fix(plugins): hide internal OpenClaw plugins**：修复了插件管理界面中显示内部/运行时绑定的 OpenClaw 插件的问题，避免了用户对这些不应被管理的插件进行误操作，提升了系统健壮性。 *链接: [PR #2096](https://github.com/netease-youdao/LobsterAI/pull/2096)*

- **协作与用户体验**
    - **[已合并] #2095 fix(cowork): support subagent batch deletion**：为子代理（Subagent）功能新增了批量删除会话的支持，并优化了网关清理流程的并发控制和重试机制，提升了协作功能的稳定性和使用体验。 *链接: [PR #2095](https://github.com/netease-youdao/LobsterAI/pull/2095)*
    - **[已合并] #2094 fix: 优化分享成功弹窗的信息层级**：优化了分享成功弹窗的展示样式，移除了冗余状态标识，使信息层级更清晰，属于典型的用户体验微调。 *链接: [PR #2094](https://github.com/netease-youdao/LobsterAI/pull/2094)*
    - **[已合并] #2092 Feat/2026.5.28 artifacts**：这是一个包含 Artifacts 功能相关变更的较大版本更新（从分支名推断），虽摘要信息不完整，但涉及渲染器、文档、主进程等多个区域，预计为 Artifacts 模块的迭代。 *链接: [PR #2092](https://github.com/netease-youdao/LobsterAI/pull/2092)*

- **性能与运维**
    - **[已合并] #2091 feat(mcp): optimize npx MCP launch resolution & add first response timing logs**：对基于 npx 的 MCP（Model Context Protocol）启动进行了重大优化。通过预解析和本地安装 npm 包，将启动命令固化，避免了每次会话都走慢速的 npx 路径，并增加了首次响应计时日志，有助于后期排查性能瓶颈。 *链接: [PR #2091](https://github.com/netease-youdao/LobsterAI/pull/2091)*

## 3. Bug 与稳定性

今日无新 Bug 报告，已合并的 PR 主要解决了两类现存问题，按严重程度排列如下：

- **[中等] 模型功能缺失：MiniMax-M3 无法使用图像输入**：该问题源于历史代码硬编码，导致用户无法使用新模型的多模态能力。**已有修复 PR #2093 已合并**。
- **[低] 插件管理 UI 混乱：显示不应被管理的内置插件**：该问题可能导致用户误删除或修改系统关键组件，影响稳定性。**已有修复 PR #2096 已合并**。

此外，PR #2091 中加入了重试机制，用以修复应用重启或进程中断导致 MCP 安装状态“卡住”的问题，提升了系统在非正常情况下的自恢复能力。

## 4. 功能请求与路线图信号

- **新模型支持与模型升级**：PR #388 **(Open)** 提议将 MiniMax 模型的默认版本升级至 M3。虽然此 PR 标记为 `stale`，但结合今日合并的 PR #2093（修复 M3 图像输入），可以推断团队正在进行向 M3 模型的迁移工作，这是明确的路线图信号。 *链接: [PR #388](https://github.com/netease-youdao/LobsterAI/pull/388)*
- **MCP 延迟优化**：已合并的 PR #2091 直接回应了用户在使用 npx 启动 MCP 时可能遇到的缓慢问题，并提供了系统级的优化方案。这表明团队正在认真对待与外部工具集成的性能和稳定性，可能成为下一个版本的重点优化方向。

## 5. 用户反馈摘要

今日无新的 Issue 评论。但从已合并的 PR 中可以间接推断用户的使用场景与痛点：
- **子代理功能**：PR #2095 对子代理的批量删除和网关清理进行了优化，表明用户可能在复杂的协作场景中处理大量子代理会话，并遇到了管理或性能上的不便。
- **分享功能**：PR #2094 对弹窗信息层级的调整，反映出用户对最终交付物（如图片、代码片段）的分享体验有较高要求，希望界面更清晰、简洁。

## 6. 待处理积压

以下为长期未合并的关键 PR，需要维护者关注：

- **#388 feat: upgrade MiniMax default model to M3**：一个较老的功能请求，标记为 `stale`。鉴于今日有关于 M3 模型的修复 PR 合并，该项目可能有更高优先级，建议维护者同步更新此 PR 或关闭后以新的方式推进。 *链接: [PR #388](https://github.com/netease-youdao/LobsterAI/pull/388)*
- **#1277 chore(deps-dev): bump the electron group**：一个由机器人自动提交的依赖更新 PR，涉及 Electron 和 electron-builder 的核心依赖升级。该 PR 已经开放两个多月，可能存在版本兼容性或 CI 问题需要人工介入。 *链接: [PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277)*
- **#1464 fix(im): add duplicate validation for instance name and credential ID**：这是一个重要的 IM 功能修复，为钉钉、飞书、QQ 等平台的实例管理添加重复校验，防止用户创建同名实例或重复添加同一机器人。该 PR 已开放两个月，建议尽快推进合并，以改善多实例管理体验。 *链接: [PR #1464](https://github.com/netease-youdao/LobsterAI/pull/1464)*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 — 2026-06-03

## 1. 今日速览
- 过去24小时内社区活动保持低活跃，仅有1条新Issue和1条待合并PR被更新。
- 项目无新版本发布，核心开发仍聚焦于会话历史管理与频道交互体验优化。
- **活跃度评估：** 维持温和节奏，无突发故障或热门争议，整体处于稳定演进阶段。

---

## 2. 版本发布
（今日无新版本发布）

---

## 3. 项目进展
今日**无**PR被合并或关闭，主要进展体现在：
- PR #1089（`Cap persisted tool results before rehydration`）自6月1日开启，已更新至6月3日，仍在等待审查与合并。该PR旨在限制会话历史重新水化时持久化的工具/工具结果内容，涉及普通聊天、流式聊天、压缩后重试、提示检查、静默记忆轮次及LLM支持的压缩提示等多个场景，是提升内存使用效率与稳定性的关键改动。
- 整体项目进度：即将完成对工具结果上限机制的集成，但尚未进入主分支。

---

## 4. 社区热点
**Issue #1092** — [Add a config option to disable channel Activity log tool-status messages](https://github.com/moltis-org/moltis/issues/1092)  
- **作者：** s-salamatov  
- **评论数：** 0 | **👍：** 0  
- **诉求分析：**  
  用户指出在Telegram等渠道中，Agent回复后常附带一个可折叠的“Activity log”HTML块，或当主回答通过内联流式编辑发送时，工具状态消息会作为单独的后续消息出现。  
  - 核心诉求：希望新增配置开关，允许用户禁用这些工具状态消息，以减少信息干扰，获得更清爽的交互体验。  
  - 该请求涉及用户体验中的“噪音”问题，可能影响多数使用Telegram、Discord等消息平台的用户，具有较高代表性。由于尚无人评论，社区反馈尚未累积，但方向明确。

---

## 5. Bug 与稳定性
- 今日**未报告**任何Bug、崩溃或回归问题。  
- 项目当前稳定性良好，暂无紧急修复需求。

---

## 6. 功能请求与路线图信号
- **#1092** 提出的禁用Activity log配置选项属于**显式功能请求**。结合现有PR #1089对工具结果内容的优化，可以看出项目正在系统性地改善工具交互的用户体验：一方面从后端限制数据量（PR #1089），另一方面从前端提供可选择的通信行为（#1092）。  
- 若PR #1089先行合并，可能为#1092的实现铺平技术路径（如对工具结果的整体处理逻辑更清晰）。推测该功能有较高概率被纳入下一小版本（如v0.x.y）。

---

## 7. 用户反馈摘要
- 今日所有Issue/PR下**无用户评论**，暂无直接的满意/不满意反馈。  
- 根据Issue #1092的描述，用户对当前“工具状态消息强制显示”感到不便，属于隐式不满，但尚未形成讨论。

---

## 8. 待处理积压
| 项目 | 状态 | 备注 |
|------|------|------|
| **PR #1089** — Cap persisted tool results before rehydration | 已开启5天（6月1日创建），6月3日有更新，但仍未合并 | 涉及多个核心流程，需维护者重点审查。当前无冲突标签，建议尽快安排review，避免阻塞后续功能。 |
| **Issue #1092** — 新增配置禁用Activity log | 24小时内新开，无任何响应 | 可作为下一个版本的功能候选，但需要收集更多社区反馈或维护者给出初步设计方向。 |

> 点评：项目今日节奏平稳，但PR #1089长期未合并可能成为短期瓶颈；Issue #1092代表了一个呼声较高的用户体验优化点，值得在下一轮迭代中优先考虑。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目的分析师，根据您提供的 CoPaw 项目 GitHub 数据，我已为您整理生成 2026 年 6 月 3 日的项目动态日报。

---

### CoPaw 项目动态日报 | 2026-06-03

**项目名称**: CoPaw
**数据来源**: github.com/agentscope-ai/CoPaw
**报告周期**: 2026-06-02 至 2026-06-03

---

#### 1. 今日速览

过去24小时，CoPaw项目活跃度**极高**，社区贡献与问题报告呈现爆发式增长。项目团队与社区共同处理了大量事务，36条Issue和29条PR的更新量表明项目正处于密集的迭代与修复期。尤其值得注意的是，安全研究团队（`YLChen-007`）报告了多个严重安全漏洞（已关闭），同时用户也反馈了多个影响日常使用体验的Bug和功能请求，其中微信定时任务投递失败和浏览器启动崩溃问题是社区关注的焦点。总体而言，项目在修复安全短板和稳定性的同时，也在积极吸纳新功能，整体健康状况需要在快速迭代与质量保障之间取得平衡。

---

#### 2. 版本发布

**无**。今日未有新版本发布。

---

#### 3. 项目进展

今日项目主要进展体现在对关键Bug的修复和部分功能的迭代上，许多重要PR已合并或关闭，推动了项目稳定性向前迈进。

- **关键Bug修复**:
    - **[CLOSED] WeCom频道安全加固**: PR [#4850](https://github.com/agentscope-ai/QwenPaw/pull/4850) 已合并，修复了企业微信频道中，可通过Prompt注入访问其他用户历史记录的会话隔离漏洞。
    - **[CLOSED] 微信/企微定时任务投递修复**: PR [#4883](https://github.com/agentscope-ai/QwenPaw/pull/4883) 已合并，解决了定时任务结果无法推送至微信/企业微信的问题。
    - **[CLOSED] Windows浏览器进程残留修复**: PR [#4853](https://github.com/agentscope-ai/QwenPaw/pull/4853) 已合并，针对Windows系统解决了 `browser_use` 工具使用后浏览器进程残留和临时目录锁定的问题。
    - **[CLOSED] 非标准Provider参数兼容**: PR [#4689](https://github.com/agentscope-ai/QwenPaw/pull/4689) 已合并，现在像 DashScope 的 `enable_search` 等非标准参数可以通过 `generate_kwargs` 正确传递给后端，扩展了模型兼容性。
    - **[CLOSED] 版本号更新**: PR [#4907](https://github.com/agentscope-ai/QwenPaw/pull/4907) 合并，版本号提升至 `v1.1.11b1`，为下一个版本迭代做准备。

- **功能开发推进**:
    - **[OPEN] Windows文件浏览器支持多盘符**: PR [#4906](https://github.com/agentscope-ai/QwenPaw/pull/4906) 已合并，修复了Windows下编码模式下文件浏览器被锁定在C盘的问题，现可浏览所有驱动器。
    - **[OPEN] 插件系统升级**: PR [#4804](https://github.com/agentscope-ai/QwenPaw/pull/4804) 新增了Prompt Section Registry，允许插件向Agent系统提示词注入自定义区域。PR [#4693](https://github.com/agentscope-ai/QwenPaw/pull/4693) 支持插件注册自定义频道，并附带Schema驱动的配置UI。

---

#### 4. 社区热点

今日社区讨论主要围绕**用户体验故障**和**安全问题**展开，同一安全研究人员集中报告了多个漏洞，引发了广泛关注。

- **定时任务投递失败**: Issue [#4878](https://github.com/agentscope-ai/QwenPaw/issues/4878) **（评论: 5）** 是今日最热的话题。用户报告定时任务能正常触发，但无法推送到微信，日志中出现了含混的错误码（`errcode=0`）。多位用户表达了对此问题的困扰，该问题也已通过PR #4883修复。
- **严重安全漏洞集中披露**: 安全研究员 `YLChen-007` 一口气关闭了多个安全相关的Issue（#4908, #4909, #4910, #4911, #4912, #4913, #4914, #4863），每个都有3-4条评论，显示出社区对安全问题的关注度极高。这些漏洞涵盖了API未授权修改全局设置、ToolGuard绕过、路径遍历导致文件泄露、工作区导出泄露密钥等，凸显了项目在API安全设计上仍需加强。
- **“系统级”拒绝回答**: Issue [#4837](https://github.com/agentscope-ai/QwenPaw/issues/4837) **（评论: 2）** 自v1.1.9升级后，用户频繁遭遇Agent返回固定fallback消息“无法处理您的问题”。该问题在用户升级后普遍出现，严重影响核心体验，但目前仍未标记为已关闭。

---

#### 5. Bug 与稳定性

今日报告的Bug种类繁多，覆盖核心功能、系统稳定性和外部集成。

- **严重**:
    - **系统服务中断**: Issue [#4922](https://github.com/agentscope-ai/QwenPaw/issues/4922) 报告了因一次文件路径操作失败后，所有对话都报 `Permission denied` 错误，导致Agent完全无法使用。**（无关联修复PR）**
    - **核心功能回归**: Issue [#4837](https://github.com/agentscope-ai/QwenPaw/issues/4837) 中，Agent频繁返回“无法处理”的默认回复，这是一个严重影响用户体验的回归问题。**（无关联修复PR）**
    - **上下文压缩失败**: Issue [#4924](https://github.com/agentscope-ai/QwenPaw/issues/4924) 和 [#4551](https://github.com/agentscope-ai/QwenPaw/issues/4551) 报告了上下文压缩因旧格式文件块而失败，可能导致上下文溢出和回复异常。

- **中危**:
    - **浏览器管理崩溃**: Issue [#4919](https://github.com/agentscope-ai/QwenPaw/issues/4919) 报告了在 Windows 上使用 `browser_use` 时，CDP 超时和浏览器闪退，用户需要手动降级 Playwright 版本。**（有关联修复PR #4853）**
    - **UI卡顿**: Issue [#4917](https://github.com/agentscope-ai/QwenPaw/issues/4917) 报告当聊天历史较长时，切换到聊天界面会长时间卡顿，猜测是前端渲染性能问题。**（无关联修复PR）**
    - **自定义频道管理Bug**: Issue [#4877](https://github.com/agentscope-ai/QwenPaw/issues/4877) 描述了自定义频道在保存设置时会错误地停止频道监听，这是代码逻辑问题。**（无关联修复PR）**
    - **子任务进展不可见**: Issue [#4923](https://github.com/agentscope-ai/QwenPaw/issues/4923) 报告通过 `spraw_subagent` 启动的子任务，在运行期间无法查看其内部进展。

- **低危**:
    - **MCP工具名含点号报错**: Issue [#4918](https://github.com/agentscope-ai/QwenPaw/issues/4918) 指出当MCP工具名包含 `.` 时，`gpt-5.5` 模型会因API校验失败而无法调用。
    - **多轮对话DeepSeek错误**: Issue [#3985](https://github.com/agentscope-ai/QwenPaw/issues/3985) 描述了多轮对话中DeepSeek模型的 `reasoning_content` 未正确回传导致的HTTP 500错误。

---

#### 6. 功能请求与路线图信号

今日用户请求的新功能主要集中在**易用性提升**和**高级能力扩展**方面，部分请求已有对应的PR开发中。

- **将纳入或已有PR的请求**:
    - **Windows桌面端改进**: 用户（`rescodexx`）集中反馈了多个Windows版本痛点，如“文件上传应直接传路径而非限制大小”（#4893）和“支持拖拽上传”（#4894）。这表明项目组在Windows端用户体验上有持续的优化方向。
    - **子Agent的模型选择**: Issue [#4901](https://github.com/agentscope-ai/QwenPaw/issues/4901) 提出 `spawn_subagent` 应该支持为不同子任务分配不同模型，以节省成本。这是一个高级功能需求，概念上与`Claude Code`的Haiku/Opus模式相似，体现了用户对更精细成本控制的需求。
    - **上下文无损压缩**: Issue [#4551](https://github.com/agentscope-ai/QwenPaw/issues/4551) 提出了基于DAG（有向无环图）的摘要与CJK（中文、日文、韩文）Token修复的无损上下文压缩方案，直击长对话场景下的核心痛点。虽然暂无直接PR，但这是一个很有价值的路线图信号。
    - **侧边栏UI简化**: Issue [#4904](https://github.com/agentscope-ai/QwenPaw/issues/4904) 提出侧边栏菜单过于复杂，用户日常使用频率不高，建议简化。这表明项目需要关注核心交互路径的优化。

- **潜在需求**:
    - **图片/附件不应直接加载到上下文**: Issue [#4921](https://github.com/agentscope-ai/QwenPaw/issues/4921) 提出图片等参考信息不应以Base64形式直接占用宝贵的上下文Token，提示需要更智能的上下文管理策略。

---

#### 7. 用户反馈摘要

- **痛点与不满**:
    - **“服务突然就全挂了”**: 用户 `svenyu` 在 #4922 中描述了因一次失败操作导致Agent完全不可用，情绪沮丧。
    - **“大量搜索结果被压缩后丢失”**: 用户 `lioude` 在 #4551 中详细描述了当前压缩机制导致的多场景下信息丢失问题，这是深度用户的典型痛点。
    - **“切换界面要卡很长时间”**: 用户 `rescodexa` 在 #4917 中抱怨大量聊天数据下的UI响应问题，这直接影响了日常使用流畅度。

- **使用场景与诉求**:
    - **自动化工作流**: #4878 展示了用户利用定时任务和微信投递构建自动化场景的需求，但失败的推送体验打击了用户信心。
    - **企业级应用**: #4845 和 #4850 的讨论突显了企业微信用户在安全与隔离方面的刚性需求。
    - **跨平台体验**: `rescodexx` 用户对Windows版的一系列改进建议，显示出不同平台间用户体验不一致是普遍现象。

---

#### 8. 待处理积压

部分重要Issue/PR长期未关闭或被响应，建议维护者重点关注。

- **重大Bug长期未修复**:
    - **[OPEN] AgentScope 2.0 迁移**: PR [#4846](https://github.com/agentscope-ai/QwenPaw/pull/4846) 这是一个重大的破坏性变更，旨在将AgentScope框架从1.x升级到2.0。此PR自6月1日起持续开放并标记为“Under Review”，需要更多关注和资源投入。
    - **[OPEN] 系统级Fallback回复**: Issue [#4837](https://github.com/agentscope-ai/QwenPaw/issues/4837) 该问题严重影响核心对话体验，且自5月31日以来仍未关闭或有关联修复PR，需优先处理。

- **长期未响应的功能请求**:
    - **[OPEN] E2B和AgentScope沙箱集成**: PR [#2275](https://github.com/agentscope-ai/QwenPaw/pull/2275) 自3月25日开启，已近3个月，是增强Agent安全能力的重要功能，但进展缓慢。
    - **[OPEN] Tauri桌面自动更新**: PR [#4669](https://github.com/agentscope-ai/QwenPaw/pull/4669) 作为提升桌面端用户体验的关键功能，也持续开放了较长时间，建议推动合并。
    - **[OPEN] 工具定义按需加载**: Issue [#4836](https://github.com/agentscope-ai/QwenPaw/issues/4836) 提出了减少初始上下文Token开销的明确方案，能显著优化性能，但未有PR跟进。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 ZeroClaw 项目数据，为您生成 2026 年 6 月 3 日的项目动态日报。

---

# ZeroClaw 项目日报 | 2026-06-03

## 今日速览

今日 ZeroClaw 项目状态 **极其活跃，处于一个重要的发布后沉淀与关键 Bug 修复期**。核心动态是 **v0.8.0-beta-2 版本的发布**，该版本带来了重量级新功能“zerocode” TUI。社区响应热烈，配合版本发布，在 24 小时内关闭了高达 33 个 Issues 和 47 个 PRs，反映了项目团队强大的交付和问题解决能力。当前社区讨论焦点集中在修复因版本更新和配置错误导致的安全绕过、初始化崩溃及功能兼容性问题。整体项目健康度良好，正从大规模开发阶段进入稳定性强化阶段。

## 版本发布

- **v0.8.0-beta-2**: 该版本是自 v0.7.5 以来最大的一次更新，核心亮点是 **zerocode** —— 一个全新的、功能完备的终端 UI（TUI），允许用户在不离开终端的情况下运行和操作代理。此外，该版本还发布了多智能体运行时（multi-agent runtime），为未来更复杂的协作场景奠定了基础。
    - **破坏性变更**: 无明确提及，但“多智能体运行时”的引入可能对内部 API 和技能开发方式产生影响。
    - **迁移注意事项**: 对于现有用户，建议仔细阅读此版本的更新日志，了解 TUI 和多智能体功能的具体启动和使用方式。技能开发者需关注可能存在的 API 变动。

## 项目进展

今日项目推进速度极快，核心在于解决版本发布后暴露的安全漏洞和功能故障，并同步优化了文档和基础设施。

- **安全与权限修复**:
    - **PR #6207** (关闭) 修复了 Web 仪表盘 / WebSocket 网关绕过 `ApprovalManager` 的严重安全漏洞，确保工具调用审批流程适用于所有通道。
    - **PR #5981** (关闭) 修复了技能系统忽略 `allow_scripts` 配置的问题，现在脚本权限能正确生效。
    - **PR #5952** (关闭) 重新定义了技能审核范围，将其限定为结构和文件系统检查，将命令内容安全交由执行时策略处理，明确了安全职责边界。
- **平台兼容性与 Bug 修复**:
    - **PR #6878** (关闭) 修复了 Bubblewrap 沙箱在 Fedora 43 上因缺少 `lib64` 目录而崩溃的问题。
    - **PR #6681** (关闭) 修复了 `zeroclaw skills install` 命令在多线程运行时环境中因使用阻塞 HTTP 客户端而导致的崩溃 (panic)。
    - **PR #6269** (关闭) 修复了上下文压缩器丢弃 `reasoning_content` 的问题，保障了依赖推理内容的模型（如 DeepSeek）的正常工作。
- **功能完善与生态建设**:
    - **PR #7023** (合并/关闭) 实现了版本化的文档部署和版本选择器，极大改善了用户按版本查阅文档的体验。
    - **PR #6009** (合并/关闭) 丰富了 OpenTelemetry (OTel) 工具调用追踪的语义属性，提升了对代理行为的可观测性。
    - **多个文档 PR (如 #6057, #5863)** 被合并，新增了 Python 技能快速入门、技能格式等关键文档，降低了新用户的上手门槛。

## 社区热点

今日社区讨论热度最高的议题主要围绕新版本安装与核心功能故障：

1.  **#[6123] [Bug]: default_model issue on fresh install** (评论: 18) - 该 Issue 获得了今日最多的关注，反映了新用户在首次安装配置时的普遍痛点。用户报告在 LXC 容器中进行全新安装后，即使完成了 onboarding，也无法选择非本地的 Ollama 模型，导致工作流完全被阻塞。背后的核心诉求是 **“零配置”或更智能的网络发现/配置引导**，以简化首次使用体验。
2.  **#[5722] Default shell sandbox configuration blocks all realistic Python skill patterns** (评论: 6) - 这是一个来自资深开发者关于沙箱配置的深度反馈。用户指出，默认的 shell 沙箱配置（如仅允许特定命令）对大多数真实的 Python 技能开发场景来说过于严格，导致开发受阻。这反映了社区对 **“开箱即用”与“安全沙箱”之间的平衡** 有强烈需求，希望提供更灵活的开发沙箱配置选项或预设。
3.  **#[6246] [Bug]: WhatsApp Web channel: pair succeeds but messages don't flow** (评论: 6) - 该问题报告，即使扫码配对成功，WhatsApp Web 通道在 2026 年 4 月的服务端协议升级后无法收发消息。这显示了 **渠道连接对上游第三方协议变更的脆弱性**，社区期望能有更鲁棒的连接检测和快速修复预案。

## Bug 与稳定性

今日报告的 Bug 主要集中在版本兼容性和配置错误引起的功能阻塞上，且大部分已得到迅速修复。

| 严重程度 | Issue 编号 | 标题 | 当前状态 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| **S1 - Workflow blocked** | #6207 | Web dashboard / WebSocket gateway path bypasses ApprovalManager | **已关闭** | 严重安全漏洞，已修复。 |
| **S1 - Workflow blocked** | #6681 | zeroclaw skills install clawhub:* panics | **已关闭** | 安装命令崩溃，已修复。 |
| **S1 - Workflow blocked** | #6878 | Bubblewrap fails on Fedora 43 due to bwrap parameters | **已关闭** | Linux 平台兼容性问题，已修复。 |
| **S1 - Workflow blocked** | #6123 | default_model issue on fresh install | **已关闭** | 新用户安装配置问题，已关闭，可能通过文档或配置优化解决。 |
| **S1 - Workflow blocked** | #6246 | WhatsApp Web channel: pair succeeds but messages don't flow | **已关闭** | 第三方协议变更导致，已关闭。 |
| **S2 - Degraded behavior** | #6269 | Context compressor drops reasoning_content | **已关闭** | 核心功能降级，影响 DeepSeek 推理能力，已修复。 |
| **S2 - Degraded behavior** | #6431 | SQLite memory schema init can fail during concurrent startup | **已关闭** | 并发启动问题，已修复。 |
| **S2 - Degraded behavior** | #5962 | Ollama Provider call failed when tools are needed | **开放中** | 已知问题，影响 Ollama 用户使用工具能力，仍需关注。 |

## 功能请求与路线图信号

今日社区提出的功能请求主要围绕 TUI 的完善和协议扩展，这与 v0.8.0-beta-2 的发布方向高度一致。

- **#[6824] [Tracker]: TUI Agent Chat** - 该跟踪器总结了 TUI 交互式聊天的现状，并计划添加 diff 显示、文件提议等高级功能。鉴于 TUI 是新版本的核心，这些功能极有可能被纳入后续的小版本或补丁中。
- **#[6820] [Feature]: ACP protocol extensions for diff/file-proposal message types** - 这是一个与 TUI 功能协同的协议扩展请求。考虑到已有原型和明确的用例，该功能有很大概率加入下一个版本。
- **#[4853] [Feature]: Installing skills from `.well-known` URI** - 这是一个已开放数周的需求，旨在使技能安装遵循 `.well-known` 标准。虽然优先级为 P2，但它表明了社区对去中心化、标准化技能生态的长期愿景。

## 用户反馈摘要

- **正向反馈**: 用户对新版文档（#5863, #6057）和技能创建功能（#5874）表现出积极兴趣，表明更强的文档支持和 LLM 辅助技能创建是受欢迎的方向。
- **痛点反馈**:
    - **配置复杂性**: 多个 Issue (如 #6123, #5962) 反映出用户对新版配置（如 Provider 选择、技能设置、沙箱配置）的复杂性感到困扰，希望有更智能的默认值和自动检测。
    - **安全问题与用户预期**: #6207 暴露的安全漏洞表明，即便功能强大，用户对安全性也极为敏感。同时，#5722 中关于沙箱过于严格的意见，也体现了安全性与易用性之间的拉扯。开发者 RyanHoldren 在 #5956 中明确了对技能审核范围的界定，是对此的积极回应。
    - **渠道稳定性**: 第三方渠道（如 WhatsApp）的协议变更会导致服务中断 (#6246)，这使得核心功能的稳定性依赖于外部服务，是用户的一大焦虑点。

## 待处理积压

以下为一些长期开放但更新较少或未关闭的重要问题，建议维护团队投入关注：

- **#[5962] [Bug]: Ollama Provider call failed when tools are needed** (开放, P2) - 这是一个影响范围较广的 Bug，阻塞了 Ollama 用户的工具调用工作流。虽然更新为 6 月 3 日，但状态仍为“in-progress”。鉴于其 S1 严重性，建议优先解决。
- **#[4853] [Feature]: Installing skills from `.well-known` URI** (开放, P2) - 一个长期等待的标准功能请求，对于构建开放技能生态至关重要。可能因其涉及大规模架构变更而被推迟，但应有所规划。
- **#[5155] [Bug]: Delegate agents ignore [skills].prompt_injection_mode** (开放, P1) - 一个涉及多代理运行时正确性的关键 Bug，其状态自 3 月以来未有进展，考虑到 v0.8.0 引入了多智能体运行时，解决此问题显得尤为迫切。

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*