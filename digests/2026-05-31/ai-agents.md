# OpenClaw 生态日报 2026-05-31

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-05-31 06:56 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 OpenClaw GitHub 数据，生成 2026-05-31 的项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-05-31

### 1. 今日速览

今日 OpenClaw 项目社区异常活跃，24小时内产生了 500 条 Issue 和 500 条 PR 更新，并发布了 2 个新版本。Issue 关闭率（129/500）与 PR 合并率（72/500）均处于较高水平，表明项目维护与修复工作推进迅速。社区焦点集中在**渠道稳定性**（飞书、Telegram、Discord）、**Codex 运行时恢复**以及**代理（Agent）会话管理**上。尽管新提交的 PR 数量庞大（待合并高达 428 条），但核心维护者处理关键问题的效率很高，项目整体健康度良好。

### 2. 版本发布

- **[v2026.5.30-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.5.30-beta.1):** 本次发版专注于提升系统稳定性和恢复能力。
    - **Agent & CLI 运行时：** 修复了因中断的工具调用、过期会话绑定、预压缩（compaction）交接以及媒体投递重试导致的崩溃或恢复不干净问题。
    - **渠道稳定性：** 增强了 Telegram、WhatsApp、iMessage、Slack 等渠道的消息投递可靠性。


- **[v2026.5.28](https://github.com/openclaw/openclaw/releases/tag/v2026.5.28):** 本次发版同样专注于运行时恢复。
    - **Agent & Codex：** 强化了子代理（subagent）与工作目录（cwd）的隔离、Hook 上下文的本地性、会话锁的超时释放机制，并修复了 Codex 应用服务器/助手初始化失败的问题。

### 3. 项目进展

今日合并/关闭了一些重要的 PR，显著推进了项目的稳定性和功能边界。

- **运行时状态重构：** 将运行时状态迁移到 SQLite 的里程碑式 PR `#81402` 仍在推进中，虽暂未合并，但后续的 `refactor(telegram): persist plugin state in sqlite` (PR `#88469`) 展示了基于该架构下 Telegram 渠道的阶段性成果，通过将插件状态存储到 SQLite 替代 JSON 文件，提升了数据一致性和可靠性。
- **新渠道支持：** 新提出的 `feat: add Twilio SMS channel` (PR `#88476`) 为项目带来了短信渠道的初步支持。该 PR 代码量大（XL），但框架清晰，为未来扩展多种渠道奠定了基础。
- **操作控制增强：** `feat: improve MCP operator controls` (PR `#88536`) 为 MCP 引入了诊断、状态查询和注销等 CLI 控制命令，并新增了专属的 UI 设置页面，大幅提升了用户对 MCP 工具的管理和调试能力。
- **关键 Bug 修复：** 核心维护者合并了针对 Discord 会话内回复投递 (PR `#87179`)、Mattermost 文本块边界处理 (PR `#87449`) 和 iMessage 媒体附件路由 (PR `#87904`) 等多个关键问题的修复。这些修复直接解决了用户报告的渠道交互核心痛点。

### 4. 社区热点

以下 Issue 和 PR 因其高讨论度和点赞量，成为今日社区热点：

1.  **`#87395`** [CLOSED] [Native hook relay intermittently becomes unavailable on 2026.5.26](https://github.com/openclaw/openclaw/issues/87395) (评论: 14, 👍: 8)
    - **诉求：** 用户升级到 v2026.5.26 后，macOS 上的原生 Hook 中继间歇性不可用，导致内存/文件系统工具被阻塞。该问题严重影响了开发者的本地工作流，引发了强烈反响。
    - **分析：** 社区对版本升级的稳定性极为敏感，尤其是直接影响开发效率的核心运行时功能。

2.  **`#87646`** [CLOSED] [[BUG] cannot dispatch messages after v2026.5.27 upgrade](https://github.com/openclaw/openclaw/issues/87646) (评论: 12, 👍: 1)
    - **诉求：** 用户升级后，飞书（Feishu）渠道完全无法投递消息，报错 `TypeError: Cannot read properties of undefined (reading 'run')`。
    - **分析：** 渠道是用户与 Agent 交互的入口，任何渠道的完全失效都会导致业务中断。该问题被标记为 P1 级，体现了社区对飞书渠道高可靠性的需求。

3.  **`#78308`** [OPEN] [[Feature]: Channel-mediated approval for MCP tool calls](https://github.com/openclaw/openclaw/issues/78308) (评论: 11, 👍: 1)
    - **诉求：** 用户希望 MCP 服务器的工具调用（如发送邮件、写数据库）能像 shell 执行一样，集成到 OpenClaw 现有的渠道审批（approval）管道中。
    - **分析：** 这是一个长期存在的功能需求，社区对其讨论不减。它反映了用户对 MCP 安全管控的深层渴望，被认为是将 MCP 用于生产环境的关键一步。

### 5. Bug 与稳定性

今日报告了多个严重的 Bug 和回归问题，主要集中在会话状态、渠道兼容性和运行时稳定性。

| 严重程度 | Issue 编号与摘要 | 是否有 Fix PR？ |
| :--- | :--- | :--- |
| **P1 (Platinum Hermit)** | [#88020](https://github.com/openclaw/openclaw/issues/88020) [Bug] Anthropic ‘Invalid signature in thinking block’ 导致硬性会话失败，而非重试 | 是，[PR #88407](https://github.com/openclaw/openclaw/pull/88407) (codex continuity fix) |
| **P1 (Platinum Hermit)** | [#87016](https://github.com/openclaw/openclaw/issues/87016) [Bug] 预压缩（Preflight compaction）死锁：空会话边缘情况导致消息被反复退回 | 已关闭 |
| **P1 (Platinum Hermit)** | [#86239](https://github.com/openclaw/openclaw/issues/86239) [Bug] 事件循环饥饿下，已注册的 Harness 报错 MissingAgentHarnessError | 已关闭 |
| **P1 (Diamond Lobster)** | [#88443](https://github.com/openclaw/openclaw/issues/88443) [Bug] `auth.cooldowns` 配置变更强制重启 Gateway，导致正在运行的 CLI 任务被丢 | 是，[PR #88329](https://github.com/openclaw/openclaw/pull/88329) (fallback fix) |
| **P1 (Diamond Lobster)** | [#87736](https://github.com/openclaw/openclaw/issues/87736) [Regression] 预压缩仍报告缺失 Codex 线程故障 | 有相关 PR |
| **P1 (Diamond Lobster)** | [#87646](https://github.com/openclaw/openclaw/issues/87646) [BUG] 飞书渠道升级后无法发送消息 | 已关闭 |
| **P2 (Diamond Lobster)** | [#87436](https://github.com/openclaw/openclaw/issues/87436) [Bug] Codex 任务会在 doctor --fix 后重建旧的遗留路由状态 | 已关闭 |

**总结：** 今日 Bug 修复的重点在于**会话状态的完整性**（避免死锁、丢失上下文、错误恢复）和**主流渠道的稳定性**（避免因升级或配置变更导致服务中断）。多个 P1 级回归问题 (Regressions) 的出现，提示项目在快速迭代中可能忽视了部分边缘情况，需加强回归测试。

### 6. 功能请求与路线图信号

- **`#78308`** **MCP 工具调用审批（Approval）：** 该功能需求呼声极高，是社区最渴望的安全管控特性。虽然暂无直接合并的 PR，但 `#88536` (MCP operator controls) 的提出，表明维护团队正在积极地系统性地增强 MCP 的用户体验和控制能力，该特性有可能在接下来的一两个版本中作为重点推进。
- **`#79458`** **斜杠命令 i18n 支持：** 非英语用户对命令描述本地化的需求再次被提出。目前尚无对应的实现性 PR，但考虑到项目日益增长的全球用户基础，这是一个明确的社区信号。结合 `#79034` (UI元数据本地化) 等 Issue，**本地化 (i18n)** 正在成为一个被多次提及的路线图信号。
- **语音功能增强：** `#73699` (Discord 语音通道转文字) 是一个典型的提升用户体验的需求。它描述了当前语音对话与文本会话隔离带来的割裂感，用户期望将语音输入融入主文本流中。这可能是一个潜在的 Roadmap 方向，以弥合多模态交互的体验差距。

### 7. 用户反馈摘要

- **痛点：版本升级的伴随风险。** 多起 Bug（如 `#87646` 飞书失效、`#87395` Hook 中断）都发生在版本升级后，用户抱怨“升级即出问题”。社区对“升级稳定性”和“降级/回滚能力”有强烈诉求。
- **场景：多账号/多渠道的复杂管理。** 多个 Issue (`#77359`、`#78082`) 聚焦于多 Discord 账号、多 Telegram bot 的配置和管理复杂性，例如斜杠命令注册不全、配置冲突等。这表明用户正在将 OpenClaw 部署到更复杂、更大规模的生产环境中。
- **满意度：关键问题的修复速度受到认可。** 尽管报错多，但许多 P1 级严重 Bug 在短时间内被关闭或已有 Fix PR，用户对维护团队的响应速度和处理能力总体表示满意。例如 `#87646` 和 `#87016` 等 Bug 在短时间内从报告到关闭，体现了社区的高效协作。
- **期望：更高的默认安全性与可控性。** 围绕 MCP 审批 (Issue `#78308`)、`doctor --fix` 原子性 (Issue `#77802`) 等讨论都指向同一个方向：用户希望 OpenClaw 在框架层面提供更安全、更可预期的默认行为，并拥有更精细的控制权。

### 8. 待处理积压

以下重要 Issue 或 PR 长期未得到回应或推进，需要维护者关注：

1.  **`#78308`** **渠道介导的 MCP 工具调用审批** ([Issue](https://github.com/openclaw/openclaw/issues/78308))
    - **重要性：** 高。社区呼声极高的安全特性，且已提出超过三周，是当前最重要的阻塞性功能需求之一。
    - **状态：** 等待产品决策和维护者审核。建议维护者评估与 MCP 增强系列 PR (`#88536`) 的优先级和关联性。

2.  **`#77802`** **`doctor --fix` 在存在多个验证错误时原子性失败** ([Issue](https://github.com/openclaw/openclaw/issues/77802))
    - **重要性：** 中。该问题影响用户升级后的配置修复流程，会导致用户陷入“修复-失败-再修复”的死循环，对新手用户极不友好。
    - **状态：** 自 5月5日起无人回复。该问题已影响多用户，建议维护者快速评估并修复。

3.  **`#81917`** **OpenClaw 仪表盘记录裸 URL 并可能在 Linux/KDE 浏览器启动时挂起** ([Issue](https://github.com/openclaw/openclaw/issues/81917))
    - **重要性：** 中（安全）。日志泄露裸 URL 存在安全风险，且在特定环境下导致启动挂起，影响用户体验。
    - **状态：** 等待产品决策和安全审查。建议将其与 `#85246` (UI更新按钮导致Gateway崩溃) 等仪表盘/UI相关问题合并处理。

---

## 横向生态对比

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将基于您提供的各项目日报数据，为您生成一份横向对比分析报告。

---

### **AI智能体与个人AI助手开源生态横向对比分析报告 (2026-05-31)**

本报告基于对 OpenClaw、NanoBot、Hermes Agent 等10个主流开源项目的社区动态分析，旨在揭示当前生态的核心趋势、各项目定位及未来发展方向。

#### **1. 生态全景**

当前AI智能体开源生态正处于 **“从原型验证迈向生产部署”的关键转折期**。社区活跃度极高，反映出开发者对这一领域的巨大热情。然而，**安全与稳定性**已取代“新功能探索”，成为所有项目的核心议题。多渠道体验（Telegram、Discord、飞书等）、多模型提供商兼容性以及跨平台会话连续性，是用户普遍关注的“痛点”。同时，项目普遍面临**快速迭代带来的回归风险**和**社区贡献的审查瓶颈**，净推荐值与稳定性之间呈现微妙平衡。生态整体呈现出“百花齐放”但“标准尚未统一”的繁荣与混沌并存的态势。

#### **2. 各项目活跃度对比**

| 项目名称 | 今日Issues (新开/活跃) | 今日PRs (提交/合并) | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 (129关闭) | 500 (72合并) | 2 | **极高活跃**，迭代迅速，修复效率高，但PR积压严重。 |
| **NanoBot** | 7 (4关闭) | 20 (6合并) | 0 | **高度活跃**，安全和稳定性修复是重点，待合并PR积压。 |
| **Hermes Agent** | 高 (P0/P1问题多) | 50 (4合并) | 0 | **高强度开发**，社区讨论热烈，但合并流程是瓶颈。 |
| **ZeroClaw** | 50 (19关闭) | 50 (15合并/关闭) | 0 | **高活跃**，架构演进与安全加固并行，有多个严重Bug待修复。 |
| **PicoClaw** | 8 (4关闭) | 12 (3合并) | 1 (Nightly) | **中等活跃**，有明确的社区痛点，但维护者对Bug响应需加强。 |
| **NanoClaw** | 高 | 15 (3合并) | 0 | **高风险活跃**，PR提交量创新高，但供应链安全和稳定性问题突出。 |
| **CoPaw** | 高 (热点问题多) | 1 (合并) | 0 | **用户反馈活跃**，但核心Bug处理进度慢，稳定性堪忧。 |
| **IronClaw** | - | 16 (9合并) | 0 | **高效交付**，架构演进迅速，核心团队主导开发。 |
| **Moltis** | 0 | 1 (待合并) | 0 | **低活跃**，项目状态平稳，但缺乏可见进展。 |
| **LobsterAI** | 0 | 1 (Stale) | 0 | **停滞状态**，存在一个由社区PR修复、但近两个月未合并的关键Bug。 |
| **ZeptoClaw** | 0 | 0 | 0 | **静默维护**，健康度稳定但无可见进展。 |
| **TinyClaw** | 0 | 0 | 0 | **无活动**。 |
| **NullClaw** | 0 | 0 | 0 | **无活动**。 |

#### **3. OpenClaw 在生态中的定位**

OpenClaw 稳居**生态的“枢纽”与“标杆”地位**，其动态几乎定义了社区的发展节奏和关切点。

- **优势：** 社区规模与活跃度远超其他项目，日处理500+ Issue/PR的能力是其核心护城河。修复效率极高，尤其擅长处理P0/P1级关键问题，体现了成熟的项目治理能力。
- **技术路线：** 侧重于构建一个**高度可扩展、多渠道聚合、运行稳定的通用Agent运行时**。对MCP（Model Context Protocol）生态的重视，以及对渠道稳定性的持续投入，是其核心技术差异化。
- **对比：** 相较于NanoBot和Hermes Agent，OpenClaw在社区规模和组织效率上具备明显优势。与ZeroClaw、IronClaw等更侧重架构探索或特定功能（如安全、触发器）的项目相比，OpenClaw更注重**全栈体验**和**开箱即用的稳定性**。

#### **4. 共同关注的技术方向**

以下是多个项目社区中涌现的共同需求，代表了行业共识：

1.  **细粒度安全管控与审批机制** (涉及：OpenClaw, Hermes Agent, ZeroClaw, NanoClaw)
    - **具体诉求：** 对MCP工具调用、Shell命令执行、文件访问等进行渠道化的审批（Approval）或更精细的RBAC（角色权限控制）。用户普遍对“Agent越权”感到担忧，希望获得类似“sudo”的控制能力。

2.  **会话状态与跨平台连续性** (涉及：Hermes Agent, NanoClaw, OpenClaw)
    - **具体诉求：** 用户期望在不同设备（CLI、Telegram、WebUI）和会话间切换时，Agent能无缝恢复对话上下文和任务状态。这是个人AI助手从“玩具”走向“生产力工具”的关键。

3.  **版本升级的稳定性与回滚能力** (涉及：OpenClaw, Hermes Agent, PicoClaw, CoPaw)
    - **具体诉求：** 用户普遍抱怨“升级即体验下降”，Bug多由版本回归导致。社区渴望更稳健的发布策略、清晰的升级指南和便捷的降级/回滚方案。

4.  **对非OpenAI API的深度兼容** (涉及：CoPaw, OpenClaw, Moltis)
    - **具体诉求：** 不再满足于简单的“代理适配”，用户要求原生支持其他提供商的独特参数（如DashScope的`enable_search`），以及更好地处理如`temperature`等参数的默认值和边界情况。

5.  **MCP Server管控与安全性** (涉及：OpenClaw, ZeroClaw, NanoClaw)
    - **具体诉求：** 多个社区暴露出MCP生态的安全风险，包括恶意MCP包（NanoClaw）、工具调用绕过权限配置（ZeroClaw）等。这促使项目方加强MCP的白名单、签名和运行时隔离。

#### **5. 差异化定位分析**

| 项目 | 核心定位 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | **通用Agent枢纽**，成熟的运行时与多渠道集成。 | 中高级开发者，追求稳定与确定性。 | 插件化渠道架构，SQLite状态存储，强调MCP集成。 |
| **NanoBot** | **安全优先的个人助手**，侧重运行时加固与隔离。 | 对安全性有极致要求的开发者和企业用户。 | **bwrap沙箱**、细粒度权限控制、SSRF防护。 |
| **Hermes Agent** | **企业级/全功能Agent**，面向复杂工作流与多场景。 | 期望用Agent替代多种工具的Power User。 | 强大的Kanban任务系统，面向生产环境的多种平台适配（Windows, Linux）。 |
| **ZeroClaw** | **下一代Agent平台**，侧重架构创新与多租户。 | 探索Agent高级能力和平台级部署的开发者。 | **RBAC多租户**、统一输出路由模型、computer-use支持。 |
| **IronClaw** | **技术实验田**，探索底层触发器、通信等新范式。 | 核心开发者和技术极客，关注前沿架构。 | “Reborn”架构，libSQL触发器数据库，出站通信偏好模型。 |
| **CoPaw** | **垂直化、易用化Agent**，强调非标准API兼容与群聊。 | 普通用户和中级开发者，注重开箱即用体验。 | 专注于DashScope等中国模型，Windows平台支持（虽不完善），斜杠指令优化。 |
| **PicoClaw** | **轻量级、专注于Web与i18n的Agent**。 | 小型开发者和个人用户，追求简洁部署。 | 轻量架构，支持多语言（如孟加拉语），但稳定性（如Web UI）是短板。 |

#### **6. 社区热度与成熟度**

- **第一梯队（高活跃+高成熟度）：** **OpenClaw**、**Hermes Agent**、**ZeroClaw**。这些项目拥有庞大的社区、完善的Issue流程和强大的核心维护团队，处于从“快速发展”向“质量巩固”过渡的阶段，但都面临着“代码审查瓶颈”和“版本回归”的成熟期挑战。
- **第二梯队（高活跃+风险偏高）：** **NanoBot**、**NanoClaw**、**CoPaw**。这些项目社区参与度很高，贡献了大量代码和反馈，但项目本身在处理“供应链安全”、“核心Bug阻塞”等关键风险方面的能力有待加强，处于“远未成熟”的快速迭代阶段。
- **第三梯队（中等活跃+稳定成长）：** **PicoClaw**、**IronClaw**。社区有特定领域的热度，项目发展稳健、有明确方向，但无论是用户基数还是代码规模，都尚不具备挑战第一梯队的能力。
- **第四梯队（低活跃/停滞）：** **Moltis**、**LobsterAI**、**ZeptoClaw**、**TinyClaw**、**NullClaw**。这些项目可能处于维护期、归档期或社区重组的阶段，对于希望寻求长期技术合作或投入的开发者而言，需要谨慎评估。

#### **7. 值得关注的趋势信号**

1.  **“安全2.0”时代到来：** 对Agent权限的控制已从“有/无”的二元控制，转向**细粒度的、可配置的、由上下文驱动的审批策略**。这将是2026年下半年所有Agent项目必须补齐的能力，也是企业级用户的核心诉求。

2.  **从“单点工具”到“平台生态”：** 个人AI助手正在从单一功能的聊天机器人，演变为集**搜索、执行、协作、审批**于一体的复杂工作流平台。对MCP、MCP-Security、Kanban等生态的支持深度，将成为区分项目等级的关键。

3.  **“版本迭代”正在成为双刃剑：** 高频的版本更新是社区活力的象征，但也带来了严重的回归问题。**“稳定滚发布”和“自动化回归测试”** 将成为衡量项目治理成熟度的核心指标，而非仅仅是功能数量。

4.  **开发者角色正在分化：**
    - **初级用户/普通用户** 更偏向**CoPaw**、**PicoClaw**等开箱即用、配置简单的项目。
    - **资深开发者/运维人员** 更青睐**OpenClaw**、**Hermes Agent**这类可深度定制、集成度高、渠道稳定的“基础设施”。
    - **技术布道者/极客** 则在**ZeroClaw**、**IronClaw**等项目中探索未来Agent的边界。

**结论：** 当前生态正处于**从“可用”迈向“好用”、“安全”的关键时期**。对于开发者而言，选择哪个项目不仅取决于功能，更取决于其**社区治理成熟度、安全管控能力以及解决用户痛点的优先级**。跟踪 **OpenClaw、Hermes Agent、ZeroClaw** 三大标杆项目的动态，将能很好地把握整个行业的技术脉搏。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 NanoBot 项目数据，我为您生成了 2026-05-31 的项目动态日报。

---

### NanoBot 项目动态日报 | 2026年5月31日

---

#### 1. 今日速览

NanoBot 项目今日保持高度活跃，24 小时内处理了 7 条 Issue（关闭 4 条，新开 3 条），PR 活动尤为密集，达到了 20 条。虽然无新版本发布，但项目在**安全加固、Bug 修复和功能增强**三大方向齐头并进。值得关注的是，待合并 PR 积压至 14 条，表明社区贡献热情高涨，但维护团队的审查速度面临挑战。项目整体健康度良好，正朝着更加稳定、安全且功能丰富的方向快速迭代。

#### 2. 版本发布

无

#### 3. 项目进展 (重点合并/关闭的 PR)

今日有 6 个 PR 被合并或关闭，显著推进了项目的稳定性和安全性：

- **修复并发与资源竞争问题**：
    - **[#4104] fix(agent): acquire per-session lock in process_direct**：关闭了 Issue #4080，该 PR 修复了 `process_direct()` 函数绕过会话级锁的 Bug，消除了因并发访问导致的历史记录损坏风险。这是对消息处理核心逻辑的重要加固。
    - **[#4108] feat(webui): refine output timeline and model controls**：此 PR 已合并，对 WebUI 进行了用户体验优化，重新设计了输出时间线，并使模型控制更加清晰。

- **关键安全修复**：
    - **[#4086] fix(security): normalize IPv6-mapped IPv4 addresses in SSRF checks**：关闭了安全相关的 Issue，修复了 SSRF（服务端请求伪造）检查中对 IPv6 映射 IPv4 地址的绕过漏洞，提升了系统的安全性。
    - **[#4106] [security] fix(matrix): bound inbound media downloads**：合并了一个针对 Matrix 通道的重要安全修复，通过强制实施媒体大小限制，防止无限制下载导致的潜在资源耗尽或攻击。

- **兼容性与配置增强**：
    - **[#4054] [bug, enhancement, valid] fix: coerce typeless Anthropic content blocks + add Dream enable toggle**：这是一个多合一的 PR，一次性关闭了两个 Issue (#3993, #3885)。它修复了与 Anthropic 提供者的兼容性问题，同时为 Dream 系统作业添加了全局开关配置，赋予了用户更高的控制权。

**总结**：项目不仅在被动修复 Bug，也在主动进行安全加固和架构层面的优化，表明项目成熟度正在稳步提升。

#### 4. 社区热点

- **最受关注的 Issue: [WebUI: Code blocks without language specifier cause white screen crash (#4116)](https://github.com/HKUDS/nanobot/issues/4116)**
    - **标签**: Bug, High severity
    - **热度**: 虽然是今日新开，但严重性标记为“高”，且提交者立即提供了修复 PR。
    - **分析**: 该 Issue 报告了 WebUI 的一个严重崩溃问题。当用户加载包含未指定语言的代码块会话时，整个前端会白屏。用户 (`Flinn-X`) 不仅报告了问题，还准确指出了崩溃点 (`react-syntax-highlighter` 组件的 `language` prop 为 `undefined`)，并提交了对应的修复 PR [#4117](https://github.com/HKUDS/nanobot/pull/4117)。这体现了社区 “发现即修复” 的高效协作模式。

- **最活跃的 PR/Issue 话题:**
    - **Heartbeat 定时任务的行为讨论**：围绕 Issue [#4111](https://github.com/HKUDS/nanobot/issues/4111) (Heartbeat 误报) 和其两个竞争修复 PR ([#4112](https://github.com/HKUDS/nanobot/pull/4112), [#4114](https://github.com/HKUDS/nanobot/pull/4114))，社区对“失败关闭 (fail-closed)”和“消息传递安全”产生了深入讨论。这表明用户对机器人的自主行为有严格的控制要求，背后是对系统可预测性和无侵扰性的深层诉求。

#### 5. Bug 与稳定性

- **高**
    - **[WebUI: Code blocks without language specifier cause white screen crash (#4116)](https://github.com/HKUDS/nanobot/issues/4116)**：严重性高，整个 WebUI 崩溃。 **已有修复 PR #4117**。
    - **[Heartbeat 定时任务在无任务时错误发送 'All clear.' 到飞书 (#4111)](https://github.com/HKUDS/nanobot/issues/4111)**：严重性中，造成用户困扰。 **已有两个竞争修复 PR (#4112, #4114)**。

- **中**
    - **[MatrixChannel: no m.key.verification.* handling blocks Element X 'unverified device' clearance (#4042)](https://github.com/HKUDS/nanobot/issues/4042)**：虽已关闭，但这是一个影响用户体验的兼容性问题，已在 PR #4110 中修复。

- **已修复**
    - [Bug: process_direct bypasses per-session dispatch locks (#4080)](https://github.com/HKUDS/nanobot/issues/4080) - 已通过 PR #4104 合并修复。
    - [Bug/安全] 多个安全相关的修复已通过 PR #4086, #4106 合并。

#### 6. 功能请求与路线图信号

- **高概率纳入下一版本**:
    - **为 Dream 系统作业添加全局开关 (Issue #3885)**: 已在 PR #4054 中实现并关闭，用户可通过配置 `"dream": {"enabled": false}` 来禁用。此功能预期会在下个版本中提供。
    - **Anthropic 内容块类型兼容 (Issue #3993)**: 同上，已在 PR #4054 中修复。
    - **Matrix 设备验证支持 (Issue #4042)**: 已在 PR #4110 中实现。
    - **Allow configuring additional bind mounts for bwrap sandbox (Issue #4107)**: 用户提交的增强功能，希望为 bwrap 沙箱增加可配置挂载点，以获得更灵活的安全控制。目前无关联 PR，但方向与项目当前的安全优化一致，很可能被采纳。

- **路线图信号**:
    - **WebSocket / Gateway 重构**: PR [#4115](https://github.com/HKUDS/nanobot/pull/4115) 提取了 `GatewayHTTPHandler`，这是解耦 WebSocket 和 AgentLoop 的第一步，预示着未来可能支持热加载和更清晰的架构。
    - **跨 Agent 协作**: 长期开放的 PR [#3992](https://github.com/HKUDS/nanobot/pull/3992)（agent-collab）旨在实现多 Agent 实例间的消息总线通讯。这表明社区对构建更复杂的、可协作的 AI 系统充满兴趣。
    - **轻量级 RAG**: PR [#4109](https://github.com/HKUDS/nanobot/pull/4109) 提出了为记忆检索添加本地嵌入的轻量级 RAG 功能，表明项目在探索更高效的本地知识检索方案。

#### 7. 用户反馈摘要

- **痛点反馈**:
    - **配置控制缺失**: 用户 `codeLong1024` 在 Issue #3885 中明确表达了希望有开关能完全禁用 Dream 作业的强烈需求，即使通过其他方式（如禁用技能、设置超长间隔）也无法阻止作业注册。这反映了用户对系统资源占用和后台行为有精细控制的期望。
    - **沙箱灵活性不足**: 用户在 Issue [#4107](https://github.com/HKUDS/nanobot/issues/4107) 中抱怨 bwrap 沙箱的挂载点是硬编码的，对于需要访问特定目录的用户来说不够灵活。
- **使用场景**:
    - **安全环境**: 用户 `PaddyPatPat` 在 Issue #4042 中描述了在使用 Element X 这种强调端到端加密验证的客户端时遇到的问题，暴露了 NanoBot 在严格安全合规环境下的使用瓶颈。
    - **企业办公**: 用户 `CashSoldier` 在 Issue #4111 中描述的 Heartbeat 误报问题，直接影响了其在飞书办公场景下的体验，突显了健壮性对于生产环境使用的重要性。
- **满意/不满意**:
    - **满意 (协作效率)**: Issue #4116 的快速修复流程（报告 -> PR -> 讨论）展示了高效的社区协作，这种“问题驱动开发”的模式获得了正向反馈。
    - **不满意 (等待时间)**: 大量待合并 PR 积压可能暗示贡献者需要等待较长时间才能获得反馈，这可能是社区协作中的一个潜在摩擦点。

#### 8. 待处理积压

- **长期开放的功能性问题**:
    - **[PR #3992] feat(agent-collab) - enable cross agent messaging**: 从 5月24日开放至今，已超过一周，且未标记为 “draft”。这个功能对项目未来扩展性影响重大，但缺乏维护者的明确意见。
    - **[PR #4034] Add GitAgent Protocol support**: 虽然被打上 `duplicate` 标签，但该提案尝试引入一个标准协议。维护者应向社区解释为何标记为重复，以避免挫伤贡献者的积极性。

- **需要关注的未解决 Issue**:
    - **[Issue #4107] Allow configuring additional bind mounts for bwrap sandbox**: 这是一个用户提出的明确增强需求，且与安全沙箱相关，目前无 PR 关联。建议维护者给予初步回应，是计划采纳、搁置还是拒绝。

**建议**: 项目维护团队可考虑安排一次集中的 PR 审查会议，专门处理目前积压的 14 个待合并 PR，尤其是那些与安全（如 #4099, #4103）和核心功能（如 #3997）相关的 PR，以保持社区贡献的热情和项目迭代的速度。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 Hermes Agent 开源项目的分析师，我将根据您提供的 2026-05-31 数据，生成一份结构化的项目动态日报。

---

# Hermes Agent 项目日报 - 2026-05-31

## 1. 今日速览

Hermes Agent 项目今日社区活动极其活跃，无论是问题报告还是功能讨论均处于高位，显示出项目正处于快速迭代和用户大规模使用的阶段。**核心亮点**在于安全与稳定性相关的 P0/P1 级 Issue 得到了快速响应和修复（如配置文件泄露、Dashboard 循环重载等），体现了维护团队对关键问题的重视。**主要风险**是目前 Pull Request 合并率较低（4/50），大量高质量修复正在排队等待审查与合并，可能造成用户等待修复时间延长。总体而言，项目处于 **“高强度开发 + 广泛社区参与”** 的健康状态，但代码审核流程是潜在的瓶颈。

## 2. 版本发布

*   **本次日报无新版本发布。**

## 3. 项目进展

今日有 4 个 PR 被合并或关闭，标志着多项关键修复和改进已完成交付。项目在**安全加固、核心函数修复、跨平台兼容性**方面取得了扎实的进展：

*   **安全加固 (P2)**：**PR #35588** 被合并，修复了 Kanban 工具集在 `all` 或 `*` 配置别名下无法正确启用的问题。此修复确保了全局权限配置按预期工作，是权限系统正确性的重要一环。
*   **核心函数修复 (P3)**：**Issue #35597** 被关闭，其关联的修复已落地。该工作将“全息记忆治理”相关审计发现（holographic memory governance audit caveats）进行了可操作化处理，增强了系统记忆检索的可靠性和可观测性。
*   **Bug 修复 (P2)**：**Issue #35611** (Discord @提及被错误屏蔽) 和 **Issue #34202** (Dashboard 无限循环重载) 被关闭，标志着这两个影响用户实际体验的 Bug 已被修复。

尽管合并/关闭数量不多，但这些问题均属于影响面较大的关键 Bug 或安全增强，对项目稳定性的提升具有实际意义。

## 4. 社区热点

今日社区讨论热度集中在**安全策略**和**跨平台体验**两个核心方向：

*   **安全策略与最佳实践 (最高评论)**：
    *   **Issue #9179** ([链接](NousResearch/hermes-agent Issue #9179))：该 Issue 持续引发讨论，用户提议启用 GitHub 私有漏洞报告功能。这反映出社区用户对项目安全治理的强烈参与意识和责任心，并希望建立一个更完善、更隐蔽的漏洞提交流程。
*   **跨平台工作流连续性 (最高赞)**：
    *   **Issue #8366** ([链接](NousResearch/hermes-agent Issue #8366))：获得了 6 个 👍 和 5 条评论，是社区呼声最高的功能需求。用户痛点非常明确：在不同设备（CLI、Telegram、iMessage）间切换时，对话和任务上下文中断。这说明用户将 Hermes Agent 视为一个**真正的跨平台个人助理**，而不仅仅是单一终端的聊天机器人，对无缝体验有极高期待。

## 5. Bug 与稳定性

今日报告了大量 Bug，涵盖从核心功能到特定平台的多个层面。以下按严重程度列出：

*   **P0 - 严重/安全风险**
    *   **配置文件泄露**：**Issue #35584** (已关闭) 报告了一个严重的安全漏洞：当文件变异验证器拒绝写敏感配置时，网关仍会通过 `extract_local_files` 将其内容附加到响应中。此问题已被标记为 P0 并已关闭，表明已得到紧急修复。 ([链接](NousResearch/hermes-agent Issue #35584))

*   **P1 - 高优先级/功能性损坏**
    *   **命令返回格式损坏**：**Issue #35595** 报告 v0.15 版本中 `/model` 等斜杠命令返回结构化的字段列表而非人类可读的消息，破坏了基本功能。目前仍为开启状态，急需修复。([链接](NousResearch/hermes-agent Issue #35595))
    *   **Cron 任务自毁循环**：**Issue #30719** (已关闭) 描述的 Agent 可以创建杀死自身运行时的 cron 任务，导致无限重启。此问题已被关闭，表明修复已到位。([链接](NousResearch/hermes-agent Issue #30719))

*   **P2 - 中等优先级/特定场景损坏**
    *   **Windows 兼容性**：**Issue #35654** 指出，在 Windows 上使用浏览器工具时，URL 中的 `&` 等 Shell 字符会导致命令失败。([链接](NousResearch/hermes-agent Issue #35654))
    *   **TUI 缺陷**：多个 Issues (#35671, #35192, #35738) 报告了 TUI 界面在自动滚动、输入框消失、在某些终端（如 Warp）布局错乱等问题，影响核心聊天体验。
    *   **特定平台功能损坏**：**Issue #35739** (Telegram 媒体路由)、**Issue #35576** (飞书 Auto-resume 失败)、**Issue #21168** (Discord Markdown 表格渲染) 分别报告了各自平台的特定功能问题。

*   **P3 - 低优先级/改进建议**
    *   **功能静默失效**：**Issue #29617** 报告 `web.search_backend` 等配置为空时会静默禁用搜索功能，给用户排查带来困扰。
    *   **技能与权限管理**：**Issue #35743** (技能视图误报冲突)、**Issue #35736** (技能管理工具参数混淆) 反映了技能管理模块的易用性问题。

目前，针对 #35595、#35654、#35736、#35738 等 Bug 已有对应的修复 PR (#35741, #35738 等) 在排队等待合并。

## 6. 功能请求与路线图信号

今日用户提出了多项富有前瞻性的功能需求，其中一些已指向了未来可能的版本规划：

*   **进阶权限与安全模型**：这是今日最强烈的信号。**Issue #21849** (工具权限门控系统)、**Issue #33905** (按工具/工具集设置审批策略)、**Issue #35479** (对特定授权用户进行工具集限制) 三项提案，都旨在建立一个**更细粒度、更安全的权限体系**。结合已合并的安全修复 (#35588)，可以预见 **“打造可配置、多层级的工具与数据访问控制”** 将是项目下一阶段的重要方向。
*   **多Agent协作框架**：**Issue #35688** 提出在现有的 `delegate_task` 和 `kanban` 之间，构建一个**“审核员/执行者 + 共享内存”**的后台轻量级多Agent框架。这暗示了项目正在探索比简单任务委派更复杂的、具有内部审查和协作机制的 Agent 工作流。
*   **跨平台体验增强**：**Issue #8366** 的跨平台会话续传功能，虽然是一个巨大工程，但其高赞数表明解决此痛点的优先级非常高。
*   **后端兼容性**：**Issue #29327** 提出针对 LiteRT 等严格后端进行聊天历史标准化，表明项目正在积极扩展其AI后端的兼容范围，以适应更多本地化、定制化的部署场景。

## 7. 用户反馈摘要

从今日的 Issue 讨论中，可以提炼出用户最真实的感受：

*   **“更新破坏了我的工作流”**：`louiemota` 报告当 `NODE_ENV=production` 时，`hermes update` 会因缺少开发依赖而构建失败。这是一个典型的部署环境问题，暴露了项目构建脚本对环境的假设不足。([#27430](NousResearch/hermes-agent Issue #27430))
*   **“Windows 体验不佳”**：`kmukul123` 报告了浏览器工具在 Windows 上因 Shell 字符而失败。`sujianddd-dev` 和 `rockeverm3m` 则报告了 Windows TUI 和桌面应用的渲染问题。这传递了一个清晰的信号：**Windows 平台的支持和测试仍需加强**。([#35654](NousResearch/hermes-agent Issue #35654), [#35671](NousResearch/hermes-agent Issue #35671))
*   **“文档与行为不符”**：`sadeegamhewa` 发现 `web.search_backend` 默认空值导致功能静默失效，这与用户配置了 `web.backend` 的预期行为不一致。`DiscountDarcy` 则指出 Discord 平台对 Markdown 的支持问题，希望文档或行为能有自动处理。([#29617](NousResearch/hermes-agent Issue #29617), [#21168](NousResearch/hermes-agent Issue #21168))
*   **“希望更安全，也希望更灵活”**：围绕权限和安全功能的讨论，如 `alt-glitch` 和 `YEZIHANGISM` 的提案，显示高级用户希望在保持安全的同时，能根据自身场景微调权限，而非简单的一刀切。

## 8. 待处理积压

以下是在未来版本中具有重要价值但尚未推进或响应的议题/PR，可能已超出维护者关注范围：

*   **待合并的 PR**：
    *   **跨平台会话恢复**：`#13272` ([链接](NousResearch/hermes-agent PR #13272)) 和 `#13274` ([链接](NousResearch/hermes-agent PR #13274)) 是来自社区的 PR，旨在解决 Telegram 跨频道话题和用户名 ID 的路由问题。这些 PR 自 4 月中旬就已打开，是改善社区版跨平台体验的关键，但迟迟未合并。
*   **需要关注的 Issue**:
    *   **跨平台会话延续**：`#8366` ([链接](NousResearch/hermes-agent Issue #8366)) 作为社区呼声最高的 Feature Request，自 4 月提出后长期未获官方回复或路线图承诺。若能将此功能纳入未来规划，将极大提升社区信心。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

## PicoClaw 项目动态日报 — 2026-05-31

### 1. 今日速览
过去 24 小时项目整体活跃度较高：共处理 8 条 Issue（4 条新开/活跃、4 条已关闭）和 12 条 PR（3 条已合并/关闭、9 条待合并）。同时发布了 **v0.2.9-nightly** 自动构建版本。社区反馈集中在 **Web UI 升级后的消息混乱**、**/context 显示异常** 以及 **新版发布节奏** 的讨论上。Azure Identity 支持与孟加拉语文支持功能已被合入主干，cron 工具与 Codex OAuth 修复等改进正在排队等待合并。

---

### 2. 版本发布
- **nightly (v0.2.9-nightly.20260531.1ce353ba)**  
  此版本为自动构建的快照版本，可能包含不稳定代码。  
  **变更日志**：对比 v0.2.9 至 main 分支的所有提交。  
  **注意事项**：不建议生产环境直接使用，如需测试请提前备份数据。  
  🔗 [Release 页面](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

---

### 3. 项目进展
今日有 **3 个 PR 被合并**，为项目新增了以下能力：

- **Web 前端图片粘贴与拖拽上传** (#2969)  
  用户可直接在聊天输入框粘贴图片或拖拽上传，混合剪贴板内容保留文本粘贴行为。  
  🔗 [PR #2969](https://github.com/sipeed/picoclaw/pull/2969)

- **Azure OpenAI 提供者支持 Azure Identity 认证** (#2971)  
  可选的 Azure 托管身份认证，适配禁止本地密钥的订阅策略。需使用 `azidentity` 构建标签。  
  🔗 [PR #2971](https://github.com/sipeed/picoclaw/pull/2971)

- **i18n 添加孟加拉语 (bn-in)** (#2974)  
  基于已有 PR 模板实现，Web 应用现在支持孟加拉语界面。  
  🔗 [PR #2974](https://github.com/sipeed/picoclaw/pull/2974)

此外，**cron 工具** 新增 `get` 和 `update` 行为 (#2977)、**Codex OAuth 空响应修复** (#2967) 等 PR 已提交，正在等待审查。

---

### 4. 社区热点
- **#2952 [Feature]“好久没发新版本了”**  
  评论数 3，用户 `xhynice` 集中反映了三个痛点：exec 命令的 `actions:run` 默认不带导致报错、QQ 渠道重启后自动重触发、模型提供商界面建议改进。该 Issue 代表了社区对 **稳定版发布** 和 **核心稳定性修复** 的迫切需求。  
  🔗 [Issue #2952](https://github.com/sipeed/picoclaw/issues/2952)

- **#2972 [BUG] 升级到 v0.2.9 后 Web UI 消息混乱**  
  用户 `xpader` 报告每次新会话都会附加旧消息历史，影响正常使用，已引发 2 条评论。  
  🔗 [Issue #2972](https://github.com/sipeed/picoclaw/issues/2972)

- **#2742 [CLOSED] gateway 在 v0.2.8 启动时无频道**  
  虽然已关闭，但拥有 6 条评论，说明该问题曾引起较多关注，最终被解决。  
  🔗 [Issue #2742](https://github.com/sipeed/picoclaw/issues/2742)

---

### 5. Bug 与稳定性
| 严重程度 | Issue | 描述 | 状态 |
|----------|-------|------|------|
| **高** | #2972 | 升级 v0.2.9 后 Web UI 新会话始终附着旧消息历史 | OPEN，无关联 fix PR |
| **中** | #2968 | `/context` 始终显示 `Compress at: 76800 tokens`，可能为 token 压缩逻辑异常 | OPEN，获 1 个 👍 |
| **中** | #2880 (CLOSED) | Android 设备上启动服务时因目录创建权限而被拒绝 | 已关闭，可能已在 0.1.4+ 修复 |
| **低** | #2952 中提及 | exec 的 `actions:run` 默认不传递导致模型多余执行命令 | OPEN，但未单独开 bug 跟踪 |

- **关键观察**：暂无 PR 直接对应 #2972 或 #2968 的修复，建议维护者优先分析这两项回归问题。

---

### 6. 功能请求与路线图信号
- **新增提供者请求**：用户 `urtaevS` 请求添加 **omniroute** 作为 AI 提供者 (#2978)，这是一个社区聚合路由器。若获采纳，可增加 API 路由灵活性。  
  🔗 [Issue #2978](https://github.com/sipeed/picoclaw/issues/2978)

- **cron 工具增强**：PR #2977 正在为 cron 工具增加查询与部分更新能力，防止代理流程因 `remove -> add` 引发重调度问题，预计将进入下一小版本。  
  🔗 [PR #2977](https://github.com/sipeed/picoclaw/pull/2977)

- **Agent 工具策略过滤**：PR #2838（stale）扩展了 `AGENT.md` 的 frontmatter 以支持工具 allow/deny 策略，该功能对权限管理有长远价值，但已近三周未被更新。  
  🔗 [PR #2838](https://github.com/sipeed/picoclaw/pull/2838)

- **消息附件与 Telegram 富媒体**：PR #2856（stale）首次迭代消息工具支持附件和 Telegram 富文本发送，对多渠道体验提升明显，但同样停滞。  
  🔗 [PR #2856](https://github.com/sipeed/picoclaw/pull/2856)

---

### 7. 用户反馈摘要
- **稳定性焦虑**：`xhynice` 在 #2952 中表示“好久没发新版本了”，并列举了 exec 命令、QQ 渠道重启循环等具体问题，说明部分用户已在生产环境中遇到稳定性障碍，迫切期待正式版本修复。
- **升级后体验下降**：`xpader` 在 #2972 和 #2968 中反映从 v0.2.8 升级到 v0.2.9 后，Web UI 与上下文压缩表现异常，提示当前 nightly 构建可能存在回归。
- **配置不便**：用户在 #2952 中建议模型添加提供商时支持下拉选择、API Key 复用及自动获取模型列表，体现对配置流程自动化的需求。
- **平台兼容性**：`coppo99` 在 #2880 中报告 Android 访问文件目录权限问题，虽已关闭但警示移动端适配仍需关注。

---

### 8. 待处理积压
以下 Issue/PR 长时间未获维护者响应，建议纳入下轮审查重点：

| 条目 | 类型 | 创建时间 | 最后更新 | 备注 |
|------|------|----------|----------|------|
| [#2838](https://github.com/sipeed/picoclaw/pull/2838) | PR | 2026-05-09 | 2026-05-30 | Agent 工具策略过滤，标记 `stale` |
| [#2856](https://github.com/sipeed/picoclaw/pull/2856) | PR | 2026-05-11 | 2026-05-30 | 消息附件与 Telegram 富媒体，标记 `stale` |
| [#2962](https://github.com/sipeed/picoclaw/pull/2962) | PR (dependabot) | 2026-05-28 | 2026-05-30 | Anthropic SDK 升级（v1.26.0 → v1.46.0） |
| [#2963](https://github.com/sipeed/picoclaw/pull/2963) | PR (dependabot) | 2026-05-28 | 2026-05-30 | LarkSuite oapi-sdk-go 升级（v3.7.5 → v3.9.3） |

- 依赖升级 PR 通常可安全合并，但需注意 Anthropic SDK 跨越多个大版本，建议验证 API 兼容性后再操作。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 NanoClaw 项目实时数据的动态日报。

---

# NanoClaw 项目动态日报 | 2026-05-31

## 1. 今日速览
项目今日处于 **高活跃、高风险** 状态。单日 PR 提交量达到 15 条，创近期新高，但合并率偏低（仅 20%），代码积压风险上升。社区焦点集中在 **供应链安全** 和 **核心网关稳定性** 两个维度的重大漏洞报告，可能影响用户信任。同时，多项针对 Docker/Apple Container 兼容性的修复表明项目正积极适配不同部署环境。整体来看，项目开发势头强劲，但需警惕因关键 Bug 和积压 PR 导致的维护瓶颈。

## 2. 版本发布
今日无新版本发布。

## 3. 项目进展
今日有 **3 个 PR 被合并/关闭**，推进了以下关键领域：
- **多实例部署兼容性：** PR #2652 (matty271828) 已合并，重写了 OneCLI 代理端口处理逻辑，解决了在 `instances.conf` 配置多实例时，代理端口被硬编码导致路由错误的痛点。这表明项目正从单用户向多租户场景拓展。
- **群聊上下文感知能力：** PR #2645 (yairixStudio) 已合并，为群聊中的 Agent 增加了可配置的上下文窗口。Agent 在被 `@提及` 触发时，能看到最新的上下文，极大提升了群聊内的对话连贯性与智能性。这是一项重要的体验改进。
- **日志与监控优化：** PR #2521 (crookies) 已合并，让转录日志文件包含了消息来源的 `channelType` 信息。对于自建监控面板的用户来说，这是一个小而美的修复。

**项目整体向前迈进：** 完成了从单实例到多实例的兼容性升级，并显著增强了群聊交互的实用性和可观测性。

## 4. 社区热点
今日社区讨论热度最高的是关于 **功能回归** 的 Issue。

-   **Issue #2044: [v2] 使用 `@chat-adapter/discord` 对 `<URL>` 的处理方式适得其反** (评论: 1, 👍: 2)
    -   **链接：** [nanocoai/nanoclaw Issue #2044](https://github.com/nanocoai/nanoclaw/issues/2044)
    -   **诉求分析：** 用户 `pwinnski` 反馈，在 v2 版本中，Discord 适配器将一个用户用来 *抑制* URL 预览的语法 (`<URL>`) 错误地转换为了一个 Markdown 链接，导致回复消息总是包含无用的预览图。两个点赞表明这不是个例。这体现了用户对 **“已习惯的功能不应无故失效”** 的强烈诉求，以及对 **“可控的 UI 互动方式”** 的期待。用户期待的是对原有 Discord 语法的尊重，而非开发者“自以为是”的改进。

## 5. Bug 与稳定性
今日报告了 **3 个严重 Bug**，均与核心代理和部署环境稳定性相关。

1.  **【严重】【Fix PR 已提交】** **供应链安全风险：** Issue #2641 警告，项目文档或技能中推荐的 `@gongrzhe/server-gmail-autoauth-mcp` 包可能诱导用户安装恶意代码并泄露 Gmail 密码。这是 **最高优先级** 的风险，要求项目立即审查并替换相关依赖，指导用户采取措施。
    -   链接: [nanocoai/nanoclaw Issue #2641](https://github.com/nanocoai/nanoclaw/issues/2641)
2.  **【严重】** **OneCLI 网关因文件描述符耗尽而崩溃：** Issue #2655 (mshirel) 报告，OneCLI 网关在突发流量下因默认 1024 的文件描述符软限制而硬退出，导致所有 Agent 静默失联。这是一个典型的 “容量规划”与服务可用性 Bug，影响所有生产部署。
    -   链接: [nanocoai/nanoclaw Issue #2655](https://github.com/nanocoai/nanoclaw/issues/2655)
3.  **【严重】** **OneCLI 网关缺乏自愈能力：** Issue #2657 (mshirel) 指出，即使 OneCLI 网关进程死亡，Docker 容器仍标记为 'Up' 但 'unhealthy'，导致代理层完全瘫痪而系统无任何自动恢复动作。这是对 #2655 问题的放大，暴露了项目在 **容器韧性（Resilience）** 方面的缺失。
    -   链接: [nanocoai/nanoclaw Issue #2657](https://github.com/nanocoai/nanoclaw/issues/2657)
4.  **【高】** **Apple Container 文件挂载损坏：** PR #2649 (jurre-mbt-it) 修复了在 `Apple Container` 上，嵌套文件挂载导致 `stat()` 返回成功但 `read()` 返回 `EACCES` 的怪异问题。这导致所有 MCP Server 配置无法加载。
    -   链接: [nanocoai/nanoclaw Issue #2649](https://github.com/nanocoai/nanoclaw/pull/2649)
-   **补充：** 作为修复，PR #2656 (MoonCaves) 解决了因主机覆盖容器 ENTRYPOINT 导致 mnemon 钩子无法注册的逻辑 Bug。
    -   链接: [nanocoai/nanoclaw PR #2656](https://github.com/nanocoai/nanoclaw/pull/2656)

## 6. 功能请求与路线图信号
今日用户提出 **1 个重要功能需求**，与已有的 PR 结合后，指向了未来的发展方向。

-   **【未来候选】** **单安装多用户支持：** Issue #2653 (elancode) 请求在一个设备（如 Mac Mini）上为不同用户（如家庭成员）运行独立的 Agent，每个用户有自己的 Telegram Bot 和独立记忆空间。作者点出了数据模型已支持，但 `src/` 层级存在阻碍。
    -   **路线图信号：** 此需求与 PR #2652 (多实例端口修复) 和 PR #212 (WebUI控制面板) 的长期目标高度吻合，表明 **“从个人工具到家庭/小团队共享平台”** 可能是 NanoClaw 的下一个重要演进方向。多用户支持很可能被纳入 v2.x 的中期规划。

## 7. 用户反馈摘要
-   **【痛点】功能回归令人沮丧：** 用户在 Issue #2044 中的反馈非常明确，对于“修复”一个本无问题的功能感到不满。这提醒项目组，任何 “改善”都必须以不破坏现有用户习惯为前提，尤其是在“浏览器兼容性”或“平台协议一致性”这类敏感领域。
-   **【痛点】稳定性是核心关切：** 用户 `mshirel` 在 #2655 和 #2657 中的报告技术性极强，直指系统在高负载下的薄弱环节。这位用户显然是有一定运维经验的深度用户，他的反馈代表了 **“早期专业用户”** 对项目健壮性的高标准要求。
-   **【需求】文档/指南需更清晰：** Issue #2641 的供应链安全问题，根源在于技能文档缺乏对第三方依赖的安全审查说明。用户需要清晰的安全警示和如何验证依赖真实性的指南。

## 8. 待处理积压
-   **【严重积压】** **PR #212: WebUI 控制面板** (状态: Open, 自 2026-02-13)
    -   **链接：** [nanocoai/nanoclaw PR #212](https://github.com/nanocoai/nanoclaw/pull/212)
    -   **状态：** 已悬而未决超过 3 个月。尽管该 PR 是使项目具备图形化运维能力的关键，但其长期未被合并可能导致代码分支严重过时，维护困难。维护者需评估是否继续合并、需要大幅重构，或在此方向上另起炉灶。
-   **【中等积压】** **Issue #2044: Discord URL 处理回归** (状态: Open, 自 2026-04-27)
    -   **链接：** [nanocoai/nanoclaw Issue #2044](https://github.com/nanocoai/nanoclaw/issues/2044)
    -   **状态：** 这是社区明确指出的 Bug，且持续 1 个月以上无人响应。这会影响所有 Discord 用户的使用体验，建议尽快安排修复或至少给出官方回应。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，以下是为您生成的 IronClaw 项目动态日报。

---

# IronClaw 项目动态日报 — 2026-05-31

## 今日速览

项目今日活跃度极高，核心开发团队围绕“Reborn”架构的底层基础设施（触发器、出站通信、产品认证）和关键 Bug 修复提交了大量重量级 PR。过去24小时内，共有16条 PR 被处理，其中9条已被合并或关闭，展现了高效的交付节奏。社区热点集中在 **crates.io 版本发布延迟** 这一关键依赖阻塞问题上，虽然该 Issue 评论数众多，但核心团队尚未明确回应。整体来看，项目正处于密集开发期，架构演进迅速，但新版本发布停滞是当前最大的隐忧。

## 项目进展

今日项目在架构演进和稳定性修复上取得了双线进展。多个由核心贡献者 henrypark133 提交的“Reborn”系列 PR 被合并，标志着该架构的多个基础模块建设完成。

- **合并：Rehorn 触发器与出站通信骨架搭建完成**
  - `#4261 [CLOSED]` **`Add ironclaw_triggers crate skeleton`**: 正式合并了全新的 `ironclaw_triggers` 工作空间包，包含触发器领域类型、Cron 调度验证等核心基础设施，是 Reborn 触发器功能的第一步。
  - `#4260 [CLOSED]` **`Add outbound communication preferences store`**: 为出站通信引入了用户偏好存储，细化了用户对最终回复、进度更新等不同通信类型的偏好设定。
  - `#4255 [CLOSED]` **`Add outbound delivery resolution domain types`**: 实现了出站解析器的领域类型，定义了通信投递请求和意图的标准化模型。
  - `#4254 [CLOSED]` **`Add trusted inbound facade`**: 为 Reborn 触发器入口增加了可信入站门面，通过一次性令牌和幂等性机制确保入口的可靠性。

- **关键修复：提升运行时稳定性和自省能力**
  - `#4259 [CLOSED]` **`allow synthetic capabilities to be introspected via capability_info`**: 修复了一个影响模型自省能力的 Bug。之前模型调用 `capability_info` 工具查询自身时失败，导致运行中断。现已支持对合成能力的自省。
  - `#4258 [CLOSED]` **`route dispatch failures through PR #4236 disposition`**: 修复了两个相关 Bug，防止 LLM 传递格式化错误的 JSON 数组（如 `stringified JSON array`）时导致 Agent 循环进入“恢复失败”的终态路径，转而向模型显示正确的工具错误。

> 总结：项目在架构上完成了“触发器”和“出站通信”两个新模块的领域建模与基础实现；在稳定性上修复了两个会中断 Agent 运行的严重 Bug，提升了模型的鲁棒性。

## 社区热点

- **`#3259 [OPEN]` `Publish 0.25.0–0.27.0 to crates.io`**  
  [链接](https://github.com/nearai/ironclaw/issues/3259) | 评论: 12 | 👍: 0
  
  这是当前社区最关注的 Issue。自4月29日 `0.27.0` 版本被标记后，crates.io 上始终只提供 `0.24.0` 版本。下游用户被锁定在旧版本，并且由于 wasmtime 28.x 的 CVE 漏洞而面临安全风险。用户请求 “Publish to crates.io” 的呼声很高，但项目维护者尚未在 Issue 中给出具体发布时间表。这已成为影响外部集成的主要障碍。

## Bug 与稳定性

- **[高] `#4108 [OPEN]` `Nightly E2E failed`**  
  [链接](https://github.com/nearai/ironclaw/issues/4108)  
  **状态**：持续失败，尚无关联 Fix PR。  
  **影响**：Nightly E2E 测试套件当日运行失败，影响范围涉及 `Full E2E / E2E (extensions)` 测试。这可能是代码合并引入的回归问题。
  
- **[中] `#4206 [CLOSED]` `Make runtime HTTP egress async end to end`**  
  [链接](https://github.com/nearai/ironclaw/issues/4206)  
  **状态**：已关闭。  
  **说明**：已完成 HTTP 出站的全异步化改造，消除了同步调用带来的阻塞风险。这是一个提升性能的修复性重构。

## 功能请求与路线图信号

- **[核心功能] `#4263 [OPEN]` `feat(triggers): add libsql repository`** 和 `#4262 [OPEN]` `feat(outbound): add resolution engine`  
  这两条 PR 是今日提交的 XL 级任务，分别实现了 **`libSQL` 触发器后端持久化**和 **出站通信的候选解析引擎**。它们明确标记了下一步工作范围（不包含验证、重试等），是 Reborn 架构的延续。这表明 `Triggers` 和 `Outbound` 模块是当前版本开发的核心重点。

- **[功能增强] `#228 [OPEN]` `[enhancement, scope: agent] feat: add deny-by-default delegation policy for sub-job creation`**  
  [链接](https://github.com/nearai/ironclaw/issues/228)  
  该 Issue 提出为 `CreateJobTool` 增加“默认拒绝”的委托策略，以防止 LLM 幻觉或提示注入导致的失控子任务创建。虽然为旧的（从日期判断）功能请求，但涉及 Agent 安全性，预计仍将被纳入后续 Agent 安全改进中。

## 用户反馈摘要

- **痛点**：**版本发布停滞**是用户最核心的不满，主要体现在 `#3259` 的讨论中。用户表示，由于无法获取新版本，他们无法利用最新的功能和关键的 CVE 修复。
- **使用场景**：`#3259` 的评论反映出用户对项目有明显的生产依赖。他们通过 `wasmtime` 等间接依赖与项目绑定，版本锁定直接影响了他们的安全合规。
- **正面反馈**：`#4112` 及其相关 PR（如 `#4257`, `#4256`）展示了 WebUI v2 在 OAuth 认证（GSuite, Notion, GitHub）方面的进展，用户社区对原生 SSO 集成（特别是 GitHub SSO PR #4229）表现出关注和期待。

## 待处理积压

- **`#228 [OPEN]`** `feat: add deny-by-default delegation policy for sub-job creation`  
  [链接](https://github.com/nearai/ironclaw/issues/228)  
  **创建**：2026-02-19 | **更新**：2026-05-31  
  这是一个历史悠久的增强请求，对 Agent 安全性至关重要。在今天架构快速迭代的背景下，该 Issue 重新获得关注（今日有更新），建议维护者考虑将其排入下一个 Agent 安全改进周期。

- **`#4035 [OPEN]`** `feat(slack): add Reborn ProductAdapter core`  
  [链接](https://github.com/nearai/ironclaw/pull/4035)  
  **创建**：2026-05-25 | **更新**：2026-05-30  
  这是一个来自社区贡献者 `danielwpz` 的 XL 级 PR，已经过了几天仍未合并。它实现了 Slack 的 `ProductAdapter`，是 Reborn 平台扩展的重要拼图。建议项目组尽快给予评审反馈，以避免社区贡献者等待过久。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-05-31

## 1. 今日速览
- 过去24小时内项目无新 Issue 或版本发布，整体活跃度偏低。
- 唯一动向是 **PR #1465** 由 `linlihua` 提交，旨在修复已删除定时任务重启后以“幽灵会话”重新出现的 Bug，但由于该 PR 已标记为 `stale` 且提交后近两个月未获合并，社区对此 bug 的修复进展仍然停滞。
- 目前项目未发布新版本，所有功能改动均处于开发分支等待评审状态。

## 2. 版本发布
（今日无新版本发布，此项省略）

## 3. 项目进展
今日无任何 PR 被合并或关闭，核心推进为零。`PR #1465` 仍处于待合并状态，该 PR 关联的 Issue #1359（用户报告定时任务未正确清理）依然未得到解决。项目在 **定时任务数据一致性** 方面的长期积压问题未获实质进展。

## 4. 社区热点
**唯一活跃项**：[PR #1465](https://github.com/netease-youdao/LobsterAI/pull/1465)  
- 创建于 2026-04-04，最后一次更新于今日（2026-05-31），但评论数为 undefined（可能缺失或为0）。
- 该 PR 直接针对用户反馈的痛点：删除定时任务后，重启应用会出现空内容的幽灵会话。其根本原因是本地 SQLite `cowork_sessions` 表中关联的会话记录未被同步清理。
- 社区对该问题关注度较高（关联 Issue #1359），但因长期未获合并，用户可能对修复周期感到失望。

## 5. Bug 与稳定性
无新报告的 Bug。但持续存在的 **严重 bug**（已关联 PR）属于：
- **严重程度：高**  
  - **描述**：定时任务删除后，重启应用导致空会话重新出现（幽灵会话），影响用户正常使用和会话管理。  
  - **影响范围**：所有使用定时任务并执行删除操作的用户。  
  - **修复 PR**：#1465（待合并）  
  - **链接**：[PR #1465](https://github.com/netease-youdao/LobsterAI/pull/1465)

## 6. 功能请求与路线图信号
今日无新功能请求提出。从 PR #1465 所述的根本原因（删除操作仅调用网关侧 `cron.remove`，未清理本地会话表）来看，该项目在 **任务与本地数据持久化一致** 方面存在设计缺口。未来版本可能需要引入统一的删除回调（如级联清理本地记录），该思路或可被纳入路线图。

## 7. 用户反馈摘要
由于今日无新 Issue 和评论，反馈均来自之前积累。通过 PR #1465 的摘要可以提取典型用户痛点：
- **场景**：用户删除定时任务后，重启应用，发现已删除的任务仍以空白会话形式出现。
- **不满**：反复删除仍反复出现，操作无效，影响对会话列表的信任。
- **诉求**：期望删除定时任务时能同步清理所有相关本地数据，消除幽灵会话。

## 8. 待处理积压
- **[PR #1465]** (Open, Stale)  
  - 创建时间：2026-04-04，距今已 **58 天** 未合并  
  - 影响：关键 Bug 修复停滞，用户问题长期无法解决  
  - 建议：维护者尽快评审并决定合并策略，或关闭后采用更优方案  
  - 链接：https://github.com/netease-youdao/LobsterAI/pull/1465

- **关联 Issue #1359**（未在此次日报数据中显示，但从 PR 摘要获知）  
  - 状态未知，但作为母问题同样需要关注。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 | 2026-05-31

## 1. 今日速览
- 过去24小时内项目活跃度较低，未产生新Issue或新版本发布，仅收到1个Pull Request（#1088），目前处于待合并状态。
- 该PR专注于改进OpenAI Codex提供者中工具调用（tool-call）参数的处理逻辑，属于功能完善与兼容性增强。
- 无Bug报告、无紧急回归、无社区讨论热点，整体项目状态平稳，维护节奏正常。

## 2. 版本发布
（无新版本发布）

## 3. 项目进展
### 待合并 PR
- **#1088 [codex] Handle OpenAI Codex final tool-call arguments**  
  - **作者**: s-salamatov  
  - **状态**: OPEN，待合并  
  - **概要**: 该PR对OpenAI Codex提供者的工具调用参数处理流程进行了三项改进：  
    1. 记录 `response.function_call_arguments.done` 载荷，确保最终参数能被正确捕获。  
    2. 当未发射参数增量（argument deltas）时，从最终参数中合成流式参数增量，保持接口一致性。  
    3. 确保空累积参数字符串仍能通过解码诊断（decode diagnostics）流动，防止因缺少参数而引发异常。  
  - **项目意义**: 该修复完善了OpenAI Codex提供者对工具调用最终参数的处理，解决了流式场景下可能出现的参数丢失或错误解码问题。一旦合并，将提升与OpenAI Codex交互的鲁棒性，尤其对使用工具调用（function calling）的复杂Agent工作流有直接帮助。  
  - **链接**: [PR #1088](https://github.com/moltis-org/moltis/pull/1088)

## 4. 社区热点
今日无产生新Issue、无活跃讨论、无高赞回复。项目社区当前处于静默期，无突出话题。

## 5. Bug 与稳定性
今日未报告任何Bug、崩溃或回归问题。上述PR #1088本身是为解决潜在的非正常参数流问题，属于预防性修复，尚未有用户反馈其触发。

## 6. 功能请求与路线图信号
今日无新功能请求。PR #1088所针对的OpenAI Codex工具调用参数处理可以视为对现有功能的优化，其方向暗示项目正在持续关注与大型语言模型（LLM）工具调用协议的兼容性，未来可能扩展更多模型提供者的工具调用支持。

## 7. 用户反馈摘要
今日无用户反馈记录。近期无新增Issue评论，无法提取具体痛点或使用场景。

## 8. 待处理积压
目前无长期未响应的重要Issue或PR。PR #1088自创建后尚不足24小时，等待维护者审核或合并，属于正常流程内。

---

**总体健康度评估**：****良好**。项目在24小时内保持了稳定的代码贡献，虽活跃度不高，但单个PR质量清晰、目的明确。无积压问题、无社区负面情绪，项目处于可持续演进状态。建议维护者尽快审核PR #1088，确保其对流式参数处理的影响经过充分测试后再合并。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的CoPaw项目数据，为您生成一份结构清晰、数据驱动的2026年5月31日项目动态日报。

---

# CoPaw (QwenPaw) 项目动态日报 | 2026-05-31

## 1. 今日速览

今日社区反馈活跃，主要暴露出两个核心问题：一是Windows平台下执行shell命令时cmd窗口频繁闪烁的Bug未根除，二是`/mission`指令导致控制台完全卡死的严重稳定性问题。尽管有一个相关的Bug报告被关闭，但根本问题的讨论仍在继续。此外，项目在处理非标准API参数和无效配置文件时的健壮性受到了挑战。整体来看，项目处于高活跃度、高用户期待、但面临多个关键Bug亟待解决的阶段。

## 2. 版本发布

无新版本发布。社区对当前版本（v1.1.7, v1.1.9）中存在的Bug反馈集中，预计下一个小版本将主要聚焦于稳定性和Bug修复。

## 3. 项目进展

今日有一个功能型PR被合并，同时一个关键的参数兼容性PR持续受到关注。

- **PR #4810 [CLOSED]：优化聊天输入栏的斜杠技能提示**
  - **内容**：`feat(console): improve chat slash skill suggestions issue#4796`，主要改进了聊天输入框的斜杠命令（`/`）技能建议功能，包括显示当前Agent可用技能、保持提示弹出框紧凑、限制显示数量并增加滚动支持，以及添加调试日志。
  - **意义**：该PR直接提升了日常使用的交互便捷性和流畅度，是用户体验的正向迭代。相关链接：[PR #4810](https://github.com/agentscope-ai/QwenPaw/pull/4810)

- **PR #4689 [OPEN]：路由非标准生成参数到额外请求体**
  - **内容**：`feat(providers): route non-standard generate_kwargs into extra_body`，旨在解决如DashScope的`enable_search`等非标准提供者参数被OpenAI Python SDK静默忽略的问题。
  - **意义**：此PR是今年社区强烈关注的功能之一，若被合并，将大幅增强项目对多模型提供商（尤其是非OpenAI兼容API）的适配能力，是通往更开放生态的关键一步。相关链接：[PR #4689](https://github.com/agentscope-ai/QwenPaw/pull/4689)

## 4. 社区热点

今日社区的热点主要集中在两个Bug报告上，它们吸引了大量评论和关注。

- **Issue #4454：`/mission` 指令导致控制台完全卡死**
  - **热度**：评论4条，创建于5月17日，持续活跃至今。
  - **诉求**：这是一个严重的可用性Bug。用户报告执行核心指令后整个界面无响应，且无法通过常规方法（如清空目录、重置session）恢复。这直接影响了Agent工作流的核心功能，用户对此非常困扰。
  - **分析**：该问题已存在两周，至今未被解决，表明该Bug的根因可能比较复杂，涉及内存管理、消息队列阻塞或任务调度器死锁。相关链接：[Issue #4454](https://github.com/agentscope-ai/QwenPaw/issues/4454)

- **Issue #4123：Windows下执行shell命令闪窗**
  - **热度**：评论8条，是今日评论数最多的议题，创建于5月8日，长期活跃。
  - **诉求**：Windows用户对于执行shell命令时弹出的cmd窗口闪烁体验非常敏感。该问题在多份报告中都被提及（#4123, #4832, #4828），是Windows用户最大的痛点之一。
  - **分析**：尽管有用户提交了修复方案（见#4832），但该问题仍作为长期Bug存在，说明修复可能未能完美处理所有场景，或者尚未被合入主分支。相关链接：[Issue #4123](https://github.com/agentscope-ai/QwenPaw/issues/4123)

## 5. Bug 与稳定性

今日新报告的Bug集中在进程管理和代码逻辑层面，对稳定性和体验影响较大。

- **Bug #4454 [致命]：`/mission` 指令导致控制台完全卡死**
  - **严重性**：灾难级。破坏了核心功能。
  - **状态**：未修复，无关联PR。
  - 相关链接：[Issue #4454](https://github.com/agentscope-ai/QwenPaw/issues/4454)

- **Bug #4834 [严重]：MCP服务器进程积累，导致控制台加载缓慢**
  - **严重性**：高。每次重启服务都会导致进程泄漏，长期运行会显著拖慢系统性能甚至耗尽资源。
  - **状态**：未修复。
  - 相关链接：[Issue #4834](https://github.com/agentscope-ai/QwenPaw/issues/4834)

- **Bug #4123 / #4832 [中高]：Windows下shell命令闪窗**
  - **严重性**：中高。严重影响Windows用户的使用体验和观感。
  - **状态**：用户@felixphong在#4832中指出了根因（缺少`CREATE_NO_WINDOW`标志）并提交了报告，但尚未合并修复。已关闭的#4828很可能是重复报告。
  - 相关链接：[Issue #4123](https://github.com/agentscope-ai/QwenPaw/issues/4123), [Issue #4832](https://github.com/agentscope-ai/QwenPaw/issues/4832)

- **Bug #4835 [中等]：jobs.json中单个无效任务导致整个工作空间启动失败**
  - **严重性**：中。配置文件的健壮性不足，降低了容错率。
  - **状态**：未修复。
  - 相关链接：[Issue #4835](https://github.com/agentscope-ai/QwenPaw/issues/4835)

- **Bug #4833 [中等]：pre_reasoning钩子中内存压缩失败**
  - **严重性**：中。核心代码逻辑异常，可能导致推理性能下降或非预期错误。
  - **状态**：未修复。
  - 相关链接：[Issue #4833](https://github.com/agentscope-ai/QwenPaw/issues/4833)

## 6. 功能请求与路线图信号

今日无新的功能性Issue提出，但PR #4689的持续关注度是一个强烈的路线图信号。它表明社区和贡献者非常渴望项目能**突破单一OpenAI API的限制**，更好地支持DashScope、Anthropic、Gemini等不同厂商的独特参数。

- **信号**：用户不再满足于“能用”，而是要求“好用”和“兼容”。对非标准参数的支持，将是项目吸引更广泛用户群体的关键。

## 7. 用户反馈摘要

- **Windows用户体验是最大短板**：多个用户反复报告“cmd窗口闪烁”问题，甚至有用户被闪烁问题困扰到将此作为唯一反馈内容（#4828），这已成为影响Windows用户留存和使用的首要负面反馈。
- **稳定性是第一要务**：`/mission`命令卡死的Bug表明，在Agent执行复杂或长时间任务时，系统的稳定性仍有很大提升空间。用户对此表现出强烈的挫败感，因为该问题阻碍了工作流的正常进行。
- **用户具备技术洞察力**：用户@felixphong在#4832中直接指出了闪窗问题的代码级根因，展现了社区用户的技术成熟度。项目团队应重视这类来自社区的“根因分析”，快速响应和合入。

## 8. 待处理积压

以下两个老问题应引起维护者的紧迫关注：

- **Issue #4123：Windows Shell闪窗**
  - **状态**：自2026-05-08报告，已有2个相关PR或重复报告（#4828, #4832）。问题讨论时间长，影响用户广，但迟迟没有官方的修复版本。
  - **建议**：优先评估用户@felixphong在#4832中建议的修复方案（添加`CREATE_NO_WINDOW`标志），并进行测试合并。
  - 相关链接：[Issue #4123](https://github.com/agentscope-ai/QwenPaw/issues/4123)

- **Issue #4454：`/mission` 指令卡死**
  - **状态**：自2026-05-17报告，是当前最严重的功能Bug。
  - **建议**：应将此Issue列为**P0（最高优先级）**，分配核心开发者进行排查，并考虑是否需要发布一个热修复版本（Hotfix）。
  - 相关链接：[Issue #4454](https://github.com/agentscope-ai/QwenPaw/issues/4454)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw 项目动态日报 (2026-05-31)

## 1. 今日速览
项目今日整体活跃度极低：过去24小时内仅有1条 Issue 被关闭，无新 Issue、无 Pull Request、无版本发布。关闭的 Issue #609 为自动触发的仓库级安全扫描任务（Codex Security Scan），属于例行维护而非用户驱动的功能或修复。项目当前无待合并 PR 或未关闭的新问题，处于静默维护状态。整体健康度稳定但缺乏可见进展。

## 2. 版本发布
无新版本发布。

## 3. 项目进展
今日无 PR 被合并或关闭，项目功能无任何新增或变更。唯一的活动是 Issue #609 被关闭，该 Issue 完成了一次针对 Webhook 身份路由的代码安全扫描，属于内部自动化流程，对项目外部用户无直接影响。

## 4. 社区热点
无活跃讨论。Issue #609 只有1条评论（作者自关闭），无用户参与。该项目今日无社区热点或高互动议题。

## 5. Bug 与稳定性
今日无新的 Bug、崩溃或回归问题报告。代码库稳定性未受任何已知问题的挑战。

## 6. 功能请求与路线图信号
今日无用户提出新功能请求。结合已有 PR 与 Issue 列表（暂无），暂无明确的下版本功能纳入信号。

## 7. 用户反馈摘要
今日无用户反馈。Issue #609 为自动化安全扫描，不涉及用户痛点或使用场景。

## 8. 待处理积压
无长期未响应的重要 Issue 或 PR。目前项目积压量为零，所有已知问题或任务均已处理完毕。

---

**注**：以上日报完全基于 ZeptoClaw（github.com/qhkm/zeptoclaw）在 2026-05-31 的公开数据生成。若需进一步分析历史趋势或长期积压，请提供更长时间范围的数据。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目日报 — 2026‑05‑31

---

## 1. 今日速览

- 过去 24 小时项目继续保持高活跃度：**50 条 Issue 更新**（新开/活跃 31，关闭 19），**50 条 PR 更新**（待合并 35，合并/关闭 15），无新版本发布。
- 社区焦点集中在**安全与多租户控制**（RBAC、工具权限、进程隔离）以及**核心运行时重构**（providers 架构统一、输出路由模型、cron 管线化）。
- 多个**高风险 RFC**（如 #6909 computer‑use、#6954 路由调度、#6969 统一输出路由）进入讨论，表明项目正在向更通用、更安全的 agent 平台演进。
- 同时有 3 个 **S1 严重性 Bug**（#7022、#5962、#5866）仍处于开放状态，维持者需优先关注。

---

## 2. 版本发布

**无**（过去 24 小时无新 Release）。

---

## 3. 项目进展

以下为今日合并/关闭的重要 PR（数据中未单独列出已合并列表，但根据概览共有 15 个已合并/关闭的 PR，以下为开放 PR 中值得关注的较大改动，部分可能已接近合并）：

- **#7030 – Loop improvements + agent‑directed provider selection**  
  (作者: richard‑deliveryboy)  
  包含 Workstream A（对话循环全面重构：上下文管线、流式工具执行、退避重试、钩子治理、上下文折叠等 28 项）和 Workstream B（agent 可委托工具时指定 provider）。这是近期最重要的运行时改进之一。  
  [PR #7030](https://github.com/zeroclaw-labs/zeroclaw/pull/7030)

- **#7036 – feat(web): add ACP console**  
  (作者: Audacity88)  
  在 Web UI 中添加 `/acp-console` 控制台，维护者可通过 Web 界面直接调用网关 ACP 端点，提升调试和运维体验。  
  [PR #7036](https://github.com/zeroclaw-labs/zeroclaw/pull/7036)

- **#6924 – feat(skills): scoped tool elevation for built‑in and MCP tools**  
  (作者: alex‑nax)  
  实现技能范围内临时提升工具权限，允许 skill 在执行期使用 `allowed_tools` 之外的工具，同时保持安全隔离。对应 RFC #6915。  
  [PR #6924](https://github.com/zeroclaw-labs/zeroclaw/pull/6924)

- **#7034 – fix(channels/whatsapp‑web): match LID bot mentions**  
  (作者: rifuki)  
  修复 WhatsApp Web 频道中 `mention_only` 模式无法识别 LID JID 提及的问题。  
  [PR #7034](https://github.com/zeroclaw-labs/zeroclaw/pull/7034)

- **#7035 – fix(channels/media‑pipeline): inline image data for vision**  
  (作者: rifuki)  
  修复媒体管线中视觉路径未正确内联图片数据的问题。  
  [PR #7035](https://github.com/zeroclaw-labs/zeroclaw/pull/7035)

> 项目在**安全管控**、**Web 可观测性**、**频道适配**和**运行时鲁棒性**上均有实质推进。

---

## 4. 社区热点

| Issue / PR | 标题 | 评论数 | 核心诉求 |
|-----------|------|--------|----------|
| [#5937](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) | [Feature]: refactor: Unify providers architecture and reqwest client management | 9 | 重构 providers 模块，解决 `reqwest` 客户端和模型参数的不一致与重复代码，属于架构级改进。 |
| [#5982](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) | [Feature]: Per‑sender RBAC for multi‑tenant agent deployments | 8 | 要求为多租户场景添加基于发送者的角色权限控制（RBAC），隔离工作区、工具集和系统提示。 |
| [#4842](https://github.com/zeroclaw-labs/zeroclaw/issues/4842) | [Bug]: update command downloads wrong architecture binary on aarch64 (Raspberry Pi) | 7 | aarch64 设备执行 `zeroclaw update` 时下载错误的 x86_64 二进制，导致“Exec format error”。已关闭，表明已修复。 |
| [#6647](https://github.com/zeroclaw-labs/zeroclaw/issues/6647) | [Bug]: Cron job output not routed to configured channels | 4 | 定时任务结果仅出现在 Web 仪表盘，未路由到配置的渠道（如 Telegram）。已关闭，可能已修复。 |
| [#6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909) | [Feature]: computer‑use support (screen interaction like Codex / Peekaboo) | 4 | 请求为 agent 添加桌面 GUI 交互能力（截图、鼠标/键盘事件），类似 OpenAI Codex。获得 0 个 👍，但讨论热烈。 |
| [#6969](https://github.com/zeroclaw-labs/zeroclaw/issues/6969) | RFC: unified output routing model (per‑peer modality preference + agent send_via tool) | 3 | 用户从 Letta 迁移后反馈无法控制回复的“方式和位置”，建议统一输出路由模型。 |

- **趋势**：社区的核心关注点从单一功能转向**多租户安全**、**架构统一**和**高级交互模式**（桌面控制、意图路由）。

---

## 5. Bug 与稳定性

按严重程度排列（S1 = 工作流阻塞，S2 = 行为降级）：

| 编号 | 标题 | 严重度 | 状态 | 关联修复 |
|------|------|--------|------|----------|
| [#7022](https://github.com/zeroclaw-labs/zeroclaw/issues/7022) | [Bug]: kimi‑k2.6 fails with 400 invalid temperature because compatible.rs always sends baseline 0.7 | **S1** | OPEN | 无 PR |
| [#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962) | [Bug]: Ollama Provider call failed when tools are needed | **S1** | OPEN | 无 PR |
| [#5866](https://github.com/zeroclaw-labs/zeroclaw/issues/5866) | [Bug]: in the Telegram group bot ignores replies on its messages when mention_only=true | **S1** | OPEN | 无 PR |
| [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) | [Bug]: Gemini CLI OAuth is simply not working | **S1** | OPEN | 无 PR |
| [#5122](https://github.com/zeroclaw-labs/zeroclaw/issues/5122) | [Bug]: web_fetch allowed_private_hosts list is essentially useless for domain names that resolve to private IPs | **S2** | OPEN | 无 PR |
| [#6876](https://github.com/zeroclaw-labs/zeroclaw/issues/6876) | risk_profile.allowed_tools does not restrict MCP tools — by design or documentation gap? | **S1** | OPEN | 相关 PR #6914（已提案） |
| [#6916](https://github.com/zeroclaw-labs/zeroclaw/issues/6916) | feat: process‑memory limits on shell/skill_tool subprocess execution | **S1** | OPEN | 无 PR（属增强请求，但可缓解 OOM） |
| [#4842](https://github.com/zeroclaw-labs/zeroclaw/issues/4842) | update command downloads wrong architecture binary on aarch64 | **S1** | **CLOSED** | 已修复 |
| [#6647](https://github.com/zeroclaw-labs/zeroclaw/issues/6647) | Cron job output not routed to configured channels | **S1** | **CLOSED** | 已修复 |

- 今日无 S0（服务完全不可用）级别的 Bug 报告。
- **需优先关注**：#7022（Kimi 兼容 provider 必现 400）、#5962（Ollama 工具调用阻塞会话）、#5866（Telegram 群组回复忽略）。

---

## 6. 功能请求与路线图信号

以下为今日最可能纳入下一版本的增强请求（已有对应 RFC 或 PR 支持）：

| 请求 | 对应 RFC/PR | 说明 |
|------|-------------|------|
| [#5937](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) 统一 providers 架构 | 无直接 PR，但属架构级重构 | 影响所有 provider 消费者，可能为 v0.9 的基础工作 |
| [#5982](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) 多租户 RBAC | 无直接 PR | 需求强烈，与安全路线图密切相关 |
| [#6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909) computer‑use 支持 | 无 PR | 引用 OpenClaw 同类项目，可能成为差异化功能 |
| [#6954](https://github.com/zeroclaw-labs/zeroclaw/issues/6954) 路由定时任务通过 orchestrator 管线 | 无 PR | 解决一组回归 Bug（#6037, #6105, #6648 等）的最简方案 |
| [#6969](https://github.com/zeroclaw-labs/zeroclaw/issues/6969) 统一输出路由模型 | 无 PR | 用户从 Letta 迁移痛点，提升可配置性 |
| [#6850](https://github.com/zeroclaw-labs/zeroclaw/issues/6850) 解耦 memory 策略层 | RFC | 允许插拔检索与合并策略 |
| [#6914](https://github.com/zeroclaw-labs/zeroclaw/issues/6914) 强制 agent 循环中的工具白名单 | 关联 PR #6914（草稿） | 修复 MCP 工具绕过 `allowed_tools` 的安全问题 |
| [#6915](https://github.com/zeroclaw-labs/zeroclaw/issues/6915) skill‑scoped 临时提权 | PR #6924（已提交） | 正在审查中 |

> 路线图信号：**安全管控**（RBAC、工具白名单、进程限制）、**架构解耦**（providers、memory）和**高级交互**（computer‑use、输出路由）是当前三大方向。

---

## 7. 用户反馈摘要

从 Issues 评论中提炼的真实用户声音：

- **Ollama 用户**（#5962）： *“Throws error blocks sending any message again in the same session”* — 使用 Ollama 时一旦工具调用失败，整个会话被阻塞，无法继续交互，属于严重工作流阻断。
- **Telegram 群组用户**（#5866）： *“If you reply to the bot messages in the Telegram group, you will get ignored until bot directly mentioned with mention_only=true”* — 期望直接回复 bot 消息时被响应，但当前实现忽略回复，必须 @bot 才能触发。
- **Kimi/K2.6 用户**（#7022）： *“always sends baseline 0.7 temperature”* — 使用 Moonshot/Kimi 兼容 provider 时，即使未配置 `temperature`，代码仍发送 0.7，导致 API 返回 400 错误。
- **Gemini CLI 用户**（#4879）： *“Right after successfully authenticated Gemini CLI: Error: All providers/models failed”* — 完成 OAuth 认证后立即获得 rate_limited 错误，工作流完全阻塞，且无有效 workaround。
- **aarch64 用户**（#4842，已修复）： *“`zeroclaw update` fails on aarch64 (ARM64) systems with 'Exec format error'”* — 更新功能自动下载了错误架构的二进制，用户需手动下载，影响树莓派和 ARM 服务器用户。
- **迁移自 Letta 的用户**（#6969）： *“I recently migrated from Letta to ZeroClaw and one behaviour I relied on heavily is gone: the ability to control *how* and *where* a reply is delivered”* — 期望保留对回复渠道和方式的精细控制，当前模型只能被动响应。

---

## 8. 待处理积压

以下为长期未解决（超过一个月）且仍处于开放状态的关键 Issue 或 PR，提醒维护者关注：

| 编号 | 标题 | 创建日期 | 最后活跃 | 积压原因 |
|------|------|----------|----------|----------|
| [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) | [Bug]: Gemini CLI OAuth is simply not working | 2026-03-28 | 

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*