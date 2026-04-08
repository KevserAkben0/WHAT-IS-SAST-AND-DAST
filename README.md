# WHAT-IS-SAST-
SAST's general operating logic
---

##  SAST Nedir?

SAST (Static Application Security Testing), kaynak kodu analiz ederek güvenlik açıklarını tespit eden bir yöntemdir. Bu sayede uygulama henüz yayınlanmadan önce hatalar bulunur ve düzeltilir. Bu süreç, güvenli bir yazılım geliştirme yaşam döngüsünün (SDLC) önemli bir parçasıdır.

Örneğin bir uygulamada güvenlik açığı olduğunu düşünelim. Geliştirici bunun farkında olmayabilir ancak bir saldırgan bu açığı keşfederse kullanıcı verileri tehlikeye girebilir. İşte SAST burada devreye girer ve uygulama daha geliştirme aşamasındayken bu tür riskleri önlemeye yardımcı olur.

SAST araçları, `eval()` gibi dinamik kod çalıştıran fonksiyonları AST (Abstract Syntax Tree) üzerinde analiz eder. Eğer bu fonksiyonlara kullanıcıdan gelen ve temizlenmemiş veri giriyorsa, bu durum "Taint Analysis" kapsamında riskli olarak işaretlenir.

---

##  Doğru SAST Aracı Nasıl Seçilir?

Doğru araç seçimi güvenlik tespitlerinin kalitesi açısından kritik öneme sahiptir. Aşağıdaki kriterler dikkate alınmalıdır:

### 1. Dil ve Framework Desteği
Seçilen araç, kullanılan programlama dili ve framework ile tam uyumlu olmalıdır.

### 2. Düşük False Positive Oranı
Yanlış alarmlar geliştirici zamanını boşa harcar. Bu yüzden doğru tespit oranı yüksek araçlar tercih edilmelidir.

### 3. Kural Özelleştirme
Projeye özel güvenlik kuralları tanımlanabilmelidir.

### 4. IDE ve CI/CD Entegrasyonu
Araç, geliştirme ortamına entegre olmalı ve CI/CD süreçlerinde aktif kullanılabilmelidir.

### 5. Hız ve Performans
Büyük projelerde bile hızlı sonuç veren araçlar tercih edilmelidir.

---

##  SAST Analiz Yöntemleri

SAST araçları farklı analiz teknikleri kullanarak güvenlik açıklarını tespit eder:

###  Sözdizimsel ve Anlamsal Analiz
Kod AST yapısına dönüştürülerek güvensiz fonksiyon kullanımları tespit edilir.

###  Veri Akışı Analizi (Data Flow)
Verinin program içerisindeki hareketi izlenir ve mantıksal hatalar belirlenir.

###  Taint (Kirlilik) Analizi
Güvenilmeyen verinin temizlenmeden kritik noktalara ulaşıp ulaşmadığı kontrol edilir.

###  Kontrol Akışı Analizi
Kodun çalışabileceği tüm yollar analiz edilerek yetki atlama gibi riskler bulunur.

###  Yapısal ve Konfigürasyon Analizi
`.yaml`, `.json` gibi dosyalar incelenerek güvenlik açıkları tespit edilir.

###  Prosedürler Arası Analiz
Farklı modüller arasındaki veri akışı analiz edilir.

###  Sembolik Çalıştırma
Kod çalıştırılmadan farklı senaryolar matematiksel olarak test edilir.

###  İşaretçi ve Alias Analizi
Bellek erişimleri kontrol edilerek çakışmalar önlenir.

###  Değer ve Aralık Analizi
Değişkenlerin sınırları analiz edilerek overflow gibi hatalar tespit edilir.

###  İkili Kod ve Bytecode Analizi
Kaynak kod yoksa derlenmiş dosyalar analiz edilir.

---

## 

SAST, güvenliği yazılım geliştirme sürecinin başına taşıyan kritik bir yaklaşımdır.  
Erken tespit edilen açıklar, maliyet ve riskleri büyük ölçüde azaltır.



---
Endpoint-labs intern project

