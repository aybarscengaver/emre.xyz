---
layout: post
title:  "Bir başka Javascript kütüphanesi - Laroux.js"
date:   2014-11-19
categories: javascript kütüphane
---

Javascript ne gelişti arkadaş. Netscape javascript'in bu kadar büyüyeceğini bilseydi başta nasıl hareket ederdi merak ediyorum. 

Gün geçmiyor ki teknoloji ilerlemesin, gün geçmiyor ki yeni bir javascript zaafı giderilmesin. Jquery çıktığı günlerde ne teknolojiydi, coşturmuştu resmen, kolay kullanımı, temiz yazımı ve bilimum artısıyla saf javascript yazmaktan çoğu insanı vazgeçirmiş, frontend developerların vazgeçilmezi olmuştu. Tabi sonrasında çıkan mvc frameworkler jQuery ününe bayağı gölge düşürdüler. Tarayıcıların gelişmesiyle de artık jQuery bir ton eleştiri almaya başladı tabi. Ancak hala baktığınızda iyi bir kullanım oranı var.

Esas konuya gelecek olursak, Eser önderliğinde 2013 başında geliştirilmeye başlayan laroux.js diye bir kütüphane stabil sürüme ulaştı. Şahsi tercih sebebim, jQuery'den daha performanslı çalışması ve [eser](http://eser.ozvataf.com/blog/free-software/laroux-js-tanitim/)`in kendi blogunda belirttiği sebepler oldu.

---
- jQuery’nin her browser’ı ve platformu’u destekleme çabası ile bloatware olmaya başlayan kodu yavaş bir frontend deneyimi yaşatabiliyor. Her browser v8 kullanmıyor ve jQuery 2.0 için dahi Windows 8 gibi JavaScript ile geliştirme yapılabilen platformlar kapsam içerisinde oysa ki yalnızca web’de frontend geliştirmesi için kullanıyorum jQuery’i.
- Yine “2010’dan önce üretilmiş herhangi bir browser’ı desteklemek zorunda değilim” diye düşünen biri olarak modern bir browser’ın native fonksiyonları ile değil jQuery API’si ile konuşmak zorunda kalıyorum.
- Sizzle’ın yaptığı işi modern browser’larda querySelector metodu üstlenebiliyor ama ben bu performansdan iki üç ekstra selector için feragat etmek zorunda kalıyorum.
- JavaScript yazarken jQuery wrapper’ı içinden DOM objesine ulaşmak, DOM objesini jQuery wrapper’a döndürme hem performans kaybı hem de type karmaşası yaşıyorum.
- jQuery idiot-proof tasarlandığı için ne yaptığını bilen bir kişi için başta CSS fonksiyonları olmak üzere inanılmaz fazla constraint kontrolüne sahip. 

---

Bu sebepler haricinde, jQuery kullanımın dom yapısından uzak olarak wrapperlar üzerinden yürüyor olması da ayrı bi olay.

Laroux.js sizi bu gibi sıkıntılardan kurtarıyor. [Kullanım örneklerine](https://larukedi.github.io/laroux.js/) , [performans testlerine](https://larukedi.github.io/laroux.js/benchmarks.html), [wiki sayfalarına](https://github.com/larukedi/laroux.js/wiki) ve [proje sayfasına](https://larukedi.github.io/laroux.js/) giderek daha detaylı bilgiye sahip olabilirsiniz.


Ayrıca projeyi geliştirici olarak desteklemek isterseniz [github reposundan](https://github.com/larukedi/laroux.js) forklayabilirsiniz.

Herhangi bir konuda geliştirme isteğiniz yada farkettiğiniz bugları [github issues](https://github.com/larukedi/laroux.js/issues) üzerinden paylaşırsanız ayrı bir destek olmuş olursunuz.


