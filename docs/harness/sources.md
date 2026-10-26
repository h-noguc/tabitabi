# 開発ハーネスの出典

調べた日: 2026-10-26。調査はAIのサブエージェントが実施。

**検証レベル**（2026-10-26 再確認）
- ◎ 本文を開いて主張を確認した
- 論文は arXiv の要旨で、16本すべての実在とタイトル・主な主張を確認した。要旨にない数値は使わない
- † 本文を開けていない（openai.com は 403）

## 公式資料・海外ブログ

| 記号 | 出典 |
|---|---|
| BP | Claude Code, "Best practices" https://code.claude.com/docs/en/best-practices ◎ |
| MEM | Claude Code, "Memory" https://code.claude.com/docs/en/memory ◎ |
| HOOKS | Claude Code, "Hooks" / "Hooks guide" https://code.claude.com/docs/en/hooks ◎ |
| MON | Claude Code, "Monitoring usage"（OpenTelemetry） https://code.claude.com/docs/en/monitoring-usage ◎ |
| LRA | Justin Young, "Effective harnesses for long-running agents", Anthropic, 2025-11-26 https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents ◎ |
| HD | Prithvi Rajasekaran, "Harness design for long-running application development", Anthropic, 2026-03-24 https://www.anthropic.com/engineering/harness-design-long-running-apps ◎ |
| CC | Nicholas Carlini, "Building a C compiler with a team of parallel Claudes", Anthropic, 2026-02-05 https://www.anthropic.com/engineering/building-c-compiler ◎ |
| SBX | "Beyond permission prompts", Anthropic, 2025-10-20 https://www.anthropic.com/engineering/claude-code-sandboxing ◎ |
| EVAL | "Demystifying evals for AI agents", Anthropic, 2026-01-09 https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents ◎ |
| CTX | "Effective context engineering for AI agents", Anthropic, 2025-09-29 ◎ |
| SK | github/spec-kit README・spec-driven.md https://github.com/github/spec-kit ◎ |
| AGENTS | openai/agents.md README ◎ |
| OAI | Ryan Lopopolo, "Harness engineering", OpenAI, 2026-02-11 https://openai.com/index/harness-engineering/ †（「AGENTS.md は百科事典でなく地図」は未確認） |
| BOE | Birgitta Böckeler, "Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl", martinfowler.com, 2025-10-15 https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html ◎（spec-kit は Markdown が多く冗長。constitution の条項に**過剰に従う**例がある） |
| BOE2 | Birgitta Böckeler, "Harness Engineering - first thoughts", 2026-02-17 https://martinfowler.com/articles/exploring-gen-ai/harness-engineering-memo.html ◎。正式版 "Harness engineering for coding agent users"（2026-04-02、/articles/harness-engineering.html）は未読 |
| GH | GitHub Docs, "Best practices for using GitHub Copilot to work on tasks"（現在の名称は Copilot cloud agent） ◎（Issue をプロンプトとして書き、受け入れ条件と変更するファイルを含める） |

## 日本語記事（すべて本文で確認 ◎。補足は確認で分かった注意）

| 記号 | 出典 |
|---|---|
| cc-sdd | gotalab/cc-sdd v3 https://github.com/gotalab/cc-sdd ◎ |
| SmartHR | 2026-09-16 https://tech.smarthr.jp/entry/2026/09/16/110205 （ハーネスを先に作る。完了条件12項目をシェルスクリプトにしてデグレを止める。「2.5か月」は当初の見積もりで実績比較ではない）/ 2026-03-12 https://tech.smarthr.jp/entry/2026/03/12/134348 （CLAUDE.md を AGENTS.md へのシンボリックリンクにして一元管理） |
| CyberAgent | Ken Takao, 2026-06-18 https://developers.cyberagent.co.jp/blog/archives/64334/ （ハーネスとコンテキストは最小限、検証できる手段を与える） |
| pepabo | 2026-04-21 https://zenn.dev/pepabo/articles/claude-code-rules-skills-split （CLAUDE.md・rules・skills の3層。「毎回注意してほしいか」「明示的に呼ぶか」で分ける） |
| tomada | 2025-12-13 https://qiita.com/tomada/items/cb05d3a7aa00cb35c486 （paths 指定のルールは必要になるまで読み込まれない） |
| smartshopping | 2025-08-14 https://zenn.dev/smartshopping/articles/refactor-fat-claude-md （CLAUDE.md をコマンド・サブエージェント・下位の CLAUDE.md に分散。フックへの移し替えは書かれていない） |
| yurukusa | 2026-05-04 https://qiita.com/yurukusa/items/ab9387816b372b7ae210 （--no-verify による pre-commit 回避を PreToolUse でブロック。事例は Claude Code の GitHub Issue #40117） |
| yureki_lab | 2026-09-25 https://qiita.com/yureki_lab/items/6f9175d70d294840311c （deny → ask → allow の順。パス指定が効くのは Edit() と Read() だけ） |
| chatii | 2025-12-26 https://zenn.dev/chatii/articles/353571ee68c3d8 （SessionEnd フックで transcript を保存し、後で棚卸し） |
| hty1123445_a | 2026-03-29 https://qiita.com/hty1123445_a/items/514d864ec0484f323ea9 （1回の不満は無視、2〜3回繰り返したら改善候補。採用は必ず人が判断） |
| japannomu | 2026-03-21 https://zenn.dev/japannomu/articles/20260321_claude-code-harness-control （テストの期待値は設計書から導かせて改ざんを防ぐ。テストファイルの保護そのものは書かれていない） |
| kosk_t | 2026-04-21 https://zenn.dev/kosk_t/articles/adr-lightweight-decision-records-for-ai （ADR 1枚、却下した案を残す。CLAUDE.md からの参照は任意の強化策） |

## 研究論文（すべてアブストラクトの抜粋のみ）

| 主題 | 論文 |
|---|---|
| 指示ファイルが成功率を下げコストを増やす | Gloaguen et al., arXiv:2602.11988 |
| 指示ファイルで時間とトークンが減る | Lulla et al., arXiv:2601.20404（ICSE JAWs 2026） |
| CLAUDE.md の実態 | Chatlatanagulchai et al., arXiv:2509.14744（PROFES 2025） |
| エージェントPRの受け入れ | Li et al., arXiv:2507.15003（AIDev）/ Ehsani et al., arXiv:2601.15195（MSR 2026） |
| テストを添えると正解率が上がる | Mathews & Nagappan, arXiv:2402.13521（ASE 2024） |
| テストの悪用（報酬ハッキング） | Zhong et al., ImpossibleBench, arXiv:2510.20270 / EvilGenie, arXiv:2511.21654 |
| TDD を指示するだけでは逆効果 | TDAD, arXiv:2603.17973 |
| LLM のテストは実装をなぞる | Konstantinou et al., arXiv:2410.21136 |
| ADR と LLM | Dhar et al., arXiv:2403.01709（ICSA 2024）/ arXiv:2602.07609 |
| エージェントの軌跡分析 | Bouzenia & Pradel, arXiv:2506.18824（ASE 2025） |
| エージェントへのインジェクション・RCE | arXiv:2509.22040 / arXiv:2509.05755 |
| マージ結果は品質を表さない | arXiv:2605.22534（MSR 2026） |

## 確認で外した主張

| 主張 | 理由 |
|---|---|
| 「PostToolUse フックから lefthook を呼ぶ」（ennagara128） | 記事に lefthook は出てこない。出典から削除 |
| 「繰り返したパターンだけを昇格」の出典を hiroshi75 としていた | 記事にその内容はなく、hty1123445_a の内容だった。差し替え |
| 「spec-kit の constitution は無視される」（BOE） | 記事では過剰に従われる例。修正 |
| 「ImpossibleBench で GPT-5 が76%」 | 要旨に数値がない。使わない |
