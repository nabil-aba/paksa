# PAKSA 🔨

> **Paksa Buat Aplikasi Android** — Ultra-lightweight Android project generator for Windows & Linux + VS Code.

Create a new Android project in seconds directly from the terminal. Choose a template, fill in the app name and package, and your project is ready to open in VS Code — **without manual setup**.

Designed specifically for developers coding on **low-end laptops (Potato PCs)** who still want to use the latest Android APIs without overheating their laptop.

Built with ❤️ from Indonesia.

***

## ✨ Why PAKSA?

* **Pure CLI Build:** Runs purely with Gradle and the Command-Line — your RAM is completely safe!
* **100% Portable Toolchain:** Does not pollute your OS Environment Variables (`PATH`, `JAVA_HOME`, `ANDROID_HOME`) at all. All tools are neatly isolated inside the `tools/` folder.
* **Isolated Gradle Cache:** By default, Gradle dumps gigabytes of dependency cache into `%USERPROFILE%\.gradle` (Windows) or `~/.gradle` (Linux) — scattered across your system. PAKSA redirects all of that into `tools/.gradle_cache` inside its own folder, keeping your home directory clean and everything self-contained.
* **Smart Zero Configuration:** No need to bother with Google SDK licenses or JDK installation. Just run `setup.exe` once. The setup is also smart enough to re-sync the configuration without re-downloading if the files already exist.
* **Cross-Platform Watch Mode:** *Auto-Rebuild* feature powered purely by Native OS API! Every time you save a file (`Ctrl+S`), PAKSA automatically builds and restarts the app on your phone. No RAM overhead, no Node.js/Nodemon required!
* **Ultra-Fast Native Engine:** No longer relying on slow PowerShell or CMD. Downloading, extracting ZIPs, and replacing *package names* are all executed instantly at memory (RAM) level using a Rust engine.
* **Smart Auto-Uninstall:** Frequently hitting `INSTALL_FAILED_UPDATE_INCOMPATIBLE` errors when switching between Release and Debug builds? PAKSA automatically detects *signature* conflicts and performs a silent *clean install*.
* **Smart Crash Parser:** App suddenly *Force Closing*? A dedicated menu pulls crash logs from ADB, filters by package name & PID, and points directly to the Java/Kotlin line causing the error — no Android log noise.
* **Smart ADB Wi-Fi:** Interactive wireless connection feature for Android 10 & 11+. For users who frequently get *stuck at 97%* when installing apps via Wi-Fi, PAKSA has a master tactic (Local Web Server Tunneling)!
* **Auto-Output & AAB Support:** Build results (APK & AAB) are automatically saved neatly in the `output/` folder. Ready to upload to the Play Store without hunting for files deep inside Gradle folders!
* **Modern Standard:** Pre-configured with **Android API 37**, **Build Tools 37.0.0**, **Jetpack Compose** support, and the **Latest Gradle**.
* **Multi-Language Interface:** The CLI interface is now available in Indonesian and English. Preferences are automatically saved to `paksa_config.json`.

***

## 🤖 PAKSA AI Assistant (Experimental Beta)

PAKSA comes with a smart AI Code Generator that can write *boilerplate* code (MainActivity, Layout, Theme, and Manifest configuration) based on your natural language instructions.

### How to Configure AI (Universal Hybrid Client)
On first launch, PAKSA will create a **`paksa_config.json`** file. You are free to use any AI model without needing to recompile the application.

**Option 1: Using Google AI Studio (Gemini) - FREE & Fast**
Get a free API Key at [Google AI Studio](https://aistudio.google.com/), then edit `paksa_config.json` to:
```json
{
  "api_url": "https://generativelanguage.googleapis.com/v1beta/models/gemini-3.5-flash:generateContent",
  "api_key": "AIzaSy...YOUR_API_KEY_HERE",
  "model": "gemini-2.5-flash"
}
```

**Option 2: Using OpenRouter (Supports DeepSeek, Claude, Llama)**
Get an API Key at [OpenRouter](https://openrouter.ai/), then set the configuration:

```json
{
  "api_url": "https://openrouter.ai/api/v1/chat/completions",
  "api_key": "sk-or-v1-...YOUR_API_KEY_HERE",
  "model": "google/gemini-3.5-flash"
}
```

*(Note: PAKSA's AI system includes *Anti-Hallucination* protection, automatic Manifest theme synchronization, and Auto-Dependency Injection. Just type your idea and run it on your phone!)*

***

## 🛠️ One-Time Setup (Just 1 Click!)

Forget the old way of manually installing Java and the Android SDK. PAKSA is powered by **100% Native RUST 🦀** that automates everything safely and quickly.

1. Download or *clone* this repository:
   ```bash
   git clone https://github.com/nabil-aba/paksa.git
   cd paksa
   ```
2. Run **`setup.exe`** (Windows) or **`./setup`** (Linux).
3. Answer the questions in the terminal (`y`/`n`). The program will display a *Progress Bar* and automatically download **Microsoft OpenJDK 25.0.3** and **Android Command-line Tools** into the `tools/` folder (~500 MB - 900 MB).
4. Answer `y` when asked whether to register `paksa` to the system PATH so it can be called from any folder.
5. Wait until you see **`[OK] SETUP COMPLETE`**.

> **Recommended VS Code Extensions:**
> * 🧩 [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
> * ☕ [Prettier Java Plugin](https://marketplace.visualstudio.com/items?itemName=RudraPatel.prettier-plugin-java-vscode)
> * 📝 [XML Tools](https://marketplace.visualstudio.com/items?itemName=DotJoshJohnson.xml)

***

## 🚀 Usage

### 1. Create a New Project (`paksa.exe` / `paksa`)

Open a Terminal (CMD/PowerShell/Bash) in the folder where you want to store your project, then type `paksa` (if registered to PATH) or double-click `paksa.exe`:

```text
========================================================
  PAKSA - Paksa Buat Aplikasi Android
  github.com/nabil-aba/paksa
========================================================
1. New Project Folder Name  : MyApp
2. Application Name (on phone): My Application
3. Package (com.myname.app) : com.nabil.myapp

========================================================
  AVAILABLE TEMPLATES:
  [1] android-library.zip
  [2] cpp-ndk-basic.zip
  [3] java-basic.zip
  [4] kotlin-basic.zip
  [5] kotlin-compose-basic.zip
========================================================
Choose Number [1-5]: 1

========================================================
  PAKSA AI - Smart Code Assistant
========================================================
💡 Have a feature idea? (e.g. 'Create a minimalist login page')
   Leave blank to use the default template:
   >> create a cool purple login page
🤖 [PAKSA-AI] Using Google AI Studio Spec (Gemini)...
[PAKSA-AI] ⚡ Success! Applying code to project...
📦 [PAKSA-AI] Injecting libraries (dependencies) into build.gradle...
✅ [PAKSA-AI] Your app code is ready to run!

```

### 2. Setup VS Code for an Existing Project (`paksa init`)

Have an existing Android project and want to add **VS Code build task shortcuts**? Just run this command in your project's root folder:

```bash
cd MyExistingProject
paksa init
```

PAKSA will automatically:
1. Detect the project type (**APK Application** or **.aar Library**) from `app/build.gradle`
2. Create the `.vscode/` folder along with an appropriate `tasks.json`
3. Ask for confirmation if `tasks.json` already exists

```text
========================================================
  PAKSA INIT - Setup .vscode for This Project
========================================================

✅ .vscode/tasks.json successfully created!
   Detected project type: Application (APK/AAB)

   Open this folder in VS Code then press Ctrl+Shift+B
   to see all available build tasks.
```

### 3. Open in VS Code

```bash
cd MyApp
code .
```

Plug in your phone via USB (make sure USB Debugging is enabled), open the Terminal tab in VS Code, press **`Ctrl+Shift+B`**, and choose a Task!

***

## 🎮 Build Tasks (`Ctrl+Shift+B`)

After creating a project (or after running `paksa init`), these features are automatically integrated as Tasks in VS Code.

### For Application Projects (APK/AAB)

| Task | Function |
|------|----------|
| 🚀 **1. Run Debug (Build & Install)** | Build debug APK → save to `output/` → install to phone via ADB → auto launch |
| 💎 **2. Build Release (APK + AAB Ready to Publish)** | Build signed release APK + AAB → save to `output/` → install test to phone |
| 🔑 **3. Generate Keystore (Signing Key)** | Create `.jks` signature file via `keytool` → automatically save config to `local.properties` |
| 🐛 **4. View Error Log (Crash/Force Close)** | Pull crash log from ADB → filter by package & PID → display the erroring code line |
| 👀 **5. Watch Mode (Auto-Rebuild on Save)** | Monitor `app/src/` folder → auto-rebuild & reinstall live every time a file is saved (`Ctrl+S`) |
| 📡 **6. Connect ADB Wi-Fi (Wireless)** | Connect laptop and phone wirelessly via IP/mDNS (Supports Android 10 & 11+) |
| 📦 **7. Build & Push to Phone Screen (Via Browser, No Manual Install)** | Build APK and transfer instantly via Local Web Server + ADB Tunneling. Completely bypasses FUSE/MIUI security systems that often cause ADB to get *stuck*! |
| 🧹 **8. Clean Project (Delete Build Cache & Output)** | Run gradle clean → delete output/ and .gradle/ folders → project cleared of build cache |

### For Library Projects (.aar)

| Task | Function |
|------|----------|
| 📦 **1. Build Debug Library (.aar)** | Build debug version of library |
| 💎 **2. Build Release Library (.aar Ready to Publish)** | Build release version of library ready for distribution |
| 👀 **3. Watch Mode (Auto-Rebuild on Save)** | Auto-rebuild library every time a file is saved |
| 🧹 **4. Clean Project (Delete Build Cache & Output)** | Run gradle clean → delete output/ and .gradle/ folders |

> ⚠️ **Note:** Run Task **3 (Generate Keystore)** before running Task **2 (Build Release)** for the first time.

***

## 📁 Folder Structure

```text
paksa/                         ← PAKSA engine folder
├── paksa.exe                  ← Project Generator (CLI)
├── setup.exe                  ← Smart Toolchain Installer
├── paksa-tools.exe            ← Build & Dev Tools / Android Wrapper
├── paksa_config.json          ← External API & AI Model Configuration
├── tools/                     ← Android Environment & Tools (output of setup)
│   ├── jdk/                   ← Microsoft OpenJDK 25.0.3
│   ├── android-sdk/           ← Android SDK (platform-tools, build-tools, etc.)
│   ├── cache/                 ← Downloaded zip file cache
│   ├── .gradle_cache/         ← Internet library storage
│   ├── env.bat / env.sh       ← Environment variables script
│   └── VERSION.txt            ← Installed tools version info
└── templates/                 ← Android project templates (*.zip)

MyApp/                         ← Your project folder (output of generate)
├── app/                       ← Android application source code
├── output/                    ← APK & AAB build results automatically saved here
├── .vscode/
│   └── tasks.json             ← Build task shortcuts for Ctrl+Shift+B
├── .gitignore
├── gradlew / gradlew.bat
└── local.properties           ← Keystore configuration (automatically ignored by Git)
```

***

## ⚖️ License

Copyright © 2026 Nabil. All rights reserved.

This repository distributes PAKSA binaries for free use. However, **the PAKSA engine source code is proprietary and may not be redistributed, modified, or used for commercial purposes without written permission from the owner.**
