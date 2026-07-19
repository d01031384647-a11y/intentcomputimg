# 03 - 全球OTA的AI战略与去中介化风险

> 研究日期：2026-07-19 ｜ 信息时效：以2025-2026年为主 ｜ 方法：16次WebSearch（中英文混合），仅搜索引擎摘要，未直接抓取网页
> 核心问题：OTA们是在抵抗agent还是在拥抱agent？他们与模型厂商的合作是防御还是自杀？专业机构判断OTA被绕开的概率与时间线如何？

## 概述

**总判断：全球主要OTA没有抵抗agentic AI，而是在系统性地把自己改造成"AI智能体的供给方/交易底座"，且截至2026年中，这一防御在事实层面是成功的。**

三条主线证据：
1. **OTA全面拥抱**：Booking、Expedia、Trip.com都已推出自有agentic产品，并把库存以App/MCP/API形式接入ChatGPT等AI入口；Booking 2026年追加约7亿美元投资推进GenAI与Connected Trip。
2. **模型厂商撤退**：OpenAI于2026年3月放弃ChatGPT内直接完成交易（Instant Checkout），将交易环节交回第三方App（Booking.com、Expedia等）；Google公开声明"无意成为OTA"、不做merchant of record。消息公布后Expedia股价+12%、Booking +8%——市场把"AI平台不做交易"解读为OTA的重大利好。
3. **专业机构判断**：摩根士丹利认为OTA"可能是AI的赢家而非受害者"（将Booking上调至增持）；Skift调研显示仅2%旅行者愿让AI代订；McKinsey×Skift报告给出四种情景，"agent接管"只是其中最远期一种；IDC预测到2030年经智能体完成的预订最多占30%。近期（1-3年）OTA被大规模绕开的概率被主流机构判定为低，但2月2026年Booking财报超预期后仍暴跌6-8%（"AI panic"），说明资本市场对长期叙事风险的定价分歧巨大。

**对本项目最重要的反面事实**：a) OTA正在自我革命，H2假设的"窗口期"比预想窄；b) "0佣金"并非空白定位——京东2025年6月已在中国推出"最高三年0佣金"酒旅计划（两天近5万家酒店申请），PayPal/Selfbook也提供免佣金酒店预订通道；c) 消费者只有2-8%愿意让AI完成支付，C端个人智能体直接完成订房的需求侧成熟度远低于供给侧叙事。

---

## 关键发现（按主体分组，每条注明信息性质）

### 1. Booking Holdings：从"被颠覆对象"到"agent供给方"

- 【事实】Booking Holdings在2025年全年推出多项GenAI/agentic能力（自然语言搜索、智能筛选、AI客服agent），2026年重点是把这些agentic能力互联为统一个性化体验；GenAI已使其客服成本同比下降（同时处理量+10%）。来源：https://www.pymnts.com/earnings/2026/ai-cuts-booking-holdings-customer-service-costs-10-as-volumes-rise/
- 【事实】Booking 2026年在基线之外追加约7亿美元投资，用于GenAI、Connected Trip、亚洲与美国扩张、广告业务。来源：https://stocktwits.com/news-articles/markets/equity/bkng-stock-climbs-q4-earnings-beat-stock-split-700-m-ai-push/cZRjK4KR4wd
- 【事实】Booking.com与OpenAI深度合作：AI Trip Planner基于OpenAI GPT模型（2023年6月上线，10周做出原型），2025年10月成为ChatGPT首批"应用内App"合作伙伴，体验"由MCP server驱动"，用户可在ChatGPT内探索并进入其酒店库存。来源：https://openai.com/index/booking-com/ ；https://news.booking.com/bookingcom-debuts-agentic-ai-innovations-adding-to-its-robust-suite-of-genai-tools-for-customers/ ；https://www.phocuswire.com/openai-chatgpt-apps-expedia-booking-tripadvisor
- 【事实】CEO Glenn Fogel在2025年2月财报会上公开淡化"agentic AI平台将取代Booking"的担忧；2026年2月强调与独立酒店的关系是护城河，并透露正与AI平台就"数据共享与经济安排"谈判。来源：https://skift.com/2025/02/20/booking-holdings-downplays-concerns-that-agentic-ai-platforms-will-displace-it/ ；https://skift.com/2026/02/18/booking-ceo-touts-ties-with-independent-hotels-as-agentic-ai-and-airbnb-seek-gains/
- 【事实】Booking Q4 2025营收63.5亿美元（+16.1%），EPS超预期，但财报次日股价暴跌6-8%，被普遍归因于"AI叙事恐慌"而非基本面。来源：https://www.tikr.com/blog/booking-stock-tumbles-6-on-ai-panic-do-analysts-see-a-rebound-to-8200-in-2026 ；https://markets.financialcontent.com/stocks/article/marketminute-2026-2-19-booking-holdings-beats-earnings-but-shares-sink-as-ai-disruption-fears-mount
- 【事实】Booking take rate保持稳定约10.3%（2025 Q1），Q1 2025总预订额467亿美元（+7%）。行业层面OTA佣金普遍15-30%，叠加可见性/推广费后部分酒店有效费率接近30-40%。来源：https://thehotelblueprint.com/ota-market-snapshot-2025-strategic-shifts-trends/ ；https://www.cloudbeds.com/online-travel-agencies/commissions/
- 【公司宣传】Connected Trip战略：用AI把机票、住宿、租车、体验缝合成单一行程（2024年经其平台售出约4900万张机票、8300万租车日），瞄准佣金率20-30%的体验类目（酒店为10-15%）。来源：https://www.youngurbanproject.com/booking-com-case-study/ ；https://www.klover.ai/booking-holdings-ai-strategy-analysis-of-dominance-in-new-era-of-travel/

### 2. Expedia：B2B/API是其agentic时代的核心押注

- 【事实】Expedia于2024年5月发布AI助手Romie（自有模型+OpenAI混合训练），可在iMessage/WhatsApp群聊中辅助规划、追踪航变；2025年10月与Booking.com同批成为ChatGPT首发App合作伙伴，也是微软Copilot Actions首发伙伴。来源：https://www.travelweekly.com/Travel-News/Travel-Technology/Expedia-Group-unveils-Romie-AI-assistant ；https://www.phocuswire.com/openai-chatgpt-apps-expedia-booking-tripadvisor
- 【事实】Expedia FY2025年报（10-K）首次将agentic AI明确列为风险因素（上一年年报完全未提及）；同时其B2B业务（向合作方AI智能体开放库存的API）增速超过C端。这被解读为"OTA打算成为AI助手底下的铁轨（rails）"。来源：https://skift.com/2026/02/20/expedia-ai-agentic-10k-earnings-q4-2025/ ；https://www.customerexperiencedive.com/news/expedia-ai-experience-copilot-openai-mobile/747814/
- 【事实】OpenAI宣布放弃交易环节后，Expedia单日股价+12%。来源：https://www.tourismtribe.com/chatgpt-instant-checkout-travel-operators/

### 3. Airbnb：明确拒绝早期接入ChatGPT，自建AI

- 【事实】CEO Brian Chesky（2025年10月）：ChatGPT"还不够健壮"，暂不接入；他公开表示"用ChatGPT分发旅行可以，但把OTA切掉'非常困难'"；认为旅行/电商需要富交互界面而非纯文本聊天。来源：https://skift.com/2025/10/22/airbnbs-brian-chesky-chatgpt-can-distribute-travel-but-cutting-out-otas-is-very-difficult/ ；https://www.cnbc.com/2025/10/22/airbnb-chatgpt-ai-chesky.html
- 【事实】Airbnb转而在自有App内堆叠AI能力：客服解决时间从近3小时压缩到6秒，混用OpenAI/阿里/谷歌等13个模型；2026年6月宣布开设AI实验室。来源：https://finance.yahoo.com/news/airbnb-ceo-freezes-chatgpt-deal-083329080.html ；https://americanbazaaronline.com/2026/06/05/airbnb-to-open-ai-lab-as-ceo-chesky-expands-companys-ai-push-482242/

### 4. Trip.com Group：TripGenie全球化最快

- 【事实/公司宣传】TripGenie已在200+国家使用，2025上半年用户数同比+200%；规划阶段平均会话时长+50%；AI聊天与自助工具处理80%以上售后咨询。另推出Intelli-Trip帮酒店承接入境需求（26种语言）。来源：https://www.investing.com/news/transcripts/earnings-call-transcript-tripcom-posts-robust-q1-2025-growth-eyes-ai-expansion-93CH-4204929 ；https://beyondspx.com/quote/TCOM/analysis/trip-com-s-ai-powered-travel-platform-china-s-outbound-boom-meets-margin-inflection-nasdaq-tcom
- 【事实】2026年携程大会披露"智能引擎3.0"规模化落地，称为合作伙伴带来超10%订单增长；2026年6月8日携程、同程接入"微信AI"，用户可自然语言直接订酒店——预订入口从"货架"转向"管家"。来源：http://mp.cnfol.com/59432/article/1780659651-142472391.html
- 【事实】中国市场格局剧变：京东2025年6月18日公开信宣布酒店"最高三年0佣金"（PLUS会员计划），两天收到近5万家酒店入驻申请，逻辑是靠供应链服务而非佣金赚钱；抖音酒旅GMV年增50%+；美团酒旅份额升至约13%。来源：https://m.traveldaily.cn/article/187384 ；https://finance.sina.com.cn/jjxw/2025-06-18/doc-infanwwc5584911.shtml ；http://mp.cnfol.com/59432/article/1780659651-142472391.html

### 5. 酒店集团：自建agentic直订能力，但接入AI入口同样依赖平台

- 【事实】万豪2026年2月宣布当年技术投资超10亿美元（1/3以上投数字化转型），构建"agentic mesh"共享智能层，重建PMS/中央预订/忠诚度平台；希尔顿2026年3月在hilton.com上线AI Planner；雅高把忠诚度App以20多种语言接入ChatGPT；洲际推出AI增强CRM并把酒店内容重构为机器可读格式。来源：https://www.hospitalitynet.org/opinion/4133283/hotel-chains-built-ai-for-the-traveler-who-comes-to-them-first-that-traveler-is-leaving ；https://otelciro.com/en/news/hilton-ai-planner-yarisina-girdi
- 【事实】MCP在2026上半年成为酒店分销的事实性集成标准：SiteMinder通过MCP向AI模型直供实时库存与价格；Simple Booking发布MCP连接器；创业公司Agentic Hospitality的TravelOS MCP+ChatGPT App主打"品牌而非中介居于AI预订中心"。来源：https://www.siteminder.com/r/ai-hotel-booking-distribution/ ；https://www.hospitalitynet.org/news/4132950/simple-booking-accelerates-ai-transformation-of-hotel-distribution-with-release-of-mcp-connectors ；https://www.hospitalitynet.org/news/4132086/agentic-hospitalitys-travelos-mcp-chatgpt-app-is-putting-brands-not-intermediaries-at-the-center-of-ai-bookings
- 【媒体推测】"酒店将再输一次分销战争（这次输给AI助手）"：OpenAI进入旅行走的是聚合商（即OTA）而非单体酒店路线，酒店集团的AI是为"先来官网的客人"建的，而客人正在流向AI入口。来源：https://medium.com/predict/hotels-are-about-to-lose-another-distribution-war-this-time-to-ai-assistants-52b4843e1356

### 6. AI平台方：集体退出"交易"、退守"发现"

- 【事实】OpenAI于2025年推出Instant Checkout与Agentic Commerce Protocol（与Stripe共建），但2026年3月撤回travel场景的站内交易——原因包括仅约12家Shopify商户真正上线、用户"到输入信用卡那一步就流失去自己信任的渠道"、旅行的实时库存/合规/售后过于复杂；交易改由第三方App（Booking.com、Expedia、Skyscanner、Tripadvisor、雅高等）承接。来源：https://skift.com/2026/03/05/openai-chatgpt-checkout-walkback/ ；https://www.phocuswire.com/news/technology/openai-chatgpt-instant-checkout-travel-intermediaries ；https://openai.com/index/buy-it-in-chatgpt/
- 【事实】Google公开澄清"无意成为OTA"、不做merchant of record：AI Mode的agentic机酒预订（2026年宣布、截至6月未上线）由Booking.com、Expedia、万豪、洲际、Choice、Wyndham等伙伴承接交易与履约。来源：https://skift.com/2025/11/20/google-agentic-ai-travel-booking-no-intention-become-ota/ ；https://www.phocuswire.com/google-agentic-travel-booking-ai
- 【事实】Perplexity（2025年3月）与Selfbook、Tripadvisor合作实现站内订酒店（约14万家酒店池）；Selfbook同时为PayPal提供酒店预订，PayPal Offers渠道的酒店专属价**不收佣金**。来源：https://www.phocuswire.com/perplexity-selfbook-agentic-ai-travel-booking-tripadvisor ；https://newsroom.paypal-corp.com/2025-06-09-Selfbook-Chooses-PayPal-as-Commerce-Partner
- 【事实】2026年2月Sabre+PayPal+MindTrip宣布端到端agentic预订管线（自然语言→Sabre Mosaic API的420+航司/200万酒店→PayPal支付）。来源：https://www.hospitalitynet.org/opinion/4128688.html （及相关报道）

### 7. 专业机构对"去中介化概率与时间线"的判断

- 【事实（机构观点）】摩根士丹利：OTA可能是AI受益者而非受害者——早期agentic工具并未绕开OTA，而是把用户导流回OTA的App/网站完成交易；AI平台不愿承担支付风险、客服、退款与监管义务，OTA仍居交易流中心；已将Booking上调至增持（Overweight）。来源：https://in.investing.com/news/economy-news/online-travel-agencies-may-emerge-as-ai-winners-morgan-stanley-says-5265306 ；https://seekingalpha.com/news/4555773-booking-holdings-has-little-to-fear-from-agentic-ai-disruption---morgan-stanley
- 【事实（调研数据）】Skift Research：90%+消费者信任AI生成的旅行信息，但仅约2%愿让AI代为完成购买；Expedia 2026年4月调研：仅8%的人放心让AI订行程（顾虑：控制权、隐私、客服）。来源：https://skift.com/2026/04/14/expedia-ai-survey-travel-discovery-booking-8-percent/ ；https://skift.com/2026/03/03/travel-brands-are-building-ai-agents-for-a-consumer-that-doesnt-exist/
- 【事实（调研数据）】供给侧：仅11%的旅行企业拥有能实时定价并完成预订的AI agent（2026年6月，Gimmonix）；61%的旅行企业在试验或扩展agentic AI；约40%美国旅行者2025年用GenAI规划行程。来源：https://gimmonix.com/news/only-11-percent-agent-ready-2026 ；https://www.digitalapplied.com/blog/agentic-ai-for-hospitality-travel-marketing-vertical-2026
- 【事实（机构预测）】IDC：到2030年经由智能体完成的预订最多可达30%。McKinsey×Skift《Remapping Travel with Agentic AI》给出四种情景：Copilot commerce（agent嵌入现有结构，OTA/官网仍是入口）→ AI体验策展 → 直订复兴（供应商自有agent）→ Agent接管（C端agent与供给端agent直接协商交易）；并警告若LLM"拥有"旅行者关系，中介将被推入幕后基础设施角色。"极度使用"AI规划行程的旅行者一年内从13%升至30%（+124%）。来源：https://www.mckinsey.com/~/media/mckinsey/industries/travel/our%20insights/remapping%20travel%20with%20agentic%20ai/remapping-travel-with-agentic-ai_final.pdf ；https://skift.com/insights/new-report-remapping-travel-with-agentic-ai/
- 【媒体推测/反方观点】"AI搜索若经官方API把高意图旅客直接导向brand.com，OTA的15-25%佣金在结构上是脆弱的"（Google agentic shift分析）；"清洁基础设施上的OTA在agentic世界可能更强大——agent无法逐家敲几千个供应商的门，能实时交易的库存早已被聚合、标准化"（OTA韧性论）。来源：https://www.americasgreatresorts.net/google-io-2026-agentic-search-hotel-demand/ ；https://www.mylighthouse.com/resources/blog/ai-is-changing-hotel-distribution ；https://gimmonix.com/news/agentic-ai-is-coming-to-cut-otas-out-or-is-it

---

## 关键数据点（表格）

| 指标 | 数值 | 年份 | 来源 |
|---|---|---|---|
| Booking take rate | 约10.3%（保持稳定） | 2025 Q1 | thehotelblueprint.com |
| 行业OTA佣金区间 | 15-30%；叠加推广费后有效费率可达30-40% | 2025-2026 | cloudbeds.com / thehotelblueprint.com |
| OTA占全球酒店预订份额 | 约55% | 2025 | thehotelblueprint.com |
| Booking Q4 2025营收 | 63.5亿美元（+16.1%），财报超预期后股价仍跌6-8%（AI panic） | 2026.2 | tikr.com / financialcontent |
| Booking 2026追加AI等投资 | 约7亿美元（基线之上） | 2026 | stocktwits.com / pymnts.com |
| 愿让AI代订的旅行者比例 | Skift约2%；Expedia调研8% | 2025-2026 | skift.com |
| 能被AI agent实时交易的旅行企业 | 仅11% | 2026.6 | gimmonix.com |
| "极度使用"AI规划行程的旅行者 | 13%→30%（+124% YoY） | 2025 | McKinsey×Skift |
| 经智能体预订占比预测 | 最高30%（2030年） | IDC预测 | gimmonix.com转引 |
| TripGenie | 200+国家使用，用户+200% YoY；会话时长+50% | 2025 H1 | investing.com |
| 万豪技术投资 | 超10亿美元/年（含agentic mesh） | 2026 | hospitalitynet.org |
| 京东酒店0佣金 | 最高3年0佣金，两天近5万家酒店申请 | 2025.6 | traveldaily.cn / sina |
| OpenAI撤回travel站内交易后股价 | Expedia +12%、Booking +8%、Tripadvisor +5% | 2026.3 | tourismtribe.com / skift.com |

---

## 对相关假设的含义

- **H1（OTA将被A2A交易取代而消失）：当前证据总体不支持强形式的H1。** AI平台方（OpenAI、Google）在2026年集体退守"发现"环节、把交易交回OTA；摩根士丹利等判断OTA反而受益；消费者只有2-8%愿让AI代订。弱形式（OTA被推入幕后基础设施、品牌溢价与广告价值受损）有McKinsey情景与Google agentic shift分析支持，但时间线在2030年前后且路径不确定。**H1需要降级为长期条件性假设。**
- **H2（OTA不会自我革命，留下窗口期）：被显著削弱。** Booking追加7亿美元、Expedia把B2B API作为主战略、Trip.com的TripGenie全球化、携程接入微信AI——OTA在积极自我改造。但有一个重要保留：OTA的"自我革命"没有触碰佣金模式本身（take rate稳定在10.3%），它们革的是交互层的命，不是商业模式的命。**窗口期存在，但只在"佣金结构"维度，不在"AI能力"维度。**
- **H3（微信智能体是重大机会）：获得间接支持。** 2026年6月携程、同程已接入微信AI实现自然语言订酒店——证明微信AI入口真实存在且OTA已抢先入驻；这既验证机会真实，也意味着"帮酒店直连微信智能体"要与已入驻的OTA正面竞争。
- **H5（全球首家0手续费定位）：受到直接挑战。** 京东2025年6月已推出"最高三年0佣金"酒旅计划（虽为期限性补贴而非A2A架构），PayPal/Selfbook通道亦免佣。"全球首家0手续费"表述在事实层面站不住；可辩护的差异化是"首家基于A2A协议的0佣金直连平台"，但需重新措辞。
- **H4（免费接入+数字员工订阅收费）：方向获得旁证。** 供给侧仅11%企业agent-ready、MCP成为事实标准、酒店集团巨额投入说明"帮中小酒店变得agent-ready"是真实缺口；但需求侧（个人agent代订）成熟度低意味着短期收入必须靠数字员工订阅而非A2A交易量——与该模式设计一致。

## 证据缺口

1. Booking/Expedia与OpenAI等"数据共享与经济安排"谈判的具体分成条款未公开——无法判断AI入口最终抽成结构。
2. 摩根士丹利、大摩之外的卖方（高盛、伯恩斯坦、Jefferies）对去中介化概率的量化评估未直接获取（仅有二手转述）。
3. 经ChatGPT/Perplexity等AI入口实际产生的酒店预订量/GMV没有任何公开数字——"AI入口贡献度"完全缺数据。
4. 酒店集团（万豪等）经AI渠道的直订占比、以及MCP直连产生的实际交易量无公开数据。
5. 微信AI订酒店的详细产品形态、抽成与开放政策（对非OTA商户是否开放）需在"微信智能体"专项维度中补充核实。

## 来源列表

1. https://www.pymnts.com/earnings/2026/ai-cuts-booking-holdings-customer-service-costs-10-as-volumes-rise/
2. https://skift.com/2025/02/20/booking-holdings-downplays-concerns-that-agentic-ai-platforms-will-displace-it/
3. https://skift.com/2026/02/18/booking-ceo-touts-ties-with-independent-hotels-as-agentic-ai-and-airbnb-seek-gains/
4. https://stocktwits.com/news-articles/markets/equity/bkng-stock-climbs-q4-earnings-beat-stock-split-700-m-ai-push/cZRjK4KR4wd
5. https://www.tikr.com/blog/booking-stock-tumbles-6-on-ai-panic-do-analysts-see-a-rebound-to-8200-in-2026
6. https://openai.com/index/booking-com/
7. https://news.booking.com/bookingcom-debuts-agentic-ai-innovations-adding-to-its-robust-suite-of-genai-tools-for-customers/
8. https://www.phocuswire.com/openai-chatgpt-apps-expedia-booking-tripadvisor
9. https://www.klover.ai/booking-holdings-ai-strategy-analysis-of-dominance-in-new-era-of-travel/
10. https://www.youngurbanproject.com/booking-com-case-study/
11. https://thehotelblueprint.com/ota-market-snapshot-2025-strategic-shifts-trends/
12. https://www.cloudbeds.com/online-travel-agencies/commissions/
13. https://www.travelweekly.com/Travel-News/Travel-Technology/Expedia-Group-unveils-Romie-AI-assistant
14. https://www.customerexperiencedive.com/news/expedia-ai-experience-copilot-openai-mobile/747814/
15. https://skift.com/2026/02/20/expedia-ai-agentic-10k-earnings-q4-2025/
16. https://skift.com/2025/10/22/airbnbs-brian-chesky-chatgpt-can-distribute-travel-but-cutting-out-otas-is-very-difficult/
17. https://www.cnbc.com/2025/10/22/airbnb-chatgpt-ai-chesky.html
18. https://finance.yahoo.com/news/airbnb-ceo-freezes-chatgpt-deal-083329080.html
19. https://americanbazaaronline.com/2026/06/05/airbnb-to-open-ai-lab-as-ceo-chesky-expands-companys-ai-push-482242/
20. https://www.investing.com/news/transcripts/earnings-call-transcript-tripcom-posts-robust-q1-2025-growth-eyes-ai-expansion-93CH-4204929
21. https://beyondspx.com/quote/TCOM/analysis/trip-com-s-ai-powered-travel-platform-china-s-outbound-boom-meets-margin-inflection-nasdaq-tcom
22. https://www.hospitalitynet.org/opinion/4133283/hotel-chains-built-ai-for-the-traveler-who-comes-to-them-first-that-traveler-is-leaving
23. https://otelciro.com/en/news/hilton-ai-planner-yarisina-girdi
24. https://www.siteminder.com/r/ai-hotel-booking-distribution/
25. https://www.hospitalitynet.org/news/4132950/simple-booking-accelerates-ai-transformation-of-hotel-distribution-with-release-of-mcp-connectors
26. https://www.hospitalitynet.org/news/4132086/agentic-hospitalitys-travelos-mcp-chatgpt-app-is-putting-brands-not-intermediaries-at-the-center-of-ai-bookings
27. https://medium.com/predict/hotels-are-about-to-lose-another-distribution-war-this-time-to-ai-assistants-52b4843e1356
28. https://skift.com/2026/03/05/openai-chatgpt-checkout-walkback/
29. https://skift.com/2026/03/20/otas-ai-discovery-transactions/
30. https://www.phocuswire.com/news/technology/openai-chatgpt-instant-checkout-travel-intermediaries
31. https://openai.com/index/buy-it-in-chatgpt/
32. https://www.tourismtribe.com/chatgpt-instant-checkout-travel-operators/
33. https://skift.com/2025/11/20/google-agentic-ai-travel-booking-no-intention-become-ota/
34. https://www.phocuswire.com/google-agentic-travel-booking-ai
35. https://www.americasgreatresorts.net/google-io-2026-agentic-search-hotel-demand/
36. https://www.phocuswire.com/perplexity-selfbook-agentic-ai-travel-booking-tripadvisor
37. https://newsroom.paypal-corp.com/2025-06-09-Selfbook-Chooses-PayPal-as-Commerce-Partner
38. https://in.investing.com/news/economy-news/online-travel-agencies-may-emerge-as-ai-winners-morgan-stanley-says-5265306
39. https://seekingalpha.com/news/4555773-booking-holdings-has-little-to-fear-from-agentic-ai-disruption---morgan-stanley
40. https://skift.com/2026/04/14/expedia-ai-survey-travel-discovery-booking-8-percent/
41. https://skift.com/2026/03/03/travel-brands-are-building-ai-agents-for-a-consumer-that-doesnt-exist/
42. https://gimmonix.com/news/only-11-percent-agent-ready-2026
43. https://gimmonix.com/news/agentic-ai-is-coming-to-cut-otas-out-or-is-it
44. https://www.mckinsey.com/~/media/mckinsey/industries/travel/our%20insights/remapping%20travel%20with%20agentic%20ai/remapping-travel-with-agentic-ai_final.pdf
45. https://skift.com/insights/new-report-remapping-travel-with-agentic-ai/
46. https://www.mylighthouse.com/resources/blog/ai-is-changing-hotel-distribution
47. http://mp.cnfol.com/59432/article/1780659651-142472391.html
48. https://m.traveldaily.cn/article/187384
49. https://finance.sina.com.cn/jjxw/2025-06-18/doc-infanwwc5584911.shtml
50. https://www.digitalapplied.com/blog/agentic-ai-for-hospitality-travel-marketing-vertical-2026
