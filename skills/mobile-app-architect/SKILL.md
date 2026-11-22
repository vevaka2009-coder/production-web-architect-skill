---
name: mobile-app-architect
description: Exclusively built for native and cross-platform mobile applications (React Native, Flutter, Swift/iOS, Kotlin/Android, Expo). Built for AI project builders and vibe-coders building mobile apps. Detects, reports, and corrects everything AI and novice builders miss in mobile apps—including runtime permission crashes, offline-first sync & SQLite migrations, deep link cold starts, push notification token lifecycles, safe area insets (notches/dynamic islands), memory leaks & bitmap OOM, in-app purchase receipt validation, and Apple/Google store compliance (privacy manifests, in-app account deletion).
metadata:
  author: vevaka2009-coder
  version: 1.0.0
  tags:
    - mobile-apps-only
    - react-native
    - flutter
    - ios-swift
    - android-kotlin
    - vibe-coding
    - mobile-architecture
---

# Mobile App Architect & Vibe-Coding Guard (Mobile Apps Only)

> ⚠️ **STRICT SCOPE NOTICE: MOBILE APPS ONLY**  
> This skill is **strictly for mobile applications** (React Native, Expo, Flutter, iOS Swift, Android Kotlin).  
> **DO NOT USE FOR:** Web-only browser apps, desktop software, or backend automation scripts. It specifically audits mobile operating system constraints, device hardware permissions, touch gestures, mobile offline storage, safe area insets, push notification daemons, and App Store / Google Play guidelines.

Built specifically for **AI project builders and vibe-coders** creating mobile apps using AI assistants (Cursor, Claude, Devin, ChatGPT, Copilot). It automatically inspects your mobile codebase, identifies critical mobile platform oversights, explains why they will crash devices or fail app review, and writes the code and architecture plans to correct them.

## When to Activate This Skill
- When building or reviewing a **mobile application** (React Native, Flutter, Swift, Kotlin, Expo) created with AI.
- Before submitting an app to the Apple App Store or Google Play Store.
- When an app works in simulator/happy path but encounters crashes on physical devices (permission denials, backgrounding, offline disconnects, memory OOM).
- When implementing mobile hardware features: Camera/Gallery, Geolocation, Biometrics (FaceID/Fingerprint), Push Notifications, In-App Purchases, or Deep Links.

## What It Does
1. **Detects What AI Missed in Your Mobile App:** Scans the codebase across 6 essential mobile pillars and 20 critical mobile failure modes.
2. **Explains the Gaps:** Reports findings in clear language with file paths and risk ratings (`✅ Passed`, `⚠️ Partial`, `❌ Missing`).
3. **Corrects & Builds the Missing Pieces:** Generates tailored, copy-pasteable production implementations for your specific mobile framework.
4. **Multi-Agent Orchestration:** Dispatches parallel worker sub-agents (`agent-mobile-perms`, `agent-mobile-offline`, `agent-mobile-ux-insets`, `agent-mobile-push`, `agent-mobile-store-compliance`) when running in multi-agent environments.

## Quick Command
To run an instant audit on your mobile codebase, run the prompt in `commands/audit-mobile-app-readiness.md`:
```markdown
/audit-mobile-app-readiness
```
