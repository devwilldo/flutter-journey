When you **pull a Flutter project** from Git that was **pushed from an old system**, and you're setting it up **fresh on a new machine (Windows or macOS)**, follow this **clean checklist** to avoid issues and make the project run smoothly:

---

## ✅ What to Do After a Fresh Git Pull (Old Push → New System)

### 🔹 1. **Open the Project Folder**

Make sure you open the **root of the Flutter project**, where `pubspec.yaml` is located.

```bash
cd your_flutter_project
```

---

### 🔹 2. **Get All Packages**

Install project dependencies:

```bash
flutter pub get
```

> 💡 This also rebuilds `.dart_tool/`, `.packages`, and lock files (which are often ignored in `.gitignore`).

---

### 🔹 3. **(If using web) Enable Web Support**

```bash
flutter config --enable-web
```

Then re-run:

```bash
flutter pub get
```

---

### 🔹 4. **Run a Clean Build**

Clear old build files and make a clean build:

```bash
flutter clean
flutter pub get
flutter run
```

---

### 🔹 5. **(Optional) Regenerate Code**

If you use tools like `json_serializable`, `freezed`, or `build_runner`, regenerate files:

```bash
flutter pub run build_runner build --delete-conflicting-outputs
```

---

### 🔹 6. **Check for Missing Local Files**

Verify the project doesn’t need:

* `.env` files
* `firebase_options.dart`
* Keys or credentials that may be ignored in `.gitignore`

> 🔐 These might not have been committed from the old system for security.

---

### 🔹 7. **Check Platform-Specific Setup**

If you're building for:

* **iOS/macOS**: run `pod install` in the `ios/` or `macos/` directory

  ```bash
  cd ios
  pod install
  cd ..
  ```
* **Android**: Ensure `local.properties` exists (it contains SDK path)

If missing:

```bash
echo "sdk.dir=$ANDROID_SDK_ROOT" > android/local.properties
```

---

### 🔹 8. **Run on the Target Device**

```bash
flutter devices
flutter run -d chrome         # For web
flutter run -d android        # For Android
flutter run -d ios            # For iOS/macOS (on macOS only)
```

---

## 🧹 Summary Checklist

| Step | Action                                     |
| ---- | ------------------------------------------ |
| ✅    | `flutter pub get`                          |
| ✅    | `flutter clean`                            |
| ✅    | `flutter config --enable-web` (if needed)  |
| ✅    | Rebuild codegen (`build_runner`) if used   |
| ✅    | Add `.env`, `local.properties`, or secrets |
| ✅    | Run with `flutter run -d <device>`         |

---
