# WHAT-IS-SAST-AND-DAST?
SAST's general operating logic
---


##  SAST NEDİR?

SAST araçları kodları analiz ederek olası güvenlik açıklarını tespit eder. Bu sayede geliştirilen uygulama herkese açık olarak kullanıma sunulmadan kodlarda bulunan hatalar tespit edilip düzeltile bilinmektedir. Bu süreç, güvenli bir yazılım geliştirme yaşam döngüsünü (SDLC) oluşturur.

Mesela bir uygulamaya giriş yapacaksınız ve uygulama da güvenlik açıkları var. Bunu geliştiren kişinin de bilmediğini ama bir saldırganın şans eseri olarak fark etmesiyle bilgilerinizin çalındığını düşünün. Kötü olurdu değil mi? İşte SAST tam olarak burada önemli çünkü uygulama daha geliştirme aşamasındayken hata tespiti yapılarak olası açıkların önüne geçilmesini sağlar.

SAST araçları, `eval()` gibi 'dinamik kod çalıştıran' fonksiyonları AST (Soyut Sözdizimi Ağacı) üzerinde hemen işaretler. Eğer bu fonksiyonun içine giren veri kullanıcıdan geliyorsa ve temizlenmemişse, bu bir 'Taint Analysis' (Kirlilik Analizi) alarmıdır.

---

Doğru SAST aracını seçmek tespitler için önemlidir. Peki doğru SAST aracı nasıl seçilir? Piyasadaki onlarca araç arasından projeniz için en doğrusuna karar verirken göz önünde bulundurmanız gereken 5 temel kriter şunlardır:

### Dil ve Framework Desteği
Seçtiğiniz araç, projenizin teknoloji yığınıyla tam uyumlu olmalıdır. Sadece programlama dilini değil, kullandığınız framework’lere özgü spesifik zafiyetleri ve yanlış yapılandırmaları da tanıyabilmesi kritik bir detaydır.

### Düşük Yanlış Pozitif (False Positive) Oranı
SAST araçlarının en büyük handikap asılsız alarmlardır. Geliştirici ekibinin zamanını “sahte” güvenlik hatalarını ayıklamakla harcamaması için isabet oranı yüksek bir araç tercih edilmelidir.

### Kural Özelleştirme Esnekliği
Her projenin mimarisi ve iş mantığı farklıdır. Aracın yalnızca standart kurallarla yetinmeyip, kurumunuza ve projenize özel güvenlik kurallarını kolayca yazmanıza izin vermesi büyük bir avantajdır.

### IDE ve CI/CD Entegrasyonu
Güvenlik sonradan eklenen bir yama değil, kod yazım sürecinin doğal bir parçası olmalıdır. Aracınızın kod editörlerine eklenti olarak kurulabilmesi ve CI/CD (Sürekli Entegrasyon/Sürekli Dağıtım) süreçlerinde sürtünmesiz çalışması şarttır.

### Hız ve Performans
Kodunuz her değiştiğinde uzun süren taramaları beklemek çevik geliştirme hızını düşürür. Kod tabanı büyüdükçe performansı düşmeyen, sonuçları hızlıca veren çözümlere yönelmek gerekir.

---

##  SAST SIRASINDA KULLANILAN ANALİZ YÖNTEMLERİ

### Sözdizimsel ve Anlamsal Analiz (Lexical & Semantic)
Analizin ilk aşamasıdır. Kod, bir “Soyut Sözdizimi Ağacı”na (AST) dönüştürülür. Bu sayede sadece kelimeler değil, kodun gramer yapısındaki güvensiz fonksiyon kullanımları (örneğin; eval(), strcpy()) tespit edilir.

### Veri Akışı Analizi (Data Flow)
Bir değişkenin program içindeki yaşam döngüsünü izler. Verinin nerede tanımlandığı, nerede güncellendiği ve nerede tüketildiği takip edilerek mantıksal tutarsızlıklar ve bellek sızıntıları aranır.

### Taint (Kirlilik) Analizi
Güvenlik analizinin “altın standardı”dır. Dış dünyadan (Source) gelen güvenilmeyen girdilerin, bir temizleme (Sanitization) işleminden geçmeden tehlikeli bir fonksiyona (Sink) ulaşıp ulaşmadığını denetler.

### Kontrol Akışı Analizi (Control Flow)
Uygulamanın tüm olası yürütme yollarını (execution paths) haritalandırır. Kodun hangi şartlar altında hangi bloğa gireceğini analiz ederek yetkilendirme atlatma risklerini ve ulaşılamayan kodları bulur.

### Yapısal ve Konfigürasyon Analizi
Yazılım sadece koddan ibaret değildir. Araç; `.yaml`, `.json` gibi yapılandırma dosyalarını inceleyerek zayıf şifreleme algoritmalarını veya hatalı güvenlik başlıklarını raporlar.

### Prosedürler Arası Analiz (Inter-procedural)
Analizi tek bir fonksiyonun kapsamından çıkarır. Farklı sınıflar ve modüller arasındaki karmaşık veri geçişlerini takip ederek, birimler arası entegrasyondan doğabilecek açıkları yakalar.

### Sembolik Çalıştırma (Symbolic Execution)
Kodu fiziksel olarak çalıştırmadan, değişkenlere matematiksel semboller atayarak “ya şu değer gelirse?” senaryolarını simüle eder. En derin ve bulunması en zor mantık hatalarını bu yöntemle çözer.

### İşaretçi ve Alias Analizi
Bellek yönetiminin kritik olduğu dillerde, iki farklı işaretçinin (pointer) aynı bellek adresini gösterip göstermediğini denetler. Yetkisiz bellek erişimlerini ve çakışmaları önler.

### Değer ve Aralık Analizi (Value & Range)
Değişkenlerin alabileceği alt ve üst sınırları matematiksel olarak hesaplar. Tam sayı taşmalarını (integer overflow) ve dizi sınırlarının (buffer) dışına çıkılmasını engeller.

### İkili Kod ve Bytecode Analizi
Kaynak kodun erişilebilir olmadığı durumlarda derlenmiş dosyaları veya üçüncü parti paketleri tersine mühendislik yöntemleriyle tarayarak “kapalı kutu” güvenliğini sağlar.

---

Ancak SAST uygulamanın çalışma anında neler olduğunu bilmez. Buda yanlış pozitif üretebilmesine yol açar. Bu yüzden de çalışma ortamındayken de oluşabilecek zafiyetlerin tespiti için DAST araçları tercih edilir.

---

##  DAST NEDİR?

DAST mantıken pentest testine benzer şekilde zafiyetleri tespit eder. SAST araçlarından farklı olarak burada HTTP istekleri ile uygulamanın çalışma anında verdiği yanıtlara göre analizler yapılır. DAST araçlarının en avantajlı yanı uygulama çalışırken gelen yanıtlara göre değerlendirmelerin yapılıyor oluşudur.

Tabii şunu unutmamak lazım, DAST ve SAST bir bütündür. Biri burda “açık olabilir.” derken biri kontrol eder ve “evet burda açık var. İçeri sızabiliyorum” diyerek durumu kanıtlar. Yani SAST ile uygulama henüz kullanıma sunulmadan olası açıklara bakılıp DAST ile birliktede kullanımdaki tepkilerine bakarak gözden kaçan ya da yanlış tespit edilen zafiyetlere bakılır.

---

##  DAST’ın 3 Temel Özelliği

### Kara Kutu (Black-Box) Yaklaşımı
DAST aracı kodun içine bakmaz, hangi dille yazdığınızla veya hangi algoritmaları kurduğunuzla ilgilenmez. Sadece dışarıdan HTTP istekleri gönderir ve uygulamanın verdiği yanıtları dinler.

### “Canlı” Performans (Runtime) Analizi
Bazı hatalar sadece kodda değil, uygulama bir sunucuya kurulduğunda ortaya çıkar. DAST burada uygulama kullanılma hata yapıp yapmadığını kontrol eder.

### Dışarıdan İçeriye Sızma
Bir saldırganın ilk göreceği açıklar (zayıf şifreleme yöntemleri, oturum yönetimi hataları veya yanlış yönlendirmeler) DAST’ın radarına takılır. Yani DAST, savunma hattınızın dışarıdan ne kadar aşılabilir olduğunu size gösterir.

---



---
Endpoint-labs intern project

