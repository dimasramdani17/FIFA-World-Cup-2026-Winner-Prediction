# ⚽ Prediksi Juara FIFA World Cup 2026 Menggunakan Random Forest

## 📌 Project Overview

FIFA World Cup merupakan kompetisi sepak bola terbesar di dunia yang mempertemukan tim nasional terbaik dari berbagai negara. Menentukan kandidat juara sebelum turnamen berlangsung merupakan tantangan yang menarik karena dipengaruhi oleh berbagai faktor seperti FIFA Ranking, Elo Rating, performa pertandingan, serta statistik historis tim.

Dengan memanfaatkan Machine Learning, data historis dapat digunakan untuk menemukan pola yang berkaitan dengan keberhasilan suatu negara menjadi juara dunia. Pada proyek ini dibangun model klasifikasi menggunakan algoritma **Random Forest** untuk memprediksi peluang suatu negara menjadi juara FIFA World Cup 2026.

---

## 🎯 Business Understanding

### Problem Statements

1. Faktor apa saja yang mempengaruhi peluang suatu negara menjadi juara FIFA World Cup?
2. Apakah data historis FIFA Ranking dan Elo Rating dapat digunakan untuk memprediksi juara dunia?
3. Negara mana yang memiliki peluang terbesar menjadi juara FIFA World Cup 2026?

### Goals

1. Mengidentifikasi faktor-faktor yang mempengaruhi peluang juara dunia.
2. Membangun model Machine Learning untuk memprediksi juara FIFA World Cup.
3. Menghasilkan prediksi kandidat juara FIFA World Cup 2026 berdasarkan data terbaru.

### Solution Approach

Pendekatan yang digunakan dalam proyek ini adalah **Supervised Learning** dengan algoritma **Random Forest Classifier**.

Alasan pemilihan Random Forest:

- Mampu menangani hubungan non-linear antar fitur.
- Memiliki performa yang baik pada data tabular.
- Mengurangi risiko overfitting.
- Menyediakan informasi Feature Importance untuk interpretasi model.

---

## 📊 Data Understanding

### Dataset

Proyek ini menggunakan tiga dataset utama:

#### 1. WC.csv

Dataset historis FIFA World Cup yang berisi informasi negara juara pada setiap edisi Piala Dunia.

#### 2. fifa_ranking_2026.csv

Dataset ranking FIFA terbaru yang digunakan untuk menggambarkan kekuatan tim nasional berdasarkan peringkat resmi FIFA.

#### 3. elo_ratings_wc2026.csv

Dataset Elo Rating yang berisi statistik performa tim nasional seperti rating, kemenangan, kekalahan, jumlah gol, dan statistik lainnya.

---

### Informasi Dataset

| Dataset | Jumlah Data | Jumlah Fitur |
|----------|----------|----------|
| WC.csv | 20 | 10 |
| fifa_ranking_2026.csv | 211 | 8 |
| elo_ratings_wc2026.csv | 4683 | 23 |

---

### Variabel yang Digunakan

| Variabel | Deskripsi |
|----------|----------|
| rank | Ranking FIFA |
| rating | Elo Rating |
| wins | Jumlah kemenangan |
| draws | Jumlah hasil imbang |
| losses | Jumlah kekalahan |
| goals_for | Jumlah gol yang dicetak |
| goals_against | Jumlah gol yang kebobolan |
| target | Label juara (1) dan bukan juara (0) |

---

## 🔍 Exploratory Data Analysis (EDA)

### Missing Value Analysis

Pemeriksaan missing value dilakukan untuk memastikan kualitas data sebelum digunakan dalam proses pemodelan.

**Hasil:**

- Tidak ditemukan missing value pada fitur yang digunakan.
- Dataset siap digunakan untuk tahap selanjutnya.

<img width="173" height="640" alt="image" src="https://github.com/user-attachments/assets/f30ae33a-387a-4b94-9ae4-53c0256d9154" />


---

### Distribusi Elo Rating

Gambar histogram Elo Rating.

<img width="558" height="378" alt="image" src="https://github.com/user-attachments/assets/52bdf8a8-9c23-4434-ab3a-68a001fa18e0" />


**Insight:**

Distribusi Elo Rating menunjukkan bahwa sebagian besar negara berada pada rentang rating menengah, sedangkan hanya sedikit negara yang memiliki Elo Rating sangat tinggi.

---

### Top FIFA Ranking

Hasil Top FIFA Ranking.

<img width="635" height="279" alt="image" src="https://github.com/user-attachments/assets/a74222d7-2ba5-4b06-980d-6d18ad47d949" />


**Insight:**

Negara dengan ranking FIFA terbaik cenderung menjadi kandidat kuat dalam kompetisi internasional.

---

### Top Elo Rating

Hasil Top Elo Rating.

<img width="1402" height="298" alt="image" src="https://github.com/user-attachments/assets/300233d0-bd6e-494d-ade2-ba11876375a5" />


**Insight:**

Negara dengan Elo Rating tinggi menunjukkan performa historis yang lebih konsisten dibandingkan negara lain.

---

## 🛠 Data Preparation

Tahapan data preparation yang dilakukan meliputi:

### 1. Data Cleaning

Melakukan penyamaan nama negara yang memiliki penulisan berbeda.

<img width="303" height="79" alt="image" src="https://github.com/user-attachments/assets/deb9d261-25b7-47f6-9721-02496c7acfd2" />


---

### 2. Pembuatan Target

Target dibuat berdasarkan data juara dunia historis.

| Kondisi | Target |
|----------|----------|
| Juara Dunia | 1 |
| Bukan Juara Dunia | 0 |

---

### 3. Feature Selection

Fitur yang digunakan dalam pemodelan:

```python
features = [
    'rank',
    'rating',
    'wins',
    'draws',
    'losses',
    'goals_for',
    'goals_against'
]
```

---

### 4. Train-Test Split

Dataset dibagi menjadi:

- Training Data : 80%
- Testing Data : 20%

---

### 5. Feature Scaling

Standarisasi dilakukan menggunakan StandardScaler untuk menyamakan skala seluruh fitur.

---

## 🤖 Modeling

### Random Forest Classifier

Model yang digunakan:

```python
RandomForestClassifier(
    n_estimators=200,
    random_state=42
)
```

Model dilatih menggunakan data training dan kemudian digunakan untuk melakukan prediksi pada data testing.

---

## 📈 Evaluation

### Metrik Evaluasi

Evaluasi model dilakukan menggunakan:

- Accuracy
- Precision
- Recall
- F1-Score
- Confusion Matrix

---

### Accuracy

Hasil evaluasi model:

```python
pred_rf = rf.predict(X_test)

acc_rf = accuracy_score(
    y_test,
    pred_rf
)
```



---

### Classification Report

```python
from sklearn.metrics import classification_report

print(classification_report(
    y_test,
    pred_rf
))
```
<img width="429" height="130" alt="image" src="https://github.com/user-attachments/assets/a4c13b6f-1384-437f-ab79-d85f0e1eeb22" />

---

### Confusion Matrix

Gambar confusion matrix.

<img width="445" height="345" alt="image" src="https://github.com/user-attachments/assets/e4129e89-6f18-4a82-9e33-0d309ae7451f" />


**Interpretasi:**

Confusion Matrix menunjukkan jumlah prediksi yang benar dan salah pada masing-masing kelas sehingga dapat digunakan untuk mengevaluasi performa model secara lebih detail.

---

### Feature Importance

Tambahkan grafik Feature Importance.

<img width="211" height="237" alt="image" src="https://github.com/user-attachments/assets/c5680a27-597e-4d74-9371-fa8653baffa0" />


**Interpretasi:**

Fitur dengan nilai importance tertinggi memiliki pengaruh terbesar terhadap peluang suatu negara menjadi juara dunia. Berdasarkan hasil model, Elo Rating dan FIFA Ranking merupakan faktor yang paling berpengaruh dalam proses prediksi.

---

## 🌎 Prediksi FIFA World Cup 2026

Setelah model selesai dilatih, dilakukan prediksi terhadap data peserta FIFA World Cup 2026.

### Top 10 Kandidat Juara

<img width="205" height="313" alt="image" src="https://github.com/user-attachments/assets/697be8e7-59d2-4ad2-871a-580fdaeeda97" />


---

### Insight Prediksi

Berdasarkan probabilitas yang dihasilkan oleh model Random Forest, negara-negara dengan Elo Rating tinggi, FIFA Ranking terbaik, serta performa pertandingan yang konsisten memiliki peluang terbesar untuk menjadi juara FIFA World Cup 2026.

---

## 🚀 Deployment

Model disimpan dalam format `.pkl` agar dapat digunakan kembali dalam aplikasi berbasis Streamlit.

### Struktur Proyek

```text
FIFA_World_Cup_2026_Prediction/
│
├── data/
│   ├── WC.csv
│   ├── fifa_ranking_2026.csv
│   └── elo_ratings_wc2026.csv
│
├── notebook/
│   └── FIFA_World_Cup_2026_Prediction.ipynb
│
├── deployment/
│   ├── app.py
│   ├── model.pkl
│   └── requirements.txt
│
├── results/
│   └── hasil_prediksi_wc2026.csv
│
└── README.md
```

---

## 🏆 Conclusion

Berdasarkan hasil pemodelan menggunakan algoritma Random Forest, model berhasil digunakan untuk memprediksi peluang suatu negara menjadi juara FIFA World Cup.

Fitur yang paling berpengaruh terhadap prediksi adalah Elo Rating, FIFA Ranking, dan statistik performa pertandingan. Model kemudian digunakan untuk menghasilkan prediksi kandidat juara FIFA World Cup 2026 berdasarkan data terbaru yang tersedia.

Hasil prediksi menunjukkan bahwa negara-negara dengan performa historis kuat dan rating tinggi memiliki peluang terbesar untuk menjadi juara FIFA World Cup 2026.

---

## 👨‍💻 Author

**Nama:** Dimas Ramdani(2330511004) dan Muhamad Daffa(2330511024)   
**Program Studi:** Teknik Informatika
**Mata Kuliah:** Machine Learning  
**Tahun:** 2026
