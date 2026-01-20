# ML-Akilli-Ev-Enerji-Tuketimi-Tahmini

Bu projede bir akıllı ev sistemine ait enerji tüketim verileri kullanılrak, evin toplam elektrik tüketimi (use [kW]) tahmin edilmeye çalışılmıştır.
projenin amacı farklı saatlerde ve hava koşullarında oluşan normaltüketim alışkanlığını sayısal bir referans (baseline) olarak modele öğretmektir.
Bu sebepten pivot tablo kullanımı özellikle tercih edilmiştir.


## kullanılan veri seti

veri seti yaklaşık 40.000 satır ve 32 sütundan oluşmaktadır.
Bu veri seti; zaman bilgisi, ev içi toplam enerji tüketimi, hava durumu verileri (sıcaklık, nem, basınç vb.), hava durumu özet bilgileri (summary, icon) gibi 
bilgiler içermektedir.


## veri ön işleme

Veriye şu işlemleri uyguladım:
1.eksik verileri veri setinden çıkardım.
2.unix formatındaki time sütununu, tarih-saat formatına çevrdim.
3.saat ve ay bilgileri ayrı sütunlar olarak elde ettim.
4.Kategorik verileri (summary, icon) label encod,ng yöntemi ile sayısal hale getirttim.


## pivot tablo (baseline oluşturma)

saatlere göre ortalama ev tüketimi hesaplanmıştır.
bu işlem için pivot tablo kullandım:

- satırlar: Saatler (0–23)
- değerler: `use [kW]`
- İşlem: Otalama (mean)

Bu pivot tablo sayesinde her saat için "Bu saatte evin normalde ne kadar elektrik tükettiği bilgisini" elde ettim.
Elde edilen bu saatlik ortalama tüketim (baseline), ana veri setine yeni bir özellik olarak ekledim.


## kullanılan özellikler (features)

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

1. Random forest regressor
2. 2. K-nearest neighbors (KNN)

## Model Sonuçları

![Sonuclar](/images/img1.png)

sonuc: toplam ev tüketimi, birçok cihazın anlık ve kullanıcıya bağlı çalışması nedeniyle tam olarak tahmin edilmesi zor bir değişkendir.
Bu nedenle elde edilen r^2 değerleri beklenen seviyededir.


## Grafikler

### 1. Saatlere göre ortalama ev tüketimi (Baseline)

Bu grafik, pivot tablo kullanılarak elde edilen saatlik ortalama tüketim değerlerini göstermektedi.

![saatlik ort tuketim](/images/img2.png)


### 2. gerçek değerler vs model tahminleri

İlk 50 test verisi için gerçek tüketim değerlerini ve random Forest modelinin tahminleri karşılaştırılmıştır.

![gercekvstahmin](/images/img3.png)


### 3. özellik önem düzeyleri (feature ımportance)

Random Forest modeli kullanılrak,modelin karar verirken hangi özelliklere daha fazla önem verdiği analiz edilmiştir.
sonuçlara göre: basınç , sıcaklık, nemi, saatlik baseline bilgisi model üzerinde onemli bir etkiye sahiptir

![featureimp](/images/img4.png)


## Genel Değerlendirme

Bu projede pivot tablo kullanılarak saat bazlı baseline oluşturulmuştur. sonra bu baseline bilgisi modele eklenerek tahmin süreci desteklenmiştir.
Uygun modeller tercih edilmiş ve analiz edilmiştir. sonuçlar da grafiklerle yorumlanabilir hale getirilmiştir.
burasaki amaç, enerji tüketiminin zamansal ve çevresel koşullarla olan ilişkisini anlamlandırmaktır.

## kütüphaneler

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

## sertifikalarım

| ![sertifika1](/images/setifika1.png) | ![sertifka2](/images/setifika2.png) |
