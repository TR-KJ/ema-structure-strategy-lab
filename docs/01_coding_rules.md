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

確定足

* Triggerは確定足で判定する
* barstate.isconfirmed を重視する
* 未来参照・ルックアヘッドバイアスを避ける

配列・UDT

* 配列は必ず空チェックする
* インデックスアクセス前にサイズチェックする
* Pineの and / or の短絡評価に依存しない

line / label

* deleteしたら変数をnaに戻す

forループ

* 範囲反転に注意する
* 必要なら事前にガードする
* by -1 は使わない
