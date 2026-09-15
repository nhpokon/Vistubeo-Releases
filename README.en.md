# Vistubeo Public Edition

[日本語](README.md)

Vistubeo Public Edition is a Windows desktop application for viewing and organizing transcripts from public YouTube videos. It provides transcripts, timestamps, AI summaries, AI chapters, AI questions, AI translation of foreign-language transcripts, and Markdown export.

Vistubeo is the successor to the application's former development name, QuickTube. Vistubeo Public Edition is the version intended for general distribution. Vistubeo Full Edition (Development) is for development and verification and is not distributed publicly.

- Developed and provided by: nhpokon
- Contact: [contactnhpokon@gmail.com](mailto:contactnhpokon@gmail.com)

## What you can do

- Retrieve and display YouTube transcripts, video information, and thumbnails
- Search transcripts and open the matching time in YouTube
- Use AI summaries, chapters, and answers to questions about a video
- Translate foreign-language transcripts into the configured AI output language
- Switch between Original, AI Translation, and Original + AI Translation
- Save displayed summaries and related information as Markdown

## Public Edition limitations

Public Edition is limited to using existing transcripts from public, regular YouTube videos. It does not support:

- Live streams, live transcription, or live AI features
- Audio downloads or transcription from audio when a video has no transcript
- faster-whisper fallback
- Videos that require sign-in, membership, age verification, or similar access
- Firefox Cookie retry

Vistubeo does not add further workarounds for unavailable videos.

## Requirements and distribution

Vistubeo Public Edition is distributed as a Windows x64 onedir ZIP. There is no installer or Microsoft Store version. The distribution contains a `Vistubeo` directory with `Vistubeo.exe`; ZIP files are named `Vistubeo-vX.Y.Z-windows-x64.zip`. Downloads are available from [Vistubeo Releases](https://github.com/nhpokon/Vistubeo-Releases/releases).

Microsoft Visual C++ Redistributable x64 is required. It is not bundled in the Vistubeo ZIP, and Vistubeo may not start if it is missing. See Microsoft's [Latest supported Visual C++ Redistributable](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) and install the x64 version. The direct installer is [vc_redist.x64.exe](https://aka.ms/vc14/vc_redist.x64.exe).

## Improvements in v0.62.0

- Added Windows-style right-click menus for copying displayed transcripts, AI summaries, and AI answers, plus standard editing commands in URL, search, and question fields.
- Improved rendering and searching for long transcripts while preserving multilingual text display.
- Shows a clear duration-unavailable message instead of LIVE when a regular video's duration cannot be retrieved.
- Made Settings and Markdown saving more resilient by using safer atomic-save handling.
- Improved recovery when changing videos or when video and network processing fails, including protection against outdated AI question results.
- Strengthened timestamp boundary handling and retry-state recovery.
- Improved Full Edition FFmpeg cleanup and error safety. Sensitive command details, stream URLs, and tokens are not shown in user-facing errors or logs.

## Basic use

1. Start `Vistubeo.exe`.
2. Enter the URL of a public, regular YouTube video.
3. Select **Summarize**.
4. Review the transcript, video information, AI summary, and AI chapters.
5. Use AI questions, AI translation, or Markdown export as needed.

If a video URL contains a playlist query, Vistubeo processes only the video specified by that URL. Playlist-only URLs are not supported.

## Settings

When you save Settings, the display language, font size, summary length, timestamp count, AI output language, and automatic-AI settings apply immediately. The Settings window stays open and continues to show the saved current values.

Choose the display language from **Japanese**, **English**, **Korean**, **Simplified Chinese**, or **Traditional Chinese**. For AI Output Language, choose **Match Display Language** or any of those five languages. **Match Display Language** uses the current display language; an explicitly selected language stays fixed independently of it. This setting applies to AI summaries, AI chapters, answers to AI questions, AI translation of transcripts, automatic summaries, automatic translations, and live AI summaries in Full Edition. Saving Settings alone does not call the OpenAI API.

Use **Reset to Defaults** in Settings to restore application settings to their defaults. It does not delete a saved OpenAI API key, operating-system environment variables, or migration information. Major error messages also explain the next action to take.

By default, Vistubeo checks GitHub Releases once after startup and shows an in-app notice only when a newer stable version is available. Turn off **Check for updates at startup** in Settings to disable this request from the next startup. Even when it is off, you can check manually with **Check for Updates Now** in Settings. Vistubeo does not automatically download or install updates.

## OpenAI API key (BYOK)

AI summaries, AI chapters, AI questions, and AI translation require your own OpenAI API key. Vistubeo can still start without an API key, and transcript and video-information features remain available.

### 1. Create an API key

1. Open [OpenAI Platform API Keys](https://platform.openai.com/api-keys) and sign in to your OpenAI account.
2. Select **Create new secret key** to create an API key.
3. Copy the displayed key. The full key may not be shown again, so enter it in Vistubeo at this time.

### 2. Set it in Vistubeo

1. Open **Settings** in Vistubeo.
2. Paste the key into the masked **API Key** field.
3. Select **Test Connection**.
4. After a successful result, select **Save API Key**.

Common connection failures include an incorrect key, OpenAI API billing or quota issues, and network connectivity. Check the key, your OpenAI Platform billing settings, and your network connection.

### API costs

ChatGPT Plus or Pro is a subscription for the ChatGPT service and is separate from OpenAI API billing. A paid ChatGPT plan does not automatically make API usage free. OpenAI API charges may apply based on use; see [OpenAI API Pricing](https://platform.openai.com/pricing). Vistubeo is free, but it does not bill for OpenAI API usage on your behalf.

Enabling `auto_summary` or `auto_translate` can automatically use the OpenAI API when a video is loaded. Both settings are OFF by default.

### API key storage, retention, and security

The `OPENAI_API_KEY` operating-system environment variable takes priority when it is set. A key saved by Vistubeo is stored in plaintext at `%APPDATA%\Vistubeo\.env`; it is not stored in `settings.json` or a repository-root `.env` file. The delete button removes only the key saved by Vistubeo and does not change the operating-system environment variable. On the first Vistubeo launch, eligible legacy QuickTube settings and `.env` data can be migrated safely.

You normally do not need to enter your API key again when updating Vistubeo. Replacing the application files with a newly extracted ZIP preserves the setting as long as `%APPDATA%\Vistubeo` remains for the same Windows user. Set the key again when moving to another PC, after reinstalling Windows, after deleting `%APPDATA%\Vistubeo`, when using a different Windows user, or if the key was deleted or revoked on OpenAI's side.

Because the saved `.env` is currently plaintext, take care on shared computers. Do not share an API key, commit it to a public repository, or include it in screenshots. If you suspect exposure, revoke the old key in [OpenAI Platform API Keys](https://platform.openai.com/api-keys) and create a new key if needed.

Connection tests use a temporary OpenAI client for the entered key and set `store=False` for the Responses API. Even a small test request may incur a small API charge.

## AI translation of transcripts

Use **Translate with AI** to translate a foreign-language transcript into the configured AI output language. This is an OpenAI API-based feature. After translation, you can switch between the original, AI translation, and both. Changing the display mode does not make another OpenAI API request. If the transcript language already matches the configured AI output language, Vistubeo does not call the translation API.

When you run AI summaries, questions, or translations, the required transcript text, timestamped transcript text, and question text are sent to the OpenAI API. Video and audio files themselves are not sent to the OpenAI API. See the [Privacy Policy](PRIVACY.md) for details.

## About Deno

Deno is an optional system dependency and is not bundled with Vistubeo. Vistubeo does not download it automatically. Vistubeo first attempts YouTube processing without Deno, but Deno can be required for some YouTube JavaScript Challenges. Deno and Firefox Cookies are separate mechanisms; Public Edition does not use Firefox Cookies.

## Notes

- YouTube and OpenAI changes can temporarily make retrieval or AI features unavailable.
- AI output can contain errors or inaccurate translations. Verify important information against the original video or transcript.
- When using videos and transcripts, confirm YouTube's terms, rights holders' rights, and applicable laws.

## License and public documents

Vistubeo-specific portions are provided under the Vistubeo Proprietary Freeware License. Individuals and organizations may use it free of charge, including for work. Unauthorized redistribution, resale, and distribution of modified Vistubeo versions are prohibited. Third-party OSS included with Vistubeo remains subject to its respective license; the Vistubeo license does not limit those rights.

- [Vistubeo License](LICENSE)
- [Terms of Use](TERMS.md): Terms for using Vistubeo
- [Privacy Policy](PRIVACY.md): Handling of data, API keys, and external services
- [Third-Party License Notices](THIRD_PARTY_NOTICES.txt)
- [Third-Party Licenses](LICENSES/): Third-party license documents
- [Source Compliance](SOURCE_COMPLIANCE.md)

The License, Terms of Use, and Privacy Policy are currently provided in Japanese.
