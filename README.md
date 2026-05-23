# PAKSA 🔨

> **Paksa Buat Aplikasi Android** — Android project generator ultra-ringan untuk Windows + VS Code.

Buat project Android baru dalam hitungan detik langsung dari terminal. Pilih template, isi nama app dan package, dan project siap dibuka di VS Code — **tanpa Android Studio, dan tanpa setup manual yang rumit**.

Dirancang khusus untuk developer yang coding di **laptop low-end (Potato PC)** tapi tetap mau pakai Android API terbaru tanpa bikin laptop kepanasan atau SSD penuh.

Built with ❤️ from Indonesia.

***

## ✨ Kenapa PAKSA?

* **Tanpa Android Studio:** Jalan murni pakai Gradle dan Command-Line, resource RAM komputer aman!
* **100% Portable Toolchain:** Tidak mengotori Environment Variables (`Path`, `JAVA_HOME`, `ANDROID_HOME`) Windows kamu sama sekali. Semua tools terisolasi rapi di dalam folder `tools/`.
* **Zero Configuration:** Tidak perlu pusing atur lisensi SDK Google atau instalasi JDK secara manual. Cukup 1 kali klik `setup.exe`.
* **Win32 Watch Mode [NEW]:** Fitur *Auto-Rebuild* murni menggunakan Native Windows API! Setiap kali kamu men-*save* file (`Ctrl+S`), Paksa otomatis mem-build dan merestart aplikasi di HP-mu. Tanpa membebani RAM, dan tanpa butuh Node.js/Nodemon!
* **Smart Auto-Uninstall [NEW]:** Sering kena error `INSTALL_FAILED_UPDATE_INCOMPATIBLE` saat bolak-balik dari versi Release ke Debug? Paksa otomatis mendeteksi bentrok *signature* dan melakukan *clean install* secara diam-diam.
* **Smart Crash Parser:** Aplikasi tiba-tiba *Force Close*? Tersedia menu khusus untuk menarik log *crash* dan langsung menunjuk ke baris kode Java yang error tanpa *log sampah* bawaan Android.
* **Auto-Output & AAB Support:** Hasil build (APK & AAB) otomatis tersimpan rapi di folder `output/`. Siap upload ke Play Store tanpa perlu nyari-nyari file di dalam folder Gradle yang dalam!
* **Modern Standard:** Pre-configured dengan **Android API 37**, **Gradle 9.5.1**, dan **AGP 9.2.1**.

***

## 🛠️ One-Time Setup (Cukup 1x Klik!)

Lupakan cara lama menginstal Java dan Android SDK secara manual. Paksa dibangun dengan **100% Native C++** yang akan mengotomatiskan segalanya untukmu.

1. Download atau *clone* repositori ini:
   ```bash
   git clone https://github.com/nabil-aba/paksa.git
   cd paksa
   ```
2. Klik dua kali (jalankan) file **`setup.exe`**.
3. Ketik `y` dan enter. Program akan otomatis mengunduh Microsoft OpenJDK 25 dan Android Command-line Tools ke dalam folder `tools/` (~600MB).
4. Tunggu sampai tulisan **[OK] SETUP SELESAI**.
5. *Selesai! Komputer kamu sekarang sudah siap membuat aplikasi Android.*

> **Catatan Ekstensi VS Code:** 
> Agar koding lebih nyaman dan auto-format, sangat disarankan menginstal:
> * 🧩 [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
> * ☕ [Prettier Java Plugin](https://marketplace.visualstudio.com/items?itemName=RudraPatel.prettier-plugin-java-vscode)
> * 📝 [XML Tools](https://marketplace.visualstudio.com/items?itemName=DotJoshJohnson.xml)

***

## 🚀 Cara Pakai

### 1. Buat Project (`paksa.exe`)
Double-click `paksa.exe` atau jalankan dari terminal untuk membuat project baru:
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

### 2. Buka di VS Code
```bash
cd MyApp
code .
```
Project langsung siap di-build. Colok HP-mu menggunakan kabel USB, buka tab Terminal di VS Code, tekan tombol sakti `Ctrl+Shift+B`, dan pilih Task!

***

## 🎮 Build Tasks (Ctrl+Shift+B)

Setelah project dibuat, fitur-fitur sakti ini sudah otomatis terintegrasi di VS Code kamu:

* 🚀 **1. Run Debug (Sekali Build & Install)**
  Build APK versi Debugging, simpan ke folder `output/`, install ke HP, dan luncurkan aplikasinya secara otomatis.

* 💎 **2. Build Release (APK + AAB Siap Publish)**
  Otomatis membuat file **.apk** dan **.aab** (Android App Bundle) yang sudah di-sign dan dioptimasi. Hasilnya langsung diekstrak ke folder `output/` dan siap untuk di-upload ke Google Play Store. *(Jalankan Task 3 dulu sebelum build release pertama kali!)*

* 🔑 **3. Generate Keystore (Kunci Gembok)**
  Membuat *signature* `.jks` resmi untuk aplikasi kamu dan otomatis menyimpannya ke `local.properties` (Aman dari Git/Maling).

* 🐛 **4. Lihat Error Log (Khusus Crash/Force Close)**
  Aplikasi kamu tiba-tiba *Force Close* saat dimainkan tanpa mencolok kabel? Colok HP-mu, jalankan task ini! *Smart Parser* Paksa akan melacak memori HP dan menampilkan baris kode Java mana yang menyebabkan aplikasimu meledak.

* 👀 **5. Watch Mode (Auto-Rebuild saat file di-Save)**
  *(Highly Recommended)* Aktifkan mode ini, dan nikmati pengalaman ngoding ala *React / WebDev*. Setiap kali kamu menyimpan kode (`Ctrl+S`), Paksa otomatis akan mendeteksinya, melakukan instalasi pembaruan, dan me-restart aplikasinya di HP-mu. Dilengkapi dengan *Timestamp Logging* agar histori *build* tetap rapi!

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
├── output/                ← File APK & AAB hasil build akan muncul di sini!
├── .vscode/
│   └── tasks.json         ← Shortcut tombol build
├── gradlew.bat
└── local.properties       ← Konfigurasi rahasia
```

***

## 📜 Security & Engine
Tools executable Paksa (`.exe`) dikompilasi secara **statis** menggunakan Native C++. Diperkuat dengan fitur **Compile-time String Obfuscation** dan **Anti-Debugging Traps** untuk mencegah modifikasi/reverse engineering ilegal.

## ⚖️ License
MIT License — bebas clone, modifikasi, dan bangun *empire startup* dari laptop kentang! 🥔🚀