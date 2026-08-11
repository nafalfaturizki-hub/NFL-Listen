🦻 NFL — Nafal Faturizki Listener

Open Architecture for Affordable Hearing Assistance

«“Mendengar itu gratis dan hak semua orang.”»

NFL (Nafal Faturizki Listener) adalah proyek open-source untuk membangun platform alat bantu dengar yang murah, dapat diperbaiki, dapat diaudit, dan tidak bergantung pada vendor tertentu.

NFL bukan sekadar sebuah desain alat bantu dengar. NFL dirancang sebagai arsitektur terbuka yang memungkinkan siapa pun membuat perangkat hearing assistance menggunakan berbagai jenis mikrocontroller, codec audio, sensor, amplifier, dan receiver selama perangkat tersebut memenuhi spesifikasi antarmuka NFL.

Tujuan utamanya sederhana:

«Menghilangkan biaya dan ketergantungan teknologi sebagai penghalang seseorang untuk mendapatkan bantuan pendengaran.»

---

🌍 Mengapa NFL?

Alat bantu dengar modern mampu melakukan banyak hal: memperkuat frekuensi tertentu, menyesuaikan suara berdasarkan gangguan pendengaran, mengurangi noise, mengendalikan feedback, dan mengoptimalkan suara percakapan.

Namun teknologi tersebut sering hadir sebagai produk tertutup dengan:

- hardware proprietary,
- firmware tertutup,
- software vendor,
- aplikasi wajib,
- cloud service,
- biaya servis,
- komponen khusus,
- dan ekosistem yang sulit diperbaiki atau diganti.

NFL mengambil pendekatan berbeda.

Teknologi hearing assistance seharusnya dapat dipelajari, dibuat, diperbaiki, dimodifikasi, dan digunakan kembali oleh komunitas.

NFL karena itu dirancang dengan prinsip:

- Open source
- Open hardware
- Offline-first
- No mandatory cloud
- No mandatory subscription
- Vendor-independent architecture
- Repairable
- Low-cost
- Privacy-first
- Rust-based
- Modular
- Reproducible

---

🏗️ Bukan Satu Hardware

NFL tidak dikunci pada satu MCU atau satu vendor.

Arsitekturnya terdiri dari beberapa lapisan:

┌──────────────────────────────────────────┐
│              NFL USER LAYER              │
│ Audiogram • Profiles • Presets • Safety  │
├──────────────────────────────────────────┤
│               NFL DSP CORE               │
│ EQ • WDRC • Noise Reduction • Feedback   │
│ Limiter • Gain • Frequency Shaping       │
├──────────────────────────────────────────┤
│             NFL AUDIO RUNTIME            │
│ Buffer • DMA • Scheduling • Clock        │
├──────────────────────────────────────────┤
│         HARDWARE ABSTRACTION LAYER       │
│ Audio • Storage • Radio • Power          │
├──────────────────────────────────────────┤
│                 HARDWARE                │
│ MCU • ADC/DAC • Mic • Amp • Receiver     │
└──────────────────────────────────────────┘

Dengan pendekatan ini, algoritma NFL tidak bergantung pada satu jenis microcontroller.

Sebuah implementasi dapat menggunakan MCU murah untuk perangkat entry-level, MCU dengan BLE untuk perangkat portable, atau hardware yang lebih kuat untuk algoritma DSP yang lebih kompleks.

Hardware adalah implementasi. NFL adalah arsitekturnya.

---

🎧 Audio Processing

Jantung NFL adalah real-time digital signal processing (DSP).

Pipeline dasarnya dapat terdiri dari:

Microphone
     │
     ▼
Audio Capture
     │
     ▼
Input Conditioning
     │
     ▼
Frequency Shaping / EQ
     │
     ▼
Multi-band WDRC
     │
     ▼
Noise Reduction
     │
     ▼
Feedback Control
     │
     ▼
Gain
     │
     ▼
MPO / Safety Limiter
     │
     ▼
Audio Output
     │
     ▼
Receiver

Setiap blok dirancang sebagai modul independen sehingga implementasi sederhana dapat menggunakan DSP minimal, sementara hardware yang lebih kuat dapat menggunakan algoritma yang lebih kompleks.

---

🧠 Rust sebagai Fondasi

Firmware NFL dikembangkan menggunakan Rust dengan tujuan:

- memory safety,
- deterministic execution,
- tanpa garbage collector,
- cocok untuk bare-metal,
- dapat digunakan pada sistem dengan resource terbatas,
- modular,
- mudah diuji,
- dan dapat dibangun secara reproducible.

Algoritma DSP juga dirancang agar dapat dijalankan di simulator desktop sebelum dipindahkan ke hardware.

Contohnya:

WAV file
   │
   ▼
NFL DSP
   │
   ▼
Processed WAV
   │
   ├── latency analysis
   ├── SNR analysis
   ├── frequency response
   ├── THD analysis
   └── speech-quality metrics

Kode DSP yang sama kemudian dapat digunakan pada perangkat embedded.

---

👤 Personal Hearing Profile

NFL menggunakan konsep Hearing Profile yang terpisah dari hardware.

Sebuah profile dapat berisi:

Hearing Profile
├── Audiogram
├── Frequency response
├── Band gain
├── WDRC parameters
├── Noise reduction
├── Feedback parameters
├── MPO
├── Environment presets
└── Calibration metadata

Dengan demikian profile pengguna tidak terikat pada satu perangkat.

Profile
   │
   ├── NFL Device A
   ├── NFL Device B
   └── NFL Device C

Hardware calibration dan user profile juga dipisahkan sehingga karakteristik microphone, DAC, amplifier, dan receiver dapat dikompensasikan secara individual.

---

🔬 Simulator dan Benchmark

NFL tidak mengandalkan klaim subjektif seperti “suara lebih jelas”.

Setiap algoritma harus dapat diuji secara terukur.

Benchmark mencakup:

- CPU utilization
- memory usage
- cycles/sample
- latency
- power consumption
- frequency response
- noise floor
- THD+N
- dynamic range
- feedback margin
- acoustic output
- speech intelligibility

Pengembangan dilakukan dalam tiga tahap:

SIMULATION
    ↓
ELECTRONIC BENCHMARK
    ↓
ACOUSTIC VALIDATION

Dengan demikian perubahan algoritma dapat dibandingkan secara objektif sebelum digunakan pada perangkat nyata.

---

🔐 Privacy by Design

NFL dirancang offline-first.

Pemrosesan audio utama terjadi di perangkat.

Tidak diperlukan:

- akun cloud,
- server audio,
- upload rekaman suara,
- analytics wajib,
- subscription,
- koneksi internet untuk fungsi dasar.

Data pengguna seperti audiogram dan hearing profile dapat disimpan secara lokal.

Jika komunikasi dengan smartphone digunakan, fungsinya terutama untuk:

- konfigurasi,
- kalibrasi,
- profile management,
- diagnostik,
- dan firmware update.

---

🔧 Repairability

NFL dirancang agar perangkat tidak menjadi barang sekali pakai.

Dokumentasi proyek mencakup:

- schematic,
- PCB source,
- Gerber,
- BOM,
- firmware source,
- mechanical design,
- calibration procedure,
- testing procedure,
- dan assembly documentation.

Tujuannya adalah memungkinkan:

Rusak
  ↓
Diagnosis
  ↓
Ganti komponen
  ↓
Kalibrasi
  ↓
Gunakan kembali

Bukan:

Rusak
  ↓
Buang
  ↓
Beli baru

---

🌱 Ekosistem Terbuka

NFL dapat dikembangkan oleh:

- engineer,
- mahasiswa,
- maker,
- sekolah teknik,
- universitas,
- NGO,
- teknisi lokal,
- komunitas open-source,
- produsen kecil,
- dan organisasi sosial.

Seseorang dapat membuat:

NFL Basic

untuk perangkat ultra-low-cost,

atau:

NFL Advanced

dengan DSP yang lebih kuat.

Selama mengikuti spesifikasi NFL, keduanya tetap berada dalam ekosistem yang sama.

---

💡 Tujuan Akhir

NFL tidak bertujuan mengalahkan perusahaan hearing-aid profesional dalam seluruh aspek teknologi.

Tujuannya berbeda.

NFL ingin membuktikan bahwa:

«perangkat hearing assistance yang berguna dapat dibangun dengan teknologi terbuka, biaya rendah, dan tanpa ketergantungan pada cloud atau vendor tertentu.»

Jika sebuah komunitas di kota besar dapat membuat perangkat sendiri, itu bagus.

Jika sebuah SMK dapat memperbaikinya, lebih bagus.

Jika sebuah NGO dapat membangun 100 perangkat dengan biaya rendah, lebih bagus lagi.

Dan jika satu perangkat akhirnya membuat seseorang kembali mendengar suara anaknya, keluarganya, atau lingkungan di sekitarnya, maka proyek ini telah mencapai tujuannya.

---

❤️ Filosofi NFL

NFL lahir dari keyakinan sederhana:

«Alat bantu dengar bukan kemewahan.»

Jutaan orang hidup dengan keterbatasan pendengaran sementara teknologi untuk membantu mereka sebenarnya telah tersedia.

Hambatannya sering bukan karena teknologi tidak ada.

Hambatannya adalah akses.

NFL berusaha mengurangi hambatan tersebut melalui teknologi terbuka.

Bukan untuk mengalahkan industri.

Bukan untuk membuat semua orang menggunakan satu perangkat.

Tetapi untuk membuat sebuah fondasi yang dapat digunakan siapa saja untuk membangun perangkat mereka sendiri.

Satu desain.

Satu firmware.

Satu profil.

Satu komunitas.

Satu orang yang kembali mendengar dunianya.

«“Mendengar itu gratis dan hak semua orang.”»

---

📜 Lisensi

NFL dirancang sebagai proyek open-source dan open-hardware.

Lisensi yang ditargetkan:

Bagian| Lisensi
Firmware| GPL-3.0
Software / DSP| GPL-3.0
Hardware design| CERN-OHL-S v2
Dokumentasi| CC BY-SA 4.0

Setiap bagian proyek harus memiliki dokumentasi build dan penggunaan yang memadai sehingga komunitas tidak bergantung pada pengetahuan pribadi pembuatnya.

---

🚀 NFL dalam satu kalimat

NFL adalah platform open-source dan open-hardware untuk membangun alat bantu dengar yang murah, modular, dapat diperbaiki, privat, dan tidak terkunci pada vendor tertentu.
