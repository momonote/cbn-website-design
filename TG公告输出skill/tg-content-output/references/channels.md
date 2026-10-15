# 品牌 × 语言 × 频道 × Bot 映射

> 发布频道清单（**2026-10-14 经用户校正**）。输出语言规则以 `announcement-formats.md` 的 COMMON 为准。
> **语言口径已校正（2026-10-14）**：B2 = EN / RU / PT-BR / ES / FA，B1 = EN / RU，B3 = RU 发布 + EN 对照。全品牌**无印尼语（ID）频道**。

| 品牌 | 语言 | 频道数 | Bot |
|---|---|---|---|
| B2 Turbo VPN | EN · RU · BR(PT-BR) · ES · FA | 5 | 专属 Bot（username 待补） |
| B1 VPN Proxy Master | EN · RU | 2 | 专属 Bot（username 待补） |
| B3 Turbo Secure Proxy（机场） | RU（发布）+ EN（审核对照） | 2 | @TurboSecureProxyBot |

共 9 个频道；一个品牌一个 Bot（各自独立 token）。

## 已知频道（来源：《品牌公告要求》B3 固定 footer）

- 频道：@TurboProxyVpn
- Bot：@TurboSecureProxyBot
- 客服/支持：@TurboSafeGuard

## 待补清单

| 项 | 用途 | 补法 |
|---|---|---|
| Turbo VPN / VPN Proxy Master 的频道 username | 定向发布 | 用户提供后填入本表 |
| 各频道 chat_id | tg-publish 定向发布 | 发布阶段用 Bot API getChat 按 username 解析，无需手工整理 |
| 三个 bot 的 token | tg-publish 发送凭据 | 只进 tg-publish 的环境变量/凭据管理，不写入任何文件 |

## 备注

- FA（伊朗波斯语）**仅 B2 Turbo VPN 有频道**，B1 / B3 不出 FA 版本。
- 旧版本记载的「B1 仅 EN」「B2 无 FA」等出入已按2026-10-14 校正结果统一：本文档与 `announcement-formats.md` 语言口径一致，任一侧新增或修改语种时须同步更新另一侧。