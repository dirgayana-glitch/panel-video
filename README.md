# Video Panel + Iklan di Tengah Video (Blogger)

Alurnya: link video yang kamu sebar → halaman player di blog kamu → video diputar →
setelah beberapa detik, **atau** saat penonton mempercepat / loncat ke depan, video berhenti dan
muncul **iklan Adsterra** dengan tombol "Lewati iklan" (aktif setelah 5 detik) → video lanjut.

## Isi folder

| File | Fungsi |
|---|---|
| `panel.html` | Panel untuk menambah video dan membuat link. Dibuka di komputer kamu, tidak perlu hosting. |
| `halaman-player.html` | Kode halaman player. Dipasang **sekali** di Blogger sebagai Halaman. |

## Pasang (sekali saja)

1. Di Adsterra, buat unit **Banner 300x250** (dan opsional **Smartlink**) untuk domain blogmu.
2. Blogger → **Halaman → Halaman baru**. Beri judul misalnya `Nonton`.
3. Pindah ke **Tampilan HTML** (ikon `< >`), lalu tempel seluruh isi `halaman-player.html`.
4. Di dalam `<textarea id="vp-ad-code" ...>` tempel **kode Banner Adsterra** apa adanya, lengkap dengan dua `<script>`-nya.
5. Opsional: atur bagian **KONFIGURASI**:
   - `iklanSetelahDetik`: iklan muncul di detik ke berapa (default 10).
   - `iklanSaatDipercepat`: iklan muncul saat penonton loncat atau mempercepat video (default aktif).
   - `bolehLewatiSetelah`: tombol Lewati aktif setelah berapa detik (default 5).
   - `maksIklanPerVideo`: maksimal iklan per tontonan (default 2).
   - `smartlinkUrl`: kalau diisi, muncul link "Kunjungi Sponsor" di bawah banner.
6. **Publikasikan**, lalu salin alamat halamannya, misalnya `https://namablog.blogspot.com/p/nonton.html`.

## Menambah video

1. Buka `panel.html`, isi **URL halaman player** dari langkah 6.
2. Isi judul dan **URL file video langsung** (`.mp4` / `.webm`). Klik **▶ Coba putar URL** untuk memastikan videonya bisa diputar.
3. Klik **Simpan**, lalu **📋 Copy link**. Link itulah yang kamu sebar.

Data panel tersimpan di browser. Rajin-rajin **Export JSON** untuk backup.

## Login panel

Panel dikunci dengan username dan password. Di dalam kode hanya tersimpan **hash** password
(PBKDF2-SHA256 + salt), bukan password aslinya.

**Ganti username atau password:**
1. Buka `ganti-password.html` di situs GitHub Pages, isi username dan password baru, lalu klik **Buat kode**.
2. Salin hasilnya, lalu ganti blok `var AUTH = { ... };` di `panel.html`.
3. Commit dan push.

**Batasan:** situs ini statis (tanpa server), jadi kunci ini adalah gerbang di sisi browser.
Kunci ini cukup untuk menghalangi pengunjung biasa. Tapi orang yang paham teknis tetap bisa membaca source halaman,
dan password yang lemah bisa ditebak dari hash-nya. Gunakan password yang panjang.
Kalau butuh login yang benar-benar aman, pindahkan situs ke Cloudflare Pages dan pasang **Cloudflare Access** (gratis).
Dengan itu, login dicek di server sebelum halaman dikirim.

## Hal penting supaya aman

- **Video harus milikmu atau kamu punya hak menyebarkannya.** Film atau video bajakan bisa membuat blog dihapus karena DMCA, dan akun Adsterra ikut kena.
- **YouTube tidak bisa dipakai.** Aturan YouTube melarang iklan ditaruh di atas player mereka. Gunakan hosting video sendiri, misalnya Bunny Stream, Cloudflare R2, atau Backblaze B2. Google Drive dan Dropbox biasanya tidak stabil untuk streaming.
- Judul dan thumbnail harus sesuai isi video. Judul atau thumbnail menipu (clickbait palsu) termasuk pelanggaran yang paling sering bikin akun Adsterra diblokir.
- Jangan naikkan `maksIklanPerVideo` terlalu tinggi atau `bolehLewatiSetelah` terlalu lama. Kalau penonton kesal dan langsung kabur, kualitas traffic-mu turun di mata Adsterra.
