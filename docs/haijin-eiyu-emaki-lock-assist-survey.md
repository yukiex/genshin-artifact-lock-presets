# 灰燼の都に立つ英雄の絵巻 Lock Assist 調査メモ

セット: **灰燼の都に立つ英雄の絵巻 (Scroll of the Hero Standing in the Ashen City)**

## 1. 推奨設定の根拠
- [x] `docs/reference/haijin-eiyu-emaki-lock/` に部位ごとのスクリーンショットを配置（flower / plume / sands / goblet / circlet）。
- [x] 下表に、各画像から読み取った主ステータス・サブステ条件・必須ステータスを転記。

| スロット | 画像ファイル | 主ステータス | サブステ候補 (いずれか2個) | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `スクリーンショット 2025-11-10 213033.png` | HP | 攻撃力% / 防御力% / 会心率 / 会心ダメージ / 元素熟知 / 元素チャージ効率 | 会心率 / 元素チャージ効率 |
| 羽 | `スクリーンショット 2025-11-10 213037.png` | 攻撃力 | 攻撃力% / 防御力% / 会心率 / 会心ダメージ / 元素熟知 / 元素チャージ効率 | 会心率 / 元素チャージ効率 |
| 時計 | `スクリーンショット 2025-11-10 213041.png` | 防御力% / 元素熟知 / 攻撃力% | 攻撃力% / 防御力% / 元素チャージ効率 / 元素熟知 | 元素チャージ効率 |
| 杯 | `スクリーンショット 2025-11-10 213045.png` | 攻撃力% / 炎元素DMG% / 防御力% / 岩元素DMG% / 元素熟知 | 攻撃力% / 防御力% / 元素チャージ効率 / 元素熟知 | 元素チャージ効率 |
| 冠 | `スクリーンショット 2025-11-10 213049.png` | 攻撃力% / 防御力% / 与える治療効果% / 元素熟知 | 攻撃力% / 防御力% / 元素チャージ効率 / 元素熟知 | 元素チャージ効率 |

- UIでは花・羽のみ会心率＋元素チャージ効率が黄色ハイライト、その他3部位は元素チャージ効率のみ。`substats_required_all_of` は花/羽で `[ER, CR]`、他スロットは `[ER]` とし、`substats_required_min: 2` を徹底する。
- YAML 反映時は `presets/haijin-eiyu-emaki/recommended.yml` と `presets/lock-presets.yml` の該当セクションで同期。

## 2. Custom Preset 調査

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | 夜魂反応を大量に起こすサポーター／ドライバー（シトラリ、イアンサ） | Gamerch ([gamerch.com/genshinwiki/866749](https://gamerch.com/genshinwiki/866749)) がシトラリ/イアンサを最優先候補に挙げ、「元素反応で味方の元素ダメージを上げられる」と説明。Game8 ([game8.jp/genshin/633758](https://game8.jp/genshin/633758)) でも「夜魂バースト/夜魂の加護を活かして味方全体の反応ダメージを伸ばすサポート向け」と記載。→ setting1 では ER を必須にしつつ、元素熟知を必ず含める構成で夜魂反応ドライバー向けに絞る。 |
| setting2 | 防御スケールのドライバー/バッファー（カチーナ、Xilonen など） | 神ゲー攻略 ([kamigame.jp/genshin/page/325004257587650983.html](https://kamigame.jp/genshin/page/325004257587650983.html)) で「コマちゃんのダメージは防御力依存」「厳選ステータスは防御力を重視」と明記。GameWith/神ゲー攻略のナタバッファー記事([gamewith.jp/genshin/article/show/704642](https://gamewith.jp/genshin/article/show/704642)、[kamigame.jp/genshin/page/330120947891746952.html](https://kamigame.jp/genshin/page/330120947891746952.html))でも HP/防御/チャージの3軸を推奨。→ setting2 は ER+防御% を必須にし、残りは HP% など耐久ステで埋める構成に変更。 |

> 補足: setting2 の goblet 主ステはスクショ由来の推奨プリセットと同期させるため、対象キャラが Geo（岩）であっても `PyroDMG%` を含む UI の候補リストをそのまま残している。Lock Assist 側のチェックボックス配置にズレが出ないようにする狙い。 

## 3. 作業ログ
- リント: `yamllint presets docs`
- スロット確認: `yq '.preset.slots | keys' presets/haijin-eiyu-emaki/*.yml`
- 必須サブステ確認: `yq '.preset.slots[] | select(.substats_required_min == null)' presets/haijin-eiyu-emaki/*.yml`

## 4. 反映済みファイル
- [x] `presets/haijin-eiyu-emaki/recommended.yml`
- [x] `presets/haijin-eiyu-emaki/setting1.yml`
- [x] `presets/haijin-eiyu-emaki/setting2.yml`
- [x] `presets/lock-presets.yml`
- [ ] `docs/ui-mapping.md`

## 5. 備考
- setting1/2 ともに推奨ON前提。`recommended` は常時有効、setting1/2 は追加フィルタ。
- setting1 は元素熟知＋ERを必須化し、`substats_required_min: 3` で厳しめにサポート特化。setting2 は HP%/DEF%/ER を優先する構成とする。
- 参考スクショ UID:842081775。別 UID の画像とは混在させない。
