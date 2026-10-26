# 0002 専用レポに分ける

状態: 決定（2026-10-26）
判断者: 自分
議論: https://claude.ai/code/session_01RRsWb1PMfgKNATkiZKYMQQ

## 決定
個人のツール集レポから分け、非公開の `tabitabi` レポで開発する。

## 理由
- 個人レポは bot の state 更新コミットが1日に何度も入り、PR の基準ブランチと CI が騒がしい
- GitHub Actions の secrets はレポ単位。他の workflow と秘密情報を共有しない
- AI に渡す権限をこのアプリに限れる
- ブランチ保護・必須チェック・CLAUDE.md・lockfile を他ツールと混ぜずに設定できる

## 移すもの
- `tools/places_stock/` は Maps リストの一回限りの取り込み処理としてのみ参考にする（論点7）
- `tools/common/slack.py` は必要になったらコピーする
