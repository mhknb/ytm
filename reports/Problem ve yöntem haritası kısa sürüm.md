# Problem ve yöntem haritası (kısa sürüm)

Bir tezin iki ayağı var. Birincisi **problem**: önemli olmalı ve çözüldüğünde işe yaramalı. İkincisi **yöntem**: güncel bir yaklaşımın üzerine yeni bir şey koymalı.

Bu sürümde bir şart daha var: **problem üzerinde çalışabilmek için en az 2 açık veri seti olmalı.** Bu şartı sağlamayan problemler listeden çıkarıldı.

Belge tez konusu önermiyor. Yalnızca seçim yaparken bakılacak haritayı veriyor.

---

## 1. Ana fikir

Sahada en çok ihtiyaç duyulan problemlerle en hızlı gelişen yöntemler henüz buluşmamış. Boşluklar özellikle iki durumda toplanıyor:

- **Koşullar değiştiğinde:** sahaya yeni bir drone tipi ya da yeni bir karıştırma yöntemi geldiğinde sistemin kendini uyarlaması.
- **Ortam düşmanca olduğunda:** bağlantı kesildiğinde ya da sensör yanlış bilgi verdiğinde sistemin bunu fark edip doğru davranması.

---

## 2. Veri şartını geçen 7 problem

Her problem için en az 2 açık veri seti var. "Doğrulandı" işareti, veri setinin yayın ya da indirme sayfasını bu çalışma sırasında açıp kontrol ettiğimiz anlamına geliyor.

### Problem 1. Radyo yaymayan küçük drone'ları tespit etmek

- **Neden önemli:** Ukrayna'da hasarın büyük kısmı küçük kamikaze drone'lardan geliyor. Fiber optik kabloyla yönetilenler radyo yaymıyor. Bu yüzden klasik dedektörler onları göremiyor. NATO 2025'te buna özel yarışma açtı.
- **Eksik olan:** Ses, kamera ve termal ile düşük güçlü tespit henüz zayıf. Kuş ile drone sık karışıyor.
- **Açık veri setleri:**
  - **Anti-UAV410:** 410 termal video, 438 bin etiketli kutu (doğrulandı).
  - **FRED:** 7 saatten fazla olay kamerası ve normal kamera kaydı, 5 drone tipi (doğrulandı).
  - **DADS:** yaklaşık 60 saatlik drone sesi (doğrulandı).
  - **MMAUD:** aynı anda kaydedilmiş ses, kamera, lidar ve radar (doğrulandı).
- **Not:** Fiber optik drone kaydı içeren açık veri yok. Çalışma "radyo dışı sensörlerle tespit" olarak kurulabilir.

### Problem 2. Aylarca pille çalışan gözetleme sensörleri

- **Neden önemli:** Ukrayna'nın yaklaşık 10.000 ucuz ses sensörlü ağı bu fikrin sahada işe yaradığını gösteriyor.
- **Eksik olan:** Uzun süre az enerjiyle ve az yanlış alarmla çalışmak. Üst üste binen olayları (insan, araç, drone) ayırmak.
- **Açık veri setleri:**
  - **ASD:** hareketli hedefler için ses ve sismik kayıt. IEEE DataPort'ta; ücretsiz üyelik gerekebilir.
  - **M3N-VC:** çok düğümlü mikrofon ve sismik sensör ile araç sınıflandırma (GitHub).
  - **ACIDS:** ABD Ordusu'nun eski ses-sismik verisi, 9 araç tipi, 270'ten fazla geçiş; erişimi kontrol edilmeli.
- **Not:** Kayıtlar kısa. Aylar süren gerçek saha kaydı yok.

### Problem 3. İHA üzerinde hedef görme (gece ve termal dahil)

- **Neden önemli:** Yapay zekalı görüş, İHA'nın hedefi tanıma mesafesini ve vuruş başarısını belirgin şekilde artırmış.
- **Eksik olan:** Küçük hedefi doğru görmek ile küçük bilgisayara sığmak çelişiyor. Sahada değişen koşullara (arazi, kamuflaj) uyum yok.
- **Açık veri setleri:**
  - **HIT-UAV:** 2.898 termal görüntü, insan ve araç (doğrulandı).
  - **DroneVehicle:** 28.439 normal ve kızılötesi görüntü çifti, gece ve gündüz (doğrulandı).
- **Not:** Askeri hedef ve kamuflaj içeren açık veri yok.

### Problem 4. Uydu sinyali karıştırma ve aldatmayı fark etmek

- **Neden önemli:** 2025'te Baltık'ta binlerce uçuş etkilendi. Ukrayna'da drone kayıplarının büyük kısmı karıştırmadan.
- **Eksik olan:** Laboratuvarda yüzde 95'in üstünde başarı var, ama yeni tür saldırıda çöküyor.
- **Açık veri setleri:**
  - **TEXBAT:** Texas Üniversitesi'nin aldatma test kayıtları.
  - **OAKBAT:** TEXBAT'ı tamamlayan aldatma kayıtları.
  - **GNSS girişim ve aldatma veri seti:** Data in Brief 2024.
  - **Jammertest 2025:** Norveç'teki resmi karıştırma testinden kayıtlar (Zenodo).
- **Not:** Kayıtlar çoğunlukla yerde alınmış. Uçuşta gerçek saldırı altında kamera ve iç sensör verisi içeren açık set yok.
- **Yasal not:** Türkiye'de izinsiz karıştırma yayını yasak. Bu yüzden bu veri setleri, yasal kalarak çalışmanın tek yolu.

### Problem 5. Uydu sinyali olmadan konum bulmak ve bu konuma ne kadar güvenileceğini bilmek

- **Neden önemli:** Karıştırma altında İHA'nın tek dayanağı kamera ve iç sensörler. Yanlış konuma güvenmek, hiç konum olmamasından daha tehlikeli.
- **Eksik olan:** Yöntemler güçlü ve pahalı kartlarda çalışıyor. Enerji ölçümü neredeyse yok. "Ne kadar eminim" bilgisi olgun değil.
- **Açık veri setleri:**
  - **UAV-VisLoc:** 6.742 İHA görüntüsü, 11 uydu haritası, 400-2.000 m irtifa (doğrulandı).
  - **SatLoc:** Remote Sensing 2025 (doğrulandı).
  - **AerialVL:** 11 uçuş, yaklaşık 70 km rota, uydu haritası ile eşleştirme (IEEE RA-L 2024).
  - **University-1652:** alçak irtifa, bina odaklı eşleştirme verisi.
- **Not:** İlk listedeki "konumun yanlış olduğunu bilmek" problemi için ayrı bir veri seti yok. Aynı veri setlerine yapay hata eklenerek çalışılabildiği için buraya katıldı.

### Problem 6. Sürüde İHA'ların birbirine göre yerini bilmesi

- **Neden önemli:** Uydu yokken çarpışmamak ve düzende kalmak için gerekli. Havelsan'ın bu konuda patent başvurusu var.
- **Eksik olan:** Deneylerin çoğu kapalı alanda ve pahalı kamera sistemleriyle yapılıyor.
- **Açık veri setleri:**
  - **MILUV:** 3 İHA, aralarında UWB ölçümleri ve ham sinyal izi, 217 dakika (doğrulandı).
  - **AAU Multi-Agent UVDAR:** 3 İHA arasında göreli konum ölçümleri (Zenodo, doğrulandı).
  - Tek İHA'lı yardımcı setler: **Q-Drone UWB** (dış ortam, doğrulandı) ve **NTU VIRAL**.
- **Not:** Dış ortamda çok İHA'lı açık veri yok.

### Problem 7. Birden çok İHA'nın birlikte görmesi

- **Neden önemli:** Bir İHA'nın engel yüzünden göremediğini diğeri görebilir.
- **Eksik olan:** Bağlantı bozulması gerçekçi modellenmiyor. Gerçek uçuşta deneme çok az.
- **Açık veri setleri:**
  - **U2UData:** 3 İHA (doğrulandı).
  - **U2UData+:** 15 İHA, 120 saat (doğrulandı).
  - **CoPerception-UAVs:** 5 İHA.
- **Not:** Üç veri seti de **benzetimden** üretilmiş. Veri şartını geçiyor, ama gerçek dünyaya geçişte risk var.

---

## 3. Veri şartını geçemeyen problemler

Bu üç problem önemli. Ama üzerinde çalışılacak açık veri seti yok; yalnızca benzetim ortamları var.

| Problem | Durum |
|---|---|
| İHA kaybedildiğinde ve bağlantı koptuğunda görev paylaşımı | Yalnızca benzetim programları var, kayıtlı veri seti yok. |
| Düşman drone sürüsüne karşı savunma | Yalnızca benzetim. Drone sürüsü görüntü setleri var, ama savunma kararlarına ait veri yok. |
| Operatörün sürüye doğal dille görev vermesi | Tek bir görev kümesi var, standart veri seti yok. |

---

## 4. Güncel yöntemler ve ne kadar hazır oldukları

Olgunluk üç düzeyde verildi:

- **Hazır:** sahada ya da üretici araçlarında kullanılıyor.
- **Laboratuvarda:** gerçek donanımda gösterilmiş ama yaygın değil.
- **Benzetimde:** çoğunlukla bilgisayar benzetiminde ya da hakemsiz yayında.

| Yöntem | Ne yapar (basitçe) | Olgunluk |
|---|---|---|
| **Modeli küçültme** | Büyük yapay zeka modelini küçük çipe sığdırır. | Hazır |
| **Sahada kendini uyarlama** | Model, sahada yeni koşulla karşılaşınca kendini günceller; yeniden eğitime gerek kalmaz. | Laboratuvarda |
| **"Emin değilim" diyebilme** | Model tahminiyle birlikte güven düzeyini de verir; tanımadığı şeyi "bilmiyorum" diye işaretler. | Laboratuvarda |
| **Beyinden esinlenen düşük güçlü işlem** | Çok az enerjiyle, yalnızca değişim olduğunda çalışan kamera ve çipler. | Laboratuvarda |
| **Büyük modelden küçük modele bilgi aktarma** | Güçlü bir modelin bilgisini küçük modele öğretir. | Güçlü kartlarda hazır, küçük çiplerde benzetimde |
| **Yeni nesil dizi modelleri (Mamba)** | Ses ve sinyal gibi zaman içinde akan veriyi az hesapla işler. | Benzetimde |
| **Ne zaman haberleşeceğini öğrenme** | İHA'lar yalnızca gerektiğinde mesaj gönderir; bağlantı az kullanılır. | Laboratuvarda |
| **Güvenlik kalkanı** | Öğrenen sistemin çarpışma gibi tehlikeli hareketlerini matematiksel olarak engeller. | Laboratuvarda |
| **Öğrenen konum filtresi** | Klasik konum hesabını yapay zeka ile düzeltir. | Laboratuvarda |

---

## 5. Boşluklar nerede? (Veri şartını geçen problemlerde)

Bu taramada örneği bulunamayan, yani tez için fırsat olabilecek eşleşmeler:

1. **Sahada kendini uyarlama ve "emin değilim" diyebilme → Problem 1 ve Problem 4**
   Yöntemler küçük çiplerde çalışır hale gelmiş. Ama drone tespitine ve uydu sinyali saldırısı tespitine uygulanmamış. İki problem de sürekli değişiyor: yeni drone tipi, yeni saldırı türü.

2. **"Emin değilim" diyebilme ve öğrenen filtre → Problem 5**
   Uydusuz konumun ne zaman yanlış olduğunu bilmek hâlâ açık bir sorun. Kayıtlı veriyle çalışılabiliyor, yasal izin gerekmiyor.

3. **Yeni dizi modelleri ve düşük güçlü işlem → Problem 1 (ses), Problem 2 (sismik), Problem 4 (uydu sinyali)**
   Bu yöntemler savunma sinyallerine neredeyse hiç uygulanmamış.

4. **Öğrenen filtre ve konum hatasını hesaba katan güvenlik → Problem 6**
   Güvenlik yöntemleri komşunun yerini kesin biliyormuş gibi davranıyor. MILUV bunu ölçmek için hazır.

5. **Sahada kendini uyarlama ve ne zaman haberleşeceğini öğrenme → Problem 7**
   Benzetimden gerçeğe geçiş ve bağlantı bozulması birlikte ele alınmamış.

---

## 6. Bir boşluğu seçerken sorulacak 5 soru

1. **Önem iki yerden kanıtlanıyor mu?** Hem bir saha raporu (NATO, ABD Ordusu vb.) hem de hakemli bir derleme bu problemi önemli buluyor mu?
2. **Yöntem ne çok eski ne çok yeni mi?** "Hazır" bir yöntemi uygulamak yenilik sayılmayabilir. "Benzetimde" düzeyindeki bir yöntem tez süresinde çalışmayabilir. En uygunu "laboratuvarda" düzeyi.
3. **Veri gerçekten problemi karşılıyor mu?** Veri seti var diye yetmez. Problemin zor kısmını (gece, yeni drone tipi, saldırı) içeriyor mu?
4. **Donanıma taşınabilir mi?** Seçilen kartta bu yöntem çalışıyor mu?
5. **Yasal mı?** Türkiye'de izinsiz uydu sinyali karıştırma yasak (BTK izni gerekir). Bu yüzden ilgili deneyler kayıtlı veriyle yapılmalı.

---

## 7. Dikkat edilecekler

- "Boşluk" burada "bu taramada örnek bulunamadı" demek. Bir boşluk seçilmeden önce o konuya özel ayrı bir tarama yapılmalı.
- "Doğrulandı" işareti olmayan veri setleri başka doğrulanmış yayınlarda geçiyor. Seçimden önce indirme sayfası ayrıca açılıp kontrol edilmeli.
- Bazı rakamlar basın ya da şirket açıklamalarından geliyor. Uzun raporda bunlar ayrıca işaretli.

Ayrıntılar ve kaynaklar için uzun rapor: `reports/Edge AI ve sürü problem haritası.md`

---

## Kısaltma listesi

| Kısaltma | Açılımı | Kısa anlamı |
|---|---|---|
| **AAU** | Alpen-Adria-Universität Klagenfurt | Avusturya'da bir üniversite (veri setini yayımlayan) |
| **AI** | Artificial Intelligence | Yapay zeka |
| **ASD** | Acoustic and Seismic Dataset | Ses ve sismik veri seti |
| **BTK** | Bilgi Teknolojileri ve İletişim Kurumu | Türkiye'de telsiz yayın izinlerini veren kurum |
| **DADS** | Drone Audio Detection Samples | Drone sesi veri seti |
| **Edge AI** | Edge Artificial Intelligence | Yapay zekanın buluta değil cihazın kendisinde çalışması |
| **FPV** | First Person View | Kameradan canlı izlenerek uçurulan küçük drone, çoğunlukla kamikaze |
| **FRED** | Florence RGB-Event Drone dataset | Olay kamerası ve normal kamera ile drone veri seti |
| **GNSS** | Global Navigation Satellite System | Uydu konumlama sistemlerinin genel adı (GPS, Galileo vb.) |
| **GPS** | Global Positioning System | ABD'nin uydu konumlama sistemi |
| **İHA** | İnsansız Hava Aracı | Drone |
| **MILUV** | Multi-UAV Indoor Localization with UWB and Vision | 3 İHA'lı, UWB ve kamera içeren açık veri seti |
| **MMAUD** | Multi-Modal Anti-UAV Dataset | Çok sensörlü drone tespit veri seti |
| **NATO** | North Atlantic Treaty Organization | Kuzey Atlantik Antlaşması Örgütü |
| **NTU VIRAL** | Nanyang Technological University Visual-Inertial-Ranging-Lidar dataset | Tek İHA'lı kamera, UWB ve lidar veri seti |
| **OAKBAT** | Oak Ridge Spoofing and Interference Test Battery | Uydu sinyali aldatma ve girişim test kayıtları |
| **Q1** | Birinci çeyrek | Alanındaki dergilerin en çok atıf alan dörtte biri |
| **RF** | Radio Frequency | Radyo frekansı, telsiz sinyali |
| **TEXBAT** | Texas Spoofing Test Battery | Uydu sinyali aldatma test kayıtları |
| **TinyML** | Tiny Machine Learning | Çok küçük ve düşük güçlü çiplerde çalışan makine öğrenmesi |
| **U2UData** | UAV-to-UAV Data | Çok İHA'lı birlikte görme veri seti (benzetim) |
| **UAV** | Unmanned Aerial Vehicle | İHA'nın İngilizcesi |
| **UVDAR** | UltraViolet Direction And Ranging | İHA'ların morötesi ışıklarla birbirinin yerini ölçtüğü sistem |
| **UWB** | Ultra-Wideband | Cihazlar arası mesafeyi santimetre düzeyinde ölçen telsiz teknolojisi |
