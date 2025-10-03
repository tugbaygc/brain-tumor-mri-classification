MRI Görüntüleriyle Dört Farklı Beyin Tümörü Sınıflandırması
Bu proje, Manyetik Rezonans Görüntüleme (MRI) verilerini kullanarak dört farklı sınıfı (Glioma, Meningioma, Pituitary ve Notumor) sınıflandırmak için derin öğrenme tabanlı bir Evrişimsel Sinir Ağı (CNN) modelinin geliştirilmesini içerir.

Proje Hedefleri ve Yöntem
Amaç: Verilen MRI görüntülerini doğru tümör tipine atayabilen yüksek doğruluklu bir model oluşturmak.

Yöntem: Temel CNN mimarisi kullanılarak modelin sıfırdan eğitilmesi.

Optimizasyon: Veri Çoğaltma (Data Augmentation) ve Dropout katmanları ile aşırı öğrenmenin (overfitting) kontrol altına alınması.

Model Performansı (Test Seti Sonuçları)
Modelin, daha önce hiç görmediği Test Seti üzerindeki nihai değerlendirme sonuçları aşağıdadır:

Metrik	Sonuç	Yorum
Genel Doğruluk (Test Accuracy)	%73	Aşırı öğrenmeye rağmen elde edilen güçlü bir temel skor.
En İyi Performans (Recall)	Notumor: %97	Modelin tümör olmayan görüntüleri ayırt etme başarısı çok yüksek.
En Zayıf Performans (Recall)	Meningioma: %31	Model, Meningioma vakalarının büyük bir kısmını yanlış sınıflandırmıştır.

Teknik Detaylar
Bileşen	Detay
Veri Seti	4 sınıf (Glioma, Meningioma, Pituitary, Notumor) içeren MR görüntüleri.
Model Mimarisi	2 Evrişimsel bloktan oluşan, sıfırdan oluşturulmuş derin CNN.
Epoch Sayısı	Aşırı öğrenmeyi kontrol etmek için 15 epoch ile eğitim yapılmıştır.
Optimizasyon	Adam Optimizer
Kayıp Fonksiyonu	Categorical Crossentropy
Veri Ön İşleme	Normalizasyon, Döndürme, Kaydırma, Yakınlaştırma (Data Augmentation).

Değerlendirme Çıkarımları ve Gelecek Öneriler
Model, eğitim verisini ezberleme eğilimindedir (Eğitim Doğruluğu: %90+). Bu durumu çözmek için gelecekteki çalışmalarda şu adımlar önerilmektedir:

Dropout Oranlarını Artırma: Aşırı öğrenmeyi daha etkili bir şekilde azaltmak için Dropout oranları yükseltilmelidir.

Transfer Öğrenme: Daha az veriyle daha iyi genelleme sağlamak için VGG16 veya ResNet gibi önceden eğitilmiş modellere (Transfer Learning) geçiş yapılmalıdır.

Sınıf Dengesi: Meningioma sınıfındaki düşük performans, modelin bu tümör tipinin ayırt edici özelliklerini tam olarak öğrenemediğini göstermektedir; bu sınıfa odaklı iyileştirmeler yapılmalıdır.

brain-tumor-mri-classification.ipynb dosyasında tüm kodlar, grafikler (Accuracy/Loss Eğrileri) ve detaylı değerlendirme raporları (Confusion Matrix, Classification Report) bulunmaktadır.
