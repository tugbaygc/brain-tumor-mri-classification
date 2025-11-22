# Akbank Derin Öğrenme Bootcamp - Beyin Tümörü Sınıflandırma ve XAI Projesi

Bu proje, **Akbank Derin Öğrenme Bootcamp** kapsamında geliştirilmiş uçtan uca bir derin öğrenme projesidir. Projenin temel amacı, beyin MR (Manyetik Rezonans) görüntülerini analiz ederek tümör tespiti yapmak ve **Grad-CAM** tekniği ile modelin karar mekanizmasını açıklanabilir (Explainable AI) hale getirmektir.

## 1. Projenin Amacı

Sağlık alanında yapay zeka kullanımının en kritik noktalarından biri "güvenilirlik"tir. Bu projede sadece yüksek doğruluklu bir CNN modeli geliştirmekle kalınmamış, aynı zamanda *"Model bu kararı neden verdi?"* sorusuna yanıt aramak için ısı haritaları (heatmap) oluşturulmuştur.

Hedeflenen 4 ana sınıf şunlardır:
* **Glioma**
* **Meningioma**
* **Pituitary (Hipofiz)**
* **No Tumor (Tümör Yok)**

## 2. Veri Seti Hakkında Bilgi

Projede Kaggle üzerinde halka açık olarak sunulan **"Brain Tumor MRI Dataset"** kullanılmıştır. Veri seti toplam **7.022 adet** görüntüden oluşmaktadır.

| Sınıf | Açıklama | Görüntü Sayısı |
| :--- | :--- | :--- |
| **glioma** | Glioma tümörü içeren görüntüler | 1.321 |
| **meningioma** | Meningioma tümörü içeren görüntüler | 1.339 |
| **notumor** | Sağlıklı (tümörsüz) beyin görüntüleri | 1.595 |
| **pituitary** | Hipofiz bezi tümörü içeren görüntüler | 1.457 |

## 3. Kullanılan Yöntemler ve Model Mimarisi

Model performansını optimize etmek ve aşırı öğrenmeyi (overfitting) engellemek için aşağıdaki stratejiler izlenmiştir:

* **Transfer Öğrenme (Transfer Learning):** Sıfırdan model eğitmek yerine, ImageNet üzerinde eğitilmiş **VGG16** mimarisi temel alınmıştır.
* **Veri Ön İşleme:** Görüntüler 224x224 boyutuna getirilmiş, normalize edilmiş ve veri çoğaltma (augmentation) teknikleri uygulanmıştır.
* **Fine-Tuning:** VGG16'nın evrişim katmanları dondurulmuş, modele özel Flatten, Dense ve Dropout katmanları eklenmiştir.
* **Açıklanabilirlik (XAI):** Modelin odaklandığı pikselleri görselleştirmek için **Grad-CAM** (Gradient-weighted Class Activation Mapping) algoritması entegre edilmiştir.

## 4. Elde Edilen Test Sonuçları

Model, test veri seti üzerinde **%72 Genel Doğruluk (Accuracy)** oranına ulaşmıştır.

| Metrik | Değer |
| :--- | :--- |
| **Test Doğruluğu (Accuracy)** | **%72.00** |
| **Test Kayıp (Loss)** | **0.78** |

### Sınıf Bazlı Performans Tablosu

| Sınıf | Precision | Recall (Duyarlılık) | F1-Score |
| :--- | :--- | :--- | :--- |
| **glioma** | 0.90 | 0.41 | 0.56 |
| **meningioma** | 0.48 | 0.52 | 0.50 |
| **notumor** | 0.75 | **0.99** | 0.85 |
| **pituitary** | 0.87 | 0.88 | 0.88 |

> **💡 Önemli Bulgular:**
> * Modelimiz, **"No Tumor" (Sağlıklı)** sınıfını **%99 Recall** oranıyla tespit etmektedir. Bu, sağlıklı bir bireye yanlışlıkla "hasta" denilme ihtimalinin çok düşük olduğunu gösterir.
> * **Pituitary (Hipofiz)** tümörlerinde %88 başarı sağlanmıştır.

## 5. Grad-CAM ile Model Görselleştirme

Aşağıdaki örnekte, modelin bir Hipofiz tümörünü tespit ederken MR görüntüsünün hangi bölgesine odaklandığı görülmektedir. Kırmızı/Sarı alanlar, modelin "Tümör burada" dediği bölgeleri temsil eder.

*(Buraya Grad-CAM çıktısı olan görseli ekleyebilirsiniz. Örn: ![][gradcam_resmi])*

## 6. Kaggle Notebook

Projenin kodlarına, eğitim grafiklerine ve detaylı analizlerine aşağıdaki bağlantıdan ulaşabilirsiniz:

https://www.kaggle.com/code/tubayac/cnn-ile-beyin-t-m-r-tespiti-ve-tip-analizi
