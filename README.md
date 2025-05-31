# Borsa Kapanış Fiyatlarının LSTM ile Tahmini

Bu proje, finansal zaman serisi verilerini kullanarak Apple, Netflix ve Microsoft gibi NASDAQ hisselerinin kapanış fiyatlarını Long Short-Term Memory (LSTM) tabanlı bir modelle tahmin etmeyi amaçlamaktadır.

## İçerik

- [Kullanılan Ortam ve Kütüphaneler](#kullanılan-ortam-ve-kütüphaneler)
- [Veri Seti](#veri-seti)
- [Zaman Serisi Dönüşümü](#zaman-serisi-dönüşümü)
- [Model Mimarisi](#model-mimarisi)
- [Model Eğitimi](#model-eğitimi)
- [Performans ve Değerlendirme](#performans-ve-değerlendirme)
- [Model Bağlantıları](#model-bağlantıları)
- [Referanslar](#referanslar)

---

## Kullanılan Ortam ve Kütüphaneler

- **Geliştirme Ortamı**: [Kaggle](https://www.kaggle.com/)
- **Framework**: PyTorch
- **Görselleştirme**: Matplotlib
- **Ölçekleme**: Scikit-learn (MinMaxScaler)
- **Takip Araçları**: Weights & Biases, Huggingface

## Veri Seti

- Kaynak: [Stock Market Data on Kaggle](https://www.kaggle.com/datasets/paultimothymooney/stock-market-data)
- İçerik: NASDAQ, NYSE, S&P500 vb. piyasalardan 50 yıllık hisse senedi verisi
- Kullanılan Özellik: Kapanış fiyatı
- Ön İşleme: 
  - Gereksiz sütunların kaldırılması
  - Min-Max normalizasyonu (0-1)

## Zaman Serisi Dönüşümü

Veriler `window_size` kadar geçmiş kapanış fiyatını içerecek şekilde zaman serisi örneklerine dönüştürülmüştür. LSTM katmanı için 3 boyutlu tensörlere çevrilmiştir.

## Model Mimarisi

- **Model Türü**: Çift yönlü (bidirectional) LSTM
- **Hidden Size**: 64
- **Head Layer**: Fully Connected + ReLU + Output Layer
- **Kayıp Fonksiyonu**: MSE
- **Optimizer**: Adam

Alternatif mimariler (RNN, GRU, Transformer) değerlendirilmiş, ancak hesaplama maliyeti, bağlam modelleme yeteneği ve veri miktarına göre LSTM tercih edilmiştir.

## Model Eğitimi

- **Epoch**: Maksimum 250 (Early Stopping: patience=15)
- **Doğrulama Takibi**: Validation kaybına göre en iyi model `best_model.pth` dosyasında tutulmuştur.
- **Görselleştirme**: Eğitim süreci loglarla izlenmiştir.

## Performans ve Değerlendirme

Modeller hem fiyat seviyesi hem de trend yönü (iniş/çıkış) açısından başarılı sonuçlar vermektedir. Ancak fiyatların dışına taşan değerlerde normalizasyon nedeniyle sapmalar gözlenmiştir.

## Model Bağlantıları

- [Netflix (NFLX)](https://huggingface.co/kaanrkaraman/nflx-stock-price-prediction)
- [Apple (AAPL)](https://huggingface.co/kaanrkaraman/aapl-stock-price-prediction)
- [Microsoft (MSFT)](https://huggingface.co/kaanrkaraman/msft-stock-price-prediction)

## Referanslar

- Hochreiter & Schmidhuber (1997), *Long Short-Term Memory*
- Kingma & Ba (2017), *Adam Optimizer*
- Vaswani et al. (2017), *Attention Is All You Need*
- Diğer kaynaklar için: Raporun sonunda yer alan referans listesi

---

> **Not**: Bu çalışma Python Programlamaya Giriş dersi kapsamında gerçekleştirilmiştir.
