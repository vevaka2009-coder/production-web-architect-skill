# UNIVERSAL AI AGENT COMMAND: MOBILE APP ARCHITECTURE AUDIT & ORCHESTRATOR

```markdown
Run Command: /audit-mobile-app-readiness

You are an expert Principal Mobile Systems Architect and Lead Mobile Security Engineer. Your task is to perform an exhaustive, multi-dimensional Production Architecture & "Vibe-Coding" Anti-Pattern Audit on this MOBILE application, and orchestrate the remediation plan.

---

### PRE-FLIGHT CHECK 0: MOBILE SCOPE VERIFICATION
Confirm that this repository is a **MOBILE APPLICATION** (e.g. React Native, Expo, Flutter, iOS Swift/SwiftUI, Android Kotlin/Java).
- 🛑 **STOP CONDITION:** If this project is a website, web application, desktop software, or CLI backend script, STOP immediately and output:
  > "Error: This audit skill is strictly specialized for mobile applications (React Native, Flutter, iOS, Android). Please use the appropriate domain skill."

---

### PRE-EXECUTION CHECK: AGENT CAPABILITY DETECTION & WORKFLOW SELECTION

Before starting file analysis, evaluate your execution runtime and capabilities:
1. CAN YOU SPAWN, DELEGATE, OR INVOKE SUB-AGENTS / WORKERS?
   - Examples: Antigravity Swarm (invoke_subagent / swarm add), Claude Code task delegators, Devin subtasks, CrewAI / AutoGen / LangGraph agent pools, etc.

#### BRANCH A: If you CAN spawn sub-agents (Multi-Agent Swarm Mode):
- Do NOT perform the entire audit in a single monolithic thread.
- Spawn and delegate the audit across 5 specialized sub-agents running in parallel:
  1. `agent-mobile-perms`: Audits Runtime Permissions, Info.plist / AndroidManifest entries, Biometric Auth, and Secure Storage (Keychain / EncryptedSharedPreferences).
  2. `agent-mobile-offline`: Audits SQLite / Realm / WatermelonDB migrations, offline mutation queues, and network state listeners.
  3. `agent-mobile-ux-insets`: Audits Safe Area insets (notches/Dynamic Island), KeyboardAvoidingView, minimum 44x44pt touch targets, and Splash Screen transition.
  4. `agent-mobile-lifecycle`: Audits Deep Linking / Universal Links (cold start routing), Android physical back handler, and background/foreground lifecycle hooks.
  5. `agent-mobile-compliance`: Audits Push notification token refreshes, StoreKit / Play Billing validation, Apple Privacy Manifests (PrivacyInfo.xcprivacy), and in-app account deletion buttons.
- Each sub-agent reports its findings back to you with file references, missing code, and fixes.
- Once all sub-agents finish, aggregate their reports into the master scorecard and assign remediation tasks to dedicated builder sub-agents.

#### BRANCH B: If you CANNOT spawn sub-agents (Single-Agent Autonomous Mode):
- Execute the inspection sequentially across all 6 mobile pillars yourself following the protocol below.

---

### STEP 1: DEEP MOBILE CODEBASE INSPECTION (6 PILLARS)
Scan configuration files (`app.json`, `package.json`, `Podfile`, `build.gradle`, `Info.plist`, `AndroidManifest.xml`), navigation structures, local databases, and native bridging modules.

1. PERMISSIONS & HARDWARE GOVERNANCE:
   - [ ] Runtime permission flows (Are Camera, Location, Audio permissions requested just-in-time with explanation dialogs, or does the app crash when denied?).
   - [ ] OS manifest strings (Are `NSCameraUsageDescription`, `NSLocationWhenInUseUsageDescription` defined in iOS Info.plist and AndroidManifest?).
   - [ ] Secure storage (Are auth tokens stored in iOS Keychain / Android EncryptedSharedPreferences, NOT plain AsyncStorage / SharedPreferences?).
   - [ ] Biometrics fallback (Does FaceID / Fingerprint prompt offer graceful fallback to device passcode or account password?).

2. OFFLINE DATA & PERSISTENCE INTEGRITY:
   - [ ] Local database migration strategy (Does local SQLite, Realm, or WatermelonDB have explicit schema versioning and migration tables?).
   - [ ] Reconnection sync queue (Are offline user actions queued locally and replayed with idempotency when network connectivity returns?).
   - [ ] Network state listener (Does the app gracefully inform the user when offline via NetInfo listeners rather than throwing unhandled fetch errors?).

3. MOBILE UX, SAFE AREAS & KEYBOARD RESILIENCE:
   - [ ] Safe Area insets (Are layouts wrapped in SafeAreaProvider / SafeAreaView, preventing content overlap with notches, camera islands, and home indicator bars?).
   - [ ] Keyboard handling (Are input forms wrapped in KeyboardAvoidingView / ScrollView so the on-screen keyboard never obscures active text inputs?).
   - [ ] Touch target sizes (Do all buttons and interactive elements meet Apple/Android minimum guidelines of 44x44 pt / 48x48 dp?).
   - [ ] Splash screen flash (Is the native splash screen held until fonts, theme, and initial auth state are fully resolved, avoiding white flashes?).

4. DEEP LINKING & NAVIGATION LIFECYCLE:
   - [ ] Cold start deep link routing (Does the app handle incoming universal links / URL schemes when launched from a cold, killed state?).
   - [ ] Android hardware back button (Are modal dialogs, drawer menus, and nested stacks wired to Android BackHandler?).
   - [ ] App state transitions (Does the app pause heavy animations/timers and refresh stale data when transitioning between background and foreground?).

5. PUSH NOTIFICATIONS & IN-APP PURCHASES:
   - [ ] Push token refresh lifecycle (Are FCM / APNs tokens sent to the backend upon refresh, and are notification channels registered for Android 8+?).
   - [ ] Background notification payloads (Are silent / data-only pushes handled properly in background task handlers?).
   - [ ] In-App Purchases (IAP) (Are StoreKit 2 / Google Play Billing purchases validated server-side, with a functioning 'Restore Purchases' button?).

6. STORE COMPLIANCE & RESOURCE EFFICIENCY:
   - [ ] Apple Privacy Manifests (Does the app include `PrivacyInfo.xcprivacy` declaring required reason APIs for iOS 17+?).
   - [ ] In-App Account Deletion (Is there a functioning in-app button allowing users to delete their account and data, as mandated by Apple/Google?).
   - [ ] Image downsampling & Memory leaks (Are large images downsampled before rendering, and are navigation listeners/timers explicitly cleaned up on unmount?).

---

### STEP 2: GENERATE THE AUDIT REPORT
Present your analysis in the following structured format:

### 1. Executive Summary & Mobile Readiness Score
- Overall Score: [X / 100]
- Execution Mode Used: [Multi-Agent Swarm / Single-Agent Sequential]
- Top 3 Critical Risks: Immediate failure modes that will cause crashes, App Store rejection, or data loss.

### 2. Comprehensive Compliance Matrix
| Pillar / Category | Feature / Requirement | Status (✅ Passed / ⚠️ Partial / ❌ Missing) | File(s) / Code Evidence | Failure Impact |
| :--- | :--- | :--- | :--- | :--- |

### 3. Detailed Gap Breakdown
For each item identified as ⚠️ Partial or ❌ Missing:
- What is Missing: Exact technical explanation of what is lacking in this mobile codebase.
- Vulnerability / Production Impact: What happens on real devices or during App Store / Google Play review.
- Recommended Architecture: The correct pattern, library, or code snippet for THIS specific mobile framework.

---

### STEP 3: TAILORED STEP-BY-STEP REMEDIATION PLAN & SUB-AGENT HAND-OFF
Formulate an engineering roadmap specifically tailored to this mobile application, divided into 3 executable phases:
- Phase 1: Review Blockers & Crash Hotfixes (Missing Info.plist descriptions, Keychain tokens, unhandled permission rejections, account deletion button).
- Phase 2: Resilience & Device Polish (Safe Area insets, KeyboardAvoidingView, SQLite migrations, offline queue).
- Phase 3: Push, Deep Linking & Performance (FCM/APNs refresh, Universal Links cold start, image downsampling, memory leak cleanup).

FOR EACH PHASE, SPECIFY:
1. Target file path(s) to create or modify.
2. Architecture specification & native libraries to use.
3. Sub-agent delegation brief (if sub-agents are supported).
4. Verification command or device test case to prove the fix works.

Do not write random code snippets yet. Present the Audit and the Remediation Plan first, then ask the user which phase or item they want you to implement or delegate to sub-agents.
```
