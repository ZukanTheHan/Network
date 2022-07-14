
# Switch Boot Sekansı

1 - İlk olarak ROM içerisinde yüklü olan power on self test (POST) programı çalıştırılır. Bu programla CPU, DRAM ve flash dosya sistemini kontrol eder.

2 - Daha sonra ROM'da bulunan boot loader software çalışır ve düşük seviye CPU işlemlerini başlatır. Fiziksel belleğin nereye eşlendiğini, bellek miktarını ve hızını denetleyen CPU kayıtlarını başlatır.

3 - Flash dosyalama sistemi boot loader tarafından başlatılır.

4 - Son olarak boot loader IOS işletim sisteminin yerini bulur ve başlatır. İşletim sistemi flash üzerinden RAM'e kopyalanır. 

Flash cihazın depolama alanıdır. İşletim sistemi ve konfigürasyon dosyası burada bulunur. Flash dosyalama sisteminde eğer yeteri kadar yer varsa birden fazla işletim sistemi yüklenebilir. Cihaz tekrar başlatıldığında en eski olan işletim sistemini yükler bunu önlemek için `boot system [dosya yeri]` komutunu kullanırız, bu şekilde cihaza yeni işletim sisteminin yerini gösteririz. Eğer işletim sistemi bozuksa cihaz ROM-MON moda düşer. Cisco cihazlarda böyle adlandırılır. Bu mod üzerinden işletim sistemi yüklenmesi gerekir. Parola unutulduğunda da bu moda girilmesi gerekir. Fiziksel olarak cihazın yanına gidip cihazı kapatıp mode tuşuna basılı tutarken cihazı tekrar açmamız gerekiyor. Cihaz ROM-MOD moduna düşecektir. `switch:` komut istemi bu şekilde gözükecektir. Önce flash dosyasını tanıtmamız gerekiyor. Bunun için `flash-init` komutunu çalıştırmamız gerekiyor. Daha sonra `dir flash:` komutu ile flash dosyasının içine girip `rename flash:[konfigürasyon dosyası] flash:[yeni adıyla konfigürasyon dosyası]` komutuyla kullanılan konfigürasyon dosyasının adını değiştiriyoruz. `reset` komutuyla cihazı yeniden başlatınca cihaz parolasız bir şekilde açılacaktır. 

![image](https://user-images.githubusercontent.com/70758694/178928657-fa0ba680-821b-4791-8569-2fc0ea76094f.png)

Yukarıdaki görselde çalışan bir cihaz içerisindeki flash dosyası görüntülenmektedir. .bin uzantılı dosya işletim sistemi, config.text dosyası ise konfigürasyon dosyasıdır. 






