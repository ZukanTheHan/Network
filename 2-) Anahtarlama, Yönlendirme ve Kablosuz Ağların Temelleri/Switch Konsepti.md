# Switch Konsepti

Switch cihazının bağlı olduğu portuna frame gönderen kaynak MAC adresine sahip cihaz 'Ingress' trafik oluşturur. Switch cihazı MAC tablosuna bakar ve hedef cihaza gelen frame gönderilir. Bu trafiğe ise 'Egress' trafik denir. 

Switch cihazının MAC tablosunda eğer kaynak MAC adrese ait bir bilgi yoksa ilgili porta kaynak MAC adresi kaydedilir. Hedef MAC adresinin kaydı MAC tablosunda yoksa 1 frame, gelen port hariç tüm portlara gönderilir. Hedef cihaz cevap döndüğünde MAC adresi ilgili port için MAC tablosuna kaydedilir. 

MAC tablosu Content Addreasble Memory (CAM) tablosu olarakta bilinir. Switch cihazı çok hızlı bir şekilde çalışır, bunun nedeni application-specific-integrated circuits (ASIC) denen yapıdır. ASIC, cihazın frame işleme süresini azaltır ve cihazın, performansı düşürmeden artan sayıda frame yönetmesine olanak tanır.

Switch cihazları frame iletimi yaparken iki yöntemden birini kullanır. Store and forward ve cut-through switching. Store and forward switching yönteminde, switch cihazı frame yapısının tamamını tampon belleğine alır. FCS kontrolüyle frame yapısının bozulup bozulmadığını anlar ve frame iletimini gerçekleştirir. Cut-through switching yönteminde, switch cihazı sadece hedef MAC adresi kısmına kadar kontrol işlemini gerçekleştirir ve gönderimi yapar. Bu yöntem 10 microsaniye gecikmenin altına inilmek isteniyorsa kullanılır.

## Collision Domain ve Broadcast Domain

Bir colllision gerçekleştiğinde bundan etkilenen cihazların oluşturduğu bölgeye collision domain denir. 

![image](https://user-images.githubusercontent.com/70758694/182135927-54e261a3-11cd-411d-90cb-73e26d28a06c.png)

Yukarıdaki örnekte HUB cihazı kullanılmıştır. Bu yüzden oluşan herhangi bir collision bağlı olan tüm HUB'larda ve cihazlarda oluşur. Çünkü HUB'lar FCS kontrolü yapamaz, konfigüre edilemez ve gelen her frame tüm portlardan iletilir.

![image](https://user-images.githubusercontent.com/70758694/182138769-fbb31485-c505-4e21-aa5e-0252f01d4b89.png)

Switch cihazları ise collisionları protları arasında iletmezler. Çünkü, MAC adresi tablosuna göre frame iletimi gerçekleştirirler ve FCS kontrolü yaparlar. Collision domain switch cihazının her portunda olur. Yukarıdaki örnekte 7 collision domain vardır. 

![image](https://user-images.githubusercontent.com/70758694/182139501-4999d825-7567-404a-acae-f316b0adea9d.png)

Broadcast domain ise sadece Layer 3 cihazları tarafından kesilir. Switch cihazları arasında broadcast iletimi olacağı için burada sadece bir tane broadcast domain yapısı mevcuttur. 



