# AI 类资源

收集 AI 工具、学习资源和行业动态。

## 子分类

- **工具/产品** — 实用的 AI 工具和产品
- **学习资源** — 教程、课程、论文
- **行业动态** — 新闻、趋势、观点
- **开源项目** — 代码仓库、技术实现

## 链接列表

### 工具/产品

- **RTK (Rust Token Killer)** — 高性能 CLI 代理工具，减少 LLM token 消耗 60-90%
  - URL: https://github.com/rtk-ai/rtk
  - 标签: Rust, CLI, LLM, Token优化
  - 添加时间: 2026-03-09

### 学习资源

- **You Need to Rewrite Your CLI for AI Agents** — 如何为 AI 代理重新设计 CLI
  - URL: https://justin.poehnelt.com/posts/rewrite-your-cli-for-ai-agents/
  - 作者: Justin Poehnelt (Google)
  - 标签: CLI设计, AgentDX, 最佳实践
  - 添加时间: 2026-03-09

- **OpenClaw 2026.3.7 更新解读** — 上下文管理插件化、Agent路由升级
  - URL: https://mp.weixin.qq.com/s/s_8yqfuwh_hhiey7pYB-aQ
  - 来源: 量子位 (公众号)
  - 标签: OpenClaw, 上下文管理, lossless-claw, Agent记忆
  - 要点:
    - 可插拔的上下文引擎 (ContextEngine)
    - lossless-claw 插件实现"永不丢失上下文"
    - Agent路由能力升级（频道、topic绑定）
    - GPT-5.4 和 Gemini Flash 3.1 支持
  - 添加时间: 2026-03-09

### 行业动态

- [Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/) — OpenAI 团队分享零手写代码、全 Codex agent 驱动的产品开发实践与经验。添加于 2026-03-31

- [你不知道的 Agent：原理、架构与工程实践](https://x.com/HiTw93/status/2034627967926825175) — Tw93 深度解析 Agent 底层原理，涵盖 Agent Loop、上下文工程、工具设计、记忆系统、多 Agent 协作与评测。添加于 2026-04-01

- [Writing CLI Tools That AI Agents Actually Want to Use](https://dev.to/uenyioha/writing-cli-tools-that-ai-agents-actually-want-to-use-39no) — 构建 AI Agent 友好的 CLI 工具的 8 条实践规则，涵盖 JSON 输出、退出码、幂等设计等。添加于 2026-04-01

- [You Need to Rewrite Your CLI for AI Agents](https://justin.poehnelt.com/posts/rewrite-your-cli-for-ai-agents/) — 面向 AI Agent 的 CLI 设计原则，包括 JSON 优先、运行时 schema 自省、输入防幻觉、dry-run 安全机制等。添加于 2026-04-01

- [awesome-design-md](https://github.com/VoltAgent/awesome-design-md/tree/main) — 精选知名网站 DESIGN.md 文件集合，供 AI 代理生成一致 UI（⭐ 25.5k）。添加于 2026-04-07

- [我敢说这是2026最强的Agent Harness框架：Hermes Agent 全面调研解读](https://zhuanlan.zhihu.com/p/2022015752258027715) — Hermes Agent 开源 Agent 框架全面调研，内置闭环学习与自进化系统（⭐ 17K）。添加于 2026-04-08
- [AI 时代，我们为什么还要学习？](https://mp.weixin.qq.com/s/RoLV6EDJrtFLhNhWy2N8-A) — 探讨 AI 让智能成本骤降后，教育应从“培养技能”转向“塑造独立思考的人”。添加于 2026-04-13

- [Claude Code源码解析：98.4%代码与AI无关](https://m.weibo.cn/status/5289548764677505) — 论文拆解Claude Code v2.1.88源码，仅1.6%是AI决策逻辑，其余98.4%是上下文管理、权限、安全等确定性工程基础设施，揭示其「最小脚手架，最大操作环境」的架构哲学。添加于 2026-04-21
