# EtherChannel

![image](https://user-images.githubusercontent.com/70758694/183258642-b54d9f9a-da22-4fef-b252-108d6edfbe96.png)

EtherChannel teknolojisiyle birlikte iki veya daha fazla (maksimum 8) kabloyu tek bir mantıksal kablo göstererek yedeklilik, bant genişliği ve yük paylaşımı yapılabilir. Görselde görüldüğü gibi iki kablo mantıksal olarak tek bir kablo olarak gösterilebilir ve bu şekilde döngü oluşmaz. Dikkat edilmesi gereken en önemli şey iki kablonun aynı hızı desteklemesidir. Yani 100Mbps - 100Mbps, 10Gbps - 10Gbps vb. gibi. İki farklı hızı bu teknoloji desteklemez. 

Karşılıklı portların konfigürasyonu aynı olmalıdır. Hatalı bir işlem yapılmasını önlemek için PAgP Cisco (Port Aggregation Protocol) veya LACP IEEE-802.3ad (Link Aggregation Control Protocol) etherchannel yapılacak portların birbirlerini kontrol edebilmesini sağlar. Eğer portlar aynı konfigürasyonlara sahip değilse etherchannel gerçekleşmez. İstenirse statik bir şekilde etherchannel kurulabilir ama önerilmez. Protokol ayarlanmışsa her 30 saniyede bir cihazlar birbirlerine kontrol paketi gönderir. 

## Konfigürasyon 

![image](https://user-images.githubusercontent.com/70758694/183258559-d7212d22-84bf-4f53-8b98-a89fe0d08566.png) ![image](https://user-images.githubusercontent.com/70758694/183258714-6d646806-e95f-4a43-a236-c3cf5315d853.png)

![image](https://user-images.githubusercontent.com/70758694/183258674-adf0c46a-8b85-48fd-8cbc-fdb1fc5ef570.png) ![image](https://user-images.githubusercontent.com/70758694/183258688-954f5575-9859-48b4-8b47-8fc40a161605.png)

Öncelikle etherchannel kullanılacak portların altına `range` komutuyla giriyoruz ve `channel-group [1-6 arası bir sayı] mode [LACP-PAgP-Manuel]` komutuyla görselde görüldüğü gibi bir grup oluşturuyoruz, birden fazla grup oluşturabiliriz ve karşılıklı aynı olmasına gerek yok, hangi protokolü kullanacağımızı veya manuel yapıp yapmayacağımızı belirliyoruz. Biz burada PAgP protkolünü seçtik, LACP protokolü de seçilebilir. Daha sonra mantıksal arayüz oluşturulur ve bundan sonra bu iki port için girilecek herahngi bir konfigürasyon bu arayüz altından yapılmalıdır. Biz burada trunk port olarak atadık, VLAN için işlemlerde yapılabilir veya herhangi konfigürasyon. Diğer switch içinde aynı şeyleri yaptıktan sonra konfigürasyonları aynı olmak zorunda olduğu için burayı da trunk port olarak ayarlıyoruz. 

![image](https://user-images.githubusercontent.com/70758694/183259178-80057bf0-afce-4f18-8d5f-c7bc2242e6f5.png) ![image](https://user-images.githubusercontent.com/70758694/183258799-a3a707d0-1619-4475-bfd6-6b66dbbefd9c.png)

IP adresi atamalarını deneme yapmak için atadık. Ping denememizde diğer kabloyu çıkartıyoruz ve herhangi bir gecikme olmadan göründüğü gibi yedeklilik için uygun koşulları sağlıyor. 

![image](https://user-images.githubusercontent.com/70758694/183259634-2711888e-9c36-4f64-ac5c-39f9b5d5e6a6.png)

`show etherchannel summary` komutuyla etherchannel hakkında bilgi edinebiliriz. 



