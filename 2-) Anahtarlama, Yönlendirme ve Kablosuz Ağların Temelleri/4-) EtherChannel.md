# EtherChannel

EtherChannel teknolojisiyle birlikte iki veya daha fazla (maksimum 8) kabloyu tek bir mantıksal kablo göstererek yedeklilik, bant genişliği ve yük paylaşımı yapılabilir. Görselde görüldüğü gibi iki kablo mantıksal olarak tek bir kablo olarak gösterilebilir ve bu şekilde döngü oluşmaz. Dikkat edilmesi gereken en önemli şey iki kablonun aynı hızı desteklemesidir. Yani 100Mbps - 100Mbps, 10Gbps - 10Gbps vb. gibi. İki farklı hızı bu teknoloji desteklemez. 

Karşılıklı portların konfigürasyonu aynı olmalıdır. Hatalı bir işlem yapılmasını önlemek için PAgP Cisco (Port Aggregation Protocol) veya LACP IEEE-802.3ad (Link Aggregation Control Protocol) etherchannel yapılacak portların birbirlerini kontrol edebilmesini sağlar. Eğer portlar aynı konfigürasyonlara sahip değilse etherchannel gerçekleşmez. İstenirse statik bir şekilde etherchannel kurulabilir ama önerilmez. Protokol ayarlanmışsa her 30 saniyede bir cihazlar birbirlerine kontrol paketi gönderir. 
