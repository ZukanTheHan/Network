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


 
