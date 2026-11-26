# Darklands 简体中文语言包（zh-Hans）

> A Simplified Chinese (zh-Hans) language pack for **Darklands Restoration Project 1.1.4+**
> (verified against 1.1.4 and 1.1.5).
> 本仓库只含语言包，**不含任何游戏文件**；它替换文字，不改变引擎，也不改变玩法。

---

## 这是什么

《Darklands》（1992，MicroProse）的简体中文翻译，做成上游 1.1 引入的**语言包**（language pack）：

- 卡片正文、选项行、对话叙述
- 界面文本：交易 / 商店 / 拾取、客栈、炼金、人物详情、人物创建、祈祷、队伍信息、菜单栏
- 数据表名称：物品、配方、圣徒、城市字段、地点、敌人名
- 随包字体：Fusion Pixel 中文点阵字（10px / 8px），放在包的 `fonts/` 下

安装方式：把 `darklands-zh/` 整个目录放进游戏的 `packs/languages/`，然后在启动器里选中它
（或在命令行加 `--language-pack <目录>`）。**不需要改动引擎，不需要 mod。**

---

## 运行依赖

| 需要 | 说明 |
| --- | --- |
| Darklands Restoration Project **1.1.4 或更高**（已在 1.1.4 / 1.1.5 实测） | 语言包机制是 1.1 才有的；1.1.4 起卡片文本的代词变量（`var-he`、`var-his`…）与地图消息等键可用：<https://github.com/Arkana-Mechanika-Studios/darklands-restoration/releases/latest> |
| 你自己的 **Darklands 英文版**（483.07） | 例如 GOG 或 Steam 版。**本仓库不含游戏本体**，也不会提供 |

本包不含游戏文件、不含存档、不含任何来自原版的数据拷贝；所有中文都写在 `.ftl` 文本里。

---

## 安装

```text
DarklandsRP/
  packs/
    languages/
      darklands-zh/     <- 把本仓库的内容放这里
```

然后任选一种：

1. 启动 `DarklandsRP Launcher.exe`，在 Advanced 页找到语言包一行，选 **darklands-zh**；
2. 或命令行：
   ```text
   DarklandsRP.exe <你的游戏目录> --language-pack <...\packs\languages\darklands-zh>
   ```

自检（会列出语法错误、超宽文本、字体缺字）：

```text
DarklandsRP.exe --no-launcher --check-language-pack <...\packs\languages\darklands-zh>
```

---

## 目录结构

```text
darklands-zh/
  pack.json                 语言标签 zh-Hans、名称、作者、base 版本
  fonts/
    slot1.json slot2.json slot3.json   三个槽位的字号与行距
    fusion-pixel-10px-zh_hans.ttf      卡片正文 / 槽位 3
    fusion-pixel-8px-zh_hans.ttf       界面 / 槽位 1、2
    FusionPixel-LICENSE-OFL.txt        字体许可（SIL OFL 1.1）
  text/zh-Hans/
    exe.ftl                 游戏内嵌字符串（各界面）
    tables.ftl              数据表名称（物品、圣徒、城市、地点、敌人…）
    ui.ftl                  语言包自身的提示语（含货币词）
    msg/*.ftl               卡片文本（按 .MSG 文件分文件）
  interface/layout.json     按语言调整的布局（加宽盒子、增加行数）
```

---

## 字体设置

| 槽位 | 用途 | 字体 / size |
| --- | --- | --- |
| slot 1 | 侧窗、屏幕页、菜单、队伍面板 | Fusion Pixel 8px / 8 |
| slot 2 | 部分界面行 | Fusion Pixel 8px / 8 |
| slot 3 | 卡片窗口（正文、选项） | Fusion Pixel 10px / 10 |

两者都是原生网格尺寸，字形锐利不发虚。因为中文一字占一个 em 方，8px 下两个字宽 16px，
比原版拉丁文略宽；人物详情等窄列会显得挤。上游已确认该问题计划在 1.2 处理
（每槽行高 / 整列移动），见「已知缺口」。


`translations_zh.tsv` 形式的「英文串 → 中文」对照表在本项目的姊妹仓库里，语言包就是从它转换而来的。
语言包里的 `.ftl` 用的是上游的 id（`exe:DS:XXXX`、`msg:$FILE#n`、`lst:item/n.name` …），
所以它和英文原文并非逐行对应；这是语言包能跟着引擎一起更新的原因。

---

## 已知缺口

上游已在 1.1.3 修复的：圣徒 / 配方 / 城市描述（`snt:saint/n.desc`、`alc:n.desc`、`dsc:n.desc`）
现已进入 `tables.ftl`，祈祷界面、炼金书、配方页与城市卡都从语言包读取。本包已灌入中文。

仍然存在的问题：

**像素网格对齐的中文字体与固定的槽位高度冲突。** 上游三个槽位的原生高度是 7 / 8 / 9 px，
而中文一字占一个 em 方。Fusion Pixel 的原生网格是 8px / 10px，按 7px 渲染会把字形缩放到非整数网格。
人物详情面板等窄列会出现折行或挤压。上游表示该问题计划在 1.2 处理（每槽行高、整列移动），
当前临时方案是 slot 1 = 7 px + 必要处 `lines: 2`（见 `interface/layout.json`）。

此外：

- 城市描述（`dsc:`）的中文尚未翻译——原翻译表里没有这些英文串，需要新译；
- 地名与城市字段（`loc:` / `cty:`）暂保留原文（多为专有名词），敌人名（`enm:`）暂未翻译。

---

## 字体与许可

字体：**Fusion Pixel**（融合像素），由 TakWolf 发布，SIL Open Font License 1.1。
许可全文见 `fonts/FusionPixel-LICENSE-OFL.txt`。

本包的 `.ftl` 文本、布局与工具脚本以 MIT 发布（见仓库根目录 LICENSE）。
语言包与游戏引擎相互独立，不构成衍生关系。

---

## 相关链接

- 上游项目：<https://github.com/Arkana-Mechanika-Studios/darklands-restoration>
- 翻译者指南：`docs/TRANSLATING.md`（在上游发布包的 `docs/` 里）
- 语言包规范：`docs/LOCALISATION.md`
- 编辑工具 Darklands Workshop：见上游 releases

---

## 实验性专名（experimental/proper-nouns 分支）

本分支收录**尚无定译的专有名词**，供试玩与讨论；合并进 `main` 前会再校一遍。

命名原则：

1. **有通行中译的用通行译法**——如恶魔 `Rofocale` 作「罗弗寇」（中文百科既定条目）、`Bezaleel`
   作「比撒列」（《出埃及记》造会幕者）；
2. **有语源但无通行中译的，按语源意译并在此注明**——如 `Mantiphage`（希腊语 mantis+phagein）
   作「食蝗者」、`Calefactor`（拉丁语「加热者」）、「避光者」对应 `Lucifuge`；
3. **其余为音译**，拼写统一、可读即可，便于日后替换。

### 龙名（16，`exe:290E:0873..091B`）

| 英文 | 中文 | 出处 |
| --- | --- | --- |
| Enitharmon | 厄尼色芒 | 威廉·布莱克神话中的女性形象（Los 之配偶） |
| Sarcopteryx | 肉翼龙 | 希腊语 sarx（肉）+ pteryx（翼） |
| Gorgorex | 戈尔戈雷克斯 | 生造词，无文献出处 |
| Rodomont | 罗多蒙特 | 阿里奥斯托《疯狂的罗兰》中的英雄 |
| Calefactor | 加热者 | 拉丁语 calefactor |
| Vendichisme | 旺迪希斯姆 | 生造词，无文献出处 |
| Odonanga vexans | 奥多南加·威克桑斯 | 生造词，无文献出处 |
| Lucifuge | 避光者 | 《大魔法书》(Grand Grimoire) 地狱宰相之名前半 |
| Rofocale | 罗弗寇 | 《大魔法书》；通行中译见中文百科「罗弗寇」 |
| Venifer | 维尼费 | 恶魔学 Venien/Venifer 系 |
| Mantiphage | 食蝗者 | 希腊语 mantis（预言者）+ phagein（食） |
| Luveh serpens | 卢维蛇 | 拉丁化生造，serpens＝蛇 |
| Sator monitor | 萨托尔监视者 | Sator 方阵（古罗马） |
| Bezaleel | 比撒列 | 《出埃及记》31:2，造会幕的工匠 |
| Eru damnosum | 被咒之厄鲁 | 拉丁语 damnosum＝被诅咒者 |
| Baruch ophidious | 巴鲁克蛇族 | Baruch（耶利米的书记）+ ophidia（蛇类） |

来源：https://en.wikipedia.org/wiki/List_of_dragons_in_mythology_and_folklore ；
Lucifuge Rofocale 诸资料（Grand Grimoire / Goetia 研究）。

### 矮人名（38，`exe:290E:092C..0A25`）

均出自《女巫预言》（Völuspá）的 Dvergatal（矮人名录）或《散文埃达》，个别为 MicroProse 自拟。

| 英文 | 中文 | 出处 |
| --- | --- | --- |
| Alveig | 阿尔薇格 | 埃达系女性名 Alvǫr |
| Angerboda | 安格尔波达 | Angrboða，芬里尔与海拉之母 |
| Asmund | 阿斯蒙德 | Ásmundr |
| Bikke | 比克 | — |
| Brok | 布洛克 | Brokkr，与辛德里同为铁匠 |
| Dromi | 德罗米 | — |
| Dvalin | 德瓦林 | Dvalinn，矮人首领（「沉睡者」） |
| Egil | 埃吉尔 | Egill |
| Egther | 埃格瑟 | — |
| Fyalar | 菲亚拉 | Fjalar |
| Gelgya | 盖尔吉亚 | — |
| Grep | 格雷普 | Grer/Grep |
| Groa | 格罗亚 | Gróa，女先知 |
| Gudhorm | 古德霍姆 | — |
| Gulveig | 古尔薇格 | Gullveig |
| Gymer | 吉梅尔 | — |
| Gyoll | 焦尔 | — |
| Hadding | 哈丁 | — |
| Hardgrep | 哈德格雷普 | — |
| Honer | 霍纳尔 | Hœnir |
| Hother | 霍特尔 | Hǫðr |
| Leding | 莱丁 | — |
| Managarm | 玛纳加尔姆 | Mánagarmr，逐月之犬 |
| Mimer | 密米尔 | Mímir，智慧之泉守护者 |
| Mimingus | 米明古斯 | Mimingr，海姆达尔之号角 |
| Morn | 莫尔恩 | — |
| Narve | 纳尔维 | — |
| Nidhad | 尼德哈德 | Niði／Níðhöggr 一系 |
| Ope | 奥佩 | — |
| Orvandel | 奥尔万德尔 | — |
| Sindre | 辛德里 | Sindri，与布洛克同为铁匠 |
| Skade | 丝卡蒂 | Skaði |
| Suttung | 苏图恩 | Suttungr，诗蜜酒守护者 |
| Thyasse | 蒂亚瑟 | Þjazi |
| Thviti | 斯维提 | — |
| Tope | 托佩 | — |
| Ull | 乌尔 | Ullr |
| Volund | 沃尔隆德 | Vǫlundr，即「铁匠韦兰」 |

来源：Dvergatal 原文 https://glaemscrafu.jrrvf.com/english/dvergatal.html ；
名录 https://en.wikipedia.org/wiki/List_of_dwarfs_in_Norse_mythology

> 注：这些名字里的一部分（如 Alveig、Gudhorm、Thviti 等）在中文出版物中没有固定译法，
> 本表按统一音译规则处理；一旦出现更通用的中译，直接替换即可。

### 地名（414，`exe:290E:0x????` / `tables.ftl` 的 `loc:<n>.name`）

全部按**通行中文地名译法**处理：真实存在的城市与地区用中国地图出版社《世界地名译名词典》及
中文维基条目的通行名；村落、山地、荒野地点按德语/捷克语地名的通行音译规则处理。

**原文拼写残缺的条目**（原版数据文件里的字符串本身就是截断的，不是本包的错误）：

| 包内英文 | 通译依据 | 中文 |
| --- | --- | --- |
| `Vordingbrd` | Vordingborg（丹麦维堡） | 维堡 |
| `Naskskov` | Nykøbing（尼克宾） | 尼克宾 |
| `Braunschwg` | Braunschweig | 不伦瑞克 |
| `Duisberg` | Duisburg | 杜伊斯堡 |
| `Brandenbrg` | Brandenburg | 勃兰登堡 |
| `Fürstenbrg` | Fürstenberg | 菲尔斯滕贝格 |
| `Recklinghsn` | Reckhausen | 雷克灵豪森 |
| `Aschaffen` | Aschaffenburg | 阿沙芬堡 |

**简写标记**（原版为避免重名而加的后缀，保留其含义）：

- `Frankfurt O` / `Frankfurt M` → 「法兰克福（奥得河）」/「法兰克福（美因河）」
- `South Nürn` / `North Nürn` → 「纽伦堡南区」/「纽伦堡北区」

**荒野地点**为同一类型的重复地名，统一译法：`Spring`→泉水、`Lake`→湖泊、
`Cave`→洞穴、`Shrine`→神龛、`Tomb`→陵墓、`Pagan Altar`→异教祭坛、
`Lair`→龙穴、`Alpine Cave`→高山洞穴。

**网络核查记录（2026-11-26）**：地名定稿后逐条对照中文维基条目与百度百科词条复查，
一处错误已改：`Vordingbrd`（原按 Viborg 作「维堡」）应为丹麦 **沃尔丁堡**（Vordingborg），
以中文维基条目为准。其余条目均有对应条目或为同一地名的不同拼写，予以保留。

未能查到独立中文条目的条目（多为千人以下的小镇、山林荒野地点）按其德语/捷克语/丹麦语
词源音译，并在上表注明原文拼写；若日后出现权威译法，直接替换即可。

### 城市字段（1562，`tables.ftl` 的 `cty:<n>.*`）

每个城市 18 个字段（`short`/`full`/统治者/各建筑名），去重后只有 480 个不同英文值，其中
393 处是空占位 `{" "}`（该城没有此建筑），保持原样。其余词条按下列原则处理：

- **统治者与教长**用通行封号：「汉萨同盟」「条顿骑士团」「波希米亚国王」「迈森藩侯」
  「科隆大主教」「明斯特亲王主教」等；
- **公共建筑**用中文通名：「市政广场」「集市广场」「老市场」「军械库」「贫民区」「修道院」
  「大教堂」「城堡」「宫殿」；
- **市场名**按构成词直译：「鱼市」「牲畜市场」「乳市场」「铸币广场」「市政厅酒窖」；
- **旅馆、酒馆、城门**按德语专名音译或意译：「金狮旅馆」「熊旅馆」「黑门」「制烛匠门」
  「铁塔楼」「女巫塔楼」；
- **堂区教堂**统一为「圣X教堂」（如 `St.Marienkirche`→圣玛利亚教堂）。

原文同样存在拼写残缺（`Vordingbord`、`Naskskov`、`Lüneberg`、`Duisberg`），
与地名一节同法处理：按真实地名取通译。

## 译名依据与核查

本包所有专有名词都先查中文既有译法，按三级处理：**①有通行中译的用通行译法**；
**②无大众通行但有小众／学术出处的，用该出处的译法**（下表）；**③都没有的才音译**，
并在表中写明原文拼写。

### 封号与机构（对照中文维基条目名）

| 英文 | 中文 | 依据 |
| --- | --- | --- |
| Hanseatic League | 汉萨同盟 | 中文维基 / 《中国大百科全书》第2版主条目名 |
| Teutonic Knights | 条顿骑士团 | 通行译名 |
| Hussites | 胡斯派 | 通行译名（胡斯运动） |
| Margrave | 藩侯 | 中文维基「藩侯」为主条目，另译方伯、边境伯爵 |
| Landgrave | 方伯 | 中文维基「方伯」（德国节：领地伯爵 Landgraf） |
| Count Palatine | 行宫伯爵 | Pfalzgraf，中文维基作「行宮伯爵」，与藩侯、方伯同级 |
| Prince-Bishop | **采邑主教** | 中文维基主条目名（或译王公主教、亲王主教） |
| Prince-Abbot | **采邑隐修院院长** | 通行译名，德文 Fürstabt |
| Archbishop / Bishop | 大主教 / 主教 | 通行译名 |
| Swiss Confederation | 瑞士联邦 | 通行译名 |

> 初版曾把 `Prince-Bishop` 译作「亲王主教」、`Prince-Abbot` 译作「亲王院长」，
> 网络核查后按中文维基主条目改为「采邑主教」「采邑隐修院院长」。

### 地名（部分）

- `Vordingborg` → **沃尔丁堡**（初版误作「维堡」，那是 Viborg；已按中文维基条目改正）
- `Nykøbing` → **尼克宾**（Naskskov 为原数据截断拼写）
- `Frankfurt an der Oder` / `am Main` → 法兰克福（奥得河）/（美因河），以区分两地
- 哈茨山、布罗肯山、瓦茨曼山等山地按中国地图出版社《世界地名译名词典》的写法

### 龙名与矮人名

见上方两节的两张表：通行译法（如 `Rofocale`→罗弗寇、`Bezaleel`→比撒列、
`Mimer`→密米尔）注明来源；其余为音译并标出原文拼写，便于日后替换。

### 职业名

全部依据官方 *Darklands Clue Book*（1992，MicroProse）OCCUPATION QUALIFICATIONS 一节：
`Schulz` 原文要求「须先为农民且历任军职/神职」，故取「村长」而非音译「舒尔茨」；
`Oblate` 为「在修道院学习者」，取「见习修士」。

### 人名（角色生成器的三张表，`exe:290E:1171..1D19`）

- **男名（108）、女名（88）**：历史上真实存在的德语人名。有通行中译的用通行
  （`Otto→奥托`、`Heinrich→海因里希`、`Friedrich→弗里德里希`、`Wolfgang→沃尔夫冈`、
  `Katherine→凯瑟琳`、`Maria→玛利亚`），其余按统一音译。
  北欧神话来源的名字沿用中文既有译法（`Freyja→芙蕾雅`、`Brünnhilde→布伦希尔德`、
  `Siegfried→齐格弗里德`、`Gudrun→古德龙`）。
- **姓氏（144）**：按《世界人名翻译大辞典》的音译规则处理；有通行中译的用通行
  （`Goethe→歌德`、`Luther→路德`、`Kepler→开普勒`、`Müller→米勒`、`Schmidt→施密特`）。
- **贵族氏号（42 条 `of X`）**：译作「X 的」，地名部分复用 `loc` 一节的地名译法。

> 说明：这些人名在原数据里是随机生成器的素材，没有官方中文版本，因此本包只保证拼写统一、
> 读音可还原，不宣称是唯一正确的译法。
