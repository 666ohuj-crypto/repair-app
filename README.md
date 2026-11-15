# AutoDoc — Offline Vehicle Fault Guidance

AutoDoc is a self-contained Capacitor Android app. Its diagnostic rules run locally in the WebView; it does not call Anthropic/Claude or require a separately deployed Node.js backend.

## Features
- Car and motorcycle symptom-based diagnostic rules
- Local microphone capture and basic waveform measurements when supported by the Android WebView
- Photo/video/file capture for technician reference (media is not automatically interpreted)
- Local diagnosis history using device storage
- Searchable mechanic quick-reference guide
- Debug and release APK builds through GitHub Actions

## Build APKs
Push to `main` or run **Actions → Build AutoDoc Android APKs → Run workflow**. Download the artifact named `AutoDoc-debug-and-release-apks`.

The workflow creates a temporary release signing key for sideload testing. This release APK is not signed with a permanent company/Play App Signing key. For production distribution, configure a company-controlled keystore and keep its passwords in GitHub Actions secrets. A temporary CI signature cannot be used to publish future updates over this build.

## Local build
Requirements: Node.js 20, Java 17, Android SDK platform 34.

```sh
npm install
npx cap add android
npx cap sync android
cd android
./gradlew assembleDebug assembleRelease
```

## Important limitations
- Diagnosis is a transparent rule-based aid, not a certified inspection or an AI model. Scores indicate rule-match priority, not statistically validated fault probabilities.
- Photos and videos are stored/previewed as evidence; no offline computer-vision model is bundled.
- Audio capture/decoding depends on Android WebView microphone permissions and supported codecs.
- Local history is stored on the device and can be lost if app data is cleared or the app is uninstalled.
- Always follow vehicle-specific service data. Stop driving for brake/steering faults, fuel leaks, overheating, oil-pressure warnings or serious engine knocks.
