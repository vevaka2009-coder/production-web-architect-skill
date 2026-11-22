# Mobile Application Production Architecture & AI "Vibe-Coding" Field Guide
### Platform Rigor, Native Constraints, and Systemic Pitfalls in Modern Mobile Development

---

## Executive Summary: The Mobile "Vibe-Coding" Dilemma

When AI tools (Cursor, Claude, Devin) generate mobile applications (React Native, Flutter, Swift, Kotlin), they synthesize code that works cleanly inside desktop emulators under ideal conditions:
- Fast internet connection (no offline latency or dropped packets).
- Ambient desktop window sizing (no device notches, dynamic islands, or software keyboards).
- Pre-granted permissions (camera, location, photo library).

However, mobile operating systems (iOS and Android) are hostile, sandboxed environments with aggressive resource management, strict security boundaries, and mandatory App Store / Play Store guidelines. 

```
                               THE MOBILE VIBE-CODING TRAP
    Emulator Velocity
         ▲
         │      /────────────────────────── AI Vibe-Coding (Happy-Path Emulator)
         │     /
         │    /
         │   /
         │  /                              CRITICAL REAL-WORLD FAILURES:
         │ /                               - Hard crashes on Camera/Location permission denial
         │/                                - Notch / Dynamic Island content truncation
         │                                 - Auth tokens stolen via plain AsyncStorage
         │───────┬───────────────────────  - App Store rejection: Missing Account Deletion
         │       │ Physical Device Launch  - Out-of-Memory (OOM) crashes on camera photos
         │       ▼
         └─────────────────────────────────► Real-Device Operational Scale
```

This guide details the **Top 20 Critical Pitfalls** in AI-generated mobile applications, followed by production-grade architectural blueprints.

---

## Part 1: Top 20 Mobile AI & Vibe-Coding Blindspots

### 1. Unhandled Runtime Permission Denials & Missing Manifest Keys
* **The Pitfall:** AI calls `ImagePicker.launchCameraAsync()` without checking permissions first, or assumes permission is always granted. Furthermore, AI omits the required justification strings in iOS `Info.plist`.
* **Failure Mode:** On iOS, accessing the camera without `NSCameraUsageDescription` causes an immediate `SIGABRT` crash on app launch. On Android, if a user clicks "Deny", the app throws an unhandled exception or freezes.
* **Remedy (React Native / Expo):**
  ```typescript
  import { Camera, PermissionStatus } from "expo-camera";
  import { Alert, Linking } from "react-native";

  export async function requestCameraAccess(): Promise<boolean> {
    const { status, canAskAgain } = await Camera.getCameraPermissionsAsync();
    
    if (status === PermissionStatus.GRANTED) return true;

    if (canAskAgain) {
      const result = await Camera.requestCameraPermissionsAsync();
      return result.status === PermissionStatus.GRANTED;
    }

    Alert.alert(
      "Camera Permission Required",
      "Please enable camera access in your device settings to take profile photos.",
      [
        { text: "Cancel", style: "cancel" },
        { text: "Open Settings", onPress: () => Linking.openSettings() }
      ]
    );
    return false;
  }
  ```

---

### 2. Insecure Storage of Authentication Tokens (AsyncStorage / SharedPreferences)
* **The Pitfall:** AI routinely writes `AsyncStorage.setItem('jwt_token', token)`.
* **Failure Mode:** On rooted or jailbroken devices, or via automated backup extraction, plain AsyncStorage (which is an unencrypted SQLite or XML file) can be read by other apps or malware.
* **Remedy:** Store sensitive credentials exclusively in the hardware-backed secure enclave using `expo-secure-store` or `react-native-keychain`:
  ```typescript
  import * as SecureStore from "expo-secure-store";

  export async function saveAuthToken(token: string) {
    await SecureStore.setItemAsync("user_session_token", token, {
      keychainAccessible: SecureStore.AFTER_FIRST_UNLOCK,
    });
  }

  export async function getAuthToken(): Promise<string | null> {
    return await SecureStore.getItemAsync("user_session_token");
  }
  ```

---

### 3. Safe Area Insets & Dynamic Island Overlaps
* **The Pitfall:** AI wraps screens in standard `<View style={{ flex: 1, padding: 16 }}>`.
* **Failure Mode:** On modern iPhones (iPhone 14 Pro, 15, 16) and Android hole-punch displays, buttons, headers, and status bars are cut off by the Dynamic Island or obscured by the home indicator bar at the bottom.
* **Remedy:**
  ```tsx
  import { useSafeAreaInsets } from "react-native-safe-area-context";
  import { View } from "react-native";

  export function ScreenContainer({ children }: { children: React.ReactNode }) {
    const insets = useSafeAreaInsets();

    return (
      <View
        style={{
          flex: 1,
          paddingTop: insets.top,
          paddingBottom: insets.bottom,
          paddingLeft: insets.left,
          paddingRight: insets.right,
          backgroundColor: "#ffffff",
        }}
      >
        {children}
      </View>
    );
  }
  ```

---

### 4. Software Keyboard Obscuring Input Fields
* **The Pitfall:** Placing `<TextInput>` at the bottom of the screen without keyboard awareness.
* **Failure Mode:** When a user taps the input, the on-screen keyboard pops up and completely hides the input field and submit button.
* **Remedy:** Enclose interactive forms in `KeyboardAvoidingView` with platform-specific behavior and `TouchableWithoutFeedback` to dismiss:
  ```tsx
  import { KeyboardAvoidingView, Platform, ScrollView, TouchableWithoutFeedback, Keyboard } from "react-native";

  export function FormWrapper({ children }: { children: React.ReactNode }) {
    return (
      <KeyboardAvoidingView
        behavior={Platform.OS === "ios" ? "padding" : "height"}
        style={{ flex: 1 }}
      >
        <TouchableWithoutFeedback onPress={Keyboard.dismiss}>
          <ScrollView contentContainerStyle={{ flexGrow: 1 }} keyboardShouldPersistTaps="handled">
            {children}
          </ScrollView>
        </TouchableWithoutFeedback>
      </KeyboardAvoidingView>
    );
  }
  ```

---

### 5. Lack of SQLite / Realm Schema Migrations
* **The Pitfall:** When updating the local database structure, AI runs raw `CREATE TABLE IF NOT EXISTS` queries without tracking schema version numbers.
* **Failure Mode:** When existing app users update to the new version from the App Store, their local database already exists with the old columns. The app crashes with `no such column` errors upon accessing new fields.
* **Remedy:** Implement explicit user_version pragmas in SQLite:
  ```sql
  -- Run on every database open
  PRAGMA user_version;
  -- If user_version < 2:
  ALTER TABLE notes ADD COLUMN category_id TEXT;
  PRAGMA user_version = 2;
  ```

---

### 6. App Store Rejection: Missing In-App Account Deletion
* **The Pitfall:** AI builds a full authentication system with sign-up and sign-in, but omits an account deletion flow.
* **Failure Mode:** **Guaranteed App Store Review Rejection (Apple Guideline 5.1.1(v)).** Apple mandates that any app that supports account creation must also allow users to initiate deletion of their account from within the app.
* **Remedy:** Provide an explicit Danger Zone in Settings:
  ```tsx
  export function DeleteAccountSection() {
    const handleDelete = () => {
      Alert.alert(
        "Delete Account",
        "This will permanently erase all your data. This action cannot be undone.",
        [
          { text: "Cancel", style: "cancel" },
          { text: "Delete Permanently", style: "destructive", onPress: confirmDelete }
        ]
      );
    };
    return <Button title="Delete Account" color="#dc2626" onPress={handleDelete} />;
  }
  ```

---

### 7. Large Image Out-Of-Memory (OOM) Crashes
* **The Pitfall:** Rendering full 48-megapixel camera photos directly into `<Image source={{ uri }}>` tags in a flatlist.
* **Failure Mode:** Android and iOS kill the app process immediately with `OutOfMemoryError` after scrolling through 10-15 images.
* **Remedy:** Downsample images upon capture or fetch using image manipulation libraries before rendering or uploading:
  ```typescript
  import * as ImageManipulator from "expo-image-manipulator";

  export async function compressAvatar(uri: string) {
    const manipResult = await ImageManipulator.manipulateAsync(
      uri,
      [{ resize: { width: 600 } }], // Constrain max dimension
      { compress: 0.8, format: ImageManipulator.SaveFormat.JPEG }
    );
    return manipResult.uri;
  }
  ```

---

### 8. Push Notification Token Refresh & Android Channels
* **The Pitfall:** Storing the push token once during onboarding and never refreshing it. Also, failing to create Notification Channels on Android.
* **Failure Mode:** Tokens expire or change on app updates, resulting in silent notification delivery failure. On Android 8.0+, notifications never show because channels are missing.
* **Remedy:**
  ```typescript
  import * as Notifications from "expo-notifications";
  import { Platform } from "react-native";

  export async function setupPushNotifications() {
    if (Platform.OS === "android") {
      await Notifications.setNotificationChannelAsync("default", {
        name: "General Notifications",
        importance: Notifications.AndroidImportance.MAX,
        vibrationPattern: [0, 250, 250, 250],
        lightColor: "#4f46e5",
      });
    }

    const token = (await Notifications.getExpoPushTokenAsync()).data;
    // Always sync latest token with backend
    await api.post("/users/push-token", { token });
  }
  ```

---

### 9. Deep Linking & Cold Start URL Handling
* **The Pitfall:** Listening only to `Linking.addEventListener('url', ...)` which fires only when the app is already open in background.
* **Failure Mode:** When a user taps a deep link (e.g. `myapp://order/123`) while the app is closed, the app opens to the home screen instead of the target order.
* **Remedy:** Always inspect `getInitialURL()` upon app mount:
  ```typescript
  import * as Linking from "expo-linking";
  import { useEffect } from "react";

  export function useDeepLinking(navigate: (path: string) => void) {
    useEffect(() => {
      // 1. Cold start
      Linking.getInitialURL().then((url) => {
        if (url) navigate(Linking.parse(url).path || "/");
      });

      // 2. Foreground event
      const subscription = Linking.addEventListener("url", (event) => {
        navigate(Linking.parse(event.url).path || "/");
      });

      return () => subscription.remove();
    }, []);
  }
  ```

---

### 10. Apple Privacy Manifest Compliance (`PrivacyInfo.xcprivacy`)
* **The Pitfall:** Forgetting to declare `PrivacyInfo.xcprivacy` in iOS builds.
* **Failure Mode:** In iOS 17+, App Store Connect rejects binary uploads with error ITMS-91053 for apps using standard APIs (like `NSUserDefaults`, file timestamps, or disk space) without declaring required reason codes.
* **Remedy:** Add `PrivacyInfo.xcprivacy` to native iOS Xcode project or Expo plugin configuration declaring exact API categories and reasons.

---

## Part 2: Mobile Production Checklist
- [ ] Runtime permissions verified on physical Android & iOS devices.
- [ ] Auth tokens stored exclusively in Keychain / EncryptedSharedPreferences.
- [ ] Safe Area Insets verified on devices with Dynamic Island.
- [ ] KeyboardAvoidingView tested on low-end Android and small iPhone SE screens.
- [ ] Offline reconnection queue preserves user actions.
- [ ] Image downsampling applied to prevent OOM memory crashes.
- [ ] In-App Account Deletion button active in settings.
- [ ] Push notification channels created for Android 8+.
- [ ] Deep linking tested from cold (killed) state.
- [ ] Privacy manifests configured for iOS 17+.
