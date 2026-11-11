# motorsport-portal-data

iOS アプリ「Motorsport Portal」が起動時に読み込む日程データです。
GitHub Pages で公開しています：

https://feninaadmin.github.io/motorsport-portal-data/schedule.json

- ここを更新すると、アプリのアップデートなしで全ユーザーの日程が更新されます。
- 読み込めない時（オフラインなど）は、前回保存したデータか、アプリに入っているデータを使います。
- このデータは各シリーズが公式に発表している日程をもとに、開発者がまとめたものです。

## schedule.json の形式（schemaVersion 1）

| 項目 | 内容 |
|---|---|
| `schemaVersion` | 形式のバージョン。アプリが知らない番号なら読み込まない |
| `updated` | データ更新日（`yyyy-MM-dd`）。アプリの「データ更新日」に表示 |
| `links.privacyPolicy` / `links.contact` | アプリ内のプライバシーポリシー・お問い合わせのリンク先 |
| `seasons[]` | シリーズごとのシーズン（`series` は `F1` / `MotoGP` / `Formula E` / `WEC` / `IndyCar` / `WSBK`。WSBK はアプリの設定でオンにした人だけに表示） |
| `nextSeasonOpeners[]` | 次シーズンの開幕戦（シーズンオフのウィジェット表示用） |

ラウンド：`label`, `name`, `circuit`, `start` / `end`（開催日 `yyyy-MM-dd`）, `sessions[]`, `cancelled`（省略時 false）, `note`（任意）

セッション：
- `name`：セッション名（日本語。アプリ内で各言語に翻訳）
- `start`：開始時刻（UTC、`yyyy-MM-ddTHH:mmZ`）。`time: false` の時は日付のみ（`yyyy-MM-dd`）
- `time`：false = 時刻未発表（省略時 true）
- `est`：true = 予想時刻（通知しない。省略時 false）
- `class`：下位カテゴリのセッション（`F2` / `F3` / `Moto2` / `Moto3`）。F1・MotoGP のラウンドの中に入れる。アプリの設定でオンにした人だけに表示、ウィジェットには出さない。省略時はメインのセッション

## 互換性の注意
- 1.1 以降のアプリが読む。今後も既存の項目の意味は変えず、項目の追加だけにする（古いアプリは知らない項目を無視する）
- 形式を大きく変える時は `schemaVersion` を上げる（古いアプリはそのデータを読まず、保存済みのデータを使い続ける）
