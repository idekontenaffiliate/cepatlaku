# Motor Market — Sistem Catat Jual-Beli Motor Bekas

Aplikasi web (Google Sheets + Apps Script) untuk mencatat motor yang dibeli dari penjual,
menyimpan data penjual (banyak no. WA & alamat), spesifikasi motor, status surat/pajak,
checklist verifikasi, foto, lalu membagikan link khusus ke pembeli — **tanpa menampilkan
info penjual atau motor lain**.

## Isi paket ini
- `Code.gs` — backend Apps Script (data, login, upload foto, dst).
- `Index.html` — tampilan web (admin & halaman untuk pembeli).

## Cara pasang (5–10 menit)
1. Buka https://sheets.google.com → buat Spreadsheet baru (kosong).
2. Menu **Extensions > Apps Script**.
3. Di editor Apps Script: hapus semua isi file `Code.gs` bawaan, tempel isi `Code.gs` dari paket ini.
4. Klik **File > New > HTML**, beri nama persis `Index` (tanpa `.html`), tempel isi `Index.html` dari paket ini.
5. Di dropdown fungsi (atas), pilih `setupSheets`, klik **Run**. Izinkan semua permintaan akses Google.
   - Ini otomatis membuat sheet: Users, Sessions, Sellers, Motors, LinkViews.
6. Klik **Deploy > New deployment**.
   - Type: **Web app**
   - Execute as: **Me**
   - Who has access: **Anyone**
   - Klik Deploy, salin URL yang muncul.

## Fitur utama
- **Login multi-admin** — bisa tambah admin lain lewat tab "Pengguna".
- **Data penjual** — nama, no. WA, alamat, catatan (banyak penjual, bisa dicari).
- **Data motor** — jenis, merek, tahun, kondisi mesin & eksterior, pemakaian (km), tipe
  bersih/tidak, harga beli, target jual, harga jual aktual (untuk hitung untung), sumber
  didapat dari mana, dan penjualnya.
- **Saran harga jual otomatis** +10% dan +20% dari harga beli, muncul begitu harga beli diisi.
- **Status Surat/Pajak** — Lengkap-Pajak Hidup / Lengkap-Pajak Mati / Tidak Lengkap.
- **Foto STNK / screenshot cek pajak** (mis. dari e-Samsat) — upload terpisah dari foto motor,
  dan **sengaja tidak pernah dikirim ke link pembeli** karena biasanya memuat nama & alamat
  pemilik asli di STNK/BPKB.
- **Checklist verifikasi** (STNK ada, BPKB ada, pajak hidup, no. rangka & mesin sesuai, fisik
  sudah dicek, foto lengkap) — kotak centang besar, gampang ditekan pakai jempol di HP. Progress
  ("5 dari 7 item sudah dicentang") langsung kelihatan.
- **Foto motor** — upload banyak, otomatis tersimpan ke folder Google Drive `MotorMarket_Photos`.
- **Link khusus untuk pembeli** — tombol "Bagikan ke Pembeli" di tiap motor menghasilkan link
  yang hanya menampilkan: foto motor, harga, tahun, status surat, dan checklist verifikasi (✓/○)
  — TANPA menampilkan penjual, harga beli, motor lain, atau foto STNK. Setiap link dibuka,
  tercatat di tab "Riwayat" (bisa lihat siapa & kapan).
- **Laporan untung** — rekap semua motor yang sudah terjual: total unit, total untung, rata-rata
  margin, per unit.
- **Pencarian & filter** — cari jenis/merek/tahun/sumber/status surat, filter status
  tersedia/terjual, tipe bersih/tidak, dan status surat.

## Alur kerja yang disarankan
1. Dapat info motor dari penjual (mis. Beat 2010-an ~Rp4.000.000) → catat penjual & motornya.
2. Cek tahun motor + screenshot bukti pajak (e-Samsat) → upload di "Foto STNK/Screenshot Pajak".
3. Centang checklist yang sudah terverifikasi.
4. Isi harga beli → lihat saran jual +10%/+20% → isi target jual.
5. Setelah yakin, klik "Bagikan ke Pembeli" → kirim link itu ke calon pembeli. Pembeli tinggal
   cek fisik motornya langsung — sisanya (tahun, status surat, checklist) sudah kelihatan di link.
6. Kalau sudah laku, edit motor → isi "Harga Jual Aktual" & ubah status ke "Terjual" → otomatis
   masuk ke Laporan Untung.

## Catatan
- Sesi login "bergulir" — selama dibuka minimal sekali tiap ~180 hari, tidak perlu login ulang.
- Semua data tersimpan di Google Sheets Anda sendiri (bukan server pihak ketiga), foto di Google
  Drive Anda sendiri.
