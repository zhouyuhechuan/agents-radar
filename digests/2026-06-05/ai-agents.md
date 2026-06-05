# OpenClaw 生态日报 2026-06-05

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-05 02:43 UTC

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

好的，这是为您生成的 OpenClaw 项目动态日报。

---

## OpenClaw 项目动态日报 — 2026-06-05

### 1. 今日速览

过去24小时，OpenClaw 项目保持高度活跃，共计处理了500条Issue和500条PR。然而，项目整体呈现出“高产出、高压力”的态势。一方面，社区提交了大量针对2026.6.1版本的回归性Bug报告和修复补丁；另一方面，待合并PR积压严重（391条），显示出维护者审查资源可能面临瓶颈。最显著的风险点集中在**多个信源通道（Slack、Matrix、Telegram、Discord）的消息丢失/状态损坏**以及**新版OpenAI ChatGPT Responses传输的兼容性问题**。整体来看，项目正处于重大功能迁移（如Codex运行时、SQLite会话存储）和稳定性修复的关键期，健康度评级为 **“需高度关注 (Watch)”**。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日无PR被合入主分支。但以下几个关键PR已进入“准备维护者审查 (ready for maintainer look)”或“自动合并就绪 (automerge armed)”状态，代表了项目近期的主要推进方向：

- **CI/安全加固**: [#90287 fix(ci): scope PR merge diff checks to first parent](openclaw/openclaw Pull Request #90287) **（已关闭/合并）**。此PR修复了CI在检查PR差异时可能因使用错误的commit SHA而导致误判的问题，提升了CI流程的可靠性，属于重要的基础设施改进。
- **会话状态管理**: [#90514 fix(session): clear stale fallback model state on reset](openclaw/openclaw Pull Request #90514)。此PR解决了`/reset`或`/new`命令后，会话模型回退状态未被清除的问题，直接回应了社区关于Discord频道超大会话的反馈，对提升用户体验至关重要。
- **信源通道修复**:
    - [#90212 fix(agents): deliver native /compact replies through source suppression](openclaw/openclaw Pull Request #90212)。修复了飞书（Feishu）频道中`/compact`命令回复不显示的问题。
    - [#89744 Fix Discord default account startup priority](openclaw/openclaw Pull Request #89744)。修复了多Discord账号配置下，主账号启动顺序不优先的问题。
- **性能与底层优化**: [#89040 perf: avoid event-loop stall during embedded_run bootstrap-context](openclaw/openclaw Pull Request #89040)。此PR尝试解决`embedded_run`启动时因同步I/O导致的事件循环阻塞（14-22秒）问题，这对于减少消息丢失和提升系统响应性非常重要。

**项目整体向前迈进了关键一步**：修复了一批高优先级的、与Codex运行时和会话核心逻辑相关的回归性Bug，并持续夯实CI基础设施。然而，高达391条的待合并PR表明，项目的交付速度正受到审查流程的制约。

### 4. 社区热点

过去24小时内，社区讨论高度集中于以下三个焦点：

1.  **Slack 连接静默丢失 (Issue #72808)**
    - **链接**: [Issue #72808 [Bug]: Silently lost connection to Slack](openclaw/openclaw Issue #72808)
    - **热度**: 20条评论，评论数最高。
    - **诉求**: 用户反映与Slack的连接会在后台静默断开，且无任何错误提示。该问题已被标记为`P1`优先级和`impact:message-loss`，属于严重影响用户体验的回归问题。社区对此表现出了高度关注，也反映出用户对连接稳定性的核心诉求。

2.  **核心Session/Transcript SQLite迁移跟踪 (Issue #88838)**
    - **链接**: [Issue #88838 Track core session/transcript SQLite migration via accessor seam](openclaw/openclaw Issue #88838)
    - **热度**: 17条评论。
    - **诉求**: 这是一个内部跟踪Issue，但评论数高说明社区或维护者对该重大重构方案（从JSON文件迁移到SQLite）的技术细节和潜在风险有热烈讨论。社区希望该迁移能通过“按抽象分支 (Branch by Abstraction)”的方式分步进行，以避免大型重写带来的高风险，体现了对项目稳定性的关注。

3.  **Codex-vs-Pi运行时一致性QA (Issue #80171)**
    - **链接**: [Issue #80171 Codex-vs-Pi runtime parity QA harness (RFC + tracking)](openclaw/openclaw Issue #80171)
    - **热度**: 15条评论，已关闭。
    - **诉求**: 社区对OpenClaw默认运行时从Pi迁移到Codex后的行为一致性非常关心。用户期望在同一问题上，使用不同运行时能获得相同的结果。该Issue虽已关闭（可能转为内部跟踪），但其高评论数表明了社区对运行时切换稳定性的深度关注。

### 5. Bug 与稳定性

今日报告的Bug集中在**2026.6.1版本的回归问题**和**长期存在的连接/状态损坏问题**上，严重程度普遍较高。

| 严重程度 | 问题描述 | Issue 链接 | 相关 PR |
| :--- | :--- | :--- | :--- |
| **极高** | **[Bug]: 2026.6.1 OpenAI ChatGPT Responses transport fails with invalid_provider_content_type** 升级后，gpt-5.4/5.5的推理完全失败 | [#90083](openclaw/openclaw Issue #90083) | 无明确修复PR |
| **极高** | **Cron state silently wiped during SQLite migration on upgrade to 2026.6.1** 升级后45个定时任务中的44个静默丢失 | [#90072](openclaw/openclaw Issue #90072) | 无明确修复PR |
| **高** | **[Bug]: active-memory circuit breaker too aggressive; fallback prompt pollutes main session** 内存断路器过于激进，导致会话被“请重试”的提示污染 | [#90082](openclaw/openclaw Issue #90082) | 无明确修复PR |
| **高** | **openai-chatgpt-responses native replay sends encrypted reasoning and breaks next turn** 多轮对话中，重放带有加密推理内容会导致后续对话失败 | [#90093](openclaw/openclaw Issue #90093) | 无明确修复PR |
| **高** | **[Bug]: Silently lost connection to Slack** Slack连接静默丢失，无任何告警 | [#72808](openclaw/openclaw Issue #72808) | 无明确修复PR |
| **中** | **Session model route drifts from openai/gpt-5.5 to openai-codex/gpt-5.5** 会话模型路由在Codex运行时下发生漂移 | [#90036](openclaw/openclaw Issue #90036) | 无明确修复PR |
| **中** | **[Bug]: Repeated hard resets on same session key** 特定群组会话反复触发硬重置 | [#63216](openclaw/openclaw Issue #63216) | 无明确修复PR |

**结论**：2026.6.1版本发布后，出现了数个与OpenAI新API、SQLite迁移、以及信号断路器相关的严重回归问题，项目急需发布一个补丁版本（2026.6.2）来修复这些关键问题。

### 6. 功能请求与路线图信号

- **[RFC] Control UI plugin contribution slots (Issue #71736)**: 社区提出为控制UI添加数据驱动的插件贡献槽，以实现插件定制聊天模式、审批卡片等功能。虽然状态为`stale`，但它代表了社区对UI可扩展性的需求。结合其他关于控制UI的Feishu显示截断（#88929）和WebChat文本重复（#72341）等问题，**优化和插件化Web UI** 很可能是下一阶段的重要方向。
- **[Feature]: 支持敏感数据脱敏 (Issue #64046)**: 这是一个长期存在的功能请求，希望API Key等敏感信息在配置文件、日志和UI中实现脱敏。鉴于安全性一再被强调（如#65624 Mattermost令牌暴露），**此功能很可能被纳入下一个大版本的安全加固计划中**。
- **与Codex运行时相关的持续优化**: 多个Issue和PR都围绕Codex运行时展开，如路由漂移（#90036）、OAuth刷新失败（#86215）、Event-loop阻塞（#89040）等。这表明**Codex作为默认运行时的稳定性与兼容性**是当前开发的重中之重，短期内不会有新的重大功能引入，而是聚焦于打磨现有架构。

### 7. 用户反馈摘要

- **痛点**:
    - **升级恐惧症**: 多位用户反映升级到2026.6.1后遭遇严重问题，如GPT-5.x模型完全不可用（#90083）、定时任务被全部清空且无警告（#90072），导致用户对“升级”行为产生担忧。有用户在#90072中表示“希望有备份或提示”。
    - **“Silent Failure”问题突出**: 多个Bug（如Slack断连#72808、Codex OAuth失败#86215）都是静默发生的，用户只能被动发现并忍受数小时的服务中断。这极大地降低了用户对系统的信任感。
    - **配置与操作复杂度**: 用户提到`openclaw.json`难以手动编辑（#89992 PR摘要），以及`/model`指定的模型被错误地加入回退列表（#88039），反映出配置系统和模型选择逻辑的用户体验有待优化。

- **满意点**:
    - **快速响应和修复**: 尽管存在诸多问题，但社区看到大量修复PR被提交，如针对Discord启动顺序（#89744）、飞书速率限制（#89659）等。用户对核心团队和社区的快速反应能力表示了肯定。
    - **向Codex运行时迁移的整体方向**: 从相关Issue的讨论（如#80171, #88838）可以看出，社区理解并支持对架构进行现代化改造，尤其是在性能和可维护性方面。

### 8. 待处理积压

以下为几个**长期未解决且影响重大**的Issue，建议维护者优先处理：

| 问题描述 | Issue 链接 | 创建时间 | 严重性 | 状态原因分析 |
| :--- | :--- | :--- | :--- | :--- |
| **Heartbeat isolated mode: cadence stalls, ‘heartbeat last’ mislabels exec-events, etc.** 心跳隔离模式下的多重回归问题 | [#65161](openclaw/openclaw Issue #65161) | 2026-04-12 | `P2` / `impact:session-state` `impact:message-loss` | 问题维度多，分析复杂，可能需要较大重构，等待产品决策或维护者深入审查。 |
| **[Bug]: Repeated hard resets on same session key despite high reserveTokensFloor** 同一会话反复硬重置 | [#63216](openclaw/openclaw Issue #63216) | 2026-04-08 | `P1` / `impact:session-state` `impact:message-loss` | 根因分析（`extraSystemPromptHash`漂移）已明确，但修复可能需要触及核心会话逻辑，/或需要项目内部统一意见。 |
| **[Feature]: 希望支持敏感数据脱敏** 敏感信息明文存储与展示 | [#64046](openclaw/openclaw Issue #64046) | 2026-04-10 | `P1` / `impact:security` `impact:auth-provider` | 功能请求，但关联多个安全漏洞。等待安全审查和产品决策，可能涉及较大范围的配置管理和UI改造。 |
| **Claude CLI sessions reset on every turn in group channels** 群组频道中Claude会话每轮都重置 | [#69118](openclaw/openclaw Issue #69118) | 2026-04-19 | `P1` / `impact:session-state` | 问题根因已定位（`extraSystemPromptHash`漂移），且有明确的fix PR形状（`fix-shape-clear`），但可能因与`mcpConfigHash`修复（#64386）的协调问题而被搁置。 |

---

## 横向生态对比

好的，作为AI智能体与个人AI助手领域的资深技术分析师，现根据您提供的2026-06-05各项目动态数据，为您呈上一份横向对比分析报告。

---

### **AI智能体与个人AI助手开源生态横向分析报告 (2026-06-05)**

#### **1. 生态全景**

当前，个人AI助手/自主智能体开源生态正处于从 **“功能可用”向“生产可用”转型的阵痛期**。多项目同时爆发式迭代，核心架构（如运行时迁移、多通道支持、MCP协议）趋于成熟，但伴随而来的是**频繁的回归性Bug、稳定性挑战以及社区对“静默失败”的普遍不满**。生态内部呈现出明显的差异化分层：头部项目（如OpenClaw）作为参照系正承受巨大的平台压力，而专注于特定方向（如MCM、本地优先）的项目则展现了更强的灵活性和创新性。总体而言，社区对构建**可靠、可理解、可扩展**的智能体系统的渴望，已超越了对单一功能堆叠的需求。

#### **2. 各项目活跃度对比**

| 项目名称 | 今日Issues | 今日PRs | 新版本 | 健康度评估 | 核心状态 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 (新/活跃) | 500 (待合并391) | 无 | **需高度关注** | 高产出，高压力，主流参照系，处质量巩固+平台压力期 |
| **NanoBot** | 6 (新开2) | 59 (合并/关闭) | 无 | **优秀** | 高速迭代，稳定性显著提升，向1.0候选阶段冲刺 |
| **PicoClaw** | 大量 | 22 (合并12) | v0.2.9-nightly | **良好** | 快速迭代，修复存量Bug，兼容上游变化 |
| **IronClaw** | 与PR共89 | 与Issue共89 | 无 | **良好** | “Reborn”架构闭环推进，从功能开发向生产级稳定过渡 |
| **LobsterAI** | 1 (活跃) | 16 (合并) | 无 | **优秀** | 聚焦核心模块（Cowork, MCP）稳定性与功能增强 |
| **CoPaw** | 32 | 33 | v1.1.11-beta.1 | **良好** | 高活跃度，社区反馈与核心修复形成良好闭环 |
| **ZeroClaw** | 32 (新/活跃) | 50 (待合并35) | 无 | **良好** | 高活跃，修复多S1级Bug，互操作新功能(RFC)涌现 |
| **Hermes Agent** | - | - | - | **信息缺失** | 无法评估 |
| **NanoClaw** | 1 | 8 (合并3) | 无 | **稳定** | 维护驱动，重点修复特定通道（Signal, WhatsApp）Bug |
| **NullClaw** | 0 | 0 | 无 | **休眠** | 过去24小时无活动 |
| **TinyClaw** | 0 | 0 | 无 | **休眠** | 过去24小时无活动 |
| **Moltis** | 2 | 3 (待合并) | 无 | **稳定** | 聚焦技术深耕（Shadow DOM），社区提出明确功能诉求 |
| **ZeptoClaw** | 0 | 0 | 无 | **休眠** | 过去24小时无活动 |

*(注：Hermes Agent 数据缺失，健康度无法评估。OpenClaw的Issue/PR数量为当日处理总数，非新开数。)*

#### **3. OpenClaw在生态中的定位**

- **生态核心参照系**: OpenClaw作为本报告的核心，其社区规模（日处理500条Issue/PR）和积压压力（391条待合并PR）远超其他任何项目，它定义了“全能型”个人AI助手的技术栈复杂度。
- **优势**: 拥有最完整的通道矩阵（Slack、Discord、飞书等）和最活跃的社区贡献，是生态中**功能覆盖度最广**的项目，任何在OpenClaw上验证成功的设计和修复，都可能成为整个生态的标杆。
- **技术路线差异**: OpenClaw正承受从旧的Pi运行时向新的Codex运行时迁移的巨痛。这种大规模架构重构带来了显著的回归问题（如#90083），其**高复杂性带来高风险**。相比之下，其他项目如NanoBot、PicoClaw的选择更聚焦，架构包袱更小，迭代速度和质量控制反而更优。
- **社区规模对比**: OpenClaw的社区活跃度是第二梯队（如NanoBot、ZeroClaw、IronClaw）的数十倍，但其问题解决效率（审查瓶颈）与社区期望之间已出现鸿沟。其他项目在维护者和贡献者之间保持着更健康的协作节奏。

#### **4. 共同关注的技术方向**

- **运行时/Provider兼容性与稳定性**：
    - **涉及项目**: OpenClaw, PicoClaw, CoPaw, ZeroClaw, NanoBot
    - **具体诉求**: 多个项目在处理新版OpenAI API (如ChatGPT Responses传输)、OAuth认证、工具调用ID一致性、模型路由漂移等细节问题上暴露出bug。这反映了生态对**核心LLM交互层的标准兼容性**要求极高，容错空间极小。
- **消息可靠性与状态一致性**：
    - **涉及项目**: OpenClaw, NanoClaw, IronClaw, ZeroClaw
    - **具体诉求**: “静默失败”（如Slack断连无告警、MCP重连失败、WhatsApp认证自毁）和“状态损坏/丢失”（如会话过期、定时任务丢失、压缩后输出标签不闭合）是多项目共有的严重痛点。用户对**系统行为的透明度和可观测性**需求已上升为首要关切。
- **Web UI与用户体验重构**：
    - **涉及项目**: OpenClaw, IronClaw, CoPaw, ZeroClaw, NanoBot
    - **具体诉求**: 多个项目正在或计划重构其Web界面，包括优化Provider配置面板、添加会话书签/标签、改善工具调用实时显示。这表明**第一印象和日常操作便利性**是吸引和留住用户的关键。
- **安全与访问控制**：
    - **涉及项目**: OpenClaw, ZeroClaw, NanoBot, PicoClaw
    - **具体诉求**: 社区对敏感信息（API Key）脱敏、跨渠道认证、工作区权限（workspace guard）、SSRF防护等提出了明确需求。这表明**随着Agent权限和自动化能力增强，安全已成为不可回避的基础设施问题**。

#### **5. 差异化定位分析**

| 维度 | OpenClaw | NanoBot / PicoClaw | IronClaw / ZeroClaw (Rust系) | LobsterAI / CoPaw (熟人系) | Moltis / TinyClaw (专业化) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **核心定位** | **全能型平台** | **轻量级高效实战** | **高性能、企业级架构** | **中文友好、生态集成** | **特定场景专家** |
| **技术栈** | 复杂，多语言 | Go (PicoClaw) / TypeScript (NanoBot) | Rust | Python (CoPaw) / Python (LobsterAI) | Web技术 (Moltis) / TBD (TinyClaw) |
| **目标用户** | 追求功能全面的高级用户与开发者 | 追求简便、快速部署的个人/小型团队 | 对性能、可靠性及系统集成有高要求的企业/高级开发者 | 中文AI生态用户，与网易系产品集成 | 语音助手 (Moltis) 或特定任务 |
| **关键差异** | 功能最全，但架构负担重，稳定性风险高 | 迭代敏捷，Bug修复快，专注解决核心痛点（如fallback、CLI） | 以Rust的零成本抽象追求极致性能，正进行复杂架构重构（"Reborn"），社区呼声高的功能（A2A，计算机操控）在其路线图上 | 围绕“协作”和“记忆”做深度优化，与本地AI社区（如MiniMax）结合紧密 | 深耕特定技术（如Shadow DOM），强调离线/本地化能力，用户基数小但需求明确 |

#### **6. 社区热度与成熟度**

- **第1梯队 (高度活跃，功能快速迭代期)**: **NanoBot, CoPaw, LobsterAI, ZeroClaw, PicoClaw**. 这些项目每日有大量PR合并，Bug修复和新功能交付速度快，社区反馈与开发响应形成良好闭环。它们代表了生态中最具活力的部分，更适合希望贡献代码或快速体验新功能的开发者。
- **第2梯队 (活跃，质量巩固期)**: **OpenClaw, IronClaw**. 这些项目拥有庞大用户基数和复杂架构，当前阶段的核心任务是解决存量Bug、提升稳定性，而非引入大量新功能。它们的社区热度极高但讨论焦点多集中在“问题与修复”上，适合需要成熟稳定平台的用户，但要容忍其发布节奏。
- **第3梯队 (稳定维护期)**: **NanoClaw, Moltis**. 这些项目活跃度平稳，专注于特定模块的维护和技术深耕，社区需求明确但讨论热度不高。适合有特定需求的用户（如需要Signal/WhatsApp通道、或对本地STT有刚需）。
- **第4梯队 (休眠/停滞期)**: **NullClaw, TinyClaw, ZeptoClaw**. 过去24小时无任何活动，可能处于项目中断或人员调整期，风险较高。

#### **7. 值得关注的趋势信号**

1.  **“升级恐惧症”成为社区痛点**：用户因版本升级遭遇数据丢失（#90072）、模型完全不可用（#90083）等严重问题，产生对升级的抵触心理。这要求项目必须将**版本兼容性和平滑迁移能力**提升到前所未有的高度，并建立更完善的CI/CD发布前验证机制。
2.  **“静默失败”是信任杀手**：多个项目报告了Slack断连、MCP断开却无告警的bug。这给开发者一个强烈信号：**必须投资于构建可观测性和智能告警系统**，而非仅仅添加功能。一个无法被理解的智能体是无法被信任的。
3.  **Agent互操作性（A2A）需求萌芽**：ZeroClaw社区对A2A协议的高赞和持续讨论表明，单一Agent的能力边界已触及天花板。未来，**多Agent协作、Agent发现与编排**将成为下一个必须攻克的技术高地，这也是生态从“单体英雄”走向“智能体网络”的关键一步。
4.  **对“本地优先、隐私保护”的渴望增强**：Moltis用户明确要求集成本地Whisper STT引擎。这反映了在云端API成本、延迟和隐私担忧并存的背景下，**离线或准离线的AI能力**不再只是“备选”，而可能成为差异化竞争优势。
5.  **社区驱动、高质量的“需求-功能”闭环成为项目成功关键**：CoPaw和NanoBot对社区Bug报告的快速响应和修复，以及ZeroClaw将高赞的“计算机控制”特性正式纳入路线图，都印证了**保持与社区反馈的紧密同步**是维护项目健康、提升用户忠诚度最有效的策略。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 (2026-06-05)

## 1. 今日速览

过去 24 小时内，NanoBot 项目保持高活跃度：共处理 6 个 Issues（新开 2 个，关闭 4 个），合并/关闭 59 个 PR，另有 16 个 PR 待合并。新版本未发布。社区围绕**模型降级容错**、**Azure AAD 认证**、**WebUI UX 改进**等方向进行了密集的合并与修复，项目稳定性与功能完整性显著提升。

## 2. 版本发布

*（无新版本发布，此部分省略）*

## 3. 项目进展

今日合并/关闭的重要 PR 覆盖多个模块，体现出项目在多方面齐头并进：

- **Provider 扩展**：`#4126` 为 Azure OpenAI 提供者添加了基于 Azure AAD 的身份认证支持，解决了严格安全策略下无法使用 API Key 的痛点。  
- **Agent 生命周期**：`#4176` 新增运行级 Agent Hook 回调（before_run/after_run/on_error/on_finally），为插件化拦截和监控奠定基础。  
- **CLI 兼容性**：`#4164` 在 pip 不可用（如通过 uv tool 安装时）自动回退至 `uv pip`，修复了 WebUI CLI App 安装失败的问题。  
- **Tool Call ID 一致性**：`#3984` 修复了 OpenAI 兼容 API（如 GLM-4.7、Kimi 2.6）中工具调用 ID 被替换导致结果匹配失败的回归。  
- **MCP 重连**：`#4027` 重置 `_mcp_connected` 状态并添加重连回调，解决了 MCP 会话断开后无法自动恢复的缺陷。  
- **测试基建**：`#4189` 使用确定性时钟/事件替代时序等待，大幅提高单元测试稳定性和覆盖率。  
- **WebUI 增强**：`#4163` 为用户消息添加“从此处 Fork”功能，支持历史会话分支编辑。

此外还有 50+ 个小型修复与清理 PR 被合并，项目整体向 **1.0 候选阶段**稳步推进。

## 4. 社区热点

- **`#1121` Fallback model not triggered on LLM timeout（已关闭）**：作者报告当主模型超时或返回 503 时，配置的 fallback 模型未被触发，用户只能得到错误。此 Issue 获 3 个 👍 和 3 条评论，是近期最受关注的稳定性问题。该问题已在 24 小时内被修复并关闭。  
- **`#912` Support Task-Specific Model Configuration（长期开放）**：提议为对话、工具调用、浏览器使用分别配置不同模型。虽标为 stale，但仍获得 4 条评论和 3 个 👍，社区对精细控制模型选择的需求依然强烈。  
- **`#4125` Azure AAD Based Auth（已关闭）**：企业用户因策略限制需使用 Azure Identity 认证，该需求在 5 月 31 日提出后迅速被实现（`#4126`），表明项目对合规性诉求响应积极。

## 5. Bug 与稳定性

| 严重程度 | 问题描述 | 状态 | 对应修复 PR |
|----------|----------|------|-------------|
| **高** | 主模型超时/503 时 fallback 模型未触发，直接报错给用户 | 已关闭 | `#4027`（MCP 重连）及关联修复 |
| **中** | uv tool 环境下 pip 模块缺失导致 CLI 安装失败 | 已关闭 | `#4164` 回退至 uv pip |
| **中** | MCP 会话断开后无法自动重连 | 已关闭 | `#4027` 重置连接状态 + 重连回调 |
| **中** | OpenAI 兼容 API 工具调用 ID 不匹配 | 已关闭 | `#3984` 保留原始 ID |
| **低** | WebUI 仅有一个全局快捷键（Cmd+K），缺少新建对话快捷键 | 已关闭 | `#4178` 新增 Cmd/Ctrl+Shift+O |

另外，今日新开 Issue `#4196` 报告火山引擎图片生成提供者不被支持，属于功能缺失而非 Bug。

## 6. 功能请求与路线图信号

- **`#912` Task-Specific Model Configuration**：虽为 stale，但涉及核心模型调度架构，社区呼声高。近期有 PR `#4190` 强化工具调用校验，可能为后续按任务配置模型铺垫。  
- **`#4196` 支持火山引擎图片生成**：新提出，用户需多通道图像生成（Seedream 5.0 Lite）。项目已支持多种图片生成提供者，可期待纳入下一轮 Provider 扩展。  
- **`#3968` `/skill` 命令列出已启用技能**：PR 已完成开发，等待合并。该功能直接响应 Issue `#3959`，解决用户无法发现可用技能的痛点。  
- **`#4192` Subagent 继承 MCP 工具**：PR 允许子代理继承主代理的 MCP 工具，提升多代理编排灵活性，已标记 `Fixes #4166`，有望随下一个小版本发布。  
- **`#4195` Desktop shell 和共享 WebUI 表面**：首次引入桌面宿主支持，虽为实验性 PR，但标志项目从纯 Web/CLI 向桌面端迈进。

## 7. 用户反馈摘要

- **稳定性痛点**：多位用户反馈 LLM 超时后无 fallback 机制，直接影响生产可用性。该问题已修复，社区满意度预计回升。  
- **企业合规诉求**：`#4125` 作者明确提到“Azure 订阅有严格策略禁止 API Key 认证”，需要 Azure Identity 认证。该 PR 快速合入，获得正面评价。  
- **易用性改进**：`#4178` 用户指出 WebUI 新建对话缺少快捷键，合并后提升高频操作效率。  
- **新需求涌现**：`#4196` 用户提出对火山引擎的支持，且给出具体模型名，表明用户对多提供者集成的期待已不限于主流国际厂商。  
- **闲置 Issue 关注**：`#912` 虽已 stale，但仍有用户在评论中讨论实现细节，表明“按任务配置模型”是许多高级用户的真实需求。

## 8. 待处理积压

以下 Issue/PR 长期未合并或响应，建议维护者关注：

- **`#912` [stale] Support Task-Specific Model Configuration**（创建于 2026-02-20，4 评论，3 👍）  
  虽标为 stale，但仍是社区最关注的功能之一。建议重新评估优先级或在路线图中明确定位。  
  [链接](https://github.com/HKUDS/nanobot/issues/912)

- **`#3968` feat(command): add /skill slash command**（创建于 2026-05-23，Open）  
  功能开发已完成，但尚未合并。该 PR 实现简单且直接解决用户痛点，建议尽快 review 合并。  
  [链接](https://github.com/HKUDS/nanobot/pull/3968)

- **`#3982` test: add scripted agent runner harness**（创建于 2026-05-24，Open）  
  测试基础设施 PR，可提高未来 Agent 测试的可重复性。已有多日未更新，需 maintainer 推动。  
  [链接](https://github.com/HKUDS/nanobot/pull/3982)

- **`#4053` fix(tools): keep read-only roots out of write paths**（创建于 2026-05-29，Open）  
  重要的安全加固 PR，阻止写工具访问只读根目录。建议优先合并以降低安全风险。  
  [链接](https://github.com/HKUDS/nanobot/pull/4053)

- **`#4123` fix(mcp): reject unsafe HTTP URLs before probe**（创建于 2026-05-31，Open）  
  SSRF 防护增强，对 MCP 的 HTTP URL 进行前置校验。安全性相关，不宜积压。  
  [链接](https://github.com/HKUDS/nanobot/pull/4123)

---

*生成时间：2026-06-05 UTC+8 | 数据来源：[NanoBot GitHub](https://github.com/HKUDS/nanobot)*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ 摘要生成失败。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据您提供的 PicoClaw 项目数据生成的 2026-06-05 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-06-05

## 1. 今日速览

今日项目活跃度极高，社区与开发团队协作紧密。**PR 更新量达到 22 条**，其中 12 条已合并/关闭，展现了积极的维护节奏。**核心修复集中于稳定性与兼容性**，包括 PID 文件检查、OneBot 协议适配、Codex OAuth 工具调用等问题。同时，一个 `nightly` 版本发布，包含次夜构建的累积变更。总体而言，项目正处于快速迭代、修复存量 Bug 并兼容上游依赖变化的关键阶段。

## 2. 版本发布

- **Nightly Build (v0.2.9-nightly.20260605.5224b9a4)**
  - **说明**: 自动化的夜间构建版本，包含截至 `main` 分支的最新提交。
  - **警告**: 此版本被标注为**可能不稳定**，仅供测试和使用，请谨慎用于生产环境。
  - **变更对比**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

## 3. 项目进展

以下为今日合并/关闭的重要 PR，它们修复了关键 Bug 并推进了代码质量。

- **[#3000] 修复 PID 单例检查 (fix(pid): verify process identity...)**: 这是一个重要的稳定性修复，解决了由于 PID 被系统复用导致 Gateway 启动失败的 bug。现在会通过进程名验证来确保检测到的进程确实是 PicoClaw 实例。此问题由 Issue #2720 报告，PR #2813 也曾尝试修复。今日已合并。 [PR #3000](https://github.com/sipeed/picoclaw/pull/3000)
- **[#3007] 修复 Codex OAuth 流式工具调用丢失 (fix: preserve streamed Codex tool calls)**: 针对 Issue #3006 报告的高优先级 Bug，解决了使用 `gpt-5.5` 模型时工具调用被丢弃的问题。此修复确保了流式响应中的函数调用能正确解析。已合并。 [PR #3007](https://github.com/sipeed/picoclaw/pull/3007)
- **[#2996] 修复 exec 工具中的 JSON 序列化错误处理 (fix(tools): handle json.Marshal errors...)**: 提升了 `pkg/tools/shell.go` 中 7 处 `json.Marshal` 调用的健壮性，将静默失败改为明确的错误上报。这避免了因序列化失败导致 LLM 收到空响应的隐患。已合并。 [PR #2996](https://github.com/sipeed/picoclaw/pull/2996)
- **[#2999] 修复 Makefile 中 Go 版本号存在空格的问题 (fix: handle space in go env GOVERSION...)**: 修复了在某些 Go 工具链下，`go env GOVERSION` 返回包含空格的字符串（如 `go1.25.10 X:nodwarf5`）导致编译失败的问题。已合并。 [PR #2999](https://github.com/sipeed/picoclaw/pull/2999)
- **[#3008] 适配 LarkSuite SDK 破坏性变更 (fix: adapt to larksuite oapi-sdk-go v3.9.4...)**: 紧随 Dependabot 的依赖更新 PR #3005，修复了由于 SDK 升级导致的编译错误（`ReceiveIdTypeChatId` 重命名）。体现了维护者对社区贡献的快速响应。已合并。 [PR #3008](https://github.com/sipeed/picoclaw/pull/3008)

## 4. 社区热点

- **[Issue #2968: `/context` 命令始终显示压缩阈值为 76800 tokens]**: 此 Bug 由用户 `xpader` 报告，引发了 4 条讨论，说明用户对上下文管理器显示信息的准确性非常关注。用户希望看到的是软触发（summarize）阈值，而非硬压缩阈值。**已有 PR #2985 在修复这个问题**，显示社区反馈与开发响应形成闭环。 [Issue #2968](https://github.com/sipeed/picoclaw/issues/2968)
- **[Issue #3006: Codex OAuth 工具调用丢失]**: 虽然评论数为 0，但作为今日被快速修复的高价值 Bug，它实际上获得了社区和开发者的高度关注。报告者 `SebastianBoehler` 精准定位了问题根因，促使 PR #3007 迅速诞生并合并。 [Issue #3006](https://github.com/sipeed/picoclaw/issues/3006)
- **[Issue #3002: OneBot 群聊回复错用私聊接口]**: 由用户 `Xuan-Xuann` 报告，这是一个协议集成层面的 Bug，直接导致 NapCat 适配器出错。该问题精准描述了复现步骤和根因，贡献价值很高。**已有 PR #3009 正在修复**。 [Issue #3002](https://github.com/sipeed/picoclaw/issues/3002)

## 5. Bug 与稳定性

今日无严重影响系统可用性的崩溃或回归问题被报告。以下为按严重程度排列的 Bug：

- **[高] Issue #3002: OneBot 群聊回复使用错误 API**：导致群聊功能完全失效。**已有 PR #3009 修复**。 [Issue #3002](https://github.com/sipeed/picoclaw/issues/3002)
- **[高] Issue #3006: Codex OAuth GPT-5.5 工具调用丢失**：影响特定模型（`gpt-5.5`）的 Agent 功能。**已通过 PR #3007 修复并合并**。 [Issue #3006](https://github.com/sipeed/picoclaw/issues/3006)
- **[中] Issue #2968: `/context` 始终显示硬压缩阈值**：不涉及崩溃，但严重影响可用性和用户理解。**已有 PR #2985 修复**。 [Issue #2968](https://github.com/sipeed/picoclaw/issues/2968)
- **[低] Issue #2720: PID 检查不完善导致启动循环**：这是一个历史 Bug，**已于今日通过 PR #3000 修复并合并**。 [Issue #2720](https://github.com/sipeed/picoclaw/issues/2720)
- **[中] Issue #2972: 升级到 v0.2.9 后 Web UI 消息混乱**：影响用户会话体验。**已被开发者关闭**，推测已由内部其他 PR 修复。 [Issue #2972](https://github.com/sipeed/picoclaw/issues/2972)

## 6. 功能请求与路线图信号

- **[Issue #2981: 更新 v0.2.9 版本的使用手册]**: 这是一个明确的维护型任务，表明随着 v0.2.9 的大量变更，官方文档已滞后。这预示着下一阶段可能会出现针对文档的专项更新。 [Issue #2981](https://github.com/sipeed/picoclaw/issues/2981)
- **[PR #3001: 允许 workspace guard 处理 scheme-less URLs]**: 该 PR 旨在让 `restrict_to_workspace` 功能不应错误地拦截如 `curl wttr.in/Beijing` 这样的命令。这是一个针对安全/工作区功能的增强，很可能被纳入下一版本。 [PR #3001](https://github.com/sipeed/picoclaw/pull/3001)
- **[PR #2934: 允许 WhatsApp 使用原生模式]**: 一个已开放近两周的功能 PR，旨在支持 WhatsApp 的原生模式，降低对 `bridge` 的依赖。如果此功能被合并，将扩展 PicoClaw 的独立部署能力。 [PR #2934](https://github.com/sipeed/picoclaw/pull/2934)

## 7. 用户反馈摘要

- **用户 `xpader` (NetBSD/Localsend 用户)**: 报告了多个关于 v0.2.9 版本的问题（Issues #2968, #2972），主要集中在 Web UI 在继承旧会话和/context 显示信息两个方面。这暗示 v0.2.9 版本可能引入了与用户状态或会话管理相关的回归问题，特别是在非主流操作系统上。
- **用户 `SebastianBoehler`**: 针对 Codex OAuth 提供商进行了深入的故障排查，并提供了包含 root cause 分析的错误报告（Issue #3006）和修复方案（PR #3007）。这种高质量贡献者是开源项目的宝贵财富。
- **用户 `Xuan-Xuann`**: 使用 NapCat 适配器的用户，报告了 OneBot 协议实现的逻辑错误（Issue #3002）。这表明 PicoClaw 的多协议栈在支持第三方客户端时，存在集成边界上的 Bug，用户期待更完善和兼容的实现。

## 8. 待处理积压

- **[PR #2813] fix(pid): (updated) verify gateway identity...**: 早在 5 月 7 日就已提交的关于 PID 检查的 PR，其核心功能已被今日合并的 PR #3000 覆盖。建议维护者考虑关闭此 PR，以避免不必要的混淆。 [PR #2813](https://github.com/sipeed/picoclaw/pull/2813)
- **[PR #2956] fix: preserve channel enabled state when merging security.yml**: 已开放超过一周，至今没有评论或更新。此问题修复了配置合并时的重要行为，影响用户体验，建议维护者关注并推进审查。 [PR #2956](https://github.com/sipeed/picoclaw/pull/2956)
- **[PR #2947] fix: correct claude-sonnet-4.6 model ID to use hyphens**: 同样已开放超过一周的修复性 PR，解决了默认配置导致的 404 API 错误。已被标注为 `[stale]`，容易被遗忘。 [PR #2947](https://github.com/sipeed/picoclaw/pull/2947)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-06-05

## 1. 今日速览

- 过去24小时项目活跃度中等，共处理 **1 条新 Issue** 和 **8 条 Pull Request**（其中 **3 条已合并/关闭**，**5 条待合并**）。  
- 修复集中出现在 **Signal** 和 **WhatsApp** 通道：DM消息静默丢失、LID群组发送失败、认证自毁等关键Bug得到解决。  
- **无新版本发布**，但多项核心修复已进入待合并队列，预计近期将形成补丁型发布。  
- 社区互动较少，所有Issue/PR均无评论和点赞，整体呈维护驱动型节奏。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日 **关闭/合并** 了以下重要PR，项目稳定性和通道可靠性稳步提升：

| PR | 状态 | 主要内容 |
|----|------|----------|
| [#2633](https://github.com/nanocoai/nanoclaw/pull/2633) `Fix/whatsapp self destruct and shutdown auth wipe` | ✅ 已合并 | 修复WhatsApp插件在Baileys 7.x上的两个结构性Bug：adapter自毁认证文件、关闭时清空认证，导致配对丢失。 |
| [#104](https://github.com/nanocoai/nanoclaw/pull/104) `fix: replace as any casts with proper BoomError type` | ✅ 已合并 | 规范`BoomError`类型定义，消除两处`as any`强制类型转换，提升TypeScript类型安全。 |
| [#2687](https://github.com/nanocoai/nanoclaw/pull/2687) `[follows-guidelines] Trip agent` | ❌ 已关闭 | 该PR为模板提交，未附带实际代码变更，合并前自行关闭。 |

此外，**PR #2685（docs(signal)）** 虽未合并，但已完成Signal群组打字指示、出站反应、引用回复等文档更新，为后续用户使用提供明确指引。

## 4. 社区热点

今日所有 Issue/PR 均无评论、无点赞，暂无明显社区热点。  
单条新 Issue [#2686](https://github.com/nanocoai/nanoclaw/issues/2686) 标题为“Traveling”，内容为“I want to travel to Canada”，推测为测试或失误提交，不具备技术讨论价值。

## 5. Bug 与稳定性

今日有多项修复指向此前未暴露的隐蔽Bug，按严重程度排序如下：

| 严重程度 | 相关PR | 问题描述 |
|----------|--------|----------|
| **严重** | [#2689](https://github.com/nanocoai/nanoclaw/pull/2689) | **Signal DM首条消息静默丢失**：`isMention` 未设为`true`导致路由跳过自动创建`messaging_groups`行，首次对话无响应。同时DM platform ID缺少`signal:`前缀，影响后续路由。 |
| **严重** | [#2688](https://github.com/nanocoai/nanoclaw/pull/2688) | **WhatsApp LID群组回复失败**：`getNormalizedGroupMetadata` 将群参与者JID转换为phone JID，导致Baileys 7.x上报`ack 421`错误，消息无声到达。 |
| **严重** | [#2633](https://github.com/nanocoai/nanoclaw/pull/2633) | **WhatsApp认证自毁**：adapter在启动过程中早期触发`self.destroy()`，删除已保存的认证文件；停止时清空auth状态，造成每次重启都需重新配对。 |
| **中等** | [#2405](https://github.com/nanocoai/nanoclaw/pull/2405) | **poll-loop自动压缩后输出标签不闭合**：模型在`<message to="...">`包装中经常只开不关，导致下游解析异常。 |

上述修复中，前三个严重Bug已通过对应PR给出解决代码（#2689、#2688 待合并，#2633已合并），`poll-loop`问题仍在待合并状态。

## 6. 功能请求与路线图信号

- **语音转录（本地Whisper）**：PR [#2459](https://github.com/nanocoai/nanoclaw/pull/2459) 为Discord及所有Chat SDK桥接通道（Slack、Teams、Webex、Google Chat等）添加了基于`whisper.cpp`的本地语音转录功能，无需云API。该PR已存在逾三周，若被合并将显著扩展多模态交互能力，是下一版本的重要候选特性。  
- **Signal通道完善**：PR [#2685](https://github.com/nanocoai/nanoclaw/pull/2685) 补充了群组打字指示、出站反应、引用回复等文档，结合前述修复，表明团队正系统性地补全Signal通道的功能死角。

社区层面，单条 Issue [#2686](https://github.com/nanocoai/nanoclaw/issues/2686) 内容空泛，暂不视为有效功能请求。

## 7. 用户反馈摘要

今日无用户评论或明确反馈，未能提炼有用信息。

## 8. 待处理积压

以下 PR 已停留较长时间，建议维护者优先审查合并：

| PR | 创建时间 | 停留天数 | 重要性 |
|----|----------|----------|--------|
| [#2405](https://github.com/nanocoai/nanoclaw/pull/2405) `fix(poll-loop)` | 2026-05-11 | 25天 | **中等**：修复自动压缩后输出不闭合，影响稳定性 |
| [#2459](https://github.com/nanocoai/nanoclaw/pull/2459) `feat(skill): voice transcription` | 2026-05-13 | 23天 | **高**：新增本地语音转录，路线图重点特性 |
| [#2689](https://github.com/nanocoai/nanoclaw/pull/2689) `fix(signal)` | 2026-06-04 | 1天 | **高**：修复Signal DM关键Bug，建议优先合并 |
| [#2688](https://github.com/nanocoai/nanoclaw/pull/2688) `fix(whatsapp)` | 2026-06-04 | 1天 | **高**：修复WhatsApp LID群组消息失败 |
| [#2685](https://github.com/nanocoai/nanoclaw/pull/2685) `docs(signal)` | 2026-06-04 | 1天 | **低**：文档更新，可稍后处理 |

积压总量尚在可控范围，但 #2405 和 #2459 的长期停滞可能拖慢功能交付节奏，建议本周内安排 Code Review。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 IronClaw (nearai/ironclaw) 项目数据生成的 2026-06-05 项目动态日报。

---

# IronClaw 项目日报 — 2026-06-05

## 1. 今日速览

今日项目活跃度极高，24小时内共有89次 Issue 与 PR 更新。核心工作集中在 **“Reborn”** 架构的重构与稳定性修复上，特别是围绕子代理（Subagent）、触发器（Trigger）和认证（OAuth）等关键模块的闭环问题修复与功能交付。社区与核心贡献者在解决持续性 Bug（如工具可见性、循环退出透明性）上高度一致，同时多个大型 PR（如 Slack 集成、WebUI 重做）完成了合并，标志着 Reborn 架构正从单一的功能开发向生产级稳定性和用户体验优化阶段迈进。待合并 PR 池（32个）仍维持高位，表明后续几天将有大量变更落地。

## 2. 项目进展

今日合并/关闭了多项重大功能与修复 PR，显著推进了 Reborn 架构的成熟度。

- **Reborn Slack 集成实现闭环**：PR #4476 ([链接](https://github.com/nearai/ironclaw/pull/4476)) 和 #4478 ([链接](https://github.com/nearai/ironclaw/pull/4478)) 成功合并，为 Slack 通道集成了完整的用户身份映射（actor/subject）、认证挑战提示以及运行时凭证注入，使 Slack 交互具备了完整的端到端能力。
- **核心循环与容错机制强化**：
    - PR #4440 ([链接](https://github.com/nearai/ironclaw/pull/4440)) 解决了 Agent 循环在遇到不稳定转写片段时硬错误的问题，引入了优雅的“暂缓-重试”机制。
    - PR #4466 ([链接](https://github.com/nearai/ironclaw/pull/4466)) 修复了触发器创建时的配对问题，确保创建者与触发器之间的事务完整性。
    - PR #4467 ([链接](https://github.com/nearai/ironclaw/pull/4467)) 为模型可见的 HTTP 工具结果引入了预算控制，防止输出过大导致模型调用失败。
- **WebUI v2 用户体验重构**：PR #4480 ([链接](https://github.com/nearai/ironclaw/pull/4480)) 和 #4477 ([链接](https://github.com/nearai/ironclaw/pull/4477)) 对 LLM 提供商设置面板进行了彻底的重构，引入了分组、折叠和清晰的配置状态标签，显著提升了用户配置体验。
- **安全问题修复**：PR #3719 ([链接](https://github.com/nearai/ironclaw/pull/3719)) 合并了多个依赖项的安全补丁，包括 `rustls-webpki` 和 `hyper`，修复了关键的拒绝服务和内容混淆漏洞。

> 项目通过一系列闭环修复，正将 Reborn 架构从“功能可用”推向“生产可用”，系统的鲁棒性和用户界面友好度均有显著提升。

## 3. 社区热点

今日讨论热度最高的 Issue 反映了社区对 **Reborn 架构可靠性和内部工作透明性**的强烈关注。

- **Issue #3280 - [Reborn] Add ProductWorkflow and InboundTurnService facade** ([链接](https://github.com/nearai/ironclaw/issues/3280))
    - 6条评论，是今日评论数最多的 Issue。
    - **分析**：该 Issue 是 Reborn 架构中“产品层”与“主机层”分离的关键设计讨论。它试图定义清晰的边界（ProductWorkflow），连接产品适配器与底层 Reborn 服务。高关注度表明社区期望项目能尽快完成架构重组，以减少模块间的耦合，提升代码可维护性和可扩展性。

- **Issue #4424 - Reborn: builtin.spawn_subagent advertised ... but absent from structured tools array** ([链接](https://github.com/nearai/ironclaw/issues/4424))
    - 4条评论，且已关闭。
    - **分析**：这是一个被快速发现并修复的严重 Bug。API 声明与模型实际看到的工具列表不一致，导致模型无法调用关键功能。社区的快速响应和修复体现了项目对模型交互正确性的重视，但也暴露了在“可见性”与“可用性”之间的一致性检查上存在漏洞。随后创建的 Issue #4431 ([链接](https://github.com/nearai/ironclaw/issues/4431)) 要求增加回归测试，正是对此类问题的制度化回应。

## 4. Bug 与稳定性

今日报告了多个影响系统稳定性和用户感知的 Bug，严重程度较高。

- **[严重]** Issue #4424 - `spawn_subagent` 工具对 OpenAI 兼容模型不可见。(已修复)
    - 这是核心功能 Bug。模型被告知可以使用某个工具，但实际调用时工具箱里却没有，导致模型行为异常。**PR #4466 和 #4350 等已包含相关修复。**
- **[严重]** Issue #4420 - 触发器 `CompleteAfterFirstFire` 策略被存储但从不执行。(待修复)
    - 导致用户创建的一次性触发器会无限循环执行，是严重的行为错误。**已创建 Tracking Issue #4475 监督修复。**
- **[高]** Issue #4427 - Reborn 循环退出原因（如达到迭代限制）对运维不可见。(待修复)
    - 用户和管理员无法通过日志看到 Agent 循环为何结束，严重阻碍了问题排查和性能调优。
- **[中]** Issue #4437 - 子代理完成结果分发缺乏持久化幂等性。(已关闭/跟踪中)
    - 引起潜在的结果重复分发或丢失。**该问题的解决方案被纳入更大的 Tracking Issue #4474。**
- **[中]** Issue #4084 - 后台子代理运行结果无法交付给父代理。(已修复)
    - 这是一个长期存在的 Bug，**PR #4348** 的合并使其得以解决。

## 5. 功能请求与路线图信号

结合今日的 Issue 和 PR，以下是用户/核心团队提出的关键新功能需求，极有可能被纳入近期规划。

- **长期运行的 Trigger 体系完善**：从 Issue #4473 (一次性运行支持)、#4472 (激活状态) 和 #4420 (完成策略) 以及相关的 **Tracking Issue #4475** 可以看出，项目的触发器系统正在从基础的定时任务向更精细的生命周期管理演变。**一次性运行**和**激活状态**是社区用户非常期待的产品特性。
- **第三方扩展与 Hook 激活**：PR #3951、#3938 等一揽子 PR（部分待合并）正在推进第三方的 Hook 扩展包在 Reborn 中安全激活。这标志着 IronClaw 生态系统建设的重要一步，允许社区贡献可安全运行的插件。
- **Reborn 代码结构治理**：出现多个关于代码解耦的 Issue，如 #4470 (重构 composition crate)、#4471 (运行时分解)、#4469 (工厂分解)。这反映出随着功能膨胀，核心团队开始重视代码架构的长期健康，主动提出重构以避免模块的无穷膨胀。**接下来可能会有更多关于创建独立 Crate 和强制执行模块边界的动作。**

## 6. 待处理积压

以下是一些长时间未关闭或状态可疑的 Issue/PR，可能需要维护团队关注。

- **PR #3951 ([链接](https://github.com/nearai/ironclaw/pull/3951))**：`[size: XL] feat(hooks): third-party extension hook activation...`。该 PR 创建于 5月23日，状态为 OPEN。它涉及一个重要的生态系统功能（第三方 Hook 激活），且依赖于其他 PR。它的持续 Open 状态可能成为其他相关功能（如 #3922, #3936）的阻塞点。建议发起者确认其依赖关系是否已就绪，或是否需要 rebase。
- **PR #3922 ([链接](https://github.com/nearai/ironclaw/pull/3922))**：`[size: XL] feat: wire SecurityAuditSink...`。同样创建于5月23日，状态 OPEN。作为 `hooks` 系列的一部分，其进展与 #3951 等 PR 的状态密切相关。维护者应评估该系列 PR 的整体推进计划，避免其中某个 PR 长期挂起导致其他工作的返工。

## 7. 用户反馈摘要

从近期的 Issue 评论和 Bug 报告中，可以提炼出以下用户反馈：

- **核心痛点**：模型行为的不可预测性（如 Issue #4424 中的工具不可调用）和难以理解系统内部状态（如 Issue #4427 中看不到循环退出原因）是用户当前最大的痛点。这直接影响了开发者在构建复杂 Agent 流程时的信心。
- **功能诉求**：对于不熟悉的用户，配置 LLM 提供商的过程过于复杂。近期对 WebUI v2 的重组（如 Provider 分组）正是对这一反馈的积极回应。同时，用户（尤其是在代码编辑器环境中）对一次性触发器（Trigger）的需求非常明确，以避免定时任务产生不期望的重复输出。
- **满意之处**：社区对 Bug 的修复速度（如 #4424 和 #4084）感到满意，这表明项目维护者对于破坏性问题的响应非常迅速和负责任。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 LobsterAI 开源项目分析师，我将根据您提供的数据，生成一份结构清晰、数据驱动的项目动态日报。

---

### LobsterAI 项目动态日报 (2026-06-05)

**分析师点评：** 项目今日表现出极高的维护活跃度。尽管没有新版本发布，但代码库在24小时内高效合并了16个Pull Request，重点关注核心的 **Cowork** 和 **MCP** 模块的稳定性增强与功能优化。这表明团队正积极响应社区反馈，并推进架构重构。唯一活跃的Issue是一个长期存在的启动问题，已获得社区关注。

---

#### 1. 今日速览

- **核心活跃度：高**。过去24小时内合并/关闭了16个PR，表明项目维护和开发迭代速度非常快，团队正集中精力进行代码合并与质量提升。
- **专注领域**：今日所有合并的PR几乎都围绕 **MCP（模型上下文协议）优化**、**Cowork（协作会话）功能增强与重构**、以及**OpenClaw网关的稳定性修复**。项目核心功能模块正在经历关键的打磨期。
- **社区互动**：社区讨论热度平稳，主要集中在单个长期存在的启动问题（Issue #769）上，该问题虽已开启数月，但最近仍有评论更新。
- **总体健康度：优秀**。大量PR被高效处理和合并，未发现新的严重Bug被报告，显示出项目代码质量和维护流程都处于良好状态。

#### 3. 项目进展

今日合并的16个PR标志着项目在**稳定性**和**用户体验**上迈出了重要一步。关键进展如下：

- **OpenClaw 网关稳定性与安全性提升**：
    - 合并了 `fix(cowork): guard oversized OpenClaw image payloads` (PR #2110)，检测并防止巨型图像负载导致网关失败。
    - 合并了 `fix(mcp): validate remote server urls` (PR #2103)，为远程MCP服务器增加了URL验证，防范配置错误。
    - 合并了 `fix(plugins): hide internal OpenClaw plugins` (PR #2096)，优化插件管理界面，隐藏内部插件以避免用户混淆。

- **MCP 核心功能优化**：
    - 合并了 `feat(mcp): optimize npx MCP launch resolution & add first response timing logs` (PR #2091)，通过预解析npx命令，大幅缩短了MCP服务器的启动时间，并增加了诊断日志，这是解决开发者痛点的重要改进。
    - 合并了 `fix(mcp): keep managed installs node-aware` (PR #2100)，确保以托管方式安装的MCP服务器能正确使用Node.js环境，解决了部分用户遇到的运行时问题。

- **Cowork 功能增强与重构**：
    - 合并了 `refactor(cowork): split voice input modules` (PR #2111)，对语音输入模块进行解耦，使代码结构更清晰，便于未来维护和功能扩展。
    - 合并了 `fix(cowork): support subagent batch deletion` (PR #2095)，优化了子代理会话的批量删除和清理逻辑。
    - 多个“陈旧（stale）”PR被合并，如为Cowork增加会话标签系统和书签功能的 `feat(cowork): 会话标签分类系统` (PR #1542) 和 `feat(cowork): 为AI回复消息添加收藏/书签功能` (PR #1538)，以及为会话完成状态增加系统通知的 `feat(cowork): Cowork 会话完成/失败时发送系统通知` (PR #1536)，这些功能显著提升了用户体验和内容管理能力。

#### 4. 社区热点

今日社区讨论最活跃的议题是Issue #769。

- **[Issue #769] OpenClaw 网关未能在规定时间内启动成功。**
    - **作者:** 15999803458-boop
    - **动态:** 该Issue于2026年3月创建，在昨日（2026-06-04）有最新评论更新。
    - **核心诉求:** 用户遇到了OpenClaw网关启动超时的问题，并附上了故障截图。这很可能是一个由**环境配置、网络问题或系统资源**引发的常见但棘手的问题。
    - **主要链接:** [Issue #769](https://github.com/netease-youdao/LobsterAI/issues/769)
    - **分析:** 虽然单个问题讨论热度不高，但此类启动问题通常是新用户或配置变更后最常遇到的障碍。问题的持续关注表明社区用户对稳定、可靠的启动体验有强烈需求。

#### 5. Bug 与稳定性

今日无新Bug报告，但大量修复了长期的稳定性问题。按严重程度排列如下：

- **严重（影响核心功能/崩溃）**：
    - **[已修复]** `fix(mcp): keep managed installs node-aware` (PR #2100): 修复了托管MCP安装的环境依赖问题，解决了实际QA日志中发现的故障。
    - **[已修复]** `fix(cowork): guard oversized OpenClaw image payloads` (PR #2110): 解决了超大图像会导致网关失败的问题，属于**关键稳定性修复**。

- **中等（影响特定功能/用户体验）**：
    - **[已修复]** `fix: enable image input support for MiniMax-M3` (PR #2093): 修复了MiniMax-M3模型不支持图像输入的硬编码错误（这是一个相对隐蔽的Bug）。
    - **[已修复]** `fix(mcp): validate remote server urls` (PR #2103): 阻止了用户输入无效远程MCP地址导致的问题。

- **低（UI/本地化/小瑕疵）**：
    - **[已修复]** 多个本地化修复PR (如 #1540, #1543, #1544) 处理了硬编码字符串、英文模式下显示中文、以及设置页面组件卸载时未清理轮询等问题。

**评估：** 项目在稳定性和Bug修复方面展现了很高的效率，所有本周报告的Bug都已迅速有对应的修复PR被合并。

#### 6. 功能请求与路线图信号

今日无新的功能请求Issue，但从已合并的PR中可以看出项目未来的发展方向：

- **开发者体验（DX）优先级高**：`feat(mcp): optimize npx MCP launch resolution` (PR #2091) 的合并，证明了团队将提升开发者部署和使用MCP的感受作为重要任务。
- **会话管理与个性化**：`feat(cowork): 会话标签分类系统` (PR #1542) 和 `feat(cowork): 为AI回复消息添加收藏/书签功能` (PR #1538) 的合并，表明**用户体验**和**会话数据管理**是当前迭代的重点。
- **架构重构进行中**：`refactor(cowork): split voice input modules` (PR #2111) 的合并，预示着后续可能会对语音输入等复杂功能进行更深度的优化和扩展。

**路线图信号：** 下一次版本发布很可能侧重于优化MCP生态和增强Cowork的会话管理功能。

#### 7. 用户反馈摘要

今日仅从一个活跃Issue中提取到用户反馈：

- **用户痛点**: **配置/环境问题。** 用户在 Issue #769 中遇到了OpenClaw网关启动失败的问题，并详细附上了截图。虽然问题本身尚不明确，但表明**用户在上手和使用过程中，环境的复杂性和配置的正确性是一个挑战**，尤其是在涉及到网络和本地服务（如OpenClaw）时。
- **满意点**: 无直接不满反馈。大量PR的快速合并，尤其是对启动速度优化和模型支持修复，可能会在下次发布后得到用户的积极评价。

#### 8. 待处理积压

- **[Issue #769] OpenClaw 网关未能在规定时间内启动成功。**
    - **风险:** 该Issue自3月份开启，虽然昨日有评论，但至今无官方回复或明确的解决方案。作为一个影响用户上手的核心问题，长期积压可能影响新用户的留存率和社区口碑。
    - **链接:** [Issue #769](https://github.com/netease-youdao/LobsterAI/issues/769)
    - **建议:** 维护者应尽快响应此Issue，询问用户更详细的系统环境（如网络、杀毒软件、防火墙配置等），或提供标准化的排查脚本/步骤。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是为您生成的 Moltis 项目动态日报。

---

# Moltis 项目动态日报 | 2026-06-05

**项目名称:** Moltis
**数据来源:** github.com/moltis-org/moltis
**分析日期:** 2026-06-05

---

### 1. 今日速览

今日 Moltis 项目处于稳定的维护与功能迭代阶段，社区贡献活跃。过去 24 小时内，有 2 个新 Issue 被提交，分别涉及本地语音识别引擎的集成和新的通信渠道支持；同时，有 3 个 Pull Request 处于待合并状态，其中两个针对浏览器工具对 Shadow DOM 的支持优化，反映了对 Web 组件兼容性的技术深耕。项目整体活跃度高，社区需求与技术改进并进，但暂无新版本发布。

### 2. 版本发布

无。

---

### 3. 项目进展

今日无合并或关闭的 PR。但有 3 个重要 PR 仍处于开放/待合并状态，推动了以下方向的技术改进：

- **Shadow DOM 兼容性修复 (PR #1103 / #1100):** 这是今日技术讨论的焦点。贡献者 `s-salamatov` 和 `resumeparseeval` 提交了两个高度相关的 PR，旨在修复浏览器自动化工具在遇到 Web 组件 (`Shadow DOM`) 时无法正确查找元素的问题。`#1100` 提出了解决方案，而 `#1103` 在此基础上进行了代码优化和审查修复。该修复对于支持基于 Web 组件的现代 Web 应用（如 Salesforce）至关重要。
    - [PR #1100 链接](https://github.com/moltis-org/moltis/pull/1100)
    - [PR #1103 链接](https://github.com/moltis-org/moltis/pull/1103)
- **会话历史管理优化 (PR #1089):** `s-salamatov` 还提交了另一个优化，旨在对会话恢复（rehydration）时工具结果的体积进行限制，避免内容过长导致问题。这是一个面向稳定性和性能的内部改进，涉及聊天、流式聊天、记忆压缩等多个核心流程。
    - [PR #1089 链接](https://github.com/moltis-org/moltis/pull/1089)

### 4. 社区热点

尽管今日的 Issues 和 PRs 评论数为 0，但以下两个 Issue 和两个 PR 代表了社区最强烈的两类诉求：

1.  **本地 STT 引擎集成诉求 (Issue #1102):** 用户 `LauraGPT` 提议集成 `FunASR` 或 `SenseVoice` 作为本地语音转文字引擎，强调其超低延迟（SenseVoice-Small 处理10秒音频仅需约70ms）和原生流式支持。这反映了社区对**隐私保护**和**高性能本地 AI 能力**的渴望，是向离线优先体验迈进的强烈信号。
    - [Issue #1102 链接](https://github.com/moltis-org/moltis/issues/1102)
2.  **跨平台渠道扩展需求 (Issue #1101):** 用户 `joeblew999` 请求增加 SMS 和 LINE 作为新的通信渠道。这表明社区不仅将 Moltis 视为一个语音助手，更希望其成为一个**跨平台、多渠道的统一通信代理**。
    - [Issue #1101 链接](https://github.com/moltis-org/moltis/issues/1101)
3.  **技术债务修复 (PR #1100 & #1103):** 这两份针对 Shadow DOM 的 PR 是技术社区关注的热点，虽然无讨论，但它们解决了 Web 自动化中的一个普遍痛点，预计合并后将显著提升 Moltis 浏览器工具在复杂 Web 应用上的实用性。

### 5. Bug 与稳定性

今日没有明确的 Bug 或崩溃报告。

- **稳定性改进:**
    - **待合并 - 会话恢复崩溃预防 (PR #1089):** 该 PR 通过对工具结果实施容量限制，直接预防了因持久化数据过大而在会话恢复时可能出现的异常或性能问题，属于重要的稳定性提升。

### 6. 功能请求与路线图信号

结合今日的 Issues 和活跃的 PRs，项目的未来路线图信号清晰：

- **短期 (可能性高):**
    - **Web 组件兼容性增强 (Shadow DOM):** 两个待合并的 PR 是强烈信号。一旦合并，Moltis 浏览器工具的功能完整性和可靠性将大幅提升。此功能很可能包含在下一个维护性版本中。
    - **会话历史稳定性优化:** PR #1089 的优化方案相对独立，亦有很大可能随下一个版本发布。

- **中期 (社区呼声高，有待评估规划):**
    - **离线/本地 AI 能力增强:** Issue #1102 提出的本地 STT 引擎，与 Moltis 的 “个人助手” 定位高度契合。集成此类引擎将是实现全本地、低延迟语音交互的关键一步。
    - **多渠道通信支持:** Issue #1101 提出的 SMS 和 LINE 支持，预示着项目从“语音助手”向“全能消息代理”的进化方向。

### 7. 用户反馈摘要

今日无直接的用户评论，但从 Issue 内容可提炼出如下用户痛点与期望：

- **痛点:** 对第三方云 STT 服务（如 Azure、Google）的依赖可能带来隐私和延迟问题。用户 `LauraGPT` 的提议直接指向此痛点。
- **期望场景:** 用户 `joeblew999` 希望能将 Moltis 的能力扩展到日常高频使用的短信（SMS）和 LINE 上，表明他们期望一个能够整合碎片化通信的统一入口。
- **满意点:** 用户 `LauraGPT` 在提出 Issue 时开篇即称赞 “Great voice assistant project!”，表明现有项目质量获得了用户好评。

### 8. 待处理积压

以下是一个需要维护者关注的长期未响应 PR：

- **PR #1089: “Cap persisted tool results before rehydration”**
    - 创建于 2026-06-01，至今已 4 天未获合并或明确反馈。此 PR 涉及多个核心流程的稳定性改进，应及时进行 Review 或提供指导。
    - [PR #1089 链接](https://github.com/moltis-org/moltis/pull/1089)

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 CoPaw (github.com/agentscope-ai/CoPaw) 项目数据，现为您呈上 2026-06-05 的项目动态日报。

---

# CoPaw 项目日报 | 2026年06月05日

## 今日速览

今日 CoPaw 项目继续保持高活跃度，共处理了 32 条 Issue 和 33 条 PR，并发布了 v1.1.11-beta.1 版本。社区中，关于上下文压缩崩溃（`/compact`）和 DeepSeek 回复显示异常等问题讨论热烈，是用户当前的关注焦点。项目维护者响应迅速，不仅修复了多个关键 Bug（如 MCP 工具名兼容性、聊天列表加载失败），还在核心功能上取得了重要进展，例如新增子代理工具和推进前端单元测试覆盖。整体而言，项目处于健康、积极的发展轨道。

## 版本发布

### v1.1.11-beta.1
- **发布链接**: [v1.1.11-beta.1](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.11-beta.1)
- **更新内容**:
    - **修复**: 为 `ProviderManager` 添加了回退逻辑，解决了 `get_model_max_input_length` 在某些情况下无法获取模型配置的问题 (#4827)。
    - **重构**: 禁用了类型为 `agent` 的定时任务（Cron Job）的“推送气泡”功能，优化了任务执行体验 (#4803)。
- **破坏性变更**: 无。
- **迁移注意事项**: 建议用户升级到此版本以获取最新的模型配置兼容性与 Cron 任务优化。

## 项目进展

过去 24 小时内，项目在核心功能、稳定性和测试方面均取得了显著进展，有多项重要 PR 被合并。

- **核心功能增强**:
    - [PR #4806](https://github.com/agentscope-ai/QwenPaw/pull/4806) 合并：新增 `spawn_subagent` 工具，允许主 Agent 在工作区内生成临时的子 Agent 执行子任务，丰富了 Agent 间的协作模式。
    - [PR #4879](https://github.com/agentscope-ai/QwenPaw/pull/4879) 合并：增强了飞书 (Feishu) 渠道的消息解析能力，现在支持提取互动卡片中的文本内容。
    - [PR #4848](https://github.com/agentscope-ai/QwenPaw/pull/4848) 合并：为 QQ 频道渠道添加了扫码授权功能，简化了配置流程。

- **稳定性与兼容性修复**:
    - [PR #4958](https://github.com/agentscope-ai/QwenPaw/pull/4958) 合并：修复了当 MCP 工具名包含特殊字符（如点 `.`）时，因不符合 OpenAI/Anthropic API 命名规范而导致调用失败的问题。
    - [PR #4900](https://github.com/agentscope-ai/QwenPaw/pull/4900) 开启：旨在修复 Tauri 桌面版在 PyInstaller 环境下插件加载失败和桌面宠物启动异常的问题，预计将极大改善桌面用户体验。

- **其他重要变更**:
    - [PR #4332](https://github.com/agentscope-ai/QwenPaw/pull/4332) 合并：完成了前端单元测试里程碑，新增了 10 个测试文件和约 100 个测试用例，覆盖了 constants, contexts, layouts, api-types, components 等模块，提升了代码健壮性。

## 社区热点

- **热点 Issue #1**: **[Bug] Console UI: tool calls often not displayed until page refresh** (#4644)
    - **链接**: [Issue #4644](https://github.com/agentscope-ai/QwenPaw/issues/4644)
    - **热度**: 20 条评论，是过去24小时内讨论最热烈的问题。
    - **诉求分析**: 用户报告了一个影响“开箱即用”体验的严重问题：控制台 Web UI 无法实时显示大部分工具调用结果，必须手动刷新页面才能看到，且无任何错误日志。该问题直接影响了用户对 Agent 执行流程的可观察性，社区关注度极高。

- **热点 Issue #2**: **[Bug] context compact fails: 'str' object has no attribute 'get'** (#4956) & **Bug: /compact crashes with 'str' object has no attribute 'get'** (#4953)
    - **链接**: [Issue #4956](https://github.com/agentscope-ai/QwenPaw/issues/4956) & [Issue #4953](https://github.com/agentscope-ai/QwenPaw/issues/4953)
    - **热度**: 两个相似 Issue 合计产生 4 条评论，且出现时间非常接近。
    - **诉求分析**: 这是一个社区刚刚集中暴露出的 Bug，当消息内容 `content` 字段包含混合类型的列表（如既有纯字符串又有字典）时，执行上下文压缩 (`/compact`) 会直接崩溃。这说明新引入的消息结构在某些边缘情况下存在处理漏洞，社区维护者需要快速跟进修复。

## Bug 与稳定性

| 严重程度 | Bug 描述 | Issue/PR 链接 | 状态 | 已有 Fix PR? |
| :--- | :--- | :--- | :--- | :--- |
| **高** | **上下文压缩 (`/compact`) 崩溃**: 当消息 `content` 为混合类型列表时，引发 `'str' object has no attribute 'get'` 错误。 | [#4956](https://github.com/agentscope-ai/QwenPaw/issues/4956), [#4953](https://github.com/agentscope-ai/QwenPaw/issues/4953) | **未关闭** | 无 |
| **高** | **DeepSeek 回复折叠到思考过程**: 使用 DeepSeek API 时，实际回复内容被错误地折叠在“思考过程”板块内，需要额外一步才能展开查看。 | [#4962](https://github.com/agentscope-ai/QwenPaw/issues/4962) | **未关闭** | 无 |
| **中** | **Agent 执行陷入死循环无法退出**: 用户报告 Agent 在任务执行过程中陷入无限循环，无法终止。 | [#4967](https://github.com/agentscope-ai/QwenPaw/issues/4967) | **未关闭** | 无 |
| **中** | **Latex 公式显示异常**: 用户在控制台中发现 Latex 公式渲染存在问题。 | [#4959](https://github.com/agentscope-ai/QwenPaw/issues/4959) | **未关闭** | 无 |
| **低** | **`/compact` 命令忽略模型 `max_input_length`**: `/compact` 命令仍使用 128K 默认值，而非从模型配置中读取的 512K 设置。 | [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937) | **未关闭** | 无 |
| **已修复** | **MCP 工具名包含点号 `.` 导致调用失败**: 因不满足 OpenAI/Anthropic 的 `name` 字段正则校验。 | [#4918](https://github.com/agentscope-ai/QwenPaw/issues/4918) | **已关闭** | [#4958](https://github.com/agentscope-ai/QwenPaw/pull/4958) (已合并) |

## 功能请求与路线图信号

昨日用户提出的新功能需求主要围绕 Agent 的自主性和用户控制力，结合已有 PR，以下功能请求有较高概率被纳入后续版本：

1.  **中断 Agent 执行**: 用户 `feng183043996` 连续提交了两个 Issue ([#4961](https://github.com/agentscope-ai/QwenPaw/issues/4961), [#4964](https://github.com/agentscope-ai/QwenPaw/issues/4964))，强烈要求在用户发送新消息时能够中断正在执行的 Agent。这是一个提升交互控制感的普适性需求，与 `spawn_subagent` (PR #4806) 等增强 Agent 自主性的功能相辅相成。
2.  **Cron 任务支持直接执行脚本**: 同样由 `feng183043996` 提出的增强功能 ([#4950](https://github.com/agentscope-ai/QwenPaw/issues/4950), [#4963](https://github.com/agentscope-ai/QwenPaw/issues/4963))，希望在定时任务中增加直接执行 Shell 脚本的类型，而无需经过 AI Agent 处理。这拓宽了 Cron 功能的应用场景。
3.  **Provider 自动降级**: 用户 `ziyu-code` 提出的需求 ([#4757](https://github.com/agentscope-ai/QwenPaw/issues/4757))，希望内置 Provider 自动降级机制，当主 LLM Provider 达到 Token/速率限制时能自动切换到备份 Provider。这在追求高可用性的场景下非常实用。
4.  **会话 Token 使用信息可视化**: 多个 Issue ([#4767](https://github.com/agentscope-ai/QwenPaw/issues/4767), [#4782](https://github.com/agentscope-ai/QwenPaw/issues/4782)) 希望在前端界面显示当前会话的 Token 使用量和上下文大小。而 [PR #4433](https://github.com/agentscope-ai/QwenPaw/pull/4433) 正是为此功能而设计，目前尚在开启状态，预计将被推进并合并。

## 用户反馈摘要

- **对记忆系统的“只记录不学习”感到不满**：用户 `feng183043996` 在 Issue #4652 中详细描述了当前记忆系统“信息堆砌”的问题，认为 Agent 只会记录而不会总结、关联和提炼知识，导致用户“踩了坑还会再踩”。这是一个对 AI Agent 学习能力有较高期望的典型反馈。
- **对生成文件缺乏快捷操作表示困扰**：用户 `rescodexa` 在 Issue #4786 中反馈，Agent 生成 Word/PPT 文件后，没有提供快捷打开或定位文件的入口，用户需要手动在文件管理器中查找，体验不够流畅。他希望至少能提供一键打开文件或所在文件夹的功能。
- **对 Provider 配置界面提出优化建议**：用户在 Issue #4765 中建议，将同一品牌（如智谱）的多个 Provider 卡片合并，并通过下拉菜单选择具体套餐/端点，以减少界面混乱。这反映了用户对更简洁、更强大的配置界面的需求。

## 待处理积压

- **DeepSeek 前缀缓存命中率优化** (#3891)：该 Issue 已存在一个多月，提出了一个具有重大成本效益的问题。虽然更新至昨日，但尚未有具体的解决方案或 PR 跟进，建议项目维护者评估其优先级，特别是对于大量使用 DeepSeek 模型的用户。
- **前端单元测试里程碑后续** (#4330)：虽然对应 PR #4332 已合并，但该 Issue 本身尚未关闭。建议确认所有计划内的测试模块是否均已覆盖，然后及时关闭该 Issue。
- **长期未响应的功能请求**: 例如 `Token Information Each Session` (#4767) 等，虽然已有相关 PR (#4433) 在推进，但 Issue 本身处于开放状态，建议维护者在该 PR 合并后统一更新或关闭这些关联 Issue，以避免信息混乱。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目日报 — 2026-06-05

---

## 1️⃣ 今日速览

过去24小时项目活跃度较高：共处理 **32 条 Issues**（新开/活跃 27，关闭 5）和 **50 条 PR**（待合并 35，已合并/关闭 15）。虽无新版本发布，但多个高优先级 bug 被修复（Ollama 编译恢复、Windows Shell 双引号问题、Twitter 频道缺失等），同时涌现了若干高风险 RFC（结构化可观测性、A2A 发现、计算机操控），社区对互操作性和安全性的需求日益强烈。v0.8.0/v0.8.1 两条发布线均在密集推进，整体项目健康度良好，但 PR 积压量较大需维护者关注。

---

## 2️⃣ 版本发布

今日无新版本发布。

---

## 3️⃣ 项目进展

以下为今日合并/关闭的重要 PR 和 Issues，代表了项目在稳定性和功能上的实质性推进：

- **🚀 [PR #7231] fix(ollama): restore compiling master build**  
  修复因 PR #7095 合并后导致 `master` 分支无法编译的回归问题，Ollama Provider 恢复可构建状态。  
  [链接](https://github.com/zeroclaw-labs/zeroclaw/pull/7231)

- **🚀 [Issue #7083] [CLOSED] Bug: Windows shell tool mangles commands containing double quotes**  
  修复 Windows 下 shell 工具处理包含双引号的命令时因 cmd.exe 转义错误导致 S1 级工作流阻塞的问题。  
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7083)

- **🚀 [Issue #7069] [CLOSED] Bug: Twitter/X channel not available in pre-built binary**  
  解决了 `channel-twitter` 功能在预编译二进制中未开启的文档与实际不符问题，现已包含在正式构建中。  
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7069)

- **🚀 [Issue #7179] [CLOSED] Bug: ZeroClaw Reaps Idle RPC Sessions at 10 Minutes**  
  修复了闲置会话 10 分钟即被回收导致工作流中断的 S1 级 bug，现已调整为合理超时策略。  
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7179)

- **🚀 [Issue #5962] [CLOSED] Bug: Ollama Provider call failed when tools are needed**  
  修复 Ollama Provider 在需要工具调用时抛错并阻塞同一会话后续消息的问题。  
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)

此外，多个新功能 PR 已提交待审核（详见后文路线图信号），项目正向 v0.8.0 稳定版迈进。

---

## 4️⃣ 社区热点

以下 Issues/PR 在今日讨论最为活跃，反映了社区的核心关注点：

- **#3566 [Feature] A2A (Agent-to-Agent) Protocol Support**  
  评论 5，👍 7（今日所有 Issue 中最高赞）。社区对跨代理通信协议的需求极为迫切，该 issue 自 3 月提出以来持续收到关注，目前状态为 `blocked`，等待维护者审查。  
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/3566)

- **#6909 [Feature] computer-use support (screen interaction like Codex / Peekaboo)**  
  评论 5。用户强烈希望 ZeroClaw 能像 OpenAI Codex 一样控制桌面 GUI，该功能已被接受（status:accepted），是 v0.8.0 路线图上的高优先级特性。  
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6909)

- **#7069 [CLOSED] Bug: Twitter/X channel not available in pre-built binary**  
  虽然已关闭，但关闭前获得 3 条评论，用户对预构建二进制与文档不一致表达不满，社区对“开箱即用”体验非常敏感。  
  [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/7069)

分析：用户群体对**互操作性**（A2A）、**高级GUI操控**（computer-use）以及**配置易用性**（预构建功能完整性）有强烈诉求。

---

## 5️⃣ Bug 与稳定性

今日报告的 Bug 按严重程度排列，并标注是否已有修复 PR：

| 严重级别 | Issue ID | 描述 | 状态 | 修复 PR |
|----------|----------|------|------|---------|
| **S1 - workflow blocked** | #7227 | zerocode Quickstart 硬编码 `default` 别名，与已有 provider 冲突 | OPEN | 无 |
| **S1 - workflow blocked** | #7125 | TUI (zerocode) 在 daemon 断连时完全冻结 | OPEN | 无 |
| **S1 - workflow blocked** | #7179 | 闲置 RPC 会话 10 分钟回收 | CLOSED | 已修复 |
| **S1 - workflow blocked** | #7083 | Windows shell 双引号转义错误 | CLOSED | 已修复 |
| **S2 - degraded behavior** | #7225 | WhatsApp Web `mention_only` 忽略对机器人消息的回复 | OPEN | 无 |
| **S2 - degraded behavior** | #7126 | Web UI "Clear all" 仅清除前端，后端 session 未清理 | OPEN | PR #7222 已提交 |
| **S2 - degraded behavior** | #7143 | Agent 重复执行近似的 shell discovery 命令直到耗尽迭代次数 | OPEN | 无 |
| **S2 - degraded behavior** | #7151 | Observability telemetry 泄漏到聊天 WS，渲染永久 "unknown" 工具卡片 | OPEN | PR #7221 已提交 |

**分析**：S1 级 bug 今日有明显好转（关闭了 3 个），但新开了 2 个（#7227、#7125），仍需紧急处理。Web UI 相关的 S2 级 bug 已有对应的修复 PR 进入审核，有望在 v0.8.0 前解决。

---

## 6️⃣ 功能请求与路线图信号

今日新提出的功能需求及 RFC 中，以下可能被纳入下一版本：

| Issue ID | 功能描述 | 风险 | 对应 PR 或状态 |
|----------|----------|------|----------------|
| #7232 | 结构化可观测性增强：丰富事件上下文、OTel 链路关联、桥接重构 | 高 | PR #7233 已提交 |
| #7228 | 为 Azure OpenAI 专用 provider 添加 `reasoning_effort` 支持 | 低 | 无 |
| #7218 | A2A agent 发现机制（`.well-known/agent-card.json`） | 中 | 无 |
| #7155 | 高风险 shell 命令的每执行确认层级 + 命令模式策略（allow/ask/deny） | 高 | 无 |
| #7100 | 每模型可配置 `vision` 和 `context_window` 能力 | 高 | 无 |
| #6909 | 计算机控制（截图+鼠标键盘事件） | 高 | 已接受（accepted） |
| #5907 | LSP 支持以提升代码生成质量 | 高 | 状态 blocked |

此外，**#7230** 将 UI 中的 "Scheduled Jobs" 重命名为 "Automations"（低风险，已提 PR），**#7229** 新增 MCP、Skills、Plugins & Providers 管理面板（高价值，PR 已提交）。

**路线图信号**：v0.8.0 追踪 issue #7112 和 v0.8.1 追踪 issue #6970 均处于活跃状态，表明团队正在集中处理稳定性和插件化架构。安全性与可观测性成为本轮开发的两大主题。

---

## 7️⃣ 用户反馈摘要

从 Issues 评论中提取的真实用户声音：

- 🔴 **#7143** — "We are seeing a ZeroClaw Slack-connected coding agent hit `max_tool_iterations` because it repeatedly calls `shell` with near-duplicate commands."  
  用户反馈 Slack 场景下 agent 陷入重复执行类似 shell 命令的死循环，直到迭代上限耗尽。期望更智能的去重或缓存机制。

- 🟡 **#7227** — "The zerocode TUI Quickstart hardcodes the new model-provider alias to `default` and never exposes it for editing."  
  用户在初始化时因别名冲突导致工作流阻塞，暴露了新手引导中配置灵活性不足的问题。

- 🟢 **#7069** — "Twitter/X channel not available in pre-built binary despite channel-twitter feature existing."  
  用户发现文档声称支持但实际不可用，强调可执行文件应默认开启所有已实现的通道。

- 🟢 **#7179** — "After the last prompt turn in a Chat or Code session, ZeroClaw starts counting down from 600 seconds. If there have been no prompt turns in that time, ZeroClaw reaps the session."  
  用户对 10 分钟空闲回收感到困惑，认为应保持会话持久或提供更长的超时配置（该问题已修复）。

- 🔴 **#7211** — "The repo is huge as hell."（附带截图显示 1.32 GiB）  
  用户抱怨仓库体积过大，建议清理构建产物或使用 git LFS。

**总体评价**：用户对 Rust 实现的高性能表示赞赏（#7143 中 "great to see a Rust-based agent runtime that is much lighter on resources"），但配置易用性和稳定性仍需改善。

---

## 8️⃣ 待处理积压

以下为长时间未响应或状态阻塞的重要 Issue/PR，建议维护者优先关注：

| 编号 | 类型 | 标题 | 创建时间 | 最后更新 | 风险 | 备注 |
|------|------|------|----------|----------|------|------|
| #3566 | Feature | A2A 协议支持 | 2026-03-15 | 2026-06-04 | 高 | 7 👍，状态 blocked，需维护者决策 |
| #5907 | Feature | LSP 支持 | 2026-04-19 | 2026-06-04 | 高 | 状态 blocked，依赖架构决策 |
| #6074 | Enhancement | 追踪 153 个遗失提交的恢复 | 2026-04-24 | 2026-06-04 | 高 | in-progress，但进展不明 |
| #5797 | PR | 为自定义推理 provider 添加 `tls_ca_cert_path` | 2026-04-16 | 2026-06-05 | 高 | 未合并，企业用户强烈需求 |
| #6970 | Tracker | v0.8.1 集成/通道/provider/tool PR 队列 | 2026-05-27 | 2026-06-05 | 中 | 追踪 issue，长期未关闭 |
| #7112 | Tracker | v0.8.0 发布队列和 Stable-tier 阻塞项 | 2026-06-02 | 2026-06-04 | 高 | 对发布计划至关重要 |
| #7227 | Bug | Quickstart 硬编码 alias 冲突 | 2026-06-04 | 2026-06-04 | S1 | 新开，无任何响应 |
| #7125 | Bug | TUI 断连冻结 | 2026-06-03 | 2026-06-04 | S1 | 新开，需快速修复 |

**特别提醒**：PR #5797（TLS 证书路径支持）已搁置近两个月，影响了使用私有 CA 的企业用户部署；Issue #3566（A2A）作为社区呼声最高的特性，其阻塞状态应尽快通过 RFC 讨论解除。

---

*本日报基于 GitHub 公开数据自动生成，仅供参考。所有链接均指向原始 Issue/PR。*

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*