# ai-detector
# TeksScope — Detektor Teks AI

Tool analisis heuristik untuk mendeteksi apakah sebuah teks ditulis oleh AI atau manusia. Dibangun tanpa dependensi eksternal — semua analisis berjalan langsung di browser.

## Demo

> Buka `index.html` di browser, atau akses via GitHub Pages setelah deploy.

## Cara Kerja

TeksScope menggunakan empat heuristik berdasarkan penelitian NLP tentang perplexity dan burstiness:

| Metrik | Sinyal AI | Sinyal Manusia |
|--------|-----------|----------------|
| **Burstiness** (std dev panjang kalimat) | Rendah — kalimat seragam | Tinggi — variatif |
| **Rata-rata panjang kalimat** | >18 kata — formal & panjang | <10 kata — pendek & padat |
| **AI Phrase Fingerprint** | Banyak frasa transisi formulaik | Bersih dari frasa template |
| **Informal Markers** | Tidak ada kata gaul/singkatan | Ada ekspresi spontan |

Tidak ada model ML, tidak ada API, tidak ada server. Pure JavaScript.

## Findings

Pengujian manual terhadap beberapa model dengan pertanyaan yang sama:

| Model / Sumber | Skor Terdeteksi | Catatan |
|----------------|-----------------|---------|
| ChatGPT (behavior adjusted) | ~20% | Instruksi informal membuat burstiness naik |
| Gemini Flash | ~20% | Output pendek, kurang formulaik |
| Gemini Thinking | ~25% | Sedikit lebih terstruktur dari Flash |
| Gemini Pro | ~40% | Lebih verbose, phrase fingerprint mulai muncul |
| Ringkasan artikel oleh AI | ~40% | Kosakata kaya tapi struktur tetap AI |

**Temuan menarik:** Ringkasan artikel yang dibuat AI menunjukkan sinyal campuran — TTR tinggi dari sumber aslinya, tapi frasa transisi tetap terdeteksi.

## Struktur File

```
ai-detector/
├── index.html    ← semua konten, tool, dan logika ada di sini
└── README.md
```

## Limitasi

- Mudah di-bypass jika AI diberi instruksi menulis informal
- False positive pada manusia yang menulis dengan gaya formal
- Kamus phrase fingerprint masih terbatas (~40 frasa)
- Belum ada baseline data pelajar Indonesia

## Roadmap

- [ ] Highlight in-text — frasa mencurigakan di-highlight langsung di teks
- [ ] Kamus frasa per mata pelajaran (Biologi, Sejarah, PKn)
- [ ] Dataset jawaban asli pelajar SMA/SMK Indonesia
- [ ] Deteksi teks hybrid (ditulis manusia, dipoles AI)

## Konteks

Proyek ini dibuat sebagai portofolio dan penelitian independen. Dilatarbelakangi oleh fenomena penggunaan AI untuk menjawab soal ujian di tingkat SMA/SMK, dengan fokus pada konteks Bahasa Indonesia.

---

*Open source · dibuat untuk keperluan portofolio & penelitian*
