---
layout: post
title: Github URL Kısaltma Servisi
date:  14.09.2013
categories: github genel servis 
---



Github’ın bu ayın 10′unda başlattığı bir servisten bahsetmek istiyorum. GitHub ShortURL

**Nedir ?**

İsminden de anlaşılabileceği gibi bir adres kısaltma servisidir. Fakat bu servis bir arayüz ile desteklenmiyor. Kullanabilmek için Curl ile işlem yapmak gerekiyor.

**Nasıl Kullanılır ?**

`curl -i [http://git.io](http://git.io)-F "url=https://github.com/..."`

Komut satırınızından url değeri olarak göndereceğiniz adres size şöyle bir sonuç verecek :

	HTTP/1.1 100 Continue
	HTTP/1.1 201 Created
	Server: nginx/1.0.4
	X-Node: gitio3
	X-Sha: 1e46433578b8b8979a831867afc9e1b4650353a1
	Content-Type: text/html;charset=utf-8
	Date: Sun, 13 Nov 2011 22:21:00 GMT
	Status: 201 Created
	**Location: [http://git.io/lazMnQ](http://git.io/lazMnQ)**
	X-Runtime: 0.008073
	Connection: keep-alive
	Content-Length: 0

Location kısmındaki adresi kısaltımış adrestir.

**Neye Yarar ?**

Tabiki uygulama geliştirirken kullanılmanız için yapılmış bir hizmettir.
