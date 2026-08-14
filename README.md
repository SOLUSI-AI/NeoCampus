# AI4CampusDeck — Strategi Percepatan Enrollment Kampus

Presentation deck untuk mempercepat enrollment perguruan tinggi (fokus: **PTS**
yang terdampak penurunan pendaftar), menampilkan strategi transformasi kampus
menjadi ekosistem futuristik berbasis AI & FinTech.

Deck ini **generik & reusable** — nama kampus, % penurunan, dan angka pendaftar
bisa diubah sesuai prospek tanpa menyentuh kode (via menu ⚙ di deck atau URL).
Awalnya dibuat untuk **Universitas Kristen Widya Mandala Surabaya (UKWMS)**.

Lihat [Kustomisasi Nama Kampus](#kustomisasi-nama-kampus).

## Demo / Live

Deck sudah live di GitHub Pages:

```
https://solusi-ai.github.io/NeoCampus/
```

> Repo berada di bawah organisasi **SOLUSI-AI**, jadi URL memakai domain org
> (`solusi-ai.github.io`), bukan domain username.
>
> Default menampilkan `Kampus Nusantara` (generik). Tim marketing bisa mengubah
> nama kampus sesuai prospek via menu ⚙ di deck atau URL — lihat
> [Kustomisasi Nama Kampus](#kustomisasi-nama-kampus).

## Fitur

- **15 slide interaktif** — navigasi tombol, keyboard (←/→/spasi), swipe, dan dot
- **8 program lengkap** dengan modal *deep-dive* per program
- **Menu ⚙ “Pengaturan Kampus”** — isi nama kampus & angka kunci, tersimpan di
  browser, plus **Salin Link Kustom** siap kirim ke prospek
- **Override via URL** — `?campus=...` tanpa edit file
- **Zero build** — HTML statis, langsung jalan di GitHub Pages

## Kustomisasi Nama Kampus

Nama kampus & angka kunci deck **tidak di-hardcode** — bisa diubah sesuai
prospek oleh tim marketing. Default: `Kampus Nusantara` (generik).

### Cara 1 — Menu ⚙ di dalam deck (paling mudah, untuk tim marketing)

Klik tombol **⚙** di navigasi bawah, lalu isi:

- **Nama kampus** (singkat & lengkap)
- **Angka kunci**: penurunan pendaftar (%), rata-rata pendaftar/th (lalu),
  pendaftar/th (kini)

Klik **Simpan & Terapkan** — tersimpan otomatis di browser (localStorage).
Tombol **Salin Link Kustom** membuat URL dengan nama kampus terisi, siap
langsung dikirim ke prospek. **Reset** mengembalikan ke default Kampus Nusantara.

### Cara 2 — Via URL (tanpa edit file)

```text
https://solusi-ai.github.io/NeoCampus/?campus=UKSW&campusFull=Universitas%20Kristen%20Satya%20Wacana&penurunan=25%25&pendaftarSebelum=1200&pendaftarTerakhir=900
```

- `campus` → nama singkat (default: `Kampus Nusantara`)
- `campusFull` → nama lengkap
- `penurunan` → persen penurunan (default: `30%`)
- `pendaftarSebelum` → rata-rata pendaftar/th sebelumnya (default: `1000`)
- `pendaftarTerakhir` → pendaftar/th dua tahun terakhir (default: `700`)

### Cara 3 — Edit default di `index.html`

Cari blok `BRAND_DEFAULT` di bagian `<script>`:

```js
const BRAND_DEFAULT = {
  short: 'Kampus Nusantara',
  full: 'Kampus Nusantara',
  penurunan: '30%',
  pendaftarSebelum: '1000',
  pendaftarTerakhir: '700',
};
```

Ubah nilainya, commit & push — GitHub Pages otomatis rebuild.

## Three Pillars

1. **Early-Engagement Funnel** — Innovator Sandbox and Bridging Program (RPL) to secure student commitment since high school.
2. **Inclusive & Ethical Value** — Women & Youth Financial Inclusivity Hub and Invezthink FinLit Track to provide real-world value from semester one.
3. **Sustainable Career Integration** — AI-Driven Campus Micro-Agency and Corporate-Bonded Scholarships for clear career pathways.

## Eight Programs

| # | Program |
|---|---------|
| 1 | Innovator Sandbox & PoW |
| 2 | Hybrid Nano-Degree SMA |
| 3 | Invezthink FinLit Track |
| 4 | Campus Micro-Agency |
| 5 | Corporate-Bonded Track |
| 6 | Women & Youth Hub |
| 7 | Student Ambassador |
| 8 | Green Ledger Campus |

## Files

| File | Keterangan |
|------|------------|
| `index.html` | Deck utama dengan navigasi slide (landing page) |
| `260604_UKWMS_EnrollmentDeck_v01.slides.html` | Arsip versi v01 (masih ber-brand UKWMS, tidak di-link dari deck utama) |

## Cara Deploy ke GitHub Pages

### Opsi A — Cepat (gh CLI)

Prasyarat: sudah login `gh auth login` dan punya akses admin ke repo.

```bash
# 1. Push repo (jika repo baru)
git init
git add .
git commit -m "feat: enrollment strategy deck"
git branch -M main
git remote add origin https://github.com/SOLUSI-AI/NeoCampus.git
git push -u origin main

# 2. Aktifkan GitHub Pages dari branch main / root
gh api -X POST "repos/SOLUSI-AI/NeoCampus/pages" \
  -f "source[branch]=main" -f "source[path]=/"

# 3. Cek status build (built = siap)
gh api repos/SOLUSI-AI/NeoCampus/pages --jq .status

# 4. Deck live di:
#    https://solusi-ai.github.io/NeoCampus/
```

> Ganti `SOLUSI-AI/NeoCampus` dengan `owner/repo` milikmu. Jika repo ada di
> akun pribadi, URL live jadi `https://<username>.github.io/<nama-repo>/`.

### Opsi B — Manual (UI GitHub)

1. **Buat repo baru di GitHub** (contoh: `enrollment-deck`), jangan centang "Initialize with README".
2. Push file dari folder ini:
   ```bash
   git init
   git add .
   git commit -m "feat: enrollment strategy deck"
   git branch -M main
   git remote add origin https://github.com/<username>/<nama-repo>.git
   git push -u origin main
   ```
3. Di GitHub: **Settings → Pages → Source → Deploy from a branch → `main` → `/ (root)`** → Save.
4. Tunggu 1–2 menit, deck live di `https://<username>.github.io/<nama-repo>/`.

## Tech Stack

- **Presentation**: HTML + Tailwind CSS v4 (CDN) + Google Fonts
- **Hosting**: GitHub Pages (static HTML, tanpa build step)
- **Build**: None — static HTML, open `index.html` in any browser

## License

See [LICENSE](LICENSE).
