# Montoro - Zoom Account Monitor

Dashboard untuk mengambil data akun Zoom secara aman melalui backend Vercel + Zoom Server-to-Server OAuth.

## Struktur

- `index.html` - frontend dashboard
- `api/zoom/_zoom.js` - helper OAuth + request ke Zoom API
- `api/zoom/health.js` - tes koneksi Zoom
- `api/zoom/users.js` - daftar user Zoom
- `api/zoom/meetings.js` - jadwal meeting seluruh user aktif
- `api/zoom/usage.js` - laporan penggunaan harian
- `vercel.json` - konfigurasi Vercel

## 1. Buat aplikasi Zoom

Di Zoom App Marketplace / Developer Portal buat aplikasi **Server-to-Server OAuth**.

Tambahkan minimal scope berikut pada aplikasi:

- `user:read:admin` atau granular scope untuk list users
- `meeting:read:admin` atau granular scope untuk list meetings
- `report:read:admin` untuk daily usage report

Untuk akun yang menggunakan master-account API, scope dan endpoint berbeda. Project ini memakai endpoint akun biasa untuk S2S OAuth.

## 2. Isi Environment Variables di Vercel

Project Settings -> Environment Variables:

- `ZOOM_ACCOUNT_ID`
- `ZOOM_CLIENT_ID`
- `ZOOM_CLIENT_SECRET`

Jangan masukkan Client Secret ke `index.html`, GitHub, atau kode frontend.

## 3. Deploy

Upload/push seluruh isi folder ini ke repository GitHub. Import repository tersebut ke Vercel.

Setelah deploy, tes:

- `/api/zoom/health`
- `/api/zoom/users`
- `/api/zoom/meetings`
- `/api/zoom/usage`

## Catatan

- Data schedule berasal dari meeting terjadwal yang dikembalikan Zoom.
- Daily usage berasal dari Zoom Reports API.
- Dashboard ini belum menggunakan webhook real-time. Status kartu menunjukkan status berbasis jadwal yang berhasil diambil, bukan presence real-time.
- Daily usage Zoom hanya dapat diminta untuk bulan yang masih berada dalam periode yang diizinkan Zoom.
