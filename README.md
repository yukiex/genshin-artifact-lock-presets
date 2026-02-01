# Genshin Artifact Lock Presets
原神「自動ロック（ロックアシスト）」向けに整形した YAML プリセット集です。  
`substats_required_any_of`＋`substats_required_min` だけで **「いずれか N 個以上」**条件を再現し、`main_allowed` をヒントとして添えることで誤ロックを防ぎます。

> 現在の収録セット
> - **月を紡ぐ夜の歌 / Moonweaver**: 支援・オフフィールド向け、ER/EM の拾い漏れ防止
> - **天穹の顕現せし夜 / Night of the Sky**: オンフィールド DPS 向け、会心サブ重視
> - **深廊の終曲 / Finale of the Deep**: 氷アタッカー（スカーク想定）向けのゼロエネルギー特化セット
> - **長き夜の誓い / Song of Days Past**: 落下攻撃系アタッカー＋閑雲サポート向けセット
> - **黒曜の秘典 / Obsidian Codex**: Nightsoul バフを活かすオンフィールド会心特化（ムアラニ/キィニチ/チャスカ等）
> - **灰燼の都に立つ英雄の絵巻 / Ashen Hero Scroll**: Citlali/Iansan/Kachina 向けの ER+DEF サポーター＆バッファー
> - **大地を流浪する楽団 / Wanderer's Troupe**: 弓/法器重撃アタッカー向け、会心＋熟知の両対応

---

## Highlights
- 1セットにつきゲーム内推奨 (`recommended`) と、用途別にチューニングした `setting1` / `setting2`（キャラクターアーキタイプ向けカスタム）を提供
- UI と YAML の対応は [`docs/ui-mapping.md`](./docs/ui-mapping.md) に表形式で整理
- `presets/lock-presets.yml` はすべてのセットを 1 ファイルにまとめた「配布用カタログ」

---

## Preset Catalog
| Set ID | 日本語名 | 目的 / Intent | サンプル用途 |
| --- | --- | --- | --- |
| `tsukuyo` | 月を紡ぐ夜の歌 | `support_offfield` | 付着役 / ヒーラー向けに ER/EM を広く確保 |
| `tenkyu` | 天穹の顕現せし夜 | `onfield_dps` | 会心系サブが揃ったダメージ用候補の確保 |
| `shinro` | 深廊の終曲 | `onfield_dps` | スカーク/マーヴィカなど氷メインDPSの会心確保 |
| `naganoya` | 長き夜の誓い | `onfield_plunge` | 魈/嘉明/ヴァレサの落下攻撃特化ビルド |
| `kokuyo-hiten` | 黒曜の秘典 | `onfield_dps` | Nightsoul 会心バフを活かすオンフィールドキャリー |
| `haijin-eiyu-emaki` | 灰燼の都に立つ英雄の絵巻 | `support_reaction` | Citlali/Iansan/Kachina の ER+耐久サポート |
| `wanderers-troupe` | 大地を流浪する楽団 | `onfield_dps` | 弓/法器の重撃アタッカー向け会心/熟知 |

各プリセットの想定キャラは YAML の `targets` を参照してください（ロック判定には影響しません）。

---

## Repository Layout
```text
genshin-artifact-lock-presets/
├─ README.md               # このガイド
├─ AGENTS.md               # 貢献ルール（コマンド付き）
├─ docs/
│  ├─ ui-mapping.md        # UI と YAML の対応表
│  ├─ lock-assist-survey-template.md  # 証跡メモの雛形
│  ├─ haijin-eiyu-emaki-lock-assist-survey.md
│  ├─ kokuyo-hiten-lock-assist-survey.md
│  └─ reference/
│        ├─ haijin-eiyu-emaki-lock/*.png
│        └─ kokuyo-hiten-lock/*.png
└─ presets/
   ├─ lock-presets.yml     # 配布用の結合ファイル
   ├─ tsukuyo/             # Moonweaver：recommended / setting1 / setting2
   ├─ tenkyu/              # Night of the Sky：recommended / setting1 / setting2
   ├─ shinro/              # Finale of the Deep 系列
   ├─ naganoya/            # Song of Days Past 系列
   ├─ kokuyo-hiten/        # Obsidian Codex 系列
   ├─ haijin-eiyu-emaki/   # Ashen Hero Scroll 系列
   └─ wanderers-troupe/    # Wanderer's Troupe 系列
```

---

## Quick Start
1. Clone:
   ```bash
   git clone https://github.com/yukiex/genshin-artifact-lock-presets.git
   cd genshin-artifact-lock-presets
   ```
2. Open `presets/<set>/<preset>.yml` (例: `presets/tenkyu/setting2.yml`) で狙う部位と閾値を確認。
3. ゲーム内「ロックアシスト」で対象セットを選択し、部位ごとに:
   - YAML の `substats_required_any_of` に載っているサブステをチェックで指定
   - `substats_required_min` と同じ数値を UI の「いずれか N 個以上」に入力
   - `main_allowed` を参考に UI のメイン効果フィルタを絞り込み（杯=元素ダメ% 等）
   - **推奨（Recommended）は常時オンにし、必要に応じて `setting1/setting2` を追加で有効化する**（推奨を外すのは、さらに狭い条件だけを拾いたい特殊ケース）
4. Strict → Lenient の順でロックすると在庫整理がスムーズです（天穹で会心無しを除去 → 月を紡ぐで ER/EM 良品を確保）。

---

## Lock Assist Workflow
- **Strict presets**: 花/羽/冠で会心サブ必須、杯は元素ダメ%固定で誤ロックを遮断。
- **Lenient presets**: 支援セットは ER/EM を最低 2 本確保しつつ会心があれば拾う。
- 改修時は `presets/lock-presets.yml` と個別ファイルを **同じ値** に保つこと。
- `docs/ui-mapping.md` の省略名（CR/CD/ER/EM など）以外を使う場合は必ず同ファイルを更新。
- **証跡メモ**: `docs/lock-assist-survey-template.md` を複製して各セット専用の調査メモを作成し、根拠URL・スクショとの対応を残す。
- **スクリーンショット**: `docs/reference/<set-id>-lock/` に flower～circlet の5枚を配置して YAML への転記元を明示する。

---

## YAML Schema Cheatsheet
```yaml
version: 1                 # schema version
set_id: tsukuyo | tenkyu | naganoya | shinro | kokuyo-hiten | haijin-eiyu-emaki
        | wanderers-troupe
set_name_ja: ...           # 日本語名
preset:
  key: recommended|setting1|setting2
  name: ...                # 表示名
  nickname_en: ...         # 任意
  intent: support_offfield | onfield_dps | ...
  targets: [ ... ]         # 想定キャラ（任意）
      slots:
        flower|plume|sands|goblet|circlet:
          main_allowed: [Any|ER%|<Element>DMG% ...]  # UI フィルタのヒント
          substats_required_any_of: [CR, CD, ER, EM]  # UI でチェックする候補
          substats_required_min: 1..3                 # いずれか N 個以上
          substats_required_all_of: [ER, EM]          # “必須ステータス”として全て含める
```

略語や UI 文言の正確な対応は `docs/ui-mapping.md` を参照してください。

---

## Quality & Contribution Checklist
- `yamllint presets docs` で基本的なフォーマット崩れを検知。
- `yq eval '.preset.slots | keys' presets/<set>/recommended.yml` で 5 部位が揃っているか確認。
- `yq eval '.preset.slots[] | select(.substats_required_min == null)' presets -o=json` が空になることを確認。
- コントリビューションフロー、命名規則、PR 要件は [`AGENTS.md`](./AGENTS.md) に詳細があります。
- 新規セット調査時は `docs/lock-assist-survey-template.md` を使い、証跡ドキュメントと `docs/reference/<set-id>-lock/` のスクショ配置をセットで更新する。

---

## License & Disclaimer
- **License**: MIT（予定）。OSS 化までの間は個人利用を想定しています。
- **Disclaimer**: 本プロジェクトは miHoYo / HoYoVerse 非公式です。ゲーム側のバランス変更で最適な閾値が変化する可能性があるため、実プレイに合わせて値を調整してください。
