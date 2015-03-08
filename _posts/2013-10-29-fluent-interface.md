---
layout: post
title: Fluent Interface
date:  29.10.2013
categories: php design-pattern
---

Yazılım geliştirme alanında bir tasarım şablonudur. Basittir, hoştur.

`<?php echo $okul()->sinif()->sira()->ogrenci()->isim() ;?>`
şeklinde kullanılır. Bu güzelliği bizim arka arkaya işlevleri çalıştırmamızı sağlar. Oluşturulması çok kolaydır. Sınıfın her işlevinden sonra sınıfı döndürmeniz yetecektir.

{% highlight php %}
<?php
class Okul(){
    public function Sınıf(){
        $this->sinif="5a"
        return $this;
    }
    public function Ogrenci(){
        $this->ogrenciler=$model->get($this->sinif);
        return $this;
    }
    public function __get($name){
        return $this->ogrenciler[$name];
    }
}
{% endhighlight %}