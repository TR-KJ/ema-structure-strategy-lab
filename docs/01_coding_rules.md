# Pine Script v6 Coding Rules

## 基本

- Pine Script v6を使用する
- 1行1文
- セミコロンは使わない
- 既存ロジックは、明示的な依頼がない限り変更しない

## request.security

request.security を使う場合は必ず以下を指定する。

```pine
gaps = barmerge.gaps_off
lookahead = barmerge.lookahead_off
