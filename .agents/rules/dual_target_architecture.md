# Rule: Dual-Target Architecture (Standalone & Android Studio)

## Overview
Snoopy is designed to be shipped in two distinct formats:
1. **Standalone Application**: A self-contained application (web/desktop/engine) that can be run, developed, and tested quickly on any standard workstation without requiring Android toolchains.
2. **Android Studio Application**: A mobile application built, compiled, packaged, signed, and published to Google Play using Android Studio.

## Architecture Guidelines

### 1. Platform-Agnostic Core (`/core`)
- All detection heuristics, rule engines, URL parsers, phishing checkers, scam pattern matching, database lookups, and shared data models must reside in `/core`.
- The `/core` library must NEVER import Android platform APIs (`android.*`, `androidx.*`, etc.) or desktop-only APIs directly.
- Use interface-based design or adapter patterns for any platform-dependent capabilities:
  - Clipboard reading
  - Local push notifications
  - File / database storage
  - Background task scheduling
  - Network reachability and proxy detection

### 2. Standalone Application (`/standalone`)
- Contains the web or desktop runner, developer test harness, local web UI, or CLI interface.
- Imports `/core` directly.
- Emulates platform capabilities in a developer-friendly way (e.g. mock notifications in the browser, file-based local storage).

### 3. Android Studio Integration (`/android`)
- Contains the native Android Studio project structure:
  - `build.gradle` (Project & App level)
  - `AndroidManifest.xml` (Permissions, Intent filters, activities)
  - Java/Kotlin source files for platform bridges
  - Resource folders (`res/`, drawables, layouts, mipmap icons)
  - Release signing and Proguard / R8 configurations
- Platform-specific features to support in Android Studio:
  - **Share Sheet Receiver**: Allows users to "Share to Snoopy" from any browser or messaging app to instantly check a URL or message.
  - **Notification / SMS scam listener** (where allowed by Google Play permissions).
  - **Offline Scam Database**: Local SQLite / Room or encrypted key-value store synced with the core engine.
  - **Background Worker**: Android WorkManager for periodic rule updates.

## Android Studio Publication Checklist
Before promoting any feature or code change to the Android packaging pipeline:
- [ ] Ensure all Android permissions in `AndroidManifest.xml` comply with Google Play Developer Policies.
- [ ] Ensure core logic changes compile cleanly in both the standalone environment and Android Gradle build.
- [ ] Do not leave hardcoded URLs or development debug tokens in production Android builds.
- [ ] Verify that asset synchronization between `/core` or `/standalone` and `/android/app/src/main/assets` is up to date.
