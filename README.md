# Progress Pal (PWA)

## Menjalankan untuk uji lokal
Karena PWA memerlukan service worker, jangan membuka `index.html` dengan double-click (`file://`). Jalankan server lokal dari folder ini:

```bash
python -m http.server 8000
```

Lalu buka `http://localhost:8000` di browser. Untuk dipasang di HP dan mendapatkan notifikasi, deploy seluruh isi folder ke hosting HTTPS (misalnya GitHub Pages untuk UI statis, atau hosting web lain).

## Fitur
- Desain dark glassmorphism responsif, navigasi desktop dan navigasi bawah di HP.
- Dashboard, jam real-time, tanggal, progres jadwal hari ini, dan pelajaran berikutnya.
- Jadwal kelas berdasarkan data yang diekstrak dari `DATA_RESMI` di program Progress Pal. Ketuk blok untuk menambah catatan yang terhubung dengan mapel/kelas.
- Blok lampau menjadi abu-abu berdasarkan waktu lokal perangkat. Break/jeda ditampilkan jika ada celah JP pada hari tersebut.
- Catatan per mapel/kelas dengan tanggal pengingat, waktu, dan pilihan H-1/H-2/H-3/H-7/H-14.
- Notifikasi browser saat tanggal/jam pengingat tercapai ketika aplikasi/halaman aktif, izin notifikasi diberikan, dan browser mendukungnya.
- Daftar tugas dengan prioritas, tenggat, dan checklist.
- Cari jadwal berdasarkan guru, mapel, atau kelas.
- Penyimpanan profil, catatan, tugas, dan pengingat di localStorage perangkat.
- PWA manifest dan service worker untuk pemasangan layar utama dan cache dasar.

## Batasan penting tentang lockscreen
Notifikasi browser bisa tampil di layar kunci setelah izin diberikan dan perangkat/browser mendukungnya. Namun, pemeriksaan pengingat pada versi ini berjalan saat halaman aktif; jika browser/OS menutup aplikasi sepenuhnya, pengingat terjadwal tidak dijamin muncul. Agar notifikasi H-1/H-7 tetap dikirim saat aplikasi tertutup, perlu backend dengan scheduler + Web Push (VAPID) atau aplikasi Android native dengan alarm/notification. PWA ini juga menyimpan data di perangkat dan belum menyinkronkan catatan antarperangkat.

## Deploy
Unggah seluruh isi folder ke hosting yang menyediakan HTTPS. Di Android Chrome buka URL, pilih menu ⋮ lalu “Tambahkan ke layar utama”/“Install app”. Notifikasi membutuhkan izin eksplisit pengguna.

## Fitur tambahan progres belajar
- Halaman Progres Belajar: target waktu belajar harian yang dapat diubah, jumlah menit, jumlah sesi, streak hari, dan total waktu belajar tujuh hari terakhir.
- Pencatatan sesi belajar manual atau melalui timer Pomodoro; sesi yang selesai dicatat ke riwayat dan dapat dihapus.
- Kutipan harian berbahasa Inggris dengan pilihan untuk melihat kutipan lain.
- Checklist kebiasaan harian yang tersimpan per tanggal.
- Pengingat pribadi dengan tanggal dan waktu, penandaan selesai, serta penghapusan.
- Data progres, target, checklist, dan pengingat disimpan pada penyimpanan lokal browser di perangkat.

## Batasan fitur progres dan pengingat
- Progres dan pengingat tersimpan pada perangkat/browser yang sedang digunakan; data tidak otomatis tersinkronisasi dengan perangkat lain.
- Timer Pomodoro berjalan selama halaman tetap aktif di browser. Jika browser menangguhkan atau menutup halaman, timer dapat berhenti atau terlambat.
- Pengingat tambahan diperiksa saat halaman terbuka. Notifikasi ketika aplikasi tertutup atau perangkat tidak menjalankan halaman tidak dijamin tanpa layanan push terjadwal atau aplikasi Android native.
- Kutipan harian adalah pilihan kutipan singkat dalam bahasa Inggris; atribusi dicantumkan jika dikenal dan label Progress Pal digunakan untuk kutipan orisinal.


## Fitur tambahan (v4)
- **Statistik mingguan**: ringkasan menit dan sesi belajar selama 7 hari terakhir serta grafik per hari.
- **Countdown ujian**: simpan beberapa ujian beserta tanggalnya dan pantau sisa hari.
- **Backup & restore**: ekspor data localStorage Progress Pal ke JSON dan impor kembali di browser yang sama/berbeda. Restore mengganti data aplikasi yang cocok.
- **Vocabulary dinamis**: mencoba mengambil kata acak dan definisi dari layanan publik saat online, menyimpan kata yang pernah muncul, menampilkan 20 kata harian, dan menggunakan bank lokal jika API tidak tersedia. Kata yang berasal dari kamus online memiliki definisi bahasa Inggris; terjemahan Indonesia tidak selalu tersedia. Tidak ada layanan gratis yang menjamin kata baru tanpa batas atau bebas kuota, jadi pengulangan masih mungkin setelah sumber yang tersedia habis.

Data tetap tersimpan secara lokal di browser. Backup disarankan sebelum berpindah perangkat atau menghapus data browser.


## Vocabulary dan quotes dinamis (v5)
- Quotes mencoba mengambil kutipan dari ZenQuotes, lalu menggunakan koleksi lokal saat offline, API gagal, atau kutipan online sudah pernah ditampilkan.
- Kosakata mencoba mengambil kata acak dan definisi dari Random Word API + Dictionary API, menyimpan riwayat di browser, dan menyediakan fallback lokal.
- Aplikasi membutuhkan koneksi internet untuk konten online. API pihak ketiga dapat mengalami batas kuota, CORS, atau perubahan layanan. “Unlimited” tidak dapat dijamin secara literal; sistem menghindari pengulangan selama tersedia konten baru yang diketahui aplikasi.
- Karena definisi dari kamus online berbahasa Inggris, arti Indonesia untuk kata-kata online tidak dijamin; bank lokal tetap menyertakan glosarium Indonesia.


## v6 — akun lokal dan perbaikan mobile
- Layar pemilihan profil muncul sebelum aplikasi digunakan pertama kali.
- Bisa membuat beberapa profil di satu browser/perangkat dan beralih akun dari tombol ⇄ di header.
- Data Progress Pal disimpan dalam ruang penyimpanan terpisah per profil pada browser ini. Profil bukan login online dan tidak dilindungi kata sandi.
- Profil pertama akan mencoba membawa data Progress Pal lama ke ruang akun baru.
- Logo PP memakai ukuran tetap; navigasi bawah HP disederhanakan menjadi lima tombol agar tidak terdistorsi. Menu lain tetap tersedia di navigasi samping.
- Cache PWA dinaikkan ke v6 agar file akun dan perbaikan tampilan ikut diperbarui.
