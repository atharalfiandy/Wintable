# WinTable

[![Rilis](https://img.shields.io/badge/release-v1.0.8-blue)](https://github.com/atharalfiandy/Wintable/releases/tag/1.0.8)
![Platform](https://img.shields.io/badge/platform-Windows-0078D4)
![PowerShell](https://img.shields.io/badge/PowerShell-WinForms-5391FE)

**WinTable** adalah aplikasi Windows untuk membuat media USB bootable dari file ISO Windows. Aplikasi ini menyediakan antarmuka grafis untuk mengenali ISO, memilih USB dan pengaturan media, lalu menyiapkan USB agar dapat digunakan untuk memulai Windows Setup.

WinTable berfokus pada pembuatan media instalasi. Aplikasi ini bukan sistem operasi, bukan file ISO Windows, dan bukan pengganti lisensi Windows.

## Daftar Isi

- [Tentang WinTable](#tentang-wintable)
- [Tujuan](#tujuan)
- [Fitur Utama](#fitur-utama)
- [Dukungan Windows dan Media](#dukungan-windows-dan-media)
- [Pengaturan Media](#pengaturan-media)
- [Perlindungan dan Peringatan](#perlindungan-dan-peringatan)
- [Persyaratan Sistem](#persyaratan-sistem)
- [Unduhan WinTable v1.0.8](#unduhan-wintable-v108)
- [Batasan yang Perlu Diketahui](#batasan-yang-perlu-diketahui)
- [Privasi dan Pemrosesan](#privasi-dan-pemrosesan)
- [Lisensi dan Hak Penggunaan](#lisensi-dan-hak-penggunaan)
- [Informasi Proyek](#informasi-proyek)

## Tentang WinTable

WinTable membantu menyiapkan USB instalasi Windows dengan memanfaatkan ISO Windows yang telah dimiliki pengguna. ISO diperiksa sebelum proses penulisan agar jenis Windows di dalam file sesuai dengan versi yang dikenali dari ISO tersebut.

Antarmuka WinTable menampilkan perangkat USB yang memenuhi syarat, informasi perangkat, pilihan skema partisi dan sistem berkas, status proses, serta konfirmasi penghapusan data. Proses pembuatan media dilakukan dengan utilitas bawaan Windows.

WinTable dibuat untuk pengguna yang membutuhkan media instalasi Windows pada komputer yang mendukung boot dari USB. Kesesuaian media yang dibuat tetap bergantung pada ISO, konfigurasi firmware, dan perangkat keras komputer tujuan.

## Tujuan

- Menyatukan pembuatan USB bootable Windows dalam satu aplikasi desktop.
- Membantu memeriksa ISO Windows sebelum media USB diubah.
- Menyediakan pilihan konfigurasi media yang relevan untuk firmware dan sistem berkas.
- Menampilkan perangkat USB dan kapasitasnya sebelum pengguna mengonfirmasi penghapusan.
- Memberikan status kemajuan selama media instalasi sedang dibuat.

## Fitur Utama

### Pemeriksaan ISO

- Memilih file ISO Windows dari komputer.
- Memeriksa volume dan berkas instalasi di dalam ISO.
- Mengenali keluarga versi Windows berdasarkan informasi citra instalasi, bukan hanya nama file.
- Menampilkan status ketika versi terdeteksi, tidak dikenali, atau ISO tidak dapat diperiksa.
- Menolak ISO yang tidak dikenali sebagai media instalasi Windows yang didukung oleh pemeriksaan WinTable.

### Deteksi USB

- Mencantumkan perangkat penyimpanan yang terhubung melalui USB.
- Menampilkan nomor disk, model, kapasitas, serta informasi produsen atau nomor seri jika tersedia.
- Mengecualikan disk boot dan disk sistem dari daftar target.
- Memeriksa kembali identitas perangkat terpilih sebelum media diubah untuk mengurangi risiko salah sasaran.

### Konfigurasi media

- Memilih skema partisi GPT atau MBR.
- Memilih target firmware UEFI atau BIOS dengan pemeriksaan kecocokan konfigurasi.
- Memilih FAT32 atau NTFS sesuai kombinasi target yang didukung.
- Menentukan label volume dan ukuran cluster yang tersedia pada antarmuka.
- Menggunakan FAT32 untuk media UEFI standar.

### Penanganan citra berukuran besar

- Menangani berkas citra instalasi yang melebihi batas ukuran berkas FAT32 dengan membaginya menjadi beberapa bagian yang dapat digunakan Windows Setup.
- Mendukung sumber instalasi berbentuk WIM, ESD, atau SWM apabila struktur ISO dapat dibaca dan diperiksa oleh Windows.

### Opsi kompatibilitas Setup

- Menyediakan opsi untuk menambahkan pengaturan kompatibilitas TPM dan Secure Boot pada media Windows Setup.
- Opsi ini diterapkan pada media yang dibuat dan tidak mengubah pengaturan firmware komputer.
- Penggunaan opsi kompatibilitas dapat mengurangi persyaratan pemeriksaan perangkat Windows Setup. Hal tersebut tidak menjamin dukungan, kestabilan, pembaruan, atau kelayakan perangkat untuk Windows.

### Status proses

- Menampilkan tahapan dan kemajuan proses pembuatan media.
- Menyampaikan pesan apabila pemeriksaan atau proses pembuatan gagal.
- Menampilkan hasil proses setelah pembuatan USB selesai.
- Menyediakan opsi untuk meminta komputer memulai ulang ke firmware setelah proses berhasil.

## Dukungan Windows dan Media

Versi Windows yang dikenali oleh pemeriksaan ISO WinTable:

| Keluarga Windows | Deteksi ISO |
|---|---|
| Windows 11 | Didukung |
| Windows 10 | Didukung |
| Windows 8.1 | Didukung |
| Windows 8 | Didukung |
| Windows 7 | Didukung |
| Windows Vista | Didukung |

Keterangan “didukung” di atas merujuk pada pengenalan keluarga Windows oleh aplikasi. Ini bukan jaminan bahwa setiap ISO, komputer, atau kombinasi firmware akan berhasil melakukan boot atau instalasi. Gunakan ISO yang valid dan sesuai dengan perangkat tujuan.

### Jenis sumber instalasi

WinTable memeriksa ISO Windows yang berisi direktori `sources` dan citra instalasi Windows yang dikenali, seperti:

- `install.wim`
- `install.esd`
- `install.swm`

ISO perlu dapat dipasang dan dibaca oleh Windows. ISO yang rusak, dimodifikasi dengan cara yang tidak dikenali, atau tidak mempunyai struktur media instalasi yang sesuai dapat ditolak.

## Pengaturan Media

| Pengaturan | Keterangan |
|---|---|
| GPT | Digunakan dengan target UEFI. |
| MBR | Tersedia untuk konfigurasi target yang kompatibel. |
| UEFI | Memerlukan FAT32 untuk media boot standar yang dibuat WinTable. |
| BIOS | Dapat menggunakan FAT32 atau NTFS sesuai pilihan dan pemeriksaan aplikasi. |
| FAT32 | Memiliki batas ukuran berkas tunggal dan batas pemformatan Windows yang perlu diperhatikan. |
| NTFS | Tersedia untuk skenario BIOS; bukan pilihan media UEFI standar pada WinTable. |
| Label volume | Label dibersihkan dari karakter yang tidak didukung dan dibatasi panjangnya saat media disiapkan. |
| Ukuran cluster | Pilihan disesuaikan dengan sistem berkas; pada FAT32 nilai yang terlalu besar dibatasi. |

Konfigurasi yang tidak cocok akan ditolak sebelum proses pembuatan media dimulai. Pemilihan UEFI dan GPT/FAT32 atau BIOS dan MBR tetap harus sesuai dengan kemampuan firmware komputer tujuan.

## Perlindungan dan Peringatan

> **PENTING: Seluruh isi USB yang dipilih akan dihapus.** Salin terlebih dahulu semua data penting ke lokasi lain. Pastikan model, kapasitas, dan nomor disk yang tampil benar sebelum menyetujui proses.

- WinTable meminta konfirmasi tambahan sebelum mengubah USB.
- Pengguna harus mengetik `ERASE` pada kolom konfirmasi.
- Hanya perangkat USB yang memenuhi kriteria aplikasi yang ditampilkan sebagai target.
- Disk boot dan disk sistem tidak ditampilkan sebagai target yang memenuhi syarat.
- Identitas disk diverifikasi kembali sebelum operasi penyiapan dimulai.
- ISO diperiksa sebelum USB diubah; kegagalan pemeriksaan ISO menghentikan proses.
- USB tetap dapat kehilangan seluruh data apabila pengguna mengonfirmasi perangkat yang salah.
- Jangan mencabut USB atau mematikan komputer ketika proses pembuatan sedang berlangsung.
- Gunakan hak administrator Windows untuk menjalankan aplikasi.
- Simpan salinan cadangan data USB sebelum memulai.

WinTable berinteraksi dengan partisi, sistem berkas, dan isi perangkat penyimpanan. Pastikan perangkat yang dipilih memang USB tujuan dan bukan perangkat yang menyimpan data penting.

## Persyaratan Sistem

- Komputer berbasis Windows.
- Hak akses administrator untuk menyiapkan media USB.
- USB penyimpanan yang terdeteksi Windows dan memiliki kapasitas memadai untuk berkas ISO.
- ISO instalasi Windows yang valid dan dapat dibaca oleh Windows.
- Ruang dan waktu yang cukup untuk menyalin serta menyiapkan berkas instalasi.
- Dukungan firmware komputer tujuan untuk boot dari USB.

WinTable menggunakan komponen dan utilitas Windows untuk memasang ISO, memeriksa citra, mengelola disk, menyalin berkas, dan menyiapkan media. Ketersediaan serta kebijakan Windows pada komputer dapat memengaruhi keberhasilan proses.

## Unduhan WinTable v1.0.8

Pilih salah satu format arsip berikut:

| Format | Tautan |
|---|---|
| ZIP | [Unduh WinTable v1.0.8 (.zip)](https://github.com/atharalfiandy/Wintable/releases/download/1.0.8/wintable-v1.0.8.zip) |
| TAR | [Unduh WinTable v1.0.8 (.tar)](https://github.com/atharalfiandy/Wintable/releases/download/1.0.8/wintable-v1.0.8.tar) |
| RAR | [Unduh WinTable v1.0.8 (.rar)](https://github.com/atharalfiandy/Wintable/releases/download/1.0.8/wintable-v1.0.8.rar) |
| 7Z | [Unduh WinTable v1.0.8 (.7z)](https://github.com/atharalfiandy/Wintable/releases/download/1.0.8/wintable-v1.0.8.7z) |

Unduhan disediakan sebagai arsip dalam beberapa format. Isi arsip dan nama berkas dapat dilihat setelah arsip dibuka. Unduh hanya dari halaman rilis resmi proyek.

## Batasan yang Perlu Diketahui

- FAT32 tidak dapat menyimpan satu berkas yang lebih besar dari batas FAT32. WinTable membagi citra instalasi besar yang didukung agar media dapat digunakan dengan FAT32.
- Windows membatasi pemformatan FAT32 melalui alur yang digunakan aplikasi. Untuk perangkat USB yang lebih besar dari 32 GB, WinTable menyiapkan partisi FAT32 berukuran sekitar 32 GB; sisa kapasitas perangkat dapat tidak digunakan.
- UEFI memerlukan FAT32 untuk media boot standar di WinTable.
- Dukungan deteksi keluarga Windows tidak berarti setiap edisi, pembaruan, atau citra kustom sudah diuji.
- Perilaku boot bergantung pada pengaturan firmware, Secure Boot, arsitektur komputer, dan kompatibilitas ISO.
- Opsi kompatibilitas TPM/Secure Boot tidak menjamin Windows dapat dipasang atau berjalan pada perangkat yang tidak memenuhi persyaratan Microsoft.
- Opsi mulai ulang ke firmware dapat gagal jika firmware atau Windows tidak mendukung permintaan tersebut.
- WinTable tidak menyediakan ISO, kunci produk, lisensi, atau dukungan untuk aktivasi Windows.

## Privasi dan Pemrosesan

Fungsi pembuatan media dalam skrip WinTable bekerja dengan ISO dan USB yang dipilih pada komputer pengguna, menggunakan utilitas Windows setempat. File ISO dipasang untuk diperiksa dan disalin; USB target diubah sesuai konfigurasi yang dipilih.

Jangan memilih ISO atau perangkat penyimpanan yang tidak Anda percayai. Periksa isi arsip unduhan dan pastikan sumber aplikasi adalah halaman rilis resmi proyek. Informasi ini menjelaskan alur yang terlihat pada skrip aplikasi dan bukan jaminan mengenai perilaku setiap distribusi atau paket pihak ketiga.

## Lisensi dan Hak Penggunaan

WinTable tidak menyertakan sistem operasi Windows. Pengguna bertanggung jawab untuk memperoleh ISO Windows dari sumber yang sah serta mematuhi ketentuan lisensi Microsoft yang berlaku.

Nama Windows dan merek terkait merupakan milik pemegang hak masing-masing. WinTable adalah alat pihak ketiga dan tidak menyatakan afiliasi, dukungan, atau persetujuan dari Microsoft.

## Informasi Proyek

- **Nama:** WinTable
- **Versi rilis yang ditautkan:** v1.0.8
- **Jenis aplikasi:** Aplikasi desktop Windows
- **Kegunaan:** Membuat media USB bootable dari ISO Windows
- **Repositori:** [atharalfiandy/Wintable](https://github.com/atharalfiandy/Wintable)
- **Rilis:** [WinTable v1.0.8](https://github.com/atharalfiandy/Wintable/releases/tag/1.0.8)
