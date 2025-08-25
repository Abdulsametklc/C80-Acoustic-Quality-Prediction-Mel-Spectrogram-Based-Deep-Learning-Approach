# 🎵 C80 Akustik Kalite Tahmini – Mel Spektrogram Tabanlı Derin Öğrenme

Bu proje, bir konser salonundaki koltukların **C80 akustik kalite değerlerini** tahmin etmeyi amaçlar.  
C80 değerleri, **Mel spektrogram** görüntüleri (feature) kullanılarak derin öğrenme ile modellenir.  
Eksik ölçüm verileri, **PyTorch tabanlı CNN modeli** ile doldurulur.

---

## 📌 Proje Amacı
Konser salonlarındaki akustik kalitesinin değerlendirilmesi, hem seyirci deneyimi hem de akustik tasarım açısından kritiktir.  
Bu proje ile:
- Eksik C80 ölçümlerinin tahmin edilmesi
- Frekans, koltuk konumu ve mel spektrogram verilerinin birleştirilerek daha doğru tahmin yapılması
- Tahmin sonrası ısı haritaları ile akustik kalite dağılımının görselleştirilmesi hedeflenmiştir.

---

## 📂 Veri Seti Yapısı
- **acoustic_matrix**: (11x24) boyutunda, her hücrede C80 değeri (dB). Eksik veriler NaN.
- **mel_matrix**: (11x24) boyutunda, her hücrede mel spektrogram görüntüsü (RGB/RGBA, 600x1500 piksel).
- **info**: İstatistiksel meta bilgiler (ortalama, min, max C80, dolu koltuk sayısı vb.)

---

## 🛠 Kullanılan Teknolojiler
- **Python 3**
- **PyTorch** (EfficientNet-B0 backbone)
- **Torchvision** (görüntü ön işleme)
- **NumPy / Pandas**
- **Matplotlib** (görselleştirme)
- **Google Colab** (eğitim ve deneyler)
- **CUDA GPU** (hızlı eğitim için)

---

## 📊 Model Mimarisi
- **Backbone**: EfficientNet-B0 (ImageNet ön-eğitimli)
- **Ek Özellikler**:
  - Frekans bilgisi (one-hot encoding)
  - Koltuk konumu (normalize edilmiş)
- **Çıkış**: Tek bir C80 değeri (float)

---

## 🚀 Eğitim Süreci
1. **Veri yükleme** – Tüm .npy dosyaları okunur, mel ve C80 verileri eşleştirilir.
2. **Ön işleme** – Mel spektrogramlar normalize edilir ve 224x224 boyutuna getirilir.
3. **Model eğitimi** – AdamW optimizasyonu ve L1 Loss ile eğitim yapılır.
4. **Erken durdurma** – Val MAE metrik takibine göre en iyi model kaydedilir.
5. **Tamamlama** – Eksik C80 değerleri model tahmini + IDW interpolasyon ile doldurulur.

---

## 📈 Metrikler
- **MAE (Mean Absolute Error)** – Ortalama mutlak hata
- **RMSE (Root Mean Square Error)** – Karekök ortalama kare hata
- **±1 dB doğruluk** – Tahmin ile gerçek değer arasındaki farkın 1 dB’den küçük olma oranı

---

## 🖼 Görselleştirme
- **Önce/Sonra C80 ısı haritaları**
- Frekans bazlı doğruluk analizi
- Eksik veri oranlarının azalması
