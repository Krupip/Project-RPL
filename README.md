# Ide Rekayasa Perangkat Lunak (RPL)

Dokumen ini berisi kumpulan ide dan rancangan spesifikasi awal untuk pengembangan proyek Rekayasa Perangkat Lunak (RPL). Dokumen ini mencakup deskripsi masalah, profil pengguna, arsitektur alur kerja, daftar fitur inti (MVP), integrasi sistem pihak ketiga, serta kriteria keberhasilan aplikasi.

---

## CueReserve: Sistem Reservasi Meja Biliar Online Terintegrasi Payment Gateway (DP)

### Deskripsi Masalah
Pengelolaan operasional *billiard pool/lounge* umumnya masih mengandalkan sistem *walk-in* atau reservasi manual melalui pesan instan (WhatsApp) dan buku catatan kasir. Metode konvensional ini menimbulkan sejumlah kendala:
* **Tingginya Angka Pembatalan Sepihak (*No-Show*):** Pelanggan memesan meja namun tidak hadir tanpa konsekuensi finansial, sehingga meja menganggur dan pengelola kehilangan potensi pendapatan.
* **Risiko *Double Booking*:** Potensi bentrok reservasi meja pada jam sibuk (*peak hours*) akibat keterlambatan admin memperbarui ketersediaan meja.
* **Verifikasi Pembayaran Manual yang Lambat:** Proses cek mutasi bank manual untuk uang muka (*down payment*) memperlambat konfirmasi pemesanan dan rawan kesalahan pencatatan.
* **Visibilitas Meja yang Rendah:** Pelanggan tidak dapat mengetahui ketersediaan meja secara *real-time* tanpa harus bertanya langsung ke pihak pengelola.

---

### Profil Target Pengguna
* **Pelanggan / Pemain Biliar:** Pemain perorangan atau komunitas yang ingin memesan meja spesifik pada tanggal dan jam tertentu tanpa risiko kehabisan meja saat tiba di lokasi.
* **Kasir / Operator Tempat Biliar:** Staf operasional yang memvalidasi kedatangan pelanggan (*check-in*), memantau status meja secara langsung, dan menyelesaikan pelunasan sisa tagihan.
* **Pemilik / Pengelola (*Owner/Manager*):** Pihak yang membutuhkan visibilitas riwayat transaksi, laporan utilisasi meja, dan ringkasan dana DP yang masuk.

---

### Manfaat Aplikasi
* **Mengurangi Risiko Kerugian Akibat *No-Show*:** Penerapan kewajiban pembayaran DP secara otomatis mengikat komitmen pelanggan sebelum slot dikunci.
* **Eliminasi Jadwal Bentrok (*Anti-Double Booking*):** Validasi otomatis di sisi *backend* memastikan tidak ada dua pemesanan yang bertabrakan pada meja dan rentang waktu yang sama.
* **Konfirmasi Reservasi Instan & Otomatis:** Integrasi *payment gateway* (QRIS/VA) memverifikasi pembayaran secara asinkron tanpa intervensi manual staf kasir.
* **Efisiensi Manajemen Meja:** Memudahkan kasir melacak status meja (tersedia, dipesan, sedang digunakan, atau kedaluwarsa) dalam satu antarmuka terpadu.

---

### Daftar Fitur Inti (MVP)

1. **Katalog & Ketersediaan Meja Interaktif:**
   * Tampilan daftar meja biliar beserta jenis/tipe meja, tarif sewa per jam, dan status ketersediaan berbasis filter tanggal serta rentang jam.
2. **Alur Pemesanan & Validasi Jadwal:**
   * Pemilihan meja, durasi sewa, dan perhitungan estimasi total sewa serta nominal uang muka (DP).
   * Validasi *overlap schedule* untuk mencegah konflik jadwal.
3. **Penguncian Slot Sementara (*Temporary Hold*):**
   * Meja berstatus terkunci sementara (*Pending Payment*) selama 10–15 menit saat transaksi tagihan dibuat agar tidak diambil pengguna lain.
4. **Integrasi Payment Gateway Otomatis (Midtrans Sandbox / QRIS & VA):**
   * Pembuatan token transaksi otomatis untuk menampilkan popup/antarmuka pembayaran langsung di website.
   * Mendukung pembayaran instan via QRIS Dinamis dan Virtual Account.
5. **Webhook Notifikasi & Transisi Status Otomatis:**
   * *Endpoint* khusus penerima notifikasi HTTP POST dari payment gateway untuk mengubah status transaksi menjadi *Confirmed* secara instan setelah pembayaran sukses.
   * Pembatalan otomatis (*Cancelled/Expired*) jika pembayaran melewati batas waktu, sehingga meja kembali berstatus tersedia.
6. **Dashboard Manajemen Kasir/Admin:**
   * Antarmuka pemantauan status pesanan masuk, pencarian kode pemesanan/QR saat pelanggan *check-in*, dan pencatatan pelunasan sisa sewa di kasir.

---

### Integrasi Eksternal & Lingkungan Pengembangan
* **Payment Gateway API:** Midtrans Snap API (Sandbox Environment).
* **Payment Tunneling (Testing Localhost):** Ngrok / Cloudflare Tunnel untuk penanganan Webhook Notifikasi HTTP POST.
* **Metode Pembayaran Utama:** QRIS Dinamis dan Bank Virtual Account (Simulasi Sandbox).

---

### Kriteria Aplikasi Dinyatakan Berhasil
* Sistem berhasil menolak reservasi baru jika jam yang dipilih beririsan (*overlap*) dengan reservasi yang sudah berstatus *Confirmed* atau *Pending Payment* aktif.
* Token transaksi dan pop-up pembayaran berhasil dimunculkan dengan nominal DP yang tepat.
* Webhook dari payment gateway berhasil memverifikasi *signature/hash key* dan memperbarui status pesanan di basis data dari `PENDING_PAYMENT` menjadi `CONFIRMED` dalam hitungan detik setelah transaksi sukses di simulator.
* Sistem secara otomatis mengembalikan status meja menjadi tersedia jika waktu tunggu pembayaran (15 menit) habis tanpa adanya konfirmasi pembayaran dari gateway.