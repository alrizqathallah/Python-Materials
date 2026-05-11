# BAB 1: Pondasi Fundamental & Sistem Eksekusi Python (Versi Paripurna)

## 1.1 Arsitektur Eksekusi (Bagaimana Sebenarnya Python Bekerja)

**Fokus Pembelajaran**: Memahami perbedaan *Compiler* dan *Interpreter*, CPython, dan eksekusi melalui antarmuka baris perintah (*Command Line*).

**Penjelasan Materi**:
Sebelumnya kita mengatakan Python diterjemahkan oleh *Interpreter*. Itu adalah penjelasan yang terlalu disederhanakan. Secara teknis, Python melwati dua tahap: **Kompilasi** dan **Interpretasi**.

1. **Source Code (`.py`)**: Ini adalah teks yang kita tulis di IDE/Code Editor. Komputer sama sekali tidak mengerti ini.
2. **Bytecode (`.pyc`)**: Saat kita menjalankan program, Python pertama-kali akan *mengompilasi* (menerjemahkan secara rahasia) kode kita menjadi *Bytecode*. Ini adalah instruksi tingkat rendah yang disimpan di memori (atau di dalam *folder* tersembunyi `__pycache__`).
3. **PVM (Python Virtual Machine)**: *Bytecode* ini kemudian dikirim ke PVM. Di sinilah proses interpretasi terjadi. PVM adalah mesin virtual yang menerjemahkan *bytecode* menjadi bahasa mesin (instruksi biner 0 dan 1) yang disesuaikan dengan sistem operasi (seperti subsistem Linux atau Windows) dan prosesor (CPU) kita.

Implementasi standar dari keseluruhan sistem ini ditulis dalam bahasa C, dan secara resmi disebut **CPython**. Pemahaman ini penting karena eksekusi baris per baris inilah yang membuat Python sedikit lebih lambat dibandingkan bahasa yang dikompilasi penuh seperti C++ atau Go, yang mana akan menjadi pertimbangan kita kelak saat memilih teknologi untuk sistem berskala besar.

**Praktik Eksekusi Asli (*Engineer Way*)**:
Sebagai *Engineer*, kita harus berhenti bergantung pada tombol 'Play' (GUI) di VS Code. Tombol itu menyembunyikan proses sebenarnya. Kita akan berinteraksi langsung dengan *kernel* menggunakan perintah terminal/Linux.

**Latihan**:
Mari kita buktikan bahwa kita bisa mengontrol proses ini secara manual.
1. Buka terminal di VS Code.
2. Buat sebuah *file* bernama `arsitektur.py`.
3. Tulis kode sederhana ini didalamnya:
   ```Python
  print("Eksekusi via terminal berhasil!")
   ```
4. Jangan tekan tombol 'Play'. Di terminal, ketik perintah ini dan tekan Enter: `python arsitektur.py` (atau `*python3 arsitektur.py*` tergantung sistem).

Apa yang terjadi di terminal setelah mengetikkan perintah eksekusi manual tersebut.

```Terminal
Eksekusi via terminal berhasil!
```

Luar biasa! Kita baru saja mengeksekusi program layaknya seorang *Backend Engineer* profesional. Di dunia industri, terutama saat kita bekerja menggunakan sistem operasi Linux (seperti lingkungan WSL2 Ubuntu yang sangat direkomnedasikan untuk pengembangan perangkat lunak modern), kita tidak akan menemukan tombol 'Play'. Semua eksekusi kode, pengujian, hingga *deployment* ke *server cloud* dilakukan melalui terminal. Menguasai antarmuka baris perintah (*Command Line Interface*) adalah keterampilan fundamental mutlak.

Mari kita lanjutkan penyelaman kita ke dalam fundamental Python.

## 1.2 Anatomi Variabel dan Manajemen Memori (Di Balik Layar)

**Fokus Pembelajaran**: Memahami bahwa variabel di Python bukanlah sebuah "wadah", melainkan sebuah referensi (label) yang menunjuk pada alamat memeori tertentu, serta memahami cara kerja *Garbage Collector*.

**Penjelasan Materi**: Pada tutorial tingkat dasar, variabel sering dianalogikan sebagai "kardus penyimpanan barang". Namun, bagi seorang *Engineer*, analogi tersebut keliru dan bisa menyesatkan saat kita menangani data berskala besar atau terstruktur data yang kompleks (seperti *List* atau *Dictionary* yang akan kita pelajari lebih dalam nanti).

Di dalam arsitektur CPython, variabel sebenarnya adalah **referensi** atau **pointer** (petunjuk arah).
Ketika kita menulis kode

```Python
x = 10
```

Ini yang sebenarnya dilakukan oleh komputer di latar belakang:
1. Python meminta alokasi ruang di RAM (memori komputer).
2. Python membuat sebuah "Objek Integer" bernilai `10` dan menyimpannya di ruang memori tersebut.
3. Python membuat nama/label variabel `x`.
4. Python mengikatkan (menunjukan) label `x` ke alamat memori tempat angka `10` itu berada.

**Pembuktian dengan Fungsi `id()`**:
Bagaimana kita membuktikan bahwa variabel adalah petunjuk alamat memori? Python menyediakan fungsi bawaan bernama `id()`. Fungsi ini akan mengembalikan deretan angka yang merepresentasikan identitas unik (atau lamat memori virtual) dari objek yang ditunjukan oleh variabel.

Contoh:

```Python
a = 100
print(id(a))  # Hasilnya akan berupa deretan angka acak yang panjang, misalnya: 1407238129384
```

**Apa itu *Garbage Collection* (Pengumpulan Sampah)?**
Apa yang terjadi jika kita mengubah nilai variabel `x` dari `10` menjadi `20`?

```Python
x = 10 
x = 20
```

Objek `10` di memori **tidak ditimpa** atau dihapus secara langsung. Variabel `x` hanya memutus talinya dari `10` dan menempelkannya ke alamat memori objek `20` yang baru dibuat. Lalu bagaimana nasib objek `10` yang kini "yatim piatu" tanpa label? Python memiliki sistem otomatis bernama **Garbage Collector** berbasis *Reference Counting* (Penghitung Referensi). Karena objek `10` kini memiliki 0 referensi yang menunjuk ke arahnya, *Garbage Collector* akan menyapunya dari memori agar RAM komputer kita tidak penuh (mencegah *Memory Leak*).

**Latihan:**
Mari kita lakukan investigasi memori ini secara langsung untuk melihat kecerdasan optimasi memori CPython (dikenal sebagai *Integer Interning*).

Buat *file* baru bernama `memori.py` di VS Code, lalu ikuti instruksi ini:
1. Buat variabel `angka1` dan isi dengan nilai `256`.
2. Buat variabel `angka2` dan isi juga dengan nilai `256`.
3. Cetak alamat memori `angka1` menggunakan `print(id(angka1))`.
4. Cetak alamat memori `angka2` menggunakan `print(id(angka2))`.
5. (*Eksperimen*) Sekarang, buat variabel `angka3` dan `angka4`, tetapi beri keduanya nilai `1000`. Cetak juga kedua alat memorinya menggunakan fungsi `id()`.

Jalankan skrip ini menggunakan terminal (`python memori.py`). Tuliskan kode beserta *output* deretan angka yang muncul di terminal. Coba perhatikan baik-baik alamat memori `angka1` vs `angka2`, dan bandingkan fenomenanya dengan `angka3` vs `angka4`. Apa yang ditemukan?

**Jawaban:**

```Python
angka1 = 256
angka2 = 256

print(id(angka1))
print(id(angka2))

angka3 = 1000
angka4 = 1000

print(id(angka3))
print(id(angka4))
```

```Terminal
11763848
11763848
140164165451376
140164165451376
```

*Dalam hasil tersebut terlihat `angka1` dan `angka2` memiliki hasil alamat memori yang sama, dan `angka3` dan `angka4` memiliki alamat memori yang sama, dan berbeda dari dua sebelumnya.*

Analisis yang sangat tajam! Kita baru saja membedah apa yang terjadi di dalam mesin CPython. Hasil dari terminal terungkap **dua mekanisme optimasi memori** yang sangat canggih yang bekerja di belakang layar.

Mari kita bongkar mengapa hasilnya demikian:

1. **Fenomena `angka1` dan `angka2` (Small Integer Interning)**:
   Saat CPython pertama kali menyala, ia langsung memesan tempat di RAM untuk angka-angka dari **-5 hingga 256**. Mengapa? Karena berdasarkan riset pembuat Python, angka-angka ini adalah yang paling sering digunakan dalam perulangan dan logika program sehari-hari. Jadi, alih-alih membuat objek baru setiap kali kita mengetik angka `256`, Python cukup menunjuk variabel kita ke objek `256` yang *sudah ada* di memori. Itulah sebabnya ID-nya identik.
2. **Fenomena `angka3` dan `angka4` (Compiler Optimization / Constant Folding)**:
   Secara teori, karena `1000` berada diluar batas angka yang disimpan (-5 s.d 256), Python seharusnya membuat dua objek berbeda dengan ID berada. *Namun*, kita menjalankan *kode ini di dalam satu skrip (satu file `.py`)*.
   Disinilah pintarnya compiler. Saat ia membaca skrip dari atas ke bawah sebelum mengeksekusinya, ia melihat, "*Hei, ada angka 1000 digunakan dua kali di blok kode yang sama. Daripada membuang RAM untuk membuat dua angka 1000, saya tentukan saja alamatnya!*"
   (*Sebagai catatan Engineer: Jika kita mengetikan kode yang sama baris-per-baris di terminal interkatif / REPL, `1000` akan memiliki ID yang berbeda karena compiler tidak bisa membaca masa depan*).

Memahami alokasi memori seperti ini adalah bekal krusial saat kita mulai membangun *backend* atau *database architecture* yang harus memproses jutaan dat dalam satu waktu. Mencegah aplikasi rakus RAM dimulai dari pengetahuan dasar ini.

Mari kita lanjutkan ke lapisan berikutnya dari pondasi kita.

## 1.3 Anatomi Tipe Data (Strong & Dynamic Typing)

**Fokus Pembelajaran**: Memahami miskonsepsi terbesar pemula tentang tipe data di Python dan membuktikan bahwa Python memiliki aturan tipe data yang ketat.

**Penjelasan Materi**:
Mitos terbesar di kalangan programmer pemula adalah: "*Python itu bahasa yang santai, tidak punya tipe data*." Ini adalah pemahaman yang salah fatal.

Di bahasa seperti C atau Java (yang bersifat *Statically Typed*), kita harus memesan kardus dengan bentuk spesifik:
`int umur = 28` (Artinya: Kardus ini cuma boleh diisi angka bulat).

Python bersifat **Dynamically Typed**. Kita tidak perlu menuliskan `int` atau `string`. Namun, ingat prinsip dari bagian 1.2 **Varibel hanyalah label/penujuk**. Oleh karena itu, aturan sebenarnya di Python adalah:
"**Variabel tidak memiliki tipe data. Yang memiliki tipe data adalah OBJEK di dalam memori**."

Lebih jauh lagi, Python bersifat **Strongly Typed** (Tipe Data Kuat). Artinya, setelah objek tercipta di memori sebagai teks (*String*), komputer akan menolak keras jika kita memperlakukannya seperti angka (*Integer*), kecuali kita mengubahnya secara paksa (*Type Casting*).

Mari kita gunakan alat inspeksi kelas *Engineer* yaitu fungsi `type()`. Fungsi ini memungkinakn kita membedakan "DNA" dair objek yang sedang ditunjukan oleh varibel.

**Latihan:**
Mari kita buktikan ketegasan (Strong Typing) dari Python.
Di VS Code, buat *file* beru bernama `tipedata.py` dan tulis urutan logika ini:
   1. Buat variabel `harga` dan isi dengan nilai `50000` (angka bulat).
   2. Buat variabel `diskon` dan isi dengan teks `"10000"` (gunakan tanda kutip).
   3. Cetak DNA (tipe data) dari objek `harga` dengan perintah: `print(type(harga))`
   4. Cetak DNA (tipe data) dari objek `diskon` dengan perintah: `print(type(diskon))`
   5. Di baris terakhir, paksa komputer untuk menjumlahkan keduanya: `total = harga - diskon`, lalu perhatikan baik-baik apa yang terjadi saat kita menjalankan skripnya di terminal.

Jalankan kodenya lewat terminal. Silahkan salin kode, hasil `type()`, dan terutama **pesan error merah panjang (Traceback)** yang muncul. Mari kita bedah anatomi *error* tersebut bersama-sama. Bagaimana hasilnya?

**Jawban:**

```Python
harga = 50000
diskon = "10000"

print(type(harga))
print(type(diskon))

total = harga - diskon
print(total)
```

```Terminal
<class 'int'>
<class 'str'>
Traceback (most recent call last):
  File "/home/bengs/lessons/python-material/bab_1/tipedata.py", line 7, in <module>
    total = harga - diskon
            ~~~~~~^~~~~~~~
TypeError: unsupported operand type(s) for -: 'int' and 'str'
```

Mari kita bedah anatomi *error* yang baru saja dihasilkan. Di dunia nyata, pesan merah ini bukanlah musuh, melainkan log investigasi terbaik.

**Membaca Traceback (Jejaka Rekam Error):**
  1. `Traceback (most recent call last): ` -> Python memberi tahu, "*Ini adalah jejak langkah terakhir sebelum sistem saya menabrak dinding*."
  2. `File "/home/bengs/...", line 7` -> Python menunjukan dengan presisi lokasi persis baris kode yang meledak. Saat kita mengelola ribuan baris kode nanti, informasi baris ini adalah penyelamat hidup.
  3. `TypeError: unsupported operand type(s) for -: 'int' and 'str'` -> Ini adalah inti masalahnya. Python berteriak: "*Saya menolak melakukan operasi pengurangan (-) antara objek ber-DNA Integer dan Objek ber-DNA String!*"

Inilah bukti absolut bahwa **Python adalah bahasa pemrograman Strongly Typed**. Bahasa yang *Weakly Typed* (seperti JavaScript atau PHP) mungkin akan diam-diam menebak maksud kita dan mengubah teks `"10000"` menjadi angka secara otomatis (yang sering kali memicu *bug* tak terduga diproduksi). Python memilih filosofi: "**Lebih baik mati (*crash*) dan memberi tahu programmer ada yang salah, daripada diam-diam menebak dan berpotensi merusak data keuangan**."

**Solusinya: Type Casting (Konversi Paksa)**
Karena Python menolak menebak, kitalah yang harus memberinya instruksi eksplisit untuk mengubah wujud objek tersebut. Ini disebut *Type Casting*.

Kita bisa menggunakan fungsi pembungkus seperti:
  - `int()`: Mengubah objek menjadi Integer (angka bulat).
  - `float()`: Mengubah objek menjadi Float (angka desimal).
  - `str()`: Mengubah objek menjadi String (teks).

Untuk memperbaiki program kasir kita, baris ke tujuh harus diubah menjadi:
`total = harga - int(diskon)`

Coba perbaiki baris tersebut di *file* kita dan jalankan kembali untuk memastikan terminal kita mencetak angkan `40000` denga bersih.

Jika sudah berhasil, mari kita selami satu persatu fundamental di bawah kap mesin Python sebelum kita masuk ke struktur data. Ini adalah materi yang sering dilewatkan pemula, padahal ini adalah penyebab utama 80% *bug* misterius di tingkat menengah/lanjut.

**Perbaikan:**

```Python
harga = 50000
diskon = "10000"

print(type(harga))
print(type(diskon))

total = harga - int(diskon)
print(total)
```

```Terminal
<class 'int'>
<class 'str'>
40000
```

## 1.4 Sifat Anatomi Objek (Mutability vs Immutability)

**Fokus Pembelajaran**: 