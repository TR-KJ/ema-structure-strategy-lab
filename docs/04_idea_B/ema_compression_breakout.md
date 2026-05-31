## Indicator v1 Visual Check

### 対象

- EMA Compression Breakout Indicator v1
- 1分足
- EMA20 / EMA50 / EMA100
- compressionTicks = 50
- compressionLookback = 20
- requiredCompressionBars = 10
- rangeLen = 20
- cooldownBars = 20

### 確認内容

- EMA20 / EMA50 / EMA100 の表示 OK
- Compression背景表示 OK
- Range High / Low 表示 OK
- Long / Short Trigger矢印表示 OK
- SL/TP候補ライン表示 OK

### メモ

- v1ではHTFフィルターなし
- v1では最低レンジ幅 / 最大レンジ幅フィルターなし
- Range High / Low は現在足を含めず、過去rangeLen本で計算
- SL/TP候補はTrigger確定足close基準、RR1.0

### 結論

Indicator v1の挙動は問題なし。
次は同一ロジックでStrategy v1を作成する。
