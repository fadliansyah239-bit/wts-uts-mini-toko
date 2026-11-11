# Laporan UTS Web Software Tools

**Nama:**
**Nomor Induk Mahasiswa:**
**Kelas:**
**Tanggal:** 11 November 2026

## A. Bukti pemeriksaan masalah
| Masalah | Alat yang digunakan | Bukti pemeriksaan | Perkiraan penyebab | Perbaikan | Hasil setelah perbaikan |
|---|---|---|---|---|---|
| Produk | Browser dan pemeriksaan kode | `public/app.js` meminta `/api/barang`, sedangkan `server.mjs` menyediakan `/api/products`; ketidakcocokan ini membuat permintaan gagal. Setelah diperbaiki, halaman menampilkan 4 produk. | Path API pada frontend berbeda dari route server. | Mengubah URL fetch menjadi `/api/products`. | Keempat produk tampil dan status menunjukkan `4 produk tersedia`. |
| Tombol keranjang | Pemeriksaan kode dan uji interaksi browser | HTML tombol memakai kelas `.add-button`, tetapi listener mencari `.add-to-cart`. Setelah diperbaiki, klik tombol menambahkan produk dan klik kedua menaikkan kuantitas menjadi 2. | Selector listener tidak cocok dengan kelas tombol yang dirender. | Memasang listener pada `.add-button`. | Mouse Nirkabel tampil sebagai satu baris dengan kuantitas 2 di keranjang. |
| Total belanja | Tes otomatis Node.js dan uji interaksi browser | Implementasi awal menjumlahkan harga unit saja. Tes untuk kuantitas lebih dari satu dan uji browser menunjukkan 2 × Rp75.000 menghasilkan Rp150.000. | Kuantitas tidak dikalikan dengan harga unit. | Menghitung `item.price * item.quantity` untuk setiap item. | Total browser menjadi Rp150.000 untuk 2 Mouse Nirkabel. |

## B. Hasil pengujian
- Jumlah pengujian sebelum perbaikan: Tidak dijalankan sebelum perubahan, sehingga baseline tidak tersedia.
- Jumlah pengujian berhasil setelah perbaikan: 7 dari 7 (`node --test tests/*.test.mjs`).
- Catatan perubahan pada fungsi yang diperiksa: `calculateTotal` kini mengalikan harga dengan kuantitas; pengujian mencakup satu barang kuantitas dua dan dua jenis barang dengan kuantitas berbeda.

## C. Kualitas kode
- Temuan sebelum perbaikan: Endpoint katalog dan selector tombol tidak cocok; total mengabaikan kuantitas. Pemeriksaan Biome awal juga menemukan format `public/app.js` belum sesuai.
- Perbaikan yang dilakukan: Memperbaiki endpoint, selector, dan rumus total; memformat file JavaScript yang diubah dengan Biome.
- Hasil pemeriksaan ulang: `npm.cmd run quality:check` lulus untuk `public/app.js` dan `src/cart.js` tanpa temuan.

## D. Git
- Branch (jika membuat): `fix/three-store-bugs`.
- Ringkasan commit: Perbaikan pemuatan katalog, tombol keranjang, dan perhitungan total.
- Hasil pemeriksaan `git status`: Sebelum commit, tiga file terkait berubah pada branch ini; tidak ada file lain yang berubah.

## E. Pemakaian kecerdasan buatan (jika digunakan)
- Nama alat: GitHub Copilot.
- Pertanyaan/instruksi yang diberikan: Memeriksa dan memperbaiki tiga masalah pada daftar produk, tombol keranjang, dan total belanja; melengkapi bukti pemeriksaan pada laporan.
- Bagian jawaban yang diterapkan: Penyesuaian path API, selector tombol, rumus total, dan pemformatan file yang diubah.
- Cara memeriksa apakah saran tersebut benar: Menjalankan 7 tes Node.js, `npm.cmd run quality:check`, serta menguji halaman di browser dengan menambahkan Mouse Nirkabel dua kali.

## F. Refleksi singkat
- Satu pelajaran paling penting dari ujian ini: Saat menelusuri bug, cocokkan kontrak antarbagian aplikasi, seperti endpoint server dengan URL frontend dan kelas tombol dengan selector event; uji juga kasus kuantitas lebih dari satu.
