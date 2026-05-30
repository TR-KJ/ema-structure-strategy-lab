---

# docs/idea_A_ema_pullback/README.md の構成案

```md
# Idea A: EMA Pullback

## 概要

EMAが順行配列になっている状態で、短期EMAへの押し戻りから再加速する場面を狙う。

## 狙う相場

- トレンド継続
- 押し目買い
- 戻り売り

## 使用EMA

- EMA20
- EMA50
- EMA200

## Setup

### Long

- EMA20 > EMA50
- EMA50 > EMA200
- close > EMA50
- 過去10本以内に low <= EMA20

### Short

- EMA20 < EMA50
- EMA50 < EMA200
- close < EMA50
- 過去10本以内に high >= EMA20

## Trigger

### Long

- close > EMA20
- close[1] <= EMA20[1]
- barstate.isconfirmed

### Short

- close < EMA20
- close[1] >= EMA20[1]
- barstate.isconfirmed

## SL/TP 初期案

- SL：直近10本の高値/安値
- TP：RR 1.0

## 現在のステータス

- Indicator v1 作成予定
- Strategy 未着手

## メモ

まずは勝てるかどうかではなく、シグナル位置が感覚と合うかを確認する。
