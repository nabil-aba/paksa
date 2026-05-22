# PAKSA 🔨

> **Paksa Buat Aplikasi Android** — Android project generator ultra-ringan untuk Windows + VS Code.

Buat project Android baru dalam hitungan detik langsung dari terminal. Pilih template, isi nama app dan package, dan project siap dibuka di VS Code — tanpa Android Studio, dan **tanpa setup manual yang rumit**.

Dirancang khusus untuk developer yang coding di **laptop low-end (Potato PC)** tapi tetap mau pakai Android API terbaru tanpa bikin laptop kepanasan atau SSD penuh.

Built with ❤️ from Indonesia.

***

## ✨ Kenapa PAKSA?

* **Tanpa Android Studio:** Jalan murni pakai Gradle dan Command-Line.
* **100% Portable Toolchain:** Tidak mengotori Environment Variables (`Path`, `JAVA_HOME`, `ANDROID_HOME`) Windows kamu sama sekali! Semua tools terisolasi di dalam folder `tools/`.
* **Zero Configuration:** Tidak perlu pusing atur lisensi SDK atau instalasi JDK secara manual. Cukup 1 kali klik.
* **Anti Overheat:** Tidak ada Red Hat Java Language Server yang berat. Pakai formatter ringan saja.
* **Modern Standard:** Pre-configured dengan **Android API 37**, **Gradle 9.5.1**, dan **AGP 9.2.1**.
* **Automated Build:** Setelah project dibuat, semua build task langsung terintegrasi di VS Code (`Ctrl+Shift+B`).

***

## 🛠️ One-Time Setup (Cukup 1x Klik!)

Lupakan cara lama menginstal Java dan Android SDK secara manual. Paksa sudah dilengkapi dengan **Automated Installer**.

1. Download atau clone repositori ini:
   ```bash
   git clone https://github.com/nabil-aba/paksa.git
   cd paksa
   ```
2. Klik dua kali (jalankan) file **`setup.exe`**.
3. Ketik `y` dan enter. Program akan otomatis mengunduh Microsoft OpenJDK 25 dan Android Command-line Tools ke dalam folder `tools/` (~600MB).
4. Tunggu sampai tulisan **[OK] SETUP SELESAI**.
5. *Selesai! Komputer kamu sekarang sudah siap membuat aplikasi Android.*

> **Catatan:** Install ekstensi ringan ini di VS Code kamu agar koding lebih rapi:
> * 🧩 [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
> * ☕ [Prettier Java Plugin](https://marketplace.visualstudio.com/items?itemName=RudraPatel.prettier-plugin-java-vscode)
> * 📝 [XML Tools](https://marketplace.visualstudio.com/items?itemName=DotJoshJohnson.xml)

***

## 🚀 Cara Pakai

### 1. Jalankan `paksa.exe`
Double-click `paksa.exe` atau jalankan dari terminal untuk membuat project baru:
```cmd
paksa.exe
```

### 2. Isi Data Project
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

### 3. Buka di VS Code
```bash
cd MyApp
code .
```
Project langsung siap di-build. Colok HP, tekan `Ctrl+Shift+B`, dan pilih task.

***

## 🎮 Build Tasks (Ctrl+Shift+B)

Setelah project dibuat, semua task ajaib ini sudah langsung tersedia di VS Code:

* 🚀 **1. Run Android (Debug & Test)**
  Build APK debug, install ke HP, dan launch otomatis. Untuk coding sehari-hari.

* 💎 **2. Build APK (Rilis Resmi)**
  Build APK release yang sudah di-sign, siap untuk di-upload ke Play Store.
  ⚠️ **Jalankan Task 3 dulu** sebelum build release pertama kali!

* 🔑 **3. Bikin Kunci Gembok (Keystore)**
  Membuat signature `.jks` resmi untuk aplikasi kamu dan otomatis menyimpannya ke `local.properties` (Aman dari Git).

***

## 📁 Struktur Setelah Setup & Generate

```text
(Folder Alat PAKSA)
paksa/
├── paksa.exe              ← Project Generator
├── setup.exe              ← Portable Toolchain Installer
├── paksa-tools.exe        ← Build Tools Manager
├── tools/                 ← (Hasil dari setup.exe) JDK & Android SDK
└── templates/             ← Pilihan template project Android (*.zip)

=======================================================

(Folder Project Kamu - Di mana pun kamu jalankan paksa.exe)
MyApp/
├── app/
├── .vscode/
│   └── tasks.json         ← Shortcut tombol build
├── gradlew.bat
└── local.properties       ← Konfigurasi rahasia
```

***

## 📜 License

MIT License — bebas clone, modifikasi, dan bangun *empire startup* dari laptop kentang! 🥔🚀