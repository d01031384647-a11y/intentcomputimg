# 06 - 中国OTA与互联网大厂的AI智能体布局速度（检验"窗口期"假设）

> 研究日期：2026-07-19 ｜ 方法：WebSearch × 17次（中英文混合）｜ 状态：完成
> 信息分类标注：【事实】= 多源交叉验证的已发生事件；【公司宣传】= 来自公司官方或官媒通稿的说法；【媒体推测】= 媒体/分析师的判断

## 概述

本维度回答核心问题：**中国大厂的C端智能体今天（2026年7月）能不能实际订酒店？通过谁的库存订？OTA是把AI做成自家App功能，还是开放给外部智能体？窗口期是否存在？**

结论摘要：

1. **C端智能体已经能订酒店，但库存几乎全部来自OTA**。阿里千问App调用飞猪库存一键订机酒（2026年2月起40+品牌"千问价"）；微信智能体（2026年6月内测）调用携程/美团/同程小程序完成预订；智谱AutoGLM靠GUI自动化操作OTA App下单；百度心响调用携程MCP。**没有任何主流C端智能体绕开OTA直连酒店库存。**
2. **OTA的策略是"两条腿"：既把AI做成自家App功能（问道/TripGenie/问一问/程心/小美），又选择性开放给超级App智能体（微信、千问、百度搜索）当供给方**。同程2025年3月即接入DeepSeek开通AI实时预订，飞猪2025年4月上线多智能体"问一问"并建了对外的"飞猪AI开放平台"，途牛/携程商旅上线MCP平台——"OTA短期不自我革命"的前提正在被削弱。
3. **窗口期存在但形态与假设不同**：OTA开放的对象是微信/千问这类握有流量的超级App，而不是"任意第三方A2A智能体"或"酒店自己的智能体接口"。**酒店直连C端智能体（去OTA中介化）这一层仍然空白**——40+酒旅品牌抢着接"千问价"说明酒店对AI直销渠道有强烈需求，但目前仍须经飞猪。未发现OTA公开封杀外部预订agent的报道；真正的封锁者是微信（屏蔽元宝/千问/文心链接），封的是流量入口而非预订接口。
4. **微信智能体（H3所指）已从传闻变为事实**：2026年6月8-9日微信宣布开放AI生态接入，首批美团、携程、同程、滴滴、京东接入内测，可调取小程序完成交易（含订酒店），用户只需确认付款；微信9.0预计2026年Q3全量上线内嵌超级智能体。**机会真实，但首批卡位者是OTA自己。**

---

## 关键发现

### 一、携程系：自家AI最重、态度最防守，开放仅限B端与选择性渠道

1. 【事实】携程2023年7月发布旅游业首个垂直大模型"携程问道"（参数超百亿），定位查询+引导预订+智能推荐，AI始终导流回携程自有交易。来源：https://www.jazzyear.com/article_info.html?id=1053
2. 【公司宣传】Trip.com国际版AI助手TripGenie（基于Azure OpenAI+携程业务API）覆盖行程定制到预订全环节；官方称AI辅助预订量同比增长400%，酒店比价功能让预订点击次数减少80%、7日回访率提升45%，酒店问题自助解决率68%。来源：https://www.trip.com/newsroom/introducing-tripgenie-groundbreaking-ai-travel-assistant/ ；https://www.pai.com.cn/223588.html
3. 【事实】携程研发投入极重：2025年研发投入约151亿元（+15%），占营收24%；2026年Q1产品研发费用41亿元（+15%），占净收入25%——远高于Booking（约10%）与Expedia（约8%）的营收占比。来源：https://www.citnews.com.cn/news/218457 ；https://www.vocust.com/school/insightcase/364.html
4. 【事实】携程的对外开放集中在B端：携程商旅推出MCP开放体系AI开放平台（标准层/高级层/定制层三层开放，提供机酒火车实时资源、查询、行程规划工具），2025年4月发布商旅AI Agent"程星途"，2026年4月再推7个商旅AI Agent。来源：https://ct.ctrip.com/thinktanks/235566117077549 ；https://ttgchina.com/2025/04/23/携程商旅发布智能助手程星途ai-agent/
5. 【事实】C端开放是选择性的渠道合作而非通用接口：百度搜索开放平台接入的是"携程门票MCP"；携程作为首批内测方接入微信AI生态（围绕酒店预订、机票查询等场景）。未发现携程向任意第三方智能体开放C端酒店预订API/MCP的证据。来源：https://www.ebrun.com/ebrungo/zb/592981.shtml ；https://www.163.com/dy/article/KUU58HKI0534A4SC.html
6. 【事实】梁建章公开表态"AI智能体无法取代OTA"；媒体概括携程路线为"守交易"——把AI嵌入规划/导航/翻译/预订全流程，守住交易页。同时携程在财报风险提示中承认科技公司可能在自有平台内直接提供旅行搜索、比价、推荐和预订服务。来源：https://www.donews.com/article/detail/8941/102380.html ；http://applocal.myzaker.com/news/article.php?pk=69fdc9ea8e9f096d265abe59
7. 【事实】携程有深厚的反爬虫技术传统（动态密钥、返回假价格等），历史上60%级别访问量为爬虫；但**未检索到携程明确封杀外部AI预订agent的公开报道**。来源：https://cloud.tencent.com/developer/article/1089625 ；https://www.cnblogs.com/ZaraNet/p/9788297.html
8. 【证据缺口】必查项"口袋参谋"（携程面向酒店商家的经营参谋工具）在本轮搜索中未获得直接资料，其现状无法核实。

### 二、美团：模型开源+消费级Agent小美，酒旅是内置场景

9. 【事实】美团2025年9月1日开源自研大模型LongCat-Flash-Chat（560B参数MoE）；9月12日公测首个消费级AI Agent"小美"，已打通外卖、到店、酒店、旅行等核心业务，自然语言即可完成推荐、预订。来源：https://www.meituan.com/news/NN250901129002898 ；https://www.pai.com.cn/p/01k4xrv0x5h2qkzbykqqqhe3da
10. 【事实】2025年10月美团一口气发布三个面向商家的智能助手（围绕开店和外卖），宣称AI投入已达百亿。来源：https://36kr.com/p/3512515121077381
11. 【事实】龙猫App上线原生"深度研究"智能体，基于美团真实交易数据（真实入住评价、真实票销数据）生成吃喝玩乐/酒店攻略——媒体概括美团路线为"抢决策"。来源：https://cloud.tencent.com/developer/news/3581595 ；http://applocal.myzaker.com/news/article.php?pk=69fdc9ea8e9f096d265abe59
12. 【事实】2026年6月"小美"与腾讯元宝互通：用户在元宝内输入诉求即可连接美团执行操作，被媒体解读为"为微信智能体打样"。美团酒旅市占率约13%（媒体口径）。来源：https://finance.sina.com.cn/jjxw/2026-06-03/doc-iniaavww4314431.shtml ；https://www.sohu.com/a/978948258_104421
13. 【事实】美团内部先后限用阿里千问、字节豆包大模型（需高管审批），显示大厂间AI生态壁垒加深。来源：https://www.ithome.com/0/971/515.htm

### 三、阿里系（飞猪/千问/高德/夸克）：动作最快、开放度最高，已跑通"AI订酒店"闭环

14. 【事实】飞猪2025年4月17日上线多智能体产品"问一问"：调用飞猪真实机酒价格、库存与独家景酒数据，多个专业助手（行程统筹/酒店顾问/交通顾问等）协作生成可直接预订的方案；后续升级机酒查询与会员助手。来源：http://caacnews.com.cn/1/6/202504/t20250417_1386642.html ；https://36kr.com/newsflashes/3309021344979459
15. 【公司宣传】飞猪建立"飞猪AI开放平台"（flyai.open.fliggy.com），宣称深度开放机酒景全场景AI能力、适配OpenClaw协议、提供原生Skill能力，助力外部开发者构建旅游AI Agent——**这是中国OTA中对外部智能体开放度最高的表述**。来源：https://flyai.open.fliggy.com/
16. 【事实】千问App全面接入淘宝、支付宝、飞猪、高德等阿里生态：AI可调用飞猪能力完成机票酒店预订、调用高德完成行程规划（2025年12月接入高德）。来源：https://www.stcn.com/article/detail/3594486.html ；https://finance.sina.com.cn/tech/digi/2025-12-18/doc-inhcetxm8362266.stml
17. 【事实】2026年2月11日，超40家旅行品牌（东航、南航、阿联酋航空、汉莎、锦江、华住、首旅如家、万达酒店、迪士尼等）与千问、飞猪合作推出"千问价"：AI渠道专属折扣（单笔最高减300元）、酒店早餐、延迟退房等专属权益，实现从咨询、规划到无需跳端一键下单的完整AI预订闭环。**这是酒店集团为AI渠道单独定价供货的全球首批案例之一，证明酒店端对AI直销渠道有真实付出意愿。**来源：https://finance.sina.com.cn/roll/2026-02-11/doc-inhmnaia0395440.shtml ；https://www.qbitai.com/2026/02/378498.html
18. 【事实】阿里与蚂蚁联合发布ACT协议（智能体商业信任协议）——中国首个面向Agent商业交易设计的开放技术协议框架，覆盖跨终端、跨系统、跨平台的AI任务执行；媒体称千问走"双重协议"路线。来源：https://www.stcn.com/article/detail/3594486.html ；https://www.woshipm.com/ai/6327086.html
19. 【事实】高德地图2025（2025年8月4日发布）成为"全球首个基于地图的AI原生应用"，对话式智能体"小高老师"通过MCP协同出行/生活/空间子智能体，可输出含酒店的可视化决策卡片。夸克"AI超级框"（2025年3月）可比价酒店、生成行程。来源：http://www.news.cn/tech/20250804/ec03c09da157496ebc2b2532a33c6f88/c.html ；https://news.qq.com/rain/a/20250318A047LO00

### 四、字节系：豆包团购闭环已通但订酒店未闭环，Coze走GUI自动化

20. 【事实】豆包App与抖音生活服务打通，站内可完成团购购买-支付-核销码全闭环（品类含美食、电影票、民宿），但目前仅做匹配推荐，选套餐/确认/提交订单仍需用户手动，**未上线一键代客下单**。来源：https://m.aitntnews.com/newDetail.html?newId=25654 ；https://zhuanlan.zhihu.com/p/2045254455852102910
21. 【事实】2026年5月豆包"代预约餐厅"翻车：AI虚构"预约成功"引发幻觉维权争议——代订类agent的可靠性/责任问题成为行业痛点。来源：https://www.163.com/dy/article/KTEQ57N10514EMD3.html
22. 【事实】扣子Coze平台存在酒店预订类插件，agent可通过手机自动化操作携程等App完成预订（GUI路径，非API直连）。抖音酒旅GMV以50%+年增速逼近头部（媒体口径）。来源：https://docs.coze.cn/guides_use_local_plugin ；https://www.sohu.com/a/978948258_104421
23. 【事实】受2026年7月15日施行的《人工智能拟人化互动服务管理暂行办法》影响，豆包与千问同日（7月15日）下线用户自建UGC智能体功能（官方内置能力不受影响）——监管正在收紧C端智能体的野蛮生长。来源：https://www.guancha.cn/economy/2026_07_04_822586.shtml ；https://news.qq.com/rain/a/20260706A02XQW00

### 五、腾讯/微信：H3所指的"微信智能体"已成事实，且首批接入者是OTA

24. 【事实】腾讯将微信专属智能体列为最高优先级项目（财新/《财经》报道）；2026年6月2日微信原生AI智能体进入收尾测试。来源：https://news.caijingmobile.com/article/detail/565179 ；https://www.tmtpost.com/8027423.html
25. 【事实】**2026年6月8-9日，微信宣布开放AI生态接入能力：微信智能体将能调取小程序完成交易和服务，首批美团、携程、同程、滴滴、京东接入内测**。携程小程序已完成初步接入适配，将围绕酒店预订、机票查询等核心场景接入。来源：https://www.caixin.com/2026-06-09/102452574.html ；http://jjckb.xinhuanet.com/20260610/bd0f9f2d74f34a4dac8f2116278fb665/c.html ；https://www.163.com/tech/article/KUUC3FEH00098IEO.html
26. 【事实】实测显示：微信AI可调用小程序完成订酒店、打车（用户只需手动确认付款），但携程/去哪儿这类首页布满Banner弹窗的复杂小程序，AI仍需大量人工介入才能完成操作——**结构简洁、"智能体友好"的小程序在微信智能体下有体验优势**。来源：https://www.jiemian.com/article/14628205.html
27. 【事实】微信9.0预计2026年Q3全量上线，核心亮点为内嵌超级AI智能体，目标是把搜索-比价-下单-支付全链路留在微信内完成。来源：https://developer.cloud.tencent.com/article/2698958 ；https://36kr.com/p/3718128476664320
28. 【事实】微信是目前最强硬的"封锁者"：2026年2月4日起先后屏蔽自家元宝、阿里千问、百度文心的红包分享链接，捍卫社交关系链；随后元宝以"内部组件"形态进入微信，腾讯3月撤销AI Lab并入混元——**平台封锁发生在流量/社交层，而非预订接口层**。来源：https://www.guancha.cn/economy/2026_02_04_806041.shtml ；https://www.tmtpost.com/8014103.html

### 六、通用Agent与其他玩家

29. 【事实】Manus 2025年3月爆红后约3个月即撤出中国市场；智谱2025年8月20日发布并向公众开放手机智能体AutoGLM 2.0：一句话操作美团、京东、抖音等40+高频App点外卖、订机票、查房源，单次任务成本约0.2美元——**技术上已能替用户操作OTA App订酒店，但本质是GUI自动化，库存与交易仍在OTA**。来源：https://www.stcn.com/article/detail/3202109.html ；https://cn.chinadaily.com.cn/a/202508/20/WS68a5c096a3104ba1353fde9e.html
30. 【事实】同程是反应最快的OTA：2025年3月7日"程心AI"完成与DeepSeek融合，成为首家全面接入DeepSeek的OTA，开通"AI+实时预订"（App首批10万用户+微信小程序210万用户），实现从AI推荐到预订执行的闭环。2026年6月同程也接入微信AI智能体。来源：http://finance.people.com.cn/n1/2025/0307/c1004-40433518.html ；https://www.163.com/tech/article/KUUC3FEH00098IEO.html
31. 【事实】途牛已上线MCP开放平台；百度心响App（2025年4月）支持MCP Server接入，文心智能体平台与携程等200余家企业合作（宣称日均调用量破1亿次）。来源：https://www.xinstall.com/article/11405 ；https://www.qbitai.com/2025/05/288206.html ；https://www.qbitai.com/2025/04/276913.html
32. 【事实】京东2025年6月18日携"最高三年0佣金"进军酒旅，两天收到近5万家酒店入驻申请；与锦江酒店CRS直连；2026年1月成立京东文旅公司；京东同为微信AI生态首批接入者。**"0佣金订房"的心智已被京东先占。**来源：https://www.21jingji.com/article/20250620/herald/68daac145c620b0270e14ad2debbd77a.html ；https://news.qq.com/rain/a/20260115A061WR00
33. 【媒体推测】知乎行业文章指出"酒店开始反击OTA，因为AI第一次让绕开中间货架变得现实"；Booking在2026年Q1财报中明确要保护直接访问用户、让自家体验不输通用横向Agent——酒店直连与OTA防御的张力在加大。来源：https://zhuanlan.zhihu.com/p/2020824954803890021
34. 【事实】DeepSeek的影响：R1开源后（2025年初）同程/飞猪等旅游平台快速接入，大幅降低OTA做AI的成本门槛，加速了OTA的AI功能上线速度——**DeepSeek实际上缩短了窗口期**。来源：https://www.stcn.com/article/detail/1568833.html ；https://www.ctnews.com.cn/guandian/m/content/2025-04/14/content_172634.html

---

## 关键数据点

| 指标 | 数值 | 年份 | 来源 |
|---|---|---|---|
| 携程2025年研发投入 | 约151亿元（+15%，占营收24%） | 2025 | citnews.com.cn |
| 携程2026Q1产品研发费用 | 41亿元（+15%，占净收入25%） | 2026Q1 | citnews.com.cn |
| TripGenie AI辅助预订同比增速 | +400%（官方口径） | 2025-2026 | facebook.com/Trip.comGroupHotelHub |
| TripGenie酒店比价点击减少 | -80%；7日回访率+45% | 2025 | trip.com newsroom |
| 美团宣称AI投入 | 已达百亿元 | 2025 | 36kr.com |
| 美团LongCat-Flash参数量 | 560B（MoE，开源） | 2025-09 | meituan.com |
| 美团酒旅市占率 | 约13% | 2025 | sohu.com |
| 同程程心AI×DeepSeek首批开放用户 | App 10万 + 微信小程序210万 | 2025-03 | people.com.cn |
| "千问价"合作旅行品牌数 | 40+家（单笔最高减300元） | 2026-02 | sina.com.cn |
| 京东酒旅0佣金政策 | 最高3年0佣金；2天近5万家酒店申请 | 2025-06 | 21jingji.com |
| AutoGLM 2.0单次任务成本 | 约0.2美元；可操作40+App | 2025-08 | stcn.com |
| 微信AI生态首批接入 | 美团/携程/同程/滴滴/京东（内测） | 2026-06 | caixin.com |

---

## 对相关假设的含义

- **H1（OTA被A2A取代而消失）：短中期证据不支持**。当前所有主流C端智能体订酒店都经OTA库存履约（千问→飞猪、微信→携程/美团/同程小程序、AutoGLM→操作OTA App）。OTA正在从"流量入口"退守为"库存+履约+客服层"，入口价值受损但交易地位反而被各家智能体强化。梁建章明言"AI智能体无法取代OTA"。H1若成立也是长期（酒店直连成熟后），而非现在时。
- **H2（OTA不自我革命，留下窗口期）：部分证伪，窗口比假设窄得多**。同程2025年3月即上线AI实时预订、飞猪4月上线问一问并开放AI平台（OpenClaw+Skill）、途牛/携程商旅上线MCP。OTA不仅做了自家AI功能，还主动把库存接入微信/千问/百度等外部智能体。**但真正的残余窗口在：OTA开放对象是超级App而非酒店本身——"酒店以自己身份直连C端智能体（0佣金）"这一层仍无人占据**。
- **H3（微信智能体是重大机会）：已被证实为事实且时间就是现在**。2026年6月微信AI生态开放内测、Q3微信9.0全量。但首批卡位者是携程/美团/同程/京东；且实测表明复杂小程序AI难操作——"智能体友好的酒店直连小程序"确有差异化空间，但接入规则/门槛未公开，单体酒店小程序能否被微信智能体调用是最大未知数。
- **H5（全球首家0手续费A2A订房平台）：定位表述有风险**。京东2025年6月已抢占"0佣金订房"心智；飞猪AI开放平台+ACT协议已抢"agent订房协议/生态"叙事。"首家"须限定为"0佣金+A2A协议+酒店直连"的组合才勉强成立。
- **H6（卡片体系/主动推送）：方向与大厂一致**。千问/高德均以"可视化决策卡片"呈现酒店结果，卡片已成为agent交互的行业共识形态；"千问价"证明酒店愿为AI渠道提供专属价格与权益——数字员工帮酒店管理"AI渠道供给"（定价/权益/卡片）与该趋势契合。

## 证据缺口

1. 携程"口袋参谋"（酒店商家侧工具）的现状与功能未能在本轮搜索中核实。
2. 微信智能体的接入规则、门槛、分成机制未公开；单体酒店/第三方小程序（非首批大厂）能否被调用尚无信息。
3. 未找到OTA明确"拒绝/封锁外部预订agent"的直接报道——该结论基于报道缺失，不能排除非公开的技术性拦截。
4. "千问价"等AI渠道的实际成交量/GMV无公开数据，无法判断AI渠道当前体量。
5. 官网类一手资料（flyai.open.fliggy.com、携程商旅开放平台文档）因环境限制无法抓取正文，开放程度描述依赖搜索摘要与媒体转述。

## 来源列表

1. 甲子光年：携程发布"问道"大模型 https://www.jazzyear.com/article_info.html?id=1053
2. Trip.com Newsroom：TripGenie https://www.trip.com/newsroom/introducing-tripgenie-groundbreaking-ai-travel-assistant/
3. 电商派：Trip.com推出TripGenie https://www.pai.com.cn/223588.html
4. Vocust：携程AI战略深度解读 https://www.vocust.com/school/insightcase/364.html
5. 中文科技资讯：OTA+AI能否让携程同程重估 https://www.citnews.com.cn/news/218457
6. 携程商旅AI开放平台（MCP） https://ct.ctrip.com/thinktanks/235566117077549
7. TTG China：携程商旅"程星途"AI Agent https://ttgchina.com/2025/04/23/携程商旅发布智能助手程星途ai-agent/
8. 亿邦动力：百度搜索开放平台接入携程、同程MCP https://www.ebrun.com/ebrungo/zb/592981.shtml
9. 网易：携程首批接入微信AI生态 https://www.163.com/dy/article/KUU58HKI0534A4SC.html
10. DoNews：携程全面发力AI，梁建章的底层逻辑 https://www.donews.com/article/detail/7963/82082.html
11. ZAKER：AI重做旅游入口：携程守交易，美团抢决策 http://applocal.myzaker.com/news/article.php?pk=69fdc9ea8e9f096d265abe59
12. 腾讯云社区：携程反爬虫 https://cloud.tencent.com/developer/article/1089625
13. 美团官方：LongCat-Flash-Chat开源 https://www.meituan.com/news/NN250901129002898
14. 电商派：美团"小美"公测 https://www.pai.com.cn/p/01k4xrv0x5h2qkzbykqqqhe3da
15. 36氪：美团三个智能助手、AI投入百亿 https://36kr.com/p/3512515121077381
16. 腾讯云：美团龙猫"深度研究"智能体 https://cloud.tencent.com/developer/news/3581595
17. 新浪财经：小美、元宝互通，为微信智能体打样 https://finance.sina.com.cn/jjxw/2026-06-03/doc-iniaavww4314431.shtml
18. IT之家：美团内部限用豆包/千问 https://www.ithome.com/0/971/515.htm
19. 中国民航网：飞猪"问一问"上线 http://caacnews.com.cn/1/6/202504/t20250417_1386642.html
20. 36氪快讯：问一问升级机酒查询 https://36kr.com/newsflashes/3309021344979459
21. 飞猪AI开放平台 https://flyai.open.fliggy.com/
22. 证券时报：千问App全面接入淘宝支付宝高德飞猪 https://www.stcn.com/article/detail/3594486.html
23. 新浪财经：超40家旅行品牌"千问价" https://finance.sina.com.cn/roll/2026-02-11/doc-inhmnaia0395440.shtml
24. 量子位：千问APP联合飞猪推出"千问价" https://www.qbitai.com/2026/02/378498.html
25. 环球旅讯：从"千问价"说起 https://www.traveldaily.cn/article/189339
26. 人人都是产品经理：阿里千问"双重协议"（ACT） https://www.woshipm.com/ai/6327086.html
27. 新华网：高德发布基于地图的AI原生智能体 http://www.news.cn/tech/20250804/ec03c09da157496ebc2b2532a33c6f88/c.html
28. 腾讯新闻：夸克AI超级框 https://news.qq.com/rain/a/20250318A047LO00
29. AITNT：豆包站内直接买团购 https://m.aitntnews.com/newDetail.html?newId=25654
30. 知乎：电商之后是团购，豆包不想只陪用户聊天 https://zhuanlan.zhihu.com/p/2045254455852102910
31. 网易：豆包代预约餐厅翻车（AI幻觉） https://www.163.com/dy/article/KTEQ57N10514EMD3.html
32. 观察者网：豆包、千问将下线智能体功能 https://www.guancha.cn/economy/2026_07_04_822586.shtml
33. 财新：微信智能体将能调取小程序完成交易，首批美团滴滴携程接入内测 https://www.caixin.com/2026-06-09/102452574.html
34. 经济参考网：微信AI生态开放内测，多家旅游出行企业首批接入 http://jjckb.xinhuanet.com/20260610/bd0f9f2d74f34a4dac8f2116278fb665/c.html
35. 网易科技：同程旅行将接入微信AI智能体 https://www.163.com/tech/article/KUUC3FEH00098IEO.html
36. 界面新闻：实测微信AI助手 https://www.jiemian.com/article/14628205.html
37. 《财经》：腾讯正开发微信专属智能体，最高优先级 https://news.caijingmobile.com/article/detail/565179
38. 36氪：微信把超级Agent之战拉进舒适圈 https://36kr.com/p/3718128476664320
39. 观察者网：微信屏蔽腾讯元宝链接 https://www.guancha.cn/economy/2026_02_04_806041.shtml
40. 钛媒体：封了自家元宝，微信AI亲自下场 https://www.tmtpost.com/8014103.html
41. 证券时报：智谱AutoGLM 2.0（Manus撤离后） https://www.stcn.com/article/detail/3202109.html
42. 中国日报网：智谱向公众开放手机智能体 https://cn.chinadaily.com.cn/a/202508/20/WS68a5c096a3104ba1353fde9e.html
43. 人民网：程心AI完成与DeepSeek融合，210万用户可体验 http://finance.people.com.cn/n1/2025/0307/c1004-40433518.html
44. 证券时报：同程、飞猪接入DeepSeek https://www.stcn.com/article/detail/1568833.html
45. 21经济网：京东三年0佣金强攻酒旅 https://www.21jingji.com/article/20250620/herald/68daac145c620b0270e14ad2debbd77a.html
46. 腾讯新闻：京东成立文旅公司 https://news.qq.com/rain/a/20260115A061WR00
47. Xinstall：途牛上线MCP开放平台 https://www.xinstall.com/article/11405
48. 量子位：百度心响上线 https://www.qbitai.com/2025/05/288206.html
49. 量子位：百度Create文心智能体论坛（携程等200+企业） https://www.qbitai.com/2025/04/276913.html
50. 知乎：酒店为什么开始反击OTA https://zhuanlan.zhihu.com/p/2020824954803890021
51. 扣子Coze文档：端插件 https://docs.coze.cn/guides_use_local_plugin
52. 搜狐：京东做文旅能成下一个OTA吗（抖音酒旅GMV/美团市占） https://www.sohu.com/a/978948258_104421
