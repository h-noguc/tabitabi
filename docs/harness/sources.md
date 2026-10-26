# 開発ハーネスの出典

調べた日: 2026-10-26。調査はAIのサブエージェントが実施。

**検証レベルの注意**: 調査環境のネットワーク制限で、多くのサイトの本文を開けなかった。
- ◎ 本文を開いた: anthropic.com、code.claude.com、raw.githubusercontent.com、github.com/gotalab/cc-sdd
- †・無印の論文: 検索結果の要約・抜粋のみ。数値は未確認。引用する前に原典で確かめる

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
| OAI | Ryan Lopopolo, "Harness engineering", OpenAI, 2026-02-11 † |
| BOE | Birgitta Böckeler, "Understanding Spec-Driven-Development", martinfowler.com, 2025-10-15 † |
| GH | GitHub Docs, Copilot coding agent のベストプラクティス † |

## 日本語記事（すべて † 。ただし cc-sdd は ◎）

| 記号 | 出典 |
|---|---|
| cc-sdd | gotalab/cc-sdd v3 https://github.com/gotalab/cc-sdd ◎ |
| SmartHR | SmartHR Tech Blog 2026-09-16 https://tech.smarthr.jp/entry/2026/09/16/110205 / 2026-03-12 https://tech.smarthr.jp/entry/2026/03/12/134348 |
| CyberAgent | https://developers.cyberagent.co.jp/blog/archives/64334/ |
| pepabo | https://zenn.dev/pepabo/articles/claude-code-rules-skills-split |
| tomada | https://qiita.com/tomada/items/cb05d3a7aa00cb35c486 |
| smartshopping | https://zenn.dev/smartshopping/articles/refactor-fat-claude-md |
| yurukusa | https://qiita.com/yurukusa/items/ab9387816b372b7ae210 |
| yureki_lab | https://qiita.com/yureki_lab/items/6f9175d70d294840311c |
| chatii | https://zenn.dev/chatii/articles/353571ee68c3d8 |
| hiroshi75 | https://zenn.dev/hiroshi75/articles/20251214_claude-code-skill-reflection-loop |
| japannomu | https://zenn.dev/japannomu/articles/20260321_claude-code-harness-control |
| kosk_t | https://zenn.dev/kosk_t/articles/adr-lightweight-decision-records-for-ai |
| ennagara128 | https://qiita.com/ennagara128/items/66e5188d0d0edd874a8d |

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
