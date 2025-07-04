
# Proyek Akhir: Menyelesaikan Permasalahan Human Resource JAYAJAYA MAJU

## Business Understanding

Perusahaan **"Jaya Jaya Maju"** menghadapi tantangan dalam mempertahankan karyawannya. Tingkat atrisi (perpindahan karyawan) yang tinggi menjadi perhatian utama manajemen karena dapat mengganggu operasional dan produktivitas perusahaan. Proyek ini bertujuan untuk menganalisis faktor-faktor utama yang menyebabkan atrisi karyawan dan memberikan rekomendasi strategis berbasis data untuk mengatasi masalah ini.

## Permasalahan Bisnis

Berdasarkan analisis awal, tingkat atrisi di perusahaan Jaya Jaya Maju saat ini adalah **16,92%**, yang melebihi ambang batas wajar sebesar **10%**. Permasalahan utama yang akan diselesaikan adalah:

- Mengidentifikasi faktor-faktor kunci yang paling signifikan yang mendorong karyawan untuk meninggalkan perusahaan.
- Merumuskan langkah-langkah yang dapat ditindaklanjuti untuk menekan angka atrisi.

## Cakupan Proyek

Cakupan dari proyek ini adalah sebagai berikut:

- Melakukan analisis data eksplorasi untuk memahami distribusi dan hubungan antar variabel dalam dataset karyawan.
- Menggunakan model **Random Forest Classifier** untuk mengidentifikasi dan mengukur tingkat kepentingan dari setiap fitur yang berpotensi mempengaruhi atrisi karyawan.
- Membuat visualisasi data untuk menyajikan faktor-faktor paling berpengaruh terhadap atrisi.
- Menyusun rekomendasi strategis yang dapat diimplementasikan oleh perusahaan untuk mengurangi tingkat atrisi.

## Persiapan

**Sumber data**: Dataset yang digunakan dalam proyek ini bersumber dari **Dicoding Employee Dataset** yang bisa diakses melaliu link berikut : https://github.com/dicodingacademy/dicoding_dataset/tree/main/employee

**Akun Metabase email**: root@mail.com, password: root123

Dataset ini berisi informasi demografis karyawan, metrik terkait pekerjaan, dan status atrisi.

**Setup environment**:

- **Instalasi Package via Requirements.txt**
  - **Setup Environment - Anaconda**
  ```conda create --name main-ds python=3.9
  conda activate main-ds
  pip install -r requirements.txt
  ```
  - **Setup Environment - Shell/Terminal**
  ```pip install pipenv
  pipenv install
  pipenv shell
  pip install -r requirements.txt
  ```

- **Akses Dashboard Metabase**
  **Prasyarat :**
    - [Docker](https://www.docker.com/products/docker-desktop/) terinstal dan sedang berjalan.
    - Repository ini telah di-clone ke mesin lokal Anda.

  Untuk mengakses dashboard yang telah dikonfigurasi, ikuti tahapan berikut:
  1.  **Clone Repository (jika belum)**
      ```bash
      git clone [URL_REPOSITORY_ANDA]
      cd [NAMA_DIREKTORI_PROYEK]
      ```

  2.  **Verifikasi File Database**
      Pastikan file database Metabase, yaitu `metabase.db.mv.db`, terdapat pada direktori utama proyek ini (direktori yang sama dengan file `readme.md` ini). File ini berisi semua konfigurasi, dashboard, dan pertanyaan yang telah dibuat.

  3.  **Jalankan Metabase via Docker**
      Buka terminal atau command prompt Anda, lalu jalankan perintah berikut. Perintah ini akan membuat container Docker untuk Metabase dan me-mounting file database lokal Anda ke dalamnya.

      ```bash
      docker run -d -p 3000:3000 \
        -v "$(pwd)/metabase.db.mv.db:/metabase.db/metabase.db.mv.db" \
        --name metabase-proyek \
        metabase/metabase
      ```
      **Catatan:**
      * `-d` menjalankan container di background.
      * `-p 3000:3000` memetakan port 3000 di mesin Anda ke port 3000 di dalam container.
      * `-v "$(pwd)/..."` adalah bagian terpenting. Ini menghubungkan file `metabase.db.mv.db` di direktori Anda saat ini ke lokasi database di dalam container.
      * `--name metabase-proyek` memberikan nama yang mudah diingat untuk container Anda.

  4.  **Tunggu Metabase Siap**
      Setelah menjalankan perintah di atas, Metabase memerlukan waktu sekitar 1-3 menit untuk proses inisialisasi. Anda bisa melihat log-nya dengan perintah:
      ```bash
      docker logs -f metabase-proyek
      ```
      Tunggu hingga Anda melihat pesan seperti `Metabase initialization COMPLETE`. Tekan `Ctrl + C` untuk keluar dari log.

  5.  **Akses Dashboard**
      Buka browser Anda dan kunjungi alamat berikut:
      [**http://localhost:3000**](http://localhost:3000)

  6.  **Login ke Metabase**
      Gunakan kredensial berikut untuk masuk dan melihat dashboard yang telah disiapkan.

      -   **Email:** `root@mail.com`
      -   **Password:** `root123`

## Business Dashboard

Dashboard attrition karyawan perusahaan **Jaya Jaya Maju** dikembangkan menggunakan **Metabase** untuk membantu tim manajemen dan HR memantau indikator-indikator utama terkait tingkat perpindahan karyawan (attrition) secara visual dan interaktif.

### Fitur Dashboard

Dashboard ini menyajikan beberapa visualisasi penting:

- **Tingkat Attrition Keseluruhan**  
  Menampilkan indikator utama attrition secara ringkas di tengah tampilan dashboard, yaitu **1.692%** dari total karyawan.

- **Top 10 Features Importance (Model Random Forest)**  
  Bar chart yang menunjukkan 10 fitur teratas yang paling berkontribusi terhadap prediksi attrition, termasuk:
  - MonthlyIncome
  - Age
  - DailyRate
  - DistanceFromHome
  - TotalWorkingYears
  - OverTime
  - YearsInCompany
  - WorkLifeBalance
  - EnvironmentSatisfaction

- **Attrition per Gaji (Monthly Income Bins)**  
  Histogram yang memperlihatkan hubungan antara kategori gaji dan jumlah kasus attrition. Terlihat bahwa kelompok pendapatan menengah memiliki angka attrisi yang cukup signifikan.

- **Job Satisfaction dan Environment Satisfaction**  
  Tabel pivot yang menampilkan jumlah karyawan berdasarkan kombinasi kepuasan kerja dan kepuasan lingkungan kerja. Ini membantu melihat korelasi antara kepuasan dan attrition.

- **Age vs MonthlyIncome vs Attrition**  
  Tabel interaktif yang menyajikan jumlah karyawan berdasarkan rentang umur dan pendapatan bulanan, disertai jumlah yang puas dalam pekerjaan. Ini mendukung identifikasi segmen karyawan dengan risiko tinggi attrition.

### Tujuan Penggunaan

Dashboard ini bertujuan untuk:
- Memberikan insight visual terhadap pola attrition berdasarkan faktor demografis dan pekerjaan.
- Mendukung keputusan strategis HR dalam mengurangi attrisi.
- Menyediakan data real-time yang dapat diakses dan dipahami oleh manajemen non-teknis.

### Screenshot

![Dashboard Attrition di Metabase](.Amelia gizzela_dashboard.png)


Untuk memonitor faktor-faktor yang mempengaruhi atrisi, sebuah business dashboard dapat dibuat. Dashboard ini akan berfungsi sebagai alat pemantauan bagi manajemen untuk melacak indikator-indikator kunci secara berkala.

Meskipun tautan ke dashboard interaktif tidak tersedia, dashboard ini akan memvisualisasikan beberapa metrik penting seperti:

- **Tingkat Atrisi Keseluruhan**: Menampilkan persentase atrisi saat ini.
- **Faktor Paling Berpengaruh**: Grafik yang menunjukkan fitur-fitur teratas yang mempengaruhi atrisi, seperti OverTime, MonthlyIncome, Age.
- **Atrisi Berdasarkan Jam Lembur (Overtime)**: Visualisasi perbandingan tingkat atrisi antara karyawan yang sering lembur dengan yang tidak.
- **Atrisi Berdasarkan Kepuasan Kerja dan Keseimbangan Hidup (JobSatisfaction & WorkLifeBalance)**: Grafik yang menunjukkan korelasi antara kepuasan dan keseimbangan hidup dengan atrisi.
- **Distribusi Pendapatan Bulanan (MonthlyIncome)**: Perbandingan pendapatan bulanan antara karyawan yang bertahan dan keluar.

Dashboard ini memungkinkan manajemen untuk secara proaktif mengidentifikasi tren negatif dan mengambil keputusan berbasis data untuk meningkatkan retensi karyawan.

## Conclusion

Analisis data menunjukkan bahwa tingkat atrisi sebesar **16,92%** didorong oleh beberapa faktor utama. Berdasarkan analisis **feature importance** menggunakan model Random Forest, fitur yang paling signifikan mempengaruhi keputusan karyawan untuk keluar adalah:

- **Lembur (OverTime)**: Karyawan yang bekerja lembur memiliki kecenderungan atrisi yang jauh lebih tinggi.
- **Pendapatan Bulanan (MonthlyIncome)**: Karyawan dengan pendapatan bulanan yang lebih rendah lebih mungkin untuk keluar.
- **Usia (Age)**: Karyawan yang lebih muda memiliki tingkat atrisi yang lebih tinggi.
- **Total Tahun Bekerja (TotalWorkingYears)**: Pengalaman kerja yang lebih singkat berkorelasi dengan atrisi yang lebih tinggi.
- **Jarak dari Rumah (DistanceFromHome)**: Jarak yang lebih jauh sedikit meningkatkan kemungkinan atrisi.

Faktor-faktor lain seperti **WorkLifeBalance** dan **JobSatisfaction** juga terbukti memiliki korelasi dengan tingkat atrisi.

## Rekomendasi Action Items

- **Membatasi dan Mengelola Jam Lembur**: Tingkat atrisi mencapai 40% pada karyawan yang bekerja lembur >6 jam/minggu. Disarankan untuk membatasi lembur maksimal 2 jam/minggu. Terapkan pemantauan lembur dan insentif bagi divisi yang berhasil menekan lembur tanpa mengorbankan produktivitas.
- **Meningkatkan Kepuasan Kerja**: Terapkan program engagement seperti sesi umpan balik rutin, pengembangan karir, dan kegiatan apresiasi.
- **Meninjau Struktur Kompensasi**: Lakukan kajian ulang terhadap struktur gaji, terutama untuk peran dengan tingkat atrisi tinggi.
