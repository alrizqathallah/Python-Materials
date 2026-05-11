# Fase 1: Pemula - Fundamental Python

## Materi 1.1 Pengenalan Python

### A. Python Intro - Sejarah, Filosofi dan Keunggulan Python

**1. Fokus Pembelajanan**
Memahami asal-usul Python, filosofi desain yang mendasarinya (The Zen of Python) dan alasan strategis mengapa bahasa ini sangat dominan di industri *Software Engineering*, khususnya untuk infrastruktur *backend* dan otomatisasi sistem.

**2. Penjelasan Materi**
  - **Sejarah Singkat**: Diciptakan oleh Guido Van Rossum dan dirilis pada tahun 1991. Nama "Python" tidak diambil dari jenis ular, melainkan dari grup komedi televisi inggris favorit Guido. *Monty Python's Flying Cicrcus*.
  - **Filosofi Inti**: Pendahulu Python sering kali didesain untuk memudahkan kerja mesin komputer. Python mendobrak ini dengan filosofi yang berpusat pada manusia (*Developer Centric*). Prinsip utamanya adalah "**Readability Counts**" (Keterbacaan itu penting). Python memaksa penulisan yang rapi melalui sisten indentasi (menjorok) dan membuang penggunaan simbol rumit seperti kurung kurawal `{}` atau titik koma `:`.
  - **Keunggulan Industri**:
    - *Ekspresif*: Kode lebih singkat untuk mengeksekusi logika yang sama dibandingkan bahasa lain (seprti Java atau C++).
    - *Ekosistem Raksasa*: Memiliki pustaka (*library*) siap pakai untuk segala kebutuhan, mulai dari pembuatan API (FastAPI, Django) hingga kecerdasan buatan.
    - **Cross-Platform**: Kode berjalan identik di Windows, macOS, maupun distribusi Linux.

**3. Study Kasus dan Penerapa Nyata**
Bayangkan kita sedang merancang arsitektur sistem berskala *Enterprise*, seperti sistem manajemen berbasis data terpadu untuk sebuah sekolah (mencakup relasi entitas siswa, staf dan tahun ajaran akademik). Jika dibangun menggunakan bahasa tingkat rendah, *Engineer* akan menghabiskan puluhan jam hanya untuk mengatur alokasi memori di *server*. Dengan menggunakan Python, urusan memori dan *Garbage Collection* ditangani secara otomatis di belakang layar. Hal ini memungkinkan *Engineer* memfokuskan 100% waktunya pada perancangan Entity Relationship Diagram (ERD), efisiensi *query*, dan perumusan logika bisnis.

**4. Common MIstakes (Kesalahan Umum)**
- **Menganggap Python tidak cocok untuk skala besar**: Banyak pemula mengira Python terlalu lambat. Faktanya, perusahaan seperti Instagram dan Spotify menggunakan Python sebagai tulang punggung *backend* mereka dengan mengkombinasikannya bersama arsitektur *microservices* dan basis data berkinerja tinggi.
- **Menulis Python dengan gaya bahasa lain**: Programmer yang terbiasa dengan bahasa lain sering menulis kode Python tanpa memanfaatkan sintaks bawaannya yang elegan, sehingga kode menjadi panjang dan sulit dirawat.

**5. Best Practices (Praktik Terbaik)**
- **Internalisasi The Zen of Python**: Selalu utamakan kode yang sederhana (*Simple is better than complex*) dan eksplisit (*Explicit is better than implicit*).
- **Tulis Kode untuk dibaca manusia**: Kode dibaca 10 kali lebih sering daripada ditulis. Prioritaskan kebersihan struktur di atas trik kode yang terlalu rumit.

**6. Latihan Materi**
Mari kita lakukan inspeksi langsung ke dalam mesin Python untuk memanggil pedoman filosofis yang disembunyikan oleh para penciptanya.
  1. Buka terminal.
  2. Ketik perintah `python3` (atau `python`) lalu tekan Enter untuk masuk ke mode interaktif.
  3. Ketik perintah ini: `import this` lalu tekan Enter.
  4. Baca puisi teknis yang muncul, lalu ketik `exit()` untuk keluar

```Terminal
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
```

**7. Kesimpulan Materi**
Python bukanlah sekedar alat untuk mengetik instruksi ke komputer, melainkan bahasa yang dirancang khusu untuk memaksimalkan produktivitas *Software Engineer*. Dengan mengutamakan keterbacaan dan kesederhanaan, Python memastikan tim *developer* dapat membangun, membaca, dan memelihara sistem yang kompleks dengan tingkat efisiensi tinggi.

### B. Python Get Started - Instalasi Python & Editor (VS Code / PyCharm)

**1. Fokus Pembelajaran**
Memastikan lingkungan kerja (*Environment*) terpasang dengan benar. Ini mencakup instalasi mesin penerjemah (Interpreter Python), pemahaman tentang *Environment Variable* (PATH), dan konfigurasi *Code Editor* standar industri agar alur kerja penulisan kode menjadi efisien.

**2. Penjelasan Materi**
- **Instalasi Interpreter Python**: Komputer secara bawaan tidak mengerti bahasa Python. Kita harus menginstal CPython (penerjemah resmi).
  - Di Windows: Diunduh dari `python.org`.
  - Di Linux / WSL 2 (Ubuntu): Diinstal melalui terminal dengan perintah `sudo apt install python3 python3-pip`.
- **Konsep PATH (Penting)**: PATH adalah peta jalan bagi sistem operasi. Saat kita mengetik `python` di terminal, OS harus tahu di *folder* mana program Python itu berada. Di Windows, ini dilakukan dengan mencentang kotak "**Add Python to PATH**" saat instalasi awal.
- **Code Editor (VS Code vs PyCharm)**:
  - *Visual Studio Code (VS Code)*: Sangat ringan, modular dan menjadi favorit *Engineer* modern. Ia membutuhkan tambahan *Extensions* (Ekstensi resmi Microsoft: "Python" dan "Pylance") agar bisa memahami kode Python.
  - *PyCharm*: Sebuah IDE (*Intergrated Development Environment*) lengkap dari JetBrains. Fiturnya sangat canggih dan langsung siap pakai tanpa perlu instalasi tambahan, namun memakan lebih banyak memori (RAM).

**3. Study Kasus dan Penerapan**
Penerapan *Environment* yang tepat sangat krusial saat menangani proyek berskala nyata. Bayangkan saat kita merancang arsitektur sistem berskala *Enterprise*, seperti *database* menajemen sekolah SMA HAJARA JAKARTA. Kita akan membutuhkan *Code Editor* yang fleksibel. Dengan menggunakna VS Code yang terhubung ke lingkungan WSL2 (Ubuntu), kita bisa menulis koode desain *Entitiy Relationship Diagram* (ERD) di antarmuka grafis yang nyaman, sementara kodenya secara *real-time* dieksekusi di dalam terminal Linux di panel bawahnya. Ini menyimulasikan kondisi *server* produksi (dunia nyata) secara akurat tanpa perlu memiliki dua komputer berbeda.

**4. Common Mistakes**
- **Lupa mencentang "Add Python to PATH"**: Ini adalah kesalahan nomor satu pemula di OS Windows, yang mengakibatkan terminal memunculkan pesan *error* `'python' is not recognized as an internal or external command`.
- **Menggunakan Ekstensi VS Code Berlebihan**: Menginstal ekstensi acak yang tidak resmi membuat VS Code menjadi lambat dan berat.
- **Menjalankan program dengan *Double-Click***: Pemula sering kali menjalankan *file* `.py` dengan mengklik ganda *file*-nya seperti membukan dokumen Word. *Engineer* sejati selalu menjalankan program melalui Terminal/CLI.

**5. Best Practices**
- **Gunakan Terminal secara Ekslusif**: Biasakan diri untuk selelu berpindah direktori (menggunakan perintah `cd`) dan mengeksekuis kode (menggunakan perintah `python3 nama_file.py`) langsung dari terminal.
- **Standar Ekstensi VS Code**: Cukup instal ekstensi **Python** dan **Pylance** dari Microsoft. Jika menggunakan WSL2, tambahkan ekstensi **WSL** untuk integrasi yang mulus.
- **Selalu cek versi**: Biasakan mengecek versi Python yang sedang aktif agar tidak terjadi konflik pustaka (*library*).

**6. Latihan Materi**
Mari kita lakukan validasi terhadap mesin Python yang sudah ada di sistem.
  1.  Buka Terminal (sangat disarankan menggunakan terminal bawaan VS Code atau terminal WSL Ubuntu).
  2.  Ketik perintah ini untuk mengecek ketersediaan dan versi Python: `python3 --version` (*Jika error, coba `python --version`)
  3.  Ketik perintah ini untuk mengecek ketersediaan PIP (Manajer Paket Python): `pip3 --version` (*Jika error, coba `pip --version`)
  
  **Jawaban:**

  ```Terminal
  python3 --verison

  pip3 --version
  ```

  ```Terminal
  Python 3.12.3

  pip 24.0 from /usr/lib/python3/dist-packages/pip (python 3.12)
  ```

**7. Kesimpulan Materi**
Lingkungan kerja yang solid adalah fondasi dari *Software Engineering*. Mesin Python bertugas sebagai penerjemah, *Code Editor* bertugas sebagai meja kerja, dan Terminal bertugas sebagai pusa komando komputernya. Ketiga komponen ini harus terhubung dengan sempurna agar proses pembuatan program dapat berajalan mulus.

### C. Python Syntax - Indentasi, Case-Sensitivity, Struktur Kode

**1. Fokus Pembelajaran**
