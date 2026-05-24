# PAKSA 🔨

> **Paksa Buat Aplikasi Android** — Android project generator ultra-ringan untuk Windows (Support Mac & Linux) + VS Code.

Buat project Android baru dalam hitungan detik langsung dari terminal. Pilih template, isi nama app dan package, dan project siap dibuka di VS Code — **tanpa Android Studio, dan tanpa setup manual yang rumit**.

Dirancang khusus untuk developer yang coding di **laptop low-end (Potato PC)** tapi tetap mau pakai Android API terbaru tanpa bikin laptop kepanasan atau SSD penuh.

Built with ❤️ from Indonesia.

***

## ✨ Kenapa PAKSA?

* **Tanpa Android Studio:** Jalan murni pakai Gradle dan Command-Line, resource RAM komputer aman!
* **100% Portable Toolchain:** Tidak mengotori Environment Variables (`PATH`, `JAVA_HOME`, `ANDROID_HOME`) OS kamu sama sekali. Semua tools terisolasi rapi di dalam folder `tools/`.
* **Zero Configuration:** Tidak perlu pusing atur lisensi SDK Google atau instalasi JDK secara manual. Cukup 1 kali jalankan `setup.exe`.
* **Cross-Platform Watch Mode:** Fitur *Auto-Rebuild* murni menggunakan Native OS API! Setiap kamu men-*save* file (`Ctrl+S`), Paksa otomatis mem-build dan me-restart aplikasi di HP-mu. Tanpa membebani RAM, tanpa butuh Node.js/Nodemon!
* **Ultra-Fast Native Engine:** Tidak lagi mengandalkan PowerShell atau CMD yang lambat. Download, ekstrak ZIP, hingga replace *package name* kini dieksekusi secara instan di level memori (RAM).
* **Smart Auto-Uninstall:** Sering kena error `INSTALL_FAILED_UPDATE_INCOMPATIBLE` saat bolak-balik dari versi Release ke Debug? Paksa otomatis mendeteksi bentrok *signature* dan melakukan *clean install* secara diam-diam.
* **Smart Crash Parser:** Aplikasi tiba-tiba *Force Close*? Menu khusus untuk menarik log *crash* dari ADB, filter berdasarkan package name & PID, dan langsung menunjuk ke baris kode Java yang error — tanpa *log sampah* bawaan Android.
* **Auto-Output & AAB Support:** Hasil build (APK & AAB) otomatis tersimpan rapi di folder `output/`. Siap upload ke Play Store tanpa perlu nyari-nyari file di dalam folder Gradle yang dalam!
* **Modern Standard:** Pre-configured dengan **Android API 37**, **Build Tools 37.0.0**, **Gradle 9.5.1**, dan **AGP 9.2.1**.

***

## 🛠️ One-Time Setup (Cukup 1x Klik!)

Lupakan cara lama menginstal Java dan Android SDK secara manual. Paksa ditenagai oleh **100% Native RUST 🦀** yang mengotomatiskan segalanya dengan aman dan cepat.

1. Download atau *clone* repositori ini:
   ```bash
   git clone https://github.com/nabil-aba/paksa.git
   cd paksa
   ```
2. Jalankan file **`setup.exe`** (Windows) atau **`./setup`** (Mac/Linux).
3. Ketik `y` → Enter. Program menampilkan *Progress Bar* dan otomatis mengunduh **Microsoft OpenJDK 25.0.3** serta **Android Command-line Tools** ke folder `tools/` (~600 MB).
4. Jawab pertanyaan apakah ingin mendaftarkan `paksa` ke PATH sistem agar bisa dipanggil dari mana saja.
5. Tunggu sampai tulisan **`[OK] SETUP SELESAI`**.

> **Catatan Ekstensi VS Code yang Disarankan:**
> * 🧩 [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
> * ☕ [Prettier Java Plugin](https://marketplace.visualstudio.com/items?itemName=RudraPatel.prettier-plugin-java-vscode)
> * 📝 [XML Tools](https://marketplace.visualstudio.com/items?itemName=DotJoshJohnson.xml)

***

## 🚀 Cara Pakai

### 1. Buat Project Baru (`paksa.exe` / `paksa`)

Double-click `paksa.exe` atau jalankan dari terminal:

```text
========================================================
  PAKSA - Paksa Buat Aplikasi Android
  github.com/nabil-aba/paksa
========================================================
1. Nama Folder Project baru : MyApp
2. Nama Aplikasi (di HP)    : My Application
3. Package (com.saya.app)   : com.nabil.myapp

========================================================
  TEMPLATE TERSEDIA:
  [1] template-empty-compose.zip
  [2] template-java-xml.zip
========================================================
Pilih Nomor [1-2]: 1
```

Paksa akan otomatis:
- Extract template yang dipilih ke folder project baru
- Baca `applicationId` lama dari `app/build.gradle`
- Ganti package name lama → baru di: `build.gradle`, `AndroidManifest.xml`, `strings.xml`, dan semua file `.java`
- Pindahkan struktur folder `java/<old_pkg>` → `java/<new_pkg>`
- Generate `.gitignore` dan `.vscode/tasks.json` siap pakai

### 2. Buka di VS Code

```bash
cd MyApp
code .
```

Colok HP via USB, buka tab Terminal di VS Code, tekan **`Ctrl+Shift+B`**, dan pilih Task!

***

## 🎮 Build Tasks (`Ctrl+Shift+B`)

Setelah project dibuat, fitur-fitur ini sudah otomatis terintegrasi di VS Code:

| Task | Fungsi |
|------|--------|
| 🚀 **1. Run Debug (Build & Install)** | Build APK debug → simpan ke `output/` → install ke HP via ADB → launch otomatis |
| 💎 **2. Build Release (APK + AAB Siap Publish)** | Build APK + AAB release yang sudah di-sign → simpan ke `output/` → install test ke HP |
| 🔑 **3. Generate Keystore (Kunci Gembok)** | Buat file `.jks` signature via `keytool` → simpan konfigurasi ke `local.properties` |
| 🐛 **4. Lihat Error Log (Crash/Force Close)** | Tarik crash log dari ADB → filter per package & PID → tampilkan baris Java yang error |
| 👀 **5. Watch Mode (Auto-Rebuild saat Save)** | Monitor `app/src/` → auto-rebuild & reinstall setiap file di-save (`Ctrl+S`) |

> ⚠️ **Jalankan Task 3 (Keygen) terlebih dahulu** sebelum pertama kali menjalankan Task 2 (Release).

***

## 📁 Struktur Folder

```text
paksa/                         ← Folder tools PAKSA
├── paksa.exe                  ← Project Generator
├── setup.exe                  ← Portable Toolchain Installer
├── paksa-tools.exe            ← Build & Dev Tools
├── tools/                     ← JDK & Android SDK hasil setup.exe
│   ├── jdk/                   ← Microsoft OpenJDK 25.0.3
│   ├── android-sdk/           ← Android SDK (platform-tools, build-tools, dst)
│   ├── cache/                 ← Cache file download (agar setup ulang tidak re-download)
│   ├── env.bat / env.sh       ← Script environment variables
│   └── VERSION.txt            ← Info versi tools yang terpasang
└── templates/                 ← Template project Android (*.zip)

MyApp/                         ← Folder project kamu (di mana pun paksa.exe dijalankan)
├── app/
├── output/                    ← APK & AAB hasil build tersimpan di sini
├── .vscode/
│   └── tasks.json             ← Shortcut build tasks
├── .gitignore
├── gradlew / gradlew.bat
└── local.properties           ← Konfigurasi keystore (jangan di-commit ke Git!)
```

***

## 📜 Security & Engine

Tools executable Paksa dikompilasi **Native dengan Rust 🦀**:

- Bebas *Memory Leak*, tidak menggunakan *Shell Command* eksternal yang rentan bug
- **Compile-time String Obfuscation** (`obfstr`) — URL download dan hash lisensi SDK dienkripsi saat *compile*, tidak dapat dibaca dari binary
- **Anti-Debugging Traps** — program self-exit jika terdeteksi ada debugger aktif, mencegah *reverse engineering*

***

## ⚖️ License

MIT License — bebas clone, modifikasi, dan bangun *empire startup* dari laptop kentang! 🥔🚀