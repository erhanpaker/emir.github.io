---
layout: post
title: Laravel 5 için Paket Geliştirme ve Workbench
description:
category: Laravel 5
comments: true
---

*Önbilgi**: Bu başlık birkaç yazı dizisinden oluşacak. Bir sonraki yazıda paket geliştirirken kullanabileceğimiz, Laravel bağımlı kaynaklardan bahsediyor olacağım.*

Laravel 4’de paket geliştirmek için **workbench** adında öntanımlı olarak gelen bir artisan komutu vardı:

`php artisan workbench vendor/package`

*(Burada vendor/package Packagist için, GitHub kullanıcı adınız/repo adı şeklinde.)*

Bu komut, daha önce config/workbench.php'de belirteceğiniz(!) Email ve Name değerlerini kullanarak ve illuminate/support paketini bağımlılık olarak ekleyerek sizin için bir composer.json, klasör yapısı ve Service Provider sınıfı oluşturuyordu.

Laravel 5'de ise workbench komutu öntanımlı olarak gelmiyor([?](https://twitter.com/taylorotwell/status/556111657898737665)) ama workbench komutunu sağlayan illuminate/workbench paketi Laravel 5 desteği ile güncellenmiş durumda.

**Projemize dahil etmek için,** komut satırından Laravel 5 projemizin kurulu olduğu dizin altında,

`composer require illuminate/workbench --dev`

komutunu çalıştırarak veya elle eklemek istiyorsak: **composer.json** dosyasında require-dev altına,

`"illuminate/workbench": "dev-master"`

satırını ekleyerek, workbench paketini geliştirme ortamı bağımlılığı olarak ekliyoruz.

Ardından **config/app.php**'i açarak **providers** anahtarı altına WorkbenchServiceProvider'ı ekleyerek Laravel'e tanıyoruz.

`'Illuminate\Workbench\WorkbenchServiceProvider'`

Son olarak **config** klasörü altına **workbench.php** dosyası oluşturarak aşağıdaki satırları kopyalıyoruz.

{% gist 9a5a5352695aa45dcf13 %}

Tebrikler artık `php artisan workbench vendor/package` olarak **workbench**'i Laravel 5'de de kullanabiliyoruz.

###Bitirmeden,

Laravel ile paket geliştirmek için Workbench'in oluşturduğu yapıya direk sadık kalmak zorunda değilsiniz. Projenizin herhangi bir yerinde composer paket yapınızı oluşturup, Laravel projenizin composer.json dosyasında psr-4 autoloading altında tanıtarak kullanmaya başlayabilirsiniz. Ve tabiki Laravel'in bağımlıklarını kullanabilmek için illuminate/support ve Service Provider'a ihtiyacınız olacak.