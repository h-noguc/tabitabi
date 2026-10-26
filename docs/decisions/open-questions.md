# 未決の論点と順序

上から順に決める。決まったら判断記録にして、ここから消す。

| # | 論点 | メモ |
|---|---|---|
| 3 | 場所検索・地図表示の提供元 | Google Places / OSM 系（Photon など）/ 併用。規約（保存可否・表示条件）と OSS 化で比較。必要な網羅性（小さな飲食店まで要るか）が決め手 |
| 4 | DB・認証・ホスティング | Postgres 系を前提。Neon + 認証（Better Auth など）か、Supabase を Postgres と認証だけに使うか。判断軸: 素の Postgres、位置検索、認証込みの手軽さ、料金、ネイティブでの利用 |
| 5 | アプリのスタック | TypeScript モノレポ（apps/api: Hono+Zod、apps/web: React+Vite、packages/domain、後で apps/mobile: Expo）。0006 の確定が前提 |
| 6 | 意思決定とセッションログの保存 | 判断記録はこのディレクトリ。Claude のセッションログは Stop/SessionEnd フックで秘密を除いて別DBへ。アプリのDBとは分ける。収集の仕組みはこのレポの外に置く |
| 7 | 既存 places_stock の扱い | Maps リストからの一回限りの取り込みとして使う |
| 8 | 最小のハーネス | README/CLAUDE.md、仕様と AC、Vitest、PR で動く CI |

（論点1「正本と Google との関係」は 0005、論点2「データモデル」は 0010 で決定）
