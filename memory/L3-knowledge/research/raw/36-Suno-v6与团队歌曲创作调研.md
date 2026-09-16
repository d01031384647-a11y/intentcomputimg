# 36 · Suno v6 与团队歌曲创作调研（2026-09-16）

## 调研目的、方法与置信度说明

- **目的**：为住小叮团队歌重做三首（上一首《一路同心》2026-08-26 由 Suno 生成，老板"觉得不错但要优化"）提供决策依据：①Suno 最新模型（v6）现状；②简单模式 vs 高级模式如何选；③高级模式提示词写法；④中文普通话歌词的经验与坑；⑤企业/团队歌创作要点；⑥商用与版权。
- **方法**：六个角度并行检索（v6 事实、模式对比、提示词工程、中文生成、团队歌创作、商用版权）+ 每个角度 1–3 轮"怀疑者"独立复核 + 评论员找缺口 + 5 项定向补查。全程仅 WebSearch（WebFetch/curl 被环境禁止），所有事实来自搜索结果条目的摘要，未读取网页全文。
- **置信度说明**：
  - v6-facts 角度获得 3 轮有配额的独立复核（共 70 次检索），结论最可靠；modes / prompting / chinese / anthem-craft / licensing 五个角度的复核以及 5 项补查因会话搜索配额耗尽（200/200）**未能执行独立检索**，其判决仅为来源结构审计 + 模型既有知识（截止 2026-06），不应视为独立确认。
  - 标注规则：**[官方]** = suno.com / help.suno.com / @suno 原文；**[媒体]** = TechCrunch、Variety、MBW、DMN 等；**[第三方]** = jackrighteous、hookgenius、roo.beehiiv、undetectr、kie.ai、unifically 等教程站/API 转售商；**[社区]** = Reddit、知乎、CSDN、B 站等；**[推断]** = 本报告把事实映射到本项目的推论，置信度 low。
  - 来源集中度风险：v6 高级模式 UI 细节（滑杆默认值、Variety 档位、Duration 范围）几乎全部来自 jackrighteous / hookgenius / GitHub issue #562 三处 2026-09-09~12 的观察，发布一周内可能已被热修复改动，**以股东实际打开 Create 页面为准**。

## 一、Suno v6 现状

### 1.1 已确认（多源一致，含官方）

- **发布**：2026-09-09 正式发布，官方博客《Introducing v6》https://suno.com/blog/introducing-v6 、Release Notes https://suno.com/release-notes/introducing-v6 、帮助中心 v6 FAQ https://help.suno.com/en/articles/13924481 、《Current Models: v6》https://help.suno.com/en/articles/13924737 、《What's new in v6?》https://help.suno.com/en/articles/13924801 、官方 X 推文 https://x.com/suno/status/2097714273942163823 （原文 "Welcome to the v6 era. Our best models yet, built in partnership with artists and producers."）。同日媒体：TechCrunch https://techcrunch.com/2026/09/09/suno-replaces-its-ai-models-with-a-new-one-trained-on-licensed-music-as-copyright-suits-pile-up/ 、Variety https://variety.com/2026/music/news/suno-new-label-backed-model-v6-1236855351/ 、DMN https://www.digitalmusicnews.com/2026/09/09/suno-v6-launch/ 、Music Ally https://musically.com/2026/09/09/suno-launches-its-v6-ai-music-models-heres-what-you-need-to-know/ 、腾讯新闻 https://news.qq.com/rain/a/20260909A0DXKT00 、IT之家 https://www.ithome.com/1/000/351.htm 。
- **三模型家族**：v6（旗舰，"reliable, precise… follows detailed instructions better than any previous Suno model"[官方 13924737]）、v6-wild（"less predictable and more varied"）、v6-mini（"faster, more efficient version available to everyone"）。v6 与 v6-wild 仅 Pro/Premier；v6-mini 对含免费在内所有用户开放。
- **旧模型退役**：官方措辞 "As v6 rolls out, we will retire our previous models and move Suno entirely onto the v6 generation"；第三方实测 9 月 9 日当天 v4/v4.5/v5/v5.5 全部从模型选择器移除 https://hookgenius.app/learn/what-happened-to-suno-v5/ 。旧歌保留在库中可听、分享、Remaster、Cover，但"any new iterations will be made with our latest models"[官方 FAQ，经 https://heho.ai/blog/suno-retired-older-models-your-songs 转述]；用户自训 Custom Models 自动升级为 v6 驱动。
- **训练数据（修正后表述）**：与 Warner Music Group、BMG、Believe 合作；Suno 称 v6 未使用训练旧版本所用的音乐（TechCrunch），且不含 UMG/Sony 数据；CPO Jack Brody 原话是 "a combination of data that's been licensed from these partners, user data（用户偏好数据）, but most importantly… the accumulation of the team's learnings… and other technical breakthroughs and R&D" https://imusician.pro/en/resources/blog/suno-v6-licensed-ai-music-models 。**不是**"仅基于授权目录从头训练"。艺人/词曲作者分享 Suno 200 万+付费订户收入（该订户数首次公布于 2026-02-26，https://www.musicbusinessworldwide.com/suno-hits-2m-paid-subscribers-300m-annual-revenue/ ），分成先付给厂牌、再由厂牌分配。
- **官方新功能**：自然语言分段编辑（只改某一段）；单词/单句歌词修改不重做整曲；多源 Mashup；采样/分离；多模态输入（文字、音频、图片、视频、语音备忘录）；单次生成最长 8 分钟；**Max Mode**（"Uses more compute to maximize consistency throughout the song. Costs 2x credits per song"，官方建议用于 >2 分钟的歌、想贴近原曲的 Cover、风格迁移、全曲人声/风格一致性）[官方 FAQ 13924481]。
- **Variety（高级模式新增）**：官方 FAQ 原文 "The Variety slider is designed to introduce variety in your outputs by adjusting and updating your style prompts… If you'd like to retain full control of your style tags, reduce the Variety slider to 0"。第三方 UI 观察：五档离散 Off "Exact style" → Normal "Balanced variety" → High "Distinct styles" → Extra "Bold exploration" → Max "Unreasonably varied"；v6 与 v6-mini 默认 Normal，v6-wild 默认 Off；改写后的风格提示词"更短更弱" https://github.com/bitwize-music-studio/claude-ai-music-skills/issues/562 、https://undetectr.com/blog/suno-v6-changing-your-prompt 。
- **积分**：任何模式点一次 Create 出 2 首共 10 积分，三模型同价，"v6 song generations have the same credit cost as previous models"[官方 FAQ]；Max Mode 20 积分/次。发布期促销（付费用户 v6/v6-wild 零积分）窗口 2026-09-10 开启、至 09-12 结束，**今日已过期** https://roo.beehiiv.com/p/suno-v6-free-48-hours-paid-plan 。
- **chirp 引擎代号与版本对应**（社区/API 转售商共识，Suno 官方从未公开）：v4.5 = chirp-auk（2025-05-03）、v4.5+ = chirp-bluejay（2025-07-17）、v5 = chirp-crow（2025-09-23）、**v5.5 = chirp-fenix（2026-03-26 发布）**、v6 家族 = chirp-hawk / chirp-hawk-wild / chirp-goose（v6-mini）。来源 https://unifically.com/blogs/suno 、https://www.cometapi.com/suno-v5-5-what-is-new-and-how-to-use-it-via-api--studio/ 、https://sunoaiwiki.com/news/2025/09-25-suno-v5-chirp-crow-api/ 、https://kie.ai/blog/what-is-suno-v6 。v5.5 官方发布页 https://suno.com/release-notes/introducing-v5-5-voices-custom-models-and-my-taste 、DMN https://www.digitalmusicnews.com/2026/03/26/suno-launches-version-5-5/ 。Remaster 专用代号 chirp-flounder/carp/bass 仅 suno-cli 单源，low。
- **结论：《一路同心》（chirp-fenix-engine-b）= v5.5 Fenix**，即 2026-08-26 时的最新模型，现已退役；重做只能在 v6 家族上进行，听感必然与旧歌不完全一致。精确字符串 "chirp-fenix-engine-b" 在搜索引擎中无任何 Suno 相关结果（两轮独立确认），"-engine-b" 后缀含义无来源，推断为 v5.5 的服务/变体标识（low）。

### 1.2 社区反馈（已确认存在，但属主观评价）

- r/SunoAI 发布日置顶帖标题 "a massive downgrade"；主要抱怨：混音发闷、人声被埋、高频缺失（"blanket over the speakers"）、忽略 BPM/速度/曲风/编配指令、把指令念出来而不是唱、Duration=Auto 时更长更稀疏；高赞评论 "It's called complying to a lawsuit" https://undetectr.com/blog/suno-v6-reactions 。也有用户认为人声更干净、Cover 更好 https://www.eesel.ai/blog/suno-v6-review 。日本评测以"無難化"（趋于保守）批评。
- 首日听测：曲风识别更强，但"human messiness"弱、偶有刺耳人声伪影；同一 v6 提示词两个 take 之间的差异可能大于改提示词的差异 https://jackrighteous.com/en-us/blogs/guides-using-suno-ai-music-creation/suno-v6-reviews-problems-whats-next 。
- 2026-09-11 前后 Suno 发布了针对"人声念指令、v6 改写风格提示词、混音发闷"的排障指引；是模型热更新还是仅文档，摘要未明确。
- **中文表现：未找到任何 v6 中文普通话咬字的系统评测**（B 站 https://www.bilibili.com/video/BV1RPY86oEQb/ 、V2EX https://www.v2ex.com/t/1241366 、大佬说 https://www.locdd.com/t/topic/89638 均为功能讨论）。掘金文章的建议是通用性的：Suno 训练数据以英文为主，中文"一字一音节、四声、多音字"需逐句对词校验 https://juejin.cn/post/7682684241834508288 。大佬说用户称"V6 需要比 5.5 更细的提示词，否则风格容易重复"。

### 1.3 已排除的误传（核查判为 refuted / 需修正）

- ✗ "免费账户歌曲默认公开"——两轮检索无任何来源支持，删除。
- ✗ "v6 仅基于授权目录从头训练"——Suno 自述含用户偏好数据与研发积累（见 1.1）。
- ✗ "额外下载 $2.99 来自官方定价页"——实为 roo.beehiiv 对 App 内购界面截图的转述（1 首 $2.99 / 3 首 $8.95 / 5 首 $14.95 / 10 首 $29.90）https://roo.beehiiv.com/p/suno-download-prices-explained ；官方 8 月公告时明确"价格尚未公布"。
- ✗ "免积分促销自 9 月 9 日发布日开始"——实为 9 月 10 日开启。
- ✗ "Variety 是 0–100 连续滑杆、默认一律 Normal"——五档离散，v6-wild 默认 Off。
- ✗ "官方未对指令遵从度作任何承诺"——官方《Current Models: v6》有 "follows detailed instructions better than any previous Suno model"；但**多语言/中文**方面确无 v6 专属官方说明。
- ✗ anthem-craft 角度"chirp-fenix v5.5 已是最新模型、重做无代际跃升"——该角度检索时未覆盖 v6 消息，与其余五角度矛盾，以 v6 已发布为准。
- ✗ prompting 角度"chirp-fenix = v5 时代引擎"——应为 v5.5。
- ✗ "Suno 2026-01 起要求用户声明歌词来源"——仅中文自媒体 https://www.tixiaolu.com/v2/posts/v2-d56805c3.html 一处，官方与英文来源均无，不采用。

## 二、简单模式 vs 高级模式

界面标签：2026-09 第三方指南称 v6 Create 页为 Simple / Advanced / Sounds 三模式 https://jackrighteous.com/en-us/blogs/guides-using-suno-ai-music-creation/inside-suno-v6-create-simple-advanced-sounds-guide ；官方帮助中心旧文仍写 "Custom" https://help.suno.com/en/articles/2415873 ，官方 v6 FAQ 也用 "Custom Mode"。给股东写操作指南时同时写"高级/自定义（Advanced/Custom）"。Sounds 模式生成音效/循环素材，与整曲无关。

| 项目 | 简单模式（Simple） | 高级模式（Advanced / Custom） | 置信度 · 来源日期 |
|---|---|---|---|
| 输入框 | 仅一个自然语言描述框 + Instrumental 开关；v6 起可附加参考物（Suno 歌曲/播放列表/音频/图片/视频），模型自动决定 Cover/Remix/Extend | Lyrics 歌词框、Styles 风格框、Title、Exclude Styles、More Options 面板 | high[第三方] 2026-09 |
| 歌词归属 | 由 AI 根据描述自动撰写，**不能提供逐字歌词**（官方："要用自己的歌词请切到 Custom"） | 用户手写，Suno 按歌词框演唱；框内右上魔法棒可 AI 助写 | high[官方] 长期文章 |
| 描述框/风格框上限 | ~200 字符（多篇旧指南）vs 3,000 字符（hookgenius v6 实测），**冲突，以界面计数器为准** | Style 1,000 字符（v4 时代 200）；社区建议 100–300 字符、4–7 个不重叠描述符 | medium[第三方] 2026-09 |
| 歌词框上限 | 无 | 5,000 字符（v4 为 3,000）；超限静默截断；社区称约 3,000 字符为甜点 | high[第三方] 2026-09 |
| 排除风格 | 无 | Exclude Styles 1,000 字符，界面显示 "-piano"；**仅 Pro/Premier**；建议 ≤5 项 https://suno.com/release-notes/exclude-styles | high(存在)/medium(档位) |
| 标题 | 无 | 100 字符（API 80） | medium |
| 人声性别 | 无 | Vocal Gender：Male / Female 二选（无"混声"选项） | high[第三方] |
| 时长 | Auto | Duration：Auto 或 Custom 10 秒–6 分钟（5 秒步进，默认 3:00）；到点硬切非淡出；官方"单次最长 8 分钟"与 6 分钟滑杆上限并存未厘清 | medium |
| 滑杆 | 无 | Weirdness（Safe→Chaos，默认 50%）、Style Influence（Loose→Strong，默认 50%）、Audio Influence（附音频时出现，默认 25%）、**Variety**（五档，见 1.1） https://help.suno.com/en/articles/13924481 | high[官方+第三方] |
| Max Mode | 未明确 | 开关，2x 积分（20/次） | high[官方] |
| Persona / Inspo / My Taste | 无 | Persona（从库内歌曲提取人声+风格，Pro/Premier；有用户反馈旧 Persona 在 v6 上失真）https://suno.com/blog/personas ；Inspo（歌词框上方 +Inspo 选播放列表）https://help.suno.com/en/articles/6882753 ；My Taste（风格框魔法棒，所有档位，会让默认风格漂移）https://help.suno.com/en/articles/11362561 | medium |
| 后期编辑 | — | Extend / Cover / Remaster / Replace Section（Pro/Premier，https://help.suno.com/en/articles/3271873 ）/ v6 自然语言分段编辑与单词替换（有失败报告） | high |
| 积分 | 10 积分/次出 2 首 | 同左；Max Mode 20 | high[官方] |

- **订阅档位（2026-09）**：Free 每日 50 积分、仅 v6-mini、终身 7 次试用下载（9 月 3 日后新注册者"may receive downloads on occasion"）、无商用权；Pro $10/月（年付 $8）2,500 积分 + 20 次下载/月；Premier $30/月（年付 $24）10,000 积分 + 60 次下载/月 + Studio 2.0（Studio 导出不限下载）。下载上限 2026-09-03 生效、追溯适用于库内所有旧歌；按"歌曲"计数，同一歌曲多格式/重复下载只算 1 次。来源 https://suno.com/pricing 、https://variety.com/2026/music/news/suno-unveils-download-caps-for-free-paid-tiers-generator-1236831589/ 、https://www.musicbusinessworldwide.com/suno-limits-subscribers-downloads-per-month/ 、https://lumimusic.ai/blog/suno-pricing 、https://chotto.news/suno-to-implement-download-restrictions-from-september-3-2026-free-users-can-download-7-times-in-their-lifetime-pro-users-20-times-per-month-and-premier-users-60-times-per-month/ 。
- **推荐：必选高级模式**。理由：(1) 它是唯一有独立歌词框的模式，"歌词一字不改"只能在此实现 https://undetectr.com/blog/suno-ai-custom-mode-guide ；(2) Variety=Off、Style Influence、Exclude Styles、Vocal Gender、Duration、Max Mode 全部只在高级模式；(3) 简单模式"适合探索，不适合出成品"[第三方共识]。v6 简单模式把整段歌词粘进描述框是否会逐字演唱——无任何来源确认，保守假设不会。
- **v6-mini 是否开放全部高级控件**（滑杆、Max Mode）未获确认；Exclude Styles、Persona 明确为 Pro/Premier 专属。

## 三、高级模式提示词工程要点

- **字段分工**：风格框只写"声音"，歌词框只写歌词与段落标签，有专用控件（时长、人声性别、排除）就用控件 https://jackrighteous.com/en-us/blogs/guides-using-suno-ai-music-creation/where-to-put-your-suno-prompt-guide 。
- **风格框写法**：主流派放最前（社区称前置词权重更高，官方未证实）→ 情绪 → 速度/能量 → 核心乐器 → 人声类型 → 制作质感；4–7 个描述符，100–300 字符；混合流派用一句话定主次；可写 BPM（"文字速度 + 数字"）与调性，但均为概率性影响，v5 时代 BPM 服从差（要求 150 实际 90–110 https://zhuanlan.zhihu.com/p/1967182170595493783 ），v6 社区亦报告忽略 BPM https://www.musicful.ai/music-tips/suno-prompts/ 、https://hookgenius.app/learn/suno-prompt-guide-2026/ 。
- **v6 精确控制配方（社区）**：Variety=Off；Style Influence 拉到 75–85（默认 50% 意味风格提示"权重被折半"）；Weirdness ≤50；风格框内绝不写"不想要的东西"（会被当正向词），排除放 Exclude 字段 https://hookgenius.app/learn/suno-negative-prompting/ 。
- **结构标签**：[Intro][Verse][Pre-Chorus][Chorus][Bridge][Outro]/[End] 最稳；独占一行、放所控歌词上方、统一方括号；每次想出现副歌都要重写 [Chorus]（写一次通常只唱一次）；以 [Outro]/[End] 收尾可降低拖长/循环风险（非"必然截断"）；不要每行加标签 https://hookgenius.app/learn/suno-lyrics-formatting/ 。v6 无新标签语法、官方仍无完整列表 https://jackrighteous.com/en-us/pages/suno-ai-meta-tags-guide 。
- **括号语义**：方括号 [ ] = 给引擎的指令（独占一行时通常不被唱）；圆括号 ( ) = **会被唱出**的和声/应答/即兴；不带括号的指令词会被当歌词唱 https://medium.com/@J.S.Matkowski/how-to-control-suno-ai-music-with-brackets-and-parentheses-with-real-examples-00956a629585 。团队歌可用圆括号做 call-and-response。
- **人声标签是概率性提示而非命令**；v6 对"带描述的方括号"（如 [Chorus – full team unison, march drums]）比裸标签更听话（heho.ai 观察）；每段标签 ≤2–4 个；[Male]/[Female]/[Both] 只是引导 https://jackrighteous.com/en-us/blogs/guides-using-suno-ai-music-creation/duet-harmony-theme-meta-tags-suno 。v6 更"字面"：没写清谁唱/怎么结束时会随机选且每次不同，结尾要写明方式和长度（"hard stop after the last chorus"）https://undetectr.com/blog/suno-v6-duet-prompts 。
- **歌词框顶部长段 Song Instruction**：社区共识不推荐（可能被唱出、消耗字符、与关键指令竞争），推荐改为顶部 1–2 行短标签 "top-anchor"（如 [Male baritone lead, unison choir on chorus]）。**但**旧歌正是用长指令在 v5.5 上生成且老板认可——该做法"有风险"而非"必然失败"，v6 上无实证，需 A/B。"8 syllables per line""strict 4/4"等数值指令是否被执行无任何来源，音节对齐应靠歌词本身写齐（各行相差 ≤1–2 音节）。
- **齐唱/合唱触发词**：lineup（group/choir）+ harmony（unison / call-and-response）+ delivery（belted/anthemic）三类；"anthemic chorus""singalong hook""gang vocals""like a crowd singing together" 会叠加人声；副歌加 "Oh-oh" 音节强化群唱 https://usesuno.com/guide/vocals/ 、https://suno.com/style/big-sing-along-chorus-with-gang-vocals 。6 人小店适合 "unison group vocals" 而非 "choir harmonies"（分声部）。
- **副歌上口**：2–4 行；最强一句放段首（社区称每段第一行旋律权重最大，单源）；围绕一个重复词/短句做锚点、重复 2–4 次；每行 6–10 音节且一致；v6 主歌:副歌 ≈ 2:1 行数（8:4），太短会赶拍（hookgenius 单源，low）https://hookgenius.app/learn/suno-song-structure-tips/ 。
- **迭代流程**：固定风格框、每次只改一个变量、Variety=Off 便于复现；选出 Keeper 后：音质打磨→Remaster；换风格保歌词旋律→Cover；结构不完整→Extend；某段弱→Replace Section；原则 Keeper→诊断→保护→最小改动→A/B https://jackrighteous.com/en-us/blogs/guides-using-suno-ai-music-creation/suno-remix-covers-edits-studio 。重做旧歌用 Cover + 高 Audio Influence（≥80%）而非 Remaster（Genx Notes 单源经验）https://blog.genxnotes.com/en/how-to-remake-your-old-suno-songs-with-the-latest-version/ ，官方建议 Cover 时开 Max Mode。
- **踩坑对策**：歌词被改写/跳行/赶拍——Suno 把歌词当"表演脚本"，避免大块相同文本与杂乱结构，想重复的句子显式写出 https://jackrighteous.com/en-us/blogs/music-creation-process-guide/why-ai-music-ignores-lyrics ；标签被念出——标签短（1–3 词）、独占一行、只放歌词框 https://stokemctoke.com/the-complete-suno-ai-meta-tags-guide/ 。

## 四、中文歌词生成经验与坑

（以下全部基于 v4–v5.5 时代经验，v6 中文表现无任何专项评测，需实测。）

- **每行字数**：各教程区间 6–15 字不一（AI House 7–10；知乎 10–15；suno.ing 7–10、超 12 拆行；海洋大学 6–12），共同点是**各行长度保持一致、避免长句**；副歌更短 https://zhuanlan.zhihu.com/p/1990938898797441842 、https://li.ntou.edu.tw/var/file/29/1029/img/1560/NTOU_AI_SUNO_Tutorial.pdf 。旧歌固定 8 字（4+4）落在区间内。
- **押韵**：不必每句押，副歌尽量押，韵脚放句末，可押近似韵。
- **多音字/生僻字**：Suno 会唱错或跳过（v2–v3.5 时代实测，CSDN 2024-06 https://blog.csdn.net/linxingliang/article/details/139751079 ）；最有效对策是**常用同音字替换**（朝→招、还→环、重→崇、盎然→昂然），生成后再把展示歌词改回；2026 年繁中案例仍在用此法（獴→猛、猴→喉）https://vocus.cc/article/69e34e4bfd89780001fd6d78 。新模型上严重程度很可能已减弱，应作为"A/B 发现问题后再用"的兜底。
- **汉字优于拼音**：直接写汉字，拼音只用于个别关键字，标准拼音易被当英文单词读 https://hookgenius.app/learn/suno-chinese-prompts/ 。
- **品牌名"住小叮"**：zhù xiǎo dīng 三字均为单音常用字，无多音字风险（语言事实，high）；搜索无任何 Suno 唱该词的案例；若实测唱错再用同音字替换。**不要**用 "(ding)" 括号注音——括号内容会被唱出，与第三章矛盾。建议放句首或句末重音位，副歌其他句尾可选 -ing/-eng 近韵（同行/星/赢/城/灯）以统一韵脚 [推断]。
- **标点与断句**：社区意见不一（台湾教程"行尾不加标点"，英文社区"用标点控停顿"），非官方规则，**保持一致即可**；用换行而非标点断句；每段 4–8 行，段间空行。
- **风格框用英文**：CSDN 称中文提示词会被自动转英文并丢信息（社区推测，非官方机制）https://blog.csdn.net/u014177256/article/details/158155063 ；必须显式写 "Mandarin Chinese vocals / singing in Mandarin"，用 Mandopop / C-Pop / Chinese folk 等具体词而非 "Chinese music"；Suno 默认英文歌词。分工：**风格框英文、歌词框汉字**。
- **语速快/吞字**：Suno 语速偏快；对策：缩短句子、句间空行或加"哦/嘿"即兴词、重复副歌、风格框加 mid-tempo/Adagio（BPM 指令服从差）https://blog.csdn.net/qq_17766199/article/details/140746445 。
- **夹英/粤语**：歌词全汉字 + 风格框写 Mandarin，可用 Exclude 排除 Cantonese / English vocals（Pro+；"English vocals"排除有效性为推断）。指定"大陆标准普通话 vs 台湾腔"无已知可靠提示词，v5 对口音指令服从差。
- **中文说唱易成"数来宝"**：句式太工整所致，长短句交错 https://jxysys.com/post/13462.html ；对进行曲团队歌反而是"工整"需求，不冲突。
- **参数**：Weirdness 50 为中性，人声太完美无感情→调高；走音/咬字乱→降 Weirdness、提高 Style Influence https://acetaggen.com/blog/weirdness-exclude-styles-reference-suno-advanced-parameters 。
- **v5.5 卖点**"中文/方言演唱识别与咬字全面增强"仅知乎二手转述；第三方竞品页称 Mureka V9 中文声调明显优于 Suno（立场偏向，打折）。

## 五、企业/团队歌创作要点与案例

- **结构**（修正后）：主歌 2 段、副歌 3 次（末尾可双副歌，即 ABABCBB）、桥段 1 段；副歌在 60 秒内首次出现；4/4 拍 90 BPM、前奏/尾奏/主歌/副歌各 8 小节 + 间奏 16 小节 ≈ 3:33 https://www.zhihu.com/question/430777970 。前奏从 1980 年代 ~20 秒缩到如今 ≤10 秒（学术出处应为 Gauvin 2017, Musicae Scientiae，未能检索到 URL，low）。
- **歌词禁忌**：口号堆砌、形容词+抽象名词堆叠（"共创辉煌"式）；要找独特切入角度、提炼 1–2 句"词眼"、用词朴素口语化、多意象少直陈、一首歌只写一个内容 http://www.sybrc.com/a/doubt/2012/1110/12.html 、https://zhuanlan.zhihu.com/p/34520464 。英文经验：副歌是"核心承诺"，短、可重复、用开口元音；术语旁放人话翻译。
- **反面案例**：KPMG《Our Vision of Global Strategy》（"We're as strong as can be / A dream of power and energy"）2001 年被员工外泄混音嘲讽，收录站一周 20 万访客 https://edition.cnn.com/2002/BUSINESS/04/03/corporate.songs/ ；IBM《Ever Onward》（1931，"Our reputation sparkles like a gem"）成自夸反面教材，评论称员工自写企业歌"几乎一律糟糕" https://www.peoplemanagement.co.uk/article/1746574/employees-penning-corporate-anthems-ear-splitting-results ；海底捞店歌《携手明天》被前员工称"共创美好未来"式"口水歌"（单一口述，medium）https://zhuanlan.zhihu.com/p/424772648 ；36 氪："最失败的企业文化是喊口号喊到员工心累" https://36kr.com/p/3451660467902081 。
- **正面案例**：蜜雪冰城主题曲只有一句词，改编自《Oh! Susanna》，反复不超 30 秒，"土"与低价定位一致反而强化亲民 https://news.qq.com/rain/a/20210625A0DC7C00 ——**极简低价业态与"简单、直白、可重复"的歌是匹配的**；阿里 20 周年《We are Alibaba》员工合唱、2874 位五年陈共创歌（具体数字单源，low）https://izxxz.com/article/1159 ——员工共创 + 具体仪式承载情感；年会改编歌靠人名、内部梗、会议金句引发共鸣 https://zhuanlan.zhihu.com/p/49412555 ；"打工人"梗证明自嘲比鸡汤更易引起年轻基层共鸣 https://zhuanlan.zhihu.com/p/269700577 。华为无被确认的官方司歌。
- **齐唱参数**（借用会众歌/校歌经验值，Suno 能否按指令控制音域**无任何证据**）：未经训练混声音域约一个八度加三/四度（保守 B♭3–D5，G3–B4 可覆盖 84% 会众）https://forum.musicasacra.com/forum/discussion/2615/congregational-singing-range/p1 ；校歌"低音 C 到高音 D"；进行曲 116–120 BPM，校歌 110–120 BPM https://zgycgc.com/gequ/yinyue/15496.html ；中速 pop 92–110 BPM；6 人小团队用单声部齐唱 https://www.163.com/dy/article/JOF5UITC055695S7.html 。
- **未找到**任何青年旅舍/民宿/经济型酒店品牌的团队歌案例（中英文均无）。

## 六、商用与版权

- **付费档**（Pro/Premier）订阅期间生成的歌曲享商用权，退订后保留 https://help.suno.com/en/articles/9601665 、https://help.suno.com/en/articles/2416769 ；"commercial use" 定义为 "your ability to earn money from the music" https://help.suno.com/en/articles/9601985 。
- **免费档**歌曲所有权归 Suno，仅限 "personal, non-commercial use" https://help.suno.com/en/articles/9601601 ；升级付费**不追溯**（"does not give you retroactive commercial use licensing… Suno may offer retroactive rights in certain cases, but this is not guaranteed"）https://help.suno.com/en/articles/2425729 。
- **2026-09-03 新条款**：商用权与"付费档配额内的官方下载（permitted Download）"绑定，合规下载后商用权永久、不受退订/降级影响；第三方律所解读称条款删去用户 "Ownership" 措辞、改为永久商用许可（需以原文为准）https://www.tornevalls.se/suno-is-changing-its-terms-in-september-but-the-scary-version-is-not-quite-what-the-terms-actually-say/ 、https://suno.com/terms-september-2026 、https://suno.com/blog/suno-updates-tos 、https://help.suno.com/en/articles/13614785 。**内部矛盾待解**：新 FAQ"付费订户下载的任何歌曲均有商用权"与旧文"不追溯"对"免费期生成、付费后下载"的旧歌结论相反。
- **企业内部播放**：官方未逐字界定；免费档限 "personal"，公司晨会/年会播放不属个人使用，**应按商用处理**——付费档生成并官方下载后再用于任何公司场景 [推断，medium]。
- **免责与风险**：Suno 明确 "makes no representation or warranty… that any copyright will vest in any Output"，用户须对输出引发的索赔向 Suno 赔偿；用户提交的歌词授予 Suno 永久许可 https://suno.com/terms-of-service 、https://terms.law/ai-output-rights/suno/ 。美国版权局以人类创作为登记前提。
- **诉讼**：Warner（2025-11-25 和解并授权）https://www.forbes.com/sites/conormurray/2025/11/25/warner-music-settles-lawsuit-with-suno-and-will-partner-with-ai-music-generator/ 、BMG、Believe 已成合作方；UMG/Sony 案（D. Mass.，Saylor 法官）继续：2026-08-18 驳回扩至 61,026 首录音的动议，8 月 25 日追加 YouTube stream-ripping 指控，取证 2026-09-30 截止，简易判决 2027-04-09 https://www.musicbusinessworldwide.com/why-a-fight-over-61000-recordings-could-shape-the-future-of-ai-music-licensing/ ；Suno 在 2026-09-01 答辩中承认曾用 yt-dlp 抓取 YouTube 音频。德国 GEMA v. Suno 慕尼黑地区法院 2026-07-31 判 Suno 败诉（含"输出物本身构成侵权复制"），待上诉 https://www.twobirds.com/en/insights/2026/germany/munich-district-court-rules-on-ai-generated-music-gema-v-suno 。
- **v6 合规优势**：授权数据训练；全部输出带 Audible Magic 水印/指纹；Musixmatch Sentinel 筛查提示词与输出中的既有歌词 https://www.musicbusinessworldwide.com/suno-first-customer-of-musixmatchs-sentinel-which-screens-ai-prompts-and-outputs-for-copyrighted-material/ 。旧歌《一路同心》（v5.5，非授权数据）合规性弱于 v6 新作。
- **中国大陆可及性**：官方站需代理；支付走 Stripe 仅外卡/PayPal，国内 IP 支付受限，虚拟卡 2025 下半年起风控收紧 https://zhuanlan.zhihu.com/p/28202305474 ；代充/合租违反条款且商用权归账号持有人而非公司；suno.cn"苏诺之音"（深圳超时代软件）与 Suno Inc. 授权关系无法确认，**视为非官方渠道不要使用** https://www.aitop100.cn/tools/suno-cn 。iOS App 内购（非中国区 Apple ID）为可能替代路径（记忆，未核实）。
- **国内发布合规（未能检索，模型记忆 low）**：《人工智能生成合成内容标识办法》2025-09-01 施行，AI 音频需显式（语音提示）+ 隐式（元数据）标识，抖音/视频号已上线 AI 声明开关；网易云/QQ 音乐上架政策未知。仅内部播放不触发，对外发布须核实。

## 七、对住小叮三首歌的操作建议（初稿，供主研究员采用）

### 7.1 写歌前必须向股东确认（决定路径，搜索无法替代）

1. 《一路同心》在谁的 Suno 账号生成（股东本人/员工/代充）？2026-08-26 时是免费档还是付费档？手上 64kbps mp3 是官方 Download 还是分享链接/微信转存（官方 MP3 通常 ≥128kbps，64kbps 可疑，low）？——决定老歌商用权、能否作 Cover/Persona 素材。
2. 老板对旧歌八项的"保留/改/无所谓"：曲风（进行曲）、速度、人声（混声齐唱）、咬字/发音有无具体错句、歌词（套话→业态细节？品牌名次数？）、时长 2:02、干脆收尾、使用场景（晨会齐唱/年会/招聘视频/门店 BGM）。
3. 三首是同一主题三种风格版本供挑选，还是三种用途？是否对外发布（触发商用 + AI 标识义务）？
4. 品牌敏感点：是否允许把"4 平米、共享卫浴、夜班巡逻、催预离/要好评"写进歌里，是否允许自嘲口吻，必须/禁止出现的词。

### 7.2 账号与模式

- 用**公司或股东本人控制的 Pro 账号**（$10/月，2,500 积分 ≈ 250 次生成，20 次下载/月，三首成品 + 若干备选足够；下载按歌曲计数，不要每版都下载）。免费档只能用 v6-mini 且无商用权，不适合出成品。
- **高级模式**（Advanced/Custom），模型选 **v6**（非 wild）；v6-wild 只用于探索编曲变体。
- 参数：Variety=**Off**；Style Influence 75–85；Weirdness 40–50；Vocal Gender 不选或试 Male（无混声选项，混声靠风格框与标签）；Duration Custom 2:15–2:45（若股东要 3 分钟以上再放宽）；Max Mode：>2 分钟或最终定稿版开启（20 积分），草稿不开。

### 7.3 提示词结构（A/B 两套模板，各出 2–3 轮）

- **模板 A（延续旧模板，保证连续性）**：沿用歌词框首行短化后的 Song Instruction（压缩到 ≤12 词，如 `[4/4 march, one note per syllable, no melisma, sing only written lyrics]`），段落标签保留 `[Verse 1 | firm mixed vocals]` `[Refrain | full team unison, mid-range, no shouting]` `[Outro | hard stop after last line]`。风格框英文补齐：`Mandarin Chinese team anthem, march, 116 BPM, snare cadence, brass, unison group vocals, mixed male and female voices, clear articulation, mid-range melody, easy to sing along`。
- **模板 B（社区推荐分工）**：歌词框只放汉字歌词 + 裸/短标签；所有音乐描述放风格框；Exclude：`rap, EDM, auto-tune, whisper, English vocals, Cantonese, choir harmonies`（≤5 项择要）。
- 对比维度：是否把指令念出来、咬字错字数、是否齐唱、结尾是否干脆、速度是否接近要求。两套模板各抽 2–3 轮（4–6 个候选）再挑 Keeper。

### 7.4 歌词写作（三首方向，待股东定夺）

- 通用规则：每行 7–10 字（旧歌 8 字可延续）、各行一致；副歌 2–4 行、押韵、第一行放"词眼"、最后一行落品牌名"住小叮"；全歌约 150–220 字对应 2–2.5 分钟；避免多音字（行/长/重/还/朝）；"住小叮"全曲 3–4 次；主歌写可核对的真实细节（四平米一张床一盏灯、凌晨三点前台灯亮着、阿姨拖把先过一遍再开门、共享卫浴排队的早晨、催预离/要好评/办会员），替换"四面八方/共创辉煌"式套话。
- 方向 A **进行曲升级版**（保留老板认可的曲风，只换歌词内容）：116–120 BPM，副歌口号化，可在圆括号写应答句做 call-and-response。
- 方向 B **齐唱口号版**（中速 96–108 BPM 民谣摇滚/indie pop，anthemic, singalong hook, "Oh-oh"）：更适合年轻团队日常哼唱，音域控制在一个八度左右（靠试唱筛选，非提示词保证）。
- 方向 C **夜班叙事版**（慢-中速 80–92 BPM，写值夜、交班、阿姨与夜班各一段独唱，副歌全员齐唱）：自嘲式骄傲，需股东授权口吻。
- 若股东要求三首同风格，则 A 出三版（词不同）；否则 A/B/C 各一。

### 7.5 迭代与交付

- 每首：Keeper → 逐句对词记录错字 → 错字优先试 v6 单词替换/Replace Section（中文可用性未验证），失败则同音字替换重抽 → 定稿开 Max Mode 再抽 1 次 → 官方 Download（MP3+WAV 只计 1 次）→ 保留下载记录与订阅凭证。
- 老歌《一路同心》若在可控付费账号内：可作 Cover（Audio Influence ≥80% + Max Mode）或 Inspo 播放列表素材延续气质；否则只作风格参考。
- 若对外发布：勾选平台 AI 声明，并另行核实《标识办法》对音频显式标识的要求。

## 八、未解问题

1. v6 对中文普通话咬字/吞字相对 v5.5 是进步还是退步——无任何评测，只能用《一路同心》歌词做对照 A/B。
2. 歌词框长段 Song Instruction 与数值指令（8 syllables、strict 4/4）在 v6 上是否仍有效/是否被唱出——无实证，需模板 A/B 对照。
3. v6 简单模式描述框上限（~200 vs 3,000 字符）与"粘入歌词能否逐字演唱"——需界面核实。
4. Vocal Gender 只有 Male/Female，如何稳定获得男女混声齐唱；gang vocals/unison 触发词在 v6 上是否仍有效。
5. Suno（任何版本）能否按指令控制调性/音域/最高音——无证据，"便于齐唱"只能靠生成后试唱筛选。
6. 2026-09-03 新条款原文对"免费期生成、付费后官方下载"旧歌的商用权处理；"公司内部播放"是否有官方界定；中国大陆公司能否用公司账户付款/开发票。
7. v6 单词替换/Replace Section 是否支持中文歌词并可用于修发音。
8. v6-mini 是否开放全部高级控件与 Max Mode；Exclude Styles 是否确为 Pro/Premier 专属。
9. 2026-09-11 的"修复"是模型热更新还是仅文档；截至 09-16 有无点版本。
10. "-engine-b" 后缀含义；Remaster 专用 chirp 代号（flounder/carp/bass）仅单源。
11. Duration 滑杆 6 分钟上限与"单次最长 8 分钟"如何并存（对 2–3 分钟团队歌无影响）。
12. 国内平台（抖音/视频号/网易云/QQ 音乐）对 AI 音乐的标识与上架规则——本次未能检索。
13. 股东侧四组事实问题（7.1）全部待答。

## 九、来源列表（去重）

https://suno.com/blog/introducing-v6
https://suno.com/release-notes/introducing-v6
https://help.suno.com/en/articles/13924481
https://help.suno.com/en/articles/13924737
https://help.suno.com/en/articles/13924801
https://x.com/suno/status/2097714273942163823
https://suno.com/release-notes/introducing-v5-5-voices-custom-models-and-my-taste
https://suno.com/blog/v5-5
https://suno.com/pricing
https://suno.com/blog/suno-updates-tos
https://suno.com/terms-september-2026
https://suno.com/terms-of-service
https://suno.com/release-notes/exclude-styles
https://suno.com/blog/personas
https://suno.com/hub/how-to-make-a-song
https://suno.com/style/big-sing-along-chorus-with-gang-vocals
https://help.suno.com/en/articles/2415873
https://help.suno.com/en/articles/6882753
https://help.suno.com/en/articles/11362561
https://help.suno.com/en/articles/3271873
https://help.suno.com/en/articles/13670529
https://help.suno.com/en/articles/9601665
https://help.suno.com/en/articles/2416769
https://help.suno.com/en/articles/9601985
https://help.suno.com/en/articles/9601601
https://help.suno.com/en/articles/2425729
https://help.suno.com/en/articles/13614785
https://techcrunch.com/2026/09/09/suno-replaces-its-ai-models-with-a-new-one-trained-on-licensed-music-as-copyright-suits-pile-up/
https://variety.com/2026/music/news/suno-new-label-backed-model-v6-1236855351/
https://variety.com/2026/music/news/suno-unveils-download-caps-for-free-paid-tiers-generator-1236831589/
https://www.digitalmusicnews.com/2026/09/09/suno-v6-launch/
https://www.digitalmusicnews.com/2026/03/26/suno-launches-version-5-5/
https://musically.com/2026/09/09/suno-launches-its-v6-ai-music-models-heres-what-you-need-to-know/
https://www.rollingstone.com/music/music-news/suno-new-model-v6-warner-music-group-1235623431/
https://www.musicbusinessworldwide.com/suno-limits-subscribers-downloads-per-month/
https://www.musicbusinessworldwide.com/suno-hits-2m-paid-subscribers-300m-annual-revenue/
https://www.musicbusinessworldwide.com/why-a-fight-over-61000-recordings-could-shape-the-future-of-ai-music-licensing/
https://www.musicbusinessworldwide.com/suno-first-customer-of-musixmatchs-sentinel-which-screens-ai-prompts-and-outputs-for-copyrighted-material/
https://www.forbes.com/sites/conormurray/2025/11/25/warner-music-settles-lawsuit-with-suno-and-will-partner-with-ai-music-generator/
https://www.twobirds.com/en/insights/2026/germany/munich-district-court-rules-on-ai-generated-music-gema-v-suno
https://imusician.pro/en/resources/blog/suno-v6-licensed-ai-music-models
https://news.qq.com/rain/a/20260909A0DXKT00
https://www.ithome.com/1/000/351.htm
https://jackrighteous.com/en-us/blogs/guides-using-suno-ai-music-creation/inside-suno-v6-create-simple-advanced-sounds-guide
https://jackrighteous.com/en-us/blogs/guides-using-suno-ai-music-creation/suno-v6-reviews-problems-whats-next
https://jackrighteous.com/en-us/blogs/guides-using-suno-ai-music-creation/where-to-put-your-suno-prompt-guide
https://jackrighteous.com/en-us/blogs/guides-using-suno-ai-music-creation/suno-remix-covers-edits-studio
https://jackrighteous.com/en-us/blogs/guides-using-suno-ai-music-creation/duet-harmony-theme-meta-tags-suno
https://jackrighteous.com/en-us/blogs/music-creation-process-guide/why-ai-music-ignores-lyrics
https://jackrighteous.com/en-us/pages/suno-ai-meta-tags-guide
https://hookgenius.app/learn/suno-v6-guide/
https://hookgenius.app/learn/what-happened-to-suno-v5/
https://hookgenius.app/learn/suno-character-limits/
https://hookgenius.app/learn/suno-chinese-prompts/
https://hookgenius.app/learn/suno-prompt-guide-2026/
https://hookgenius.app/learn/suno-lyrics-formatting/
https://hookgenius.app/learn/suno-song-structure-tips/
https://hookgenius.app/learn/suno-negative-prompting/
https://undetectr.com/blog/suno-v6-changing-your-prompt
https://undetectr.com/blog/suno-v6-reactions
https://undetectr.com/blog/suno-v6-duet-prompts
https://undetectr.com/blog/suno-ai-custom-mode-guide
https://roo.beehiiv.com/p/suno-v6-features
https://roo.beehiiv.com/p/suno-v6-free-48-hours-paid-plan
https://roo.beehiiv.com/p/suno-download-prices-explained
https://github.com/bitwize-music-studio/claude-ai-music-skills/issues/562
https://kie.ai/blog/what-is-suno-v6
https://unifically.com/blogs/suno
https://www.cometapi.com/suno-v5-5-what-is-new-and-how-to-use-it-via-api--studio/
https://sunoaiwiki.com/news/2025/09-25-suno-v5-chirp-crow-api/
https://heho.ai/blog/suno-retired-older-models-your-songs
https://heho.ai/blog/suno-v6-what-changed-for-lyrics
https://blog.genxnotes.com/en/how-to-remake-your-old-suno-songs-with-the-latest-version/
https://www.eesel.ai/blog/suno-v6-review
https://lumimusic.ai/blog/suno-pricing
https://chotto.news/suno-to-implement-download-restrictions-from-september-3-2026-free-users-can-download-7-times-in-their-lifetime-pro-users-20-times-per-month-and-premier-users-60-times-per-month/
https://www.tornevalls.se/suno-is-changing-its-terms-in-september-but-the-scary-version-is-not-quite-what-the-terms-actually-say/
https://terms.law/ai-output-rights/suno/
https://usesuno.com/guide/vocals/
https://www.musicful.ai/music-tips/suno-prompts/
https://medium.com/@J.S.Matkowski/how-to-control-suno-ai-music-with-brackets-and-parentheses-with-real-examples-00956a629585
https://stokemctoke.com/the-complete-suno-ai-meta-tags-guide/
https://acetaggen.com/blog/weirdness-exclude-styles-reference-suno-advanced-parameters
https://juejin.cn/post/7682684241834508288
https://www.bilibili.com/video/BV1RPY86oEQb/
https://www.v2ex.com/t/1241366
https://www.locdd.com/t/topic/89638
https://zhuanlan.zhihu.com/p/1990938898797441842
https://zhuanlan.zhihu.com/p/1967182170595493783
https://zhuanlan.zhihu.com/p/34520464
https://zhuanlan.zhihu.com/p/424772648
https://zhuanlan.zhihu.com/p/49412555
https://zhuanlan.zhihu.com/p/269700577
https://zhuanlan.zhihu.com/p/28202305474
https://www.zhihu.com/question/430777970
https://blog.csdn.net/linxingliang/article/details/139751079
https://blog.csdn.net/u014177256/article/details/158155063
https://blog.csdn.net/qq_17766199/article/details/140746445
https://vocus.cc/article/69e34e4bfd89780001fd6d78
https://li.ntou.edu.tw/var/file/29/1029/img/1560/NTOU_AI_SUNO_Tutorial.pdf
https://jxysys.com/post/13462.html
http://www.sybrc.com/a/doubt/2012/1110/12.html
https://edition.cnn.com/2002/BUSINESS/04/03/corporate.songs/
https://www.peoplemanagement.co.uk/article/1746574/employees-penning-corporate-anthems-ear-splitting-results
https://36kr.com/p/3451660467902081
https://news.qq.com/rain/a/20210625A0DC7C00
https://izxxz.com/article/1159
https://forum.musicasacra.com/forum/discussion/2615/congregational-singing-range/p1
https://zgycgc.com/gequ/yinyue/15496.html
https://www.163.com/dy/article/JOF5UITC055695S7.html
https://www.aitop100.cn/tools/suno-cn
https://www.tixiaolu.com/v2/posts/v2-d56805c3.html
