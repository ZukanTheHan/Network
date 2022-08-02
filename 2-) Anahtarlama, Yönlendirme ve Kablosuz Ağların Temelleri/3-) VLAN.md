# VLAN

Vlan kurmak bize aynı cihaz üzerinde segmentler oluşturabilmemizi sağlar. Bu şekilde şirket içindeki farklı departmanları farklı ağalara bölebiliriz. Broadcast, multicast ve unicast trafiğini her VLAN için izole eder. Her VLAN için ayrıca tanımlanmış IP aralığı vardır. Bu şekilde yönetim daha da kolaylaşır. 

![image](https://user-images.githubusercontent.com/70758694/182159293-2552c9d5-5aa5-4af5-9ecc-7ff9e97cf4d3.png)

Yukarıdaki yapıda göründüğü gibi her cihaz tek bir switch cihazına bağlı ve aynı ağda. Bunları ayırmak istediğimizi düşünelim. Bunun için farklı switch cihazları almamız gerekir. Yukarıdaki örnek için toplam 3 ayrı switch almamız gerekir. IT departmanı için aldığımız switch cihazının sadece 10 portunu kullanbileceğiz. HR için 5. IP telefonlar içinse 3 port. Bunun sadece ilk kat olduğunu düşünün her kat her departman için ayrı ayrı switch cihazı almamız gerekir. Bu oldukça maliyetli ve yönetimi zor bir tasarım olur. Bunun yerine VLAN teknolojisinden yararlanabiliriz. Yukarıdaki örnek için 24 portlu bir switch cihazını kullanarak gerçekleştirebiliriz. 10 portu IT departmanına, 5 portu HR departmanına ve 3 portu da IP telefonlara. Toplam 18 portu kullanmış oluruz ve geriye 6 port daha kalmış olur.

![image](https://user-images.githubusercontent.com/70758694/182161754-4766db51-3a1c-49b0-956d-42befb6a47e7.png)
 
 Bu sayede her departman sadece kendi arasında iletişim sağlar. Böylelikle hem broadcast domainleri düşürdük, hem de daha güvenli ağ oluşturduk. 
 
 Peki, aynı VLAN gruplarına sahip iki switch cihazı üzerindeki cihazların birbirleriyle iletişim halinde olmasını istersek nasıl bir yol izleyebiliriz? 
 
 ![image](https://user-images.githubusercontent.com/70758694/182173193-9599b40c-8e0a-4e52-8419-894854ea2968.png)

Basit olarak yukarıdaki gibi boşta olan portlardan birini VLAN 1, birini VLAN 2 ve birini de VLAN 3'e atarım. Daha sonra diğer switch cihazı ile bağlarım. Diğer switch cihazı da aynı şekilde VLAN gruplarına atıldığı için soldaki switch cihazından çıkan VLAN 1 grubuna ait bir broadcast sağdaki switch üzerindeki VLAN 1 grubuna ait cihazlara da gidecektir. Diğer gruplar içinde aynı şekilde tasarımı gerçekleştirdiğimizde aslında bunun etkili bir yol olamadığını anlayabiliriz. Çünkü grup sayısı arttıkça kullanılacak port sayısıda artmaktadır ve bu şekilde switch cihazı etkili bir şekilde kullanılamayacaktır. Buna çözüm olarak Cisco ISL adında bir protokol ortaya çıkarmıştır. ISL protokolü sayesinde sadece tek bir port üzerinden VLAN gruplarına ait frameler geçirilebilmektedir. Yani VLAN 1,2,3 ve daha fazlası aynı kablo üzerinden diğer switch üzerindeki aynı VLAN gruplarıyla haberleşebilmektedir. Kullanılan bu porta TRUNK protu denilmektedir. Bunun için frame yapısına ek olarak L2 başlığı ve kuyruğu eklenir. Bu şekilde frame oldukça büyür. Bu şekilde tasarlanmasının sebebi ethernet dışında başka protokoller ile haberleşme yapıldığında ortaya çıkabilecek uyumluluk sorunlarını engellemektir. Günümüzde ise ethernet yapısı kullanıldığı için bu protokol yerine IEEE organizasyonunun geliştirdiği 802.1q protokolü kullanılmaktadır. Bu protokolde ise frame yapısına sadece 4 baytlık bir alan eklenmektedir. Buna etiket (tag) denir. VLAN grubuna göre etiket alan frame trunk portundan geçtikten sonra ve diğer switch üzerinden ait olduğu grup belirlendikten sonra etiketi sökülür ve frame grubuna iletilir. 

## VLAN Etiketi 

![image](https://user-images.githubusercontent.com/70758694/182210627-69653c1b-a57c-470e-bf0d-a3a2e5d13155.png)

Frame yapısına eklenen etiket yukarıdaki gibidir.

Type ==> L2 frame yapısındaki type kısmı gibi gelen paketini yapısını bildirir. L2 frame yapısında IPV4 bilgisini verdiği gibi burada da bunun bir 802.1q etiketi olduğu bilgisini verir.

Pri ==> QoS için önceliklendirme bilgisi. IP telefonlar için örnek olarak 5 bilgisi girilirse ve  bilgisayarlara da 0 bilgisi girilirse telefonlara öncelik verecektir. 

CFI ==> Token ring protokolü için kullanılan kısımdır. Günümüzde kullanılmaz.

VID ==> VLAN grup bilgisi verilir. 

## VLAN Türleri

![image](https://user-images.githubusercontent.com/70758694/182207156-83b51241-834d-4e3a-b1c1-d6912e2ef443.png)

Switch cihazlarında varsayılan olarak sadece VLAN 1 grubu vardır ve bu grup silinemez. VLAN grupları atamalarında birinci grup herhangi bir şey için atanmamalıdır. Çünkü switch cihazına takılan herhangi bir cihaz otamatik olarak birinci gruba atanır. Güvenlik için VLAN 1 grubu kullanılması önerilmez. 

Yönetim VLAN'i, switch cihazına IP adresi ataması yaptığımız VLAN'dir. Eğer VLAN 2'ye atanmışsa yönetim VLAN'i VLAN 2'dir. VLAN 3'e atanmışşa VLAN 3 yönetim VLAN'idir.

Data VLAN, bilgisayarlar gibi son cihazların kullandığı VLAN gruplarıdır. IP telefon VLAN grupları ise Voice VLAN olarak bilinir. Voice VLAN'ler oluşturumamazın ilk nedeni güvenlik ve QoS sağlamaktır. Bant genişliğinde dar boğaz olmasını engellemek ve gecikmeyi engellemek gibi QoS yöntemleri uygulanır. 

Native VLAN, etiketsiz taşınan frame verileri için atanan VLAN grubudur. Örnek olarak native VLAN olarak VLAN 2'yi atadığımızı düşünelim, diğer VLAN grupları için iki switch arasında trunk ile geçişlerini sağlayalım. Etiket taşımayan her frame trunk üzerinden de etiketsiz bir şekilde taşınıp VLAN 2 grubundaki cihazlara ulaşır. Bu şekilde çalışabilmesi için iki switch içinde native VLAN atamalarının aynı olması lazım. 

## VLAN Konfigürasyonu

![image](https://user-images.githubusercontent.com/70758694/182361424-c5dcd9f7-1e9a-451a-9590-7ac535182080.png)

VLAN konfigürasyonu oldukça kolaydır. Yukarıdaki dizayn için VLAN konfigürasyonunu aşağıda gerçekleştirdik. PC0 VLAN 2 grubuna dahil edildi. Öncelikle `config` moda geçiş yapıyoruz ve atamak istediğimiz VLAN grubunu seçiyoruz. Burada VLAN 2 seçildi. Daha sonra opsiyonel olarak buna bir isim verdik. İlgili bilgisayarımızın bağlandığı portu konfigüre etmek için fastEthernet 0/1 altına girdik ve `switchport mode access` komutu ile bu portun bir access portu olduğunu belirttik ve `switchport access vlan 2` komutuyla bu portu VLAN 2 grubuna aldık.

![image](https://user-images.githubusercontent.com/70758694/182361197-110d1a83-1727-43c7-9c60-f60aa500b9af.png)

VLAN ataması ile önceden aynı ağ üzerinde bulunan iki bilgisayar artık haberleşemiyor. 

![image](https://user-images.githubusercontent.com/70758694/182363327-1f19d3e2-242c-48b7-913a-58776de9e309.png)

Yaptığımız tüm bu VLAN işlemleri flash dosyasının altında vlan.dat dosyasında tutulur. 

![image](https://user-images.githubusercontent.com/70758694/182362867-3a24f6cc-bd02-4b5a-bf2d-dbfac903ded7.png)

Yaptığımız konfigürasyonu görmek için `show vlan` komutundan yararlanabiliriz. Varsayılan olarak tüm portlar VLAN 1 olduğu için konfigüre edilmemiş olanlar aşağıda görüldüğü VLAN 1 altındadır. 1002-1003-1004-1005 VLAN grupları ethernet dışında token-ring, fddi gibi eski protokolleri kullanabilmek için oluşturulmuştur. Silinemez ve değiştirilemezler. Toplamda 4096 VLAN grubu oluşturulur. Şirketler genelde ilk 1001 VLAN grubunu kullanır, sonrasını ise ISP'ler kullanır. Katı bir sınırlama yoktur. İstenilen VLAN grubu kullanılabilir. 

![image](https://user-images.githubusercontent.com/70758694/182367422-e7f1ec11-536e-4bc2-9eb8-bf1523e20aac.png)

Oluşturulan VLAN gruplarını silmek istersek `no switchport access vlan 2` ve `no vlan 2` komutlarını kullanabiliriz.

![image](https://user-images.githubusercontent.com/70758694/182370728-8ea4d5cf-35c0-419b-a85e-be5dd2a37bf7.png)

`no switchport access vlan 2` komutuyla arayüz üstünde tanımlanmış VLAN grubunu kaldırdık yani bağlı bilgisayar artık VLAN 1 grubuna geçti. `no vlan 2` komutuyla bu grup tanımlamasını sildik.

![image](https://user-images.githubusercontent.com/70758694/182370764-65aa78f2-53c4-42be-af6c-3a7b1bc532a2.png)

Tüm VLAN konfigürasyonunu silmek istersek eğer flash altındaki vlan.dat dosyasını silmemiz gerekiyor. 

![image](https://user-images.githubusercontent.com/70758694/182371687-855b6d8f-91c7-4336-af13-259208632abf.png)

![image](https://user-images.githubusercontent.com/70758694/182379932-de161f38-a41f-47b7-992e-0ed9b02d880f.png)

Yukarıdaki dizayn için VLAN konfigürasyonumuzu yapalım. Burada yapacağımız tek farklı şey iki switch arasında etiketleri kontrol eden portları yani trunk portlarını oluşturmak. Bilgisayarların bağlı olduğu portlar yukarıdaki örnekte olduğu gibi konfigüre edilmiştir. 

![image](https://user-images.githubusercontent.com/70758694/182377680-151bf14f-254a-42c6-b501-a4435f25e9f0.png) ![image](https://user-images.githubusercontent.com/70758694/182377844-678f4dde-5b7f-47dc-bb19-3d8824713155.png)

Switch cihazlarının bilgisayarların bağlı olduğu portlarının VLAN konfigürasonu yukarıdaki gibidir. 

![image](https://user-images.githubusercontent.com/70758694/182378129-474bc79f-a331-48ae-a9f9-42db33deedb4.png) ![image](https://user-images.githubusercontent.com/70758694/182378258-4189073d-8ca9-42e1-be24-91773010001f.png)

PC0 ve PC2 bilgisayarlarının haberleşebilmesi için Switch1 cihazının Fa0/3 portu ve Switch2 cihazının Fa0/4 portu trunk yapılmadır.

![image](https://user-images.githubusercontent.com/70758694/182378441-f3980424-2677-4bef-aa4e-39744dea33b4.png) ![image](https://user-images.githubusercontent.com/70758694/182378513-081d6eeb-5786-4067-be93-09d724c0770c.png)

PC0 PC2'ye ulaşabilirken PC1 ulaşamamaktadır. Bu şekilde başarılı bir şekilde VLAN konfigürasyonu yaptığımızı söylebiliriz. 

![image](https://user-images.githubusercontent.com/70758694/182405153-a425f170-bae3-4859-9e5c-b114d52bfc01.png)

`show interfaces trunk` komutuyla yukarıdaki gibi trunk portlar hakkında bilgi alınabilir. 

Cisco cihazlarda bu şekilde trunk konfigürasyonunu gerçekleştirebilirsiniz ama başka marka cihazlarda trunk portlarına hangi etikete ait VLAN paketlerini geçireceğini belirtmemiz lazım. Cisco cihazlarda da buna ihtiyaç duyabiliriz, çünkü bu şekilde her broadcast paketi geçer ama ilgili etikete sahip değilse son cihazlara ulaşmaz. Eğer cihaz sayısı çok fazlaysa bu durum sorun yaratabilir. 

VLAN konfigürasyon örneklerimizde her switch cihazı için tek tek işlem yapmıştık. Bunu kolaylaştırmak için VTP kullanabiliriz. VTP protokolüyle bir switch cihazına yaptığımız konfigürasyon tüm switch cihazlarına otomatik olarak aktarılır. Örnek, VLAN 20 IP Telefon grubu oluşturalım bu bilgi tüm switch cihazlarına bu protokol sayesinde aktarılır ve trunk portlarında izin verilir.

![image](https://user-images.githubusercontent.com/70758694/182432037-a0a7ff7a-51db-4d5f-ae96-289984902320.png)

Yukarıdaki örnekte IP telefon ve laptop için ayrı ayrı kablo çekmek yerine IP telefonların içine gömülü switch cihazından yararlanıp laptopu IP telefona bağladık. Laptopu personel VLAN grubuna IP telefonunu ise ayrı bir VLAN grubuna almak isteyelim. Bunun için yapılacak konfigürasyon aşağıdaki gibidir. Burada yapılan tek farklı şey voice VLAN ataması gerçekleştirmek.

![image](https://user-images.githubusercontent.com/70758694/182431950-bc448038-9381-4eb3-a985-f1ca6e7464ec.png)

![image](https://user-images.githubusercontent.com/70758694/182445581-30c37fb8-d3ab-4ba9-bd87-5e44c9daeed4.png)

Trunk portlarda yukarıdaki gibi bazı VLAN'lere veya VLAN gruplarına izin verebiliyoruz. İzin verilen VLAN gruplarını kaldırabilir veya yeni VLAN grupları eklenebilir.
Portları konfigüre ederken `switchport mode access` komutuyla access moduna çekiyoruz, varsayılanda portlar DTP protokolünde çalışır. Dynamic Trunk Protocol, takılan cihaza göre yani bilgisayar gibi son cihaz veya switch cihazına göre portu trunk veya access moduna çekiyor. Bu şekilde bırakılması güvenlik sorunana neden olabilir. Saldırgan herhangi bir porttan bağlanıp bağlı olduğu switch cihazına DTP paketleri göndererek portu trunk moda çekebilir. Bu şekilde istediği VLAN gruplarını üstünden geçirebilir yani MITM saldırısı gerçekleştirebilir. Bunu önlemek için trunk portu haricinden diğer tüm portları acces moda çekmek gerekir. 

![image](https://user-images.githubusercontent.com/70758694/182450980-46adf224-0698-4781-b568-98037a8fea82.png)



