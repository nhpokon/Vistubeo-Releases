# Vistubeo Public Edition

[English](README.en.md)

Vistubeo Public Editionは、公開されているYouTube通常動画の字幕を見やすく整理するWindows向けデスクトップアプリです。字幕、タイムスタンプ、AI要約、AIチャプター、AI質問、字幕のAI翻訳、Markdown保存を利用できます。

QuickTube は Vistubeo に名称変更しました。Vistubeoは、開発初期に「QuickTube」という名称で開発していたアプリの後継版です。既存の同名サービスとの混同を避けるため、Vistubeoへ名称変更しました。現在の一般公開対象はVistubeo Public Editionです。Vistubeo Full Edition (Development)は開発・検証用であり、一般配布の対象ではありません。

- 開発・提供：nhpokon
- お問い合わせ先：[contactnhpokon@gmail.com](mailto:contactnhpokon@gmail.com)

## できること

- YouTube字幕、動画情報、サムネイルの取得と表示
- 字幕検索とタイムスタンプからのYouTube再生
- AIによる要約、チャプター、質問回答
- 外国語字幕を設定したAI出力言語へ翻訳
- 「原文」「AI翻訳」「原文＋AI翻訳」の表示切替
- 表示中の要約等のMarkdown保存

## Public Editionで利用できないこと

Public Editionは、公開通常動画の既存字幕を利用する範囲に限定しています。次の機能・動画には対応していません。

- ライブ配信、ライブ文字起こし、ライブAI機能
- 字幕がない動画の音声ダウンロードや音声からの文字起こし
- faster-whisper fallback
- ログイン、メンバーシップ、非公開、年齢確認等が必要な動画
- Firefox Cookieを利用した再試行

取得できない動画への追加の回避操作は行いません。

## 動作環境と配布形態

Vistubeo Public EditionはWindows x64向けのonedir ZIPで配布します。インストーラーおよびMicrosoft Store版はありません。配布物は`Vistubeo.exe`を含む`Vistubeo`ディレクトリで、ZIP名は`Vistubeo-vX.Y.Z-windows-x64.zip`です。配布先は[Vistubeo Releases](https://github.com/nhpokon/Vistubeo-Releases/releases)です。

Microsoft Visual C++ Redistributable x64が必要です。VistubeoのZIPにはVC Runtimeを同梱しません。未導入の場合、Vistubeoが起動できないことがあります。Microsoft公式の[Latest supported Visual C++ Redistributable](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)を確認し、x64版を導入してください。直接ダウンロードは[vc_redist.x64.exe](https://aka.ms/vc14/vc_redist.x64.exe)です。

## v0.61.0の改善

- 動画や通信の失敗後でも再操作しやすいよう、状態管理を改善しました。
- 同じ動画を再読み込みした際に、古いAI質問結果が表示される可能性を修正しました。
- 動画時間を超えるタイムスタンプの検証を強化しました。
- 字幕描画処理を効率化し、長い字幕や検索結果の表示処理を改善しました。
- 動画時間を取得できない通常動画をLIVEと誤表示しないよう改善しました。
- Markdown保存を安全なatomic保存方式へ改善しました。
- Full EditionのFFmpeg終了処理と、エラー時の安全性を改善しました。

## 基本的な使い方

1. Vistubeo Public Editionの`Vistubeo.exe`を起動します。
2. 公開通常動画のYouTube URLを入力します。
3. 「要約」を押します。
4. 字幕、動画情報、AI要約、AIチャプターを確認します。
5. 必要に応じてAI質問、字幕のAI翻訳、Markdown保存を利用します。

動画URLにplaylist queryが付いている場合は、URLで指定された1本の動画だけを処理します。playlist単体URLには対応していません。

## 設定

設定を保存すると、表示言語、文字サイズ、要約の長さ、タイムスタンプ件数、AI出力言語、自動AI設定はすぐに反映されます。設定画面は閉じず、保存した現在値をそのまま確認できます。

表示言語は「日本語」「English」「한국어」「简体中文」「繁體中文」から選択できます。AI出力言語は「表示言語に合わせる」と、これら5言語から選択できます。「表示言語に合わせる」は現在の表示言語を使用し、明示的に選んだ言語は表示言語とは別に固定できます。この設定はAI要約、AIチャプター、AI質問の回答、字幕のAI翻訳、自動要約、自動翻訳、およびFull EditionのライブAI要約に適用されます。設定を保存するだけではOpenAI APIを呼び出しません。

設定の「初期設定に戻す」を使うと、アプリ設定を初期値へ戻せます。保存済みのOpenAI APIキー、OS環境変数、移行情報は削除しません。主なエラー表示には、次に確認する操作を案内します。

初期設定では、起動後にGitHub Releasesを1回確認し、新しい安定版がある場合だけ画面内でお知らせします。設定の「起動時にアップデートを確認」をOFFにすると、次回起動から確認通信を行いません。OFFの場合でも、設定の「今すぐアップデートを確認」から手動で確認できます。Vistubeoが更新ファイルを自動ダウンロードまたは自動インストールすることはありません。

## OpenAI APIキー（BYOK）

AI要約、AIチャプター、AI質問、字幕のAI翻訳には、利用者自身のOpenAI APIキーが必要です。APIキーが未設定でもVistubeoは起動でき、字幕や動画情報の取得は利用できます。

### 1. APIキーを作成

1. [OpenAI PlatformのAPI Keysページ](https://platform.openai.com/api-keys)を開き、OpenAIアカウントでログインします。
2. 「Create new secret key」から新しいAPIキーを作成します。
3. 表示されたキーをコピーします。完全なキーを再表示できない場合があるため、この時点でVistubeoへ設定してください。

### 2. Vistubeoへ設定

1. Vistubeoの「設定」を開きます。
2. 「APIキー」のマスクされた入力欄へ、コピーしたキーを貼り付けます。
3. 「接続テスト」を押します。
4. 成功表示を確認してから「APIキーを保存」を押します。

接続に失敗する主な理由は、APIキーの貼り付け間違い、OpenAI API側のbillingまたはquota、ネットワーク接続です。キーを確認しても改善しない場合は、OpenAI Platformのbilling設定とネットワーク接続を確認してください。

### 料金について

ChatGPT Plus / ProはChatGPTサービスの契約であり、OpenAI APIの利用料金とは別です。有料プランに加入していても、API料金が自動的に無料になるわけではありません。OpenAI APIは利用量に応じて料金が発生する場合があります。料金は[OpenAI API Pricing](https://platform.openai.com/pricing)で確認してください。Vistubeo本体は無料ですが、VistubeoはOpenAI API料金を代理請求しません。

設定で`auto_summary`または`auto_translate`（自動要約／自動翻訳）を有効にすると、動画読み込み時にOpenAI API利用が自動で発生する場合があります。どちらも初期設定ではOFFです。

### APIキーの保存・引き継ぎと安全な管理

OS環境変数`OPENAI_API_KEY`が設定されている場合はそちらが優先されます。Vistubeoで保存したキーは`%APPDATA%\Vistubeo\.env`へ平文保存されます。`settings.json`やリポジトリ直下の`.env`には保存しません。設定画面の削除ボタンで削除できるのはVistubeoが保存したキーだけで、OS環境変数は変更しません。旧QuickTubeの設定と`.env`は、Vistubeoの初回起動時だけ安全に移行されます。

`%APPDATA%\Vistubeo\.env`は現在平文保存です。通常のVistubeoバージョンアップでは、APIキーを再入力する必要はありません。新しいZIPを展開してアプリ本体を入れ替えても、同じWindowsユーザーで`%APPDATA%\Vistubeo`が残っていれば設定は引き継がれます。別PCへの移行、Windowsの再インストール、`%APPDATA%\Vistubeo`の削除、別Windowsユーザーでの利用、またはOpenAI側でキーを削除・失効した場合は、再設定が必要です。

現在は暗号化保存ではないため、共有PCでの利用には注意してください。APIキーはGitHubやチャット、スクリーンショットへ貼り付けず、第三者へ共有しないでください。漏洩した可能性がある場合は、[OpenAI PlatformのAPI Keysページ](https://platform.openai.com/api-keys)で該当キーを失効させ、新しいキーを作成してください。

接続テストは入力されたキーを使う一時的なOpenAI clientで行い、Responses APIの`store=False`を指定します。小さなAPIリクエストでも少額の利用が発生する可能性があります。

## 字幕のAI翻訳

外国語字幕は「AI翻訳」から、設定したAI出力言語へ翻訳できます。この機能はOpenAI APIを利用するAI翻訳です。翻訳完了後は原文、AI翻訳、両方の表示を切り替えられます。表示切替だけではOpenAI APIを再度呼び出しません。字幕の言語と設定したAI出力言語が同じ場合は、翻訳APIを呼び出しません。

AI要約、AI質問、AI翻訳を実行すると、処理に必要な字幕本文、タイムスタンプ付き字幕、質問文等がOpenAI APIへ送信されます。映像・音声そのものはOpenAI APIへ送信しません。詳しくは[プライバシーポリシー](PRIVACY.md)をご確認ください。

## Denoについて

DenoはVistubeoへ同梱していない任意のsystem dependencyです。VistubeoはDenoを自動ダウンロードしません。DenoがなくてもまずYouTube処理を試みますが、一部のYouTube JavaScript ChallengeではDenoが必要になる場合があります。DenoとFirefox Cookieは別の仕組みであり、Public EditionではFirefox Cookieを利用しません。

## 注意事項

- YouTubeおよびOpenAIの仕様変更により、取得やAI処理が一時的に利用できなくなる場合があります。
- AIの出力には誤りや不正確な翻訳が含まれる可能性があります。重要な内容は元動画や字幕で確認してください。
- 動画や字幕の利用にあたっては、YouTubeの規約、権利者の権利、適用される法令等を確認してください。

## ライセンス・公開文書

Vistubeo固有部分はVistubeo Proprietary Freeware Licenseで提供します。個人・法人とも無料で利用でき、業務利用も可能です。Vistubeo本体の無断再配布、再販売、改変版配布は禁止しています。Vistubeoに含まれる第三者OSSにはそれぞれのライセンスが適用され、本体ライセンスによってその権利は制限されません。

- [Vistubeo本体ライセンス](LICENSE)
- [利用規約](TERMS.md)：Vistubeoの利用条件
- [プライバシーポリシー](PRIVACY.md)：データ、APIキー、外部サービス等の取扱い
- [第三者ライセンス通知](THIRD_PARTY_NOTICES.txt)
- [Third-Party Licenses](LICENSES/)：第三者ライセンス文書
- [Source Compliance](SOURCE_COMPLIANCE.md)
