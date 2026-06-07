# OpenClaw 生态日报 2026-06-07

> Issues: 294 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-07 02:50 UTC

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

好的，这是根据您提供的 OpenClaw GitHub 数据生成的 2026 年 6 月 7 日项目动态日报。

---

# OpenClaw 项目动态日报 - 2026-06-07

## 1. 今日速览

OpenClaw 项目在 2026 年 6 月 6 日保持极高活跃度。过去 24 小时内，有近 300 条 Issue 更新和 500 条 PR 更新，反映出项目维护和社区参与的热度。新发布了两个 `2026.6.5` 测试版，主要修复了 QQ 机器人的推理内容泄露和 MCP 工具结果格式化问题。然而，高度活跃的表象下，社区围绕 `2026.6.1` 版本升级后出现的 OpenAI Responses API 兼容性问题、Codex 应用服务器卡顿以及成本飙升等严重 Bug 展开了激烈讨论，表明最新稳定版可能存在一些关键性回归问题。

## 2. 版本发布

过去 24 小时内发布了 2 个版本。

- **[v2026.6.5-beta.2](https://github.com/openclaw/openclaw/releases/tag/v2026.6.5-beta.2)** & **[v2026.6.5-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.5-beta.1)**
  - **主要更新**:
    1.  **QQBot修复**: 现在会在消息发送前自动剥离模型输出的推理/思考过程标签 (如 `<thinking>`)，防止原始内容泄露到群聊回复中。
    2.  **MCP工具结果强化**: 对 MCP (Model Context Protocol) 工具返回的结果进行了类型强制转换，特别是对 `resource_link`、`resource`、`audio` 以及格式错误的图片等数据类型进行规范化处理，增强了稳定性。
  - **破坏性变更与迁移注意事项**: 无需要特别关注的破坏性变更。

## 3. 项目进展

尽管未合并大规模 PR，但社区的代码贡献仍在持续推进关键的 Bug 修复和功能完善。

- **代理模型目录继承** ([PR #90903](https://github.com/openclaw/openclaw/pull/90903)): 修复了二级（非默认）代理无法继承默认代理模型目录的问题，解决了特定情况下运行时模型不可知的错误。
- **会话清理策略** ([PR #91057](https://github.com/openclaw/openclaw/pull/91057)): 提出为“模型运行”类型的临时会话引入独立的保留时长配置，并清理过期会话，以减少资源占用。
- **Google/Vertex AI 支持** ([PR #90960](https://github.com/openclaw/openclaw/pull/90960)): 修复了 Vertex AI 图片和视频生成功能因凭据获取机制而失败的问题。
- **模型配置性能** ([PR #90741](https://github.com/openclaw/openclaw/pull/90741)): 优化了模型配置的认证凭据指纹缓存和目标提供商短路逻辑，有望减少不必要的插件发现和提供商目录查询，提升启动和运行时性能。

## 4. 社区热点

今日社区讨论的焦点集中在 `2026.6.1` 版本升级后出现的几个严重问题上，用户情绪较为焦虑。

1.  **OpenAI Responses API 兼容性问题** ([Issue #90083](https://github.com/openclaw/openclaw/issues/90083), [Issue #90093](https://github.com/openclaw/openclaw/issues/90093)): 这两个 Issue 均报告了在 `2026.6.1` 版本中，`openai/gpt-5.4` 和 `gpt-5.5` 模型调用 OpenAI Responses API 失败，报错 `invalid_provider_content_type` 或 `invalid_encrypted_content`。评论数众多，成为当日最活跃的讨论。这表明新版本在 API 对接上可能存在严重的协议兼容问题，直接影响核心聊天功能。用户 @richardmqq 在 #90093 中描述了首轮对话成功、次轮必败的“鬼畜”现象，还原度极高。

2.  **Codex 应用服务器卡顿** ([Issue #88312](https://github.com/openclaw/openclaw/issues/88312)): 一个高优先级的回归问题。用户 @"yair" 报告从 `2026.5.27` 版本开始，Codex 应用服务的多工具代理回合会频繁卡死，报错“Codex stopped before confirming the turn was complete”。此问题曾于 #84076 报告并在 #85107 修复，如今再次回归，社区对此表示失望。

3.  **升级后成本飙升与功能失效** ([Issue #91018](https://github.com/openclaw/openclaw/issues/91018)): 用户 @RavenSS213 发布严重警告，称升级到 `2026.6.1` 后 DeepSeek 模型的 Prompt Cache 功能完全失效，导致在一小时内烧掉了约 6 美元。这个 Issue 虽然评论数不多，但其直接的经济损失警示性强，引发了社区的广泛关注和担忧。

## 5. Bug 与稳定性

今日报告的 Bug 数量多且严重，主要集中在 `2026.6.1` 版本的回归问题上。

- **P1 (严重)**:
  - **[Bug]: OpenAI ChatGPT Responses fails…** ([#90083](https://github.com/openclaw/openclaw/issues/90083)) - API 兼容性问题，无关联的 Fix PR。
  - **[Bug]: Codex app-server turn-completion stall returns** ([#88312](https://github.com/openclaw/openclaw/issues/88312)) - 严重回归问题，无关联的 Fix PR。
  - **[Bug]: Subagent announce compaction for Codex/OAuth falls…** ([#90925](https://github.com/openclaw/openclaw/issues/90925)) - 子代理压缩路径错误，导致 Codex/OAuth 路由失败，无关联的 Fix PR。
  - **[Bug]: Cron scheduled trigger contaminates global runtime state** ([#90991](https://github.com/openclaw/openclaw/issues/90991)) - 定时任务可能导致系统过载，影响范围广。
  - **[Bug]: 升级 2026.6.1 后 Prompt Cache 失效** ([#91018](https://github.com/openclaw/openclaw/issues/91018)) - 导致用户成本飙升，影响严重。

- **P2 (中等)**:
  - **[Bug]: gateway hangs at `[gateway] starting...`** ([#90886](https://github.com/openclaw/openclaw/issues/90886)) - 提供者配置缺少凭据导致网关启动挂起，这是一个回归问题。
  - **[Bug]: `read` tool fails to read WebChat uploaded images** ([#90964](https://github.com/openclaw/openclaw/issues/90964)) - WebChat 上传的图片无法被 `read` 工具访问，这是一个回归问题。
  - **[Bug]: exec tool triggers gateway SIGTERM restart on WSL2** ([#90428](https://github.com/openclaw/openclaw/issues/90428)) - 在特定环境下执行工具导致网关重启。

## 6. 功能请求与路线图信号

尽管社区被 Bug 困扰，但仍有一些与未来路线图相关的功能请求被提出。

- **更多本地模型提供商** ([Issue #89265](https://github.com/openclaw/openclaw/issues/89265)): 用户提议将本地模型视为“一等公民”，降低对高价云 API 的依赖。这反映了社区对成本控制和对本地化部署的强烈诉求。
- **Topic 会话家族** ([Issue #90916](https://github.com/openclaw/openclaw/issues/90916)): 提出为同一 AI 助手创建多个独立的话题上下文通道，同时共享长期记忆。这是一个高级功能请求，可能对架构有较大影响。
- **预压缩内存追加的边界验证** ([Issue #90354](https://github.com/openclaw/openclaw/issues/90354)): 建议为内存追加操作增加硬性限制和验证，防止模型写入过大或冗余内容。这显示出社区对内存管理和会话质量的精细化思考。

## 7. 用户反馈摘要

- **主要痛点**:
  - **升级恐惧**: `2026.6.1` 版本带来的多重回归问题（OpenAI API 兼容性、Codex 卡顿、成本飙升）严重消耗了用户的信任和耐心。现有用户对“升级”这一行为产生了抵触情绪。
  - **功能质量下滑**: 一些核心功能，如 ChatGPT Responses 接口、Codex 应用服务，在升级后反而失效或降级，用户体验不佳。
  - **本地化与成本**: 许多用户表达了对增加本地模型支持、减少对昂贵云 API 依赖的强烈愿望。这反馈了整个行业对推理成本日益敏感的趋势。

- **使用场景**: 用户广泛使用 OpenClaw 作为个人 AI 助手，连接各类聊天平台（如 QQ、飞书）和 AI 模型（如 GPT、Claude、DeepSeek），并利用 Codex 等工具进行编程辅助。大量 Bug 报告都围绕这些核心场景。

## 8. 待处理积压

以下 Issue 或 PR 较为重要且存在时间较长，但仍未被解决或得到维护者明确回应：

- **Issue #58730**: [Feature Request] exec() sandbox isolation and tool permission model (创建于 2026-04-01) - 关于 sandbox 隔离的重要功能提议，可能对安全性有深远影响。
- **Issue #58818**: [Feature] guarantee last N raw messages in agent context (创建于 2026-04-01) - 关于代理上下文保留的重要功能，对提升对话连贯性至关重要。
- **Issue #62615**: [Feature]: Add gateway-side circuit breaker for unhealthy sessions (创建于 2026-04-07) - 提议增加熔断机制，对提升系统稳定性有益。
- **PR #78441**: feat(subagents): forward toolsAllow from sessions_spawn (创建于 2026-05-06) - 一个增强子代理功能的重要 PR，标记为“ready for maintainer look”，但已等待一个多月，建议维护者关注。
- **Issue #45508**: [Feature]: Self-hosted STT/TTS provider support in webchat (创建于 2026-03-13) - 一个长期未响应的功能请求，涉及对自托管语音服务的支持。

---

## 横向生态对比

好的，作为一名专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，我已仔细审阅了您提供的 2026 年 6 月 7 日各项目的社区动态数据。现基于这些数据，为您呈现一份横向对比分析报告。

---

### **AI 智能体开源生态横向对比分析报告 (2026-06-07)**

#### **1. 生态全景**

当前个人 AI 助手/自主智能体开源生态呈现出 **“爆炸式增长与分化”** 的态势。一方面，核心项目（如 `OpenClaw`, `ZeroClaw`）保持着极高的开发活跃度，PR/Issue 数量动辄数百，社区参与热情空前高涨。另一方面，这种快速发展也伴随着 **“激进迭代的双刃剑效应”**： `OpenClaw` 与 `CoPaw` 在最新版本中均暴露出严重的回归性 Bug，导致用户出现“升级恐惧”，表明生态在追求功能丰富度的同时，稳定性保障已成为关键挑战。同时，差异化竞争格局日益清晰，部分项目（如 `ZeroClaw` 的 WASM 插件、`PicoClaw` 的嵌入式定位）正通过独特的技术路线寻求细分市场的领导地位。

#### **2. 各项目活跃度对比**

| 项目名称 | Issue 更新 (24h) | PR 更新 (24h) | 版本发布 | 健康度评估 (基于数据)* |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | ~300 | ~500 | 2个Beta | **高风险**：极高活跃度，但社区因核心回归 Bug (API/Codex) 而焦虑，稳定性堪忧。 |
| **ZeroClaw** | 39 | 50 | 0 | **高速冲刺**：高产出，聚焦安全/WASM，开发效率高，但无版本发布，积压多。 |
| **Hermes Agent** | 50 | 50 (新开) | 0 | **快速迭代**：Bug修复和功能PR密集，但合并率偏低，积压趋势上升。 |
| **IronClaw** | - | 31 (总) / 10 (合) | 0 | **架构冲刺**：围绕 “Reborn” 重构高强度开发，CI/稳定性问题突出。 |
| **NanoBot** | 7 (新开4) | 24 (总) / 10 (合) | 0 | **稳健发展**：社区贡献高效，修复与功能并重，无新版本但活跃度健康。 |
| **PicoClaw** | 12 (新开10) | 15 (合) | 1个Nightly | **快速发展**：修复与功能并进，多智能体框架是亮点，社区贡献积极。 |
| **CoPaw** | 11 (新开9) | 0 | 0 | **问题爆发**：v1.1.10 版本出现多个回归 Bug，无修复 PR，用户反馈集中，维护需加强。 |
| **LobsterAI** | 6 (均活跃) | 2 (合) | 0 | **小幅迭代**：平稳维护，功能增强（导出、多Agent），但长期Bug未修复。 |
| **NanoClaw** | ~2 | 14 (总) / 3 (合) | 0 | **修复冲刺**：PR 活动频繁，大量修复和重构 PR 在等待合并，节奏紧张。 |
| **ZeptoClaw** | 3 (1新开) | 1 (待合) | 0 | **聚焦治理**：围绕“二进制大小”门禁进行制度建设，开发节奏相对缓慢。 |
| **Moltis** | 3 (新开) | 0 | 0 | **低活跃**：无代码推进，但有2个高优先级 Bug 待响应，需警惕风险。 |
| **NullClaw / TinyClaw** | 0 | 0 | 0 | **休眠状态**：过去24小时无任何活动。 |

*注：健康度评估基于数据综合判断，反映了项目的活跃度、稳定性、社区情绪。

#### **3. OpenClaw 在生态中的定位**

- **核心参照与“众矢之的”**：`OpenClaw` 凭借其全面的功能和庞大的社区，已成为事实上的生态标杆。其 `OpenAI Responses API` 兼容问题和 `Codex` 服务卡顿等回归 Bug 之所以引发巨大反响，正是因为其用户基数大、影响面广。
- **技术路线差异**：与 `ZeroClaw` 押注 WASM 插件不同，`OpenClaw` 更侧重于构建一个“大而全”的平台，集成多种协议（如 MCP）、支持多个聊天平台（QQ、飞书等）。其核心问题暴露了 **“规模化管理复杂性”** 的挑战。
- **社区规模对比**：从 Issue/PR 数量级（数百条）看，`OpenClaw` 的社区规模在所有项目中断崖式领先。然而，其社区情绪也最为复杂，既有积极贡献者，也有因升级问题而沮丧的活跃用户。
- **竞争替代威胁**：`NanoBot` 和 `PicoClaw` 凭借更轻量、更稳定的特性，正在吸引那些对 `OpenClaw` 版本升级感到疲惫的用户。如果 `OpenClaw` 不能尽快解决稳定性问题，可能会面临用户流失的风险。

#### **4. 共同关注的技术方向**

- **成本控制与模型优化 (OpenClaw, NanoBot, CoPaw)**：
    - **诉求**：`OpenClaw` 用户报告升级后 Prompt Cache 失效导致成本飙升；`NanoBot` 用户报告缓存失效。`CoPaw` 用户抱怨 `/compact` 命令忽略 `max_input_length`。
    - **信号**：社区对 AI 推理成本的敏感度已达到新高度，模型上下文管理、缓存策略、压缩机制的优化成为刚需。
- **平台集成与渠道扩展 (OpenClaw, NanoBot, PicoClaw, Hermes Agent)**：
    - **诉求**：`PicoClaw` 合并了 Google Chat 支持；`NanoBot` 优化了 WhatsApp 和 Discord；`Hermes Agent` 提交了 QQ、钉钉等的稳定性修复。
    - **信号**：从单一聊天平台向“全渠道”AI 助手演进是共同趋势，Slack、Telegram、企业微信等成为必争之地。
- **MCP 集成与工具生态 (OpenClaw, NanoBot, NanoClaw, ZeroClaw)**：
    - **诉求**：`OpenClaw` 强化 MCP 工具结果；`NanoBot` 修复 MCP 相关问题；`NanoClaw` 有支持 MCP HTTP/SSE 的PR；`ZeroClaw` 则另辟蹊径主打 WASM 插件。
    - **信号**：生态正围绕“MCP vs WASM”两种工具扩展路径形成分化，MCP 是主流，但 WASM 在安全性和跨语言方面展现出潜力。
- **安全与权限控制 (ZeroClaw, Hermes Agent, NanoClaw, PicoClaw)**：
    - **诉求**：`ZeroClaw` 修复 `[secret]` 泄露，提出 OAuth 支持；`NanoClaw` 修复工作区逃逸漏洞；`PicoClaw` 大量防御性修复。
    - **信号**：随着智能体被赋予更多敏感操作（文件、网络、执行命令），安全已成为所有项目的“默认高优先级”。
- **多智能体/子代理协作 (PicoClaw, IronClaw, LobsterAI)**：
    - **诉求**：`PicoClaw` 合并了“多智能体协作框架”；`IronClaw` 在设计文档中敲定了“子代理+上下文压缩”方案；`LobsterAI` 为定时任务增加了Agent归属选择。
    - **信号**：从单一智能体向“智能体网络”演进是下一个重要方向，子代理管理、上下文共享、任务编排是核心挑战。
- **用户体验 (UX) 与交互优化 (LobsterAI, CoPaw, Hermes Agent)**：
    - **诉求**：`LobsterAI` 反馈未保存提示、任务中断；`CoPaw` 建议侧栏会话切换、实时反馈；`Hermes Agent` 要求桌面端功能增强。
    - **信号**：当基础功能趋于完善，用户对操作流畅度、信息反馈、跨平台一致性等软性体验的要求显著提升。

#### **5. 差异化定位分析**

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全能平台 | 高级玩家、团队、企业 | 功能堆叠（多协议/多平台），但暴露了“大而全”的管理痛点。 |
| **ZeroClaw** | 安全、插件化 | 对安全敏感、追求可扩展性的用户 | 【核心差异】WASM 插件系统，安全沙箱，构建独特生态。 |
| **PicoClaw** | 轻量嵌入式、多Agent | 开发者、IoT/机器人、资源受限场景 | 聚焦多智能体框架，防御性编码，适合作为 SDK 或嵌入式组件。 |
| **NanoBot** | 稳定、即时通讯聚合 | 日常个人用户、多平台社媒管理 | 【核心差异】稳定的即时通讯桥接，社区修复效率高，偏“实用工具”。 |
| **Hermes Agent** | 学术研究、桌面体验 | 研究者、独立开发者 | 关注命令行和桌面体验，提供商支持广泛，但对“智能体”本身特性挖掘较浅。 |
| **IronClaw** | 工作流引擎、企业级 | 企业应用开发者 | 【核心差异】“Reborn”重构，向 OpenAI API 兼容的 AI 产品工作流平台演进。 |
| **CoPaw** | Coding Mode 体验 | 程序开发者 | 聚焦编程辅助场景，但近期回归问题严重，偏离了其核心定位的稳定性。 |

#### **6. 社区热度与成熟度**

- **快速迭代/架构层**：
    - **OpenClaw, ZeroClaw, IronClaw**：这三个项目处于最前沿的探索和开发阶段，社区贡献巨大，但伴随而来的大量 Bug 和不稳定是其共性问题。它们代表了生态的技术“天花板”和“可能性”。
- **质量巩固/功能层**：
    - **NanoBot, PicoClaw, Hermes Agent**：这些项目在特定方向上已相对成熟，社区贡献主要集中在 Bug 修复、性能优化和功能完善上。它们是生态的中坚力量，更稳定可靠。
- **低活跃/冷启动层**：
    - **CoPaw, LobsterAI, NanoClaw, Moltis**：这些项目要么在修复关键问题（CoPaw），要么在缓慢迭代（LobsterAI），要么处于早期或停滞状态（Moltis, NullClaw）。它们或有特定亮点，但整体影响力有限。

#### **7. 值得关注的趋势信号**

1.  **“升级恐惧”成为社区普遍情绪 (OpenClaw, CoPaw)**：当“新版本 = 新 Bug”成为常态，用户对升级的抵触情绪将威胁整个生态的健康度。这提示所有项目，**“稳定压倒一切”** 不应只是口号，而应是发布周期的核心准则。
2.  **成本敏感性驱动技术选择 (OpenClaw, NanoBot, CoPaw)**：用户开始主动监控和分析 API 成本。这推动了对 **更高效的缓存策略、模型压缩算法、以及本地模型优先** 的需求。智能体框架的“成本治理”将成为一个新的功能领域。
3.  **WASM 插件生态异军突起 (ZeroClaw)**：在 MCP 成为事实标准时，`ZeroClaw` 勇敢地押注 WASM，旨在解决 MCP 在安全性、跨语言和运行时隔离上的潜在不足。无论成败，这都为生态带来了宝贵的“方案多样性”，**WASM vs MCP** 的路线之争值得长期关注。
4.  **“本地化”与“多模态”是下一个战场 (PicoClaw, Hermes Agent, ZeroClaw)**：从 `PicoClaw` 的嵌入式定位到 `Hermes Agent` 对语音 API 的支持，再到 `ZeptoClaw` 对 aarch64 体积的控制，社区对 **隐私、离线、低延迟、多感官交互** 的渴望愈发强烈。
5.  **从“助手”到“平台”的演进 (IronClaw, ZeroClaw)**：`IronClaw` 的 “Reborn” 重构和 `ZeroClaw` 的 WASM 注册中心，都显示出项目正致力于从“一个AI助手”进化为“一个能运行和管理AI智能体的平台”。这种 **“平台化”倾向** 是行业走向成熟的重要标志。

**对技术决策者的建议**：
- **优先选择成熟稳定的项目**：对于核心业务，建议优先选择 `NanoBot`、`PicoClaw` 等处于“质量巩固层”的项目，它们更可靠。
- **关注使用成本**：在选择模型和框架时，将 **上下文缓存、压缩策略、成本监控** 等能力纳入重点评估指标。
- **拥抱差异化**：如果你的应用场景对安全、可扩展性有极致要求，`ZeroClaw` 的 WASM 路线值得探索。如果需要强工作流引擎，则应关注 `IronClaw` 的进展。
- **理解风险**：使用 `OpenClaw` 这样的标杆项目，需要建立相应的“升级规避”和“快速回滚”机制，以应对潜在的回归问题。
- **警惕“沉寂”项目**：对于 `NullClaw`、`TinyClaw` 这类长期无活动的项目，除非有特殊需求，否则应视为“放弃”状态，避免技术选型依赖。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 NanoBot 项目 GitHub 数据生成的 **2026-06-07 项目动态日报**。

---

## NanoBot 项目动态日报 | 2026-06-07

### 1. 今日速览

今日项目活跃度**高**。过去24小时内，社区贡献热情高涨，共有 **24 条 PR 更新**，其中 **10 条已合并/关闭**，展现了高效的协作与迭代能力。但同时，**14 条待合并 PR** 也带来了一定的积压压力。Issues 方面，有 **7 条更新**，其中 4 个新问题被提出，主要集中在稳定性与功能增强上。值得关注的是，**WhatsApp 桥接**、**Cron 任务**和**多用户隔离**等方向成为了近期的社区贡献热点，表明项目正在向更成熟的生产环境应用迈进。**无新版本发布**，建议重点关注待合并 PR 的整合进度。

### 2. 版本发布

无

### 3. 项目进展

今日社区合并/关闭了一系列重要 PR，显著推进了项目的稳定性、安全性与功能完整性：

-   **稳定性与错误修复**
    -   [PR #4228](https://github.com/HKUDS/nanobot/pull/4228) **(已合并)**：修复了自定义提供商在流式响应中丢弃空 `reasoning_content` 导致推理过程丢失的问题（[Issue #4105](https://github.com/HKUDS/nanobot/issues/4105)），这对使用 DeepSeek 等模型的用户至关重要。
    -   [PR #4209](https://github.com/HKUDS/nanobot/pull/4209) **(已合并)**：解决当 OpenAI 兼容的图片 API 不支持 `response_format` 参数时生成图片失败的问题（[Issue #4167](https://github.com/HKUDS/nanobot/issues/4167)），增强了与第三方 API 的兼容性。
    -   [PR #4211](https://github.com/HKUDS/nanobot/issues/4211) **(已关闭)**：修复了通过 SDK 使用 stdio MCP 服务器时，程序关闭可能出现的 `RuntimeError` 问题，提升了 SDK 的健壮性。

-   **特性增强与平台完善**
    -   [PR #2968](https://github.com/HKUDS/nanobot/pull/2968) **(已合并)**：实现**每用户内存隔离**功能 (`per_user_memory`)，解决了多用户部署下共享记忆导致数据混乱的问题，向多租户支持迈出关键一步。
    -   [PR #4195](https://github.com/HKUDS/nanobot/pull/4195) **(已合并)**：进行了**桌面版**的初步打磨，优化了桌面环境下的 WebUI 体验，并增加了文件预览、自动化等网关 API，为即将到来的桌面端应用铺平了道路。
    -   [PR #2555](https://github.com/HKUDS/nanobot/pull/2555)、[#2529](https://github.com/HKUDS/nanobot/pull/2529)、[#2528](https://github.com/HKUDS/nanobot/pull/2528) **(均已合并)**：这三条 PR 共同优化了**WhatsApp 桥接**的稳定性，解决了重连导致的消息重复、语音消息转录以及启动时重放历史消息的问题。

-   **代码清理与重构**
    -   [PR #2533](https://github.com/HKUDS/nanobot/pull/2533) **(已关闭/合并)**：为 MCP 服务器增加了 `allowFrom` 访问控制，允许限制敏感工具的使用者，提升了安全性。
    -   [PR #2532](https://github.com/HKUDS/nanobot/pull/2532) **(已关闭/合并)**：增加了 Serper.dev 作为 Google 搜索的新提供商，丰富了 Web 搜索选项。

### 4. 社区热点

-   **[Issue #2573](https://github.com/HKUDS/nanobot/issues/2573): GitHub Copilot 登录失败** (👍 9)
    -   **动态**：该 Issue 于近日关闭，但获得了 9 个点赞和 3 条评论，是过去一段时间内社区反应最强烈的问题。
    -   **分析**：用户在使用 `nanobot provider login github-copilot` 时遭遇认证错误，问题指向使用 OpenAI 库替换 LiteLLM 后引入的新 Bug。**核心诉求是核心功能的稳定性和关键入口的可用性**，这也解释了为何会获得高赞。

-   **[PR #4094](https://github.com/HKUDS/nanobot/pull/4094): 修复频道分发的持久化与流身份** (待合并，1周)
    -   **动态**：该 PR 从 5 月 29 日提出至今，评论数为 *undefined*，但其修复的三个 Issue（#4062, #4063, #4064）均涉及 WebSocket 消息持久化与流身份识别，**对构建可靠的实时通信系统至关重要**。
    -   **分析**：该 PR 长期待合并，可能由于改动较大或需要更多评审。其背后反映的是社区对**消息投递可靠性**和**多用户/多会话场景下数据一致性**的较高要求。

### 5. Bug 与稳定性

按严重程度排列：

-   **高**
    -   [Issue #4222](https://github.com/HKUDS/nanobot/issues/4222) **[OPEN]**：`max_messages` 截断与微压缩机制持续导致**前缀/提示缓存失效**。这会显著增加 API 调用成本和延迟，严重影响使用体验。目前暂无关联的 fix PR。
    -   [Issue #4105](https://github.com/HKUDS/nanobot/issues/4105) **[OPEN]**：自定义提供商在 tool_call 消息中丢弃空的 `reasoning_content`。这被认为是一个错误行为，因为某些 API（如 DeepSeek）要求该字段存在。已有 [PR #4228](https://github.com/HKUDS/nanobot/pull/4228) 和 [PR #4227](https://github.com/HKUDS/nanobot/pull/4227) 提出修复。

-   **中**
    -   [PR #4221](https://github.com/HKUDS/nanobot/pull/4221) **[OPEN]**：修复 `exec` 工具中**相对符号链接导致的工作区逃逸**漏洞。这是一个安全修复，确保受限命令的执行环境安全。关联 [Issue #4072](https://github.com/HKUDS/nanobot/issues/4072)。
    -   [PR #4223](https://github.com/HKUDS/nanobot/pull/4223) **[OPEN]**：修复微信频道在 session 过期后**永久静默**的死循环问题。该 Bug 会导致用户必须重新扫码才能恢复服务，影响严重。
    -   [PR #4219](https://github.com/HKUDS/nanobot/pull/4219) **[OPEN]**：修复 session 历史记录中，末尾存在孤立 tool result 消息时，`retain_recent_legal_suffix` 函数可能返回空列表的问题。关联 [Issue #4203](https://github.com/HKUDS/nanobot/issues/4203)。

-   **低**
    -   [Issue #4167](https://github.com/HKUDS/nanobot/issues/4167) **[CLOSED]**：图片生成与不兼容 OpenAI 接口的 API 出错。问题已通过 [PR #4209](https://github.com/HKUDS/nanobot/pull/4209) 修复。

### 6. 功能请求与路线图信号

-   **企业级支持**：**[Issue #4220](https://github.com/HKUDS/nanobot/issues/4220) [OPEN]** 提出增加对 **GitHub Copilot for Business / Enterprise** 的支持，指向了更高的企业服务市场需求。该项目目前仅支持个人账户。
-   **WebUI 管理能力**：**[Issue #4218](https://github.com/HKUDS/nanobot/issues/4218) [OPEN]** 请求在 WebUI 中增加 **Cron 任务管理**功能。结合并行提出的 [PR #4225](https://github.com/HKUDS/nanobot/pull/4225)（Cron 静默模式与锁定接收者），可以看出社区在如何更好地使用 Cron 功能上进行探索，而更友好的 UI 管理是自然延伸。
-   **基础设施增强**：**[PR #4123](https://github.com/HKUDS/nanobot/pull/4123) [OPEN]** 为 MCP 连接增加了**SSRF（服务端请求伪造）防护**，这是一个重要的安全增强。**[PR #4033](https://github.com/HKUDS/nanobot/pull/4033) [OPEN]** 则为**多人在同一频道聊天（如 Discord）** 的场景增加了发送者身份识别，显著提升了群聊场景下的交互智能。

> **路线图信号**：上述功能点和待合并 PR 共同指向了几个未来发展方向：
> 1.  **多租户与企业支持**（用户隔离、Enterprise 支持）
> 2.  **生产环境级稳定性与安全性**（SSRF 防护、消息可靠性、漏洞修复）
> 3.  **更丰富的平台集成**（WebUI 管理、Discord 群聊、WhatsApp 桥接优化）

### 7. 用户反馈摘要

-   **痛点与真实场景**：
    -   **认证/登录障碍**：`GitHub Copilot` 的登录失败是近期最引人注目的问题。用户 `cheanus` 详细描述了操作步骤和报错，表明这是一个影响新用户上手的**关键阻塞点**。
    -   **API 兼容性问题**：`gkd2323c` 由于使用的第三方图片 API 不支持 `response_format` 参数而无法生成图片。这反映了真实世界中用户服务的多样性和项目需要兼容**非标准 API** 的挑战。
    -   **上下文理解丢失**：`imkuang` 报告了缓存失效问题，这是一个高级用户才会关注的技术细节，但直接影响成本和使用流畅度。他精确地分析了 `max_messages` 截断和微压缩机制的问题，展现了**专业用户对性能优化的高要求**。
-   **满意/不满意**：
    -   从 [PR #4228](https://github.com/HKUDS/nanobot/pull/4228) 快速响应并修复 `reasoning_content` 问题来看，社区维护者对 bug 的响应是积极的。
    -   [Issue #4222](https://github.com/HKUDS/nanobot/issues/4222) 缓存失效问题目前尚无修复，可能会让部分高级用户感到不满或等待。

### 8. 待处理积压

-   **[Issue #4105](https://github.com/HKUDS/nanobot/issues/4105) [Expires: ~1周]**: 关于自定义提供商丢弃 `reasoning_content` 的问题，现已有一个未合并的 [PR #4227](https://github.com/HKUDS/nanobot/pull/4227) 和一个已合并的 [PR #4228](https://github.com/HKUDS/nanobot/pull/4228)，请注意跟进哪个 PR 是最终解决方案。
-   **[PR #4094](https://github.com/HKUDS/nanobot/pull/4094) [Expires: 9天]**: 修复消息投递可靠性的核心 PR，亟待维护者给出评审。该 PR 长期未合并可能会影响其他相关功能的开发。
-   **[PR #4033](https://github.com/HKUDS/nanobot/pull/4033) [Expires: 10天]**: 增加聊天发送者身份识别的特性，对 Discord 等多用户频道至关重要，建议尽快处理。
-   **[PR #4123](https://github.com/HKUDS/nanobot/pull/4123) [Expires: 7天]**: 增加 SSRF 防护的安全性增强，建议尽快合并、发布，以降低安全风险。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-06-07

---

## 1. 今日速览

过去 24 小时 Hermes Agent 项目社区活跃度极高：Issues 与 PR 各新增 50 条，其中新开/活跃 Issue 40 条、待合并 PR 42 条，反映出大量用户反馈和贡献者响应。但合并/关闭率偏低（Issues 关闭 10 条，PR 合并/关闭仅 8 条），积压趋势仍在上升。值得注意的是，今日无新版本发布，但多个 P1/P2 级别的 Bug 已对应提交修复 PR，稳定性改善正在加速。桌面端（macOS/Windows）兼容性问题、提供商标配化、网关/安全加固成为今日主线。

---

## 2. 版本发布

**无新版本发布。**

---

## 3. 项目进展

今日共有 **8 个 PR 被合并或关闭**（具体详情未在公开数据中单独列出），同时有 **42 个新 PR 提交待合并**，覆盖以下重要推进方向：

- **安全加固**：Telegram 网关已提交 PR #40916，在事件构造前就拒绝未授权用户，防止 Prompt 注入；`skill_view` 命令已提交 PR #40920，修复路径遍历漏洞。
- **跨平台兼容**：Windows 桌面安装因 `powershell.exe` 路径解析问题导致卡死，已提交 PR #40927 修复；macOS 用户目录含空格导致的安装失败，已提交 PR #40923 修复。
- **插件生态**：新增 AGIone 提供商适配（PR #40910）、知识召回工具（PR #37884）、辅助模型插槽在 Dashboard 中端到端生效（PR #40922）。
- **网关可靠性**：QQBot C2C 会话权限审批（PR #40926）、DingTalk 流模式稳定性（PR #40929）、微信 WeCom 用户 ID 加载（PR #40930）均有修复 PR 提交。
- **核心配置**：`load_gateway_config()` 流式回退对标量 gateway 值做防御（PR #40914），`migrate_config()` 不再展开默认配置写入（PR #40921）。

这些 PR 一旦合并，将显著改善多平台用户体验与网关安全性。

---

## 4. 社区热点

| Issue/PR | 评论数 | 核心话题 |
|---------|-------|---------|
| [#37505](https://github.com/NousResearch/hermes-agent/issues/37505) | 6 | **macOS DMG 仅 arm64**，Intel Mac 用户无法启动，公开讨论最热烈。用户已提供完整环境信息和复现步骤，社区要求提供通用二进制或 x86_64 构建。 |
| [#27683](https://github.com/NousResearch/hermes-agent/issues/27683) | 4 | **Web 工具插件未初始化**导致搜索/提取/爬取静默失败，多位用户跟随报告同样问题，影响 `v0.13.0` 及之后版本。 |
| [#40820](https://github.com/NousResearch/hermes-agent/issues/40820) | 3 | **用户目录含空格时安装失败**，外置硬盘用户受影响，已关联 PR #40923 修复。 |
| [#6718](https://github.com/NousResearch/hermes-agent/issues/6718) | 3 | **后台进程自动通知失效**，被用户标记为与 cron 投递同源 Bug，持续近两个月未解决，社区关注度较高。 |
| [#39281](https://github.com/NousResearch/hermes-agent/issues/39281) | 3 | **Gemma4 + Ollama 后端输出截断**，模型输出 token 限制警告，影响本地部署用户实验最新模型。 |

社区诉求集中体现在 **桌面端跨架构支持不足**、**开箱即用的 Web 工具依赖正确初始化**、以及 **路径空格这一长期被忽视的兼容性问题**。

---

## 5. Bug 与稳定性

按严重程度排列，已关联修复 PR 的标注“✅ 已有 fix PR”。

### P1（严重）

| Issue | 描述 | 状态 |
|-------|------|------|
| [#24433](https://github.com/NousResearch/hermes-agent/issues/24433) | 交互式聊天模式报“未配置推理提供商”，尽管配置正确。影响 OpenAI Codex 用户。 | 待修复，社区提供详细复现步骤，P1 优先级 |
| [#40831](https://github.com/NousResearch/hermes-agent/issues/40831) | macOS 26 上 `hermes gateway start` 错误使用 `user/<uid>` 域，导致 Aqua 会话下无法正确加载。 | 待修复，P1 |
| [#40490](https://github.com/NousResearch/hermes-agent/issues/40490) | CLI 输入在懒加载依赖安装时死锁，终端完全无响应（`bare input()` 与 `prompt_toolkit` 冲突）。已关闭。 | ✅ **已关闭**（可能通过 PR 修复） |

### P2（中等）

| Issue | 描述 | 状态 |
|-------|------|------|
| [#27683](https://github.com/NousResearch/hermes-agent/issues/27683) | Web 工具因插件未初始化静默失败 | 待修复，影响 `v0.13.0` 新装用户 |
| [#40820](https://github.com/NousResearch/hermes-agent/issues/40820) | 安装器路径未引用空格导致失败 | ✅ 已有 PR #40923 |
| [#39281](https://github.com/NousResearch/hermes-agent/issues/39281) | Gemma4 + Ollama 输出截断 | 待修复 |
| [#34197](https://github.com/NousResearch/hermes-agent/issues/34197) | `/goal` 自动续跑可能因预压缩/会话分裂恢复过期任务状态，导致非预期继续工作 | 待修复，影响长时间运行的 goal 任务 |
| [#40250](https://github.com/NousResearch/hermes-agent/issues/40250) | 终端响应头部逃逸序列导致前 1-3 个字符被吞 | 待修复 |
| [#40801](https://github.com/NousResearch/hermes-agent/issues/40801) | Cron 脚本路径守卫误拒绝默认 profile 脚本目录中的任务 | ✅ 已有 PR #40918 |
| [#40913](https://github.com/NousResearch/hermes-agent/issues/40913) | Codex 提供商忽略 `model.base_url` 和 `HERMES_CODEX_BASE_URL` | ✅ 已有 PR #40924 |
| [#40915](https://github.com/NousResearch/hermes-agent/issues/40915) | `/kanban create` 当标题含弯引号时失败 | ✅ 已有 PR #40925 |

### P3（较低/桌面体验）

- [#37505](https://github.com/NousResearch/hermes-agent/issues/37505) macOS 仅 arm64 DMG（P3 但社区热度高）
- [#40101](https://github.com/NousResearch/hermes-agent/issues/40101) mnemosyne-hermes 插件注册失败（P3）
- [#40215](https://github.com/NousResearch/hermes-agent/issues/40215) 远程网关配置操作报 `ERR_INVALID_ARGUMENT`
- [#40843](https://github.com/NousResearch/hermes-agent/issues/40843) Camofox HTTP 客户端忽略 `browser.command_timeout`（硬编码30s）
- [#40937](https://github.com/NousResearch/hermes-agent/issues/40937) macOS Dock 图标尺寸异常
- [#22961](https://github.com/NousResearch/hermes-agent/issues/22961) Dashboard 中 `vision_analyze` 工具结果显示为用户消息（已关闭）
- [#38358](https://github.com/NousResearch/hermes-agent/issues/38358) `hermes update` 缺少 `--workspace web` 标志导致失败（已关闭）

---

## 6. 功能请求与路线图信号

| Issue/PR | 功能 | 优先级 | 与已有 PR 关联 |
|---------|------|--------|---------------|
| [#30577](https://github.com/NousResearch/hermes-agent/issues/30577) | 为网关 `/goal` 添加结构化元数据状态通知 | P3 | 暂无对应 PR，但社区强调对第三方集成有意义 |
| [#27777](https://github.com/NousResearch/hermes-agent/issues/27777) | 添加 Goal 生命周期插件钩子（`on_goal_set/pause/resume/complete`） | P3 | 已在今日 PR #37884 中体现了类似插槽思想 |
| [#40917](https://github.com/NousResearch/hermes-agent/issues/40917) | 看板（Kanban）支持 Board 级事件订阅，无需逐任务订阅 | P3 | 尚无 PR，但可配合未来多 agent 工作流 |
| [#13529](https://github.com/NousResearch/hermes-agent/issues/13529) | Agent 活动 API 与情绪状态暴露 | Feature | 长期未响应，但用户跨平台使用场景强烈 |
| [#40484](https://github.com/NousResearch/hermes-agent/issues/40484) | Desktop 文件树支持通过 Delete 键或右键删除文件 | P3 | 简单体验改进，尚未有 PR |
| [#40873](https://github.com/NousResearch/hermes-agent/issues/40873) | OpenAI 兼容语音 API 直通（audio passthrough） | P3 | 用户希望在 Ollama 本地模型中使用语音聊天 |
| [#40940](https://github.com/NousResearch/hermes-agent/issues/40940) | ScoutGate v2：将 `/goal` 权限绑定到生命周期租约/epoch/清单 | Feature | 高级安全/权限框架，路线图级别 |
| [#37884](https://github.com/NousResearch/hermes-agent/pull/37884) | 知识召回工具（knowledge_answer）新增 source-backed 推理 | P3 | ✅ 已有 PR，集成记忆、技能、Markdown 知识库 |
| [#40942](https://github.com/NousResearch/hermes-agent/pull/40942) | Desktop 添加“保持工具调用展开”开关 | P3 | ✅ 已有 PR，改善调试体验 |

**路线图信号**：短期可预见 `knowledge_answer` 工具与 AGIone 提供商将被合并；`/goal` 生命周期插件和 Board 级通知（#27777、#40917）正在积蓄社区呼声，可能进入下一版本讨论。

---

## 7. 用户反馈摘要

### 正面反馈（隐含）

- PR #40942 被用户期待：默认折叠工具调用在复杂任务中影响回顾，`Keep Tool Calls Expanded` 延续了社区对 UI 细节改进的诉求。
- PR #37884 知识召回工具为长期记忆整合提供新思路，获正面评价（虽无评论数量）。

### 痛点与不满

1. **macOS 架构歧视**：Intel Mac 用户（#37505）抱怨 DMG 只提供 arm64，无法在主力开发机上使用桌面应用，要求提供 universal binary。
2. **Web 工具开箱不可用**（#27683）：多位用户反馈新安装后搜索/爬取静默失败，排查困难，认为是插件初始化缺失导致的“活该被弃用”体验。
3. **路径空格问题**（#40820）：用户将 Home 放在外置硬盘，安装过程直接崩溃，认为是 macOS 和 Electron 常见坑却未被上游覆盖。
4. **Codex 提供商 `base_url` 不可配置**（#40913）：企业用户需要通过代理/负载均衡转发 Codex 流量，当前硬编码导致完全不可行，用户无法使用。
5. **CLI 死锁**（#40490）：懒加载提示框与 prompt_toolkit 冲突，终端完全无响应，重度 CLI 用户遇到即冻结，必须强制杀死进程。
6. **Kanban 弯引号**（#40915）：iOS 自动更正导致 `/kanban create` 失败，跨平台输入习惯未考虑。

### 使用场景亮点

- 用户 `theghostglitch`（#40873）将 Hermes 搭配本地 Gemma4 模型，希望能利用语音输入能力，体现了本地+多模态的用例。
- 用户 `cheong-yi`（#40940）提出 ScoutGate 安全框架，显示高级用户开始关注权限与审计，项目正从个人工具向平台级演化。

---

## 8. 待处理积压

以下 Issue / PR 长期未得到维护者响应或修复，可能影响用户留存：

| ID | 标题 | 创建日期 | 最后更新 | 优先级 | 备注 |
|----|------|---------|---------|--------|------|
| [#6718](https://github.com/NousResearch/hermes-agent/issues/6718) | Background Process Auto-Notifications Not Delivering | 2026-04-09 | 2026-06-07 | P2 (社区标记) | 无人认领，与 cron 通知同源 Bug |
| [#13529](https://github.com/NousResearch/hermes-agent/issues/13529) | Agent Activity API & Emotional State Exposure | 2026-04-21 | 2026-06-07 | Feature | 无人评论/指派，但有 1 👍 |
| [#24433](https://github.com/NousResearch/hermes-agent/issues/24433) | ‘No inference provider configured’ in interactive chat | 2026-05-12 | 2026-06-07 | P1 | 影响众多 new user onboarding，无 PR 关联 |
| [#27683](https://github.com/NousResearch/hermes-agent/issues/27683

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目日报 2026-06-07

## 1. 今日速览
项目在过去24小时内保持高度活跃：共更新12个Issue（新开/活跃10个，关闭2个），合并/关闭15个PR，并有1个夜间构建版本发布。大量由 `chengzhichao-xydt` 提交的修复PR集中解决了代码中的 goroutine 泄漏、类型断言安全问题和错误处理遗漏，显著提升了核心稳定性。同时，多位社区成员提交了关于 Google Chat 渠道、DeepSeek 协议支持以及 Slack 格式改进等重要功能PR，项目整体正向多平台集成和代码健壮性方向稳步推进。

## 2. 版本发布
- **nightly 构建** `v0.2.9-nightly.20260607.7d2b0c2a`
  - 这是一个自动化构建，可能不稳定，建议谨慎使用。
  - **完整变更日志**：[v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
  - 本次版本没有官方发布的破坏性变更说明，但包含大量防御性修复，建议用户在测试环境验证后再部署生产。

## 3. 项目进展
今日合并/关闭的15个PR中，以下关键合并推动了重要功能与稳定性改进：

### 功能增强
- **PR #3020** – `[Slack] 改进格式化和频道路由`
  - 增强了 Slack 工具反馈跟踪和消息格式，增加了频道级别 `allow/ignore` 过滤，并更新了相关测试和文档。
  - 链接：https://github.com/sipeed/picoclaw/pull/3020
- **PR #1112** – `[provider] 添加 DeepSeek-ai 协议支持（modelscope.cn）`
  - 修复了配置 `deepseek-ai/DeepSeek-V3.2` 模型时出现的协议未识别问题。
  - 链接：https://github.com/sipeed/picoclaw/pull/1112
- **PR #830** – `[channel] 添加 Google Chat 频道支持`
  - 为 PicoClaw 新增 Google Chat 渠道集成（功能开关）。
  - 链接：https://github.com/sipeed/picoclaw/pull/830
- **PR #423** – `[multi-agent] 基础多智能体协作框架与共享上下文`
  - 包含 Blackboard（线程安全共享上下文池）、agent handoff 和发现工具，构建于之前的 provider 重构和模型回退链之上。
  - 链接：https://github.com/sipeed/picoclaw/pull/423

### 稳定性与防御性修复（由 `chengzhichao-xydt` 系列提交）
- **PR #3014 / #3016** – 修复 `Manager.Reload()` 中的 goroutine 泄漏（取消旧 context）及 nil agent 守卫。
  - 链接：https://github.com/sipeed/picoclaw/pull/3014  
  - 链接：https://github.com/sipeed/picoclaw/pull/3016（仍为 OPEN 状态，但内容相似）
- **PR #3021** – 修复 `GetStartupInfo()` 在 nil agent 时的 panic。
- **PR #3022** – 为 `sync.Map.LoadAndDelete` 类型断言添加 `ok` 检查（涉及 Slack、Windows、飞书）。
- **PR #3023** – 修复 updater 解压函数中 `Close()` 错误被忽略的问题，避免静默文件损坏。
- **PR #3017** – 修复 base64 编码器在 `io.Copy` 失败时未关闭导致的缓冲区不完整。
- **PR #3018** – 为 LINE 频道、Evolution store 等添加类型断言 `ok` 检查和 `os.Getwd` 错误处理（OPEN 状态）。
- **PR #3019** – 修复 WhatsApp 频道中冗余类型断言、配置中敏感词过滤器 nil 守卫、SQLite `LastInsertId` 错误检查。
- **PR #2965** – 修复 `restrict_to_workspace` 启用时 `exec` 工具错误解析无 scheme 的 URL（如 `wttr.in/Beijing?T`）。

### 其他关闭
- **PR #2711** – 修复前端复制按钮在 HTTP 环境下的异常（已合入）。
- **PR #2838** – 支持 `AGENT.md` frontmatter 中的工具策略过滤器（`allow/deny` + glob 模式）。
- **PR #2662** – 统一 providers 文档中的 vendors 表格（文档改进）。
- **PR #3013** – 移除 skill-creator 中缺失的脚本引用，更新文档步骤。

> 综合来看，项目今天在**多智能体协作**、**新渠道（Google Chat）**、**DeepSeek 模型兼容**和**代码防御性加固**四个方面均有实质进展。

## 4. 社区热点
今日讨论最活跃的议题集中在已关闭的长期 Issue 上：

- **Issue #2625** – `[Feature] 提供带 WhatsApp 支持的编译版本`
  - 评论数：8 | 👍：1 | 状态：已关闭（2026-06-06）
  - 用户期望默认 arm64 构建包含 WhatsApp 支持，以便在 Raspberry Pi Zero 2 上快速更新。维护者在评论中讨论了编译标志的方案，最终通过调整默认构建参数满足需求。
  - 链接：https://github.com/sipeed/picoclaw/issues/2625

- **Issue #2929** – `[Task] 添加一等公民的智能体间通信`
  - 评论数：3 | 👍：2 | 状态：已关闭（2026-06-06）
  - 该任务提出在现有 `spawn`/`subagent`/`delegate` 基础上建立对等通信层。今日关闭可能因 PR #423 的协作框架已提供部分能力，但完整方案仍需后续迭代。
  - 链接：https://github.com/sipeed/picoclaw/issues/2929

- **新开 Issue 系列（#3024-#3032）**：由 `jcafeitosa` 在 2026-06-06 集中创建，涉及交易所模块（Binance 连接器、无锁 order book ring buffer、CLI 结构、CI/CD 等），尚未产生大量讨论，但密集的 task 编号暗示这是一个有计划的功能模块开发。

## 5. Bug 与稳定性
今日报告的 Bug 严重程度中等，均有对应的修复 PR 正在处理或已合入：

| 严重程度 | Issue/PR | 描述 | 当前状态 |
|----------|----------|------|----------|
| **高** | #3015 | Windows 平台下 QQ 频道连接失败（token 获取超时） | OPEN，尚无关联修复 PR |
| **中** | 多个 PR（#3014, #3016, #3021, #3022, #3023, #3017, #3019） | goroutine 泄漏、nil 指针 panic、类型断言未检查、Close 错误忽略等一系列防御性修复 | 大部分已合入，其中 #3016 和 #3018 仍为 OPEN |
| **低** | #2965 | 工作区卫士误将无 scheme URL 当作绝对路径 | 已合并（2026-06-06） |

**值得注意**：#3015 的 QQ 频道问题目前没有 PR 关联，是唯一一个未获修复的新报告 Bug。Windows 用户需注意该问题。

## 6. 功能请求与路线图信号
以下新需求可能被纳入下一版本：

- **交易所模块（EX 系列）**：用户 `jcafeitosa` 一口气创建了 `EX-001` 至 `EX-005`、`RG-001`、`EXM-001` 至 `EXM-003` 共 9 个任务 Issue，涉及 Binance 连接器（REST/WebSocket）、无锁 order book ring buffer、延迟基准测试、风险管理器接口、ClawHub 消息类型、CI/CD 流水线等。这些 Issue 引用了 `SDD-001`、`SDD-002`、`SDD-009` 等设计文档，表明项目正在有计划地构建**加密货币交易子系统**，可能是一个重要的路线图方向。
  - 代表链接：https://github.com/sipeed/picoclaw/issues/3024

- **WhatsApp 默认构建支持**（#2625）：已关闭，但社区呼声较高，预计后续版本会默认包含 WhatsApp 协议。
- **多智能体对等通信**（#2929）：PR #423 已提供基础框架，但#2929 关闭可能意味着完全实现仍需等待，路线图信号为“进行中”。

## 7. 用户反馈摘要
- **Raspberry Pi 用户**（#2625）：反馈默认 arm64 构建缺少 WhatsApp 支持，导致需要自行编译，增加了更新成本。社区对此表达了 1 个 👍，维护者最终采纳了将 WhatsApp 纳入默认编译的建议。
- **Windows 用户**（#3015）：报告 QQ 频道在 Windows 版本中完全不可用，错误信息为“获取 app access token 超时”，而 Pico 频道正常。该问题目前无维护者回复，可能影响部分 Windows 用户使用。
- **高级用户**（#2929）：提出了智能体间对等通信的需求，强调当前 `spawn/subagent/delegate` 模式无法满足协同工作流，期待更灵活的通信层。
- **Slack 用户**（PR #3020）：社区提交的 Slack 格式和频道路由改进得到了明确的正向反馈，提升了 Slack 渠道的实用性。

## 8. 待处理积压
以下 Issue/PR 长期未得到响应或合并，建议维护者关注：

| 类型 | 编号 | 标题 | 创建时间 | 最后更新 | 备注 |
|------|------|------|----------|----------|------|
| PR | #2935 | docs(i18n): add Traditional Chinese (zh-TW) locale and READMEs | 2026-05-24 | 2026-06-06 | 标注为 `stale`，增加中文社区文档的贡献，但未合入 |
| PR | #3016 | fix: cancel old dispatchTask on reload and guard nil ts.agent | 2026-06-06 | 2026-06-06 | 与已合入的 #3014 内容相同，可能重复提交，需要审核 |
| PR | #3018 | fix: add ok checks for type assertions and handle os.Getwd error | 2026-06-06 | 2026-06-06 | 与 #3022 等系列修复同属一批，但未合并，可能等待细粒度 review |
| Issue | #3015 | [BUG] QQ channel connection failure on Windows | 2026-06-06 | 2026-06-06 | 新报 Bug，尚无关联 PR，建议优先处理 |

**额外提醒**：虽然 #2625 和 #2929 已关闭，但涉及的需求（WhatsApp 默认支持、agent 对等通信）可能仍需后续跟进，以防关闭后遗留需求细节未完成。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，这是根据您提供的 NanoClaw 项目数据生成的 2026-06-07 项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-06-07

## 1. 今日速览

今日项目处于 **活跃的开发与修复状态**。虽然无新版本发布，但 Pull Request 活动异常频繁，共有 14 条更新，其中 11 条 PR 仍在等待合并，显示出团队在集中进行多项修复和功能改进。社区提交的 Bug 报告（Issues）数量不多，但揭示了两个关键的用户体验和配置问题，其中关于新手引导路径的 Bug 可能导致用户首次体验严重受阻。整体来看，项目代码变动活跃，但合并效率有待观察，社区提交的修复提案（PR）积压较多。

- **活跃度评估**：⭐⭐⭐☆☆ (中等偏上，开发活动密集，但合并与发布节奏放缓)
- **核心状态**：**修复导向的开发冲刺**，大量围绕 Bug 修复和技能库重构的 PR 已提交并等待审核。

## 2. 版本发布

无

## 3. 项目进展

今日有 3 个 PR 被成功关闭/合并，标志着关键的功能改进和长期维护工作取得进展：

- **技能库现代化改造**：`gavrielc` 的 PR **[#2698]** 已合并。这是一个重量级的重构工作，旨在让整个技能库变得 **“可升级维护”**。该项目确保每一个技能都遵循新的模型规范，包含测试、清理脚本（`REMOVE.md`），移除了未使用的验证文件（`VERIFY.md`）。这是项目保证向后兼容性和长期健康的重要一步。
- **首个标杆技能升级**：伴随上一条 PR，**[#2696]** 被合并。这个 PR 为 `add-dashboard` 技能提供了合规性修复，并附带了首个测试。在编写测试时，发现并修复了因核心代码重构导致的导入路径漂移(Build Drift)问题，证明了新技能模型的有效性。
- **防止消息重复发送**：`simonstudios` 的 PR **[#2697]** 被合并。该 PR 引入了主机的单实例锁机制，以解决因多个主机进程（如手动启动的 `pnpm run dev` 与系统服务）同时运行而导致的消息重复发送问题，提升了系统的稳定性。

## 4. 社区热点

今日 PR 讨论活跃度极高，主要集中在 Slack 适配器修复、技能库重构和多项长期存在的 Bug 修复上。

- **最热门 PR 系列：Slack 集成修复**：`mperraillon` 提交的 **[#2702]** 和 **[#2700]** 都旨在将 Slack 适配器从 HTTP Webhook 模式切换到 Socket Mode。
    - **背后的诉求**：Webhook 模式需要一个对公网可达的 URL，这对于大多数个人开发者或在本地环境测试的用户来说门槛极高，是导致他们无法正常使用 Slack 集成的首要问题。切换到 Socket Mode 可以彻底消除对公网服务器的依赖，大幅降低 Slack 集成的使用门槛。这是一个社区驱动的、直击用户痛点的改进。

- **关注度高的长期 PR**：由 `cfis` 提交的 **[#2531]** (修复中途发送消息导致的文本重复问题) 和 **[#2184]** (会话失效后立即重试) 在今天被更新。这表明这些长期存在的 Bug 修复正在被积极处理，社区和开发者都在关注这些影响日常使用体验的重要修复何时能被合并。

## 5. Bug 与稳定性

今日共报告 2 个新 Bug，并按严重程度排列如下。

- **[关键] 新手引导路径导致命令挂起**：**Issue #2703** 🚨
    - **问题**：按照推荐的安装流程配置后，`cli/local` 通道未正确连接，导致 `pnpm run chat hi` 命令会挂起 120 秒然后超时退出。整个过程中没有任何错误提示，对新手极不友好。
    - **分析**：这是一个严重的 **开箱即用体验问题**，如果用户按照官方推荐路径操作，会直接卡在最开始的步骤上，可能导致用户直接放弃。**尚无对应的 Fix PR**。

- **[中等] “rebuild”命令在无包配置时报错**：**Issue #2701**
    - **问题**：`ncl groups restart --rebuild` 命令在 `packages_apt` 和 `packages_npm` 都为空时失败，提示需要先安装包。用户期望的是，当没有需要安装的包时，`rebuild` 应该跳过包安装步骤。
    - **分析**：这是一个逻辑不完善的回归，导致一个本应正常执行的命令报错。**尚无对应的 Fix PR**。

- **[中等-来自PR] 多个来自 PR 的 Bug 修复**：
    - **信号(Signal)适配器问题**：PR **[#2694]** 修复了来自 Signal 的私信被静默丢弃的问题（缺少 `isMention`/`isGroup` 标记）；PR **[#2695]** 修复了 Signal 图片附件无法被容器内代理读取的问题（路径不正确）。
    - **重复消息问题**：PR **[#2697]** 解决了主机并发导致的重复消息问题（已合并）。
    - **CRUD ID生成**：PR **[#2699]** 修复了 `ncl groups create` 生成的 ID 必须以字母开头的问题，以符合 OneCLI 的格式要求。

## 6. 功能请求与路线图信号

今日无新功能请求 Issue。但从更新和修复的 PR 中可以推测未来的路线图方向：

- **短期（预计下一版本）**：**Slack Socket Mode 支持**（PR #2700, #2702）和 **新手流程体验优化**（需要 Issue #2703 对应的修复）将是下一个版本的核心关注点。所有悬而未决的信号(Signal)适配器修复（PR #2694, #2695）也有很高的优先级。
- **中期**：**MCP (Model Context Protocol) 服务器 HTTP/SSE 传输支持**（PR #2208） 和 **容器运行时的 Podman 兼容性**（PR #2230） 表明项目正在向更广泛的生态和运行环境靠拢。添加新的 Google Contacts 工具（PR #2693）则表明持续扩大实用技能插件的路线图。

## 7. 用户反馈摘要

今日 Issue 评论数为 0，因此无法从评论中提取用户反馈。但可以从 Bug 报告中推断用户痛点：

- **新手用户**：在尝试快速上手时，极可能被 **Issue #2703** 阻塞，这将导致失败的首次体验，对项目口碑有负面影响。
- **高级用户/运维者**：在使用 `rebuild` 命令时，遇到不合理的报错（Issue #2701），破坏了操作的流畅性。他们可能正在依赖 `groups` 功能进行复杂的部署。
- **信号(Signal)用户**：从 PR #2694 的提交记录看，该用户（cfis）发现通过 Signal 收到的私信和图片附件根本无法工作，这是该渠道的致命问题，导致该集成对其完全不可用。

## 8. 待处理积压

以下为需要维护者关注的重要长期未响应 Issue 或 PR：

- **[高] 长期未合并的 PR：容器运行和 MCP 功能增强（重要架构变更）**
    - **PR #2208** `[feat(mcp): support http and sse MCP server transports]`：已开放 35 天，触及到扩展 AI 代理能力范围的核心功能。
    - **PR #2230** `[fix(container-runner): map host user via keep-id on rootless podman]`：已开放 35 天，解决了 Podman 用户在无根模式下运行时的权限问题。
    - **PR #2349** `[fix(mount-security): tolerate allowlist entries missing path field]`：涉及安全性，避免因配置错误导致整个功能崩溃。

这些 PR 均已开放超过一个月，且都标记为“遵循指南(follows-guidelines)”，表明其质量已被初步认可。它们的长时间积压可能会阻碍其他依赖它们的开发工作，并传递出社区贡献可能未被及时处理的信号。

---
*数据更新时间：2026-06-07*
*项目链接：[github.com/qwibitai/nanoclaw]*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是根据您提供的 IronClaw 项目数据生成的 2026-06-07 项目动态日报。

---

### **IronClaw 项目日报 - 2026年06月07日**

#### **1. 今日速览**

IronClaw 项目今日维持高强度开发模式。核心贡献者正围绕“Reborn”重构计划进行大规模功能推进，主要集中在 **Slack 通道管理**、**OpenAI 兼容API路由**、**用户偏好体系**以及**WebUI 会话能力**等关键模块的建设上。今日 PR 活动极为活跃，共 31 条，其中 10 条已被合并，显示出敏捷的迭代节奏。同时，项目也存在较为严重的 E2E 测试不稳定问题（Issue #4108），社区中来自新贡献者和自动化 bot 的 PR 也在持续增加。整体来看，项目处于架构升级的关键冲刺期，活跃度非常高，但稳定性监控仍需加强。

#### **2. 版本发布**

无新版本发布。

> *注意：存在一个长期待合并的版本发布 PR（#3708），其中包含了 `ironclaw_common` 和 `ironclaw_skills` 的破坏性变更，积压已超过三周，可能成为下一个版本的发布基础。*

#### **3. 项目进展**

今日有 10 个 PR 被合并，标志着项目在多个功能线上取得实质性进展：

- **CI 与基础设施优化**：PR #4520 已合并，优化了 CI 流水线，确保仅与“Reborn”相关的 PR 不会触发大量遗留系统的测试，从而加快了核心开发迭代速度。这直接响应了项目当前以 Reborn 为重心的战略。
- **功能迭代与设计共识**：
    - **重复调用处理改进**：PR #4508 已合并，将原本直接停止的重复能力调用，改为一个两阶段的警告门控机制，提升了模型的鲁棒性和用户体验。
    - **Slack 通道集成**：PR #4509 已合并，实现了基于 Slack 通道的主体路由功能，为后续的 Slack 集成能力奠定了基础。这与此前已关闭的 Notion MCP 能力路径（Issue #3805）共同完善了 Reborn 的渠道策略。
    - **设计文档定稿**：PR #4486 和 #4485 (重复提交) 已合并，正式纳入了“子代理 + 上下文压缩”的统一设计方案，这是一个关键的架构决策文档，明确了 `PostCapabilityStage` 等核心概念。
- **代码质量与修复**：PR #4523 (open) 和 #4520 (merged) 分别处理了 host API 的序列化问题和 CI 配置，体现了对代码质量和基础设施稳定性的持续投入。

#### **4. 社区热点**

今日社区焦点集中在围绕 **“Reborn”项目**的一系列大型功能 PR 上，这些 PR 由核心团队成员密集提交和更新，反映出项目已进入深度开发周期。

- **最受关注的功能系列**：
    - **[PR #4519] Add WebUI session capabilities endpoint**: 新增 WebUI 会话能力接口，允许服务端宣告 `isAdmin` 等权限。这是向“声明式前端”架构转变的关键一步。
    - **[PR #4522] feat(llm): scaffold tool_args.rs shared parsing primitives**: 作为 RC3/M9 阶段的一部分，此 PR 铺平了 LLM 共享工具参数解析能力，为即将到来的“标准化提供商”装饰器打下基础。这暗示了 LLM 工具调用将迎来一次重要的统一化升级。
    - **[PR #4511] [codex] Add outbound preference facade contracts**: 新增外部投递偏好外观合约，这通常涉及多渠道（如邮件、Slack）的输出管理，是用户个性化体验的重要一环。

**社区诉求分析**：这些活跃的 PR 表明，核心贡献者们正在系统性地构建 Reborn 的“会话层”和“用户偏好层”，用户的潜在需求（如更自由的 LLM 调用、自定义投递渠道）正在被快速转化为代码实现。

#### **5. Bug 与稳定性**

- **严重**：
    - **[Issue #4108] Nightly E2E failed**: 这是一个持续存在的自动报告问题，最新的 E2E 测试套件（特别是 `extensions` 部分）再次失败。目前还没有关联的修复 PR。该问题自 5 月 27 日首次报告以来已持续多日，是需要开发团队优先关注的稳定性风险。
      [链接](https://github.com/nearai/ironclaw/actions/runs/27052471094)

- **中低危**：
    - **[PR #4523] fix(host_api): round-trip system sentinel through string_id Deserialize**: 定位并修复了一个序列化/反序列化不对称问题，该问题会导致系统哨兵值 (`\x1fSYSTEM\x1f`) 被拒绝，进而引发 `service_unavailable` 错误。
      [链接](https://github.com/nearai/ironclaw/pull/4523)

#### **6. 功能请求与路线图信号**

今日没有新增的 Feature Request Issue。但大量的开发 PR 揭示了未来版本的方向：

- **OpenAI API 兼容性**：PR #4489 和 #4495 在推进 `chatcmpl-*` 和 `resp_*` 等兼容引用，以及将聊天补全路由到 `ProductWorkflow` 后端。这表明 IronClaw 正在努力成为一个兼容 OpenAI API 的多模型代理平台，这是一个重要的路线图信号。
- **多渠道扩展 (Slack)**：PR #4510 和 #4509 共同推进了 Slack 渠道的路由、配置和管理后端。结合已关闭的 Notion MCP 集成（Issue #3805），可以预见下一版本将显著增强对第三方 MCP 工具和社交渠道的支持。
- **本地开发体验**：PR #4517 为 Reborn 运行时添加了首次启动时自动生成配置文件的功能，这是为了改善开发者的本地部署和上手体验。

**路线图信号分析**：这些 PR 指向了 IronClaw 正从单纯的 agent 框架，向一个具备“原生 AI 产品工作流管理”能力的平台演进。下一版本的看点在于 OpenAI API 兼容性的成熟度和多渠道（Notion、Slack）的集成深度。

#### **7. 用户反馈摘要**

今日的 Issues 和 PR 评论中没有来自终端用户的直接反馈。然而，从 PR 的内容可以间接看出开发团队关注的一些用户痛点：

- **开发体验**：PR #4517（自动生成配置）和 PR #4521（JSON 清洁器，来自新贡献者）表明，开发者在配置和环境搭建上可能遇到障碍。
- **稳定性与错误处理**：PR #4523 修复的 `service_unavailable` 错误，以及 PR #4508 重构的重复调用停止逻辑，都直接回应了用户在使用中可能遇到的“不可用”和“卡死”等负面体验。

#### **8. 待处理积压**

以下为值得维护者关注的、长时间未响应的关键 Issue 和 PR：

- **功能冻结与版本发布**：
    - **[PR #3708] chore: release**: 一个已开放超过 3 周的版本发布 PR，包含 `ironclaw_common` 和 `ironclaw_skills` 的 API 破坏性变更。此 PR 的积压可能阻碍了社区用户使用新特性。建议开发团队评估是否可合并并发布。
      [链接](https://github.com/nearai/ironclaw/pull/3708)

- **严重 Bug**：
    - **[Issue #4108] Nightly E2E failed**: 持续的自动化测试失败问题。由于是自动化报告，可能被忽略，但其持续的 failure 状态会降低 CI 系统的可信度。建议分配专人排查根因。
      [链接](https://github.com/nearai/ironclaw/issues/4108)

- **新贡献者的 PR**：
    - **[PR #4521] Add JSON cleaner**: 一位新贡献者提交的 PR。虽然风险等级为中等，但对于初次贡献者来说，应当得到及时的代码审查和指导，以鼓励社区参与。
      [链接](https://github.com/nearai/ironclaw/pull/4521)

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 – 2026-06-07

---

## 1. 今日速览

过去24小时内，项目共收到 **6 条 Issue 更新**（均为活跃态，无新关闭），**2 条 PR 完成合并**，无新版本发布。社区活跃度中等，主要集中于**用户反馈的稳定性问题（任务中断、无返回）** 及**UI 操作体验（未保存确认丢失）**，同时两项功能增强 PR 已成功合并。整体呈**维护与小幅迭代并行** 的健康态势。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 2 个 PR 均为功能改进，分别增强了批量操作与多 Agent 调度能力：

| PR | 标题 | 状态 | 摘要 |
|----|------|------|------|
| [#1529](https://github.com/netease-youdao/LobsterAI/pull/1529) | `feat(cowork): 批量模式新增导出功能，支持将选中会话导出为JSON文件` | ✅ 已合并 | 在批量模式下增加「导出」按钮，用户可将选中的多个会话导出为结构化 JSON 文件，保存位置可自选，默认文件名含时间戳。 |
| [#1530](https://github.com/netease-youdao/LobsterAI/pull/1530) | `feat(scheduledTask): 多Agent状态下支持新建任务选择归属 Agent` | ✅ 已合并 | 当启用 Agent 数 >1 时，新建定时任务时可下拉选择归属 Agent（默认 main），解决任务归属混乱的问题。 |

这两个 PR 分别提升了**数据处理能力** 和**多 Agent 管理的一致性**，项目在交互完善和功能深度上各迈进了一步。

---

## 4. 社区热点

今日讨论热度最高的 Issue 是 **#2120「建议」**（[链接](https://github.com/netease-youdao/LobsterAI/issues/2120)），由用户 `nbjoe` 于今日新开，包含三条具体建议，目前已获 1 条评论。其诉求直指**连续工作流与 UI 自适应性**，反映了真实开发场景下的痛点：

1. **任务预输入**：借鉴 Workbuddy，在任务运行时允许预输入下一个任务，提升连续性。
2. **延长单次任务时长**：运行数据采集脚本时出现 `terminated` 提示，影响开发。
3. **UI 列数自适应**：2560×1600 全屏下双列展示不好看，建议改为三列。

此外，旧 Issue **#1496**（任务显示完成但无返回）和 **#1495**（无故中断进程）各自仍有评论，表明用户对稳定性高度关注。

---

## 5. Bug 与稳定性

当日无新 Bug 报告，但多个**长期未修复的 Bug** 今日被重新关注（更新日期为 2026-06-06）。按严重程度排列如下：

| Issue | 标题 | 严重性 | 当前状态 | 是否有 fix PR |
|-------|------|--------|----------|---------------|
| [#1495](https://github.com/netease-youdao/LobsterAI/issues/1495) | 无缘无故中断进程 | ⚠️ 严重 – 影响核心运行 | OPEN（stale）| ❌ 无 |
| [#1496](https://github.com/netease-youdao/LobsterAI/issues/1496) | 任务显示完成，但是没有返回 | ⚠️ 严重 – 数据不一致 | OPEN（stale）| ❌ 无 |
| [#1468](https://github.com/netease-youdao/LobsterAI/issues/1468) | 创建Agent弹窗关闭时无未保存确认 | ⚠️ 中 – 数据静默丢失 | OPEN（stale）| ❌ 无 |
| [#1469](https://github.com/netease-youdao/LobsterAI/issues/1469) | Agent设置面板关闭时无未保存确认 | ⚠️ 中 – 配置静默丢失 | OPEN（stale）| ❌ 无 |
| [#1470](https://github.com/netease-youdao/LobsterAI/issues/1470) | MCP服务器配置弹窗关闭时无未保存确认 | ⚠️ 中 – 环境变量静默丢失 | OPEN（stale）| ❌ 无 |

这些 Bug 均已存在超过 2 个月（创建于 4 月初），虽今日被更新（可能为机器人标记或用户再次评论），但依然没有对应的修复 PR。建议项目组优先关注**进程中断**与**数据丢失**问题。

---

## 6. 功能请求与路线图信号

除了**#2120** 中的三条建议外，今日无新增其他功能请求。结合已合并的 PR 进行分析：

- **多 Agent 选择器**（PR #1530）已落地，表明团队正在完善 Agent 维度的管理，未来可能扩展至更多场景（如多 Agent 对话分派）。
- **批量导出**（PR #1529）回应了用户对数据持久化与备份的需求，#2120 中的“预输入任务”可视为**任务队列**功能的雏形，若被采纳，可能纳入下一版本。

路线图信号：**用户体验（未保存确认）** 和 **稳定性（进程中断）** 是目前最大缺口，属于高优先级待解决问题。

---

## 7. 用户反馈摘要

- **#2120**（用户 `nbjoe`）：强调任务连续性和 UI 适配，表示当前单次任务时长限制“有点影响开发”，建议延长并引入队列机制。
- **#1495**（用户 `xuzhiwu123`）：上传截图显示 `terminated` 提示，困惑是客户端还是大模型问题，希望明确原因并修复。
- **#1468/#1469/#1470**（用户 `MaoQianTu`）：详细描述了 Agent 创建、设置面板、MCP 配置三个场景中未保存数据静默丢失的 bug，虽未提供额外评论，但重复出现表明该问题对用户操作打断严重。

整体来看，用户对 **“运行稳定性”** 和 **“操作安全（防丢失）”** 的满意度较低，而对功能扩展类贡献（如导出、多 Agent 归属）持积极态度。

---

## 8. 待处理积压

以下为长期未响应或未分配的重要 Issue / PR，建议维护者关注：

| 类型 | 编号 | 标题 | 创建时间 | 最后更新 | 备注 |
|------|------|------|----------|----------|------|
| Issue | [#1496](https://github.com/netease-youdao/LobsterAI/issues/1496) | 任务显示完成，但是没有返回 | 2026-04-07 | 2026-06-06 | 严重 Bug，无任何标签或 Assignee |
| Issue | [#1495](https://github.com/netease-youdao/LobsterAI/issues/1495) | 无缘无故中断进程 | 2026-04-07 | 2026-06-06 | 严重 Bug，获 👍1 |
| Issue | [#1468](https://github.com/netease-youdao/LobsterAI/issues/1468) | 创建Agent弹窗关闭时无未保存确认 | 2026-04-04 | 2026-06-06 | 数据丢失，同类 3 个 issue |
| Issue | [#2120](https://github.com/netease-youdao/LobsterAI/issues/2120) | 建议（任务预输入、时长、UI 列数） | 2026-06-06 | 2026-06-06 | 新开，期待团队反馈 |

这些 issue 累计超过 2 个月未解决，可能影响用户体验与口碑。建议项目团队分配资源，优先评估严重 Bug 的修复方案，并回应 #2120 中的可行性。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 (2026-06-07)

**项目仓库**: [github.com/moltis-org/moltis](https://github.com/moltis-org/moltis)

---

## 1. 今日速览

过去 24 小时，Moltis 项目共新增 3 个 Issue（2 个 Bug、1 个功能请求），无新 Pull Request 或版本发布。社区活跃度处于 **低水平**，但 Bug 报告集中在核心功能（认证禁用、Cron 归档）上，表明用户正在积极使用最新版本并发现关键问题。项目团队尚未对这些问题进行回复或指派，建议尽快确认。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

过去 24 小时无任何 Pull Request 合并或关闭，项目代码库未向前推进。当前未发现待处理 PR，开发节奏暂缓。

---

## 4. 社区热点

今日唯一拥有评论的 Issue 为：

- **[#1112] [Bug]: Disabling auth doesn't seem to disable auth (Docker)**  
  [链接](https://github.com/moltis-org/moltis/issues/1112)  
  作者: methompson | 评论: 1 | 👍: 0  
  **诉求分析**：用户报告在 Docker 部署环境下，即使配置中关闭了身份认证功能，系统仍然要求认证。该问题直接关系到生产环境的可用性，且与安全配置相关，优先度较高。社区暂无其他讨论，该 Issue 的潜在影响面较大。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 摘要 | 是否有修复 PR |
|----------|-------|------|---------------|
| 🔴 高 | [#1112](https://github.com/moltis-org/moltis/issues/1112) | Docker 环境下禁用认证后认证仍生效 | 无 |
| 🟡 中 | [#1111](https://github.com/moltis-org/moltis/issues/1111) | 归档 Cron 会话后界面无可见效果（可能是前端缓存或后端逻辑缺失） | 无 |

两个 Bug 均发生在最新版本中，且均未提供复现步骤之外的详细信息。建议维护者对 #1112 优先排查认证中间件配置加载逻辑，对 #1111 检查归档后的状态更新与 UI 刷新机制。

---

## 6. 功能请求与路线图信号

- **[#1110] [Feature]: A keyword to suppress cron job notifications, like NO_REPLY**  
  [链接](https://github.com/moltis-org/moltis/issues/1110)  
  作者: IlyaBizyaev | 👍: 0  
  **需求描述**：用户希望引入一个特殊关键字（例如 `NO_REPLY`），在 Cron 作业的输出中包含该关键字时，系统将静默处理并抑制通知推送。  
  **路线图信号**：该功能与已有的 Cron 会话管理、通知系统紧密相关，属于体验优化。当前无对应 PR 或开发分支，但鉴于用户明确提出了具体实现方案（如类似邮件系统的 `NO_REPLY` 关键词），可能会被纳入下一小版本的增强项。

---

## 7. 用户反馈摘要

从今日仅有的 3 个 Issue 正文及评论中，可提炼以下用户反馈：

- **痛点**：Docker 部署场景下，用户期望通过配置文件彻底关闭认证以简化内部测试或单机使用，但发现配置失效。说明文档或配置校验环节可能存在缺陷。
- **使用场景**：Cron 会话的归档操作用户期望产生视觉反馈（如列表隐藏、状态标记等），当前无响应说明前端交互体验缺失。
- **满意点**：暂无正向反馈。用户均表示已确认使用最新版本，表明用户对项目保持关注且愿意报告问题。

---

## 8. 待处理积压

过去 24 小时内无长时间未响应的 Issue 或 PR。当前项目中所有 3 个 Issue 均创建于 2026-06-06，尚未收到维护者回复。建议保持关注，特别是以下两项：

- [#1112](https://github.com/moltis-org/moltis/issues/1112) —— 认证 bug，可能需要紧急修复
- [#1111](https://github.com/moltis-org/moltis/issues/1111) —— UI 交互 bug，影响用户体验

未发现超过 48 小时无人回应的积压项。

---

**总结**：项目今日进展缓慢，但 Bug 报告质量较高，建议维护者在下个工作周期内优先处理 Docker 认证 Bug 和 Cron 归档无反馈问题。功能请求 #1110 为明确的增强方向，可纳入后续讨论。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-06-07

> 数据来源：GitHub (agentscope-ai/QwenPaw)  
> 数据时段：2026-06-06 ~ 2026-06-07  

---

## 1. 今日速览

过去 24 小时内，项目共收到 11 条 Issue 更新，其中新开/活跃 9 条、已关闭 2 条；Pull Request 和版本发布均为 0。社区活跃度中等，但 bug 报告集中爆发，特别是 v1.1.10 版本出现多起回归性问题（本地模型无响应、Coding Mode 会话切换失败、Windows 路径溢出等），反映出近期发版质量需加强。功能请求方面，用户对 UI 交互体验（会话切换、实时反馈）和渠道扩展（MAX Messenger）有明确需求。

## 2. 版本发布

**无**（过去 24 小时内无新 Releases）

---

## 3. 项目进展

**Pull Request 合并/关闭情况：无**  
今日未合并或关闭任何 PR，项目整体无明显代码层面的推进。仅有的两个关闭 Issue 均为用户自解（#4984 用户确认已有审批命令；#4661 为历史 bug 标记关闭）。

---

## 4. 社区热点

### 🔥 讨论最活跃的 Issue

1. **[#4661] [CLOSED] [Bug]: v1.1.8post1 模型上下文长度配置，记忆压缩未生效**  
   - 评论数：6  
   - 链接：[#4661](https://github.com/agentscope-ai/QwenPaw/issues/4661)  
   - 分析：虽然已关闭，但讨论持续至更新日。用户反馈升级后上下文压缩阈值从 200K 变为 131K，且全局配置选项消失，单个模型配置不生效。反映配置系统在版本演进中可能存在兼容性问题。

2. **[#4937] [OPEN] [Bug]: /compact command ignores model's max_input_length, still uses 128K default**  
   - 评论数：5  
   - 链接：[#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937)  
   - 分析：用户添加 MiniMax M3 模型（max_input_length=512K）后，`/compact` 命令仍使用 128K 默认值，与 #4661 同属上下文压缩失效问题，且影响范围延伸至 v1.1.10。社区对配置优先级和自动推导逻辑存在普遍困惑。

3. **[#4989] [OPEN] [Bug]: 1.1.9 & 1.1.10 版本，使用本地部署的千问3.6-27B模型，对话页面提交问题后，无响应**  
   - 评论数：1（但问题严重性高）  
   - 链接：[#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989)  
   - 分析：用户通过 vLLM 部署的标准 OpenAI 兼容模型在 1.1.9/1.1.10 中完全无响应（仅旋转加载），而 1.1.5.post2 工作正常。提示后端请求处理流程可能发生回归。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 简述 | 是否有 fix PR |
|----------|-------|------|---------------|
| 🔴 严重 | [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) | 本地部署千问模型在 v1.1.9/1.1.10 无响应，回归问题 | 无 |
| 🔴 严重 | [#4988](https://github.com/agentscope-ai/QwenPaw/issues/4988) | Session 文件名中 Session ID 重复拼接，导致 Windows 路径超限 | 无 |
| 🟠 高 | [#4987](https://github.com/agentscope-ai/QwenPaw/issues/4987) | v1.1.10 Coding Mode 下会话切换始终失败，回归 | 无 |
| 🟠 高 | [#4990](https://github.com/agentscope-ai/QwenPaw/issues/4990) | 企业微信返回信息中调用工具后，关闭时返回“抱歉，无法回答” | 无 |
| 🟠 高 | [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937) | `/compact` 命令忽略模型 max_input_length，始终使用 128K 默认值 | 无 |
| 🟡 中 | [#4661](https://github.com/agentscope-ai/QwenPaw/issues/4661) | v1.1.8post1 上下文压缩未按配置生效（已关闭，但根源未修复？） | 无 |
| 🟢 低 | [#4985](https://github.com/agentscope-ai/QwenPaw/issues/4985) | 删除命令显示不换行，需拖动滑块查看 | 无 |

**总结**：v1.1.10 版本出现至少 3 个回归性 bug（模型无响应、Coding Mode 会话切换、路径溢出），且均无对应 PR 修复，严重影响用户体验，建议开发团队优先排查。

---

## 6. 功能请求与路线图信号

### 新增功能需求

1. **[#4971] [Feature]: 会话管理太麻烦，建议增加会话栏方便切换**  
   - 链接：[#4971](https://github.com/agentscope-ai/QwenPaw/issues/4971)  
   - 核心诉求：当前需点两次才能切换会话，希望有直接侧边栏一键切换。属于基础 UX 改进，开发成本低，预计可能纳入下一小版本。

2. **[#4886] [Feature]: 添加 MAX Messenger 作为 QwenPaw 频道**  
   - 链接：[#4886](https://github.com/agentscope-ai/QwenPaw/issues/4886)  
   - 核心诉求：面向俄语用户的主流通讯平台，与 “Every channel” 理念契合。若社区有贡献者，可能以社区 PR 形式实现。

3. **[#4986] [Feature]: shell 执行或写文件时需实时交互信息显示**  
   - 链接：[#4986](https://github.com/agentscope-ai/QwenPaw/issues/4986)  
   - 核心诉求：参考 cursor/workbuddy，避免用户误以为卡顿。直接关系到 Coding Mode 的可用性，可能优先解决。

### 路线图信号

- 多个请求涉及 **配置系统透明度**（模型 max_input_length 与 /compact 行为不一致），表明当前配置 UI 与运行时逻辑存在脱节。
- **Coding Mode 稳定性** 成为 v1.1.10 后的关键痛点，开发团队应在下个版本重点修复。

---

## 7. 用户反馈摘要

- **配置困惑**：用户 @Timqt 在 [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937) 中详细描述了按文档配置后 `/compact` 仍无效的步骤，并附截图，表达 frustration。类似反馈在 [#4661](https://github.com/agentscope-ai/QwenPaw/issues/4661) 中也有体现。
- **回归抱怨**：用户 @Cancerhzc 在 [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) 中明确指出“1.1.5.post2 可以正常问答，升级后就不行了”，强调了降级意愿。
- **交互期待**：用户 @rescodexx 在 [#4986](https://github.com/agentscope-ai/QwenPaw/issues/4986) 中直接参考竞品，希望 QwenPaw 在 Coding Mode 中提供实时代理反馈，否则“以为卡住了”。
- **社区互助**：用户 @Sclifftop 在 [#4984](https://github.com/agentscope-ai/QwenPaw/issues/4984) 中主动承认自己未读文档，关闭 Issue，体现了积极的社区氛围。

---

## 8. 待处理积压

| Issue | 创建时间 | 最后更新 | 标签 | 说明 |
|-------|----------|----------|------|------|
| [#4661](https://github.com/agentscope-ai/QwenPaw/issues/4661) | 2026-05-25 | 2026-06-06 | bug / closed | 虽已关闭，但 #4937 表明同样问题在 v1.1.10 中未彻底解决，需回溯验证。 |
| [#4886](https://github.com/agentscope-ai/QwenPaw/issues/4886) | 2026-06-02 | 2026-06-06 | enhancement | 未获官方回复，已有 5 天。若社区有意愿可进入候选，建议维护者至少标记 `welcome contribution`。 |
| [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937) | 2026-06-03 | 2026-06-06 | bug | 等待开发者诊断，建议 patch 优先修复 `compact_threshold_ratio` 自动推导逻辑。 |

**提醒**：上述 bug 中 #4937、#4987、#4988、#4989 均涉及 v1.1.10 核心功能，且无 patch 或临时修复方案，建议维护者在下一个 hotfix 版本（如 v1.1.11）中集中处理，并加快发布节奏。

---

*以上日报基于公开 GitHub 数据自动生成，仅供项目管理参考。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

好的，以下是基于您提供的 ZeptoClaw 项目 GitHub 数据生成的 2026-06-07 项目动态日报。

---

# ZeptoClaw 项目动态日报 | 2026-06-07

## 1. 今日速览

今日项目开发活动集中在持续集成（CI）流程优化与性能基准控制上。核心聚焦于将二进制文件大小检查正式化为PR的硬性门禁，以遏制项目体积增长。过去24小时内，有一项关于此议题的PR(#611)进入待合并状态，同时一个相关的旧Issue(#612)已关闭，并开启了一个新的Issue(#629)来细化门禁策略。整体活跃度中等，但技术方向非常聚焦。

## 2. 版本发布

无。

## 3. 项目进展

今日无PR被合并，但核心进展体现在一个即将合并的关键PR上：

- **PR #611: 提升二进制大小检查为PR门禁 (7.5MB上限)** 
  此PR将项目已有的`binary-size`检查功能从仅限主分支运行的“事后分析”提升为每个PR都必须通过的门禁。当前设置的门禁上限为7.5MB。该PR已进入待合并状态，标志着项目在软件供应链安全和资源消耗控制上迈出了制度性的一步。

## 4. 社区热点

今日社区讨论的核心议题围绕着项目二进制文件大小的严格控制展开。两条相关的Issue和一条PR形成了清晰的讨论脉络：

- **Issue #612 (已关闭) & Issue #629 (新开)**: 这两个Issue共同代表了社区和核心开发者对“项目体积过胖”的担忧。
  - **#612** 指出当前PR #611设置7.5MB的门禁上限是一个“妥协方案”，因为当前版本（6.98MB）离7MB的战略目标仅差21KB。该Issue要求审计导致二进制大小从6.2MB低水位线膨胀了~800KB的原因，并将门禁收紧至7MB。讨论反映了对代码膨胀的零容忍态度。
  - **#629** 则进一步明确了战略目标：“6MB上得机器人”的护城河实际上是**aarch64**架构（树莓派/Jetson/Apple Silicon），而非x86_64。该Issue要求为aarch64架构单独设立7MB的门禁，以确保在边缘设备上的部署效率。

**核心诉求**：社区和开发者强烈希望将项目体积控制在极小的范围内，特别是针对嵌入式/边缘计算场景（aarch64），任何体积的增长都需要严格审查和遏制。

**链接**:
- Issue #612: [https://github.com/qhkm/zeptoclaw/issues/612](https://github.com/qhkm/zeptoclaw/issues/612)
- Issue #629: [https://github.com/qhkm/zeptoclaw/issues/629](https://github.com/qhkm/zeptoclaw/issues/629)
- PR #611: [https://github.com/qhkm/zeptoclaw/pull/611](https://github.com/qhkm/zeptoclaw/pull/611)

## 5. Bug 与稳定性

今日未报告新的严重Bug或崩溃问题。稳定性相关讨论主要围绕性能基准控制：

- **性能基准漂移 (Issue #612，已关闭)**：虽然此Issue已关闭，但它揭示了项目存在约800KB的二进制大小漂移问题。该问题已被识别，并通过即将合并的PR #611（设置7.5MB软上限）和后续的Issue #629（设置7MB硬上限）来处理，本质上是一个通过强化CI门禁来防止进一步恶化的“治理”行为。

## 6. 功能请求与路线图信号

- **aarch64架构二进制大小门禁 (Issue #629)**: 这是一个明确的功能请求，要求CI在aarch64架构上也实施二进制大小限制。它强烈暗示了项目将**树莓派、Jetson等ARM设备作为关键部署目标**。鉴于这是一个P2高优先级且存在已提交的PR，它极有可能被纳入下一版本。

## 7. 用户反馈摘要

从今日的Issue评论中可以提炼出关键的用户/维护者反馈：

- **痛点**: 项目二进制文件大小在持续增长，已经从历史低点6.2MB膨胀到6.98MB，逼近7MB的心理和战略红线。这对在资源受限的机器人或边缘设备上部署是主要痛点。
- **使用场景**: 用户（尤其是维护者）明确将“能在aarch64机器人上运行”（Pi/Jetson）作为核心使用场景和“战略护城河”。
- **满意度**: 对当前的体积增长趋势不满意，表现为要求立即收紧门禁（从7.5MB降至7MB）并对历史漂移进行审计。
- **建议**: 建议对不同架构设置不同的、更严格的体积限制，而非使用“宽松的”统一标准。

## 8. 待处理积压

- **PR #611: 提升二进制大小检查为PR门禁 (7.5MB)**
  - **状态**: 已进入待合并状态。
  - **建议**: 该PR是解决#612和#629所述问题的关键一步。建议维护者尽快合并，以便团队能在此基础上迭代，朝着7MB甚至6MB的目标进发。
  - **链接**: [https://github.com/qhkm/zeptoclaw/pull/611](https://github.com/qhkm/zeptoclaw/pull/611)

- **Issue #629: 为aarch64添加二进制大小门禁 (7MB)**
  - **状态**: 新开，尚无关联PR。
  - **建议**: 这是PR #611合并后的下一个逻辑步骤，将7MB门禁从x86_64迁移或扩展至aarch64。建议在PR #611合并后，尽快将其纳入开发路线图。
  - **链接**: [https://github.com/qhkm/zeptoclaw/issues/629](https://github.com/qhkm/zeptoclaw/issues/629)

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，以下是基于您提供的 GitHub 数据生成的 ZeroClaw 项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-06-07

**项目分析师**: AI 智能体与个人 AI 助手领域开源项目分析师
**数据来源**: ZeroClaw (github.com/zeroclaw-labs/zeroclaw)
**统计周期**: 2026-06-06 ~ 2026-06-07

## 今日速览

ZeroClaw 项目在 2026 年 6 月 7 日呈现出极高的活跃度，过去 24 小时内产生了 39 条 Issue 和 50 条 PR 更新。项目在安全、插件和稳定性方面的投入显著增强，尤其是在 WASM 插件生态和权限控制模型上取得了实质性进展。尽管无新版本发布，但大量关注的 PR 待合并（45 条），显示出开发团队正在密集推进多个功能模块的落地，项目整体处于“重开发、高产出”的冲刺阶段。

## 版本发布

无。

## 项目进展

今日项目主要进展体现在对安全加固和功能缺陷的快速响应上，多个高风险 Bug 已被修复并合入主分支：

1.  **修复严重安全/数据泄露 Bug**：`#6978` 修复了 `[secret]` 嵌套字段在配置显示中泄露的问题；`#7252` 修复了会话管理系统中的一个严重 Bug，该 Bug 可导致已被杀死的 ACP 会话从持久化历史中复活，存在数据丢失/安全风险。这两个问题均在今天被关闭。
2.  **强化路径安全策略**：`#7133` 发现路径安全策略在处理引号内包含 `~` 符号的命令时存在误报。今日关闭的 PR `#7281` 已修复了该问题，防止了 `heredoc` 体误触发路径安全告警。
3.  **稳定化 Telegram 与 Web 端**：合并的 PR `#7334` 修复了 Telegram 频道中零间隔消息更新的 Bug；关闭的 `#7126` 和 `#7151` 分别解决了网页 UI 中“清空”按钮不生效和观测工具遥测数据泄漏导致的“未知”工具卡片问题，提升了 Web 端稳定性。
4.  **核心功能修复**：PR `#7307` 确保运行时 profile 设置能正确应用到 delegate 子代理循环中，修复了配置继承不完整的问题。

这些动作表明，项目在推进新功能的同时，正在系统性地修复安全与稳定性的积弊，正向着一个更健壮的 v0.8.0 版本稳步迈进。

## 社区热点

今日社区讨论和协作焦点主要集中在两个方面：基础设施架构和插件生态系统拓展。

1.  **OIDC 与 OAuth 认证支持（#7141, #5601）**：这两个 Issue 获得了最多的关注（共 11 条评论）。`#5601` 自提出以来已有两个月，社区持续关注对 **Ollama Cloud**、**智谱**、**月之暗面** 等国内主流平台的原生订阅式 OAuth 支持。`#7141` 作为追踪 Issue，系统性规划了 OIDC 认证提供者的支持。这反映出用户对摆脱静态 API Key 管理、实现更安全灵活的认证方式的强烈需求，是提升企业级用户体验的关键一步。
    - [#7141 OIDC Authentication Provider support](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)
    - [#5601 Subscription-native OAuth support](https://github.com/zeroclaw-labs/zeroclaw/issues/5601)

2.  **WASM 插件生态的快速构建**：由 `theonlyhennygod` 发起的一系列 PR（`#7335`, `#7337`, `#7336`）构成了一个“沙箱隔离”与“命名空间”的插件基础设施栈。这标志着项目正在快速构建一个安全、可管理的 WASM 插件运行环境。同时，几十个新的具体插件 PR（如 n8n 工作流、ACE-Step 音乐生成、Stable Diffusion 图像生成等）在短短几天内涌现，显示社区和开发团队对该方向的极高热情，这将是 ZeroClaw 区别于 MCP 路线的关键差异化优势。
    - [介绍 WASM 插件沙箱的 PR #7335](https://github.com/zeroclaw-labs/zeroclaw/pull/7335)
    - [插件工具命名空间与限速的 PR #7337](https://github.com/zeroclaw-labs/zeroclaw/pull/7337)

## Bug 与稳定性

今日报告的 Bug 修复效率很高，但有数个高优先级、高风险问题被快速解决。按严重程度排列如下：

1.  **S0 - 数据丢失/安全风险**：
    - `#7252` **[已关闭]**：已杀死的 ACP 会话可从持久化历史中被恢复，存在严重数据安全风险。**已有修复合入**。
    - `#6978` **[已关闭]**：配置中 `[secret]` 字段在 `ObjectArray` 中未正确遮蔽，导致秘密泄露。**已有修复合入**。
2.  **S1 - 关键功能失效**：
    - `#7068` **[已关闭]**：Telegram 频道可能错误地将 Codex 的内部工具转录作为最终回复发送给用户。**已有修复合入**。
3.  **S2 - 功能退化**：
    - `#7332` **[已关闭]**：Telegram 部分流式传输允许零更新间隔，导致消息被频繁编辑，影响体验。**已有修复（PR #7334）合入**。
    - `#7126` **[已关闭]**：Web UI “清空所有”按钮仅清空前端显示，未清除后端会话历史，造成行为不一致。**已有修复合入**。
    - `#7197` **[已关闭]**：Windows 上 Web 工具栏加载缓慢并弹出黑框。**已有修复合入**。

总体而言，今日项目响应了多个严重等级 Bug，修复动作迅速且有效，展现了良好的项目维护状态。目前开放的 `#6914`（强制执行 `allowed_tools`）等 P1 级高风险 Issue 仍在推进中。

## 功能请求与路线图信号

今日的功能请求和路线图信号非常清晰，预示着未来版本的重点发展方向：

1.  **WASM 插件系统是绝对焦点**：`v0.8.2` 和 `v0.8.3` 的追踪 Issue（`#7314`, `#7320`）及大量相关 RFC（`#7338`, `#7339`）和 PR 表明，WASM 插件的 **生命周期钩子、沙箱隔离、远程注册中心、仪表盘管理** 等配套功能正在同步开发。这将是 ZeroClaw 区别于传统 AI 助手，构建可扩展生态的核心。
    - [WASM 插件可行性追踪 #7339](https://github.com/zeroclaw-labs/zeroclaw/issues/7339)

2.  **安全和权限控制深化**：多个 P1/P2 级别的 Feature（如 `#6914` 强制工具黑白名单、`#5775` 按技能分配权限）表明社区和团队正致力于构建一个更细粒度、更安全的权限模型，这符合企业级应用的需求。这些功能很可能会在 v0.8.0 或后续版本中被优先考虑。

3.  **基础设施改进**：`#7184` 的 RFC 提出将翻译文件迁移到 git 子模块，是一个良好的过程改进信号，表明项目正在为更广泛的国际化贡献和更快的协作做准备。`#5908` 和 `#6906` 分别要求改进 CI/CD 容器构建和 Nix flake 支持，反映了社区对完善开发者和运维体验的诉求。

## 用户反馈摘要

从今日的 Issue 和 PR 讨论中，可以提炼出以下用户核心反馈：

1.  **痛点：WASM 插件难以发现和安装**：PR `#7333` 的提出直接回应了这一痛点。用户明确表示“手动复制 `.wasm` 文件是采用瓶颈”，强烈需要一个类似包管理器的远程注册中心和 `plugin search`/`install` 命令。

2.  **痛点：安全策略过于严苛或存在误报**：`#7133` 的用户反馈了路径安全策略在处理复杂 shell 命令时存在误报，影响了正常使用。这促使了 `#7281` 的快速修复。

3.  **满意/关注：对“自托管”/“本地优先”特性的喜爱**：在新增的插件 PR（如 `ace-step`、`sd-webui`、`ollama-embed`）中，“本地”、“自托管”、“隐私”、“无需付费”成为卖点和社区讨论的焦点。这反映了用户群体对数据主权和离线能力的强烈偏好。

## 待处理积压

以下为需要维护者重点关注、时间较久或状态为阻塞的重要 Issue 与 PR：

1.  **高优先级、长期阻塞的需求**：`#5601`（OAuth 支持）和 `#5607`（Cron 任务前置钩子）自 4 月提出以来已近 2 个月，仍因状态为 `blocked` 而未解决。这可能是由于设计复杂或依赖其他组件。建议维护者定期同步状态，更新预期时间线。
    - [Feature]: OAuth 支持（#5601）
    - [Feature]: Cron 前置钩子（#5607）

2.  **v0.8.0 发布版的巨额 PR**：`#7229`（新增 MCP/Skills/Plugins 仪表盘标签页）是一个标签为 `size: XL` 的巨大变更，涉及 Web UI 重构，目前仍有 45 个未合并 PR。这一个 PR 的合并质量将直接影响 v0.8.0 的交付稳定性，需要最慎重的代码审查。

3.  **Nix 构建支持**：`#6906` 明确指出现有的 Nix flake 未提供预期的 `zeroclaw` 包和模块，用户期待修复。这个请求相对独立，技术实现路径清晰，可以作为改善开发者体验的 Quick Win 来处理。
    - [Feature]: 改进 Nix flake（#6906）

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*