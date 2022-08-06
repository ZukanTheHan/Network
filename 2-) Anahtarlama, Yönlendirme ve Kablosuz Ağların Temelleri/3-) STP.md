# STP (IEEE 802.1D)

Ağlarda yanlış kablolama ve planlama sonucunda döngüler (loop) meydana gelebilir. Özellikle Layer 2 cihazlarında broadcast, konfigürasyonu yapılmamış multicast ve bilinmeyen unicat paketleri yüzünden ağda sürekli olarak akarak haberleşmeyi bitiren sitenmeyen bi olaydır. STP protokolü de ağda oluşabilecek döngüyü (loop) engellemek için geliştirilmiştir. 

![image](https://user-images.githubusercontent.com/70758694/183071088-f65a3bbf-c1f6-4ab0-908f-e423805e46be.png)

Yukarıdaki basit modelde herhangi bir uç cihazdan gönderilecek broadcast geldiği port hariç tüm portlardan gönderileceği için sonsuz bir döngü oluşturur. 

![image](https://user-images.githubusercontent.com/70758694/183072018-35468699-fabb-43cf-bae8-dba820b79725.png)

Bu şekilde oluşan bir döngü, ağı birkaç saniyede kullanılamaz hale getirir. Switch cihazlarına ulaşım engellenir. MAC veritabanı sürekli değişerek stabil olmaz. Cihazlarda CPU artışına neden olur. 

![image](https://user-images.githubusercontent.com/70758694/183081738-6a0bd10f-1620-4ebd-8f3e-892f0a8516e8.png)

STP protokolü döngüye sebep olacak portu bloklar ve döngü olmasını engeller. Yukarıda üç switch arasındaki bağlantı durumları verilmiştir. Soldaki modelde swtich cihazları arasında henüz bir bağlantı yok. STP prtokolü bir döngü olup olmadığını anlamaya çalışıyor. En sonda da bir portun bloklandığını görüyoruz. Bu işlem toplam 30 saniye sürüyor. Döngü olup olmadığını ise switch cihazları birbirine gönderdiği BPDU paketleriyle anlar. İki saniyede bir BPDU paketleri gönderilir ve buna hello süresi de denir. Switch daha sonra Listening moda geçer. Bu süre boyunca switch cihazları sadece birbirine BPDU paketi gönderir ve alır. Bu süre zarfında switch cihazları herhangi bir veriyi iletmezler veya MAC adresi kaydetmezler. Buna forward delay denir ve 15 saniye sürer. Daha sonra Learning moduna geçer ve burada MAC adreslerini öğrenmye başlar ama paket iletimi gerçekleşmez. Bu durum da 15 saniye sürer. En son olarak Forwarding durumuna geçilir ve paketleri iletmeye de başlar. 

Listenin durumunda döngüye neden olabilecek bir port varsa blocking durumuna geçilir. Block durumunda port sadece BPDU paketlerini alır. Diğer kablolarda bir sorun çıktığında tekrar aktif duruma geçer. Bloklanacak portun belirlenmesi için önce root switch seçilir. Bu BPDU paketleriyle gerçekleşir. BPDU paketi içerisinde her switch kendi tayin ettiği root switch bilgisini de yollar. İlk başta herkes kendini root switch ilan eder. Ama root switch yine BPDU paketi içerisinde yer alan bridge id numarasıyla belirlenir. Bridge ID, bridge priority ve MAC adresinden oluşur. Bridge priority değeri konfigüre edilebilir. Bridge ID değeri küçük olan root switch olarak seçilir. Root switch belirlendikten sonra portlara değerler atılır; designated port, root switch cihazından çıkan ve root cihazından dışarıya doğru paketleri ileten porttur, root portsa root cihazına doğru giden porttur. 

![image](https://user-images.githubusercontent.com/70758694/183092483-0f7b7c4c-ab56-42fa-8b44-c6d394dea670.png)

Port durumları da BPDU paketi içerisinde gönderilir. Eğer yukarıda görüldüğü iki designated port karşı karşıya gelirse biri portunu bloke eder. Bunu da öncelikle path cost denilen değere bakarak yaparlar. Path cost, portun sahip olduğu hızdır.

- 10 Gbps => 2
- 1 Gbps => 4
- 100 Mbps => 19
- 10 Mbps => 100

Path cost değeri büyük olan portunu bloke eder. Bunlar da eşitse o zaman bridge id değerlerine bakılır ve büyük olan yine portunu bloklar. Bridge ID değerleri eğer eşit olursa bunun olması için switch cihazının iki portu birbirine bağlı olaması gerekir. Çünkü, bridge id değerinin MAC adresi içerdiğini söyledik, iki farklı cihazın MAC adresinin normal koşullar altında aynı olması beklenmez. Böyle bir durumda port id değerlerine bakılır. Port id ise port priority değeri ve port numarısından oluşur. Port numaraları farklı olacağı için port numarası büyük olan portunu bloklar.

![image](https://user-images.githubusercontent.com/70758694/183099658-d939de69-ce60-44d5-8eb0-70c877e5a106.png) Yukarıdaki gibi bir durumda öncelikle root switch belirlenir. Sonra, port durumları birbirlerine iletilir. Alttaki switch cihazı iki portununda root port olduğunu bilir ve birini bloklaması gerekir. Path cost ve bridge id birbirine eşit olduğu için port id değerine bakılır. Root cihazdan gelen BPDU paketinin içerisinde yer alan port id numarasına göre alttaki switch portlardan birini bloklar. Örnekte görüldüğü gibi root cihazdan gelen BPDU paketindeki port id değeri daha küçük olduğu için birinci port engellenmiştir. 

![image](https://user-images.githubusercontent.com/70758694/183101594-3c2f403e-2f6e-43f8-8e80-1567cedf49dc.png) ![image](https://user-images.githubusercontent.com/70758694/183101614-0cf19ff2-3e79-4d1b-b05a-dfabc442c517.png)

Eğer kablolardan biri koparsa yukarıdaki görseldeki gibi switch cihazı 15 saniye Listening, 15 saniye Learning toplam 30 saniye sonra bloklanmış portunu açar. 

![image](https://user-images.githubusercontent.com/70758694/183210877-e1907829-8fec-411a-ab7c-525e20cb6f54.png)

Burada farklı bir durum söz konusu. Bloklanmış portun BPDU paketlerini almaya devam ettiğinden bahsetmiştik. BPDU paketi içerisinde root switch bilgisinin yer aldığını da söylemiştik. Buna göre switch 1 cihazı kendini root ilan edecek ve BPDU paketi içerisinde bu bilgiyi gönderecektir. 15 saniye Listening, 15 saniye Learning toplam 30 saniye sonra bloklanmış port açılır. 

![image](https://user-images.githubusercontent.com/70758694/183214135-aa46511a-c4be-4fc4-b99d-3c5d14a22190.png)

Yukarıdaki örnekte arada yönetilemez switch cihazının olduğu ağda turuncu daire ile gösterilmiş port STP sonucunda bloklanmıştır. Daha sonra yönetilemez switch cihazının diğer kablolamasında sorun ortaya çıkmış ve haberleşme durmuştur. Bu durumda bloklanmış port BPDU paketlerini beklediği moda geçer ve 20 saniye bekler. Buna max age denir. 20 saniye sonra yine listening ve learning durumlarında toplam 30 saniye bekledikten sonra bloklanmış port hizmete açılır. 


STP, oldukça yavaş bir protokol. En küçük sorunda en az 30 saniye hizmet alamıyoruz. Yedeklilik için takılan kablolar yük paylaşımı da gerçekleştirmiyor. Bu yüzden hem Cisco hem de IEEE pek çok varyasyon geliştirmiştir.

## STP Versiyonları

PVSTP+(Per-VLAN Spanning Tree Protocol), Cisco tarafından geliştirilmiştir. Yük paylaşımı özelliği getirmiştir. STP, sadece tek bir ağaç oluşturur. PVSTP+ ise her VLAN için ağaç oluşturur ve bu sayede bir VLAN tarafından kullanılmayan port diğer VLAN tarafından kullanılır ve bu sayede yük paylaşımı gerçekleştirilmiş olur. Ayrıca, PVSTP+ ile PortFast, UplinkFast, BackboneFast, BPDU guard, BPDU filter, root guard ve loop guard desteğiyle hız ve güvenlikte sağlanmıştır. 

RSTP(Rapid Spanning Tree Protocol - 802.1w), IEEE tarafından geliştirilmiştir. Oldukça hızlıdır. Yük paylaşımı yapmaz. Switch cihazalrı arasında oldukça hızlı bir şekilde çalışan bu protokol bir sorun çıktığında maksimum 2 saniye içinde hattı açar, eğer switch cihazının ucunda bir bilgisayar takılıysa bilgisayar BPDU paketi gönderemediğinden switch yine 30 saniye bekler. Bunu hızlandırmak için PortFast desteğinden yararlanabiliriz, bu sayede bir başka sorun olan bilgisayar gibi cihazların IP alamayıp internete çıkamamasını engelleyebiliriz ama PortFast durumunda cihazlar uyarı mesajı gönderirler çünkü döngüye neden olabilir, dikkatli bir şekilde kullanılaması önerilir. PortFast aktif edilmiş port döngüye neden olmasın diye BPDU guard desteği kullanılabilir. BPDU guard, ucunda son cihaz olduğu belirlenmiş port üzerinden BPDU paketi gelirse döngüye neden olmasın diye portu kapatır. STP protokolünde bulunan Learning ve Listening durumlarına RSTP protokolünde Discarding denir. Block porta ise Backup veya Alternate port denir. 

Rapid PVST+, Cisco tarafından geliştirilmiştir. Hem çok hızlıdır hem de yük paylaşımı yapar.

MSTP(Multiple Spanning Tree Protocol - 802.1s), IEEE tarafından ortaya çıkarılmıştır. Tüm markalarda kullanılabilir. Çok hızlıdır ve yük paylaşımı gerçekleştirir. 


## Konfigürasyon

STP protokolünün çalışması için hernagi bir konfigürasyon yapılasına gerek yok. Otomatik olarak çalışır. Belli switch cihazlarının root switch olmasını istiyorsanız Bridge priority değerini değiştirebilirsiniz. 

![image](https://user-images.githubusercontent.com/70758694/183244961-be1f731a-967a-412c-9f8f-a6208b615fef.png)

Yukarıdaki modelde Layer 3 switch cihazının root siwtch olmasını isterken otomatik olarak çalışan STP ile bir başka cihaz root switch seçildi. 

![image](https://user-images.githubusercontent.com/70758694/183244953-10c857fb-737d-4118-b8b4-3d1571f1a0ed.png)

`show spanning-tree` komutuyla yukarıda Layer 3 switch cihazı için STP konfigürasyonunu kontrol ediyoruz. Göründüğü gibi root switch olarak başka bir switch cihazını atamış. 

![image](https://user-images.githubusercontent.com/70758694/183245940-4518770a-35b6-4e0a-9938-40c526cb500c.png) ![image](https://user-images.githubusercontent.com/70758694/183245981-c7fb6bdb-71d4-4b46-b5f8-d8388e84febf.png)

Priority değerini değiştirerek root switch atamasını tekrar gerçekleşitiriyoruz.

![image](https://user-images.githubusercontent.com/70758694/183248147-c5963e2d-c42f-46a7-938f-733386f7bd0f.png) PVSTP+ yavaş çalışır, rapid PVSTP+ moduna almak için yukarıdaki konfigürasyonu her switch üzerinde yapmamız gerekir. 

![image](https://user-images.githubusercontent.com/70758694/183248324-8414c763-8e0e-4c7d-8e3d-a0e369431344.png)

Ucuna bilgisayar takılan portları PortFast durumuna getirerek hızlıca IP almasını sağlayabiliriz. Eğer yapmazsak 30 saniye bekleyeceği için cihaz IP almayabilir. Son kullanıcı için bu bir sorundur. 

![image](https://user-images.githubusercontent.com/70758694/183248375-65e74b23-e8de-45ef-8541-978100e74707.png)

Cihazın takılı olduğu port arayüzünde PortFast ve BPDU guard özelliğini aktif ettik. Anında link alabilecek ve ucuna BPDU gönderen bir cihaz takıldığında bağlantıyı sonlandıracaktır. 

![image](https://user-images.githubusercontent.com/70758694/183248425-3492c926-e4b0-4872-836d-500789f9675e.png)

Göründüğü switch cihazı takıldığı anda bağlantı sonlandırıldı. 





















