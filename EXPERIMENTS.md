# Experiment Log

Catat setiap percobaan hyperparameter di sini. **Minimal 5 eksperimen.**

> Tips: ubah **satu hyperparameter pada satu waktu** agar bisa mengisolasi efeknya. Setelah memahami efek tiap variabel, baru gabungkan untuk hasil terbaik.

---

## 📋 Tabel Ringkasan

Isi tabel ini setelah selesai semua eksperimen.

| # | Hidden | Neurons | Activation | Optimizer | LR     | Batch | Epochs | Dropout | Test Acc | Train Time |
|---|--------|---------|------------|-----------|--------|-------|--------|---------|----------|------------|
| 0 | 1      | 64      | relu       | sgd       | 0.01   | 32    | 10     | 0.0     | ~85%     | ~30s       |
| 1 | 2      | 128     | tanh       | adam      | 0.01   | 512   | 10     | 0.5     | ~86%      | ~45s       |
| 2 | 2      | 128     | sigmoid    | adamax    | 0.01   | 128   | 30     | 0.0     | ~87%     | ~82s       |
| 3 | 4      | 256     | elu        | sgd       | 0.01   | 32    | 10     | 0.3     | ~61%     | ~30s       |
| 4 | 2      | 64      | tanh       | adam      | 0.001  | 128   | 10     | 0.3     | ~86%     | ~26s       |
| 5 | 5      | 128     | relu       | adam     | 0.001   | 32    | 20     | 0.2     | ~88%     | ~144s      |

> **Eksperimen #0** = baseline (jangan ubah, ini patokan kalian).

---

## 🧪 Detail Setiap Eksperimen

Gunakan template di bawah untuk SETIAP eksperimen.

---


## **Eksperimen #1**

### **Apa yang diubah dari baseline**

* Mengganti **optimizer dari SGD → Adam**
* Menambah **hidden layer dari 1 → 2**
* Menambah **jumlah neuron dari 64 → 128**
* Mengubah **fungsi aktivasi menjadi tanh**
* Menambahkan **dropout 0.5**
* Menyesuaikan **batch size menjadi 512**
  Baseline lainnya dipertahankan.

---

### **Hipotesis sebelum run**

Optimizer **Adam** bersifat adaptif terhadap learning rate sehingga diharapkan mampu mencapai konvergensi lebih cepat dibandingkan SGD. Penambahan hidden layer dan jumlah neuron diperkirakan meningkatkan kemampuan model dalam menangkap pola data yang lebih kompleks, sementara dropout 0.5 diharapkan mampu mengurangi overfitting. Dengan kombinasi tersebut, akurasi model diprediksi meningkat dengan generalisasi yang lebih baik.

---

### **Hasil**

* **Train accuracy:** 94%
* **Validation accuracy:** 90%
* **Test accuracy:** 91%
* **Train time:** ±45 detik
* **Apakah overfit/underfit?**
  Tidak overfit, terdapat gap kecil antara train dan validation accuracy yang masih wajar.

---

### **Observasi & Insight**

Model menunjukkan peningkatan akurasi dibandingkan baseline dengan proses training yang stabil. Penggunaan Adam mempercepat konvergensi, sementara dropout 0.5 efektif menekan overfitting meskipun sedikit menahan akurasi training. Batch size besar membuat training lebih cepat namun berpotensi melewatkan detail gradien kecil.

---

### **Rencana eksperimen berikutnya**

* Mengurangi **dropout menjadi 0.3** untuk melihat potensi peningkatan akurasi
* Mencoba **aktivasi ReLU** untuk membandingkan stabilitas dan performa
* Mengurangi **batch size (128 atau 256)** untuk melihat pengaruh terhadap generalisasi


### Eksperimen #2
**Apa yang diubah:**
- Hidden Layer menjadi 2
- Neurons per layer menjadi 128
- Optimizer menjadi adamax
- Batch Size menjadi 128
- Epochs menjadi 30

**Hipotesis:**
- Train time lebih lama karena epoch lebih banyak.
- Hasil menjadi lebih akurat karena hidden layer dan neurons per layer lebih banyak.
- Komputasi lebih kompleks.

**Hasil:**
- Test accuracy: 87.44%
- Train accuracy: 95.26%
- Validation accuracy: 87.78%
- Train time: 82.9 detik
- Apakah overfit/underfit? kemungkinan OVERFITTING

**Observasi:**
Gap train vs val = 7.5% — kemungkinan OVERFITTING.
Coba: kurangi neuron, tambah dropout, atau kurangi epoch.

---

### Eksperimen #3

**Apa yang diubah:**
- Mengganti optimizer dari SGD → tanh
- Menambah hidden layer dari 1 → 2
- jumlah neuron tetap
- Mengubah fungsi aktivasi menjadi tanh
- Menambahkan dropout 0.3
- Menyesuaikan batch size menjadi 128
- Epochs menjadi 10

**Hipotesis:**
Terbukti: Waktu komputasi memang lebih lama (82.9 detik) dan model menjadi terlalu kompleks sehingga menyebabkan gap akurasi yang lebar (overfitting).

**Hasil:**
Test accuracy: 86.29%
Train accuracy: 86.20%
Validation accuracy: 87.38%
Train time: 26.3 detik
Model baru ini TIDAK Overfit dan TIDAK Underfit, melainkan berada di kondisi Good Fit (Ideal).

**Observasi:**
Meskipun akurasi train-nya turun dari 95% ke 86%, akurasi pengujian (test accuracy) stabil di angka 86.29% (hanya selisih sekitar 1.15% dari Eksperimen #2 yang overfit).

---

### Eksperimen #4

**Apa yang diubah**:Jumlah Hidden ditingkatkan menjadi layer 4 dengan neuron 256 per layer, menggunakan aktivasi ELU dan dropout 0.3.

**Hipotesis**: Penambahan hidden layer dan neuron diharapkan meningkatkan kemampuan model dalam memplajari pola data yang lebih kompleks sehingga akurasi meningkat

**Hasil**:
- Train accuracy: 57.73%
- Validation accuracy: 62.82%
- Test accuracy: 61.89%
- Test loss: 9.9008%

**Observasi**:
Model menunjukkan performa validasi dan test yang cukup baik, namun train accuracy masih relatif rendah. Learnig rate 0.1 kemungkinan terlalu besar sehingga proses traainning kurang stabil dan menyebabkan loss . Model belum optimal dan masih dapat ditingkatkan melalui penyesuaian hyperparameter seperti learning rate yang lebih kecil atas penambhan epoch

---

### Eksperimen #5

**Apa yang diubah:**

  Hidden layers     : 2
  Neurons per layer : 128
  Activation        : relu
  Dropout rate      : 0.2
  Optimizer         : adam
  Learning rate     : 0.001
  Batch size        : 32
  Epochs            : 20
  
**Hipotesis:**

Dengan menggunakan arsitektur jaringan yang lebih sederhana dan stabil, optimizer Adam, learning rate yang lebih kecil, serta aktivasi ReLU dan dropout moderat, model diharapkan dapat belajar lebih efektif sehingga akurasi klasifikasi meningkat dan performa generalisasi menjadi lebih baik.

**Hasil:**

TEST ACCURACY  : 87.98%
Test loss      : 0.3457
Train accuracy : 90.11%
Val accuracy   : 88.52%

**Observasi:**

✅ Train-val gap sehat. Lanjut eksperimen!

---

## 🏆 Konfigurasi Terbaik

Setelah semua eksperimen, salin konfigurasi terbaik kalian ke sini:

```python
HIDDEN_LAYERS     = ?
NEURONS_PER_LAYER = ?
ACTIVATION        = ?
DROPOUT_RATE      = ?
OPTIMIZER         = ?
LEARNING_RATE     = ?
BATCH_SIZE        = ?
EPOCHS            = ?
```

**Test accuracy final: ___%**
