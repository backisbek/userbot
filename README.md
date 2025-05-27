# Telegram Userbot Forwarder

Bot Telegram yang dirancang untuk mengelola akun pengguna (userbot) untuk keperluan penerusan pesan. Fitur meliputi penerusan otomatis (Auto Forward), manajemen whitelist target, dan operasi lainnya.
## ✨ Fitur Utama

-   **Setup Userbot Interaktif:** Proses pengaturan terpandu untuk API ID/Hash dan login sesi userbot melalui konsol.
-   **Manajemen Whitelist:** Tambah, lihat, dan hapus target chat (grup/channel/user) untuk penerusan pesan.
-   **Auto Forward Periodik:** Jadwalkan pesan dari link sumber untuk diteruskan secara berkala ke semua target di whitelist.
-   **Forward Manual:** Teruskan pesan secara instan ke target whitelist dengan opsi jeda antar target.
-   **Kontrol & Notifikasi Admin:** Aktifkan/nonaktifkan notifikasi progres dan kendalikan status Auto Forward.
-   **Ekspor Daftar Chat:** Dapatkan daftar grup dan channel userbot dalam format file `.txt`.
-   **Aman & Terbatas untuk Admin:** Seluruh fungsionalitas hanya dapat diakses oleh Admin yang terdaftar.
-   **Konfigurasi Terpusat:** Semua pengaturan disimpan dalam satu file `config.json` yang dibuat otomatis.

## 🚀 Instalasi & Konfigurasi Awal

1.  **Instal Dependensi:**
    Di direktori proyek, jalankan:
    ```bash
    npm install telegraf telegram input
    ```

2.  **Jalankan Bot untuk Pertama Kali:**
    ```bash
    node index.js
    ```
    Pada saat pertama kali dijalankan, jika file `config.json` tidak ditemukan, file tersebut akan otomatis dibuat dengan struktur dan nilai default.

3.  **Edit `config.json`:**
    Buka file `config.json` yang baru saja dibuat. **Anda wajib mengisi bagian berikut**:
    -   `botSettings.botToken`: Ganti dengan token bot Telegram Anda dari @BotFather.
    -   `botSettings.adminUserId`: Ganti dengan User ID Telegram numerik **Anda**. Ini krusial agar hanya Anda yang bisa mengontrol bot.

    Biarkan `botSettings.apiId`, `botSettings.apiHash`, dan `botSettings.userSession` apa adanya (`null` atau string kosong). Bot akan memandu Anda untuk mengisinya nanti.

4.  **Restart Bot:**
    Setelah menyimpan perubahan pada `config.json`, hentikan bot (Ctrl+C) dan jalankan kembali.

## 🤖 Setup Koneksi Userbot

Setelah bot admin berjalan dengan `botToken` dan `adminUserId` yang benar:

1.  **Mulai Chat dengan Bot Admin Anda:** Kirim perintah `/start` ke bot Telegram Anda.
2.  **Input Kredensial API:** Jika `apiId` dan `apiHash` belum terisi di `config.json`, bot akan meminta Anda untuk memasukkan:
    -   **API ID** Anda.
    -   **API Hash** Anda.
3.  **Login Userbot (via Konsol):** Setelah API ID & Hash tersimpan, **perhatikan konsol/terminal** tempat aplikasi Node.js Anda berjalan. Anda akan diminta untuk memasukkan:
    -   Nomor telepon akun userbot (format internasional, contoh: `+628123xxxx`).
    -   Kode verifikasi yang dikirim ke akun Telegram userbot.
    -   Kata sandi Two-Factor Authentication (2FA) jika diaktifkan pada akun userbot.
4.  **Koneksi Selesai:** Setelah userbot berhasil login, sesi koneksi (`userSession`) akan disimpan secara otomatis ke `config.json`. Bot kini siap digunakan dan akan menampilkan menu utama.

## ⚙️ Penggunaan Bot

Interaksi utama dengan bot dilakukan melalui perintah dan tombol inline:

-   `/start` atau `/menu`: Menampilkan menu utama. Memulai proses setup/koneksi userbot jika belum terhubung.
-   `/status`: Menampilkan status koneksi userbot dan ringkasan konfigurasi.
-   `/help`: Menampilkan panduan singkat ini.

**Menu Utama menyediakan akses ke:**

-   **⚙️ Pengaturan:** Konfigurasi jeda (delay) Auto Forward, sumber pesan & interval Auto Forward, serta status notifikasi admin.
-   **🎯 Whitelist:** Tambah, lihat, atau hapus target penerusan pesan.
-   **📂 Daftar Chat:** Ekspor daftar grup atau channel yang diikuti userbot.
-   **➤ Forward Sekarang:** Meneruskan pesan secara manual dari link yang diberikan.
-   **▶️ Start / ⏹️ Stop Auto Forward:** Mengontrol status fitur penerusan pesan periodik.

## ⚠️ Catatan Penting

-   **Akses Admin:** Operasional bot sepenuhnya dibatasi untuk `adminUserId` yang telah Anda atur di `config.json`.
-   **Keamanan `config.json`:** Jaga kerahasiaan file `config.json` Anda, terutama karena berisi `userSession` yang aktif.
-   **Batasan Telegram (Rate Limit):** Gunakan fitur jeda (delay) dengan bijak, terutama jika meneruskan ke banyak target, untuk menghindari pembatasan sementara dari Telegram.
-   **Kepatuhan:** Selalu patuhi Persyaratan Layanan Telegram.
-   **Sesi Userbot:** Jika userbot sering terputus, coba `/start` untuk re-koneksi. Jika gagal, Anda mungkin perlu menghapus nilai `userSession` dari `config.json` dan restart bot untuk proses login ulang penuh via konsol.

## 🐛 Troubleshooting Dasar

-   **Bot Admin Tidak Merespon:**
    -   Pastikan `botSettings.botToken` dan `botSettings.adminUserId` di `config.json` sudah benar.
    -   Periksa konsol/terminal untuk pesan error.
-   **Userbot Gagal Terhubung/Login:**
    -   Verifikasi API ID & API Hash yang dimasukkan saat setup via bot.
    -   Pastikan input nomor telepon, kode, dan 2FA (jika ada) di **konsol** sudah benar.
-   **Penerusan Pesan Gagal:**
    -   Userbot harus menjadi anggota grup/channel privat (baik sumber maupun target).
    -   Userbot harus memiliki izin untuk mengirim pesan di chat target.
    -   Pastikan whitelist tidak kosong dan berisi ID/username yang valid. Cek status via `/status`.

---
