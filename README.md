
# ⬛️ News RSS Reader (AI-Powered)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![Vanilla JS](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

Obsidianのターミナルを彷彿とさせる洗練されたダークUIを備えた、**ローカルファースト・AI駆動型**のシングルページRSSリーダーです。
サーバーやデータベースの構築は一切不要。このHTMLファイルをブラウザで開くだけで、最新情報の収集からAIによる自動フィルタリング・翻訳までが完結します。

## ✨ 主な機能 (Features)

### 📰 スマートなRSS管理
- **複数フィードの取得**: CORSプロキシ (`allorigins.win`) を経由し、あらゆるRSS/Atomフィードを安全に取得。
- **スワイプアクション**: モバイルに最適化された直感的な操作。
  - 👉 **右スワイプ**: お気に入り（★）に追加
  - 👈 **左スワイプ**: 記事の削除（非表示）
- **無限スクロール**: スクロールに応じたシームレスな追加読み込み。

### 🤖 強力なAIパイプライン連携
お好みのLLM APIを使用して、取得した記事を自動分析・分類します。
- **マルチプロバイダー対応**: Gemini, OpenAI (ChatGPT), Anthropic (Claude), xAI (Grok) のAPIキーをネイティブサポート。
- **カスタムプロンプト**: `{{TITLE}}`, `{{CONTENT}}`, `{{PREV_RESULT}}` 変数を用いて、独自のAIタスク（関連度判定、要約、感情分析など）を直列で実行可能。
- **AIタグフィルタリング**: AIの判定結果をもとに、記事をワンクリックで絞り込み。

### 🌐 DeepL連携による即時翻訳
- DeepL APIキーを設定することで、記事のタイトルと概要をワンクリックで高精度な日本語に翻訳します。

### 💾 究極のローカルファースト・プライバシー設計
- **IndexedDB**: 記事データ、設定、**APIキー**など全てのデータはブラウザ内にのみ保存されます。外部サーバーへのデータ漏洩の心配はありません。
- **File System Access API**: ローカルPC上のJSONファイルに自動同期（バックアップ）可能。
- **スマートクリーンアップ**: 削除した記事は3日後にデータベースから自動的に物理削除され、ストレージを圧迫しません。

---

## 🚀 使い方 (Getting Started)

### 1. 起動方法
本アプリはビルド不要です。リポジトリをクローンまたはダウンロードし、`index.html` をお好みのモダンブラウザ（Chrome, Edge, Safari推奨）で開くだけで起動します。

### 2. 初期設定 (Settings)
右上の歯車アイコン（⚙️）から設定画面を開き、以下の設定を行います。

1. **RSSフィードの追加**: 購読したいサイトのRSS URLを入力し「追加」をクリックします。
2. **APIキーの登録**: AIフィルタリングや翻訳機能を利用する場合は、対応するAPIキーを入力して「キーを保存」を押します。（※キーはブラウザのローカルDBに暗号化なしで保存されます。個人利用端末でのみ設定してください）
3. **AIパイプラインの有効化**: トグルスイッチをONにし、判定タスクを追加します。

### 3. 記事の取得
トップ画面に戻り、ヘッダーの更新ボタン（🔄）をクリックすると記事の取得とAI処理が開始されます。

---

## 🧠 AIパイプラインの活用例

設定画面の「AIタスク」では、以下のようなプロンプトを設定することで、高度な情報収集が可能になります。

**例: AI関連ニュースのみを抽出するタスク**
```text
以下の記事はAI、機械学習、LLM、または関連技術について記述していますか？
回答は「AI関連: true」または「AI関連: false」から始め、理由を1文で述べてください。

タイトル: {{TITLE}}
概要: {{CONTENT}}
```
*※タスクを複数追加した場合、直前のAIの出力結果を `{{PREV_RESULT}}` として次のプロンプトに引き継ぐことができます。*

---

## 🛠 技術スタック (Tech Stack)

- **UI/UX**: HTML5, CSS Variables, CSS Animations
- **Logic**: Vanilla JavaScript (ES6+)
- **Storage**: IndexedDB (Local Database), File System Access API
- **Security**: [DOMPurify](https://github.com/cure53/DOMPurify) (XSSサニタイゼーション)
- **APIs**: 
  - 各種LLM API (RESTful)
  - DeepL API
  - Wake Lock API (AI処理中のスリープ防止)

---

## ⚠️ 注意事項・制限事項

- **CORSプロキシ**: 本アプリは `api.allorigins.win` を利用してRSSを取得します。機密性の高い社内ネットワーク等のRSS取得には適さない場合があります。
- **API利用料**: OpenAIやAnthropic等のAPIを利用する場合、各プロバイダーの従量課金が発生します。利用状況は各プラットフォームのダッシュボードでご確認ください。
- **ブラウザ互換性**: File System Access APIなど一部の最新機能は、SafariやFirefoxでは動作が制限される場合があります。Chromium系ブラウザでの利用を推奨します。

---

## 📄 ライセンス (License)

このプロジェクトは [MIT License](LICENSE) のもとで公開されています。自由に改変、再配布、商用利用が可能です。
```

### 💡 README作成のポイント
1. **デザインの特徴を言語化**: CSSの解析結果から、「Obsidian風」「ターミナル風」といった開発者が意図したデザインの魅力を言語化して冒頭に配置しました。
2. **AIパイプラインの図解（文章化）**: このアプリの最大の特徴である「変数を活用したタスクの直列実行」を分かりやすく解説しました。
3. **セキュリティとプライバシーの明記**: APIキーがどう保存されるか（IndexedDBへのローカル保存）を明記し、ユーザーに安心感と注意喚起の両方を与えています。
4. **モダンなバッジ・絵文字**: GitHubなどで映えるように視覚的な装飾を施しています。