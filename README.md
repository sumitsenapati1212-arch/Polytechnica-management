# AgroPoly Smart — Android WebView wrapper

This is a native Kotlin Android project that opens the existing AgroPoly Smart website in Android WebView. It preserves the website as the source of truth instead of duplicating its dashboard logic.

- **App name:** AgroPoly Smart
- **Application ID:** `com.agropoly.smart` (debug builds use `com.agropoly.smart.debug`)
- **Website:** https://sumitsenapati1212-arch.github.io/Agropoly-AI/
- **Minimum Android:** Android 6.0 / API 23
- **Compile/target SDK:** 35
- **Language:** Kotlin

## Implemented in source

- Direct website launch with no intermediate in-app screen.
- WebView JavaScript and DOM storage enabled for the website's interactive dashboard.
- Horizontal page-load progress indicator.
- Friendly offline/network-error page with a retry button.
- Android Back navigates WebView history; double-Back confirmation behavior when history is exhausted.
- Same-origin HTTPS navigation remains in the app; external HTTP(S) links open in the system browser.
- `mailto:` and `tel:` links are handed to a suitable system app. Other non-HTTP schemes are rejected.
- HTML file chooser support for website file inputs (including leaf-photo upload where the WebView exposes the input).
- HTTP(S) downloads use Android DownloadManager and include available session cookies.
- Cookies persist through Android WebView's CookieManager; third-party cookies are disabled by default.
- TLS certificate errors are cancelled; mixed content and cleartext app traffic are disabled.
- WebView Safe Browsing is enabled on supported Android versions.
- No advertising SDK, app-added ads, tracking SDK, or notification promotions are included.
- Minimal permissions: Internet and network-state access only.

## Important limitations

- This is a WebView shell. Website features that depend on server APIs, ESP32 hardware, external services, or a reachable network still depend on those services working. The Android wrapper cannot make a missing backend available.
- Website-provided advertising, if any appears in the website later, has not been removed or tested. The app does not add advertisements or implement an ad blocker.
- The file picker is supported. Camera capture behavior depends on the website's HTML input and the installed WebView/file-picker implementation; a dedicated native camera flow is not included.
- External links open in the device's browser rather than inside the app.
- This environment did not have Android SDK, Gradle, or ADB installed. Therefore no APK was compiled, installed, or runtime-tested here. The project is source code ready to open and build in Android Studio, subject to the SDK/plugin versions being available.

## Build a debug APK in Android Studio

1. Install the current stable Android Studio and its Android SDK Platform 35, Android SDK Build-Tools, and JDK 17.
2. Extract this project ZIP.
3. In Android Studio choose **Open** and select the `AgroPolyAndroid` folder.
4. Allow Gradle sync to finish.
5. Select **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
6. The debug APK will normally be at `app/build/outputs/apk/debug/app-debug.apk`.
7. Transfer the APK to your Android phone, open it, and allow installation from that file manager if Android asks. Only install APKs from sources you trust.

You can also build from a terminal after installing Gradle and Android SDK:

```bash
gradle assembleDebug
```

## Build a signed release APK

1. In Android Studio choose **Build → Generate Signed Bundle / APK**.
2. Select **APK**, then create or select a keystore you control.
3. Keep the keystore and passwords private and outside source control.
4. Choose the `release` build variant and complete the wizard.
5. Test the signed APK on a real device before distributing it.

No signing credentials are embedded in this project, and no signed release APK is included.

## Suggested device QA checklist

- Launch with a working connection and confirm the dashboard appears.
- Switch through Dashboard, Sensors, Analytics, Irrigation, Ventilation, Crops, AI Scanner, Fertilizer, Weather, Economics, and ESP32 Setup.
- Test Back navigation and external links.
- Upload a supported image in AI Scanner and verify the site's diagnostic flow.
- Test file downloads, if the website offers them.
- Test offline launch, then reconnect and retry.
- Test portrait and landscape orientations, keyboard resizing, and different screen sizes.
- If using physical ESP32 hardware, verify the backend endpoint and hardware command flow separately; this project does not emulate or validate the hardware.
- Inspect the website for ads independently; no advertisement-removal behavior is claimed.
