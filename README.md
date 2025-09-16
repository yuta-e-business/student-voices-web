# 学生の声 / Student Voices (Express + SQLite)

授業選択の参考になる「学生の声（レビュー）」を集約・共有する Web アプリです。  
**Express（Node.js）× SQLite** で、認証・コメント投稿・科目（シラバス）閲覧を実装。  
スクレイピングによる科目データ投入、セッション管理、DAO 層分離など、**バックエンド実装と設計面の工夫**を重視しています。

> **プライバシーと再配布に関する方針**  
> リポジトリには **個人情報を含む実データや実DBは同梱しません**。  
> 動作再現は `db/schema.sql` と **ダミー** `db/seed.sql` を用いて行います。  
> スクレイピングした実HTMLやメールアドレス等の情報は**配布しません**（必要時は取得手順のみを公開）。

---

## 1. 主要機能
- **ユーザー登録 / ログイン**（セッションベース認証）
- **科目一覧 / 詳細の閲覧**
- **コメント投稿・閲覧**（ユーザーごと）
- **スクレイピング（ETL）での科目データ投入**（手順・サンプルのみ公開）
- **入力バリデーション / SQL インジェクション対策（プレースホルダクエリ）**

---

## 2. アーキテクチャ（バックエンドの責務分割）

```mermaid
flowchart LR
  A[Browser<br/>HTML/CSS/JS] --> B[Express<br/>Routing/Controller]
  B --> C[Service Layer<br/>Validation/Rules]
  C --> D[DAO Layer<br/>SQLite3 prepared statements]
  D --> E[(SQLite DB)]
  B --> F[Auth & Session<br/>express-session]
  B --> G[Scraper CLI<br/>取得手順のみ公開]
