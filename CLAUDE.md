# 项目引导文件（每次新对话必读）

这是「住小叮 / Intent Computing —— A2A 酒店智能体平台」的战略研究与项目文档仓库。
仓库采用**三层记忆架构**（参考 Hermes Agent），目的：任何一个全新的对话（没有任何先前上下文的 Claude 实例）
读完本文件和 L1 层之后，都能准确恢复任务并继续推进。

## 如何恢复任务（严格按顺序读）

1. `memory/L1-core/project-charter.md` —— 项目宪法：业务背景、六个待验证假设、目标与约束（很少变更）
2. `memory/L1-core/current-state.md` —— 当前状态快照：进行到哪一步、下一步该做什么
3. `memory/L1-core/key-conclusions.md` —— 已确立的关键结论（研究判决、重要事实）
4. `memory/L2-working/task-board.md` —— 任务清单与实时状态
5. `memory/L2-working/decision-log.md` —— 与股东（用户）的决策记录及理由
6. 需要深入材料时，再按需查 `memory/L3-knowledge/`（研究原始材料、完整报告、归档）——不要全量读取，按 current-state.md 的指引选读

## 三层记忆的维护规则

- **L1 核心记忆**：保持精炼（单文件 ≤ 200 行），只放"必须知道"的信息。每次重大进展后必须更新 `current-state.md`。
- **L2 工作记忆**：工作台。任务状态实时更新；每一个影响方向的用户决策（含日期和原因）记入 `decision-log.md`；临时上下文放 `context-notes.md`。
- **L3 长期知识库**：只增不改。研究原始材料放 `research/raw/`（按 `NN-主题.md` 编号），成品报告放 `research/reports/`，过期/被取代内容移入 `archive/`。
- 所有产出使用**中文**；引用外部信息必须附来源 URL。
- 每次会话结束前：更新 L1/L2，`git commit` 并尝试 `git push -u origin claude/ai-agent-hotel-platform-z5whni`（若远端 403 说明 GitHub App 写权限未开通，见 decision-log 2026-07-24 补记）。

## 环境约束（重要，新对话务必知晓）

- 本远程环境的网络策略**只允许 WebSearch（搜索引擎）**；WebFetch / curl 抓取任何外部网页都会被代理 403 拦截，不要浪费时间重试。
- 公司官网 `www.intent-computing.com` 无法直接访问；产品信息以股东提供的描述 + 搜索引擎索引摘要为准（见 L3 `research/raw/00-产品现状.md`）。
- GitHub 操作使用 MCP 工具（`mcp__github__*`），没有 `gh` CLI；开发分支固定为 `claude/ai-agent-hotel-platform-z5whni`，不要推送到其他分支。
- 推送写权限截至 2026-07-24 尚未生效（远端 403），股东正在按指引开通；每次会话结束仍应尝试推送。
