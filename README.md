# ML-Akilli-Ev-Enerji-Tuketimi-Tahmini

Bu projede bir akıllı ev sistemine ait enerji tüketim verileri kullanılrak, evin toplam elektrik tüketimi (`use [kW]`) tahmin edilmeye çalışılmıştır.
projenin amacı farklı saatlerde ve hava koşullarında oluşan “normal” tüketim alışkanlığını sayısal bir referans (baseline) olarak modele öğretmektir.
Bu sebepten pivot tablo kullanımı özellikle tercih edilmiştir.


## Kullanılan Veri Seti

veri seti yaklaşık 40.000 satır ve 32 sütundan oluşmaktadır.

içerdiği başlıca biligler:
- zaman bilgisi (unix time)
- ev içi toplam enerji tüketimi
- hava durumu verileri (sıcaklık, nem, basınç vb.)
- hava durumu özet bilgileri (summary, icon)


## Veri Ön İşleme

Projede aşağıdaki ön işlemler yapılmıştır:

- eksik veriler veri setinden çıkarılmıştır.
- unix formatındaki time sütunu, tarih-saat formatına çevrilmiştir.
- Saat ve ay bilgileri ayrı sütunlar olarak elde edilmiştir.
- Kategorik veriler (`summary`, `icon`) label encod,ng yöntemi ile sayısal hale getirilmiştir.


## Pivot Tablo (baseline oluşturma)

saatlere göre ortalama ev tüketimi hesaplanmıştır.
bu işlem için pivot tablo kullandım:

- satırlar: Saatler (0–23)
- değerler: `use [kW]`
- İşlem: Otalama (mean)

Bu pivot tablo sayesinde her saat için "Bu saatte evin normalde ne kadar elektrik tükettiği bilgisi" elde edilmiştir.
Elde edilen bu saatlik ortalama tüketim (baseline), ana veri setine yeni bir özellik olarak ekledim.


## Kullanılan Özellikler (Features)

Modelde aşağıdaki özellikler kullanılmıştır:

- temperature  
- humidity  
- visibility  
- pressure  
- hour  
- month  
- summary_encoded  
- hourly_baseline  

Tahmin edilmeye çalışılan hedef değişken: use [kW] (Toplam ev tüketimi)


## Kullanılan Modeller

Veriyi %80 eğitim ve %20 test olacak şekilde ayırdım. Daha sonrasında iki farklı regresyon modeli kullandım:

1. Random Forest Regressor
2. 2. K-Nearest Neighbors (KNN)

## Model Sonuçları

![Sonuclar](img1.png)

sonuc: toplam ev tüketimi, birçok cihazın anlık ve kullanıcıya bağlı çalışması nedeniyle tam olarak tahmin edilmesi zor bir değişkendir.
Bu nedenle elde edilen r^2 değerleri beklenen seviyededir.


## Grafikler

### 1. Saatlere Göre Ortalama Ev Tüketimi (Baseline)

Bu grafik, pivot tablo kullanılarak elde edilen saatlik ortalama tüketim değerlerini göstermektedir.

![Saatlik Ortalama Tüketim](img2.png)


### 2. Gerçek Değerler vs Model Tahminleri

İlk 50 test verisi için gerçek tüketim değerlerini ve random Forest modelinin tahminleri karşılaştırılmıştır.

![Gerçek vs Tahmin](img3.png)


### 3. Özellik Önem Düzeyleri (Feature Importance)

Random Forest modeli kullanılraak,modelin karar verirken hangi özelliklere daha fazla önem verdiği analiz edilmiştir.
sonuçlara göre: basınç , sıcaklık, nemi, saatlik baseline bilgisi model üzerinde onemli bir etkiye sahiptirç

![Feature Importance](img4.png)


## Genel Değerlendirme

Bu projede pivot tablo kullanılarak saat bazlı baseline oluşturulmuştur. sonra bu baseline bilgisi modele eklenerek tahmin süreci desteklenmiştir.
Basit ve anlaşılır modeller tercih edilmiştir. Sonuçlar grafiklerle yorumlanabilir hale getirilmiştir.
Amaç, enerji tüketiminin zamansal ve çevresel koşullarla olan ilişkisini anlamlandırmaktır.

## kütüphaneler

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

## sertifikalarım

| ![sertfka](sertifika1.png) | ![sertifka](sertifika2.png)
