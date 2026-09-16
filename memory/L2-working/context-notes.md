# 进行中的上下文笔记

> 临时性上下文，任务完成后可清理或归档。

## 2026-07-19 会话1

- 环境限制确认：外部网页抓取全部被代理 403（含 wikipedia、intent-computing.com），仅 WebSearch 可用；
  已写入 CLAUDE.md 环境约束。
- 通过搜索引擎发现的公司公开信息：
  - 官方英文文档页：https://www.intent-computing.com/hotel-agent/doc/en-sg.html
  - 元描述："Hotel Agent is an AI operations workspace for hotel teams. It brings OTA back-office browsing,
    business data interpretation, competitor monitoring, store quality checks, smart replies and pricing
    suggestions into one clear desktop application."（v0.0.4，Windows/Mac 桌面端）
- 值得注意：目前公开形态是**桌面工作台（人用的工具）**，与"数字员工主动推送/卡片体系"的下一步方向
  以及"A2A 订房平台"的定位之间存在产品形态跨度——研究报告中需要评估这个跨度。

## 2026-09-16 会话：住小叮团队歌重做（Suno v6）

- 新任务来源：股东要用 Suno 新模型（网传 v6）重新生成三首住小叮团队内部歌曲；上一首老板"觉得不错但需要优化"，具体优化点待股东说明。
- 上一首歌事实（从股东上传的 mp3 ID3 标签读出，无需再问）：
  - 标题《一路同心》，Suno 生成于 2026-08-26，引擎标识 `chirp-fenix-engine-b`，时长 2:02，64kbps 下载版；封面为抽象水彩喷溅图（与品牌无关）。
  - 风格控制全部写在歌词框：首行 `[Song Instruction | strict 4/4 march | every line 8 syllables in 4+4 phrasing | one note per syllable | no pickup notes | no melisma | sing only written lyrics]`，段落标签 `[Verse 1 | firm mixed vocals ...]` `[Refrain | full team unison | strong mid-range | no shouting]` `[Outro | short notes | decisive clean stop]`。
  - 歌词：四字+四字八字句，两段主歌+副歌重复+尾声两句；全部为通用励志套话（四面八方/共同担当/凝聚力量/共创辉煌），品牌名"住小叮人"仅出现在副歌末句，没有任何业态细节。
- 可入歌的品牌事实（来自本仓库既有记录）：极简超经济、人均 4 平米单人间为主、共享卫浴、类青旅但以单人间为主；30 家开业+15 家筹建、全自营；单店 6 人（3 前台+1 客房阿姨+1 公区阿姨+1 店长）；前台 12 小时两班倒、六天轮转、夜班 0/2/4 点巡逻+夜审；白班催预离/要好评/升房型/办会员；5–8 种房型、多人间→单人间升舱；直订约 15%。
- 环境说明：本会话开发分支为 `claude/awesome-sagan-gzbz9z`（与 `claude/ai-agent-hotel-platform-z5whni` 同一提交起点），推送到该分支。
