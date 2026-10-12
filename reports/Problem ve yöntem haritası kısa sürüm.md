# Problem ve yöntem haritası (kısa sürüm)

Bir tezin iki ayağı var. Birincisi **problem**: önemli olmalı ve çözüldüğünde işe yaramalı. İkincisi **yöntem**: güncel bir yaklaşımın üzerine yeni bir şey koymalı. Bu belge iki soruyu cevaplıyor:

1. Sahada hangi problemler hâlâ çözüm bekliyor?
2. Hangi yeni yöntemler bu problemlere henüz uygulanmamış?

Belge tez konusu önermiyor. Yalnızca seçim yaparken bakılacak haritayı veriyor.

---

## 1. Ana fikir

Sahada en çok ihtiyaç duyulan problemlerle en hızlı gelişen yöntemler henüz buluşmamış. Boşluklar özellikle iki durumda toplanıyor:

- **Koşullar değiştiğinde:** sahaya yeni bir drone tipi ya da yeni bir karıştırma yöntemi geldiğinde sistemin kendini uyarlaması.
- **Ortam düşmanca olduğunda:** bağlantı kesildiğinde, İHA kaybedildiğinde ya da sensör yanlış bilgi verdiğinde sistemin bunu fark edip doğru davranması.

---

## 2. Çözüm bekleyen önemli problemler

| # | Problem | Neden önemli | Eksik olan |
|---|---|---|---|
| 1 | **Radyo yaymayan küçük drone'ları tespit etmek** | Ukrayna'da hasarın büyük kısmı küçük kamikaze drone'lardan. Fiber optik kabloyla yönetilenler radyo yaymadığı için klasik dedektörler onları görmüyor. NATO 2025'te buna özel yarışma açtı. | Ses, kamera ve termal ile düşük güçlü tespit henüz zayıf. Kuş ile drone karışıyor. Fiber optik drone kaydı içeren açık veri seti yok. |
| 2 | **Aylarca pille çalışan gözetleme sensörleri** | Ukrayna'nın yaklaşık 10.000 ucuz ses sensörlü ağı bu fikrin sahada işe yaradığını gösteriyor. | Uzun süre düşük yanlış alarmla ve az enerjiyle çalışma. Üst üste binen olayları (insan, araç, drone) ayırmak. |
| 3 | **İHA üzerinde hedef görme** | Yapay zekalı görüş, saldırı başarısını belirgin şekilde artırmış. | Küçük hedefi doğru görmek ile küçük bilgisayara sığmak çelişiyor. Sahada değişen koşullara (arazi, kamuflaj) uyum yok. |
| 4 | **Uydu sinyali karıştırma ve aldatmayı fark etmek** | 2025'te Baltık'ta binlerce uçuş etkilendi. Ukrayna'da drone kayıplarının büyük kısmı karıştırmadan. | Laboratuvarda yüzde 95'in üstünde başarı var, ama yeni tür saldırıda çöküyor. Uçuşta gerçek saldırı altında kaydedilmiş açık veri yok. |
| 5 | **Uydu sinyali olmadan konum bulmak** | Karıştırma altında İHA'nın tek dayanağı kamera ve iç sensörler. | Kamerayı uydu haritasıyla eşleştiren yöntemler var, ama güçlü ve pahalı kartlarda çalışıyor. Enerji ölçümü neredeyse hiç yok. |
| 6 | **Konumun yanlış olduğunu bilmek** | Yanlış konuma güvenmek, hiç konum olmamasından daha tehlikeli. | Kameraya dayalı konumda "ne kadar eminim" bilgisi henüz olgun değil. |
| 7 | **Sürüde İHA'ların birbirine göre yerini bilmesi** | Uydu yokken çarpışmamak ve düzende kalmak için gerekli. Havelsan'ın bu konuda patent başvurusu var. | Deneylerin çoğu kapalı alanda ve pahalı kamera sistemleriyle yapılıyor. Dış ortamda açık veri yok. |
| 8 | **İHA kaybedildiğinde ve bağlantı koptuğunda görev paylaşımı** | ABD'nin Replicator programı tam bu yazılımda zorlandı. | Kayıp, bağlantı kopması ve güvenlik koşulları ayrı ayrı çalışılmış, birlikte çalışılmamış. Sonuçların çoğu yalnızca benzetimde. |
| 9 | **Düşman drone sürüsüne karşı savunma** | Sürü saldırıları artıyor. | Yöntemler büyük sayılarda ölçeklenmiyor. Deneyler yalnızca benzetimde. |
| 10 | **Birden çok İHA'nın birlikte görmesi** | Bir İHA'nın göremediğini diğeri görebilir. | Veri setlerinin neredeyse hepsi benzetimden. Bağlantı bozulması gerçekçi modellenmiyor. |
| 11 | **Operatörün sürüye doğal dille görev vermesi** | Operatörün iş yükünü azaltır. | Dil modelleri hata yapabiliyor ve yavaş. Bağlantı kaybı altında hiç denenmemiş. |

---

## 3. Güncel yöntemler ve ne kadar hazır oldukları

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
| **Çok ajanlı pekiştirmeli öğrenme** | Sürüdeki her İHA deneme yanılmayla birlikte çalışmayı öğrenir. | Laboratuvarda (çoğu benzetimde) |
| **Ne zaman haberleşeceğini öğrenme** | İHA'lar yalnızca gerektiğinde mesaj gönderir; bağlantı az kullanılır. | Laboratuvarda. 10 İHA ile gerçek uçuş yapılmış tek örnek: CATA (IEEE TAES 2026). |
| **Güvenlik kalkanı** | Öğrenen sistemin çarpışma gibi tehlikeli hareketlerini matematiksel olarak engeller. | Laboratuvarda |
| **Öğrenen konum filtresi** | Klasik konum hesabını yapay zeka ile düzeltir. | Laboratuvarda |
| **Büyük dil modeli ile planlama** | Operatörün sözlü komutunu görev planına çevirir. | Benzetimde ya da laboratuvarda |

---

## 4. Boşluklar nerede? (Problem ile yöntemin buluşmadığı yerler)

Bu taramada örneği bulunamayan, yani tez için fırsat olabilecek eşleşmeler:

1. **Sahada kendini uyarlama ve "emin değilim" diyebilme → drone tespiti ve uydu sinyali saldırısı tespiti**
   Yöntemler küçük çiplerde çalışır hale gelmiş. Ama bu iki savunma problemine uygulanmamış. İki problem de sürekli değişiyor: yeni drone tipi, yeni saldırı türü.

2. **"Emin değilim" diyebilme ve öğrenen filtre → uydusuz konum bulma**
   Konumun ne zaman yanlış olduğunu bilmek hâlâ açık bir sorun. Avantajı: kayıtlı veriyle çalışılabiliyor, yasal izin gerekmiyor.

3. **Yeni dizi modelleri ve düşük güçlü işlem → ses, sismik ve radyo sinyalleri**
   Bu yöntemler savunma sinyallerine neredeyse hiç uygulanmamış.

4. **Kayıp, bağlantı kopması ve güvenlik birlikte → sürüde görev paylaşımı**
   Saha ihtiyacı en güçlü olan alan bu. Risk: 3-5 İHA ile yapılan deney "küçük ölçekli" eleştirisi alabilir.

5. **Konum hatasını hesaba katan güvenlik → sürüde birbirine göre konum**
   Güvenlik yöntemleri komşunun yerini kesin biliyormuş gibi davranıyor. MILUV veri seti bunu ölçmek için hazır.

---

## 5. Bir boşluğu seçerken sorulacak 5 soru

1. **Önem iki yerden kanıtlanıyor mu?** Hem bir saha raporu (NATO, ABD Ordusu vb.) hem de hakemli bir derleme bu problemi önemli buluyor mu?
2. **Yöntem ne çok eski ne çok yeni mi?** "Hazır" bir yöntemi uygulamak yenilik sayılmayabilir. "Benzetimde" düzeyindeki bir yöntem tez süresinde çalışmayabilir. En uygunu "laboratuvarda" düzeyi.
3. **Ölçülebilir mi?** En az iki açık veri seti var mı, yoksa veri toplamak mümkün mü?
4. **Donanıma taşınabilir mi?** Seçilen kartta bu yöntem çalışıyor mu?
5. **Yasal mı?** Türkiye'de izinsiz uydu sinyali karıştırma yasak (BTK izni gerekir). Bu yüzden ilgili deneyler kayıtlı veriyle yapılmalı.

---

## 6. Dikkat edilecekler

- "Boşluk" burada "bu taramada örnek bulunamadı" demek. Bir boşluk seçilmeden önce o konuya özel ayrı bir tarama yapılmalı.
- Bazı rakamlar basın ya da şirket açıklamalarından geliyor. Uzun raporda bunlar ayrıca işaretli.

Ayrıntılar ve kaynaklar için uzun rapor: `reports/Edge AI ve sürü problem haritası.md`

---

## Kısaltma listesi

| Kısaltma | Açılımı | Kısa anlamı |
|---|---|---|
| **AI** | Artificial Intelligence | Yapay zeka |
| **BTK** | Bilgi Teknolojileri ve İletişim Kurumu | Türkiye'de telsiz yayın izinlerini veren kurum |
| **CATA** | Communication-Aware Task Allocation | Haberleşmeyi hesaba katan görev paylaşımı yöntemi |
| **CIR** | Channel Impulse Response | Telsiz sinyalinin alıcıya nasıl ulaştığını gösteren iz |
| **C-UAS** | Counter Unmanned Aircraft Systems | Drone'lara karşı savunma sistemleri |
| **Edge AI** | Edge Artificial Intelligence | Yapay zekanın buluta değil cihazın kendisinde çalışması |
| **FPV** | First Person View | Kameradan canlı izlenerek uçurulan küçük drone, çoğunlukla kamikaze |
| **GNSS** | Global Navigation Satellite System | Uydu konumlama sistemlerinin genel adı (GPS, Galileo vb.) |
| **GPS** | Global Positioning System | ABD'nin uydu konumlama sistemi |
| **IEEE TAES** | IEEE Transactions on Aerospace and Electronic Systems | Havacılık ve elektronik alanında Q1 dergi |
| **İHA** | İnsansız Hava Aracı | Drone |
| **LLM** | Large Language Model | Büyük dil modeli (ChatGPT, Claude gibi) |
| **MARL** | Multi-Agent Reinforcement Learning | Çok ajanlı pekiştirmeli öğrenme: birden çok ajanın deneme yanılmayla birlikte öğrenmesi |
| **MILUV** | Multi-UAV Indoor Localization with UWB and Vision | 3 İHA'lı, UWB ve kamera içeren açık veri seti |
| **NATO** | North Atlantic Treaty Organization | Kuzey Atlantik Antlaşması Örgütü |
| **Q1** | Birinci çeyrek | Alanındaki dergilerin en çok atıf alan dörtte biri |
| **RF** | Radio Frequency | Radyo frekansı, telsiz sinyali |
| **TinyML** | Tiny Machine Learning | Çok küçük ve düşük güçlü çiplerde çalışan makine öğrenmesi |
| **UWB** | Ultra-Wideband | Cihazlar arası mesafeyi santimetre düzeyinde ölçen telsiz teknolojisi |
| **WoS** | Web of Science | Bilimsel dergileri dizinleyen veri tabanı |
