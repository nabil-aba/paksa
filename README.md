# PAKSA 🔨

> **Paksa Buat Aplikasi Android** — Android project generator ultra-ringan untuk Windows (Support Mac & Linux) + VS Code.

Buat project Android baru dalam hitungan detik langsung dari terminal. Pilih template, isi nama app dan package, dan project siap dibuka di VS Code — **tanpa Android Studio, dan tanpa setup manual yang rumit**.

Dirancang khusus untuk developer yang coding di **laptop low-end (Potato PC)** tapi tetap mau pakai Android API terbaru tanpa bikin laptop kepanasan atau SSD/Drive C penuh.

Built with ❤️ from Indonesia.

***

## ✨ Kenapa PAKSA?

* **Tanpa Android Studio:** Jalan murni pakai Gradle dan Command-Line, resource RAM komputer sangat aman!
* **100% Portable Toolchain:** Tidak mengotori Environment Variables (`PATH`, `JAVA_HOME`, `ANDROID_HOME`) OS kamu sama sekali. Semua tools terisolasi rapi di dalam folder `tools/`.
* **Drive C Savior (Anti-Bengkak):** Paksa secara otomatis mengalihkan *Global Cache* Gradle (yang ukurannya bisa bergiga-giga) ke dalam folder `tools/.gradle_cache`. Drive C (sistem Windows) kamu dijamin aman dari tumpukan file sampah!
* **Smart Zero Configuration:** Tidak perlu pusing atur lisensi SDK Google atau instalasi JDK. Cukup 1 kali jalankan `setup.exe`. Setup ini juga cukup pintar untuk mensinkronkan ulang konfigurasi tanpa perlu men-download ulang jika file sudah ada.
* **Cross-Platform Watch Mode:** Fitur *Auto-Rebuild* murni menggunakan Native OS API! Setiap kamu men-*save* file (`Ctrl+S`), Paksa otomatis mem-build dan me-restart aplikasi di HP-mu. Tanpa membebani RAM, tanpa butuh Node.js/Nodemon!
* **Ultra-Fast Native Engine:** Tidak lagi mengandalkan PowerShell atau CMD yang lambat. Download, ekstrak ZIP, hingga replace *package name* dieksekusi secara instan di level memori (RAM).
* **Smart Auto-Uninstall:** Sering kena error `INSTALL_FAILED_UPDATE_INCOMPATIBLE` saat bolak-balik dari versi Release ke Debug? Paksa otomatis mendeteksi bentrok *signature* dan melakukan *clean install* secara diam-diam.
* **Smart Crash Parser:** Aplikasi tiba-tiba *Force Close*? Menu khusus untuk menarik log *crash* dari ADB, mem-filter berdasarkan package name & PID, dan langsung menunjuk ke baris kode Java/Kotlin yang error — tanpa *log sampah* bawaan Android.
* **Auto-Output & AAB Support:** Hasil build (APK & AAB) otomatis tersimpan rapi di folder `output/`. Siap upload ke Play Store tanpa perlu nyari-nyari file di dalam folder Gradle yang dalam!
* **Modern Standard:** Pre-configured dengan **Android API 37**, **Build Tools 37.0.0**, Dukungan **Jetpack Compose**, dan **Gradle Terbaru**.

***

## 🛠️ One-Time Setup (Cukup 1x Klik!)

Lupakan cara lama menginstal Java dan Android SDK secara manual. Paksa ditenagai oleh **100% Native RUST 🦀** yang mengotomatiskan segalanya dengan aman dan cepat.

1. Download atau *clone* repositori ini:
   ```bash
   git clone https://github.com/nabil-aba/paksa.git
   cd paksa
   ```
2. Jalankan file **`setup.exe`** (Windows) atau **`./setup`** (Mac/Linux).
3. Jawab pertanyaan di terminal (`y`/`n`). Program akan menampilkan *Progress Bar* dan otomatis mengunduh **Microsoft OpenJDK 25.0.3** serta **Android Command-line Tools** ke folder `tools/` (~500 MB - 900 MB).
4. Jawab `y` saat ditanya apakah ingin mendaftarkan `paksa` ke PATH sistem agar bisa dipanggil dari folder mana saja.
5. Tunggu sampai tulisan **`[OK] SETUP SELESAI`**.

> **Catatan Ekstensi VS Code yang Disarankan:**
> * 🧩 [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
> * ☕ [Prettier Java Plugin](https://marketplace.visualstudio.com/items?itemName=RudraPatel.prettier-plugin-java-vscode)
> * 📝 [XML Tools](https://marketplace.visualstudio.com/items?itemName=DotJoshJohnson.xml)

***

## 🚀 Cara Pakai

### 1. Buat Project Baru (`paksa.exe` / `paksa`)

Buka Terminal (CMD/PowerShell/Bash) di folder tempat kamu ingin menyimpan project, lalu ketik `paksa` (jika sudah didaftarkan ke sistem) atau double-click `paksa.exe`:

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
  [1] java-basic.zip
  [2] kotlin-basic.zip
  [3] kotlin-compose.zip
========================================================
Pilih Nomor [1-3]: 1
```

Paksa akan otomatis:
- Mengekstrak template yang dipilih ke folder project baru.
- Membaca `applicationId` lama dari `app/build.gradle`.
- Menganalisis dan mengganti *package name* lama → baru di: `build.gradle`, `AndroidManifest.xml`, `strings.xml`, dan seluruh file `.java` / `.kt`.
- Memindahkan struktur folder `java/<old_pkg>` → `java/<new_pkg>` secara aman.
- Men-generate `.gitignore` dan `.vscode/tasks.json` yang menyembunyikan file raksasa (seperti folder `build/`) dari pandangan Explorer VS Code.

### 2. Buka di VS Code

```bash
cd MyApp
code .
```

Colok HP via USB (pastikan USB Debugging aktif), buka tab Terminal di VS Code, tekan **`Ctrl+Shift+B`**, dan pilih Task!

***

## 🎮 Build Tasks (`Ctrl+Shift+B`)

Setelah project dibuat, fitur-fitur ini sudah otomatis terintegrasi sebagai Task di VS Code:

| Task | Fungsi |
|------|--------|
| 🚀 **1. Run Debug (Build & Install)** | Build APK debug → simpan ke `output/` → install ke HP via ADB → launch otomatis |
| 💎 **2. Build Release (APK + AAB Siap Publish)** | Build APK + AAB release yang sudah di-sign → simpan ke `output/` → install test ke HP |
| 🔑 **3. Generate Keystore (Kunci Gembok)** | Buat file `.jks` signature via `keytool` → otomatis simpan konfigurasi ke `local.properties` |
| 🐛 **4. Lihat Error Log (Crash/Force Close)** | Tarik crash log dari ADB → filter per package & PID → tampilkan baris kode yang error |
| 👀 **5. Watch Mode (Auto-Rebuild saat Save)** | Monitor folder `app/src/` → auto-rebuild & reinstall secara langsung setiap file di-save (`Ctrl+S`) |

> ⚠️ **Catatan:** Jalankan Task **3 (Generate Keystore)** terlebih dahulu sebelum pertama kali menjalankan Task **2 (Build Release)**.

***

## 📁 Struktur Folder

```text
paksa/                         ← Folder engine PAKSA
├── paksa.exe                  ← Project Generator (CLI)
├── setup.exe                  ← Smart Toolchain Installer
├── paksa-tools.exe            ← Build & Dev Tools / Android Wrapper
├── tools/                     ← Environment & Tools Android (Hasil setup)
│   ├── jdk/                   ← Microsoft OpenJDK 25.0.3
│   ├── android-sdk/           ← Android SDK (platform-tools, build-tools, dst)
│   ├── cache/                 ← Cache file zip download
│   ├── .gradle_cache/         ← Penyimpanan library internet
│   ├── env.bat / env.sh       ← Script environment variables
│   └── VERSION.txt            ← Info versi tools yang terpasang
└── templates/                 ← Template project Android (*.zip)

MyApp/                         ← Folder project kamu (Hasil generate)
├── app/                       ← Source code aplikasi Android
├── output/                    ← APK & AAB hasil build tersimpan otomatis di sini
├── .vscode/
│   └── tasks.json             ← Shortcut build tasks untuk Ctrl+Shift+B
├── .gitignore
├── gradlew / gradlew.bat
└── local.properties           ← Konfigurasi keystore (otomatis terabaikan oleh Git)
```

***

## ⚖️ License

MIT License — bebas clone, modifikasi, dan bangun *empire startup* dari laptop kentang! 🥔🚀