# PaySim Finansal Dolandırıcılık Tespiti (AML) - LightGBM & XGBoost

Bu proje, sentetik bir finansal veri seti olan **PaySim** kullanarak şüpheli işlemleri (kara para aklama ve dolandırıcılık) tespit etmek amacıyla geliştirilmiştir. Proje kapsamında veri analizi (EDA), veri ön işleme ve makine öğrenmesi modelleri (LightGBM ve XGBoost) uygulanmıştır.

## 🚀 Proje Hakkında

Finansal kuruluşlar için dolandırıcılık tespiti kritik bir öneme sahiptir. Bu projede, milyonlarca işlem arasından dolandırıcılık belirtisi gösteren işlemleri yüksek doğrulukla tespit edebilen modeller eğitilmiştir.

### Kullanılan Teknolojiler
- **Python** (Pandas, NumPy, Scikit-learn)
- **LightGBM** (Ana model)
- **XGBoost** (Alternatif model)
- **Matplotlib & Seaborn** (Veri görselleştirme)
- **Jupyter Notebook**

## 📊 Veri Seti Özellikleri

Projede kullanılan `paysim.csv` veri seti şu sütunları içermektedir:
- **step:** Zaman birimi (1 step = 1 saat).
- **type:** İşlem türü (CASH_IN, CASH_OUT, DEBIT, PAYMENT, TRANSFER).
- **amount:** İşlem tutarı.
- **nameOrig / nameDest:** İşlemi başlatan ve karşı tarafın kimlik bilgileri.
- **oldbalanceOrg / newbalanceOrig:** Gönderenin işlem öncesi ve sonrası bakiyesi.
- **oldbalanceDest / newbalanceDest:** Alıcının işlem öncesi ve sonrası bakiyesi.
- **isFraud:** Hedef değişken (1: Dolandırıcılık, 0: Normal).

### Önemli Bulgular
- Veri seti oldukça dengesizdir (Dolandırıcılık oranı oldukça düşüktür).
- Dolandırıcılık vakalarının sadece `TRANSFER` ve `CASH_OUT` işlem türlerinde gerçekleştiği tespit edilmiştir.
- Bu nedenle model eğitimi sırasında veriler bu işlem türlerine göre filtrelenmiştir.

## 🛠️ Kurulum

Projeyi yerel makinenizde çalıştırmak için:

1. Depoyu klonlayın:
   ```bash
   git clone https://github.com/kullanici-adiniz/aml-xgboost.git
   ```
2. Gerekli kütüphaneleri yükleyin:
   ```bash
   pip install pandas numpy scikit-learn lightgbm xgboost matplotlib seaborn
   ```
3. `lightGBM_AML.ipynb` dosyasını Jupyter Notebook veya Google Colab ile açın.

## 📁 Proje Yapısı

- `lightGBM_AML.ipynb`: Veri analizi, görselleştirme ve model eğitim süreçlerini içeren ana notebook.
- `full_pipeline.pkl`: Veri ön işleme adımlarını (scaling, encoding vb.) içeren kaydedilmiş pipeline dosyası.
- `model_xgb.json`: Eğitilmiş XGBoost modelinin JSON formatındaki yedeği.

## 📈 Model Performansı

Dolandırıcılık tespiti gibi dengesiz veri setlerinde (Fraud oranı %0.1'den az), modelin başarısını ölçmek için **F1-Score** ve **Recall** metrikleri temel alınmıştır.

### **XGBoost (Ana Model)**
Projede final modeli olarak sunulan ve `model_xgb.json` olarak kaydedilen XGBoost modelinin sonuçları:
*   **Test F1-Score:** `%77.40`
*   **Eğitim (Train) F1-Score:** `%99.99`
*   **Doğruluk (Accuracy):** `%99.90+`

### **Karşılaştırmalı Analiz**
Notebook içerisinde yapılan testlerde farklı modellerin sunduğu performanslar:

| Model | Test F1-Score | Test Recall | Accuracy |
| :--- | :---: | :---: | :---: |
| **XGBoost** | **%77.40** | **%64.00** | %100 |
| **Random Forest** | %82.00 | %70.00 | %100 |
| **Lojistik Regresyon** | %7.90 | %90.00* | %94.00 |

*\*Lojistik Regresyon SMOTE ile eğitildiği için yüksek Recall vermiştir ancak çok fazla yanlış pozitif (False Positive) ürettiği için F1-Skoru düşük kalmıştır.*

---
*Bu proje eğitim ve araştırma amaçlı geliştirilmiştir.*

