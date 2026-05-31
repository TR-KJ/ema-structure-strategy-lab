# Idea B: EMA Compression Breakout

## 概要

EMAが収縮している状態をSetupとし、その後のレンジブレイクをTriggerとしてEntry候補を検出する。

Idea Aでは、EMA20押し戻り再クロス型が1分足ノイズとコストに弱いことが分かった。

Idea Bでは、押し戻り継続型ではなく、収縮後の初動ブレイクを狙う。

## Indicator v1 目的

- EMA収縮状態がチャート上で自然か確認する
- Range High / Low がブレイク対象として妥当か確認する
- Trigger矢印が出すぎないか確認する
- SL/TP候補が現実的な幅か確認する

## v1 初期仕様

| 項目 | 内容 |
|---|---|
| EMA | 20 / 50 / 100 |
| Compression | EMA20-EMA50距離、EMA50-EMA100距離 |
| compressionTicks | 50 |
| compressionLookback | 20 |
| requiredCompressionBars | 10 |
| rangeLen | 20 |
| Long Trigger | Setup中、EMA20 > EMA50、close > rangeHigh |
| Short Trigger | Setup中、EMA20 < EMA50、close < rangeLow |
| Cooldown | ON、20本 |
| SL | Long = rangeLow、Short = rangeHigh |
| TP | RR1.0 |
| HTF | v1ではなし |
