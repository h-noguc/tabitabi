# 0011 論点になっていない技術スタックは「推し」で確定する

状態: 決定（2026-10-26）
判断者: 自分
議論: https://claude.ai/code/session_01RRsWb1PMfgKNATkiZKYMQQ
一覧: [docs/stack.html](../stack.html)

## 決定
技術スタックのうち、論点として明記していないものは、推していた選択で確定する。0006（API の境界は持ち、中核は薄く）も決定に変える。

| 層 | 確定したもの |
|---|---|
| アプリ | TypeScript、npm workspaces のモノレポ、Hono + Zod、React + Vite（PWA）、TanStack Query、Postgres + Drizzle |
| 実行環境 | 秘密情報（本番はホスティングの環境変数、CI は GitHub secrets、手元は 1Password）、Node 版を `.node-version` で固定、クラウド環境は起動時フックで依存を入れる |
| ハーネス | GitHub Issues と入力フォーム、`specs/*.md`、Vitest・PGlite・Playwright、Biome、GitHub Actions と Lefthook、AGENTS.md を正本に CLAUDE.md はリンク、settings.json の deny とサンドボックス、フック、`/retro` スキル |

## まだ決めないもの（論点として残す）
- 地図表示と場所検索の提供元（論点3）
- DB の置き場・認証・ホスティング・環境の分け方。PostGIS の要否もここで決める（論点4）
- 会話ログの保存先（論点6）
- AC の書き方（EARS か Given/When/Then か）、パートナーの Issue の経路、Cursor も使うか

## 理由
論点として残したもの以外は、選び直しても影響が小さく、推しの理由（0006、docs/stack.html）に異論がないため。
