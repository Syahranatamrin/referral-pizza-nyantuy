# Web App Admin Referral – Pizza Nyantuy

## Isi folder
- `index.html` – aplikasi web (1 file, tanpa instalasi).
- `n8n-referral-action.json` – workflow n8n untuk aksi (catat klaim, tandai kirim, klaim free).

## 1. Buka aplikasi
- **Lokal:** klik dua kali `index.html` (butuh internet untuk Chart.js & data).
- **Hostinger:** hPanel → File Manager → upload `index.html` ke `public_html/referral/` → buka `https://domainmu.com/referral/`.
- PIN awal: **1234** (ganti di menu Pengaturan). PIN cuma pengaman ringan, bukan keamanan sungguhan — jangan sebar link-nya.

## 2. Webhook data (GET db-referral)
Sudah jalan & CORS sudah diizinkan. Jika suatu saat data gagal dimuat, di node Webhook db-referral → Options → *Allowed Origins (CORS)* isi `*` (atau domain web app), dan Respond = *All Incoming Items*.
Catatan: tiap refresh menjalankan workflow 1x, jadi pakai tombol Refresh / auto 60 detik saja.

## 3. Import workflow aksi
1. n8n → Workflows → ⋯ → **Import from File** → pilih `n8n-referral-action.json`.
2. Di 4 node Google Sheets (Ambil Rows, Update Qty Klaim, Update Status Kirim, Update Klaim Free): pilih **credential** Google, **spreadsheet** & **sheet** yang sama dengan db-referral.
3. Save → **Active**. URL-nya: `https://n8n.srv1123014.hstgr.cloud/webhook/referral-action`.
4. Di web app → Pengaturan → klik **Tes koneksi aksi** (harus muncul ✅).

## 4. Aturan reward
Default: tiap 5 klaim = 1 free, maksimal 3 free. Ubah di Pengaturan (tersimpan per browser).

## Saran
- Rapikan nomor WA di sheet ke format 62xxx dan tanggal yang seragam (app sudah menormalkan tampilannya).
- Cek WA duplikat (ditandai merah) – bisa jadi daftar 2x.
- Tambahkan kolom "Log Klaim" (tanggal, kode, catatan) agar riwayat klaim tercatat, bukan hanya jumlahnya.
- Kirim notif WA otomatis saat free jatuh tempo (kolom Notif free).
