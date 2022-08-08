# FHRP 

Bugüne kadar L1 ve L2 yedekliliğini sağladık. Şimdi L3 seviyesinde yedeklilik sağlamaya geldi. FHRP bir protokol değildir, açılımı First Hop Redundancy Protocols, yani aslında protokoller topluluğudur. Pek çok protokol geliştirilmiştir. Ana felsefe Virtual Router oluşturup varsayılan ağ geçidi olarak atamaktır.

![image](https://user-images.githubusercontent.com/70758694/183307786-f1e38831-6127-4ca6-a6a1-b48392654cd1.png)

Yukarıdaki görselde görüldüğü gibi router cihazlardan biri aktif varsayılan ağ geçidi diğeri beklemede varsayılan ağ geçidi olarak atanmıştır. Virtual IP ve MAC adresi son cihaza varsayılan ağ geçidi bilgileri olarak konfigüre edilmiştir. Eğer Aktif router cihazı aksaklık yaşarsa son cihazda herhangi bir konfigürasyon yapmadan trafik beklemede olan router üzerinden geçmeye başlar. 

Genellikle HSRP ve VRRP protokolü kullanılır. HSRP, Cisco tarafından geliştirilmiştir. VRRP, open standart bir protokoldür. Birde GLBP protokolü vardır. Cisco tarafından geliştirilmiştir. HSRP protokolünden farkı bu protokolle birlikte yük paylaşımı yapabilmemizdir. İki router cihazı da aktif olarak kullanılır. 

Örneklerle anlatabilmemiz için iki router cihazından oluşan modeller üzerinden gidildi ama ikiden fazla router cihazıyla da bu işlem gerçekleştirilebilir.  

## HSRP

Cisco tarafından geliştirilmiştir. Aktif, beklemede ve diğer şeklinde router cihazları adlandırılır. Aktif olan cihaz aksaklık yaşadığında beklemede olan cihaz aktif olur ve diğer cihaz beklemeye geçer. Virtual IP adresi farklı bir IP adresi olmak zorundadır. VRRP protokolünde aynı IP adresi verilebilir.

İki farklı versiyonu bulunur. V1, IPv4 destekler. V2, IPv6 desteği için geliştirilmiştir. V1'de 0-255 arası bir grup numarası verilir, grup numarasının cihazlarda aynı olması gerekir. Çünkü, grup numarasıyla V1'de virtual MAC adresinin son iki basamağı tamamlanır. Eğer grup numaraları farklı olursa farklı virtual MAC adreslerine sahip olurlar, bu şekilde sistem istediğimiz gibi çalışmaz. V2'de grup numarası 0-4095 aralığındadır. Virtual MAC adresinin son basamağı grup numarasıyla tamamlanır. 

İki versiyon için atanmış MAC adres aralığı vardır. 

V1 => 0000.0C07.AC**00** - 0000.0C07.AC**FF** Son iki basamağı grup numarasından oluşur. 

V2 => IPv4 - 0000.0C9F.F**000** - 0000.0C9F.F**FFF** IPv6 - 0005.73A0.0**000** - 0005.73A0.0**FFF** Son üç basamağı grup numarasından oluşur.

İki versiyonda da router cihazları birbirleriyle haberleşebilmesi için multicast adresler atanmıştır. V1'de 224.0.0.2. V2'de IPv4 - 224.0.0.102 IPv6 - FF02::66.

V2'de ayrıca MD5 authentication özelliği mevcuttur. Bu şekilde kurum dışı bir cihazın kendini gateway olarak anons etmesini engellenmeye çalışılır. 

HSRP protokolünde cihazlar multicast adreslerine hello paketleri gönderir ve her 3 saniyede bir yaparlar. Bu şekilde çalışmaya devam ettiğini bildirmiş olur. Aktif cihaz IP adresinin sayısal olarak büyüklüğüne göre seçilir. Eğer diğer cihazın aktif olmasını istereseniz o cihazın priority değerini arttırabilirsiniz. Varsayılan olarak bu değer 100'dür. 

HSRP 5 durumdan oluşur. Initial, Learn, Listen, Speak ve Standby. Initial, konfigürasyon yapılmış ama daha sistem çlışmıyor. Learn, router virtual IP adresini, aktif router cihazını bilmiyor ve hello mesajı bekliyor. Listen, virtual IP adresini öğrenmiştir ama aktif veya bekleme modunda değildir, hello paketini bekler. Speak, yönlendirici periyodik olarak hello mesajları gönderir ve aktifle beklemede olan router seçilir. Stanby, router bir sonraki aktif router adayıdır ve periyodik olarak hello paketleri gönderilir. 

Beklemede olan router, aktif cihazdan 10 saniye boyunca hello paketi alamazsa aktif router rolünü üstlenir. Bu süre değiştirilebilir. Aktif router tekrar hizmet vermeye dönerse varsayılan olarak beklemede kalır ama Preemption özelliği ile istenilirse aktif cihaz hizmete geri döndüğünde tekrar aktif cihaz rolünü alır.

## Konfigürasyon

![image](https://user-images.githubusercontent.com/70758694/183488685-ef6edc01-72b8-4f8d-b5d7-0c6993455d46.png)

Çalışacağımız model yukarıdaki gibidir. Router cihazlarının adreslerini şekilde göründüğü gibi atadık. Son cihazların varsayılan ağ geçidi virtual IP adresi olarak ayarlanmıştır. 

![image](https://user-images.githubusercontent.com/70758694/183489152-3711c92e-f4ab-4f35-8218-83bd2d8ae836.png) ![image](https://user-images.githubusercontent.com/70758694/183489228-e9698cb1-e065-412a-8f49-301f83fb7058.png)

Router cihazalrı üzerindeki konfigürasyon bu şekilde oldukça kolay. Sadece tek satır komutla bunu gerçekleştirebiliyoruz. `show standby brief` komutuyla HSRP hakkında özet bilgi alabiliriz. 

![image](https://user-images.githubusercontent.com/70758694/183489842-98078c41-91fc-4622-b2aa-186f6b4e737d.png)

YUkarıdaki görsel bir son cihazın ping atma işlemini gösteriyor. Bu işlem sırasında aktif olan router cihazının bağlantısını kesiyoruz ve işaretli alanda görüldüğü gibi biraz gecikme olduktan sonra beklemede olan router aktif role bürünüyor ve paketleri almaya devam ediyor.

IP adresinin sayısal büyüklüğü aktif router cihazını belirlediğini söylemiştik, buradaysa tam tersi bir durum söz konusu. Bunun sebebi 10.0.0.1 router cihazını daha önce konfigüre etmemiz. 

![image](https://user-images.githubusercontent.com/70758694/183492488-b7122796-b032-41c4-9b69-6e914bbe34c3.png)

Priority değerini değiştirerek hangi cihazın aktif olacağını seçebiliriz. Eğer herhangi bir sorun olursa tekrar aktif cihaz rolünü oynaması için preemption özelliğinden yararlanabiliriz.
