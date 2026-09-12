# Ide Rekayasa Perangkat Lunak (RPL)

Dokumen ini berisi kumpulan ide dan rancangan spesifikasi awal untuk pengembangan proyek Rekayasa Perangkat Lunak (RPL). Setiap ide mencakup deskripsi masalah, target pengguna, manfaat, daftar fitur inti (MVP), fitur, serta kriteria keberhasilan aplikasi.

## Sistem Manajemen Jadwal & Reservasi Lapangan Olahraga Lokal

### Deskripsi Masalah
Pengelola fasilitas olahraga skala komunitas atau kampus (seperti lapangan badminton, basket, dan futsal) umumnya masih menggunakan pencatatan manual via chat aplikasi pesan atau buku kas fisik. Hal ini menimbulkan berbagai kendala, seperti:
* Kesalahan pencatatan slot ganda (*double booking*).
* Kesulitan verifikasi pembayaran uang muka (*DP*) secara rapi.
* Repotnya pemain yang ingin mengecek ketersediaan jam tanpa harus menunggu balasan admin.

### Profil Target Pengguna
* **Penyewa / Komunitas Olahraga:** Pemain yang mencari slot lapangan kosong untuk latihan rutin atau *sparing*.
* **Pengelola Fasilitas Olahraga:** Pihak yang mengontrol jadwal, pencatatan pembayaran, dan pemeliharaan fasilitas.

### Manfaat Aplikasi
* Menghilangkan potensi *double booking* di slot jam latihan yang sama.
* Mengurangi beban operasional admin dalam membalas pertanyaan ketersediaan jadwal secara manual.

### Daftar Fitur Inti (MVP)
1. **Kalender Slot Jadwal:** Tampilan grid interaktif berisi status slot waktu lapangan (Kosong vs Terisi).
2. **Reservasi Slot Lapangan:** Pemilihan lapangan, tanggal, dan rentang jam main langsung di kalender.
3. **Unggah & Verifikasi Bukti Pembayaran:** Fitur unggah bukti transfer manual bagi penyewa dan tombol konfirmasi bagi admin untuk mengunci status reservasi (*Locked*).
4. **Laporan Ringkasan Penggunaan:** Rekap utilisasi jam penggunaan per lapangan mingguan atau bulanan bagi pengelola.

### Kriteria Aplikasi Dinyatakan Berhasil
* Ketika satu pengguna mengunci slot jam tertentu, slot tersebut langsung berstatus nonaktif bagi pengunjung lain.
* Admin dapat mengubah status reservasi dari *Pending Verification* menjadi *Confirmed* yang secara otomatis memperbarui rekap kas masuk.

---

## Portal Pendataan Kerusakan & Keluhan Fasilitas Lingkungan Perumahan/RT

### Deskripsi Masalah
Warga lingkungan perumahan sering melaporkan kerusakan fasilitas umum (seperti lampu jalan mati, saluran air tersumbat, portal rusak, atau tumpukan sampah) melalui grup chat warga yang acak. Akibatnya:
* Laporan cepat tenggelam oleh obrolan harian.
* Pengurus RT/RW kesulitan memprioritaskan anggaran perbaikan.
* Warga tidak tahu apakah laporan mereka sedang ditindaklanjuti atau diabaikan.

### Profil Target Pengguna
* **Warga Lingkungan:** Pelapor kerusakan fasilitas di area tempat tinggalnya.
* **Pengurus RT/RW / Tim Pemeliharaan:** Pihak yang memverifikasi, menentukan tingkat urgensi, dan memperbarui status pengerjaan fasilitas.

### Manfaat Aplikasi
* Mencegah laporan keluhan fasilitas umum tercecer di percakapan grup chat biasa.
* Memberikan transparansi proses tindak lanjut perbaikan fasilitas umum kepada warga.

### Daftar Fitur Inti (MVP)
1. **Form Pelaporan Tiket:** Warga mengunggah foto kerusakan, titik lokasi/blok, kategori fasilitas, dan deskripsi masalah.
2. **Status Tracking Tiket:** Alur status laporan yang jelas (Diterima, Disurvei, Pengerjaan, Selesai Ditangani).
3. **Validasi "Upvote/Konfirmasi Warga":** Warga lain di area yang sama dapat menandai bahwa masalah tersebut juga mereka alami guna membantu menentukan prioritas penanganan.
4. **Unggah Bukti Hasil Perbaikan:** Pengurus mengunggah foto bukti fisik fasilitas setelah selesai diperbaiki sebelum menutup tiket (*Close Ticket*).

### Kriteria Aplikasi Dinyatakan Berhasil
* Setiap tiket yang diajukan memiliki nomor identifikasi unik (*tracking ID*) dan riwayat perubahan status dari masuk hingga ditutup.
* Laporan tidak dapat diselesaikan oleh admin tanpa mengunggah minimal satu foto dokumentasi bukti perbaikan.

---

## Sistem Booking & Tracking Antrean Bengkel Kendaraan Roda Dua

### Deskripsi Masalah
Pemilik sepeda motor sering menghabiskan waktu menunggu lama di bengkel tanpa kepastian giliran servis rutin atau ganti oli. Di sisi bengkel independen:
* Antrean fisik yang menumpuk di area parkir sering memicu komplain pelanggan.
* Mekanik kewalahan mengalokasikan unit kerja.
* Riwayat perawatan motor pelanggan lama tidak tercatat dengan rapi.

### Profil Target Pengguna
* **Pemilik Kendaraan:** Pengendara motor yang membutuhkan servis tanpa harus menunggu berjam-jam di lokasi.
* **Service Advisor / Pemilik Bengkel:** Pengatur antrean masuk, penugasan mekanik, dan pencatat estimasi pengerjaan.

### Manfaat Aplikasi
* Menghilangkan waktu tunggu jenuh pelanggan di ruang tunggu fisik.
* Memberikan transparansi tahapan servis dan riwayat perawatan berkala kendaraan.

### Daftar Fitur Inti (MVP)
1. **Reservasi Slot Jam Servis:** Pelanggan memilih tanggal, slot jam kedatangan, dan jenis layanan (servis ringan, ganti oli, atau servis besar).
2. **Live Antrean & Status Pengerjaan:** Pemantauan status unit secara *real-time* (Menunggu Panggilan, Dikerjakan, Selesai, Siap Diambil).
3. **Papan Kerja Mekanik (Dashboard Admin):** Penugasan mekanik per unit motor yang sedang berada di pit.
4. **Buku Servis Digital (Service Log):** Riwayat tanggal pengerjaan, kilometer terakhir, dan catatan suku cadang yang diganti.

### Kriteria Aplikasi Dinyatakan Berhasil
* Pelanggan dapat memantau perpindahan status motor mereka tanpa perlu mendatangi meja kasir atau mekanik.
* Sistem membatasi jumlah reservasi maksimal sesuai kapasitas pit servis per jam agar tidak terjadi penumpukan unit.