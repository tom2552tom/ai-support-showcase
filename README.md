# 🤖AI カスタマーサポートシステム

[![PHP](https://img.shields.io/badge/PHP-7.4-777BB4?style=flat-square&logo=php&logoColor=white)](https://www.php.net/)
[![CakePHP](https://img.shields.io/badge/CakePHP-2.x-D33C43?style=flat-square&logo=cakephp&logoColor=white)](https://cakephp.org/)
[![Google Gemini](https://img.shields.io/badge/Google_Gemini_API-4285F4?style=flat-square&logo=google&logoColor=white)](https://ai.google.dev/)
[![Retell AI](https://img.shields.io/badge/Retell_AI-Voice-00C7B7?style=flat-square)](https://www.retellai.com/)
[![Freshdesk](https://img.shields.io/badge/Freshdesk_API-25C16F?style=flat-square)](https://www.freshdesk.com/)
[![MySQL](https://img.shields.io/badge/MySQL-5.7-4479A1?style=flat-square&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Status](https://img.shields.io/badge/Status-本番稼働中-brightgreen?style=flat-square)]()
[![Dev Period](https://img.shields.io/badge/開発期間-2026年1〜3月-blue?style=flat-square)]()

> **Google Gemini API × Retell AI × Freshdesk** を組み合わせた、  
> Webチャット＋AI電話自動応答を一体化したカスタマーサポートシステム。  
> FAQをAIが横断検索し、**24時間365日・多言語対応のサポートを実現**。

---

## 📊 導入効果

| 指標 | 導入前 | 導入後 | 改善率 |
|------|--------|--------|--------|
| カスタマーサポート対応時間 | 基準値 | 約20% | **⬇️ 約80%削減** |
| 対応チャネル | 電話・メールのみ | Webチャット＋AI電話 | **24時間365日化** |
| FAQ参照先 | 人手で確認 | AI自動横断検索 | **即時回答** |

---

## 🎯 プロジェクト概要

カスタマーサポート業務をAIで自動化。  
問い合わせ内容をAIが解析し、Freshdesk FAQデータ・自社FAQ DB・公式サイト情報を横断的に参照して最適な回答を生成します。  
Webチャット（マイページ・公開サイト）と電話（Retell AI音声）の両チャネルに対応した統合サポートシステムです。

```
【対応チャネル】
┌─────────────────────────────────────────────┐
│  Webチャットウィジェット    │   AI電話自動応答        │
│  (マイページ・公開サイト)   │   (Retell AI連携)       │
└──────────────┬──────────────┴──────────┬────────────┘
               │                          │
               ▼                          ▼
        ┌─────────────────────────────────────────┐
        │         AiAssistantController.php        │
        │         (CakePHP 2.x バックエンド)        │
        └───────────────────┬─────────────────────┘
                            │
              ┌─────────────┼──────────────┐
              ▼             ▼              ▼
        Freshdesk      自社 FAQ DB     公式サイト
        API検索        (MySQL)         情報参照
              │             │              │
              └─────────────┴──────────────┘
                            │
                            ▼
                ┌───────────────────────┐
                │   Google Gemini API   │
                │   (回答生成エンジン)    │
                └───────────┬───────────┘
                            │
                            ▼
                ┌───────────────────────┐
                │  AI生成回答 + ソース表示 │
                │  (利用FAQ・チケット番号) │
                └───────────────────────┘
```

---

## ✨ 主な機能

### 🧠 AI回答生成
- Google Gemini API による自然言語での回答生成
- プロンプトエンジニアリングで回答精度を最適化
- 回答に利用したFAQソースを画面に表示（透明性の確保）

### 🔍 3段階FAQ検索
1. **Freshdesk API** — クラウドFAQ・チケットシステムから検索
2. **自社FAQ DB** — MySQLに蓄積した独自FAQを全文検索
3. **公式サイト情報** — サービス仕様・料金プランを参照

### 💬 Webチャットウィジェット
- **マイページ埋め込み型** — ログインユーザーの会員情報・契約情報を自動取得してパーソナライズ回答
- **公開サイト型** — 未ログインユーザー向けの汎用問い合わせ対応

### 📞 AI電話自動応答（Retell AI連携）
- Retell AI との Webhook 連携による音声会話
- 電話でのSIM契約・サポート問い合わせをAIが自動応対
- 通話ログをDBに自動保存・管理

### 📋 管理画面
- チャットログ・通話ログの一覧・詳細表示
- AI回答生成テスト（顧客メール・電話番号・チケットID指定）
- FAQ登録・編集・並び順管理

### 👤 顧客情報自動取得
- メールアドレスから会員情報・契約プランを自動取得
- US電話番号からSIM契約情報を逆引き検索
- Freshdesk チケット番号からサポート履歴を参照

---

## 🛠️ 技術スタック

| カテゴリ | 技術・ツール | 用途 |
|---------|------------|------|
| **バックエンド** | PHP 7.4 / CakePHP 2.x | APIコントローラ・ビジネスロジック |
| **AI エンジン** | Google Gemini API | 回答生成・自然言語処理 |
| **音声 AI** | Retell AI | AI電話自動応答・Webhook連携 |
| **FAQ 管理** | Freshdesk API | クラウドFAQ・チケット取得 |
| **データベース** | MySQL 5.7 | チャットログ・FAQ・顧客情報 |
| **フロントエンド** | JavaScript / jQuery | チャットウィジェット・非同期通信 |
| **認証** | APIキー認証 | 管理画面・Webhook保護 |

---

## 🗄️ データベース設計

### `chat_logs` テーブル（チャット・通話ログ）

| カラム名 | 型 | 説明 |
|---------|-----|------|
| `id` | INT | 主キー |
| `member_id` | INT | 会員ID（マイページ連携） |
| `session_id` | VARCHAR | セッション識別子 |
| `user_email` | VARCHAR | 顧客メールアドレス |
| `user_name` | VARCHAR | 顧客氏名 |
| `message_type` | ENUM | `user` / `assistant` |
| `message_text` | TEXT | メッセージ本文 |
| `detected_phone` | VARCHAR | 検出された電話番号 |
| `customer_info` | JSON | 顧客情報スナップショット |
| `response_sources` | JSON | 回答に使用したFAQソース一覧 |
| `conversation_history` | JSON | 会話履歴（マルチターン） |
| `source` | ENUM | `webchat` / `phone` |
| `phone_number` | VARCHAR | 発信元電話番号（電話AI用） |
| `call_id` | VARCHAR | Retell AI コールID |
| `is_public_chat` | TINYINT | 公開サイトからの問い合わせフラグ |
| `ip_address` | VARCHAR | アクセス元IP |
| `created` | DATETIME | 作成日時 |
| `modified` | DATETIME | 更新日時 |

### `faqs` テーブル（自社FAQデータ）

| カラム名 | 型 | 説明 |
|---------|-----|------|
| `id` | INT | 主キー |
| `question` | TEXT | FAQ質問文 |
| `answer` | TEXT | FAQ回答文 |
| `detail_url` | VARCHAR | 詳細ページURL |
| `sort` | INT | 表示並び順 |

---

## 📁 ファイル構成

```
app/
├── Controller/
│   └── AiAssistantController.php   # メインコントローラ（API・管理画面）
├── Model/
│   ├── ChatLog.php                 # チャットログモデル
│   └── Faq.php                     # FAQモデル
└── View/
    ├── AiAssistant/
    │   ├── admin_index.ctp         # 管理画面：ログ一覧
    │   ├── admin_view.ctp          # 管理画面：ログ詳細
    │   ├── admin_generate.ctp      # 管理画面：AI回答テスト
    │   ├── admin_faqs.ctp          # 管理画面：FAQ一覧
    │   └── admin_faq_edit.ctp      # 管理画面：FAQ編集
    └── Elements/
        ├── ai_chat_widget.ctp      # チャットウィジェット（マイページ用）
        └── ai_chat_widget_public.ctp # チャットウィジェット（公開サイト用）

sql/
├── create_chat_logs_table.sql      # chat_logsテーブル作成SQL
└── add_phone_columns.sql           # 電話AI対応カラム追加SQL

.env.example                        # 環境変数サンプル
```

---

## 🔗 外部API・サービス連携

| サービス | 用途 | 連携方式 |
|---------|------|---------|
| **Google Gemini API** | AI回答生成・自然言語処理 | REST API（HTTP POST） |
| **Freshdesk API** | FAQ・チケット情報取得 | REST API（Basic認証） |
| **Retell AI** | 音声AI電話・会話フロー | Webhook（POST受信） |

### 連携フロー（電話AI）
```
顧客が電話発信
    │
    ▼
Retell AI（音声認識・TTS）
    │ Webhook POST
    ▼
AiAssistantController::retell_webhook()
    │
    ├─ Freshdesk FAQ 検索
    ├─ 自社 FAQ DB 検索
    └─ Gemini API で回答生成
          │
          ▼
    Retell AI にテキスト返却
          │
          ▼
    顧客に音声で回答
```

---

## 🖥️ 管理画面

| 機能 | URL |
|------|-----|
| AI回答生成テスト | `/admin/ai_assistant/generate` |
| チャットログ一覧 | `/admin/ai_assistant/index` |
| チャットログ詳細 | `/admin/ai_assistant/view/{id}` |
| FAQ一覧 | `/admin/ai_assistant/faqs` |
| FAQ編集 | `/admin/ai_assistant/faq_edit/{id}` |

---

## 📸 スクリーンショット

### AI回答生成テスト画面（管理画面）
![管理画面 - AI回答生成](./screenshots/admin_generate.png)

### AI生成回答 + 情報ソース表示
![AI生成回答](./screenshots/ai_response.png)

> **実際の動作例:**  
> 問い合わせ: 「eSIMに切り替えたい」  
> → Freshdesk FAQ（eSIM対応・切り替え方法・EID/IMEI確認方法）を参照し、  
> 　 切り替え手順・必要情報・注意事項を自動生成・回答

---

## ⚙️ 環境変数

```env
# Freshdesk API
FRESHDESK_DOMAIN=your-domain.freshdesk.com
FRESHDESK_API_KEY=your_freshdesk_api_key

# Google Gemini API
GEMINI_API_KEY=your_gemini_api_key

# 管理画面・API認証
AI_ASSISTANT_API_KEY=your_internal_api_key
```

---

## 🚀 セットアップ（概要）

```bash
# 1. 環境変数設定
cp .env.example .env
# .env を編集して各APIキーを設定

# 2. DBマイグレーション
mysql -u root -p your_db < sql/create_chat_logs_table.sql
mysql -u root -p your_db < sql/add_phone_columns.sql

# 3. CakePHP ルーティング設定
# app/Config/routes.php に以下を追加
Router::connect('/api/ai-assistant/*', ['controller' => 'AiAssistant', 'action' => 'api']);
Router::connect('/api/retell-webhook', ['controller' => 'AiAssistant', 'action' => 'retell_webhook']);
```

> ⚠️ **ソースコードはクライアント都合により非公開です。**  
> 技術的な詳細・実装についてはお気軽にお問い合わせください。

---

## 👤 Author

**畑中 智和 (Tomokazu Hatanaka)**  
📍 Los Angeles, California  
🔗 GitHub: [https://github.com/tom2552tom](https://github.com/tom2552tom)  
📧 Email: tom2552tom@gmail.com  

---

## 🔗 関連プロジェクト

- [AIマッチングシステム](https://github.com/tom2552tom/ai-matching-system-showcase) — Django × Gemini API × Celery による案件×エンジニア自動マッチング

