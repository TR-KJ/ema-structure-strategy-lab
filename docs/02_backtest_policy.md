---

# docs/02_backtest_policy.md の構成案

```md
# Backtest Policy

## 基本思想

- Triggerは確定足で判定する
- 注文は次足始値約定想定
- TP/SLはTrigger確定足の終値基準で計算する
- RR初期値は1.0
- SLは最初は明確な機械ルールで置く

## Strategy基本設定

```pine
initial_capital = 1000000
default_qty_type = strategy.percent_of_equity
default_qty_value = 2
commission_type = strategy.commission.percent
commission_value = 0.04
slippage = 2
pyramiding = 0
process_orders_on_close = false
calc_on_every_tick = false

```

TradingView確認

* pine_check / コンパイルだけで判断しない
* 実チャート上のruntime挙動を確認する
* エントリー位置
* SL/TP位置
* 未決済トレードの残り方
* HTFフィルターの挙動
* リペイント疑い
