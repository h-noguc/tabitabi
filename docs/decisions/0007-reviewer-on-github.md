# 0007 独立した評価役は GitHub 上で動かす

状態: 決定（2026-10-26）
判断者: 自分
議論: https://claude.ai/code/session_01RRsWb1PMfgKNATkiZKYMQQ

## 背景
同じモデルが同じ文脈で書いたテストは、仕様ではなく実装の挙動をなぞりやすい（arXiv:2410.21136）。実装したセッションとは別の文脈で PR を評価する役が要る（docs/harness/model.md の「独立した評価役」）。

## 決定
PR のレビューは、GitHub Actions 上の anthropics/claude-code-action で行う。手元の Claude Code のサブエージェントは使わない。

## 理由
- 実装したセッションと文脈が必ず分かれる
- PR に記録が残り、実装したセッションが指摘を受けて直せる
- 手元の環境やセッションの有無に左右されない

## 評価役に見させること
- 仕様と AC に対して、テストが期待結果（実装の挙動ではない）を確かめているか
- テストファイルや期待値の変更に理由があるか
- 「人の確認」が必要な変更種別に当たるか
- 正しさと要件に関わる指摘に絞る。好みの指摘はしない（Claude Code Best practices）

## 未決
- 認証: `CLAUDE_CODE_OAUTH_TOKEN`（Pro/Max のサブスクリプション。`claude setup-token` で発行）か `ANTHROPIC_API_KEY`（従量課金）
- 起動の条件: PR を開いたときと push ごとか、ラベルや `@claude` のときだけか
- レビュー結果を必須チェックにするか（初期案: しない。マージは人が判断）
