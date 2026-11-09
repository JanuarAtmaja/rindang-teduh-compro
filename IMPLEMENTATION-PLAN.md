# Rencana Implementasi Rindang Teduh

## 1. Tujuan

Membangun website company profile Rindang Teduh dengan CodeIgniter 4 sesuai SRS, dimulai dari fondasi aplikasi dan fitur berprioritas tinggi. Implementasi akan dilakukan bertahap setelah keputusan pada bagian **Konfirmasi yang Masih Dibutuhkan** disepakati.

## 2. Acuan dan Batasan

- Sumber kebutuhan: [SOFTWARE REQUIREMENT SPECIFICATION.md](./SOFTWARE%20REQUIREMENT%20SPECIFICATION.md).
- Framework yang disebut dalam SRS: CodeIgniter 4.
- Referensi visual: [IPPUKU&MATCHA](https://ippukuandmatcha.jp/).
- Referensi dipakai untuk mengambil arah visual—hero fotografi yang dominan, navigasi minimal, tipografi elegan, ruang kosong, dan kontras gelap—bukan menyalin teks, logo, foto, atau aset proprietari situs tersebut.
- Produk tetap beridentitas Rindang Teduh. Foto, warna akhir, isi menu, kontak, dan informasi bisnis harus berasal dari pemilik.
- POS, chatbot, pembayaran online, dan integrasi transaksi eksternal bukan bagian rilis awal sesuai SRS.
- Tahap ini hanya perencanaan; belum membuat atau mengubah kode aplikasi.

## 3. Spesifikasi Arah Desain

### 3.1 Prinsip visual

- **Karakter:** editorial, tenang, premium tetapi tetap terasa seperti cafe yang ramah; gunakan foto besar, komposisi asimetris, ruang kosong yang lega, dan sedikit ornamen.
- **Adaptasi referensi:** ambil pola umum berupa header minimal di atas hero fotografis, headline di sisi kiri, subjek foto sebagai fokus visual di sisi kanan, serta navigasi yang tidak mendominasi. Jangan menyalin logo, copy, foto, ikon khas, maupun aset IPPUKU&MATCHA.
- **Identitas Rindang Teduh:** visual utama menggunakan suasana tempat, makanan/minuman, tanaman, atau detail interior milik Rindang Teduh. Jangan mengunci desain pada matcha atau budaya Jepang; isi dan foto harus sesuai bisnis sebenarnya.
- **Prioritas:** nama cafe dan tindakan utama terbaca jelas sebelum dekorasi. Hindari teks tipis/berkontras rendah di atas foto.

### 3.2 Color palette awal

Warna berikut adalah token awal desain, bukan klaim sebagai warna brand resmi. Dapat dikalibrasi setelah aset/identitas cafe tersedia.

| Token | Hex | Penggunaan |
| :--- | :--- | :--- |
| `Forest Night` | `#0B1410` | Latar dark utama, header/footer gelap |
| `Canopy` | `#14231B` | Surface/kartu pada area gelap |
| `Deep Forest` | `#244333` | Tombol/aksen hijau dan elemen aktif |
| `Moss` | `#74866A` | Aksen sekunder, ikon atau detail dekoratif |
| `Matcha Mist` | `#B8C7A3` | Highlight, hover/focus yang lembut pada dark |
| `Warm Cream` | `#F2EEE3` | Latar section terang dan teks utama di area gelap |
| `Paper` | `#FCFAF5` | Kartu/menu dan permukaan terang |
| `Ink` | `#202820` | Teks utama di permukaan terang |
| `Muted Ink` | `#626B60` | Teks sekunder di permukaan terang |
| `Line on Dark` | `#344239` | Garis pemisah/border pada dark |
| `Line on Light` | `#D8D6CB` | Border pada permukaan terang |

- CTA utama di area gelap: latar `Warm Cream`, teks `Forest Night`; pada hover gunakan `Matcha Mist`.
- CTA utama di area terang: latar `Deep Forest`, teks `Warm Cream`.
- Tautan sekunder menggunakan teks kontras tinggi dan underline/indikator hover; jangan mengandalkan perbedaan warna saja.
- Warna status dashboard harus konsisten dan dilengkapi label teks (contoh: “Menunggu Konfirmasi”), bukan warna saja.

### 3.3 Dark mode dan ritme terang-gelap

- **Default situs publik:** tema dark editorial dengan latar `Forest Night`; inilah art direction utama, bukan sekadar filter otomatis dari preferensi perangkat.
- Gunakan section `Warm Cream`/`Paper` secara bergantian untuk konten yang padat atau membutuhkan kenyamanan baca—terutama daftar menu dan form reservasi. Dengan begitu karakter dark tetap kuat tanpa membuat seluruh halaman berat dan monoton.
- Hero, section cerita/brand, footer, dan area foto dapat memakai dark; kartu informasi, menu, serta form dapat memakai latar terang.
- **Toggle dark/light:** tidak disediakan pada MVP; pilihan yang dikonfirmasi adalah dark editorial dengan section krem. Ini menjaga karakter visual konsisten tanpa menambah kompleksitas tema kedua.
- Dashboard admin menggunakan permukaan terang/netral untuk tabel dan form agar tugas operasional mudah dibaca; identitas hijau-krem dipakai sebagai aksen, bukan memenuhi seluruh layar dengan dark.
- Jaga kontras teks dan kontrol sesuai WCAG AA sebagai target; verifikasi nilai akhir dengan alat contrast checker, terutama teks kecil di atas foto dan warna muted.

### 3.4 Grid, jarak, dan tipografi

- Konten desktop menggunakan container maksimal sekitar `1200–1320px`, lebar baca teks sekitar `60–70 karakter`, dan gutter tepi minimal `5vw`.
- Grid dasar 12 kolom di desktop; beralih ke 4 kolom pada mobile. Gunakan kelipatan jarak `8px` (8/16/24/32/48/64/96px) dan hindari menjejalkan elemen.
- Headline memakai serif display yang elegan; isi, label, tombol, dan form memakai sans-serif yang jelas. Pilih font dengan lisensi yang sesuai, dukungan karakter Indonesia, dan fallback sistem; hindari tracking ekstrem untuk teks panjang.
- Hierarki acuan: headline hero desktop `clamp(2.5rem, 5vw, 5rem)`, headline section `clamp(2rem, 3.5vw, 3.5rem)`, isi minimal `16px`, label navigasi minimal `12px` dengan keterbacaan yang cukup.
- Animasi hanya untuk transisi singkat (fade/geser ringan); hormati `prefers-reduced-motion` dan jangan menjadikan animasi sebagai syarat untuk melihat konten.

### 3.5 Susunan halaman publik

1. **Header / navigasi**
   - Desktop: header transparan di atas hero, tinggi sekitar `88–104px`; logo/wordmark Rindang Teduh di kiri, navigasi di kanan.
   - Navigasi berisi Beranda, Menu, Reservasi, dan Kontak/Lokasi. CTA “Reservasi” menjadi satu-satunya tombol navigasi yang menonjol.
   - Gunakan pemisah garis tipis atau jarak yang lega; jangan menaruh terlalu banyak ikon. Saat halaman digulir, header dapat berubah menjadi solid `Forest Night` dengan tinggi lebih ringkas.
   - Mobile: tampilkan wordmark di kiri dan tombol menu yang jelas di kanan; menu terbuka sebagai panel/overlay yang mudah ditutup dan bisa digunakan dengan keyboard.
2. **Hero beranda**
   - Tinggi acuan desktop `min(100svh, 900px)`, dengan foto full-bleed dan overlay gradien gelap agar teks terbaca.
   - Headline, deskripsi singkat, dan CTA ditempatkan di kiri pada area sekitar sepertiga tengah layar; batas lebar copy sekitar `520px`.
   - Foto utama/subjek visual ditempatkan di tengah-kanan; sisakan area tenang di kiri untuk teks dan hindari crop yang memotong subjek penting.
   - CTA utama: “Lihat Menu” atau “Reservasi” sesuai prioritas bisnis; sediakan CTA sekunder yang lebih ringan. Tambahkan petunjuk scroll kecil di bagian bawah, bukan beberapa tombol bersaing.
   - Teks hero harus menggunakan konten Rindang Teduh yang disetujui; jangan memakai headline Jepang/contoh situs.
3. **Perkenalan cafe**
   - Section editorial dua kolom: narasi singkat di satu sisi dan foto suasana/detail di sisi lain; pada section berikutnya posisi dapat dibalik untuk ritme visual.
   - Gunakan latar gelap atau cream bergantian dan batasi panjang narasi agar tetap seperti company profile, bukan artikel panjang.
4. **Pratinjau menu**
   - Judul dan pengantar di atas, diikuti grid 3 kartu per baris desktop, 2 tablet, 1 mobile.
   - Setiap kartu berisi foto konsisten, nama, deskripsi singkat bila tersedia, dan harga; status ketersediaan ditampilkan sebagai teks yang jelas.
   - Tautan “Lihat semua menu” mengarah ke halaman menu lengkap. Jangan memasang harga/foto dummy seolah data resmi.
5. **Reservasi**
   - Section mudah ditemukan dari navigasi dan CTA. Desktop menggunakan layout dua kolom: informasi ketentuan di kiri, form/estimasi di kanan; mobile menjadi satu kolom dengan urutan informasi lalu form.
   - Form memisahkan pilihan jadwal/durasi, jumlah orang, data kontak, ringkasan estimasi, dan tombol kirim. Validasi/error tampil dekat field terkait; total estimasi diberi label “estimasi” sampai dikonfirmasi admin.
   - Batas maksimal 80 orang dan status permintaan dijelaskan secara eksplisit; jangan menjanjikan slot terkonfirmasi sebelum admin mengonfirmasi.
6. **Kontak dan lokasi**
   - Tampilkan alamat, jam operasional, tombol peta, dan tautan Instagram dalam blok yang mudah dipindai; gunakan dua kolom desktop dan susunan vertikal mobile.
   - CTA Instagram mengarah ke akun Rindang Teduh yang telah diberikan; peta dapat berupa tautan/embed ringan sesuai keputusan implementasi.
7. **Footer**
   - Latar `Forest Night`, wordmark, tautan utama, kanal sosial, alamat/jam bila datanya tersedia, serta copyright.
   - Hindari footer yang padat atau menduplikasi seluruh isi halaman.

### 3.6 Adaptasi responsif

- **Desktop (≥1024px):** hero dua fokus (copy kiri, foto kanan); grid menu tiga kolom; form reservasi dua kolom.
- **Tablet (768–1023px):** kurangi ruang navigasi dan ukuran headline; grid menu dua kolom; ubah reservasi menjadi kolom tunggal bila ruang terlalu sempit.
- **Mobile (<768px):** hero sekitar `80–90svh` dengan copy di bagian bawah-kiri pada lapisan gradien; jaga subjek foto tetap terlihat. Navigasi menjadi menu overlay, grid satu kolom, tombol utama selebar area konten bila membantu penggunaan.
- Jaga target sentuh minimal sekitar `44×44px`, cegah scroll horizontal, dan jangan menaruh teks penting hanya di atas bagian foto yang terang/ramai.
- Foto di luar viewport menggunakan lazy loading; hero memakai ukuran/crop responsif dan tidak di-lazy-load bila itu memperlambat tampilan awal.

### 3.7 Prinsip visual dashboard admin

- Pisahkan layout publik dan admin; jangan memakai hero atau animasi editorial di layar operasional.
- Sidebar/nav admin sederhana: Ringkasan, Menu, Reservasi, dan akun/logout sesuai hak akses.
- Halaman reservasi mengutamakan tabel yang bisa dipindai: identitas pemesan, jadwal/durasi, jumlah orang, estimasi, status, dan aksi. Status selalu berupa badge berlabel teks.
- Form admin memakai label permanen, validasi yang jelas, tombol simpan/batal yang berbeda, dan konfirmasi sebelum penghapusan.
- Desain dashboard diprioritaskan untuk desktop tetapi tetap dapat digunakan di tablet/mobile.

### 3.8 Aset, performa, dan kriteria review desain

- Gunakan aset asli yang diberikan pemilik atau aset berlisensi; jangan hotlink foto dari situs referensi.
- Sediakan foto hero landscape beresolusi cukup, crop mobile, foto menu konsisten, logo/wordmark (jika ada), dan teks bisnis final sebelum polishing.
- Targetkan gambar tampilan sekitar `≤200 KB` sesuai RT-NF-04 jika kualitas visual memungkinkan; gunakan format modern yang didukung dan fallback yang sesuai.
- Sebelum implementasi dianggap siap ditinjau, periksa desktop/mobile, keterbacaan tanpa gambar, kontras, keyboard/focus, kondisi validasi/error form, dan performa halaman awal.

## 4. Urutan Pengerjaan yang Diusulkan

### Tahap 0 — Fondasi CodeIgniter 4

- Siapkan aplikasi CI4, konfigurasi lingkungan, koneksi basis data, routing, layout publik/admin, dan struktur view yang terpisah.
- Siapkan pola validasi, migrasi/seed data awal, serta pengamanan dasar CI4 (CSRF, escaping output, validasi input).
- Pastikan beranda dan halaman dasar dapat dijalankan secara lokal sebelum fitur bisnis ditambahkan.

**Hasil yang diharapkan:** aplikasi CI4 minimal yang bisa dijalankan, dengan struktur siap dikembangkan dan tanpa fitur di luar lingkup.

### Tahap 1 — Fitur Prioritas Tinggi (MVP)

1. **Autentikasi admin (RT-F-01)**
   - Login/logout untuk pengguna yang berhak mengakses dashboard.
   - Pembatasan akses dashboard dan pengelolaan berdasarkan peran, mengikuti proposal peran admin yang telah disetujui.
2. **Kelola menu dan opsi reservasi (RT-F-02)**
   - Admin yang berwenang dapat menambah, mengubah, dan menghapus data menu.
   - Pengelolaan jadwal, harga, ketentuan, serta kapasitas reservasi.
3. **Halaman publik dan daftar menu (RT-F-04A, RT-F-06, RT-F-07)**
   - Menampilkan informasi umum yang disetujui untuk MVP serta daftar menu terbaru dari data admin.
   - Beranda, menu, reservasi, dan kontak dapat dijangkau maksimal tiga klik (RT-NF-11).
4. **Informasi dan alur permintaan reservasi (RT-F-09 s.d. RT-F-12)**
   - Pengunjung memilih durasi dan jumlah orang; sistem menghitung estimasi akumulatif dan memvalidasi jumlah maksimum 80 orang.
   - Rumus harga final serta jumlah minimum belum ditentukan; kalkulator harga belum bisa diselesaikan sampai aturan tersebut tersedia.
   - Sistem menyimpan permintaan beserta kontak, pilihan durasi/jadwal, jumlah orang, estimasi harga, dan status awal “Menunggu Konfirmasi”.
   - Admin dapat memperbarui status reservasi melalui dashboard.
   - Setelah penyimpanan berhasil, pengunjung diarahkan ke Instagram bisnis untuk menghubungi admin dan melanjutkan konfirmasi.
5. **Kebutuhan lintas fitur prioritas tinggi**
   - Validasi server-side dan perlindungan terhadap SQL injection, XSS, serta CSRF (RT-NF-06).
   - Pencatatan data permintaan reservasi sesuai kebutuhan audit transaksi (RT-NF-05).
   - Sasaran performa beranda di bawah lima detik pada perangkat/koneksi sesuai RT-NF-01; gambar mengikuti batas dan teknik optimasi dalam RT-NF-04.

**Kriteria selesai MVP:** skenario admin mengelola menu/jadwal, pengunjung melihat informasi dan menu, lalu mengirim permintaan reservasi tersimpan dengan status awal yang benar dapat diuji end-to-end.

## 5. Fitur Berikutnya (Prioritas Sedang/Rendah)

Tidak dikerjakan sebelum MVP disetujui, kecuali diprioritaskan ulang:

- Log login/logout dan percobaan login gagal (RT-F-03).
- Pengelolaan informasi cafe oleh admin, Google Maps, jam operasional, CTA media sosial, dan QR Code (RT-F-04B, RT-F-05, RT-F-14; perlu klarifikasi karena nomor RT-F-14 digunakan lebih dari sekali dalam SRS).
- Detail menu (RT-F-08), kontrol ketersediaan oleh kasir (RT-F-13).
- Penyesuaian sesi otomatis, pengujian kompatibilitas dan beban, serta informasi kapasitas tambahan (RT-NF-02/03/08/10/12/13).

## 6. Keputusan dan Asumsi yang Telah Dikonfirmasi

- Arah visual: editorial gelap dengan aksen hijau-krem.
- Tema publik: dark editorial dengan section krem untuk menu/form, tanpa toggle dark/light.
- Kanal konfirmasi reservasi: Instagram.
- Pembagian hak akses admin pada rencana disetujui.
- Seluruh fitur Tahap 1 termasuk lingkup MVP.
- Estimasi reservasi dihitung dari durasi dan jumlah orang secara akumulatif; maksimum 80 orang, minimum dan rumus harga menyusul.
- Permintaan reservasi disimpan di website; admin memperbarui status melalui dashboard, dan pengunjung diarahkan ke Instagram setelah pengajuan tersimpan.
- Akun Instagram bisnis: [@rindangteduh_](https://www.instagram.com/rindangteduh_/).
- Lingkungan yang diinginkan: PHP 8.5.12, Supabase sebagai database, dan Vercel sebagai pilihan hosting utama.

## 7. Keputusan Teknis Awal yang Diusulkan

- Gunakan CodeIgniter 4 sesuai SRS. Sebelum scaffold, verifikasi kompatibilitas versi CI4 yang dipilih dengan PHP 8.5.12.
- Gunakan PostgreSQL pada Supabase; pastikan opsi koneksi yang sesuai untuk aplikasi yang berjalan di Vercel.
- Usahakan deployment di Vercel terlebih dahulu dan verifikasi jalur CI4 (runtime, routing, dan penyimpanan konfigurasi). Jika hosting tersebut tidak cocok, minta persetujuan sebelum memilih alternatif.
- Database relasional dengan migrasi skema dan data awal terpisah dari kode aplikasi.
- Tampilan menggunakan HTML/CSS responsif dan JavaScript seperlunya; pemilihan framework CSS ditunda sampai preferensi tim dikonfirmasi.
- Reservasi disimpan dahulu, baru diarahkan ke Instagram; kegagalan penyimpanan tidak boleh terlihat seperti pengiriman berhasil.
- Foto dan konten contoh tidak akan dianggap sebagai data final.

## 8. Risiko dan Ketergantungan

- Rumus harga dan jumlah minimum belum ditentukan; kalkulator estimasi belum dapat diimplementasikan benar tanpa aturan tersebut.
- Field kontak minimum dan daftar status reservasi yang boleh dipilih admin perlu dipastikan saat desain form/dashboard.
- Aturan durasi/slot dan penerapan batas 80 orang perlu diselaraskan dengan RT-NF-12 dalam SRS.
- Versi CI4 yang kompatibel dan jalur deployment di Vercel perlu diverifikasi sebelum membuat fondasi; jika tidak cocok, perlu persetujuan untuk solusi alternatif.
- Data nyata (menu, harga, foto, jam operasional, lokasi, tautan konfirmasi) dibutuhkan untuk menghindari konten placeholder saat siap rilis.

## 9. Konfirmasi yang Masih Dibutuhkan Sebelum Implementasi

Keputusan berikut masih diperlukan sebelum alur reservasi dan implementasi dapat diselesaikan:

1. **Rumus harga dan minimum pemesan:** formula per durasi/per orang dan jumlah minimum menyusul; kalkulasi harga final tertahan sampai nilai ini tersedia.
2. **Aturan slot:** bagaimana durasi yang tersedia ditentukan, dan bagaimana batas maksimum 80 orang diterapkan pada slot yang dipilih?
3. **Data kontak dan status:** SRS menyebut nama serta nomor telepon/WhatsApp; mohon konfirmasi jika ada field lain atau daftar status khusus selain “Menunggu Konfirmasi”.
4. **Arah Instagram:** akun telah ditentukan; perlu dipilih apakah CTA membuka profil atau tautan DM.
5. **Hosting:** Vercel diusahakan terlebih dahulu; jika uji kompatibilitas CI4 menemui kendala, persetujuan diperlukan untuk alternatif hosting.
6. **PHP:** versi yang dikonfirmasi adalah PHP 8.5.12; ketersediaan dan kompatibilitasnya tetap perlu diverifikasi pada target deployment.

## 10. Langkah Setelah Konfirmasi

1. Lengkapi aturan harga/slot dan evaluasi kompatibilitas runtime/deployment.
2. Perbarui rencana bila jawaban mengubah ruang lingkup atau alur.
3. Siapkan fondasi CodeIgniter 4 dan jalankan aplikasi lokal.
4. Implementasikan fitur Tahap 1 secara berurutan, dengan validasi dan pengujian untuk setiap alur.
5. Tinjau hasil MVP sebelum memulai fitur prioritas sedang/rendah.
