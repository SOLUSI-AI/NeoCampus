# DESIGN — Redesign Visual Deck Enrollment (index.html)

> Dokumen desain final hasil sesi brainstorming. Dibuat sebelum implementasi
> dimulai. Status: **disetujui** — siap implementasi.

---

## 1. Ringkasan Pemahaman

1. **Yang dibangun:** upgrade visual menyeluruh pada `index.html` (deck
   enrollment statis: 15 slide + 8 modal program) — konten teks boleh disajikan
   ulang, struktur boleh dirombak, elemen baru boleh ditambah.
2. **Kenapa:** deck dirasa kurang profesional & menarik; ingin lebih estetis,
   harmonis, penuh animasi dan visual yang meyakinkan calon mahasiswa & orang tua.
3. **Untuk siapa:** dipakai ganda — presentasi live oleh tim marketing
   (projector/zoom) **dan** dibuka sendiri via link oleh prospek (Gen Z + orang
   tua) di gadget mereka.
4. **Arah visual:** polish tema dark futuristik yang ada — palet hijau/krem/emas
   dipertahankan tapi di-elevate (lebih terkontrol, tajam, premium).
5. **Visual:** hybrid — ilustrasi & mockup SVG/CSS custom sebagai fondasi + foto
   stok netral (Unsplash) untuk slide emosional (cover/penutup).
6. **Animasi:** ambient background hidup + transisi antar-slide cinematic +
   visualisasi data bergerak (count-up, timeline draw-in, ring SVG). **Tanpa**
   autoplay & micro-interaction berat.
7. **Target kinerja:** perangkat modern saja (desktop + HP terbaru); efek
   GPU-heavy dibolehkan; `prefers-reduced-motion` tetap dihormati.

## 2. Asumsi

- **Zero-build wajib dipertahankan** — HTML statis + Tailwind CSS v4 (CDN) +
  GitHub Pages; tanpa framework/build step.
- **Sistem token branding wajib tetap berfungsi** — `{{KAMPUS}}` dkk, menu ⚙,
  URL params, localStorage. Ini fitur inti tim marketing.
- **Visualisasi data adaptif terhadap angka dinamis** — animasi membaca nilai
  dari DOM setelah `applyBranding()`, bukan hardcode.
- **Konten teks kalimat tidak diubah** — yang dirombak cara penyajiannya.
- **File arsip `260604_UKWMS_EnrollmentDeck_v01.slides.html` tidak disentuh.**
- Target beban total halaman ringan (< ~2–3 MB termasuk gambar; foto lazy-load).

## 3. Decision Log

| # | Keputusan | Alternatif | Alasan |
|---|-----------|-----------|--------|
| 1 | Mode ganda (live + self-serve) | Live saja / link saja | Dipakai keduanya oleh tim marketing |
| 2 | Polish tema dark yang ada | Redesign terang / cinematic baru | Identitas tetap, risiko rendah |
| 3 | Visual hybrid: SVG/CSS + Unsplash | Semua SVG / semua foto / AI-gen | Seimbang, on-brand, emosional |
| 4 | Animasi: ambient + transisi + data-viz | +autoplay, +micro-interaction | Sesuai permintaan, aman untuk live |
| 5 | Target perangkat modern saja | Support perangkat lama | Efek GPU-heavy dibolehkan |
| 6 | Bebas restrukturisasi | Visual only | Ruang kreatif penuh |
| 7 | **Pendekatan: Opsi A — full polish in-place** | Modular rebuild / tambalan | Kohesif, satu file, incremental, risiko rendah |
| 8 | Tanpa library animasi (GSAP/Three.js/WebGL) | Pakai library | CSS + vanilla JS + SVG cukup; tetap zero-build |
| 9 | Struktur baru 16 slide (tambah agenda + CTA) | Tetap 15 slide | Navigasi live lebih jelas, penutup lebih kuat |

## 4. Desain Final

### 4.1 Design System (fondasi harmoni)

**Prinsip 60-30-10:** 60% latar gelap, 30% permukaan/teks, 10% aksen (hanya
penekanan). Maksimal 2 aksen terlihat per slide.

| Token | Nilai | Peran |
|---|---|---|
| `bg` / `bg-deep` | `#0b1220` / `#020617` | Latar berlapis |
| `surface` | `#16213a` | Kartu/panel |
| `accent-1` (hijau) | gradien `#86EFAC→#4ADE80→#16A34A` | Aksen utama, angka, CTA |
| `accent-2` (krem) | `#FDF6E3` | Sentuhan serif/penekanan halus |
| `accent-3` (emas) | `#EAB308` | Highlight jarang |
| Teks | `#F8FAFC` / `#CBD5E1` / `#94A3B8` | Primer / sekunder / redup |

**Tipografi:** Instrument Serif (judul, *italic accent* pada 1–2 kata kunci) +
Inter (body/data). Angka statistik `tabular-nums`. Jarak & lebar baris
distandarkan. **Komponen seragam:** satu resep glass panel, badge kicker,
stat tile, icon chip, tombol. Semua tetap di CSS variabel.

### 4.2 Background & Ambient Effects

Latar 4 lapis per slide: (1) base gradient radial, (2) aurora blob bergerak
lambat (12–25s, `data-ambient="green|cream|gold"` per slide), (3) grain film
halus + vignette, (4) mouse spotlight dihaluskan. Plus ±20–30 partikel cahaya
ambient melayang pelan. Semua gerak hanya `transform`+`opacity` (60fps);
`will-change` dibatasi; `prefers-reduced-motion` → latar statis bersih.

### 4.3 Transisi Antar-Slide & Navigasi

- Transisi **directional**: masuk dari arah navigasi (kiri/kanan/bawah-untuk-jump),
  durasi 600–800ms, blur→fokus. Lapisan dekoratif ber-parallax via
  `data-speed="slow|mid|fast"`.
- Reveal di-upgrade ke *blur-in* (opacity + geser 12px + blur 4px → jernih),
  stagger 60–80ms.
- Dot aktif diberi mini progress bar; modal backdrop blur + scale-in konsisten.
- Semua mekanik lama dipertahankan: keyboard ←/→/spasi, swipe, dot, blokade
  saat modal terbuka, reset scroll. Fallback fade saat reduced-motion.

### 4.4 Visualisasi Data Bergerak

1. **Stat tile + count-up** (1.2–1.8s, easeOutExpo, format id-ID, suffix `%`).
2. **Ring donut SVG draw-in** untuk penurunan % (nilai dari regex pada DOM).
3. **Timeline animated** untuk roadmap & jalur karier (node + garis draw-in).
4. **Journey stepper** 4 langkah untuk alur siswa SMA.
5. **Pillar cards upgrade**: ikon chip + garis aksen + angka pilar.

Aturan: trigger saat slide aktif; re-render saat `applyBranding()` dipanggil;
reduced-motion → nilai final langsung; teknologi SVG + `requestAnimationFrame`,
tanpa library.

### 4.5 Strategi Gambar & Ilustrasi

- **SVG/CSS custom inline:** ilustrasi ekosistem kampus (cover/penutup), ikon
  3 pilar, ikon 8 program, 2 mockup produk (dashboard micro-agency, layar HP
  finlit).
- **Foto stok Unsplash** (hanya slide emosional: cover + penutup, maks. 1–2
  lagi): subjek netral-kampus, selalu di bawah overlay gradien gelap + tint
  hijau; `loading="lazy"` + parameter CDN; fallback warna solid.
- Satu gaya konsisten untuk semua ikon/ilustrasi (stroke, radius, palet).

### 4.6 Struktur Baru (17 slide)

| # | Slide | Perubahan |
|---|---|---|
| 1 | Cover | Cinematic: foto + ikon 3 pilar + tagline |
| 2 | Agenda (BARU) | Peta deck ber-ikon |
| 3 | Konteks & masalah | Donut ring + 2 stat tile count-up |
| 4 | Insight pasar | Dua kolom + ikon |
| 5 | Visi reposisi | Layout dirapikan + ikon |
| 6 | Tiga pilar | Kartu + ikon + angka pilar |
| 7 | Pilar 1 (funnel) | Ikon per poin |
| 8 | Journey siswa SMA | Stepper 4 langkah |
| 9 | Pilar 2 | Ikon per poin |
| 10 | Dampak keluarga | Ikon per poin |
| 11 | Pilar 3 | Ikon per poin |
| 12 | Jalur karier | Timeline animated 2 track |
| 13 | Mengapa sekarang | 3 kartu argumen + ikon |
| 14 | Roadmap | Timeline Tahun 1 → Tahun 2 |
| 15 | Mandat | Ikon per poin |
| 16 | Portal 8 program | Grid + ikon + kategori + hover |
| 17 | Penutup CTA (BARU) | Foto + ajakan + tombol aksi |

**Dipertahankan:** 8 modal deep-dive (konten), modal ⚙ pengaturan kampus,
sistem token & URL branding.

## 5. Risiko & Mitigasi

| Risiko | Mitigasi |
|---|---|
| Angka animasi tidak sinkron token dinamis | Data-viz baca DOM pasca-`applyBranding()`; refresh saat branding berubah |
| Performa di HP | Animasi trigger saat slide aktif saja; transform/opacity; foto lazy-load |
| File membesar | Ikon/ilustrasi sebagai sprite SVG inline; batas total aset |
| Tailwind CDN down | Ketergantungan existing; fallback CSS variabel di `<style>` |

## 6. Non-Goals (tidak dikerjakan)

- Konversi ke framework/website (React/Vite/build step) — tetap HTML statis.
- Backend, autentikasi, analytics tambahan.
- Mengubah sistem token branding / menu ⚙.
- Menyentuh file arsip v01.
- Autoplay slide & scroll-driven storytelling.
