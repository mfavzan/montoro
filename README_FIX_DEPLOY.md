# Perbaikan deployment Vercel

Perbaikan ini menghapus konfigurasi `runtime: nodejs20.x` dari `vercel.json`. Runtime Node.js untuk file JavaScript di folder `/api` sudah dideteksi otomatis oleh Vercel; runtime seperti `nodejs20.x` tidak perlu dicantumkan sebagai community runtime.

`package.json` menambahkan `"type": "module"` agar `export default` di file API dikenali sebagai ES modules.

Langkah:
1. Ekstrak ZIP ini.
2. Upload/replace seluruh isi folder `montoro/` ke root repository GitHub `mfavzan/montoro` (bukan membuat folder montoro bersarang di dalam repository).
3. Pastikan `index.html`, `package.json`, `vercel.json`, dan folder `api/` ada di root repository.
4. Commit ke branch `main` dan tunggu deployment Vercel.
5. Pertahankan Environment Variables `ZOOM_ACCOUNT_ID`, `ZOOM_CLIENT_ID`, `ZOOM_CLIENT_SECRET` di Vercel. Jangan masukkan secret ke GitHub.
6. Uji `https://montoro.vercel.app/api/zoom/health`.
