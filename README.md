# JCDSBDGAM-09_Beta

# Telco Customer Churn Analysis & Prediction

[![Streamlit App](https://img.shields.io/badge/Streamlit-App-FF4B4B?style=for-the-badge&logo=streamlit)](https://telcobeta.streamlit.app/)
[![Tableau Dashboard](https://img.shields.io/badge/Tableau-Dashboard-E97627?style=for-the-badge&logo=tableau)](https://public.tableau.com/views/TelcoCustomerDashboard_17706500189310/Home)
[![Presentation](https://img.shields.io/badge/Canva-Presentation-00C4CC?style=for-the-badge&logo=canva)](https://www.canva.com/design/DAHA1t4vfG4/9u-LAc0nukx-1IARdZsJ9w/edit)

## 📋 Latar Belakang

Industri telekomunikasi menghadapi tingkat persaingan yang sangat tinggi dengan **churn rate global mencapai 15-25% per tahun**. Churn rate (tingkat pelanggan yang berhenti berlangganan) menjadi permasalahan krusial karena:

- **Biaya akuisisi pelanggan baru 5-10x lebih mahal** dibanding mempertahankan pelanggan existing
- Pelanggan cenderung **price-sensitive** dengan banyak alternatif provider
- Kehilangan pelanggan berdampak langsung pada **pendapatan dan sustainability bisnis**

Pendekatan konvensional yang reaktif (bertindak setelah pelanggan churn) terbukti kurang optimal. Oleh karena itu, diperlukan **pendekatan prediktif berbasis machine learning** untuk mengidentifikasi pelanggan berisiko churn secara dini.

---

## 🎯 Problem Statement

Perusahaan telekomunikasi belum memiliki sistem prediktif yang mampu mengidentifikasi pelanggan berpotensi churn secara akurat berdasarkan data historis. Padahal, data seperti:
- Karakteristik pelanggan (demografi, geografis)
- Penggunaan layanan
- Jenis paket dan kontrak
- Riwayat interaksi

dapat dimanfaatkan untuk mengenali pola perilaku pelanggan yang berisiko churn.

**Pertanyaan bisnis utama:**
- Siapa pelanggan yang paling rentan churn?
- Di mana (lokasi geografis) konsentrasi churn tertinggi?
- Faktor apa yang paling mempengaruhi keputusan pelanggan untuk churn?

---

## 🎯 Goals

1. **Menganalisis pola perilaku pelanggan** yang berkontribusi terhadap churn melalui analisis demografi dan geografi
2. **Membangun model machine learning** untuk memprediksi kemungkinan churn pelanggan secara akurat
3. **Menghasilkan insight berbasis data** untuk strategi retensi yang proaktif dan tepat sasaran
4. **Mendukung pengambilan keputusan bisnis** dengan menyediakan informasi pelanggan berisiko churn tinggi

---

## 🔬 Analytical Approach

### 1. **Data Collection & Preprocessing**
- Menggabungkan dataset dari dua sumber (Kaggle + HuggingFace)
- Handling missing values, duplicate removal
- Feature engineering dan selection

### 2. **Exploratory Data Analysis (EDA)**
**Fokus Demografi:**
- Analisis profil pelanggan (gender, age, senior citizen, family status)
- Korelasi satisfaction score dengan churn

**Fokus Geografi:**
- Pemetaan distribusi churn menggunakan **Folium heatmap**
- Identifikasi top cities dengan churn tertinggi

### 3. **Machine Learning Modeling**
- Binary classification problem (churn vs non-churn)
- Algoritma: Logistic Regression, Decision Tree, Random Forest, XGBoost
- Handling imbalanced data: SMOTE, RandomOverSampler, RandomUnderSampler, NearMiss
- Hyperparameter tuning menggunakan GridSearchCV

### 4. **Model Interpretation**
- Feature importance analysis
- SHAP values untuk explainability
- LIME untuk local explanations

---

## 📊 Metrics Evaluation

### Confusion Matrix Components
- **True Negative (TN)**: Prediksi tidak churn ✓ (benar)
- **False Positive (FP)**: Prediksi churn ✗ (salah, Type I Error)
- **False Negative (FN)**: Prediksi tidak churn ✗ (salah, **Type II Error - lebih kritis**)
- **True Positive (TP)**: Prediksi churn ✓ (benar)

### Primary Metric: **F2-Score**
```
F2 = (1 + 2²) × (Precision × Recall) / (2² × Precision + Recall)
```

**Mengapa F2-Score?**
- Memberikan **bobot 2x lebih besar pada Recall**
- Meminimalkan False Negative (pelanggan churn yang terlewat)
- Lebih fokus pada deteksi pelanggan berisiko churn

**Trade-off:**
- **False Positive** → Biaya retensi tidak perlu ($10.6)
- **False Negative** → Kehilangan pelanggan ($53)
- FN **5x lebih merugikan**, sehingga harus diminimalkan

---

## 📁 Dataset Description
Untuk mendapatkan hasil analisis dan machine learning yang lebih memadai, kami mencoba mencari data tambahan yang bersumber dari link di bawah, sehingga kami menggunakan 2 sumber data yang akan digunakan pada project ini
**Source:** 
- [Kaggle - Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- [HuggingFace - Telco Customer Churn](https://huggingface.co/datasets/aai510-group1/telco-customer-churn)

**Total Records:** 7,043 customers  
**Features:** 42 columns (setelah cleaning dan feature engineering)

### Key Features:

**Demographic:**
- `age`, `gender`, `seniorcitizen`, `partner`, `dependents`

**Geographic:**
- `city`, `latitude`, `longitude`, `zipcode`, `population`

**Service Usage:**
- `internetservice`, `phoneservice`, `multiplelines`, `streamingmovies`, `streamingtv`, `streamingmusic`

**Service Add-ons:**
- `onlinesecurity`, `onlinebackup`, `deviceprotection`, `techsupport`

**Contract & Billing:**
- `contract`, `paymentmethod`, `paperlessbilling`, `monthlycharges`, `tenure`

**Financial:**
- `totalcharges`, `totalrevenue`, `cltv`, `totalrefunds`

**Target Variable:**
- `churn` (Yes/No atau 1/0)

---

## 🔍 Key Findings

### 📊 EDA Insights - Demografi

**Profil Pelanggan Berisiko Tinggi:**
1. **Senior Citizen (60+ tahun)** memiliki churn rate signifikan lebih tinggi
2. **Single & No Dependents** paling rentan churn (kurang sticky)
3. **Satisfaction Score 1-3** → 90%+ berisiko churn (zona bahaya)

**Gender:** Tidak ada perbedaan signifikan antara pria dan wanita

### 🗺️ EDA Insights - Geografi

**Hotspot Churn:**
- **San Diego** → Churn tertinggi (anomali mengingat populasi < LA)
- **Los Angeles** → Churn tinggi (sesuai populasi besar)
- **Southern California** → Konsentrasi churn terbesar

**Rekomendasi:** Audit jaringan dan kompetitor di San Diego & LA Selatan

### 💡 Churn Reason Analysis

**Top Churn Categories:**
1. **Competitor (45%)** - Penawaran lebih baik, device lebih menarik
2. **Attitude (16.8%)** - Pengalaman buruk dengan support staff
3. **Dissatisfaction (16.2%)** - Kualitas produk & jaringan
4. **Price (11.3%)** - Harga terlalu tinggi
5. **Other (10.7%)** - Alasan lainnya

**Insight:** Churn lebih banyak dipicu faktor **kompetitor & layanan** dibanding harga

### 🎯 Contract & Payment Insights

**Contract Type vs Churn:**
- **Month-to-month:** 42.7% churn rate ⚠️
- **One year:** 11.3% churn rate
- **Two year:** 2.8% churn rate ✅

**Payment Method vs Churn:**
- **Electronic check:** 45.3% churn rate ⚠️
- **Auto-payment (Bank/CC):** ~15% churn rate ✅

**Paperless Billing:** 33.6% churn (vs 16.3% non-paperless)

---

## 🤖 Machine Learning Results

### Model Terbaik: **Logistic Regression + RandomUnderSampler**

**Hyperparameters:**
```python
{
    'C': 1000,
    'penalty': 'l1',
    'solver': 'liblinear',
    'max_iter': 100,
    'max_features': 15
}
```

### Performance Metrics

| Metric | Train | Test |
|--------|-------|------|
| **Accuracy** | 94.36% | 94.75% |
| **Precision** | 85.13% | 86.23% |
| **Recall** | 95.38% | 95.45% |
| **F1-Score** | 89.97% | 90.61% |
| **F2-Score** | 93.14% | 93.46% |

### Business Impact

**Tanpa Model:**
- Total Loss: **$10,971**
- Semua pelanggan diberi treatment retensi (tidak efisien)

**Dengan Model:**
- Total Loss: **$1,505**
- Penghematan: **$9,466** (86.3% reduction)
- **7.29x lebih efektif** dibanding tanpa model

### Feature Importance (Top 10)

1. **satisfactionscore** (-) → Kepuasan tinggi = churn rendah
2. **onlinesecurity_Yes** (-) → Add-on security = lebih loyal
3. **numberofreferrals** (-) → Banyak referral = lebih engaged
4. **tenure** (-) → Masa langganan lama = loyal
5. **referredafriend** (+) → Indikator kompleks
6. **internetservice_Fiber optic** (+) → Segmen berisiko
7. **paperlessbilling_Yes** (+) → Pelanggan fleksibel (mudah pindah)
8. **streamingmusic** (+) → Standalone service (kurang sticky)
9. **multiplelines_Yes** (-) → Bundle = lebih loyal
10. **techsupport_Yes** (-) → Add-on support = retensi lebih baik

---

## 💼 Business Recommendations

### 🎯 Strategi Retensi Prioritas

**1. Fokus pada Month-to-Month Customers**
- Tawarkan **upgrade ke kontrak 1-2 tahun** dengan insentif
- Bundling paket dengan diskon menarik

**2. Migrasi ke Auto-Payment**
- Target pelanggan **Electronic Check** (churn 45%+)
- Berikan **cashback/diskon** untuk switch ke auto-payment

**3. Service Add-on sebagai Retensi Tool**
- **Tech Support** dan **Online Security** terbukti menurunkan churn
- Free trial/bundling untuk pelanggan berisiko tinggi

**4. Program "Silver Support" untuk Lansia**
- Layanan customer support **prioritas dan humanis** (bukan bot)
- Edukasi teknologi yang lebih intensif

**5. Bundling Keluarga**
- Promo agresif untuk pelanggan **Single & No Dependents**
- Incentive untuk mengajak keluarga bergabung

**6. Customer Satisfaction Program**
- **Monitoring pelanggan rating ≤3** (zona bahaya)
- Quick response team untuk handling komplain

**7. Investigasi Geografis**
- Audit kualitas jaringan di **San Diego & LA Selatan**
- Riset kompetitor di area hotspot churn

### 📊 Implementasi Model

**Workflow:**
1. **Scoring bulanan/mingguan** semua pelanggan
2. **Segmentasi** berdasarkan churn probability:
   - High risk (>70%): Personal outreach + promo agresif
   - Medium risk (40-70%): Email campaign + loyalty program
   - Low risk (<40%): Standard engagement
3. **A/B testing** strategi retensi per segmen
4. **Monitor ROI** program retensi vs biaya akuisisi


## 🛠️ Tech Stack

**Data Processing & Analysis:**
- Python 3.13
- pandas, numpy
- scipy, statsmodels

**Visualization:**
- matplotlib, seaborn
- folium (geospatial heatmap)
- Tableau Public

**Machine Learning:**
- scikit-learn
- XGBoost
- imbalanced-learn
- SHAP, LIME

**Deployment:**
- Streamlit
- pickle (model persistence)

---

## 📱 Live Demo & Resources

- **🌐 Interactive Prediction App:** [Streamlit](https://telcobeta.streamlit.app/)
- **📊 Interactive Dashboard:** [Tableau Public](https://public.tableau.com/views/TelcoCustomerDashboard_17706500189310/Home)
- **🎤 Project Presentation:** [Canva](https://www.canva.com/design/DAHA1t4vfG4/9u-LAc0nukx-1IARdZsJ9w/edit)

---

## 👥 Team

Project ini merupakan kolaborasi tim untuk Final Project Purwadhika Data Science Program yaitu:
Muhammad Zulfan Alghifari JCDSBDGAM-009-005 (zulfanghifari29@gmail.com)
Hashfi Putraza Hikmat JCDSBDGAM-09-001 (hashfiputrazah@gmail.com)
Muhamad Wildan Trisianly JCDS-0808-006 (wildan.trisianly@gmail.com)

---

## 📚 References

1. Investopedia. (2023). [Churn Rate Definition](https://www.investopedia.com/terms/c/churnrate.asp)
2. Statista. (2022). [Customer churn rate by industry](https://www.statista.com/statistics/816735/customer-churn-rate-by-industry-us/)
3. Harvard Business Review. (2014). [The Value of Keeping the Right Customers](https://hbr.org/2014/10/the-value-of-keeping-the-right-customers)
4. IBM. (2023). [Customer Churn Prediction Using Machine Learning](https://www.ibm.com/topics/customer-churn)

---

## 📊 Dokumentasi Dashboard
![WhatsApp Image 2026-02-09 at 20 46 49](https://github.com/user-attachments/assets/dbcda58d-57f9-44e8-baf3-2d7a21724791)
![WhatsApp Image 2026-02-09 at 20 47 18](https://github.com/user-attachments/assets/7c9a10df-3419-40e9-858e-c60c2f2135e7)
![WhatsApp Image 2026-02-09 at 21 18 11](https://github.com/user-attachments/assets/57f2a073-786b-470d-8819-3c046cda4995)
![WhatsApp Image 2026-02-09 at 22 21 12](https://github.com/user-attachments/assets/7d096c03-c2ee-4886-b670-2377fbc652bd)

## 📄 License

This project is for educational purposes as part of Purwadhika Data Science Final Project.

---

**Last Updated:** February 2026
