## Strategy v1 Baseline Backtest

### 目的

EMA Compression Breakout Strategy v1 の初回ベースライン結果を記録する。

Indicator v1と同一ロジックでStrategy化し、EMA収縮Setup → レンジブレイクTrigger がバックテスト上でどの程度機能するか確認する。

### 対象コード

- `src/idea_B/strategy_v1.pine`

### 共通条件

| 項目 | 内容 |
|---|---|
| 手法 | Idea B EMA Compression Breakout Strategy v1 |
| 時間足 | 1分足 |
| 検証期間 | 2021/01/01〜2025/12/31 |
| HTFフィルター | なし |
| 決済 | SL/TPのみ |
| 反対シグナル決済 | なし |
| Entry条件 | ポジションなしの時だけ |
| Entry/Exit | 同一Entryブロック内で発注 |

### パラメーター

| 項目 | 値 |
|---|---:|
| EMA Fast | 20 |
| EMA Middle | 50 |
| EMA Slow | 100 |
| compressionTicks | 50 |
| compressionLookback | 20 |
| requiredCompressionBars | 10 |
| rangeLen | 20 |
| Cooldown | ON |
| cooldownBars | 20 |
| RR | 1.0 |

### Strategy基本設定

| 項目 | 値 |
|---|---:|
| Initial Capital | 1,000,000 |
| Order Size | 2% of equity |
| Commission | 0.04% |
| Slippage | 2 |
| Pyramiding | 0 |
| Process Orders On Close | false |
| Calc On Every Tick | false |

### 結果

| 指標 | 値 |
|---|---:|
| 純利益 | -232492.67 |
| 総利益 | 36347.18 |
| 総損失 | 268839.86 |
| PF | 0.135 |
| 勝率 | 22.54% |
| 総トレード数 | 16166 |
| 最大ドローダウン | 23.25% |
| 平均トレード | -14.38 |
| 平均勝ち | 9.97 |
| 平均負け | 21.47 |

### 目視確認

- Indicator v1のTrigger矢印とStrategy v1のEntry位置：
- EntryはTrigger確定足の次足に出ているか：
- SL/TP位置：
- 未決済トレードの残り方：
- 明らかな連発：
- レンジブレイクとして自然か：

### 気づき

- 
### 暫定評価

Strategy v1は通常コスト条件では不採用。

案A v1と比較すると、総トレード数は減少しており、PFも案A v1よりは改善している。

ただし、PF 0.135であり、損益分岐には遠い。

また、RR1.0設計にもかかわらず、平均勝ち9.97に対して平均負け21.47となっており、平均負けが大きい。

次はCost-Off診断を行い、ロジック自体が悪いのか、コスト・約定条件の影響が大きいのかを切り分ける。

## Strategy v1 Cost-Off Diagnostic

### 目的

Strategy v1のロジック自体に優位性があるか、またはコストで大きく悪化しているだけかを確認する。

CommissionとSlippageを0にして、同一期間・同一パラメーターで比較する。

### 設定変更

| 項目 | 通常BT | Cost-Off |
|---|---:|---:|
| Commission | 0.04% | 0 |
| Slippage | 2 | 0 |

### 結果比較

| 条件 | PF | 勝率 | 総トレード数 | 最大DD | 平均トレード | 平均勝ち | 平均負け | メモ |
|---|---:|---:|---:|---:|---:|---:|---:|---|
| Costあり | 0.135 | 22.54% | 16,166 | 23.25% | -14.38 | 9.97 | 21.47 | 通常条件 |
| Costなし |  |  |  |  |  |  |  | 診断用 |

### 評価メモ

未記録。

### 暫定結論

未記録。

## Strategy v1 Compression Ticks Test

### 目的

EMA収縮判定の閾値である compressionTicks を変更し、Setupの広さと成績の変化を確認する。

compressionTicks が小さいほど収縮判定は厳しくなり、大きいほど収縮判定は広くなる。

### 共通条件

| 項目 | 内容 |
|---|---|
| 手法 | Idea B EMA Compression Breakout Strategy v1 |
| 時間足 | 1分足 |
| 検証期間 | 2021/01/01〜2025/12/31 |
| compressionLookback | 20 |
| requiredCompressionBars | 10 |
| rangeLen | 20 |
| Cooldown | ON |
| cooldownBars | 20 |
| RR | 1.0 |
| Commission | 0.04% |
| Slippage | 2 |

### 結果比較

| compressionTicks | PF | 勝率 | 総トレード数 | 最大DD | 平均トレード | 平均勝ち | 平均負け | メモ |
|---:|---:|---:|---:|---:|---:|---:|---:|---|
| 30 |  |  |  |  |  |  |  | 厳しめ |
| 50 |  |  |  |  |  |  |  | 初期値 |
| 70 |  |  |  |  |  |  |  |  |
| 100 |  |  |  |  |  |  |  | 広め |

### 評価ポイント

- compressionTicksを広げるとトレード数が増えるか
- PFが改善する領域があるか
- 収縮判定が厳しすぎてトレード数が少なくならないか
- 収縮判定が広すぎて普通のブレイク手法になっていないか
- 平均トレードが案Aより改善しているか

### 暫定結論

未記録。
