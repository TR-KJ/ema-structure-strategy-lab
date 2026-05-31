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
