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



