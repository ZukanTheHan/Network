
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







