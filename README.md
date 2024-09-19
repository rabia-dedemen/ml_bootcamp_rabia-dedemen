Dünya'ya Yakın Cisimler (1910-2024) Tehlike Sınıflandırması

Bu proje, NASA'nın Dünya'ya Yakın Cisimler verisetini kullanarak nesneleri tehlikeli veya tehlikesiz olarak sınıflandırmak için çeşitli makine öğrenimi modellerini kullanmaktadır. Veriseti, her bir cismin mutlak parlaklığı, tahmini çapları, göreceli hızı ve Dünya'ya yakın geçiş mesafesi gibi bilgileri ve tehlikeli olup olmadığı sınıflandırmasını içermektedir.

## Veriseti
Bu projede kullanılan veri NASA'nın 1910-2024 yıllarındaki Dünya'ya Yakın Cisimler veriseti olup, [Kaggle](https://www.kaggle.com/datasets) üzerinden indirilebilir.

### Veriseti Sütunları:
- **neo_id**: Her nesne için benzersiz bir kimlik.
- **name**: Nesnenin adı.
- **absolute_magnitude**: Nesnenin mutlak parlaklığı.
- **estimated_diameter_min**: Tahmini minimum çap (kilometre cinsinden).
- **estimated_diameter_max**: Tahmini maksimum çap (kilometre cinsinden).
- **orbiting_body**: Nesnenin yörüngesinde döndüğü gök cismi (tüm girdiler için Dünya).
- **relative_velocity**: Nesnenin göreceli hızı (kilometre/saat cinsinden).
- **miss_distance**: Nesnenin Dünya'ya olan en yakın geçiş mesafesi (kilometre cinsinden).
- **is_hazardous**: Nesnenin tehlikeli olup olmadığını belirten bir bool değeri (True/False).

### Veri Ön İşleme

Veri ilk olarak eksik değerlerin temizlenmesiyle işlenir. Daha sonra şu adımlar gerçekleştirilir:

    Gereksiz Sütunların Kaldırılması: neo_id, name ve orbiting_body gibi sütunlar sınıflandırma görevine katkı sağlamadığı için çıkarılır.
    Aykırı Değerlerin İşlenmesi: İstatistiksel yöntemler (IQR) kullanılarak aykırı değerler kaldırılır.
    Veri Dengesizliği: Verisetinde tehlikesiz cisimler tehlikeli olanlardan daha fazla olduğundan, SMOTE (Sentetik Azınlık Aşırı Örnekleme Yöntemi) kullanılarak sınıflar dengelenir.
Model Eğitimi

Birden fazla makine öğrenimi modeli denenmiştir:

    Lojistik Regresyon
    Karar Ağacı
    K-En Yakın Komşu (KNN)
    K-Means Clustering

Supervised her model 5 katlı çapraz doğrulama ile değerlendirilmiş ve en yüksek doğruluk oranını Karar Ağacı modeli elde etmiştir.
En İyi Model: Karar Ağacı Sınıflandırıcı

    Çapraz doğrulama doğruluğu: %94.46
    Dengelenmiş veri üzerinde SMOTE kullanılarak eğitilmiştir.

### Değerlendirme

Gösterdiği düşük performanstan dolayı unsupervised yaklasımın bu dataset için uygun olmadığına karar verilmiştir.
Son Karar Ağacı modeli, yeniden örneklenmiş eğitim verisi üzerinde eğitilmiş ve ayrı bir test seti üzerinde değerlendirilmiştir. Kullanılan değerlendirme metrikleri:

    Doğruluk: %95
    Kesinlik: %95
    Duyarlılık: %95
    F1 Skoru: %95

Bu metrikler hem tehlikeli hem de tehlikesiz sınıflarda dengeli sonuçlar vermiştir.
Sonuçlar

    Tehlikeli vs Tehlikesiz Dağılımı: Veriseti oldukça dengesizdi, ancak SMOTE kullanılarak denge sağlandı ve model performansı iyileştirildi.
    Karar Ağacı Sınıflandırıcı en iyi performans gösteren model olarak seçildi ve çapraz doğrulama setinde %94.46, test setinde %95 doğruluk elde etti.
