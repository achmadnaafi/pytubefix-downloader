# pytubefix-downloader

**Deskripsi singkat:** Skrip Notebook Python (`.ipynb`) sederhana untuk mengunduh video/audio YouTube menggunakan `pytubefix` dan (opsional) menggabungkan stream video adaptif dengan audio menggunakan `ffmpeg`.

---

## Tentang Pembuat

Skrip Notebook Python ini dibuat oleh **Achmad Nurnaafi** sebagai proyek pribadi dan open-source untuk berbagi dengan siapa pun yang membutuhkan alat sederhana untuk belajar dan eksperimen.

> ⚠️ **Disclaimer penggunaan:** Skrip ini hanya untuk tujuan **pendidikan dan penggunaan pribadi**. **Dilarang keras memperjualbelikan**, mendistribusikan ulang, atau menggunakan kode ini untuk **kepentingan komersial** maupun kegiatan yang **melanggar hukum**. Proyek ini **gratis** dan dimaksudkan untuk berbagi ilmu.

> **Penting — Disclaimer legal tambahan:** Mengunduh video/audio berhak cipta tanpa izin pemilik konten **dapat melanggar hukum** dan/atau Ketentuan Layanan YouTube. Gunakan hanya untuk materi yang Anda miliki haknya, konten lisensi bebas, atau untuk tujuan pendidikan/penelitian di mana hal tersebut diizinkan oleh hukum setempat. Penulis tidak bertanggung jawab atas penyalahgunaan kode ini.

---

## Ringkasan

Skrip ini membantu mengunduh stream MP4 dari YouTube (menggunakan pustaka `pytubefix`). Jika Anda memilih stream video adaptif (video tanpa audio), notebook akan mendownload audio terbaik terpisah lalu *menggabungkan* video + audio menggunakan `ffmpeg` untuk menghasilkan file final.

---

## Fitur

* Pilihan stream berdasarkan resolusi / audio bitrate
* Mendukung stream **progressive** (video+audio) dan **adaptive** (video tanpa audio)
* Ketika stream adaptive dipilih, notebook otomatis mengunduh audio terbaik dan menggabungkannya ke video menggunakan `ffmpeg`.

---

## Persiapan (environment)

1. Pastikan Anda menjalankan Python 3.8+ dengan Jupyter Notebook atau JupyterLab.
2. Buat virtual environment (opsional tetapi direkomendasikan):

   ```bash
   python -m venv venv
   source venv/bin/activate   # macOS / Linux
   .\venv\Scripts\activate  # Windows
   ```
3. Install dependensi (contoh `requirements.txt` minimal):

   ```text
   pytubefix
   ```

   Lalu:

   ```bash
   pip install -r requirements.txt
   ```
4. Buka file notebook:

   ```bash
   jupyter notebook pytubefix-downloader.ipynb
   ```

---

## Cara pakai

1. Jalankan notebook sel per sel di Jupyter.
2. Masukkan URL YouTube ketika diminta di cell input.
3. Pilih nomor stream dari daftar yang tampil.
4. Masukkan nama file output (tanpa ekstensi).

Jika Anda memilih stream yang **adaptive** (video tanpa audio), notebook akan:

* Mengunduh file video (tanpa audio) dan file audio terpisah,
* Menggabungkannya menggunakan `ffmpeg` menjadi `<nama>_final.mp4`.

---

## Menginstall & Mengatur `ffmpeg`

Notebook menggunakan `ffmpeg` untuk menggabungkan stream video dan audio. Ada dua cara mengatur `ffmpeg` supaya berjalan lancar:

### Opsi A — Pasang `ffmpeg` dan tambahkan ke `PATH` (direkomendasikan)

1. Download build `ffmpeg` untuk sistem operasi Anda (mis. dari [https://www.gyan.dev/ffmpeg/builds/](https://www.gyan.dev/ffmpeg/builds/) untuk Windows atau paket manajer untuk macOS/Linux).
2. Ekstrak dan letakkan folder bin `ffmpeg` di lokasi yang aman.
3. Tambahkan folder yang berisi `ffmpeg.exe` (Windows) atau `ffmpeg` (macOS/Linux) ke environment variable `PATH`.
4. Setelah itu Anda cukup memanggil `ffmpeg` tanpa path absolut di kode. Contoh `cmd` pada kode menjadi: `"ffmpeg"` atau hanya `ffmpeg`.

### Opsi B — Gunakan path absolut (sesuaikan di kode)

Jika Anda tidak ingin atau tidak bisa menambahkan `ffmpeg` ke PATH, ubah baris `cmd` pada kode menjadi path lengkap ke `ffmpeg.exe` di komputer Anda. Contoh (Windows):

```python
cmd = [
    r"C:\\Users\\achma\\AppData\\Local\\Programs\\ffmpeg\\bin\\ffmpeg.exe",
    "-y",
    "-i", video_path,
    "-i", audio_path,
    "-c:v", "copy",
    "-c:a", "aac",
    output_name
]
```

> **Catatan:** Gunakan raw string (`r"..."`) atau escape backslash (`\\`) saat menuliskan path Windows agar karakter backslash tidak diinterpretasikan sebagai escape sequence di Python.

---

## Contoh konfigurasi yang aman

* Jangan commit file besar (seperti hasil unduhan) ke repository publik.
* Tambahkan file/output yang dihasilkan ke `.gitignore`:

  ```gitignore
  *.mp4
  *_audio.m4a
  *_final.mp4
  venv/
  __pycache__/
  ```

---

## Perhatian etika & hukum

* Mengunduh konten yang dilindungi hak cipta tanpa izin pemegang hak biasanya melanggar hukum hak cipta dan/atau Term of Service platform.
* Pastikan Anda memahami lisensi konten sebelum menyimpan atau mendistribusikannya.
* Bila notebook ini disalahgunakan, penulis/kontributor repository tidak bertanggung jawab.

---

## Kontribusi

Jika Anda ingin menambahkan fitur (mis. integrasi GUI, better error handling, progress bar `ffmpeg`, dukungan format lain), buka issue atau pull request. Harap sertakan deskripsi yang jelas tentang tujuan perubahan.

---

## Catatan tambahan & troubleshooting

* Jika `subprocess.run` mengembalikan error saat memanggil `ffmpeg`, cek:

  * Apakah path `ffmpeg` benar?
  * Apakah `ffmpeg` dapat dijalankan dari terminal/command prompt?
  * Pastikan Anda punya izin untuk membaca file input dan menulis file output di direktori kerja.
* Jika audio dan video tidak cocok (sinkronisasi), pertimbangkan untuk mere-encode audio atau video alih-alih `-c:v copy`.

---

* ✍️ **Dibuat oleh:** Achmad Nurnaafi
* 📜 **Lisensi:** Gratis untuk digunakan, bukan untuk diperjualbelikan.
* 🙏 Mohon digunakan dengan bijak dan tidak untuk pelanggaran hak cipta.
* 📩 **Hubungi:** [📸 @achmad.naafi_](https://instagram.com/achmad.naafi_) jika ingin bertanya lebih lanjut atau memberikan masukan.
