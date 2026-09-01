# Vistubeo プライバシーポリシー

- 制定日：2026年8月28日
- 最終更新日：2026年8月28日

## 1. はじめに

本ポリシーは、Vistubeo Public Editionが取り扱う情報と外部サービスへの送信について説明します。Vistubeoには、現時点でユーザーアカウント、ポイント、決済、広告、運営者側のAI APIサーバーはありません。

## 2. YouTube関連データ

Vistubeo Public Editionは、利用者が入力したYouTube URLを用いて、公開通常動画の動画情報、字幕、サムネイルを取得します。動画URLや動画ID、通信に伴うネットワーク情報はGoogleまたはYouTubeへ送信されることがあります。

Public Editionは動画音声のダウンロード、ライブ録音、Firefox Cookieの利用を行いません。映像・音声そのものをVistubeo運営者へ送信することもありません。GoogleおよびYouTubeによる情報の取扱いには、それぞれの規約およびプライバシーポリシーが適用されます。

## 3. OpenAI APIの利用

Vistubeoは、AI要約、AIチャプター、AI質問回答、字幕のAI翻訳でOpenAI APIを使用します。これらの機能では利用者自身のOpenAI APIキーを使用します。

AI機能を実行すると、処理に必要な字幕テキスト、タイムスタンプ付き字幕、質問文、AI処理に必要なテキストがOpenAIへ送信されます。接続テストでは、接続確認のための短い固定文字列が送信されます。映像・音声そのものをOpenAI APIへ送信する処理はありません。AI機能および接続テストを使用しない場合、これらの情報をVistubeoからOpenAI APIへ送信しません。

VistubeoはOpenAI Responses APIで`store=False`を指定します。これはVistubeoが指定するAPI設定であり、OpenAIにおける不正利用監視その他の保持や処理まで一切行われないことを保証するものではありません。OpenAI側での情報の取扱いには、OpenAIの最新の規約およびデータポリシーが適用されます。

## 4. APIキーの保存

VistubeoはOS環境変数`OPENAI_API_KEY`を優先して使用します。利用者が設定画面からAPIキーを保存した場合は、`%APPDATA%\Vistubeo\.env`へ保存します。旧QuickTubeの`.env`は、Vistubeoの初回起動時の移行に限って参照される場合があります。

Vistubeoに保存したAPIキーは現在暗号化されません。APIキーは`settings.json`には保存されず、通常の画面や診断ログへ全文を意図的に表示しません。APIキーはOpenAI APIの認証に使用されますが、Vistubeo運営者側のサーバーへ送信または収集されることはありません。Vistubeoに保存したキーは設定画面から削除できます。OS環境変数のキーは設定画面から変更・削除しません。

## 5. ローカルデータ

`%APPDATA%\Vistubeo\settings.json`には、要約の長さ、本文文字サイズ、Markdownの既定保存先が保存されます。旧QuickTubeの設定は、Vistubeoの初回起動時に安全に移行されます。利用者がMarkdown保存を実行した場合は、利用者が指定した場所へMarkdownファイルを作成します。

Public Editionは音声ダウンロードや音声文字起こしを行わないため、その機能に伴う音声一時ファイルを作成しません。

## 6. ログ・テレメトリ

現行版には、Vistubeo運営者へ利用状況、analytics、crash report、telemetry、usage statisticsを自動送信する機能はありません。

「起動時にアップデートを確認」が有効な場合、または利用者が設定画面から手動確認を実行した場合、Vistubeoは公開配布先であるGitHub Releasesへ通常のHTTPSリクエストを送信します。この確認は新しい安定版の有無を調べるためのもので、analyticsやtrackingではありません。OpenAI APIキー、YouTube URL、字幕、AI出力、ローカルパス、PCのユーザー名、固有識別子はこのリクエストへ含めません。起動時の確認は設定から無効にできます。

Vistubeoは字幕本文、翻訳本文、質問本文、APIキー、Cookieを意図的に診断ログへ出力しません。ただし、第三者ライブラリが生成する例外メッセージの内容まで完全に管理できるものではありません。

## 7. 第三者サービス

Vistubeoの利用には、機能に応じてOpenAIおよびGoogle・YouTubeのサービスが関係します。各サービスでの情報の取扱いには、それぞれのプライバシーポリシー、利用規約、APIデータポリシーが適用されます。

- [OpenAI Privacy Policy](https://openai.com/policies/privacy-policy/)
- [OpenAI API Data Controls](https://developers.openai.com/api/docs/guides/your-data)
- [Google Privacy Policy](https://policies.google.com/privacy)
- [YouTube Terms of Service](https://www.youtube.com/t/terms)

## 8. データの削除

Vistubeoに保存したAPIキーは設定画面から削除できます。その他のローカル設定は、`%APPDATA%\Vistubeo`内の関連ファイルを削除することで消去できます。利用者が保存したMarkdownファイルは、保存先から利用者自身で削除できます。

Vistubeoは運営者側のユーザーアカウントやサーバーデータベースを持たないため、運営者側で削除するアカウントデータはありません。OpenAIおよびGoogle・YouTubeが保持する情報については、それぞれのサービスへご確認ください。

## 9. セキュリティ

Vistubeoは、APIキーを通常の画面や診断ログへ意図的に表示しない設計ですが、ローカルに保存したAPIキーは現在暗号化されません。端末、Windowsユーザーアカウント、APIキーを適切に管理し、共有PCでの利用には注意してください。

## 10. 未成年者の利用

未成年者がVistubeoおよび第三者サービスを利用する場合は、必要に応じて保護者の同意を得たうえで、各サービスの利用条件を確認してください。

## 11. 本ポリシーの変更

Vistubeoの機能、外部サービス、法令または配布方法の変更に応じて、本ポリシーを変更する場合があります。重要な変更を行う場合は、配布ページなどの適切な方法でお知らせします。

## 12. お問い合わせ

問い合わせ主体：nhpokon

お問い合わせ先：[contactnhpokon@gmail.com](mailto:contactnhpokon@gmail.com)
