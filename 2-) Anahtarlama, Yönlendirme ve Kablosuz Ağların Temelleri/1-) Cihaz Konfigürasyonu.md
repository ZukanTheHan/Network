
# Switch Boot Sekansı

1 - İlk olarak ROM içerisinde yüklü olan power on self test (POST) programı çalıştırılır. Bu programla CPU, DRAM ve flash dosya sistemini kontrol eder.

2 - Daha sonra ROM'da bulunan boot loader software çalışır ve düşük seviye CPU işlemlerini başlatır. Fiziksel belleğin nereye eşlendiğini, bellek miktarını ve hızını denetleyen CPU kayıtlarını başlatır.

3 - Flash dosyalama sistemi boot loader tarafından başlatılır.

4 - Son olarak boot loader IOS işletim sisteminin yerini bulur ve başlatır. İşletim sistemi flash üzerinden RAM'e kopyalanır. 

Flash cihazın depolama alanıdır. İşletim sistemi ve konfigürasyon dosyası burada bulunur. Flash dosyalama sisteminde eğer yeteri kadar yer varsa birden fazla işletim sistemi yüklenebilir. Cihaz tekrar başlatıldığında en eski olan işletim sistemini yükler bunu önlemek için `boot system [dosya yeri]` komutunu kullanırız, bu şekilde cihaza yeni işletim sisteminin yerini gösteririz. Eğer işletim sistemi bozuksa cihaz ROM-MON moda düşer. Cisco cihazlarda böyle adlandırılır. Bu mod üzerinden işletim sistemi yüklenmesi gerekir. Parola unutulduğunda da bu moda girilmesi gerekir. Fiziksel olarak cihazın yanına gidip cihazı kapatıp mode tuşuna basılı tutarken cihazı tekrar açmamız gerekiyor. Cihaz ROM-MOD moduna düşecektir. `switch:` komut istemi bu şekilde gözükecektir. Önce flash dosyasını tanıtmamız gerekiyor. Bunun için `flash-init` komutunu çalıştırmamız gerekiyor. Daha sonra `dir flash:` komutu ile flash dosyasının içine girip `rename flash:[konfigürasyon dosyası] flash:[yeni adıyla konfigürasyon dosyası]` komutuyla kullanılan konfigürasyon dosyasının adını değiştiriyoruz. `reset` komutuyla cihazı yeniden başlatınca cihaz parolasız bir şekilde açılacaktır. 

![image](https://user-images.githubusercontent.com/70758694/178928657-fa0ba680-821b-4791-8569-2fc0ea76094f.png)

Yukarıdaki görselde çalışan bir cihaz içerisindeki flash dosyası görüntülenmektedir. .bin uzantılı dosya işletim sistemi, config.text dosyası ise konfigürasyon dosyasıdır. 

Switch cihazını uzaktan yönetmek için bir SVI arayüzü oluşturumamız ve IP adresi vermemiz gerekiyor. Aynı zamanda default gateway adresi de verilmesi gerekiyor. 

**Not:** Switch cihazlarını uzaktan yönetmek için IPv4 adresi yanında IPv6 adresi de verilebilir. Layer 2 switch cihazlarının bazıları IPv6 desteklemeyebilir. Bunun için  `sdm prefer dual-ipv4-and-ipv6 default` komutu kullanılır. Daha sonra `reload` komutuyla cihazı yeniden başlatılır. 


SVI arayüzü için genellikle vlan 1 arayüzü seçilir. Vlan konusu daha sonra anlatılacaktır. 

![image](https://user-images.githubusercontent.com/70758694/178953244-57884447-f658-413c-83aa-41c94afe8b34.png)

![image](https://user-images.githubusercontent.com/70758694/178953847-66b4f539-e360-4990-8a0d-988903a2ae72.png)

![image](https://user-images.githubusercontent.com/70758694/178954253-e2194e23-c6f6-4bf6-ba27-855be94c1a87.png)

## Switch Portlarını Konfigüre Etmek

Portlar full veya half dubleks olarak ayarlanabilir. Full dubleks aynı anda veri alıp verebilen half dubleks ise birim zamanda sadece veri gönderebilen veya alabilen demektir. Switch portları genellikle auto durumundadır. Bağlanan cihaza göre full/half dubleks olarak kendini ayarlar. GigabitEthernet portları ise sadece full dubleks olarak çalışır. Aynı zamanda speed ayarı da bulunmaktadır. Portlar 10/100/1000 olarak otomatik olarak ayarlanabilen hızlara sahip olabilir. Sabitlenip  tek bir hızda hizmet vermesi de sağlabilir. 

![image](https://user-images.githubusercontent.com/70758694/178958176-bb0f2e27-ff83-4d78-9934-c7262e67c7c7.png)

### Switch Doğrulama Komutları

1-) Arayüz durumunu ve konfigürasyonunu göster --> `show interfaces [arayüz id]`

![image](https://user-images.githubusercontent.com/70758694/178963042-7eea1e66-c6c2-4b5a-92dd-c4b647b6f0f8.png)

2-) Başlangıç konfigürasyonunu gösterir --> `show startup-config`

![image](https://user-images.githubusercontent.com/70758694/178963423-305ae119-aedd-48be-a64c-e8071b8b2d24.png)

3-) Çalışan konfigürasyonunu gösterir --> `show running-config`

![image](https://user-images.githubusercontent.com/70758694/178963693-a5112dd2-5382-4ab1-b58f-da8b8e547016.png)

4-) Flash dosya sisttemini görüntüler --> `show flash`

![image](https://user-images.githubusercontent.com/70758694/178963936-f7cc99b0-ce24-491f-a4ab-ba11882cab19.png)

5-) Donanım ve yazılım durumunu gösterir --> `show version`

![image](https://user-images.githubusercontent.com/70758694/178964315-620e391c-7f7c-4164-afab-126405d58b3f.png)
 
6-) Komut geçmişini gösterir --> `show history`

![image](https://user-images.githubusercontent.com/70758694/178965137-88ba9a38-eb4c-426a-9530-b90457103e0d.png)

7-) Bir arayüz hakkındaki IP bilgilerini gösterir --> `show ip interfaces [arayüz id]`

![image](https://user-images.githubusercontent.com/70758694/179165720-be33cbc3-e1fc-4d4e-9cd1-9f3b0670df34.png)

### Ağ Erişim Katmanı Sorunları

![image](https://user-images.githubusercontent.com/70758694/179168849-1bab4ed6-10be-4f55-a0aa-fbb6416032b5.png)


Ağ erişim katmanında çeşitli sorunlar yaşayabiliriz. Kullandığımız arayüzlerde herhangi bir problemin olup olmadığını kontrol edebilmek için switch cihazımız üzerinde `show interfaces [arayüz id]` komutunu çalıştırabiliriz. Switch cihazı hatalı verilerin istatistiğini tutar. İşaretli olan yerler bize hatalı verileri gösterir.

**Input Errors**- Bir arayüze giren yani dışarıdan gelen paketlerdeki hataların toplamıdır. Runts, giants, no buffer, CRC, frame, overrun ve ignored counts verilerini içerir.

**Runts**- Ethernet frame boyutu en küçük 64 byte olabilir. Bu değerden daha küçük veri gelirse runt olarak adlandırılır. 

**Giants**- Ethernet frame boyutu en fazla 1518 byte olabilir. Bu değerden daha büyük veri gelirse giant olarak adlandırılır. Ethernet frame boyutu özel arttırılabilir ve bunlara jumbo frame denir.

**CRC**- 2. katmanda pakete bir kuyruk eklenir. Buna FCS numarası denir. CRC algoritması ile hesaplanan bu değer eğer gelen frame ile eşleşmiyorsa CRC hatası artar. 

**Output Errors**- Arayüzden çıkan paketlerdeki hatalara denir. 

**Collisions**- Half dubleks çalışan cihazlarda meydana gelebilecek bir hatadır. Aynı anda veri gönderimi olursa çarpışma olur ve işlem tamamlanamaz. Günümüzde full dubleks çalışıldığı için bu hatayla karşılaşmayız.

**Late Collisions**- Half dubleks çalışan cihazlarda çarpışma meydana geldiğinde bir JAM sinayli yollanır ve cihazlar tekrar gönderim sağlarlar. Eğer gönderim boyutu 512 bit değeri geçmişse gönderim sonunda çarpışma olduğu anlaşılır. 

## Güvenli Uzaktan Erişim

Cihazlarımıza güvenli bir şekilde uzaktan erişmek için telnet yerine ssh kullanmalıyız. Telnet, düz metin şeklinde veri gönderip aldığı için araya giren herhangi bir saldırgan kolaylıkla tüm oturumu dinleyebilir ve parolaları çalabilir. SSH ise tüm oturumu şifreler ve araya girmeye çalışan biri olsa bile sadece şifrelenmiş veri görecektir. Bazı cihazlar ssh desteklemeyebilir. Örnek olarak Cisco bazı ülkelere kriptoloji destekleyen cihazları satmaz. Cihazınızın ssh destekleyip desteklemediğini anlamak için `show version` komutunu kullanabiliriz. Eğer "k9" ibaresi geçiyorsa cihaz ssh destekliyor demektir.

![image](https://user-images.githubusercontent.com/70758694/179174609-544bf16e-7c05-408a-8885-d63b0847f7ac.png)


### SSH Konfigürasyonu

![image](https://user-images.githubusercontent.com/70758694/179200437-73f92511-41d6-4e91-9df3-2265bc937ab3.png)

1. Önce bir hostname ve domain-name ataması gerçekleştirdik.
2. Kripto anahtarını RSA kullanarak oluşturduk. Daha önce oluşturulmuş bir tane anahtar var, tekrar oluşturma işlemi için sordu. İlk kez yapıldığında bu soruyu sormaz. Anahtar boyutunu minumum 1024 bit olarak ayarlamamız gerekir. Maksimum 2048 bit anahtar uzunluğu olabilir. 
3. Oturumu açmak için bir kullanıcı ve parolaya ihtiyacımız var. Username ve secret komutları ile bunları da oluşturduk. Bu işlem kimlik doğrulama sunucuları ile de yapılabilir. Password komutu da kullanılabilir ama password komutuyla atanan parolalar geri çözülebilir bir kriptoyla şifrelenir. Secret ise Salted MD5 kriptoloma algoritmasını kullanılır. Daha sonra bu konuya tekrar değineceğiz. 
4. Line vty 0-15 hatlarına geçtik ve burada sadece SSH protokolünü etkinleştirdik. Oluşturduğumuz kullanıcı adı ve parolanın etkinleştirilmesini sağladık.
5. SSH versiyon 2'yi etkinleştirdik. Varsayılan olarak versiyon 1 ve versiyon 2 etkindir. Daha sıkı bir güvenlik versiyon 2'yi tercih etmeliyiz.

## Router Cihazları

Router cihazları birçok arabirim türünü destekler. Seri, DSL, kablo ve Gigabit Ethernet arabirimlerini destekler. HWIC yuvalarına sahiptir. 

![image](https://user-images.githubusercontent.com/70758694/179215337-975e960d-73c9-4223-91ad-e9d41028d24e.png)

Yukarıda görüldüğü gibi 4 yuvaya sahiptir. En soldaki yuvaya Serial High Speed WAN interface card takılmıştır. İki serial portu bulunmaktadır. 

![image](https://user-images.githubusercontent.com/70758694/179216873-b9e56236-885f-4562-8b67-667d4c62ac95.png)

Yukarıdaki gibi takılan bir başka modül konfigüre edilebilir. `description` komutuyla açıklama yazılabilir.





