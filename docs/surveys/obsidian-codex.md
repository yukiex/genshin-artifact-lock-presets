# 黒曜の秘典 Lock Assist 調査メモ

セット: **黒曜の秘典 (Obsidian Codex)**

## 1. 推奨設定の根拠
- [x] `docs/references/obsidian-codex/` に部位ごとのスクリーンショットを配置（flower / plume / sands / goblet / circlet）。
- [x] 下表に、各画像から読み取った主ステータス・サブステ条件・必須ステータスを転記。

| スロット | 画像ファイル | 主ステータス | サブステ候補 (いずれか2個) | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `flower.png` | HP | HP% / 攻撃力% / 元素熟知 / 会心率 / 会心ダメージ | 会心率 / 会心ダメージ |
| 羽 | `plume.png` | 攻撃力 | HP% / 攻撃力% / 元素熟知 / 会心率 / 会心ダメージ | 会心率 / 会心ダメージ |
| 時計 | `sands.png` | HP% / 元素熟知 / 攻撃力% | HP% / 攻撃力% / 会心率 / 会心ダメージ / 元素熟知 | 会心率 / 会心ダメージ |
| 杯 | `goblet.png` | 炎元素DMG% / 水元素DMG% / 草元素DMG% / 攻撃力% | HP% / 攻撃力% / 会心率 / 会心ダメージ / 元素熟知 | 会心率 / 会心ダメージ |
| 冠 | `circlet.png` | 会心率 / 会心ダメージ | HP% / 攻撃力% / 元素熟知 / 会心率 / 会心ダメージ | 会心率 / 会心ダメージ |

- YAML 反映時は `presets/obsidian-codex/recommended.yml`を更新する。
- UI では全スロットで会心率 / 会心ダメージが黄色ハイライト。`substats_required_all_of: [CR, CD]` を全スロットに設定する。
- Game8のおすすめキャラ表([game8.jp/genshin/633756](https://game8.jp/genshin/633756))では **マーヴィカ / ムアラニ / キィニチ / シロネン / チャスカ / ヴァレサ** が推奨と明記。`targets` はこの6名をすべて含むよう更新済み。

## 2. Custom Preset 調査

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | 夜魂値を消費して張り付き火力を出すオンフィールドメイン（ムアラニ、キィニチ、チャスカ、マーヴィカ、ヴァレサなど） | Gamerch 解説([gamerch.com/genshinwiki/866745](https://gamerch.com/genshinwiki/866745))がムアラニ/キィニチ/チャスカを最推薦キャラに挙げ、会心40%バフを活かした常時オンフィールド運用を推奨。GameWith ([gamewith.jp/genshin/article/show/704641](https://gamewith.jp/genshin/article/show/704641)) でも夜魂値を自前で消費し続けられるメインアタッカーへの適性を強調。さらに Game8 ([game8.jp/genshin/633756](https://game8.jp/genshin/633756)) でマーヴィカ/ヴァレサが推奨キャラに含まれていたため `targets` へ追記。→ 会心2種＋攻撃%を厳しめに要求し、サブステにHP%は含めない構成でクリ系を優先。 |
| setting2 | サブ火力・オフフィールド寄りの夜魂サポート/ドライバー（防御/HPスケール支援、元素反応特化） | 神ゲー攻略 ([kamigame.jp/genshin/page/330119898476862343.html](https://kamigame.jp/genshin/page/330119898476862343.html)) で「控え攻撃不可なのでメインアタッカー以外には向きづらい」としつつ、今後の夜魂サポーター想定で防御%やHP%を要求する記述あり。Game8 も「サブ火力は会心バフを活かしにくい」と注意喚起([game8.jp/genshin/633756](https://game8.jp/genshin/633756))。→ setting2 は会心1本＋耐久ステ/元素チャージを重視し、HP/防御スケールのサブアタ向けフィルタにする。 |

## 3. 作業ログ
- リント: `yamllint presets docs`
- スロット確認: `yq '.preset.slots | keys' presets/obsidian-codex/*.yml`
- 必須サブステ確認: `yq '.preset.slots[] | select(.substats_required_min == null)' presets/obsidian-codex/*.yml`

## 4. 反映済みファイル
- [x] `presets/obsidian-codex/recommended.yml`
- [x] `presets/obsidian-codex/setting1.yml`
- [x] `presets/obsidian-codex/setting2.yml`
- [ ] `docs/ui-mapping.md`

## 5. 備考
- setting1/2 は推奨On前提の追加フィルタ。UI上は推奨設定のトグルを維持しつつ設定1/2を有効化する前提で YAML も `recommended` を親とした構成にする。
- setting1 では会心2種＋攻撃%を最低3枠に指定し、夜魂値消費のメインアタが即ロックされるよう `substats_required_min: 3`。設定2は ER/HP%/DEF% を混ぜた耐久寄り構成を想定。
- 参考スクショは UID:842081775 の推奨画面。別 UID のサンプルを混用しないよう注意。
