# 🎮 Strategic Greenlight System: Pre-Launch Game Sales Forecasting

> **Evolution Status:** Project ini telah berevolusi dari *Basic Regression* menjadi *Historical Pattern Analysis Engine* untuk mencegah Data Leakage.

## 📋 Executive Summary
Project ini bertujuan membangun **Decision Support System** bagi publisher game untuk mengestimasi potensi penjualan *sebelum* game dirilis. Berbeda dengan pendekatan konvensional yang menggunakan skor kritik (*Critics Score*)—yang menyebabkan kebocoran data masa depan—model ini murni menggunakan **atribut pra-rilis** dan **pola historis**.

---

## 🛑 The Evolution: Why We Rebuilt This?

### Versi 1.0 (The Flaw)
Awalnya, proyek ini menggunakan fitur `CRITICS_POINTS` dan `USER_POINTS` untuk memprediksi penjualan.
* **Masalah:** Skor kritik baru tersedia *setelah* game rilis. Menggunakannya untuk prediksi bisnis adalah bentuk **Data Leakage** (kecurangan statistik).
* **Konsekuensi:** Model terlihat akurat (RMSE rendah), tapi tidak berguna untuk keputusan bisnis nyata (budgeting/marketing).

### Versi 2.0 (The Strategic Fix)
Kami merombak total pendekatan menjadi **Pre-Launch Forecasting**.
* **Aturan Baru:** DILARANG menggunakan data masa depan.
* **Inovasi:** Menciptakan fitur **Historical Power** menggunakan teknik *Expanding Window Statistics*.
    * *Contoh:* Prediksi penjualan game Ubisoft tahun 2015 hanya boleh melihat rata-rata penjualan Ubisoft tahun 1990-2014.

---

## 🛠️ Methodology & Tech Stack

**Engine:** Python, CatBoost Regressor  
**Validation Strategy:** Time-Series Split (Bukan Random Split)

### 1. Feature Engineering (The Secret Sauce)
Kami mengubah data kategorikal menjadi sinyal numerik menggunakan sejarah:
* **Publisher Momentum:** Rata-rata penjualan game sebelumnya dari publisher tersebut.
* **Genre Fatigue:** Tren penjualan genre terkait di masa lalu.
* **Platform Install Base Proxy:** Performa historis platform/konsol.

### 2. Time-Based Validation
Untuk mensimulasikan tantangan dunia nyata:
* **Training Data:** Game rilis sebelum tahun 2015.
* **Validation Data:** Game rilis tahun 2015 - 2019.
* **Tujuan:** Menguji apakah model yang belajar dari era *Physical Disc* (PS2/PS3) bisa memprediksi era *Digital/Indie* (PS4/Switch).

---

## 📊 Results & Business Intelligence

### Model Performance (Validation Phase)
| Metrik | Skor | Interpretasi |
| :--- | :--- | :--- |
| **RMSE** | **2.15 Juta Unit** | Rata-rata deviasi prediksi. Angka ini cukup konservatif untuk industri game global. |
| **R2 Score** | **0.025 (2.5%)** | Indikasi kuat adanya **Market Shift**. Pola pasar pasca-2015 sangat berbeda dengan pra-2015. |

### Key Drivers (Feature Importance)
Berdasarkan analisis model CatBoost, faktor penentu kesuksesan game adalah:
1.  🥇 **Publisher Historical Power:** (Dominan) Reputasi penerbit adalah prediktor terbaik. Game dari publisher besar cenderung tetap laku karena *brand loyalty*.
2.  🥈 **Category (Genre):** Tren genre sangat mempengaruhi minat pasar.
3.  🥉 **Year of Release:** Faktor inflasi dan tren industri tahunan.

---

## 💡 Strategic Conclusion
Meskipun R2 Score rendah (yang wajar untuk prediksi perilaku manusia yang kompleks di industri kreatif), model ini memberikan *Actionable Insight*:

1.  **Invest in Reputation:** Data membuktikan bahwa nama besar Publisher lebih berharga daripada Genre.
2.  **Market Volatility:** Rendahnya akurasi di era 2015+ menunjukkan bahwa industri game menjadi semakin tidak terprediksi (kemunculan game Indie viral, pergeseran ke Mobile/Microtransactions).
3.  **Risk Management:** Model ini sebaiknya digunakan sebagai *Baseline Konservatif*, bukan angka target absolut.

---

## 📂 Repository Structure
* `prediksi_sales_gaming.ipynb`: Notebook eksperimen V1 (Legacy).
* `PreLaunch_Game_Sales_Forecasting_Engine.ipynb`: **[MAIN]** Notebook evolusi V2 dengan metodologi Time-Series.
* `PreLaunch_Evolution_Submission.csv`: Hasil prediksi final pada data test.
* `Train.csv` / `Test.csv`: Dataset mentah.

## 🚀 How to Run
1. Clone repository ini.
2. Buka `PreLaunch_Game_Sales_Forecasting_Engine.ipynb` di Google Colab.
3. Pastikan dataset (`Train.csv`, `Test.csv`) sudah di-upload.
4. Jalankan semua sel untuk melihat proses Feature Engineering dan Training.

---
*Created by [Ardho Mihada]*
