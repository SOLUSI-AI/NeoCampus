# AI4CampusDeck — UKWMS Enrollment Strategy

A business proposal presentation deck for **Universitas Kristen Widya Mandala Surabaya (UKWMS)**,
showcasing a comprehensive strategy to accelerate new student enrollment by transforming the campus into a futuristic ecosystem driven by AI & FinTech.

> Deck ini versi **standalone** — diekstrak dari riwayat git portfolio pribadi
> (branch `ukwms-legacy`), disiapkan untuk repo GitHub Pages sendiri.

## Demo / Live

Setelah di-push ke GitHub dan Pages diaktifkan, deck bisa diakses di:

```
https://<username>.github.io/<nama-repo>/
```

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
