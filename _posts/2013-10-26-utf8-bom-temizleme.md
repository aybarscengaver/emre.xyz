---
layout: post
title: UTF8 Dosyalardan Bom Temizleme
date:  26.10.1013
categories: genel linux
---

Önce tree uygulamasını yükleyin

`apt-get install tree - yum install tree `

Sonra kodu çalıştıracağız

{% highlight bash %}
a=$(tree -if)
for i in $(echo $a | tr " " "\n"); do
	sudo sed -iv '1 s/^\xef\xbb\xbf//' $i;
done
{% endhighlight %}

hadi hayırlı olsun