# Pemanfaatan Kecerdasan Buatan (KB) untuk Kelompok Ilmu Kepolisian (KIK)

Materi dan notebook untuk analisis sentimen, pemodelan topik, deteksi ujaran kebencian, deteksi promosi judi daring, dan ekstraksi informasi pengaduan.

## Materi

| Topik | Slide | Notebook |
|---|---|---|
| Peningkatan pelayanan | [Slide 01](slide/01_Pemanfaatan_AI_untuk_Peningkatan_Pelayanan.pdf) | [Sentimen dan topik](notebook/01_pelayanan_sentimen_dan_topik.ipynb) | 
| Pengamanan media sosial | [Slide 02](slide/02_Pemanfaatan_AI_untuk_Pengamanan_Media_Sosial.pdf) | [Deteksi ujaran kebencian](notebook/02_pengamanan_deteksi_ujaran_kebencian.ipynb) | 
| Deteksi tindak kriminal | [Slide 03](slide/03_Pemanfaatan_AI_untuk_Deteksi_Tindak_Kriminal_di_Media_Sosial.pdf) | [Deteksi promosi judi daring](notebook/03_deteksi_promosi_judi_online.ipynb) | 
| Penyelidikan dan penyidikan | [Slide 04](slide/04_Pemanfaatan_AI_untuk_Membantu_Penyelidikan_dan_Penyidikan.pdf) | [Ekstraksi informasi pengaduan](notebook/04_ekstraksi_informasi_pengaduan.ipynb) | 

## Isi tiap topik

### 1. Peningkatan pelayanan

**Slide:** opini masyarakat tentang layanan kepolisian, analisis sentimen, pemodelan topik, dan penggabungan keduanya untuk memahami keluhan layanan.

**Notebook:** klasifikasi sentimen dengan TF-IDF dan Logistic Regression, evaluasi melalui confusion matrix dan macro-F1, pengujian pada komentar kepolisian sintetis, serta pemodelan topik dengan NMF. Keluaran akhirnya berupa kata kunci topik dan ringkasan sentimen per topik.

### 2. Pengamanan media sosial

**Slide:** perbedaan kritik, bahasa kasar, dan ujaran kebencian; klasifikasi multilabel; tantangan bahasa; serta risiko salah menandai konten.

**Notebook:** pengenalan label HS dan Abusive, klasifikasi teks, pemilihan ambang keputusan berdasarkan data validasi, evaluasi precision/recall, analisis false positive dan false negative, serta prediksi dua label secara bersamaan.

### 3. Deteksi tindak kriminal di media sosial

**Slide:** pola promosi judi daring, perbedaan promosi dengan berita atau edukasi, ejaan tersamar, sinyal teks dan jaringan, serta verifikasi hasil deteksi.

**Notebook:** perbandingan fitur kata dan karakter untuk klasifikasi promosi judi, pemilihan model dan ambang pada data validasi, evaluasi data uji, serta pengujian tambahan pada contoh berita, edukasi, dan promosi tersamar.

### 4. Penyelidikan dan penyidikan

**Slide:** ekstraksi informasi dari narasi pengaduan, entitas dan peran orang, waktu, lokasi, nominal, bukti, kronologi, dan penelusuran isian ke teks sumber.

**Notebook:** anotasi BIO, pelatihan NER dengan CRF, evaluasi rentang entitas, serta ekstraksi aduan sintetis ke JSON menggunakan aturan. Setiap isian disertai kutipan dan posisi karakter. Tersedia contoh kesalahan peran dan rancangan prompt LLM tanpa pemanggilan API.

## Dataset

| Dataset | Jumlah | Isi |
|---|---:|---|
| SmSA | 12.679 teks | Sentimen positif, netral, dan negatif pada komentar umum |
| Komentar layanan kepolisian sintetis | 72 teks | Contoh sentimen dan topik layanan |
| Ibrohim–Budi 2019 | 12.992 teks | Ujaran kebencian, bahasa kasar, dan sublabel terkait |
| Promosi judi daring | 3.370 teks | Promosi dan nonpromosi |
| NERGrit | 2.090 kalimat | Entitas orang, tempat, dan organisasi |
| Aduan sintetis | 24 dokumen | Narasi pengaduan dengan anotasi informasi dan bukti teks |

Jumlah di atas mengikuti data setelah pembersihan. Data sintetis dipisahkan dari data nyata dan labelnya belum divalidasi manusia. [Rincian sumber, label, pembagian data, dan lisensi](dataset/README.md).

## Struktur

```text
dataset/          Data dan keterangan sumber
notebook/         Empat notebook
slide/            Empat PowerPoint
requirements.txt  Dependensi Python
```

## Pengakuan dan Penafian
Slide, kode notebook, dan README pada repositori ini dibantu digenerasi oleh ChatGPT dan Claude dengan dicek dan diedit kembali.