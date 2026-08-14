# AI4CampusDeck — UKWMS Enrollment Strategy

A business proposal presentation deck untuk mempercepat enrollment perguruan tinggi
(pertama kali dibuat untuk **Universitas Kristen Widya Mandala Surabaya / UKWMS**),
menampilkan strategi transformasi kampus menjadi ekosistem futuristik berbasis AI & FinTech.

> Nama kampus di deck **generik & bisa diganti** — cocok dipakai ulang untuk kampus
> mana pun. Lihat [Kustomisasi Nama Kampus](#kustomisasi-nama-kampus).

## Demo / Live

Deck sudah live di GitHub Pages:

```
https://solusi-ai.github.io/NeoCampus/
```

> Repo berada di bawah organisasi **SOLUSI-AI**, jadi URL memakai domain org
> (`solusi-ai.github.io`), bukan domain username.
>
> Default menampilkan nama generik (`NAMA KAMPUS`). Ganti via URL atau config —
> lihat [Kustomisasi Nama Kampus](#kustomisasi-nama-kampus).

## Kustomisasi Nama Kampus

Nama kampus **tidak di-hardcode**. Di dalam HTML memakai token `{{KAMPUS}}`
(nama singkat) dan `{{KAMPUS_FULL}}` (nama lengkap), yang diganti otomatis oleh
blok `KONFIGURASI KAMPUS` di bagian `<script>`.

### Cara 1 — Via URL (tanpa edit file)

```text
https://solusi-ai.github.io/NeoCampus/?campus=UNAIR&campusFull=Universitas%20Airlangga
```

- `campus` → nama singkat (default: `NAMA KAMPUS`)
- `campusFull` → nama lengkap (default: `Nama Universitas Anda`)

### Cara 2 — Edit konfigurasi di `index.html`

Cari blok `KONFIGURASI KAMPUS` di bagian `<script>`:

```js
const BRAND = {
  short: 'NAMA KAMPUS',
  full: 'Nama Universitas Anda',
};
```

Ubah kedua nilai, commit & push — GitHub Pages otomatis rebuild.

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
| `260604_UKWMS_EnrollmentDeck_v01.slides.html` | Versi slides v01 |

## Cara Deploy ke GitHub Pages

### Opsi A — Cepat (gh CLI)

Prasyarat: sudah login `gh auth login` dan punya akses admin ke repo.

```bash
# 1. Push repo (jika repo baru)
git init
git add .
git commit -m "feat: UKWMS enrollment strategy deck"
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

1. **Buat repo baru di GitHub** (contoh: `ukwms-enrollment-deck`), jangan centang "Initialize with README".
2. Push file dari folder ini:
   ```bash
   git init
   git add .
   git commit -m "feat: UKWMS enrollment strategy deck"
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
