# Kredi Kartı Temerrüt Tahmini (Credit Card Default Prediction)

Bu proje, Tayvan kredi kartı sahiplerinin temerrüt (default) durumunu tahmin etmek amacıyla makine öğrenmesi tekniklerini kullanan bir sınıflandırma projesidir.

## 📊 Proje Özeti

Projenin amacı, kredi kartı sahiplerinin finansal ve demografik verilerini kullanarak bir sonraki ay ödeme yapıp yapamayacaklarını (default durumunu) tahmin etmektir. Bu tür modeller, bankalar ve finans kurumları için risk yönetiminde kritik öneme sahiptir.

## 📁 Veri Seti

**Kaynak:** Taiwan Credit Card Default Dataset  
**Dosya:** `data/credit_card_default_taiwan.csv`

### Özellikler (Features)

| Özellik | Açıklama |
|---------|----------|
| `LIMIT_BAL` | Verilen kredi miktarı (Tayvan doları) |
| `SEX` | Cinsiyet (1=erkek, 2=kadın) |
| `EDUCATION` | Eğitim durumu (1=lisansüstü, 2=üniversite, 3=lise, 4=diğer) |
| `MARRIAGE` | Medeni durum (1=evli, 2=bekar, 3=diğer) |
| `AGE` | Yaş |
| `PAY_0 - PAY_6` | Geçmiş ödeme durumları (-1=zamanında ödeme, 1-9=ay gecikme) |
| `BILL_AMT1 - BILL_AMT6` | Aylık fatura tutarları |
| `PAY_AMT1 - PAY_AMT6` | Aylık ödeme tutarları |

### Hedef Değişken (Target)

- `Y` (default payment next month): Bir sonraki ay temerrüt durumu (1=evet, 0=hayır)

### Veri Dağılımı

- **Temerrüt yok (0):** %77.88
- **Temerrüt var (1):** %22.12

## 🛠️ Kullanılan Teknolojiler

- **Python 3.x**
- **pandas** - Veri manipülasyonu
- **numpy** - Sayısal işlemler
- **scikit-learn** - Makine öğrenmesi modelleri
- **matplotlib** - Görselleştirme

## 📈 Model Geliştirme Süreci

### 1. Veri Ön İşleme
- Eksik verilerin temizlenmesi
- Veri tiplerinin dönüştürülmesi
- Train/Test ayrımı (%80/%20, stratified sampling)

### 2. Baseline Model
- **DummyClassifier** (most_frequent strategy)
- Accuracy: %78 (ancak sadece çoğunluk sınıfını tahmin ettiği için yanıltıcı)

### 3. Logistic Regression
- StandardScaler ile ön işleme
- `class_weight='balanced'` kullanarak dengesiz veri setine uyum
- GridSearchCV ile hiperparametre optimizasyonu

### 4. Random Forest
- Ensemble yöntemi ile daha güçlü tahminler
- Feature importance analizi

## 📊 Model Performansı

### Logistic Regression (Optimized)
```
              precision    recall  f1-score   support
           0       0.87      0.70      0.77      4673
           1       0.37      0.62      0.46      1327
    accuracy                           0.68      6000
   macro avg       0.62      0.66      0.62      6000
weighted avg       0.76      0.68      0.70      6000

ROC-AUC: 0.708
```

## 🚀 Nasıl Çalıştırılır

### Gereksinimler
```bash
pip install pandas numpy scikit-learn matplotlib
```

### Jupyter Notebook'u Çalıştırma
```bash
jupyter notebook ml-credit-risk-prediction.ipynb
```

## 📂 Proje Yapısı

```
ml-credit-risk-prediction/
├── data/
│   └── credit_card_default_taiwan.csv
├── ml-credit-risk-prediction.ipynb
├── README.md
└── .gitignore
```

## 🎯 Sonuç ve Öneriler

1. **Dengesiz Veri Sorunu:** Veri seti dengesiz olduğu için `class_weight='balanced'` kullanımı kritiktir.
2. **Feature Engineering:** Ödeme geçmişi özellikleri en önemli tahmin ediciler olarak öne çıkmaktadır.
3. **Model Seçimi:** Logistic Regression, yorumlanabilirlik açısından avantajlı; Random Forest ise performans açısından daha iyi sonuç verebilir.

## 📝 Lisans

Bu proje eğitim amaçlıdır.