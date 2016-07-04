---
title: Docker - Dinghy
date: '2016-07-04 05:07:00'
layout: post
---
# Dinghy ile Docker
Dinghy codekitchen kişisinin yazdığı, macOs üzerinde Docker kullanmayı daha keyifli hale getiren bir araç.

En sevdiğim tarafı, standart olarak vm providerların dosya paylaşımındaki yavaşlığı ortadan kaldırması. Yani host dediğimiz, kod yazdığımız makinamızdaki dosyaların sürekli olarak vm ile eşleştirilmesi olayı. Bu olay acayip can sıkıcı olabiliyor. Symfony ile development modda bir proje geliştirirken bomboş bir uygulamanın açılması 30–40 saniye sürebiliyordu normal Docker kurulumunda. Bunu aşmak için vmlere NFS desteği eklemek lazımdı. Bu iş bana biraz sancılı geldi açıkcası, tam Docker sevdamdan vazgeçmek üzereyken Dinghy ile karşılaştım. Hiç bir ayarla uğraşmama gerek kalmadan gayet hızlı çalışan bir enviroment sahibi oluverdim.

Diğer bir güzel tarafı dosyalarda yaptığınız değişiklikler, normal şartlarda bazen yakalanamayabiliyor. Bu da dosyanızın vm ile eşleştirilmeyeceği anlamına geliyor. Tabi ki bir sürü stabil çözümü var. Örneğin Dinghy kullanmadığımda atıl duran bir bilgisayara coreOs kurup `rsync` ve `fsevents` ile dosya eşleştirme olayını hızlıca çözmüştüm. Tabi bunu ayarlamak falan baya işti. Bu işi de ortadan kaldırdı Dinghy.

Benim pek kullanmadığım bir diğer artısı da, içerisinde bir DNS ve Http-Proxy ile beraber gelmesi. Bu sayede `<servisid>.<projeid>.docker` gibi bir url ile direk container içindeki servise ulaşmanızı sağlıyor. Ama bunu hala kendim ayarlamayı tercih ediyorum nedense. Siz de kullanmak istemezseniz `vim ~/.dinghy/preferences.yml` dosyasına biz göz atın.

### Kullanım
Dinghy direk `brew` ile kurulabiliyor. Önşartlar: bilgisayarınızda Docker ve Docker Toolbox kurulu olmalı. DockerMachine için bir vm provider bulunmalı. Virtualbox, vmware, parallels veya xhyve olabilir. Ben xhyve tercih ettim. Daha küçük daha tatlış.

İlk olarak `brew tap codekitchen/dinghy` tap ı brew`e tanıtmak lazım. Ardından `brew install dinghy` diyerek yüklenebiliyor.

Yükleme tamamlandıktan sonra :

````
dinghy create —-provider xhyve
```

diyerek bir vm oluşturmanız gerekiyor. Sonrasında `docker run -it redis` diyerek container’ı başlatabilirsiniz.
Ayrıca docker-compose kullanıyorsanız, hiç bir fark olmadan kullanmaya devam edebilirsiniz. `docker-machine env machinename` kullanımı yerine `dinghy env` dediğinizde tüm docker değişkenleri export edilebiliyor.

Detaylı dökümantasyonu [github reposu](https://github.com/codekitchen/dinghy)ndan ulaşılabilir durumda.
