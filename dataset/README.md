# Dataset untuk praktik

Hanya berkas yang dipakai oleh empat notebook disertakan. Semua CSV hasil olahan menggunakan UTF-8. Teks, label dan prediksi digabungkan melalui `id`.

| Awalan | Sumber dan isi | Penggunaan |
|---|---|---|
| `01_smsa` | SmSA/IndoNLU;12.679 teks nyata; negative,neutral,positive | Latih/validation/test sentimen umum |
| `01_pelayanan` |72 komentar layanan kepolisian sintetis | Demonstrasi perpindahan domain; bukan opini masyarakat nyata |
| `01_topic_modeling` |72 komentar yang sama, tanpa label topik/sentimen | NMF tanpa label |
| `02_hate_speech` | Ibrohim–Budi 2019;12.992 teks setelah deduplikasi dan pemisahan konflik | Label utama `label=HS`; sublabel asli tetap tersedia |
| `03_promosi_judi` | tyogoutomo;3.370 teks setelah normalisasi, masking dan deduplikasi |0nonpromosi,1promosi |
| `04_nergrit` | NERGrit/IndoNLU;2.090 kalimat nyata | Token dan tag BIO dalam array JSON; PERSON,PLACE,ORGANISATION |
| `04_aduan_sintetis` |24narasi fiktif LLM,12train/6validation/6test | Gold JSONL berisi kutipan, start dan end untuk setiap field |

## Cara membaca data

- `content` adalah teks sumber; `content_cleaned` melalui NFKC, perapian spasi dan masking URL/mention. Negasi dan tanda baca tetap ada.
- `*_final_train/val/test.csv`: data klasifikasi dibagi64/16/20 per label dengan seed42 setelah deduplikasi. NERGrit mempertahankan split sumber1.672/209/209 kalimat.
- Tidak ditemukan teks identik setelah transformasi antarsplit pada audit. Parafrasa/duplikasi semantik belum diaudit. Ini split tutorial baru, bukan benchmark resmi.
- `HS` dan `Abusive` berbeda; keduanya bisa tumpang tindih. `HS_Other` adalah kategori Other. Label riset bukan keputusan hukum.
- `tokens` dan `ner_tags` pada NERGrit dibaca dengan `json.loads`. Satu baris satu kalimat, teks disusun ulang dengan spasi antartoken.
- Gold aduan dipasangkan melalui `id`. Offset memakai indeks karakter Python, start inklusif/end eksklusif. Field kosong `[]` berarti tidak ada informasi yang memenuhi aturan. `nominal_disebut` tidak otomatis kerugian; bukti belum tersedia tidak dimasukkan ke `bukti_tersedia`.
- Semua komentar polisi dan aduan sintetis dibuat LLM pada25Oktober 2026, bukan laporan polisi atau posting masyarakat nyata. Label semantiknya belum divalidasi manusia. Data kecil dan pola generator dapat membuat skor terlalu tinggi.

## Sumber dan atribusi

1. [IndoNLU, Wilie et al.2020](https://github.com/IndoNLP/indonlu), snapshot `ce728f6926a36174b9923dfe49d6a6839b6e9bb7`. [Paper](https://aclanthology.org/2020.aacl-main.85/).
2. [Ibrohim & Budi 2019](https://github.com/okkyibrohim/id-multi-label-hate-speech-and-abusive-language-detection), snapshot `be98de98e974b65838d2b5145ee2c89e9bf53a6b`. Muhammad Okky Ibrohim and Indra Budi. Multi-label Hate Speech and Abusive Language Detection in Indonesian Twitter. ALW3,46–57. [Paper](https://aclanthology.org/W19-3506/).
3. [tyogoutomo](https://github.com/tyogoutomo/INDONESIAN_ONLINE_GAMBLING_WEBSITE_PROMOTION_DATASET), snapshot `32bb3817126d68e4cc39551cf1f35e13698b0863`. Prosedur anotasi rinci dan representasi negatif tidak didokumentasikan lengkap.

## Lisensi dan perubahan

Dataset Ibrohim–Budi memakai **CC BY-NC-SA4.0** ([ketentuan](https://creativecommons.org/licenses/by-nc-sa/4.0/)): atribusi, nonkomersial dan ShareAlike tetap berlaku untuk data olahan. Jangan menganggap izin kode MIT meliputi data ini.

Repo tyogoutomo memakai **Apache2.0**. File LICENSE aktual repo IndoNLU juga Apache2.0, tetapi card Hugging Face menyebut MIT dan loader SEACrowd SmSA menyebut CC BY-SA4.0. Ketidaksesuaian metadata tersebut belum terselesaikan; cocokkan ketentuan korpus dengan pengelola untuk redistribusi lanjutan. Salinan Apache2.0 disertakan dalam `LICENSES.md`.

Perubahan dari sumber: pembersihan ringan, masking, deduplikasi, pemisahan anotasi konflik, split klasifikasi baru, serta konversi token/tag NERGrit menjadi CSV.59 baris HS berkonflik/bermasalah dikarantina; tidak dipakai untuk latihan.3.421 baris promosi sumber menjadi3.370 setelah masking dan deduplikasi. Korpus sintetis dipisahkan dari data nyata.

## Field acuan untuk aduan sintetis

`pelapor`, `korban`, `terlapor`, `saksi`, `waktu_kejadian`, `lokasi_kejadian`, `nominal_disebut`, `bukti_tersedia`. Setiap field berupa daftar `{"text":"kutipan persis","start":0,"end":14}`; `end` tidak termasuk karakter terakhir. Peran terlapor adalah klaim narator, bukan temuan bersalah. Waktu dapat berupa rentang atau dua klaim yang belum pasti. Jangan menebak lokasi dari rute atau tanggal kejadian dari waktu penemuan. Validator kutipan hanya memeriksa struktur dan kecocokan substring; ia tidak memastikan makna peran benar.
