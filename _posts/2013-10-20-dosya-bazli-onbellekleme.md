---
layout: post
title: PHP İle Dosya Bazlı Önbellekleme
date:  20.10.2013
categories: php cache
---

Selamlar,

Basit bir şekilde dosya bazlı önbelleklemeden bahsedeceğim. Eğer salt php kullanmıyorsanız bu işlem için smarty,zend,codeigniter vb şeylerin çok güzel özellikleri var. Ancak php’yi yazarım ben sadece diyorsanız, nasıl html cache yapacağınıza değinelim.

Uygulayacağımız mantık çok basit.

* Girilen adresi öğren
* Girilen adresi md5 e çevir md5(iletisim)
* Dosyalarına bir bak bakalım bu isimde bir dosya var mı ?
* Yok diyorsun madem hemen ob_start diyerek işlemleri not etmeye başla.
* Not ettiğin içeriği bir değişkene atayıp oradan da md5lenmiş ismi olan bir dosyaya yaz.
* Sonrasında içeriği göster.
* Sayfayı yenile
* 1. adıma kadar geldin baktın aynı isimde dosya var.
* O halde zamanı bir kontrol et bakalım ne zaman oluşturulmuş.
* Çok eski bir dosya diyorsan 4 adıma git.
* Dosyamız gayet yeni ise file_get_contents yapıp içeriği alalım.
* Ekrana basıp exit komutunu verelim.

Kodlarla anlatmak gerekirse .


{% highlight php %}
<?php
$request = $_SERVER['REQUEST_URI']; //adım 1
$file_name = md5($request); //adım 2
$file = $_SERVER['DOCUMENT_ROOT'].'/cache/'.$file_name;
 //unutma dosyanın mantıklı bir yerde olması lazım. ve chmod ayarı 777 olsun.
if(is_file($file)){ //adım 3
    (int)$create_time = filectime($file);//adım 9
    (int)$time = time(); //şimdiki zaman adım 9
    $s = $time-$create_time; // bak bakalım adım 9
    if($s >(60*60*5)){//adım 9
        //create new file
        $opened_file = file_get_contents($file); //adım 11
        echo $opened_file;
        echo '';
        exit;//adım 12
    }
}
ob_start(); //adım 4

echo 'Bu kısımda tüm sitemizin içeriğini include falan etmişiz meğersem';

$full_page = ob_get_contents(); //adım 5
$fopen = fopen($file,'w+'); //adım 5
fwrite($fopen,$full_page); //adım 5
echo '';
?>

{% endhighlight %}

İş arasında bu kadar hızlı oluyor ancak.

Saygılar