---
title: サンプル記事 - タイトル
date: 2021-01-01 12:00:00
tags:
  - Information
  - Example
disableDisclaimer: false
---

記事概要

<!-- more -->

記事本文

<!-- 文字修飾 -->

**太字**

~~訂正せん~~

*斜め文字*

<!-- 引用 -->

> 引用
>> 引用

<!-- 見出し -->

## 見出し (大)
### 見出し (中)
#### 見出し (小)

<!-- リスト -->

- リスト
   - リスト
   - リスト
- リスト

<!-- 数字リスト -->

1. 数字リスト
   1. 数字リスト
   2. 数字リスト
2. 数字リスト
3. 数字リスト

<!-- 区切り線 -->

---

<!-- リンク -->

[Japan Azure IaaS Core Support Blog](https://jpaztech.github.io/blog/)

<!-- 画像 (リポジトリ内ファイルを参照 -->

![](./example/example01.png)

<!-- 画像 (外部 URL を参照) -->

![](https://jpaztech.github.io/blog/vm/re-install-windows-azure-guest-agent/service.png)

<!-- コード ブロック -->

```CMD
net stop rdagent
net stop WindowsAzureGuestAgent
net stop WindowsAzureTelemetryService
```

<!-- 表 -->

| 見出し | 見出し |
| ---- | ---- |
| セル | セル |
| セル | セル |

<!-- ノート -->

> [!NOTE]
> THIS IS NOTE
> `[!NOTE]` と書くと `Note` になります。
> これだけ MS 公式ドキュメントと異なります。 (公式ドキュメントだと `NOTE` も `注意` に変換される…)

<!-- ヒント -->

> [!TIP]
> THIS IS TIP
> `[!TIP]` とかくと `ヒント` になります。

<!-- 重要 -->

> [!IMPORTANT]
> THIS IS IMPORTANT
> `[!IMPORTANT]` とかくと `重要` になります。

<!-- 注意事項 -->

> [!CAUTION]
> THIS IS CAUTION
> `[!CAUTION]` と書くと `注意事項` になります。

<!-- 注意 -->

> [!WARNING]
> THIS IS WARNING
> `[!WARNING]` と書くと `警告` になります。

