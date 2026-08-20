# 30-供应商调研：开放API摄像头与视觉AI方案（公共区域非人脸分析）

- 调研日期：2026-08-12（信息以搜索引擎索引摘要为准，环境限制无法直接抓取官网原文）
- 调研目标：为 2 店 POC（公共区域摄像头几路）+ 45 店满配（约百路级）选型"开放API/本地可接管"的摄像头与视觉分析方案
- 红线约束：客房内禁装摄像头；人脸识别不作方案核心；只做公共区域非人脸的行为/状态分析（保洁验收、客流、异常滞留）
- 筛选标准：①RTSP/ONVIF 或开放API可被桌面引擎统一接管 ②小批量友好 ③经济型价格带 ④深圳/大湾区可实地拜访优先

---

## 一、概述与核心判断

1. **技术路线判断（本次调研最重要结论）**：满足"隐私合规 + 成本最低 + 桌面引擎统一接管"三个条件的架构是——
   **标准协议 IPC（ONVIF/RTSP，100~300元/路）→ 店内本地分析层（店内电脑 GPU 或 RK3588 边缘盒子）→ 结果事件推给桌面智能体**。
   视频流不出店，只上传结构化事件（如"1508房保洁验收不合格：垃圾桶未清"），天然规避隐私与合规风险。云API路线（萤石云/涂鸦）反而有持续订阅费+视频出店合规暴露，仅适合做补充。

2. **"保洁合格/不合格"自定义模型部署在哪层最省**：
   - **摄像头端**：需买各家 AI 相机+其训练平台绑定（海康AI开放平台模式），单路成本高（AI相机千元级），且被单一厂商生态锁定，POC 阶段不划算；
   - **边缘盒子**：RK3588 盒子约 2500 元可分析 8 路，摊到每路约 300 元，本地推理、可跑自训 YOLO 类模型，45 店规模最省【确认，价格见下】；
   - **店内电脑 GPU**：POC 阶段最省（0 增量硬件，桌面智能体本来就装在店内电脑上），2 店试点建议直接用店内电脑跑推理，验证算法后再决定是否加盒子。
   → **建议：POC 用"白牌/VIGI 标准 IPC + 店内电脑推理"，满配阶段按店加 RK3588 盒子。**

3. **每路成本量级（硬件一次性）**：标准 IPC 100~300 元/路 + 边缘算力摊销 0~300 元/路 ≈ **150~600 元/路**；对比海康双目客流专用相机 4500~8000 元/套、云API年费路线（萤石企业套餐 E1 起步+按量计费），差一个数量级。

4. **深圳可实地拜访名单（本周行程可安排）**：TP-LINK（总部深圳）、同为股份 TVT（深圳上市公司）、Reolink 睿联（深圳）、英码科技（深圳）、共达地（深圳）、极视角（深圳注册）、爱莫科技（深圳南山）、金亚太 Geniatech/启朔/触觉智能/米尔（均深圳）；华强北可现场看白牌 IPC 模组（雄迈/安佳等方案）。

---

## 二、公司清单总表

| # | 公司/平台 | 类别 | 开放性 | 价格量级 | 地点 | 经营状态 |
|---|---|---|---|---|---|---|
| 1 | TP-LINK VIGI | 商用IPC | 全系RTSP+ONVIF S/G/T，官方FAQ明示对第三方开放 | IPC约100~300元/路 | **深圳总部** | 确认在营 |
| 2 | 海康威视开放平台/AI开放平台 | IPC+训练平台 | 设备SDK/ISAPI/RTSP/ONVIF开放；AI开放平台可自训模型下发自家AI相机 | 普通款智能相机200~500元；AI相机千元级；平台商用授权待核实 | 杭州（深圳有分支机构） | 确认在营 |
| 3 | 萤石云开放平台（海康子品牌） | 消费IPC+云API | 云API按量计费；本地RTSP可手动开启，**无ONVIF** | 相机100~300元；企业套餐E1起步、按量后付费 | 杭州 | 确认在营 |
| 4 | 大华/乐橙imou开放平台 | IPC+云平台 | 设备SDK/ONVIF/GB28181开放；乐橙云API；巨灵平台自训算法 | 与海康同档 | 杭州 | 确认在营 |
| 5 | 宇视 Uniview | 商用IPC | SDK/ONVIF开放，第三方平台普遍已适配 | 与海康同档略低 | 杭州 | 确认在营 |
| 6 | 涂鸦智能 IPC 生态 | 云API聚合 | 云OpenAPI统一但**按设备+流媒体服务收费**；本地RTSP普遍不开放 | 相机几十~200元；云服务按UUID计费 | 杭州（深圳有办公室，待核实） | 确认在营 |
| 7 | Reolink 睿联技术 | 消费/商用IPC | PoE款支持CGI/RTSP/ONVIF | 200~500元/路（零售价） | **深圳** | 确认在营 |
| 8 | 同为股份 TVT | 商用IPC/NVR | ONVIF/国标/API+SDK，OEM能力强 | 待核实（行业中档） | **深圳**（深交所上市） | 确认在营 |
| 9 | 白牌IPC模组（雄迈/天视通/安佳等） | 白牌底座 | 模组默认开ONVIF/RTSP/GB28181 | 模组几十元级，整机约50~150元 | 杭州为主，**深圳华强北渠道现货** | 确认在营 |
| 10 | 英码科技 EMA | 边缘AI盒子 | 海思/瑞芯微/算能多平台盒子+算法移植全链条服务 | RV1126轻量款低价、RK/算能款千元~数千元 | **深圳** | 确认在营 |
| 11 | RK3588盒子厂商群（金亚太/启朔/金海创/触觉智能/米尔） | 边缘AI盒子 | 标准Linux+NPU，可跑自训模型，接RTSP流 | 6TOPS/8路分析约2499元起 | **深圳** | 确认在营 |
| 12 | 算能 SOPHGO（SE5/BM1684） | 边缘AI盒子 | 开放工具链，16路视频分析 | BM1684整机约3599元起 | 北京（深圳有生态伙伴） | 确认在营 |
| 13 | 共达地 GDDi | AutoML自训平台 | 0代码训练自定义模型，适配近百款云边端芯片一键下发 | POC约3天/落地1周；报价待核实 | **深圳** | 待核实（融资信息为2021-2022年） |
| 14 | 极视角 | 算法商城 | 1500+算法，按路/按服务器/按年授权 | 部分算法低至几百元 | **深圳**注册 | 待核实（近两年动态少） |
| 15 | 爱莫科技 | 定制视觉AI | 定制算法+终端+系统全栈，门店场景数据强 | 定制报价待核实 | **深圳南山** | 确认在营（2025年仍有对比文提及） |

（对照参考，不入清单：悠络客/万店掌——连锁门店视频巡检 SaaS，客流+巡店成熟但为封闭 SaaS 生态，不符合"桌面引擎统一接管"标准，可作为功能对标与价格锚点。）

---

## 三、每家详情

### 1. TP-LINK VIGI【确认在营｜深圳总部｜首选POC底座】
- **为什么重要**：官方 FAQ 明确"TP-LINK IPC 均支持标准 RTSP 协议，可在第三方网站/平台/客户端取流"，并支持 ONVIF Profile S/G/T 接入第三方 NVR/软件——是大厂里对第三方最开放、文档最直白的。商用 VIGI 线价格贴近消费级，渠道现货、单只起买，完美匹配"小批量友好"。总部在深圳，本周可约。
- **开放API**：RTSP（默认可用）+ ONVIF（设置中开启，默认端口80）；无强制云绑定【确认】。
- **价格**：主流 200万/400万 商用枪机/半球零售约 100~300 元/路（渠道常识，具体型号待现场核价）【待核实】。
- **红线适配**：取 RTSP 流在店内本地分析，视频不出店，合规最优。
- **来源**：TP-LINK 官方FAQ RTSP取流 https://security.tp-link.com.cn/service/detail_article_4432.html ；双目机RTSP取流 https://security.tp-link.com.cn/service/detail_article_4729.html ；ONVIF第三方接入 https://www.tp-link.com/us/support/faq/4201/
- **联系线索**：官网 security.tp-link.com.cn（服务与支持页有400电话入口）；总部深圳南山。

### 2. 海康威视 开放平台 + AI开放平台【确认在营｜杭州总部】
- **开放性**：open.hikvision.com 提供设备 API/SDK/OTAP/HEOP 等接入能力，设备侧 SDK/ISAPI 免费下载；全系支持 RTSP/ONVIF（行业标准配置）【确认】。AI开放平台（ai.hikvision.com）提供"预训练大模型+场景微调"零代码训练，**自训模型（如"保洁合格/不合格"）可自动化下发到海康全系 AI 相机/超脑NVR 边缘部署，也可云端API发布或私有化部署**【确认，训练启动数据量降90%的官方宣传】。
- **非人脸智能**：3系列普通款已带"智能警戒lite"（区域入侵/越界/徘徊/物品遗留等），无需另付费【确认】——公共区域"异常滞留"可用现成功能覆盖。
- **价格**：普通智能款 200~500 元/路；AI开放平台训练本身有免费额度、**商用授权与装载费待核实**；双目客流专用相机 4500~8000 元/套（客流场景没必要上专用机）。
- **风险**：生态强但"统一接管"意愿弱，自训模型绑定海康 AI 相机（千元级），POC 性价比一般；适合满配阶段做备选。
- **来源**：https://open.hikvision.com/ ；https://ai.hikvision.com/ ；AI开放平台训练与部署介绍 https://blog.csdn.net/qq_53751953/article/details/136417842 ；智能警戒lite与订阅式"智能检测"服务 http://m.cps.com.cn/index.php?m=Index&a=show&id=942507 ；客流相机价格区间 https://www.getic.com/product/hikvision-dual-lens-people-counting-camera-ds-2cd6825g0-c-ivs
- **联系线索**：open.hikvision.com 官网合作入口；深圳有分公司（渠道遍布华强北）。

### 3. 萤石云开放平台（EZVIZ，海康消费子品牌）【确认在营｜杭州】
- **开放性**：云 API 体系完整（open.ys7.com），但**设备默认不开 RTSP，需在 App 内逐台手动开启本地服务；不支持 ONVIF**【确认】。云端取流（RTMP）需关闭码流加密走萤石云。
- **价格**：企业版按套餐+按量后付费（E1 套餐起步，商用前需预充值）；消息业务免费；平台定制套餐门槛为设备量>2000台或带宽>100M【确认，来自社区/官网价格页摘要】。相机整机 100~300 元。
- **判断**：相机便宜但"云优先"架构与我们"本地接管"的诉求相反，逐台手动开 RTSP 在 45 店运维上是负担；仅当需要远程回看/云存储时做补充。
- **来源**：价格页 https://open.ys7.com/cn/s/price ；收费明细（社区）https://ezsuperfans.com/portal.php?mod=view&aid=410 ；收费标准解读 https://blog.csdn.net/hq123897/article/details/144448928 ；RTSP需手动开启 https://blog.csdn.net/u013008898/article/details/136801061 ；无ONVIF、有RTSP(554) https://wp.gxnas.com/1451.html
- **联系线索**：官网 open.ys7.com；公开商务邮箱 open-team@ezvizlife.com（来自搜索摘要）。

### 4. 大华 / 乐橙 imou 开放平台 + 巨灵AI平台【确认在营｜杭州】
- **开放性**：大华设备 SDK 免费、全系 ONVIF/RTSP/GB28181【确认】；乐橙云开放平台（open.imou.com / open.lechange.com）支持大华、海康、宇视等经 GB28181 接入做设备管理与音视频分发【确认】。巨灵AI平台支持无代码自训算法、一键跨端部署（对标海康AI开放平台）【确认，官方宣传】。
- **价格**：整机与海康同档；乐橙云 API 收费标准未在索引中查到【待核实】；设备侧本地路线免费。
- **非人脸智能**：大华相机内置绊线/区域入侵/物品遗留/徘徊/人员聚集等智能事件【确认】。
- **来源**：https://open.imou.com/ ；https://open.lechange.com/ ；GB28181接入说明 https://blog.csdn.net/weixin_44117635/article/details/118632019 ；巨灵平台 https://www.thepaper.cn/newsDetail_forward_13346313 ；智能事件清单 https://www.hhikvision.com/news/7978.html
- **联系线索**：open.imou.com 官网；深圳有大华分支渠道。

### 5. 宇视 Uniview【确认在营｜杭州】
- **开放性**：官网提供网络设备 SDK（Windows/Linux）下载做二次开发；EasyCVR 等第三方平台已适配宇视 SDK/ONVIF，接入成熟【确认】。
- **价格**：行业第三名，价格通常略低于海康/大华同档【待核实】。
- **判断**：作为标准协议 IPC 供应来源之一即可，无独特开放优势；总部杭州，深圳行程优先级低。
- **来源**：SDK获取方式 https://blog.csdn.net/Uniview400/article/details/123481941 ；EasyCVR适配宇视SDK https://www.cnblogs.com/easycvr/p/17928851.html
- **联系线索**：官网 www.uniview.com（SDK下载入口）。

### 6. 涂鸦智能 IPC 生态【确认在营｜杭州】
- **开放性**：云 OpenAPI 统一、IPC 零代码开发/SDK 齐全【确认】；但 **IPC 视频流媒体服务按激活设备（UUID/DeviceID）收费，云平台按套餐+超量计费**【确认，官方帮助中心】；涂鸦生态相机普遍**不开放本地 RTSP**（云优先架构，搜索未见官方本地取流文档）【待核实但方向明确】。
- **判断**：与智能按钮同一生态是诱惑（一朵云管全部），但对摄像头这条线，"每台每年云费+视频出店"与我们红线/成本都冲突。**按钮走涂鸦、摄像头走本地 RTSP，两条线分开**是更优解。
- **来源**：IPC流媒体收费 https://support.tuya.com/zh/help/_detail/K8sdygc22xb31 ；产品定价 https://developer.tuya.com/cn/docs/iot/membership-service?id=K9m8k45jwvg9j ；IPC开发包 https://developer.tuya.com/cn/ipc-sdk
- **联系线索**：developer.tuya.com；涂鸦深圳有办公点（待核实，可与按钮调研一并确认）。

### 7. Reolink 睿联技术【确认在营｜深圳】
- **开放性**：官方支持文档明确大部分 PoE 有线款支持 CGI/RTSP/ONVIF（ONVIF端口8000/RTSP端口554）；少数入门Wi-Fi款（E1系列）需搭配Hub才有RTSP、4G款不支持【确认】。
- **价格**：零售 200~500 元/路；做外贸消费市场为主，国内渠道弱【待核实】。
- **判断**：深圳本土、协议开放、单只可买，适合 POC 快速凑设备；但商用交付/对公渠道不如 TP-LINK 顺。
- **来源**：官方协议支持清单 https://support.reolink.com/articles/900000617826-Which-Reolink-Products-Support-CGI-RTSP-ONVIF/ ；RTSP/ONVIF设置 https://www.smartrtsp.com/cameras/reolink
- **联系线索**：reolink.com 官网；总部深圳（具体对公渠道现场核实）。

### 8. 同为股份 TVT【确认在营｜深圳，深交所上市】
- **开放性**：产品支持国标协议、ONVIF，兼容主流厂家后台，**提供 API 和 SDK 供第三方扩展**【确认，官网表述】；2004年成立、2016年上市，以海外 OEM/ODM 见长。
- **价格**：行业中档【待核实】；OEM 基因意味着小批量定制议价空间可谈。
- **判断**：深圳可拜访的"正规军"IPC 厂，若想要"白牌价格+上市公司供货资质"，TVT 是华强北模组与一线大厂之间的折中选项。
- **来源**：官网产品页 https://cn.tvt.net.cn/products/1527.html ；公司介绍 http://tvt.corp.dav01.com/index.html
- **联系线索**：官网 cn.tvt.net.cn（联系我们页）；深圳总部。

### 9. 白牌 IPC 模组（雄迈 / 天视通 / 中维 / 安佳等）【确认在营｜杭州为主，深圳华强北渠道现货】
- **开放性**：市场主流模组厂为雄迈、中维世纪、天视通、安佳等；**雄迈方案模组默认开启 ONVIF**，各家普遍支持 ONVIF/RTSP/GB28181【确认】。这是"自建本地分析底座"最便宜的物理层。
- **价格**：1688 上模组几十元级，整机（含镜头/外壳/电源）约 50~150 元【确认量级，1688索引】。
- **风险**：品控参差、固件安全（雄迈曾有海外安全通报历史）、无对公售后；45 店满配需锁定一家有质保的组装厂而非散货。
- **判断**：POC 阶段买 5~10 只试穿透（RTSP稳定性/断流重连），若稳定则满配时按整机 100 元/路极限压成本；董事长在华强北安防市场半天可看完所有方案。
- **来源**：模组厂家格局 https://ipc.name/name/module/ ；雄迈模组批发 https://s.1688.com/kq/-D0DBC2F5C4A3D7E9.html ；ONVIF开启方法 https://www.ruodian360.com/tech/security-monitoring/38236.html
- **联系线索**：1688/华强北安防市场现场；无单一官网。

### 10. 英码科技 EMA【确认在营｜深圳】
- **开放性**：2006年成立，边缘计算盒子覆盖海思/瑞芯微/算能多平台（RV1126轻量款、IVP03X算能款、IVP09A海思鸿蒙款等），**提供算法训练、算法移植、硬件集成到对接业务平台的全链条闭环服务**【确认，官网】——正是"把我们自训的保洁模型移植上盒子"需要的服务商。
- **价格**：RV1126 轻量款主打"超高性价比"（适合 1~2 路轻场景）；RK/算能款千元~数千元【待核实具体报价】。
- **来源**：官网 https://www.ema-tech.com/ ；RV1126盒子 https://www.ema-tech.com/NewsDetail/3374975.html ；IVP03E(BM1688) https://www.ema-tech.com/NewsDetail/4905043.html
- **联系线索**：官网 ema-tech.com（联系方式页）；深圳可拜访。

### 11. RK3588 边缘盒子厂商群（金亚太 Geniatech / 启朔 / 金海创 / 触觉智能 / 米尔）【确认在营｜均深圳】
- **开放性**：RK3588 = 6TOPS NPU + 标准 Linux，生态开放（RKNN 工具链），接 RTSP 流跑自训 YOLO 类模型无授权费；一盒管 8 路 1080p 分析【确认】。
- **价格**：**6TOPS/8路分析款约 2499 元起**（百度AI市场行情），摊每路约 300 元【确认量级】；飞凌 RK3588J 工业款支持 16 路（保定，非深圳）。
- **厂商**：金亚太 Geniatech（1997年成立，深圳，APC3588）；启朔科技（深圳，6T~48T产品线）；金海创（深圳）；触觉智能（2012年成立，深圳，核心板/工控）；米尔电子（深圳，核心板）。
- **判断**：45 店满配时每店一盒（2500元×45≈11万）超预算，实际可先用店内电脑GPU，仅高负载店加盒；或选 RV1126/RK3576 低配款（几百元级）做 2~4 路。
- **来源**：RK3588盒子行情 https://aim.baidu.com/product/35c00a6a-283b-4314-976c-01f42d51c8d2 ；价格分析 https://www.iotdt.com/news/chanpingxunxi/671.html ；金亚太 https://www.geniatech.cn/product/apc3588/ ；启朔 https://www.cheersucloud.com/products/2814/10.html ；触觉智能 https://www.industio.cn/ ；米尔 https://www.myir.cn/
- **联系线索**：各官网；均在深圳。

### 12. 算能 SOPHGO（SE5 / BM1684）【确认在营｜北京总部】
- **开放性**：开放工具链，SE5 微服务器支持 16 路视频流分析（17.6TOPS）【确认】；深圳有英码等生态集成商可代交付。
- **价格**：BM1684 16路整机约 3599 元起【确认量级，百度AI市场】。
- **判断**：单店不需要 16 路，优先级低于 RK3588；列为满配阶段集中式方案（如总部集中分析）备选。
- **来源**：SE5行情 https://aim.baidu.com/product/937c34b2-ce9e-4724-928a-b4bce78c8402 ；SE5评测 https://www.asmag.com.cn/test/202006/70793.html
- **联系线索**：sophgo.com 官网；或经深圳英码科技。

### 13. 共达地 GDDi【待核实经营状态｜深圳】
- **开放性**：2020年成立于深圳，AutoML 0代码自训练平台——三步训练自定义视觉算法，**提前适配10+品牌近百款云边端AI芯片，一键下发部署**；官方宣称新行业算法 POC 仅 3 天、落地 1 周【确认为官方宣传口径】。
- **与我们的匹配点**："保洁合格/不合格"正是碎片化长尾算法，共达地的商业模式就是为此设计；训练出的模型可下发到 RK3588 盒子/店内电脑，不锁定相机品牌。
- **风险**：公开融资/新闻集中在 2021-2022 年，**2024-2026 年经营动态未在索引中查到，见面前必须核实存续状态**（硬件/AI创业公司死亡率高）。
- **来源**：官网应用页 https://application.gddi.com.cn/index.html ；36氪融资报道 https://36kr.com/p/1775889698884229 ；CSDN发布会报道 https://www.csdn.net/article/2021-12-31/122258070
- **联系线索**：官网 gddi.com.cn；深圳（具体地址官网核实）。

### 14. 极视角【待核实经营状态｜深圳注册】
- **开放性**：算法商城 1500+ 算法（离岗/摔倒/抽烟/反光衣等行为识别现货），**按路数/按服务器/按年包三种授权**，可搭配其推理平台部署【确认】。
- **价格**：部分算法低至几百元【确认，官方交付说明】——"垃圾/杂物检测""物品遗留"这类现货算法可能几百到几千元买断每路授权，比自训更快。
- **风险**：公开报道多为 2019-2023 年，近两年动态少，**经营状态待见面核实**。
- **来源**：算法商城 https://www.extremevision.com.cn/marketplace/ ；购买交付方式 https://www.extremevision.com.cn/news/372.html ；北大创新创业介绍 https://sie.pku.edu.cn/yxal/xmtd/eb0ce23631a048518dcd3af36f040ab4.htm
- **联系线索**：官网 extremevision.com.cn。

### 15. 爱莫科技【确认在营｜深圳南山】
- **开放性**：2018年成立，定制 AI 全栈（算法+AI终端+系统），零售门店场景数据 300万+ 门店、20万+ 商品图谱；有"一拍即核"（拍照即验收）产品形态——**与"保洁拍照/摄像头验收"场景高度同构**；有智能人体分析做实时客流（非人脸路线可谈）【确认】。2025 年行业对比文章仍将其与万店掌/悠络客并列，经营状态较新。
- **价格**：定制路线，报价待核实；客户以大品牌为主，小单议价能力待验证。
- **来源**：官网 https://www.mall-ai.com/about ；36氪A+轮 https://www.36kr.com/p/1508310136803072 ；行业对比 https://gitcode.csdn.net/69eb480c54b52172bc6fcb05.html
- **联系线索**：官网 mall-ai.com；深圳市南山区国际创新谷（官网自述）。

### 对照参考：悠络客 / 万店掌（不入采购清单）
- 连锁门店"云值守/AI巡店"SaaS 双雄（悠络客上海、万店掌苏州），客流分析、远程巡店、违规识别成熟，签约门店百万级【确认】。但均为封闭 SaaS（自有相机+自有云），与"桌面引擎统一接管+本地分析"路线冲突；**价值在于做功能对标和给保洁验收场景定价锚点**（可要一份公开报价单）。
- 来源：https://www.ulucu.com/news/official/ulucu-BusinessIntelligencePlatform ；https://www.wistore.net/ ；对比文 https://gitcode.csdn.net/69eb480c54b52172bc6fcb05.html

---

## 四、关键问题结论

1. **RTSP/ONVIF 开放性 vs 云API收费**：TP-LINK VIGI / 大华 / 海康 / 宇视 / TVT / Reolink(PoE款) / 白牌模组 → 本地协议全开、零持续费用；萤石（RTSP可开但无ONVIF、云API按量计费）与涂鸦（云优先、按设备收流媒体费）为云绑定路线，与本地接管诉求冲突。**结论：底座选"标准协议阵营"。**
2. **自定义模型部署层**：POC 在店内电脑 GPU（零增量成本）→ 满配视负载加 RK3588 盒（约300元/路摊销）→ 相机端部署（海康AI相机路线）留作大规模阶段选项。训练侧：先问极视角有无现货算法（几百元级），没有再用共达地/海康AI开放平台自训，最后才是爱莫定制。
3. **非人脸行为分析谁开放且便宜**：海康/大华普通款相机已内置徘徊/滞留/物品遗留/区域入侵等智能事件（无附加费，事件可经 ONVIF/SDK 上报）——"异常滞留"场景可能零算法成本解决；"保洁验收"才需要自训模型。
4. **每路成本量级**：硬件一次性 150~600 元/路（白牌底座可压到 100 元内）；专用客流相机 4500~8000 元/套不推荐；云路线另有持续年费。

## 五、证据缺口（见面必问清单见结构化输出）

1. 萤石/乐橙/涂鸦云 API 的**精确价目**（每路每年多少钱）未在索引中获得，需官网价格页或商务确认。
2. 共达地、极视角 **2024-2026 年经营状态**未获公开佐证，见面前先电话/工商核实。
3. 海康 AI 开放平台**自训模型商用授权费与装载费**（免费额度之外）未查到。
4. 白牌模组整机在**7×24 连续 RTSP 拉流下的稳定性**无公开数据，只能实测。
5. TP-LINK VIGI / TVT / Reolink 的**对公小批量报价**（10~100 只档）需现场询价。

## 六、来源列表（全部）

- TP-LINK RTSP/ONVIF 官方FAQ：https://security.tp-link.com.cn/service/detail_article_4432.html / https://security.tp-link.com.cn/service/detail_article_4729.html / https://www.tp-link.com/us/support/faq/4201/ / https://www.tp-link.com/us/support/faq/5054/
- 海康开放平台：https://open.hikvision.com/ ；AI开放平台：https://ai.hikvision.com/ ；训练部署解读：https://blog.csdn.net/qq_53751953/article/details/136417842 ；智能警戒lite：http://m.cps.com.cn/index.php?m=Index&a=show&id=942507 ；客流相机：https://www.getic.com/product/hikvision-dual-lens-people-counting-camera-ds-2cd6825g0-c-ivs
- 萤石价格：https://open.ys7.com/cn/s/price / https://ezsuperfans.com/portal.php?mod=view&aid=410 / https://blog.csdn.net/hq123897/article/details/144448928 ；萤石RTSP：https://blog.csdn.net/u013008898/article/details/136801061 / https://wp.gxnas.com/1451.html
- 乐橙/大华：https://open.imou.com/ / https://open.lechange.com/ / https://blog.csdn.net/weixin_44117635/article/details/118632019 ；巨灵：https://www.thepaper.cn/newsDetail_forward_13346313 ；大华智能事件：https://www.hhikvision.com/news/7978.html
- 宇视SDK：https://blog.csdn.net/Uniview400/article/details/123481941 / https://www.cnblogs.com/easycvr/p/17928851.html
- 涂鸦：https://support.tuya.com/zh/help/_detail/K8sdygc22xb31 / https://developer.tuya.com/cn/docs/iot/membership-service?id=K9m8k45jwvg9j / https://developer.tuya.com/cn/ipc-sdk
- Reolink：https://support.reolink.com/articles/900000617826-Which-Reolink-Products-Support-CGI-RTSP-ONVIF/ / https://www.smartrtsp.com/cameras/reolink
- 同为TVT：https://cn.tvt.net.cn/products/1527.html / http://tvt.corp.dav01.com/index.html
- 白牌模组：https://ipc.name/name/module/ / https://s.1688.com/kq/-D0DBC2F5C4A3D7E9.html / https://www.ruodian360.com/tech/security-monitoring/38236.html
- 英码科技：https://www.ema-tech.com/ / https://www.ema-tech.com/NewsDetail/3374975.html / https://www.ema-tech.com/NewsDetail/4905043.html
- RK3588盒子：https://aim.baidu.com/product/35c00a6a-283b-4314-976c-01f42d51c8d2 / https://www.iotdt.com/news/chanpingxunxi/671.html / https://www.geniatech.cn/product/apc3588/ / https://www.forlinx.com/product/199.html / https://www.cheersucloud.com/products/2814/10.html / https://www.industio.cn/ / https://www.myir.cn/
- 算能SE5：https://aim.baidu.com/product/937c34b2-ce9e-4724-928a-b4bce78c8402 / https://www.asmag.com.cn/test/202006/70793.html
- 共达地：https://application.gddi.com.cn/index.html / https://36kr.com/p/1775889698884229 / https://www.csdn.net/article/2021-12-31/122258070
- 极视角：https://www.extremevision.com.cn/marketplace/ / https://www.extremevision.com.cn/news/372.html / https://sie.pku.edu.cn/yxal/xmtd/eb0ce23631a048518dcd3af36f040ab4.htm
- 爱莫科技：https://www.mall-ai.com/about / https://www.36kr.com/p/1508310136803072 / https://gitcode.csdn.net/69eb480c54b52172bc6fcb05.html
- 悠络客/万店掌：https://www.ulucu.com/news/official/ulucu-BusinessIntelligencePlatform / https://www.wistore.net/
- 保洁AI验收案例：https://m.leiphone.com/category/aijuejinzhi/lVDROhetxzqIPFFe.html ；客流双目方案商：https://www.sunpn-iot.com/list_64
