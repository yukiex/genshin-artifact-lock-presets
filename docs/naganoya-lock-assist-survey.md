# Naganoya Lock Assist 調査メモ

セット: **長き夜の誓い (Song of Days Past)**

## 1. 推奨設定の根拠
- [ ] `docs/reference/naganoya-lock/` に部位ごとのスクリーンショットを配置（flower / plume / sands / goblet / circlet）。
- [ ] 下表に、各画像から読み取った主ステータス・サブステ条件・必須ステータスを転記。

| スロット | 画像ファイル | 主ステータス | サブステ候補 (いずれか2個) | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `スクリーンショット 2025-11-09 222122.png` | HP | 攻撃力% / 会心率 / 会心ダメージ | 会心率, 会心ダメージ |
| 羽 | `スクリーンショット 2025-11-09 222127.png` | 攻撃力 | 攻撃力% / 会心率 / 会心ダメージ | 会心率, 会心ダメージ |
| 時計 | `スクリーンショット 2025-11-09 222131.png` | 攻撃力% | 会心率 / 会心ダメージ | 会心率, 会心ダメージ |
| 杯 | `スクリーンショット 2025-11-09 222136.png` | 炎元素ダメージ / 雷元素ダメージ / 風元素ダメージ / 攻撃力% | 攻撃力% / 会心率 / 会心ダメージ | 会心率, 会心ダメージ |
| 冠 | `スクリーンショット 2025-11-09 222141.png` | 会心率 / 会心ダメージ | 攻撃力% / 会心率 / 会心ダメージ | 会心率, 会心ダメージ |

- YAML 反映時は `presets/naganoya/recommended.yml` と `presets/lock-presets.yml` の両方を更新する。

## 2. Custom Preset 調査
- `setting1` / `setting2` は厳しさではなく**異なるキャラクタータイプ**を表す。攻略サイト・ビルドガイドなど、根拠となる URL とポイントを以下に整理する。

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | 落下攻撃メインのアタッカー（魈・嘉明・ヴァレサ） | Game8 は「落下攻撃主体のアタッカーと相性が良い」として魈/嘉明/ヴァレサを挙げ、スタック維持の立ち回り例を掲載 ([game8.jp/genshin/676659#hl_4](https://game8.jp/genshin/676659#hl_4))。Gamerch も同3名を最適キャラに記載し、落下攻撃・重撃・元素スキルでスタックを稼ぐ運用を推奨 ([gamerch.com/genshinwiki/910745](https://gamerch.com/genshinwiki/910745))。→ 会心2種＋攻撃%を軸に、砂はATK%固定、杯は対応元素/ATK%。 |
| setting2 | 閑雲サポート込みの疑似落下アタッカー（フリーナ、ナヴィア等） | Game8 は閑雲の元素爆発で任意キャラに落下攻撃手段を付与でき、長き夜でバフを乗せられると解説 ([game8.jp/genshin/676659#hl_2](https://game8.jp/genshin/676659#hl_2))。神ゲー攻略でも「落下攻撃の火力上昇に最適」「重撃/スキルで層を刻む」と言及 ([kamigame.jp/genshin/page/360583686942375503.html](https://kamigame.jp/genshin/page/360583686942375503.html))。→ 通常は落下攻撃を持たないキャラ（フリーナ、ナヴィアなど）を閑雲でジャンプ強化し、会心＋攻撃%の良品を確保。 |

## 3. 作業ログ
- リント: `yamllint presets docs`
- スロット確認: `yq '.preset.slots | keys' presets/naganoya/*.yml`
- 必須サブステ確認: `yq '.preset.slots[] | select(.substats_required_min == null)' presets/naganoya/*.yml`
