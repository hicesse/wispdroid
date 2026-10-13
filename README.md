# ⚡ Wispdroid - Android Native Starter Template

<p align="left">
  <img src="https://img.shields.io/badge/Platform-Android-3DDC84?style=for-the-badge&logo=android&logoColor=white" alt="Platform Android" />
  <img src="https://img.shields.io/badge/Language-Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" alt="Language Java" />
  <img src="https://img.shields.io/badge/Gradle-8.5-02303A?style=for-the-badge&logo=gradle&logoColor=white" alt="Gradle 8.5" />
  <img src="https://img.shields.io/badge/AGP-8.2.2-34A853?style=for-the-badge&logo=android&logoColor=white" alt="AGP 8.2.2" />
  <img src="https://img.shields.io/badge/Min%20SDK-24-007EC6?style=for-the-badge" alt="Min SDK 24" />
  <img src="https://img.shields.io/badge/Target%20SDK-34-007EC6?style=for-the-badge" alt="Target SDK 34" />
  <img src="https://img.shields.io/badge/Template-Android%20Native-6f42c1?style=for-the-badge" alt="Template Android Native" />
</p>

Template proyek Android Native (Java + XML) berbasis Gradle murni. Dirancang agar ringan, bersih, dan kompatibel untuk pengembangan tanpa Android Studio (menggunakan Terminal, Antigravity IDE, VS Code, Neovim, dll.) maupun saat dibuka langsung di Android Studio.

---

## 🛠️ Prasyarat Sistem

Sebelum menjalankan proyek, pastikan perangkat telah memiliki:
1. **JDK 17** (Java Development Kit versi 17 direkomendasikan untuk Gradle 8.5 & AGP 8.2.2).
2. **Android SDK** (Command-line Tools atau Android Studio).
   - Pastikan variabel lingkungan `ANDROID_HOME` telah diarahkan ke folder SDK Anda, atau sediakan berkas `local.properties` (lihat bagian [Troubleshooting](#-troubleshooting)).

---

## 🚀 1. Persiapan Proyek Baru

Pilih salah satu metode berikut untuk mulai menggunakan template:

### Opsi A: Melalui Fitur GitHub Template (Disarankan)
Jika repositori ini sudah dijadikan **Template Repository** di GitHub:
1. Klik tombol hijau **"Use this template"** > **"Create a new repository"** di halaman GitHub.
2. Clone repositori baru milikmu. Riwayat commit lama otomatis bersih tanpa perlu langkah manual.

### Opsi B: Clone Manual / Salin Folder
Jika mengunduh atau melakukan `git clone` secara langsung, lepaskan riwayat Git bawaan:

- **Windows (PowerShell):**
  ```powershell
  Remove-Item -Recurse -Force .git
  git init
  ```

- **Git Bash / Linux / macOS:**
  ```bash
  rm -rf .git
  git init
  ```

---

## ⚙️ 2. Penyesuaian Identitas Proyek

Buka folder proyek di editor Anda, lalu sesuaikan bagian-bagian berikut:

### a. `settings.gradle`
Ubah nama root project:
```groovy
rootProject.name = "nama_projek_kamu"
```

### b. `app/build.gradle`
Ubah `namespace` dan `applicationId`:
```groovy
android {
    namespace 'com.example.nama_projek_kamu'

    defaultConfig {
        applicationId "com.example.nama_projek_kamu"
        // ...
    }
}
```

### c. Struktur Folder Kode Sumber Java (`app/src/main/java/`)
1. Ganti struktur direktori paket:
   ```text
   com/example/helloworld/  ->  com/example/nama_projek_kamu/
   ```
2. Buka berkas `MainActivity.java`, sesuaikan deklarasi package pada baris paling atas:
   ```java
   package com.example.nama_projek_kamu;
   ```

### d. Nama Tampilan Aplikasi di HP (`app/src/main/res/values/strings.xml`)
Ubah nilai string `app_name`:
```xml
<resources>
    <string name="app_name">Nama Aplikasi Kamu</string>
</resources>
```

---

## 📦 3. Kompilasi & Menjalankan Aplikasi

Template ini menyertakan Gradle Wrapper untuk Windows (`gradlew.bat`) dan Linux/macOS (`gradlew`).

### a. Hanya Kompilasi / Membuat File APK (Tanpa HP Terhubung)
Gunakan perintah ini untuk memeriksa build atau menghasilkan berkas APK debug:
- **Windows (PowerShell / CMD):**
  ```powershell
  .\gradlew.bat assembleDebug
  ```
- **Git Bash / Linux / macOS:**
  ```bash
  ./gradlew assembleDebug
  ```
> Berkas APK debug akan tersimpan di: `app/build/outputs/apk/debug/app-debug.apk`

---

### b. Kompilasi dan Pasang Langsung ke Perangkat (ADB)
Pastikan opsi **USB Debugging** di HP Android sudah aktif dan kabel data tersambung.

1. **Periksa Sambungan Perangkat:**
   ```bash
   adb devices
   ```
   *(Pastikan status perangkat terdaftar sebagai `device`, bukan `unauthorized` atau `offline`)*

2. **Kompilasi & Pasang:**
   - **Windows:**
     ```powershell
     .\gradlew.bat installDebug
     ```
   - **Git Bash / Linux / macOS:**
     ```bash
     ./gradlew installDebug
     ```

---

### c. Membersihkan Cache Build
Jika ingin membersihkan build lama:
- **Windows:** `.\gradlew.bat clean`
- **Linux / macOS:** `./gradlew clean`

---

## 🔍 Troubleshooting

### 1. `SDK location not found`
Jika Gradle tidak menemukan lokasi Android SDK, buat berkas bernama `local.properties` di root folder proyek:
- **Windows:**
  ```properties
  sdk.dir=C:\\Users\\NamaUser\\AppData\\Local\\Android\\Sdk
  ```
- **macOS:**
  ```properties
  sdk.dir=/Users/NamaUser/Library/Android/sdk
  ```
- **Linux:**
  ```properties
  sdk.dir=/home/NamaUser/Android/Sdk
  ```
*(Berkas `local.properties` ini sudah otomatis diabaikan oleh `.gitignore` sehingga tidak akan terunggah ke repositori).*

### 2. Linux / macOS: `Permission denied: ./gradlew`
Jalankan perintah ini di terminal untuk memberikan izin eksekusi pada wrapper script:
```bash
chmod +x gradlew
```