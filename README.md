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
