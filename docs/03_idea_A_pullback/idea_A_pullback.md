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
