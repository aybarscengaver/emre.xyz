---
layout: post
title:  "OJS Open Journal Services - Açık Dergi Hizmetleri"
date:   2015-04-02
categories: genel
---

4 aydır [OkulBilişim](http://okulbilisim.com) bünyesinde çalışıyorum. Geliştirdiğimiz
bir projeden bahsetmek istiyorum. Adından belli olduğu üzere online bir dergi
yayınlama servisi olan [Ojs.io](http://ojs.io) projesinden bahsedeceğim.

4 Mart 2014  tarihinde başlayan proje şu anda hala geliştirme aşamasında olmasına
rağmen güzel ilgi gördü. Hızla ilk release'i çıkartmaya çalışıyoruz.

### Nedir?

OJS, kurumların, özel şirketlerin veya kişilerin, aylık - haftalık - yıllık
döngülerde dergilerini yayınlayabilecekleri bir hizmet. OJS'yi farklı kılan şey
ise inceleme süreci.

OJS'de önce kurumlar var, bu kurumlara ait dergiler. Derginizi oluşturduğunuzda
isterseniz hemen içerik oluşturmaya başlayabiliyorsunuz. İsterseniz bir hakem
heyeti oluşturarak, gönderilen her makalenin belli bir inceleme sürecinden
geçmesini sağlayabiliyorsunuz. Bu süreç tamamiyle isteğe bağlı olarak güncellenebiliyor.

Makaleler hakemlerden geçtikten sonra editörlerinize ulaşıyor. Editörleriniz ise
her adım gibi burada da servis üzerinden yeni bir sayı oluşturarak inceleme sürecini
tamamlamış makaleleri derginin belirlenmiş bölümlerine ekleyip yayınlayabiliyorlar.

Bu proje ile tanışana kadar online dergi, hele de bilimsel dergilerin online inceleme
sürecine fazlasıyla yabancıydım. Hala aşikar sayılmam ancak eskisinden daha iyi
durumda olduğumu düşünüyorum. Bilim dünyasına ne kadar katkı sağlayacağını daha
iyi anlıyorum en azından.


### Amaç ?

OJS'nin temel amacı, bilimsel dergilerin yayınladıkları makalelerin güvenli ve
doğru süreçleri izleyerek yayınlanması ve bilimsel makale kalitesinin artmasıdır.
Şu anda halihazırda dergipark üzerinde bulunan PKPOjs'nin geliştirme sürecindeki
sıkıntıları sebebiyle böyle bir servisi Symfony ile geliştirmek hem kod kalitesini
fazlasıyla arttırdı, hem de performansı yükseltti.

### Neyle ?

OJS alt yapısında PHP 5.2 kullanır. Bunu da en ideal framework olarak gördüğümüz
Symfony2.6 ile yapar. Arama kısmında ElasticSearch kullanır, istatistiksel verileri
MongoDB üzerinde tutar. Veritabanı olarak ise PostgreSQL gibi bir yapıya tutunmuştur.

### Proje

Dediğim gibi projemiz hala geliştirme aşamasında, ancak incelemek isterseniz
[github reposundan](http://github.com/okulbilisim/ojs) çekip bilgisayarınıza
kurarak test edebilirsiniz. Aynı repo üzerinden destek olabilirsiniz ve herhangi
bir hata görürseniz veya bir isteğiniz olursa [issues](https://github.com/okulbilisim/ojs/issues)
kısmından bizimle paylaşabilirsiniz.
