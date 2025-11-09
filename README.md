# Genshin Artifact Lock Presets
**原神「自動ロック（ロックアシスト）」**向けのプリセット集です。  
セットごとに **Recommended / Setting1（lenient） / Setting2（strict）** を用意し、**サブステのみ“いずれか N 個以上”**で判定できるよう最適化しています。  
メイン効果は UI 上で必須にできないため、本リポジトリでは **`main_allowed` を“ヒント”として併記**します（UI のメイン効果フィルタと併用推奨）。

> 初期収録セット
> - **月を紡ぐ夜の歌**（Moonweaver / 支援・オフフィールド向け：ER/EM 重点）
> - **天穹の顕現せし夜**（Night of the Sky / オンフィールド DPS：会心重点）

---

## 目次
- [レポジトリ構成](#レポジトリ構成)
- [クイックスタート](#クイックスタート)
- [プリセット設計思想](#プリセット設計思想)
- [YAML 仕様（キー定義）](#yaml-仕様キー定義)
- [UI ↔ YAML 対応](#ui--yaml-対応)
- [使用例（UI 操作手順）](#使用例ui-操作手順)
- [対象キャラクター（例）](#対象キャラクター例)
- [よくある落とし穴](#よくある落とし穴)
- [拡張ロードマップ](#拡張ロードマップ)
- [貢献ガイド](#貢献ガイド)
- [ライセンス / 免責](#ライセンス--免責)

---

## レポジトリ構成
```

genshin-artifact-lock-presets/
├─ README.md
├─ presets/
│  ├─ tsukuyo/                 # 月を紡ぐ夜の歌（Moonweaver）
│  │  ├─ recommended.yml
│  │  ├─ setting1.yml
│  │  └─ setting2.yml
│  └─ tenkyu/                  # 天穹の顕現せし夜（Night of the Sky）
│     ├─ recommended.yml
│     ├─ setting1.yml
│     └─ setting2.yml
└─ docs/
└─ ui-mapping.md            # UI チェック項目と YAML の対応表

````

- 各 `*.yml` は部位（flower / plume / sands / goblet / circlet）ごとに  
  `substats_required_any_of` と `substats_required_min` を定義しています。
- `main_allowed` は **UI のメイン効果フィルタと整合させるための“参考”** です（必須ではありません）。

---

## クイックスタート
1. **クローン**
   ```bash
   git clone https://github.com/yukiex/genshin-artifact-lock-presets.git
   cd genshin-artifact-lock-presets
````

2. **プリセットを選択**
   例）支援枠を整える → `presets/tsukuyo/recommended.yml`
   例）DPS 並品一掃 → `presets/tenkyu/setting2.yml`
3. **ゲーム内のロックアシスト画面を開く**

   * 対象セットを選択
   * 部位ごとに **サブステータス（会心率/会心ダメ/ER/EM…）** をチェック
   * **「いずれか N 個以上」** を YAML の `substats_required_min` と同じ値に設定
   * 可能なら **メイン効果のフィルタ**も `main_allowed` に合わせて限定
4. **在庫圧縮の推奨フロー**

   * **天穹（strict）**で会心サブの無い並品を掃除
   * **月を紡ぐ（rec/lenient）**で ER/EM 良サブを回収
   * 余りは **聖遺物廻聖**、残品は **+20 で素材圧縮**

---

## プリセット設計思想

* **月を紡ぐ夜の歌（Moonweaver）**

  * **支援・オフフィールド運用**を想定。**ER/EM** を広く拾い、会心は“あると嬉しい”。
  * 杯は **元素ダメ% or EM** を推奨（HP/DEF 杯は原則除外。ヒーラー保険は手動管理）。
  * 冠は **会心 or 治療 or EM**。ヒーラー時は **ER サブ**を重視。
* **天穹の顕現せし夜（Night of the Sky）**

  * **オンフィールド DPS**。花/羽/冠で **会心サブ必須**（lenient=最低1、strict=2 推奨）。
  * 杯は **元素ダメ% 固定**で誤ロック防止。
  * 砂は **ATK%（標準）/ EM（反応）/ HP%（HP スケーラー）**＋会心/ER を要求。

---

## YAML 仕様（キー定義）

```yaml
version: 1                # スキーマバージョン
set_id: tsukuyo|tenkyu    # セット識別子
set_name_ja: ...          # 日本語名
preset:
  key: recommended|setting1|setting2
  name: ...               # 表示名
  nickname_en: ...        # 英語別名（任意）
  intent: ...             # 用途メタ（例: onfield_dps / support_offfield）
  targets: [ ... ]        # 想定キャラ（メタ情報。判定には未使用）
  slots:
    <slot>:
      main_allowed: [ ... ]               # UI フィルタのヒント（必須ではない）
      substats_required_any_of: [ ... ]   # サブ候補（例: [CR, CD, ER, EM]）
      substats_required_min: N            # いずれか N 個以上（整数）
```

**略語**（詳細は [`docs/ui-mapping.md`](./docs/ui-mapping.md) 参照）

* `CR`=会心率, `CD`=会心ダメ, `ER`=元素チャージ効率, `EM`=元素熟知
* `ATK%`, `HP%`, `DEF%` は割合。`ATK`, `HP`, `DEF` はフラット値
* `ElementalDMG%`=元素ダメージ%（炎/水/雷/風/氷/岩/草）, `PhysicalDMG%`=物理ダメ%
* `Healing%`=治療効果

---

## UI ↔ YAML 対応

* UI の **「追加するサブステータス」** → `substats_required_any_of`
* UI の **「いずれか N 個以上」** → `substats_required_min`
* UI で **メイン効果を必須指定できない** → YAML の `main_allowed` を“範囲ヒント”として記述し、
  **UI 側のメイン効果フィルタ**で近い条件に絞り込む（誤ロック防止）。

> 具体例は [`docs/ui-mapping.md`](./docs/ui-mapping.md) に操作手順つきで記載。

---

## 使用例（UI 操作手順）

### 天穹（Strict）で並品一掃

* **花/羽**：会心率・会心ダメ・元素熟知 → **いずれか 2 個以上**
* **砂**：会心率・会心ダメ・元素熟知・元素チャージ効率 → **いずれか 2 個以上**
* **杯**：会心率・会心ダメ・元素熟知 → **いずれか 2 個以上**

  * メイン効果を **元素ダメ% のみにフィルタ**
* **冠**：会心率・会心ダメ → **いずれか 2 個以上**

### 月を紡ぐ（Recommended）で支援良品回収

* **花/羽**：ER・EM・会心率・会心ダメ → **いずれか 2 個以上**
* **砂**：同上（メインは **ER%/EM** に絞れると尚良）
* **杯**：会心率・会心ダメ・ER・EM → **いずれか 2 個以上**

  * メイン効果は **元素ダメ% / EM** を推奨
* **冠**：ER・EM・会心率 → **いずれか 2 個以上**

  * ヒーラーなら **治療冠＋ER サブ**を優先

---

## 対象キャラクター（例）

* **Moonweaver（支援寄り）**
  行秋 / 夜蘭 / 香菱 / フィッシュル / 八重神子 / 北斗 / 心海 / 白朮 / ベネット / ディオナ / レイラ / キララ / バーバラ / トーマ / 七七 / 久岐忍 / コレイ / カーヴェ …
* **Night of the Sky（オンフィールド DPS）**
  セノ / 刻晴 / クロリンデ / アルハイゼン / ティナリ / 宵宮 / 胡桃 / 甘雨 / タルタリヤ / ヌヴィレット / エウルア …

> `targets` は **メタ情報**です。プリセットのロック判定には使われません。
> 手持ちに合わせて自由に更新してください。

---

## よくある落とし穴

* **杯の HP%/DEF% を誤ロック**
  → 天穹では `main_allowed: [ElementalDMG%]` を徹底し、UI 側でも元素杯のみ表示に。
* **会心サブ無しを拾う**
  → 天穹（DPS）は **花/羽/冠で会心必須**（lenient=1, strict=2）を守る。
* **ER 不足で回らない**
  → 月を紡ぐ（支援）は **ER を any_of に必ず含める**。治療冠は **ER サブ付き個体**を優先。
* **フラット値の混入で質低下**
  → lenient でも `ATK/HP/DEF（フラット）` を候補に入れない運用が無難。

---

## 拡張ロードマップ

* `presets/index.yml`（目録）と **結合/検証ツール**（`tools/`）の追加
* **YAML スキーマ**（`schemas/preset.schema.json`）と CI バリデーション
* 他セット（翠緑・絶縁・金メッキ・深林・千岩・海染・華館…）の追加
* 例外ルール（例：ヒーラー用 HP 杯“1 枚のみ許容”の運用 Tips）を docs に整理

---

## 貢献ガイド

1. Issue で提案またはバグ報告
2. フォーク → ブランチ作成 → 変更
3. `README.md` / `docs/ui-mapping.md` の対応も更新
4. Pull Request（変更理由・スクショを添付いただけると助かります）

**命名方針**

* セットごとにディレクトリ、**`recommended.yml` / `setting1.yml` / `setting2.yml`** を基本形に統一
* 略語は `CR/CD/ER/EM` を使用（docs 参照）

---

## ライセンス / 免責

* **License**: MIT（予定）
* **免責**: 本リポジトリは miHoYo/HoYoVerse とは無関係の **非公式** 資料です。
  ゲーム内仕様変更によりプリセットの最適値が変わる場合があります。各自の判断で調整してください。

---

### 付録：サンプル抜粋

**天穹 / setting2（strict）— 花**

```yaml
flower:
  main_allowed: [Any]
  substats_required_any_of: [CR, CD, EM]
  substats_required_min: 2
```

**月を紡ぐ / recommended — 砂**

```yaml
sands:
  main_allowed: [ER%, EM]
  substats_required_any_of: [ER, EM, CR, CD]
  substats_required_min: 2
```
