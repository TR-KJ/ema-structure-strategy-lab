# Idea A EMA Pullback Test Log

## 2026-xx-xx Strategy v1 Baseline Backtest

### 目的

Indicator v1と同一ロジックのStrategy v1について、初回ベースライン結果を記録する。

### 対象コード

- `src/idea_A/strategy_v1.pine`

### 検証条件

| 項目 | 内容 |
|---|---|
| 手法 | Idea A EMA Pullback Strategy v1 |
| 銘柄 | USDJPY |
| 時間足 | 1分足 |
| 期間 | 2021/01/01〜2025/12/31 |
| HTFフィルター | なし |
| 反対シグナル決済 | なし |
| 決済 | SL/TPのみ |

### パラメーター

| 項目 | 値 |
|---|---:|
| EMA Fast | 20 |
| EMA Middle | 50 |
| EMA Slow | 200 |
| Pullback Lookback | 10 |
| Cooldown | ON |
| Cooldown Bars | 10 |
| SL Lookback | 10 |
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
| 純利益 |  |
| 総利益 |  |
| 総損失 |  |
| PF |  |
| 勝率 |  |
| 総トレード数 |  |
| 最大ドローダウン |  |
| 平均トレード |  |
| 平均勝ち |  |
| 平均負け |  |
| 平均保有バー数 |  |

### 目視確認

- Indicator v1のTrigger矢印とStrategy v1のEntry位置は一致
- SL/TP位置：
- 不自然な未決済トレード：
- 明らかな連発：
- レンジでの挙動：

### 気づき

- 

### 暫定評価

- 
