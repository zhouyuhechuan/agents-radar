# OpenClaw 生态日报 2026-06-14

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-14 02:54 UTC

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

# OpenClaw 项目日报 — 2026-06-14

---

## 1. 今日速览

过去 24 小时内，项目保持极高活跃度：**500 条 Issue 更新（399 新开/活跃，101 关闭）** 与 **500 条 PR 更新（301 待合并，199 已合并/关闭）**，表明社区反馈密集且贡献者持续跟进。版本方面发布两个 Beta 版（v2026.6.7-beta.1、v2026.6.8-beta.1），重点增强 Telegram、WhatsApp、Slack 等渠道的消息交付健壮性。然而，多个 **P1/P0 级 Bug**（如网关内存泄漏、子代理静默失败、多代理会话锁冲突）仍在讨论或等待修复，整体处于“快速迭代中需加固稳定性”的阶段。

---

## 2. 版本发布

### v2026.6.8-beta.1

- **Highlights**  
  - Telegram 和 WhatsApp 渠道交付更丰富、更健壮：Telegram 支持结构化富文本（表格、列表、可展开引用块）、CLI 后端保留提示语、自动迁移旧的原生草稿、更安全的富媒体边界；WhatsApp 同步改进。
  - 其他底层修复：随附优化。

### v2026.6.7-beta.1

- **Highlights**  
  - 跨 Slack、Telegram、出站媒体、静默回复、进度草稿和分页操作结果的信道交付更加紧凑：相同频道的 Slack 最终回复持久化在对话记录中；顶层 `image` 消息工具可发送附件；Telegram 可展开引用块及 spool 机制改进。
  - 安全性、稳定性修补。

**迁移注意事项**：两个版本均为 Beta，建议用户在测试环境验证后再升级生产部署。无明确破坏性变更声明，但涉及草稿迁移和富媒体边界变更，注意检查自定义 Telegram 扩展的兼容性。

---

## 3. 项目进展

今日共有 **199 个 PR 被合并或关闭**，涵盖功能增强、Bug 修复、文档完善。以下选取几个代表性合并项：

- **#91824** [CLOSED] —— `fix(agents): add usage guidance to sessions_spawn tool description`  
  为 `sessions_spawn` 工具添加使用指导，帮助模型正确决策何时委托子代理，避免大任务绕过子代理通道。
- **#91403** [CLOSED] —— `fix(openai-completions): route empty stop with no content into error path`  
  解决 OpenAI 兼容提供商返回 `finish_reason: stop` 但无内容时，渠道发送空白回复的问题。
- **#90991** [CLOSED] —— `Cron scheduled trigger contaminates global runtime state`  
  修复 Cron 触发污染全局状态导致系统过载的 P1 问题，提升定时任务可靠性。
- **#45698** [CLOSED] —— `Control UI becomes progressively stuck`  
  解决控制界面长时间打开后卡顿的回归问题。

此外，大量新 PR 被提交（如 #92846 Telegram 发送者 isBot 字段、#92824 Codex OAuth 媒体路由、#92840 飞书 HTTP 服务器关闭等待等），表明社区持续贡献。

---

## 4. 社区热点

今日讨论最活跃、评论数最高的 Issue 反映出用户对 **子代理可靠性** 和 **安全注入** 的高度关注：

| Issue | 标题 | 评论数 | 核心诉求 |
|-------|------|--------|----------|
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | [Bug]: Subagent completion silently lost | 19 | 子代理超时后无重试、无通知、无自动重启，结果静默丢失。影响 Telegram 论坛模式。 |
| [#48788](https://github.com/openclaw/openclaw/issues/48788) | feat: centralized filename encoding utility | 18 | 飞书中文字符乱码的广泛解决方案，要求中心化文件名编码工具处理多编码（Shift-JIS、GB18030 等）。 |
| [#48183](https://github.com/openclaw/openclaw/issues/48183) | [Bug]: Feishu monitor state cleanup incomplete | 18 | 飞书插件监控停止时 HTTP 服务器 Map 未等待关闭即删除条目，导致内存泄漏和端口冲突。 |
| [#45740](https://github.com/openclaw/openclaw/issues/45740) | gh-issues skill: untrusted issue body injected | 13 | `gh-issues` 技能将非受信任的 Issue 正文直接注入子代理提示，存在严重安全风险（提示注入攻击）。 |
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | Critical: Gateway Memory Leak (RSS 350MB→15.5GB) | 10 | 网关进程 2-3 天内 RSS 从 350MB 增长至 15.5GB，触发 OOM 杀进程，导致反复重启循环。 |

**分析**：用户对“静默失败”容忍度低，期望明确的错误反馈和自动恢复机制；安全方面，外部内容注入子代理提示是高风险模式，急需加入验证或隔离层。

---

## 5. Bug 与稳定性

按严重程度排列今日报告中关键 Bug（含历史积压，今日仍有活跃讨论）：

| 严重级别 | Issue | 标题 | 状态 / 是否有 Fix PR |
|----------|-------|------|----------------------|
| **P0** | [#91588](https://github.com/openclaw/openclaw/issues/91588) | Gateway Memory Leak — RSS grows from 350MB to 15.5GB | OPEN，暂无关联 Fix PR，社区紧急要求修复 |
| **P1** | [#44925](https://github.com/openclaw/openclaw/issues/44925) | Subagent completion silently lost | OPEN，标记 `no-new-fix-pr`，等待评审 |
| **P1** | [#48003](https://github.com/openclaw/openclaw/issues/48003) | Steer mode does not inject messages mid-turn | OPEN，有 `linked-pr-open`（但未合并） |
| **P1** | [#43367](https://github.com/openclaw/openclaw/issues/43367) | Multi-agent orchestration unstable (config overwrite, session-lock) | OPEN，多个子问题未解决 |
| **P1** | [#40540](https://github.com/openclaw/openclaw/issues/40540) | `openclaw update` fails with EBUSY on Windows | OPEN，等待产品决策 |
| **P1** | [#41744](https://github.com/openclaw/openclaw/issues/41744) | Feishu: read image tool result loses media | OPEN，有 `linked-pr-open` |
| **P2** | [#48183](https://github.com/openclaw/openclaw/issues/48183) | Feishu monitor state cleanup memory leak | 有 PR #48588（OPEN，stale）待合并 |
| **P2** | [#45740](https://github.com/openclaw/openclaw/issues/45740) | gh-issues skill untrusted body injection | OPEN，需安全评审 |
| **P2** | [#90991](https://github.com/openclaw/openclaw/issues/90991) | Cron global state contamination | **已关闭**（已修复） |
| **P2** | [#45698](https://github.com/openclaw/openclaw/issues/45698) | Control UI stuck after prolonged use | **已关闭**（已修复） |

**小结**：内存泄漏和子代理可靠性是当前最紧迫的稳定性问题；多个 P1 Bug 虽已立项但缺乏明确 Fix PR，维护者需加速推进。

---

## 6. 功能请求与路线图信号

以下功能需求获得较多社区支持，且部分已有关联 PR 或处于可实施状态，可能被纳入后续版本：

- **#42475** — Per-agent cost budget enforcement at gateway level（P2，Gateway 级别按代理设置日/月预算），已有 `fix-shape-clear` 标记。
- **#42840** — Add MathJax/LaTeX rendering to Control UI（P2，7 👍），提升数学公式显示体验。
- **#39979** — Path-scoped RWX permissions for exec and file tools（P2，替代二进制白名单的场景）。
- **#40786** — Add .gitignore-like exclude patterns to backup CLI（P2，避免备份 node_modules 和敏感文件）。
- **#45608** — Pre-reset agentic memory flush（P1，4 👍），解决 `/new` 或每日重置时丢失记忆的问题，已有 `fix-shape-clear`。
- **#43015** — `message.send` schema overexposes poll/components/modal（P1，3 👍），导致 GPT 自动填充不必要字段而失败，已有 `fix-shape-clear`。

结合已有 PR 信号（如 #91632 增加工具搜索目录模式、#86655 推进 Claude Bridge 扩展），下一版本可能侧重新增模型支持与配置灵活性。

---

## 7. 用户反馈摘要

从 Issue 描述和评论中提炼的真实用户痛点与场景：

- **“子代理任务悄无声息地消失，没有重试，也没有错误通知。”**（#44925）—— 用户期待至少重试或回退机制，无法容忍静默失败。
- **“飞书图片用 `read` 工具读取成功，但最终回复里图片丢失。”**（#41744）—— 渠道间媒体传递不一致。
- **“`gh-issues` 技能直接拼装非信任的 Issue 正文到子代理提示里，这是典型提示注入入口。”**（#45740）—— 安全团队担忧。
- **“`/new` 重置会话后，成本仪表盘不统计归档文件，导致严重低估花费。”**（#46252）—— 成本管控失真。
- **“跨 Slack/Telegram 的多代理群聊中，自然语言规则训练不稳定，不同代理表现不一致。”**（#41366）—— 多模态规则同步差。
- **“`openclaw update` 在 Windows 下因 EBUSY 失败，无法自己更新自己。”**（#40540）—— Windows 用户部署障碍。
- **“控制 UI 长时间打开后越来越卡，不是渠道或模型问题。”**（#45698，已修复）—— 用户对 Web UI 性能敏感。
- **“开启了 `tools.elevated.enabled: true` 后，所有 exec 调用都路由到网关主机，即使没有提权标志。”**（#46786）—— 权限模型混乱。

---

## 8. 待处理积压

以下 Issue/PR 创建超过 3 个月，仍处于开放状态，且缺乏有效推进，提请维护者重点关注：

### 长期未解决的 Issue

| Issue | 创建日期 | 标题 | 状态标记 |
|-------|----------|------|----------|
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | 2026-02-03 | Memory Trust Tagging by Source | `stale`, `needs-product-decision` |
| [#38327](https://

---

## 横向生态对比

# AI智能体与个人AI助手开源生态横向对比分析报告（2026-06-14）

---

## 1. 生态全景

当前个人AI助手/自主智能体开源生态正处于 **快速迭代与分化并行** 的阶段。核心项目（如OpenClaw）以极高的社区活跃度牵引生态演进，聚焦消息交付健壮性、子代理可靠性与安全注入防护；与此同时，一批差异化项目（如Hermes Agent、ZeroClaw、NanoBot）在**记忆机制、多模态交互、自动化运维、插件系统**等方向密集创新，社区贡献者热情高涨。整体呈现“一个中心（OpenClaw参照系）+多个特色分支”的格局，但**稳定性问题（内存泄漏、静默失败、配置失效）仍是各项目共同面临的共性挑战**。

---

## 2. 各项目活跃度对比

| 项目名称 | Issues当日更新(新开/活跃/关闭) | PR当日更新(待合并/合并关闭) | 版本发布 | 整体健康度 | 核心阶段 |
|---|---|---|---|---|---|
| **OpenClaw** | 500 (399新开/活跃, 101关闭) | 500 (301待合并, 199合并/关闭) | 2个Beta | 🟢 极高活跃，稳定性需加固 | 快速迭代+稳定性修复 |
| **NanoBot** | 未明确统计（约4+活跃） | 约14待合并, 约5合并关闭 | 无 | 🟢 高活跃，维护者响应快 | 功能开发+密集bug修复 |
| **Hermes Agent** | 50 (44新开/活跃, 6关闭) | 50 (48待合并, 2合并/关闭) | 无 | 🟡 极高活跃，PR积压严重 | 功能扩展+社区贡献爆发 |
| **PicoClaw** | 2 (1新开/活跃, 1关闭) | 7 (2待合并, 5合并/关闭) | 1个nightly | 🟢 中等活跃，迭代稳健 | 国际化+多模态修复 |
| **NanoClaw** | 1 (误操作关闭) | 6 (2待合并, 4合并/关闭) | 无 | 🟡 内部开发冲刺期，社区互动少 | 核心重构+SDK升级 |
| **NullClaw** | 0新, 1活跃 | 1待合并, 0合并 | 无 | 🟡 中等活跃，聚焦单一严重bug | Bug修复+社区关注 |
| **IronClaw** | 0新 (1长期活跃) | 22 (17待合并, 5合并/关闭) | 无 | 🟢 高活跃，核心功能攻坚 | 附件链路+Slack审批修复 |
| **LobsterAI** | 0新 (4个stale问题) | 2 (0待合并, 2合并/关闭) | 无 | 🔴 低活跃，积压严重 | 清理旧PR，但社区响应差 |
| **Moltis** | 1新开/活跃 | 3待合并, 0合并 | 无 | 🟡 中等活跃，OAuth修复关键 | 外部服务集成兼容性 |
| **CoPaw (QwenPaw)** | 8 (7新开/活跃, 1关闭) | 8 (6待合并, 2合并/关闭) | 无 | 🟡 中等活跃，多语言扩展+bug修复 | 国际化+桌面端性能 |
| **TinyClaw** | 无活动 | 无活动 | 无 | ⚫ 停滞 | - |
| **ZeptoClaw** | 无活动 | 无活动 | 无 | ⚫ 停滞 | - |
| **ZeroClaw** | 42 (约30+新开/活跃) | 50 (约40+待合并, 10+合并/关闭) | 无 | 🟢 极高活跃，多个S1阻断bug | 核心架构统一+插件RFC |

> 注：健康度分级：🟢 高活跃/健康 🟡 有风险/积压 🔴 低活跃/需关注 ⚫ 无活动

---

## 3. OpenClaw在生态中的定位

**核心参照系地位**：OpenClaw今日产生500条Issue和500条PR更新，远超其他项目，是当前个人AI助手生态中**社区规模最大、迭代速度最快**的标杆项目。其Beta版本发布频率（两日两版）和199个PR合并量体现了强烈的交付能力。

**技术路线差异**：
- **通信渠道健壮性**：OpenClaw在Telegram、WhatsApp、Slack等渠道的消息交付方面投入巨大，强调富文本、引用块、自动迁移等细节，是其他项目（如PicoClaw、NullClaw）的参照对象。
- **子代理可靠性**：OpenClaw的子代理“静默失败”问题（#44925）成为全生态瞩目案例，直接引发社区对重试、通知机制的讨论，影响NanoBot、CoPaw等项目的设计。
- **安全注入防护**：OpenClaw报告的gh-issues技能注入攻击（#45740）被多项目引用，成为典型安全模式。

**社区规模对比**：OpenClaw单日500条Issue，而排名第二的ZeroClaw为42条、Hermes Agent为50条，说明OpenClaw的社区活跃度是其他项目的10倍以上。但其P0级内存泄漏（#91588）和P1级多代理锁冲突（#43367）也暴露了快速迭代下的稳定性代价。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **子代理/多智能体可靠性** | OpenClaw, NanoBot, Hermes Agent, ZeroClaw, IronClaw | 子代理超时静默失败、会话锁冲突、委派模型配置忽略、审批循环等 |
| **记忆与长期上下文管理** | OpenClaw, NanoBot, Hermes Agent, ZeroClaw, CoPaw | `idleCompact`错误总结、自动记忆合并(Dream Mode)、上下文压缩丢失、记忆满容量循环 |
| **渠道/平台兼容性** | OpenClaw, PicoClaw, Moltis, CoPaw, ZeroClaw | Telegram富消息、飞书中文字符乱码、MCP OAuth失败、Zalo Bot支持、中文IM流式卡片 |
| **内存泄漏/性能退化** | OpenClaw, NanoBot, CoPaw, ZeroClaw | Gateway内存泄漏(RSS 350MB→15.5GB)、WebUI卡顿、桌面端启动缓慢、容器outbound.db污染 |
| **安全与配置信任** | OpenClaw, Hermes Agent, ZeroClaw, IronClaw | gh-issues注入攻击、`allowed_tools`对MCP失效、`api_key_env`被忽略、凭据缺失审批顺序错误 |
| **跨平台部署体验** | Hermes Agent, CoPaw, ZeroClaw | Windows安装失败(EBUSY)、Docker VOLUME冲突、macOS桌面应用空白、非TTY回环 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|---|---|---|---|
| **OpenClaw** | 多消息渠道集成、子代理编排、企业级部署 | 中大型团队、需要多平台通讯的用户 | 高扩展的插件化网关，Beta版强调交付健壮性，侧重于“消息中枢” |
| **NanoBot** | 轻量级Agent、WebUI自动化、TTS/多模态 | 个人开发者、快速原型、多模型支持 | 基于Pydantic的模块化配置，强调启动速度和WebUI体验，支持Ollama等本地模型 |
| **Hermes Agent** | 多模型接入(Bedrock/kimi-k2.7-code)、桌面端 | 模型爱好者、跨云用户 | 强大的Provider抽象层，支持自定义模型列表，但PR积压严重 |
| **PicoClaw** | 轻量级开源版、国际化(i18n)、TTS容错 | 嵌入式/边缘设备、中文社区 | 基于Go编写，强调代码质量（显式错误处理），nightly构建快速 |
| **NanoClaw** | 运行时能力扩展、提供者钩子、SDK升级 | 高级开发者、架构定制者 | 引入“能力面”声明和内存持久化框架，侧重于运行时架构创新 |
| **NullClaw** | 定时任务可靠性、JIRA集成(规划中) | 任务自动化用户 | 专注于Cron Agent消息交付修复，社区规模小但需求明确 |
| **IronClaw** | 附件完整支持(Slack/Web)、审批流程优化 | 企业协作用户(Slack/Gmail) | 重客户端架构，侧重“运行管理”和系统反馈，Nightly E2E测试持续失败 |
| **LobsterAI** | MCP集成、技能管理、开源工具链 | 国内开发者、网易生态用户 | 中文社区优先，但上游依赖(OpenClaw)兼容性问题严重，响应迟缓 |
| **Moltis** | MCP OAuth兼容性、Docker部署 | 第三方MCP服务器用户(Notion/Linear) | 专注于OAuth流程修复和容器化，社区讨论集中于外部服务集成 |
| **CoPaw (QwenPaw)** | 多语言(i18n)、Zalo Bot、Kimi API接入 | 东南亚市场、付费AI订阅用户 | 基于Qwen生态，Tauri桌面端性能问题突出，技能管理增强 |
| **ZeroClaw** | 核心架构统一、Dream Mode、插件系统RFC | 高级用户、插件开发者 | 大范围RFC驱动设计，S1级阻断bug多但修复快，强调“Agent学习能力” |

---

## 6. 社区热度与成熟度

**第一梯队（极高活跃/快速迭代）**：
- **OpenClaw**：199个PR合并/关闭，双版本发布，但P0/P1 bug积压。
- **ZeroClaw**：42 Issue + 50 PR，多个S1阻断bug和架构RFC并行，社区讨论深度高。
- **Hermes Agent**：50 PR提交，48个待合并，社区贡献爆发但审查瓶颈明显。

**第二梯队（中高活跃/功能攻坚）**：
- **NanoBot**：维护者响应快，6个社区贡献者PR待合并，核心机制（idleCompact）修复及时。
- **IronClaw**：22 PR，Slack审批循环修复和附件链路贯通，但Nightly E2E测试持续失败。
- **CoPaw**：8 Issue + 8 PR，多语言和渠道扩展诉求明确，但桌面端性能问题未解。

**第三梯队（中等活跃/稳定性巩固）**：
- **PicoClaw**：国际化推进，Evolution Token消耗bug待修复，PR积压较少。
- **NanoClaw**：内部重构冲刺，社区互动少，但PR合并率高。
- **NullClaw**：聚焦单个严重Bug，修复PR已提交。
- **Moltis**：OAuth修复PR待合并，Docker兼容性改善。

**低活跃/停滞**：
- **LobsterAI**：7个stale项超2个月，上游依赖兼容缺失，社区信任下降。
- **TinyClaw/ZeptoClaw**：无活动，项目可能已弃用或休眠。

---

## 7. 值得关注的趋势信号

1. **“Agent记忆学习”成为下一个竞争高地**：多个项目（ZeroClaw的Dream Mode、NanoBot的idleCompact修复、Hermes Agent的Auto Dream请求）均将**长期记忆自动整合与反思**列入优先级。这标志着AI助手从“对话工具”向“持续学习伙伴”的进化拐点。

2. **安全注入与认证授权成为核心隐忧**：OpenClaw的gh-issues注入、ZeroClaw的`allowed_tools`对MCP不生效、IronClaw的Slack审批循环——社区对**不可信内容注入、权限模型混乱**的容忍度极低。未来项目可能普遍引入内容安全过滤器和OAuth凭证管理标准化。

3. **多模态与富媒体交互加速落地**：IronClaw的附件支持贯通、OpenClaw的Telegram富文本、CoPaw的中文IM流式卡片、NanoBot的TTS系统——**文件上传、图像理解、语音合成**正在快速成为标配能力，纯文本交互已无法满足用户期望。

4. **配置系统透明性与可调试性需求爆发**：多处Bug（环境变量未解析、`api_key_env`被忽略、配置项不生效）表明，用户期望**配置生效的实时反馈**和**错误诊断工具**。未来项目可能引入配置验证页面或lint工具。

5. **社区贡献者管理迎来挑战**：Hermes Agent的48个待合并PR、ZeroClaw的“等待作者响应”标签、NanoBot的6个first-time-contributor PR——**贡献者积极性高涨但审查者资源不足**是普遍瓶颈。生态需要更自动化的CI/CD流程或分级review机制。

6. **小语种和新兴市场成为差异化突破口**：CoPaw的越南语/Zalo渠道、PicoClaw的繁体中文、ZeroClaw的飞书支持——**非英语市场用户增长明显**，项目国际化（i18n + 本地IM平台）将成为获取用户的重要策略。

---

*报告生成日期：2026-06-14 | 数据来源：各项目GitHub动态日报 | 分析视角：AI智能体与个人AI助手开源生态*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 NanoBot (HKUDS/nanobot) 项目的 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 2026-06-14 数据，现为您呈上项目动态日报。

---

### NanoBot 项目动态日报 | 2026-06-14

### 1. 今日速览

今日 NanoBot 项目整体**高度活跃**，代码提交与社区讨论均处于高频状态。项目在 **Bug 修复**与**功能增强**方面双管齐下：一方面，团队针对 WebUI 性能、AI 模型适配及核心记忆机制等关键问题进行了快速响应和修复；另一方面，WebUI 自动化管理、TTS 系统、子代理模型配置等重大新功能正在积极开发中。值得注意的是，PR 数量激增，待合并队列达到 14 条，表明项目正处于密集的功能开发和社区贡献期。整体上，项目健康度良好，维护者响应迅速，技术债务处理及时。

### 2. 版本发布

无

### 3. 项目进展

今天有多项关键改动被合并或关闭，显著提升了项目的稳定性和功能完整性。

- **核心稳定性修复：**
    - **修复了 `idleCompact` 记忆压缩机制的重要 Bug** (#4326): 该 Bug 导致模型在对话历史中的错误学习记录未被正确总结。此修复确保了 `idleCompact` 能基于完整的、未压缩的历史进行总结，防止错误认知被固化到长期记忆中，对 Agent 的持续学习能力至关重要。
    - **修复了 WebUI 启动时的阻塞问题** (#4327): 通过将慢速 HTTP 处理程序移出主线程，并优化侧边栏和聊天界面的数据加载方式，大幅提升了 WebUI 的启动速度和响应流畅度。
    - **修复了 `exec` 工具的工作区越狱和路径查找问题** (#4098): 此 PR 处理了两个严重的安全性与功能性问题。一是阻止了受限制的命令通过相对符号链接逃离工作区（#4072），二是修复了 `pathAppend` 命令的路径查找优先级（#4083），确保用户配置的工具能优先于系统工具。

- **功能与架构增强：**
    - **合并了工具配置架构解耦** (#4314): 将共享的 Pydantic 配置基类移动至独立模块，打破了工具配置间的循环依赖。这增强了代码的可维护性，并为将来拓展更多自定义工具奠定了更清晰的架构基础。
    - **显著提升了 WebUI 与 `config.json` 的配置一致性** (#4313): 新增了数个 WebUI 设置面板的写操作端点，并增加了对应的 UI 控件，涵盖了温度、Tool调用限制、Dream功能、频道和记忆等设置项，极大提升了用户通过 WebUI 进行精细化配置的能力。

### 4. 社区热点

- **#4264 会话历史压缩问题引发热烈讨论**
    - **热度**: 评论数 1，但触发了核心修复。
    - **链接**: [Issue #4264](https://github.com/HKUDS/nanobot/issues/4264)
    - **分析**: 此 Bug 报告精准指出了 `idleCompact` 机制的一个逻辑缺陷：在用户反复纠正模型的场景中，最后的关键纠正和正确结果可能被排除在总结范围外。该议题迅速引发了维护者的重视，并在同一天内由 PR #4326 修复完毕。这体现了社区对 Agent **长期记忆质量**的高度关注，以及维护者对此类核心机制问题的快速响应能力。

- **#4329 全新的 TUI 终端界面**
    - **热度**: 作为新特性 PR，评论数未体现，但作为一份包含大量改动的 PR，无疑是今日亮点。
    - **链接**: [PR #4329](https://github.com/HKUDS/nanobot/pull/4329)
    - **分析**: 一位贡献者提交了一份庞大的 PR，为 `nanobot agent` 引入了全新的内联 TUI（终端用户界面）。该界面支持 Markdown 渲染、斜杠命令面板、多模态输入等功能，且向后兼容。这表明社区对**交互式终端体验**有强烈诉求，希望获得比传统 Rich-Live 循环更丰富、更可控的交互方式。

### 5. Bug 与稳定性

今日报告了几个关键的 Bug，其中两个已得到快速修复，另一个也已得到初步修复建议。

- **严重**:
    - **#4264 `idleCompact` 错误总结** (已修复): 记录关键历史上下文时出现逻辑缺陷。**修复 PR: #4326**。
    - **#4333 Anthropic新的 Opus-4-8模型请求全部失败** (未修复，但有对应 PR): 由于发送了已弃用的 `temperature` 参数，导致所有请求被 API 拒绝 400。此Bug阻断了使用最新模型的用户。**修复 PR: #4334**。

- **高**:
    - **#4322 `session_key` 变量未定义导致启动崩溃** (未修复): Merge 冲突导致代码中出现未定义的变量引用，Agent 启动失败。此问题需要立即处理，确保开发分支的稳定性。

- **中**:
    - **#4323, #4325, #4324 `load_config()` 未解析环境变量** (有修复 PR): 一系列关于语音转录和 WebUI 设置模块的问题，均源于 `load_config()` 返回了未经环境变量替换的原始 `${VAR}` 字符串，导致 API Key 等凭据无法被正确读取。
    - **#4083 `pathAppend` 路径查找优先级** (已修复): 用户配置的工具无法覆盖同名的系统工具。**修复 PR: #4098**。

### 6. 功能请求与路线图信号

从今日的 PR 中，可以清晰看到项目面向未来版本的几个功能演进方向：

- **多模态与媒体支持增加**: `feat(tts)` (#4316) 添加了TTS系统，支持 OpenAI、Groq等。`fix(webui)` (#4327) 优化了聊天负载。这些信号表明项目正积极增强 Agent 的交互边界，向更具表现力的多模态助手迈进。
- **Agent 管理能力增强**: `feat(webui)` (#4330) 增加了 WebUI 自动化管理视图。`feat(spawn)` (#4291) 允许子代理解放模型配置。这两个信号强烈表明，项目正从单一智能体向**多智能体编排与管理平台**的方向演进。
- **部署与集成体验优化**: `webui` (#4328) 为反向代理和子路径提供了支持。这意味着项目正考虑更复杂的企业级部署场景，向**生产环境友好**迈出了一步。
- **交互体验革新**: `Nanobot TUI` (#4329) 的出现，与现有的 `nanobot agent` CLI 交互竞争，表明社区对于更现代、功能更强大的**终端交互范式**有高度热情。

### 7. 用户反馈摘要

- **积极反馈**: 从 Issue #193（Ollama API 支持）的关闭和后续讨论可以看出，用户对未来支持更广泛的本地模型提供商（如 Ollama）抱有很强烈的期望。Issue #4264 的快速修复也得到了正面评价。
- **痛点与问题**:
    - **配置复杂性**: Issue #4322 反映的 `session_key` 未定义及 #4323-#4325 系列的环境变量问题，揭示了项目在**配置加载**环节存在技术债，易导致用户排查配置问题时感到困惑。
    - **工具发现性**: Issue #4083 关于 `pathAppend` 的优先级问题，体现了用户在**自定义工具链**方面的强烈需求，希望控制工具的执行行为。
    - **模型兼容性**: Issue #4333 反映了用户在对齐前沿模型（如 Anthropic 最新模型）时的挫败感，强调了对模型供应商 API 变更保持**即时兼容**的重要性。

### 8. 待处理积压

- **#4303 MCP服务器 `_close_server` GC崩溃**: 这是一个关键的稳定性修复 PR，涉及 asyncio 任务管理中的严重错误。目前处于 OPEN 状态且待合并，需尽快评审。
- **#4291 子代理使用可配置模型预设**: 此 PR 涉及多智能体场景下的模型灵活性，是一项重要功能。已开放数日，需要被评审和测试，以确定它是否符合项目的架构愿景。
- **#4138 为内置文件系统工具添加开关**: 此功能 PR 标识为“valid/enhancement”，但对于那些只想通过 MCP 暴露特定文件系统的部署场景至关重要。等待了一段时间，建议尽快安排合并。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 | 2026-06-14

## 今日速览

过去 24 小时内，Hermes Agent 社区保持极高活跃度：共产生 50 条 Issue 更新（其中 44 条新开/活跃，6 条关闭）和 50 条 PR 更新（48 条待合并，2 条已合并/关闭）。无新版本发布。项目讨论集中在 **Web UI Gateway 长期需求**（#501）、**自动记忆合并**（#10771）、**Telegram Bot API 10.1 富消息支持**（#44428 / #45864）以及多平台配置与稳定性修复。48 个开放 PR 表明贡献热情高涨，但也反映合并审查压力较大。

## 版本发布

无新版本。

## 项目进展

今日合并/关闭的两个 PR 推进了关键功能与修复：

- **PR #45464 (merged)** — `feat: fully wire kimi-k2.7-code across provider lists and setup flows`  
  将 kimi-k2.7-code 模型完整接入提供者列表、默认模型及设置向导，修复了因接线缺失导致的验证失败。  
  https://github.com/NousResearch/hermes-agent/pull/45464

- **PR #45728 (merged)** — `fix: target_model drives Bedrock api_mode routing`  
  修复 Bedrock 双路径路由中 `target_model` 参数被忽略的 bug，使 `anthropic_messages` 与 `bedrock_converse` 模式能正确选择。该 PR 是社区贡献者 @roadhero 的修复（#27829）的重制版，并增加了回归测试。  
  https://github.com/NousResearch/hermes-agent/pull/45728

## 社区热点

以下 Issue 和 PR 在过去 24 小时获得最多关注与讨论：

- **Issue #501 (已关闭)** — `Feature: Web UI Gateway — Local Browser-Based Interface`  
  评论 14 条，获 👍 1。该项目最长期的功能请求之一，讨论覆盖了交互模式补全、Artifact 渲染等，最终于今日关闭，但尚未明确是否已实现。  
  https://github.com/NousResearch/hermes-agent/issues/501

- **Issue #10771 (开放)** — `Feature Request: Automatic Memory Consolidation (Auto Dream)`  
  评论 8 条，获 👍 5。用户强烈需求自动记忆清理与去重，灵感来自 Claude Code 的 “Auto Dream”，讨论热度持续。  
  https://github.com/NousResearch/hermes-agent/issues/10771

- **Issue #44428 (开放)** — `[Feature]: Support Telegram Bot API 10.1 Rich Messages`  
  评论 5 条，获 👍 3。同日有重复请求 #45864（1 评论，1 👍），表明 Telegram 富消息是当前社区关注焦点。  
  https://github.com/NousResearch/hermes-agent/issues/44428

- **Issue #42366 (开放)** — `Hermes Desktop chat does not auto-scroll and input prompt disappears`  
  评论 2 条，获 👍 3。核心可用性 bug 引起用户强烈反馈，已有一个 PR #45926 针对性修复。  
  https://github.com/NousResearch/hermes-agent/issues/42366

## Bug 与稳定性

今日报告的 bug 按严重程度（P1/P2/P3）整理如下：

### 🔴 P1（严重）

- **#29205 (已关闭)** — Anthropic fallback 因 trailing assistant prefill 失败。已在今日合并的 #45728 关联修复中部分解决。  
  https://github.com/NousResearch/hermes-agent/issues/29205

### 🟠 P2（中等）

- **#23975** — 上下文压缩被网关消息中断，导致 fallback summary marker。新 PR 正在审查中。  
  https://github.com/NousResearch/hermes-agent/issues/23975
- **#44666** — `api_key_env` 在命名自定义提供者中静默忽略，导致认证失败。  
  https://github.com/NousResearch/hermes-agent/issues/44666
- **#31155** — `delegation.model` 配置被忽略，子代理始终继承父模型。  
  https://github.com/NousResearch/hermes-agent/issues/31155
- **#43586** — `provider: custom` + `key_env` 发送 `no-key-required` → 401。  
  https://github.com/NousResearch/hermes-agent/issues/43586
- **#45783** — 会话恢复时触发工具调用突发导致大量 API 费用。  
  https://github.com/NousResearch/hermes-agent/issues/45783
- **#42405** — 记忆满容量时进入 `replace` 重试循环，导致静默挂起。  
  https://github.com/NousResearch/hermes-agent/issues/42405
- **#45860** — Windows 安装发现 3 个 Bug（hermes.exe 丢失、路径问题等）。  
  https://github.com/NousResearch/hermes-agent/issues/45860

### 🟢 P3（低影响）

- **#42366** — Desktop 不自动滚动（已有 PR #45926 修复）。  
  https://github.com/NousResearch/hermes-agent/issues/42366
- **#45493** — Matrix 平台线程初始消息丢失。  
  https://github.com/NousResearch/hermes-agent/issues/45493
- **#45834** — 全局与 profile 补丁目录重复应用。  
  https://github.com/NousResearch/hermes-agent/issues/45834
- **#45877** — Cron 后台审查阻止只读工具。  
  https://github.com/NousResearch/hermes-agent/issues/45877

已有相关 fix PR 的问题：  
- #42366 → PR #45926  
- #23975 → 有部分修复 PR 正在审查  
- #45860 → 暂无关联 PR

## 功能请求与路线图信号

1. **Telegram Bot API 10.1 富消息**（#44428 / #45864）  
   用户期望支持表格、LaTeX、折叠块、脚注等新格式。该功能与 `sendRichMessage` 工具扩展（#45854）关联，可能进入下一版本。

2. **自动记忆合并 (Auto Dream)**（#10771）  
   高票需求，社区希望定期清理/去重记忆文件，避免陈旧日期和冗余条目。目前无关联 PR，但可能在规划中。

3. **规划顾问（Planning Consultant）**（#19344）  
   允许在低成本模型运行时，通过 `/consult` 调起前沿模型进行复杂架构审阅。目前处于 feature request 阶段。

4. **Web UI Gateway**（#501，已关闭）  
   虽然该 Issue 已关闭，但社区对本地浏览器界面的需求依然存在，可能通过其他方式（如 Desktop 增强）推进。

5. **桌面端原生 OS 通知**（PR #45866）  
   社区贡献者已提交实现，支持按类型开关原生通知，预计将合并到 trunk。

## 用户反馈摘要

- **积极反馈**：社区对 kimi-k2.7-code 提供者接入（PR #45464）和 Bedrock 路由修复（#45728）表示认可，这些解决了长期配置问题。
- **痛点**：
  - Desktop 界面自动滚动缺失（#42366）被多位用户评为 “High severity”，影响日常使用。
  - Photon (iMessage) 插件不可用（#42454），因上游 SDK 域名失效，用户无法使用。
  - Windows 安装体验不佳（#45860），中断更新后二进制文件丢失，提示不够清晰。
  - Docker 环境认知错误（#45792），用户反映容器内执行指令不识别自身环境，可能与路径挂载有关。
- **使用场景**：中国用户展示了基于 Hermes Agent 开发的 ThinkCheck 推理评估引擎（#22417），提示项目在多语言和自定义工具领域的扩展潜力。

## 待处理积压

以下重要 Issue/PR 长期未响应或等待维护者审查：

- **PR #27829 (5月18日)** — Bedrock api_mode 路由修复的原始版本，因缺少回归测试被搁置，后被 #45728 替代。但 #27829 仍开放，建议关闭或标记为 superseded。  
  https://github.com/NousResearch/hermes-agent/pull/27829
- **PR #40739 (6月6日)** — 添加 Linear 网关集成，已 8 天未更新，无 review。  
  https://github.com/NousResearch/hermes-agent/pull/40739
- **Issue #22417 (5月9日)** — 紫鸾/CPRC 场域健康引擎展示，非报告性 Issue，但社区展示案例有助于项目推广，建议更新标签或移至 Discussion。  
  https://github.com/NousResearch/hermes-agent/issues/22417
- **Issue #19245 (5月3日)** — 会话搜索在崩溃后返回空，孤立的 session JSON 未恢复。P2 级别但至今无进度。  
  https://github.com/NousResearch/hermes-agent/issues/19245

项目整体健康度：社区贡献意愿强，Bug 修复与功能请求并行，但维护团队需加快 PR 合并节奏（48 开放 PR 中许多等待审查），并优先处理 P2 级别稳定性问题，避免用户信任度下降。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目日报 | 2026-06-14

## 1. 今日速览

过去 24 小时内，项目整体保持中高热度的迭代节奏：共出现 **2 条 Issue 更新**（其中 1 条新活跃、1 条关闭）和 **7 条 PR 更新**（其中 5 条已合并/关闭，2 条待合并）。同时发布了 **1 个 nightly 版本**。社区修复与功能开发并行，核心稳定性与用户体验改善占据主流，项目健康状况良好。

## 2. 版本发布

**nightly 构建** `v0.2.9-nightly.20260614.cf67dd38`

- 类型：自动构建，非稳定版
- 完整变更日志：[v0.2.9…main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- ⚠️ 注意：该构建可能包含未完全验证的改动，不建议在生产环境直接使用。如遇问题，建议优先基于 v0.2.9 稳定版排查。

## 3. 项目进展

今日合并/关闭的 5 个 PR 主要围绕 bug 修复、国际化及功能增强展开：

| PR | 标题 | 简述 | 状态 |
|---|---|---|---|
| [#2935](https://github.com/sipeed/picoclaw/pull/2935) | docs(i18n): 添加繁体中文 (zh-TW) 本地化支持 | 全量文档及前端 i18n 系统增加繁体中文（台湾）翻译 | ✅ 已关闭 |
| [#3065](https://github.com/sipeed/picoclaw/pull/3065) | fix(seahorse): 显式忽略 PRAGMA/迁移失败路径中的 Close() 错误 | 消除 4 处 linter 警告 | ✅ 已关闭 |
| [#3066](https://github.com/sipeed/picoclaw/pull/3066) | fix: 显式忽略临时文件写入/同步失败路径中的 Close() 错误 | 统一处理 3 处 `tmpFile.Close()` 未检查的返回值 | ✅ 已关闭 |
| [#3119](https://github.com/sipeed/picoclaw/pull/3119) | fix(tts): 支持 OpenRouter 语音参数覆盖与回退 | 新增 `extra_body` 配置覆盖 voice/response_format，自动单次重试降级 | ✅ 已关闭 |
| [#3117](https://github.com/sipeed/picoclaw/pull/3117) | fix(agent): 将媒体轮次路由至图像模型 | 修复 #3108 图像描述幻觉问题 | ✅ 已关闭 |

**整体推进方向**：代码质量提升（显式忽略错误）、新区域支持（繁体中文）、TTS 容错增强、Agent 多模态路由优化。项目在稳定性和国际化方面迈出了扎实的一步。

## 4. 社区热点

今日讨论最活跃的 Issue 为 **[#3012 [BUG] 启用进化功能后每分钟持续消耗 Token](https://github.com/sipeed/picoclaw/issues/3012)**（3 条评论，作者 xpader）。用户报告在启用 Evolution（进化）功能后，即使没有任何交互，系统仍然每分钟消耗 Token，涉及环境为 MiniMax 模型 + FreeBSD。该问题已存在 9 天，至今尚未有对应修复 PR，社区正在等待进一步排查。该 Bug 直接影响用户使用成本，诉求强烈。

## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 修复状态 |
|---|---|---|---|
| 🔴 高 | [#3012](https://github.com/sipeed/picoclaw/issues/3012) | **进化功能开启后每分钟持续消耗 Token**（已活跃 9 天，3 条评论） | 尚无对应 PR |
| 🟡 中 | [#3108](https://github.com/sipeed/picoclaw/issues/3108) | 请求图像描述时，若当前模型不支持视觉（如 deepseek/deepseek-v4-flash 文本模型），会导致幻觉回答 | ✅ 已由 [#3117](https://github.com/sipeed/picoclaw/pull/3117) 修复并关闭 |

**#3012 影响面较大**，涉及持续计费问题，建议优先跟踪。若您也遇到该问题，可前往 Issue 提供更多环境信息以协助定位。

## 6. 功能请求与路线图信号

### 新增功能 PR（待合并）

- **[#2964 Feat/image input compression](https://github.com/sipeed/picoclaw/pull/2964)**（作者 afjcjsbx，创建于 5 月 28 日，至今未合并）  
  在视觉管道中增加可配置的多级图像压缩策略，解决媒体文件仅受 `max_media_size` 限制、缺乏压缩策略的问题。该 PR 属于需求较明确的增强，很有可能被纳入 v0.3.0 或后续版本。

- **[#3118 Add remote Pico WebSocket mode](https://github.com/sipeed/picoclaw/pull/3118)**（作者 jp39，创建于 6 月 12 日，待合并）  
  为 `picoclaw agent` 命令添加可选的远程 WebSocket 模式（`--remote ws://...`），允许 Agent 通过 WebSocket 远程连接 Pico。这是社区对远端部署能力的需求信号。

### 路线图信号

当前 PR/Issue 中未见明确的远期路线图声明，但图像压缩与远程 WS 模式两项均为实际使用诉求，预计会被优先评估。

## 7. 用户反馈摘要

- **Token 消耗异常（#3012）**：用户 xpader 在 FreeBSD 上使用 MiniMax 模型时，Evolution 功能每分钟无理由消耗 Token，属于 **高成本 bug**，用户表示“急迫需要修复”。评论区未显示其他用户复现情况，但问题本身明确。
- **图像幻觉（#3108）**：用户 afjcjsbx 反馈在 OpenRouter 上使用仅文本模型时，Agent 仍尝试调用图像描述并给出虚构回答，影响可信度。该问题已被 #3117 修复，用户预期将获得更合理的模型路由逻辑。
- 整体社区讨论量不大，当前活跃用户以开发者/贡献者为主，反馈侧重功能缺陷而非新功能期望。

## 8. 待处理积压

| 跟踪项 | 类型 | 状态 | 建议 |
|---|---|---|---|
| [#2964](https://github.com/sipeed/picoclaw/pull/2964) 图像输入压缩 | PR | 待合并（5 月 28 日创建，距今 17 天） | 功能价值明确，建议维护者尽快安排 review 并决定是否合并或要求修改 |
| [#3012](https://github.com/sipeed/picoclaw/issues/3012) Evolution 持续消耗 Token | Issue | 未关闭，无 PR 关联（9 天） | 应指定负责人或标为 **priority**，防止用户流失 |
| [#3118](https://github.com/sipeed/picoclaw/pull/3118) 远程 WebSocket 模式 | PR | 待合并（创建 2 天，尚在合理窗口期） | 功能新且非紧急，可纳入下一轮合并计划 |

---

**数据截止**：2026-06-14 10:00 UTC（基于 2026-06-13 GitHub 活动数据）  
**数据源**：[PicoClaw - sipeed/picoclaw](https://github.com/sipeed/picoclaw)  
**作者**：AI 智能体 & 开源项目分析师

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将基于您提供的 GitHub 数据，生成 2026年6月14日的 NanoClaw 项目动态日报。

---

### NanoClaw 项目日报 | 2026年6月14日

**数据洞察周期：** 2026年6月13日 00:00 UTC — 2026年6月14日 00:00 UTC

---

#### 1. 今日速览

今日项目活跃度较高，主要表现为 Pull Request (PR) 的密集合并与提交流程。共有 **6 条 PR 更新**，其中 **4 条已合并**，表明核心开发团队正在快速推进功能和修复。Issues 方面仅有 1 条因误操作而关闭的无效条目，社区新提出的问题较少。总体来看，项目处于 **内部开发与重构冲刺期**，代码库迭代迅速，但面向社区的原始问题反馈和互动有限。

#### 3. 项目进展

今日项目在功能开发与系统稳定性方面取得了显著进展，4个核心PR的合并标志着多个功能模块的落地。主要推进方向包括：

- **核心功能扩展：** 合并了 **#2754**，引入了可选的 `onExchangeComplete` 提供者钩子以及斜杠命令中断机制，增强了Agent运行时与外部系统的交互能力。同时，**#2746** 被合并，建立了一个“Agent能力面（agent-surfaces capability seam）”，允许提供者声明其具备的能力，为更灵活的模块化系统奠定了基础。
- **持久化与配置管理：** **#2745** 已合并，为提供者新增了可选的内存持久化框架（`usesMemoryScaffold`），允许Agent会话维持更复杂的上下文。
- **开发者体验与SDK升级：** **#2747** 描述了重要的SDK升级（`@onecli-sh/sdk` 0.5.0 → 2.2.1），并引入了凭据挂载（credential-stub mounts）和可机器校验的PINs，这将提升安全性和配置的标准化水平。

这些改进共同推动项目向 **更健壮、模块化、可扩展的运行环境** 迈出了坚实一步。

#### 4. 社区热点

今日无高互动量的讨论话题。唯一的 Issue **#2755** 由作者自己标记为错误发布并关闭，未引发社区讨论。所有合并的 PR 评论数显示为 `undefined`，表明社区成员未在 PR 页面上留下公开评论。这一现象可能意味着当前的开发迭代主要由核心团队主导，社区参与主要集中在代码贡献而非讨论层面。

#### 5. Bug 与稳定性

今日没有新增的直接 Bug 报告。但项目在稳定性方面取得了重要进展：
- **关键 Bug 修复（待合并）：** **#2750** 正在等待合并。该 PR 旨在修复两个与容器管理相关的严重问题：
    - **#2516 (严重):** 容器被 SIGKILL 后，`outbound.db` 日志出现陈旧数据，可能导致数据不一致。
    - **#2640 (严重):** 主机 `outbound.db` 句柄在热日志轮询时出现竞争条件（race condition），可能导致数据库损坏或行为异常。
- **系统稳健性加固（待合并）：** **#2732** 也在等待合并，该 PR 来自一次对抗性审计，修复了包含容器生命周期、崩溃-生成断路器（circuit breaker）和 Docker 回退机制在内的多个安全性问题。

这两条待合并的PR是当前解决稳定性问题的关键。

#### 6. 功能请求与路线图信号

今日无用户提出的新功能请求。不过，通过分析已合并的 PR，可以清晰地看到项目路线图的方向：
- **提供者（Provider）能力模型：** 从 **#2746** (能力声明) 和 **#2745** (持久化内存) 来看，项目正在构建一个更强大的提供者框架，允许第三方扩展在标准框架内声明能力和状态。
- **交互协议标准化：** **#2754** 中 `onExchangeComplete` 钩子和斜杠命令的引入，表明项目在标准化 Agent 与用户、Agent 与外部服务之间的通信协议。
- **安全与配置：** **#2747** 中的 SDK 更新和凭据挂载系统是明确的安全和运维改进信号，预计这些特性将成为下一版本的核心组成部分。

#### 7. 用户反馈摘要

今日从 Issues 和 PR 评论中未提取到直接的用户反馈或痛点。唯一的 Issue **#2755** 是误操作，这本身也反映了社区成员偶尔会面临仓库管理上的小问题。

#### 8. 待处理积压

目前没有明显的长期未响应 Issue。但有两项重要的 **开放 PR** 值得项目维护团队优先关注，因为它们直接关系到系统的稳定性和安全性。

- **#2775 (待合并):** `fix: recover stale outbound.db journals after container kills; classify hot-journal poll races ( #2516, #2640 )`
    - **链接：** `nanocoai/nanoclaw PR #2750`
    - **重要性：** **高**。该PR修复了两个严重的数据库损坏风险，对于运行中的生产环境至关重要。
- **#2773 (待合并):** `Harden host + agent-runner from health audit findings`
    - **链接：** `nanocoai/nanoclaw PR #2732`
    - **重要性：** **高**。来自安全审计的修复，解决了容器生命周期管理和Agent运行时的潜在崩溃和安全问题。

**建议：** 维护者应尽快审查并合并这两个 PR。社区开发者也可关注这些修复的进展，了解项目安全基线的最新状态。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，以下是根据 NullClaw 项目在 2026-06-14 的 GitHub 数据生成的日报。

---

# NullClaw 项目动态日报 | 2026-06-14

## 今日速览

过去24小时，NullClaw 项目活跃度中等，主要围绕一个**高优先级 Bug 的修复**展开。项目收到1个新的严重 Bug 修复 PR，该 PR 直接指向了一个影响“一次性定时任务”消息交付的阻塞性问题。同时，社区对一个已有的功能请求（JIRA 集成）保持关注，但社区讨论热点主要集中在 Agent 类型定时任务的可靠性问题上。项目无新版本发布，整体处于 **Bug 修复与稳定性加固** 阶段。

## 版本发布
无。

## 项目进展
- **Bug 修复 PR 待合并**: 今日最重要的进展是 PR #954 被提交。该 PR 直接针对 Issue #941 中报告的“Agent 类型定时任务静默失败”的严重问题。PR 作者定位了根因——`OutboundMessage.channel` 对象的“释放后使用”问题，并提供了修复方案。该 PR 目前处于 **待合并** 状态，一旦合并，将显著提升定时任务的消息投递可靠性。

## 社区热点
- **#941 [OPEN] Agent-type cron jobs don't spawn a subprocess — Telegram delivery never happens** 🗣️ (7 条评论)
  - **链接**: [Issue #941](https://github.com/nullclaw/nullclaw/issues/941)
  - **分析**: 这是今日社区讨论最活跃的 Issue。用户报告了一个严重影响使用的 Bug：通过 `schedule` 创建 `job_type: "agent"` 的定时任务后，任务状态显示完成，但底层 Agent 子进程从未启动，导致无法通过任何渠道（如 Telegram）接收消息。该 Issue 持续讨论了近两周，评论数达到7条，凸显了用户对于任务执行透明度和可靠性的强需求。该问题已由 PR #954 直接锁定和修复。

## Bug 与稳定性
- **严重**: [#941 Agent-type cron jobs don't spawn a subprocess](https://github.com/nullclaw/nullclaw/issues/941)
  - **状态**: **Open** / **已有修复 PR (#954)**
  - **描述**: 用户配置“一次性”或“定时”Agent 任务后，任务标记为完成但子进程未执行，导致消息（如 Telegram）交付失败。这是一个功能性的静默失败，严重影响用户信任度。
- **根本原因**: 根据 PR #954 的描述，根因是 `OutboundMessage.channel` 对象在发送消息前被错误释放（use-after-free），导致消息无法找到目标渠道而被丢弃。

## 功能请求与路线图信号
- **#914 [ENHANCEMENT] Create JIRA access tool** ⭐ (1 条评论)
  - **链接**: [Issue #914](https://github.com/nullclaw/nullclaw/issues/914)
  - **分析**: 这是一个已提出一个月的功能请求，要求为 NullClaw 开发一个 JIRA 集成工具。该功能可让 Agent 和工作流直接与 JIRA 交互，执行读取、创建、更新工单等操作。尽管目前评论数不多，但这代表了一种将 AI Agent 与项目管理软件深度打通的明确需求，符合团队协作场景下的自动化趋势。目前尚无关联 PR，但该功能若被开发，将极大拓展 NullClaw 在企业级场景下的应用范围。

## 用户反馈摘要
- **核心痛点**: 用户 `weissfl` 报告了一个“静默失败”的 Bug：**定时任务执行结果不透明**。任务标记为完成，但用户预期中的消息（如 Telegram）并未送达，造成了功能完全丧失且用户无法感知的糟糕体验。这表明用户不仅需要任务被执行，更需要可靠、可验证的任务交付机制。
- **专业反馈**: PR #954 的作者 `vernonstinebaker` 不仅给出了修复代码，还详细描述了根因（use-after-free），展现了对 NullClaw 内部消息传递机制的深入理解，这对于项目维护者来说是非常高质量的社区贡献。

## 待处理积压
- **长期未处理的功能请求**: **#914 [ENHANCEMENT] Create JIRA access tool** — 该 Issue 已存在超过 30 天，处于开放状态且无维护者回复。随着社区对 Agent 能力的期待提升，建议项目维护者对该功能的优先级进行评估并给出初步反馈，避免社区需求长期被忽视。
- **待合并的紧急 Bug 修复**: **PR #954 Fix: one-shot cron jobs silently fail to deliver messages** — 该 PR 直接修复了 Issue #941 中的严重问题。鉴于该问题社区关注度高且影响范围广（所有使用 Agent 定时任务的用户），建议项目维护者尽快安排代码审查与合并。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 IronClaw 项目 GitHub 数据，为您生成 2026 年 6 月 14 日的项目动态日报。

---

### **IronClaw 项目日报 | 2026-06-14**

**项目健康度评估：** **高活跃，核心功能攻坚阶段。** 项目今日迎来开发量与修复力度的显著提升，尤其是在修复 Slack 集成循环、构建附件支持体系这两个核心路线上取得了关键性进展。虽然 Issues 层面无明显增长，但 PR 流水线繁忙，表明团队正在内部密集推进代码合并与重构。

---

### **1. 今日速览**

今日项目活跃度极高，共处理了 22 条 Pull Request，其中 5 条已被合并/关闭，显示出强劲的交付动能。开发重点高度集中在**修复 Slack 重新审批循环**和**构建完整的附件处理链路**（从字节落地到模型可见）这两条主线上。与此同时，社区新提出的 Issue (#4845) 旨在进一步优化代码结构，体现了代码质量意识的提升。总体来看，项目正处于问题攻坚与功能收尾的关键阶段。

### **2. 版本发布**

无

### **3. 项目进展**

今日合并/关闭的 PR 主要集中在 **附件功能** 的基础设施建设上，标志着该项目已基本完成核心后端链路的搭建，即将进入前端集成和测试阶段。

*   **附件功能（#4644 系列）基础链路贯通：** 今日成功合并了实现该功能的多个核心 PR，标志着从“接收文件字节”到“存储并在对话上下文中引用”的完整闭环已形成。
    *   **#4672** `feat(reborn): accept inline attachment uploads on the WebChat v2 send path` [已合并] - 在 WebChat v2 发送端实现了附件上传，打通了用户与后端存储的入口。
    *   **#4670** `feat(attachments): bridge inbound bytes into transcript AttachmentRefs` [已合并] - 建立了将上传的字节桥接到对话记录引用的关键桥梁。
    *   **#4668** `feat(attachments): MountView-based attachment landing crate` [已合并] - 实现了基于 `MountView` 的附件持久化存储层。
    *   **#4655** `feat(threads): carry attachment refs through the Reborn transcript contract` [已合并] - 扩展了 Reborn 对话契约，使其能够携带附件引用，而非只处理纯文本。
    *   **#4654** `feat(common): extensible attachment format registry` [已合并] - 建立了一个可扩展的附件格式注册表，取代了散落在各处的硬编码列表，从根本上解决了格式支持不一致导致的 Bug。 这些合并在短短几天内完成了从无到有的基础设施构建，项目进度推进迅猛。

*   **核心修复方向转移：** 今日未合并的 PR 工作重点已从 **“Slack 重新审批循环”** 的修复转向 **“运行管理”** 和 **“系统反馈”** 的优化。
    *   **#4841** `reborn: no run-borking failures — failure explanation + retryable failed runs` [待合并] - 旨在消除 Reborn 二进制文件中的“致命”错误，让运行失败时系统能给出解释并提供重试机会，提升系统鲁棒性。
    *   **#4838** `Explicit gate-open feedback for busy threads (no parking)` [待合并] - 提出当线程繁忙时，新消息不再被隐藏等待，而是直接向用户发送明确的排队通知，将重试决策权交还给用户。

### **4. 社区热点**

今日社区讨论焦点并非集中在单个 Issue 或 PR 的评论数上，而是通过一系列 **紧密关联的 PR** 形成了两大热点领域，展现了开发团队的高度协作与集中攻关态势。

1.  **热点一：Slack 重新审批循环修复（#4839 及相关课题）**
    *   **核心诉求：** 解决在需要用户审批+凭据的复杂场景（如 Gmail）下，系统反复要求用户确认的“死循环”问题。
    *   **关联 PR：** 该热点主要由 **#4839** (`fix: preserve invocation identity across auth-gate re-dispatch`) 和修复细分 Bug 的 **#4843** (单飞门控交付)、**#4844** (过滤门控路由) 以及 **#4840** (修正凭据缺失时的门控顺序) 共同构成。这组 PR 从多个角度系统性地修复了该顽疾。
    *   **分析：** 这组 PR 的密集出现表明，Slack 与 Gmail 等外部服务的集成问题严重阻碍了用户体验（连续四次审批），是当前项目最高优先级的待办事项。团队正在进行地毯式排查与修复。

2.  **热点二：附件完整支持链路（#4644 系列及其后续）**
    *   **核心诉求：** 让模型能够“看到”并处理用户上传的文档（如 CSV、PDF、图片）。
    *   **关联 PR：** 从 **#4675** (文本提取独立crate) 到 **#4676** (落地路径提取) 以及今日合并的 **#4672, #4670, #4668, #4655, #4654**，整个链路已基本打通。目前的待合并项 **#4738** (`feat(reborn): attachment web UX on the WebChat v2 SPA`) 是最后的前端 UI 环节。
    *   **分析：** 此热点是产品能力从“纯文本对话”迈向“多模态交互”的关键一步。用户期待已久，其实现将极大扩展 IronClaw 的应用场景。今日的多项合并标志着后端架构已就绪，只待前端集成面世。

### **5. Bug 与稳定性**

*   **严重：Nightly E2E 测试持续失败**
    *   **Issue:** **#4108** `Nightly E2E failed` (创建于 2026-05-27，最后更新 2026-06-13)
    *   **状态：** 仍未修复，已持续超过两周。最后更新显示失败记录于 2026-06-13 日。
    *   **影响：** 影响项目持续集成稳定性。若此问题未解决，新合并的代码可能引入未知的回归问题。
    *   **链接：** [Issue #4108](https://github.com/nearai/ironclaw/issues/4108)

*   **中等：Slack 重新审批循环（已有多项修复 PR）**
    *   **相关 PR：** **#4839** (核心修复), **#4843** (多路发送修复), **#4844** (门控过滤修复), **#4840** (门控顺序修复)
    *   **状态：** 已有明确的修复策略和多个 PR 待合并。这是当前修复工作的重中之重，预计将在近一两天内解决。
    *   **影响：** 直接影响所有需要通过 Slack 交互并需二次授权（如 Google OAuth）的用户，导致无法正常使用，体验糟糕。

*   **低：凭据缺失时审批门控顺序错误**
    *   **PR:** **#4840** `fix: surface missing-credential auth gate before the approval gate`
    *   **状态：** 已有待合并的修复 PR。
    *   **描述：** 当缺少凭据时，系统会先要求用户审批操作，审批通过后才发现缺少凭据而失败，浪费用户一次审批操作。此 PR 修正为先提示认证，再通过审批，逻辑更符合直觉。

### **6. 功能请求与路线图信号**

*   **代码架构优化信号：** 今日新开的 Issue **#4845** (`Extract shared resume-authority head across resume_json / auth_resume_json`) 源于对 **#4839** PR 的进一步重构思考。这并非新功能要求，而是核心团队在修复 Bug 后进行代码优化的信号，表明团队正持续提升代码质量与可维护性。
*   **用户体验改进信号：** PR **#4838** (`Explicit gate-open feedback for busy threads`) 和 **#4836** (`surface connected channels, delivery state, and run origin`) 体现了从“被动处理”到“主动告知”的系统反馈哲学转变。这表明路线图开始关注如何让用户更清晰地理解系统状态，降低使用困惑。
*   **路线图演进推测：** 随着附件功能的贯通（#4644 系列），以及 Slack 审批循环的修复，我们有理由相信下一阶段的开发重点将是：1) 前端 UI 集成的最终落地；2) 深入优化多通道（如 Slack）的稳定性和“智能”；3) 可能开始探索更多外部服务（Dropbox, OneDrive 等）的集成。

### **7. 用户反馈摘要**

从 Issue 和 PR 的标题/摘要中提取，今日未捕获到明确的来自最终用户的直接评论或抱怨。当前的所有活动主要由核心开发者驱动，反映了开发阶段的特点。然而，从大量针对 Slack 审批循环的修复 PR 可以推断，此问题是阻碍用户流畅使用 IronClaw 的**最突出痛点**。开发者对“四次连续审批”的描述直接反映了真实用户场景下的糟糕体验。

### **8. 待处理积压**

*   **长期开放且关键的版本发布 PR:**
    *   **PR #3708** `chore: release` - 已开放近一个月（2026-05-16），至今更新频繁但未合并。该 PR 涉及多个 crate 的版本更新，包括 `ironclaw_common` 和 `ironclaw_skills` 的 API 破坏性变更。此 PR 的长期开放可能阻塞依赖于这些 crate 的外部项目。建议维护者评估此 PR 的阻塞点，并加速版本发布流程。 [链接](https://github.com/nearai/ironclaw/pull/3708)

*   **Nightly E2E 测试持续失败:**
    *   **Issue #4108** - 作为“守门员”，此 Issue 已存在超过两周。在大量新功能代码被合并的今天，这个 Red 状态应引起核心维护者的最高警惕。尽快修复或定位失败原因是当务之急。 [链接](https://github.com/nearai/ironclaw/issues/4108)

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

## LobsterAI 项目动态日报 — 2026-06-14

### 1. 今日速览
过去24小时内项目无新版本发布，无新Issue或新PR创建。2个长期停滞的PR（#1466、#1467）于当日被合并/关闭，表明维护者在进行积压清理。但当前仍存在4个Stale状态的Issue和3个Stale状态的PR，均超过2个月无实质性交互，项目整体活跃度偏低，社区反馈和功能贡献的响应周期较长。

### 3. 项目进展
今日共合并/关闭2个PR，均为 bug fix：

- **#1466 fix(mcp): modal close button unreachable when content grows tall**  
  修复了MCP服务器表单模态框内容过长时，关闭按钮不可点击的问题。合并后提升了长表单场景的操作可达性。  
  [PR #1466](https://github.com/netease-youdao/LobsterAI/pull/1466)

- **#1467 fix(shortcuts): display Cmd (⌘) instead of Ctrl on macOS**  
  修复了macOS平台设置页快捷键显示为Ctrl而非Cmd的跨平台适配问题。合并后macOS用户将获得正确的键位提示。  
  [PR #1467](https://github.com/netease-youdao/LobsterAI/pull/1467)

这两个修复均来自同一位贡献者（linlihua），且已在当日合并入主分支，项目在用户体验细节上取得小幅改进。

### 4. 社区热点
所有Issue和PR在统计周期内均无新增评论，讨论热度极低。相对值得关注的是：

- **#1443 [OPEN] [stale] 有计划支持新版本的openclaw吗？**  
  用户询问官方是否计划适配OpenClaw v2026.3.24（包含breaking change），本地尝试报错无法拉起。该问题已存在超过2个月无维护者回覆，反映社区对上游依赖更新的迫切需求。  
  [Issue #1443](https://github.com/netease-youdao/LobsterAI/issues/1443)

其余Issues（#1437、#1439、#1442）均为技能/Agent相关使用bug，同样长时间未得到官方回应，社区可能存在挫败感。

### 5. Bug 与稳定性
**未修复的 Bug（按严重性排列）：**

1. **[严重] #1439 — 上传技能已停用，对话中仍然可以调用**  
   技能停用后仍可通过关键字触发，可能导致安全或功能紊乱。目前无对应修复PR。  
   [Issue #1439](https://github.com/netease-youdao/LobsterAI/issues/1439)

2. **[中等] #1442 — Agent添加技能后对话不展示已选技能，切换会话才恢复**  
   用户对技能选择的作用存疑，且UI反馈存在延迟。无修复PR。  
   [Issue #1442](https://github.com/netease-youdao/LobsterAI/issues/1442)

3. **[中等] #1437 — 创建定时任务时不选择重复计划并清空日历，点击创建无反应**  
   前端无任何错误提示，属于静默失败。无修复PR。  
   [Issue #1437](https://github.com/netease-youdao/LobsterAI/issues/1437)

4. **[低] #1443 — OpenClaw新版本兼容问题**  
   属于环境适配bug，未提供错误日志，无法判断紧急程度。  
   [Issue #1443](https://github.com/netease-youdao/LobsterAI/issues/1443)

**今日修复的 Bug：**
- MCP模态框关闭按钮不可点击（#1466）
- macOS快捷键显示错误（#1467）

### 6. 功能请求与路线图信号
当前暂无新功能请求提出。但以下Stale PR包含未完成的功能特性，可能影响路线图：

- **#1440 — feat(cowork): 将已选技能标签移至输入框内顶部展示**  
  优化技能标签布局，提升多技能场景下的UI清晰度。该PR若合并将改善用户操作体验，但已停滞2个月。  
  [PR #1440](https://github.com/netease-youdao/LobsterAI/pull/1440)

- **#1441 — feat(artifacts): add extensible preview pipeline for HTML, React and Mermaid**  
  增加对HTML/React/Mermaid工件的可扩展预览管道，是原#1011的冲突修复版本。此功能有助于增强协作会话的富媒体展示能力，若合并将显著提升项目竞争力。  
  [PR #1441](https://github.com/netease-youdao/LobsterAI/pull/1441)

- **#1445 — fix(skills): 修复技能重复导入无校验及zip导入目录名异常**  
  虽标记为修复，但涉及对导入逻辑的增强，可视为稳定性功能。  
  [PR #1445](https://github.com/netease-youdao/LobsterAI/pull/1445)

这些PR均由社区贡献，长期未合并可能打击贡献者积极性。

### 7. 用户反馈摘要
从Issues描述中可提炼出以下核心用户痛点：

- **技能管理混乱**：技能停用后仍可调用（#1439）、选中技能在对话后消失（#1442）、重复技能无校验（对应#1445）。用户对技能选择与注入机制感到困惑。
- **定时任务创建无反馈**：特定操作导致按钮失效且无任何错误提示（#1437），暴露出前端表单校验缺陷。
- **上游依赖滞后**：OpenClaw新版本无法使用，且官方未回应适配计划（#1443），影响依赖该工具链的用户部署。

用户整体满意度较低，因多个明显bug长时间未被确认或修复，且缺乏沟通渠道。

### 8. 待处理积压
以下Issue和PR已标记为Stale且超过2个月未得到维护者更新，建议优先关注：

| 类型 | 编号 | 标题 | 创建时间 | 最后更新 | 链接 |
|------|------|------|----------|----------|------|
| Issue | #1443 | 有计划支持新版本的openclaw吗？ | 2026-04-03 | 2026-06-13 | [链接](https://github.com/netease-youdao/LobsterAI/issues/1443) |
| Issue | #1437 | 创建定时任务时，计划选择不重复，清空日历，点击创建无反应 | 2026-04-03 | 2026-06-13 | [链接](https://github.com/netease-youdao/LobsterAI/issues/1437) |
| Issue | #1439 | 上传技能已停用，对话中仍然可以调用 | 2026-04-03 | 2026-06-13 | [链接](https://github.com/netease-youdao/LobsterAI/issues/1439) |
| Issue | #1442 | Agent添加技能，对话后引用的技能不展示 | 2026-04-03 | 2026-06-13 | [链接](https://github.com/netease-youdao/LobsterAI/issues/1442) |
| PR | #1440 | feat(cowork): 将已选技能标签移至输入框内顶部展示 | 2026-04-03 | 2026-06-13 | [链接](https://github.com/netease-youdao/LobsterAI/pull/1440) |
| PR | #1441 | feat(artifacts): add extensible preview pipeline | 2026-04-03 | 2026-06-13 | [链接](https://github.com/netease-youdao/LobsterAI/pull/1441) |
| PR | #1445 | fix(skills): 修复技能重复导入无校验 | 2026-04-03 | 2026-06-13 | [链接](https://github.com/netease-youdao/LobsterAI/pull/1445) |

强烈建议项目维护者针对上述积压进行回复或合入，以恢复社区信任。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 | 2026-06-14

## 1. 今日速览

- 项目今日活跃度中等：共产生 1 条新 Issue 和 3 条新 Pull Request，无新版本发布。
- 核心问题聚焦于 **MCP OAuth 鉴权失败**（Notion、Linear 等第三方服务器），已由同一作者提交修复 PR，社区响应及时。
- Docker 镜像构建中的 VOLUME 声明与挂载冲突问题被修复，提升容器化部署的兼容性。
- 依赖升级方面，`esbuild` 从 0.25.12 跳升至 0.28.1（跨主版本更新），涉及 JavaScript UI 构建工具链的增强。
- 所有 PR 目前均为待合并状态，无已合并或关闭项，需关注后续审查进度。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日无已合并或关闭的 PR，但 **3 个重要 PR 已提交**，分别推进了以下方向：

- **PR #1120**（`fix(mcp): use direct fetch for resource_metadata URL from WWW-Authenticate`）  
  直接对应 Issue #1119，修复 MCP OAuth 流程中 `invalid_target` 错误。该 PR 修改了 `discover_and_register()` 中处理 `resource_metadata` 参数的方式，改用直接 fetch 而非错误传递。  
  → 链接：https://github.com/moltis-org/moltis/pull/1120

- **PR #1122**（`fix: drop VOLUME declarations that shadow the home bind mount`）  
  修复 Dockerfile 中显式声明 VOLUME 导致 `--bind mount` 被遮蔽的问题，提升容器部署的稳定性。  
  → 链接：https://github.com/moltis-org/moltis/pull/1122

- **PR #1121**（`chore(deps-dev): bump esbuild from 0.25.12 to 0.28.1`）  
  由 Dependabot 自动提交的 JavaScript 构建工具升级，包含多项性能改进和 bug 修复。  
  → 链接：https://github.com/moltis-org/moltis/pull/1121

**项目向前迈进的幅度**：尽管今日没有合并，但 OAuth 兼容性瓶颈已被定位并提交修复，容器化部署的易用性得到改善，核心依赖链保持更新。

## 4. 社区热点

- **Issue #1119**（[Bug]: MCP OAuth fails with `invalid_target` for servers using `resource_metadata`）  
  作者 `xzavrel` 报告了连接 Notion、Linear 等 MCP 服务器时的完整失败场景，浏览器弹出 JSON 错误。该 Issue 获得 1 条评论（未公开内容），并已关联 PR #1120。  
  → 链接：https://github.com/moltis-org/moltis/issues/1119

- **PR #1120** 作为修复方案，与 Issue 形成闭环，显示社区对第三方 MCP 服务器兼容性的强烈需求。预期该修复将被快速纳入下一版本。

## 5. Bug 与稳定性

| 严重程度 | Issue / PR | 描述 | 状态 |
|----------|------------|------|------|
| **高** | #1119 | MCP OAuth 在 `WWW-Authenticate` 包含 `resource_metadata` 参数时失败，导致无法添加 Notion/Linear 等远程 MCP 服务器 | 🔧 已有修复 PR #1120 |
| **中** | #1122 | Dockerfile 中 VOLUME 声明导致用户 home 目录挂载被覆盖，影响容器化部署的持久化配置 | 🔧 PR 已提交，待合并 |

注：无崩溃或回归问题报告。

## 6. 功能请求与路线图信号

- 当前无直接的新功能请求 Issue。  
- **PR #1122** 隐含了用户对 **Docker 部署体验** 的改进需求，尤其是期望 `--bind mount` 与容器内路径无缝配合。这可能是社区对生产环境部署的持续关注点。  
- **PR #1121**（esbuild 升级）属于常规维护，但跨主版本更新暗示项目前端构建工具链正跟随上游演进。  

未来若 OAuth 修复合并，将可能打通主流第三方 MCP 服务器（Notion、Linear）的集成，为 Moltis 作为 AI 智能体中心的生态扩展铺路。

## 7. 用户反馈摘要

- **Issue #1119** 作者详细描述了失败步骤，浏览器返回 `{"err...}` 错误，指出 `invalid_target`。用户场景清晰：试图通过 OAuth 添加 Notion 或 Linear 的 MCP server 时流程中断。评论者可能提供了补充信息或表示同类问题。  
- 当前无其他用户情绪反馈（如满意/不满意评论），但修复 PR 的快速提交表明维护者对高质量用户体验的重视。

## 8. 待处理积压

- **PR #1120**（MCP OAuth 修复）和 **PR #1122**（Docker VOLUME 修复）均提交于今日，目前无维护者响应或审查标记。建议优先审查这两个 PR，以尽快解决影响面广的 Bug 和改进基础设施稳定性。  
- **PR #1121**（esbuild 升级）为 Dependabot 自动 PR，通常风险较低，但仍需人工确认兼容性后合并。  

无长期未响应的 Issue 或 PR 积压。

---

*以上日报基于 Moltis 官方 GitHub 仓库实时数据生成，数据截止 2026-06-14。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目日报 – 2026-06-14

## 1. 今日速览

过去 24 小时内 CoPaw（QwenPaw）项目保持中等活跃度：共产生 8 条 Issue 更新（7 条新开/活跃，1 条已关闭）和 8 条 PR 更新（6 条待合并，2 条已合并/关闭）。社区诉求集中在**多语言支持（越南语）**、**渠道扩展（Zalo Bot）** 以及 **第三方 API 接入（kimi-for-coding）** 上。Bug 方面，Tauri 桌面端启动慢、上下文压缩丢失等老问题仍在发酵，但已有多个修复 PR 处于待合并状态。整体来看，项目在功能拓展和稳定性修补上并行推进，但部分长期 bug 仍未得到彻底解决。

## 3. 项目进展

今日合并/关闭了两个 PR，对核心流程和功能有所优化：

| PR | 状态 | 摘要 |
|----|------|------|
| [#2498](https://github.com/agentscope-ai/QwenPaw/pull/2498) | **已合并** | `fix(agents): use console language when creating agent and fallback unsupported langs` — 修复新建 Agent 时语言选择固定为英文的问题，现在会读取用户界面的语言设置，并对不支持的语言自动降级。 |
| [#4969](https://github.com/agentscope-ai/QwenPaw/pull/4969) | **已合并** | `feat(skill): Add skill tag batch download` — 技能批量下载支持按标签过滤，相关 Issue #2961 已解决。 |

这两个合并标志着项目在**用户体验（多语言适配）** 和**功能易用性（技能管理）** 上迈出了坚实一步。

## 4. 社区热点

本期讨论最活跃的 Issue 是 [#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156) **「建议支持 kimi-for-coding / 加入 uv 白名单」**，获得 4 条评论。用户明确表达了**已订阅 Kimi coding 套餐却无法在 CoPaw 中使用**的痛点，希望项目方扩展官方 API 之外的接入方式。此需求反映了社区对**主流付费 AI 服务整合**的强烈期待，背后是用户在已有订阅与工具链之间寻求无缝连接的诉求。

此外 [#5047](https://github.com/agentscope-ai/QwenPaw/issues/5047) **「Windows Tauri 桌面端启动特别慢」** 同样有 3 条评论，用户描述启动时间从原本的一两分钟恶化到十几分钟，并伴有无响应状态。该问题虽属老 Issue，但持续获得关注，说明桌面端性能退化已成影响用户日常使用的关键障碍。

## 5. Bug 与稳定性

今日新增/活跃的 Bug 按严重程度排列如下：

| 严重程度 | Issue | 摘要 | 修复 PR 现状 |
|----------|-------|------|--------------|
| **严重** | [#5172](https://github.com/agentscope-ai/QwenPaw/issues/5172)（已关闭） | 聊天会话过一段时间后再次对话一直等待，点停止报错 `Task has been cancelled!`，影响 QQ/微信等无法手动停止的场景。 | 虽已关闭，但关闭原因未指明修复方式，需关注是否已有后续补丁。 |
| **高** | [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171) | 上下文压缩时，若人设文件 token 超过保留阈值，会将上下文完全压缩为 0，导致任务信息完全丢失。 | 暂无对应 PR。 |
| **中** | [#5174](https://github.com/agentscope-ai/QwenPaw/issues/5174) | Cron agent 无法产出知识文件，心跳 agent 不执行知识提取重任务，怀疑是定时/心跳机制的固有限制。 | 暂无 PR。 |
| **低** | [#5047](https://github.com/agentscope-ai/QwenPaw/issues/5047) | Tauri 桌面端启动极度缓慢（10+ 分钟），Windows 11 环境复现。 | 无直接修复 PR；多个用户在等待中。 |

另外，社区贡献者 **ly-wang19** 提交的 6 个修复 PR（#5035、#5170、#5040、#5037、#5041、#5038）均处于 **Under Review** 状态，涵盖 llama.cpp 版本号解析、缓存文件读取、定时任务 JSON 解析、Linux 浏览器检测、备份跳过不可读文件、上下文空列表保护等边界情况。这些 PR 若合并，将明显提升项目的鲁棒性。

## 6. 功能请求与路线图信号

以下新提出的功能请求反映了用户对 **国际化** 和 **渠道扩展** 的明确需求，可能与下一版本路线图相关：

- **[#5169](https://github.com/agentscope-ai/QwenPaw/issues/5169)**：请求添加**越南语（vi）** 界面语言，提供如印尼语（#4219）、巴西葡萄牙语（#4294）相同的实现方式。项目已支持 6 种语言，越南语是自然延伸。
- **[#5168](https://github.com/agentscope-ai/QwenPaw/issues/5168)**：请求添加**官方 Zalo Bot 渠道**，因 Zalo 是越南主流即时通讯平台，类似 Telegram/WhatsApp 在本地的重要性。此需求与越南语界面请求形成协同，暗示项目在越南市场的潜在用户群体。
- **[#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156)**：支持 `kimi-for-coding` API，解决已订阅 Kimi 套餐用户无法接入的痛点。若项目计划拓展第三方模型接入面，此需求优先级较高。

此外，PR [#2498（已合并）](https://github.com/agentscope-ai/QwenPaw/pull/2498) 对多语言支持进行了改进，为后续新增语言（如越南语）降低了落地门槛。

## 7. 用户反馈摘要

- **满意度较高**：越南语和 Zalo 渠道的请求用户均以 respectful 语气表达需求，对项目目前功能表示认可（“感谢团队维护”“great project”）。
- **核心痛点**：
  - 付费订阅无法用：`kimi-for-coding` 用户抱怨“已经付费订阅了 Kimi 的 coding 套餐却没法接入 CoPaw”，指出目前仅支持官方 API 的局限性。
  - 稳定性焦虑：“聊天总出现问完问题没反应一直等待，这么严重问题竟然一直存在”（#5172），用户对长期未修复的对话挂起问题表达失望。
  - 性能退化：Tauri 桌面端从“一两分钟”变成“十几分钟”启动时间，用户尝试卸载重装无效，对版本变更导致体验倒退感到困惑。

## 8. 待处理积压

以下 Issue 或 PR 长期未得到官方回应或修复，建议维护者近期关注：

| 项 | 类型 | 创建时间 | 摘要 | 链接 |
|----|------|----------|------|------|
| #5047 | Bug | 2026-06-09 | Windows Tauri 桌面端启动极慢（10+ 分钟），至今无官方评论或指派。 | [链接](https://github.com/agentscope-ai/QwenPaw/issues/5047) |
| #5035 | PR（待合并） | 2026-06-09 | 修复 llama.cpp 版本号解析依赖固定宽度切片，即将因 build number 超过 9999 而崩溃。 | [链接](https://github.com/agentscope-ai/QwenPaw/pull/5035) |
| #5040 | PR（待合并） | 2026-06-09 | 修复定时任务 JSON 中单个作业格式错误会导致全部任务失败的问题。 | [链接](https://github.com/agentscope-ai/QwenPaw/pull/5040) |
| #5041 | PR（待合并） | 2026-06-09 | 修复备份时因单个文件不可读导致整个备份失败的问题（Windows 环境下高概率触发）。 | [链接](https://github.com/agentscope-ai/QwenPaw/pull/5041) |

以上 6 个 PR 均由同一位贡献者 ly-wang19 提交，且均标记为 `first-time-contributor`，建议项目维护者加速审核，以鼓励社区贡献热情并提升项目稳定性。

---

**日报生成日期**：2026-06-14  
**数据来源**：GitHub (agentscope-ai/QwenPaw)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 ZeroClaw 项目数据，生成了以下项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-06-14

## 1. 今日速览

ZeroClaw 项目在 **2026-06-14** 显示出极高的活跃度，24小时内共有42条 Issue 和50条 PR 更新。社区讨论热烈，多个关于核心架构、安全与用户体验的大规模功能请求（`RFC`）正在深入讨论，同时也有几个严重的 `S1` 级阻断性 Bug 被报告并获得了快速响应。项目的“功能路线图”与“稳定性和 Bug 修复”两条主线并行推进，整体项目健康度良好，但需要处理新兴的重大问题。

## 2. 版本发布

无。

## 3. 项目进展

今日项目在架构统一和核心功能完善上取得了关键进展。

- **核心架构统一**：Issue #7415 `RFC: Unify the three agent turn engines` 已关闭。该 RFC 提议将三种不同的 Agent 处理循环合并为一个，旨在消除重复逻辑并提高模块化。该 RFC 经由维护者指导，已通过一个**单一的合并 PR** （#7540）完成执行。这标志着项目在核心 Agent 执行引擎上迈出了重要的一步，降低了未来的维护成本与潜在 Bug。
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/7415
- **Cron 任务管理增强**：PR #7398 `feat(cron): add pause/resume for scheduled tasks` 已被合并。此功能允许用户无需删除和重新创建即可暂停/恢复定时任务，提升了对日常任务编排的灵活性和易用性。
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/pull/7398
- **安全与配置边界**：多个关于安全风险配置（如 `allowed_tools` 对 MCP 工具无效 #6876，OpenAI 提供者超时配置被忽略 #6723）的问题已关闭，表明团队正积极清理配置与安全策略上的漏洞。
    - 链接：#6876: https://github.com/zeroclaw-labs/zeroclaw/issues/6876
    - 链接：#6723: https://github.com/zeroclaw-labs/zeroclaw/issues/6723

## 4. 社区热点

今日社区讨论主要集中在两个高影响力的 `RFC` 和一个备受期待的新特性上。

1.  **Dream Mode（#5849）- 评论数最多（18条）**
    - **诉求**：用户 `Svtter` 提出的让 Agent 在空闲时进行后台记忆整合和反思学习的“梦想模式”。这获得了社区的广泛讨论，反映了用户对 Agent 更加智能、更具“生命感”的深层需求。
    - **分析**：该功能若实现，将显著提升 Agent 的长期记忆和个性化能力，是通往强学习型 Agent 的关键一步。已有对应的 **PR #6693** 在等待合并。
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/5849

2.  **RFC: 统一的插件系统（#7420 & #7497）- 评论数各3条和2条**
    - **诉求**：两个 RFC 分别提出了“原生动态链接库插件系统”（#7420）和“OCI 容器注册表作为 WASM 插件的存储与发现机制”（#7497）。这表明社区对插件的**安全性、可扩展性和使用体验**有较高要求，希望超越简单的 JSON 索引文件方式。
    - **分析**：社区开始深入探讨插件的底层架构设计，这对于 ZeroClaw 作为一个 AI 助手生态平台至关重要。最终方向将对项目未来的可扩展性产生深远影响。
    - 链接：#7420: https://github.com/zeroclaw-labs/zeroclaw/issues/7420
    - 链接：#7497: https://github.com/zeroclaw-labs/zeroclaw/issues/7497

## 5. Bug 与稳定性

今日有多达 6 个 `S1 - workflow blocked` 级别的严重 Bug 被报告，主要集中在 WebSocket 通信、Dashboard 可用性和桌面端兼容性上。幸运的是，其中一些 Bug 已得到快速响应，并有修复 PR 提交。

- **[S1 Bug]  Web Dashboard 不可用（#7523）**：macOS 用户通过 Homebrew 安装后，无法访问 Web 控制台，构建流程说明不清晰。
    - 状态：Open
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/7523
- **[S1 Bug] `canvas` 工具回归问题（#7563）**：`#6986` 的合并引入了回归，导致 WebSocket 会话中的 `/canvas` 页面空白。
    - 状态：**Open，新报告**
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/7563
- **[S1 Bug] `ask_user` 在 Web Dashboard 中失败（#7542）**：当 Agent 在 WebSocket 会话中调用 `ask_user` 工具时，立即失败并显示误导性错误。**已有多个修复 PR** (#7584, #7586, #7588)。
    - 状态：**Open，有修复PR**
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/7542
- **[S1 Bug] macOS 桌面应用无法工作（#7527）**：安装后无法检测权限，显示空白页面。
    - 状态：Open
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/7527
- **[S1 Bug] `quickstart` 死循环（#7507）**：在非 TTY 环境下运行 `quickstart` 命令会无限重绘，并产生 4.3GB 的日志输出。
    - 状态：**已关闭**
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/7507
- **[S1 Bug] `web_fetch` 在 WhatsApp 中失效（#6223）**：用户反馈该工具在 WhatsApp Web 渠道中无法使用。
    - 状态：**已关闭**
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/6223
- **[Bug] MCP 工具未被风险配置文件限制（#6876）**：`allowed_tools` 配置对 MCP 工具不生效，这是一个文档或设计上的“坑”。**已关闭**。
    - 状态：已关闭
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/6876

## 6. 功能请求与路线图信号

除上文提到的热点外，以下新功能需求也反映了产品演进方向，很可能被纳入后续版本规划：

- **`delegate` 工具语义变更（#7514）**：请求允许委派给具有不同风险配置文件的子代理，以实现更有效的关注点分离。这反映了用户对复杂多 Agent 协作场景的需求。
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/7514
- **多会话支持（#7543）**：用户希望 Web Chat UI 能支持多个独立会话（新建、切换、重命名），而非单一会话。这是提升 Web UI 基础用户体验的关键特性。
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/7543
- **`file_read` 工具支持更多编码（#7521）**：当前工具在读取非 UTF-8 的文本文件（如 Latin-1, Shift-JIS）时，会输出乱码。用户希望增加自动字符集检测功能。
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/7521
- **支持中文 IM 平台的流式卡片消息（#7531）**：用户请求为 QQ、钉钉、飞书等平台增加流式卡片消息支持，减少用户等待焦虑。
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/7531

## 7. 用户反馈摘要

从 Issue 评论中可以提炼出一些共性反馈：

- **配置体验问题**：多个 Bug 报告（如 #6723, #6876）都指向配置文件中的某些选项“形同虚设”，实际运行时并未生效。这表明配置系统的**透明度与可靠性**需要加强，用户期望所见即所得。
- **平台兼容性与部署痛点**：macOS 应用不可用（#7527）、Homebrew 安装后 dashboard 无法访问（#7523）以及非 TTY 环境下的回环 Bug（#7507），反映了用户在**非标准或特定部署环境**下遇到的挑战，项目在兼容性测试上仍有提升空间。
- **用户对智能性与人格化的期待**：#5849 的“梦想模式”获得大量关注，表明用户对 Agent 的期望已超越简单的命令执行，希望它能像“伙伴”一样学习和成长。
- **工具路由与安全控制**：用户 `vrurg` 提出的 `delegate` 工具语义变更（#7514）和对 `ask_user` 失败 Bug（#7542）的快速报告，表明其在使用复杂的 Agent 协作和在安全工作流方面有较高要求。

## 8. 待处理积压

以下 Issue 和 PR 长期处于开放或“待作者响应”状态，提醒维护者关注：

- **PR #6693: `feat(memory): add dream mode for periodic memory consolidation`**
    - **状态**：启用了 `needs-author-action` 标签。这是一个与社区热点 #5849 直接相关的大功能 PR，已停留多日，若与维护者方向一致，建议尽快处理。
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/pull/6693
- **PR #6667: `feat(skills): background review fork + skill_manage tool`**（`needs-author-action`）
    - **状态**：同样需要作者响应。
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/pull/6667
- **PR #5797: `feat(providers): add tls_ca_cert_path support for custom inference providers`**（Open）
    - **摘要**：为企业级定制推理端点添加 TLS CA 证书支持，创建于2026-04-16，已开放近两个月，可能对企业用户部署非常关键。
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/pull/5797
- **Issue #6211: `[Feature]: stabilize nodejs version to latest lts`**（Open）
    - **摘要**：一个简单的 CI 改进请求，将 Node.js 版本锁到最新 LTS 版本（v24），已开放一个半月，值得快速处理。
    - 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/6211

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*