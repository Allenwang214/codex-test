# 手把手教學：打造文字轉語音 APP 並上架 Google Play 與 App Store

本文件示範如何使用 Flutter 建立一個簡單的文字轉語音 (TTS) 應用程式，讓使用者輸入文字後即可生成語音檔。若需要對話功能，可另外串接聊天 API（例如 OpenAI ChatGPT 或其他語言模型）。

## 1. 安裝開發環境

1. [安裝 Flutter](https://docs.flutter.dev/get-started/install)（支援 Windows、macOS、Linux）。
2. 安裝 Android Studio 或 Xcode 以便在裝置模擬器中測試。
3. 在終端機執行 `flutter doctor`，確認所有必要套件已就緒。

## 2. 建立 Flutter 專案

```bash
flutter create flutter_tts_app
cd flutter_tts_app
```

此範例的主要程式碼位於 [`flutter_tts_app/lib/main.dart`](flutter_tts_app/lib/main.dart)。

## 3. 加入 TTS 套件

在 `pubspec.yaml` 中加入 `flutter_tts` 依賴：

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_tts: ^3.5.2
```

安裝依賴：

```bash
flutter pub get
```

## 4. 實作簡易介面與語音播放

`lib/main.dart` 提供一個輸入框及「朗讀」按鈕，按下後會呼叫 `FlutterTts.speak` 播放語音。

```dart
final FlutterTts _flutterTts = FlutterTts();
final TextEditingController _controller = TextEditingController();
...
Future _speak() async {
  if (_controller.text.isNotEmpty) {
    await _flutterTts.speak(_controller.text);
  }
}
```

完整程式碼請參考 [`lib/main.dart`](flutter_tts_app/lib/main.dart)。

## 5. (選擇性) 串接對話功能

若想加入聊天機器人，可在按下朗讀前先將輸入文字送往聊天 API，取得回覆後再呼叫 TTS 播放。例如使用 [OpenAI ChatGPT API](https://platform.openai.com/docs/introduction)，或其他可用的對話服務。

## 6. 建置並上架

1. Android：
   - 於 `android/app/src/main/AndroidManifest.xml` 內設定必要權限。
   - 執行 `flutter build apk` 或 `flutter build appbundle` 產生檔案後，上傳至 Google Play Console。
2. iOS：
   - 確認在 `Info.plist` 中設定麥克風、語音等權限。
   - 在 macOS 執行 `flutter build ios`，使用 Xcode 將程式碼簽章並上傳至 App Store Connect。

上架流程需要符合各平台的政策，請依照 Google Play 與 App Store 的審核規範調整內容與隱私政策。

## 7. 進一步擴充

- 根據需求新增語音選擇、語速等設定。
- 整合登入、儲存紀錄或聊天紀錄等功能。
- 若對話服務有額外費用，記得處理 API 金鑰與流量控管。

完成以上步驟即可打造一款基礎的文字轉語音 APP，並能視需求擴充對話功能，最終上架到 Google Play 與 App Store。
