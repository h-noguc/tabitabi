# 開発ハーネスのモデル

状態: 下書き（2026-10-26）
議論: https://claude.ai/code/session_01RRsWb1PMfgKNATkiZKYMQQ
出典の一覧: [sources.md](sources.md)

アプリに依存しない骨格。`Check`・`Gate`・`Permission` の中身（どの検査・どの確認・何を禁じるか）はアプリの論点（データモデル、DB、ホスティング）が決まってから埋める。

## クラス図

```mermaid
classDiagram
  direction LR

  class Human["判断者"]
  class Issue["Issue"]{ 利用者; 困りごと; 今回やらない }
  class Spec["仕様"]{ 状態; 判断者; 範囲外 }
  class AC["受け入れ条件"]{ id: AC-n; 入力; 期待結果 }
  class Test["テスト"]{ 参照: specs/n AC-m }
  class Decision["判断記録"]{ 状態; 却下した案; 置き換え先 }
  class PR["PR"]{ AC↔テスト対応; 未確認事項 }
  class Check["検査"]{ コマンド; 必須か }
  class Runner["実行場所"]{ CI | 手元のフック }
  class Gate["人の確認"]{ 対象の変更種別 }
  class Reviewer["独立した評価役"]{ 新しいコンテキスト }
  class Playbook["手順書（skills）"]
  class Rule["規約"]{ 適用パス }
  class Instruction["AIへの指示（AGENTS.md）"]{ 目次として短く }
  class Permission["権限・隔離"]{ deny; サンドボックス }
  class Hook["フック"]{ 決定論的に強制 }
  class Session["AIセッション"]{ id }
  class Progress["進捗メモ"]
  class Transcript["会話ログ"]{ 秘密を除去 }
  class LogStore["ログ保存先"]
  class Retro["振り返り"]{ 2〜3回繰り返したものだけ昇格 }

  Issue "1" --> "0..*" Spec : 具体化
  Spec "1" *-- "1..*" AC
  AC "1" <-- "1..*" Test : 検証
  Human --> Spec : 承認
  Human --> AC : 承認（テストの基準）
  Human --> Decision : 決める
  Human --> PR : 取り込む
  Decision --> Decision : 置き換え
  Decision ..> Session : 議論の出典

  PR --> Spec : 実装
  PR "1" --> "0..*" Test : 追加・変更
  PR --> Check : 結果を受ける
  Check --> Runner : で実行
  Gate --> PR : 変更種別で要求
  Reviewer --> PR : 実装者と別に評価

  Instruction --> Rule : 参照
  Instruction --> Playbook : 参照
  Instruction --> Decision : 1行で参照
  Session --> Instruction : 読む
  Session --> Playbook : に従う
  Session --> Progress : 読み書き
  Session --> PR : 作成
  Permission --> Session : 制限
  Hook --> Session : 介入
  Hook --> Check : 回避を禁止
  Hook --> Transcript : 書き出し
  Transcript --> LogStore : 保存
  Transcript --> Session : の記録

  Retro --> Transcript : 材料
  Retro --> PR : 対象
  Retro ..> Rule : 改善・剪定
  Retro ..> Playbook : 改善
  Retro ..> Check : 自動化
  Retro ..> Hook : 強制へ昇格

  class Check:::appdep
  class Gate:::appdep
  class Permission:::appdep
  classDef appdep stroke-dasharray: 5 5
```

破線はアプリ依存。

## 要素と出典の状況

凡例: ◎ 一次資料を開いて確認 / ○ 検索要約のみ / － 出典なし（自分たちの設計判断）

| 要素 | 状況 | 主な出典（[sources.md](sources.md) の記号） |
|---|---|---|
| Issue | ○ | BP（fix-issue スキル）、GH† |
| 仕様 | ◎ | BP、SK、HD、cc-sdd |
| 受け入れ条件 | ◎ | HD（sprint contract）、LRA（機能リスト）、cc-sdd（EARS） |
| テスト | ◎ | BP、CC、論文 TDD（ASE 2024） |
| ACのIDをテスト名に入れる | － | 直接の出典なし。近いのは LRA の機能ごとの passes、EARS の要求ID |
| 判断記録 | ○ | 日本語記事（ADR とAI）、論文（ICSA 2024/2026） |
| PR | ◎ | BP、論文（AIDev, MSR 2026） |
| 検査・実行場所 | ◎ | BP、CC、SmartHR† |
| 人の確認（変更種別） | － | 直接の出典なし。CODEOWNERS をゲートにする例も見つからず |
| 独立した評価役（追加） | ◎ | HD（Evaluator）、BP（Writer/Reviewer）、論文（同じモデルのテストは実装をなぞる） |
| 手順書 | ◎ | BP（skills）、pepabo† |
| 規約（パス指定で段階的に読む、追加） | ◎ | BP、MEM、SmartHR†、tomada† |
| AIへの指示 | ◎ | BP、MEM（200行未満）、論文（肥大化で成功率低下） |
| 権限・隔離（追加） | ◎ | SBX、論文（RCE・インジェクション）、yureki_lab† |
| フック | ◎ | HOOKS、yurukusa†（--no-verify の禁止） |
| 進捗メモ（追加） | ◎ | LRA、CC、CTX |
| 会話ログ | ◎ | HOOKS（transcript_path）、chatii†。DB に入れる例はなし（ファイルが主流）。代替に OTel（MON） |
| 振り返り | ○ | BP（CLAUDE.md の剪定）、hiroshi75†（繰り返したものだけ昇格） |

## 採用を保留したもの

| 候補 | 保留理由 | 再検討する条件 |
|---|---|---|
| Eval セット（EVAL） | 個人開発の初期には過剰 | AI の失敗パターンが同じ形で繰り返したとき |
| Planner/Generator/Evaluator の多段ハーネス（HD） | 1回20分・9ドル vs 6時間・200ドルの差。モデル単独で解けない規模の作業で元が取れる | 単独セッションで完成しない大きな機能が出たとき |
| spec-kit 一式の手順（SK） | 冗長さと「SDD疲れ」の指摘。小さな変更は仕様なしで進める経路が要る | — |
| マージ率を品質指標にする | マージ結果は品質を表さない（論文 MSR 2026） | 採用しない |
