# KYY SCRIPT PRO — Update Server

Paket ini hanya berisi halaman informasi update. Jangan masukkan source code aplikasi atau private key ke repository publik ini.

## Struktur
- `index.html`: halaman sederhana server update.
- `version.json`: metadata versi yang dibaca aplikasi.
- `.github/workflows/pages.yml`: deploy otomatis ke GitHub Pages.

## Cara menyiapkan (gratis, tanpa domain)
1. Buat repository GitHub baru bernama `kyy-script-updates`.
2. Atur repository ini sebagai **Public**. Repository ini hanya untuk metadata update dan bukan source code.
3. Unggah seluruh isi folder paket ini ke branch `main` (termasuk folder `.github`).
4. Buka Settings → Pages. Pada Build and deployment, pilih **GitHub Actions**.
5. Tunggu workflow `Deploy KYY Update Server` selesai.
6. Endpoint metadata akan berbentuk:
   `https://USERNAME.github.io/kyy-script-updates/version.json`
   Ganti USERNAME dengan username GitHub pemilik repository.

## Rilis APK
1. Buat GitHub Release pada repository update terpisah.
2. Lampirkan APK final sebagai asset Release.
3. Salin URL unduhan APK ke field `apkUrl` pada `version.json`.
4. Hitung SHA-256 APK final lalu isi field `sha256`.
5. Naikkan `version` dan `versionCode` untuk setiap rilis baru.
6. Commit perubahan `version.json`; GitHub Pages akan deploy otomatis.

## Keamanan dan kompatibilitas
- Repository update publik berarti metadata dan APK yang dipublikasikan dapat dilihat/diunduh siapa pun. Source code tetap di repository Private.
- Jangan pernah mengunggah private key lisensi, keystore, password, token, atau source code.
- APK pembaruan harus ditandatangani dengan sertifikat yang sama seperti APK terpasang agar Android dapat memperbaruinya tanpa uninstall.
- Aplikasi perlu memverifikasi SHA-256 dan tanda tangan APK sebelum menawarkan instalasi.
- `version.json` saat ini template. `apkUrl` dan `sha256` harus diisi setelah APK Release final tersedia.
- Server ini belum terhubung ke aplikasi. Integrasi endpoint, parser JSON, unduhan, checksum, dan installer masih perlu ditambahkan ke source aplikasi dan diuji.
