# LAN Güvenlik Konsepti

Ağları saldırgan erişimden korumak için çeşitli ağ güvenlik cihazları kullanılmaktadır. Bu cihazlara örnek olarak VPN etkin router, yeni nesil bir güvenlik duvarı (NGFW) ve NAC cihazı verilebilir.

VPN özellikli bir router, kullanıcılara ortak bir ağ üzerinden kurumsal ağa güvenli bağlantı sağlar. VPN hizmetleri güvenlik duvarına entegre edilebilir.

Bir NGFW, durum bilgisi olan paket denetimi, uygulama görünürlüğü ve kontrolü, yeni nesil izinsiz giriş önleme sistemi (NGIPS), gelişmiş kötü amaçlı yazılım koruması (AMP) ve URL filtreleme sağlar.

Bir NAC cihazı, kimlik doğrulama(authentication), yetkilendirme(authorization) ve kayıt etme(accounting) (AAA) hizmetlerini içerir.

Ancak birçok saldırı ağın içinden de kaynaklanabilir. Dahili bir host cihaza sızılırsa, tehdit aktörünün sunucular ve hassas veriler gibi kritik sistem cihazlarına erişmesi için bir başlangıç noktası olabilir.

Uç noktalar, genellikle dizüstü bilgisayarlar, masaüstü bilgisayarlar, sunucular, IP telefonları ve çalışanlara ait cihazlardan oluşur. Uç noktalar, özellikle e-posta veya web üzerinde bulaşan kötü amaçlı yazılımlarla ilgili saldırılara karşı hassastır. Bu uç noktalar tipik olarak antivirüs/kötü amaçlı yazılımdan koruma, host tabanlı güvenlik duvarları ve host tabanlı izinsiz giriş önleme sistemleri (HIPS'ler) gibi host tabanlı güvenlik özelliklerini kullanır. Ek olarak günümüzde uç noktalar en iyi şekilde NAC, host tabanlı AMP yazılımı, e-posta güvenlik cihazı ve web güvenlik cihazı kombinasyonu ile korunmaktadır.

E-mail güvenlik cihazları, son kullanıcı mail aktivitelerini izlerler ve tehdit istihbaratından bilgilerle sürekli sistemlerini güncel tutarlar. Bilinen tehditleri engeller, kötü amaçlı yazılımlara karşı koruma sağlar, kötü amaçlı bağlantı içeren e-postaları tespit eder ve veri kaybını önlemek için giden e-postadaki içeriği şifreler. Sandbox çözümleri kullanan sistemlerde vardır. Son kullanıcıya iletilmeden önce ileti sandbox ortamında açılır ve test edilir. 

Web güvenlik cihazları, web tabanlı tehditlere karşı kullanılan bir teknolojidir. Kuruluşların web trafiğini güvence altına alma ve kontrol etme zorluklarını ele almasına yardımcı olur. Bu güvenlik çözümü, kötü amaçlı yazılım koruması, uygulama görünürlüğü ve denetimi, kabul edilebilir kullanım ilkesi denetimleri ve raporlama işlemleri gibi pke şeyi yapabilme imkanı sağlar. 

Web güvenlik cihazı, kullanıcıların internete nasıl eriştiği üzerinde tam kontrol sağlar. Sohbet, mesajlaşma, video ve ses gibi belirli özelliklere ve uygulamalara, kuruluşun gereksinimlerine göre izin verilebilir, zaman ve bant genişliği sınırlarıyla sınırlandırılabilir veya engellenebilir. URL'lerin kara listeye alınması, URL filtreleme, kötü amaçlı yazılım taraması, URL kategorizasyonu, Web uygulaması filtreleme ve web trafiğinin şifrelenmesi ve şifresinin çözülmesi işlemlerini gerçekleştirebilir.

## AAA

Ağ cihazlarına erişim ve yönetim için AAA işlemlerini gerçekleştirmek ve her kullanıcıyı buna tabi tutmak önemlidir. Bu işlemi local olarak veya sunucu bazlı şekilde gerçekleştirebiliriz. Ağ küçükse local seviyede bu işlemler gerçekleştirilebilir ama büyük bir ağa sahipsek ve kullanıcı sayımız fazla ise sunucu bazlı AAA işlemlerini gerçekleştirmemiz daha doğru olur. En önemli katkısı kolay yönetim olacaktır. Bunun için RADIUS veya TACACS+ protokolleri kullanılabilir.  

![image](https://user-images.githubusercontent.com/70758694/183660776-b30f8627-68f9-4d4c-85ae-e971a1358178.png)

Erişim kontrolü için ağ cihazlarında 802.1x protokolü kullanılabilir. Varsayılada bu protokol kapalıdır. Şekilde görüldüğü gibi bu protokol bazında client olan son cihaz supplicant, kimlik denetleyeci olarak switch cihazı ve kimlik denetleme işlemini yapan sunucu da authentication sunucusu olarak isimlendirilmektedir. Son cihaz erişim yetkisi alabilmesi için aracı görevi gören switch cihazını istenilen bilgileri vermelidir. Sunucu da bu son kullanıcının erişimini kontrol edip geri dönüş sağlar. TACACS+ veya RADIUS sunucusu kullanılabilir. Kablolu veya kablosuz herhangi bir ortamda ve switch dışında başka bir ağ cihazıyla da bu işlem gerçekleştirebilir. 

## Güvenlik zafiyetleri, saldırılar ve önleme

MAC address flooding saldırısıyla saldırgan farklı farklı binlerce MAC adresi oluşturur ve bunlarla trafik oluşturur. Switch cihazı da tüm bu MAC adreslerini öğrenir ve sınıra dayanır. MAC adresi tablosu dolduğunda yeni bir MAC adresi öğrenemeyeceği için gelen her paketi geldiği port tüm portlardan iletir. Port güvenliği alınarak tek bir port üzerinden öğrenilecek MAC adresini sınırlandırabilirsiniz. 

VLAN hoping saldırısı, Cisco cihazlarda VLAN konfigürasyonunda port Dynamic-auto olarak bırakılmışsa saldırgan DTP trafiği yaratıp kendi bulunduğu portu trunk porta çekip istediği VLAN grubuna erişim sağlayabilir. Bunun en kolay trunk portu dışındaki tüm portları access moda çekmek. 

DHCP starvation saldırsında saldırgan Gobbler gibi araçlarla kiralanabilir tüm IP adreslerini kiralar, bunu sahte MAC adresleri türeterek gerçekleştirir. Başka bir kullanacı IP adresi alamadığı için internet hizmeti alamaz. Bunun için son cihazların kiralayabileceği IP adresine sınır getirip koruma sağlayabiliriz.

DHCP spoofing saldırsındaysa saldırgan sahte bir DHCP sunucusu kurar ve kullanıcılara bilgi dağıtmaya başlar. IP adreslerini yanlış verip internet hizmetinden yararlanmalarını engelleyebilir, sahte bir DNS adresi verir ve meşru sitelerin sahte adreslerini kullancıya sağlayıp kullancı bilgilerini çalmaya çalışabilir veya varsayılan ağ geçidi adresi olarak kendi cihazının adresini verebilir ve trafiği üstünden geçirebilir. DHCP snooping özelliği ile bu iki atağa karşı koruma sağlayabiliriz. DHCP snooping, portlara trust ve untrust denilen iki rol atar. Trust portlar server tarafının gönderebileceği DHCP paketlerini gönderebilir, untrust ise client tarafında bulunan cihazların gönderebileceği DHCP paketlerini sadece gönderebilir. Ayrıca untrust portlar 

ARP zehirleme saldırısında saldırgan MAC address spoofing yaparak hedef cihazların MAC adresi tablosunu manipüle edebilir. Örnek olarak saldırgan aynı ağda bulunan hedef cihaza ARP reply paketi göndererek kendini varsayılan ağ geçidi olarak tanıtabilir, buna da paket içerisinde MAC adresini göndererek yapar. Diğer taraftan başka bir ARP reply ile varsayılan ağ geçidine kendini hedef cihaz olarak tanıtabilir. Hedef cihaz üzerinden oluşturualn trafik farklı ağlara gidecekse saldırgan üzerinden geçer. 

IP spoofing saldırısıyla saldırgan kendini başka bir cihaz olarak gösterebilir. Bunu da IP adresini değiştirerek yapar. IP Source Guard ile hem MAC spoofing hem de IP spoofing engellenebilir. 

STP saldırısı, saldırganın BPDU paketleri oluşturarak kendini switch olarak ilan etmesidir. Bu şekilde eğer ortama koşulları sağlıyorsa belli bir trafiği üstünden geçirebilir. Ama daha çok ağ bağlatısını sekteye uğratmak için kullanılabilir. Sürekli priority değerini değiştirerek root switch olup bırakabilir. Bu şekilde bloklanacak port sürekli değişeceği için ağ üzerinde paket iletiminde sorun olabilir. BPDU Guard ile bunu engelleyebiliriz.

CDP vee LLDP protokolleriyle ağ cihazları kendileri hakıında her 30 saniyede bir bilgi yayınlarlar. Keşif saldırısı gerçekleşmesin diye bu protokoller kapatılabilir. Konfigürasyon modunda `no cdp run` veya `no lldp run` komutlarıyla bu yapılabilir. Kapatılaması önerilmez. Portlar üzerinde ayrı ayrı kapatılabilir. CDP için `no cdp enable` LLDP için `no lldp transmit` ve `no lldp receive` komutlarıyla gerçekleştirilir. 

Kullanılmayan portların kapalı kalması ek bir güvenlik sağlar. 

![image](https://user-images.githubusercontent.com/70758694/183700617-d2974576-f6a7-46f1-9947-a2f1317fe71d.png)

Port security özelliğiyle port üzerinde tanımlanacak maksimum MAC adresi sınırlandırılır. Varsayılan olarak bu 1'dir. Bu sayı arttırılabilir. Örnek olarak eğer IP telefon arkasına bilgisayar bağlanmışsa en az iki MAC adresinin aynı port üzerinden hizmet alması gerekir. Switch cihazları arası bir portsa zaten bunun uygulanması önerilmez. Yukarıdaki görselde görüldüğü gibi tek satır komutla port security tanımlanabilir. Violation mode, kural ihlalinde gerçekleştirilecek durumdur, eğer birden fazla MAC adresi tanımlanmaya çalışılırsa port kendini kapatacaktır. Ayrıca port dynamic modda olmaması gerekir. 

![image](https://user-images.githubusercontent.com/70758694/183716781-e7c799a4-a029-4caf-87a4-e61ba8e60046.png)

Port-security modunun pek çok özelliği konfigüre edilebilir. Yukaırda maksimum kabul edeceği MAC adresi sayısını değiştirdik. İşaretli olan yerde göründüğü gibi bunu 2 MAC adresine çektik. 

![image](https://user-images.githubusercontent.com/70758694/183721670-196dbf30-0991-4581-8913-f084d68a6056.png)

MAC adres bazlı güvenlik önlemi alınabilir. Yukarıdaki görselde görüldüğü gibi port üzerinden bağlanacak cihazların MAC adresleri önceden tanımlanabilir. Manuel olarak MAC adresi girilip portun spesifik olarak belli cihazlara hizmet vermesi sağlanabilir. Başka bir cihaz gelip bu porttan ağa bağlanamaz. Cihaz sayısı çok fazlaysa ve farklı portlardan bağlanan cihazlarsa manuel olarak bunların atamalarını yapmak oldukça zor olur. Bunun yerine `switchport port-security mac-address sticky` komutuyla otomatik olarak bağlanan ilk cihazın MAC adresini öğrenir ve switch kapatılıp açılsa bile konfigürasyona kaydedilebildiği için MAC adres bilgisi silinmez. Varsayılan olarak bu özellik dinamiktir, konfigürasyona kaydedilmez. 

Son kullanıcı cihazının sürekli değiştiği bir durumda dinamik olarak atanmış bir port security işimizi görür ama switch cihazıyla arasında başka bir cihaz varsa, örnek olarak IP telefon veya başka bir switch cihazı, link süreli olarak çalışır durumda olduğu için MAC adresi silinmeyecektir, bu yüzden yeni gelen kullanıcı ağa bağlanamaz ve violation shutdown ise port kapanır. Bunun olmaması için aging özelliği devreye alınabilinir. Bu özellikle birlikte belirli bir süre trafik oluşturmayan cihaza ait MAC adresi silinir ve bu sayede başka bir cihaz ağa dahil olabilir veya belirli bir süreden sonra cihaz aktif olarak bağlı olsa da MAC adresi silinir ve tekrar trafik oluşturduğunda MAC adresi dahil edilir. 

![image](https://user-images.githubusercontent.com/70758694/183755170-8f7aa3a5-660e-405a-a3b0-50a4db61b884.png)

Yukarıdaki görselde aging inactivity olarak seçilmiştir. Bu sayede 10 dakikanın sonunda ilgili MAC adresi trafik oluşturumazsa MAC adres bilgisi silinir. Bir MAC adresi için yer açılır. Absolute seçilirse 10 dakikanın sonunda MAC adrese sahip cihaz aktif olsun veya olmasın silinir. Tekrar trafik oluşturduğunda dahil edilir.

Violation modunu konfigüre edebiliyoruz. Shutdown ile port error-disabled durumuna geçer, syslog mesajı oluşturur ve tekrar açılması için yöneticinin önce `shutdown` sonra `no shutdown` komutlarını girmesi gerekir. Restrict ile kural ihlali yapıldığında bağlı olan cihazlar trafik gönderip almaya devam ederler ama kural ihlali yapan cihaz ağa bağlanamaz ve syslog mesajı oluşturulur. Protect modunda ise kural ihlali yapan ağa bağlanamaz, diğer cihazların bağlantısında bir aksama olmaz ama syslog mesajı da oluşturmaz.

![image](https://user-images.githubusercontent.com/70758694/183927411-eab55299-be61-4fc3-ac9b-008d2bf27861.png)

Yukarıdaki görselde göründüğü gibi üç farklı şekilde komut girilebilir. 

![image](https://user-images.githubusercontent.com/70758694/183931660-7fade083-5d86-45b1-a6ee-7fb40f896ab1.png) ![image](https://user-images.githubusercontent.com/70758694/183931488-38701cca-9988-4856-93ea-c1d492bd6169.png)

![image](https://user-images.githubusercontent.com/70758694/183934270-f1029be1-7f62-4a84-a960-7af1117105b7.png)

![image](https://user-images.githubusercontent.com/70758694/183935422-116ab80b-d810-47dc-855c-47dbf7783872.png)

Yukarıdaki dizaynda 2 bilgisayar ve yönetilebilen switch cihazının MAC adresleri olduğu için dördüncü bir cihazla birlikte violation kuralı uygulanıyor. 





