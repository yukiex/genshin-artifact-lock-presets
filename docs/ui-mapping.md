# UI ↔ YAML Mapping (Lock Assist)
**目的**：原神の「自動ロック（ロックアシスト）」UIのチェック項目を、このリポジトリの **YAML プリセット**に正しく落とし込むための対応表と設計指針。

> 前提
> - UIは**サブステータスに対して「いずれかN個以上」**の条件を指定できる  
> - **メインステータスを必須にはできない**（→ 可能なら“許可フィルタ”として `main_allowed` を使い誤ロックを軽減）  
> - スロット：`flower`, `plume`, `sands`, `goblet`, `circlet`

---

## 1. 表記と略語
| UI表示（日本語） | YAML略号 | 備考 |
|---|---|---|
| 会心率 | `CR` | Crit Rate |
| 会心ダメージ | `CD` | Crit DMG |
| 元素チャージ効率 | `ER` | Energy Recharge |
| 元素熟知 | `EM` | Elemental Mastery |
| 攻撃力% | `ATK%` | |
| HP% | `HP%` | |
| 防御力% | `DEF%` | |
| 攻撃力（実数） | `ATK` | フラット値 |
| HP（実数） | `HP` | フラット値 |
| 防御力（実数） | `DEF` | フラット値 |
| 元素ダメージ%（炎/水/雷/風/氷/岩/草） | `ElementalDMG%` | 杯の主ステ系 |
| 物理ダメージ% | `PhysicalDMG%` | 杯の主ステ |
| 治療効果 | `Healing%` | 冠の主ステ |

> YAML例での省略：  
> - **会心系**は `"CR", "CD"`  
> - **反応/サポ系**は `"ER", "EM"` をよく使います。

---

## 2. 基本マッピング（サブステの指定）
UIの「追加するサブステータス」と「いずれかN個以上」は、YAMLでは下記に対応します。

```yaml
substats_required_any_of: [CR, CD, ER, EM]
substats_required_min: 2
