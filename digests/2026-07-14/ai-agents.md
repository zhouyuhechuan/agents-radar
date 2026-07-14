# OpenClaw 生态日报 2026-07-14

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-07-14 01:49 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 OpenClaw 项目数据，我为您生成了 2026 年 7 月 14 日的项目动态日报。

---

### OpenClaw 项目日报 (2026-07-14)

#### 1. 今日速览

今日 OpenClaw 项目异常活跃，共处理近千条 Issue 与 PR，显示出社区极高的参与度和维护团队的积极响应。新版本 v2026.7.1 发布，带来了多项模型与提供者的更新，但同时也引入了新的回归问题。值得注意的是，多个 P0 级严重 Bug（如工具结果返回占位符、数据库损坏）目前仍处于“开放”状态，亟需维护团队优先处理，这对项目的稳定性构成了挑战。总体而言，项目处于高迭代、高活跃度，但稳定性风险并存的状态。

**活跃度评估：****极高**。

#### 2. 版本发布

- **最新版本**: **v2026.7.1**
- **核心亮点**:
    - **新模型与提供者**: 新增了 Featherless, Claude Sonnet 5, Mythos 5, Meta Muse Spark 1.1 和 ClawRouter。
    - **默认模型更新**: 新安装的默认模型变更为 **GPT-5.6**。
        - 对于 **Sol** 和 **Terra** 代理，默认启用 `/think ultra` 思维模式。
        - 对于 **Luna** 代理，默认启用 `max` 模式。
    - **兼容性提升**: 支持了 Z.AI 提供者的 `max` 模式。
    - **OAuth 改进**: 刷新了 OAuth 授权后的模型可用性列表。
- **潜在问题**: 此版本引入了导致 `models list` 命令崩溃的回归问题（详情见“Bug 与稳定性”部分）。

#### 3. 项目进展

今日有多个重要 PR 推进了项目进展，主要集中在通道、安全性和核心功能修复上。

- **通道适配**: [PR #106026](https://openclaw/openclaw/pull/106026) 修复了进度草案在短时间内重复出现的问题，并优化了跨多个平台（Discord, Matrix, Slack 等）的长任务进度提示。
- **安全强化**: [PR #81185](https://openclaw/openclaw/pull/81185) 引入了一项关键安全特性：在将 `exec` 工具的执行结果返回给 AI 模型之前，对结果负载（包括 stdout/stderr）中的敏感信息进行**脱敏处理**。该 PR 已准备好等待维护者审查。
- **飞书（Feishu）通道修复**: [PR #104322](https://openclaw/openclaw/pull/104322) 解决了飞书消息发送因网络瞬态故障而丢失的问题，通过引入重试机制保障了消息的可靠投递。同样，[PR #106541](https://openclaw/openclaw/pull/106541) 添加了入站媒体下载的超时机制，防止流程被永久阻塞。
- **核心功能修复**: [PR #106963](https://openclaw/openclaw/pull/106963) 修复了中断的 Agent 会话中工具调用历史损坏的问题，防止了 Anthropic API 持续拒绝请求的错误。此修复对于提升 Agent 的鲁棒性至关重要。

#### 4. 社区热点

- **Issue #75: [Linux/Windows Clawdbot Apps](https://openclaw/openclaw/issues/75)**
    - **热度**: 评论 112 条，获得 81 个 👍。评论数遥遥领先，是今日最受关注的话题。
    - **诉求**: 自 2026 年初起，社区持续强烈呼吁 OpenClaw 推出 Linux 和 Windows 平台的桌面应用。该项目目前仅有 macOS、iOS 和 Android 客户端，导致大量其他平台用户无法获得本地级体验。这表明**跨平台桌面支持**是社区当前最核心的未满足需求，且长期未得到解决，积累了明显的用户不满。

- **Issue #106914: [`models list` crashes: TypeError...](https://openclaw/openclaw/issues/106914)**
    - **热度**: 虽评论不多，但作为新版本 **v2026.7.1** 立即暴露的回归问题，社区关注度极高。
    - **诉求**: 用户期望基础命令行工具能够稳定运行。该 Bug 使得核心管理命令 `models list` 直接崩溃，严重影响了用户体验和版本升级意愿。用户希望能在第一时间得到修复，并对版本发布的测试质量提出质疑。

#### 5. Bug 与稳定性

今日暴露的 Bug 严重程度分布极广，从 P0 级灾难性错误到可容忍的问题均有出现。

**P0 (灾难级别)**:
- **[Bug]: 所有工具结果返回 "(see attached image)" 占位字符串。** ([Issue #104721](https://openclaw/openclaw/issues/104721)) - **无修复 PR**。
    - **摘要**: 核心工具调用被完全破坏。所有工具（如文件读取、Exec 执行）的返回结果都被一个固定的占位符文本替代，系统已完全丧失实际功能。
- **CLI 启动前检检查可破坏正在运行的网关数据库。** ([Issue #101290](https://openclaw/openclaw/issues/101290)) - **无修复 PR**。
    - **摘要**: 在网关运行期间执行健康检查命令，可能导致 SQLite 数据库损坏 (malformed)，数据丢失风险极高。
- **遗留状态迁移源仍阻塞网关启动。** ([Issue #103076](https://openclaw/openclaw/issues/103076)) - **无修复 PR**。
    - **摘要**: 即使经过部分修复，仍有多个遗留状态（如 Matrix、Memory Core 等）的迁移问题导致网关无法正常启动，影响用户升级和部署。

**P1 (高严重度)**:
- **`models list` 命令在新版 v2026.7.1 中崩溃。** ([Issue #106914](https://openclaw/openclaw/issues/106914)) - **已关闭，有修复 PR**。
    - **摘要**: 新版本回归问题，`models list` 因无法处理某些模型的成本信息而直接报错。该问题已被快速修复。
- **Exec/工具失败后抑制模型响应并显示无意义文本。** ([Issue #100121](https://openclaw/openclaw/issues/100121)) - **无修复 PR**。
    - **摘要**: 当工具调用失败时，模型不会返回任何关于失败原因的说明，反而显示 "see attached image"，造成严重误导。
- **会话上下文在多轮对话中静默丢失。** ([Issue #76665](https://openclaw/openclaw/issues/76665)) - **无修复 PR**。
    - **摘要**: 在使用特定提供者（z.ai）时，Agent 会忘记前面轮次的对话内容，导致对话不连续，功能失效。

#### 6. 功能请求与路线图信号

社区持续提出新功能请求，部分已有关联 PR 存在，显示出较高的采纳可能性。

- **动态模型发现** ([Issue #10687](https://openclaw/openclaw/issues/10687)): 用户请求支持从 OpenRouter 等平台动态拉取最新的模型列表，而非依赖静态配置文件。此功能对快速创新提供者尤其重要，如被采纳，将极大提升平台的灵活性。
- **文件系统沙箱配置** ([Issue #7722](https://openclaw/openclaw/issues/7722)): 用户请求为 `exec` 工具添加细粒度的文件系统访问控制，以提升安全性。此功能与已提案的 PR [PR #81185](https://openclaw/openclaw/pull/81185) (对工具结果进行脱敏) 方向一致，共同强化 Agent 的安全边界。
- **Webhook 多轮对话支持** ([Issue #11665](https://openclaw/openclaw/issues/11665)): 请求修复 Webhook 会话功能，使得当 `sessionKey` 不变时，API 调用能维持多轮对话上下文。这对于集成到外部系统是一个重要功能。
- **Exec 命令黑名单支持** ([Issue #6615](https://openclaw/openclaw/issues/6615)): 用户希望除了现有的白名单（允许列表）外，还能配置黑名单（拒绝列表），实现更灵活的“放行所有，仅阻止特定高危命令”的安全策略。

#### 7. 用户反馈摘要

从今日的 Issue 和 PR 评论中，可以提炼出用户的真实痛点：

- **跨平台桌面应用缺失(User Feedback in Issue #75)**: 大量 Linux 和 Windows 用户表达了强烈的需求，他们希望获得与 macOS 用户同样流畅的原生桌面体验。
- **配置与升级的痛苦(User Feedback in Issue #90213)**: 用户反映即使是运行 `openclaw doctor --fix` 命令，也无法彻底解决升级后遗留的配置迁移警告，导致新版本体验受阻，感到沮丧。
- **会话数据丢失(User Feedback in Issue #77012, #76665)**: 用户对“会话丢失”或“对话宕机”这类问题异常敏感。在 WebChat 或特定提供者上，Agent 会忘记之前的对话，这会严重破坏用户对 AI 助手最基本的信任。用户明确回到了“这是一个回退”的错误。
- **功能的不确定性(User Feedback in Issue #77675)**: 用户对配置了 `SecretRef` 后，在未使用该配置的提供者上仍出现“未解决的 SecretRef”错误感到困惑，这表明错误提示不够精准，增加了用户的调试难度。

#### 8. 待处理积压

以下为长期未响应或被标记为 `stale`，但影响广泛的 Issue 和 PR，值得维护者关注。

- **Issue #38327**: [[Bug] "Cannot convert undefined or null to object" with google-vertex/gemini-3.1-pro-preview](https://openclaw/openclaw/issues/38327)
    - **状态**: 已开放超过 4 个月，影响稳定版本，涉及 Auth Provider 和崩溃循环，但至今无实质性进展。
- **Issue #75**: [Linux/Windows Clawdbot Apps](https://openclaw/openclaw/issues/75)
    - **状态**: 已开放 6 个多月，社区呼声最高但未被作为优先项目。考虑到其高热度，应考虑将其纳入路线图。
- **Issue #77121**: [exec tool can launch known-heavy upstream validation commands inside live Gateway resource domain](https://openclaw/openclaw/issues/77121)
    - **状态**: 重要的安全风险（可能造成 DoS），但处于 stale 状态，未得到维护者响应。
- **PR #81185**: [Redact exec tool result payloads](https://openclaw/openclaw/pull/81185)
    - **状态**: 提升安全性的重要 PR，已被标记为“ready for maintainer look”，但却等待了两个月仍未得到合并或实质性反馈。

---

## 横向生态对比

好的，作为 AI 智能体与个人 AI 助手领域开源生态的资深技术分析师，我将基于您提供的各项目 2026 年 7 月 14 日的社区动态，为您呈现一份横向对比分析报告。

---

### 2026-07-14 AI 智能体与个人 AI 助手开源生态横向对比分析报告

**分析师：** 资深技术分析师

---

#### 1. 生态全景

当前，个人 AI 助手与自主智能体开源生态正处于 **“大版本迭代后的深度修复与能力巩固期”**。一方面，以 `OpenClaw` 和 `CoPaw` 为代表的成熟项目在发布重要版本后，正集中精力解决社区反馈的 P0/P1 级稳定性问题，如上下文压缩导致工具调用失效、安装部署卡死等，优先保障核心体验。另一方面，`NanoClaw`、`NullClaw` 等新兴力量则在积极拓展信道（如电话/SMS）、强化安全审批流和引入跨提供商共享记忆等创新功能，预示着生态正从单纯的对话能力向更复杂的任务交付与系统集成演进。社区参与模式也从“提需求”转向“交代码”，多项目的关键修复与功能均来自外部贡献，但部分项目（如 `ZeroClaw`）因代码评审瓶颈面临贡献者积极性受挫的风险。

#### 2. 各项目活跃度对比

以下表格汇总了各项目在 2026-07-14 的核心活跃度指标。

| 项目名称 | 活跃 Issue 数 / 新开 | 活跃 PR 数 / 总活动 | 版本发布 | 项目健康度评估 | 核心阶段 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | ~1000 (总处理) / 多P0 Bug | ~1 (关键修复) | **v2026.7.1** | ⚠️ 高活跃但稳定性风险高 | 紧急修复/回归问题处理 |
| **NanoBot** | 2 (新开) | 44 (总) / 17 (合并) | 无 | ✅ 良好 | 功能迭代与 Bug 修复并重 |
| **Hermes Agent** | 22 (新开) | ~13 (关闭) | 无 | ✅ 良好 | 系统性清债与稳定性修复 |
| **PicoClaw** | 低 (历史 Issue 讨论) | 4 (待合并) | 无 | ⚠️ 活跃度中等，评审迟缓 | 关键功能修复等待合入 |
| **NanoClaw** | 0 | 27 (合并) | 无 | ✅ 极佳 | 功能创新与安全加固 |
| **NullClaw** | 0 | 12 (待合并) | 无 | ✅ 良好，但互动寡淡 | 代码产出高，功能模块完善 |
| **IronClaw** | 28 (活跃) | 50 (总) / 16 (合并) | 无 | ✅ 良好 | 架构演进与通道能力扩展 |
| **LobsterAI** | 0 | 21 (总) / 19 (合并) | 无 | ✅ 极佳 | 高强度稳定性加固与平台体验 |
| **CoPaw** | ~100 (总) | 大量 Fix PR | **v2.0.0.post1** | ⚠️ 关键修复期 | v2.0 稳定性补救与漏洞修复 |
| **TinyClaw** | - | - | - | 🔴 无活动 | 停滞 |
| **Moltis** | 0 | 1 (待合并) | 无 | ⚠️ 低活跃度窗口期 | 单一功能修复 |
| **ZeptoClaw** | - | - | - | 🔴 无活动 | 停滞 |
| **ZeroClaw** | 多 (严重Bug) | 50 (待合并) / 3 (处理) | 无 | ⚠️ 活跃但评审瓶颈严重 | 版本收尾与PR积压 |

#### 3. OpenClaw 在生态中的定位

- **核心参照与生态基石**：OpenClaw 在社区规模、Issues/PR 数量以及版本迭代节奏上（每日发布）处于 **绝对领先地位**，是个人 AI 助手领域的“标准制定者”。其日均近千条的社区活动量（今日数据）是其他项目的 10-100 倍，表明了其庞大的用户和开发者基础。
- **优势与成熟度**：OpenClaw 的主要优势在于其 **功能广度**（新模型、新通道、新提供者支持）与 **社区治理成熟度**（有明确的 Bug 响应和 PR 评审体系）。它是集成各类 AI 模型和端点的首选 Gateway。
- **技术路线差异**：相比 `NanoBot` 强调“社区功能”或 `NullClaw` 强调“安全与系统级集成”，OpenClaw 的技术路线是 **“大而全的通用基础设施”**。它试图提供一个单一平台，满足从个人聊天到复杂任务编排的所有需求。其高昂的社区活动量也反映了维护这种复杂性所需的巨大努力。
- **核心痛点**：今日日报显示，OpenClaw 存在多个 **P0 级别** 的未修复 Bug（如工具结果返回占位符、数据库损坏），这在其历史版本中较为罕见，表明 v2026.7.1 可能是一次匆忙的发布。这与其庞大的功能集带来的高熵值有关，是其当前最大的风险点。

#### 4. 共同关注的技术方向

以下方向是多项目共同涌现的热点趋势：

1.  **多平台桌面端体验**：
    - **涉及项目**：`OpenClaw` (Issue #75)，`Hermes Agent` (CJK输入法问题#39538)，`LobsterAI` (Windows安装器修复#2326)。
    - **具体诉求**：用户强烈要求提供稳定、原生的 Windows/Linux 桌面应用。CJK 输入法兼容性差、安装程序崩溃或被杀软拦截是主要的交互障碍。

2.  **工具安全与审计 (Sandboxing & Approval)**：
    - **涉及项目**：`OpenClaw` (PR #81185 结果脱敏, Issue #7722 沙箱)，`NanoBot` (PR #4320 审计模块)，`NanoClaw` (PR #2998 修复审批流，PR #3037 工具白名单)，`NullClaw` (PR #969 结构化审批流程)。
    - **具体诉求**：社区普遍要求对 Agent 的 `exec` 等强力工具进行访问控制、结果脱敏、操作审批和完整审计，以防止数据泄露和未授权操作，这是 Agent 走向企业级应用的必要条件。

3.  **跨会话与跨提供者记忆 (Memory & Context)**：
    - **涉及项目**：`NanoClaw` (PR #3012 跨提供商共享内存)，`NullClaw` (PR #961 可配置记忆召回)，`CoPaw` (Issue #5986 上下文压缩破坏工具调用)。
    - **具体诉求**：开发者们正在从“解决对话历史丢失”的基础Bug，演进到探索跨不同提供商、甚至跨 Agent 的持久化、可配置、高效利用的记忆系统，这将是下一代智能体能力的基石。

4.  **流式思考与过程透明度**：
    - **涉及项目**：`LobsterAI` (PR #2324 流式展示思考块)，`CoPaw` (Issue #5953 后台工具卸载)。
    - **具体诉求**：用户不再满足于只看到最终结果，而是期望 Agent 能实时展示其“思考过程”（如推理链、工具调用进度），并确保这一过程稳定、有序。

5.  **精细化权限与配置**：
    - **涉及项目**：`CoPaw` (Issues #5947, #5963, #6020 关于MCP权限、超时、审批路由)，`NanoBot` (PR #4313 WebUI 配置同步)。
    - **具体诉求**：用户对“无感审批”、“超时硬编码”、“错误提示不准确”等粗放的管理模式不满，要求提供更细粒度、可定制、可预测的控制能力。

#### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 通用 AI 网关 & 全能助手 | AI 发烧友、开发者、集成商 | 庞大的插件和通道生态，单一服务管理多模型 |
| **NanoBot** | 社区互动 & 精细化的功能体验 | 追求丰富功能和社区感的个人用户 | 注重审计、多语言、信息流分层等用户体验细节 |
| **Hermes Agent** | 跨平台客户端 & 稳定交互 | 桌面端重度用户、CJK用户 | 强客户端方向，近期聚焦桌面端/CLI 的稳定性 |
| **PicoClaw** | 嵌入式/边缘场景 & 安全通信 | 高级用户、安全研究员 | 强调端到端加密 (E2EE) 和底层依赖安全性 |
| **NanoClaw** | 多Agent协作 & 扩展信道 | 寻求企业级功能（如电话集成）的开发团队 | 架构领先，强调跨提供商记忆和第三方信道（如Dial） |
| **NullClaw** | 高性能 & 系统级集成 | 追求极致安全和系统融合的开发者 | Zig 语言实现，定位为系统级组件，强调低资源占用和安全性 |
| **IronClaw** | 企业级工作流 & 扩展管理 | 企业团队、内部流程自动化 | 聚焦于“扩展”和“例行任务”的统一管理模型 |
| **LobsterAI** | 办公协同 (Cowork) & 多轮交互 | 办公场景下的团队用户 | 强客户端，围绕“Cowork”功能构建产品，注重跨平台部署体验 |
| **CoPaw** | 通用助手 & 中文社区 | 中文开发者社区（与腾讯Workbuddy对比） | 与特定模型（如Qwen）深度集成，v2.0后高度关注可靠性回归 |
| **ZeroClaw** | 零代码平台 & 自动化 | 希望可视化配置工作流的用户 | 强调零代码和标准操作程序(SOP)自动化 |

#### 6. 社区热度与成熟度

- **第一梯队（极高活跃，快速迭代与质量巩固并行）**：
    - **OpenClaw**、**NanoBot**、**CoPaw**。这类项目拥有庞大的社区讨论量（日产上百 Issue）和快速的 PR 合并节奏，其中 `OpenClaw` 和 `CoPaw` 因大版本迭代正面临宝贵的“质量阵痛期”。

- **第二梯队（高活跃，功能创新与稳定性完善）**：
    - **Hermes Agent**、**NanoClaw**、**LobsterAI**、**NullClaw**。这些项目今日的 PR 产出和合并效率很高，且 Bug 修复精准，表明团队或核心贡献者执行效率高。`NanoClaw` 和 `NullClaw` 在功能创新上尤其活跃。

- **第三梯队（中低活跃，需求明确但评审阻塞）**：
    - **PicoClaw**、**IronClaw**、**ZeroClaw**、**Moltis**。这些项目有少量但高质量的活动，但核心瓶颈在于维护者响应速度。`ZeroClaw` 的 50 个待合并 PR 是典型象征。

- **停滞项目**：
    - **TinyClaw**、**ZeptoClaw**。24小时内无任何活动，已基本停止迭代。

#### 7. 值得关注的趋势信号

1.  **从“对话”到“任务交付”的范式转移**：社区反馈已从“模型回答好不好”转变为 **“工具执行是否可靠”**、**“审批流程是否安全”**、**“定时任务是否稳当”**。这说明 AI 智能体已过了“图新鲜”的阶段，用户开始将其作为生产工具，**对其可靠性、安全性和可审计性提出了前所未有的高要求**。这对开发者的启示是：在构建 Agent 时，任务编排、状态管理、错误处理和权限控制的重要性将超过模型选型本身。

2.  **“记忆”成为智能体的核心竞争力**：`NanoClaw` 的跨提供商共享内存和 `NullClaw` 的可配置记忆系统是重要信号。未来的智能体将不再是“无状态”的 API 调用者，而是 **“有历史、有偏好、有知识”的持久化数字实体**。如何高效、安全、私密地管理这些“记忆”，是下一个技术高地。

3.  **安全内建 (Security by Design) 成为入场券**：从 `OpenClaw` 的脱敏到 `NanoBot` 的审计，再到 `NanoClaw` 的审批流修复和白名单，以及 `ZeroClaw` 仍在讨论的轻量化核心（暗示降低攻击面）。这说明 **社区已不能容忍 Agent 在“裸奔”状态下运行**。任何面向企业或严肃场景的 AI 智能体项目，必须将安全机制作为核心架构的一部分，而非后期补丁。

4.  **开发者体验（DX）的标准化**：`ZeroClaw` 正在制定新的贡献指南，`NanoClaw` 的 `Structured skill format` 推进，`CoPaw` 面临升级后的配置兼容性问题。这些信号表明，社区要求 **更清晰的扩展机制、更稳定的 API 和多版本兼容策略**。对开发者而言，选择生态时，其 API 稳定性和文档完备性将比功能数量更重要。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 | 2026-07-14

---

## 今日速览

过去 24 小时内，NanoBot 项目保持了较高的社区活跃度：共处理 13 个 Issue（2 个新开/活跃，11 个已关闭），44 个 PR（27 个待合并，17 个已合并/关闭）。无新版本发布。**项目整体健康度良好**，Bug 修复（尤其是 Dream 模块、Discord 集成、参数序列化）与功能开发（审计模块、国际化、通道重构）同步推进，社区反馈集中在工具链灵活性和集成体验上。两款高优先级 Bug 仍待解决，但已有相应方案在 PR 中。

---

## 版本发布

**无**（过去 24 小时内无新 Release）。

---

## 项目进展

今日共合并/关闭 17 个 PR，其中关键推进包括：

- **审计模块**（#4320 ✅ 已合并）— 增加 `tools.audit` 配置和 `AuditTool`，为 agent 动作提供可观测性，支持开关、本地/远程 scope 和挂钩，零性能开销。  
  [HKUDS/nanobot PR #4320](https://github.com/HKUDS/nanobot/pull/4320)

- **Dream 内存 diff 修复**（#4909 ✅ 已合并）— 忽略仅换行符差异的 CRLF/LF 问题，防止空文件被误报为已修改，并添加回归测试。  
  [HKUDS/nanobot PR #4909](https://github.com/HKUDS/nanobot/pull/4909)

- **WebUI 巴西葡萄牙语本地化**（#4914 ✅ 已合并）— 新增 pt-BR 完整翻译，注册到 i18n 配置。  
  [HKUDS/nanobot PR #4914](https://github.com/HKUDS/nanobot/pull/4914)

- **文档更新**（#4913 ✅ 已合并）— 刷新近期更新日志至 7 月 12 日，补充 17 天历史条目。  
  [HKUDS/nanobot PR #4913](https://github.com/HKUDS/nanobot/pull/4913)

- **移除失效 Star History 嵌入**（#4912 ✅ 已合并）— 因 GitHub 限制公开 stargazers 端点，避免 README 显示损坏图片。  
  [HKUDS/nanobot PR #4912](https://github.com/HKUDS/nanobot/pull/4912)

此外，多个 Issue（如 #4897 Discord 集成、#4882 Dream 空文件 diff、#4893 dream-log 过滤、#4894 dream session 修剪）已关闭，说明这些问题已找到修复方案并被处理。

---

## 社区热点

- **#4864 [OPEN] Bug: Endless loop for `<tool_call> <function=complete_goal>`** — 被标记为 Bug，已获 3 条评论。核心问题：Gateway 将 `recap` 参数解析为裸字符串而非 JSON 对象，导致 `complete_goal` 工具无限错误重试。该 Bug 疑似由近期工具参数序列化变更引入，影响 agent 正常完成目标。社区期待快速修复。  
  [HKUDS/nanobot Issue #4864](https://github.com/HKUDS/nanobot/issues/4864)

- **#4911 [OPEN] Enhancement: A guarded tool gateway seam so channels can run the agent's tools** — 新开讨论，无评论但标志着架构层面的需求：当前 channel 仅有 config 和 bus，无法调用 agent 工具。实况语音通道等场景需要让 channel 安全地访问工具。该提案可能影响核心设计，值得关注。  
  [HKUDS/nanobot Issue #4911](https://github.com/HKUDS/nanobot/issues/4911)

- **#1500 [CLOSED] 信息流强制输出** — 虽已关闭，但获得 1 个 👍 和 2 条讨论，用户强烈期望消息分层机制（类似日志级别），避免 agent 执行过程无差别输出。这代表了社区对用户体验精细化的普遍诉求。  
  [HKUDS/nanobot Issue #1500](https://github.com/HKUDS/nanobot/issues/1500)

---

## Bug 与稳定性

按严重程度排序：

| 严重程度 | Issue | 状态 | 简述 | 关联 Fix PR |
|----------|-------|------|------|-------------|
| **高** | [#4864](https://github.com/HKUDS/nanobot/issues/4864) | OPEN | `complete_goal` 因参数序列化错误陷入无限循环，agent 无法完成任务 | 暂无对应 PR |
| **高** | [#4897](https://github.com/HKUDS/nanobot/issues/4897) | CLOSED | Discord 集成上线后无法收到消息，bot 显示在线无响应 | 已修复（关闭） |
| **中** | [#4893](https://github.com/HKUDS/nanobot/issues/4893) | CLOSED | `/dream-log` 和 `/dream-restore` 显示非 Dream 提交，git 过滤缺失 | 已修复 |
| **中** | [#4894](https://github.com/HKUDS/nanobot/issues/4894) | CLOSED | `prune_dream_sessions()` 不匹配 base64 编码文件名，无法修剪新格式会话 | 已修复 |
| **低** | [#4882](https://github.com/HKUDS/nanobot/issues/4882) | CLOSED | Dream content diff 报告空文件为已修改（+0 -0） | 已修复（PR #4909） |
| **低** | [#4887](https://github.com/HKUDS/nanobot/issues/4887) | CLOSED | 测试环境 `dev` 缺少 `lark-oapi`，飞书测试失败 | 已修复 |

此外，高优先级 Bug 修复 PR 正在推进：  
- PR #4917：修复 Windows 下工具输出 UTF-16 解码问题（对应 #4881）  
- PR #4888：使用文件锁序列化工作区写入，防止并发修改（对应 #4798）  
- PR #4816：缩小 `BaseException` 捕获范围，避免 `KeyboardInterrupt` 被误转为工具错误

---

## 功能请求与路线图信号

- **工具网关通道集成**（#4911）— 社区提议让 channel 能安全调用 agent 工具，是实时语音等场景的基础。结合已有重构 PR #4908（通道实例所有权与设置迁移），未来可能被纳入 0.3.x 版。

- **模型预设与会话绑定**（PR #4866，OPEN）— 在 session 元数据中持久化模型预设选择，使 `/model` 命令会话作用域化，增强多模型切换体验。

- **Heartbeat 触发命令**（PR #4620，OPEN）— 增加 `nanobot heartbeat trigger`，支持 `--dry-run` 和 `--json`，填补 CLI 与定时心搏的空白。

- **自动发现 Agent Hooks**（PR #4878，OPEN）— 仿照 channel/tool 的注册模式，引入 `pkgutil` 扫描与 entry_points，简化自定义 hooks 开发。

- **WebUI 导出 Markdown**（PR #4587，OPEN）— 对话 session 导出为 `.md` 文件，包含说话人标签、时间戳和折叠细节。

- **WebUI 与 config.json 设置同步**（PR #4313，OPEN）— 新增多个写端点，让 WebUI 面板直接修改 `temperature`、工具限制、dream 等配置。

这些特性若合入，将显著提升 NanoBot 的 **可插拔性、多模态支持、开发者体验**，有望成为下一个里程碑的亮点。

---

## 用户反馈摘要

从 Issue 评论中提炼的典型用户声音：

- **信息过滤需求** (#1500)：「不希望看到每一个工具调用的详细步骤，就像日志有等级一样，应该有一个消息分层机制。」用户希望 agent 在执行任务时能按重要性输出，避免刷屏。

- **飞书文件接收问题** (#2352)：「无法找到或下载发送的文件，bot 总是打开浏览器访问飞书网页端，但给足了权限。」用户推测应有 MCP 存储接口，目前配置方法不明确。

- **Discord 集成困惑** (#4897)：「bot 显示在线但收不到消息，确保 Token 正确但还是不行。」用户对 Discord 通道的初始连接稳定性有疑虑。

- **Dream 内存 diff 误报** (#4882)：「空白文件被报告为 `+0 -0`，导致无意义的变更记录。」用户期待更智能的内容比对。

- **工具参数序列化回归** (#4864)：「complete_goal 不断报错，此前能正常工作，最近更新后 gateway 解析变了。」用户明显感受到回归问题，希望快速回滚或修复。

---

## 待处理积压

以下 PR/Issue 长期未取得充分进展或处于冲突/待审核状态，建议维护者关注：

| 类型 | 编号 | 标题 | 状态 | 滞留原因 |
|------|------|------|------|----------|
| PR | [#1599](https://github.com/HKUDS/nanobot/pull/1599) | feat(telegram): stream LLM responses via sendMessageDraft | OPEN（冲突） | 自 3 月起未合并，代码冲突 |
| PR | [#4587](https://github.com/HKUDS/nanobot/pull/4587) | Add WebUI session Markdown export | OPEN（冲突） | 依赖 #4579，代码冲突 |
| PR | [#4313](https://github.com/HKUDS/nanobot/pull/4313) | Feat(webui): config.json/webui parity | OPEN（冲突） | 涉及大量配置修改，冲突 |
| PR | [#4620](https://github.com/HKUDS/nanobot/pull/4620) | add heartbeat trigger command | OPEN | 需 Review 与合并决策 |
| PR | [#4853](https://github.com/HKUDS/nanobot/pull/4853) | feat(tools): add nano_timer core tool | OPEN（冲突） | 时间工具，冲突 |
| Issue | [#1500](https://github.com/HKUDS/nanobot/issues/1500) | 信息流强制输出 | CLOSED | 虽关闭但用户建议（消息分层）值得在未来设计中参考 |

这些积压项代表了社区长期关注的方向，若能及时解决，将提升项目对电报、飞书等非标准场景的支持力度以及配置体验的一致性。

---

*本日报由 AI 基于公开 GitHub 数据自动生成，数据截止时间：2026-07-14 02:00 UTC。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我将根据您提供的 Hermes Agent 项目 GitHub 数据，为您生成 2026 年 7 月 14 日的项目动态日报。

---

### **Hermes Agent 项目日报 | 2026-07-14**

#### **1. 今日速览**

今日项目活跃度极高，主要体现在对历史积压 Issue 的集中处理上。过去24小时内，项目团队关闭了 28 个 Issue 和 13 个 PR，这其中包括大量在 6 月初报告的、涉及 CLI、桌面端、配置和多个平台的 Bug。这表明项目正在经历一个强力的“清债”阶段，对 v0.15.1 版本后的稳定性问题进行了系统性修复。然而，今日也新涌现出 22 个活跃 Issue，其中涉及 MCP 服务器连接循环、本地大模型内存泄漏等较为深层的问题，需要团队持续关注。总体来看，项目状态健康，步调是修复优先于新功能。

#### **2. 版本发布**

- **无新版本发布。**

#### **3. 项目进展**

今日项目向前迈出了一大步，重点在于修复了影响用户日常使用的多项关键问题。多个修复 PR 被合并至主分支 (`sweeper:implemented-on-main`)，显著提升了桌面端、CLI 工具和 Dashboard 的稳定性和兼容性。

- **修复 CLI 与桌面端稳定性问题**:
  - **[PR #39557 - fix(cli): catch _build_web_ui exceptions to prevent half-updated state]**：解决了 `hermes update` 因 Web UI 构建失败而中断，导致系统处于半更新状态的严重问题。用户可安全重试更新。
  - **[PR #39543 - fix(dashboard): preserve injected session token]**：修复了 Dashboard 因 Session Token 失步导致 WebSocket 连接失败的问题。
  - **[PR #39565 - fix(desktop): clip sidebar overflow while sessions run]**：修复了桌面端侧栏在运行时会水平溢出的视觉问题。
  - **[PR #39566 - fix(desktop): inline local files for remote prompts]**：修复了桌面端连接远程网关时，无法正确上传本地图片/文件的问题。
  - **[PR #39554 - fix(desktop): omit invalid dashboard web dist env]**：修复了 macOS 上桌面端启动 Dashboard 时，因错误的 `HERMES_WEB_DIST` 环境变量导致前端 404 的问题。

- **修复核心 Agent 与 Provider 兼容性问题**:
  - **[PR #39562 - fix(model-metadata): gate Ollama api/show probes]**：修复了使用 OpenRouter 等非 Ollama 提供商时，Agent 误发 `api/show` 请求导致 404 错误的问题。
  - **[PR #39546 - fix(agent): preserve explicit CLI session source]**：确保通过 CLI 创建的 Agent 会话来源（`source`）不会被错误覆盖，保障了会话管理的一致性。

- **清除积压 Bug (由 `sweeper` 机器人标记为已合并)**：大量 6 月初报告的 Bug 今日被关闭，包括 `chinese prompt cut off`（#39534）, `CJK IME text drop`（#39538）, `backend fails with --tui`（#39503）等，表明项目对用户反馈响应积极。

#### **4. 社区热点**

今日最高讨论度的议题集中在中文、日文、韩文（CJK）输入法在桌面端的糟糕体验。

- **[Issue #39538 [CLOSED] - Desktop composer drops or fails to send CJK IME text on Enter]**: 该 Issue 获得了 6 条评论和 2 个 👍。用户抱怨使用 CJK 输入法时，按下回车后消息发送失败或只发送了部分内容。这是一个严重影响非英语用户日常使用的痛点，其关联的 Issue #39231 和 #39534 也反映了同类问题。该Issue今日已被关闭，说明社区反馈的问题得到了快速响应和解决。

#### **5. Bug 与稳定性**

今日报告的 Bug 覆盖范围广泛，从易用的配置问题到核心的执行逻辑均有涉及。已有一批修复 PR 上线，但仍有高严重性问题亟待解决。

**高优先级（P1-P2）:**

- **P2 - [Issue #64020 - [Setup]: failing payment method]**: 新用户反馈注册订阅时无法完成支付（银行卡被拒），阻碍了核心功能的接入。目前状态为 `needs-repro`，需官方确认并给出解决方案。
- **P2 - [Issue #64073 - Streamable HTTP MCP server stuck in keepalive/reconnect loop]**: Agent 与远程 MCP 服务器的连接约每 10 分钟超时一次，导致 Session 频繁断开和重建。这是一个涉及底层通信协议稳定性的问题，影响依赖 MCP 工具的任务。
- **P2 - [Issue #63849 - Tool-result images are never evicted on the OpenAI-compatible path]**: 在使用兼容 OpenAI 的本地模型时，工具调用产生的截图等图像数据永远不会被移除，最终导致内存溢出（OOM）。这是一个严重的性能与可靠性问题，会阻断长时间会话。
- **P2 - [Issue #64055 - Dashboard no longer respects auth methods]**: 自托管 Dashboard 不再支持 OIDC 认证，强制用户使用 Nous Portal 登录，破坏了自托管用户的认证流程。

**中低优先级（P3）:**

- **P3 - [Issue #63895 - [Bug] Terminal autoscrolls to bottom even when agent output is finished]**: 终端窗口在 Agent 完成回复后仍然周期性自动滚动到底部，导致用户无法正常查看对话历史。这是一个纯粹的体验问题。

**已有修复的Bug:** 今日大量关闭的 Issue 均已有对应的功能或修复在 `main` 分支上，如 #39534、#39538、#39549、#39503 等。

#### **6. 功能请求与路线图信号**

今日并未涌现大量新功能请求，社区焦点主要集中在解决现有问题。

- **潜在功能方向:**
  - **[PR #62706 - feat(desktop): autoplay image carousel from MEDIA-GALLERY: blocks]**: 这是一个仍在开放的 PR，旨在为桌面端增加多图片轮播功能。这表明项目方在探索提升 Agent 在桌面端多媒体内容展示的能力。
  - **[PR #64094 - feat(desktop): surface async process/delegation results in chat]**: 这是一个新提交的PR，希望在对话中更清晰地展示后台进程或委派任务的结果，而不是仅仅更新一个容易被忽略的状态栈。这增强了 Agent 在复杂、异步任务场景下的透明度和用户体验。

**路线图信号:** 当前版本（v0.15.x）处于一个明确的“稳定化”阶段。团队的下一个里程碑很可能是一个包含今日所有修复的 Bugfix 版本，之后才会将上述功能请求提升到更高的优先级。

#### **7. 用户反馈摘要**

从今日关闭和活跃的 Issue 中，可以提炼出以下用户反馈：

- **CJK 输入法体验是核心痛点：** 来自中文、日文、韩文用户的反馈非常集中，抱怨桌面端和 Dashboard 对 IME 输入支持不完善。这很可能是 Hermes Agent 在亚洲市场推广的一个重要体验瓶颈。
- **CLI 工具的健壮性需要提升：** 多个用户反馈 `hermes update` 命令容易失败（#39549），且对环境配置（如 `uv` 工具、`~/.hermes/.env` 文件中的环境变量覆盖）敏感，这影响了用户升级和部署的顺畅体验。
- **Dashboard 的自托管体验需改善：** 用户对 Dashboard 的配置和认证问题（#54801, #64055）感到困惑，特别是备份功能无法使用、认证方式被强制更改等问题，反映出 Dashboard 的 CI/CD 或配置管理流程可能存在测试盲区。

#### **8. 待处理积压**

以下 Issue 和 PR 存在时间较长且状态为“开放”，建议维护者关注：

- **[PR #39564 - fix(desktop): stop scroll and composer jumps]**: 创建于 2026-06-05，旨在解决桌面端滚动和 Composer 输入框跳动问题。该 PR 已开放超过一个月，与今日新增的滚动 Bug（#63895）相关，有必要考虑合并或提供替代方案。
- **[PR #39555 - fix(api): keep forked sessions listable]**: 创建于 2026-06-05，旨在修复 API Fork 会话的可列性问题。该 PR 已开放一个多月，它直接关系到 API 用户管理和查询会话的能力。
- **[PR #39542 - fix(profiles): avoid nesting custom profiles roots]**: 创建于 2026-06-05，关于自定义 Profiles 路径嵌套的逻辑修复。此 PR 处于开放状态，可能影响部分高级用户的配置布局。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，现将根据PicoClaw项目在2026年7月13日至7月14日（北京时间）的GitHub动态，生成如下项目日报。

---

## 📈 PicoClaw 项目日报 | 2026-07-14

### 1. 今日速览

今日项目活跃度中等，主要集中于长期悬而未决的功能请求和Bug报告的社区讨论更新，而非大量新问题的涌入。**issues 与 PR 的整体更新量偏低**，但其中涉及加密库替换、AI 模型兼容性及高级缓存功能等关键领域。值得注意的是，有 **1 个 PR 已被合并**，标志着 Gateway Webhook 功能或修复的落地。同时，**4 个待合并的 PR 均处于等待维护者响应的状态**，部分已持续超过两周，项目整体推进节奏略显迟缓，维护者响应速度是当前健康度的主要关注点。

### 2. 版本发布

**无新版本发布。** 项目在过去24小时内未有新的Release Tag产生。

### 3. 项目进展

今日合并了 **1 个关键 PR**，并有多项重要修复在等待合并。

-   **已合并：功能/网关Webhook (PR #3253)**：由贡献者 `tisoga` 提交的 `Feat/gateway webhook` 已被合并。虽然摘要未明确细节，但此功能的落地可能意味着 PicoClaw 在 API 网关集成或事件通知机制上有了新进展，增强了其作为智能体平台的扩展能力。

-   **待合并：模型引用解析修复 (PR #3254)**：`fix(agent)` 系列中关于模型引用解析的 PR 是今日最有价值的合并候选。它修复了 `lookupModelConfigByRef` 函数在模型名称匹配时的逻辑缺陷，**避免了一个简短的模型名错误地匹配到另一个同名的、但使用了 provider-alias 的模型。** 这个 Bug 修复将显著提升用户在多模型配置环境下的体验，确保配置的稳定性和可预测性。

-   **待合并：Anthropic 缓存支持 (PR #3228)**：此 PR 旨在修复 `anthropic-messages` 提供者无法正确处理系统消息块（`SystemParts`）及 `cache_control` 的问题。该项更新是 Anthropic 长上下文与 prompt caching 功能落地的核心前提，对深度使用 Claude 模型的用户至关重要。由于关联 Issue #3229 的持续讨论，此 PR 的状态值得关注。

### 4. 社区热点

今日社区讨论热度集中在少数几个历史问题，显示出社区对**安全性与高级模型功能**的强烈关注。

-   **热点一：[Feature] 使用 vodozemac 替代 libolm (Issue #3088)**
    -   **链接**: [Issue #3088](https://github.com/sipeed/picoclaw/issues/3088)
    -   **分析**: 这是今日讨论最活跃的问题，拥有8条评论和2个点赞。用户 `pbsds` 提出了用官方的 `vodozemac` 库替换已停止维护且存在安全隐患的 `libolm`。社区对此诉求反应积极，反映了用户群体对端到端加密通信底层安全性的高度重视。**这不仅是功能请求，更是一个安全合规性需求。** 项目是否能及时响应此迁移，将是检验其对安全承诺的关键指标。

-   **热点二：[Bug] 通过 OpenAI 兼容格式调用 Gemini API 时缺少 thought_signature (Issue #3230)**
    -   **链接**: [Issue #3230](https://github.com/sipeed/picoclaw/issues/3230)
    -   **分析**: 这是一个与多模型兼容性相关的具体 Bug。用户 `VictorSu000` 在使用 Cloudflare AI Gateway 以 OpenAI 兼容格式调用 Gemini API 时，因缺少 `thought_signature` 导致调用失败。这反映了在多供应商模型聚合场景中，**API 协议适配的复杂性和挑战**。社区正在关注此问题是否能被快速定位和修复。

### 5. Bug 与稳定性

今日报告的 Bug 数量不多，但涉及底层依赖兼容性问题。

| 严重程度 | Issue 编号 | 问题描述 | 是否已有 Fix PR |
| :--- | :--- | :--- | :--- |
| **高** | [#3230](https://github.com/sipeed/picoclaw/issues/3230) | 通过 OpenAI 兼容格式调用 Gemini API 时缺少 `thought_signature` 导致错误。 | 否 |
| **中** | [#3231](https://github.com/sipeed/picoclaw/issues/3231) | SearXNG 搜索功能无法使用 URL 拼接方式传递 `basicauth` 请求头，需要原生支持。 | 否 |

**分析**：Bug #3230 需要被优先关注，因为它直接影响了用户在特定配置下的正常使用。Bug #3231 则是关于第三方搜索集成的配置适配问题，影响面相对较小。

### 6. 功能请求与路线图信号

今日出现了一个具有潜力的功能提案，结合已有的 PR，可以看出社区对**高级缓存机制**的渴求。

-   **主要信号：滚动式对话缓存断点与运行时上下文分离 (Issue #3229)**
    -   **链接**: [Issue #3229](https://github.com/sipeed/picoclaw/issues/3229)
    -   **分析**: 用户 `AayushGupta16` 在提交了 PR #3228（修复 Anthropic 缓存支持）后，进一步提出了一个更高级的特性。该提案旨在解决 agent 工作流中，**对话历史是主要 Token 消耗源**的痛点。用户建议实现“滚动式缓存断点”，并确保易变的运行时上下文不会污染缓存的固定前缀。这是一个**深度技术讨论**，若被采纳，将极大提升使用 Anthropic Claude 等模型进行复杂任务时的效率和成本效益。这表明项目社区开始向更高级、更高效的 AI 交互模式演进，是路线图中的强烈信号。

-   **潜在纳入下一版本的功能**：
    1.  实现 `vodozemac` 库替换（Issue #3088）—— 取决于维护者的安全优先级。
    2.  完善 Anthropic 的 Prompt Caching 支持（PR #3228 及相关 Issue #3229）。

### 7. 用户反馈摘要

从今日的 Issues 评论中，可以提炼出以下用户反馈：

-   **痛点与诉求**:
    -   **安全焦虑**: 用户对使用已停止维护的 `libolm` 库感到不安，明确表达了对于端到端加密（E2EE）长期安全性的担忧。
    -   **兼容性困扰**: 使用 Gemini API 结合 OpenAI 兼容格式的用户，遇到了非标准实现导致的错误，反映出当前协议实现可能过于僵化，未能充分考虑不同供应商的细微差异。
    -   **配置灵活性不足**: 中文用户反映了在集成外部搜索服务（如 SearXNG）时，认证方式的灵活性不足，期望能原生支持各种鉴权模式。

### 8. 待处理积压

以下几项长期未响应或积压的 Issue 与 PR 需引起维护者注意，它们可能成为项目前进的瓶颈。

-   **旧 Issue，高优先级**:
    -   **[Issue #3088] 使用 vodozemac 替代 libolm** (创建: 2026-06-09，已超一个月)：此需求已被标记为 `priority: high` 和 `stale`。长期未回应可能削弱社区对项目安全更新能力的信心。

-   **等待合并的 PR (均已 `stale`)**:
    -   **[PR #3192] Docker goreleaser 基础镜像升级** (创建: 2026-06-27)
    -   **[PR #3191] 清理重复的 .gitignore 条目** (创建: 2026-06-27)
    -   **[PR #3228] Anthropic 消息缓存修复** (创建: 2026-07-06)

**总结**：开源社区贡献的 small PR（如基础镜像升级、代码清理）和关键 Bug/功能修复 PR（如 Anthropic 缓存、模型解析）长期未被合并，这会抑制外部贡献者的积极性。建议维护者在下一轮迭代中优先处理这些积压的合并请求，以保持项目的健康协作生态。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 NanoClaw (github.com/qwibitai/nanoclaw) 数据生成的 2026-07-14 项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-07-14

## 1. 今日速览

过去 24 小时，NanoClaw 项目开发活跃度极高。虽然无新版本发布，但社区和核心团队合并/关闭了 **27 个 PR**，并解决了 **3 个悬而未决的 Issues**，显示出强大的项目推进能力。重点在于对安全审批流程的修复（`add_mcp_server` 劫持漏洞）、消息投递可靠性的增强（处理离线Channel），以及新增了 **Dial**（电话/SMS）信道的原生支持。项目正处于功能迭代与安全加固并重的阶段，整体健康状况良好。

## 2. 版本发布

*无新版本发布。*

## 3. 项目进展

今日项目核心进展体现在安全修复、核心功能增强和新的信道集成三个方面。

- **安全修复与加固**：
    - **修复**：针对 `#2827` 和 `#2762` 两个高危安全漏洞，`glifocat` 在 PR `#2998` 中修复了 `add_mcp_server` 审批流，现在审批卡片会**完整渲染 MCP 服务器的 payload**（包括 `args` 和 `env`），从而防止审批走私攻击。 [查看PR](https://github.com/qwibitai/nanoclaw/pull/2998)
    - **修复**：针对消息因信道适配器缺失而被静默丢弃的 Bug (`#2995`)，`glifocat` 在 PR `#2996` 中将消息路由至重试路径，而 `kpscheffel` 在 PR `#2226` 中则让系统在不匹配时直接抛出异常，确保问题能被发现和重试。 [查看PR 1](https://github.com/qwibitai/nanoclaw/pull/2226) | [查看PR 2](https://github.com/qwibitai/nanoclaw/pull/2996)

- **核心功能增强**：
    - **强大新功能**：`amit-shafnir` 团队贡献了跨提供商共享的持久化内存系统（PR `#3012`），并为其增加了 Codex 加载支持（PR `#3013`）。这使得不同 Agent 提供商（如 Claude、OpenAI）可以共享上下文记忆，显著提升了多 Agent 协作能力。 [查看PR 1](https://github.com/qwibitai/nanoclaw/pull/3012) | [查看PR 2](https://github.com/qwibitai/nanoclaw/pull/3013)
    - **可用性提升**：`romanbsd` 开启了 MCP 工具白名单功能（PR `#3037`），允许管理员通过环境变量限制 Agent 可调用的工具，增强了安全管控。`mcaldas` 则修复了 Agent 对时间和星期混淆的问题（PR `#3036`），通过在上下文头部注入当前时间和星期，提升了调度任务的可靠性。 [查看PR 1](https://github.com/qwibitai/nanoclaw/pull/3037) | [查看PR 2](https://github.com/qwibitai/nanoclaw/pull/3036)

- **新信道集成**：
    - **重磅更新**：`OmriBenShoham` 贡献了 **Dial** 信道（PR `#3032`），这是对短信/彩信和 AI 语音通话的原生支持，并提供了安装向导（PR `#3033`）。这使得 NanoClaw 的能力扩展到了电话网络，应用场景得到巨大拓展。 [查看PR 1](https://github.com/qwibitai/nanoclaw/pull/3032) | [查看PR 2](https://github.com/qwibitai/nanoclaw/pull/3033)

## 4. 社区热点

今日社区讨论的核心围绕 **安全和消息投递可靠性** 展开，主要由核心团队主导修复。

- **最具影响力修复：`add_mcp_server` 审批流安全漏洞**。虽然 `#2827` 和 `#2762` 评论数为 0，但对应的修复 PR `#2998` 是今日最重要的合并项，直接解决了高风险的审批劫持问题。这表明社区对核心安全机制非常关注，而维护者也给予了最高优先级响应。
- **消息丢失问题的连锁修复**。Bug `#2995` 揭示了消息在离线信道被标记为“已交付”的隐蔽问题，而 `#2226`、`#2743`、`#2996` 等一系列相关 PR 同时被合并，形成了一个完整的修复链条。这表明社区对数据完整性和消息传递可靠性有很高的期望，维护者也在系统性解决此类问题。

## 5. Bug 与稳定性

今日修复的 Bug 已全部关闭，无新 Bug 报告。以下是近期修复的重点问题：

| 严重程度 | Issue/PR | 问题描述 | 修复状态 |
| :--- | :--- | :--- | :--- |
| **严重** | `#2827`, `#2762` | `add_mcp_server` 审批流存在安全漏洞，可隐藏参数和变量，导致审批劫持。 | 已修复 (PR `#2998`) |
| **高** | `#2995` | 离线信道发送的消息被标记为已交付，未实际发送，存在数据丢失风险。 | 已修复 (PR `#2996`, `#2226`) |
| **中** | `#1825` (相关) | SQLite 查询失败时，Session 清理脚本静默失败，可能导致数据丢失。 | 已修复 (PR `#1889`) |

## 6. 功能请求与路线图信号

从今日合并的 PR 来看，项目未来路线图信号明确，重点关注 **安全可控**、**记忆共享** 和 **信道拓展**。

- **信号一：安全与治理**。新增的 `MCP工具白名单`（PR `#3037`）和修复审批流漏洞，表明项目正从“能用”向“安全可控”迈进，以满足企业级部署需求。
- **信号二：跨提供商记忆**。`持久化共享内存`（PR `#3012`）的引入是一个里程碑式功能，它解决了多 Agent 系统知识孤岛的问题，很可能成为后续版本的核心特性。
- **信号三：信道生态扩张**。新的 `Dial` 信道（PR `#3032`）加入，以及 `Structured skill format`（PR `#3035`）的推行，都显示项目正致力于标准化和简化新信道的接入流程，为构建更丰富的信道生态铺路。

## 7. 用户反馈摘要

本周期无大量用户评论，但提交的 Issue 和修复的 Bug 反映了用户的核心痛点：

- **用户痛点（安全）**：从 `#2827` 和 `#2762` 看，用户（`YLChen-007`）能深入挖掘并报告复杂的安全漏洞，说明社区内部存在高水平的安全研究者。用户对 Agent 自修改行为的安全性高度警惕。
- **用户痛点（可靠性）**：Bug `#2995`（`glifocat` 报告）描述了一个非常隐蔽的消息丢失场景。用户对“消息被标记为已送达但实际未发送”的行为表示失望，这是数据一致性的底线问题，而维护者迅速修复，表明了对用户信任的重视。
- **用户满意度**：虽然无直接评论，但从多个 PR（如 `#2996`、`#3032`）被快速接受合并来看，维护者对用户报告的 Bug 和贡献的新功能都给予了高度回应。这种高效的协作氛围是项目健康度的积极信号。

## 8. 待处理积压

- **PR `#2802`：Socket 安全加固**。该 PR（`ncl socket 超时/上限`）已开启近一个月仍为 OPEN 状态。由于涉及到 `ncl` 这一关键组件的安全性和稳定性，建议维护者尽快安排审查与合并，以防止潜在的 DoS 攻击或资源耗尽风险。
  [查看PR](https://github.com/qwibitai/nanoclaw/pull/2802)

- **PR `#3012` 与 `#3013`：共享内存系统**。这两个 PR 虽为重点新功能，但仍在开放状态。考虑到其重要性，维护团队应加快节奏，优先将其合入主干，以便社区尽早进行测试和反馈，为后续版本奠定基础。
  [查看PR 1](https://github.com/qwibitai/nanoclaw/pull/3012) | [查看PR 2](https://github.com/qwibitai/nanoclaw/pull/3013)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，现根据 NullClaw 项目的 GitHub 数据，为您呈上 2026 年 7 月 14 日的项目动态日报。

---

### NullClaw 项目动态日报 | 2026 年 07 月 14 日

**分析师：** AI 智能体分析助理

---

#### 1. 今日速览

今日 NullClaw 项目处于**高产出、低反馈**的活跃开发状态。过去 24 小时内，项目无新 Issue 提出，也无新版本发布，但维护者在 PR 清理方面表现积极，共有 **12 个 Pull Requests 处于待合并状态**，其中多数来自 6 月下旬，集中在修复 Agent CLI、Matrix 通道、安全认证以及引入结构化工具调用等关键领域。尽管 Issue 讨论近乎停滞，但代码层面的工作表明项目正稳步迈向更高稳定性和功能完备性，社区焦点从提出问题转向了贡献解决方案。**项目健康度评估：良好，但需警惕社区活跃度向代码仓库以外的渠道转移。**

#### 2. 版本发布

无

#### 3. 项目进展

今日无新 PR 被合并或关闭，但维护者正在积极审查并积累代码变更，以下 PR 若能顺利合并，将显著提升项目能力：

- **Agent CLI 与 REPL 增强：**
  - **[PR #970]** `fix(cli): handle arrow keys in agent REPL`：为 `nullclaw agent` 的交互式 REPL 引入了轻量级、零分配的行编辑器。支持方向键、历史导航、光标移动等。这将显著改善用户交互体验。
    - [查看详情](https://github.com/nullclaw/nullclaw/pull/970)
  - **[PR #969]** `feat(agent): structured approval_request / approval_response flow`：为 Shell 工具引入了结构化的“审批”流程。当工具需要用户批准时，Agent 会捕获请求并通过 SSE 事件发送给用户界面，实现了更安全的工具调用循环。
    - [查看详情](https://github.com/nullclaw/nullclaw/pull/969)

- **聊天通道稳定性与安全加固：**
  - **[PR #968]** `fix(matrix): persist next_batch across restart + test env isolation`：解决了 Matrix 通道重启后需要全量同步的问题。通过持久化 `/sync` 游标，避免每次重启都触发高开销的初始同步，极大提升了通道的稳定性和重连效率。
    - [查看详情](https://github.com/nullclaw/nullclaw/pull/968)
  - **[PR #966]** `fix(http): secure buffered curl fallback on Android`：修复了在 Android (Termux) 环境下 Zig 标准库 HTTP 路径 DNS 解析失败的问题。通过安全、完整的 curl 后备方案，确保终端用户能在移动设备上稳定工作。
    - [查看详情](https://github.com/nullclaw/nullclaw/pull/966)

- **核心功能与基础设施：**
  - **[PR #964]** `Enable native API-level tool calls during streaming`：允许在流式响应期间执行 API 级别的工具调用，并保留结构化工具调用增量。这意味着 Agent 可以边生成文本边调用工具，极大增强了实时交互能力。
    - [查看详情](https://github.com/nullclaw/nullclaw/pull/964)
  - **[PR #959]** `fix(cron): persist paired token for scheduler tool access`：修复了定时任务 (Cron) 在用户重新配对设备后无法访问的问题。现在配对令牌会被持久化加密存储，确保定时任务能够稳定工作。
    - [查看详情](https://github.com/nullclaw/nullclaw/pull/959)
  - **[PR #956]** `ci(deps): bump alpine from 3.23 to 3.24`：由 Dependabot 发起的基础镜像更新，保持 Docker 环境的依赖安全和最新。
    - [查看详情](https://github.com/nullclaw/nullclaw/pull/956)

**总结：** 项目在用户体验 (REPL)、异步安全 (工具审批)、通道可靠性 (Matrix 持久化)、以及平台兼容性 (Android HTTP) 等方面都有明确的代码改进，功能完备性正在稳步提升。

#### 4. 社区热点

今日社区讨论的热点主要集中在对 **“已提交且长时间未合并的 PR”** 的关注上。虽然评论区无新内容，但以下 PR 因其解决的问题对日常使用影响重大而成为焦点：

- **[PR #969] (Agent 审批流)** 和 **[PR #964] (流式工具调用)**：这两项功能代表了 Agent 从简单的问答向复杂、安全的自主任务执行迈出的关键一步。社区对更精细的工具控制能力和更流式的交互体验有很高的期待。
- **[PR #963]** `fix(channels): document and harden Weixin iLink QR auth`：解决微信渠道的认证问题是社区热点之一，尤其对于想在微信生态内使用 NullClaw 的用户，此 PR 的合并至关重要。
    - [查看详情](https://github.com/nullclaw/nullclaw/pull/963)
- **[PR #954]** `Fix: one-shot cron jobs silently fail to deliver messages`: 一个“静默失败”的 Bug 是用户最反感的问题之一，此 PR 的根因分析和修复牵动了许多依赖 Cron 功能用户的关注。
    - [查看详情](https://github.com/nullclaw/nullclaw/pull/954)

**背后诉求分析：** 社区不再仅仅是提出“我想要XX功能”，而是开始**贡献具体的代码实现**来解决痛点。这标志着项目正从初期用户积累阶段，转向**由社区开发者贡献核心代码**的成熟期。

#### 5. Bug 与稳定性

今日无新 Bug 报告。但下列待合并的 PR 正致力于解决数个影响稳定性的 Bug，按严重程度排列：

1.  **高：**[PR #954] `Fix: one-shot cron jobs silently fail to deliver messages`。这是一个严重的 **use-after-free** 错误，导致定时任务“静默失败”，用户完全不知情。该修复正在等待合并，对于依赖定时功能的用户来说影响巨大。
    - [查看修复 PR](https://github.com/nullclaw/nullclaw/pull/954)

2.  **中：**[PR #968] `fix(matrix): persist next_batch across restart`。技术上是性能问题，但每次重启都全量同步等同于功能降级，对需要持续运行的服务场景（如家庭自动化）影响较大。
    - [查看修复 PR](https://github.com/nullclaw/nullclaw/pull/968)

3.  **低：**[PR #966] `fix(http): secure buffered curl fallback on Android`。是一个平台特定问题，仅在特定设备和网络环境下触发，但对受影响的用户来说体验极差。
    - [查看修复 PR](https://github.com/nullclaw/nullclaw/pull/966)

#### 6. 功能请求与路线图信号

今日无新功能请求。但以下 PR 明确指向了项目的未来路线图：

- **实时、安全的人工交付 (Human-in-the-Loop):** [PR #969] 的审批流功能是该方向的重要基石，未来可能扩展到更多工具。
- **无缝的流式体验:** [PR #964] 的流式工具调用能力，是下一代 Agent 交互（如边思考边搜索）的核心，预计会成为 NullClaw 的差异化优势。
- **高度可控的记忆系统:** [PR #961] `feat(memory): add configurable auto-recall, recall_limit, max_context_bytes` 引入对记忆召回的可配置性，表明项目正在向 **“用户自定义记忆行为”** 的方向发展，以满足不同隐私和效率偏好。
    - [查看详情](https://github.com/nullclaw/nullclaw/pull/961)

结合已有 PR，可以判断**流式工具调用、结构化审批流程、精细化的记忆控制**以及**更强的多渠道稳定性**很可能是下一版本的重点方向。

#### 7. 用户反馈摘要

由于今日无新 Issue 评论，反馈摘要主要来自已合并/待合并 PR 的描述。
- **痛点：** 用户（开发者）在 Android 上遇到因 Zig 标准库网络请求不兼容而导致的应用故障。他们将此问题报告并通过提交`[PR #966]`来解决，体现了“bug报告+代码修复”的深入参与模式。
- **场景：** `[PR #969]` 的描述揭示了用户需要“agent在爆破服务器之前停下来问我一下”的安全使用场景，而不是无限制地执行命令。
- **不满：** `[PR #954]` 描述了一个令人沮丧的场景：“我以为Cron任务执行成功了，但什么都没发生”。暗示用户对静默失败的容忍度为零，要求系统具备更强的故障反馈能力。

#### 8. 待处理积压

以下为长期未响应或对项目发展至关重要的遗留 Issue/PR，建议维护者优先关注：

- **[PR #954]** `Fix: one-shot cron jobs silently fail to deliver messages (use-after-free)`： **高优先级**。已创建超过一个月且包含明确的 Bug 修复代码，应尽快合并，避免影响用户对 Cron 功能的信任。
    - [查看详情](https://github.com/nullclaw/nullclaw/pull/954)
- **[PR #959]** `fix(cron): persist paired token for scheduler tool access`： **高优先级**。与 PR#954 同属 Cron 稳定性问题，令牌持久化是基础安全要求，建议同时处理。
    - [查看详情](https://github.com/nullclaw/nullclaw/pull/959)
- **[PR #968]** `fix(matrix): persist next_batch across restart + test env isolation`： **中优先级**。作为主要通道之一，Matrix 的重启性能问题值得尽快解决。
    - [查看详情](https://github.com/nullclaw/nullclaw/pull/968)

---
**日报结束**

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目日报 — 2026-07-14

## 1. 今日速览

过去 24 小时内，IronClaw 项目保持高活跃度，共处理 34 条 Issues（新开/活跃 28，关闭 6）和 50 条 PR（待合并 34，合并/关闭 16）。**无新版本发布**，但核心团队在多条主线（统一扩展模型、MCP 注册存储、Matrix 通道骨架）上密集推进，同时通过 `bug_bash` 系列 Issues 集中暴露和修复 P1/P2 级别的稳定性与 UX 问题。社区安全报告机制缺失的问题也首次被提出，值得关注。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 中，以下几项对项目架构和稳定性影响较大：

- **Matrix 通道骨架 (#6062)**：新增 Reborn 的 Matrix 通道 WASM 骨架，包含可加载的通道组件、宿主管理的能力清单、本地构建/CI 门控及运行时冒烟测试，为后续实时同步、E2EE 等功能打下基础。  
  [PR #6062](https://github.com/nearai/ironclaw/pull/6062) — 已关闭（合并）

- **扩展所有权迁移构建 (#6058)**：在 Reborn Railway 运行时镜像中发运扩展所有权迁移二进制，并利用 cargo-chef 缓存 libSQL 依赖图，使得正常源码变更无需重建整个迁移图。  
  [PR #6058](https://github.com/nearai/ironclaw/pull/6058) — 已关闭（合并）

- **OAuth 与扩展生命周期加固 (#5957)**：合并了 Slack OAuth 激活修复、扩展移除清理修复，以及生产环境所需的显式所有权迁移。  
  [PR #5957](https://github.com/nearai/ironclaw/pull/5957) — 已关闭（合并）

- **存储错误原因链修复 (#5971)**：修正了 compaction summary 持久化失败时丢弃底层 `SessionThreadError` 的问题，使排查更准确。  
  [PR #5971](https://github.com/nearai/ironclaw/pull/5971) — 已关闭（合并）

此外，依赖批量更新 PR (#6021) 也已合并，涉及 `agent-client-protocol`、`webpki-roots`、`uuid` 等 22 个包。整体来看，项目在 **稳定性修复** 和 **新通道能力扩展** 两条线上同步前进。

## 4. 社区热点

今日讨论最活跃的 Issues 集中在 **用户感知到的 UI/行为不一致**：

- **GitHub 扩展激活状态错误报告 (#5948，5 条评论)**：助手错误地报告 GitHub 扩展已“激活并配置”，而实际仅处于“已安装”状态。用户对状态反映不准确感到困惑。  
  [Issue #5948](https://github.com/nearai/ironclaw/issues/5948)

- **对话历史错误横幅 (#6050，2 条评论)**：即使当前请求执行成功，页面上仍显示“加载对话历史失败”的红色横幅，使用户误以为整个对话已损坏。  
  [Issue #6050](https://github.com/nearai/ironclaw/issues/6050) — 已有修复 PR #6064

- **安全报告渠道缺失 (#6000，1 条评论)**：一名外部研究者发现仓库缺少 `SECURITY.md` 且私有漏洞报告功能被禁用，无法私下提交安全发现。此 issue 虽评论不多，但潜在影响大，已引起维护者注意。  
  [Issue #6000](https://github.com/nearai/ironclaw/issues/6000)

社区反应表明用户对 **UI 错误反馈的准确性和一致性** 有较高期望，同时对 **安全通信渠道** 的需求真实存在。

## 5. Bug 与稳定性

今日报告的 Bug 按严重程度分级如下（P1 为最高）：

### P1（关键）
- **Slack DM 发布到错误频道 (#5943)**：用户请求“发 Slack DM”，机器人却把内容发到了公共频道。  
  [Issue #5943](https://github.com/nearai/ironclaw/issues/5943)

### P2（高）
| Issue | 摘要 | 状态 |
|-------|------|------|
| #5836 | 例行任务每隔 5 分钟执行均失败，报“No thread attached”，成功率 0% | Open |
| #5885 | 审批通知无法显示审批卡片，用户无法操作 | Open |
| #5879 | 失败后错误横幅残留，即使后续成功也不消失 | Open |
| #5707 | 例行任务创建响应暴露内部实现细节（cron、触发器ID等） | Open |
| #6048 | 模型试图调用不可用的工具导致 run 失败 | Open |
| #6047 | 任务消息时序错乱，新消息显示在老消息上方 | Open |
| #6046 | 简单邮件转表单工作流触发 124 次工具调用，效率极低 | Open |
| #6045 | 代理诊断出根因后只解释不自动修复（如缺少 User-Agent 头） | Open |
| #6044 | 输入框 Enter 键间歇性不提交消息 | Open |
| #6043 | GitHub 连接流程失败，显示通用能力错误而非启动认证 | Open |
| #5882 | 反复断开重连 Slack 后认证流程进入死锁状态 | Open |
| #5883 | 工具执行成功后跟随请求失败，报通用“模型输出无法使用”错误 | 已关闭 |

### P3（中）
- #5948（GitHub 扩展激活状态错误）、#6050（历史加载横幅）、#5889（“加载更早消息”按钮无效）、#6052（扩展注册表加载慢）、#6051（大文档误标警告图标）、#6049（断开 Gmail 失败）、#5891（“上次完成”时间戳显示当前运行时间）——均为 UX 类问题，未出现内存泄漏或数据损坏。

关键发现：**P2 级别问题数量多且集中在交互流程（认证、消息排序、工具调用），暗示近期发布的某些功能可能存在系统性兼容问题。** 已有修复 PR #6064 针对 #6050，其余均待处理。

## 6. 功能请求与路线图信号

- **安全报告机制 (#6000)**：请求增加 `SECURITY.md` 或启用私有漏洞报告。此需求若得到快速响应，将有助于吸引安全研究者参与。  
  [Issue #6000](https://github.com/nearai/ironclaw/issues/6000)

- **GitHub 扩展生命周期管理 (#6029)**：用户反馈扩展激活后无法停用、重新配置或卸载。  
  [Issue #6029](https://github.com/nearai/ironclaw/issues/6029)

- **例行任务交付目标隔离 (#6060)**：目前所有例行任务共享同一个交付目标（Slack/Email），设置一个影响全部。用户希望支持 per-routine 配置。  
  [Issue #6060](https://github.com/nearai/ironclaw/issues/6060)

- **MCP 注册存储（PR #5970）**：核心 PR 仍处于开放状态，旨在实现 per-user MCP 注册存储（T1），这是 MCP 注册栈的基础。若合入将允许用户独立管理 MCP 服务器。  
  [PR #5970](https://github.com/nearai/ironclaw/pull/5970)

- **统一扩展模型（PR #6061）**：8 个 PR 的滚合，将 Slack、GitHub 等扩展统一为单一模型，正在审查中。一旦合并，将大幅简化扩展管理。  
  [PR #6061](https://github.com/nearai/ironclaw/pull/6061)

以上功能请求与项目路线图（NEA-25 统一扩展、per-user 存储）高度吻合，预计在下一版本中部分落地。

## 7. 用户反馈摘要

从 Issues 评论中提炼的真实痛点：

- **状态不一致导致信任下降**：“助手说扩展已激活，但页面显示还需要点击‘激活’按钮”——#5948 用户对系统内部状态与 UI 状态不同步感到失望。
- **错误噪音掩盖真实问题**：“对话历史错误横幅一直挂着，即使后面的回复完全正常，我都不敢相信聊天是否还可用”——#6050 用户反馈。
- **工具调用失控**：“只是查个邮件再存到表格，却调用了 124 次工具，花了好几分钟”——#6046 用户对效率不满。
- **认证流程脆弱**：“重连 Slack 几次后，页面一直显示‘等待 Slack...’，只能彻底卸载重装”——#5882 用户经历。
- **安全顾虑**：“我有个安全问题，但找不到私下报告的地方，只能公开提 issue。”——#6000 用户表达了无奈。

总体而言，用户对 IronClaw 的能力（尤其是扩展集成）认可度较高，但对 **稳定性、错误反馈准确性和安全沟通渠道** 有明确改进诉求。

## 8. 待处理积压

以下 Issue/PR 已开放较长时间且未获得足够维护者关注：

- **#5640：集成测试缺口 — `hook_security_audit_sink` 在 harness 中始终为 None**  
  创建于 7 月 4 日，已开放 10 天，涉及生产级安全审计机制在测试中的缺失。  
  [Issue #5640](https://github.com/nearai/ironclaw/issues/5640)

- **#5741：`builtin.http.save` 在大响应时失败**  
  创建于 7 月 6 日，影响用户保存大型网页内容（如 ESPN 页面），当前无关闭迹象。  
  [Issue #5741](https://github.com/nearai/ironclaw/issues/5741)

- **PR #5598：发布版本**  
  创建于 7 月 3 日，11 天未合并，涉及 `ironclaw_common` 和 `ironclaw_skills` 的 API 破坏性变更，可能阻塞其他 PR 的发布决策。  
  [PR #5598](https://github.com/nearai/ironclaw/pull/5598)

- **PR #5936：v1 到 Reborn 离线迁移工作流**  
  创建于 7 月 10 日，高风险、大变更，目前仍开放且无最近活动。  
  [PR #5936](https://github.com/nearai/ironclaw/pull/5936)

建议维护者优先对 #5640 和 #5741 进行 triage，并推动版本发布 PR 的决策以解除后续开发阻塞。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，以下是基于您提供的 LobsterAI 项目数据生成的 2026-07-14 项目动态日报。

---

# LobsterAI 项目动态日报 | 2026-07-14

## 1. 今日速览

今日项目活跃度极高，共产出 **21 条 Pull Request**，其中 **19 条已被合并或关闭**，显示出强大的开发推进节奏。合并的 PR 主要集中在 **Windows 安装程序稳定性** 修复、**Mac 更新流程** 修复以及 **Cowork（协同工作）** 核心功能的完善（如通知系统升级、思考块流式传输）。值得注意的是，今日未产生新的公开 Issue，但有多条旧的 Issue 和 PR 被更新，表明社区维护工作在进行。整体来看，项目处于 **高强度迭代和稳定性加固** 阶段，针对多平台（特别是 Windows）的部署和用户体验优化是当前重点。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日共合并/关闭 19 个 PR，项目在以下方面取得显著进展，整体稳定性大幅提升：

- **安装与构建体验修复：**
    - **[重要]** 修复 Windows 安装程序因安全软件拦截而导致挂起的问题 (#2326, #2327)。现在安装程序会优先使用系统自带的 `tar.exe` 解压，并为 Electron 解压器设置超时保护；同时修复了 Electron 安装包内可执行文件未签名的问题，解决了杀毒软件误报。这直接解决了用户“安装卡死”的痛点。
    - **[新功能]** 新增了可选的 Windows Web 安装包目标 (#2323)，允许从 CDN 下载应用包，为网络化部署提供了基础。
    - **[修复]** 修复了 Mac 系统更新失败的问题 (#2321)，提升了 macOS 用户的更新体验。

- **Cowork 核心功能完善：**
    - **[新功能]** 升级了桌面通知系统 (#2318)，现在能显示等待中的权限请求和问题通知，并增加了前台通知模式，提升了用户感知。
    - **[新功能]** 实现了 OpenClaw 思考块的流式有序展示 (#2324)，在最终回答前展示思考过程，增强了 AI 决策的透明度。
    - **[新功能]** 重新设计了首页的快捷操作场景 (#2319)，将“教育学习”替换为更符合办公场景的“文档写作”。
    - **[修复]** 修复了多个 Cowork 相关的 Bug，包括：队列中的后续处理问题（#2315）、技能选择状态与会话独立管理（#1494）、输入过长错误分类过于宽泛（#1323）、以及引导式（Steer）后续消息的附件支持问题（#2300）。

- **Bug 与代码健康：**
    - **[修复]** 修复了定时任务（Cron Job）在启动时跳过计划的逻辑 (#2320)，确保不会错误地执行错过的任务。
    - **[修复]** 修复了 Windows 标题栏 Logo 在侧边栏收起时被压缩的问题 (#2316)。
    - **[修复]** 优化了文件卡片的显示效果 (#2322)。
    - **[修复]** 修复了 Cowork 中一个可能引起卡死的压缩重试维护问题 (#2289)。

## 4. 社区热点

今日没有活跃的 Issue 讨论。所有 PR 的评论数数据未提供，但从内容看，`#2327`（Windows 二进制签名）和 `#2326`（安装自愈修复）是解决用户实际部署难题的关键修复，预计会获得大量来自 Windows 用户的正面反馈。

> **值得关注的长期 PR：**
> *   [#1277: chore(deps-dev): bump the electron group](https://github.com/netease-youdao/LobsterAI/pull/1277): 这是一个来自 Dependabot 的自动化依赖更新 PR，尝试将 Electron 从 40.2.1 升级到 43.1.0。长期保持开放状态，可能因存在破坏性变更而等待人工审查。这表明项目正在谨慎评估重大依赖升级。

## 5. Bug 与稳定性

全天共修复 12 个以上 Bug，按严重程度排列如下：

| 严重程度 | 问题描述 | 修复 PR | 状态 |
| :--- | :--- | :--- | :--- |
| **严重** | Windows 安装程序被杀软拦截导致安装挂起，且无法恢复。 | [#2326](https://github.com/netease-youdao/LobsterAI/pull/2326), [#2327](https://github.com/netease-youdao/LobsterAI/pull/2327) | 已修复 |
| **高** | Mac 更新失败（hdiutil 失败）。 | [#2321](https://github.com/netease-youdao/LobsterAI/pull/2321) | 已修复 |
| **中** | Cowork 错误分类过于宽泛，导致短输入也显示“输入过长”的误导性 UI。 | [#1323](https://github.com/netease-youdao/LobsterAI/pull/1323) | 已合并 |
| **中** | 定时任务在启动时错误执行所有历史错过的任务。 | [#2320](https://github.com/netease-youdao/LobsterAI/pull/2320) | 已修复 |
| **低** | Windows 标题栏 Logo 在特定情况下被压缩。 | [#2316](https://github.com/netease-youdao/LobsterAI/pull/2316) | 已修复 |

整体来看，**Windows 平台的部署问题是今日修复的重中之重**，当前已得到解决。

## 6. 功能请求与路线图信号

- **Windows Web 安装程序**：PR [#2323](https://github.com/netease-youdao/LobsterAI/pull/2323) 新增了从 CDN 下载应用包的安装选项。这信号表明项目正在向更灵活的部署策略演进，可能将支持企业内部批量部署或简化初次下载体验。该特性通过环境变量 `LOBSTERAI_WEB_INSTALLER` 控制，是可选功能，可能为后续版本的企业版或轻量级部署方案做准备。

## 7. 用户反馈摘要

由于今日无新增 Issue，用户反馈主要来源于已合并 PR 的描述信息：

- **核心痛点 (Windows 用户)**：安全软件（如杀毒软件）导致安装进程挂起，这是最强烈的用户反馈信号。开发团队迅速响应并修复，解决了 `LobsterAI.exe` 未签名的问题。
- **使用场景与需求**：
    - **办公场景**：首页快捷操作从“教育学习”改为“文档写作”（PR #2319），表明项目正根据用户使用数据，将场景重心转向办公效率。
    - **AI 透明度**：流式展示 OpenClaw 的思考过程（PR #2324），响应了用户希望理解 AI 如何得出结论的需求。
    - **多任务处理**：多个 PR 针对 Cowork 的“后续处理”和“队列”进行优化（#2315, #2300），说明用户在 AI 生成内容的同时，有强烈的“排队”处理下一个任务的连续交互需求。

## 8. 待处理积压

以下 Issue/PR 长期未获响应或合并，建议维护者关注：

- **PR #1277 [OPEN]**: `chore(deps-dev): bump the electron group across 1 directory with 2 updates`。此 PR 意图将 Electron 从 v40 升级到 v43，跨度较大，可能包含重大破坏性变更。自 4 月 2 日创建以来，虽多次更新但未合并。建议维护者评估升级风险，考虑分步骤升级，或关闭该 PR 并手动处理依赖更新。
    - 链接：[#1277](https://github.com/netease-youdao/LobsterAI/pull/1277)

- **PR #1323 [OPEN] [stale]**: `fix(cowork): narrow input-too-long error classification (#1298)`。此 PR 修复了一个重要的用户侧 Bug（误导性的错误提示），已于今日被标记并合并，已从积压列表中解决。

---
*报告生成时间：2026-07-14*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 | 2026-07-14

## 1. 今日速览
- 过去24小时内，Moltis 无新增 Issue 和 PR 合并，整体活跃度较低。
- 唯一活跃的 PR #1147 仍在待合并状态，涉及 CalDAV 客户端的时间范围查询修复，项目在稳定性方面有所推进。
- 无新版本发布，也无社区讨论热点，项目当前处于低活动窗口期。

## 2. 版本发布
无新版本发布。

## 3. 项目进展
- **未合并/关闭的重要 PR**  
  - **PR #1147**（[链接](https://github.com/moltis-org/moltis/pull/1147)）：`fix(caldav): honor time range in list_events via server-side calendar query`  
    该 PR 修复了 `CalDavClient::list_events` 方法中 `_range` 参数未被实际使用的问题（参数被绑定为 `_range` 但从未传递到查询中），导致 `start`/`end` 参数无效，客户端始终拉取日历的全部资源。修复后，`list_events` 会向 CalDAV 服务器发送带时间范围的查询请求，使文档描述与实际行为一致。  
    **项目意义**：提升 CalDAV 集成工具的准确性和效率，避免不必要的全量数据拉取，对依赖日历事件的用户（如日程管理和自动化任务）有直接正面影响。

## 4. 社区热点
无。今日无 Issue 被讨论，PR #1147 评论数为 `undefined`（实际无评论），点赞数为 0，未形成讨论热点。

## 5. Bug 与稳定性
- **待修复 Bug**：无新报告的 Bug。
- **已存在但未关闭的稳定性问题**：PR #1147 所修复的 `list_events` 时间范围忽略问题属于隐蔽性 Bug，影响所有使用 CalDAV 日历功能的用户。该 Bug 在 PR 中已给出修复代码，但尚未合并（状态为 OPEN）。建议维护者尽快评审合并，以消除该回归隐患。

## 6. 功能请求与路线图信号
无。过去24小时内无新功能请求提交。PR #1147 属于缺陷修复，非新功能。结合历史数据，CalDAV 相关的改进可能持续被关注，但暂无明确路线图信号。

## 7. 用户反馈摘要
- **PR #1147 背景分析**：该 PR 作者 `thoscut` 在摘要中指出“文档声称支持时间范围，但实际代码未使用 `_range` 参数”，表明用户（或贡献者）在试用过程中发现了文档与实现的不一致。这反映了用户对接口行为文档准确性的重视，以及期望 API 能严格遵循文档描述。当前无更多用户评论可提炼。

## 8. 待处理积压
- **PR #1147**（[链接](https://github.com/moltis-org/moltis/pull/1147)）：自 2026-07-11 创建，已开放 3 天，未收到任何评论或审核。虽然 PR 本身代码改动较小（仅涉及将 `_range` 参数正确传递给 CalDAV 查询），但长期未合并可能导致其他贡献者重复修复或用户继续使用有缺陷的版本。建议项目维护者及时响应。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为一名 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为您生成的 CoPaw 项目动态日报。

---

# 🤖 CoPaw 项目动态日报 | 2026-07-14

## 1. 今日速览

今日 CoPaw 项目社区高度活跃，共产生 100 条 Issue 和 PR 更新，并发布了新的补丁版本 v2.0.0.post1，显示开发团队正在集中精力解决 v2.0.0 大版本发布后出现的系列稳定性问题。社区反馈的核心痛点集中在**上下文压缩导致工具调用出错**、**工具权限与沙箱机制**以及**功能回归**上。尽管面临挑战，项目维护者对用户反馈的响应速度较快，已有多个修复 PR 被合并或提出，项目健康状况总体稳定，正处于关键的“版本打磨与修复期”。

## 2. 版本发布

- **v2.0.0.post1**：这是一个针对 v2.0.0 的紧急修复版本。
  - **主要修复内容**：
    1.  修复了在对话中产生 `MODEL_EXECUTION_ERROR` 的问题，该问题是由于后台工具调用（offload）生成的提示消息（hint message）格式错误导致的（#6007, #6011）。
    2.  修复了在提供者搜索输入框上的浏览器自动填充问题（#6011）。
  - **破坏性变更**：无。
  - **迁移注意事项**：建议所有 v2.0.0 用户尽快升级至此版本，以获得更稳定的对话体验。
  - **链接**: [v2.0.0.post1](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.0.0.post1)

## 3. 项目进展

今日项目在修复核心 Bug 和优化内部架构方面取得了显著进展，多个重要 PR 被合并或关闭。这些工作直接回应了社区近期反馈的诸多关键问题。

- **工具调用与上下文压缩修复**:
  - **[#6058] [CLOSED]** `fix(tool_calls): flatten offload hint + temporarily disable broken offload mechanism`: 临时禁用了有问题的后台任务卸载（offload）机制，并修正了相关的提示消息格式，以解决导致 API 400 错误的核心问题。
  - **[#6052] [CLOSED]** `fix(hint): flatten background tool hint to plain assistant message`: 修复了后台工具结果作为孤立块导致的格式化错误，与 #6058 协同解决了同类问题。
  - **[#6054] [CLOSED]** `feat(governance): relax no-finding fallback and add global sandbox switch`: 改进了治理策略，减少了低价值的审批提示，并添加了全局沙箱执行开关。
- **UI/UX 与功能修复**:
  - **[#6045] [CLOSED]** `fix(console): clear message queue when a session is deleted`: 修复了删除会话后消息队列未清理的问题，这是用户反馈的“消息队列功能没有了”的根本原因之一。
  - **[#6044] [CLOSED]** `fix(plugins): bridge register_tool to runtime ToolRegistry pipeline`: 修复了通过插件 API 注册的工具在运行时不可见的问题。
- **CLI 与测试优化**:
  - **[#6061] [CLOSED]** `test(plugins): add unit tests for Ponytail Quality plugin backend`: 为“懒惰的高级开发者模式”（Ponytail）插件增加了单元测试，提升了代码质量。
  - **[#6065] [OPEN]** `fix: remove dead imports, dead module, and wrong asyncio mark`: 清理了无效代码和错误标记，提升了项目健康度。

## 4. 社区热点

今日讨论最热烈的话题集中在 **v2.0.0 版本的稳定性大幅下降**，社区情绪以抱怨和提出紧急 Bug 为主，尤其是在对比旧版本 v1.x 及其他竞品后。

1.  **[#6013] [CLOSED]** `V2.0.0的版本,越来越不稳定了,还不如V1.xxx的版本. 稳定性方面,远远不如腾讯的workbuddy` **【最热反馈】**
    - **分析**: 这条 Issue 虽然简短，但获得了 5 条评论，代表了大量普通用户的沮丧情绪。直接拿竞品对比，表明稳定性问题已经影响到用户的根本信任。这并非技术 Bug，而是用户体验的警报。
    - **链接**: [Issue #6013](https://github.com/agentscope-ai/QwenPaw/issues/6013)

2.  **[#5996] [CLOSED]** `[Bug]: 2.0.0对话时会产生MODEL_EXECUTION_ERROR` **【技术讨论焦点】**
    - **分析**: 评论数高达 10 条，是今日讨论最深入的技术问题。用户精准定位了问题根源在于 `make_offload_hint_msg()` 函数生成的非法消息格式。这直接导致 OpenAI API 返回 400 错误。社区和开发者围绕此问题进行了深度技术分析，并迅速在 v2.0.0.post1 中修复。
    - **链接**: [Issue #5996](https://github.com/agentscope-ai/QwenPaw/issues/5996)

3.  **[#5961] [OPEN]** `[Bug]: v2.0.0版本循环执行的问题`
    - **分析**: 用户反映智能体在搭配某些模型（如 qwen3.7-plus）时陷入“写入-删除-写入-删除”的死循环，导致任务无法完成。这表明智能体的决策循环逻辑可能存在问题，与某些模型的特性不兼容。
    - **链接**: [Issue #5961](https://github.com/agentscope-ai/QwenPaw/issues/5961)

## 5. Bug 与稳定性

今日报告的 Bug 数量较多，且多为 v2.0.0 版本的回归或新引入问题，严重程度普遍较高。幸运的是，大部分核心问题已有对应的修复 PR。

| 严重程度 | 问题标题 | Issue 链接 | 是否有 Fix PR | 状态影响 |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | **上下文压缩破坏 tool_call/tool_result 配对 | ** [#5986], [#5960], [#5962] | 是 ([#5953]) | 导致多轮对话后 API 400 错误，会话卡死。 |
| **严重** | **后台工具卸载(Offload)机制失效，导致孤儿 ToolResultBlock** | [#5996] | 是 ([#6058], [#6052]) | 导致 `MODEL_EXECUTION_ERROR`，影响所有长时间任务。 |
| **严重** | **智能体无限循环执行** | [#5961] | 否 | 导致任务无法完成，资源被大量消耗。 |
| **高** | **MCP 工具权限设置(允许/拒绝)失效** | [#5947] | 否 | 严重的安全功能失效，用户无法控制智能体行为。 |
| **高** | **升级后功能缺失 (SSH Offline, Profiles 返回 404)** | [#5980] | 否 | 影响依赖高级功能的用户工作流。 |
| **高** | **Dream 功能报错 (模块导入错误)** | [#6024], [#5965] | 否 (`agentscope` 路径) | 自动记忆优化功能完全失效。 |
| **中** | **Shell 命令超时硬编码为 60s** | [#5963] | 否 | 用户配置被忽略，导致长时间命令被强制终止。 |
| **中** | **TUI 点击流式输出时崩溃** | [#6008] | 是 ([#6069]) | CLI 用户界面不稳定。 |
| **中** | **审批系统路由错误/OFF 配置失效** | [#6020] | 否 | 审批流程混乱，安全设置无效。 |
| **低** | 工具列表只显示20条/ Dream 依赖缺失 | [#5788], [#6012] | 否 | 影响界面的可用性和功能的完整性。 |

[#5986]: https://github.com/agentscope-ai/QwenPaw/issues/5986
[#5960]: https://github.com/agentscope-ai/QwenPaw/issues/5960
[#5962]: https://github.com/agentscope-ai/QwenPaw/issues/5962
[#5953]: https://github.com/agentscope-ai/QwenPaw/pull/5953

## 6. 功能请求与路线图信号

尽管当前以修复为主，但社区也提出了一些新的功能需求，部分已经得到开发者的关注和响应。

1.  **免认证主机白名单支持 CIDR 段** ([#6048]): 用户希望白名单配置能支持 IP 段，而非仅单一 IP，以适配更灵活的企业网络环境。这反映了用户对自动化运维场景的深度需求。
2.  **审批系统优化** ([#6020]): 用户要求审批请求应推送至发起渠道（如钉钉），而非固定显示在桌面端。同时要求关闭审批后，所有内置工具都应遵守该设置。这表明当前审批模式在跨设备、跨渠道体验上存在短板。
3.  **改进权限模式** ([#5954]): 用户对现有的“自动/智能/关闭”权限模式提出改进建议，希望引入“工具白名单”模式，允许用户一次性授权或永久授权，以减少重复审批带来的操作负担。这暗示着需要更精细、更智能的权限控制策略。
4.  **允许只读工具豁免“死循环”检测** ([PR #6041]): 社区贡献者已提交 PR 来解决此问题，表明项目可能会采纳更智能的循环检测策略，而非一刀切地干预只读操作。

这些功能请求普遍围绕着 **精细化控制**、**跨终端一致性** 和 **企业级运维** 三个方向，为 CoPaw 的后续迭代提供了清晰的用户视角。

## 7. 用户反馈摘要

从今日的社区讨论中，可以清晰听到两类声音：

- **失望与抱怨（v2.0.0 升级用户体验差）**:
    - “稳定性方面，远远不如腾讯的workbuddy” - **用户对核心体验的评价非常直接**。
    - “V2.0.0 版本循环执行的问题...智能体总会反反复复的写入、删除、写入、删除” - **用户使用体验极差，任务无法完成**。
    - “升级到2.0版后出现了很多意想不到的情况...会自动添油加醋的增加内容...频繁出现错误” - **v2.0 的升级对老用户造成了明显的负面冲击**。
    - “更新到2.0版本后出现错误提示 ‘Is a directory: '/app/working/workspaces/default/.mcp'” - **升级之路充满障碍，基础环境适配出现问题**。

- **专业与技术分析（深度用户/开发者）**:
    - “Context compression breaks tool_call / tool_result pairing” - **用户不仅报错，还进行了深度归因分析**。
    - “Background offload kills subprocess immediately — LLM-provided timeout is silently ignored” - **开发者社区指出了后台任务调度机制的严重缺陷**。
    - “Plugin HTTP routes lost after workspace hot-reload” - **高级用户遇到了热重载场景下的状态管理 Bug**。

**总结**：普通用户对 v2.0 版本的稳定性感到极度不满，认为是一次体验上的倒退。而深度用户和技术贡献者则能精确诊断出底层架构问题，并通过提交高质量的 PR 来推动项目修复。两者结合，一方面暴露了版本重大更新可能带来的风险，另一方面也展现了开源社区强大的自我修复能力。

## 8. 待处理积压

以下 Issue 和 PR 由于长期未响应或处于停滞状态，需要项目维护者关注：

1.  **[#5872] [OPEN] 2026-07-09** `[Bug]: Docker 容器内 browser_use 启动失败 —— dbus 连接错误导致 Chromium 退出`
    - *说明*: 一个复现步骤清晰，影响 Docker 部署用户的核心问题，已存在 5 天且无官方回复。涉及浏览器自动化工具，属于重要功能。
    - **链接**: [Issue #5872](https://github.com/agentscope-ai/QwenPaw/issues/5872)

2.  **[#5069] [OPEN] 2026-06-10** `feat(agents): add visual model fallback for text-only primary models`
    - *说明*: 一个非常有价值的特性（视觉模型回退），已存在超过一个月，仍有 3 条新评论，但无合并进展。这表明该功能可能处于长期审核或开发阻塞状态。
    - **链接**: [PR #5069](https://github.com/agentscope-ai/QwenPaw/pull/5069)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为 ZeroClaw 项目生成的 **2026-07-14** 项目动态日报。

---

# ZeroClaw 项目日报 | 2026-07-14

## 1. 今日速览

ZeroClaw 在经历了一波密集的版本收尾工作后，今日社区活跃度极高，但也显露出严重的 PR 积压问题。**过去 24 小时内有 50 个 PR 处于待合并状态，而仅有 3 个被处理**，这反映了项目在代码评审环节存在明显的瓶颈。与此同时，随着 v0.8.3 版本所有子跟踪器（child tracker）关闭，项目已正式进入该版本的最终发布验证与关闭阶段。新版 RFC 和功能性 Bug 报告同步涌现，表明社区在期待新版本的同时，也对当前代码的稳定性和合规性提出了更高要求。**项目健康度评估：活跃但高负载，评审流程亟需优化。**

## 2. 版本发布

*无版本发布。*

## 3. 项目进展

今日项目取得了关键的版本里程碑推进，同时对多个持续已久的问题进行了修复与覆盖。

-   **v0.8.3 里程碑收尾**：核心发布索引跟踪器 #7320 及其 6 个子跟踪器（涵盖运行时、渠道、提供商、配置、Gateway 等）均已关闭。这表明 v0.8.3 的功能开发工作已全部冻结，项目正为最终发布做最后冲刺。([#7320](https://github.com/zeroclaw-labs/zeroclaw/issues/7320), [#8073](https://github.com/zeroclaw-labs/zeroclaw/issues/8073), [#8071](https://github.com/zeroclaw-labs/zeroclaw/issues/8071), [#8360](https://github.com/zeroclaw-labs/zeroclaw/issues/8360) 等)
-   **测试覆盖度提升**：通过 #7694、#7693、#7690、#7688 等一系列 PR 的合并/关闭，项目在内存存储、ZeroCode 安全、提供商选项及运行时钩子等方面的确定性测试覆盖率得到了显著提升。([#7694](https://github.com/zeroclaw-labs/zeroclaw/issues/7694), [#7693](https://github.com/zeroclaw-labs/zeroclaw/issues/7693))
-   **关键 Bug 修复**：PR #8777 修复了 ZeroCode 前端代码块复制时包含 markdown 围栏（fence）的问题，提升了开发者体验。PR #8562 修复了 cron 测试中因广播订阅者污染导致的偶发失败，增强了测试稳定性。
-   **项目文档与维护**：新的贡献指南 PR（#9012、#9050）正在制定中，旨在明确维护期望并压缩 AGENTS.md 文件，以降低社区的参与门槛。([#9012](https://github.com/zeroclaw-labs/zeroclaw/pull/9012), [#9050](https://github.com/zeroclaw-labs/zeroclaw/pull/9050))

## 4. 社区热点

今日讨论的焦点集中在项目的长远架构和核心交互体验上。

-   **RFC: 工作流与板自动化（#6808，14条评论）**：这条历史性的 RFC 仍在持续讨论，旨在通过标签和自动化降低维护者的手动管理工作量。它代表了社区对更智能、更自动化的项目治理的强烈诉求。
    [👉 参与讨论](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)
-   **RFC: 轻量化核心（#6165，9条评论）**：关于将长期尾（long-tail）集成从核心移出至技能和 MCP 服务器的讨论异常火热。这反映了社区对于 ZeroClaw 核心保持轻量、灵活和易于维护的期待。
    [👉 参与讨论](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)
-   **本地优先模型模式（#5287，5条评论）**：这条 RFC 收获了 2 个 👍，社区强烈希望 ZeroClaw 能为小模型提供更紧凑、无泄露的提示模式。这表明本地化、隐私优先的场景是用户的核心关注点之一。
    [👉 参与讨论](https://github.com/zeroclaw-labs/zeroclaw/issues/5287)

## 5. Bug 与稳定性

今日报告的 Bug 涵盖了从阻断工作流到体验降级的多个方面，严重程度较高。

-   **S1 - 工作流阻断**：
    -   **Docker Compose 网关端口问题（#9035）**：用户报告在 Docker 场景下，即使端口发布成功，网关也无法访问，显示“Connection refused”。此问题严重阻碍了容器的部署工作流。状态：**已接受**。
        [🔗 报告详情](https://github.com/zeroclaw-labs/zeroclaw/issues/9035)
-   **S2 - 功能降级**：
    -   **models_cache.json 文件永久缺失（#9046）**：`/model` 命令因依赖一个从未被写入的文件而永久失效。用户被提示运行 `run zeroclaw models refresh`，但此操作并未解决根本问题，形成死锁。状态：**新开**。
        [🔗 报告详情](https://github.com/zeroclaw-labs/zeroclaw/issues/9046)
    -   **Windows 下 Ctrl+C 强制退出（#9028）**：在 Windows 终端中按下 Ctrl+C 会导致 ZeroClaw 进程强制退出并返回错误代码，而非优雅终止。状态：**已接受**。
        [🔗 报告详情](https://github.com/zeroclaw-labs/zeroclaw/issues/9028)
    -   **提供商终端标记泄漏（#9006）**：OpenRouter 提供商的 `<eom>` 标记被作为普通文本显示给用户。该问题已有对应的 fix PR #9037。
        [🔗 fix PR #9037](https://github.com/zeroclaw-labs/zeroclaw/pull/9037)
-   **S3 - 次要问题**：
    -   **渠道运行时命令绕过本地化（#6548）**：一些用户可见的回复仍是硬编码英语，无多语言支持。
        [🔗 报告详情](https://github.com/zeroclaw-labs/zeroclaw/issues/6548)
    -   **Rustdoc 测试因重复主题标志失败（#8847）**：影响 CI 测试门禁。
        [🔗 报告详情](https://github.com/zeroclaw-labs/zeroclaw/issues/8847)

## 6. 功能请求与路线图信号

社区的呼声指向了两个主要方向：**精细化配置**与**更好的集成体验**。

-   **SOP 功能推进**：跟踪器 #8288 正协调将 ZeroClaw 的标准操作程序（SOP）能力提升至满级五级（5/5），这是未来版本的核心路线图之一。
-   **集成精细化**：
    -   **Slack Events API 支持（#9022）**：用户请求支持基于 HTTP 请求的 Slack Events API，以适配无服务器（scale-to-zero）部署架构，这是对云端部署场景的扩展。
    -   **渠道配对 UI（#8998）**：建议在仪表盘上为频道绑定码（pairing code）提供专门的界面，而不是仅在日志中显示，以改善用户体验。
    -   **Google Workspace 工具字母大小写兼容（#9044）**：要求扩展 `google_workspace` 工具对方法名的校验规则，以兼容官方 CLI 的驼峰命名。
-   **本地化与国际化**：对 #6548 的持续关注以及 PR #9049 的提出，表明社区不仅关心语言包，更关注如授权拒绝等关键交互信息的完整本地化。

## 7. 用户反馈摘要

-   **失望与挫折**：Docker 用户发现网关无法访问，且官方 `models_cache` 文件生成逻辑似乎存在严重缺陷，导致标准功能失效。这些是影响新用户留存率的负面体验。
-   **明确的配置需求**：用户对 cron 作业的输出格式提出了明确期望（#8438），不希望总是被包裹在冗长的元数据中。这表明高级用户正在将 ZeroClaw 作为基础设施的一部分调用。
-   **对稳定性的渴望**：在 Windows 下无法正常退出、以及开源提供商连接中断带乱码等 Bug，表明用户对运行时的可靠性和容错能力有很高的期待。

## 8. 待处理积压

当前项目最大的积压并非单个 Issue，而是大规模 PR 积压。

-   **PR 评审瓶颈**：**47 个 PR 处于待合并状态**，这构成了项目的最大风险。许多早期提交的 PR（如 #8353、#8356）已打上 `needs-author-action` 标签，但仍有大量功能性和修复性 PR（如 #8438、#8779、#8781）等待维护者审核。建议维护团队优先解决此瓶颈，否则新版本迭代速度将严重受阻，并极大挫伤贡献者的积极性。
    -   **重点关注**：PR #8898（修复跨会话内存召回）和 PR #8927（修复兼容提供商对  `strip_think_tags` 的移除）涉及核心运行时和模型兼容性，需要优先处理。
    -   **沉睡 PR**：PR #8656（修复微信 Markdown 转换）和 PR #8443（添加 Matrix 单消息草案）因长期未获响应而标记为 `needs-author-action`，应尽快跟进。

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*