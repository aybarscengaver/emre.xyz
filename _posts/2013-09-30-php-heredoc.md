---
layout: post
title: PHP Heredoc Sözdizimi
date:  30.09.2013
categories: php
---

PHP de karakter katarlarının kullanımında bilinen şekilde kullanılan 2 tür metin barındırma yöntemi mevcuttur.



{% highlight php %}
<?php
$degisken = “Değişken”;
$metin = “Çift tırnak içerisinde $degisken gönderilebilir.”;
$yeni_metin = ‘Tek tırnak $degisken tarzında tanımlamaları desteklemez.”;
{% endhighlight %}

2 Şekilde kullanım en yaygın kullanımdır. Tüm işlerimizi aslında görmeye yetecek olan bir yöntemdir bunlar. Lakin bazı durumlarda çift tırnak (“) yada tek tırnak (‘) ihtiyacımız çok olur. Bu durumda kaçış karakteri () kullanmamız gerekir. Eğer bunun başka tür bir çözümünü arıyorsanız HereDoc sözdizimi çok satırlı karakter katarlarında imdadınıza yetişecektir.
HereDoc sözdizimi «< karakterleri ile başlar. Herhangi bir karakter katarı eklenir başlangıç mahiyetinde. Alt satırdan itibaren de metnimiz girilir. Son satıra ise «< karakterlerinden sonra girdiğimiz karakter katarı girilip noktalı virgül ile bitirilir.

{% highlight php %}
<?php
$isim = "Emre";
$metin = <<<son
Metnimiz istediği kadar uzun olabilir
HTML karakterleri içerebilir. İsim = $isim şeklinde değişkenler barındılarabilir
Kaç satır yazarsak yazalım PHP yukarıda belirttiğimiz karakter katarını görene kadar 
burayı metin olarak okuyacaktır.
Aynı zamanda bu metin içerisinde tek tırnak içerisinde kullanırken sıkıntı oluşturan 
kaçış karakterleri de kullanılabilir. 
SON;
echo $metin;
{% endhighlight %}

Dikkat etmeniz gereken iki husus. HereDoc başlangıç kısmında kullandığınız kelimenin sadece son da kullanılması gerektiği ve kesinlikle bir tab dahi boşluk bulunmaması gerektiğidir. Yani ;

{% highlight php %}
<?php
$metin = <<<bitis
testasdasd
Bitis;
{% endhighlight %}

Şeklinde bir çalıştırma sonunda  `Parse error: syntax error, unexpected $end in **** ` şeklinde bir hata almanız kaçınılmazdır. Bitiş karakterinin tabsız olarak yazılmış olması gerekmektedir.

Not: Bu kullanım PHP 4 den önceki sürümlerde çalışmaz !