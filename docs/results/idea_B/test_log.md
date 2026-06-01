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
| Costなし | 1.001 | 49.21% | 16166 | 0.34% | 0.01 | 18.47 | 17.88 | 診断用 |

### 評価

CostなしではPF 1.001で、ほぼ損益分岐。

ロジック単体では明確な逆優位ではないが、優位性もほぼ確認できない。

CostありではPF 0.135まで悪化しており、現在のStrategy v1はコスト耐性がない。

平均勝ち・平均負けはCostなしではほぼ同等だが、Costありでは平均勝ち9.97、平均負け21.47となっており、コスト・スリッページの影響を強く受けている。

### 暫定結論

Idea B v1の初期仕様は、現状では実用候補ではない。

ただし、案A v1よりは通常コスト条件でのPFが高く、トレード数も少ないため、案Bはもう少し診断を継続する。

次は、EMA収縮判定の閾値である compressionTicks を変更し、収縮Setupの広さが結果に与える影響を確認する。

## Strategy v1 Compression Ticks Test

### 目的

EMA収縮判定の閾値である compressionTicks を変更し、Setupの広さが結果に与える影響を確認する。

compressionTicks が小さいほど収縮判定は厳しくなり、大きいほど収縮判定は広くなる。

### 共通条件

| 項目 | 内容 |
|---|---|
| 手法 | Idea B EMA Compression Breakout Strategy v1 |
| 時間足 | 1分足 |
| 検証期間 | 2021/01/01〜2025/12/31 |
| EMA | 20 / 50 / 100 |
| compressionLookback | 20 |
| requiredCompressionBars | 10 |
| rangeLen | 20 |
| Cooldown | ON |
| cooldownBars | 20 |
| RR | 1.0 |
| HTFフィルター | なし |
| 決済 | SL/TPのみ |

### Costあり結果

| compressionTicks | PF | 勝率 | 総トレード数 | 最大DD | 平均トレード | 平均勝ち | 平均負け | メモ |
|---:|---:|---:|---:|---:|---:|---:|---:|---|
| 30 |  |  |  |  |  |  |  | 厳しめ |
| 50 | 0.135 | 22.54% | 16,166 | 23.25% | -14.38 | 9.97 | 21.47 | 初期値 |
| 70 |  |  |  |  |  |  |  |  |
| 100 |  |  |  |  |  |  |  | 広め |

### Costなし結果

| compressionTicks | PF | 勝率 | 総トレード数 | 最大DD | 平均トレード | 平均勝ち | 平均負け | メモ |
|---:|---:|---:|---:|---:|---:|---:|---:|---|
| 30 | 0.998 | 49.35% | 14828 | 0.18% | -0.01 | 16.19 | 15.80 | 厳しめ |
| 50 | 1.001 | 49.21% | 16,166 | 0.34% | 0.01 | 18.47 | 17.88 | 初期値 |
| 70 | 0.985 | 49.14% | 16515 | 0.39% | -0.14 | 19.47 | 19.09 |  |
| 100 | 0.991 | 49.20% | 16536 | 0.27% | -0.09 | 20.36 | 19.90 | 広め |

### 評価ポイント

- CostなしでPFが1.0を明確に超えるcompressionTicksがあるか
- CostありでもPF改善するcompressionTicksがあるか
- compressionTicksを広げるとトレード数が増えすぎないか
- compressionTicksを狭めるとトレード数が少なすぎないか
- 平均トレードが改善するか

### Compression Ticks Test 評価

Costなしで compressionTicks 30 / 50 / 70 / 100 を比較した。

結果はすべてPF 1.0前後であり、明確な優位性の山は確認できなかった。

compressionTicks 50 が最も良かったが、PF 1.001、平均トレード 0.01 であり、実質的には損益分岐。

この結果から、現時点の案B v1においては、compressionTicksの調整だけでは優位性は作れないと判断する。

次は compressionTicks ではなく、Breakout後の出口設計またはRange幅フィルターを検証する。

## Strategy v1 RR Diagnostic Test

### 目的

compressionTicksを変更してもCostなしPFはほぼ1.0前後であり、EMA収縮閾値の調整だけでは優位性が確認できなかった。

次に、Breakout後の出口設計としてRRを変更し、PF・勝率・平均トレードが改善するか確認する。

まずはCostなしで比較し、ロジック単体に伸ばす余地があるかを確認する。

### 共通条件

| 項目 | 内容 |
|---|---|
| 手法 | Idea B EMA Compression Breakout Strategy v1 |
| 時間足 | 1分足 |
| 検証期間 | 2021/01/01〜2025/12/31 |
| EMA | 20 / 50 / 100 |
| compressionTicks | 50 |
| compressionLookback | 20 |
| requiredCompressionBars | 10 |
| rangeLen | 20 |
| Cooldown | ON |
| cooldownBars | 20 |
| HTFフィルター | なし |
| 決済 | SL/TPのみ |
| Commission | 0 |
| Slippage | 0 |

### Costなし結果

| RR | PF | 勝率 | 総トレード数 | 最大DD | 平均トレード | 平均勝ち | 平均負け | メモ |
|---:|---:|---:|---:|---:|---:|---:|---:|---|
| 1.0 | 1.001 | 49.21% | 16,166 | 0.34% | 0.01 | 18.47 | 17.88 | 基準 |
| 1.3 |  |  |  |  |  |  |  |  |
| 1.5 |  |  |  |  |  |  |  |  |
| 2.0 |  |  |  |  |  |  |  |  |

### 評価ポイント

- RRを上げてPFが改善するか
- 勝率低下に対して平均勝ちが十分伸びるか
- 平均トレードがプラス方向に伸びるか
- RR変更だけでPF 1.1以上が出るか
- RRを上げてもPFが1.0前後なら、出口だけでは改善不可

### 暫定結論

未記録。
