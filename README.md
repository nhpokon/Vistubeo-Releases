# Vistubeo

Vistubeoは、公開されているYouTube通常動画の字幕を見やすく整理する
Windows x64向けデスクトップアプリです。

Vistubeoは、開発初期にQuickTubeという名称で開発していたアプリの
後継版です。既存の同名サービスとの混同を避けるため、Vistubeoへ
名称変更しました。

## 主な機能

- YouTube字幕の表示と検索
- AIによる動画要約
- 字幕時刻に基づくタイムスタンプとAIチャプター
- 動画内容へのAI質問
- 外国語字幕の日本語AI翻訳

## OpenAI APIキー

AI要約、AIチャプター、AI質問、字幕のAI翻訳には、利用者自身のOpenAI
APIキーが必要です（BYOK）。ChatGPT Plus / Proの契約とOpenAI APIの
利用料金は別であり、API利用料金が利用者のOpenAIアカウント側で発生する
場合があります。VistubeoはOpenAI API料金を代理請求しません。

## 動作環境

- Windows x64
- Microsoft Visual C++ Redistributable x64（必須）
- Deno（任意。一部のYouTube JavaScript Challengeで必要になる場合あり）

## ダウンロード

公開版は[Releases](https://github.com/nhpokon/Vistubeo-Releases/releases)から
ダウンロードしてください。Vistubeoはonedir ZIPで配布します。

## 公開文書

- [Vistubeo本体ライセンス](LICENSE)
- [プライバシーポリシー](PRIVACY.md)
- [利用規約](TERMS.md)
