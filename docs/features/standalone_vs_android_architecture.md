# System Architecture: Standalone App & Android Studio Mobile Pipeline
> **Document:** Master Platform Architecture  
> **Status:** Active Standard  
> **Author:** DETOX Snoopy Core Team  
> **Applicability:** All Snoopy Features and Modules

---

## 1. Vision & Architectural Goals

Snoopy must operate with equal fidelity across two distinct deployment targets:

1. **Standalone Application**:
   - Immediate developer velocity: run, debug, and test features locally with zero mobile emulator or Gradle overhead.
   - Usable as a responsive desktop/web application or local security tool.
   - Clean, modular decoupled codebase.

2. **Android Studio Published Application**:
   - Fully convertible, packagable, signed, and published to the Google Play Store via Android Studio.
   - Native OS integration: Android Share Sheet ("Share link with Snoopy"), clipboard observation, system push notifications, background scam database sync via Android WorkManager.
   - Compliant with all Google Play Developer Policies and Android 14/15+ security requirements.

---

## 2. Universal Layered Architecture

```mermaid
graph TB
    subgraph ClientLayer["Presentation & Surface Layer"]
        A1[Standalone Web/Desktop UI]
        A2[Android Native Activity / Jetpack Compose / WebView UI]
    end

    subgraph BridgeLayer["Platform Abstraction Bridge (IPlatformAdapter)"]
        B1[Standalone Adapter: Web APIs, LocalStorage, File System]
        B2[Android Adapter: Android Services, Room DB, Intent Handlers]
    end

    subgraph CoreEngine["Snoopy Core Engine (Platform-Agnostic)"]
        C1[Heuristic Analyzer & Rule Engine]
        C2[URL & Phishing Parser]
        C3[Message & Sentiment Scam Classifier]
        C4[Offline Red-Flag Threat Intelligence Cache]
        C5[Scoring & Verdict Engine]
    end

    subgraph ExternalServices["External Cloud Feeds (Optional)"]
        D1[Known Malicious URL Lists]
        D2[Community Fraud Reports (DETOX)]
    end

    A1 --> B1
    A2 --> B2
    B1 --> CoreEngine
    B2 --> CoreEngine
    CoreEngine --> ExternalServices
```

---

## 3. The Platform Abstraction Interface (`IPlatformAdapter`)

To prevent mobile-specific code from leaking into the core or standalone app, all OS interactions must flow through a contract interface:

```typescript
// Interface defined in /core/platform/IPlatformAdapter.ts
export interface IPlatformAdapter {
  platformName: 'standalone' | 'android';
  
  // Clipboard
  readClipboardText(): Promise<string | null>;
  
  // Storage
  getSecureItem(key: string): Promise<string | null>;
  setSecureItem(key: string, value: string): Promise<void>;
  
  // Notifications / Alerts
  showSafetyAlert(title: string, message: string, riskLevel: 'low' | 'medium' | 'high'): Promise<void>;
  
  // System Sharing
  registerShareTarget(callback: (sharedContent: string) => void): void;
  
  // Background Sync
  scheduleThreatDbUpdate(intervalMinutes: number): Promise<void>;
}
```

- In **Standalone**: Uses browser/Node APIs (`navigator.clipboard`, `localStorage`, `Notification.requestPermission()`).
- In **Android Studio**: Uses native Android Kotlin/Java bridges or Capacitor/JSI plugins calling `ClipboardManager`, `EncryptedSharedPreferences`, `NotificationCompat.Builder`, and `WorkManager`.

---

## 4. Standalone vs Android Studio Build Pipeline

### Standalone Pipeline:
1. Source files in `core/` and `standalone/`.
2. Packaged or run using standard scripts:
   - Development server / live reload
   - Fast automated unit tests (`npm test` / `pytest` / `vitest`)
   - Direct mock data feeding for instant verification.

### Android Studio Pipeline:
1. `android/` directory contains standard Android Studio project files:
   - Root `build.gradle` / `settings.gradle`
   - App module: `android/app/build.gradle`
   - Manifest: `android/app/src/main/AndroidManifest.xml`
   - Native code: `android/app/src/main/java/com/detox/snoopy/`
   - Static web assets / compiled bundle synced into `android/app/src/main/assets/`
2. Workflow in Android Studio:
   - Open project root `android/` in Android Studio.
   - Sync Gradle.
   - Run on Android Virtual Device (AVD) or physical hardware.
   - Build signed Android App Bundle (`.aab`) for Google Play Console publication.

---

## 5. Google Play Publication & Compliance Checklist

When preparing an Android Studio release:
1. **Target SDK**: Target the latest Android API level (API 34/35+).
2. **Permissions**: Keep permissions minimal. Only declare permissions strictly required (e.g. `INTERNET`, `POST_NOTIFICATIONS`). Avoid restricted permissions like `RECEIVE_SMS` unless explicitly following Google Play's SMS policy exceptions.
3. **Privacy Policy**: Explicit disclosure that user URLs or message snippets are checked locally or pseudonymized without logging personal identifiers.
4. **App Signing**: Configure Google Play App Signing with upload key keystore configured via local properties (never committed to Git).
