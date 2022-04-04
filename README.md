# Harta-Tahta-Data-Final-Project-Banking Marketing Deposit Target Prediction

Dalam membuat projek ini dalam beberapa stage ;

## Stage 0
Pada stage ini menentukan beberapa hal penting sebelum memulai projek ini:
- Problem : Penjabaran mengenai permasalahan yang terjadi pada suatu suatu campaign telemarketing pada bank portugal yang tergambar pada dataset.
- Goals : Landasan kami menyelesaikan permasalahan yang ada.
- Objective : Solusi yang kami tawarkan kepada bank portugal untuk menyelesaikan masalah tersebut.
- Business Metrics : Nilai yang konkrit dan dapat dihitung untuk mengukur serta memantau tercapainya tujuan yang telah dipaparkan.

## Stage 1 
Pada stage ini melakukan EDA (Exploratory Data Analysis). Summary dari EDA:
- Pada dataset yang terdiri dari 17 kolom dan 45211 baris terlihat tidak terdapat data yang duplikat pada dataset, tidak terdapat missing values/null dan tipe data untuk setiap kolom sudah sesuai.
- Feature Engineering : `age`, `day` dengan metode standarisasi dan `balance`, `duration`, `campaign`, `pdays`, `previous` dengan metode normalisasi.
- Pada kolom pdays mwngubah nilai (-1) menjadi 999.
- Handling outliers untuk feature numerical dengan metode Z score.
- Label Encoding : `education`, `default`, `housing`, `loan`, `y`.
- One-Hot Encoding : `job`, `marital`, `contact`, `poutcome`, `month`
- Handling Class Imbalance : melakukan 4 skenario yaitu tanpa handling, ovesampling, undersampling, SMOTE.

## Stage 2 
Pada satge ini melakukan semua poin yang terdapat pada summary EDA.

## Stage 3
Split Data Train & Test: Split data train dan test sudah dilakukan pada tahap preprocessing untuk menghindari terjadinya data leak, karena data test adalah unseen data. Modeling: Model yang digunakan adalah Logistic Regression (Baseline) Decision Tree KNN SVM Random Forest (best model) Model ini untuk sementara dipilih karena memiliki score precision dan ROC_AUC yang paling tinggi disbanding model lainnya. Gradient Boosting XGBoost AdaBoost CatBoost

Model Evaluation: Pada kasus Banking Marketing Deposit target prediction ini, kami menggunakan Precision sebagai metrics utama karena tujuan utama dari prediksi model ini adalah mengurangi kesalahan model memprediksi customer (False Positive) pada saat modelling machine learning.Namun, karena dataset ini mempunyai target yang imbalance, maka kami akan memakai metrics ROC_AUC sebagai tambahan.

Walaupun model yang sudah di train sudah melewati baseline model yang berarti model sudah cukup baik, namun Model belum best-fit karena masih dapat ditemukan model yang lebih baik lagi dengan mencoba menggunakan feature-feature lain pada data yang terkena drop pada tahap preprocess (stage 2), serta dapat mentuning hyperparameter dengan lebih baik lagi

Hyperparameter Tuning: Terdapat beberapa hyperparameter yang digunakan untuk mentuning masing-masing model, namunn hyperparameter yang digunakan untuk mentuning best model adalah:

n_estimators : untuk mengatur jumlah tree dalam randomForest model
min_samples_split : minimum sample yang diperlukan untuk melakukan split pada suatu node
min_samples_leaf: minimum sample yang diperlukan dalam suatu leaf, jika kurang dari min_samples_leaf maka leaf akan di prune
max_features: maximum feature yang digunakan untuk splitting node pada tree
max_depth: maximum kedalaman yang dapat dibentuk oleh tree
bootstrap: jika true maka tiap tree akan dibuat dengan sample data, jika false semua data akan digunakan untuk semua tree
Eksperimen yang telah dilakukan adalah mencoba train semua model yang belum di tuning hyperparameternya lalu membandingkan score mereka, lalu mencoba train semua model sambal mentuning hyperparameternya lalu membandingkan score mereka. Selain itu mencoba feature scaling dari feature importances yang telah didapat. Dari semua percobaan, untuk saat ini model yang terbaik adalah model RandomForest

Feature yang mempunyai pengaruh besar adalah:

- Duration
- Balance
- Age
- Day
- Poutcome

Melihat dari feature-feature yang penting diatas dapat ditarik kesimpulan bahwa, untuk mencegah terjadinya cost per acquistion meningkat maka perlu membatasi waktu duration pada saat mengkontak customer yang terlihat tidak tertarik yaitu pada 5 menit awal, perlu adanya upaya dari pihak marketing untuk memberikan frequency campaign secara efektif dan efisien dengan besaran optimum sebanyak 3 kali campaign karena semakin banyak campaign diberikan maka conversion rate semakin kecil dan campign sebelumnya sangat mempengaruhi campaign selanjutnya karena customer yang berhasil mendaftar campaign sebelumnya cenderung subscribe kembali campaign selanjutnya dan menjadikan sebuah kesimpulan bahwa produk deposito yang  bank portugal tawarkan memiliki kualitas yang baik karena persentase sukses pada campaign sebelumnya cenderung tinggi.

Selain itu target customer yang menerima campaign ini ialah yang mememiliki history yang cukup baik pada pembayaran kredit atau terdapat pada kolom default dan ber-label "no", dengan rentang umur 20-60 dimana merupakan usia yang produktif, dan memiliki balance (rata-rata saldo tahunan lebih besar dari 630 euro) dikarenakan minimal melakukan deposito sebesar 630 euro. 
