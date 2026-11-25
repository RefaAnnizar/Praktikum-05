# Laporan Praktikum Pertemuan 5 — Pemrograman Web 1

Nama : MUHAMMAD REFA ANNIZAR NOORDIANTO  
NIM : 2510010396  
Kelas : 3A

> Catatan: tabel pengamatan di bawah diisi berdasarkan hasil yang diharapkan dan perhitungan pada modul. Angka ini merupakan hasil teoritis untuk dicocokkan kembali melalui DevTools saat file dijalankan, bukan klaim pengukuran langsung dari komputer.

## Percobaan 1 — Box Model

| No | Kondisi | Lebar Kotak A (px) | Lebar Kotak B (px) |
|---:|---|---:|---:|
| 1 | padding 20px | 350 | 300 |
| 2 | padding 40px | 390 | 300 |

| No | Kondisi | Jarak judul–paragraf (px) |
|---:|---|---:|
| 3 | Block biasa (margin collapse) | 30 |
| 4 | Di dalam flex column | 50 |

| No | Kondisi `.menu a` | Latar menimpa teks lain? |
|---:|---|---|
| 5 | inline (bawaan) | Ya, padding vertikal dapat menimpa baris teks di sekitarnya |
| 6 | inline-block | Tidak, ruang elemen ikut diperhitungkan dan baris teks terdorong |

**Penjelasan:** Pada `content-box`, lebar total dihitung dari content + padding kiri/kanan + border kiri/kanan. Karena itu Kotak A menjadi 300 + 40 + 10 = 350 px, lalu 300 + 80 + 10 = 390 px saat padding 40 px. Pada `border-box`, width 300 px sudah mencakup content, padding, dan border sehingga lebar luar tetap 300 px.

## Percobaan 2 — Flexbox Lab

| No | Properti dan nilai | Pengamatan |
|---:|---|---|
| 1 | `display: flex` | Tiga item yang semula tersusun vertikal berubah menjadi satu baris horizontal. Tinggi item mengikuti tinggi container karena nilai awal `align-items` adalah `stretch`. |
| 2 | `justify-content: space-between` | Item A berada di kiri, item C di kanan, dan item B berada di antara keduanya; ruang sisa dibagikan di antara item tanpa ruang tepi. |
| 2 | `justify-content: space-evenly` | Jarak antaritem dan jarak dari item terluar ke tepi container sama besar. |
| 3 | `align-items: stretch` vs `center` | `stretch` membuat item memenuhi tinggi cross axis; `center` mempertahankan tinggi sesuai isi dan memusatkan item pada cross axis. |
| 4 | `flex-direction: column` + `justify-content: center` | Main axis berubah menjadi vertikal. Item tersusun dari atas ke bawah dan kelompok item berada di tengah secara vertikal. |
| 5 | 8 item × 200 px, nowrap vs wrap | `nowrap` memaksa item tetap satu baris sehingga item menyusut (`flex-shrink`). `wrap` mempertahankan lebar 200 px dan memindahkan item ke baris berikutnya. |
| 6 | `.b { flex-grow: 1 }` | Item B mengambil ruang kosong yang tersedia, sedangkan A dan C tetap mengikuti ukuran dasarnya. |
| 7 | Lebar A / B / C | A = 200 px; B ≈ 266,7 px; C ≈ 533,3 px (container 1000 px, padding horizontal item sementara 0). |
| 8 | `.c { order: -1 }` | C tampil paling kiri. Urutan elemen di HTML tidak berubah. |
| 9 | `.c { margin-left: auto }` | Margin kiri otomatis menyerap ruang sisa sehingga C terdorong ke sisi kanan. |
| 10 | `gap: 24px` | Ada jarak 24 px di antara item, tanpa menambahkan jarak di tepi container. |

**Perhitungan eksperimen 7:** A ditetapkan `flex: 0 0 200px`, sehingga lebarnya 200 px. Sisa ruang adalah 1000 − 200 = 800 px. Karena B dan C memakai basis 0 dengan faktor grow 1 : 2, B memperoleh 800 × 1/3 = 266,7 px dan C memperoleh 800 × 2/3 = 533,3 px.

## Percobaan 3 — Positioning

| No | Eksperimen | Pengamatan |
|---|---|---|
| 1 | Header sticky saat digulir | Header mengikuti aliran dokumen pada posisi awal, lalu menempel di tepi atas viewport ketika halaman digulir. Paragraf tidak tertutup. |
| 2a | Header fixed tanpa padding-top body | Header keluar dari aliran normal dokumen sehingga bagian atas konten (judul/paragraf) dapat tertutup header. |
| 2b | Header fixed dengan padding-top 64px | Ruang di atas konten disediakan sebesar tinggi header sehingga konten tidak lagi tertutup. |
| 3 | `.notif` tanpa `position: relative` | Badge tidak lagi mengacu pada tombol notifikasi; ia berpindah ke leluhur terdekat yang memiliki positioning, yaitu header sticky. |
| 4 | `.lapis-1` z-index 3, lalu `.lapis-2` z-index 5 | Lapis 1 naik di atas lapis lain saat diberi z-index 3; setelah Lapis 2 diberi z-index 5, Lapis 2 menjadi yang paling depan. |
| 5 | Header z-index 1 | Lapis 1 (z-index 3) dan Lapis 2 (z-index 5) dapat menutupi header ketika bertumpuk dengannya. |
| 6 | Tombol Bantuan di layar 375 px | Tombol tetap berada di pojok kanan bawah viewport karena menggunakan `position: fixed`. |

## Percobaan 4 — Dashboard

Proyek dashboard dibuat pada folder `p4-dashboard/` dengan struktur HTML5 semantik: `header`, `nav`, `aside`, `main`, dan `footer`. Layout menggunakan Flexbox untuk navbar, sidebar dan konten, menu, serta kartu statistik. Sidebar menggunakan `flex: 0 0 240px`, navbar menggunakan `position: sticky`, badge notifikasi memakai pola `relative` + `absolute`, dan footer didorong ke bagian bawah oleh `flex: 1` pada wrapper.

Tiga tugas mandiri wajib telah ditambahkan:
1. Profil pengguna dengan avatar inisial 32 px dan teks **Admin Prodi** di antara tombol notifikasi dan Logout.
2. Tautan **Pengaturan** di bagian bawah sidebar menggunakan `margin-top: auto`.
3. Label **Baru** pada kartu **Kelas Hari Ini** menggunakan parent `position: relative` dan label `position: absolute`.

**Pemeriksaan yang perlu dilakukan di browser:** buka `p4-dashboard/index.html` dengan Live Server, cek lebar sidebar 240 px pada panel Computed, lalu uji lebar 1366 px dan 375 px. Simpan tangkapan layar aktual sebagai `desktop.png` dan `mobile.png` di folder `p4-dashboard/`. Tangkapan layar tidak disertakan sebagai hasil simulasi agar tidak dianggap sebagai bukti pengujian browser yang belum dilakukan.

## Jawaban Pertanyaan Analisis

1. `box-sizing: border-box` memudahkan pengaturan ukuran karena nilai `width` sudah mencakup content, padding, dan border. Dengan begitu, ukuran elemen lebih mudah diprediksi dan sidebar yang ditargetkan 240 px tidak melebar akibat padding atau border. Aturan global ini juga membuat perhitungan layout lebih konsisten.

2. Pada `flex-direction: column`, main axis berubah menjadi vertikal, sedangkan cross axis menjadi horizontal. Karena `justify-content` bekerja pada main axis, nilai `center` memusatkan kumpulan item dari atas ke bawah di tengah container. Inilah sebabnya item terkumpul di tengah secara vertikal.

3. Lebar A ditetapkan 200 px, sehingga sisa ruang container 1000 − 200 = 800 px. B dan C memiliki basis 0 dengan faktor `flex-grow` 1 : 2, sehingga B mendapat 800/3 ≈ 266,7 px dan C mendapat 1600/3 ≈ 533,3 px. Jika B menggunakan `flex: 1 1 auto`, basisnya mengikuti ukuran konten awal (bukan 0%), sehingga ruang sisa dibagikan setelah basis awal B dan item lain diperhitungkan; hasil lebar B dan C tidak lagi mengikuti pembagian sederhana 1 : 2 dari 800 px.

4. Badge menggunakan `position: absolute`, sehingga posisinya dihitung relatif terhadap leluhur terdekat yang memiliki positioning selain `static`. Ketika `position: relative` di `.notif` dihapus, acuan tersebut bukan lagi tombol notifikasi, melainkan header yang `position: sticky`. Akibatnya badge tampak menempel di pojok kanan atas header.

5. `sticky` tetap menjadi bagian dari aliran dokumen sebelum menempel di tepi viewport, sehingga konten di bawahnya tidak langsung tertutup. `fixed` selalu mengacu pada viewport dan keluar dari aliran dokumen, sehingga perlu ruang pengganti seperti `padding-top`. Untuk navbar dashboard ini saya memilih `sticky`, karena lebih sederhana dan konten awal tidak tertutup saat halaman dibuka.

6. `flex: 1` pada `.wrapper` membuat wrapper mengambil ruang kosong yang tersedia di dalam body yang menggunakan Flexbox kolom. Hal ini membantu footer terdorong ke dasar layar ketika konten sedikit. Jika deklarasi tersebut dihapus, wrapper hanya setinggi kontennya sehingga footer dapat naik dan tidak berada di bagian bawah viewport.

## Kesimpulan

Praktikum ini menunjukkan bahwa Box Model menentukan ukuran nyata elemen, sedangkan Flexbox membantu menyusun komponen halaman pada main axis dan cross axis. Positioning digunakan untuk membuat elemen menempel, menjadi acuan posisi, dan mengatur lapisan dengan z-index. Pada proyek dashboard, konsep tersebut diterapkan untuk membuat navbar, sidebar, kartu statistik, profil pengguna, dan footer yang responsif. Pengujian akhir melalui DevTools dan pengambilan screenshot pada ukuran desktop serta mobile tetap perlu dilakukan pada browser lokal.
