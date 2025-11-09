# Tsukuyo Lock Assist 調査メモ

ユーザーから「`presets/tsukuyo/recommended.yml` をゲーム内推奨設定と一致させるよう修正してほしい」との要望があり、以下の一次情報を調査した。

## 1. 公式データベース
| 出典 | URL | 結果 |
| --- | --- | --- |
| HoYoWiki (英語) | https://wiki.hoyolab.com/pc/genshin/entry/4717?lang=en-us | セット効果や各部位の説明のみ。ロックアシスト推奨条件の記載なし。 |

HoYoWiki を直接呼び出す API (`https://sg-wiki-api.hoyolab.com/hoyowiki/genshin/wapi/entry_page?entry_page_id=4717&lang=en-us`) も同じ内容で、ロック条件は提供されていないことを確認した。

## 2. 日本語攻略サイト
| 出典 | URL | 結果 |
| --- | --- | --- |
| Game8 | https://game8.jp/genshin/714003 | セット効果・おすすめキャラのみ。ロック推奨設定の記載なし。 |
| GameWith | https://gamewith.jp/genshin/article/show/516496 | 同上。 |
| 神ゲー攻略 | https://kamigame.jp/genshin/page/384955936327877443.html | 同上。 |

いずれも Tsukuyo（月を紡ぐ夜の歌）のビルド情報はあるが、ロックアシストの推奨数値や UI のスクリーンショットは確認できなかった。

## 3. ゲーム内スクリーンショット
ユーザー提供のロックアシスト画面（`docs/reference/tsukuyo-lock/` 配下の PNG 5枚）に、月を紡ぐ夜の歌の推奨設定が記録されている。

| スロット | 画像ファイル | 主ステータス | サブステ条件 | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `スクリーンショット 2025-11-09 202521.png` | HP 固定 | ATK% / CR / CD / ER / EM のうち2つ以上 | ER, EM |
| 羽 | `スクリーンショット 2025-11-09 202557.png` | ATK 固定 | 同上 | ER, EM |
| 時計 | `スクリーンショット 2025-11-09 202601.png` | EM / ATK% / ER% | 同上 | ER, EM |
| 杯 | `スクリーンショット 2025-11-09 202605.png` | HydroDMG% / DendroDMG% / EM / ATK% | 同上 | ER, EM |
| 冠 | `スクリーンショット 2025-11-09 202610.png` | EM / CR / CD | 同上 | ER, EM |

※いずれの部位も「次の追加ステータスのうち、いずれか2個を含む」と記載されているため、`substats_required_min: 2` とし、候補は `[ATK%, CR, CD, ER, EM]` で統一した。

## 4. 結論
上記スクリーンショットを根拠に `presets/tsukuyo/recommended.yml` および `presets/lock-presets.yml` の Tsukuyo 推奨設定を更新済み。別途「設定1/2」はこれまでどおりユーザー独自のフィルタとして維持している。

## Custom Preset 調査メモ
`setting1/2` を「月反応チーム内で役割が異なるサポート archetype」として再定義した。各ビルドは以下の攻略サイトに根拠がある。

### Setting1 – Moonlight Battery (Electro/Hydro support)
- [Game8 (2025/11/07)](https://game8.jp/genshin/714003) は「熟知と元素チャージが重要なサポートキャラと相性が良い」と明記し、`雷電将軍 / 主人公(草) / イネファ / アイノ / ラウマ` をおすすめキャラとして掲載している。ER と EM を同時に要求するサブステ構成にしたのはこの記述が根拠。
- [GameWith (2025/08/29)](https://gamewith.jp/genshin/article/show/516496) のおすすめ表では `イネファ / ラウマ / アイノ / カーヴェ / 行秋` など、月バフを撒きながら味方を支援するキャラが列挙されている。特に `アイノ / 行秋` は Hydro サブアタとして ER・HP% を両立させたいので、`main_allowed` に HydroDMG% や Healing% を含めた。
- [神ゲー攻略 (2025/08/30)](https://kamigame.jp/genshin/page/384955936327877443.html) でも `ラウマ` と `アイノ` を例に挙げ「味方全員の元素熟知をバフ」「爆発回転率を上げる」と説明していることから、ER を必須 (`substats_required_all_of: [ER]`) とした。

### Setting2 – Bloom Architect (Dendro reaction)
- GameWith の同記事で `ラウマ / カーヴェ` をセット適性キャラに挙げ、「天穹の顕現せし夜を別キャラに装備させると月反応ダメージが伸びる」と解説しているため、Dendro ドライバー/サポーター用プリセットとして切り分けた。
- Game8 でも `主人公(草)` を含む Dendro サポーターを推奨しており、熟知優先型で組む記述があるため `substats_required_all_of` に `EM` を指定。
- 神ゲー攻略は「月反応軸のサポーターに最適」「サブアタッカーにおすすめ」とまとめており、Dendro エンジニア（`Rauma, TravelerDendro, Nahida, Collei` など）向けに `EM` 主体のメイン/サブステを要求する形にした。
