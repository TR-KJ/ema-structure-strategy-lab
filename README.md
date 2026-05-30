# EMA Structure Strategy Lab

## 概要

このレポジトリは、Pine Script v6でEMA構造手法を開発・検証するための記録です。

目的は、裁量判断に依存しすぎず、セットアップとトリガーをできるだけ機械的に定義できるEMA手法を作ることです。

## 背景

これまでMTAセットアップ + 1分足Triggerを検証してきたが、Triggerだけを機械化しても優位性が出にくかった。

そのため、MTA系はいったん区切り、EMA構造そのものをSetup化する方向へ転換する。

## 検証する案

| ID | 手法名 | 内容 | 状態 |
|---|---|---|---|
| A | EMA Pullback | EMA順行中の押し戻り再加速 | 優先検証 |
| B | EMA Compression Breakout | EMA収縮後の拡散ブレイク | 未着手 |
| C | HTF EMA Touch → LTF Trigger | 15分EMA接触後、1分再加速 | 未着手 |

## 開発方針

- 1分足メイン
- 15分足はHTFフィルターとして使用可
- SetupとTriggerを機械的に定義する
- まずはシンプルな仕様から始める
- Indicator → Strategy の順番で開発する
- 最初から最適化しすぎない
- 原因切り分けを重視する

## Pine Script v6 ルール

詳細は以下を参照。

[docs/01_coding_rules.md](docs/01_coding_rules.md)

## Backtest思想

詳細は以下を参照。

[docs/02_backtest_policy.md](docs/02_backtest_policy.md)

## 現在の優先順位

1. 案A EMA Pullback Indicator v1
2. 案A EMA Pullback Strategy v1
3. 案Aの負け方分析
4. 案Bまたは案Cとの比較

## ディレクトリ構成

```text
ema-structure-strategy-lab/
│
├── README.md
├── CHANGELOG.md
├── ROADMAP.md
│
├── docs/
│   ├── 01_coding_rules.md
│   ├── 02_backtest_policy.md
│   ├── 03_idea_A_ema_pullback.md
│   ├── 04_idea_B_ema_compression_breakout.md
│   ├── 05_idea_C_htf_ema_ltf_trigger.md
│   └── 06_comparison.md
│
├── src/
│   ├── idea_A/
│   │   ├── indicator_v1.pine
│   │   └── strategy_v1.pine
│   │
│   ├── idea_B/
│   │   ├── indicator_v1.pine
│   │   └── strategy_v1.pine
│   │
│   └── idea_C/
│       ├── indicator_v1.pine
│       └── strategy_v1.pine
│
└── results/
    ├── idea_A/
    │   ├── test_log.md
    │   └── summary.md
    │
    ├── idea_B/
    │   ├── test_log.md
    │   └── summary.md
    │
    └── idea_C/
        ├── test_log.md
        └── summary.md
