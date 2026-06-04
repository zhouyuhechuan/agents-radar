# OpenClaw 生态日报 2026-06-04

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-04 02:55 UTC

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

# OpenClaw 项目动态日报 — 2026-06-04

## 1. 今日速览

过去24小时项目保持极高活跃度：共处理 **500 条 Issue**（新开/活跃 383，关闭 117）和 **500 条 PR**（待合并 406，合并/关闭 94）。发布 3 个新版本（v2026.6.2-beta.1、v2026.6.1、v2026.6.1-beta.3），核心改进集中在插件安装策略向 Operator 策略迁移、Agent 与 CLI 运行时对中断调用与媒体交付的恢复能力增强。社区讨论焦点继续围绕 **会话/转录的 SQLite 迁移**、**心跳隔离模式回归** 以及 **Windows 聊天 UI 吞输入** 等稳定性痛点，整体项目健康度处于“高强度迭代”状态。

## 2. 版本发布

- **v2026.6.2-beta.1**  
  Highlights：插件和技能安装改用 **operator install policy**，替代旧的危险代码扫描路径；同时为包、归档、源码、上传、市场等安装方式提供了更清晰的 doctor、CLI、ClawHub 和故障排查界面（#89516）。值得注意的是，此变更可能影响依赖旧扫描路径的自定义安装流程，建议测试升级后 `openclaw install` 行为。

- **v2026.6.1**  
  Highlights：Agent 和 CLI 驱动的运行时更干净地从 **中断工具调用、过期会话绑定、压缩交接和媒体交付重试** 中恢复（#88129、#88136、#88141、#88162、#88182）。多渠道（Telegram、WhatsApp、iMessage、Slack）及移动端交付更稳定。修复了多个 session 状态相关的边缘情况。

- **v2026.6.1-beta.3**  
  与 v2026.6.1 亮点相同，属于同一批修复的 beta 前序版本。

**迁移注意事项**：v2026.6.2-beta.1 中的 operator install policy 可能需要对现有自定义插件安装逻辑进行调整；建议关注 [Release Notes](https://github.com/openclaw/openclaw/releases/tag/v2026.6.2-beta.1) 中的详细说明。

## 3. 项目进展

过去24小时共有 **94 个 PR 被合并或关闭**，以下为其中代表性的合并项：

- **#90127** (`feat(control-plane): add tranche A/B registry and CI gate`)  
  新增控制平面 Tranche A+B 骨架，包含合约、模式、注册表、队列、报告、构件、仪表板和分类账，并添加了 CI 门禁。属于基础设施层面的重要推进。  
  [PR #90127](https://github.com/openclaw/openclaw/pull/90127)

- **#90131** (`fix(subagent-announce): durable-queue fallback when direct handoff is pending`)  
  修复子 agent 完成通知在直接交接挂起时无备份队列的问题，改为退回到持久队列，避免通知丢失。  
  [PR #90131](https://github.com/openclaw/openclaw/pull/90131)

- **#88020** (Issue 对应的修复 PR 已关闭)  
  针对 `REPLAY_INVALID_RE` 未识别 Anthropic “Invalid signature in thinking block” 的问题，已合入修复，将硬 session 失败改为可恢复重试。  
  [Issue #88020](https://github.com/openclaw/openclaw/issues/88020) | 关联 PR 已关闭

此外，多个涉及 TUI、QQ 频道、WhatsApp 重启、安装脚本健壮性的小型修复也已合并，提升了具体场景的稳定性。

## 4. 社区热点

过去24小时内讨论最活跃的 Issue 和 PR 如下：

| 标题 | 类型 | 评论数 | 核心诉求 |
|------|------|--------|----------|
| [#88838 Track core session/transcript SQLite migration via accessor seam](https://github.com/openclaw/openclaw/issues/88838) | Issue | 17 | 社区高度关注会话/转录运行时状态向 SQLite 的渐进式迁移，希望通过 branch-by-abstraction 避免大改风险，讨论了 seam 设计细节。 |
| [#65161 Heartbeat isolated mode: cadence stalls...](https://github.com/openclaw/openclaw/issues/65161) | Issue | 14 | 持续的热点：心跳隔离模式存在多项回归，包括心跳节奏在首次脉冲后停止、`heartbeat last` 误标执行事件等，用户急需 fix。 |
| [#67035 [Bug]: 2026.4.14 Windows chat UI regression...](https://github.com/openclaw/openclaw/issues/67035) | Issue | 14 | Windows 用户强烈反馈 WebChat UI 输入文本被吞、流式回复不可见，严重影响日常使用，社区期待尽快修复。 |
| [#88312 [Regression] Codex app-server turn-completion stall...](https://github.com/openclaw/openclaw/issues/88312) | Issue | 12 | 回归问题，之前已修复的 Codex 回合完成卡死再次出现，用户感到沮丧，已确认为 v2026.5.27 引入。 |
| [#67288 amazon-bedrock-mantle lacks config.discovery.enabled gate](https://github.com/openclaw/openclaw/issues/67288) | Issue | 11 | 用户提出 Bedrock 插件在每次请求都进行不必要的 IAM 发现，希望增加配置开关，获得较多共鸣。 |

这些讨论表明社区当前最关切 **稳定性回归** 与 **核心架构迁移（SQLite）** 两大方向。

## 5. Bug 与稳定性

按严重程度排列今日报告的 Bug/回归问题：

| 严重等级 | Issue | 摘要 | 是否有 fix PR |
|----------|-------|------|---------------|
| P1 (Platinum Hermit) | [#88312 Codex 回合完成卡死回归](https://github.com/openclaw/openclaw/issues/88312) | v2026.5.27 引入，与 #84076 相同模式，目前无直接 fix PR。 | 未关联 |
| P1 (Platinum Hermit) | [#63216 同一 session 反复硬重置](https://github.com/openclaw/openclaw/issues/63216) | 高 reserveTokensFloor 下仍发生上下文溢出循环，已标记 linked-pr-open。 | 关联 PR 开放中 |
| P1 (Platinum Hermit) | [#86214 Codex 客户端在图像/工具请求中途关闭](https://github.com/openclaw/openclaw/issues/86214) | 与大型 logs_2.sqlite 有关，需要 live repro。 | 无 |
| P1 (Diamond Lobster) | [#66561 openai-codex SSE 流本地中止](https://github.com/openclaw/openclaw/issues/66561) | 上游已开始返回但被本地误判为超时。 | 无 |
| P1 (Diamond Lobster) | [#68113 Mattermost 斜杠命令 503](https://github.com/openclaw/openclaw/issues/68113) | v2026.4.15 回归，用户等待修复。 | 无 |
| P1 (Gold Shrimp) | [#85030 MCP 工具未注入子 agent 会话](https://github.com/openclaw/openclaw/issues/85030) | 配置忽略，子 agent 只能使用内置工具。 | 无 |
| P1 (Platinum Hermit) | [#68751 session-memory 原始会话作为当前输入重放](https://github.com/openclaw/openclaw/issues/68751) | 安全风险：旧的用户命令会在 /reset 后自动重新执行。 | 无 |

此外，#67363（安全：memory-core 未蒸馏的日志提升至 MEMORY.md）和 #65624（Mattermost 回调 URL 明文暴露令牌）均标记了 `needs-security-review`，需尽快处理。

## 6. 功能请求与路线图信号

以下功能请求获得较多关注，且部分已有对应 PR 动工：

- **#72741 标准外部安全/护栏检查接口**：社区希望提供统一接口集成第三方安全检查。目前无直接 PR，但 #90003 (policy: exec approvals artifact) 部分涉及策略证据收集，方向一致。
- **#63990 多索引 embedding 内存（模型感知故障转移）**：支持多 embedding provider 避免单点故障。已有 PR **#88504** (multi-slot memory role architecture) 正在推进，可能纳入下一版本。
- **#64438 远程 Reranker 端点支持**：类似 embedding 的远程 reranker 集成。目前无对应 PR，但属于内存搜索增强方向。
- **#67000 Agent 会话预热/重用**：减少每次 `runEmbeddedPiAgent` 的冷启动开销。可能在下个性能优化阶段考虑。
- **#76159 为 cron 任务增加 acceptSilentStop 标志**：允许无输出的任务不被标记为错误。社区呼声较高。

路线图信号：**#88504 的 multi-slot memory 架构** 表明项目正在重构内存插件体系，未来可能支持多角色 slot。

## 7. 用户反馈摘要

从 Issue 评论中提炼的真实用户声音：

- **Windows UI 体验差**（#67035）：“升级到 2026.4.14 后，Web 聊天 UI 完全无法使用，输入的文字不显示，回复也看不见，只能刷新页面。TUI 正常，这严重影响团队协作。” —— 表明前端渲染层有严重缺陷。
- **Codex 回归反复**（#88312）：“同一问题在 5.27 再次出现，之前 5.26 是好的。这已经是第二次修复后被重新引入，希望有自动回归测试。” —— 用户对回归质量控制提出质疑。
- **Session 上下文膨胀**（#67419）：“每次对话 bootstraps 文件浪费 20-30% token，如果是长对话，很快就会触发 compaction。” —— 期望优化上下文骨架注入逻辑。
- **插件/工具配置复杂**（#85030）：“MCP 工具怎么配置都注入不到子 agent，文档说的方法都不生效。” —— 配置系统的易用性需改进。
- **备份因 session 清理失败**（#67417）：“`openclaw backup create` 因为备份中途 session 被删除而 ENOENT，这种竞态不该存在。”

总体上，用户对 **高可用性、配置一致性、UI 可靠性** 的期望较高，同时对回归 bug 容忍度下降。

## 8. 待处理积压

以下为创建较久、仍未得到足够响应的关键 Issue/PR，建议维护团队优先关注：

| 项目 | 创建日期 | 上次更新 | 摘要 | 状态 |
|------|----------|----------|------|------|
| [#65161 Heartbeat isolated mode 多项回归](https://github.com/openclaw/openclaw/issues/65161) | 2026-04-12 | 2026-06-03 | 心跳节奏停止、`heartbeat last` 误标、重度 heartbeatState 等，标记 `stale`。 | 开放，无明确 fix PR |
| [#64500 全局断路器按工具而非配对阻塞](https://github.com/openclaw/openclaw/issues/64500) | 2026-04-10 | 2026-06-03 | Ping-pong 循环逃逸断路器，标记 `stale`。 | 开放，无进展 |
| [#63612 主 session 因 compaction token 估计崩溃](https://github.com/openclaw/openclaw/issues/63612) | 2026-04-09 | 2026-06-03 | 长时间运行后 `Cannot read properties of undefined`，标记 `stale, linked-pr-open`，但 PR 进展缓慢。 | 开放，关联 PR |
| [#63216 session 硬重置循环](https://github.com/openclaw/openclaw/issues/63216) | 2026-04-08 | 2026-06-03 | 同上，P1 且社区讨论多，但维护者回复不足。 | 开放，需 maintainer review |
| [#67000 Agent 预热重用](https://github.com/openclaw/openclaw/issues/67000) | 2026-04-15 | 2026-06-03 | 功能请求，无维护者确认是否纳入路线图。 | 开放，需 product decision |

这些积压问题多与 **session/状态管理** 和 **心跳机制** 相关，属于核心稳定性领域，建议尽快分配资源处理。

---

*本日报由 AI 分析师基于 GitHub 公开数据自动生成，仅供参考。*

---

## 横向生态对比

好的，作为AI智能体与个人AI助手开源生态的资深技术分析师，以下是我基于您提供的2026-06-04各项目动态摘要，为您生成的一份横向对比分析报告。

---

### **个人AI助手/自主智能体开源生态横向分析报告 (2026-06-04)**

#### **1. 生态全景**

2026年6月初，个人AI助手与自主智能体开源生态呈现出 **“分化演进、共识增强”** 的态势。一方面，以OpenClaw为代表的大型全能型项目进入高强度迭代期，积极重构核心架构（如SQLite迁移、Operator策略）以应对规模化挑战；另一方面，以NanoBot、CoPaw为代表的中型项目专注于打磨特定场景的稳定性（如MCP连接、长任务可靠性）与渠道体验。生态整体正从“狂飙突进的功能竞赛”向 **“工程化、稳定化与安全化”** 的深水区过渡。值得注意的是，**会话状态管理、工具调用鲁棒性、以及安全架构升级**成为跨越多个项目共识的三大核心痛点，预示着下一阶段竞争焦点将从“能做”转向“做好”。

#### **2. 各项目活跃度对比**

| 项目名称 | Issues (新开/活跃) | PRs (新开/活跃) | 新版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 (383/117) | 500 (406/94) | 3 | **高强度迭代**：社区极活跃，但合并效率(18.8%)和大量P1 Bug表明处于功能攻坚与稳定性的平衡期。 |
| **NanoBot** | 33 (26/7) | 34 (16/18) | 0 | **稳健前进**：合并效率高(52.9%)，核心维护者积极修复Bug，但多项长期功能请求积压。 |
| **Hermes Agent** | 50 (43/7) | 50 (43/7) | 0 | **健康度承压**：社区提交多但合并效率低(14.0%)，Windows兼容性与安全漏洞问题突出。 |
| **PicoClaw** | 4 (4/0) | 10 (8/2) | 0 | **中等活跃**：无新版本，但合入了关键安全与Bug修复，核心栈Bug修复PR积压需关注。 |
| **NanoClaw** | 1 (1/0) | 9 (9/0) | 0 | **高产出蓄力**：无新版本和合入，但大量高质量PR待审核，社区贡献活跃但积压风险高。 |
| **NullClaw** | 0 | 1 (1/0) | 0 | **静默期**：仅1个PR待合入，核心团队可能在幕后开发，社区讨论几近于无。 |
| **IronClaw** | 27 (19/8) | 50 (21/29) | 1 | **冲刺阶段**：合并效率高(58.0%)，开发聚焦于“Reborn”架构的收尾，社区反馈活跃。 |
| **LobsterAI** | 1 (1/0) | 14 (2/14) | 1 | **高效交付**：合入速度快，版本迭代频繁，聚焦于cowork与MCP模块的完善。 |
| **TinyClaw** | - | - | - | **无活动**：过去24小时无任何动态，项目疑似暂停。 |
| **Moltis** | 9 (0/9) | 3 (3/0) | 2 | **高修复、低交付**：大量Bug关闭，发布新版本，但关键修复PR待合并，交付节奏待加速。 |
| **CoPaw** | 44 (22/22) | 49 (28/21) | 0 | **高频迭代**：社区贡献活跃，Bug修复与功能开发并行，但部分严重Bug（如ChromaDB崩溃）长期未解。 |
| **ZeptoClaw** | 0 | 16 (16/0) | 0 | **静默维护**：无社区互动，活跃全靠依赖更新机器人，存在感低。 |
| **ZeroClaw** | 30 (27/3) | 50 (47/3) | 0 | **阻塞积压**：贡献多但合并效率极低(6.0%)，大量S1/S2 Bug和PR积压，影响v0.8.0发布。 |

#### **3. OpenClaw在生态中的定位**

OpenClaw依然是该生态的**绝对核心参照与风向标**。其优势在于：
- **社区规模与活跃度断层领先**：日处理500+ Issue/PR的体量是其他项目的5-10倍，生态影响力巨大。
- **技术路线前沿**：率先推动核心会话存储向SQLite迁移、采用Operator安装策略，这些探索为行业提供宝贵经验。
- **功能全面性**：覆盖了Agent、CLI、多渠道（Telegram、Slack等）、WebUI等几乎全部主流场景。

**相比同类**：
- **VS IronClaw**：OpenClaw更偏通用（“全能”），而IronClaw聚焦于“Reborn”架构的垂直重构，两者技术路线差异明显。OpenClaw的社区规模是IronClaw的10倍以上。
- **VS NanoBot**：OpenClaw体积与复杂性远高于NanoBot；NanoBot更强调轻量、快速部署和特定场景（如本地Agent）的优化。
- **社区规模**：OpenClaw的社区讨论深度和广度远超其它项目，其Issue和PR的内容质量也更高，常常能驱动生态内的最佳实践。

**挑战**：体量过大带来的稳定性回归问题（如Codex卡死、Windows UI吞输入）是其当前最大软肋，考验其质量控制体系。

#### **4. 共同关注的技术方向**

- **会话/状态管理现代化**（**OpenClaw**, **PicoClaw**, **ZeroClaw**）：从内存或文件型存储向SQLite等结构化数据库迁移，以支持更可靠的持久化和查询。OpenClaw的#88838是其中代表。
- **MCP (Model Context Protocol) 工具生态稳定性**（**NanoBot**, **CoPaw**, **LobsterAI**, **IronClaw**, **ZeroClaw**）：MCP连接易中断、工具调用丢失或注入失败是普遍痛点，多项目均在为此增加自动重连、校验和日志。
- **安全架构升级**（**ZeroClaw**, **Hermes Agent**, **OpenClaw**）：多个项目开始将安全层设计为可插拔接口，支持OIDC、沙箱（Landlock/Bubblewrap）等企业级方案，路径遍历、默认放行等漏洞修复成高频议题。
- **长任务/长会话可靠性**（**NanoBot**, **Hermes Agent**, **CoPaw**）：长时间运行的Agent任务出现卡顿“无响应”、上下文膨胀、会话中断等问题，社区对预热的Agent、上下文压缩、任务重试机制需求强烈。
- **自托管与平台兼容性**（**NanoBot**, **Hermes Agent**, **PicoClaw**, **ZeroClaw**）：涵盖Docker/Podman兼容、Windows/macOS生态（文件描述符限制）、32位系统支持、系统启动自启等基础运维痛点。

#### **5. 差异化定位分析**

| 项目 | 功能侧重 | 目标用户 | 技术架构 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全能型个人AI助手平台 | 开发者、高级用户、希望一站式部署的企业 | 模块化、插件化、Python为主 |
| **IronClaw** | 新一代Agent运行时架构(“Reborn”) | 注重架构前沿性、愿意尝鲜的开发者 | 高度模块化、类型安全、强契约设计 |
| **NanoBot** | 轻量级、易部署的个人AI助手 | 追求开箱即用、资源敏感的个人用户 | 简洁、插件化、Python为主 |
| **Hermes Agent** | 桌面端优先、深度集成 | 桌面用户、依赖GUI交互的团队 | 强调TUI/Desktop体验，支持多Profile |
| **ZeroClaw** | 高性能、企业级安全 | 对性能和安全性有极致要求的开发者 | Rust实现，注重内存安全和强隔离 |
| **LobsterAI** | 协作式编码助手 | 开发者、编码协作者 | 强调cowork、代码artifact分享 |
| **CoPaw** | 跨渠道、多模态Agent | 需要多渠道接入（飞书、Telegram）的用户 | 渠道适配器丰富，注重上下文记忆 |
| **Moltis** | Telegram原生深度集成 | Telegram重度用户 | 围绕Telegram Bot API深度定制 |
| **PicoClaw** | 嵌入式/物联网场景 | IoT开发者、资源受限设备 | 极简、高度依赖Go，适合编译为二进制 |
| **NullClaw/NanoClaw** | 特定领域或概念验证 | 关注特定技术点（如MCP工具过滤、调度）的开发者 | 功能聚焦，体积小 |

#### **6. 社区热度与成熟度**

- **快速迭代阶段（功能驱动）**：
    - **OpenClaw, IronClaw, CoPaw, LobsterAI**: 社区活跃度极高，新功能和PR不断，但同时伴随较多Bug和回归问题，稳定性有待提升。
- **质量巩固阶段（稳定性与性能驱动）**：
    - **NanoBot, Moltis**: 合并率高，Bug修复响应快，版本迭代稳健，体现了较好的工程成熟度。
- **健康度承压阶段（积压与瓶颈）**：
    - **Hermes Agent, ZeroClaw**: 贡献者热情高，但PR合并效率极低，大量高质量的修复和功能被阻塞，可能挫伤社区积极性。
- **长尾与沉睡阶段**：
    - **PicoClaw, NullClaw, NanoClaw, ZeptoClaw, TinyClaw**: 活跃度参差不齐，部分项目有明确的价值主张但在生态中声音有限，TinyClaw已实质上休眠。

#### **7. 值得关注的趋势信号**

1.  **“生产级可靠性”成为核心分水岭**：社区对**回归测试**（IronClaw #4431）和**高可用性**的呼声极高。稳定压倒一切，将成为项目能否从“玩具”走向“工具”的关键。例如，OpenClaw用户对Codex回归问题的批评（“已第二次被重新引入”）即是强烈信号。

2.  **AI原生应用交付模式的分化**：一类项目（如LobsterAI）强调**“cowork”**（实时协作编码），另一类（如OpenClaw/IronClaw）则更侧重于**异步、长周期任务**。交互模式（流式vs批处理、对话vs工具链）的探索和固化将成为产品体验差异化的关键。

3.  **安全不再是附属品，而是核心特性**：多个项目开始将安全层设计为第一等公民（如ZeroClaw的`forbid unsafe_code`、可插拔安全层）。这与路径遍历（Hermes）、权限默认放行（Hermes）等实际漏洞被大量披露有关。**安全架构的优劣将直接影响企业客户的采纳决策**。

4.  **多Agent协作尚处早期探索**：NanoBot用户对多智能体的强烈诉求（#222，已开放4个月），与OpenClaw/IronClaw中关于子Agent、能力组合的讨论形成呼应。虽然尚无成熟实现，但 **Agent-to-Agent编排（A2A）** 已成为社区公认的下一个技术高地。

5.  **去中心化与本地优先的回归**：NanoBot、CoPaw社区中，对**轻量内存检索（BM25/TF-IDF）** 的坚持，以及“工具调用幻觉”的抱怨，均暗示了对于过度依赖LLM大型模型的黑盒机制的不信任。运行在用户设备上的、可解释的本地AI能力（如小型嵌入、Reranker）存在广泛需求。

**对AI智能体开发者的参考价值**：
- **优先解决稳定性**：在添加新功能前，请务必建立自动化回归测试，尤其是针对核心流程（如会话、工具调用）。社区的容忍度正在急剧下降。
- **拥抱MCP但需做足防护**：MCP协议前景广阔，但其连接脆弱性、工具注入失败等问题是当前最大的实用障碍，投资于健壮的错误处理和重试机制回报率极高。
- **安全要从设计开始**：不要事后打补丁。将安全架构（如路径检查、权限模型）作为基础设施来设计，而非特性。
- **关注“小而美”的解决方案**：不要盲目堆砌功能。在特定场景（如Telegram Bot、轻量本地Agent、嵌入式）做到极致，可能比打造“万能”平台更具竞争力。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-06-04

---

## 1. 今日速览

过去 24 小时，NanoBot 项目保持高活跃度：共处理 33 条 Issue 更新（新开/活跃 26 条，关闭 7 条），34 条 PR 更新（待合并 16 条，已合并/关闭 18 条）。虽然没有新版本发布，但核心维护者（`chengyongru`）完成了多项关键修复与重构，涵盖 MCP 连接稳定性、WebUI 启动超时、内存模块加固等。社区关注点集中在**多智能体协作**、**工具调用幻觉**、**长任务可靠性**以及**安全性**方面。项目整体健康度良好，但长期积压的 feature request（如多智能体、内存检索、任务特定模型）仍待正式规划。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日合并/关闭的重要 PR 主要集中在稳定性、体验优化与架构清理：

- **MCP 会话自动重连** (`#4171`)：当工具/资源/提示词检测到 MCP 会话已终止时自动重连，避免手动重启。该修复由社区贡献者 `chengyongru` 合并，解决了用户报告的“随机超时”问题。
- **QQ 频道配对码发送** (`#4180`)：修复 QQ 未授权 C2C 用户无法收到配对码的问题，提升了国内渠道可用性。
- **Dream 模块重构** (`#3990`)：用基于正常 agent 循环的简单 cron + `process_direct` 替代旧的两阶段 Dream 类，简化了代码并降低维护成本。
- **内存模块加固** (`#4183`)：新增 PII 脱敏、原子写入、错误处理等 6 项结构性改进，提升了安全性与代码健壮性（合并中）。
- **WebUI 运行时状态迁至事件总线** (`#4135`)：将 WebUI/WebSocket 状态转换迁至事件订阅机制，为后续多客户端同步奠定基础。
- **WebUI 启动超时修复** (`#4157`)：为启动请求添加超时保护，防止永久挂起。
- **导入顺序修复** (`#4174`)：恢复 `nanobot.cli.commands` 模块顶层导入顺序，满足 ruff 检查。

此外，多个长期优化的 PR 也于今日合并，如上下文压缩提示词优化 (`#3920`)、记忆去重与 MECE 增强 (`#3952`)、长任务持续目标防止提前退出 (`#3999`) 等，表明项目在核心循环和记忆系统上持续打磨。

---

## 4. 社区热点

| Issue/PR | 评论数 | 👍 | 主题 | 分析 |
|----------|--------|----|------|------|
| [#222 Multi agents setup](https://github.com/HKUDS/nanobot/issues/222) | 10 | 7 | 多智能体配置支持 | 用户询问是否支持多智能体，并希望有文档/指南。该项目从 2 月即存在，至今未关闭，说明社区对此需求旺盛，但尚未有明确实现计划。 |
| [#979 防执行rm指令防不住](https://github.com/HKUDS/nanobot/issues/979) | 5 | 0 | 安全性（工具滥用） | 用户演示绕过“禁止rm”限制，通过直接 `rm -rf` 成功删除文件。反映了现有安全机制（如 restrict_to_workspace 未强制生效）的缺陷。 |
| [#1022 长任务卡住](https://github.com/HKUDS/nanobot/issues/1022) | 4 | 3 | 长任务可靠性 | 用户反馈执行长时间爬取任务时 agent 卡在“Starting execution now”阶段无输出。这触及核心执行引擎的异步处理瓶颈。 |
| [#80 轻量内存检索](https://github.com/HKUDS/nanobot/issues/80) | 4 | 0 | 内存优化 | 建议引入 BM25/TF-IDF 实现 top-k 相关记忆注入，减少 token 消耗并提升相关性。该需求已搁置 4 个月，但今日仍有新评论。 |
| [#954 进度流泄露内部工具调用](https://github.com/HKUDS/nanobot/issues/954) | 3 | 1 | 隐私/体验 | v0.1.4 的新进度流功能将 `exec()`、`read_file()` 等内部工具调用广播给用户聊天界面，影响使用体验。 |
| [#912 任务特定模型配置](https://github.com/HKUDS/nanobot/issues/912) | 3 | 3 | 模型路由 | 用户希望为对话、工具使用、浏览器使用分别配置不同模型。该项目获得 3 个点赞，是路线图的关键方向。 |

社区诉求集中体现在 **多智能体协作**、**长任务稳定性**、**内存优化**和**安全性**四大方向。

---

## 5. Bug 与稳定性

### 🔴 严重
- **MCP 会话随机断开** (`#4168`，已关闭)  
  > 描述：运行随机时间后 MCP 服务器不可达，日志提示 `McpError: Session terminated`，重启即可恢复。今日已由 `#4171` PR 修复并合并。
- **文件系统工具不强制 restrict_to_workspace** (`#143`，开放)  
  > 风险：`ReadFileTool`、`WriteFileTool` 等可绕过工作区限制，导致任意文件读写。已有 4 个 👍 但未分配 fix PR。
- **Telegram/Discord 媒体文件永不清理** (`#896`，开放)  
  > 磁盘无限增长，`~/.nanobot/media/` 目录积累大量临时文件。

### 🟡 中等
- **进度流泄露内部工具调用** (`#954`，开放)  
  > 属于功能回归，影响隐私。目前无 PR 关联。
- **远程 MCP URL 超时并抛出 asyncio.CancelledError** (`#935`，开放)  
  > 启动时连接远程 MCP 服务器失败，尚未定位原因。
- **长期任务卡住** (`#1022`，已关闭)  
  > 用户主动关闭，但根本问题未明确修复（可能被其他优化间接改善）。

### 🟢 轻微
- **WhatsApp 通道在 Linux Python 3.12 下 WebSocket 连接失败** (`#150`，开放)  
  > 表现为 Python 客户端反复断开重连，影响使用。
- **飞书 bot 未处理 remove 事件导致异常** (`#3787`，已关闭)  
  > 用户报告被其他 bot @提及时出错，已修复。

---

## 6. 功能请求与路线图信号

今日新增的功能请求：

- **原生 Agent-to-Agent (A2A) 编排** (`#4179`)：建议 Supervisor → Researcher → Writer 协作模式。与现有 `#222` 多智能体方向一致，但更强调原生架构支持。
- **WebUI 新对话快捷键 Cmd/Ctrl+Shift+O** (`#4178`)：已同步有 PR `#4181` 实现，预计很快合并。
- **Bocha 搜索提供商** (`#4182` PR)：为 DeepSeek 官方搜索 API 提供支持，面向中国市场。已提交 PR，有望纳入下一版本。
- **Azure AAD 认证支持** (`#4126` PR)：支持无 API Key 的 Identity Based Auth，适合企业场景。

此外，积压的高价值功能请求：

- **多智能体配置与文档** (`#222`) — 无 PR，但 `#1006`（子 agent 控制平面）、`#1012`（子 agent 配置化工具和技能）等关联 issue 均在活跃讨论中。
- **轻量内存检索** (`#80`) — 无 PR，但今日仍有新评论，社区持续关注。
- **任务特定模型配置** (`#912`) — 获得 3 个 👍，是 `#4126` Azure 认证的延伸需求。

从 PR 动向看，下一版本可能包含：**MCP 自动重连**、**WebUI 快捷键**、**Bocha 搜索**、**Azure AAD 支持**、**QQ 频道修复**、**Dream 重构**。

---

## 7. 用户反馈摘要

- **多智能体用户** (`#222`)：“支持多智能体吗？看起来配置支持，但希望有文档/小指南。” —— 反映文档滞后于配置能力。
- **长任务用户** (`#1022`)：“我让 agent 爬取 Facebook 帖子，它返回‘Starting execution now’然后什么都不做。” —— 执行引擎在大任务场景下易卡顿，影响生产力。
- **安全性担忧** (`#979`)：“我测试了 `rm -rf`，它真的执行了。你们说的防 rm 指令完全无效。” —— 当前安全防护形同虚设，急需修复。
- **工具幻觉** (`#937`)：“因为 exec 工具太多幻觉，我已停止评估该框架。” —— 核心工具的可靠性直接影响用户留存。
- **进度流泄露** (`#954`)：“v0.1.4 后，内部工具调用出现在用户聊天界面，这是不应该的。” —— 功能发布前回归测试不足。
- **磁盘增长** (`#896`)：“媒体文件从不删除，我的服务器磁盘快满了。” —— 运维成本升高。
- **WhatsApp 用户** (`#117`)：“用自己的号码跟机器人聊天时没有回复，因为代码里显式忽略了自己的消息。” —— 用户体验断裂。

整体来看，用户对 NanoBot 的 **轻量、可扩展性** 表示赞赏，但在 **生产级可靠性、安全性、文档完整性** 方面仍有较大提升空间。

---

## 8. 待处理积压

以下 Issue/PR 长期未响应，但仍具有较高社区价值或风险，提醒维护者关注：

| 编号 | 类型 | 主题 | 创建时间 | 最后更新 | 👍 | 备注 |
|------|------|------|----------|----------|----|------|
| [#222](https://github.com/HKUDS/nanobot/issues/222) | 功能请求 | 多智能体配置与文档 | 2026-02-06 | 2026-06-03 | 7 | 评论最多，需求明确，无开发进展 |
| [#80](https://github.com/HKUDS/nanobot/issues/80) | 功能请求 | 轻量内存检索 (BM25/TF-IDF) | 2026-02-04 | 2026-06-03 | 0 | 有 4 条评论，优化 token 消耗 |
| [#97](https://github.com/HKUDS/nanobot/issues/97) | RFC | 核心架构改进（内存、安全、测试） | 2026-02-04 | 2026-06-03 | 6 | 架构性建议，但无后续 PR 承接 |
| [#143](https://github.com/HKUDS/nanobot/issues/143) | Bug | 文件系统工具不强制 restrict_to_workspace | 2026-02-05 | 2026-06-03 | 4 | 严重安全漏洞，无 fix PR |
| [#150](https://github.com/HKUDS/nanobot/issues/150) | Bug | WhatsApp 通道在 Linux Python 3.12 下异常 | 2026-02-05 | 2026-06-03 | 0 | 平台兼容问题，可能影响较多用户 |
| [#896](https://github.com/HKUDS/nanobot/issues/896) | Bug | Telegram/Discord 媒体文件永不清理 | 2026-02-20 | 2026-06-03 | 0 | 磁盘无限增长，运维风险 |
| [#935](https://github.com/HKUDS/nanobot/issues/935) | Bug | 远程 MCP URL 超时 asyncio.CancelledError | 2026-02-21 | 2026-06-03 | 1 | 连接稳定性问题，尚未有 PR 关联 |
| [#954](https://github.com/HKUDS/nanobot/issues/954) | Bug | 进度流泄露内部工具调用 | 2026-02-21 | 2026-06-03 | 1 | 功能回归，影响隐私 |

以上 Issue 均标记为 `stale` 但仍在更新，建议维护者根据优先级分配里程碑或给出官方回应。

---

*本日报由 AI 自动生成，数据来源 [NanoBot GitHub](https://github.com/HKUDS/nanobot)，统计区间 2026-06-03 00:00 UTC 至 2026-06-04 00:00 UTC。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 | 2026-06-04

---

## 1. 今日速览

过去 24 小时内，Hermes Agent 项目继续保持极高的社区活跃度：共产生 50 条 Issue 动态（新开/活跃 43 条，关闭 7 条）和 50 条 PR 动态（待合并 43 条，已合并/关闭 7 条）。尽管无正式版本发布，但社区提交了大量 Bug 报告与功能请求，尤其在 **Windows 兼容性**、**macOS 文件描述符限制**、**多平台适配器（QQBot、WeCom）稳定性** 以及 **桌面端体验** 等方面集中爆发。安全方面新增了两项 **中/高严重性** 漏洞报告（Cron 内存写入、Skill 路径遍历）。项目维护者积极响应，已合并多个关键修复 PR，尤其是 Docker/Unraid 权限映射、DeepSeek 流式重试等长期问题的补丁顺利落地。

---

## 2. 版本发布

**无新版本发布。** 当前正式版为 v0.15.2（tag v2026.5.29.2）。值得注意的是，多个 Issue 指出 `hermes update` 在 Windows 上无法正确检测到新版本（[#38618]），可能影响用户升级体验。

---

## 3. 项目进展

今日共关闭/合并 **7 条 PR**，推动以下重要改进：

| PR | 标题 | 影响 |
|----|------|------|
| [#35992] | fix(tui): strip ANSI before estimating message height (long-session resume desync) | **TUI 长会话恢复乱码** 问题根因修复，`/compress` 不再是临时解决方案 |
| [#38098] | fix(docker): accept Unraid uid mappings | **Unraid 用户 UID=99 映射** 被 Docker 镜像忽略的问题彻底解决，`pairing/` 目录权限同步修复 |
| [#35035] | fix(gateway-windows): anchor detached/startup cwd at HERMES_HOME | **Windows 网关启动时工作目录** 不再依赖源码路径，提升跨环境稳定性 |
| [#37888] | feat(desktop): connect to OAuth-gated remote gateways | 新增 **桌面端远程 OAuth 认证** 客户端实现，为托管网关提供安全连接能力（半数完成） |
| [#38631] | fix(desktop): persistent needs-input indicator, clarify UI redesign | 修复 **后台会话需输入提示** 无限挂起问题，同时清理桌面端 UI 交互 |

**整体评估：** 上述合并 PR 主要围绕 **稳定性（TUI、Docker、Windows）** 和 **桌面端功能增强**，项目在一周内持续消化积压 Bug。另外，今日新提交的大量 PR（如 ModelScope 提供商、MiniMax Vision 加速、插件 API 扩展等）预示下一版本将拓展更多平台集成与插件生态。

---

## 4. 社区热点

以下 Issue/PR 在今日讨论最活跃、或获得最多用户关注（点赞 + 评论）：

- **[#26689] Accessibility improvements for blind VoiceOver users** — 8 条评论，0 赞。**诉求：** 全盲 macOS 用户指出 Hermes Agent 当前 UX 对屏幕阅读器极不友好，要求改进 CLI/TUI 的可访问性。虽非今日新开，但讨论持续至今，反应了**无障碍支持的长期缺口**。

- **[#37881] `hermes update` bricks the install on Windows** — 3 条评论，1 赞。**核心痛点：** Windows 用户运行更新后虚拟环境重建失败，导致 `ModuleNotFoundError`。此问题与 [#38407]、[#38618] 共同指向 **Windows 安装/更新流程脆弱**。

- **[#30230] Gateway hits macOS fd limit (256)** — 3 条评论，0 赞。**技术洞察：** macOS 默认文件描述符软限制为 256，网关进程（含多 Profile + MCP 服务器）轻易超过该值，导致 `OSError: Too many open files`。用户期望项目提供自动提升限制或文档引导。

- **[#24357] QQBot gateway can stop heartbeating after reconnect** — 3 条评论，2 赞。**平台稳定性：** Docker 中运行 QQBot 适配器时，重连后心跳停止，导致会话超时循环。该 Issue 已开放近一个月，仍无修复 PR，社区关注度较高。

- **[#38552] Automated Workspace Memory** — 2 条评论，0 赞。**功能愿景：** 希望 Agent 能自动记忆每个目录的用途，避免每次会话重新学习。与 #33856 互补，反映用户对“持久化工作区语义”的强烈需求。

---

## 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列如下（P0 → P1 → P2 → P3），并标注是否已有修复 PR。

| 级别 | Issue/PR | 描述 | 已有 Fix PR |
|------|----------|------|-------------|
| **P0** | [#38643] | `skill_view` 路径遍历：恶意构造的 `name` 可读取受信任技能目录外的文件（安全漏洞，CVSS 9.1） | ❌ 无 |
| **P1** | [#38652] | `parse_available_output_tokens_from_error()` 无法识别 OpenRouter/Nous 的 "output cap too large" 错误 → 导致无限重置循环 | ❌ 无 |
| **P1** | [#37881] | Windows 上 `hermes update` 破坏 venv，导致 `ModuleNotFoundError: hermes_cli` | ❌ 无（但 [#38618] 指出版本检测缺陷） |
| **P1** | [#38471] | Hermes Desktop 跳过 onboarding → 随机使用无效 OAI API Key，用户无法输入 OAI/Codex 信息 | ❌ 无 |
| **P2** | [#38638] | QQBot 等自定义策略适配器在未配置 allowlist 时默认放行（安全漏洞，CVSS 9.1/9.3） | ✅ [#38639]（已在同一作者名下提交） |
| **P2** | [#38156] | Windows TUI+Docker 中，主机启动目录被传入 Docker 终端会话（可能导致误操作） | ❌ 无 |
| **P2** | [#38407] | Windows 桌面应用更新后因 Git 检出不完整 + FS 缓存不匹配而启动失败 | ❌ 无 |
| **P2** | [#38580] | Jetson (aarch64) 上 `requests==2.33.0` 缺少 `_types.py`，更新后崩溃 | ❌ 无 |
| **P2** | [#38085] | WeChat 适配器长会话后“正在输入”指示符永久卡住 | ❌ 无 |
| **P3** | [#38650] | `hermes dump` 报告 MCP 服务器“失败”但实际发现成功（显示层问题） | ❌ 无 |
| **P3** | [#38618] | Windows 上 `hermes update` 检测不到 v0.15.2，重复提示落后 7 commits | ❌ 无 |
| **P3** | [#38314] | 桌面端 composer 可失去焦点，需要重启 | ❌ 无 |

**今日中高严重 Bug 数量：** P0 = 1，P1 = 3，P2 = 5（含两个安全漏洞），P3 若干。项目安全态势需关注。

---

## 6. 功能请求与路线图信号

用户今日提出了多项新功能需求，结合已有 PR 可推测下一版本可能纳入的方向：

| 功能需求 Issue | 描述 | 对应 PR 或关联 | 可能性评估 |
|----------------|------|----------------|------------|
| [#38640] | **桌面端 Windows 开机自启动** | 无 | 高 – 用户高频需求，实现简单（注册表或任务计划） |
| [#38641] | **企业微信（WeCom）适配器支持流式/编辑回复** | 无 | 中 – 当前硬编码 `SUPPORTS_MESSAGE_EDITING = False`，需适配器改造 |
| [#38552] | **自动工作区记忆**（Agent 记住目录用途） | 无 | 中 – 涉及工具链和记忆系统扩展，可能作为插件或独立功能 |
| [#38647] | **Cron Agent 内存写入静默失败**（触发 `skip_memory=True`） | 无 | 高 – 属 Bug 修复，但暴露了 Cron 路径下 memory 能力缺失，需优先处理 |
| [#37713] | **桌面端远程网关支持切换活动 Profile** | 无 | 低 – 与 [#37888] OAuth 合并后可能作为后续增强 |
| [#38007] | **桌面端系统托盘（Windows/Linux）** | 无 | 中 – 但 [#38631] 已开始 UI 清理，托盘功能可顺带实现 |
| #37218 | **Kanban 完成检查点（target_node 证明门）** | PR #37218 | 低 – 已停滞 2 天，可能是内部需求 |
| #37888 | 桌面端 OAuth 远程网关（已合并一半） | PR #37888 | ✅ 已部分合并，剩余网关端 OAuth 保护待完成 |
| #38648 | **新增 ModelScope 模型提供商** | PR #38648 | 高 – 已提交完整实现，顺理成章合并 |
| #38642 | **MiniMax Token Plan 视觉加速** | PR #38642 | 中 – 特定厂商优化，可能随下个版本集成 |

**路线图信号：** 社区对 **桌面端完善**（托盘、启动项、多 Profile）、**平台适配**（WeCom 流式）、**记忆增强**（工作区、Cron 内存）以及 **安全加固**（路径遍历、权限默认关闭）的呼声最强。

---

## 7. 用户反馈摘要

从今日开放/关闭的 Issues 评论中提炼真实用户反馈：

- **Windows 安装/更新体验差：** 多位用户（[#37881]、[#38407]、[#38618]）反复遭遇 `hermes update` 破坏环境的问题，包括虚拟环境重建失败、版本检测错误、Git 检出不完整。用户 `everglow01` 直言“永久破坏了安装”。这表明 **Windows 升级流程急需测试与重写**。

- **macOS 文件描述符限制无文档化：** 用户 `BournYSix` 报告网关进程在 macOS 默认 256 限制下频繁崩溃，建议项目在安装时自动检测并提升软限制。目前项目仅提示“需要自行调整”，社区期待更无缝的体验。

- **无屏幕阅读器支持：** 盲人用户 `xiaopinpin-music` 详细描述了 TUI 中的可访问性障碍（焦点管理、动态内容提示缺失等），呼吁将无障碍纳入 P2 优先级。

- **安全担忧：** 两位安全研究员分别报告了 `skill_view` 路径遍历（[#38643]）和 QQBot 默认放行（[#38638]），前者允许任意文件读取，后者可被远程利用。社区期待快速修复补丁。

- **性能与可靠性：** 用户反馈 Nous 推理 API 流式超时（[#29418]）、QQBot 心跳死循环（[#24357]）、WeChat 输入指示器卡死（[#38085]）等长期存在问题，影响生产环境使用。

- **正面反馈：** 用户对新增的 OAuth 远程网关功能（[#37888]）和 UI 清理（[#38631]）表示期待，认为方向正确。

---

## 8. 待处理积压

以下为开放时间较长、且今日仍有讨论但未获得实质解决的重要 Issue/PR，提醒维护者关注：

| 项目 | 创建时间 | 关键度 | 现状 |
|------|----------|--------|------|
| [#24357] QQBot 心跳重连后死循环 | 2026-05-12 | **P2** | 3 条评论，2 赞。尚无修复 PR，社区在等待解决方案。 |
| [#29418] Nous API 流式超时 | 2026-05-20 | **P3** | 2 条评论，1 赞。影响 Telegram 用户，仅靠回退到非流式。 |
| [#26689] TV 屏幕阅读器无障碍 | 2026-05-16 | **P3** | 8 条评论，0 赞。讨论热烈但无行动，可能需要 Design 决策。 |
| [#17986] Fireworks 自定义端点 HTTP 400（已关闭但未根本解决） | 2026-04-30 |  **P2** | 虽已关闭（可能用户 workaround），但底层模式未改，类似情况可能复发。 |
| [#35277] 中文 i18n 合并 PR | 2026-05-30 | **P3** | 开放 6 天，仍在等待 review。社区贡献者已解决冲突，建议优先合并。 |
| [#38638] QQBot 默认放行安全问题（已有 PR #38639） | 2026-06-04 | **P2** | PR 已提交，但需维护者尽快评审合并，避免 0-day 风险。 |
| [#38643] skill_view 路径遍历（无 PR） | 2026

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 | 2026-06-04

## 今日速览

过去24小时内，项目保持中等活跃度：4个Issues获得新评论（均为此前已开启的议题），10个Pull Requests中有2个被合并或关闭（安全依赖升级和MQTT TLS配置修复），其余8个仍处于待合并状态。社区讨论焦点集中在PID文件崩溃循环、流式HTTP请求支持以及工具调用消息丢失问题。整体来看，项目在安全修补和关键Bug修复上有所进展，但多个高优先级议题尚未合并，存在一定积压风险。

---

## 版本发布

**无**（过去24小时无新版本发布）

---

## 项目进展

### 🚀 已合并/关闭的 Pull Requests

- **[PR #2899] fix: add configurable TLS verification for MQTT channel**  
  📌 合并 ✅ | 作者: yangwenjie1231  
  🔗 https://github.com/sipeed/picoclaw/pull/2899  
  修复MQTT通道硬编码`InsecureSkipVerify=true`的安全风险，新增`TLSSkipVerify`配置项（默认false），用户可自行选择跳过验证以适配自签名证书。该合入提升了通道通信的安全性基线。

- **[PR #2997] fix(deps): bump go from 1.25.10 to 1.25.11 (GO-2026-5039)**  
  📌 合并 ✅ | 作者: afjcjsbx  
  🔗 https://github.com/sipeed/picoclaw/pull/2997  
  响应Go官方安全公告GO-2026-5039（`net/textproto`中HTTP头名未正确转义导致信息泄露），将Go版本升级至1.25.11，消除该高危漏洞。建议所有部署者尽快更新。

- **[PR #2995] docs: add v0.2.5~v0.2.9 release highlights to README News**  
  📌 待合并 ⏳ | 作者: chengzhichao-xydt  
  🔗 https://github.com/sipeed/picoclaw/pull/2995  
  补充README中v0.2.5至v0.2.9版本的更新亮点，改善新用户了解项目演进通道。未关闭但已获得明确维护意图，预期近期合入。

### 📌 值得关注的待合并 PR

- **[PR #2992] fix(session): skip main-session alias during history promotion**  
  📌 待合并 | 作者: chengzhichao-xydt  
  🔗 https://github.com/sipeed/picoclaw/pull/2992  
  修复v0.2.9升级后Web UI新会话自动附带旧消息的回归问题。该修复对用户体验影响较大，建议优先审查合并。

- **[PR #2996] fix(tools): handle json.Marshal errors in exec tool responses**  
  📌 待合并 | 作者: chengzhichao-xydt  
  🔗 https://github.com/sipeed/picoclaw/pull/2996  
  修复`pkg/tools/shell.go`中7处忽略的`json.Marshal`错误，防止执行工具失败时向LLM返回空字符串导致误解。提升工具调用的健壮性。

---

## 社区热点

### 🔥 最活跃讨论

1. **[Issue #2404] [Feature] Add in config to send streaming HTTP request**  
   💬 11评论 | 👍 1  
   🔗 https://github.com/sipeed/picoclaw/issues/2404  
   用户`OuSatoru`提议在配置文件中增加`"streaming": true`选项，使PicoClaw能以流式方式向LLM后端发送HTTP请求（类似OpenAI Python SDK的`stream=True`）。讨论持续近两个月，社区呼声较高，目前尚无相关PR提交，但该功能对实时对话场景至关重要，值得维护者纳入路线图。

2. **[Issue #2720] [BUG] Singleton PID check doesn't verify process identity — stale PID causes crash loop**  
   💬 8评论 | 优先级: high  
   🔗 https://github.com/sipeed/picoclaw/issues/2720  
   用户`weissfl`报告因PID文件残留导致网关启动崩溃（旧PID被系统其他进程复用），严重影响生产环境可靠性。两个修复PR（#2813、#2955）已存在，但至今未被合并，社区对此表示焦虑。

---

## Bug 与稳定性

| 严重程度 | Issue / PR | 描述 | 修复状态 |
|----------|------------|------|----------|
| 🔴 高 | [#2720](https://github.com/sipeed/picoclaw/issues/2720) | PID文件不验证进程身份，导致启动崩溃循环 | 已有PR [#2813](https://github.com/sipeed/picoclaw/pull/2813)（stale约1个月）及 [#2955](https://github.com/sipeed/picoclaw/pull/2955)，待合并 |
| 🟠 中 | [#2958](https://github.com/sipeed/picoclaw/issues/2958) | 通过pico channel连续请求时，`tool_calls`消息被丢弃 | 已有PR [#2957](https://github.com/sipeed/picoclaw/pull/2957)（stale约1周） |
| 🟡 低 | [#2954](https://github.com/sipeed/picoclaw/issues/2954) | 不支持32位Android系统（Termux环境） | 无对应PR，属于平台兼容性需求 |
| 🟢 已修复 | [PR #2899](https://github.com/sipeed/picoclaw/pull/2899) | MQTT通道TLS验证硬编码为跳过 | 已合并 |
| 🟢 已修复 | [PR #2997](https://github.com/sipeed/picoclaw/pull/2997) | Go依赖安全漏洞GO-2026-5039 | 已合并 |

**小结**：核心稳定性Bug（PID崩溃）的两个修复PR均超过一个月未合并，社区表达持续关注。建议维护者优先决策并合入，以降低运营风险。

---

## 功能请求与路线图信号

| 提议功能 | 对应 Issue | 可能纳入下一版本的依据 |
|----------|------------|------------------------|
| **流式HTTP请求支持** | [#2404](https://github.com/sipeed/picoclaw/issues/2404) | 评论区讨论积极，且已有多个项目依赖流式输出提升体验；若无重大技术冲突，v0.3.0的可能性较高 |
| **MCP动态请求头** | [PR #2696](https://github.com/sipeed/picoclaw/pull/2696) | 增强通道向MCP服务传递认证上下文的能力，PR已存在但较长（约1.5个月）未合入，推测维护者正在审阅设计 |
| **配置通道启用状态保留** | [PR #2956](https://github.com/sipeed/picoclaw/pull/2956) | 修复`.security.yml`加载后覆盖`enabled: true`的配置问题，属于配置合并的细节优化，预期在配置重构后合并 |

这些功能反映了用户对**实时性**（流式）、**安全性**（动态头）和**易用性**（配置合并）的持续诉求，建议维护者在下一个里程碑中优先评估。

---

## 用户反馈摘要

- **流式支持呼声高**：用户`OuSatoru`在#2404中表示“特别需要流式功能”才能对接OpenAI等原生流式API，目前只能等待完整响应，影响交互延迟。
- **PID崩溃影响信任**：用户`weissfl`在#2720留言中提到“每次重启都要手动删除PID文件，生产环境不可接受”，呼应了高优先级标签。
- **工具调用丢失困扰开发者**：用户`loafoe`在#2958中详细描述了bug复现步骤，并提交了修复PR（#2957），体现社区贡献积极性。
- **32位Android用户被忽略**：用户`yeozhang`在#2954中仅简单提及“不支持”，未得到进一步讨论，可能需要明确项目对移动端（Termux）的支持策略。

---

## 待处理积压

以下为长期未响应或pending的重要工作项，建议维护者关注：

| 类型 | 链接 | 存续时间 | 风险/影响 |
|------|------|----------|-----------|
| Issue (high) | [#2720](https://github.com/sipeed/picoclaw/issues/2720) PID崩溃 | 35天 | 生产环境启动失败，已有PR待合 |
| Issue (enhancement) | [#2404](https://github.com/sipeed/picoclaw/issues/2404) 流式HTTP | 58天 | 核心体验缺失，无对应PR |
| PR | [#2813](https://github.com/sipeed/picoclaw/pull/2813) PID修复 | 28天 | 与PR #2955冲突或需协调后合入 |
| PR | [#2696](https://github.com/sipeed/picoclaw/pull/2696) MCP动态头 | 37天 | 功能完善度高，但审阅耗时较长 |
| Issue | [#2954](https://github.com/sipeed/picoclaw/issues/2954) 32位Android | 8天 | 平台兼容性，若计划支持则需明确回复 |

**优先建议**：
1. 合并PID修复PR（#2813或#2955选一），消除高危急Bug。
2. 对#2404流式需求给出官方响应（纳入路线图或说明技术原因）。
3. 鼓励社区成员review并加速#2957（tool_calls丢失）和#2992（会话历史污染）等影响日常使用的修复。

---

*日报由AI自动生成，数据来源为 PicoClaw GitHub仓库的Issues、PRs及Releases，统计周期为2026-06-03 00:00 UTC 至 2026-06-04 00:00 UTC。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的NanoClaw GitHub数据，我为您生成2026年6月4日的项目动态日报。

---

### NanoClaw 项目动态日报 | 2026年6月4日

---

#### 1. 今日速览

今日项目活跃度非常高，展现出强劲的开发势头。尽管报告了一个影响系统启动的中等严重性Bug，但社区响应迅速，作者在几小时内就提交了修复PR。社区贡献者提交了 **9个高质量的Pull Request**，主要集中在修复调度模块的持久化问题和改进容器运行时，表明项目在稳定性和功能完善上正快速推进。整体来看，项目正处于一个高产出、社区协作紧密的健康发展阶段。

#### 2. 版本发布

*   今日无新版本发布。

#### 3. 项目进展

今日虽无PR被合并，但新提交的PR质量极高，覆盖了从核心调度到外围集成的多个关键模块，显示了项目引擎的快速迭代。

*   **调度模块韧性提升：**
    *   `yairixStudio` 贡献了两个重要修复：PR [#2679](https://nanocoai/nanoclaw/issues/2679) 将永久失败的计划任务转换为用户可见的通知，而非仅记录日志；PR [#2678](https://nanocoai/nanoclaw/issues/2677) 则修复了因任务永久失败导致后续重复计划失效的问题，确保重复任务能持续运行。
    *   `shrwnsan` 提交的 PR [#2677](https://nanocoai/nanoclaw/issues/2677) 为任务执行前的脚本（Pre-task script）增加了单次失败重试机制并附带诊断信息，进一步增强了任务执行的容错性。
*   **代理网络与权限环境优化：**
    *   `shrwnsan` 提交的 PR [#2676](https://nanocoai/nanoclaw/issues/2676) 为容器运行器添加了 `NO_PROXY` 环境变量支持，解决了在特定代理环境下访问本地服务可能被错误代理的问题。
    *   `guyb1` 提交的 PR [#2605](https://nanocoai/nanoclaw/issues/2605) 旨在使子代理能够通过 OneCLI 继承父代理的权限，这对于构建复杂的多代理协作流程至关重要，该项目虽创建于5月24日，但仍处于活跃讨论中。
*   **社区技能生态丰富：**
    *   `shrwnsan` 提交了名为 QMD 的容器技能 PR [#2683](https://nanocoai/nanoclaw/issues/2683)，为项目引入了混合Markdown搜索能力（结合BM25与向量搜索），进一步扩展了NanoClaw的知识处理能力。
*   **Slack集成兼容性修复：**
    *   `IamAdamJowett` 提交 PR [#2675](https://nanocoai/nanoclaw/issues/2675)，修复了 `/add-slack` 安装的Slack适配器因未处理3000字符的`section`块限制而导致的整条消息被丢弃的问题。

#### 4. 社区热点

*   **热点 Issue：** [#2680](https://nanocoai/nanoclaw/issues/2680) - **“Service doesn't start at boot when linger is enabled on an encrypted home directory”**
    *   **热度分析：** 尽管只有1个👍，但其重要性在于它指向了一个影响特定用户（使用加密家目录）的启动Bug。该Issue清晰描述了问题场景，并迅速获得了开发者的关注，当天就产生了修复PR，体现了社区对关键问题的快速响应能力。
*   **热点 PR：** [#2681](https://nanocoai/nanoclaw/issues/2681) - **“fix(service): skip linger on per-home-encrypted systems”**
    *   **热度分析：** 作为上述 Bug 的闭环修复，该PR是社区的绝对焦点。由同一用户 `glifocat` 提交，展示了社区“发现即修复”的主动贡献模式，这种模式极大提升了项目迭代效率。

**分析：** 社区热点清晰地指向了 **系统兼容性** 与 **部署稳定性**。用户期望NanoClaw能在更多样、更复杂的系统环境中无缝运行。

#### 5. Bug 与稳定性

| Issue/PR | 标题 | 严重程度 | 状态与修复 |
| :--- | :--- | :--- | :--- |
| [#2680](https://nanocoai/nanoclaw/issues/2680) | Service doesn't start at boot when linger is enabled on an encrypted home directory | **高**（影响特定用户场景的系统启动） | 已确认，**已有修复PR** ([#2681](https://nanocoai/nanoclaw/issues/2681)) |
| [#2679](https://nanocoai/nanoclaw/issues/2679) | fix(scheduling): surface permanently-failed scheduled tasks | **中**（任务失败通知问题，影响用户体验） | 已提交修复PR |
| [#2678](https://nanocoai/nanoclaw/issues/2678) | fix(scheduling): re-arm recurrence when a run fails permanently | **中**（重复任务计划中断问题） | 已提交修复PR |
| [#2675](https://nanocoai/nanoclaw/issues/2675) | fix(add-slack): patch Slack 3000-char section-block limit | **高**（导致Slack消息完全丢失） | 已提交修复PR |

**总结：** 今日报告的Bug主要集中在**系统启动**, **任务调度持久化**, 和 **Slack集成兼容性** 上。所有Bug均已获得相应的修复PR，项目对Bug的响应速度快。

#### 6. 功能请求与路线图信号

*   **QMD混合搜索技能**：PR [#2683](https://nanocoai/nanoclaw/issues/2683) 的提交是一个强烈的信号，表明社区对 **本地、混合（本地+向量）的知识检索** 能力有浓厚兴趣。这可能推动未来版本整合更强大的本地RAG能力。
*   **父代理权限继承**：PR [#2605](https://nanocoai/nanoclaw/issues/2605) 虽然是基于OneCLI的修复，但其本质是实现 **代理间权限传递**，这是构建复杂、层级化AI代理系统（如子代理模式）的基础需求，很可能被纳入下一版本的路线图，以增强NanoClaw作为多代理平台的灵活性。

#### 7. 用户反馈摘要

*   **Bug报告：服务启动失败**（来自 Issue [#2680](https://nanocoai/nanoclaw/issues/2680)）：用户`glifocat`报告了在加密家目录系统上，启用`linger`后服务无法在启动时自动运行的痛点。该用户不仅报告了问题，还深入分析了根因（`linger`不会触发家目录解密），并最终提交了修复代码，展现了极高的专业性。
*   **事件响应：Slack消息丢失**（来自 PR [#2675](https://nanocoai/nanoclaw/issues/2675)）：用户`IamAdamJowett`遇到并修复了一个关键问题：由于未遵守Slack平台对`section`块的3000字符限制，导致长消息会被整个丢弃。这反映了用户在实际部署中遇到的真实兼容性问题。

#### 8. 待处理积压

> **提醒：** 以下条目可能因长期未响应或待合并而阻塞项目进展。

*   **PR [#2605](https://nanocoai/nanoclaw/issues/2605)** - `feat: inherit parent agent permissions via OneCLI` (作者: guyb1)
    *   **状态：** 已创建超过10天，最后更新于2026-06-03。
    *   **风险：** 该PR涉及重要的权限继承特性，长期搁置可能导致与主线代码产生冲突，增加后续合并的难度。该PR的评论状态未知，建议维护者进行评审并给出反馈，以决定是合并、要求修改还是关闭。

---

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，遵照您的指示，我将以 AI 智能体与个人 AI 助手领域开源项目分析师的身份，根据您提供的 NullClaw 项目数据，生成 2026-06-04 的项目动态日报。

---

## NullClaw 项目动态日报 | 2026-06-04

### 1. 今日速览

今日项目活跃度较低，过去24小时内无新 Issue 开启或关闭，暂无新版本发布。唯一的动态是一条编号为 #946 的 Pull Request (PR) 处于待合并状态，该 PR 专注于优化 AI Agent 的系统提示词逻辑，通过引入工具过滤机制来提升工具调用的准确性与提示词效率。整体来看，项目处于功能集成的静默期，核心团队正在推进一项对 MCP (Model Context Protocol) 工具管理至关重要的技术改进。

- **活跃度评估**: 低 (Low)。主要体现为 PR 的提交与等待审核，无新问题或公开讨论产生。

### 2. 版本发布
- 无

### 3. 项目进展

- **核心机制优化：工具过滤与提示词精简**
  - **PR #946 (待合并)**: 由贡献者 `vernonstinebaker` 提交，旨在解决智能体在生成系统提示词时，错误地包含所有 MCP 工具的问题。
  - **变更内容**:
    1. 新增 `filterToolsForPromptText` 逻辑，仅将属于“内置工具”和“始终 (always)”过滤组的 MCP 工具的 schema 写入文本形式的系统提示词中。
    2. 对于“动态群组 (Dynamic-group)”的 MCP 工具，其 schema 将**不**出现在长文本提示词中。而是在运行时，当用户的对话触发特定关键词 (turn keywords) 时，通过原生 API 工具调用机制动态发送其 schema。
  - **意义**: 此项改进直接提升了提示词的质量，减少了 Token 消耗，并避免了因冗长的工具描述干扰模型决策。同时保持了对动态工具的实时响应能力，是 Agent 系统在工具管理方面的重要优化。

  **链接**: [NullClaw PR #946](https://github.com/nullclaw/nullclaw/pull/946)

### 4. 社区热点

今日无讨论活跃的热点 Issue 或 PR。PR #946 目前处于开放状态，暂无评论，但其提交内容反映了社区在优化 Agent 提示词效率和工具调用控制方面的技术探索，具有潜在的广泛讨论价值。未来当维护者开始 review 此项变更时，预计会引发关于不同工具分组策略优缺点的讨论。

### 5. Bug 与稳定性

今日无新报告的 Bug。PR #946 本身可以被视为对一项潜在“噪音”问题的修复——即系统提示词中包含了所有工具信息，可能导致模型在不恰当的时机调用无关工具，或模型因上下文过长而产生幻觉。

- **严重性**: 中。该问题会影响 Agent 的行为准确性和性能，但不会导致崩溃或数据丢失。
- **修复 PR**: 已存在，即 PR #946。

### 6. 功能请求与路线图信号

今日无新功能请求。PR #946 提供了一种新的工具管理范式，即“静态过滤 + 动态触发”。这暗示了项目路线图中的一个重要信号：项目**可能正在规划或强化对 MCP 工具源的精细化管理**，特别是支持“始终启用”和“按需启用 (动态群组)”的灵活策略。这为未来实现更复杂的 Agent 工作流编排（如不同任务使用不同的工具集）铺平了道路。

### 7. 用户反馈摘要

今日无用户反馈。但结合 PR #946 的变更，可以推测出此前可能存在以下用户痛点：
- **提示词过长**: 用户可能反馈系统提示词因包含过多不相关的工具而异常冗长，导致 API 费用增加和响应变慢。
- **工具误调用**: 用户可能观察到 Agent 在没有明确指令的情况下，错误地调用了某个 MCP 工具。PR 的优化方向正是解决此类问题。

### 8. 待处理积压

- **PR #946 [开放待处理]**: 此 PR 是今日唯一的活跃进度，但尚未获得合并或 review。建议维护者关注此 PR，它解决了 Agent 系统在工具调用方面的一个核心痛点。如果合并，将是一个有价值的稳定性与性能优化里程碑。同时也请注意，此 PR 的作者 `vernonstinebaker` 可能正在等待反馈。

  **链接**: [NullClaw PR #946](https://github.com/nullclaw/nullclaw/pull/946)

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目日报 — 2026-06-04

## 1. 今日速览

- 过去24小时项目活跃度极高：共处理27条Issue（新开/活跃19条，关闭8条）和50条PR（待合并21条，已合并/关闭29条），并发布新版本v0.29.1。
- 核心开发集中在**Reborn架构**的稳定性、安全审计与功能补全，包括Slack集成、OAuth绑定、触发器治理等关键模块。
- 多项高影响力Bug被确认并已有修复PR在途，例如`builtin.spawn_subagent`在结构化工具中缺失、`builtin.http`导致上下文爆炸、`builtin.skill_list`无限制返回等，反映出项目对AI Agent运行时质量的严格把控。
- 社区贡献者活跃，多位“core”成员提交了XL级PR，项目整体处于快速迭代的“冲刺”阶段，健康度良好。

## 2. 版本发布

### ironclaw-v0.29.1 (2026-06-04)
- **Release Notes**: [v0.29.1](https://github.com/nearai/ironclaw/releases/tag/ironclaw-v0.29.1)
- **新增**：
  - `web`: 通过Responses API中透传温度参数（[#3641](https://github.com/nearai/ironclaw/pull/3641)）
- **修复**：
  - `engine`: 限定v1历史记录的作用域为频道对话（[#4320](https://github.com/nearai/ironclaw/pull/4320)）
- **CI/发布**：
  - `release`: 添加WeCo支持

> **迁移注意事项**：该版本为小版本修复，无破坏性变更。使用v0.29.0的用户可直接升级。

## 3. 项目进展

### 已合并/关闭的重要PR（推动功能交付与质量加固）

| PR | 标题 | 说明 |
|----|------|------|
| [#4406](https://github.com/nearai/ironclaw/pull/4406) | PR 18.5a: type-seal trusted trigger ingress | 类型密封可信触发器入口路径，移除旧的公共权限令牌门面，为触发器传递提供安全基础。 |
| [#4422](https://github.com/nearai/ironclaw/pull/4422) | Add Slack personal binding service | 为共享租户Slack应用添加Reborn组合式Slack个人绑定服务，实现按用户绑定流程。 |
| [#4421](https://github.com/nearai/ironclaw/pull/4421) | Bind Slack actors through Reborn user identities | 添加产品工作流参与者-用户解析钩子，使主机组合能够在规范会话解析前绑定外部参与者（如Slack用户）。 |
| [#4418](https://github.com/nearai/ironclaw/pull/4418) | Wire Slack host-beta route into Reborn serve | 将Slack Events API通过Reborn运行时、ProductWorkflow、主机中介HTTP出口及最终回复交付完整串联，实现Slack主机测试路线。 |
| [#4415](https://github.com/nearai/ironclaw/pull/4415) | PR18.7: trigger poller full-path integration test | 新增组合级别集成测试，驱动真实后台触发器轮询器，验证从种子记录到LLM网关的全路径。 |
| [#4417](https://github.com/nearai/ironclaw/pull/4417) | Fix WebUI live projection cursor resume | 拆分WebUI投影游标，使合成实时进度更新不再推进持久化运行时游标，修复游标恢复问题。 |
| [#4412](https://github.com/nearai/ironclaw/pull/4412) | Bind local dev runtime scope to run actor | 将本地开发能力运行时身份绑定到运行参与者，修复SSO请求参与者为空时的回退问题。 |
| [#4380](https://github.com/nearai/ironclaw/pull/4380) | Add read-only automations WebUI API | 新增WebUI v2只读自动化端点`GET /api/webchat/v2/automations`，通过产品工作流展示调度自动化行。 |

**项目整体向前迈进**：Slack集成从理论走向可用，触发器系统完成全路径测试和类型加固，WebUI投影游标修复，本地开发身份绑定完善。Reborn架构的“硬核”基础设施逐步闭合。

## 4. 社区热点

### 高讨论度Issue

- **[#4424 - `builtin.spawn_subagent`在表面文本中宣传但缺失结构化工具数组](https://github.com/nearai/ironclaw/issues/4424)**（3条评论）
  - 核心诉求：模型被告知有`spawn_subagent`工具，但OpenAI兼容模型中未实际传递，导致模型循环叙述但无法调用。直接影响了Reborn Serve的可用性。
  - 背后信号：Agent能力表面与结构化工具暴露需保持严格一致性，否则模型行为异常。

- **[#4425 - `builtin.http`返回1.2MB HTML内容引发上下文爆炸](https://github.com/nearai/ironclaw/issues/4425)**（1条评论）
  - 核心诉求：HTTP工具无大小上限、无HTML转文本、描述未引导模型使用`.save`。单次抓取即注入大量噪声，破坏上下文。
  - 背后信号：用户对工具的资源消耗和上下文管理非常敏感，需要更智能的限流与预处理。

- **[#4426 - 父循环工具表面为AllowAll，未遵循配置的profile_id](https://github.com/nearai/ironclaw/issues/4426)**（1条评论）
  - 核心诉求：虽然配置了`interactive_tools` profile，但解析器硬编码为`AllowAllCapabilitySurfaceResolver`，导致简单聊天中暴露了生命周期/变更工具，存在安全风险。

### 高讨论度PR

- **PR [#4413](https://github.com/nearai/ironclaw/pull/4413) / [#4414](https://github.com/nearai/ironclaw/pull/4414) / [#4410](https://github.com/nearai/ironclaw/pull/4410)**（均为XL级，core贡献）——分别修复子代理完成传递、循环能力验证、Google刷新场景，体现核心团队持续加固关键路径。

## 5. Bug 与稳定性

### 严重Bug（需紧急关注）

- **[#4424 - `builtin.spawn_subagent`工具缺失](https://github.com/nearai/ironclaw/issues/4424)** — **严重性：高**。模型可见但不可调用，属于API合同违反。**已有对应修复PR [#4414](https://github.com/nearai/ironclaw/pull/4414)**（Harden loop capability validation）在审查中。
- **[#4425 - `builtin.http`上下文爆炸](https://github.com/nearai/ironclaw/issues/4425)** — **严重性：高**。无上限返回可轻易超出模型token限制。暂未关联修复PR，但社区已讨论需增加HTML剥离、大小上限及引导`.save`。
- **[#4426 - 能力表面忽略profile_id](https://github.com/nearai/ironclaw/issues/4426)** — **严重性：中高**。导致未授权的工具暴露，有安全隐患。暂未关联PR。

### 其他影响较大的Bug

- **[#4427 - 循环退出原因不可见](https://github.com/nearai/ironclaw/issues/4427)** — 严重性：中。`LoopFailureKind`仅写入DB但不记录日志，运维无法调试。
- **[#4429 - 每次模型调用重建完整prompt bundle](https://github.com/nearai/ironclaw/issues/4429)** — 严重性：中。性能浪费，身份/技能缓存每次冷启动，影响响应延迟。
- **[#4428 - `builtin.skill_list`无限制，一次返回31个技能14KB](https://github.com/nearai/ironclaw/issues/4428)** — 严重性：中。消耗上下文，需分页/截断。已获1条评论。
- **[#4420 - `CompleteAfterFirstFire`触发策略未被执行](https://github.com/nearai/ironclaw/issues/4420)** — 严重性：中。触发器持续重复触发，违反用户预期。
- **[#4400 - 因陈旧PID文件导致IronClaw无法启动](https://github.com/nearai/ironclaw/issues/4400)** — 严重性：中。生产环境影响，无自动恢复机制。
- **[#4310 - 上下文溢出恢复时ShrinkContext未被执行](https://github.com/nearai/ironclaw/issues/4310)** — 严重性：中。已关闭（已修复），体现项目对Bug的快速响应。

## 6. 功能请求与路线图信号

### 新提出的功能需求（来自Issue）

- **[#4431 - 回归测试：每个可见能力必须可调用](https://github.com/nearai/ironclaw/issues/4431)** — 铁律要求，确保`visible_capabilities`与`tool_definitions`完全一致。很可能被纳入下个版本的测试套件。
- **[#4407 - 为提供者工具数量限制设计模型可见能力选择](https://github.com/nearai/ironclaw/issues/4407)** — 因Reborn能力增多超出OpenAI等提供者的`tools`数组上限，需设计能力选择机制。与PR无直接关联，但已是路线图中“工具管理”部分的明确信号。
- **[#4382 - 产品认证：每个提供者默认OAuth账户（设置一次后不再触发）](https://github.com/nearai/ironclaw/issues/4382)** — 用户希望一次认证后不再重复走OAuth门。属于UX改进，已有关联PR [#4381](https://github.com/nearai/ironclaw/issues/4381)（添加规范Reborn身份解析器）。
- **[#4377 - `/model`返回的显示名称不能用于切换模型](https://github.com/nearai/ironclaw/issues/4377)** — 生产环境用户发现显示名称与实际模型标识不匹配，影响模型切换操作。

### 已有PR可纳入下版本

- **Slack个人绑定配对流程**（PR [#4430](https://github.com/nearai/ironclaw/pull/4430)）——开放中，提供了挑战/赎回服务，是Slack集成的重要补充。
- **WebUI v2质量提升：实时线程状态 + 侧边栏固定标记**（PR [#4419](https://github.com/nearai/ironclaw/pull/4419)）——开放中，带来线程注意力持久化和活跃状态显示。

## 7. 用户反馈摘要

从Issue评论中提炼的真实用户痛点：

- **“`/model`返回的显示名称无法实际用于切换模型”**（[#4377](https://github.com/nearai/ironclaw/issues/4377)）：用户尝试使用`GPT OSS 120B`等名称切换模型失败，期望显示名称与模型ID一一对应。
- **“生产环境因陈旧PID文件无法启动”**（[#4400](https://github.com/nearai/ironclaw/issues/4400)）：用户表示实例持续重启但无自动恢复，需手动删除PID文件，对运维不友好。
- **“触发器使用`CompleteAfterFirstFire`策略后依然反复触发”**（[#4420](https://github.com/nearai/ironclaw/issues/4420)）：用户期望触发一次后自动完成，实际却无限期执行，属于功能性缺陷。
- **“Reborn Serve中`builtin.http`抓取1.2MB HTML导致模型无法响应”**（[#4425](https://github.com/nearai/ironclaw/issues/4425)）：用户反馈“context bomb”，强烈建议增加HTML转文本和大小上限。

**满意点**：社区感谢Slack集成和触发器系统的快速落地，多个XL级PR获得积极反馈。

## 8. 待处理积压

### 长期未响应的重要Issue

- **[#3283 - 将OpenAI兼容Chat及Responses API迁移到Reborn](https://github.com/nearai/ironclaw/issues/3283)**（创建于2026-05-06，1条评论）——父任务为#3031，属于Reborn核心迁移项，当前进度仅有一次更新，需明确下一步计划。
- **[#4108 - Nightly E2E持续失败](https://github.com/nearai/ironclaw/issues/4108)**（创建于2026-05-27，0条回应）——CI可靠性已成为风险，至今无人跟进分析根本原因。

### 阻塞性PR

- **[#3951 - 第三方扩展hook激活](https://github.com/nearai/ironclaw/pull/3951)**（2026-05-23创建，XL级，core贡献）——仍处于开放状态，依赖#3938，已等待2周。对接三方生态的关键功能，建议定期更新状态。
- **[#3937 - 跨后端对抗性一致性测试套件](https://github.com/nearai/ironclaw/pull/3937)**（同样2026-05-23创建，XL级）——是持久化谓词后端分割的最终PR，长期未合并可能影响hooks系统稳定性。

> 注：以上积压Issue/PR如持续无响应，建议维护者在下一个sprint规划中予以优先处理，避免技术债堆积。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 | 2026-06-04

---

## 1. 今日速览

- **项目整体活跃度：高**  
  过去24小时合并/关闭了14个PR，发布了1个新版本（2026.6.3），代码合入节奏密集。社区反馈方面，1条新Issue（关于积分清零）引发2条评论，但未出现大规模讨论；待合并PR仅2条（均为dependabot依赖更新和旧PR），积压清理情况良好。项目在cowork协作、MCP、HTML分享、快捷键重构等模块持续推进，社区功能迭代速度较快。

---

## 2. 版本发布

### 📦 LobsterAI 2026.6.3（2026-06-03）

**更新内容**  
- **MCP优化**：改进npx MCP启动解析、添加首次响应时间日志（PR #2091）  
- **HTML分享**：优化分享体验（PR #2092）  
- **cowork新增**：添加“artifact预览选中文本添加到聊天”功能（PR #2101）  
- **其他**：包含快捷键全面重构、会话同步清理、UI交互改进等多项合并（见下方项目进展）

**破坏性变更**  
- 无明确标注破坏性变更，但键盘快捷键经过全面重构（PR #2109），用户自定义快捷键可能需重新配置。建议升级后检查个人快捷键映射。

**迁移注意事项**  
- 若使用MCP远程服务器配置，新版本增加了URL校验（PR #2103），请确保远程地址格式正确，否则会被拒绝。  
- HTML分享对话框和访问控制重新设计（PR #2099），分享流程有所调整（去掉了自动复制和全局toast），用户需适应新交互。

---

## 3. 项目进展

今日合并/关闭的14个PR中，核心推进方向如下：

### 🔹 cowork协作模块
- **文本选择与上下文注入**（PR #2101 / #2098）：支持从Markdown/纯文本artifact预览中选择文本并添加到当前cowork草稿；同时支持从助手消息中选择文本并添加。该功能极大提升用户在多轮对话中引用材料的能力。  
- **本地对话分支（Fork）**（PR #2085）：允许从助手消息创建新的本地对话，保留压缩上下文。这是对长对话管理的重要扩展。  
- **频道会话同步与清理**（PR #2108）：确保重建频道会话时仅同步最新用户轮次，删除网关会话记录，替换分支图标组件。  
- **搜索模态框标题栏关闭按钮**（PR #2097）：修复cowork搜索框缺少关闭按钮的问题。

### 🔹 MCP（模型上下文协议）优化
- **URL校验**（PR #2103）：增加远程服务器URL验证，并在配置同步时拒绝无效URL，附带本地化错误提示。  
- **保持Node感知**（PR #2100）：修复managed安装的MCP插件在Electron环境下无法正确使用Node工具链的问题，注入解析后的路径，防止服务器被静默丢弃。  
- **会话超时修复**（PR #2104）：预防网关配置重新加载时会话超时。

### 🔹 快捷键重构
- **全面重构键盘快捷键**（PR #2109）：扩展动作列表并改善UX，用户可更灵活配置。

### 🔹 HTML分享
- **分享对话框与访问控制**（PR #2099）：重新设计分享对话框状态，退出测试模式，添加订阅来源属性，刷新分享细节。  
- **复制链接与代码整合**（PR #2105）：格式化复制内容，区分带代码和不带代码的链接。

### 🔹 配置与模型支持
- **保留用户配置的上下文窗口，添加Mimo v2.5模型**（PR #2102）。

### 🔹 发布流程
- **版本发布2026.6.2**（PR #2107）：集成了上述所有功能（实际为中间版本，今日发布的2026.6.3在其基础上继续迭代）。

**项目前进评估**：  
cowork模块已成为当前开发核心，连续多个PR聚焦文本选择、分支、同步，表明团队正在加速完善协作场景。MCP稳定性和配置校验也获得显著提升，预示下一代插件生态系统正在夯实。

---

## 4. 社区热点

### 🔥 Issue #2081：积分订阅清零投诉
- **作者**：zjk648491625  
- **状态**：OPEN（创建于6月1日，最后更新6月3日，2条评论）  
- **摘要**：用户质疑购买的5500积分在月底被清零，附截图表示不满。  
- **链接**：https://github.com/netease-youdao/LobsterAI/issues/2081

**分析**：该Issue直接触及付费用户的敏感点——积分清零规则。尽管只有2条评论，但“😡”情绪明显。若项目采用“月度积分不累积”策略，用户事前未充分知晓，易引发信任危机。建议维护者澄清积分有效期政策，或考虑提供积分保留或补偿机制。目前暂无官方回复记录，需优先关注。

---

## 5. Bug 与稳定性

### 🔴 严重程度：高（无明显严重Bug报告）

| 严重程度 | 问题描述 | 相关PR/Issue | 状态 |
|----------|----------|--------------|------|
| 中 | **HTML分享复制行为变更**：移除自动复制和全局toast，部分用户可能不适应新流程 | PR #2099（已合并） | 已修复 |
| 中 | **MCP远程URL未校验**：之前可能允许格式错误的URL，现增加校验 | PR #2103（已合并） | 已修复 |
| 中 | **MCP managed安装丢失Node路径**：导致特定场景下MCP服务器启动失败 | PR #2100（已合并） | 已修复 |
| 低 | **模态框标题过长溢出**：PR #1463（待合并）提供了截断方案，该PR被标记为stale | Issue #1435 → PR #1463 | 待处理 |
| 低 | **cowork搜索模态框缺少关闭按钮** | PR #2097（已合并） | 已修复 |
| 低 | **模型选择器悬停卡片溢出视口** | PR #2106（已合并） | 已修复 |
| 低 | **技能弹出框延迟关闭** | PR #2106（已合并） | 已修复 |

**结论**：今日无新报告的高危或崩溃级Bug，已合并的多个Fix有效提升了cowork UI和MCP的健壮性。

---

## 6. 功能请求与路线图信号

### 用户潜在需求（从Issue和PR推导）
- **积分/订阅规则透明化**：Issue #2081暗示用户对积分清零缺乏预期，可能需要在UI或文档中明确展示有效期，或提供积分购买确认前的弹窗说明。
- **更灵活的文本选择操作**：最新合并的PR #2098、#2101已支持从artifact和助手消息中选择文本添加到chat，但尚不支持从普通聊天历史中选择。用户可能期望全量文本选择能力。
- **长对话分支管理**：PR #2085实现了本地分支，但尚未支持云端分支或分支合并。从设计文档（PR内提及）看，未来可能支持更复杂的会话树。

### 已体现路线图的信号
- **cowork模块持续加强**：多个PR并行推进，表明cowork是当前版本重点。
- **MCP生态加固**：校验、日志、Node感知等修复表明团队正为第三方MCP插件大规模使用做准备。
- **HTML分享退出测试**：PR #2099将HTML分享正式开放，预示产品功能成熟。

---

## 7. 用户反馈摘要

### 正面反馈（无明确正面评论，但合并PR体现了社区贡献）
- 多位社区贡献者（btc69m979y-dotcom、liuzhq1986、fisherdaddy、liugang519等）活跃提交高质量PR，说明外部贡献者参与度较高。
- 快捷键全面重构（PR #2109）可能部分来自用户对快捷键自定义的需求，虽无直接评论，但改动方向符合效率用户期望。

### 负面反馈
- **积分清零**（Issue #2081）：用户表达强烈不满，认为购买积分不应月底清零。这是今日唯一的社区负面声音，可能影响付费用户留存。
- **UI交互变动**：HTML分享移除自动复制到剪贴板的行为可能在用户习惯转变中引发短暂不适。

### 使用场景暗示
- 用户常在长对话后需要引用早期artifact内容（PR #2101），说明项目正用于编码协作、文档审查等场景。
- 分支功能（PR #2085）表明用户在探索多可能性任务，需要保存不同分支的对话状态。

---

## 8. 待处理积压

### 🟡 长期未响应Issue
| Issue | 标题 | 创建时间 | 最后更新 | 标签 | 备注 |
|-------|------|----------|----------|------|------|
| #2081 | 订阅积分清零投诉 | 2026-06-01 | 2026-06-03 | 无标签 | 用户情绪高，建议尽快回复 |
| - | 目前无衰老严重Issue | - | - | - | - |

### 🟡 长期未合并PR
| PR# | 标题 | 创建时间 | 最后更新 | 状态 | 建议 |
|-----|------|----------|----------|------|------|
| #1277 | chore(deps-dev): bump electron group | 2026-04-02 | 2026-06-03 | OPEN（待合并） | 依赖升级涉及Electron 40→42，需回归测试后合并 |
| #1463 | [stale] fix long modal titles for issue 1435 | 2026-04-04 | 2026-06-03 | OPEN（stale） | 已标记为stale，但该问题影响模态框显示，建议review并合并或关闭 |

**提醒**：上述两个PR均存在2个月以上，可能产生冲突或低优先级，但#1277为安全依赖更新，建议安排合并以避免后续问题。#1463是用户体验改进，review后可快速合并。

---

*本日报由AI自动生成，数据截止于2026-06-04 08:00 UTC。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的Moltis项目GitHub数据，我已为您生成了2026年6月4日的项目动态日报。

***

### Moltis 项目日报 (2026-06-04)

**项目:** moltis-org/moltis
**日期:** 2026-06-04

---

#### 1. 今日速览

今日Moltis项目状态**高度活跃**，呈现出“高修复、高产出”的特征。团队在处理历史遗留Bug方面取得了显著进展，24小时内解决了9个Issue，并发布了2个新版本。然而，项目也暴露出了一些新的关键问题，尤其是在Docker环境下的兼容性和稳定性方面。值得关注的是，3个待合并的Pull Request均针对今日报告的核心问题，但暂无任何PR被正式合并，修复的最终落地仍需关注。整体来看，项目正处于密集的迭代和Bug修复周期，健康度良好，但交付节奏有待加速。

#### 2. 版本发布

Moltis在今日发布了两个连续的小版本更新（**20260602.05** 和 **20260603.01**），推测为夜间构建或紧急补丁版本。

- **版本 `20260602.05` & `20260603.01`:**
    - **更新内容:** 结合近期合并的Issue和已关闭的PR判断，这两个版本很可能已经包含了针对近期一系列Bug的修复。
    - **破坏性变更:** 无。
    - **迁移注意事项:** 建议所有用户尽快升级至最新版本 `20260603.01`，特别是为了解决 `send_image`/`send_document` 在Docker环境下的失败问题（[#1037](https://github.com/moltis-org/moltis/issues/1037)）以及非语法高亮问题（[#1045](https://github.com/moltis-org/moltis/issues/1045)）。

#### 3. 项目进展

过去24小时内，**没有Pull Request被合并或关闭**，这是一个值得关注的信号。所有开放的PR均处于待合并状态，这表明核心修复工作已准备就绪，但尚未正式并入主分支。尽管如此，通过Issue状态的变化，可以推断出项目修复进展显著：

- **核心Bug大量修复:** 新版本（`20260603.01`）的发布以及9个Bug/功能请求的关闭，标志着多个历史遗留问题已被解决。这包括：
  - **安全修复:** [#1054](https://github.com/moltis-org/moltis/issues/1054) (MCP服务器环境变量泄露) 已解决。
  - **核心功能修复:** [#1053](https://github.com/moltis-org/moltis/issues/1053) (自动会话标题生成) 和 [#1046](https://github.com/moltis-org/moltis/issues/1046) (Vault密码设置) 得到修复。
  - **平台兼容性修复:** [#1037](https://github.com/moltis-org/moltis/issues/1037) (Docker中的文件发送) 和 [#1052](https://github.com/moltis-org/moltis/issues/1052) (模型选择器) 已修正。
  - **UI/UX改进:** [#1045](https://github.com/moltis-org/moltis/issues/1045) (代码高亮) 和 [#1036](https://github.com/moltis-org/moltis/issues/1036) (任意文件附件) 已实现或修复。

#### 4. 社区热点

今日社区讨论和关注焦点集中在**Telegram消息交互体验**上。

- **最活跃 Issue:** **[Bug]: Telegram edit-in-place streaming mixes intermediate output into final reply** ([#1097](https://github.com/moltis-org/moltis/issues/1097))
    - **分析:** 该问题精准地指出了用户在使用Telegram Bot时遇到的痛点：流式输出过程中，中间结果被错误地混合到最终回复中，导致信息杂乱。这直接影响了用户体验。一位核心贡献者已立即提交了对应的修复PR ([#1099](https://github.com/moltis-org/moltis/pull/1099))。

- **相关 PR:** **[PR] Separate Telegram progress stream from final replies** ([#1099](https://github.com/moltis-org/moltis/pull/1099))
    - **分析:** 此PR是完全针对上述问题提出的解决方案，展示了项目对社区反馈的快速响应能力。

- **另一个高频话题:** **[Feature] Add a config option to disable channel Activity log tool-status messages** ([#1092](https://github.com/moltis-org/moltis/issues/1092))
    - **分析:** 此问题与 [#1097](https://github.com/moltis-org/moltis/issues/1097) 密切相关，反映了用户对控制Agent行为可见性的强烈需求。用户希望核心回答与工具调用痕迹（Activity log）能够分离，以实现更干净的对话体验。对应的PR ([#1093](https://github.com/moltis-org/moltis/pull/1093)) 已经存在，表明该功能很可能被纳入下一版本。

#### 5. Bug 与稳定性

今日新报告的Bug共4个，均有较高优先级。

- **严重 - [P0]:** **[Bug]: `Read`/`Write`/`Edit` tools don’t work in Docker** ([#1096](https://github.com/moltis-org/moltis/issues/1096))
    - **严重程度: 高**。Docker是主流部署方式，核心文件操作工具在Docker下失效将严重阻碍Agent的正常工作。**暂无关联PR**。

- **严重 - [P1]:** **[Bug]: Podman is not working via Moltis** ([#1095](https://github.com/moltis-org/moltis/issues/1095))
    - **严重程度: 中高**。作为重要的Docker替代品，Podman支持缺失限制了用户的选择。**暂无关联PR**。

- **中等 - [P2]:** **[Bug]: Telegram edit-in-place streaming mixes intermediate output into final reply** ([#1097](https://github.com/moltis-org/moltis/issues/1097))
    - **严重程度: 中**。影响Telegram渠道的交互清晰度，已有修复PR ([#1099](https://github.com/moltis-org/moltis/pull/1099))。

- **中等 - [P2]:** **[Bug]: De-Preferring Models** ([#1094](https://github.com/moltis-org/moltis/issues/1094))
    - **严重程度: 中**。用户无法“取消偏好”某个模型，可能是模型选择逻辑上的缺陷。**暂无关联PR**。

#### 6. 功能请求与路线图信号

尽管今日以Bug修复为主，但仍有一些功能请求透露出社区对项目未来的期望。

- **优先级高 (很可能纳入下个版本):**
    - **Agent内置Moltis文档:** [Issue #1028](https://github.com/moltis-org/moltis/issues/1028) (已关闭) 要求Agent预置项目文档访问权限，这属于Agent自身能力的增强，提升“开箱即用”感，其关闭表明该功能已完成。
    - **Activity日志控制:** [Issue #1092](https://github.com/moltis-org/moltis/issues/1092) 要求增加配置项控制工具调用日志的显示。对应的PR [#1093](https://github.com/moltis-org/moltis/pull/1093) 已存在，该功能几乎可以确定会落地。

- **优先级中 (社区呼声):**
    - **Web UI文件附件支持:** [Issue #1036](https://github.com/moltis-org/moltis/issues/1036) (已关闭) 要求Web UI支持任意文件上传，这显著提升了通用性，其实现是用户界面体验的重要一步。

#### 7. 用户反馈摘要

从今日的Issues和评论中，可以提炼出以下用户反馈：

- **痛点:**
    - **部署环境适配差:** `Docker` 和 `Podman` 用户的体验糟糕（[#1096](https://github.com/moltis-org/moltis/issues/1096), [#1095](https://github.com/moltis-org/moltis/issues/1095)）。用户在评论区明确指出“即使使用最新版本”核心功能仍无法工作，这暴露了测试覆盖率的不足。
    - **交互信息过载:** Telegram用户对“Activity log”混入主消息的行为感到困扰（[#1092](https://github.com/moltis-org/moltis/issues/1092), [#1097](https://github.com/moltis-org/moltis/issues/1097)），他们期望更干净、更智能的实时反馈机制。

- **使用场景:**
    - 用户 `RokkuCode` 在报告模型偏好问题时暗示了多模型切换的复杂场景，表明Moltis被用于涉及不同模型能力对比的深度任务。
    - `s-salamatov` 连续报告和提交关于Telegram渠道的改进，表明其是一个重度Telegram Bot用户，依赖该渠道进行Agent交互。

- **满意点:**
    - 尽管存在Bug，但连续的新版本发布（2天内2个版本）向社区传递了项目活跃维护的信号，用户愿意在出现问题后立刻报告并等待修复。

#### 8. 待处理积压

- **最紧急的待办项:**
    - **修复 [#1096](https://github.com/moltis-org/moltis/issues/1096) 和 [#1095](https://github.com/moltis-org/moltis/issues/1095):** 这两个关于Docker和Podman集成的问题尚无关联PR，且严重影响了核心功能。维护者应优先评估和响应，这可能是版本 `20260603.01` 的回归问题。
    - **合并或驳回 [#1099](https://github.com/moltis-org/moltis/pull/1099), [#1098](https://github.com/moltis-org/moltis/pull/1098), [#1093](https://github.com/moltis-org/moltis/pull/1093):** 三个待合并的PR已经存在了个工作日（至少24小时），它们是解决社区热议问题和稳定性问题的关键。长时间的待合并状态会积压风险，也可能让贡献者感到挫败。建议项目维护者尽快安排代码审查和合并。

- **长期未响应/非紧急议题:**
    - 数据中的议题均已得到快速处理（从创建到关闭或作者回应），暂无长期无人问津的迹象。本次未发现明显的积压问题。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 (2026-06-04)

## 1. 今日速览

过去 24 小时内项目活跃度极高：共处理 44 条 Issue（新开/活跃 22，关闭 22）和 49 条 PR（待合并 28，已合并/关闭 21），无新版本发布。  
社区讨论聚焦于浏览器自动化的稳定性（CDP 超时、浏览器闪退）、上下文压缩的兼容性问题（非字典 source 对象、压缩失败报错），以及记忆/向量存储的长期可靠性（ChromaDB segfault、索引无限膨胀）。  
贡献者提交了多项关键修复与功能，包括技能离线包大小限制提升、飞书/Telegram 通道增强、插件加载器解耦、MiniMax M3 模型内置支持以及内存蒸馏插件（仍在 review）。整体来看，项目正处于**高频迭代与 bug 修复并重**的阶段，健康度良好，但部分严重问题（如 ChromaDB segfault）仍需紧急关注。

## 3. 项目进展（今日合并/关闭的重要 PR）

| PR | 说明 | 类型 |
|----|------|------|
| [#4941](https://github.com/agentscope-ai/QwenPaw/pull/4941) | 提高技能包下载大小上限，修复技能市场 422 错误（关联 [#4928](https://github.com/agentscope-ai/QwenPaw/issues/4928)） | bugfix |
| [#4933](https://github.com/agentscope-ai/QwenPaw/pull/4933) | 处理媒体块中的非字典 source 对象，修复 `'str' object has no attribute 'get'` 导致的上下文压缩崩溃（关联 [#4811](https://github.com/agentscope-ai/QwenPaw/issues/4811)、[#4924](https://github.com/agentscope-ai/QwenPaw/issues/4924)） | bugfix |
| [#4935](https://github.com/agentscope-ai/QwenPaw/pull/4935) | 更新 `reme-ai` 依赖至 v0.3.1.10，修复文件监控 stop/restart 事件未重置的问题 | dependency |
| [#4821](https://github.com/agentscope-ai/QwenPaw/pull/4821) | 飞书通道新增群组会话共享模式（`share_session_in_group`），遵循微信通道的既有模式 | feature |
| [#4737](https://github.com/agentscope-ai/QwenPaw/pull/4737) | Telegram 通道新增交互式工具审批卡片（InlineKeyboardMarkup + CallbackQuery） | feature |
| [#4942](https://github.com/agentscope-ai/QwenPaw/pull/4942) | 更新项目路线图文档（内容未详，系常规维护） | docs |
| [#4943](https://github.com/agentscope-ai/QwenPaw/pull/4943) | 新增 55 个 P0 集成测试用例，覆盖 agent 路由、技能 CRUD、MCP OAuth 等场景 | test |

**总结**：上下文压缩崩溃的根本原因（非 dict source）已成功定位并修复；飞书/Telegram 通道的功能对齐进度加速；技能市场下载限制已被解除；测试覆盖率显著提升。整体项目在稳定性与功能完整性上均有实质进步。

## 4. 社区热点（讨论最活跃的 Issues）

| Issue | 评论数 | 核心诉求 | 分析 |
|-------|--------|----------|------|
| [#4919](https://github.com/agentscope-ai/QwenPaw/issues/4919) | 6 | `browser_use` 启动失败：managed CDP 超时 + Chrome/Edge 浏览器闪退 | 用户尝试了三种启动方式均失败，最终靠 npm 版 playwright-cli 兜底。反映浏览器环境适配（特别是 Windows 上多浏览器共存、profile 隔离）仍是痛点。已有修复 PR [#4944](https://github.com/agentscope-ai/QwenPaw/pull/4944) 处于 OPEN 状态。 |
| [#3470](https://github.com/agentscope-ai/QwenPaw/issues/3470) | 6 | QwenPaw 是否会引入类似 Hermes Agent 的自我进化功能（已关闭） | 虽然已关闭，但双倍评论数表明社区对此兴趣浓厚，且存在 [#3516](https://github.com/agentscope-ai/QwenPaw/issues/3516) 同类请求，可视为长期路线图信号。 |
| [#3854](https://github.com/agentscope-ai/QwenPaw/issues/3854) | 5 | ChromaDB Rust 绑定段错误（SIGSEGV）杀死整个进程，单会话崩溃 45+ 次 | 严重稳定性问题，影响 Ubuntu 25.10 + Python 3.13 用户。缺乏 Python 层异常捕获，进程直接退出。至今无关联 PR，积压已超 38 天。 |
| [#3905](https://github.com/agentscope-ai/QwenPaw/issues/3905) | 5 | Dream agent 记忆管理任务执行后 MEMORY.md 无实际内容，记忆闭环未完成 | 用户期望 Dream 能正常沉淀记忆，但仅输出空模板。可能与文件路径、触发时机有关。 |
| [#4924](https://github.com/agentscope-ai/QwenPaw/issues/4924) | 4 | 上下文压缩自动触发失败：`'str' object has no attribute 'get'` | 已确认由旧格式 file block 引起，已通过 [#4933](https://github.com/agentscope-ai/QwenPaw/pull/4933) 修复。 |

**分析**：浏览器自动化与上下文压缩是当前用户最头疼的两个领域；自我进化功能则是社区呼声最高的“未来方向”。

## 5. Bug 与稳定性

按严重程度排列（★ 越多越严重），已标注是否存在修复 PR。

| 严重度 | Issue | 描述 | 关联 PR | 状态 |
|--------|-------|------|---------|------|
| ★★★★★ | [#3854](https://github.com/agentscope-ai/QwenPaw/issues/3854) | ChromaDB Rust 绑定 SIGSEGV 杀死进程，单会话 45+ 次崩溃（Linux, Python 3.13） | 无 | OPEN，积压 38 天 |
| ★★★★ | [#4795](https://github.com/agentscope-ai/QwenPaw/issues/4795) | 向量索引无限膨胀至 37GB，`memory_search` 卡死崩溃，累计 10+ 次 | 无 | OPEN，用户已自行删除索引恢复 |
| ★★★★ | [#4888](https://github.com/agentscope-ai/QwenPaw/issues/4888) | Dream agent 使用相对路径 write_file 覆盖其他 workspace 的 MEMORY.md | [#4936](https://github.com/agentscope-ai/QwenPaw/pull/4936) | OPEN（PR 已提交） |
| ★★★ | [#4919](https://github.com/agentscope-ai/QwenPaw/issues/4919) | browser_use 启动失败：CDP 超时 + 浏览器闪退（Windows） | [#4944](https://github.com/agentscope-ai/QwenPaw/pull/4944) | OPEN（PR 已提交） |
| ★★★ | [#4924](https://github.com/agentscope-ai/QwenPaw/issues/4924) | 上下文压缩因旧格式 file block 失败 | [#4933](https://github.com/agentscope-ai/QwenPaw/pull/4933) | **已合并** |
| ★★ | [#4811](https://github.com/agentscope-ai/QwenPaw/issues/4811) | 消息包含内联 source URL 时压缩崩溃（同上根因） | [#4933](https://github.com/agentscope-ai/QwenPaw/pull/4933) | **已合并** |
| ★★ | [#4916](https://github.com/agentscope-ai/QwenPaw/issues/4916) | 创建备份时因浏览器缓存文件 PermissionError 失败（Windows） | 无 | OPEN |
| ★★ | [#4889](https://github.com/agentscope-ai/QwenPaw/issues/4889) | Tauri 桌面版插件加载器未启动（`pip install` 在 PyInstaller 环境超时） | [#4900](https://github.com/agentscope-ai/QwenPaw/pull/4900) | OPEN（PR 已提交） |
| ★ | [#4928](https://github.com/agentscope-ai/QwenPaw/issues/4928) | 技能市场下载报错 422（响应体过大） | [#4941](https://github.com/agentscope-ai/QwenPaw/pull/4941) | **已合并** |

> 注：ChromaDB segfault 问题长期未解，社区存在大量隐形成本。建议优先分配人力排查 Rust 绑定版本兼容性或提供 Python 兜底 fallback。

## 6. 功能请求与路线图信号

| Issue/PR | 描述 | 信号强度 |
|----------|------|----------|
| [#3995](https://github.com/agentscope-ai/QwenPaw/issues/3995) | 增强记忆管理：生命周期归档、冲突检测、RAG 混合搜索 | ★★★☆（11 个点赞，反复被提及） |
| [#4640](https://github.com/agentscope-ai/QwenPaw/issues/4640) | 会话结束自动总结钩子（Pre-hook Memory Archiving） | ★★★☆（有详细提案，无 PR） |
| [#3801](https://github.com/agentscope-ai/QwenPaw/issues/3801) | 模型自适应上下文（无需手动限制） | ★★★（长期需求，无 PR） |
| [#4001](https://github.com/agentscope-ai/QwenPaw/issues/4001) | 对话中删除单条消息（类似微信） | ★★★（实用性强，UI 改进） |
| [#4208](https://github.com/agentscope-ai/QwenPaw/issues/4208) | 是否支持 mem0 内存系统 | ★★☆（用户询问，无官方回复） |
| [#3944](https://github.com/agentscope-ai

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 ZeptoClaw 项目数据，我为您生成 2026-06-04 的项目动态日报。

---

## ZeptoClaw 项目日报 (2026-06-04)

### 1. 今日速览

今日 ZeptoClaw 项目进入了一个**静默维护期**。过去24小时内，项目没有产生任何新的 Issue 讨论、代码提交合并或版本发布，这表明项目核心开发可能暂时停顿，或开发者正在进行深度编码尚未提交。然而，项目活跃度并非完全为零：**自动化依赖更新（Dependabot）异常活跃，一口气提交了16个 Pull Request (PR)**，覆盖了 Rust、JavaScript、Docker 和 GitHub Actions 等多个技术栈。虽然这些 PR 均未合并，但反映了项目在持续跟踪上游依赖的最新变化，保持了良好的**技术债务清理意识**。总体而言，今日项目活跃度评估为“**低**”（主要源于自动化操作），社区互动为“**无**”。

### 2. 项目进展

今日**无任何 PR 被合并或关闭**。所有16个已打开的 PR 均处于等待审核阶段。

尽管没有实质性代码合并，但这些 PR 的提出本身就代表了项目维护的进展：
- **基础设施稳健性提升**：多个 PR 尝试更新 Docker 镜像 (`rust:1.96-slim-trixie` PR #613， [链接](qhkm/zeptoclaw PR #613)) 和核心 Rust 库 (`tokio`, `serde_json`, `scraper`等)，旨在修复潜在安全漏洞和兼容性问题。
- **Web 面板依赖同步**：针对 `/panel` 和文档站点的 JavaScript 依赖（如 `react`, `astro`, `tailwindcss`）也进行了更新，确保前端技术栈维持在较新状态。
- **CI/CD 流程优化**：更新了 `docker/login-action`、`codecov/codecov-action` 等 GitHub Actions 组件，有助于提升自动化构建与测试流程的稳定性和效率。

然而，项目距离功能特性上的“向前迈进”尚有距离，目前主要停留在“稳固基础”的阶段。

### 3. 社区热点

今日社区**缺乏讨论热点**。所有16个活跃的 Pull Request 均来自 `dependabot[bot]`，没有来自真实用户的评论或“点赞”。这反映出项目目前处于一个功能开发和社区讨论的真空期。对这些 PR 的诉求主要是维持项目在现代软件生态中的兼容性和安全性，而非引入新功能或解决用户痛点。

### 4. Bug 与稳定性

今日**无新的 Bug 报告**。在发布的 PR 中，也没有明确指出任何 Bug 修复。不过，分析这些依赖更新 PR 的摘要可以发现一些潜在的稳定性信息：
- **Tokio 更新** (`1.52.1` -> `1.52.3`， PR #623， [链接](qhkm/zeptoclaw PR #623))：摘要中提到“Fixed”，表示此版本包含了针对 Tokio 运行时的一些修复，升级后可能解决某些特定场景下的并发或性能问题。
- **rpassword 更新** (`7.4.0` -> `7.5.2`， PR #625， [链接](qhkm/zeptoclaw PR #625))：摘要中提到修复了一个 Unicode 解析问题，对密码输入的安全性有积极影响。

整体来看，项目稳定性主要通过常规依赖更新来间接保障，目前没有紧急的稳定性危机。

### 5. 功能请求与路线图信号

今日**无任何新的功能请求**。从现有数据判断，项目未来版本的路线图尚不清晰。现有的16个 PR 全部是“维护性”的，没有涉及新架构、新API或新功能。这暗示项目可能处于核心功能开发完成后的打磨期或转型规划期。下一版本的焦点很可能是集成这些依赖更新，而非推出颠覆性新功能。

### 6. 用户反馈摘要

由于今日**无用户评论**，无法提供有效的用户反馈摘录。项目当前缺乏来自用户的声音，这对于判断产品与市场需求的契合度是一个盲点。

### 7. 待处理积压

虽然今日无长期未响应的 Issue，但**16个待合并的 Dependabot PR 本身就是一种“积压”**。这些 PR 虽然技术风险较低，但长期不合并会导致项目与上游依赖的“版本差距”越来越大，增加未来一次性合并时的风险。建议项目维护者安排一次集中的“**依赖更新日**”，批量审核并合并这批 PR，以保持项目健康度。

- **重点关注 PR**：
    - **Rust 镜像版本更新** (#613， [链接](qhkm/zeptoclaw PR #613))：这是基础运行时环境的重大版本升级（1.95 -> 1.96），涉及面广，需优先审核。
    - **核心库 `scraper` 更新** (#620， [链接](qhkm/zeptoclaw PR #620))：作为可能的核心依赖，`0.26.0` 到 `0.27.0` 的版本跳跃需关注其 Breaking Changes。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目日报 | 2026-06-04

---

## 1. 今日速览

过去 24 小时内 ZeroClaw 保持极高活跃度：共产生 **30 条 Issue 更新**（新开 / 活跃 27，关闭 3）和 **50 条 PR 更新**（待合并 47，已合并 / 关闭 3）。社区关注点集中在**安全架构升级**（可插拔安全层、OIDC 认证）、**TUI 终端界面**（zerocode）以及 **v0.8.0 发布前阻断问题**。但合并交付速度明显滞后于提交速度，接近 94% 的 PR 仍处于待合并状态，项目整体处于**快速迭代但阻塞积压**阶段。

---

## 2. 版本发布

**无新版本发布。** 当前主要里程碑为 v0.8.0（[Issue #7112](https://github.com/zeroclaw-labs/zeroclaw/issues/7112)），该版本涉及配置、工具调用解析器 Stable-tier 晋升及多项阻断问题，尚在推进中。

---

## 3. 项目进展

今日仅 **3 个 PR 被合并 / 关闭**，较昨日趋于收缩：

| PR | 类型 | 内容 | 合并状态 |
|----|------|------|----------|
| [#7181](https://github.com/zeroclaw-labs/zeroclaw/pull/7181) | fix(update,skills) | 加强 `remove_file` 错误日志与路径遍历防护 | 已合并 |
| [#7168](https://github.com/zeroclaw-labs/zeroclaw/issues/7168) | Feature → Issue | 会话分支功能（fork 对话） | 已关闭（非 PR，为重复 Issue） |
| [#7167](https://github.com/zeroclaw-labs/zeroclaw/issues/7167) | Feature → Issue | 同上，重复 | 已关闭 |

其余 **47 个 PR 均处于开放待合并状态**，包括关键安全修复（[#7160](https://github.com/zeroclaw-labs/zeroclaw/pull/7160) 配置加载容错）、新提供商（[#7136](https://github.com/zeroclaw-labs/zeroclaw/pull/7136) Kilo AI Gateway）以及持久化 RPC 会话（[#7182](https://github.com/zeroclaw-labs/zeroclaw/pull/7182)）等，项目健康度受合并效率影响。

---

## 4. 社区热点

今日最受关注的两个 Issue **均来自安全架构讨论**，各有 3 条评论：

- **[#7142](https://github.com/zeroclaw-labs/zeroclaw/issues/7142) [Enhancement, Security]**: 提出将安全强制层暴露为可插拔 provider 接口，作为 v0.9.0 跟踪 issue。社区围绕如何设计统一 trait 展开讨论，涉及 Landlock、Bubblewrap 等多后端集成。
- **[#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) [Enhancement, Security]**: 为 RPC/WSS 传输层添加 OIDC 认证 provider 支持，同样是 v0.9.0 跟踪项。表明社区对**企业级身份集成**的需求强烈。

这两个 Issue 均标有 `type:rfc`，代表了项目安全架构未来的演进方向，且可能与当前的大量安全相关 PR（[#7130](https://github.com/zeroclaw-labs/zeroclaw/issues/7130) forbid unsafe_code、[#6996](https://github.com/zeroclaw-labs/zeroclaw/issues/6996) 沙箱策略）形成协同。

---

## 5. Bug 与稳定性

今日报告 **8 个新 Bug**，按严重程度排列：

| 严重级别 | Issue | 描述 | 关联修复 PR |
|----------|-------|------|-------------|
| 🚨 **S1 – 工作流阻塞** | [#7179](https://github.com/zeroclaw-labs/zeroclaw/issues/7179) | RPC 会话默认 10 分钟闲置即回收，导致长时间对话中断 | 未关联 |
| 🚨 **S1** | [#7173](https://github.com/zeroclaw-labs/zeroclaw/issues/7173) | Quickstart 渠道 webhook 配置缺少端口字段，启动失败 | 未关联 |
| 🚨 **S1** | [#7125](https://github.com/zeroclaw-labs/zeroclaw/issues/7125) | TUI (zerocode) 在守护进程断开后完全冻结，需强制退出 | 未关联 |
| ⚠️ **S2 – 行为降级** | [#7133](https://github.com/zeroclaw-labs/zeroclaw/issues/7133) | `forbidden_path_argument` 在引号/heredoc 命令中对 `~` 令牌误报 | 未关联 |
| ⚠️ **S2** | [#7151](https://github.com/zeroclaw-labs/zeroclaw/issues/7151) | 观测工具调用 telemetry 泄漏到聊天 WebSocket，产生永久“unknown”工具卡 | 未关联 |
| ⚠️ **S2** | [#7126](https://github.com/zeroclaw-labs/zeroclaw/issues/7126) | Web UI "Clear all" 仅清除前端渲染，未删除后端会话历史 | 未关联 |
| 🔹 **S3 – 小问题** | [#6702](https://github.com/zeroclaw-labs/zeroclaw/issues/6702) | 仪表盘会话气泡中工具调用卡片后产生多余空白行 | 未关联 |
| 🔹 **S3** | [#7157](https://github.com/zeroclaw-labs/zeroclaw/issues/7157) | 时间戳被渲染进消息气泡内部而非独立元数据 | 未关联 |
| 🔹 **S3** | [#7156](https://github.com/zeroclaw-labs/zeroclaw/issues/7156) | Reload banner 持续显示 `gateway.paired_tokens (secret)` 从未清除 | 未关联 |

**关键风险**：S1 级 Bug 均无对应修复 PR，可能会阻塞 v0.8.0 发布。特别是 [#7179](https://github.com/zeroclaw-labs/zeroclaw/issues/7179) 的会话回收机制与 [#7182](https://github.com/zeroclaw-labs/zeroclaw/pull/7182)（移除闲置 TTL）直接冲突，需加速合并。

---

## 6. 功能请求与路线图信号

今日收到 **15 个新功能请求**，聚焦以下方向：

| 方向 | 典型 Issue/PR | 纳入版本可能性 |
|------|--------------|----------------|
| **安全架构** | [#7142](https://github.com/zeroclaw-labs/zeroclaw/issues/7142) 可插拔安全层、[#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) OIDC 认证 | v0.9.0 明确跟踪 |
| **沙箱策略** | [#6996](https://github.com/zeroclaw-labs/zeroclaw/issues/6996) 文件系统/网络限制 RFC | 需 maintainer 评审 |
| **Web UI 增强** | [#7138](https://github.com/zeroclaw-labs/zeroclaw/issues/7138) 文件上传 UI、[#7137](https://github.com/zeroclaw-labs/zeroclaw/issues/7137) 斜杠命令 | 可能 v0.8.1 |
| **开发者体验** | [#7131](https://github.com/zeroclaw-labs/zeroclaw/issues/7131) OpenRPC 规范导出、[#7184](https://github.com/zeroclaw-labs/zeroclaw/issues/7184) i18n 子模块 | 持续改进 |
| **提供商** | [#7136](https://github.com/zeroclaw-labs/zeroclaw/pull/7136) Kilo AI Gateway | 即将合并 |
| **运行时** | [#7188](https://github.com/zeroclaw-labs/zeroclaw/pull/7188) Cron 相对延迟、[#7189](https://github.com/zeroclaw-labs/zeroclaw/pull/7189) 调度器工具保护 | 高优先级 |

**路线图信号**：v0.8.0 的配置清理（[#7112](https://github.com/zeroclaw-labs/zeroclaw/issues/7112)）与 v0.8.1 的渠道/提供商队列（[#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)）并行推进，同时 v0.9.0 安全架构设计已开始跟踪。社区对**确认式高风险命令执行**（[#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155)）也有明确需求。

---

## 7. 用户反馈摘要

从今日 Issues 中提炼典型用户声音：

- **感谢与赞赏**：用户 `sbenedetto` 在 [#7143](https://github.com/zeroclaw-labs/zeroclaw/issues/7143) 中表示“很高兴看到基于 Rust 的 agent 运行时资源消耗远低于其他系统”，表达了对项目轻量特性的认可。
- **工作流受阻**：多位用户遭遇 S1 级阻塞问题：
  - `tidux` 指出 RPC 会话 10 分钟回收导致长对话中断（[#7179](https://github.com/zeroclaw-labs/zeroclaw/issues/7179)）
  - `eugeneb50` 反馈 quickstart 配置端口缺失，创建 agent 后无法启动（[#7173](https://github.com/zeroclaw-labs/zeroclaw/issues/7173)）
  - `NiuBlibing` 报告 TUI 在守护进程断开后完全冻结，需强制退出（[#7125](https://github.com/zeroclaw-labs/zeroclaw/issues/7125)）
- **体验抱怨**：用户 `NiuBlibing` 连续提出多个 UI 问题（时间戳渲染、清除不彻底、遥测泄漏、reload banner 残留），表明 Web 仪表盘体验尚不成熟。
- **功能期望**：用户 `NiuBlibing` 同时提出文件上传 UI、斜杠命令、高风险命令确认等需求，反映出用户希望 ZeroClaw 达到 Claude Code 级交互水平。
- **i18n 反馈**：用户 `xianshishan` 指出聊天工具栏按钮在切换语言后仍显示英文（[#7139](https://github.com/zeroclaw-labs/zeroclaw/issues/7139)），多语言支持存在缺漏。

---

## 8. 待处理积压

以下 Issue/PR 长期未得到 maintainer 跟进或缺少关键决策，提醒关注：

| 项目 | 创建时间 | 标签 | 重要性 |
|------|----------|------|--------|
| [#6996](https://github.com/zeroclaw-labs/zeroclaw/issues/6996) RFC: 沙箱文件系统/网络限制 | 2026-05-28 | `needs-maintainer-review` | ⭐ 沙箱安全基础 |
| [#6826](https://github.com/zeroclaw-labs/zeroclaw/issues/6826) Tracker: ZeroClaw TUI | 2026-05-21 | `status:in-progress` | ⭐ 终端界面核心跟踪 |
| [#6825](https://github.com/zeroclaw-labs/zeroclaw/issues/6825) Tracker: TUI UX | 2026-05-21 | `status:in-progress` | ⭐ 用户体验 |
| [#7112](https://github.com/zeroclaw-labs/zeroclaw/issues/7112) v0.8.0 release queue | 2026-06-02 | `status:accepted` | ⭐ 里程碑阻塞 |
| [#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970) v0.8.1 PR queue | 2026-05-27 | `status:in-progress` | ⭐ 迭代队列 |
| [#7128](https://github.com/zeroclaw-labs/zeroclaw/issues/7128) 清理 `zeroclaw onboard` 废弃引用 | 2026-06-03 | `documentation` | 📄 文档一致性 |
| [#7130](https://github.com/zeroclaw-labs/zeroclaw/issues/7130) forbid unsafe_code 工作区 | 2026-06-03 | `security` | 🔒 安全合规 |

**建议行动**：
1. 优先评审 [[#6996]](https://github.com/zeroclaw-labs/zeroclaw/issues/6996) 沙箱 RFC，这是安全架构升级的前置条件。
2. 加速合并 [#7182](https://github.com/zeroclaw-labs/zeroclaw/pull/7182) 和 [#7160](https://github.com/zeroclaw-labs/zeroclaw/pull/7160) 以缓解当前 S1 Bug。
3. 对 v0.8.0 阻断问题（[#7112]）组织专题讨论，明确发布截止日。

---

> 数据来源：ZeroClaw GitHub 仓库 (github.com/zeroclaw-labs/zeroclaw) 2026-06-04

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*