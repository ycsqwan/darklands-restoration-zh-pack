# Darklands 简体中文语言包（zh-Hans）

> A Simplified Chinese (zh-Hans) language pack for **Darklands Restoration Project 1.1+**.
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
| Darklands Restoration Project **1.1 或更高** | 语言包机制是 1.1 才有的：<https://github.com/Arkana-Mechanika-Studios/darklands-restoration/releases/latest> |
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

## 翻译表

`translations_zh.tsv` 形式的「英文串 → 中文」对照表在本项目的姊妹仓库里，语言包就是从它转换而来的。
语言包里的 `.ftl` 用的是上游的 id（`exe:DS:XXXX`、`msg:$FILE#n`、`lst:item/n.name` …），
所以它和英文原文并非逐行对应；这是语言包能跟着引擎一起更新的原因。

---

## 已知缺口

以下两类问题**出在上游引擎，不是本包能解决的**，已在 GitHub 向上游说明：

1. **数据文件里的长描述没有进入翻译模板。**
   圣徒描述（`DARKLAND.SNT`）、炼金配方描述（`DARKLAND.ALC`）等在
   `SaintPrayerScreen.cs:380`、`AlchemyScreen.cs:144`/`:242` 处被直接读取原始字节绘制，
   不经过 `ui.Words(id)`，因此语言包无 id 可用。目前这些位置仍是英文。

2. **像素网格对齐的中文字体与固定的槽位高度冲突。**
   上游三个槽位的原生高度是 7 / 8 / 9 px，而中文一字占一个 em 方。Fusion Pixel 的原生网格是
   8px / 10px，按 7px 渲染会把字形缩放到非整数网格。人物详情面板等窄列会出现折行或挤压。
   `interface/layout.json` 能缓解个别位置，但无法解决多个文本共用窄面板的情形。

此外，地名与城市字段（`loc:` / `cty:`）暂保留原文（多为专有名词），敌人名（`enm:`）暂未翻译。

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
