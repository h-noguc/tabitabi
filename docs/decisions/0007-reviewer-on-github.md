# 0007 独立した評価役は GitHub 上で動かす

状態: 決定（2026-10-26）
判断者: 自分
議論: https://claude.ai/code/session_01RRsWb1PMfgKNATkiZKYMQQ

## 背景
同じモデルが同じ文脈で書いたテストは、仕様ではなく実装の挙動をなぞりやすい（arXiv:2410.21136）。実装したセッションとは別の文脈で PR を評価する役が要る（docs/harness/model.md の「独立した評価役」）。

## 決定
PR のレビューは GitHub 上で、実装したセッションとは別の Claude が行う。手元の Claude Code のサブエージェントは使わない。方式は A（claude-code-action）で始める。

## 理由
- 実装したセッションと文脈が必ず分かれる
- PR に記録が残り、実装したセッションが指摘を受けて直せる
- 手元の環境やセッションの有無に左右されない

## 評価役に見させること
- 仕様と AC に対して、テストが期待結果（実装の挙動ではない）を確かめているか
- テストファイルや期待値の変更に理由があるか
- 「人の確認」が必要な変更種別に当たるか
- 正しさと要件に関わる指摘に絞る。好みの指摘はしない（Claude Code Best practices）

## 起動の条件（決定）
PR を開いたとき（opened / reopened / ready_for_review）だけ。push ごとには動かさない。修正後に見直してほしいときは `@claude` で呼ぶ。

## 方式（決定）
A で始める。認証は `CLAUDE_CODE_OAUTH_TOKEN` を GitHub secrets に置く。追加費用がなく、AC とテストの対応といったこのプロジェクト固有の観点を自分で書けるため。指摘の質に不満が出たら B を検討する。

比較した選択肢:
  - A. claude-code-action + `CLAUDE_CODE_OAUTH_TOKEN`（`claude setup-token` で発行。Pro・Max・Team・Enterprise で使え、プランの利用枠の中で動く。GitHub Actions の実行時間を使う）
  - B. Claude Code Review（Team・Enterprise 向けの管理型サービス。複数のエージェントが見て、指摘を検証してから出す。プランとは別に使用量で課金。設定は組織の Owner が行い、指示は REVIEW.md に書く）
  - 出典: https://code.claude.com/docs/en/github-actions 、 https://code.claude.com/docs/en/code-review （2026-10-26 確認）
## 未決
- レビュー結果を必須チェックにするか（初期案: しない。マージは人が判断。B のチェックは失敗にならない仕様）
