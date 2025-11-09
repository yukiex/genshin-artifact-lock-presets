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
