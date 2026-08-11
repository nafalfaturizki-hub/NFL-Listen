# NFL — Nafal Faturizki Listener
## Product Requirements Document (PRD) Master
### Versi 0.1 — Single Source of Truth

---

## Bagian 0: Tentang Dokumen Ini

Dokumen ini adalah **konstitusi teknis NFL**. Seluruh spesifikasi teknis, firmware, software/DSP, hardware design, protokol, format profil, aplikasi, simulator, pengujian, manufaktur, dan dokumentasi NFL diturunkan dari dan harus konsisten dengan dokumen ini.

Apabila terjadi konflik antara sub-dokumen teknis dengan PRD ini, **PRD ini adalah otoritas tertinggi**.

**Status normatif** tiap requirement dinyatakan sebagai:

| Kata Kunci | Definisi |
|---|---|
| MUST | Wajib. Pelanggaran berarti tidak memenuhi standar NFL. |
| MUST NOT | Dilarang keras. |
| SHOULD | Direkomendasikan kuat. Penyimpangan harus didokumentasikan dan dijustifikasi. |
| SHOULD NOT | Tidak direkomendasikan. |
| MAY | Opsional. Boleh diimplementasikan atau tidak. |
| TARGET | Angka aspirasional yang membutuhkan validasi engineering atau audiologi sebelum menjadi MUST. |
| INVARIANT | Tidak boleh berubah oleh keputusan implementasi apapun. |
| NON-GOAL | Secara eksplisit bukan bagian dari NFL. |

**Notasi requirement:** Setiap requirement memiliki ID unik dalam format `NFL-[DOMAIN]-[NOMOR]`. ID ini digunakan untuk traceability dari requirement → spesifikasi → implementasi → test → bukti validasi.

---

## Bagian 1: Mission, Vision, dan Filosofi

### 1.1 Mission Statement

**INVARIANT:** NFL adalah platform open-source dan open-hardware untuk membangun alat bantu dengar yang murah, modular, dapat diperbaiki, privat, dan tidak terkunci pada vendor tertentu.

Mission NFL dapat dinyatakan dalam satu kalimat:

> *"Menghilangkan biaya dan ketergantungan teknologi sebagai penghalang seseorang untuk mendapatkan bantuan pendengaran."*

### 1.2 Filosofi Inti

**INVARIANT:** Filosofi berikut adalah prinsip yang tidak dapat dikompromikan oleh keputusan teknis, bisnis, atau komunitas apapun:

**NFL-PHIL-001** — *Mendengar adalah hak, bukan kemewahan.* NFL tidak memposisikan diri sebagai produk premium. Seluruh keputusan desain harus mempertimbangkan aksesibilitas biaya.

**NFL-PHIL-002** — *Contract over Component.* NFL mendefinisikan kontrak dan interface, bukan komponen spesifik. Implementasi bebas memilih komponen selama memenuhi kontrak.

**NFL-PHIL-003** — *Pengetahuan tidak boleh terkunci.* Seluruh pengetahuan teknis NFL harus terdokumentasi sehingga komunitas tidak bergantung pada pengetahuan pribadi pembuatnya.

**NFL-PHIL-004** — *Dapat diperbaiki adalah fitur, bukan bonus.* Setiap keputusan desain yang membuat perangkat sulit diperbaiki harus dijustifikasi secara eksplisit.

**NFL-PHIL-005** — *Privasi adalah default, bukan pilihan.* Fungsi dasar NFL harus berjalan tanpa koneksi internet, akun cloud, atau pengiriman data ke pihak ketiga.

**NFL-PHIL-006** — *Terukur, bukan subjektif.* Klaim kualitas audio NFL harus didukung oleh metrik yang dapat diukur dan direproduksi.

### 1.3 Vision

NFL ingin membuktikan bahwa perangkat hearing assistance yang berguna dapat dibangun dengan teknologi terbuka, biaya rendah, dan tanpa ketergantungan pada cloud atau vendor tertentu — dan bahwa ekosistem komunitas dapat memelihara serta mengembangkan platform tersebut secara berkelanjutan.

### 1.4 Non-Goals

Non-goal berikut adalah **INVARIANT** dan tidak boleh menjadi arah proyek:

**NFL-NG-001** — NFL bukan bertujuan mengalahkan hearing aid komersial kelas medis dalam seluruh aspek performa teknis.

**NFL-NG-002** — NFL bukan produk dengan model bisnis berbasis cloud subscription.

**NFL-NG-003** — NFL bukan platform yang mengunci pengguna pada satu vendor hardware atau software.

**NFL-NG-004** — NFL bukan perangkat medis yang diklaim dapat mendiagnosis atau mengobati kondisi medis. NFL adalah alat bantu dengar assistive technology.

**NFL-NG-005** — NFL bukan proyek yang mengumpulkan data audio pengguna untuk kepentingan apapun.

---

## Bagian 2: Problem Statement

### 2.1 Problem Utama

Teknologi hearing assistance modern secara teknis mampu membantu jutaan orang dengan gangguan pendengaran. Namun hambatan akses tetap besar:

**NFL-PROB-001** — Biaya alat bantu dengar komersial berada di luar jangkauan sebagian besar populasi dunia yang membutuhkan.

**NFL-PROB-002** — Hardware proprietary membuat perangkat tidak dapat diperbaiki atau diganti komponennya secara mandiri.

**NFL-PROB-003** — Firmware dan software tertutup membuat perangkat tidak dapat diaudit, dimodifikasi, atau disesuaikan dengan kebutuhan lokal.

**NFL-PROB-004** — Ketergantungan pada cloud service dan aplikasi vendor menciptakan risiko discontinuation dan privacy.

**NFL-PROB-005** — Ekosistem tertutup mencegah transfer pengetahuan ke komunitas lokal, teknisi, atau institusi pendidikan.

**NFL-PROB-006** — Tidak ada platform terbuka yang memungkinkan berbagai aktor (komunitas, NGO, universitas, produsen kecil) membangun perangkat hearing assistance yang interoperable.

### 2.2 Root Cause

Root cause dari seluruh problem di atas adalah absennya **standar terbuka** untuk hearing assistance platform yang mencakup hardware interface, DSP contract, profile format, dan protokol komunikasi secara bersamaan.

NFL hadir untuk mengisi gap tersebut.

---

## Bagian 3: Target Pengguna

### 3.1 End User (Pengguna Akhir)

**NFL-USR-001** — Individu dengan gangguan pendengaran (ringan hingga sedang-berat) yang membutuhkan alat bantu dengar tetapi tidak memiliki akses ke solusi komersial karena keterbatasan biaya, geografi, atau infrastruktur.

**NFL-USR-002** — Individu yang membutuhkan perangkat hearing assistance yang dapat diperbaiki dan dipelihara secara mandiri atau oleh komunitas lokal.

### 3.2 Implementer

**NFL-USR-003** — Engineer, maker, dan komunitas open-source yang ingin membangun hardware NFL-compatible.

**NFL-USR-004** — Mahasiswa dan institusi pendidikan (universitas, SMK teknik) yang menggunakan NFL sebagai platform pembelajaran.

**NFL-USR-005** — NGO dan organisasi sosial yang ingin memproduksi perangkat hearing assistance dalam jumlah kecil-menengah dengan biaya rendah.

**NFL-USR-006** — Produsen kecil yang ingin memproduksi hardware NFL-compatible tanpa harus membangun seluruh stack dari awal.

**NFL-USR-007** — Peneliti dan audiolog yang ingin bereksperimen dengan algoritma fitting dan DSP pada platform yang dapat diaudit.

### 3.3 Contributor

**NFL-USR-008** — Kontributor open-source yang mengembangkan firmware, software/DSP, hardware design, atau dokumentasi.

**NFL-USR-009** — Teknisi lokal yang memperbaiki dan mengkalibrasi perangkat NFL di lapangan.

---

## Bagian 4: Product Definition dan System Boundaries

### 4.1 Definisi Platform NFL

**INVARIANT:** NFL adalah sebuah **platform**, bukan sebuah produk tunggal. Platform NFL terdiri dari:

1. **NFL Standard** — Kumpulan kontrak, interface, format, dan protokol yang mendefinisikan apa artinya "NFL-compatible".
2. **NFL Reference Implementation** — Implementasi referensi dari Standard NFL dalam bentuk firmware, software/DSP, hardware design, dan aplikasi.
3. **NFL Ecosystem** — Seluruh implementasi hardware, firmware, dan software yang memenuhi NFL Standard, baik dari tim inti maupun komunitas.

### 4.2 System Boundaries

**NFL-SYS-001 (MUST)** — NFL sebagai platform mencakup empat domain utama dengan batas yang tegas:

```
┌─────────────────────────────────────────────────────┐
│                    NFL PLATFORM                     │
│                                                     │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐    │
│  │  SOFTWARE  │  │  FIRMWARE  │  │  HARDWARE  │    │
│  │   / DSP    │  │            │  │   DESIGN   │    │
│  └────────────┘  └────────────┘  └────────────┘    │
│                                                     │
│  ┌─────────────────────────────────────────────┐   │
│  │           NFL STANDARDS & SCHEMAS           │   │
│  └─────────────────────────────────────────────┘   │
│                                                     │
│  ┌─────────────────────────────────────────────┐   │
│  │              DOCUMENTATION                  │   │
│  └─────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
```

**NFL-SYS-002 (INVARIANT)** — Batas antar domain MUST NOT dilanggar oleh dependency langsung:

- Software/DSP MUST NOT bergantung pada hardware spesifik apapun.
- Firmware MUST NOT mengandung DSP business logic yang bypass NFL DSP Contract.
- Hardware design MUST NOT menjadi dependency source-code DSP atau firmware core.
- Documentation MUST NOT menjadi dependency runtime.

**NFL-SYS-003 (MUST)** — NFL Standards dan Schemas adalah satu-satunya mekanisme binding antar domain.

### 4.3 Apa yang Ada di Dalam Scope NFL

- Real-time audio capture, processing, dan output pada perangkat hearing assistance.
- Personal hearing profile management.
- Hardware calibration.
- Device-to-app communication untuk konfigurasi, kalibrasi, dan update.
- Over-the-air firmware update.
- Simulator dan benchmark untuk validasi algoritma.
- Open hardware reference designs.
- Dokumentasi lengkap untuk reproduksi, perbaikan, dan pengembangan.

### 4.4 Apa yang Ada di Luar Scope NFL

- Diagnosis medis gangguan pendengaran.
- Pure-tone audiometry sebagai alat medis (simulator audiogram adalah tools development, bukan alat diagnostik medis).
- Cloud-based audio processing sebagai fungsi utama.
- Prescription fitting oleh audiolog profesional (NFL dapat digunakan sebagai alat bantu, bukan pengganti).

---

## Bagian 5: Arsitektur Konseptual

### 5.1 Architectural Layers

**NFL-ARCH-001 (INVARIANT)** — Arsitektur NFL terdiri dari lapisan berikut dari bawah ke atas:

```
┌──────────────────────────────────────────────────────┐
│                   NFL USER LAYER                     │
│  Audiogram · Hearing Profile · Presets · Safety      │
├──────────────────────────────────────────────────────┤
│                   NFL DSP CORE                       │
│  EQ · WDRC · Noise Reduction · Feedback Control      │
│  Limiter · Gain · Frequency Shaping                  │
├──────────────────────────────────────────────────────┤
│                NFL AUDIO RUNTIME                     │
│  Buffer Management · Scheduling · Clock Sync         │
├──────────────────────────────────────────────────────┤
│           HARDWARE ABSTRACTION LAYER (HAL)           │
│  Audio Input · Audio Output · Storage · Radio        │
│  Power · Clock · GPIO                                │
├──────────────────────────────────────────────────────┤
│                     HARDWARE                         │
│  MCU · ADC/DAC · Microphone · Amplifier · Receiver   │
└──────────────────────────────────────────────────────┘
```

**NFL-ARCH-002 (INVARIANT)** — Setiap lapisan MUST hanya berkomunikasi dengan lapisan langsung di atas atau di bawahnya melalui interface yang terdefinisi. Bypass lapisan dilarang.

**NFL-ARCH-003 (INVARIANT)** — NFL DSP Core MUST dapat dijalankan tanpa modifikasi di tiga konteks: perangkat embedded (melalui firmware), simulator desktop, dan aplikasi mobile/desktop.

### 5.2 Domain Boundaries

**NFL-ARCH-004 (INVARIANT)** — Dependency rules antar domain:

```
NFL Schemas
     │
     ├──────────────────────────────────┐
     │                                  │
     ▼                                  ▼
 SOFTWARE/DSP                       FIRMWARE
 ├── nfl-dsp                        ├── nfl-runtime
 ├── nfl-audiology                  ├── nfl-hal
 ├── nfl-profile                    ├── nfl-boot
 ├── nfl-calibration                └── nfl-power
 └── nfl-protocol
     │                                  │
     └──────────────┬───────────────────┘
                    │
                    ▼
               HARDWARE
               (implements HAL contracts)
```

**NFL-ARCH-005 (MUST)** — Setiap kontrak antara domain MUST terdefinisi sebagai schema formal dalam `schemas/` dan MUST bersifat versioned.

### 5.3 NFL Compatibility Model

**NFL-ARCH-006 (INVARIANT)** — Sebuah hardware dikategorikan sebagai NFL-compatible apabila dan hanya apabila memenuhi seluruh kontrak berikut:

1. **NFL Hardware Contract** — Memenuhi minimum hardware requirements (Bagian 9).
2. **NFL HAL Contract** — Mengimplementasikan seluruh HAL interface yang diwajibkan.
3. **NFL Audio Contract** — Memenuhi audio interface requirements.
4. **NFL Protocol Contract** — Mendukung protokol komunikasi NFL.
5. **NFL Safety Contract** — Memenuhi seluruh safety requirements.

Tidak ada requirement untuk menggunakan MCU, codec, amplifier, atau komponen spesifik apapun.

---

## Bagian 6: Requirement Fungsional Sistem

### 6.1 Audio Processing

**NFL-REQ-001 (MUST)** — Sistem MUST mampu melakukan real-time audio capture dari microphone, memproses audio melalui NFL DSP pipeline, dan mengeluarkan audio ke receiver/speaker dalam single pipeline tanpa interupsi yang menyebabkan audio artifacts yang terdengar.

**NFL-REQ-002 (MUST)** — NFL DSP pipeline MUST mendukung setidaknya komponen berikut sebagai modul independen yang dapat diaktifkan atau dinonaktifkan:

- Input conditioning dan gain control
- Multi-band frequency equalization (EQ)
- Wide Dynamic Range Compression (WDRC)
- Noise reduction
- Feedback management/cancellation
- Output gain control
- Maximum Power Output (MPO) limiter / safety limiter

**NFL-REQ-003 (MUST)** — Setiap modul DSP MUST memiliki antarmuka yang terdefinisi sehingga dapat diuji secara independen dari modul lainnya.

**NFL-REQ-004 (MUST)** — Urutan pemrosesan dalam pipeline MUST terdokumentasi dan deterministik untuk setiap konfigurasi.

**NFL-REQ-005 (SHOULD)** — Sistem SHOULD mendukung konfigurasi multi-channel (minimum stereo/binauaral) untuk implementasi dua telinga.

**NFL-REQ-006 (MAY)** — Sistem MAY mendukung algoritma directionality berbasis multi-microphone.

### 6.2 Hearing Profile

**NFL-REQ-010 (MUST)** — Sistem MUST mendukung konsep Hearing Profile yang terpisah dari hardware spesifik.

**NFL-REQ-011 (MUST)** — Sebuah Hearing Profile MUST dapat dipindahkan antara perangkat NFL yang berbeda tanpa kehilangan informasi konfigurasi yang esensial, asalkan kedua perangkat mendukung versi schema profile yang sama.

**NFL-REQ-012 (MUST)** — Hearing Profile MUST mencakup minimal:

- Data audiogram (threshold per frekuensi)
- Konfigurasi band gain per frekuensi
- Parameter WDRC per band
- Batas MPO
- Metadata identifikasi dan versi

**NFL-REQ-013 (SHOULD)** — Hearing Profile SHOULD mencakup:

- Environment presets (tenang, ramai, musik, dll.)
- Metadata kalibrasi hardware
- Parameter noise reduction
- Parameter feedback management

**NFL-REQ-014 (MUST)** — Hearing Profile MUST disimpan dalam format yang terdefinisi oleh NFL Profile Schema dan harus dapat divalidasi terhadap schema tersebut.

**NFL-REQ-015 (MUST)** — Hardware calibration data dan user hearing profile MUST dipisahkan menjadi entitas yang berbeda. Kalibrasi hardware mendeskripsikan karakteristik fisik perangkat; hearing profile mendeskripsikan kebutuhan pendengar.

### 6.3 Kalibrasi

**NFL-REQ-020 (MUST)** — Sistem MUST mendukung kalibrasi individual untuk:

- Karakteristik microphone (frequency response, sensitivity)
- Karakteristik receiver/output (frequency response, efficiency)
- Kompensasi akustik keseluruhan sistem

**NFL-REQ-021 (MUST)** — Data kalibrasi MUST disimpan dalam format yang terdefinisi oleh NFL Calibration Schema.

**NFL-REQ-022 (MUST)** — DSP pipeline MUST dapat mengaplikasikan correction berbasis data kalibrasi secara transparan.

**NFL-REQ-023 (SHOULD)** — Prosedur kalibrasi SHOULD dapat dilakukan dengan peralatan yang tersedia secara umum, tidak memerlukan peralatan audiologi khusus yang mahal untuk kalibrasi dasar.

### 6.4 Device Management

**NFL-REQ-030 (MUST)** — Perangkat MUST mampu menyimpan minimal satu Hearing Profile secara lokal (on-device storage).

**NFL-REQ-031 (SHOULD)** — Perangkat SHOULD mampu menyimpan lebih dari satu Hearing Profile untuk multiple environment presets.

**NFL-REQ-032 (MUST)** — Perangkat MUST mampu beroperasi penuh menggunakan profile yang tersimpan secara lokal tanpa koneksi ke smartphone atau komputer.

**NFL-REQ-033 (MUST)** — Sistem MUST mendukung Over-the-Air (OTA) firmware update melalui protokol NFL yang terdefinisi.

**NFL-REQ-034 (MUST)** — OTA update MUST mendukung rollback ke versi firmware sebelumnya apabila update gagal atau menghasilkan kondisi tidak stabil.

**NFL-REQ-035 (MUST)** — Perangkat MUST menyediakan mekanisme diagnostik yang dapat diakses melalui protokol NFL tanpa memerlukan akses fisik ke debug port pada kondisi normal.

### 6.5 Komunikasi

**NFL-REQ-040 (MUST)** — Sistem MUST mendukung setidaknya satu jalur komunikasi nirkabel antara perangkat dan host (smartphone/komputer) untuk keperluan konfigurasi dan update.

**NFL-REQ-041 (MUST)** — Protokol komunikasi NFL MUST bersifat terbuka dan terdokumentasi lengkap sehingga siapapun dapat mengimplementasikan host application yang kompatibel.

**NFL-REQ-042 (MUST)** — Seluruh perintah dan respons protokol NFL MUST menggunakan format yang terdefinisi oleh NFL Protocol Schema.

**NFL-REQ-043 (SHOULD)** — Sistem SHOULD mendukung komunikasi USB untuk keperluan pengembangan, debugging, dan update alternatif.

**NFL-REQ-044 (MAY)** — Sistem MAY mendukung mode komunikasi tambahan (misalnya audio loop, proprietary link) selama tidak menggantikan kewajiban dukungan protokol NFL standar.

### 6.6 Aplikasi Host

**NFL-REQ-050 (MUST)** — NFL MUST menyediakan setidaknya satu aplikasi host referensi (mobile atau desktop) yang mengimplementasikan NFL Protocol secara lengkap.

**NFL-REQ-051 (MUST)** — Aplikasi host referensi MUST mendukung fungsi minimal:

- Koneksi ke perangkat NFL
- Baca dan tulis Hearing Profile
- Inisiasi dan panduan kalibrasi
- Baca data diagnostik perangkat
- Inisiasi firmware update

**NFL-REQ-052 (SHOULD)** — Aplikasi host SHOULD menyediakan antarmuka untuk input atau import data audiogram.

**NFL-REQ-053 (MUST)** — Aplikasi host MUST berfungsi secara offline untuk seluruh operasi device management. Koneksi internet MUST NOT diperlukan untuk fungsi dasar.

---

## Bagian 7: Requirement Non-Fungsional

### 7.1 Performance

**NFL-PERF-001 (MUST)** — End-to-end audio latency dari microphone input ke receiver output MUST tidak melebihi **threshold yang akan ditentukan melalui validasi audiologi dan usability testing**. Sebagai TARGET awal, latency ≤ 10 ms (microphone-to-receiver, pada jalur DSP, tidak termasuk I/O hardware latency yang tidak dapat dikontrol oleh DSP). *[TARGET — membutuhkan validasi audiologi sebelum menjadi MUST dengan angka spesifik.]*

**NFL-PERF-002 (MUST)** — Jitter latency MUST deterministik dan terbatas. Variasi latency MUST NOT menyebabkan audio artifacts yang terdengar dalam penggunaan normal.

**NFL-PERF-003 (MUST)** — DSP pipeline MUST mampu memproses audio secara real-time tanpa underrun pada hardware yang memenuhi minimum hardware requirements.

**NFL-PERF-004 (TARGET)** — CPU utilization DSP pipeline SHOULD tidak melebihi 70% dari kapasitas komputasi tersedia pada hardware minimum, menyisakan headroom untuk overhead sistem dan fitur tambahan. *[TARGET — membutuhkan profiling pada hardware referensi.]*

**NFL-PERF-005 (MUST)** — Memory footprint firmware MUST berada dalam batas yang memungkinkan deployment pada hardware yang memenuhi minimum memory requirements (Bagian 9).

### 7.2 Reliability dan Availability

**NFL-REL-001 (MUST)** — Firmware MUST beroperasi secara kontinu tanpa restart yang tidak disengaja dalam kondisi penggunaan normal.

**NFL-REL-002 (MUST)** — Sistem MUST mengimplementasikan watchdog mechanism yang secara otomatis me-reset perangkat apabila firmware berhenti merespons, dan MUST menjaga audio safety (tidak ada output yang berbahaya) saat reset berlangsung.

**NFL-REL-003 (MUST)** — Kegagalan modul DSP non-kritis MUST NOT menyebabkan perangkat berhenti total. Sistem MUST dapat fallback ke mode operasi yang lebih sederhana.

**NFL-REL-004 (MUST)** — Integritas data storage (profile, kalibrasi) MUST dilindungi terhadap korups akibat power loss. Mekanisme journaling atau checksumming MUST diimplementasikan.

**NFL-REL-005 (MUST)** — OTA update yang gagal MUST NOT membuat perangkat dalam kondisi unbootable secara permanen. Mekanisme rollback MUST tersedia.

**NFL-REL-006 (TARGET)** — Mean Time Between Failures (MTBF) untuk software/firmware adalah TARGET yang akan ditentukan berdasarkan field data dan acceptance testing. *[TARGET — membutuhkan data empiris.]*

### 7.3 Maintainability

**NFL-MAINT-001 (MUST)** — Seluruh source code firmware dan software MUST memiliki dokumentasi pada level modul yang cukup untuk memungkinkan engineer baru memahami fungsi dan interface tanpa perlu bertanya kepada penulis asli.

**NFL-MAINT-002 (MUST)** — Penggantian platform hardware (MCU baru) MUST hanya memerlukan penulisan atau penggantian HAL adapter, tanpa modifikasi pada firmware core, DSP, atau profile format.

**NFL-MAINT-003 (MUST)** — Seluruh build, test, dan release MUST dapat direproduksi secara deterministik dari source code menggunakan toolchain yang terdokumentasi.

**NFL-MAINT-004 (SHOULD)** — Test coverage SHOULD memadai untuk mendeteksi regresi pada seluruh komponen kritis (DSP, protocol, storage, boot, safety).

**NFL-MAINT-005 (MUST)** — Setiap perubahan pada NFL Schemas atau Protocol yang tidak backward-compatible MUST melalui proses versioning yang terdokumentasi dan MUST NOT dilakukan tanpa bumping major version.

### 7.4 Portability

**NFL-PORT-001 (MUST)** — NFL DSP Core MUST dapat dikompilasi dan dijalankan pada setidaknya tiga target: Linux (x86_64, untuk simulator), embedded ARM Cortex-M (atau arsitektur setara), dan Android/iOS (untuk aplikasi mobile).

**NFL-PORT-002 (MUST)** — DSP Core MUST NOT mengandung platform-specific code. Seluruh platform dependency MUST diisolasi pada lapisan adaptor.

**NFL-PORT-003 (SHOULD)** — Firmware SHOULD dapat diporting ke platform hardware baru dalam waktu yang reasonable oleh engineer yang familiar dengan platform target, dengan mengikuti porting guide yang tersedia.

### 7.5 Testability

**NFL-TEST-001 (MUST)** — Seluruh modul DSP MUST dapat diuji secara unit dengan audio file sintetis tanpa hardware fisik.

**NFL-TEST-002 (MUST)** — NFL MUST menyediakan simulator yang memungkinkan seluruh DSP pipeline dijalankan end-to-end pada komputer dengan audio file input dan menghasilkan output yang dapat diukur.

**NFL-TEST-003 (MUST)** — Seluruh acceptance criteria dalam PRD ini MUST memiliki test atau benchmark yang terdefinisi yang dapat memverifikasi pemenuhannya.

**NFL-TEST-004 (MUST)** — Test suite MUST berjalan dalam CI pipeline tanpa memerlukan hardware fisik untuk subset unit test dan simulator test.

---

## Bagian 8: Requirement Audio dan DSP

### 8.1 Audio Interface Contract

**NFL-AUDIO-001 (MUST)** — NFL mendefinisikan Audio Interface Contract sebagai berikut. Implementasi hardware MUST mampu menyediakan audio stream dengan parameter minimal:

- Sample rate: MUST mendukung minimum **16 kHz**; SHOULD mendukung **24 kHz atau lebih tinggi**. *[Angka spesifik membutuhkan validasi audiologi.]*
- Bit depth: MUST mendukung minimum **16-bit**; SHOULD mendukung **24-bit**.
- Channels: MUST mendukung minimum **1 channel (mono)**; SHOULD mendukung **2 channels (stereo)**.

**NFL-AUDIO-002 (MUST)** — Audio Interface MUST menyediakan jaminan timing yang cukup deterministik untuk mendukung real-time processing dengan latency yang memenuhi NFL-PERF-001.

**NFL-AUDIO-003 (MUST)** — Audio capture dan playback MUST sinkron dalam satu clock domain atau MUST menyediakan mekanisme sinkronisasi yang mencegah sample drift.

### 8.2 DSP Requirements

**NFL-DSP-001 (MUST)** — NFL DSP Core MUST mengimplementasikan pipeline yang dapat dikonfigurasi per Hearing Profile, bukan hardcoded.

**NFL-DSP-002 (MUST)** — EQ implementation MUST mendukung minimum **4 band** parametric EQ yang dapat dikonfigurasi. SHOULD mendukung **8 band atau lebih**. *[Jumlah band minimum membutuhkan validasi audiologi.]*

**NFL-DSP-003 (MUST)** — WDRC implementation MUST mendukung setidaknya per-band compression dengan parameter yang dapat dikonfigurasi: threshold, ratio, attack time, dan release time.

**NFL-DSP-004 (MUST)** — Safety Limiter / MPO MUST diimplementasikan sebagai stage terpisah yang CANNOT dinonaktifkan oleh konfigurasi profil pengguna biasa. Lihat Bagian 11 untuk safety requirements.

**NFL-DSP-005 (MUST)** — Seluruh parameter DSP yang dapat dikonfigurasi MUST memiliki range valid yang terdefinisi dan MUST divalidasi saat profile dimuat. Parameter di luar range valid MUST ditolak atau di-clamp dengan peringatan.

**NFL-DSP-006 (TARGET)** — Frekuensi band DSP SHOULD mencakup rentang yang relevan untuk speech intelligibility, yaitu 250 Hz hingga 8 kHz minimal. *[Rentang spesifik membutuhkan validasi audiologi.]*

**NFL-DSP-007 (MUST)** — Algoritma noise reduction MUST dapat diukur dan MUST memiliki parameter yang dapat dikonfigurasi termasuk setidaknya tingkat agresivitas/strength.

**NFL-DSP-008 (MUST)** — Feedback management MUST diimplementasikan. Minimum implementasi adalah feedback detection dan suppression. Feedback cancellation aktif adalah SHOULD.

**NFL-DSP-009 (MUST)** — DSP pipeline MUST beroperasi secara deterministik: input yang sama dengan konfigurasi yang sama MUST selalu menghasilkan output yang sama (dalam toleransi floating-point).

**NFL-DSP-010 (MUST)** — Processing artifacts yang dihasilkan oleh DSP (bukan inherent pada audio input) MUST berada di bawah threshold yang dapat terdengar dalam penggunaan normal. *[Threshold spesifik membutuhkan validasi audiologi dan psikoacoustics.]*

### 8.3 Audio Quality Metrics

Metrik berikut MUST dapat diukur dan dilaporkan oleh NFL benchmark suite:

**NFL-AUDIO-010 (MUST)** — **End-to-end latency** (microphone ke receiver) MUST dapat diukur.

**NFL-AUDIO-011 (MUST)** — **Frequency response** sistem MUST dapat diukur dan dibandingkan dengan target dari hearing profile.

**NFL-AUDIO-012 (MUST)** — **Signal-to-Noise Ratio (SNR)** MUST dapat diukur pada kondisi referensi.

**NFL-AUDIO-013 (MUST)** — **Total Harmonic Distortion + Noise (THD+N)** MUST dapat diukur pada kondisi referensi.

**NFL-AUDIO-014 (MUST)** — **Dynamic range** sistem MUST dapat diukur.

**NFL-AUDIO-015 (MUST)** — **Noise floor** sistem MUST dapat diukur.

**NFL-AUDIO-016 (SHOULD)** — **Speech intelligibility metric** (misalnya STI atau STIPA) SHOULD dapat dihitung oleh simulator.

**NFL-AUDIO-017 (SHOULD)** — **Compression characteristics** (attack, release, ratio per band) SHOULD dapat diverifikasi secara terukur.

Nilai numerik target untuk metrik di atas adalah **TARGET** yang akan ditetapkan berdasarkan validasi audiologi, benchmark hardware referensi, dan komparasi dengan standar industri yang relevan (misalnya IEC 60118). *[Tidak ada angka spesifik yang dinyatakan dalam PRD ini sampai validasi selesai.]*

---

## Bagian 9: Requirement Hardware

### 9.1 NFL Hardware Minimum Requirements

**NFL-HW-001 (MUST)** — Hardware yang diklaim NFL-compatible MUST memenuhi seluruh minimum requirements berikut. Hardware MUST NOT mengunci implementasi pada komponen spesifik apapun selama requirements terpenuhi.

**NFL-HW-002 (MUST)** — **Processing capability:** Hardware MUST memiliki kemampuan komputasi yang cukup untuk menjalankan NFL DSP pipeline pada sample rate dan konfigurasi band yang ditargetkan dalam real-time. *[Angka MIPS/MFLOPS minimum akan ditentukan dari profiling pada reference implementation.]*

**NFL-HW-003 (MUST)** — **Memory:** Hardware MUST menyediakan RAM yang cukup untuk audio buffers, DSP working memory, firmware stack, dan runtime overhead. Flash/ROM MUST cukup untuk firmware, bootloader, dan storage profile. *[Angka spesifik akan ditentukan dari reference implementation.]*

**NFL-HW-004 (MUST)** — **Audio input:** Hardware MUST menyediakan setidaknya satu channel audio input digital atau analog dengan dynamic range dan noise floor yang memenuhi NFL-AUDIO requirements.

**NFL-HW-005 (MUST)** — **Audio output:** Hardware MUST menyediakan setidaknya satu channel audio output ke receiver/speaker dengan karakteristik yang memenuhi NFL-AUDIO requirements.

**NFL-HW-006 (MUST)** — **Storage non-volatile:** Hardware MUST menyediakan storage non-volatile yang cukup untuk menyimpan minimum satu Hearing Profile, data kalibrasi, dan firmware image untuk keperluan rollback.

**NFL-HW-007 (MUST)** — **Communication:** Hardware MUST mendukung setidaknya satu interface komunikasi yang mampu mengimplementasikan NFL Protocol (Bluetooth Low Energy adalah SHOULD; alternatif lain diperbolehkan selama protokol NFL dapat diimplementasikan).

**NFL-HW-008 (MUST)** — **Power:** Hardware MUST menyediakan manajemen daya yang memungkinkan operasi dari baterai dengan durasi yang reasonable untuk use case hearing assistance. *[TARGET durasi baterai minimum akan ditentukan dari validasi use case.]*

**NFL-HW-009 (SHOULD)** — Hardware SHOULD mendukung debug interface (misalnya SWD, JTAG, atau UART) yang dapat diakses selama pengembangan.

**NFL-HW-010 (MUST)** — Hardware MUST memenuhi seluruh NFL Safety Requirements (Bagian 11) termasuk kemampuan untuk menghentikan output audio dalam kondisi darurat.

### 9.2 Reference Design Requirements

**NFL-HW-020 (MUST)** — NFL MUST menyediakan setidaknya satu reference hardware design yang terdokumentasi lengkap.

**NFL-HW-021 (MUST)** — Reference design MUST mencakup: schematic lengkap, PCB layout source, Gerber files, Bill of Materials (BOM) dengan part number alternatif, panduan assembly, dan panduan pengujian.

**NFL-HW-022 (MUST)** — Reference design MUST menggunakan komponen yang tersedia secara umum (tidak menggunakan komponen yang hanya tersedia dari satu distributor tunggal tanpa alternatif).

**NFL-HW-023 (SHOULD)** — NFL SHOULD menyediakan beberapa reference design dalam kategori berbeda (misalnya basic, standard, advanced) untuk mengakomodasi berbagai tradeoff antara biaya, performa, dan fitur.

**NFL-HW-024 (MUST)** — Seluruh reference design MUST diuji dan diverifikasi memenuhi seluruh NFL requirements sebelum disebut sebagai "NFL Reference Design".

### 9.3 Mechanical dan Form Factor

**NFL-HW-030 (MUST)** — NFL mendefinisikan hardware requirements sebagai capability contract, bukan form factor. Form factor (ITE, BTE, RIC, dll.) adalah keputusan implementasi.

**NFL-HW-031 (SHOULD)** — Dokumentasi hardware SHOULD mencakup panduan untuk setidaknya satu form factor yang umum digunakan.

**NFL-HW-032 (MUST)** — Desain mekanis MUST mempertimbangkan kemudahan perbaikan sebagai requirement. Komponen yang paling sering rusak SHOULD dapat diganti tanpa peralatan khusus yang mahal.

### 9.4 Affordability Target

**NFL-HW-040 (TARGET)** — Bill of Materials (BOM) untuk reference design basic SHOULD memungkinkan produksi perangkat pada biaya yang signifikan lebih rendah dari hearing aid komersial entry-level. *[Angka target biaya BOM akan ditetapkan berdasarkan riset pasar dan validasi supply chain. Angka ini adalah TARGET non-normatif dan tidak boleh dinyatakan sebagai MUST sampai divalidasi.]*

---

## Bagian 10: Requirement Firmware

### 10.1 Firmware Architecture Requirements

**NFL-FW-001 (MUST)** — Firmware MUST diimplementasikan dalam bahasa yang menyediakan memory safety atau MUST menggunakan teknik yang memadai untuk mencegah memory corruption pada komponen kritis. Rust adalah SHOULD; bahasa alternatif memerlukan justifikasi eksplisit dalam konteks keamanan dan safety.

**NFL-FW-002 (MUST)** — Firmware core (runtime, DSP integration, protocol handling) MUST tidak bergantung pada platform hardware spesifik. Seluruh hardware dependency MUST diisolasi pada HAL layer.

**NFL-FW-003 (MUST)** — HAL MUST mendefinisikan interface yang harus diimplementasikan oleh setiap platform. Interface ini MUST terdokumentasi dan stabil.

**NFL-FW-004 (MUST)** — Firmware MUST menggunakan model task/thread yang deterministik dan dapat diprediksi. Priority inversion dan deadlock MUST dicegah melalui desain.

**NFL-FW-005 (MUST)** — Firmware MUST dapat dibangun secara reproducible dari source code menggunakan toolchain yang terdokumentasi.

### 10.2 Boot dan Security Requirements

**NFL-FW-010 (MUST)** — Bootloader MUST memverifikasi integritas firmware image sebelum eksekusi menggunakan mekanisme kriptografi.

**NFL-FW-011 (MUST)** — Firmware MUST mendukung mekanisme rollback ke versi sebelumnya apabila verification gagal atau boot loop terdeteksi.

**NFL-FW-012 (SHOULD)** — Firmware SHOULD mendukung secure boot chain sehingga hanya firmware yang ditandatangani dengan kunci yang diotorisasi yang dapat dieksekusi.

**NFL-FW-013 (MUST)** — Firmware update (OTA) MUST diverifikasi kriptografisnya sebelum diaplikasikan.

**NFL-FW-014 (MUST)** — Private keys untuk signing firmware MUST tidak ada dalam source code repository atau binary yang didistribusikan.

### 10.3 Power Management Requirements

**NFL-FW-020 (MUST)** — Firmware MUST mengimplementasikan power management yang memungkinkan perangkat memasuki low-power state saat tidak aktif memproses audio.

**NFL-FW-021 (MUST)** — Transisi antara power states MUST tidak menyebabkan audio glitch yang terdengar atau kehilangan konfigurasi.

**NFL-FW-022 (MUST)** — Battery level monitoring MUST diimplementasikan dan MUST dapat dibaca melalui NFL Protocol.

**NFL-FW-023 (MUST)** — Perangkat MUST gracefully shutdown atau masuk ke safe state saat baterai kritis, tanpa menyebabkan data corruption atau audio output yang berbahaya.

### 10.4 Storage Requirements

**NFL-FW-030 (MUST)** — Storage firmware MUST mengimplementasikan wear leveling atau menggunakan storage controller yang menyediakannya, untuk mencegah premature failure pada flash storage.

**NFL-FW-031 (MUST)** — Semua write ke non-volatile storage MUST dilindungi terhadap power loss mid-write yang dapat menyebabkan data corruption.

**NFL-FW-032 (MUST)** — Firmware MUST dapat memuat dan memvalidasi Hearing Profile dari storage sebelum memulai audio processing.

**NFL-FW-033 (MUST)** — Apabila profile yang tersimpan corrupt atau tidak valid, firmware MUST fallback ke safe default configuration dan MUST melaporkan kondisi ini melalui diagnostik.

---

## Bagian 11: Safety Requirements

### 11.1 Acoustic Safety

**NFL-SAFETY-001 (INVARIANT — MUST)** — Sistem MUST mengimplementasikan Maximum Power Output (MPO) limiter yang membatasi output akustik ke batas aman. MPO limiter MUST NOT dapat dinonaktifkan oleh pengguna akhir melalui mekanisme normal.

**NFL-SAFETY-002 (INVARIANT — MUST)** — Batas MPO MUST berdasarkan standar keselamatan akustik yang diakui. *[Referensi standar spesifik — misalnya IEC 60118 atau yang setara — MUST ditentukan melalui review audiologi sebelum implementasi. Dokumen standar target: NFL Safety Specification.]*

**NFL-SAFETY-003 (MUST)** — Apabila terjadi kegagalan komponen DSP, sistem MUST fallback ke safe state yang tidak menghasilkan output akustik berlebihan. Kegagalan MUST NOT mengakibatkan amplifikasi tak terbatas.

**NFL-SAFETY-004 (MUST)** — Sistem MUST mendeteksi dan menangani kondisi feedback yang berpotensi berbahaya (acoustic howling) dengan cara yang mencegah kerusakan pendengaran.

**NFL-SAFETY-005 (MUST)** — Startup sequence MUST memastikan tidak ada burst output yang tiba-tiba saat perangkat dinyalakan. Output MUST ramp up secara terkontrol.

**NFL-SAFETY-006 (MUST)** — Seluruh nilai batas MPO yang dikonfigurasi dalam Hearing Profile MUST divalidasi terhadap batas maksimum absolut yang terdefinisi dalam firmware dan MUST NOT dapat melebihinya melalui konfigurasi profil apapun.

### 11.2 Electrical Safety

**NFL-SAFETY-010 (MUST)** — Desain hardware MUST memenuhi regulasi keamanan elektrikal yang berlaku di jurisdiksi target produksi dan distribusi. *[Regulasi spesifik ditentukan per jurisdiksi; NFL mendefinisikan requirement process, bukan regulasi spesifik.]*

**NFL-SAFETY-011 (MUST)** — Charging circuit (jika ada) MUST mengimplementasikan proteksi overcharge, overdischarge, overcurrent, dan short circuit.

**NFL-SAFETY-012 (MUST)** — Desain thermal MUST mencegah permukaan perangkat mencapai suhu yang dapat menyebabkan luka bakar pada kontak normal dengan kulit.

### 11.3 Software Safety

**NFL-SAFETY-020 (MUST)** — Safety-critical paths dalam firmware (MPO limiter, audio cutoff, emergency mute) MUST diimplementasikan dengan cara yang meminimalkan kemungkinan kegagalan akibat bug pada komponen non-kritis.

**NFL-SAFETY-021 (MUST)** — Watchdog timer MUST diimplementasikan dan MUST aktif dalam mode operasi normal.

**NFL-SAFETY-022 (MUST)** — Failure mode setiap komponen sistem MUST terdokumentasi beserta perilaku sistem saat komponen tersebut gagal.

**NFL-SAFETY-023 (MUST)** — Test suite MUST mencakup test untuk seluruh safety-critical paths.

---

## Bagian 12: Requirement Privasi

### 12.1 Privacy by Design

**NFL-PRIV-001 (INVARIANT — MUST)** — Fungsi utama NFL (audio processing, profile management, device configuration) MUST beroperasi sepenuhnya offline tanpa koneksi internet.

**NFL-PRIV-002 (MUST)** — NFL MUST NOT mengirimkan data audio pengguna ke server eksternal tanpa persetujuan eksplisit yang jelas dan terdokumentasi.

**NFL-PRIV-003 (MUST)** — Data audiogram dan Hearing Profile pengguna MUST disimpan secara lokal by default.

**NFL-PRIV-004 (MUST)** — Apabila fitur opsional memerlukan koneksi jaringan, fitur tersebut MUST dapat dinonaktifkan tanpa mengorbankan fungsi utama perangkat.

**NFL-PRIV-005 (MUST)** — NFL MUST NOT mengimplementasikan analytics telemetry yang mengirim data ke server tanpa persetujuan eksplisit.

**NFL-PRIV-006 (MUST)** — Firmware dan aplikasi host MUST dapat diaudit komunitasnya untuk memverifikasi kepatuhan terhadap requirement privasi. Source code MUST terbuka sepenuhnya.

**NFL-PRIV-007 (SHOULD)** — Data Hearing Profile yang tersimpan di perangkat SHOULD dilindungi dari akses tidak terotorisasi melalui enkripsi atau access control yang sesuai dengan kemampuan hardware.

---

## Bagian 13: Requirement Interoperabilitas

### 13.1 Profile Interoperability

**NFL-COMP-001 (MUST)** — Hearing Profile yang dibuat pada perangkat NFL X MUST dapat dimuat dan berfungsi pada perangkat NFL Y yang mendukung versi schema profile yang sama, tanpa modifikasi manual.

**NFL-COMP-002 (MUST)** — NFL Profile Schema MUST bersifat versioned. Setiap versi schema MUST terdokumentasi dengan jelas perbedaannya dari versi sebelumnya.

**NFL-COMP-003 (MUST)** — Firmware MUST menolak memuat profile dengan versi schema yang tidak dikenali dengan pesan error yang jelas, dan MUST NOT mencoba parsing profile tersebut secara ad-hoc.

**NFL-COMP-004 (SHOULD)** — Firmware SHOULD mendukung backward compatibility untuk setidaknya satu major version schema sebelumnya.

### 13.2 Protocol Interoperability

**NFL-COMP-010 (MUST)** — Seluruh implementasi protocol NFL MUST mengikuti NFL Protocol Specification dan MUST dapat berkomunikasi satu sama lain.

**NFL-COMP-011 (MUST)** — Protocol NFL MUST bersifat versioned. Versi protocol MUST dinegosiasikan saat koneksi pertama kali dibuat.

**NFL-COMP-012 (MUST)** — Setiap aplikasi host pihak ketiga yang mengimplementasikan NFL Protocol secara benar MUST dapat berkomunikasi dengan seluruh perangkat NFL.

### 13.3 Hardware Interoperability

**NFL-COMP-020 (INVARIANT)** — NFL-compatible hardware dari vendor berbeda MUST dapat menggunakan Hearing Profile yang sama, menggunakan aplikasi host yang sama, dan mengikuti protokol update yang sama, tanpa modifikasi pada standar NFL.

**NFL-COMP-021 (MUST)** — NFL MUST menyediakan conformance test suite yang memungkinkan hardware implementer memverifikasi bahwa implementasi mereka memenuhi NFL interoperability requirements.

---

## Bagian 14: Requirement Open Source dan Governance

### 14.1 Open Source Requirements

**NFL-OS-001 (INVARIANT — MUST)** — Seluruh komponen core NFL (firmware, software/DSP, hardware reference design, dokumentasi, schemas) MUST bersifat open source dengan lisensi yang memenuhi definisi Open Source Initiative atau Open Hardware.

**NFL-OS-002 (INVARIANT — MUST)** — Lisensi yang ditargetkan:

| Domain | Lisensi Target |
|---|---|
| Firmware | GPL-3.0 |
| Software / DSP | GPL-3.0 |
| Hardware Design | CERN-OHL-S v2 |
| Dokumentasi | CC BY-SA 4.0 |
| Schemas | Akan ditentukan (MUST bersifat permissive) |

**NFL-OS-003 (MUST)** — Pilihan lisensi MUST konsisten dengan tujuan memastikan bahwa modifikasi tetap open source (copyleft) sekaligus memungkinkan penggunaan oleh komunitas, NGO, dan produser kecil.

**NFL-OS-004 (MUST)** — Seluruh komponen third-party yang digunakan MUST memiliki lisensi yang kompatibel dan MUST terdokumentasi dalam NOTICE file.

### 14.2 Governance

**NFL-GOV-001 (MUST)** — NFL MUST memiliki GOVERNANCE.md yang mendokumentasikan proses pengambilan keputusan, proses perubahan standar, dan mekanisme resolusi konflik.

**NFL-GOV-002 (MUST)** — Perubahan pada NFL Standards dan Schemas yang berpotensi breaking MUST melalui proses review yang terdokumentasi sebelum diterima.

**NFL-GOV-003 (MUST)** — Setiap kontributor MUST dapat memahami proses berkontribusi melalui CONTRIBUTING.md tanpa perlu bertanya secara langsung kepada maintainer.

**NFL-GOV-004 (MUST)** — NFL MUST memiliki CODE_OF_CONDUCT.md yang berlaku untuk seluruh ruang komunitas proyek.

**NFL-GOV-005 (MUST)** — NFL MUST memiliki SECURITY.md yang menjelaskan proses pelaporan vulnerability secara responsible disclosure.

### 14.3 Aturan Perubahan terhadap PRD Ini

**NFL-GOV-010 (MUST)** — PRD ini adalah dokumen hidup yang MUST dirawat seiring perkembangan proyek.

**NFL-GOV-011 (MUST)** — Perubahan pada requirement MUST (termasuk penambahan, perubahan, penghapusan) MUST melalui review yang didokumentasikan dan MUST menghasilkan bump pada versi PRD.

**NFL-GOV-012 (MUST)** — Perubahan pada INVARIANT memerlukan justifikasi yang sangat kuat karena mengubah prinsip fundamental proyek.

**NFL-GOV-013 (MUST)** — Setiap perubahan MUST mencatat alasan perubahan, pihak yang menyetujui, dan dampaknya terhadap sub-dokumen teknis yang sudah ada.

**NFL-GOV-014 (MUST)** — Apabila terjadi konflik antara PRD ini dan sub-dokumen teknis apapun, PRD ini adalah otoritas tertinggi sampai PRD diubah melalui proses yang sah.

---

## Bagian 15: Requirement Dokumentasi

### 15.1 Documentation Requirements

**NFL-DOC-001 (MUST)** — NFL MUST menyediakan dokumentasi yang memadai sehingga seseorang dengan latar belakang engineering yang sesuai dapat:

- Memahami arsitektur sistem secara keseluruhan.
- Membangun firmware dari source code.
- Membangun hardware dari reference design.
- Mengembangkan aplikasi host yang kompatibel.
- Menulis test yang memverifikasi conformance.

**NFL-DOC-002 (MUST)** — Setiap domain (firmware, software/DSP, hardware, docs root) MUST memiliki README yang menjadi entry point dan memberikan orientasi ke dokumentasi lebih detail.

**NFL-DOC-003 (MUST)** — Seluruh NFL Standards dan Schemas MUST terdokumentasi dalam bahasa yang tidak ambigu.

**NFL-DOC-004 (MUST)** — Dokumentasi build dan porting MUST cukup detail untuk mereproduksi environment development tanpa bergantung pada pengetahuan tidak terdokumentasi.

**NFL-DOC-005 (SHOULD)** — Dokumentasi SHOULD tersedia dalam bahasa Inggris sebagai bahasa universal teknis. Terjemahan ke bahasa lain adalah SHOULD, bukan MUST, dan komunitas MAY berkontribusi terjemahan.

**NFL-DOC-006 (MUST)** — Dokumentasi hardware MUST mencakup prosedur pengujian yang dapat diverifikasi, bukan hanya deskripsi desain.

**NFL-DOC-007 (MUST)** — Seluruh perubahan pada API publik, protocol, atau schema MUST direfleksikan dalam dokumentasi sebelum release.

---

## Bagian 16: Requirement Testing dan Validasi

### 16.1 Testing Strategy

**NFL-VAL-001 (MUST)** — NFL MUST mengimplementasikan strategi pengujian yang mencakup empat level:

1. **Unit Testing** — Pengujian komponen individual secara terisolasi.
2. **Integration Testing** — Pengujian interaksi antara komponen dalam satu domain.
3. **System Testing** — Pengujian pipeline end-to-end termasuk lintas domain.
4. **Conformance Testing** — Pengujian bahwa implementasi memenuhi NFL Standard.

**NFL-VAL-002 (MUST)** — Unit test dan simulator-based integration test MUST dapat dijalankan dalam CI tanpa hardware fisik.

**NFL-VAL-003 (MUST)** — Seluruh safety requirements (Bagian 11) MUST memiliki test yang secara eksplisit memverifikasi pemenuhannya.

**NFL-VAL-004 (MUST)** — Seluruh requirement yang memiliki angka terukur (latency, THD+N, dll.) MUST memiliki benchmark yang dapat memverifikasi angka tersebut secara otomatis.

**NFL-VAL-005 (MUST)** — NFL MUST menyediakan conformance test suite yang dapat digunakan oleh implementer hardware pihak ketiga untuk memverifikasi kompatibilitas.

**NFL-VAL-006 (MUST)** — Regresi pada DSP pipeline MUST terdeteksi oleh test suite. Ini mencakup perubahan pada frequency response, gain, dan timing.

### 16.2 Validation Strategy

**NFL-VAL-010 (MUST)** — Validasi NFL terdiri dari tiga tahap yang MUST dilalui untuk setiap release major:

```
SIMULATION VALIDATION
      ↓
ELECTRONIC BENCHMARK (hardware referensi)
      ↓
ACOUSTIC VALIDATION (pengukuran akustik fisik)
```

**NFL-VAL-011 (TARGET)** — Acoustic validation SHOULD dilakukan menggunakan peralatan pengukuran akustik yang mengikuti standar yang diakui. *[Standar spesifik ditentukan dalam NFL Testing & Validation Specification.]*

**NFL-VAL-012 (MUST)** — Seluruh hasil benchmark dan validation MUST disimpan dan dapat ditelusuri ke versi release yang spesifik.

### 16.3 Definition of Compliance

**NFL-VAL-020 (INVARIANT)** — Sebuah implementasi HANYA dapat diklaim sebagai "NFL-compliant" atau "NFL-compatible" apabila:

1. Memenuhi seluruh requirement MUST dalam PRD ini.
2. Telah melewati NFL Conformance Test Suite secara lengkap.
3. Hasil conformance testing tersedia dan dapat diverifikasi publik (untuk implementasi yang mengklaim kompatibilitas ke ekosistem).

**NFL-VAL-021 (MUST)** — Implementasi yang hanya memenuhi sebagian requirement MUST NOT menggunakan label "NFL-compatible" tanpa kualifikasi yang jelas tentang subset yang dipenuhi.

**NFL-VAL-022 (MUST)** — NFL Conformance Test Suite MUST bersifat open source dan dapat dijalankan oleh siapapun.

### 16.4 Failure Criteria

**NFL-VAL-030 (MUST)** — Kondisi berikut adalah FAILURE yang MUST mencegah release atau klaim compliance:

- Pelanggaran safety requirements (NFL-SAFETY-001 sampai NFL-SAFETY-023).
- Audio output melebihi batas MPO yang ditetapkan dalam kondisi apapun.
- Pelanggaran privacy requirements inti (NFL-PRIV-001 sampai NFL-PRIV-006).
- Kegagalan boot atau audio dalam kondisi normal.
- Kegagalan rollback saat diperlukan.
- Pelanggaran memory safety yang dapat menyebabkan undefined behavior pada safety-critical paths.

---

## Bagian 17: Cost dan Affordability Requirements

**NFL-COST-001 (TARGET)** — NFL MUST berkomitmen bahwa affordability adalah requirement desain, bukan aspirasi. Setiap keputusan desain yang secara signifikan meningkatkan biaya tanpa justifikasi performa atau safety MUST direview.

**NFL-COST-002 (MUST)** — BOM reference design MUST menggunakan komponen yang tersedia dari multiple supplier tanpa lock-in ke distributor tunggal.

**NFL-COST-003 (MUST)** — Komponen yang memerlukan NDA atau agreement khusus dengan vendor MUST NOT digunakan dalam reference design.

**NFL-COST-004 (TARGET)** — Target biaya BOM akan ditentukan dan dinyatakan secara formal dalam Hardware Specification setelah riset supply chain dan validasi. PRD ini tidak menetapkan angka spesifik untuk menghindari target yang tidak realistis atau menyesatkan.

**NFL-COST-005 (SHOULD)** — Reference design SHOULD mempertimbangkan kemudahan dan biaya assembly untuk produksi skala kecil (tidak hanya optimasi untuk mass production).

---

## Bagian 18: Traceability Model

### 18.1 Requirement Traceability

**NFL-TRACE-001 (MUST)** — Setiap requirement dalam PRD ini yang memiliki ID NFL-* MUST dapat ditelusuri ke:

1. Sub-dokumen teknis yang mengimplementasikan atau mendetailkan requirement tersebut.
2. Test atau benchmark yang memverifikasi pemenuhannya.
3. Bukti validasi (hasil test, measurement) pada setiap release.

**NFL-TRACE-002 (MUST)** — Sub-dokumen teknis MUST mereferensikan ID requirement PRD yang relevan sehingga traceability dapat diverifikasi.

**NFL-TRACE-003 (SHOULD)** — NFL SHOULD memelihara traceability matrix yang memetakan NFL-REQ-* → implementasi → test → validasi.

### 18.2 Sub-dokumen Teknis

PRD ini adalah induk dari sub-dokumen berikut. Setiap sub-dokumen mendetailkan requirement untuk domain spesifik sambil tetap tunduk pada PRD sebagai otoritas tertinggi:

| Sub-dokumen | Requirement PRD yang Dirujuk |
|---|---|
| Firmware Specification | NFL-FW-*, NFL-ARCH-*, NFL-SAFETY-* (fw) |
| Software/DSP Specification | NFL-DSP-*, NFL-AUDIO-*, NFL-ARCH-* (sw) |
| Hardware Specification | NFL-HW-*, NFL-SAFETY-* (hw), NFL-COST-* |
| Audio/DSP Specification | NFL-AUDIO-*, NFL-DSP-*, NFL-PERF-* |
| Protocol Specification | NFL-REQ-040:044, NFL-COMP-010:012 |
| Profile Specification | NFL-REQ-010:015, NFL-COMP-001:004 |
| Safety Specification | NFL-SAFETY-001:023 |
| Testing & Validation Specification | NFL-VAL-001:030, NFL-TEST-001:004 |
| Privacy Specification | NFL-PRIV-001:007 |
| Manufacturing Specification | NFL-HW-020:024, NFL-HW-032, NFL-COST-* |

---

## Bagian 19: Versi dan Changelog PRD

| Versi | Tanggal | Perubahan |
|---|---|---|
| 0.1 | 2025 | Draft awal. Seluruh requirement berstatus draft sampai review engineering dan audiologi. |

**NFL-GOV-020 (MUST)** — PRD ini MUST dinyatakan sebagai versi final (1.0) hanya setelah:

1. Review oleh setidaknya satu engineer firmware embedded.
2. Review oleh setidaknya satu engineer DSP atau signal processing.
3. Review terkait safety acoustic oleh setidaknya satu audiolog atau profesional yang qualified.
4. Review lisensi open source.
5. Seluruh requirement TARGET yang memiliki angka telah divalidasi atau dinyatakan secara eksplisit sebagai TARGET pending validasi.

---

## Ringkasan Prinsip Tertinggi

**INVARIANT yang tidak dapat dikompromikan:**

1. Mendengar adalah hak semua orang — affordability adalah requirement desain.
2. Contract over Component — NFL mendefinisikan interface, bukan implementasi.
3. Privacy by default — fungsi utama HARUS offline.
4. Safety first — MPO limiter tidak dapat dinonaktifkan pengguna.
5. Keterbukaan penuh — source, hardware, dokumentasi semuanya harus open.
6. Pengetahuan tidak terkunci — dokumentasi harus cukup untuk reproduksi mandiri.
7. PRD ini adalah konstitusi — konflik dengan sub-dokumen diselesaikan oleh PRD.

---

*Dokumen ini adalah versi 0.1 — draft untuk review. Angka kuantitatif yang ditandai TARGET memerlukan validasi engineering dan audiologi sebelum dapat diperlakukan sebagai MUST. Seluruh INVARIANT berlaku sejak versi ini.*
