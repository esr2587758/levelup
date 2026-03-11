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

- **OpenClaw 最佳实践：弃用飞书，把 AI 团队搬到 Discord** — 多 Agent 架构实战指南
  - URL: https://zhuanlan.zhihu.com/p/2007731761006809270
  - 作者: 小蔡（字节AI工程师）
  - 标签: OpenClaw, Discord, 多Agent, 工作流
  - 要点:
    - Discord 频道结构天然适合多 Agent（频道=职能，线程=任务）
    - 频道 topic 可被 AI 读取，改描述=改 AI 行为
    - 配置三步：创建 Bot → 列频道 → 写 bindings
    - autoThread 实现任务级上下文隔离
  - 添加时间: 2026-03-11
