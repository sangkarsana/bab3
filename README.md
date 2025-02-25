# **Tahapan Pra-pemrosesan Data**

Tahap **pra-pemrosesan data** merupakan langkah esensial dalam memastikan bahwa dataset yang digunakan dalam penelitian memiliki kualitas yang baik, bersih, dan siap untuk dianalisis serta digunakan dalam pengembangan model **machine learning**. Proses ini melibatkan beberapa langkah utama, yaitu **pemisahan atribut**, **konversi tipe data**, **penanganan nilai hilang**, serta **normalisasi data**.

---

## **1. Pemisahan Atribut**
Dataset awal yang diperoleh memiliki struktur yang tidak terorganisir dengan baik, di mana seluruh atribut tersimpan dalam satu kolom dengan pemisah titik koma (`;`). Oleh karena itu, langkah pertama yang dilakukan adalah **memisahkan atribut-atribut tersebut ke dalam kolom yang sesuai**. Sebelum dilakukan pemisahan, data memiliki format sebagai berikut:

**Contoh data sebelum pemrosesan:**
```
"120.0;0.0;0.0;0.0;0.0;0.0;0.0;73.0;0.5;43.0;2.0;62.0;126.0;2.0;0.0;120.0;137.0;121.0;73.0;1.0;2.0"
```
Setelah dilakukan pemisahan atribut, dataset direstrukturisasi menjadi format tabel dengan masing-masing atribut memiliki kolom tersendiri, seperti berikut:

| baseline_value | accelerations | fetal_movement | uterine_contractions | light_decelerations | severe_decelerations | fetal_health |
|---------------|--------------|----------------|----------------------|----------------------|----------------------|--------------|
| 120.0        | 0.000        | 0.0            | 0.000                | 0.000                | 0.0                  | 2.0          |
| 132.0        | 0.006        | 0.0            | 0.006                | 0.003                | 0.0                  | 1.0          |

Dengan pemisahan ini, setiap fitur dapat diakses secara independen, sehingga memudahkan analisis lebih lanjut dan pengembangan model.

---

## **2. Konversi Tipe Data**
Setelah atribut terpisah, langkah selanjutnya adalah memastikan bahwa seluruh nilai pada dataset berada dalam format numerik yang sesuai. Pada dataset awal, beberapa nilai terbaca sebagai string, yang dapat menghambat perhitungan statistik dan proses pelatihan model. Oleh karena itu, seluruh nilai dikonversi ke dalam format **float** atau **integer**. Sebelum dilakukan konversi, nilai pada dataset memiliki format seperti berikut:
```
"120.0", "0.0", "0.0"
```
Setelah dikonversi menjadi tipe numerik:
```
120.0, 0.0, 0.0
```
Dengan konversi ini, dataset dapat digunakan dalam perhitungan matematis tanpa kendala tipe data.

---

## **3. Penanganan Nilai Hilang**
Ketidaksempurnaan dalam data sering kali muncul dalam bentuk nilai yang hilang (`NaN`), yang dapat memengaruhi hasil analisis dan performa model. Oleh karena itu, dilakukan **imputasi nilai hilang** dengan menggunakan **median** untuk menggantikan nilai yang kosong tanpa mengubah distribusi data. Sebelum dilakukan imputasi, dataset memiliki nilai yang hilang seperti berikut:

**Contoh data sebelum imputasi:**
| baseline_value | accelerations | fetal_movement |
|---------------|--------------|----------------|
| 132.0        | 0.006        | NaN            |
| 133.0        | NaN          | 0.0            |

Setelah dilakukan imputasi dengan nilai median:
| baseline_value | accelerations | fetal_movement |
|---------------|--------------|----------------|
| 132.0        | 0.006        | 0.0            |
| 133.0        | 0.003        | 0.0            |

Dengan metode ini, data tetap valid untuk dianalisis tanpa menghilangkan informasi penting.

---

## **4. Normalisasi Data**
Langkah terakhir dalam pra-pemrosesan adalah **normalisasi data**, yang bertujuan untuk menyamakan skala variabel numerik agar memiliki rentang yang seragam. Normalisasi ini penting untuk memastikan bahwa model tidak memberikan bobot yang lebih besar pada fitur dengan skala yang lebih tinggi. Metode yang digunakan dalam penelitian ini adalah **Min-Max Scaling**, yang mengubah rentang nilai ke dalam interval **0 hingga 1**. Sebelum dilakukan normalisasi, data memiliki rentang nilai yang cukup besar, seperti:
```
baseline_value: [120.0, 160.0]
accelerations: [0.000, 0.100]
```
Setelah normalisasi, rentang nilai berubah menjadi:
```
baseline_value: [0.0, 1.0]
accelerations: [0.0, 1.0]
```
Dengan demikian, seluruh variabel memiliki skala yang seragam, sehingga meningkatkan efisiensi model dalam mengidentifikasi pola pada data.

---

Dengan menyelesaikan seluruh tahapan pra-pemrosesan ini, dataset telah siap untuk digunakan dalam pengembangan model prediksi detak jantung janin. Pra-pemrosesan yang baik memastikan bahwa model machine learning dapat bekerja secara optimal dengan data yang bersih, terstruktur, dan relevan untuk analisis lebih lanjut.

## **Tahapan Pemilihan Model dan Proses Pengujian**  

Tahapan **pemilihan model** merupakan langkah esensial dalam pengembangan sistem prediksi detak jantung janin menggunakan **machine learning**. Pada tahap ini, dilakukan pemilihan algoritma yang sesuai berdasarkan karakteristik data serta evaluasi terhadap performa model dalam mendeteksi kondisi normal dan abnormal pada janin. Model yang digunakan dalam penelitian ini meliputi **Random Forest, Logistic Regression, Naïve Bayes, Support Vector Machine (SVM), dan Neural Networks**.  

Setelah model dipilih, dilakukan proses **pembagian dataset** (**Tahap 4**) menjadi dua subset utama, yaitu:  
1. **Training dataset (70-90%)** – Digunakan untuk melatih model agar mampu mengenali pola dalam data.  
2. **Testing dataset (10-30%)** – Digunakan untuk menguji sejauh mana model dapat melakukan prediksi terhadap data baru yang belum pernah dilihat sebelumnya.  

Setelah dataset dibagi, model menjalani **proses pelatihan (model training)** (**Tahap 5**) menggunakan training dataset. Pada tahap ini, model dipelajari dengan menyesuaikan bobot dan parameter internalnya agar dapat menghasilkan prediksi yang lebih akurat. Setelah model dilatih, langkah selanjutnya adalah **validasi model** (**Tahap 6**) untuk mengevaluasi performa model dan menghindari kemungkinan **overfitting**, yaitu ketika model terlalu menyesuaikan diri dengan data latih tetapi gagal menggeneralisasi pada data baru.  

Validasi dilakukan dengan membandingkan hasil prediksi model terhadap data yang sebenarnya menggunakan berbagai metrik evaluasi seperti **Accuracy, Precision, Recall, dan F1-Score**. Jika model belum mencapai performa yang optimal, maka dilakukan **tuning parameter** atau pemilihan model lain yang lebih sesuai. Jika model telah memenuhi standar kinerja yang diinginkan, maka proses dilanjutkan ke **pembandingan kinerja model** (**Tahap 7**) untuk menentukan model terbaik yang akan digunakan dalam implementasi akhir sistem prediksi.  

Setelah model terbaik terpilih, model tersebut digunakan untuk **mendeteksi dan memprediksi kondisi detak jantung janin** berdasarkan data baru yang masuk. Model yang telah diuji ini diharapkan mampu memberikan prediksi yang **akurat, stabil, dan dapat diandalkan** dalam mendukung analisis klinis serta membantu tenaga medis dalam memantau kesehatan janin secara lebih efektif.  

Dengan mengikuti alur pemilihan model ini, penelitian dapat memastikan bahwa sistem yang dikembangkan memiliki performa yang optimal dan dapat digunakan dalam berbagai kondisi dengan tingkat kepercayaan yang tinggi.

