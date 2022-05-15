
# Switch Boot Sekansı

1 - İlk olarak ROM içerisinde yüklü olan power on self test (POST) programı çalıştırılır. Bu programla CPU, DRAM ve flash dosya sistemini kontrol eder.

2 - Daha sonra ROM'da bulunan boot loader software çalışır ve düşük seviye CPU işlemlerini başlatır. 

3 - Flash dosyalama sistemi boot loader tarafından başlatılır.

4 - Son olarak boot loader işletim sisteminin yerini bulur ve başlatır.

Flash cihazın depolama alanıdır. İşletim sistemi ve konfigürasyon dosyası burada bulunur. Flash dosyalama sisteminde eğer yeteri kadar yer varsa birden fazla işletim sistemi yüklenebilir. Cihaz tekrar başlatıldığında en eskş olan işletim sistemini yükler bunu önlemek için `boot system` komutunu kullanırız, bu şekilde cihaza yeni işletim sisteminin yerini gösteririz.

