# Proyek Akhir: Menyelesaikan Permasalahan Perusahaan Edutech

## Business Understanding

Jaya Jaya Maju adalah perusahaan multinasional yang berdiri sejak tahun 2000 dan memiliki lebih dari 1000 karyawan yang tersebar di seluruh penjuru negeri.
Walaupun telah berkembang menjadi perusahaan besar, Jaya Jaya Maju menghadapi tantangan serius dalam mengelola karyawan, terutama terkait dengan tingginya attrition rate (rasio keluar masuk karyawan) yang mencapai lebih dari 10%.
Masalah ini berdampak pada biaya rekrutmen yang meningkat, menurunnya produktivitas tim, dan terganggunya operasional perusahaan.

### Permasalahan Bisnis

- Tingginya attrition rate di perusahaan (>10%).

- Belum adanya identifikasi faktor-faktor utama yang menyebabkan karyawan keluar.

- Kurangnya alat monitoring untuk memantau faktor-faktor penyebab attrition secara real-time.

### Cakupan Proyek

- Melakukan eksplorasi dan analisis data untuk memahami faktor-faktor attrition.

- Mengembangkan model klasifikasi untuk memprediksi kemungkinan karyawan keluar.

- Membangun business dashboard untuk monitoring attrition dan hasil prediksi.

- Memberikan rekomendasi strategi berbasis data untuk menurunkan attrition.

### Persiapan

**Sumber data:**   
Dataset internal dari perusahaan Jaya Jaya Maju (tautan: [Jaya Jaya Maju](https://github.com/dicodingacademy/dicoding_dataset/blob/main/employee/employee_data.csv)).

**Setup environment:**

```
# 1. Salin Repository dari GitHub
git clone https://github.com/username/nama-repository.git

# 2. Pindah ke Folder Proyek
cd nama-repository

# 3. Membuat Virtual Environment Baru dengan Conda
conda create -n env-attrition python=3.10

# 4. Mengaktifkan Virtual Environment
conda activate env-attrition

# 5. Instalasi Library yang Dibutuhkan
pip install pandas numpy matplotlib seaborn scikit-learn streamlit

# 6. Menonaktifkan Virtual Environment Setelah Selesai
conda deactivate
```

**Run prediction.py**

```
python prediction.py
```

**Setup Dashboard Metabase:**

```
# 1. Download Docker Image untuk Metabase
docker pull metabase/metabase:v0.46.4

# 2. Jalankan Metabase di Container Baru
docker run -p 3000:3000 --name metabase metabase/metabase

# 3. Akses Metabase dari Browser
http://localhost:3000

# 4. Login dengan akun berikut:
Username: rahmadlaska11@gmail.com  
Password: rahmad12
```


## Business Dashboard

Link Dashboard : [Attrition Analysis Dashboard](http://localhost:3000/public/dashboard/fd440be8-ed47-4a23-8e04-8e253cab6805)

**Dashboard Preview**

![HR Dashboard](https://github.com/rmdlaska11/Employee-Attrition-Analysis/blob/main/Dashboard.png)

Dashboard ini bertujuan untuk membantu tim HR dalam memahami dan memonitor attrition (tingkat keluar masuknya karyawan) di perusahaan.
Berikut fitur dan elemen yang terdapat dalam dashboard:

- **Filter Dinamis**  
  Terdapat filter berdasarkan Department, Gender, Education Field, Marital Status, Over Time, dan Age, sehingga pengguna dapat melakukan analisis lebih spesifik pada segmen tertentu.
  
- **Ringkasan Utama (KPI Cards)**
  - Total Employees: 1,470 orang.
  - Average Monthly Income: $6.5k.
  - Average Years at Company: 7.01 tahun.
  - Total Over Time: 416 orang yang pernah kerja lembur.
    
- **Visualisasi Attrition**
  - Attrition Rate: Menampilkan persentase karyawan yang keluar (Yes) dan yang tetap bertahan (No).
  - Attrition By Gender: Menunjukkan distribusi attrition berdasarkan jenis kelamin.
  - Attrition By OverTime: Membandingkan attrition antara karyawan yang sering lembur dan yang tidak.
  - Attrition By Department: Menampilkan jumlah attrition di tiap departemen seperti Research & Development, Sales, dan Human Resources.
  - Attrition By Job Satisfaction: Menggambarkan hubungan antara tingkat kepuasan kerja dengan attrition.
  - Attrition By Age: Menunjukkan usia-usia karyawan yang lebih rentan mengalami attrition.
  - Attrition By Monthly Income: Melihat hubungan antara tingkat gaji dengan tingkat keluarnya karyawan.
  - Attrition By Years at Company: Memetakan attrition berdasarkan lama masa kerja.

**Manfaat Dashboard:**  
Dashboard ini memberikan wawasan cepat kepada manajemen untuk:

- Mengidentifikasi faktor risiko attrition.
- Melihat tren attrition di berbagai kelompok karyawan.
- Membantu membuat keputusan strategis berbasis data untuk menekan turnover.

## Model Machine Learning
Untuk membantu memprediksi kemungkinan seorang karyawan meninggalkan perusahaan, dibangunlah model machine learning berbasis data historis. Dua algoritma utama yang digunakan dalam proyek ini adalah **Support Vector Machine (SVM)** dan **Naive Bayes (NB)**. Model dilatih pada data karyawan eksisting untuk kemudian digunakan dalam memprediksi potensi attrition di masa depan.

### Perbandingan Model
Kinerja dari masing-masing model dievaluasi menggunakan beberapa metrik, yaitu akurasi, presisi, recall, dan skor F1. Berikut ringkasan hasil evaluasinya:

| Model               | Akurasi   | Presisi  | Recall   | Skor F1   |
|---------------------|-----------|----------|----------|-----------|
| SVM                 | 0.8553    | 0.8769   | 0.8553   | 0.8092    |
| NB                  | 0.7956    | 0.8332   | 0.7956   | 0.8094    |

**Model Terbaik**  
Berdasarkan hasil evaluasi, **Support Vector Machine (SVM)** dipilih sebagai model yang paling optimal. SVM berhasil mencatat akurasi tertinggi sebesar 85.56% serta presisi, recall, dan F1-Score yang lebih unggul dibandingkan model lainnya. Selain itu, model ini dinilai lebih efektif dalam mengidentifikasi faktor-faktor penting yang berkontribusi terhadap risiko karyawan keluar.

### Hasil Prediksi Model
Berikut contoh hasil inferensi model SVM terhadap beberapa data karyawan:

| EmployeeId | Prediksi | Nilai Asli |
|------------|----------|------------|
| 629        | 0.00     | 0.00       |
| 403        | 0.00     | 1.00       |
| 444        | 0.00     | 0.00       |
| 41         | 0.00     | 0.00       |
| 589        | 0.00     | 1.00       |
| 275        | 0.00     | 0.00       |
| 665        | 0.00     | 1.00       |
| 245        | 0.00     | 0.00       |
| 699        | 0.00     | 0.00       |
| 820        | 0.00     | 0.00       |

### **Feature Importance based on Permutation Importance**

![Feature Importance Plot](https://github.com/rmdlaska11/Employee-Attrition-Analysis/blob/main/Feature%20Importance.png)

Berdasarkan analisis Permutation Feature Importance, faktor-faktor utama yang berkontribusi terhadap tingginya attrition rate di perusahaan Jaya Jaya Maju adalah:
- OverTime: Karyawan yang sering bekerja lembur cenderung memiliki risiko resign lebih tinggi.
- Marital Status: Status pernikahan mempengaruhi keputusan karyawan untuk bertahan atau keluar.
- Job Satisfaction: Tingkat kepuasan kerja memiliki pengaruh signifikan terhadap attrition.

Faktor lain seperti Age, Stock Option Level, Job Level, dan Relationship Satisfaction juga memberikan kontribusi, meskipun dalam tingkat sedang.

Sementara itu, faktor-faktor seperti Performance Rating, Education Field, dan Standard Hours memiliki pengaruh yang sangat kecil terhadap keputusan resign.

## Conclusion
Melalui pembangunan model machine learning dan analisis business dashboard, diperoleh beberapa kesimpulan penting terkait faktor yang mempengaruhi attrition karyawan di Jaya Jaya Maju.

**Dari sisi model machine learning:**  
Support Vector Machine (SVM) terpilih sebagai model terbaik dengan akurasi mencapai **85.53%**. Model ini mampu mengenali pola-pola penting dari karakteristik karyawan yang berisiko keluar, terutama faktor **OverTime**, **Marital Status**, **Job Satisfaction** dan **Age** . Dengan model ini, perusahaan dapat secara proaktif mengidentifikasi dan mempertahankan karyawan berisiko.

**Berdasarkan analisis dashboard, ditemukan beberapa insight utama:**
- **Departemen dengan *attrition* tertinggi:**
  - Research & Development
  - Sales

- **Job Satisfaction:**  
  Mayoritas karyawan yang keluar memiliki kepuasan kerja di tingkat *low* hingga *medium*

- **Rentang Usia:**  
  Karyawan usia 25–35 tahun mengalami tingkat *attrition* paling tinggi.

- **Pendapatan Bulanan:**  
  Karyawan dengan gaji < $5,000 mengalami tingkat keluar yang lebih tinggi dibandingkan kelompok pendapatan lainnya.

- **Masa Kerja:**  
  Karyawan yang keluar umumnya baru bekerja kurang dari 3 tahun di perusahaan.

**Kesimpulannya**, faktor-faktor kerja, demografis, dan finansial memainkan peran penting dalam keputusan karyawan untuk tetap bertahan atau keluar dari perusahaan.
Strategi retensi berbasis data sangat diperlukan untuk mengatasi permasalahan ini dan meningkatkan stabilitas tenaga kerja ke depannya.

## Rekomendasi Action Items

Berikut rekomendasi langkah konkret untuk perusahaan:

- **Perbaiki Program Retensi Karyawan Baru:**  
  Fokus pada 0–3 tahun masa kerja dengan program mentoring, engagement, dan onboarding yang lebih intensif.

- **Evaluasi Skema Gaji dan Benefit:**  
  Tinjau kembali paket kompensasi untuk kelompok karyawan dengan pendapatan rendah untuk meningkatkan loyalitas.

- **Tingkatkan Kepuasan Kerja:**  
  Lakukan survey kepuasan kerja reguler, terutama di departemen R&D dan Sales, dan implementasikan perbaikan berbasis hasil survey.

- **Kebijakan Overtime:**  
  Analisis lebih lanjut pengaruh lembur terhadap attrition, dan sesuaikan kebijakan lembur untuk menjaga keseimbangan kerja dan kehidupan karyawan.

- **Monitoring Berkelanjutan:**  
  Gunakan dashboard yang sudah dibuat untuk memonitor perkembangan *attrition* secara rutin, dan cepat ambil tindakan bila terlihat tren negatif.

