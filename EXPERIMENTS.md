# Experiment Log

Catat setiap percobaan hyperparameter di sini. **Minimal 5 eksperimen.**

> Tips: ubah **satu hyperparameter pada satu waktu** agar bisa mengisolasi efeknya. Setelah memahami efek tiap variabel, baru gabungkan untuk hasil terbaik.

---

## 📋 Tabel Ringkasan

Isi tabel ini setelah selesai semua eksperimen.

| # | Hidden | Neurons | Activation | Optimizer | LR     | Batch | Epochs | Dropout | Test Acc | Train Time |
|---|--------|---------|------------|-----------|--------|-------|--------|---------|----------|------------|
| 0 | 1      | 64      | relu       | sgd       | 0.01   | 32    | 10     | 0.0     | ~85%     | ~30s       |
| 1 |        |         |            |           |        |       |        |         |          |            |
| 2 |        |         |            |           |        |       |        |         |          |            |
| 3 |        |         |            |           |        |       |        |         |          |            |
| 4 |        |         |            |           |        |       |        |         |          |            |
| 5 |        |         |            |           |        |       |        |         |          |            |

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

**Hipotesis:**

**Hasil:**

**Observasi:**

---

### Eksperimen #4

**Apa yang diubah:**

**Hipotesis:**

**Hasil:**

**Observasi:**

---

### Eksperimen #5

**Apa yang diubah:**

**Hipotesis:**

**Hasil:**

**Observasi:**

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
