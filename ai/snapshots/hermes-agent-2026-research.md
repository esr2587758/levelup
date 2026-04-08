---
title: "我敢说这是2026最强的Agent Harness框架：Hermes Agent 全面调研解读"
source: "https://zhuanlan.zhihu.com/p/2022015752258027715"
author:
  - "[[JustBeClawAI 全干工程师]]"
published:
created: 2026-04-08
description: "我敢说这是2026最强的Agent Harness框架：Hermes Agent 全面调研解读Source: https://github.com/NousResearch/hermes-agentTL;DRHermes Agent 是 Nous Research 开发的开源（MIT）自我改进型 AI Agent 框架，GitH…"
tags:
  - "clippings"
---
> Source: [github.com/NousResearch](https://link.zhihu.com/?target=https%3A//github.com/NousResearch/hermes-agent)

### TL;DR

Hermes Agent 是 [Nous Research](https://zhida.zhihu.com/search?content_id=272252750&content_type=Article&match_order=1&q=Nous+Research&zhida_source=entity) 开发的开源（ [MIT](https://zhida.zhihu.com/search?content_id=272252750&content_type=Article&match_order=1&q=MIT&zhida_source=entity) ）自我改进型 AI Agent 框架，GitHub 17K Stars，207 位贡献者。其核心差异化在于 **内置闭环学习系统** ——能自主创建技能、在使用中改进技能、持久化跨会话记忆、构建用户画像、关键的是它把强化学习也集成了进来，连模型都可以自进化。支持 18+ 模型提供商（含本地推理）、12 个消息平台、6 种执行后端，是目前开源 Agent 领域最活跃的项目之一。

---

### 一、项目基本信息

| 字段 | 内容 |
| --- | --- |
| 项目名称 | NousResearch/hermes-agent |
| Slogan | “The agent that grows with you”（与你一起成长的 Agent） |
| Star 数 | 16,988 (~17K) |
| Fork 数 | 2,068 (~2.1K) |
| Watch 数 | 70 |
| Contributors | 207 人 |
| 主要语言 | Python 92.4%、TeX 3.9%、Shell 0.6%、JavaScript 0.3% |
| License | MIT |
| 最新版本 | v0.5.0 (2026-03-28) |
| 最近更新 | 2026-03-30（今天） |
| 官方网站 | [hermes-agent.nousresearch.com](https://link.zhihu.com/?target=http%3A//hermes-agent.nousresearch.com) |
| Python 要求 | ≥ 3.11 |
| Node.js 要求 | ≥ 18.0.0 |

---

### 二、NousResearch 组织背景

### 2.1 组织概况

**Nous Research** 是美国领先的开源 AI 研究实验室，起源于 2023 年 Discord 社区中 AI 爱好者的草根协作。

- **联合创始人** ：Teknium（灵魂人物，Hermes 模型创造者）、Karan
- **团队规模** ：18 名核心成员 + 大量社区贡献者
- **融资** ：完成 **5000 万美元 A 轮融资** ，由 Paradigm 和 North Island Ventures 领投
- **使命** ： *“通过创建和传播开源语言模型，推进人权和自由”*

### 2.2 产品生态

| 产品 | 定位 |
| --- | --- |
| Hermes 模型系列 | 旗舰开源 LLM（已到 Hermes 4） |
| Hermes Agent | 自主 AI Agent 框架 |
| Nous Portal | API 服务门户（400+ 模型） |
| Psyche | 去中心化分布式训练网络 |
| NousCoder | 代码生成模型 |

### 2.3 Hermes 模型演进

| 时间 | 模型 | 核心进展 |
| --- | --- | --- |
| 2023 初 | Hermes (原版) | 首个版本，指令遵循 |
| 2023 中 | Hermes 2 | 改进训练数据，OpenHermes 2.5 数据集 |
| 2024.03 | Hermes 2 Pro | 里程碑：原生 Function Calling + JSON Mode，90% 调用准确率 |
| 2024.08 | Hermes 3 | 旗舰版，高级 Agentic 能力，8B/70B/405B 三规格 |
| 2025.06 | Hermes 4 | 统一推理-对话模型，40 万+ 训练样本，<think> 混合推理 |

> Hermes 模型以”无审查/最少过滤”著称，在 HuggingFace 上发布 **126 个模型** 、 **39 个数据集** 。

---

### 三、核心功能与架构

### 3.1 六大核心能力

### 1️⃣ 闭环学习系统（最大差异化）

Hermes Agent 是目前 **唯一内置学习闭环** 的开源 Agent：

```
用户交互 → 工具调用 → 任务完成
    ↓
自主技能创建 → 技能自我改进
    ↓
持久化记忆 (MEMORY.md, USER.md)
    ↓
FTS5 会话搜索 + LLM 摘要
    ↓
Honcho 辩证式用户建模
    ↓
下次对话：注入记忆 + 用户模型 → 更好的响应
```

**五层记忆架构** ：

| 层级 | 类型 | 持久性 |
| --- | --- | --- |
| L1 | Transformer 上下文（短期推理） | 会话内 |
| L2 | SKILL.md 程序性知识 | 永久 |
| L3 | 向量存储索引 | 永久 |
| L4 | Honcho 辩证式用户建模（正-反-合循环，服务端 LLM 融合生成自然语言画像） | 持续进化 |
| L5 | FTS5 全文检索 + LLM 摘要 | 永久 |

### 2️⃣ 多平台接入（12 个消息平台 + CLI）

| 平台类别 | 支持 |
| --- | --- |
| 即时通讯 | Telegram、Discord、Slack、WhatsApp、Signal、Matrix、Mattermost |
| 企业协作 | DingTalk（钉钉）、Feishu/Lark（飞书）、Email |
| 智能家居 | Home Assistant |
| 通用 | Webhook、API Server（OpenAI 兼容）、CLI TUI |

所有平台通过单一 Gateway 进程统一管理。

### 3️⃣ 40+ 内置工具

| 工具类别 | 功能 |
| --- | --- |
| Web | 搜索（Exa/Parallel/Firecrawl）+ 内容提取 |
| 终端 | 命令执行（6 种后端） |
| 文件 | 读写、模糊匹配 Patch、搜索 |
| 浏览器 | 自动化（navigate/snapshot/click/type 等 11 个子工具） |
| 视觉 | 图像分析 |
| 图像生成 | AI 图像生成（via fal.ai） |
| TTS | 文字转语音（Edge TTS 免费 + ElevenLabs + OpenAI） |
| MoA | 混合代理高级推理 |
| 技能 | 技能浏览、创建、编辑、自我改进 |
| 记忆 | 持久化跨会话记忆 |
| 会话搜索 | FTS5 全文搜索 + LLM 摘要 |
| 子代理 | 隔离子 Agent 并行执行 |
| Cron | 定时任务调度 |
| MCP | 外部工具发现与集成 |
| 安全 | 命令审批、SSRF 防护、Prompt Injection 检测 |

### 4️⃣ 灵活部署（6 种执行后端）

| 后端 | 适用场景 |
| --- | --- |
| Local | 本地开发（默认） |
| Docker | 容器隔离生产环境 |
| SSH | 远程服务器 |
| Daytona | 无服务器持久化（空闲休眠） |
| Singularity | HPC 集群 |
| Modal | 无服务器 GPU/云（空闲休眠，近零成本） |

### 5️⃣ 子 Agent 委派与并行

- 生成隔离子 Agent 处理并行工作流
- Python 脚本通过 RPC 调用工具，多步流水线零上下文成本

### 6️⃣ 研究就绪

- 批量轨迹生成（并行 Worker + 检查点）
- **Atropos RL 环境** 集成强化学习训练
- 轨迹压缩用于训练数据生产
- WandB 实验追踪

### 3.2 项目架构

```
hermes-agent/
├── agent/              # Agent 核心（提示构建、模型元数据、上下文压缩、显示）
├── tools/              # 40+ 工具（自注册到 registry）
├── hermes_cli/         # CLI 命令行接口
├── gateway/            # 多平台消息网关
│   └── platforms/      # 各平台适配器
├── skills/             # 内置技能库（20+ 类别）
├── optional-skills/    # 可选技能
├── cron/               # 定时任务调度
├── honcho_integration/ # Honcho 用户建模
├── acp_adapter/        # Agent Communication Protocol（编辑器集成）
├── docker/             # Docker 部署
├── environments/       # RL 训练环境
├── run_agent.py        # ★ Agent 运行核心（AIAgent 类、对话循环）
├── model_tools.py      # ★ 工具编排层（发现、注册、调度）
├── toolsets.py          # ★ 工具集定义与组合
├── cli.py              # CLI TUI 主入口
├── mcp_serve.py        # MCP 服务器模式
├── batch_runner.py     # 批量轨迹生成
└── rl_cli.py           # RL 训练 CLI
```

**关键设计模式** ：

- **自注册工具系统** ：每个工具文件导入时通过 `registry.register()` 自动注册
- **Toolset 组合模式** ：工具可嵌套组合（ `includes` 引用其他工具集），用户可交互式启用/禁用
- **并行工具执行** ：智能判断工具批次是否可安全并行（最多 8 Worker 线程）
- **上下文自动压缩** ：接近模型上下文窗口限制时，自动摘要中间对话轮次
- **智能模型路由** ：简单请求用廉价模型，复杂请求用主力模型

---

### 四、模型与提供商支持

### 4.1 支持的提供商（18+）

| Provider | 说明 |
| --- | --- |
| Nous Portal | Nous 自有门户，400+ 模型 |
| OpenRouter | 200+ 模型聚合 |
| Anthropic | Claude 系列直连 |
| OpenAI | GPT 系列 + Codex |
| HuggingFace | HF Inference API |
| DeepSeek | DeepSeek 系列 |
| Z.AI / GLM | 智谱 AI |
| Kimi/Moonshot | 月之暗面 |
| MiniMax | MiniMax 全球/中国 |
| Alibaba (DashScope) | 通义千问 |
| GitHub Copilot | 通过 Copilot API/ACP |
| AI Gateway | Vercel AI Gateway |
| Custom | 任意 OpenAI 兼容端点 |

### 4.2 本地推理

支持 **Ollama、vLLM、llama.cpp** 本地模型推理，无需任何付费 API。

通过 `hermes model` 一键切换模型/提供商，无代码改动，无锁定。

---

### 五、API 与协议

| 接口 | 说明 |
| --- | --- |
| [OpenAI 兼容 API](https://zhida.zhihu.com/search?content_id=272252750&content_type=Article&match_order=1&q=OpenAI+%E5%85%BC%E5%AE%B9+API&zhida_source=entity) | gateway/platforms/api\_server.py 提供 HTTP API |
| MCP 服务器 | mcp\_serve.py 实现 stdio MCP，暴露 10 个工具，可被 Claude Code/Cursor/Codex 调用 |
| ACP 协议 | acp\_adapter/ 实现编辑器集成，支持 VS Code、Zed、JetBrains |
| [agentskills.io](https://link.zhihu.com/?target=http%3A//agentskills.io) | 技能遵循开放标准，已被 11+ 工具采纳（Claude Code、Cursor、GitHub Copilot 等） |

---

### 六、Release 历史

| 版本 | 日期 | 代号/重点 |
| --- | --- | --- |
| v0.5.0 | 2026-03-28 | “The hardening release” — Nous Portal 400+ 模型、HF 一等集成、插件生命周期钩子、供应链安全加固 |
| v0.4.0 | 2026-03-23 | — |
| v0.3.0 | 2026-03-17 | — |
| v0.2.0 | 2026-03-12 | — |

> 4 个 Release 均在 2026 年 3 月发布，迭代速度极快。

---

### 七、竞品对比

> Last updated: 2026-03-30 — 已更新为当前同类 Agent 产品对比（Claude Code、DeerFlow 2.0、Codex CLI、Gemini CLI、Goose、aider）

### 7.1 核心竞品一览

| 项目 | 开发者 | Stars | 开源 | 核心定位 |
| --- | --- | --- | --- | --- |
| Hermes Agent | Nous Research | 17K | ✅ MIT | 自我改进型全能 AI Agent |
| Claude Code | Anthropic | — | ✅ Apache-2.0 | Agentic Coding Harness |
| DeerFlow 2.0 | ByteDance | 53K | ✅ MIT | Super Agent Harness |
| Codex CLI | OpenAI | 68K | ✅ Apache-2.0 | Terminal Coding Agent |
| Gemini CLI | Google | 100K | ✅ Apache-2.0 | Terminal AI Agent |
| Goose | Block | 34K | ✅ 开源 | 全能工程 AI Agent |
| aider | 社区 | 43K | ✅ Apache-2.0 | Terminal AI Pair Programming |

### 7.2 全面功能对比

| 维度 | Hermes Agent | Claude Code | DeerFlow 2.0 | Codex CLI | Gemini CLI | Goose | aider |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Agent 循环 | ReAct | ReAct (Gather→Act→Verify) | LangGraph 状态图 | ReAct | ReAct | ReAct | 编辑循环 |
| 自我改进 | ✅ 闭环学习+技能自创建 | ❌ Auto Memory 仅被动记忆 | ❌ | ❌ | ❌ | ❌ | ❌ |
| 记忆系统 | 五层（FTS5+向量+Honcho+技能+MEMORY.md） | CLAUDE.md + Auto Memory（文件型） | Fact-based 长期记忆 + 摘要 | AGENTS.md + memories 目录 | GEMINI.md + Checkpoint | Memory + Chat Recall + Todo | 配置文件 |
| 模型锁定 | 无锁定（18+ Provider） | 仅 Claude 家族 | 无锁定（10+ Provider） | 偏向 OpenAI | 🔒 锁定 Gemini | 无锁定（30+ Provider） | 无锁定 |
| 本地推理 | ✅ Ollama/vLLM/llama.cpp | ❌ | ✅ 通过自定义端点 | 有限 | ❌ | ✅ Ollama/LM Studio | ✅ |
| 消息平台 | ✅ 12 个（Telegram/Discord/Slack/钉钉/飞书等） | Channels 插件 | ✅ Telegram/Slack/飞书 | ❌ | ❌ | ❌ | ❌ |
| MCP 支持 | ✅ Client + Server | ✅ Client + Server | ✅ HTTP/SSE + OAuth | ✅ Client + Server | ✅ Client + Server | ✅ 深度原生 | ❌ |
| 子 Agent/并行 | ✅ delegate\_tool + 隔离上下文 | ✅ Subagents + Agent Teams + /batch | ✅ Lead + Sub-Agent | ❌ | ❌ | ✅ Summon | ❌ |
| Cron 调度 | ✅ 内置 | ✅ 原生 + 云端定时 | ❌ | ❌ | ❌ | ❌ | ❌ |
| 沙箱执行 | 6 种后端（Local/Docker/SSH/Modal/Daytona/Singularity） | Dev Container + Worktree | Docker + K8s 三级沙箱 | macOS Seatbelt + Docker | 基础 | 权限控制 | 依赖 Git |
| 上下文管理 | 四阶段压缩 + 智能路由 | 自动压缩 + 按需加载 + 1M token | 摘要式 + Checkpointer | 取决于模型 | 1M token | 取决于模型 | Repo Map |
| 扩展机制 | 工具注册 + 技能 + MCP + 插件钩子 | Skills + MCP + Hooks + Plugins（4 层） | Skills + MCP + ACP + Guardrails | MCP + AGENTS.md | MCP + GEMINI.md | MCP 原生 + 扩展 | 配置文件 |
| UI 形态 | CLI + 12 消息平台 | CLI + Desktop + IDE + Web | Web UI + CLI + IM Bot | CLI | CLI | CLI + Desktop | CLI |
| 技能可移植 | ✅ [agentskills.io](https://link.zhihu.com/?target=http%3A//agentskills.io) （11+ 工具采纳） | ✅ [agentskills.io](https://link.zhihu.com/?target=http%3A//agentskills.io) | ❌ | ❌ | ❌ | ❌ | ❌ |
| RL 训练 | ✅ Atropos + 轨迹压缩 | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| 适合场景 | 长期个人/团队助手 | 编码 + 工程自动化 | 研究 + 复杂编排 | 编码任务 | 编码 + 脚本 | 全能工程自动化 | 结对编程 |

### Hermes Agent vs DeerFlow 2.0

DeerFlow 2.0 是字节跳动开源的”Super Agent Harness”，53K Stars。两者差异在于 **架构复杂度和使用门槛** ：

- **DeerFlow 2.0 是框架级产品** ，基于 LangGraph 构建，提供从 Agent 编排、记忆、沙箱（Docker/K8s）到 IM 集成的完整企业级基础设施。支持 Guardrails 安全防护、LangSmith 可观测性、三级上下文工程（Session/Channel/User）。但 **复杂度极高** ，配置项繁多，学习曲线陡峭，且推荐的模型与字节生态（Volcengine/Doubao）深度集成。
- **Hermes Agent 是产品级工具** ，开箱即用（ `curl | bash` 一键安装），不需要 LangGraph/LangChain 知识。它更像一个”长在你手机里的 AI 助手”，通过 Telegram 等平台随时触达，拥有自我改进能力，适合个人和小团队。

| 谁更强 | DeerFlow 2.0 | Hermes Agent |
| --- | --- | --- |
| 企业级编排 | ✅ LangGraph + K8s 沙箱 + Guardrails | 够用但非强项 |
| 上手门槛 | ❌ 高（需配置 YAML、Docker、K8s） | ✅ 低（一键安装） |
| 自我改进 | ❌ | ✅ 闭环学习 |
| 消息平台 | Telegram/Slack/飞书 | 12 个平台 |
| 可观测性 | ✅ LangSmith 原生集成 | 基础日志 |
| 研究训练 | ❌ | ✅ RL 训练 + 轨迹压缩 |

### Hermes Agent vs Goose / Codex CLI / Gemini CLI / aider

这四个项目都是 **编码/终端 Agent** ，定位与 Hermes Agent 有本质差异：

- **它们都没有自我改进能力** ——无法自动创建技能并在使用中改进
- **Goose** 最接近 Hermes 的模型自由度（30+ Provider），且 MCP 原生设计最彻底
- **Gemini CLI** Stars 最多（100K），但完全锁定 Google Gemini 模型
- **Codex CLI** 有最好的沙箱安全（macOS Seatbelt），但偏向 OpenAI 生态
- **aider** 的 Repo Map（tree-sitter 代码库索引）是独特的竞争力，专精结对编程

### 7.4 Hermes Agent 的差异化定位

综合对比后，Hermes Agent 的核心差异化可以归结为三点：

1. **唯一的闭环学习系统** — 所有竞品（包括 Claude Code）都是无状态或被动记忆型。Hermes Agent 是唯一能自动创建技能、在使用中改进技能、构建辩证式用户画像的 Agent。
2. **最广泛的消息平台覆盖** — 12 个平台原生集成（Telegram/Discord/Slack/WhatsApp/Signal/钉钉/飞书等），没有任何竞品能做到。Claude Code 通过 Channels 插件支持部分平台，DeerFlow 支持 3 个，其余全部 CLI only。
3. **真正的模型无关 + 研究就绪** — 18+ 提供商 + 本地推理 + RL 训练 + 轨迹压缩。Nous Research 作为顶级开源模型实验室，Hermes Agent 不仅是用户工具，也是训练下一代工具调用模型的数据飞轮。

---

### 八、社区反馈

### 正面评价 ✅

| 评价 | 来源 |
| --- | --- |
| “10⁄10 — 相当于已调试一周的 OpenClaw + RAG + 记忆持久化 + 更好的工具调用” | Reddit |
| “Hermes 配 OpenAI Codex 简直超级强” | Reddit |
| “我喜欢它的记忆管理，在树莓派级设备上也能运行” | Reddit |
| “有所有我关心的功能，没有多余臃肿，比 OpenClaw 更安全可审计” | Reddit |
| “自我改进是真的——做复杂任务时会自动创建技能” | Reddit |
| “真诚推荐优于 OpenClaw，OpenClaw 烧钱像流水” | Reddit |

### 需注意 ⚠️

| 关注点 | 详情 |
| --- | --- |
| Honcho 记忆默认未启用 | 需手动开启才获得自我改进能力 |
| 模型选择影响大 | 小模型（4B）效果有限，推荐 30B+ |
| 24⁄7 运行成本 | 云端 API 持续运行费用不低 |
| 新项目存在 Bug | 部分用户首次配置遇到问题 |

---

### 九、快速安装

```
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

支持 Linux、macOS、WSL2。安装脚本自动处理 Python、Node.js 和所有依赖。

Docker 部署：

```
docker run -v hermes-data:/opt/data nousresearch/hermes-agent
```

---

### 十、结论

### 适合选择 Hermes Agent 的场景

- ✅ 需要一个 **长期使用、越用越聪明** 的个人 AI 助手
- ✅ 需要 **本地/私有化部署** ，零 API 成本
- ✅ 需要在 **Telegram/Discord/Slack 等多平台** 随时触达 Agent
- ✅ 需要 Agent 具有 **持久记忆和自我改进** 能力
- ✅ 需要 **research-ready** 的 Agent 框架用于 RL 训练和数据生成

### 不太适合的场景

- ❌ 需要 **快速搭建多角色 Agent 团队**
- ❌ 只需要最简单的 **API 集成** （OpenAI SDK 更轻量）

### 总体评价

Hermes Agent 的最大赌注是： **Agent 的价值不仅在于单次任务完成，更在于长期积累的知识和对用户的理解** 。这是目前其他框架尚未涉足的方向。项目处于快速迭代期（一个月内 4 个 Release），17K Stars 和活跃社区表明市场认可度高。作为 Nous Research 这样的顶级开源模型实验室推出的产品，其在模型-Agent 协同优化上的潜力值得关注。

---

### 实现原理深度剖析

本次调研包含了对 Hermes Agent 源码的逐文件阅读和技术分析，覆盖以下核心子系统：

- **Agent 主循环（ReAct Loop）** ：双重迭代保护、三种 API 模式适配、工具调用验证与自愈、Fallback 逻辑
- **工具系统** ：自注册机制、Toolset 组合、并行安全判断（白名单 + 路径重叠检测）、异步桥接
- **记忆系统** ：MEMORY.md 文件存储、FTS5 全文检索、Honcho 辩证式用户建模
- **技能系统** ：延迟加载、自动创建、使用中自我改进、 [agentskills.io](https://link.zhihu.com/?target=http%3A//agentskills.io) 兼容
- **上下文管理** ：四阶段压缩流水线、否决式智能路由、Anthropic prompt caching
- **消息网关** ：适配器模式、非阻塞处理、会话中断、照片合并、智能分块
- **子 Agent 委派** ：上下文隔离、工具集交集安全、深度限制、全局状态保护
- **Cron 调度** ：文件锁保护、\[SILENT\] 机制、独立 Agent 实例
- **MCP 集成** ：独立事件循环、双传输、动态工具发现、Sampling 支持

### 一、Agent 主循环：ReAct 模式的工业级实现

Hermes Agent 的心脏是 `run_agent.py` 中的 `AIAgent` 类，核心方法 `run_conversation()` 是一个约 2300 行的巨型方法，实现了工业级的 ReAct（Reasoning + Acting）循环。理解这个循环，就理解了整个 Agent 的运转逻辑。

### 1.1 循环的骨架

主循环的设计异常清晰——一个 `while` 循环不断与 LLM 对话，直到 LLM 决定不再调用工具、直接回复用户为止：

```
while api_call_count < self.max_iterations and self.iteration_budget.remaining > 0:
    # 1. 中断检查
    if self._interrupt_requested:
        interrupted = True
        break

    # 2. 消耗迭代预算
    api_call_count += 1
    if not self.iteration_budget.consume():
        break

    # 3. 构造 API 消息
    api_messages = self._build_api_messages(messages, ...)

    # 4. 发起 API 调用（始终流式）
    response = self._interruptible_streaming_api_call(api_kwargs, ...)

    # 5. 处理响应：分流
    if assistant_message.tool_calls:
        self._execute_tool_calls(assistant_message, messages, ...)
        continue  # 回到循环顶部，让 LLM 看到工具结果
    else:
        final_response = assistant_message.content
        break  # LLM 不再需要工具，循环结束
```

这个 “思考-行动-观察” 的节奏非常明确：LLM 思考后，要么调用工具（行动），等待工具结果（观察），然后回到循环顶部再次思考；要么直接输出最终回复。

### 1.2 双重迭代保护

循环有两层保护机制。第一层是简单的 `api_call_count < max_iterations` （默认 90 次）。第二层是线程安全的 `IterationBudget` 计数器：

```
class IterationBudget:
    def consume(self) -> bool:
        with self._lock:
            if self._used >= self.max_total:
                return False
            self._used += 1
            return True

    def refund(self) -> None:
        with self._lock:
            if self._used > 0:
                self._used -= 1
```

`refund()` 方法是一个巧妙的设计—— `execute_code` 类型的工具调用会退还迭代次数，因为它们是廉价的 RPC 调用，不应消耗 Agent 的”思考预算”。

当迭代接近上限时，系统还会在工具结果中注入”预算压力”警告：70% 时温和提醒，90% 时紧急警告。这些警告会在下一轮会话开始时被自动清除，不污染历史记录。

### 1.3 消息数组的精细组装

每次循环迭代，系统从内部持久化的 `messages` 列表构造一个临时的 `api_messages` 。这个过程并非简单复制，而是一个多层加工：

- **Honcho 上下文注入** ：首轮融入系统提示，后续轮次附加到用户消息（避免破坏 Anthropic 的 prompt cache 前缀命中）
- **推理连续性** ：对支持多轮推理的模型（如 Moonshot、Novita），将历史 `reasoning` 字段转换为 `reasoning_content` 传递
- **字段清洗** ：移除 `finish_reason` 、 `reasoning` 等仅内部使用的字段

系统提示（system message）由多层组成，只构建一次并缓存复用：

1. **Agent 身份** ：优先加载项目中的 `SOUL.md` ，否则使用默认身份
2. **工具使用指导** ：根据实际加载的工具集动态注入
3. **工具使用强制** ：对特定模型（如 GPT 系列）注入额外指导，防止模型”描述”工具使用而不是真正发起调用
4. **上下文文件** ： `AGENTS.md` 、`.cursorrules` 等项目级指导
5. **插件上下文** ：通过 `pre_llm_call` 钩子注入的临时内容

### 1.4 三种 API 模式的统一适配

Hermes Agent 同时支持三种不同的 LLM API 协议：

```
if self.api_mode == "codex_responses":
    # OpenAI Responses API（Codex 专用）
    ...
elif self.api_mode == "anthropic_messages":
    # Anthropic Messages API
    stop_reason_map = {"end_turn": "stop", "tool_use": "tool_calls", "max_tokens": "length"}
    finish_reason = stop_reason_map.get(response.stop_reason, "stop")
else:
    # Chat Completions API（标准路径，覆盖绝大多数提供商）
    finish_reason = response.choices[0].finish_reason
```

`_build_assistant_message()` 方法将三种 API 的原始响应统一转化为包含 `content` 、 `tool_calls` 、 `reasoning` 的规范化内部消息格式，上层代码完全不需要关心底层用的是哪种 API。

### 1.5 工具调用验证与自愈

LLM 返回的工具调用并不总是正确的。系统实现了多层验证和自愈：

1. **工具名修复** ：自动修复模型的工具名幻觉（如 `web-search` → `web_search` ）
2. **无效工具名检测** ：注入错误消息让模型自我修正，3 次失败后放弃
3. **JSON 参数验证** ：空字符串自动转为 `{}` ，3 次 JSON 解析失败后注入错误结果
4. **后置防护** ：单次最多一个 `delegate_task` 调用；去重相同的工具调用

这种”给模型纠错机会”的设计，比直接报错要优雅得多——大多数情况下模型在看到错误反馈后会自我修正。

### 1.6 Fallback 逻辑

有时 LLM 在一个 turn 中同时输出了文本内容和工具调用。文本内容会被缓存到 `_last_content_with_tools` 。如果后续 LLM 返回空内容（比如 think-only 响应），就使用这个缓存作为最终回复：

```
if turn_content and self._has_content_after_think_block(turn_content):
    self._last_content_with_tools = turn_content

# 后续空回复时 fallback
if not self._has_content_after_think_block(final_response):
    fallback = getattr(self, '_last_content_with_tools', None)
    if fallback:
        final_response = self._strip_think_blocks(fallback).strip()
        break
```

这个设计防止了一种常见的失败模式：模型在中间轮次给出了很好的回答，但在最后一轮工具调用后没有再生成文本。

---

### 二、工具系统：自注册、组合、并行

### 2.1 自注册机制

Hermes Agent 的工具系统采用”自注册”模式。每个工具文件（如 `tools/terminal_tool.py` ）在被 Python 导入时，其模块级代码会自动向全局 `ToolRegistry` 注册自己：

```
# tools/terminal_tool.py
from tools.registry import registry

TERMINAL_SCHEMA = {
    "name": "terminal",
    "description": "Execute a shell command...",
    "parameters": {
        "type": "object",
        "properties": {
            "command": {"type": "string"},
            "background": {"type": "boolean"},
            "timeout": {"type": "integer"},
        },
        "required": ["command"]
    }
}

def _handle_terminal(args, **kw):
    return terminal_tool(command=args.get("command"), ...)

registry.register(
    name="terminal",
    toolset="terminal",
    schema=TERMINAL_SCHEMA,
    handler=_handle_terminal,
    check_fn=check_terminal_requirements,
    emoji="💻",
)
```

注册参数包括：工具名（全局唯一）、所属工具集、OpenAI Function Calling 格式的 JSON Schema、实际执行函数、可选的可用性检查函数，以及用于 CLI 显示的 emoji。

工具发现由 `model_tools._discover_tools()` 驱动，它使用 `importlib.import_module()` 强制导入所有工具模块，触发它们的模块级注册代码。失败的模块不会阻止其他模块加载——这保证了即使某个工具的依赖缺失（比如没装浏览器），其余工具仍然正常工作。

### 2.2 工具集（Toolset）组合系统

工具通过 **Toolset** 进行分组和组合。 `toolsets.py` 中定义了一个简洁的字典结构：

```
TOOLSETS = {
    "web":        {"tools": ["web_search", "web_extract"]},
    "terminal":   {"tools": ["terminal", "process"]},
    "file":       {"tools": ["read_file", "write_file", "patch", "search_files"]},
    "debugging":  {"tools": ["terminal", "process"], "includes": ["web", "file"]},
    "hermes-cli": {"tools": _HERMES_CORE_TOOLS},
    ...
}
```

注意 `debugging` 工具集通过 `includes` 字段组合了 `web` 和 `file` 两个工具集——这种嵌套组合使得工具管理非常灵活。

`resolve_toolset()` 实现了带循环检测的递归解析。 `visited` 集合在兄弟 includes 之间共享，确保菱形依赖只解析一次。

所有平台（CLI、Telegram、Discord 等）共享同一个 `_HERMES_CORE_TOOLS` 列表（约 40+ 工具），编辑一处即可更新所有平台的工具配置。

### 2.3 check\_fn：可用性检查

每个工具可以注册一个可用性检查函数。比如 `web_tools` 注册了 `check_web_api_key()` ，检查是否有搜索 API 密钥。没有密钥的环境中，web 工具不会出现在 LLM 的工具列表里。

`get_definitions()` 会缓存 check 结果——多个工具共享同一个 `check_fn` 时，只调用一次。这避免了不必要的重复检查（比如多个 web 工具共享同一个 API key 检查）。

### 2.4 并行工具执行

当 LLM 在一个 turn 中返回多个工具调用时，系统需要决定是串行还是并行执行。这个决策由 `_should_parallelize_tool_batch()` 做出，采用白名单制——只有明确标记为安全的工具才能并行：

```
_PARALLEL_SAFE_TOOLS = frozenset({
    "read_file", "search_files", "web_search", "web_extract",
    "vision_analyze", "session_search", "skill_view", ...
})

_PATH_SCOPED_TOOLS = frozenset({"read_file", "write_file", "patch"})
```

对于路径作用域的文件工具，系统还会检查路径是否重叠。 `write_file(/a/b)` 和 `read_file(/a/b/c)` 不能并行（路径有包含关系），但 `read_file(/a/b)` 和 `write_file(/a/c)` 可以。

并行执行使用 `ThreadPoolExecutor` （最多 8 个工作线程），结果数组保证按原始顺序返回。串行路径则支持更丰富的交互：中断检查、文件变更前的 checkpoint、破坏性命令检测等。

### 2.5 异步工具的桥接

部分工具（如 web 搜索）是异步实现的。注册表的 `dispatch()` 自动检测并桥接：

```
def dispatch(self, name, args, **kwargs):
    entry = self._tools.get(name)
    if entry.is_async:
        return _run_async(entry.handler(args, **kwargs))
    return entry.handler(args, **kwargs)
```

`_run_async()` 的实现考虑了三种场景：已在异步上下文中（开新线程）、工作线程（使用线程局部的持久事件循环）、主线程（使用全局持久事件循环）。使用持久化事件循环而非 `asyncio.run()` 是经过深思熟虑的——后者会在完成后关闭循环，导致缓存的 `httpx` 客户端在 GC 时触发 “Event loop is closed” 错误。

---

### 三、记忆系统：从 Markdown 文件到辩证式用户建模

Hermes Agent 宣称的”自我改进”能力，核心来自它的多层记忆系统。这不是一个统一的向量数据库，而是三个独立但协作的子系统，各自选择了最适合其场景的存储方式。

### 3.1 核心记忆：MEMORY.md

记忆工具（ `tools/memory_tool.py` ）的存储方案出人意料地简单——纯 Markdown 文件。Agent 的持久化记忆写在 `~/.hermes/memory/MEMORY.md` 中，每条记忆是一个时间戳标记的 Markdown 段落。

记忆工具注册了三个操作： `save` （保存新记忆）、 `search` （搜索现有记忆）、 `delete` （删除记忆）。在实现上， `save` 就是向文件追加一段带时间戳的 Markdown； `search` 是对文件内容做关键词匹配； `delete` 则移除匹配的段落。

这个设计的核心优势是 **可审计性** ——用户可以直接打开 MEMORY.md 查看 Agent 记住了什么，甚至手动编辑。相比向量数据库的黑箱，这对用户信任至关重要。

记忆注入到对话中的方式也很直接： `prompt_builder.py` 在构建系统提示时读取 MEMORY.md 的内容，作为一个专门的段落插入系统提示。同时注入一段使用指导，提醒 Agent 在合适的时机主动保存新记忆。

### 3.2 会话搜索：SQLite FTS5

`tools/session_search_tool.py` 实现了跨会话的全文检索，让 Agent 能够回忆过去的对话。技术上使用 SQLite 的 FTS5 虚拟表：

```
CREATE VIRTUAL TABLE IF NOT EXISTS session_fts USING fts5(
    session_id,
    role,
    content,
    timestamp,
    tokenize='porter unicode61'
)
```

`porter unicode61` 分词器同时支持英文词干提取和 Unicode（包括中文）。每个会话结束时，对话消息被写入 FTS5 索引。

搜索时，工具先通过 FTS5 的 `MATCH` 语法检索相关消息，然后调用辅助 LLM（auxiliary client——通常是一个更便宜的模型）对检索结果做摘要，提炼出与当前问题最相关的信息。

这个”检索 + LLM 摘要”的两阶段设计是 RAG 的经典模式。FTS5 的优势在于零外部依赖、毫秒级查询、支持中文，且 SQLite 文件天然具备可移植性。

### 3.3 Honcho 用户建模：辩证式画像

Honcho 是 Plastic Labs 开发的用户建模引擎（ `honcho_integration/` ）。这里需要重点解释”辩证法建模”到底是什么意思，以及它在代码层面如何实现。

### 3.3.1 什么是辩证法用户建模

传统的用户画像是 **累积式** 的：每次观察到一个新事实（”用户喜欢 Python”），就加一条记录。随着时间推移，画像膨胀且可能自相矛盾（”用户喜欢 Python”和一周后的”用户开始转向 Rust”并存）。

Honcho 的辩证法借鉴了黑格尔的”正-反-合”逻辑：

1. **正题（Thesis）** ：当前对用户的理解（画像的现状）
2. **反题（Antithesis）** ：新的对话中出现了与当前理解矛盾或补充的信息
3. **合题（Synthesis）** ：用 LLM 将正题和反题融合，生成一个 **更新的、更准确的** 用户理解

这个过程不是 Hermes Agent 端实现的，而是 **Honcho 服务端实现的** 。Hermes Agent 只是 Honcho 的客户端——它通过 API 将对话数据发送给 Honcho，Honcho 在服务端用自己的 LLM 执行辩证推理，返回更新后的用户画像。

### 3.3.2 具体运转流程

整个循环在 Agent 与 Honcho 服务之间运转：

```
[Agent 对话]                         [Honcho 服务端]
     │                                     │
     │  1. 对话结束时，Agent 发送            │
     │     消息历史到 Honcho                 │
     ├────────────────────────────────────▶│
     │                                     │  2. Honcho 从消息中提取
     │                                     │     新的用户观察（反题）
     │                                     │
     │                                     │  3. Honcho 取出当前用户
     │                                     │     画像（正题）
     │                                     │
     │                                     │  4. Honcho 用 LLM 将
     │                                     │     正题+反题融合为
     │                                     │     新画像（合题）
     │                                     │
     │  5. 下次对话开始时，Agent             │
     │     请求 Honcho 上下文                │
     ├────────────────────────────────────▶│
     │                                     │
     │◀────────────────────────────────────┤  6. 返回融合后的
     │     注入到系统提示中                   │     用户画像
```

举个例子来说明：

- **第 1 天** ：用户让 Agent 帮忙写 Python 脚本。Honcho 生成正题：”用户是 Python 开发者，偏好脚本化任务”
- **第 5 天** ：用户开始讨论 Rust 的内存安全。这成为反题，与”纯 Python 开发者”矛盾
- **辩证融合** ：Honcho 的 LLM 不是简单追加”也用 Rust”，而是 **重新推理** 生成合题：”用户是有 Python 背景的系统程序员，正在向 Rust 转型，关注性能和安全性”

这个合题比分别罗列事实更有价值——它捕捉了用户的 **发展趋势和动机** 。

### 3.3.3 用户画像的数据结构

Honcho 返回的画像不是结构化的键值对，而是 **自然语言描述** 。这是有意的设计——自然语言描述可以直接注入到 LLM 的系统提示中，无需额外的格式转换。画像内容类似于：

```
This user is an experienced Python developer transitioning to systems
programming with Rust. They value code correctness and performance.
They prefer concise explanations with code examples over lengthy
theoretical discussions. They work on backend services and have
recently started exploring WebAssembly.
```

### 3.3.4 Hermes Agent 端的集成实现

在 Hermes Agent 这一侧，Honcho 的集成分为两层：

**工具层** （ `tools/honcho_tools.py` ）注册四个操作供 Agent 主动使用：

```
# Agent 可以主动调用这些工具
honcho_context   # 获取当前对话的上下文增强信息
honcho_profile   # 查询用户的完整画像
honcho_search    # 在用户历史交互中搜索特定信息
honcho_conclude  # 提交新的观察/结论，触发画像的辩证更新
```

其中 `honcho_conclude` 是触发辩证循环的关键——当 Agent 在对话中观察到有价值的用户信息时，通过这个工具将观察提交给 Honcho 服务，Honcho 在服务端执行正-反-合的融合。

**自动注入层** （ `prompt_builder.py` + `run_agent.py` ）实现无感知的上下文增强：

```
# run_agent.py 中的 Honcho 上下文注入逻辑
if self._honcho_enabled:
    # 首轮对话：嵌入到系统提示中
    if is_first_turn:
        system_prompt += f"\n\n[User Context from Honcho]\n{honcho_context}"
    else:
        # 后续轮次：附加到用户消息中
        # 这是为了不破坏 Anthropic 的 prompt cache 前缀命中
        user_message_content = f"{honcho_context}\n\n{original_user_message}"
```

首轮对话将 Honcho 上下文嵌入系统提示，让 Agent 从一开始就”认识”这个用户。后续轮次为了不破坏 Anthropic 的 prompt cache 前缀（系统提示变化会导致缓存失效），改为将 Honcho 上下文附加到用户消息中。

**集成模块** （ `honcho_integration/` ）封装了与 Honcho 服务的通信细节，包括：

- `honcho-ai` Python SDK 的初始化和配置
- 会话（Session）的创建和管理——每个 Hermes 会话映射到一个 Honcho Session
- 消息的同步——对话消息在会话结束时批量发送给 Honcho
- 用户（User）和应用（App）的 ID 映射

### 3.3.5 为什么默认不启用

Honcho 默认未启用，需要用户手动配置（设置 Honcho API key）。这是有意的设计：

- 用户画像涉及 **隐私敏感数据** ，显式 opt-in 是负责任的做法
- Honcho 是 **外部服务** （由 Plastic Labs 运营），数据会发送到第三方
- 辩证融合需要额外的 LLM 调用，有 **成本和延迟** 开销
- 对于短期/一次性使用场景，用户建模的收益有限

---

### 四、技能系统：Agent 的程序性知识

技能系统是 Hermes Agent “越用越聪明”承诺的核心载体。一个技能本质上是一段结构化的 Markdown 文档，描述了完成某类任务的知识和步骤。

### 4.1 技能的文件结构

每个技能是一个目录，包含一个 `SKILL.md` 文件：

```
skills/
├── software-development/
│   ├── SKILL.md          # 技能定义文档
│   └── templates/        # 可选的模板文件
├── research/
│   ├── SKILL.md
│   └── prompts/
└── creative/
    └── SKILL.md
```

`SKILL.md` 遵循一个约定的 Markdown 结构：标题、触发条件（何时使用）、步骤说明、注意事项等。这个格式被设计为 **人机共读** ——Agent 能理解并执行，人也能直接阅读和编辑。

### 4.2 技能的发现与加载

`agent/skill_utils.py` 负责技能的发现和加载。技能来源有三个层级：

1. **内置技能** （ `skills/` 目录）：随项目发布的预置技能
2. **用户技能** （ `~/.hermes/skills/` ）：用户自定义或 Agent 自动创建的技能
3. **项目技能** （`.hermes/skills/` ）：项目级别的特定技能

发现过程扫描这三个目录，收集所有 `SKILL.md` 文件。然后 `prompt_builder.py` 在构建系统提示时，将所有可用技能的 **索引** （标题和触发条件的简要列表）注入系统提示。注意这里只注入索引而非完整内容——完整的技能文档太长，会浪费上下文窗口。

当 Agent 在对话中判断某个技能与当前任务相关时，通过 `skills_list` 或 `skill_view` 工具加载该技能的完整内容。这是一种 **延迟加载** 策略，在上下文效率和信息可用性之间取得平衡。

### 4.3 技能的自动创建

这是最令人兴奋的部分。 `tools/skill_manager_tool.py` 提供了 `skill_manage` 工具，支持 `create` 、 `edit` 、 `delete` 操作。当 Agent 完成一个复杂任务后，系统提示中的指导会提醒 Agent：如果这个任务的解决方案可能在未来被复用，应该将其沉淀为一个技能。

Agent 通过 `skill_manage` 工具的 `create` 操作，将解决方案写成结构化的 `SKILL.md` 文件，保存到用户技能目录。下次遇到类似任务时，技能索引中会出现这个新技能，Agent 可以加载并参考它。

### 4.4 技能的自我改进

技能改进发生在使用过程中。当 Agent 加载并使用某个技能完成任务后，如果发现技能文档中的步骤不完整、有错误、或者可以优化，它会通过 `skill_manage` 的 `edit` 操作更新技能内容。

这形成了一个 **正反馈循环** ：创建技能 → 使用技能 → 发现改进点 → 更新技能 → 下次使用更好的版本。这正是 “The agent that grows with you” 的含义。

### 4.5 agentskills.io 兼容性

Hermes Agent 的技能格式遵循 `agentskills.io` 开放标准。这意味着为 Hermes 编写的技能可以被 Claude Code、Cursor、GitHub Copilot 等 11+ 工具识别和使用——技能真正实现了跨框架可移植。

---

### 五、上下文管理：压缩、路由与缓存

LLM 的上下文窗口是有限的，而 Agent 的对话可能持续数十轮。如何在有限窗口中保留最重要的信息，是 Agent 框架最核心的工程挑战之一。

### 5.1 上下文压缩：四阶段流水线

`agent/context_compressor.py` 实现了一个精心设计的四阶段压缩流水线，在消息列表接近模型上下文窗口限制时自动触发。

**触发条件** ：系统在每次 API 调用前估算当前消息列表的 token 数。当总 token 数超过模型上下文窗口的某个阈值（通常是 70-80%）时，触发压缩。

**阶段一：确定保护区域** 。对话的头部（系统提示和最初几轮对话）和尾部（最近几轮对话）被标记为”受保护”，不参与压缩。这是因为系统提示包含 Agent 身份和工具定义，最初几轮包含用户意图的建立，最近几轮包含正在进行的推理——这些都是不可压缩的关键信息。

**阶段二：选择压缩候选** 。在保护区域之间的”中间地带”消息被选为压缩候选。优先选择 token 数最多的工具结果消息——它们通常包含大量原始数据（如搜索结果、文件内容），但其中的有用信息密度相对较低。

**阶段三：LLM 摘要** 。调用辅助 LLM（通常是一个更快更便宜的模型）对选中的消息做摘要。摘要的提示经过精心设计，要求保留关键事实、数据和决策，丢弃冗余细节和重复信息。

**阶段四：替换与验证** 。用摘要替换原始消息，然后重新计算 token 数。如果仍然超过阈值，则进入下一轮迭代——选择更多候选、进一步压缩。这个过程可以多次迭代，直到 token 数降到安全范围。

**迭代式摘要更新** 是一个关键特性。如果已经存在的摘要在后续仍然被选为压缩候选（比如对话持续了很长，早期摘要也变得”太旧太长”），系统会将旧摘要和新的上下文一起喂给 LLM，生成一个 **更新的摘要** 。这避免了信息在多次压缩中完全丢失。

### 5.2 智能模型路由

`agent/smart_model_routing.py` 实现了一个成本优化机制：简单请求使用便宜的模型，复杂请求使用主力模型。

路由决策基于一组 **否决式启发规则** 。系统分析用户输入的特征：消息长度、是否包含代码、是否涉及多步推理、是否需要工具调用等。如果触发任何一条”复杂性”规则（如消息超过一定长度、包含技术关键词、需要文件操作），就路由到主力模型。只有所有规则都通过”简单”判断时，才使用廉价模型。

这种否决式设计是保守的——宁愿多用一次贵模型，也不愿因为路由错误导致低质量回复。在实际使用中，日常闲聊和简单查询走便宜模型，编程和复杂推理走主力模型，成本可以降低 30-50%。

### 5.3 Anthropic 提示缓存

`agent/prompt_caching.py` 实现了对 Anthropic API 特有的提示缓存优化。Anthropic 的 prompt caching 允许在消息中标记 `cache_control` 断点，系统可以缓存断点之前的 token，后续请求如果前缀匹配就能复用缓存，节约约 75% 的输入 token 成本。

系统在三个策略位置设置缓存断点：

1. **系统提示的末尾** ——所有对话共享同一个系统提示
2. **早期对话的某个位置** ——利用前几轮对话在同一会话中通常不变的特点
3. **最近上下文的某个位置** ——在最新消息前设置，缓存到此为止的所有历史

缓存断点的位置选择是一个权衡：断点太少浪费缓存机会，断点太多增加 API 负载。系统通过分析消息列表的结构，动态选择最优的断点位置。

### 5.4 模型元数据管理

`agent/model_metadata.py` 管理着每个模型的能力信息：上下文窗口大小、最大输出 token 数、是否支持 vision、是否支持工具调用等。

对于已知的主流模型（如 Claude、GPT 系列），这些信息是硬编码的。对于未知模型（如通过 Custom endpoint 接入的模型），系统会尝试 **上下文探测** ——发送一个逐渐增长的测试消息，观察 API 何时返回 `context_length_exceeded` 错误，由此推断模型的上下文窗口大小。

Token 估算使用一个简单但实用的启发方法：英文约 4 字符一个 token，中文约 2 字符一个 token。这不精确，但对于判断”是否接近上下文限制”已经足够。精确的 tokenization 需要加载每个模型的 tokenizer，对于支持 200+ 模型的框架来说代价太高。

### 5.5 Anthropic 适配器

`agent/anthropic_adapter.py` 处理 Anthropic Messages API 与 OpenAI Chat Completions API 之间的格式差异。主要的转换包括：

- **消息格式** ：Anthropic 要求 `content` 为结构化的 content blocks 数组（TextBlock、ImageBlock、ToolUseBlock），而 OpenAI 使用字符串
- **工具定义** ：Anthropic 的 `input_schema` 对应 OpenAI 的 `parameters`
- **工具结果** ：Anthropic 要求 `tool_result` content block，OpenAI 使用 `role: "tool"` 的消息
- **认证** ：支持 API Key 和 OAuth 两种方式
- **Thinking** ：Anthropic 的 extended thinking 功能需要特殊处理

适配器还处理了 Anthropic 特有的限制，比如按模型设置原生输出限制（Opus 4.6 支持 128K 输出，Sonnet 4.6 支持 64K 输出）。

---

### 六、消息网关：适配器模式的规模化应用

### 6.1 统一抽象

消息网关是 Hermes Agent “随时随地可触达”能力的基础。其核心设计采用经典的 **适配器模式** ：定义一个统一的消息抽象层 `BasePlatformAdapter` ，每个平台实现自己的适配器。

`BasePlatformAdapter` 定义了所有平台必须实现的四个抽象方法：

- `connect()` → 连接到平台并开始接收消息
- `disconnect()` → 断开连接
- `send()` → 发送消息到指定聊天
- `get_chat_info()` → 获取聊天元信息

统一的消息数据结构 `MessageEvent` 是平台无关的归一化表示，包含文本内容、消息类型（TEXT/PHOTO/AUDIO/VOICE 等）、来源信息（平台/聊天 ID/用户 ID）、媒体 URL 列表等。

### 6.2 非阻塞处理与会话中断

网关的消息处理是 **非阻塞** 的—— `handle_message()` 立即返回，通过 `asyncio.create_task` 将实际处理放入后台。

当用户在 Agent 仍在处理上一条消息时发送新消息，系统会触发 **会话级中断** ：

```
if session_key in self._active_sessions:
    if event.message_type == MessageType.PHOTO:
        # 照片连发：不中断，合并到队列
        existing.media_urls.extend(event.media_urls)
        return
    # 普通消息：中断当前处理
    self._pending_messages[session_key] = event
    self._active_sessions[session_key].set()  # 触发中断信号
    return
```

照片连发（Photo Bursts）的特殊处理非常贴心——用户在 Telegram 中连续发多张照片，系统不会中断处理，而是将它们合并为一条多图消息。

### 6.3 富媒体路由

Agent 的回复可能包含多种媒体类型。系统依次执行：

1. 提取 `MEDIA:<path>` 标签（TTS 工具输出的音频文件）
2. 提取 Markdown/HTML 图片 URL
3. 检测裸本地文件路径（兼容不使用特殊语法的小模型）
4. 语音消息自动 TTS
5. 按类型分别发送：文本 → `send()` ，图片 → `send_image()` ，动图 → `send_animation()`

### 6.4 智能消息分块

不同平台有不同的消息长度限制（Telegram 4096 字符、Discord 2000 字符等）。 `truncate_message()` 不仅按长度分割，还会 **保持代码块边界完整** ——如果分割点落在三反引号代码块内部，会在当前块末尾关闭代码围栏，在下一块开头用相同的语言标签重新打开。

### 6.5 GatewayRunner：多平台编排

`GatewayRunner` 是整个网关的控制中枢。在 `start()` 方法中，它遍历所有已配置的平台，为每个平台创建适配器实例，注入统一的消息处理回调和错误处理器，然后并行启动所有平台连接。

`_create_adapter()` 是一个大型工厂方法，支持 14+ 平台（Telegram、Discord、Slack、WhatsApp、Signal、HomeAssistant、Email、SMS、DingTalk、Feishu、WeCom、Mattermost、Matrix 等），按平台枚举动态导入对应模块。

---

### 七、子 Agent 委派：隔离上下文的并行处理

### 7.1 设计理念

子 Agent 委派的核心理念是 **上下文隔离** ：

> 父 Agent 的上下文窗口只看到委派调用和摘要结果，永远不会看到子 Agent 的中间工具调用或推理过程。

这解决了一个关键问题：如果父 Agent 直接执行所有子任务，中间产生的大量数据（搜索结果、日志、文件内容）会迅速填满上下文窗口。通过委派，这些数据被封装在子 Agent 的独立上下文中，父 Agent 只看到最终摘要。

### 7.2 安全约束

子 Agent 有严格的限制：

- **工具限制** ： `delegate_task` （禁止递归委派）、 `clarify` （禁止用户交互）、 `memory` （禁止写入共享记忆）、 `send_message` （禁止跨平台副作用）等工具被永久封锁
- **深度限制** ：最多 2 层（parent → child → grandchild 被拒绝）
- **并发限制** ：最多 3 个子 Agent 同时运行
- **迭代限制** ：每个子 Agent 默认最多 50 轮工具调用（父 Agent 默认 90 轮）
- **工具集交集** ：子 Agent 的工具集是其请求的工具集与父 Agent 工具集的交集——子不能获得父没有的工具

### 7.3 构建与执行

`_build_child_agent()` 在主线程构建子 Agent（确保线程安全），每个子 Agent 获得：

- 全新的 AIAgent 实例，无父级历史
- 独立的任务 ID（独立的终端会话、文件操作缓存）
- 限制后的工具集
- 聚焦的系统提示（由委派目标和上下文构建）
- `skip_context_files=True` 、 `skip_memory=True` （不加载父级上下文和共享记忆）

单任务直接在当前线程运行（避免线程池开销），多任务使用 `ThreadPoolExecutor` 并行，最多 3 个 worker。

子 Agent 还支持 **独立的凭证路由** ——可以使用比父 Agent 更便宜或更快的模型。

---

### 八、Cron 调度器：文件锁保护的定时任务

### 8.1 存储与调度

Cron 系统的数据存放在 `~/.hermes/cron/` 目录下，使用 JSON 文件存储任务定义。支持三种调度类型：

- **周期性间隔** ： `"every 30m"` → 每 30 分钟
- **Cron 表达式** ： `"0 9 * * *"` → 每天 9 点（使用 `croniter` 库解析）
- **一次性定点** ：ISO 时间戳或持续时间（如 `"30m"` → 从现在起 30 分钟后）

`tick()` 函数是调度核心，由 Gateway 每 60 秒在后台线程调用一次。它使用 **跨平台文件锁** （Unix 用 `fcntl.flock` ，Windows 用 `msvcrt.locking` ）确保同一时间只有一个 tick 在运行。

关键设计：先推进 `next_run_at` ，再执行任务。如果进程在执行中崩溃，任务不会重复执行——这是一种”至多一次”语义。

### 8.2 \[SILENT\] 机制

每个 Cron 任务的提示中自动注入静默指引。当 Agent 判断”无事可报”时，回复 `[SILENT]` ，系统不会将结果发送给用户。但执行输出仍保存在 `~/.hermes/cron/output/` 目录下供审计。

这使得监控型任务（如”每天检查服务器状态”）在正常时保持安静，只在异常时通知用户。

### 8.3 任务执行

每个 Cron 任务创建一个 **完全独立的 AIAgent 实例** ，有自己的 session ID、SQLite 会话存储，并且禁用了 `cronjob` （防止递归创建定时任务）、 `messaging` （防止意外发送消息）、 `clarify` （无法向用户提问）等工具。

---

### 九、MCP 集成：双向协议桥接

### 9.1 MCP 客户端：外部工具集成

`tools/mcp_tool.py` 是一个近 2000 行的复杂模块，实现了完整的 MCP 客户端。其架构的核心挑战是： **MCP 连接需要长生命周期的异步上下文，而 Agent 的工具调用是同步的** 。

解决方案是 **独立的后台事件循环** ：

```
_mcp_loop: Optional[asyncio.AbstractEventLoop] = None

def _ensure_mcp_loop():
    _mcp_loop = asyncio.new_event_loop()
    _mcp_thread = threading.Thread(target=_mcp_loop.run_forever, daemon=True)
    _mcp_thread.start()
```

每个 MCP 服务器在这个事件循环上运行一个长生命的 `MCPServerTask` 。同步的工具调用通过 `run_coroutine_threadsafe()` 桥接到这个循环。

**双传输支持** ：stdio（通过子进程通信）和 HTTP/StreamableHTTP（包括 OAuth 2.1 PKCE 认证）。

**安全机制** 方面尤为谨慎。传递给 MCP 子进程的环境变量经过严格过滤，只保留 `PATH` 、 `HOME` 等基线变量和配置中明确指定的变量，防止 API key 等敏感信息泄露。错误消息中的凭证也会被自动脱敏。

**动态工具发现** ：当 MCP 服务器发送 `tools/list_changed` 通知时，客户端自动刷新工具列表——注销旧工具、注册新工具。

### 9.2 MCP 服务器：对外暴露能力

`mcp_serve.py` 实现了反向的 MCP 服务器，将 Hermes 的消息能力暴露给外部 MCP 客户端（如 Claude Code、Cursor）。提供 10 个工具，核心是 `messages_read` （读取对话历史）和 `messages_send` （发送消息到平台）。

事件桥接使用了 **mtime 优化** ：每次轮询先检查 SessionDB 文件的修改时间，如果没变就跳过——这使得 200ms 轮询间隔几乎零 CPU 成本。

---

### 十、RL 训练系统：从 Agent 使用到模型进化的数据飞轮

Hermes Agent 区别于所有竞品的最独特能力，是它内置了一套完整的 **从 Agent 使用到模型训练的闭环系统** 。这不是旁挂的脚本，而是深度融入框架设计的核心基础设施。

### 10.1 数据飞轮的设计理念

整个闭环可以用一句话概括：Agent 在使用工具完成任务的过程中，自动生成高质量的训练数据（轨迹），这些数据经过压缩和处理后，直接用于通过强化学习训练更好的模型，更好的模型又能生成更高质量的轨迹——形成正向循环。

```
[Agent 执行任务] → [生成轨迹数据] → [压缩清洗] → [RL 训练] → [更强模型] → 回到起点
```

这个闭环由四个核心组件构成： `batch_runner.py` （批量轨迹生成）、 `trajectory_compressor.py` （轨迹压缩）、 `environments/` （Atropos RL 训练环境）、 `rl_cli.py` + `rl_training_tool.py` （训练控制面板）。

### 10.2 批量轨迹生成（batch\_runner.py）

**轨迹（trajectory）** 是 Agent 完成一个任务的完整对话记录，采用 ShareGPT 格式（ `from/value` 对）。一条轨迹记录了从用户提问到 Agent 调用工具、获取结果、最终给出回答的全过程：

```
{
  "prompt_index": 42,
  "conversations": [
    {"from": "system", "value": "You are a helpful assistant..."},
    {"from": "human", "value": "Write a function to sort an array..."},
    {"from": "gpt", "value": "<REASONING_SCRATCHPAD>...</REASONING_SCRATCHPAD>\n I'll write..."},
    {"from": "tool", "value": "{\"content\": {\"output\": \"...\", \"exit_code\": 0}}"},
    {"from": "gpt", "value": "The function has been successfully created..."}
  ],
  "completed": true,
  "tool_stats": {"terminal": {"count": 3, "success": 3, "failure": 0}, ...},
  "toolsets_used": ["terminal", "file", "web"]
}
```

`BatchRunner` 使用 `multiprocessing.Pool` 实现真正的多进程并行。几个关键的工程设计：

**工具集分布采样** ：每个 prompt 运行前，从配置的”分布”中随机采样一组工具集。这意味着不同轨迹中 Agent 拥有不同的工具组合，保证了训练数据的多样性——模型会学到在不同工具组合下如何适应性地完成任务。

**推理质量过滤** ：生成完成后，系统检查每条轨迹是否包含推理过程（ `<REASONING_SCRATCHPAD>` ），没有任何推理的样本会被直接丢弃。

**内容级断点续传** ：恢复时不依赖索引，而是扫描所有已生成的 batch 文件，提取每条轨迹中第一条 human message 的文本与待处理数据集比对。即使数据集重新排序，也能正确跳过已完成的 prompt。

**腐败数据过滤** ：最终合并时检测并过滤掉包含模型”幻觉”出来的无效工具名的损坏条目。工具统计也做了归一化处理——即使某个工具没被调用，也生成零值记录，保证 HuggingFace Datasets 加载时 schema 一致。

**每个 prompt 可指定独立的容器镜像** ，通过 `register_task_env_overrides()` 实现任务级别的环境隔离。

### 10.3 轨迹压缩（trajectory\_compressor.py）

Agent 轨迹可能非常长——一个涉及多次工具调用的任务可能产生几万甚至十几万 token。但 RL 训练的 token 预算通常有限（如 8K-32K tokens）。直接截断会丢失关键信息，所以需要智能压缩。

压缩算法的核心思想是 **保护头尾、摘要中间** ：

```
@dataclass
class CompressionConfig:
    target_max_tokens: int = 15250        # 目标最大 token 数
    summary_target_tokens: int = 750       # 摘要 token 预算
    protect_first_system: bool = True      # 保护首条系统消息
    protect_first_human: bool = True       # 保护首条用户消息
    protect_first_gpt: bool = True         # 保护首条 GPT 回复
    protect_first_tool: bool = True        # 保护首条工具结果
    protect_last_n_turns: int = 4          # 保护最后 4 轮
    summarization_model: str = "google/gemini-3-flash-preview"
```

算法步骤：1) 计算每轮 token 数；2) 如果总量在预算内则跳过；3) 标记保护区域（首轮 + 最后 N 轮）和可压缩区域（中间部分）；4) 从可压缩区域起点开始累积，直到节省够足够 token；5) 用快速模型（Gemini Flash）对被压缩区域生成摘要；6) 拼装：保护的头部 + 摘要 + 保护的尾部。

压缩前后的差异：原始 25000 tokens、20+ 轮的轨迹，压缩后变成 ~15000 tokens、~8 轮——中间的冗长工具交互被一段 `[CONTEXT SUMMARY]` 替代，而任务定义和最终行动完整保留。

压缩器使用 `asyncio.Semaphore(50)` 控制并发，支持 50 个并行的摘要 API 调用，每条轨迹 5 分钟超时。

### 10.4 Atropos RL 训练环境（environments/）

Atropos 是 NousResearch 开发的 LLM RL 训练框架（”LLM RL Gym”）。Hermes Agent 通过 `tinker-atropos` 子模块深度集成。

**内置环境** 包括：

| 环境 | 用途 |
| --- | --- |
| HermesAgentBaseEnv | 抽象基类，定义接口契约 |
| AgenticOPDEnv | On-Policy Distillation（前沿技术） |
| TerminalTestEnv | 终端任务验证 |
| HermesSweEnv | SWE-bench 风格训练 |
| WebResearchEnv | 多步 Web 研究训练 |

每个环境必须实现四个抽象方法： `setup()` （初始化）、 `get_next_item()` （返回训练项）、 `format_prompt()` （转为用户消息）、 `compute_reward()` （评分）。

**ToolContext——奖励函数的”万能钥匙”** 是整个系统最精妙的设计。 `compute_reward` 的 `ctx: ToolContext` 参数意味着奖励函数可以 **在 Agent 的沙箱中执行任意操作来验证输出** ：

```
class ToolContext:
    def terminal(self, command, timeout=180):  # 运行终端命令
    def read_file(self, path):                 # 读取文件
    def write_file(self, path, content):       # 写入文件
    def web_search(self, query):               # 搜索网络
    def call_tool(self, tool_name, args):      # 调用任何工具
```

例如在编程任务中，验证函数可以直接在 Agent 的沙箱里跑测试： `ctx.terminal("python test_solution.py")` 并根据测试结果计算奖励。

**两阶段运行模式** ：Phase 1 使用 OpenAI 兼容 API（适用于数据生成和评估），Phase 2 使用 VLLM ManagedServer（获取精确的 token ID 和 logprobs，用于完整 RL 训练）。

**AgenticOPDEnv（On-Policy Distillation）** 是前沿技术。核心思想：Agent 执行工具调用后得到的结果（错误堆栈、测试结果）包含了事后信息。OPD 利用这些信息构建”增强 prompt”，用 VLLM 的 prompt\_logprobs 在增强分布下评分学生的 token，提供 **逐 token 的密集训练信号** ——而非仅在轨迹末尾的标量奖励。

### 10.5 RL 训练工具（tools/rl\_training\_tool.py）

系统注册了 10 个 RL 专用工具，让 Agent 自己来管理训练流程（Agent-as-Trainer）：

| 工具 | 功能 | 阶段 |
| --- | --- | --- |
| rl\_list\_environments | 列出可用环境 | 发现 |
| rl\_select\_environment | 选择环境并加载配置 | 配置 |
| rl\_get\_current\_config | 获取当前配置 | 配置 |
| rl\_edit\_config | 修改配置字段 | 配置 |
| rl\_test\_inference | 快速推理测试（144 rollouts，3 个模型） | 验证 |
| rl\_start\_training | 启动训练（3 个子进程） | 训练 |
| rl\_check\_status | 查询状态和指标 | 监控 |
| rl\_stop\_training | 停止训练 | 控制 |
| rl\_get\_results | 获取最终结果和 WandB 指标 | 评估 |
| rl\_list\_runs | 列出所有训练运行 | 管理 |

`rl_start_training` 启动三个独立进程：Atropos API 服务器（轨迹收集）、Tinker 训练器（训练 + 推理服务器 port 8001）、RL 环境（连接到 Atropos API）。

环境发现使用 **Python AST 解析** （而非导入）扫描 `environments/` 目录，避免副作用。训练基础设施参数（tokenizer、rollout\_server\_url、max\_token\_length、lora\_rank 等）被锁定，Agent 只能修改 `group_size` 、 `batch_size` 、 `wandb_project` 等训练超参数。

### 10.6 为什么竞品没有这个能力

三个层面的壁垒：

1. **工具系统的完整性** 。Hermes Agent 拥有产品级的工具系统（终端支持 6 种后端、浏览器自动化、Web 搜索等），可以生成真实的、多样化的工具调用轨迹。编排型框架（LangGraph/CrewAI）和编码 Agent（Claude Code/Codex CLI）都不具备这种深度。
2. **端到端管道** 。从 `batch_runner.py` （工业级并行轨迹生成）→ `trajectory_compressor.py` （智能压缩）→ `rl_cli.py` （训练管理）→ `environments/` （Atropos 集成），是完整的数据到训练管道。竞品在”Agent 使用”和”模型训练”之间存在巨大鸿沟。
3. **垂直集成** 。NousResearch 同时拥有 Atropos（RL 环境框架）和 Tinker（RL 训练器）。Hermes Agent 是第一个将 Agent 框架与 RL 训练框架完全打通的系统。ToolContext 让奖励函数调用任何工具验证输出，HermesAgentBaseEnv 将 Agent 的多轮工具调用循环无缝嵌入 Atropos 的 rollout 机制。

这个系统的存在表明，NousResearch 对 Hermes Agent 的定位不仅是一个 Agent 产品，更是一个 **持续自我改进的训练数据工厂** ——模型越强 → 数据越好 → 训练效果越好 → 模型更强。

---

### 十一、总结：设计哲学

纵观 Hermes Agent 的实现，几个核心设计哲学贯穿始终：

**1\. 保守但务实的并行策略** 。并行工具执行采用白名单制，未知工具一律串行。宁愿慢一点，也不引入并发 bug。

**2\. 多层容错** 。API 层 3 次重试 + 指数退避；工具名自动修复 → 错误反馈 → 3 次放弃；结果 100K 字符截断防止上下文爆炸；预算压力 70% 提醒 → 90% 警告 → 100% 强制停止。

**3\. 缓存友好** 。系统提示只构建一次；Honcho 后续注入用户消息而非系统提示；临时提示不写入 session DB——一切为了最大化 Anthropic prompt caching 的命中率。

**4\. 可审计性** 。记忆用 Markdown 文件而非向量数据库；技能用结构化文档而非编译代码；Cron 输出保存到本地文件——用户随时可以查看和编辑 Agent 的”大脑”。

**5\. 安全深度防御** 。Prompt injection 检测扫描上下文文件；工具执行需审批机制；SSRF 防护保护 web 和 vision 工具；MCP 子进程环境变量过滤；子 Agent 工具限制和深度限制；文件操作路径遍历防御。

**6\. 渐进式降级** 。从 200+ 模型的广泛兼容到三种 API 模式的统一适配，从并行执行到串行回退，从流式响应到非流式兼容——系统在每一层都有降级路径。

**7\. 数据飞轮思维** 。 `ephemeral_system_prompt` 在执行时使用但不保存到轨迹——训练数据不应包含临时指令。工具统计归一化保证 HuggingFace Datasets 的 schema 一致性。轨迹压缩保护头尾、摘要中间——保留最大训练信号。每一个设计决策都在为训练数据质量服务。

这些设计选择共同塑造了一个在复杂性和可靠性之间取得平衡的工业级 Agent 框架。它不是学术原型，而是面向真实用户的生产系统——同时也是一个持续生成高质量训练数据的自我进化引擎。这从其 17K Stars 和活跃社区的反馈中得到了印证。

还没有人送礼物，鼓励一下作者吧

编辑于 2026-03-30 18:34・北京[腾讯版小龙虾，免部署开箱即用！](https://www.codebuddy.cn/work?fromSource=gwzcw.12162961.12162961.12162961&utm_medium=ocpc&utm_id=gwzcw.12162961.12162961.12162961&cb=https%3A%2F%2Fsugar.zhihu.com%2Fplutus_adreaper_callback%3Fsi%3D6beaebda-f2ec-454a-9ba0-54b1f408e177%26os%3D3%26zid%3D1629%26zaid%3D3719187%26zcid%3D3696421%26cid%3D3696421%26event%3D__EVENTTYPE__%26value%3D__EVENTVALUE__%26ts%3D__TIMESTAMP__%26cts%3D__TS__%26mh%3D53b45bb125735346285dc7687bac0089%26adv%3D774620%26ocg%3D4%26cp%3D1000%26ocs%3D0%26aic%3D0%26atp%3D0%26ct%3D2%26ed%3DGiBNJgVzfCMmUW9XFyEvRA8xBGxJICwkOhh0FlwxKw1ZY0gnWzUoISkYYUFEJSVUVnQOfQt7aHV3F2pfBGV8AV1jViRdKj59fi0vtP74PK0Z&spu=biz%3D0%26ci%3D3696421%26si%3D051dec97-6256-4e72-a73e-0e9a3595b4b0%26ts%3D1775614636%26zid%3D1629)

[

免部署开箱即用，注册领3000 Credits体验金，极速接入多平台生态，让办公更智能。

](https://www.codebuddy.cn/work?fromSource=gwzcw.12162961.12162961.12162961&utm_medium=ocpc&utm_id=gwzcw.12162961.12162961.12162961&cb=https%3A%2F%2Fsugar.zhihu.com%2Fplutus_adreaper_callback%3Fsi%3D6beaebda-f2ec-454a-9ba0-54b1f408e177%26os%3D3%26zid%3D1629%26zaid%3D3719187%26zcid%3D3696421%26cid%3D3696421%26event%3D__EVENTTYPE__%26value%3D__EVENTVALUE__%26ts%3D__TIMESTAMP__%26cts%3D__TS__%26mh%3D53b45bb125735346285dc7687bac0089%26adv%3D774620%26ocg%3D4%26cp%3D1000%26ocs%3D0%26aic%3D0%26atp%3D0%26ct%3D2%26ed%3DGiBNJgVzfCMmUW9XFyEvRA8xBGxJICwkOhh0FlwxKw1ZY0gnWzUoISkYYUFEJSVUVnQOfQt7aHV3F2pfBGV8AV1jViRdKj59fi0vtP74PK0Z&spu=biz%3D0%26ci%3D3696421%26si%3D051dec97-6256-4e72-a73e-0e9a3595b4b0%26ts%3D1775614636%26zid%3D1629)