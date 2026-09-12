# Splitva — split bill app (liquid glass, dark)

Aplikasi web mobile-first yang jalan langsung, gaya **liquid glass / glassmorphism** dengan nuansa **purple Japanese cyberpunk (dark mode)**. Satu file HTML, tanpa build step, tanpa backend. Logo pakai aset yang kamu kirim.

## Yang baru di versi ini

- **Bingkai HP di tengah layar** — di layar lebar (desktop/tablet), app sekarang tampil dalam bingkai ala HP yang center di tengah, bukan nempel mepet ke atas. Di HP asli (layar <500px) bingkainya otomatis hilang dan app full-screen seperti biasa.
- **Tombol "Kembali" lebih jelas** — semua topbar sekarang pakai tombol bertuliskan "Kembali" (bukan cuma ikon panah). Dari layar Review, tombol Kembali juga minta konfirmasi dulu karena itu titik di mana data struk bisa hilang kalau kepencet gak sengaja.
- **Tombol batal saat scan** — layar loading OCR sekarang ada tombol "Batal, salah foto" kalau ternyata salah pilih gambar, tanpa harus nunggu proses OCR selesai dulu.
- **Tema liquid glass gelap** — background deep indigo (`#0D0B18`/`#120E24`) dengan glow ungu (`#9D4EDD`, `#C77DFF`) di beberapa titik, kartu pakai `backdrop-filter: blur()` + border tipis transparan supaya kesan kaca beneran kerasa, teks tetap putih/off-white kontras tinggi.
- **Qty stepper per item** — di layar Review sekarang ada tombol `− angka +` di tiap item. Kalau ada menu yang sama dipesan berkali-kali (mis. Es Teh x3), tinggal naikkan angkanya, gak perlu ketik ulang barisnya. Total per baris (`harga satuan × qty`) dihitung otomatis dan itu yang dipakai untuk pembagian & ringkasan.
- **Logo asli kamu** dipasang sebagai app icon (`icon-192.png`, `icon-512.png`) dan ditampilkan di header layar Home (`logo.png`).

## Cara pakai cepat

1. Buka `index.html` di browser, atau deploy ke GitHub Pages/Netlify/Vercel supaya bisa akses kamera dari HP.
2. Di HP, buka lewat Chrome lalu **Tambahkan ke layar utama** untuk pengalaman seperti app native.

> Kamera (`capture="environment"`) dan `navigator.clipboard` cuma jalan di **HTTPS** atau `localhost`. Untuk demo penuh di HP, deploy dulu.

## Deploy ke GitHub Pages

```bash
git init
git add .
git commit -m "Splitva liquid glass"
git branch -M main
git remote add origin <url-repo-kamu>
git push -u origin main
```

Lalu di GitHub: **Settings → Pages → Deploy from branch → main → / (root)**.

## Fitur

- **Scan struk** — OCR di browser via [Tesseract.js](https://github.com/naptha/tesseract.js), gambar tidak dikirim ke server manapun.
- **Parsing otomatis** item + harga, sekaligus deteksi pola qty seperti "2x" atau "x2" di teks struk.
- **Qty stepper manual** di setiap item, jadi menu duplikat cukup naikkan angka.
- **Review & edit** semua item (nama, harga satuan, qty, hapus/tambah).
- **Assign proporsional** — tap nama lalu tap item; item yang ditandai untuk beberapa orang otomatis dibagi rata.
- **Pajak & service proporsional** sesuai porsi belanja tiap orang.
- **Status bayar** per orang + field rekening/QRIS.
- **Salin ke WhatsApp** — teks rapi termasuk info qty, langsung ke clipboard.

## Batasan yang perlu kamu tahu

- **`backdrop-filter` (efek blur kaca)** butuh browser modern — Chrome/Safari/Edge versi baru semua support, tapi kalau target device lama efeknya bisa fallback ke warna solid transparan biasa (masih kebaca, cuma gak blur).
- **OCR tetap heuristik.** Struk buram/miring bisa salah baca nama, harga, atau qty — makanya semua tetap gampang diedit manual.
- **Riwayat & sesi in-memory** (hilang saat reload), karena file ini juga dipreview di Claude yang tidak mendukung `localStorage`. Setelah deploy sendiri, ganti ke `localStorage`/`IndexedDB` — ada komentar penunjuknya di `index.html`.

## Struktur file

```
patungan-app/
├── index.html      → seluruh UI + logika app (vanilla JS, tanpa framework)
├── manifest.json    → metadata PWA
├── logo.png         → logo Splitva (dipakai di header app)
├── icon-192.png
├── icon-512.png
└── README.md
```
