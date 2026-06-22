<p align="center">

![Nama](https://img.shields.io/badge/Nama-Prawiditya%20Sahrul%20Akbar-0A66C2?style=for-the-badge&logo=github&logoColor=white)
![Kelas](https://img.shields.io/badge/Kelas-I%2024%201A-1ABC9C?style=for-the-badge)
![Matkul](https://img.shields.io/badge/Matakuliah-Pemrograman%20Mobile2-FF6F00?style=for-the-badge&logo=android&logoColor=wh)

</p>

# 💰 CatatUang - Aplikasi Pencatat Keuangan Pribadi

> **Catat Uang, Atur Masa Depan.**

**CatatUang** adalah aplikasi Android modern untuk mengelola keuangan pribadi. Aplikasi ini memungkinkan pengguna mencatat pemasukan dan pengeluaran, memindai struk belanja dengan OCR dan AI, membuat target tabungan, serta berkonsultasi dengan asisten keuangan berbasis AI (Groq Llama). Dibangun dengan **Jetpack Compose** dan **Kotlin Coroutines**.

---

## 🚀 Tech Stack

![Platform](https://img.shields.io/badge/Platform-Android-brightgreen)
![Kotlin](https://img.shields.io/badge/Kotlin-1.9+-purple)
![Compose](https://img.shields.io/badge/Jetpack%20Compose-2024-blue)
![License](https://img.shields.io/badge/License-MIT-yellow)

- Kotlin (100%)
- Jetpack Compose (Material 3)
- MVVM Architecture
- Coroutines & Flow
- Google ML Kit (OCR)
- Groq API (Llama 3.3)
- Retrofit + Gson
- SharedPreferences
- CameraX
- PdfDocument

---

## ✨ Fitur Utama

### 📊 Manajemen Keuangan
- Tambah pemasukan & pengeluaran
- Kategori, deskripsi, dan tanggal otomatis
- Riwayat transaksi tersimpan rapi

### 🎯 Target Tabungan
- Buat tujuan finansial
- Pantau progres secara real-time

### 🧾 Pemindai Struk (OCR + AI)
- Scan struk dari kamera / galeri
- Ekstrak teks otomatis
- AI membaca item + harga

### 🤖 Asisten Keuangan AI
- Analisis pemasukan & pengeluaran
- Saran keuangan personal
- Chat dengan AI yang mengetahui data keuangan dan target tabungan Anda

### 📄 Ekspor PDF
- Generate laporan profesional
- Bisa dibagikan

### 📈 Statistik & Laporan
- Grafik pemasukan vs pengeluaran
- Status surplus / defisit

### 🎨 UI Modern
- Material 3
- Animasi halus
- Dark / Light mode

### 🧩 Draggable Chat Bubble
- Tombol asisten AI yang bisa dipindahkan
- Tombol mudah di kontrol
  
---

## 📸 Preview Aplikasi

<p align="center">
  <img src="https://github.com/user-attachments/assets/9a5d1ed2-7347-4e5c-a65e-3a142effb6a4" width="200"/>
  <img src="https://github.com/user-attachments/assets/9b1a066b-c40a-4b6e-a620-f67b1586114f" width="200"/>
  <img src="https://github.com/user-attachments/assets/029c16d7-d03e-4c84-b81e-650faf73e703" width="200"/>
</p>

<p align="center">
  🏠 <b>Dashboard</b> &nbsp;&nbsp;&nbsp;&nbsp;
  🧾 <b>Scan Struk</b> &nbsp;&nbsp;&nbsp;&nbsp;
  🤖 <b>AI Chat</b>
</p>

---

## ⚙️ Instalasi & Setup

### 1. Persyaratan

- Android Studio Hedgehog (2023.1.1+)
- JDK 11+
- minSdk 24
- targetSdk 34

---

### 2. Konfigurasi API Key (Groq)

Buat file:

```
secrets.properties
```

Isi dengan:

```
properties
GROQ_API_KEY=gsk_kunci_anda
```

---

### 3. Tambahkan ke build.gradle.kts

```
kotlin
android {
    buildFeatures {
        buildConfig = true
    }
}

val secretsProperties = java.util.Properties()
val secretsFile = rootProject.file("secrets.properties")

if (secretsFile.exists()) {
    secretsProperties.load(secretsFile.inputStream())
}

android.defaultConfig {
    buildConfigField(
        "String",
        "GROQ_API_KEY",
        "\"\${secretsProperties.getProperty("GROQ_API_KEY")}\""
    )
}
```

---

### 4. Permission

```
xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission 
    android:name="android.permission.WRITE_EXTERNAL_STORAGE"
    android:maxSdkVersion="28"/>
```

---

### 5. File Provider

```
xml
<provider
    android:name="androidx.core.content.FileProvider"
    android:authorities="\${applicationId}.fileprovider"
    android:exported="false"
    android:grantUriPermissions="true">
    <meta-data
        android:name="android.support.FILE_PROVIDER_PATHS"
        android:resource="@xml/file_paths" />
</provider>
```

```
xml
<paths>
    <cache-path name="cache" path="/" />
</paths>
```

---

### 6. Jalankan Aplikasi

- Hubungkan device / emulator
- Klik tombol Run ▶️

---

## 🧠 Cara Kerja AI

### 🧾 OCR + AI Struk
1. Ambil foto struk  
2. OCR membaca teks  
3. Kirim ke Groq API  
4. AI mengubah ke JSON (item + harga)  
5. Ditampilkan ke user  

---

### 🤖 AI Assistant
- Membaca data keuangan pengguna
- Membaca target tabungan Anda
- Memberikan insight & saran finansial

---

## 📁 Struktur Project
```
com.example.catatuang
├── MainActivity.kt
├── LuxuryCatatUangScreen.kt
├── ReceiptScannerHelper.kt
├── GroqClient.kt
├── AppPrefs.kt
├── PdfGenerator.kt
└── BuildConfig
```
---

## 🔮 Roadmap

- [ ] Grafik interaktif
- [ ] Dark mode otomatis
- [ ] Login biometrik
- [ ] Export CSV / Excel
- [ ] Transaksi berulang
- [ ] Cloud sync
- [ ] Multi-currency

---

## ❗Catatan Penting

- API Key Groq wajib diisi. Tanpa key, fitur AI dan ekstraksi item struk tidak akan bekerja (akan return kosong).
- Koneksi internet diperlukan untuk memanggil Groq API.
- OCR ML Kit berjalan secara offline (model bawaan), namun akurasi lebih baik dengan gambar yang jelas dan terang.
- Rotasi gambar otomatis berdasarkan metadata EXIF.
- FileProvider sudah dikonfigurasi, pastikan authority sesuai packageName.fileprovider.
- Aplikasi tidak menggunakan database SQLite, seluruh data disimpan di SharedPreferences (cocok untuk skala kecil).

## 📜 License
Hak Cipta © 2026 - Tugas Pemrograman Mobile
Dibuat untuk keperluan pendidikan. Boleh dimodifikasi dan didistribusikan.





<img width="359" height="804" alt="Screenshot 2026-05-02 072722" src="https://github.com/user-attachments/assets/89d2c36b-d9b6-41d4-a18b-b4bad8ce3af0" />
<img width="366" height="807" alt="Screenshot 2026-05-02 072744" src="https://github.com/user-attachments/assets/898862e2-06a5-4c14-b5bf-a371ff3f49d6" />
<img width="266" height="546" alt="Screenshot 2026-05-02 080238" src="https://github.com/user-attachments/assets/d3650ea9-8785-486b-9edd-09c804d33781" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d6856029-ccef-40f3-8b6d-8d3bc7e1e8e2" />
