# 開発ハーネスのモデル

状態: 下書き（2026-10-26）
議論: https://claude.ai/code/session_01RRsWb1PMfgKNATkiZKYMQQ
出典: [sources.md](sources.md)　／　表示用: [model.html](model.html)（要素ごとの出典状況、研究から引いた注意、保留した候補を含む）

アプリに依存しない骨格。`<<app依存>>` の中身（どの検査・どの確認・何を禁じるか）は、データモデル・DB・ホスティングが決まってから埋める。

## 1. 作る：仕様から取り込みまで

```mermaid
classDiagram
  direction LR
  class Human["判断者"]
  class Issue["Issue（なぜ）"] {
    利用者と場面
    困りごと
    得たい結果
    要件を決める人
    きっかけ
    今やる理由
    進め方 小 or 大
  }
  class Spec["仕様（完成の約束）"] {
    状態 下書き/承認済み/実装済み/廃止
    承認した版
    目的
    範囲
    範囲外
    影響 データ/API/権限/画面/誰に見えるか
    仮定と未決事項
    手動確認の手順
  }
  class AC["受け入れ条件"] {
    AC-n
    種類 正常/異常/境界
    前提
    入力
    期待結果
    確かめる段階 単体/API/E2E/手動
  }
  class Test["テスト"] {
    参照 specs/n AC-m
  }
  class PR["PR"] {
    AC とテストの対応
    未確認事項
  }
  class Check["検査"] {
    <<app依存>>
    コマンド
    必須か
  }
  class Runner["実行場所"] {
    CI
    手元のフック
  }
  class Gate["人の確認"] {
    <<app依存>>
    対象の変更種別
  }
  class Reviewer["独立した評価役"] {
    新しいコンテキスト
  }
  class Decision["判断記録"] {
    却下した案
    置き換え先
  }
  Issue "1" --> "0..1" Spec : 大きな変更
  Issue "1" *-- "0..*" AC : 小さな変更
  Issue --> Issue : 関連
  Spec "1" *-- "1..*" AC
  Test "1..*" --> "1" AC : 検証
  Human --> Spec : 版を承認
  Human --> AC : 期待結果を承認
  Spec --> Decision : 関連
  Human --> Decision : 決める
  Human --> PR : 取り込む
  PR --> Spec : 実装
  PR --> Test : 追加・変更
  PR --> Check : 結果を受ける
  Check --> Runner : で実行
  Gate --> PR : 変更種別で要求
  Reviewer --> PR : 実装者と別に評価
  Decision --> Decision : 置き換え
```

Issueは「なぜ」、仕様は「何をもって完成か」を持つ。小さな変更は仕様を書かず、IssueにACを直接持たせる。人は仕様を版ごとに承認し、仕様が変わったら承認し直す。ACの期待結果は人が承認し、テストは名前にACのIDを入れて参照する。実装したセッションとは別のコンテキストの評価役がPRを見る。<<app依存>> の中身は、データモデルやDBが決まってから埋める。

## 2. AIを動かす：読むもの・縛るもの・残すもの

```mermaid
classDiagram
  direction LR
  class Instruction["AIへの指示 AGENTS.md"] {
    目次として短く
  }
  class Rule["規約"] {
    適用パス
  }
  class Playbook["手順書 skills"]
  class Decision["判断記録"]
  class Session["AIセッション"] {
    id
  }
  class Progress["進捗メモ"]
  class Permission["権限・隔離"] {
    <<app依存>>
    deny
    サンドボックス
  }
  class Hook["フック"] {
    決定論的に強制
  }
  class Check["検査"]
  class Transcript["会話ログ"] {
    秘密を除去
  }
  class LogStore["ログ保存先"]
  class PR["PR"]
  Instruction --> Rule : 参照
  Instruction --> Playbook : 参照
  Instruction --> Decision : 1行で参照
  Session --> Instruction : 読む
  Session --> Playbook : に従う
  Session --> Progress : 読み書き
  Session --> PR : 作成
  Session ..> Decision : 起案
  Permission --> Session : 制限
  Hook --> Session : 介入
  Hook --> Check : 回避を禁止
  Hook --> Transcript : 書き出し
  Transcript --> LogStore : 保存
  Transcript --> Session : の記録
  Decision ..> Session : 議論の出典
```

指示ファイルは中身を抱えず、規約・手順書・判断記録への目次にする。お願いで済まないこと（検査の回避、テストの書き換え、秘密の読み取り）は、フックと権限で機械的に止める。判断記録はセッションIDで会話ログに戻れる。

## 3. 育てる：振り返りから戻す先

```mermaid
classDiagram
  direction LR
  class Retro["振り返り"] {
    2〜3回繰り返したものだけ昇格
  }
  class Transcript["会話ログ"]
  class PR["PR"]
  class Rule["規約"]
  class Playbook["手順書"]
  class Check["検査"]
  class Hook["フック"]
  Retro --> Transcript : 材料
  Retro --> PR : 対象
  Retro ..> Rule : 改善・剪定
  Retro ..> Playbook : 改善
  Retro ..> Check : 自動化
  Retro ..> Hook : 強制へ昇格
```

点線は「提案して人が承認したら変える」。1回の失敗ですぐルールにしない。不要になった規約は剪定する。
