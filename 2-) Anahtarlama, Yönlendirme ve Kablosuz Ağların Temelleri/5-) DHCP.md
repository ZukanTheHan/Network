# DHCPv4

DHCPv4, IP adresi ve diğer ağ bilgilerini dinamik bir şekilde atayan teknolojidir. Yönetme ve ölçeklendirme açısından kolaylık sağlar. Ayrıca bir sunucu DHCPv4 için ayarlabilinir veya router cihazları da DHCPv4 sunuculuğu yapabilir. Önerilen ayrı bir sunucunun ayarlanmasıdır. Cihazlara atanan IP adresleri belli bir süre kiralanır. Kira süresi değişkenlik göstebilir. Genellikle 24 saat veya haftalık olarak atanır. 

Client tarafında bulunan cihazlar DHCPDISCOVER denilen bir broadcast paketi yollarlar ve bu şekilde ortamda bulunan tüm DHCPv4 sunucularına bu paket gider, DHCPv4 sunucusu/sunucuları DHCPOFFER unicast paketiyle, çünkü DHCPDISCOVER paketiyle client cihaz kaynak MAC adresini göndermiştir, bir IP adresi teklif eder. Client DHCPREQUEST broadcast paketiyle hem teklifi yapan sunucuya hem de ortamda bulunan diğer DHCPv4 sunucularına IP adresini kabul ettiğini bildirir. Sunucu da DHCPACK unicast paketiyle işlemi onaylar. Client cihazlar kira süresini uzatmak için tekrar DHCPREQUEST paketi gönderirler, sunucu kabul ederse DHCPACK paketiyle bunu onaylar. Eğer onaylamazsa süresi dolsuktan sonra cihaz tekrar IP adresi ister.

Broadcast paketleri yüzünden bu işlem güvenlik zafiyeti içerir. Aynı ağ içerisinde bulunan saldırgan sahte bir DHCPv4 sunucusuyla diğer cihazlara kendi IP adresini varsayılan ağ geçidi olarak öğretebilir. Bu sayede trafiği görüntüleyebilir veya sahte bir DNS adresi öğreterek meşru sitelerin adreslerini sahteleriyle değiştirip parolalarınızı çalmaya çalışabilir. 

## Konfigürasyon

DHCPv4 sunucularında dağıtacağı IP adres aralığı, varsayılan ağ geçidi, kiralama süresi, DNS bilgisi, domain-name, netbios-name-server, tftp sunucusu gibi bilgiler konfigüre edilebilir ve bunları cihazlara öğretebilir. Netbios, windows cihazlarda haberleşmeyi isimlerle sağlayan bir hizmettir. Bir cihaza isim verirsiniz, örnek TestCihazı, bu cihaza ismi ile ulaşabilirsiniz. Netbios-name-server ya da WINS cihaz isimlerini diğer bilgisayarlara öğreten sunucudur. Ağ içerisinde cihazlar birbirinin adını broadcat göndererek öğrenmesin diye geliştirilmiştir. Tftp bilgisi genellikle IP telefonlar için kullanılır. IP telefon tftp sunucusunu öğrenir ve konfigürasyonunu buradan alır. 

![image](https://user-images.githubusercontent.com/70758694/183288863-a0e41812-0ab8-47af-8d18-6fc03c41182d.png) ![image](https://user-images.githubusercontent.com/70758694/183288892-efbb46c1-a635-40b1-8c09-0c410c5a1984.png)

Yukarıdaki basit modelde router cihazımızı DHCPv4 sunucusu olarak kullandık. Önce router cihazımızın 0/0/0 arayüzüne IP adresi atadık ve portu açtık. DHCP havuzu oluşturduk ve isim verdik. IP aralığımızı belirttik ve varsayılan ağ geçidiyle DNS server bilgisini de atadık. 

![image](https://user-images.githubusercontent.com/70758694/183289048-30ff2b07-e40b-497d-a9d2-c74dd4069a8f.png) Görselde de görüldüğü gibi bağlı bilgisayar DHCP üzerinden bilgilerini almış. 

![image](https://user-images.githubusercontent.com/70758694/183289221-f3badc1a-7d42-433b-9f1e-3fc9f081d459.png) `ip dhcp excluded-address 192.168.20.0 192.168.20.10` komutuyla belirli IP aralığını vermemesini sağladık. `domain-name` komutuyla bir domain adı da tanımlayabiliriz. 

![image](https://user-images.githubusercontent.com/70758694/183289387-607f372c-c657-4a71-a32e-b77c4bb075cc.png) `show ip dhcp binding` komutuyla hangi IP adresi hangi cihaza atanmış görünebiliyor. 

## DHCP Relay

Farklı ağların bulunduğu bir modelde yukarıdaki gibi router cihazını DHCP sunucusu olarak atayamayız. Router bu işlemi kaldıramaz. Onun yerine DHCP sunucusu oluşturmamız lazım ama her ağa farklı bir DHCP sunucusu kurmamız etkili bir çözüm olmaz. Onun yerine DHCP Relay tekonoljisinden yararlanmalıyız. Relay ile router cihazına gelen broadcast DHCP paketleri unicast paketlere döünüştürülerek belirtilen DHCP sunucu adresine yönlendirilir. Bu şekilde farklı ağlarda bulunan cihazlarda tek bir DHCP sunucusundan hizmet alabilir. 

![image](https://user-images.githubusercontent.com/70758694/183290989-301a8303-4875-43f9-8f0b-42b68ef0aee1.png) ![image](https://user-images.githubusercontent.com/70758694/183291005-2c047736-928e-4829-80e5-268bacee5df1.png)

`ip helper-address [DHCP IP adresi]` komutuyla router cihazının 0/0/0 arayüzne gelen broadcast DHCP paketleri unicast olarak 192.168.30.3 IP adresli DHCP sunucusuna gidecektir. 







