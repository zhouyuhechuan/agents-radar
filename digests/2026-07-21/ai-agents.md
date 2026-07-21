# OpenClaw 生态日报 2026-07-21

> Issues: 353 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-07-21 01:57 UTC

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

好的，作为您的 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据 OpenClaw 项目的 GitHub 数据，为您生成了 2026-07-21 的项目动态日报。

---

# OpenClaw 项目日报 - 2026年7月21日

## 1. 今日速览

今日 OpenClaw 项目保持了高度活跃的社区动态，在过去 24 小时内产生了 **353 条 Issue 更新** 和 **500 条 PR 更新**。社区讨论主要集中在会话稳定性、消息丢失和安全性等核心痛点上，并涌现了大量旨在提升用户体验和修复关键回归问题的 Pull Request。虽然项目并无新的正式版本发布，但从 PR 的活跃程度和议题讨论的热度来看，项目正处于一个高密度的修复和功能迭代期，项目健康度良好，社区响应积极。

## 2. 版本发布
*(今日无新版本发布)*

## 3. 项目进展

今日项目在修复关键回归问题、提升系统稳定性方面取得了重要进展。多個曾被标记为“白金级”（最高优先级）的问题已经被关闭或提交了关键修复 PR。

- **关键回归问题修复**: `#88312`，一个影响 Codex 应用服务器，导致多工具代理回合在高版本卡死的严重回归问题，已于今日被成功关闭。该问题曾被视为 `#84076` 的回归，其修复 PR 为 `#85107`。这一进展标志着项目在解决因版本迭代引入的复杂并发问题方面迈出了坚实一步。
- **核心功能增强与修复**: PR `#93218`（新增会话流模式命令）和 PR `#93247`（修复诊断系统在失败恢复后的空闲状态问题）均处于活跃状态，持续受到维护者和社区贡献者的关注，它们分别旨在提升用户对消息预览的控制和增强系统自愈能力。
- **多家平台适配优化**: 针对非主流或特定区域平台的 PR 持续进行合并或进入审查阶段，包括针对 **QQ 机器人**（`#110008`, `#110002`）、**Microsoft 语音服务**（`#110784`）和 **Kilocode 扩展**（`#109950`）的修复，显示了项目对生态多样性的持续投入。

## 4. 社区热点

今日社区讨论的焦点集中在几个长期存在且严重影响用户体验的问题上：

- **最受关注的 Issue**: `#99241` (`[P1] Tool outputs sometimes render as image attachments and become unreadable to the agent`) 以 **23条评论** 位居榜首。用户@aaajiao 的描述精准地戳中了痛点：在长时运行或带有大量 ANSI 输出的工具工作流中，输出会“坍缩”成一个图片占位符，导致 AI 代理无法读取关键的 stdout/stderr 文本。该问题引发了社区对代理“视觉盲区”的普遍担忧，讨论集中于如何避免这种信息丢失。

- **会话状态丢失与中断**: `#88312`（已关闭）和 `#87744`（开放中）均聚焦于代理会话在完成前被“卡住”或“超时”的问题。用户@yair 和@adamamzalag 的详细报告回溯了问题出现的具体版本号，并提供了明确的复现步骤，显示出用户对软件质量有较高要求，并愿意投入精力帮助开发者 Debug。

- **安全与信任**: `#10659`（`[P1] Feature Request: Masked Secrets`）获得了 **15条评论** 和 **4个点赞**，是目前最受关注的安全类需求。用户@jmkritt 提出了一个“好点子”：让 AI 代理能“用”API 密钥但不“看”到它们。这反映了社区对日益增长的提示注入攻击和凭证泄露风险的深度忧虑。

## 5. Bug 与稳定性

除上述社区热点外，今日还报告了多个影响系统稳定性的 Bug，按严重程度排列如下：

- **[P1] 上下文管理问题**:
    - `#108215` (`[Bug]: Context usage drops from 57% to 13% without compaction after large tool output`)：用户在大型工具输出后，上下文使用率异常下降，可能影响后续会话的连贯性。**尚无可用的修复 PR**。
    - `#108238` (`[Bug]: 2026.7.1 中会话上下文用量把累计 cacheRead 算进 totalTokens`)：一个中文化社区报告，明确指出最新版本中计算上下文 token 时存在逻辑错误，会导致虚假的上下文超限和压缩失败。**尚无可用的修复 PR**。该问题清晰体现了项目在应对大上下文模型时的计算逻辑仍需打磨。

- **[P1] 模型与供应商兼容性**:
    - `#109017` (`[Bug]: Anthropic provider disappears from model picker...`)：报告了 Anthropic 供应商在新版中从模型选择器中消失的问题，严重影响了依赖 Claude 的用户。**尚无可用的修复 PR**。

- **[P1] 网关与稳定性**:
    - `#56733` (`Gateway process alive but event loop frozen`)：虽然是一个较老的 Issue，但今日仍有更新，表明网关在特定条件下（如 WSL2）的“假死”问题依然存在并受到关注。**尚无可用的修复 PR**。

- **回归问题**:
    - `#99586` (`[Bug]: Runtime tool surface returns blank body after gateway-touching operations`)：框架工具表面在执行网关相关操作后返回空白，需要容器重启才能临时解决。**有相关 PR，但状态未知**。

## 6. 功能请求与路线图信号

今日的新增和活跃的功能请求显示了用户群体对安全性和可配置性的强烈需求，部分请求已有对应的 PR 在处理。

- **安全与权限**:
    - `#12219` (`[Feature]: Skill Permission Manifest Standard (skill.yaml)`)：提出为技能（Skills）建立标准化的权限描述文件。结合已有的 `#10659`（Masked Secrets）和 `#6615`（exec-approvals 黑名单），一个更全面、细粒度的安全模型正在社区中成型，这可能成为下一版本的安全特性基石。
    - 对应 PR: `#81185` (`Redact exec tool result payloads`) 正在审查中，有望在下一版本中直接禁止 `exec` 工具输出原始凭据。

- **代理行为控制**:
    - `#8299` (`[Feature request]: config option to suppress sub-agent announce`)：用户希望配置选项来禁止子代理运行后自动发布总结，以减少群聊中的信息噪音。
    - `#9912` (`Feature: Add maxTurns/maxToolCalls config option to limit agent iterations`)：用户提出为代理的迭代次数设置上限，以防止部分模型陷入死循环或忽略系统指令。这两个请求直指当前 AI 代理存在的行为不可控问题，预计会在后续版本中得到规范化。

- **模型配置**:
    - `#80752` (`[Feature request]: optional model override in CommitmentsConfig`)：用户希望能够在 `CommitmentsConfig` 中为“承诺”功能指定独立模型，以复用已有配置模式。
    - `#6599` (`Feature: Add /models test-fallback command to verify fallback chain`)：用户请求添加一个命令来测试模型降级链是否正常工作，避免了“靠运气”等待故障发生。

## 7. 用户反馈摘要

从今日的 Issue 评论和摘要中，可以提炼出以下真实用户痛点：

- **“代理看不到我看得到的东西”**: 用户在 `#99241` 中抱怨，当工具输出变成图片后，AI 代理就变成了“瞎子”，无法读取关键的文本信息（如编译错误、日志内容）。这导致了“代理无法解决自己工具产生的输出”这一悖论，用户体验极差。
- **“它承诺了，但什么都没做”**: Issue `#58450` 描述了代理在对话结尾声称“我会检查一下然后跟进”，但实际上并未启动任何后台动作。这种行为让用户感觉被 AI “忽悠”了，破坏了信任感。
- **“我的 Telegram 机器人老是超时”**: 用户@adamamzalag 在 `#87744` 中详细描述了 Telegram 会话在 `2026.5.27` 更新后频繁超时，代理在后台完成了工作但最终回复无法送达，这直接导致了“机器人坏了”的负面印象。
- **“我不想让 AI 看到我的密钥，只想让它用”**: 用户@jmkritt 在 `#10659` 中提出了一个非常技术但又贴近普通用户的痛点。他们不想在 `.env` 文件中明文存储强敏感信息，担心被 AI 代理意外泄露或泄漏，这反映了对 AI 安全边界的普遍焦虑。
- **“特定平台用不了”**: 来自不同平台的用户报告了各种兼容性问题。

## 8. 待处理积压

以下为长期未响应的、高优先级或社区讨论激烈的重要 Issue，提醒维护者关注：

- **安全与信任**:
    - `#7707` (`[P2] Feature Request: Memory Trust Tagging by Source`)：自 2026年2月提出，已有 **19条评论**，讨论了如何通过来源信任标记来防御记忆投毒攻击。这是一个影响深远且设计复杂的架构级特性，但长时间“待审核产品决策”。**无关联 PR**。
    - `#12219` (`[P2] [Feature]: Skill Permission Manifest Standard`)：同样是安全架构的核心特性，提出已超 5 个月，仍无实质性进展。**无关联 PR**。

- **平台稳定性**:
    - `#58514` (`[P1] [Bug]: Google Chat: Space/Group messages silently ignored`)：Google Chat 群组消息被“静默忽略”的问题在 3月底提出，至今仍为开放状态，对于使用谷歌生态的用户来说影响很大。**无关联 PR**。

- **UX/功能缺陷**:
    - `#78734` (`[Feature Request]: 配置选项以抑制子代理宣告`) (已合并至 #8299)：虽已有关联 PR，但问题的根本解决方案（提供一个稳定的配置选项）仍在讨论中，而非依赖模型回复 `ANNOUNCE_SKIP` 这种脆弱的方式。**有相关 PR，但问题本身未被关闭**。

- **亟待审核的 PR**:
    - `#81185` (`Redact exec tool result payloads`)：被标记为“白金级”重要性的 PR，其功能直接关系到系统的核心安全，目前已准备好进行维护者审查，应优先处理。
    - `#86450` (`test(cli): add focused coverage for node CLI daemon`)：提升测试覆盖率的 PR，虽然优先级不是最高，但对于长期的项目健康度和代码重构至关重要，不应被忽略。

---

## 横向生态对比

好的，作为您的专属技术分析师，我已根据您提供的各项目2026年7月21日动态数据，为您生成一份全面的横向对比分析报告。

---

### **AI智能体与个人AI助手开源生态横向对比分析报告 (2026-07-21)**

报告日期：2026-07-21
报告人：资深技术分析师

#### **1. 生态全景**

当前，个人AI助手与自主智能体开源生态处于 **“高速分化与深度整合”** 的十字路口。一方面，以 **Hermes Agent** 为代表的头部项目通过大版本发布（v0.19.0）和极高的代码贡献量，在功能丰富度和社区规模上持续扩张，但也面临着版本迭代过快带来的稳定性挑战。另一方面，以 **OpenClaw** 和 **ZeroClaw** 为代表的生态核心项目，正从功能扩展转向 **“质量巩固”与“安全可信”**，其社区讨论焦点高度集中在会话一致性、多工具调用可靠性、凭证保护与权限管理等痛点。值得注意的是，**NanoBot** 和 **CoPaw** 等中坚力量在性能优化（特别是本地模型缓存）、多智能体协作和特定平台适配（如飞书、QQ频道）上取得了实质性进展。然而，**NullClaw** 和 **Moltis** 等项目的长期停滞也表明，并非所有生态玩家都能跟上迭代节奏，生态内部已出现明显的活跃度分层和资源聚集效应。

#### **2. 各项目活跃度对比**

| 项目名称 | Issues 更新 | PRs 更新 | 版本发布 | 健康度评估 | 活跃度评级 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 353 | 500 | 无 | 高，迭代密集，社区响应积极 | ★★★★★ |
| **Hermes Agent** | 50 | 50 | **v0.19.0** | 极高，功能迭代与Bug修复并行，但存在严重回归 | ★★★★★ |
| **ZeroClaw** | 39 (30新开/活跃) | 50 (12合并) | 无 | 高，核心Bug修复迅速，评估框架进入冲刺期 | ★★★★☆ |
| **NanoBot** | 7 | 30 (11合并) | 无 | 高，开发效率高，核心架构重构稳步推进 | ★★★★☆ |
| **CoPaw** | 30 | 42 | 无 | 高，社区贡献活跃，多工具推理问题是焦点 | ★★★★☆ |
| **IronClaw** | 大量 (Bug Bash) | 大量 | 无 | 高，架构迁移关键期，质量攻坚阶段 | ★★★★☆ |
| **NanoClaw** | 6 | 20 | 无 | 较高，但存在严重权限安全漏洞已修复 | ★★★☆☆ |
| **PicoClaw** | 11 | 10 (5合并) | 无 | 中等，Antigravity提供商回归问题需高度关注 | ★★★☆☆ |
| **LobsterAI** | 0 (新Issue) | 15 (10合并) | 无 | 高，协作功能增强与稳定性修复上表现稳健 | ★★★☆☆ |
| **TinyClaw / Moltis** | - | - | - | 无活动 | ★☆☆☆☆ |
| **NullClaw** | - | 1 (Dependabot) | 无 | 停滞，社区互动为零 | ★☆☆☆☆ |
| **ZeptoClaw** | - | - | - | 无活动 | ☆☆☆☆☆ |

*注：活跃度评级综合考量了Issues/PRs数量、版本发布频率、社区讨论质量和问题响应速度。*

#### **3. OpenClaw 在生态中的定位**

OpenClaw 在今日数据中展现出 **“生态核心参照物”** 的定位。

- **优势在于其** **生态多样性** 和 **稳定性修复的深度**。其对 QQ 机器人、Microsoft 语音服务等非主流平台的适配，以及针对 Codex 应用服务器回归问题（#88312）的成功修复，体现了其作为 **“平台级”项目** 的广度和深度。
- **技术路线** 上，OpenClaw 与 **ZeroClaw** 高度相似，都注重底层架构的健壮性和扩展性。不同点在于，OpenClaw 的社区讨论更偏向于 ****“用户体验”层面**（如会话稳定性、信息丢失），而 ZeroClaw 则更侧重于 **“评估与治理”层面**（如评估框架、SOP控制面）。
- **社区规模** 上，OpenClaw 的 Activity 指标（353 Issue, 500 PR）仅次于 **Hermes Agent**，但后者得益于一次大版本发布。OpenClaw 的社区贡献更加“细水长流”，议题讨论质量高，尤其在 **安全（Masked Secrets）** 和 **可操作性（抑制子代理宣告）** 方面，社区诉求与解决方案的推动形成了良好闭环。

#### **4. 共同关注的技术方向**

| 技术方向 | 涉及项目 | 具体诉求/现象 |
| :--- | :--- | :--- |
| **多工具调用可靠性** | **OpenClaw**, **CoPaw** | OpenClaw：工具输出“坍缩”成图片（#99241）；CoPaw：多工具调用产生相同推理（#6257）。核心是**推理一致性与输出可读性**。 |
| **安全与凭证管理** | **OpenClaw**, **NanoBot**, **NanoClaw**, **IronClaw** | OpenClaw：`Masked Secrets` (#10659)；NanoBot：API Key明文存储 (#4803)；NanoClaw：权限系统绕过；IronClaw：Gmail扩展自动授权 (#6348)。 **信任边界与最小权限原则**是共识。 |
| **跨平台兼容性** | **ZeroClaw**, **PicoClaw**, **OpenClaw** | ZeroClaw：Windows CI缺失 (#7462)；PicoClaw：Android启动困难 (#3182)；OpenClaw：持续集成QQ、Microsoft语音等。**一等的跨平台体验**是用户刚需。 |
| **代理行为可控性** | **OpenClaw**, **CoPaw**, **Hermes Agent** | OpenClaw：`maxTurns` (#9912)；CoPaw：自定义Agent模式 (#6270)、内置“询问用户”工具 (#6274)；Hermes Agent：可配置快捷键 (#4256)。**用户对Agent行为的可预期性和可干预性**要求提升。 |
| **评估与可观测性** | **ZeroClaw**, **IronClaw**, **NanoBot** | ZeroClaw：`zeroclaw eval` 框架进入冲刺期；IronClaw：Langfuse追踪优化；NanoBot：Ollama缓存诊断指南 (#4998)。**量化代理表现、诊断性能瓶颈**成为开发者刚需。 |

#### **5. 差异化定位分析**

- **OpenClaw & ZeroClaw**：做 **“操作系统”**。追求极致的稳定、安全与标准化，目标是成为开发者的基础设施。ZeroClaw 更偏向企业级治理和安全（A2A、SOP），OpenClaw 更偏向社区驱动的功能和生态包容性。
- **Hermes Agent**：做 **“旗舰机”**。版本迭代最快，功能最丰富，社区规模最大。但也因“速度”牺牲了一定的稳定性。适合追求最新特性和前沿功能的“尝鲜”用户。
- **NanoBot & NanoClaw**：做 **“领域的瑞士军刀”**。专注于特定平台或性能场景。NanoBot 对 Ollama 性能优化极为重视，是本地模型玩家的首选；NanoClaw 在即时通讯软件（LINE, Dial）集成上独具特色，目标用户明确。
- **CoPaw & PicoClaw**：做 **“生态的探索者”**。CoPaw 在多智能体协作（多Subagent）和系统集成（Kanban）上积极尝试；PicoClaw 则关注极客和边缘计算场景（Sipeed硬件），坚持“小而美”。
- **IronClaw**：做 **“重构的先锋”**。当前处于向全新Reborn架构迁移的关键期。虽然引入了短期动荡，但长期来看，其“脱胎换骨”式的架构升级，为解决遗留技术债务和支撑未来复杂功能铺平了道路。

#### **6. 社区热度与成熟度**

- **快速迭代阶段**：
  - **Hermes Agent**：版本号 v0.19.0 证明了其迭代速度。社区贡献者超450人，但伴随而来的是v0.19.0的严重回归问题（进程误杀），处于“高速度、高风险”状态。
  - **ZeroClaw**：评估框架（`zeroclaw eval`）系列PR的密集提交，表明其正快速接近一个关键功能里程碑。同时，其对SOP和供应链安全的重视，显示出项目正从“能用”向“好用/可控”快速迈进。
- **质量巩固阶段**：
  - **OpenClaw**：在经历了密集的功能迭代后，项目正将大量精力投入到修复回归问题、提升稳定性和解决用户核心痛点上。社区讨论以 Bug 报告和功能请求为主，体现出成熟期的“精雕细琢”特征。
  - **IronClaw**：随着架构迁移大部分完成，项目进入了“高质量交付”攻坚期。内部Bug Bash活动就是最直接的证明，目标是为Reborn架构的正式可用扫清障碍。
- **稳定维护/低活跃阶段**：
  - **LobsterAI**：虽然每日有PR合并，但多为内部团队主导，且缺乏社区互动。项目更多是在一个相对稳定的状态下进行特定功能的增强和修复。
  - **NullClaw / ZeptoClaw / TinyClaw**：处于低活跃甚至停滞状态，项目健康度面临挑战。

#### **7. 值得关注的趋势信号**

1.  **安全是AI Agent的“阿喀琉斯之踵”**：来自 OpenClaw, NanoBot, NanoClaw 等多个项目的反馈一致表明，**凭证保护（API Key、Secret）、权限细粒度管理和供应链安全（技能安装审查）** 已成为所有项目方和用户的核心焦虑点。这预示着下一阶段的竞争焦点将从“功能多少”转向“安全可信”，能提供开箱即用的、细粒度的、透明安全方案的项目将获得更多青睐。
2.  **“我能看到你，但你看不到我”的信任危机**：OpenClaw 的 `#99241`（工具输出变图片导致Agent“失明”）和 `#10659`（向Agent隐藏密钥）等议题，本质上是 **Agent 与人类之间信息不对等带来的信任问题**。开发者需要设计更透明的信息流和“人类-代理”协作界面（Human-in-the-Loop），让人类能监控和验证代理的决策过程。
3.  **评估体系的缺位与觉醒**：ZeroClaw 对 `zeroclaw eval` 框架的押注，以及 IronClaw 对 Langfuse 的集成优化，是一个强有力的信号。当Agent系统变得足够复杂时，**缺乏量化评估工具将成为项目从“玩具”走向“工具”的最大瓶颈**。一个标准、可复现、多维度（成本、准确率、效率）的评估框架，将成为成熟项目的基础设施标配。
4.  **从“单打独斗”到“群智涌现”**：CoPaw 中要求“询问用户”的工具、NanoBot 中要求“多智能体协作”的提案，以及 Hermes Agent 中不断完善的内置技能子代理系统，共同指向了 **Agent 系统内部及与人类之间的复杂协作模式**。未来的AI助手不再是孤立的对话体，而是能够调用工具、委托子任务、并在必要时向人类寻求指导的“动态团队”。

**对 AI 智能体开发者的建议**：当前阶段，若您是个人开发者或初创团队，建议**优先关注 OpenClaw 或 ZeroClaw**，它们提供了较强的稳定性和社区支持，可以作为构建上层应用的“基石”。若您专注于特定平台或性能场景（如本地模型），**NanoBot** 和 **NanoClaw** 是绝佳的参考。若您追求技术前沿和功能齐全，**Hermes Agent** 是不错的风险投资，但需做好应对版本不稳定性的准备。无论选择哪个项目，**安全、可解释性与可评估性**，将是决定您产品最终成败的三个关键维度。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据NanoBot项目（github.com/HKUDS/nanobot）2026年7月21日数据生成的项目动态日报。

---

## NanoBot 项目动态日报 | 2026-07-21

### 1. 今日速览

项目今日活跃度极高，尤其在代码贡献方面。过去24小时内，项目库迎来了 **30条 Pull Request** 的更新，其中有 **11条** 已被合并或关闭，展现了非常高的协作效率和开发强度。社区讨论保持平稳，Issues 更新量为7条，其中包含3个已解决的 Bug。项目稳定地向新功能推进，重点聚焦于**性能优化**（特别是 Ollama 缓存）、**多智能体协作**、**安全性提升**以及**非技术用户部署体验**的改善。

### 2. 版本发布
无新版本发布。

### 3. 项目进展

今日项目核心进展体现在重要PR的合并与关闭，项目在稳定性、可用性和架构优化上迈出了坚实一步：

- **核心机制重构**：PR [#4993](https://github.com/HKUDS/nanobot/pull/4993) 已合并。该PR重构了内部对话（如子代理结果）的生命周期管理，统一了状态机，修复了重复处理、恢复、存储等多个环节的潜在问题。这为后续更复杂的多智能体协作和稳定的子代理结果传递打下了坚实基础。
- **核心Bug修复**：
    - 针对社区长期反馈的痛点，PR [#4768](https://github.com/HKUDS/nanobot/pull/4768) 已合并。该修复为QQ频道的WebSocket重连机制增加了**指数退避**策略，解决了DNS故障时日志洪水的问题，显著提升了在弱网环境下的稳定性。
    - 团队还修复了飞书 (PR [#4982](https://github.com/HKUDS/nanobot/pull/4982)) 和 Telegram (PR [#4981](https://github.com/HKUDS/nanobot/pull/4981)) 频道在特定边界条件下因文本分割导致的无限循环问题 (loop hang)，提升了多平台消息处理的鲁棒性。
- **新功能与特性**：
    - PR [#5007](https://github.com/HKUDS/nanobot/pull/5007) 和 [#4937](https://github.com/HKUDS/nanobot/pull/4937) 分别增加了 **Dokploy (PR #5007)** 和 **Render (PR #4937)** 的一键部署模板，降低了非技术用户的自托管门槛。
    - PR [#5009](https://github.com/HKUDS/nanobot/pull/5009) 为飞书频道新增 `groupPolicy: listen` 模式，允许群聊内容静默积累为上下文，仅在 `@提及` 时响应，提升了群聊体验。
- **性能与诊断**：团队响应了社区关于Ollama的反馈，合并了PR [#4998](https://github.com/HKUDS/nanobot/pull/4998)，专门为Ollama的**工具调用提示缓存**提供了诊断指南和优化模板，帮助用户定位和解决性能瓶颈。

### 4. 社区热点

过去24小时内，最受关注的议题是 **Ollama的缓存和性能优化**。

- **热点 Issue**: [#4867](https://github.com/HKUDS/nanobot/pull/4867) **[CLOSED]** “Preserve exact prompt prefix to enable caching in Ollama and others”
    - **分析**: 该Issue获得了15条评论，是过去24小时最活跃的讨论。用户 `The-Markitecht` 强烈投诉了与Ollama配合使用时，每轮对话都有“额外60秒”的延迟，使本地模型（32GB VRAM）**完全不可用**。核心诉求是保留精确的提示前缀，以便Ollama等模型的KV缓存机制生效。这不仅是用户痛点，也是影响本地模型性能的关键问题。该议题已在社区和开发者的共同努力下关闭，并且相关修复PR [#4998](https://github.com/HKUDS/nanobot/pull/4998) 也已合并，表明开发团队对此高度重视并迅速响应。

### 5. Bug 与稳定性

过去24小时内报告的Bug已基本得到响应，部分已有修复方案：

| 严重程度 | Bug 描述 | 状态 | 对应 PR |
| :--- | :--- | :--- | :--- |
| **严重** | [#4864](https://github.com/HKUDS/nanobot/pull/4864) `complete_goal` 工具因网关解析错误导致**无限循环**。由于参数序列化变更，工具调用后无法正常结束。 | 已开启，社区正在讨论 | 暂无，用户初步定位为网关问题 |
| **严重** | [#4803](https://github.com/HKUDS/nanobot/pull/4803) **安全漏洞**：API Key 以明文形式存储在配置文件中，尽管 `repr` 被隐藏，但 `model_dump()` 时仍会导出。 | 已开启 | PR [#5010](https://github.com/HKUDS/nanobot/pull/5010) 已提出，建议使用环境变量引用 |
| **中等** | (已修复) [#4767](https://github.com/HKUDS/nanobot/pull/4767) QQ频道在DNS/网络故障时，WebSocket重连循环产生**大量错误日志**。 | 已关闭 | PR [#4768](https://github.com/HKUDS/nanobot/pull/4768) 已合并 |
| **低危** | (已修复) [#4982](https://github.com/HKUDS/nanobot/pull/4982) 飞书频道 `_fallback_text_chunks` 在 `limit <= 0` 时**卡死 (hang)**。 | 已关闭 | 已合并 |
| **低危** | (已修复) [#4981](https://github.com/HKUDS/nanobot/pull/4981) Telegram频道 `_split_telegram_markdown` 在 `max_len <= 0` 时**卡死 (hang)**。 | 已关闭 | 已合并 |

**分析**: 目前最危险的Bug是[#4864](https://github.com/HKUDS/nanobot/pull/4864)的无限循环，可能导致系统资源耗尽。安全漏洞[#4803](https://github.com/HKUDS/nanobot/pull/4803)也是重大隐患，需尽快处理。好消息是，大部分报告的低级Bug和之前报告的QQ频道问题均已修复，显示出项目维护者快速的响应和修复能力。

### 6. 功能请求与路线图信号

过去24小时有几个重要的功能请求和趋势信号，可能会影响未来版本方向：

- **多智能体协作 (Multi-Agent Collaboration)**：Issue [#5000](https://github.com/HKUDS/nanobot/pull/5000) 提出了将当前“子代理系统”进化为真正的“多智能体协作系统”，要求子代理拥有持久身份、共享任务状态和代理间通信能力。该提案获得了关注，且作者在 [#4999](https://github.com/HKUDS/nanobot/pull/4999) 又提交了一次（可能是误操作但已被关闭）。这标志着社区对更复杂、更智能的工作流有明确需求。
- **一键部署 (One-Click Deploy)**：来自Issue [#1503](https://github.com/HKUDS/nanobot/pull/1503) 的 Dokploy 模板请求，已由 PR [#5007](https://github.com/HKUDS/nanobot/pull/5007) 实现。结合已合并的 Render 部署模板，项目正在系统性地降低成本，覆盖更多非技术用户。
- **增强安全性**：PR [#5006](https://github.com/HKUDS/nanobot/pull/5006) 提出了一个“守护工具网关”（Guarded Tool Gateway），为频道插件提供可选的、安全的工具调用环境。这是对[#4803](https://github.com/HKUDS/nanobot/pull/4803)等安全问题的一个积极回应。
- **Agent输出优化**：PR [#4963](https://github.com/HKUDS/nanobot/pull/4963) 是一个重要的WebUI优化，它将原始、嵌套的工具日志替换为统一、清晰的活动语言，并优化了流式输出的渲染，旨在提升用户体验。这表明开发者在关注底层架构的同时，也在打磨用户可见的前端交互。

### 7. 用户反馈摘要

来自 Issue 讨论的真实用户声音：

- **“完全不可用” (Totally unusable)**：Issue [#4867](https://github.com/HKUDS/nanobot/pull/4867) 中，用户对Ollama的性能表达了强烈的负面情绪，指出每轮额外60秒的延迟使本地模型“完全不可用”。这表明在Ollama场景下的性能优化是当前最迫切的需求。
- **“无限循环” (Endless loop)**：Issue [#4864](https://github.com/HKUDS/nanobot/pull/4864) 中，用户对 `complete_goal` 功能的无限循环感到沮丧，它“反复报错”，导致对话流程断裂。这揭示了一个由近期更新引入的破坏性回归问题，严重影响了自动化目标完成功能。
- **“安全性担忧”**：Issue [#4803](https://github.com/HKUDS/nanobot/pull/4803) 的作者隐晦地指出了API Key明文存储的风险，这是一个严肃的安全担忧，虽然未直接表达强烈不满，但其重要性不言而喻。
- **“日志洪水” (Excessive logs)**：Issue [#4767](https://github.com/HKUDS/nanobot/pull/4767) 反映了一个“噪音”问题，过多的错误日志淹没了有效信息，影响运维体验。幸运的是，该问题已被修复。

### 8. 待处理积压

以下为长期存在或目前暂未合并的重要PR/Issue，需维护者关注：

1. **长期被忽略的功能请求**：Issue [#1503](https://github.com/HKUDS/nanobot/pull/1503) “Template for Dokploy” 从3月发起，直到近期才有 PR [#5007](https://github.com/HKUDS/nanobot/pull/5007) 响应，期间无人应答长达数月。需要优化对这类需求的管理流程。
2. **待合并的重要安全修复**：PR [#5010](https://github.com/HKUDS/nanobot/pull/5010) “docs(security): recommend env-var references over plaintext API keys” 是对安全危机 [#4803](https://github.com/HKUDS/nanobot/pull/4803) 的直接回应，目前为开启状态。应尽快审查合并，以缓解社区对安全性的担忧。
3. **存在冲突的关键PR**：多个标记为 `conflict` 的PR（如 [#4954](https://github.com/HKUDS/nanobot/pull/4954), [#4928](https://github.com/HKUDS/nanobot/pull/4928), [#4963](https://github.com/HKUDS/nanobot/pull/4963), [#4982](https://github.com/HKUDS/nanobot/pull/4982)）需要解决合并冲突。尤其是 `priority: p1` 的 [PR#4954](https://github.com/HKUDS/nanobot/pull/4954) 和 [PR#4928](https://github.com/HKUDS/nanobot/pull/4928)，它们的停滞可能影响WebUI的稳定性和统一会话功能。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是为您生成的 Hermes Agent 项目动态日报。

---

# Hermes Agent 项目动态日报 (2026-07-21)

## 1. 今日速览

今日项目活跃度极高，24小时内处理了50条Issue和50条PR，并发布了具有里程碑意义的 **v0.19.0 “The Quicksilver Release”**。社区讨论主要围绕会话路由问题、跨平台功能扩展以及最新版本中出现的严重Bug（如杀死用户进程、插件崩溃）。尽管发布新版本带来了新的稳定性挑战，但项目整体在功能迭代和社区贡献上保持了强劲势头。

## 2. 版本发布

### [v2026.7.20] Hermes Agent v0.19.0 “The Quicksilver Release”
- **发布日期**: 2026年7月20日
- **更新内容**: 这是一个大版本发布，自 v0.18.0 以来，有约 **2,245次提交**、**1,065个PR被合并**、**~3,300个Issue被关闭**，并吸引了 **超过450位社区贡献者**。这表明项目经历了长时间的功能积累和问题修复，社区规模显著扩大。
- **破坏性变更与迁移注意**: Release 说明仅称 “Hermes is the mess”，未明确列出破坏性变更。**强烈建议用户仔细查阅** 完整的 Release Notes 或 CHANGELOG (若存在) 以确认是否有配置或API变更。同时，根据以下 Issue 描述，升级后用户应关注：
    1.  **插件兼容性**: 新版本似乎对插件API有调整 (Issue #68318)。
    2.  **桌面端会话问题**: 默认配置文件的会话侧边栏可能变空 (Issue #67600)。
    3.  **包分发问题**: PyPI 分发的 sdist 包中存在危险的测试文件 (Issue #68311)。

## 3. 项目进展

今日没有直接合并或关闭的重要PR，但项目在几个关键问题上取得了进展，多个紧急PR已被创建。

- **修复严重稳定性问题 (P1)**:
    - 针对Issue #68311（发布包中的测试文件会误杀用户进程），PR **#68317** 被快速创建，旨在使该测试用例“失败时更安全”，防止对生产环境造成损害。
    - 针对Issue #68300（推测为Telegram导入问题），PR **#68319** 被创建以修复可选导入未受保护的问题。
- **推进核心功能 (Feature)**:
    - PR **#68315** 为辅助模型调用添加了明确的配额耗尽回退链 (`fallback_on: [quota_exhausted]`)，增强了系统的韧性。
    - PR **#68306** 为TUI界面引入了“Widget App SDK”，允许开发者以更标准的方式创建内嵌应用，并提供了三个参考应用。这是TUI功能的重要扩展。
- **修复关键Bug**:
    - PR **#68320** 修复了Discord中一个可能导致回复消息无法送达的中继问题。
    - PR **#68323** 修复了桌面端会话侧边栏UI的显示瑕疵。
    - PR **#68322** 旨在修复插件平台无法接收目标标识符的问题。

## 4. 社区热点

今日讨论最热烈的话题集中在对默认配置的Bug修复和跨平台功能的新需求上。

- **#67600: [Bug]: Desktop session sidebar is empty for the `default` profile** (9条评论)
    - **链接**: [NousResearch/hermes-agent Issue #67600](https://github.com/NousResearch/hermes-agent/issues/67600)
    - **分析**: 这是一个影响特定用户（使用默认配置）的问题，但讨论度很高，表明桌面端用户基数不小，且该问题具有一定的普遍性和迷惑性（后台有数据，前台不显示），用户对这类“幽灵”Bug非常敏感。

- **#4335: Feature Request: Cross-platform session context sharing** (8条评论, 2👍)
    - **链接**: [NousResearch/hermes-agent Issue #4335](https://github.com/NousResearch/hermes-agent/issues/4335)
    - **分析**: 这是一个存在已近4个月的长期需求，但依然活跃。用户期望在CLI、Telegram等不同平台间共享会话上下文，以获得无缝体验。这反映了高级用户对“多模态统一体验”的渴望，是项目平台化战略的关键诉求。

- **#4256: Support configurable keybindings via config.yaml** (3条评论, 6👍)
    - **链接**: [NousResearch/hermes-agent Issue #4256](https://github.com/NousResearch/hermes-agent/issues/4256)
    - **分析**: 尽管评论数不多，但获得了今天最高的“点赞”数 (6👍)。这强烈表明社区对自定义快捷键的呼声很高，尤其是在终端复用器冲突和使用习惯差异的背景下，这是一个用户普遍关心的可用性痛点。

## 5. Bug 与稳定性

今日报告的Bug中，有几个严重程度较高或值得关注：

- **P0 - 安装与破坏性**:
    - **#67194**: [Windows] 安装程序 `Hermes-Setup.exe` 无法执行。*已关闭 (Duplicate)*
- **P1 - 致命错误**:
    - **#68311**: **发布到PyPI的每个sdist包都包含一个危险的测试文件**，该文件会在运行测试时执行 `os.kill(-1, SIGTERM)`，导致用户整个会话被杀死。**已有PR #68317 修复**，这是高度紧急的安全/质量事故。
    - **#29866**: `brew upgrade` 破坏了 `certifi`，导致所有平台的网关消息发送失败。这是一个持续影响Homebrew用户的问题。
    - **#68244**: 更新时选择不恢复本地更改后，dashboard和整个agent都无法启动。
- **P2 - 功能异常**:
    - **#67600**: 桌面端默认配置文件会话侧边栏为空。
    - **#66868**: Cron任务的主模型调用因401错误失败，怀疑与“provider”回退到“custom”有关。
    - **#68261**: TUI技能凭据提示可能被路由到错误的会话，一个会话状态管理问题。
    - **#57626**: “技能库更新”提示被错误地注入到子代理会话中，造成“技能污染”。
    - **#68318**: **v0.19.0 版本中的插件处理程序崩溃**，原因是 `registry.dispatch` 无意中传递了 `task_id` 参数。*已有PR #68322 修复*

## 6. 功能请求与路线图信号

今日社区提出的新功能请求加上已有的PR，为项目未来的发展提供了几个清晰的方向：

- **会话与上下文增强**:
    - **#4335**: 跨平台会话上下文共享。这是社区长期以来的核心需求。
    - **#67316**: 技能（Skills）应能随时调用，而非仅在对话开始时。这反映了对Agent交互灵活性的更高要求。
    - **#68301**: 桌面端与Telegram之间的原生会话桥接。*已关闭 (Duplicate)*
- **平台与插件生态扩展**:
    - **#64900**: 允许插件扩展 `send_message` 的schema和handler，这是平台插件生态成熟的关键一步。
    - **#68260 (PR)**: 创建了Fluxer平台插件的骨架。这表明项目正在构建新的平台适配器，扩展连接能力。
    - **#68222 (PR)**: 将ACP客户端泛化为通用编程代理接口，可对接Claude Code、Codex等。这是对“Agent调度”概念的深化。
- **管理与工具**:
    - **#690**: 提供“MCP Server管理”的CLI工具，以实现发现、选择和交互式配置，降低配置门槛。
    - **#4256**: 支持可配置的快捷键，提升用户体验。
    - **#41075**: 提供 `hermes sessions archive` 和 `compress` 命令，以解决数据库膨胀和Token成本问题。

## 7. 用户反馈摘要

- **痛点**:
    - **更新与升级问题** (#68244, #29866): 用户对升级过程中的不确定感（“Restore local changes now?”）感到困惑，对Homebrew升级后直接导致服务不可用非常不满。
    - **诊断困难** (#2788): 用户抱怨Cron job失败后“没有有用信息”，日志记录不足，导致运维排查困难。这暗示了系统监控和告警功能的缺失。
    - **稳定性与可预测性** (#67600, #61573): 会话状态相关的Bug（侧边栏为空、消息投递错误）严重破坏了用户对Agent稳定性的信任。
- **使用场景**:
    - **跨平台工作流** (#4335): 用户希望在一个聊天界面（如Telegram）发起任务，能在另一界面（如桌面）无缝继续。
    - **高效编程协作** (#68222 PR, #68314 PR): 社区积极贡献技能和扩展，以实现更复杂的编程任务（如多文件代码生成）。
- **满意方面** (从贡献热度推断):
    - 项目保持着极高的更新频率和社区活力，大量PR和Issue被创建，说明开发者社区非常有参与感和建设热情。

## 8. 待处理积压

以下是一些长期未响应但重要的Issue或PR，可能阻碍社区贡献或解决用户痛点，建议维护者关注：

- **#4335**: 跨平台会话共享。这是长期热门需求，但目前没有对应的PR被合并，可能需要在架构上投入更多讨论。
- **#690**: MCP Server管理CLI。这是一个由创始人提出的功能请求，已有明确的实现思路，但三个月来未被推进。
- **#4256**: 可配置快捷键。获得大量点赞，是提升基础用户体验的关键一步，但从未被纳入开发计划。
- **#2788**: Cron job失败缺乏日志。一个影响日常运维的P2 Bug，近4个月未得到解决。
- **PR #19650**: `fix(honcho): respect writeFrequency in sync_turn`。这是一个两个多月前的PR，解决了Honcho内存后端的一个关键配置项，目前仍处于开放状态，建议尽快审阅合并。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，遵照您的指示。以下是为 PicoClaw 项目生成的 2026-07-21 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026年7月21日

## 1. 今日速览

今日项目活跃度中等偏高，社区围绕**稳定性**、**配置持久化**及**国际化**展开了密集贡献。**Bug 修复**与**新功能开发**并行推进，共处理了 11 条 Issue 和 10 个 PR，其中一半已完成合并/关闭。值得注意的是，**Antigravity 提供商**出现了较为严重的回归问题（INVALID_ARGUMENT）和 **OAuth 政策合规问题**，可能导致部分用户服务中断，社区维护者需优先响应。此外，MCP 工具连接失败导致 Agent 挂死的 Bug 和 Matrix 同步重连逻辑缺失等可靠性问题也值得关注。正面来看，社区提交了完整的**日文本地化 PR**，并对多个主流提供商的模型列表进行了全面更新，展现了项目在功能完善和社区共建上的积极态势。

## 2. 版本发布

- **无新版本发布。**

## 3. 项目进展

今日完成了 5 个 PR 的合并/关闭，主要贡献如下：

- **工具系统稳定性修复 (PR #3277)**: 由 `m4n3z40` 提交并合并。该修复解决了因进程重启或 TTL 过期而导致**延迟工具（Deferred Tool）不可见**的严重问题。通过引入工具可见性（Visibility heal）的持久化逻辑和滑动 TTL 机制，确保 Agent 在会话中能持续、稳定地调用已发现的 MCP 工具。这是对一个已知固有问题的重要改进。
- **基础设施与文档维护**: 合并了两个清理性质的 PR，包括更新 Goreleaser 基础镜像至 Alpine 3.23 (#3192) 以及移除 `.gitignore` 中的重复条目 (#3191)，体现了项目在依赖现代化和代码整洁上的持续维护。同时，两个较早的文档与构建逻辑优化 PR (#276, #277) 也在今日完成关闭。

这些更新表明项目在解决社区反馈的痛点（尤其是MCP工具可靠性）方面迈出了坚实一步，同时持续进行着必要的技术债务清理。

## 4. 社区热点

1.  **[BUG] Antigravity provider 回归与 OAuth 屏蔽 (Issue #3274, #3278)**
    - **链接**: [#3274](https://github.com/sipeed/picoclaw/issues/3274), [#3278](https://github.com/sipeed/picoclaw/issues/3278)
    - **热度**: 这两个由同一位用户 `honbou` 在同一天提交的 Issue 直指 Antigravity 提供商的核心问题。#3274 报告了在 `main` 分支最新代码上使用 Antigravity 提供商时出现 `INVALID_ARGUMENT` 错误，这是一次回归。#3278 则报告了 Google 拒绝了 PicoClaw 的 OAuth 登录请求，理由是“不符合安全政策”。
    - **分析**: 这两个问题叠加，可能导致 Antigravity 提供商用户**完全无法使用服务**。这并非孤立的用户配置问题，而是与上游提供商的 API 变化或项目自身代码的变更直接相关。社区对此关注度高，急需维护者确认是上游变更（如模型命名或API规范调整）还是项目自身的兼容性问题，并给出临时解决方案或修复 PR。

2.  **[PR] 添加日文本地化支持 (PR #3273)**
    - **链接**: [#3273](https://github.com/sipeed/picoclaw/pull/3273)
    - **热度**: 由 `honbou` 提交的 PR，为 PicoClaw WebUI 和 Launcher 完整引入了日文（`ja`）翻译，包含了 968 行翻译文件及相应的 Dayjs 本地化配置。
    - **分析**: 这是社区积极拥抱国际化的强有力信号，尤其是在项目已有部分日文文档的背景下。该 PR 若被合并，将显著降低日本地区用户的使用门槛，有助于拓展项目用户群。维护者应尽快审查并合并该 PR。

3.  **[BUG] MCP 服务器连接失败导致 Agent 挂起 (Issue #3269)**
    - **链接**: [#3269](https://github.com/sipeed/picoclaw/issues/3269)
    - **热度**: 用户 `ruiyigen` 报告了当 MCP 服务器连接失败时，整个 Agent 循环会挂起，导致对话接口无响应。
    - **分析**: 这是一个典型的**用户体验杀手**。与 #3277 修复的“工具消失”不同，这个 Bug 更为致命，因为它会导致整个服务不可用。社区对此类问题的容忍度很低，因为它直接中断了工作流。该 Issue 需要与 PR #3277 的修复逻辑配合考虑，确保连接失败的容错机制得到完善。

## 5. Bug 与稳定性

按严重程度排列如下：

1.  **严重**: **[BUG] Antigravity OAuth 登录被 Google 阻止 (#3278)**
    - **链接**: [#3278](https://github.com/sipeed/picoclaw/issues/3278)
    - **状态**: 新建，待处理
    - **影响**: 无法通过 Google OAuth 登录 Antigravity 提供商，服务完全不可用。
    - **分析**: 可能的原因是 Google 更新了 OAuth 2.0 安全策略，PicoClaw 的客户端配置（如缺少应用审核或使用了敏感的 scope）可能已不满足要求。需要立即审查项目注册的 OAuth 凭据和安全策略。

2.  **严重**: **[BUG] Antigravity provider 回归 (#3274)**
    - **链接**: [#3274](https://github.com/sipeed/picoclaw/issues/3274)
    - **状态**: 新建，待处理
    - **影响**: 使用 Antigravity 提供商进行API调用时返回 `INVALID_ARGUMENT`，功能回归。
    - **分析**: 该问题发生在最新 `main` 分支，指向 `tool_schema_transform "simple"` 模式已经过时。这是一个典型的代码变更导致的回归问题，需要通过检查近期的代码提交来定位。与 #3278 一起，给 Antigravity 提供商用户带来了严重的稳定性风险。

3.  **高**: **[BUG] MCP 服务器连接失败导致 Agent 挂起 (#3269)**
    - **链接**: [#3269](https://github.com/sipeed/picoclaw/issues/3269)
    - **状态**: 新建，待处理
    - **影响**: Agent 在 MCP 连接失败时完全挂起，UI 无响应。
    - **分析**: 核心问题在于 Agent 循环缺乏超时和非阻塞机制。这是一个重要的可靠性缺口，应与 #3277 的修复协同考虑。

4.  **中**: **[BUG] 配置文件重写后丢失字段 (#3275)**
    - **链接**: [#3275](https://github.com/sipeed/picoclaw/issues/3275)
    - **状态**: 已关闭（可能是误操作或重复提交）
    - **影响**: 用户 `honbou` 报告在通过 Launcher WebUI 或 `auth login` 后，`model_list` 配置中的 `api_keys` 等字段丢失。
    - **分析**: 虽然已关闭，但这是一个潜在的配置持久化问题，如果复现将会严重影响用户体验。建议维护者确认其关闭原因，如果是误报则更新说明，如果是发现其他原因则指明。

## 6. 功能请求与路线图信号

- **国际化 (i18n) 已落地**: 社区贡献的**日文本地化 PR (#3273)** 现已提交，这很可能是下一个版本中加入的功能，符合项目拓展国际市场的趋势。
- **网关生命周期管理**: 用户 `honbou` 在 Issue #3276 中提出让 Launcher **支持外部管理的网关**（如通过 systemd）。这反映了用户在**生产环境部署**中对进程管理、高可用性的实际需求，是项目向更成熟服务器端产品演进的重要信号。
- **多模态与平台扩展**: PR #3270 提出了**集成阿里云 DashScope TTS** 和**支持发送微信音频文件**的功能。这显示了社区正在为不同的地域和平台（尤其是中国市场）扩展语音交互和消息渠道能力，是生态扩展的积极信号。
- **模型列表持续更新**: PR #3271 全面更新了 9 个主流提供商的默认模型列表（如 OpenAI 的 `gpt-5.6` 系列），展示了项目紧跟 AI 模型演进步伐，确保开箱即用的兼容性，这应作为常规维护任务纳入路线图。

## 7. 用户反馈摘要

- **痛点与挫败感**:
  - **Android 用户使用门槛高**: 用户 `Monessem` 在 Issue #3182 中反馈无法在 Android 上启动服务，即使已授予全部权限，且无法通过设置修改路径。这表明 PicoClaw 在移动端的使用体验离“开箱即用”还有差距。
  - **配置行为不可控**: 用户 `honbou` 对 Launcher 重写配置导致 `api_keys` 丢失的问题感到困扰 (#3275)，并指出 Antigravity OAuth 被拒是“令人沮丧的” (#3278)。配置的持久性和稳定性是用户信任的基础。
  - **Agent 可靠性不足**: 用户 `ruiyigen` 和 `weissfl` 分别报告了 Agent 因 MCP 连接失败 (#3269) 和 Matrix 同步中断 (#3203) 而挂死的 Bug。这表明 Agent 的健壮性、尤其是处理外部服务故障的能力，是社区普遍关注的“软肋”。
- **积极的社区参与**:
  - 用户 `honbou` 在同一天贡献了 3 个 Issue 和 1 个 PR，涉及日语本地化、生产环境部署和 Bug 报告，展现了极高的参与度和贡献意愿。其提出的问题通常具有前瞻性和实际意义。
  - 合并的 PR #3277 来自 `m4n3z40`，解决了MCP工具可见性的固有问题，修复方案得到了社区的认可。

## 8. 待处理积压

- **重要 PR 待合并**:
    - **[PR #3254] 修复模型引用解析逻辑**: 该 PR 于 7 月 13 日提交，旨在修复 `lookupModelConfigByRef` 在模型引用解析时可能因 `provider-alias` 分割导致匹配错误。长时间未合并可能会使依赖该逻辑的功能存在行为不稳定的风险。
    - **[PR #3251] 捕获 Anthropic 缓存 Token 使用量**: 该 PR 于 7 月 12 日提交，为 Anthropic 提供商增加了对 prompt cache token 使用情况的监控。对于依赖 Anthropic 提供高并发、长上下文服务的运营者来说，缺乏这一监控意味着无法准确进行成本分析和性能调优。
- **长期未解决的 Issue**:
    - **[Issue #3203] Matrix 同步循环无重连逻辑**: 该 Issue 自 7 月 2 日提交后已有较长时间的讨论，其描述的“静默死锁”问题对使用 Matrix 频道的用户是长期存在的稳定性隐患。尽管已有 `stale` 标签，但问题本身并未解决。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 NanoClaw 项目数据，我为您生成了 2026-07-21 的项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-07-21

## 1. 今日速览

项目在今日呈现出极高的开发活跃度，共产生 **6 条新 Issues** 和 **20 条 Pull Requests**。核心开发团队与社区贡献者围绕 **安全加固** 和 **渠道扩展** 两大主题密集协作。其中，源自社区成员 `k-fls` 的一系列关于角色权限与审批流程的漏洞报告（#3097-#3100）成为今日焦点，团队反应迅速，已在同日内提交了对应的修复 PR，显示出项目对安全性的高度重视。此外，针对 **LINE 官方账号** 和 **Dial (SMS/语音)** 等新通讯渠道的集成工作也持续推进，项目版图稳步扩张。

**活跃度评估: 高度活跃**

---

## 2. 版本发布

**无。**

---

## 3. 项目进展

今日项目核心进展体现在对 **附件处理**、**容器化** 和 **WhatsApp 集成** 的修复与优化上。

- **附件加载修复 (Merged)**：`cfis` 贡献的 PR #3108 已合并。该修复解决了当 `chat-sdk` 桥接器无法提供 `fetchData` 方法时，入站附件无法被加载的问题，提升了跨渠道的文件传输稳定性。
    - 链接: [PR #3108](https://github.com/nanocoai/nanoclaw/pull/3108)
- **容器镜像增强 (Merged)**：`cfis` 贡献的 PR #3110 已合并。现在基础 Agent 镜像中内置了 `caldav-mcp` 服务器，便于用户集成日历功能。
    - 链接: [PR #3110](https://github.com/nanocoai/nanoclaw/pull/3110)
- **WhatsApp 群组 `@` 提及修复 (Merged)**：`glifocat` 贡献的 PR #3087 已合并，修复了 WhatsApp 群组中通过 `@` 符号提及功能失效的问题。
    - 链接: [PR #3087](https://github.com/nanocoai/nanoclaw/pull/3087)
- **WhatsApp 实例迁移兼容 (Closed)**：`glifocat` 贡献的 PR #3107 已关闭，作为 #3106 的配套文档和模块拷贝，处理了实例重键后的数据行迁移问题，确保升级过程的平滑。
    - 链接: [PR #3107](https://github.com/nanocoai/nanoclaw/pull/3107)

---

## 4. 社区热点

今日社区讨论热度最高的议题围绕 **LINE 官方账号集成** 和 **角色权限安全**。

- **最活跃 Issue**: **[#3096] feat: Add /add-line skill for LINE Official Account channel support**
    - 由 `joshm1230212` 提出。LINE 作为日本、台湾等地区的主流通讯软件，该请求代表了国际化社区对渠道多样性的强烈需求。关联的 #2918 PR 显示了社区贡献者已为此工作数周，讨论内容和诉求非常明确。
    - 链接: [Issue #3096](https://github.com/nanocoai/nanoclaw/issues/3096)
- **最高关注度系列 Issue/PR**: **由 `k-fls` 提出的角色权限安全系列 (#3097-#3100)**
    - 该系列发现了 4 个严重程度不一的安全漏洞，包括“静默授予全局管理员权限”、“审批请求可自批”、“无法阻止撤销最后一位所有者”等。这些问题的披露引发了核心团队的迅速响应，社区在 PR #3101-#3104 下进行了相关技术讨论。这波操作反映出社区中资深用户对项目信任模型的高度关注。
    - 链接:
        - [Issue #3097](https://github.com/nanocoai/nanoclaw/issues/3097)
        - [Issue #3098](https://github.com/nanocoai/nanoclaw/issues/3098)
        - [Issue #3099](https://github.com/nanocoai/nanoclaw/issues/3099)
        - [Issue #3100](https://github.com/nanocoai/nanoclaw/issues/3100)

---

## 5. Bug 与稳定性

今日报告的 Bug 主要集中在 **权限系统** 和 **渠道升级** 方面，严重程度较高，但修复工作已启动。

- **严重 (Critical)**:
    - **无法阻止撤销最后一位管理员** (#3100)：系统无“信任根”保护，可能导致管理员被全部“开除”，权限系统完全失控。该问题在当日即有 **PR #3104** 提出修复。
        - 链接: [Issue #3100](https://github.com/nanocoai/nanoclaw/issues/3100) | [PR #3104](https://github.com/nanocoai/nanoclaw/pull/3104)
    - **角色变更审批流程可被绕过** (#3099)：权限变更的审批请求可能发送给被变更对象自己（自审批），或由低权限审批高权限操作。
        - 链接: [Issue #3099](https://github.com/nanocoai/nanoclaw/issues/3099) | [PR #3103](https://github.com/nanocoai/nanoclaw/pull/3103)
    - **角色授予时静默赋予全局权限** (#3097)：用户可能无意中授予了超出预期的全局管理员权限。
        - 链接: [Issue #3097](https://github.com/nanocoai/nanoclaw/issues/3097) | [PR #3101](https://github.com/nanocoai/nanoclaw/pull/3101)

- **中等等 (Moderate)**:
    - **WhatsApp Cloud 升级导致数据遗留** (#3105)：旧实例升级后，`messaging_groups` 表中的相关数据行被遗留，可能导致服务静默失效。已有 **PR #3106** 尝试修复。
        - 链接: [Issue #3105](https://github.com/nanocoai/nanoclaw/issues/3105) | [PR #3106](https://github.com/nanocoai/nanoclaw/pull/3106)

- **低 (Low)**:
    - **审批卡片可读性差** (#3098)：管理员收到的审批卡片仅显示原始命令，而非操作效果描述，不便于决策。已有 **PR #3102** 提出优化。
        - 链接: [Issue #3098](https://github.com/nanocoai/nanoclaw/issues/3098) | [PR #3102](https://github.com/nanocoai/nanoclaw/pull/3102)

---

## 6. 功能请求与路线图信号

今日最重要的功能请求信号是 **LINE 渠道** 和 **Dial 渠道** 的集成。

- **LINE 官方账号支持**: `joshm1230212` 提出的 Issue #3096 和已提交数周的 PR #2918 表明，这是一个社区呼声很高且已有成熟方案的功能。考虑到用户基础和贡献者投入，该功能大概率会被纳入下一正式版本。
    - 链接: [Issue #3096](https://github.com/nanocoai/nanoclaw/issues/3096) | [PR #2918](https://github.com/nanocoai/nanoclaw/pull/2918)
- **Dial 渠道 (SMS / AI 语音)**: 来自 `OmriBenShoham` 的两个 PR（#3041, #3050）为项目引入了 SMS 和 AI 语音通话渠道。这是一个非常有特色的新渠道，拓宽了 Agent 的能力边界，如果代码质量稳定，有望成为下一个亮点功能。
    - 链接: [PR #3041](https://github.com/nanocoai/nanoclaw/pull/3041) | [PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050)
- **本地语音转写**: 来自 `mtichikawa` 的 PR #2459 旨在为所有 Chat SDK 桥接的渠道增加基于本地 `whisper.cpp` 的语音转文字功能。虽然技术实现复杂（需要本地推理），但“隐私优先”、“无云依赖”的特点十分符合当前趋势。此PR已存在一段时间，可能路线图设计的重点。
    - 链接: [PR #2459](https://github.com/nanocoai/nanoclaw/pull/2459)

---

## 7. 用户反馈摘要

从今日的 Issues 评论和提交中，可以提炼出以下用户核心诉求：

- **安全管理诉求强烈**：用户 `k-fls` 的行为清晰地表明，他在实际部署和使用中遭遇了权限系统的模糊地带。其反馈的 `ncl roles grant` 命令缺乏 `--group` 说明 (`#3097`) 以及审批卡信息不足 (`#3098`)，都指向了一个核心诉求：**让权限操作更清晰、更可预期**。
- **国际化与渠道多样性**：用户 `joshm1230212` 持续为 LINE 渠道和繁体中文文档做贡献，反映了非英语/西方市场用户的真实需求。整合 LINE 这样本地化即时通讯工具，是 NanoClaw 作为通用 AI agent 平台的重要一步。
- **升级与维护平滑性**：用户 `glifocat` 在 Issue #3105 中报告的 WhatsApp 实例升级问题，体现了生产环境用户对“无感升级”的刚需。任何可能导致数据残留或服务静默失败的问题，都是运维痛点。

---

## 8. 待处理积压

- **重要特性 PR**: **PR #2459 (语音转写)** 和 **PR #2918 (LINE 渠道)** 均已存在一段时间，且更新日期较新（7月20日有活动），表明贡献者在持续维护。建议项目维护者加快 Code Review 进度，避免社区贡献长期搁置。这有助于保持社区贡献的热情。
    - 链接: [PR #2459](https://github.com/nanocoai/nanoclaw/pull/2459) | [PR #2918](https://github.com/nanocoai/nanoclaw/pull/2918)
- **长期测试修复 PR**: **PR #1110 (容器测试)** 是一个创建于3月份的测试修复 PR，今日被关闭。虽然它今日不再被视为“待处理”，但这类跨度很长的 PR 值得注意。
    - 链接: [PR #1110](https://github.com/nanocoai/nanoclaw/pull/1110)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，遵照您的指示，以下是根据 NullClaw 项目2026年7月21日的数据生成的日报。

---

# NullClaw 项目动态日报 — 2026-07-21

## 1. 今日速览

过去24小时内，NullClaw项目未产生新的Issue讨论或Bug报告，也无新版本发布。唯一的PR活动是Dependabot发起的一项自动化依赖更新。整体来看，项目维护活动处于极低水平，没有来自核心维护者的人工代码合并或问题响应。项目当前状态可描述为“维护休眠期”，社区交互几乎为零，需关注其长期健康度。

## 2. 项目进展

- **依赖项自动化升级**
  - **PR #956** (Open) 由 Dependabot 发起，旨在将Docker镜像基础版本从Alpine 3.23升级至3.24。该PR目前仍处于开放状态，未获得人工审核或合并。这属于常规的自动化依赖维护，未涉及任何核心功能的新增或修复。
  - 链接: [PR #956](https://github.com/nullclaw/nullclaw/pull/956)

**小结**：本次24小时内无任何实质性的功能推进或Bug修复被合并。项目进展停滞。

## 3. 社区热点

- 过去24小时内无任何活跃的讨论、评论或高反应的议题。当前Open的Issue和PR均无社区互动。项目社区活跃度趋近于零，缺乏外部沟通信号。

## 4. Bug 与稳定性

- 过去24小时内无新的Bug报告。项目稳定性数据在统计周期内无变化。

## 5. 功能请求与路线图信号

- 无新的功能请求提交。鉴于项目当前的低活动状态，无法判断下一版本的规划方向。

## 6. 用户反馈摘要

- 由于无新的Issue评论，无法提供真实用户反馈的提炼。结合长期无响应的状态，可能存在用户流失或缺乏使用反馈渠道的风险。

## 7. 待处理积压

- **PR #956**：自动化版本升级PR（Alpine 3.23 → 3.24）已开放超过一个月（自6月15日），虽不涉及功能变更，但长期积压的依赖升级PR可能在未来导致CI/CD流程兼容性问题或安全补丁滞后。建议维护者定期合并此类自动化PR。
  - 链接: [PR #956](https://github.com/nullclaw/nullclaw/pull/956)

**维护者提醒**：目前仓库中可能存在大量已沉寂的旧Issue和PR。建议维护者在有精力时对积压工作进行一次集中清理与回复，以改善项目健康度。

---
**报告周期**：2026-07-20 00:00 UTC 至 2026-07-21 00:00 UTC  
**分析依据**：GitHub 公开数据

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，以下是基于您提供的GitHub数据生成的IronClaw项目动态日报。

---

### IronClaw 项目动态日报 | 2026-07-21

---

#### 1. 今日速览

项目今日保持高活跃度，核心开发者正全力推进从v1遗留版本（`src/`）到全新“Reborn”架构的迁移工作。重要的里程碑是，删除v1老旧代码并完成生产环境部署切换的巨型PR（#6375）已成功合并，标志着项目架构演进进入新阶段。与此同时，大量修复Streaming、UI及扩展授权等问题的`bug_bash_P2`级别Issues被提交，显示出项目在稳定性和用户体验方面正进行密集打磨。依赖更新（Dependabot）和自动化流水线修复活动也十分频繁，整体上处于“高活跃、高风险、高回报”的架构重构与质量攻坚期。

#### 2. 版本发布

无新版本发布。

#### 3. 项目进展

今日项目取得了极其关键的进展，主要围绕“Reborn”架构转型的最后冲刺：

- **里程碑：删除v1遗留代码并切换部署**：被标记为`[size: XL, risk: high]`的PR [#6375](https://github.com/nearai/ironclaw/pull/6375)（`refactor(tier-b): delete v1 legacy monolith (src/) and cut deploy over to Reborn`）已成功合并。该PR删除了庞大的遗留单体应用，并将生产部署配置（Railway、GCP等）全部指向Reborn栈。这标志着IronClaw正式完成了向全新架构的跨越，是项目历史上的一个重要节点，但后续随之而来的兼容性问题（如#6379）也需快速响应。

- **架构简化（§4.4）**：
    - PR [#6374](https://github.com/nearai/ironclaw/pull/6374)（`refactor(composition): eliminate local_trigger_access...`）已合并。该PR移除了最后一个`Local*`部署类型代码泄露，将触发器访问权限整合到配置与身份体系，进一步实现了架构简化文档中的设计目标。
    - PR [#6387](https://github.com/nearai/ironclaw/pull/6387)（`refactor(composition): shrink deployment-mode branching ratchet 5->3`）开启，旨在缩减部署模式的分支，以完成`DeploymentConfig`的全面使用。

- **依赖与流水线维护**：多个Dependabot PR（如#6288, #6186）合并，更新了`tokio`、`serde`、`agent-client-protocol`等数十个核心依赖，保持了项目的健壮性。同时，PR [#6379](https://github.com/nearai/ironclaw/pull/6379)快速修复了因删除v1遗留代码而导致的主分支CI变红问题，确保了开发流程的稳定。

#### 4. 社区热点

今日最受关注的议题并非社区广泛讨论，而是核心团队内部的关键技术讨论和测试活动：

- **#6263 [OPEN] [refactoring, reborn] §4.3 final store consolidation**：此Issue以 **9条评论** 成为最活跃议题。核心开发者围绕退役`InMemoryTurnStateStore`进行了深入探讨，涉及数据持久化（Slice 0 oracle）和死锁避免（no-livelock evidence）等复杂的技术问题。这表明项目的核心存储层正在经历针对Reborn架构的最后优化。
    - 链接：[Issue #6263](https://github.com/nearai/ironclaw/issues/6263)

- **#6190 / #6189 / #6350 / #6351 等 bug_bash_P2 Issues**：由 @joe-rlo 提交的一系列P2级别的Bug报告（如多错误提示、语言切换、检查点不可用等）获得了 **4条** 评论。这并非普通社区反馈，而是项目内部的Bug Bash活动，旨在集中力量打磨产品质量，找出UI/UX和稳定性上的短板。其背后诉求是确保Reborn重构后的产品质量，为正式发布做好准备。
    - 链接：[#6190](https://github.com/nearai/ironclaw/issues/6190) | [#6189](https://github.com/nearai/ironclaw/issues/6189) | [#6350](https://github.com/nearai/ironclaw/issues/6350) | [#6351](https://github.com/nearai/ironclaw/issues/6351)

#### 5. Bug 与稳定性

今日报告了大量Bug，主要集中在通过Bug Bash活动发现的用户体验和系统稳定性问题上。按严重程度排列如下：

- **P1 级别**：
    - **在线体验核心链路易用性**：
        - **产品提供商注册后无法返回**（[#6360](https://github.com/nearai/ironclaw/issues/6360)）：界面流程设计缺陷。
        - **Gmail扩展重装后自动授权**（[#6348](https://github.com/nearai/ironclaw/issues/6348)）：严重的安全漏洞，可能导致用户隐私数据在未授权情况下被访问。

- **P2 级别**：
    - **用户感知 / 状态不一致**：
        - **语言自动切换**（[#6350](https://github.com/nearai/ironclaw/issues/6350)）：模型无故使用其他语言回答。
        - **响应被截断**（[#6353](https://github.com/nearai/ironclaw/issues/6353)）：长消息丢失，无展开选项。
        - **流式响应错误状态**（[#6189](https://github.com/nearai/ironclaw/issues/6189)）：已完成响应显示“错误”状态。
        - **流式响应循环重播**（[#6352](https://github.com/nearai/ironclaw/issues/6352)）：返回聊天页面时内容反复刷屏。
    - **功能可靠性**：
        - **检查点不可用**（[#6351](https://github.com/nearai/ironclaw/issues/6351)）：多工具请求因依赖的系统检查点不可达而失败。
        - **Telegram消息渲染异常**（[#6349](https://github.com/nearai/ironclaw/issues/6349)）：跨平台聊天记录错乱。
    - **界面交互**：
        - **多错误提示叠加**（[#6190](https://github.com/nearai/ironclaw/issues/6190)）：请求失败时显示多个矛盾的错误信息。
        - **“测试连接”与“获取模型”功能重复**（[#6362](https://github.com/nearai/ironclaw/issues/6362)）：按钮功能混淆。
        - **工具权限选择器闪烁**（[#6331](https://github.com/nearai/ironclaw/issues/6331)）：保存时下拉框值暂时回滚。
    - **Workspace / Admin**：
        - **目录树导航与辅助功能缺失**（[#6334](https://github.com/nearai/ironclaw/issues/6334)）。
        - **加载历史信息时视口跳跃**（[#6333](https://github.com/nearai/ironclaw/issues/6333)）。
        - **深层链接时内容不展开**（[#6332](https://github.com/nearai/ironclaw/issues/6332)）。
        - **用户详情页信息显示陈旧**（[#6330](https://github.com/nearai/ironclaw/issues/6330)）。

    **已有修复/处理中：**
    - **Streaming问题**：PR [#6337](https://github.com/nearai/ironclaw/pull/6337)（`fix: keep chat streams active and resume without replay`）已合并，旨在解决流式会话的活跃保持和重播问题，与之相关的多个Bug可能得到缓解。
    - **自动化错误提示**：Issue [#6178](https://github.com/nearai/ironclaw/issues/6178) 和 [#6179](https://github.com/nearai/ironclaw/issues/6179) 今日已关闭，表明相关修复已完成。

#### 6. 功能请求与路线图信号

今日主要的功能信号来自核心团队的线路图推进：

- **核心功能补全**：
    - **深度扩展集成**：[#6320](https://github.com/nearai/ironclaw/issues/6320) 目标是在Reborn中实现原生的IronHub扩展安装流程，表明下一个版本将重点加强扩展生态。
    - **线程作用域的MCP会话**：[#6325](https://github.com/nearai/ironclaw/issues/6325) 计划将MCP配置和会话绑定到正确的线程/运行上下文中，这是提升Agent安全与隔离性的关键特性。

- **用户界面重塑**：
    - **WebUI工作区重新设计**：[#6324](https://github.com/nearai/ironclaw/issues/6324) 计划为Reborn打造全新的、以聊天为先的界面和引导体验，这直接回应了之前用户对复杂界面的反馈。

- **社区驱动的功能信号**：较早的Issue [#2277](https://github.com/nearai/ironclaw/issues/2277)（关于外部代理的ACP后端）今日获得更新，表明开发团队仍在关注并可能将其纳入长远规划，尽管它并非当前版本的焦点。

#### 7. 用户反馈摘要

从今日报告的Issues中，可以提炼出以下用户痛点（主要来自内部Bug Bash）：
- **困惑与不信任**：用户对系统的状态感到困惑，例如“响应成功了却显示错误”（[#6189](https://github.com/nearai/ironclaw/issues/6189)）、“请求失败原因不明”（[#6190](https://github.com/nearai/ironclaw/issues/6190)），这破坏了用户对系统的信任。
- **可用性受阻**：基本操作受限，如“无法在引导流程中后退”（[#6360](https://github.com/nearai/ironclaw/issues/6360)）、“长消息被截断”（[#6353](https://github.com/nearai/ironclaw/issues/6353)），严重影响了核心使用场景。
- **安全忧虑**：扩展在重装后自动授权（[#6348](https://github.com/nearai/ironclaw/issues/6348)）是极其严重的隐私安全问题，会让用户对自己的数据安全感到不安。
- **前后端不一致**：Telegram与WebUI间消息渲染不一致（[#6349](https://github.com/nearai/ironclaw/issues/6349)），说明不同渠道间的状态同步存在问题，影响跨设备体验。

#### 8. 待处理积压

- **关键遗留功能的现代化**：
    - **Issue [#2277](https://github.com/nearai/ironclaw/issues/2277) [scope: agent]**: 关于支持外部ACP编程代理（如Codex, Droid）以进行任务委托。此问题自4月提出，对构建开放的Agent生态至关重要，需尽快明确其在Reborn最终路线图中的位置。
    - **Issue [#6263](https://github.com/nearai/ironclaw/issues/6263) [refactoring, reborn]**: 退役核心存储组件的TODO。因其技术复杂性（涉及数据持久化和死锁避免），需要高度关注其进展，避免成为架构转型的最后一公里瓶颈。

- **长期未合并的PR**：
    - **PR [#5598](https://github.com/nearai/ironclaw/pull/5598) [size: M]**: 这是一个由机器人发起的“发布”PR，将更新`ironclaw_common`与`ironclaw_skills`两个核心库。它自7月初已经开放超过2周，且包含破坏性API变更。为了将核心团队的代码改进交付给社区，并避免后续更多PR与其产生冲突，建议维护者优先处理此PR的合并或关闭。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-07-21

## 今日速览
过去 24 小时（2026-07-20）项目活跃度较高：共提交 15 个 Pull Request，其中 **10 个已合并/关闭**，5 个待合并；无新版本发布，无新 Issue 提交。主要进展集中在 **Cowork 协作功能**（浏览器多注释附件、滚动跳转修复、IM 消息闪烁修复）、**AI 皮肤创建流程优化**以及 **Windows 构建与环境管理**（静默安装、构建通道隔离）。多个稳定性修复同时落地，项目健康度良好。

---

## 版本发布
无新版本发布。

---

## 项目进展
本日合并/关闭的重要 PR 覆盖了功能增强、稳定性修复和构建改进，项目在协作、个性化、部署友好性上均有实质推进。

### 功能增强
- **#2366** [CLOSED] **支持浏览器多注释附件**  
  作者：liugang519  
  在内置浏览器中批量创建注释并保存裁剪截图，在 Cowork 消息中传递结构化注释上下文，隐藏裁剪截图对应的普通图片附件，改为注释数量徽标。同时补充了多注释设计文档、资产存储、Redux 和运行时适配测试。  
  → 核心协作能力大幅增强，为浏览器内多素材引用奠定基础。  
  [链接](https://github.com/netease-youdao/LobsterAI/pull/2366)

- **#2361** [CLOSED] **改进 AI 皮肤创建流程**  
  作者：btc69m979y-dotcom  
  在 Appearance 设置中增加了持久的 AI 皮肤创建入口，含首次使用引导；打开 AI Skin Designer 时提供精炼的框架提示，并保持皮肤工作流在多次对话中持续可用。  
  → 降低个性化皮肤创建门槛，提升用户探索意愿。  
  [链接](https://github.com/netease-youdao/LobsterAI/pull/2361)

### 构建与部署优化
- **#2367** [CLOSED] **为 Windows 分发构建添加显式通道入口**  
  作者：fisherdaddy  
  新增 `scripts/dist-win-channel.cjs` 和 `scripts/dist-win-web.cjs`，显式传递 keyfrom 和 web-installer 环境变量，并清除继承的 shell 环境中的泄漏变量，避免构建间参数污染。  
  → 提升 Windows 构建的可重复性和安全性。  
  [链接](https://github.com/netease-youdao/LobsterAI/pull/2367)

- **#2365** [CLOSED] **通过 RPC ack 实现 OpenClaw 配置热重载**  
  作者：fisherdaddy  
  将配置热重载的触发方式从文件监听改为 RPC ack，消除文件系统延迟和竞争风险。  
  [链接](https://github.com/netease-youdao/LobsterAI/pull/2365)

### 稳定性修复
- **#2364** [CLOSED] **修复 Cowork 会话刷新时滚动跳转**  
  作者：liuzhq1986  
  通过会话 ID 限定刷新事件范围，并保留已加载的消息历史。  
  [链接](https://github.com/netease-youdao/LobsterAI/pull/2364)

- **#2363** [CLOSED] **修复 Cowork IM 消息周期性闪烁**  
  作者：liuzhq1986  
  在 reconcil 阶段比较匹配的历史窗口，修复 gateway tail 不匹配时保持旧消息。  
  [链接](https://github.com/netease-youdao/LobsterAI/pull/2363)

- **#2360** [CLOSED] **修复认证流程中本地回调无法保留的问题**  
  作者：liuzhq1986  
  在多次、并发的登录尝试中复用有效回调服务器，添加了安全生命周期诊断和回归测试。  
  [链接](https://github.com/netease-youdao/LobsterAI/pull/2360)

- **#2359** [CLOSED] **保持 Artifact 预览面板与输入区布局稳定**  
  作者：liugang519  
  为拖拽柄和内容区设置稳定 key，避免展开切换时子树重建；同步更新输入区高度，减少闪动。  
  [链接](https://github.com/netease-youdao/LobsterAI/pull/2359)

- **#2362** [CLOSED] **修复 Cron UI bug**  
  作者：fisherdaddy  
  （具体修复内容未详述，但已合并。）  
  [链接](https://github.com/netease-youdao/LobsterAI/pull/2362)

- **#1349** [CLOSED] **为 POPO 连接测试添加真实 API 验证**  
  作者：gongzhi-netease  
  修复原空值校验导致任意凭据都显示“通过”的严重问题，改为调用 POPO API 验证 appKey 和 appSecret 有效性。  
  [链接](https://github.com/netease-youdao/LobsterAI/pull/1349)

---

## 社区热点
今日无明显热点讨论（所有 PR 评论数为 undefined，👍 数均为 0）。值得关注的是 **#2368**（Windows 静默安装）仍处待合并状态，该功能可大幅改善企业批量部署体验，预计后续会吸引更多反馈。  
[链接](https://github.com/netease-youdao/LobsterAI/pull/2368)

---

## Bug 与稳定性
本日共修复 **6 个稳定性缺陷**，所有修复均已合并：

| 严重程度 | Bug 描述 | 修复 PR |
|---------|---------|--------|
| 高 | POPO 连接测试所有凭据均显示“通过”（严重安全/体验问题） | #1349 ✅ |
| 中 | Cowork 会话刷新时滚动跳转 | #2364 ✅ |
| 中 | Cowork IM 消息周期性闪烁 | #2363 ✅ |
| 中 | 认证本地回调在多次登录中丢失 | #2360 ✅ |
| 低 | Artifact 预览面板展开/切换时闪烁 | #2359 ✅ |
| 低 | Cron UI 显示错误 | #2362 ✅ |

无新增未修复的高危 Bug。

---

## 功能请求与路线图信号
- **Windows 静默安装**（#2368，待合并）—— 启动 NSIS 安装器并通过 Start-Process 静默执行，失败时返回本地化错误，完成后自动重启应用。适合企业 IT 批量分发场景，有较高实用价值。
- **浏览器多注释附件**（#2366，已合入）—— 持续丰富 Cowork 多模态交互能力，未来可能扩展至更多引用类型（如视频帧、PDF 区域）。
- **AI 皮肤创建流程**（#2361，已合入）—— 将皮肤创建入口持久化并增加引导，表明项目在个性化 UI 方向持续投入。
- 依赖升级 PR（#1277 更新 Electron 至 43.1.1，#1282 更新 @headlessui/react 至 2.2.9，#1283 更新 React 至 19.2.4，#1284 更新 react-syntax-highlighter 至 16.1.1）虽长期未合，但反映了项目期望追赶前端技术栈的趋势。

---

## 用户反馈摘要
本日无 Issue 评论，无法提取具体用户反馈。上述修复多来自内部团队发现，暂未观测到社区直接报告的问题。

---

## 待处理积压
以下 **长期未关闭** 的依赖升级 PR 已存在超过 **3 个月**（自 2026-04-02 创建），可能因兼容性测试或 API 变更延迟合并，建议维护者评估风险后决定是否处理：

| PR | 依赖 | 目标版本 | 当前状态 |
|----|------|---------|--------|
| [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) | electron + electron-builder | 40.2.1 → 43.1.1 | OPEN |
| [#1282](https://github.com/netease-youdao/LobsterAI/pull/1282) | @headlessui/react | 1.7.19 → 2.2.9 | OPEN |
| [#1283](https://github.com/netease-youdao/LobsterAI/pull/1283) | react | 18.3.1 → 19.2.4 | OPEN |
| [#1284](https://github.com/netease-youdao/LobsterAI/pull/1284) | react-syntax-highlighter | 15.6.6 → 16.1.1 | OPEN |

此外，新提交的 **#2368**（Windows 静默安装）已近 24 小时未合入，若需较快上线可优先审批。

---

**总结**：项目昨日保持了高频率的合并节奏，在 Cowork 协作、AI 个性化、构建可靠性及多个稳定性问题上均有明显改善。无新版本发布但功能积累扎实。长期依赖升级积压是唯一需要关注的潜在风险。

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

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我已根据您提供的 CoPaw 项目 GitHub 数据，为您生成了 2026年7月21日的项目动态日报。

---

### CoPaw 项目动态日报 | 2026年7月21日

#### 1. 今日速览

CoPaw 项目今日保持**高度活跃**状态。过去24小时内，共处理了30条 Issue 和42条 PR，社区参与度旺盛。值得关注的是，近期版本的稳定性和**多工具调用推理一致性问题**成为社区讨论的焦点，同时，新功能的 PR 提交数量也显著增加，显示出社区贡献者的积极参与。项目在修复多个关键 Bug 的同时，正积极吸纳社区提出的功能增强建议，整体健康度良好。

#### 2. 版本发布

*无*

#### 3. 项目进展

今日有多个重要 PR 被合并，推动了项目在功能扩展和稳定性方面的进展：

- **PawApp 与 Kanban 应用合并** ([PR #6150](https://github.com/agentscope-ai/qwenpaw/pull/6150))：由 `zhijianma` 提交的 feat(pawapp) 分支被合并，正式引入了 PawApp SDK 和 Kanban 应用，标志着项目生态系统的扩展。
- **ReMe Light 记忆索引维护增强** ([PR #6235](https://github.com/agentscope-ai/qwenpaw/pull/6235))：`jinliyl` 的 PR 已合并，将高开销的索引重建从 Agent 自动启动流程中剥离，改为显式维护操作，并升级了底层 `reme-ai` 库，增强了长期记忆系统的稳定性。
- **Langfuse 可观测性优化** ([PR #5922](https://github.com/agentscope-ai/qwenpaw/pull/5922))：`alvinlee518` 提交的 PR 被合并，改进了 Langfuse 追踪效果，使其能正确传播用户、会话和版本信息。
- **默认循环模式重构** ([PR #6210](https://github.com/agentscope-ai/qwenpaw/pull/6210))：由 `rayrayraykk` 提交的 PR 已合并，将标准的 ReAct 循环重构为首要的 `DefaultMode`，并优化了生命周期管理，为后续模式切换功能奠定基础。

**结论**：项目通过合并 PR，在**插件生态、记忆稳定性、可观测性和架构清晰度**四个方向上均有显著推进。

#### 4. 社区热点

本周最受关注的 Issue 是 **#6257**：*[Bug]: Multiple tool calls produce identical thinking output*。该 Issue 报告了当 Agent 在单次交互中调用多个工具时，每个调用块的思考过程（thinking block）内容完全相同，而不是进行独立的推理。该问题引发了 **13 条评论**，是当前讨论最热烈的议题。社区和开发者正在此 Issue 下详细讨论定位和修复方案。同时，PR [#6280](https://github.com/agentscope-ai/qwenpaw/pull/6280) 和 [#6257](https://github.com/agentscope-ai/qwenpaw/issues/6257) 都直接与此 Bug 相关，显示出项目对此问题的高度重视。

**诉求分析**：用户强烈需求 Agent 在复杂任务中能够进行**清晰、独立、有序的推理**，而非简单的重复。这一 Bug 直接影响了 Agent 输出的可解释性和用户信任感，是当前社区核心痛点之一。

#### 5. Bug 与稳定性

今日报告的 Bug 主要集中在以下几个方面，按严重性排列：

- **严重 (Critical)**
    - **多重工具调用推理输出重复** ([Issue #6257](https://github.com/agentscope-ai/qwenpaw/issues/6257))：核心功能 Bug，影响 Agent 响应质量。已有相关修复 PR [#6280](https://github.com/agentscope-ai/qwenpaw/pull/6280) 在审。
    - **Agent 连续轮次重复与 memory_search 死循环** ([Issue #6241](https://github.com/agentscope-ai/qwenpaw/issues/6241))：框架层缺乏有效的重复检测和终止机制，导致 Agent 进入死循环。严重消耗 Token 和运行时间。
    - **桌面版Linux下缩放快捷键失效** ([Issue #6252](https://github.com/agentscope-ai/qwenpaw/issues/6252))：桌面版在 Linux 平台的可用性问题。
    - **多 Subagent 导致主Agent快速轮询** ([Issue #4873](https://github.com/agentscope-ai/qwenpaw/issues/4873))：并发任务场景下的严重性能问题，且无法从飞书端打断。

- **中等 (Medium)**
    - **`_saved_tool_refs` 导致文件名字过长崩溃** ([Issue #6246](https://github.com/agentscope-ai/qwenpaw/issues/6246))：已被标记为已关闭，但根因涉及对长工具结果的处理，需关注后续。
    - **Windows PATH拼接异常** ([Issue #6239](https://github.com/agentscope-ai/qwenpaw/issues/6239))：导致子进程丢失系统全局变量，影响环境一致性。
    - **离线环境 Code 模式无法预览文件** ([Issue #6261](https://github.com/agentscope-ai/qwenpaw/issues/6261))：在线预览依赖问题，影响离线用户的完整体验。

- **低 (Low)**
    - **v2.0.0 循环执行问题** ([Issue #5961](https://github.com/agentscope-ai/qwenpaw/issues/5961))：已关闭，怀疑与特定模型有关。
    - **沙箱不可用时审批硬编码** ([Issue #6250](https://github.com/agentscope-ai/qwenpaw/issues/6250))：已关闭，但社区认为提供的解决方案过于粗放。
    - **聊天报错** ([Issue #6255](https://github.com/agentscope-ai/qwenpaw/issues/6255))：偶发性的 OpenAI API 参数错误。

#### 6. 功能请求与路线图信号

用户今日提出了多个具有建设性的功能请求，部分已有对应 PR 或开发中，显示出社区的强大贡献力和项目的未来演进方向：

- **内置“询问用户”工具，支持 Human-in-the-Loop** ([Issue #6274](https://github.com/agentscope-ai/qwenpaw/issues/6274))：呼声很高，旨在让 Agent 处理不明确或高风险请求时暂停并向用户提问。是提升 Agent 安全性与可控性的重要功能。
- **用户可自定义 Agent 模式** ([PR #6270](https://github.com/agentscope-ai/qwenpaw/pull/6270))：`rayrayraykk` 已提交 PR，允许用户编辑和切换 Agent 的行为模式。
- **支持禁用或自定义内置工具描述** ([Issue #6286](https://github.com/agentscope-ai/qwenpaw/issues/6286))：用户反馈22个内置工具约占用每轮请求8k-10k tokens，希望减少不必要的 Token 消耗。
- **支持最小化到系统托盘** ([Issue #6264](https://github.com/agentscope-ai/qwenpaw/issues/6264))：桌面端用户期望的常见功能。
- **新增 AIOnly 模型提供商** ([Issue #6268](https://github.com/agentscope-ai/qwenpaw/pull/6271))：已有对应 PR，将支持聚合190+模型的平台，扩展模型选择范围。
- **新增会话分组/文件夹功能** ([Issue #6287](https://github.com/agentscope-ai/qwenpaw/issues/6287))：提升桌面版用户体验的功能请求。
- **Web 控制台适配移动端** ([Issue #6281](https://github.com/agentscope-ai/qwenpaw/issues/6281))：移动端远程管理的呼声。

此外，**#6283**（自动附加当前时间信息）、**#6260**（优化结果呈现）、**#6285**（支持新模型）等功能请求也反映了用户对提升产品体验的迫切期望。

**路线图信号**：项目正在积极向**用户可控、可插拔、更智能、更节约**的方向演进，特别是 **Human-in-the-Loop** 和 **用户自定义模式** 极有可能成为下个版本的核心特性。

#### 7. 用户反馈摘要

- **痛点**：
    - **“思考过程占用空间过大”** ([Issue #6260](https://github.com/agentscope-ai/qwenpaw/issues/6260))：用户 `azear` 表达了对 Agent 思考过程折叠的需求，认为“更多的期望 Agent 交付结果”，而非展示冗长的工具调用过程，这影响了用户阅读最终结果的效率。
    - **“Token消耗巨大”** ([Issue #6286](https://github.com/agentscope-ai/qwenpaw/issues/6286))：用户 `feng183043996` 明确指出内置工具的固定描述消耗大量 Token，认为这是一种资源浪费。
    - **“升级路径不明确”** ([Issue #5959](https://github.com/agentscope-ai/qwenpaw/issues/5959))：用户尝试通过脚本升级到 v2.0.0 时遇到了问题，表明版本升级的文档或工具链需要改进。

- **使用场景**：
    - **Human-in-the-Loop 场景** ([Issue #6274](https://github.com/agentscope-ai/qwenpaw/issues/6274))和**桌面 GUI 自动化** ([PR #5187](https://github.com/agentscope-ai/qwenpaw/pull/5187)) 的请求，反映出用户正在将 CoPaw 应用于更复杂的、需要人工监督或与操作系统交互的真实任务中。
    - **记忆体系统疑惑** ([Issue #6222](https://github.com/agentscope-ai/qwenpaw/issues/6222))：用户对 `MEMORY.md` 和 `Dream` digest 两套记忆体系的功能定位感到困惑，说明内部功能模块的文档和设计意图需要更清晰地对外传达。

#### 8. 待处理积压

以下为长期未关闭或缺乏维护者回应的 Issue，建议项目维护者关注：

- **Issue #4873** ([链接](https://github.com/agentscope-ai/qwenpaw/issues/4873))：`[Bug]: 同时开两个subagent会导致主agent无限快速轮询直至任务结束`。状态为 OPEN，发起于 6月1日，至今已超过50天，是较为严重的并发性能问题。由于评论数较少，可能未被充分重视。
- **Issue #5688** ([链接](https://github.com/agentscope-ai/qwenpaw/issues/5688))：`[Question]: CSS Selector Prefix Mismatch: ant- vs qwenpaw-`。状态为 OPEN，发起于 7月1日，讨论了前端 CSS 前缀不一致的问题。这虽然是样式问题，但长期存在可能影响未来前端开发的兼容性。
- **Issue #6222** ([链接](https://github.com/agentscope-ai/qwenpaw/issues/6222))：`[Question]: 请问在qwenpaw中，MEMORY.md 和 Dream产生的digest的定位分别是什么。` 状态为 OPEN，用户对记忆系统设计存在疑问。维护者回应可以澄清设计，并可能补充相关文档。

**建议**：建议项目团队优先处理 **#4873** 这个长期存在的严重 Bug，并对 **#5688** 和 **#6222** 等设计/文档类问题进行响应或关闭。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 | 2026-07-21

---

## 1. 今日速览

过去 24 小时项目活跃度保持高位：共产生 **39 条 Issue 更新**（新开/活跃 30 条，关闭 9 条）和 **50 条 PR 更新**（待合并 38 条，已合并/关闭 12 条）。关键进展集中在 **SOP (标准操作流程) 控制面**、**代理评估框架 `zeroclaw eval`** 以及 **Windows 跨平台兼容性** 的修复与增强。虽无正式版本发布，但多个高风险 Bug 已通过合并 PR 关闭，且一波大规模功能 PR 已进入审核通道。项目健康度良好，社区贡献活跃，但待合并 PR 积压（38/50）需关注。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

过去 24 小时有 **12 个 PR 被合并或关闭**，主要推动以下方面：

### 🔒 关键 Bug 修复
- **修复历史修剪静默丢失上下文**  
  Issue [#8837](#8837)（S2，已关闭）：代理在对话中突然丢失历史上下文，根因为修剪逻辑在禁用修剪时仍错误执行。修复 PR 已合入 `master`。
- **修复串行传输响应 ID 不匹配后不同步**  
  Issue [#9078](#9078)（S2，已关闭）：`SerialPeripheral::send_request` 在收到不匹配的响应 ID 后未清空缓冲区，导致后续数据错位。修复已合入。
- **修复原生工具调用参数未验证导致 Provider 400 错误**  
  Issue [#8675](#8675)（S1，已关闭）：当模型输出非 JSON 的工具调用参数时，OpenRouter/OpenAI 格式 Provider 直接透传，触发 400 并返回空回复。修复已合入。
- **修复 ZeroCode 复制代码块包含 Markdown 围栏**  
  Issue [#8664](#8664)（S2，已关闭）及 [#8644](#8644)（ZeroCode 完成 Code 轮次后无视觉输出）、[#8765](#8765)（界面继承终端背景）、[#8944](#8944)（鼠标复制干扰文本选择）均已完成修复。

### ⚙️ CI/质量改进
- **为固件协议 crate 增加 CI 覆盖**  
  Issue [#9079](#9079)（已关闭）：`firmware/zeroclaw-fw-protocol` 不再逃逸质量门禁，已配置独立 CI 工作流。
- **文档翻译流程可重复性修复**  
  PR [#9055](#9055)（待合并）：标准化 mdBook 输入生成路径，消除构建产物的环境依赖。

### 🧪 评估框架（`zeroclaw eval`）系列 PR
连续提交 6 个关联 PR（#9220~#9224、#9226、#9227、#9228），从可重复运行收据、基线回归门控、LLM-Judge 评分器、JUnit 报告到校准工具和趋势面板，标志着评估框架进入量产冲刺阶段。这些 PR 均处于打开状态，待审核。

---

## 4. 社区热点

| 排名 | Issue/PR | 评论数/👍 | 摘要 |
|------|----------|-----------|------|
| 1 | [#6808 RFC：工作通道、看板自动化与标签清理](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) | 14 评论 | 长达 21 次修订的治理 RFC，讨论如何通过自动化降低维护者人工路由负担。反映了社区对项目协作流程标准化的强烈诉求。 |
| 2 | [#7462 Windows 测试失败 74 项](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | 10 评论 | 核心 CI 仅跑 Linux，导致 Windows 上大量 Unix 命令、路径语义和控制台编码问题未被捕获。用户 NiuBlibing 提供了详细复现步骤，社区呼吁增加跨平台 CI。 |
| 3 | [#3566 A2A 协议支持](https://github.com/zeroclaw-labs/zeroclaw/issues/3566) | 9 评论 / 👍7 | 自三月份提出的 Agent-to-Agent 协议集成，获得 7 个 👍，用户期望 ZeroClaw 能与 NanoClaw、OpenClaw 或其他 A2A 兼容代理互操作。此功能被标记为 `priority:p2, status:accepted`，但尚未有 PR 进展。 |

**分析**：社区最关注的三件事依次是 **(1) 团队内部工作流自动化**（减少手动维护负担）、**(2) 跨平台兼容性**（Windows 是缺失的一环）以及 **(3) 代理互操作性**（A2A 协议）。其中 Windows 兼容性已出现明确的 Bug 报告，治理 RFC 已进入 Rollout 阶段。

---

## 5. Bug 与稳定性

按严重等级（S0 = 数据丢失/安全风险，S1 = 工作流阻塞，S2/S3 = 不同程度降级）排列：

| 严重等级 | Issue | 状态 | 说明 | 是否有 Fix PR |
|---------|-------|------|------|--------------|
| **S0** | [#9206 Cron 任务 workspace_dir 解析为 `/`](https://github.com/zeroclaw-labs/zeroclaw/issues/9206) | OPEN | `job_type="agent"` 的定时任务间歇性将工作目录设为根目录，可能严重干扰文件操作。 | 无 |
| **S1** | [#9204 Landlock 沙箱锁定自身](https://github.com/zeroclaw-labs/zeroclaw/issues/9204) | OPEN | 执行 shell 命令后 Landlock 策略影响 SQLite 内存访问等，导致工作流阻塞。 | 无 |
| **S1** | [#9207 web_fetch 返回压缩乱码](https://github.com/zeroclaw-labs/zeroclaw/issues/9207) | OPEN | `web_fetch` 工具不处理 gzip/brotli 等压缩响应，返回二进制数据。 | 无 |
| **S1** | [#9192 shared_budget TOCTOU 可致 AtomicUsize 回绕](https://github.com/zeroclaw-labs/zeroclaw/issues/9192) | OPEN | 并发父/子代理迭代可能同时通过预算检查，导致 `fetch_sub` 下溢 panic。 | 已有 PR [#9201](https://github.com/zeroclaw-labs/zeroclaw/pull/9201)（修复迭代预算下溢） |
| **S1** | [#9216 注释卫生门禁失败](https://github.com/zeroclaw-labs/zeroclaw/issues/9216) | OPEN | `master` 上 `comment_hygiene_gate.sh` 发现 Issue 引用等痕迹，导致 Lint 流水线阻塞。 | 无 |
| **S1** | [#7462 Windows 测试失败 74 项](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | OPEN | 长期遗留问题，CI 未覆盖 Windows。 | 无 |
| **S1** | [#8675 工具调用参数未验证](https://github.com/zeroclaw-labs/zeroclaw/issues/8675) | CLOSED | 已修复合入。 | 已完成 |
| **S2** | [#8837 历史修剪静默](https://github.com/zeroclaw-labs/zeroclaw/issues/8837) | CLOSED | 已修复。 | 已完成 |
| **S3** | [#9202 desktop 命令无法检测已安装的 AppImage](https://github.com/zeroclaw-labs/zeroclaw/issues/9202) | OPEN | 下载 URL 失效且未识别 Linux 上的已注册 AppImage。 | 无 |

**小结**：目前有 **4 个 S1 阻塞级 Bug** 尚无 PR 修复（#9204、#9207、#9192、#9216），其中 #9192 已有联合修复 PR #9201 在审。S0 的 #9206 风险最高，应优先处理。

---

## 6. 功能请求与路线图信号

### 近期已接受的新增需求
- **[#7065] 代理评估框架（`zeroclaw eval`）**  
  过去 24 小时围绕此功能产生了 **6 个 follow-up Issue**（#9226~#9228）和 **7 个关联 PR**（#9220~#9224 等），覆盖 JUnit 报告、LLM-Judge 校准、记忆播种、趋势面板等。说明该功能即将进入正式版本，很可能成为 **v0.9.0** 的一部分。
- **[#9178] ACP 嵌入式资源 blob + deliver_file**  
  Agent Communication Protocol 的增强，允许代理在工具结果中返回工作区文件作为内嵌资源。目前处于 OPEN，评论数 1，暂无 PR。
- **[#8581] 集中化 SOP 入口适配器**  
  已有对应 PR [#9205](https://github.com/zeroclaw-labs/zeroclaw/pull/9205) 提交，将分散的 fan-in 源统一到 `SopIngress` 适配器。
- **[#6685] SOP HTTP fan-in 未接线**  
  文档已发布但路由未实现，PR [#9203](https://github.com/zeroclaw-labs/zeroclaw/pull/9203) 已提交解决该问题。

### 可能纳入下个里程碑的功能
- **[#7432] v0.9.0 认证、安全、网关与破坏性变更跟踪器**  
  标记了 `priority:p2` 和 `risk:high`，包含 A2A 边界、工具策略等，表明 0.9.0 将是面向企业级安全的重要版本。
- **[#9084] 技能安装安全审查**  
  大型 PR（size:XL），对来自 ClawHub/Git 注册表的第三方技能增加屏幕、收据验证、沙箱门禁，是供应链安全的重要举措。
- **[#8879] Web 界面风险配置统一网格**  
  PR 待审核，将风险配置中的 `allowed_tools` / `excluded_tools` 等四个字段统一为 `ToolPicker`，提升 UX 一致性。

---

## 7. 用户反馈摘要

- **Windows 用户体验痛点**  
  > “`zerocode` doesn't start unless I set `ZEROCLAW_SOCKET` env var” – [#9117](#9117)  
  > “74 test failures on Windows 11 (Simplified Chinese, code page 936)” – [#7462](#7462)  
  > “Installed AppImage not detected, download URL 404” – [#9202](#9202)  
  反映 Windows 上首个启动失败、路径依赖、安装检测等问题，当前缺少 CI 覆盖，用户强烈建议增加 Windows CI 工作流。

- **代理行为不可预期**  
  > “Talking to the agent mid session suddenly loses its context” – [#8837](#8837)（已修复）  
  > “The agent is typing… indicator becomes permanently stuck on Discord” – [#9198](#9198)（S3，OPEN）  
  用户对会话一致性有较高期待，历史修剪和频道状态残留是主要不满点。

- **工具返回不可用数据**  
  > “`web_fetch` returns garbage binary data for compressed responses” – [#9207](#9207)  
  > “`file_download` no SSRF guard on operator‑configured endpoint URL” – [#8713](#8713)（已有 PR）  
  用户期望工具输出能被代理可靠解析，压缩处理和 SSRF 防护是当下主要呼声。

- **评估需求**  
  > “ZeroClaw has no shipped way to evaluate agent behavior at scale” – [#7065](#7065)  
  多位用户（mn13、IftekharUddin）持续推动评估框架，已形成完整的子任务队列，表明社区对量化代理质量有强烈刚需。

---

## 8. 待处理积压

| 项目 | 状态 | 创建时间 | 重要性 | 备注 |
|------|------|----------|--------|------|
| [#3566 A2A 协议支持](https://github.com/zeroclaw-labs/zeroclaw/issues/3566) | OPEN, `status:accepted` | 2026-03-15 | 高（7👍，9评论） | 提出已 4 个月，标记 accepted 但无 PR。依赖 v0.9.0 路线图（#7432）。 |
| [#6685 SOP HTTP fan-in 未接线](https://github.com/zeroclaw-labs/zeroclaw/issues/6685) | OPEN, `

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*