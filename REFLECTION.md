# Refleksi Tim

> Jawaban dalam Bahasa Indonesia. Maksimal 1 halaman (~500 kata). Yang dinilai adalah **kedalaman pemahaman**, bukan panjang tulisan.

---

## 1. Parameter vs Hyperparameter

Berdasarkan eksperimen yang kalian lakukan, jelaskan dengan **kata-kata kalian sendiri**:
- Apa yang termasuk **parameter** dalam model kalian, dan apa yang termasuk **hyperparameter**?
- Manakah yang berubah saat training berjalan, dan manakah yang ditentukan oleh kalian sebelum training?

**Jawaban:**
- Parameter merupakan nilai yang dipelajari otomatis oleh model selama proses traianing dan akan terus berubah ketika model melakukan learning berdasarkan data. Contoh parameter: weights dan bias
- Hyperparameter merupakan pengaturan yang ditentukan sebelum dilakukannya training untuk mengontrol cara model melakukan learning. Contoh hyperparameter:
  - HIDDEN_LAYERS	= Jumlah Lapisan
  - NEURONS_PER_LAYER	= Jumlah Neuron
  - ACTIVATION = Fungsi Aktivasi
  - OPTIMIZER	= Optimizer (Adam, SGD, dst)
  - LEARNING_RATE	= Learning Rate (λ)
  - BATCH_SIZE	= Batch Size
  - EPOCHS	= Epoch
  - DROPOUT_RATE	= Regularisasi
---

## 2. Hyperparameter dengan Dampak Terbesar

Dari semua hyperparameter yang kalian eksperimen, mana yang menurut kalian memberikan **dampak paling besar** terhadap akurasi? Mengapa demikian — apa yang kalian amati pada kurva loss/accuracy?

**Jawaban:**
- Menurut kami, hyperparameter yang memberikan dampak paling besar terhadap akurasi adalah `LEARNING_RATE`. Learning rate sangat memengaruhi proses pembelajaran model karena menentukan seberapa besar perubahan weight pada setiap iterasi.

Pada eksperimen yang dilakukan, learning rate yang terlalu besar membuat kurva loss menjadi tidak stabil dan accuracy sulit meningkat secara konsisten. Sebaliknya, learning rate yang lebih sesuai menghasilkan penurunan loss yang lebih stabil serta peningkatan accuracy yang lebih baik pada data training maupun validation.

---

## 3. Learning Rate

Coba set `LEARNING_RATE = 1.0` (atau bahkan lebih besar) dan jalankan sekali. Apa yang terjadi pada kurva loss? Hubungkan jawaban kalian dengan rumus:

$$W_j = W_j - \lambda \frac{\partial F(W_j)}{\partial W_j}$$

**Jawaban:**
Ketika LEARNING_RATE diset 1.0 atau bahkan lebih, kurva loss menjadi tidak stabil dan cenderung berosilasi dikarenakan rate yang terlalu besar membuat weight pada setiap iterasi menjadi terlalu besar.
Hal ini konsisten dengan rumus tersebut
- $W_j$ adalah weight,
- $\lambda$ adalah learning rate,
- $\frac{\partial F(W_j)}{\partial W_j}$ adalah gradient dari loss function.

Ketika nilai $\lambda$ terlalu besar, maka hasil pengurangan weight juga menjadi sangat besar. Akibatnya, model tidak bergerak secara perlahan menuju titik minimum loss, tetapi justru “melompat-lompat” melewati titik minimum tersebut. Hal ini menyebabkan loss sulit turun secara stabil dan akurasi model menjadi kurang baik.


## 4. Batch Size & Trade-off

Bandingkan eksperimen dengan **batch size kecil** (misal 16) vs **batch size besar** (misal 256). Apa yang kalian amati dari sisi:
- Waktu training?
- Stabilitas kurva loss?
- Akurasi akhir?

Apakah pengamatan ini sesuai dengan teori di slide kuliah?

**Jawaban:**
- Waktu training: Batch size besar cenderung memiliki waktu training yang lebih cepat karena dalam satu iterasi model memproses data lebih banyak sekaligus. Sementara itu, batch size kecil membutuhkan lebih banyak iterasi sehingga training berlangsung lebih lama. 
- Stabilitas Kurva Loss: Pada batch size kecil, kurva loss cenderung lebih fluktuatif karena update weight dilakukan lebih sering dengan jumlah data yang sedikit. Sebaliknya, batch size besar menghasilkan kurva loss yang lebih halus dan stabil karena gradient dihitung dari data yang lebih banyak.
- Akurasi akhir: Batch size kecil terkadang menghasilkan akurasi akhir yang lebih baik karena model melakukan update parameter lebih sering sehingga mampu melakukan generalisasi dengan lebih baik. Namun, batch size besar dapat menghasilkan training yang lebih stabil meskipun terkadang akurasi akhirnya sedikit lebih rendah

Pengamatan tersebut sesuai dengan teori di slide perkuliahan.

## 5. Feed Forward & Back Propagation

Pada saat kalian menekan `model.fit(...)`, sebenarnya proses feed forward dan back propagation berjalan **ribuan kali**. Hitung kira-kira berapa kali back propagation terjadi pada salah satu eksperimen kalian.

> Petunjuk: `(jumlah_sample_training / batch_size) × epochs`

Jelaskan apa yang terjadi pada **bobot** dan **bias** model kalian di antara iterasi pertama dan terakhir.

**Jawaban:**
Pada eksperimen 3 digunakan:
- Jumlah data training = 60.000
- Batch size = 128
- Epoch = 30

Jumlah back propagation dapat dihitung dengan rumus:

$$
\left(\frac{60000}{128}\right) \times 30 \approx 14062.5
$$

Sehingga proses back propagation terjadi sekitar 14.063 kali selama training berlangsung.

Di antara iterasi pertama dan terakhir, bobot (weight) dan bias pada model terus diperbarui selama proses training menggunakan back propagation dan optimizer. Pada iterasi awal, nilai weight dan bias masih acak sehingga prediksi model belum akurat dan loss masih tinggi.

Seiring berjalannya training, model menghitung error dari hasil prediksi lalu menyesuaikan weight dan bias untuk mengurangi nilai loss. Setelah banyak iterasi, parameter model menjadi lebih optimal sehingga prediksi semakin akurat, loss menurun, dan accuracy meningkat.

---

## 6. Kapan Deep Learning Tepat Digunakan?

Berdasarkan pengalaman kalian dengan Fashion-MNIST, menurut kalian apakah masalah ini *benar-benar* membutuhkan deep learning, atau bisa diselesaikan dengan machine learning klasik (misal Logistic Regression atau Random Forest)? Beri argumen.

**Jawaban:**
Menurut kami, Fashion-MNIST sebenarnya masih bisa diselesaikan menggunakan machine learning klasik seperti Logistic Regression atau Random Forest karena ukuran gambar kecil (28×28) dan jumlah kelas tidak terlalu banyak. Namun, deep learning lebih unggul dalam mempelajari pola gambar secara otomatis tanpa feature engineering manual. Neural network juga lebih fleksibel untuk menangani dataset yang lebih kompleks. Jadi, untuk Fashion-MNIST deep learning belum sepenuhnya wajib, tetapi tetap cocok digunakan karena termasuk tugas klasifikasi gambar dan dapat memberikan performa yang lebih baik.

---

## 7. Refleksi Tim

- Tantangan apa yang paling sulit?
- Apa pelajaran terpenting yang kalian dapat dari aktivitas ini?
- Jika diberi waktu lebih, apa yang ingin kalian coba lagi?

**Jawaban:**
- Tantangan yang paling sulit: menentukan kombinasi hyperparameter yang menghasilkan performa terbaik. Perubahan kecil pada learning rate, batch size, atau jumlah neuron dapat memberikan hasil yang berbeda pada akurasi dan stabilitas training.

- Pelajaran terpenting dari aktivitas ini: Kami memahami bahwa performa model deep learning sangat dipengaruhi oleh proses tuning hyperparameter. Selain itu, kami juga belajar membaca kurva loss dan accuracy untuk mengetahui apakah model mengalami overfitting, underfitting, atau training yang tidak stabil.

-   Jika diberi waktu lebih, kami ingin mencoba lebih banyak kombinasi hyperparameter, seperti optimizer lain, jumlah layer yang lebih besar, serta penggunaan dropout dan epoch yang berbeda untuk melihat pengaruhnya terhadap performa model.
