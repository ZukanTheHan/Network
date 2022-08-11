# WLAN

## Kablosuz Ağ Teknolojileri

Wireless Personel-Area Network(WPAN) - Düşük güç tüketir ve kısa mesafelidir. IEEE 802.15 standartıdır. 2.4GHz frekansta yayın yapar. Bluetooth ve Zigbee WPAN için örnek verilebilir. 

Wireless LAN(WLAN) - Orta mesafelidir. IEEE 802.11 standartıdır ve 2.4 veya 5.0 GHz frekansındadır. 

Wireless MAN(WMAN) - Büyük coğrafi alanlarda, şehir gibi, kullanılabilen bir teknolojidir. Spesifik lisanslı frekansları kullanır.

Wireless WAN(WWAN) - GSM veya uydu haberleşmesi için kullanılabilen bir teknolojidir. Spesifik lisanslı frekansları kullanır.


## 802.11 Standartı

|  IEEE Standartı | Frekans        | Açıklama |
| ----------------|:-------:| :-----:|
|     802.11      | 2.4 GHz | 2 Mb/s hız   |
| 802.11a | 5 GHz   | 54 Mb/s hız. 802.11b veya 802.11g ile çalışmaz |
| 802.11b | 2.4 GHz     | 11 Mb/s hız. 802.11a'dan dah uzun bir menzili vardır. |
| 802.11g | 2.4 GHz     | 54 Mb/s hız. 802.11b ile uyumludur. |
| 802.11n | 2.4 ve 5 GHz  | 150 - 600 Mb/s hız. MIMO tekonolojisine sahip birden fazla anten gerekir. |
| 802.11ac | 5 GHz     | 450 Mb/s - 1.3 Gb/s hız. Sekiz antene kadar destekler. |
| 802.11ax | 2.4 ve 5 GHz     | High-Efficiency Wireless (HEW). 1 GHz ve 7 GHz frekanslarını kullanabilir. |


## WLAN Komponentleri

**Wireless NICs**, kablosuz iletişim kurmak için dizüstü bilgisayarlar, tabletler, akıllı telefonlar ve hatta en yeni otomobiller, bir radyo vericisi/alıcısı içeren entegre kablosuz NIC'leri içerir.

**Wireless Home Router**, evlerimizde kullandığımız cihazlardır. Kablosuz yönlendirici şu işlevi görür:

Access Point - Bu, 802.11a/b/g/n/ac kablosuz erişim sağlar.
Switch - Bu, kablolu cihazları birbirine bağlamak için dört bağlantı noktalı, tam çift yönlü, 10/100/1000 Ethernet anahtarı sağlar.
Router - Bu, internet gibi diğer ağ altyapılarına bağlanmak için varsayılan bir ağ geçidi sağlar.

**Acces Point** - Kablosuz istemciler, SSID'lerinin reklamını yapan yakındaki AP'leri keşfetmek için kablosuz NIC'lerini kullanır. Kimliği doğrulandıktan sonra, kablosuz kullanıcılar ağ kaynaklarına erişebilir.

Autonomous AP, tüm işlemleri kendi başına yönetir. Cihazlara wireless yayın verme, kriptografik işlem yapma vs. gibi işlemleri yapar. Otonom AP'ler, kuruluşta yalnızca birkaç AP'nin gerekli olduğu durumlarda kullanışlıdır.Her AP, diğer AP'lerden bağımsız olarak çalışır ve her AP, manuel yapılandırma ve yönetim gerektirir.

Controller Based AP, bu cihazlar yapılandırma gerektirmez ve genellikle lightweight AP (LAP) olarak adlandırılır. LAP, bir WLAN denetleyicisi (WLC) ile iletişim kurmak için Lightweight Access Point Protocol (LWAPP) kullanır. Denetleyici tabanlı AP'ler, ağda çok sayıda AP'nin gerekli olduğu durumlarda kullanışlıdır. Daha fazla AP eklendikçe, her AP WLC tarafından otomatik olarak yapılandırılır ve yönetilir.

3 farklı harici anten türü vardır:

Omnidirectional, çok yönlü antenler 360 derecelik kapsama alanı sağlar ve evler, açık ofis alanları, konferans salonları ve dış alanlar için idealdir. Bu antenlerin tam ucu aslında kör noktadır. Buraya yayın vermez. 

Directional, yönlü antenler, radyo sinyalini belirli bir yöne odaklar. Antenin işaret ettiği yönde AP'ye giden ve gelen sinyal artar. Belirli bir açıyla iletim sağlanır. Açı düşürüldükçe menzil artar. Yönlü Wi-Fi antenlerinin örnekleri arasında Yagi ve parabolik çanak antenler bulunur.

MIMO, IEEE 802.11n/ac/ax kablosuz ağlar için mevcut bant genişliğini artırmak için çoklu antenler kullanır. Verimi artırmak için sekiz adede kadar verici ve alıcı anten kullanılabilir. Bu sayede aynı frekans üzerinden birden fazla paket gönderimi olur. 


## 802.11 Wireless Topoloji 

**Ad hoc mode** - Cihazları uçtan uca AP olmadan bağlamak. 

**Infastructure mode** - Son sihazları AP kullanarakağa bağlamak.

**Tethering** - Akıllı bir telefon veya tabletin hücresel bağlantısını hotspot olarak kullanarak cihazları ağa çıkarma. 

Infastructure mode, iki topoloji tipni tanımlar: Basic Service Set(BSS) ve Extended Service Set(ESS).

Basic Service Set(BSS), ilişkili tüm kablosuz istemcileri birbirine bağlayan tek bir AP'den oluşur. AP'nin MAC adresi, Basic Service Set Identifier(BSSID) olarak adlandırılan her BSS'yi benzersiz şekilde tanımlamak için kullanılır.

Extendent Service Set, tek bir BSS yetersiz kapsama sağladığında, iki veya daha fazla BSS, ortak bir dağıtım sistemi (DS) aracılığıyla bir ESS'ye dönüştürülebilir. Bir ESS, kablolu bir DS ile birbirine bağlanan iki veya daha fazla BSS'nin birleşimidir. Her ESS bir SSID ile tanımlanır ve her BSS kendi BSSID'si ile tanımlanır.

## 802.11 Frame Yapısı

![image](https://user-images.githubusercontent.com/70758694/184153155-4f1a915c-83d6-48f0-ae94-9841fc526de0.png)
Tüm 802.11 kablosuz frame yapısı aşağıdaki alanları içerir:
- Frame Control - Bu, kablosuz frame türünü tanımlar ve protokol sürümü, frame türü, adres türü, güç yönetimi ve güvenlik ayarları için alt alanlar içerir.
- Duration - Bu genellikle bir sonraki frame iletimini almak için gereken kalan süreyi belirtmek için kullanılır.

Kablosuz bir cihazdan gönderilen frame:
- Adres 1 - AP'nin MAC adresi.
- Adres 2 - Gönderenin MAC adresi.
- Adres 3 - Hedefin MAC adresi.

AP cihazından gönderilen frame:
- Adres 1 - Gönderenin MAC adresi.
- Adres 2  - AP'nin MAC adresi.
- Adres 3  - Hedefin MAC adresi.
- Sequence Control - Bu, sıralamayı ve parçalanmış çerçeveleri kontrol etmek için bilgi içerir.
- Adres 4 - Bu, yalnızca ad hoc modda kullanıldığından genellikle eksiktir.
- Payload - Bu, iletilecek verileri içerir.
- FCS - Bu, Katman 2 hata kontrolü için kullanılır.

## Kanal Yönetimi

Direct-Sequence Spread Spectrum (DSSS), bir sinyali daha geniş bir frekans bandına yaymak için tasarlanmış bir modülasyon tekniğidir. DSSS, aynı 2,4 GHz frekansını kullanan diğer cihazlardan kaynaklanan paraziti önlemek için 802.11b cihazları tarafından kullanılır.

Frequency-Hopping Spread Spectrum (FHSS), iletişim kurmak için yayılmış spektrum yöntemlerine dayanır. Birçok frekans kanalı arasında bir taşıyıcı sinyali hızla değiştirerek radyo sinyallerini iletir. Gönderici ve alıcı, kanal atlama sırası senkronize edilmelidir.Bu kanal atlama işlemi, kanalların daha verimli kullanılmasını sağlayarak kanal tıkanıklığını azaltır. Telsizler ve 900 MHz kablosuz telefonlar da FHSS kullanır ve Bluetooth, FHSS'nin bir varyasyonunu kullanır.

Orthogonal Frequency-Division Multiplexing (OFDM), tek bir kanalın bitişik frekanslarda birden çok alt kanal kullandığı frekans bölmeli çoğullamannın kullanıldığı modülasyondur. OFDM, 802.11a/g/n/ac dahil olmak üzere bir dizi iletişim sistemi tarafından kullanılır. Yeni 802.11ax, Ortogonal frekans bölmeli çoklu erişim (OFDMA) adı verilen bir OFDM varyasyonu kullanır.

### Kanal Seçimi

Birden çok AP gerektiren WLAN'lar için en iyi uygulama, örtüşmeyen kanalları kullanmaktır. Örneğin, 802.11b/g/n standartları 2,4 GHz ila 2,5 GHz spektrumunda çalışır. 2.4 GHz bandı birden çok kanala bölünmüştür. Her kanala 22 MHz bant genişliği tahsis edilmiştir ve bir sonraki kanaldan 5 MHz ile ayrılmıştır.

![image](https://user-images.githubusercontent.com/70758694/184164326-8d9c9da1-09ff-4567-abb8-9674ee6f3ae0.png)

Yukarıdaki şekilde görüldüğü gibi aynı alanda birbirleriyle çakışmayacak aslında en fazla 3 kanal var. Aralarında en az 5 kanal olan iki kanal birbirleriyle çakışmaz ve birbirlerinin verisini bozmaz. Hızı arttırmak istersek çakışmayan iki kanlı birleştirebiliriz ama bu şekilde 2 kanalıda işgal ettiğimizi ve geriye 1 kanal kaldığını unutmayalım. 

5 GHz ile birlikte kanal sayısı artmış ve bu şekilde örtüşemeyen kanallar birleştirerek daha yüksek hızlara çıkabiliriz. Ama kapsama alanı daha dardır. 

## CSMA/CA 

Frekansımız dar olduğu için her cihaza ayrı kanallar atayamıyoruz bu yüzden tüm cihazlar half-dublex bir şekilde kablosuz bağlantı sağlarlar. Çakışmaları engellemek için CSMA/CA algoritmasından yararlanılır. Paket gönderecek cihaz öncelikle ağı dinler ve AP cihazına RTS paketi gönderir. Bu paket veri içerimez, sadece AP cihazına veri göndermeye hazır olduğunu belirtir.  












