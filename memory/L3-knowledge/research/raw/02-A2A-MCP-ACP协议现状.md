# 02 - 智能体互操作协议现状（A2A / MCP / ACP / AP2 / UCP / x402）

> 研究日期：2026-07-19 ｜ 方法：WebSearch（16 次查询，中英混合）｜ 环境限制：仅能获取搜索引擎索引摘要，无法抓取原文全文
> 信息分类标注：【事实】= 多源可交叉验证；【公司宣传】= 厂商官方口径；【媒体推测】= 媒体/分析师判断

## 概述

2026 年年中，智能体互操作协议已从"协议战争"走向**分层共存**：MCP 成为智能体-工具连接的事实标准（官方 registry 约 9,600+ 服务器、97M+ 月 SDK 下载），A2A 成为智能体-智能体协作标准（150+ 组织支持、v1.0 RC），交易层则由 OpenAI/Stripe 的 ACP 与 Google/Shopify 的 UCP 两大阵营竞争，支付层有 AP2/x402（采用仍早期）。治理已统一到 Linux Foundation 旗下 Agentic AI Foundation。

**但对"个人智能体直订小酒店"这一场景，链条尚未闭环**：需求侧主流助手（ChatGPT/Gemini）在旅游品类刻意退回"发现+跳转 OTA"模式（OpenAI 2026 年 3 月明确不做旅游交易闭环）；供给侧最成熟的路径是 SiteMinder 等聚合商的 MCP 接口，而非酒店自建 agent card 被点对点发现。中国侧进展最快的是**微信 AI 智能体**（2026 年中灰度、Q3 放量，可调用小程序完成交易，携程/同程/美团/滴滴首批内测）与**支付宝 A2A 交易/AI 支付**（AI 支付已超 3 亿笔）。结论：「A2A+MCP+Skills 让个人智能体找到酒店」的**组件全部存在且快速成熟，但开放式点对点 A2A 直订在 2026 年仍无生产案例**；2026 年可落地的现实形态是"接入超级入口（微信/ChatGPT/Gemini）+聚合 MCP"。

## 关键发现

### 一、A2A 协议（Google 捐给 Linux Foundation）

1. 【事实】A2A 一周年（2026 年 4 月）：支持组织从 50+ 增至 **150+**（含 AWS、Cisco、Google、IBM、Microsoft、Salesforce、SAP、ServiceNow），GitHub 主仓 22,000+ stars，SDK 从 Python 单一实现扩展到 5 种生产级语言（JS/Java/Go/.NET）。Microsoft 已集成进 Azure AI Foundry 和 Copilot Studio，AWS 通过 Bedrock AgentCore Runtime 支持。
   来源：https://www.linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year
2. 【事实】生产级落地集中在**供应链、金融服务、保险、IT 运维**等企业内部/B2B 协同场景——**没有一个公开的消费级交易（如订房）落地案例**。A2A v1.0 Release Candidate 于 2026 年 1 月发布。
   来源：https://www.hpcwire.com/aiwire/2026/04/09/linux-foundation-a2a-protocol-marks-one-year-with-broad-enterprise-and-cloud-adoption/
3. 【事实】发现机制层面：`/.well-known/agent-card.json` 于 2025 年 4 月成为 IANA .well-known 注册表中**首个 AI 智能体专属条目**（RFC 8615 路径），配套 registry 式集中发现、Agent Name Service（ANS）等方案。发现机制"标准已定、消费未起"。
   来源：https://a2a-protocol.org/latest/topics/agent-discovery/ ；https://zylos.ai/research/2026-03-07-ai-agent-identity-discovery-trust-frameworks
4. 【媒体推测/反面证据】独立技术分析指出：A2A"实际有用范围窄于宣传"——适合预定义角色的成对协作，预设静态发现与显式协调；学术论文指出 A2A **缺乏对支付凭证等敏感载荷的专门防护**（仅泛化 token 过期），且规范非正式（状态机以散文描述、取消任务可否恢复等语义含混）。
   来源：https://www.glukhov.org/ai-systems/comparisons/a2a-protocol-2026-adoption/ ；https://arxiv.org/pdf/2505.12490

### 二、MCP（Model Context Protocol）

5. 【事实】规模：Anthropic 2025 年 12 月 9 日生态更新称 MCP 有 **10,000+ 活跃公共服务器、97M+ 月 SDK 下载**（Python+TS），被 ChatGPT、Cursor、Gemini、Microsoft Copilot、VS Code 等采用。官方 Registry 截至 2026 年 5 月 24 日收录 9,652 个最新服务器记录（28,959 个版本记录）；第三方索引 Glama 19,831+、MCP.so 16,000+。Stacklok 2026 报告：**41% 受访软件组织已在有限或广泛生产环境使用 MCP 服务器**。
   来源：https://www.digitalapplied.com/blog/mcp-adoption-statistics-2026-model-context-protocol ；https://workos.com/blog/everything-your-team-needs-to-know-about-mcp-in-2026
6. 【事实】治理：Anthropic 将 MCP 捐入 Linux Foundation 旗下 **Agentic AI Foundation（AAIF，2025 年 12 月成立）**，OpenAI、Block 为共同创始成员，AWS/Google/Microsoft/Cloudflare/GitHub/Bloomberg 为支持成员。AAIF 同时是 A2A 与 MCP 的永久归属——协议层已"统一治理、分层分工"。
   来源：https://thenewstack.io/mcp-gets-its-missing-enterprise-authorization-layer/ ；https://dev.to/alexmercedcoder/the-state-of-agentic-ai-standards-in-2026-mcp-a2a-webmcp-osi-and-the-protocol-stack-taking-3o2l
7. 【事实/反面证据】**认证与支付是 MCP 的两大缺口**：2026 年安全审计发现仅 **8.5%** 的 MCP 服务器实现了规范强制的 OAuth 2.1，**25%** 的公共服务器完全无认证，53% 依赖长期静态 API key。企业级授权（IdP 委托、零触碰 SSO）2026 年 6 月 18 日才达 stable（Okta 首家支持）。MCP 本身无支付语义，需叠加 x402/AP2/ACP。
   来源：https://nimblebrain.ai/blog/state-of-mcp-security-2026/ ；https://www.techtimes.com/articles/318708/20260619/mcp-enterprise-authorization-goes-stable-zero-touch-sso-okta-anthropic-vs-code.htm

### 三、交易与支付协议（ACP / UCP / AP2 / x402）

8. 【事实】OpenAI+Stripe 的 **ACP（Agentic Commerce Protocol）**：2025 年 9 月随 ChatGPT Instant Checkout 发布；截至 2026 年 2 月处于 beta 但已为 Etsy 处理真实交易，正扩展到 100 万+ Shopify 商家、Walmart 等；Stripe 2025 年 12 月推出 Agentic Commerce Suite（URBN、Coach、Kate Spade、Revolve 等首发）；PayPal 的 ACP server 2026 年接入。ChatGPT 周活 8-9 亿，购物类查询约 5,000 万次/天。
   来源：https://stripe.com/newsroom/news/stripe-openai-instant-checkout ；https://www.digitalcommerce360.com/2026/02/16/openai-expands-agentic-commerce-push/
9. 【事实/关键反面证据】**OpenAI 在旅游品类明确退回"不做交易闭环"**：Skift 2026 年 3 月 5 日报道《ChatGPT Bails on Transactions — Good News for Expedia and Booking》——ChatGPT 中酒店/机票仍是"发现→点击跳转 OTA 完成预订"，Instant Checkout 未覆盖旅游。Expedia、Booking.com 是 2025 年 10 月 ChatGPT Apps SDK 的**首批合作伙伴**。
   来源：https://skift.com/2026/03/05/openai-chatgpt-checkout-walkback/ ；https://skift.com/2025/10/06/expedia-booking-chatgpt-apps-openai/
10. 【事实】Google+Shopify 的 **UCP（Universal Commerce Protocol）**：2026 年 1 月 11 日 NRF 发布，与 Shopify/Etsy/Wayfair/Target/Walmart 共同开发，20+ 伙伴背书（Visa、Mastercard、Stripe、AmEx 等）；已在 Google AI Mode、Gemini、YouTube Shopping 上线；商家在自有域名托管 `/.well-known/ucp` JSON 档案供任何合规智能体读取。**零售先行，酒店业尚未进入 UCP/ACP 版图**。
    来源：https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/ ；https://searchengineland.com/google-expands-universal-commerce-protocol-and-launches-new-agentic-shopping-tools-478113
11. 【事实/反面证据】Google 的 **AP2（Agent Payments Protocol）**：2025 年 9 月 16 日发布，60+ 伙伴（Mastercard、PayPal、Coinbase、AmEx、Salesforce），但截至 2026 年 4 月**公开落地仅 3 个**（PayPal 钱包集成、Mastercard Agent Pay 试点、A2A x402 加密支付扩展），v0.2.0（2026 年 4 月）。x402 有可用开源实现但真实使用仍限于开发者实验。**支付层是整个栈中最不成熟的一层**。
    来源：https://appliedtechnologyindex.com/research/2026-comparative-analysis-agentic-commerce-payment-protocols/ ；https://ap2-protocol.org/
12. 【事实】竞争格局判定："协议战争"框架已过时——MCP=工具层、A2A=协作层、ACP/UCP=交易层各居一层；IBM 的 ACP（Agent Communication Protocol，与 OpenAI 的 ACP 重名）已于 2025 年并入 A2A。真正的竞争只在**交易层：OpenAI/Stripe 阵营（ACP）vs Google/Shopify 阵营（UCP）**。
    来源：https://zuplo.com/blog/agent-protocol-stack-mcp-a2a-acp-2026 ；https://zylos.ai/research/2026-03-26-agent-interoperability-protocols-mcp-a2a-acp-convergence/

### 四、旅游业专属努力

13. 【事实】**Sabre**：2025 年 9 月 23 日发布"业内首个"agentic API 套件，基于自研专有 MCP server（面向旅行社场景：对话式购物、预订、服务、支付全流程），CES 2026 现场演示 agent-first 订行程。**Amadeus 无官方 MCP server**，仅有社区封装（50+ 工具覆盖机票/酒店/活动），官方 AI 布局偏内部运营与个性化。
    来源：https://www.sabre.com/releases/sabre-seizes-first-mover-position-with-comprehensive-agentic-apis-for-travel/ ；https://www.phocuswire.com/sabre-api-agentic-ai-mcp ；https://skift.com/2026/01/06/sabre-ces-agentic-ai-travel-trip-booking-demo/
14. 【事实/直接竞争情报】**SiteMinder**（2026 年 4 月）："全球最大酒店生态"（53,000+ 酒店、450+ 渠道、250 万房间、年处理 3 亿+ 间夜）推出两条 MCP 产品线：**Channels Plus MCP**（agentic OTA 即插即用接入其酒店库存，无需单独签约、按完成入住收佣）与 **Direct Booking MCP**（Demand Plus 客户的直订引擎进入 ChatGPT/Gemini/Claude，客人直接与酒店成交）。**这意味着"帮酒店接入 AI 智能体渠道"的赛道已有强势在位者。**
    来源：https://www.siteminder.com/news/siteminder-ai-hotel-distribution/ ；https://www.phocuswire.com/news/technology/siteminder-links-hotel-inventory-ai-booking-channels-mcp
15. 【公司宣传】**DerbySoft**：博客层面倡导 agentic AI，已推出面向商旅的 AI Voice Agent（跨时区确认预订要素、验证虚拟卡、催收合规发票），**未见正式 MCP/agent 分销接口发布**。
    来源：https://www.derbysoft.com/resources/blog/ai-is-now-table-stakes-so-what-comes-next/
16. 【事实/行业组织】**AHLA/HTNG + OpenTravel**：AHLA/HTNG 战略简报 v2 由 DART 工作组提出"AI-Native Hospitality Commerce Ecosystem"五层参考架构，呼吁通过开放 A2A 标准让酒店"与 OTA 平起平坐"直连旅客智能体、防止新中介层形成——**目前仍处倡导/参考架构阶段，未形成可实施标准**。HTNG 分销消息仍构建于 OpenTravel 1.0 之上。
    来源：https://www.hospitalitynet.org/opinion/4129485/the-next-shift-in-ai-distribution-from-mcp-to-a2a-and-why-it-matters-for-hotels ；https://opentravel.org/news/recommendations-released-for-future-of-hotel-distribution-connectivity-standards/
17. 【事实/供给侧就绪度】酒店"可被机器读取"程度极低：121,425 家酒店主页全球审计显示 **36.3% 无任何结构化数据**、已使用者中 41.1% schema 类型用错；2026 年 3 月对 105,002 家酒店网站爬取仅 **6.3% 有 llms.txt**，且主流 LLM 生产环境**并不读取 llms.txt**。IDC 预测 2030 年 30% 旅行预订将由 AI 智能体执行；SiteMinder 2026 报告称 4/5 旅行者希望预订过程中获得 AI 协助、AI 搜住宿量为 2025 年的近 4 倍。
    来源：https://digitalfoxllc.com/llms-txt.html ；https://www.siteminder.com/r/ai-travel-agent/ ；https://www.siteminder.com/r/ai-hotel-booking-distribution/

### 五、中国国内采用情况

18. 【事实】**阿里**：百炼平台全生命周期 MCP 服务 + MCP 广场（上线首日 50+ 服务），Qwen3 原生支持 MCP，新版智能体 Agent 2.0 中外部工具一律以 MCP 协议接入。**字节**：Coze 内置 MCP 客户端能力，Coze Studio 2025 年 7 月开源、2026 年升级 Coze 2.0；未见 A2A 支持。
    来源：https://help.aliyun.com/zh/model-studio/mcp-introduction ；https://docs.coze.cn/recent-updates
19. 【事实/H3 直接证据】**腾讯/微信**：微信团队高优先级研发内置 AI Agent（周颢负责、向张小龙汇报），拟打通数百万小程序，**2026 年年中灰度测试、争取 Q3 放量**；2026 年 6 月 8 日微信公开课公布开发者接入指引（自动模式=平台解析小程序页面直接操作；开发模式=开发者自主适配）；**首批内测：美团、携程、同程、滴滴**。微信支付 MCP 已上线（腾讯元器接入，2025 年 7 月），智能体可直接收款；2026 年 6 月微信确认与华为/荣耀/小米/OPPO/vivo 五大手机厂商合作推 A2A 智能体互联。
    来源：https://companies.caixin.com/m/2026-06-09/102452577.html ；https://www.guancha.cn/economy/2026_06_08_819794.shtml ；https://news.aibase.cn/news/26099 ；https://www.qbitai.com/2025/07/304752.html
20. 【事实】**支付宝/蚂蚁**：推出"AI 付/AI 收/Token Pay/AI 钱包"全栈 AI 原生支付，截至 2026 年 5 月末 **AI 支付超 3 亿笔、支持 95% 通用智能体框架**；上线 a2a.alipay.com"A2A 交易"平台（智能体钱包+智能收，含基于 HTTP 402 的按量付费 A2M 方案、SKILL 脚本内调用支付短链）；另有 IIFAA 开源的 ASL 可信互联协议、ACT 商业信任协议。
    来源：https://a2a.alipay.com/ ；https://finance.sina.com.cn/cj/2026-05-26/doc-inhzffsq9050427.shtml ；https://cn.chinadaily.com.cn/a/202504/25/WS680b4f82a310f542634747a8.html
21. 【事实/政策】2026 年 5 月 8 日网信办、发改委、工信部联合发布《智能体规范应用与创新发展实施意见》；市场监管总局批准发布《人工智能 智能体互联》系列 **8 项国家标准化指导性技术文件（GB/Z 185-2026）**，50 家企业试点，业内预计 2026 下半年显现影响。华为+中国移动主导电信场景 A2A-T 协议。**中国走的是"国标+超级 App 生态"路线，而非直接采用 Google A2A。**
    来源：https://www.stdaily.com/web/gdxw/2026-06/09/content_529630.html ；https://www.cls.cn/detail/2412385
22. 【事实】**Anthropic Agent Skills**（SKILL.md）：2025 年 12 月 18 日开放为标准（agentskills.io），至 2026 年 6 月约 40 个兼容产品（OpenAI Codex、GitHub Copilot、Cursor、Gemini CLI、VS Code），社区目录 SkillsMP 索引约 190 万公共 skills；但质量参差（SkillsBench 平均分 6.2/12），"skill 投毒"被 Akamai 列为 2026 年 agentic AI 十大威胁。支付宝已支持"SKILL 脚本内调用支付"——**Skills 作为分发载体在中国支付场景已有实际接口**。
    来源：https://agentskills.io/home ；https://agentman.ai/blog/agent-skills-ecosystem-report-2026 ；https://aipay.alipay.com/docs/ai-receive/MACHINE_PAY.html

### 六、核心问题：普通个人智能体今天如何发现并预订一家小酒店？

23. 【综合判断】2026 年 7 月的现实链路只有三条，且**没有一条是开放式点对点 A2A**：
    - **路径 A（主流）**：ChatGPT/Gemini 对话式发现（依赖网页内容、schema.org、OTA 数据）→ 跳转 OTA/官网完成支付。OpenAI 已明确旅游品类不做交易闭环（见发现 9）。
    - **路径 B（新兴）**：酒店经由聚合商 MCP 进入 AI 渠道——SiteMinder Direct Booking MCP / Channels Plus MCP、Sabre agentic API。前提：酒店已是该聚合商付费客户。
    - **路径 C（中国特色，尚未放量）**：微信 AI Agent 调用酒店小程序完成交易（2026 Q3 放量）+ 微信支付 MCP / 支付宝 A2A 交易收款。
    - **缺失的一环**：需求侧主流个人智能体**不会**主动抓取某小酒店的 `/.well-known/agent-card.json` 来完成商业预订——agent card 的消费方今天是企业内部编排系统，不是 C 端助手；身份、信任、担保、争议处理均无消费级方案。

## 关键数据点

| 指标 | 数值 | 年份/时点 | 来源 |
|---|---|---|---|
| A2A 支持组织数 | 150+（一年前为 50+） | 2026.04 | linuxfoundation.org |
| MCP 活跃公共服务器 / 月 SDK 下载 | 10,000+ / 97M+ | 2025.12 | digitalapplied.com（引 Anthropic） |
| MCP 官方 Registry 服务器记录 | 9,652（最新版）/ 28,959（含版本） | 2026.05.24 | digitalapplied.com |
| 生产环境使用 MCP 的软件组织占比 | 41% | 2026（Stacklok 报告） | workos.com |
| MCP 服务器实现 OAuth 2.1 比例 / 完全无认证比例 | 8.5% / 25% | 2026 审计 | nimblebrain.ai |
| ChatGPT 周活 / 购物类查询 | 8-9 亿 / 约 5,000 万次每天 | 2026.02 | digitalcommerce360.com |
| AP2 公开落地数 | 仅 3 个（PayPal、Mastercard 试点、x402 扩展） | 2026.04 | appliedtechnologyindex.com |
| SiteMinder 接入酒店 / 年处理间夜 | 53,000+ 家 / 3 亿+ | 2026.04 | siteminder.com |
| 酒店主页无结构化数据比例 | 36.3%（n=121,425） | 2026 | digitalfoxllc.com |
| 酒店网站有 llms.txt 比例 | 6.3%（n=105,002） | 2026.03 | digitalfoxllc.com |
| 支付宝 AI 支付笔数 / 智能体框架覆盖 | 3 亿+ 笔 / 95% | 截至 2026.05 末 | finance.sina.com.cn |
| 微信 AI Agent 时间表 | 2026 年中灰度、Q3 放量；首批美团/携程/同程/滴滴 | 2026.06 | caixin.com / aibase.cn |
| IDC：AI 智能体执行的旅行预订占比预测 | 30% | 2030（预测） | siteminder.com 引 IDC |
| 中国《人工智能 智能体互联》国标文件 | 8 项 GB/Z 185-2026，50 家企业试点 | 2026.06 | stdaily.com / cls.cn |

## 对相关假设的含义

- **H3（微信智能体是重大机会）——本维度最强支持**：微信 AI Agent 确实存在、时间表明确（2026 年中灰度、Q3 放量）、目标就是"自然语言→调用小程序→搜索比价下单支付全闭环"，且微信支付 MCP 已就绪。但**首批内测名单是美团/携程/同程/滴滴**——大平台 OTA 抢先卡位，微信入口不天然利好小酒店直连；"自动模式"接入（平台自动解析小程序页面）可能降低住小叮方案的独占性。
- **H5（全球首家 0 手续费 A2A 订房平台）——受实质性挑战**："帮酒店接入 AI 智能体渠道"已有强在位者：SiteMinder 两条 MCP 产品线（2026.04）、Sabre agentic API（2025.09）。"全球首家"表述难以成立，需改为更精确的差异化定位（如"0 佣金 + 免费接入 + 微信生态"组合）。0 手续费本身仍是差异点（SiteMinder Channels Plus 按完成入住收佣）。
- **H1/H2（OTA 消失/窗口期）——本维度提供反面证据**：OpenAI 主动放弃旅游交易闭环、Expedia/Booking 成为 ChatGPT Apps 首批伙伴、携程/同程进入微信 AI 首批内测——OTA 非但没有"因利润受损拒绝自我革命"，反而在**主动占领每一个新智能体入口**。短窗口期存在（支付/信任层未闭环），但"OTA 被 A2A 取代而消失"在 2026 年证据不足。
- **H4/H6**：微信支付 MCP、支付宝"SKILL 内调用支付"证明**按数字员工/智能体收费的收款通路技术上已通**（支持 H4 可行性）；Skills 已成跨平台开放标准且有支付接口（支持 H6 中 Skills 载体的选择）。
- **架构可行性总判断**："A2A+MCP+Skills 让个人智能体找到酒店"在 2026 年是**"半可行"**：以 MCP 服务器+微信小程序+支付 MCP 组合、挂靠超级入口（微信/ChatGPT/Gemini）的形态可落地；以开放点对点 A2A（个人智能体读 agent card 直接下单）的形态仍属超前概念，全球范围内无生产案例，估计为 2027+ 议题。

## 证据缺口

1. 仅有搜索摘要、无法核对原文全文（环境限制），MCP registry 计数、Stacklok 41% 等数字未经原始报告复核。
2. DerbySoft 是否有正式 MCP/agent 分销接口未证实（仅见博客与 Voice Agent 宣传）。
3. 微信 AI Agent 对长尾/非头部小程序的接入门槛、审核机制、流量分配与分成机制完全未知——这是 H3 商业价值的关键变量。
4. 需求侧"个人智能体消费 A2A agent card 完成真实商业交易"的案例为零，无法判断该路径成熟时间表。
5. AHLA/HTNG DART 五层架构的细节文档与实施时间表未获取；OpenTravel 新一代分销标准的具体进度不明。

## 来源列表

1. https://www.linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year
2. https://www.hpcwire.com/aiwire/2026/04/09/linux-foundation-a2a-protocol-marks-one-year-with-broad-enterprise-and-cloud-adoption/
3. https://www.glukhov.org/ai-systems/comparisons/a2a-protocol-2026-adoption/
4. https://a2a-protocol.org/latest/topics/agent-discovery/
5. https://zylos.ai/research/2026-03-07-ai-agent-identity-discovery-trust-frameworks
6. https://arxiv.org/pdf/2505.12490 （A2A 敏感数据防护缺口）
7. https://arxiv.org/pdf/2505.02279 （四协议学术综述）
8. https://www.digitalapplied.com/blog/mcp-adoption-statistics-2026-model-context-protocol
9. https://workos.com/blog/everything-your-team-needs-to-know-about-mcp-in-2026
10. https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/
11. https://nimblebrain.ai/blog/state-of-mcp-security-2026/
12. https://www.techtimes.com/articles/318708/20260619/mcp-enterprise-authorization-goes-stable-zero-touch-sso-okta-anthropic-vs-code.htm
13. https://thenewstack.io/mcp-gets-its-missing-enterprise-authorization-layer/
14. https://stripe.com/newsroom/news/stripe-openai-instant-checkout
15. https://openai.com/index/buy-it-in-chatgpt/
16. https://www.digitalcommerce360.com/2026/02/16/openai-expands-agentic-commerce-push/
17. https://github.com/agentic-commerce-protocol/agentic-commerce-protocol
18. https://skift.com/2026/03/05/openai-chatgpt-checkout-walkback/
19. https://skift.com/2025/10/06/expedia-booking-chatgpt-apps-openai/
20. https://www.phocuswire.com/openai-chatgpt-apps-expedia-booking-tripadvisor
21. https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol
22. https://appliedtechnologyindex.com/research/2026-comparative-analysis-agentic-commerce-payment-protocols/
23. https://ap2-protocol.org/
24. https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/
25. https://searchengineland.com/google-expands-universal-commerce-protocol-and-launches-new-agentic-shopping-tools-478113
26. https://shopify.engineering/UCP
27. https://zuplo.com/blog/agent-protocol-stack-mcp-a2a-acp-2026
28. https://zylos.ai/research/2026-03-26-agent-interoperability-protocols-mcp-a2a-acp-convergence/
29. https://dev.to/alexmercedcoder/the-state-of-agentic-ai-standards-in-2026-mcp-a2a-webmcp-osi-and-the-protocol-stack-taking-3o2l
30. https://www.sabre.com/releases/sabre-seizes-first-mover-position-with-comprehensive-agentic-apis-for-travel/
31. https://www.phocuswire.com/sabre-api-agentic-ai-mcp
32. https://skift.com/2026/01/06/sabre-ces-agentic-ai-travel-trip-booking-demo/
33. https://www.siteminder.com/news/siteminder-ai-hotel-distribution/
34. https://www.phocuswire.com/news/technology/siteminder-links-hotel-inventory-ai-booking-channels-mcp
35. https://www.siteminder.com/r/ai-hotel-booking-distribution/
36. https://www.siteminder.com/r/ai-travel-agent/
37. https://www.derbysoft.com/resources/blog/ai-is-now-table-stakes-so-what-comes-next/
38. https://www.hospitalitynet.org/opinion/4129485/the-next-shift-in-ai-distribution-from-mcp-to-a2a-and-why-it-matters-for-hotels
39. https://opentravel.org/news/recommendations-released-for-future-of-hotel-distribution-connectivity-standards/
40. https://digitalfoxllc.com/llms-txt.html
41. https://www.innsight.com/blog/llm-txt-for-hotels
42. https://help.aliyun.com/zh/model-studio/mcp-introduction
43. https://docs.coze.cn/recent-updates
44. https://companies.caixin.com/m/2026-06-09/102452577.html
45. https://www.guancha.cn/economy/2026_06_08_819794.shtml
46. https://news.aibase.cn/news/26099
47. https://www.qbitai.com/2025/07/304752.html
48. https://www.tmtpost.com/8014103.html
49. https://a2a.alipay.com/
50. https://aipay.alipay.com/docs/ai-receive/MACHINE_PAY.html
51. https://finance.sina.com.cn/cj/2026-05-26/doc-inhzffsq9050427.shtml
52. https://cn.chinadaily.com.cn/a/202504/25/WS680b4f82a310f542634747a8.html
53. https://www.stdaily.com/web/gdxw/2026-06/09/content_529630.html
54. https://www.cls.cn/detail/2412385
55. https://www.163.com/dy/article/L08T5JRA05385JBT.html （微信+五大手机厂商 A2A 互联）
56. https://agentskills.io/home
57. https://agentman.ai/blog/agent-skills-ecosystem-report-2026
58. https://www.unite.ai/anthropic-opens-agent-skills-standard-continuing-its-pattern-of-building-industry-infrastructure/
