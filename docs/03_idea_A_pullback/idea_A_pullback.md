手法名：
EMA Structure Pullback Indicator v1

時間足：
1分足メイン

使用EMA：
EMA20
EMA50
EMA200

Long Setup：
EMA20 > EMA50
EMA50 > EMA200
close > EMA50
過去10本以内に low <= EMA20

Short Setup：
EMA20 < EMA50
EMA50 < EMA200
close < EMA50
過去10本以内に high >= EMA20

Long Trigger：
Long Setup成立中
close > EMA20
close[1] <= EMA20[1]
確定足

Short Trigger：
Short Setup成立中
close < EMA20
close[1] >= EMA20[1]
確定足

接触Lookback：
10本

クールダウン：
ON/OFF可能
初期値10本

SL候補：
Long = 直近10本最安値
Short = 直近10本最高値

TP候補：
RR 1.0

表示：
EMA3本
Setup背景
Trigger矢印
SL/TP候補ライン

HTFフィルター：
v1では入れない

## タッチ判定メモ

v1のEMA20タッチ判定は方向付きタッチではない。

Longは過去N本以内に low <= EMA20。
Shortは過去N本以内に high >= EMA20。

そのため、厳密な「上昇中の上からタッチ」「下降中の下からタッチ」ではなく、EMA20付近への接触判定として扱う。

目視確認でSetupが広すぎる場合、v1.1で方向付きタッチ条件を検討する。

## SL/TPメモ

v1のSL候補は、Trigger確定足を含む直近10本の高値/安値。

Long：
- SL = Trigger確定足を含む直近10本の最安値

Short：
- SL = Trigger確定足を含む直近10本の最高値

TP：
- Trigger確定足終値を基準にRR1.0で計算

今後、SLが遠すぎる場合は、Trigger足を除外した直近10本も比較する。

# Idea A EMA Pullback Test Log

## 2026-xx-xx Indicator v1 Visual Check

### 対象

- EMA Structure Pullback Indicator v1
- 1分足
- EMA20 / EMA50 / EMA200
- HTFフィルターなし

### 確認内容

- EMA20 / EMA50 / EMA200 の表示 OK
- Long / Short Setup 背景表示 OK
- Trigger矢印表示 OK
- Cooldown挙動 OK
- SL/TP候補ライン表示 OK

### メモ

- v1のSetup判定は方向付きタッチではない
- Long：過去10本以内に low <= EMA20
- Short：過去10本以内に high >= EMA20
- SL/TPはTrigger確定足を含む直近10本で計算
- TPはTrigger確定足終値基準のRR1.0

### 結論

Indicator v1の挙動は問題なし。
次は同一ロジックでStrategy v1を作成する。

### v1.2 未決済トレード発生メモ

v1.2ではTP/SLを strategy.position_avg_price 基準に変更した。

しかし、実際の約定価格と保存済みSLの位置関係によって、Riskが無効になるケースが発生した。

Longでは `strategy.position_avg_price <= plannedLongStop` の場合、longActualRiskが無効となり、strategy.exitが発注されない。

Shortでも同様に、`strategy.position_avg_price >= plannedShortStop` の場合、shortActualRiskが無効となる。

その結果、SL/TPが出ず、未決済ポジションが残るケースが確認された。

v1.2は診断版として扱い、無効Risk時はstrategy.closeで強制決済する修正を検討する。

## Strategy v1.2 診断結果

v1.2では、TP/SLを `strategy.position_avg_price` 基準に変更した。

しかし、Entry後でないとTP/SLを確定できない構造となり、EntryとExitを同一ブロックで発注できなかった。

その結果、Riskが無効になるケースで `strategy.exit` が正しく発注されず、2021年のポジションが2025年末まで未決済として残る挙動を確認した。

このため、v1.2はStrategy実装として不安定と判断し、以降の比較対象から除外する。

今後は、v1 / v1.1 と同様に、Trigger確定足時点でSL/TPを固定し、EntryとExitを同一Entryブロック内で発注する方式に戻す。

## Strategy v1.3 Trigger Strength Test

v1.3では、Indicator版は作成しない。
理由は、Setup条件はv1.1から変更せず、Trigger条件のみを強化するため。

Strategy上のplotshapeとEntry位置で挙動確認する。
