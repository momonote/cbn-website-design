---
name: TG内容运营内容输出
description: TG 频道公告文本生产 skill。为公司三产品（Turbo VPN / VPN Proxy Master / 机场=Turbo Secure Proxy）的 Telegram 频道生成公告文案：输入品牌与分区（P1–P9）→ 按《品牌公告要求》读 COMMON + BRAND[Bx] + P{n} 三块 → 产出英文母版 → 人工审核硬门控 → 多语言译版 → 输出公告文本包（master.md + 各语言 .md + manifest.json）。This skill should be used when the user asks to 写/生成/改写/迭代 Turbo VPN、VPN Proxy Master 或机场（Turbo Secure Proxy）的 Telegram 频道公告、品牌公告文案（版本更新或营销场景）。只产文本，不执行 Telegram 发送与定时（归 tg-publish）。
agent_created: true
---

# TG内容运营内容输出 · TG 频道公告文本生产

## 目的与范围

为公司三个产品的 Telegram 频道生产公告文案。三品牌 × 三场景 = 9 分区（P1–P9），各分区格式要求独立维护、互不套用。本 skill 只产文本：不产图片、不执行 Telegram 发送与定时（发布归 `tg-publish`）。

## 输入契约

开始前确认三项；缺任一项时一次性向用户问齐，不逐项追问：

| 项 | 取值 |
|---|---|
| 品牌 | B1 VPN Proxy Master / B2 Turbo VPN / B3 Turbo Secure Proxy（机场） |
| 分区 | P1–P9（品牌 × 场景，索引见 `references/announcement-formats.md` 分区索引表） |
| 素材 | 更新类分区 → changelog（版本号 · 平台 · 生效时间）；营销类分区 → 活动链接 |

用户只说"写个更新公告"未指明品牌时，先确认品牌与分区再动笔。

## 流程

1. **读格式要求**：读 `references/announcement-formats.md`，只取三块——`COMMON`（通用硬规则）+ `BRAND[Bx]`（该品牌核心）+ `P{n}`（该分区模版与示例）。无需读全文。
   - **两条格式硬规则，母版阶段就要落到位（2026-10-14 用户校正）**：
     - **标题一律加粗**：写成 `{Emoji} **标题文字**`，**不存在「单行标题不加粗」的例外**。各分区示例标题已同步改为加粗形态，不得再照旧示例写成不加粗单行。
     - **标题或第一段必须点明主题**：节日 / 活动 / 事件关键词（如 `Christmas` / `Рождество` / 版本号 / 赛事名）必须出现在标题或首段，且在前三段之内出现。标题允许小卖关子，但卖关子只能挂在非主题成分上，不得把主题词整个省掉。
   - **其余粗体落位**：`✔` 能力小标、排障/连接指引的每步关键动作、`💬` 补充句的关键动作均须 `**…**`；正文、促销句与 footer 不加粗。规范里给的是硬要求，不是可选项——漏一处即返工。
   - 译版必须**逐处对齐母版的加粗位置**，不因语序调整而丢失。
2. **定语言**：输出语言按 md 的规定——B1 = EN；B2 = EN / RU / PT-BR / ES（按发布频道适配）；B3 = RU（发布）+ EN（审核对照）。发布频道清单见 `references/channels.md`；两份依据的出入以 md 为准。
3. **产英文母版**：markdown、可复制超链接、方便审阅的纯文本；B3 按双段交付【Review English】+【Russian Release】。送审前对照第 1 步的两条格式硬规则自查一遍——**标题是否已加粗**、**标题或首段是否点明主题**。
4. **人工审核母版（硬门控）**：暂停并交付母版等用户审核；按指令返工后重新送审；未通过不得进入下一步。
5. **产对应语言版本**：母版通过后逐语言产出；各语言必须与最终通过的母版版本一致，母版返工后译版全部同步重做。
6. **输出公告文本包**：按下方输出约定落盘文件夹 + manifest。
7. **附配图分类**：在 manifest 标注该公告的配图分类，供发布侧从固定素材库取图（本 skill 不产图）。

## 输出约定

每次公告一个文件夹：

```
announcements/YYYY-MM-DD-品牌-分区/
├── master.md        英文母版
├── <语言>.md        各语言版本
└── manifest.json    品牌 / 语言 / 分区（P1–P9）/ 版本 / 配图分类 / 消息链接（发布后由 tg-publish 回填）
```

## 边界

- 只产文本；图片来自固定素材库，按 manifest 的配图分类由 agent bot 取用。
- 每次发布记录留档（由发布侧执行，manifest 预留字段）。
- 多产品同时更新：各自独立公告，不合并。
- B2 公关套话禁用、B1/B2/B3 词库与署名 footer 等细节全部以 `references/announcement-formats.md` 为准，不在本文件重复。

## 分工

| skill | 职责 |
|---|---|
| TG内容运营内容输出（本 skill） | 文本生产 |
| tg-publish | 接入 Telegram → 定时 2 天后（防草稿误发送）→ 人工审核各频道公告 → 发布 → 回读消息链接回填 manifest |
