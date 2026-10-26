# tabitabi

2人で共有する「行きたい（want）／行った（been）」場所を管理するアプリ。

## いまの状態

設計中。コードはまだない。判断の経緯は [`docs/decisions/`](docs/decisions/) に残す。

## 方針（要約）

- 正本は独自DB。Google マップは経路・ナビの「開く先」として共存する
- まず Web アプリ。本格運用でネイティブアプリへ
- OSS・一般公開は出口の候補。目的にはしない

## 判断記録

| # | 題 | 状態 |
|---|---|---|
| [0001](docs/decisions/0001-own-app-for-two.md) | 2人用の独自アプリにする | 決定 |
| [0002](docs/decisions/0002-separate-repository.md) | 専用レポに分ける | 決定 |
| [0003](docs/decisions/0003-web-first-then-native.md) | Web で出し、本格運用でネイティブ化 | 決定 |
| [0004](docs/decisions/0004-oss-as-exit-not-goal.md) | OSS・公開は出口であって目的にしない | 決定 |
| [0005](docs/decisions/0005-own-db-coexist-with-google-maps.md) | 正本は独自DB、Google マップとはリンクで共存 | 決定 |
| [0006](docs/decisions/0006-thin-api-boundary.md) | API の境界は持つ、中核は薄く | 提案 |
| [0007](docs/decisions/0007-reviewer-on-github.md) | 独立した評価役は GitHub 上で動かす | 決定 |
| [0008](docs/decisions/0008-ci-operation.md) | CI の運用 | 一部決定 |

未決の論点と順序は [`docs/decisions/open-questions.md`](docs/decisions/open-questions.md)。
