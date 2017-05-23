---
title: Symfony 4 ve Flex
date: '2017-05-23T11:36:20+00:00'
layout: ''
---


Symfony hakkında yaptığım sunumlarda hep söylediğim gibi, Symfony PHP'nin gelişmesi için her daim çabalamış bir topluluk. Symfony sadece kendisi için birşeyler yapmayıp tüm PHP camiasının faydalanabileceği işler konusunda her zaman bir adım önde giden bir topluluk.

## Symfony 4

Symfony yeni çıkartacağı sürümde bir sürü güzel özelliğin müjdesini vermeye başladı. Symfony 4 Kasım 2017 de stabil olarak sunulacak. Bir önceki sürümde 2.8 versiyonunda projeniz çalışıyor ve hiç deprecated uyarı almıyor idiyseniz çok ufak değişikliklerle tüm projenizi 3.0 versiyonuna taşıyabildiniz. Bu çoğu framework'ün bırakın yapmayı yanına yaklaşamadığı bir sürdürülebilirlik.

Bu sürümde ise 3.4 versiyonda bulunan tüm özellikler, deprecated olmuş özelliklerin temizliği ve programlamaya yeni bir yaklaşımla karşılacaksınız.

Ayrıca Symfony 4.0 yapılan bir oylama sonucu PHP 7 den aşağısını desteklememe kararı aldı.

Symfony 4.0 öncesinde HHVM üzerinde symfony uygulamalarını sorunsuzca çalıştırabiliyorduk, ancak PHP 7'nin müthiş çıkışından sonra HHVM şu anda PHP'den geri kaldığı ve bazı özellikleri desteklemediği için Symfony 4.0 sürümünde HHVM desteği de kaldırılıyor.

Symfony uygulamaları parameters.yml dosyasına bağımlılıktan `symfony/dotenv` sayesinde kurtulup tüm ayarları ortam değişkenlerinde ve/veya .env dosyalarında tutabilecek.

App_dev ve App diye iki dosya ihtiyacı kalkıyor, tek bir başlatıcı (web/index.php) ortam değişkenlerine göre mod değiştirebilecek.

TaskRunner olarak MakeFile kullanılacak.

Yeni klasör yapısında ayarlar `etc/` şablonlar `templates/` klasörü içinde bulunacak.

Ve en önemli bomba

<blockquote><p>"Dağıtımlar hatalı soyutlamalardır"</p></blockquote>

Yani artık symfony standard edition, symfony rest edition tarzı dağıtımlar olmayacak. Çünkü birinde başladığınızda diğerinize geçmeniz pek (hiç) kolay olmuyor. Ya birini, ya diğerini tamamen almanız gerekiyor, yahut tamamen custom birşey yapmanız gerekiyordu.

## Symfony Flex

Ve olan oldu. Flex bir composer eklentisi. Symfony 4.0 sürümünden sonra kullanabileceğimiz Flex ile beraber dağıtımlar kalkacak. Artık Symfony iskeletinde sadece iki bağımlılık olacak `symfony/flex` ve `symfony/framework-bundle`. Geri kalan herşey isteğe bağlı olacak. İlk bakışta işi zorlaştıracak sanabilirsiniz, ancak henüz Flex ne yapacak anlatmadım.

Flex her bağımlılığınızı eklediğinizde yahut kaldırdığınızda, manuel olarak yaptığımız tüm işlemleri (config, routing, AppKernel vs) kendisi çözecek.

Kısaca siz sadece composer require fos/user-bundle dediğinizde, gereken tüm öntanımlı ayarları, routeları ve gidip AppKernel'e eklediğimiz bundle'ı sınıfını vs kendisi yapacak. Müthiş değil mi?

Otomasyonun dibine vuruyor Smyfony 4 ve Flex. Ama nasıl?

Bundle geliştirdiğinizde flex için bir tarif (recipe) dosyası oluşturuyorsunuz. Bu tarifler SensioLabs tarafından kontrol edilecek bir sunucuda (flex.symfony.com) tutuluyor ve ihtiyaç duyulduğunda erişilebiliyor.

Örnek tam tarif aşağıdaki gibi.

```
{
    "bundles": {
        "Symfony\\Bundle\\FrameworkBundle\\FrameworkBundle": ["all"]
    },
    "copy-from-recipe": {
        "etc/": "%ETC_DIR%/",
        "src/": "%SRC_DIR%/",
        "web/": "%WEB_DIR%/"
    },
    "composer-scripts": {
        "make cache-warmup": "script",
        "assets:install --symlink --relative %WEB_DIR%": "symfony-cmd"
    },
    "env": {
        "APP_ENV": "dev",
        "APP_DEBUG": "1",
        "APP_SECRET": "%generate(secret)%"
    },
    "gitignore": [
        ".env",
        "/var/",
        "/vendor/",
        "/web/bundles/"
    ]
}

```

Ufak bir demoyu ise aşağıda görebilirsiniz

<iframe src="https://www.youtube.com/embed/o9N1nOYfAl4" allowfullscreen="" width="560" height="315" frameborder="0"></iframe>

Daha fazla bilgi için [fabpot](https://medium.com/@fabpot)'un medium hesabını kurcalayabilir ve takip edebilirsiniz.