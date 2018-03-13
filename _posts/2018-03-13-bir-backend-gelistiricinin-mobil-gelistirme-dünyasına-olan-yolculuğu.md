---
title: Backend'en mobil geliştiriciliğe !
layout: post
description: Okunması gereken tecrübe ...
image: assets/images/bir-backend-gelistiricinin-mobil-gelistirme-dunyasina-olan-yolculugu/bir-backend-gelistiricinin-mobil-gelistirme-dunyasina-olan-yolculugu.jpeg
---

# An unexpected journey
Sanırım yaklaşık on yıldır, çoğunlukla backend olmak üzere birçok proje içerisinde yer aldım. Bunların hemen hemen hepsi .Net platformundaydı. Son iki yıldır ise Python, Nodejs, Angular gibi, Türkiye’de .Net developer’larının çok girmediği mecralara girmeye başladım. Fakat mobil geliştirme deneyimim Windows Mobile’da (CE’den 6.0'a kadar) RS232 ile çalışmak ve web servis tüketmek gibi abidik gubidik işler dışında hiç olmadı.

Şubat 2017 itibari ile işimden ayrılıp Güney Doğu Asya’yı dolaşmaya başladım. Dolaşırken, gönüllülük esasına dayalı bir programa dahil oldum. Çeşitli işletmeler sizin kalacak yer ve yemek ihtiyacınızı karşılıyor, siz de karşılığında elinizden gelen işlerden, işletmeye yarayacak olanlarını yapıyorsunuz. Oldukça makul bir anlaşma.

Tahmin edebileceğiniz gibi, ben de “elimden geliştirmek gelir” diye çıktığım bu yolculukta “a aa ama I can’t mobile” diyemezdim. Genel olarak Codefiction’da paylaştığımız ortak yargılardan biri de budur. Geliştirici olarak önümüze taş da konsa geliştirmemiz gerekir ve “ben x-end geliştiriciyim sadece” demek çok şık bir hareket olmaz.

Ama sorun şu ki, süre kısıtlı, Güney Doğu’da gezilecek ülke çok. Nasıl yapsam nasıl yapsam diye düşünürken, Angular ile bir şeyler karaladığım dönemlerde biraz inceleme fırsatı bulduğum React & React-native (RN) ikilisi geldi aklıma.

Yanıma bir büyücü, bir cüce ve bir priest alarak başladım bu yolculuğa. Bir ay sonunda uygulama büyük oranda tamamlanmış, fonksiyonel olarak kullanılabilir haldeydi. Ve haftanın beş günü, günde dört saat gibi bir sürede oldu bu. Yani iş dünyası saatleriyle on iş günü gibi bir sürede uygulama tamamlandı. Peki neler içeriyordu bu uygulama? Harita, harita üzerinde point’ler, liste (grid), detay ekranı. Başlamak ve öğrenmek için oldukça sade ve eğlenceli bir uygulama.


# Expected Journey

Bu bir yazı dizisi olacak en nihayetinde. Okumakta olduğunuz part-1, genel bilgilendirme, RN’ye üstten bir bakışı içeriyor.

Bunun peşinden gelecek ikinci, belki üçüncü yazımızda birlikte bir uygulama geliştireceğiz. Ve bu arada ben de sizin ilk yolculuğunuzda, yanınızda olmaya çalışacağım (işte şimdi baltalı cüce, benim).

**Kullanıp deneyimleyeceklerimiz :
Bu yazı dizimizde değinmeyeceklerimiz :**

> # React-native (thank you cap obvius)
> #  React-native-maps
> # React-native-tab-view
> # Firebase

**Kullanıp deneyimleyeceklerimiz :
Bu yazı dizimizde değinmeyeceklerimiz :**

> # Node, npm ve React-native kurulumları
> # ReactJs
> # Objective-C ve Java geliştirmeye oranla olan farklılıklar

# Nedir bu React-native, çantasında neler vardır ?


React-native, Facebook tarafından React ürünü üzerine geliştirilen ve biz geliştiricilere Javascript yazarak, native uygulamalar çıkarabilme imkanı veren bir framework’tür kendisi. Instagram, Airbnb, Facebook Messenger gibi uygulamalar RN ile geliştirilmiştir.

RN, WebView’ın içine gömülen ve adeta bir sinsi gibi, bir native gibi takılan web uygulamaları geliştirmek için değildir. RN ile gerçekten native uygulama çıkartırsınız ortaya. Hem IOS hem Android hem de Windows Mobile (Windows tarafından desteği verilmekte) için. Üstüne üstlük, tek bir codebase’iniz olur ve istediğiniz platforma göre çalıştırırsınız. Eklediğiniz yeni özellik (feature), her iki platform için de hazır hale gelmiş olur.

Ayrıca hot reloading gibi güzel bir özellikle gelen RN ile, geliştirme zamanında yaptığınız her değişiklikten sonra uygulamayı refresh etmek yeterli oluyor. Hem de hot reloading, o anki state’i tutarak, bulunduğunuz sayfaya gelirken ki yollarınızdan geçmenizi de engelliyor (default’ta kapalı geliyor).

Bunun yanında, JS’nin interpreted bir dil olması sayesinde, live reload olarak da çalışabiliyorsunuz. Uygulamanız nodemon ile host ediliyormuşçasına, kodda yaptığınız her değişiklikten sonra otomatik olarak güncelleniyor. JS compile edilmediği için son derece hızlı bir şekilde yaptığınız değişikliği görmenize ve test etmenize olanak sağlıyor (default’ta kapalı geliyor).

Benim deneyimlemediğim ama RN’nin sunduğu bir diğer özellik ise, native kodlarınızı da çalıştırabilmeniz. Performans kaygısının ciddi olduğu durumlarda, RN’yi aradan çıkartmak isterseniz tercih edebileceğiniz bir yöntem.

# Vay be, nasıl çalışır ki acep ?

Yukarda da bahsettiğim gibi RN, Cordova ve Ionic gibi hybrid geliştirme imkanı sunan ortamların aksine, günün sonunda native bir uygulama koyar ortaya. Ama bunu, yazdığımız JS’yi native’e compile ederek falan yapmıyor. İçinde barındırdığı JS engine (JavascriptCore) ile native arasında köprü (bridge) kurarak yapıyor. Bu ne demek oluyor? Sen <Text> yazıyorsun; IOS’ta UITextView oluyor, Android’de android.widget.TextView oluyor. Diğer hybrid framework’lerde olduğu gibi bir <span> üretilmiyor.

Bu açıdan, Xamarin ile oldukça ciddi bir benzerlik göze çarpıyor. C# yazıyorum, interpreted bir dile çevriliyor, bu dil ile native kod arası bir bridge kuruluyor. Performans, development hızı gibi konulardaki karşılaştırma deneyimimi Xamarin’i hiç kullanmadığım için paylaşamayacağım ama sadece şu farkı paylaşmak istiyorum: Xamarin’de IDE’den debug edebiliyorken, RN’de Chrome V8 Engine’den veya vscode gibi debugging extension’u da yazılmış herhangi bir texteditor’den yapabiliyorsunuz. Bunu bir avantaj-dezavantaj olarak değil, aralarındaki güzel bir fark olarak paylaşıyorum.

# Var mı dezavantajı ?

JavascriptCore ve native thread’leri arasındaki mesaj sayısının anlık olarak çok yüksek olduğu bir uygulama yazmaya niyetlenirseniz, bottleneck oluşma ihtimali yüksektir. Sonrası ise kilitlenen thread’ler, ölen mesajlar, kullanıcıların telefonlarını duvara fırlatmaları… Ama bu sanırım bir oyun yazmaya kalkıştığımızda karşılaşabileceğimiz bir durum diye düşünüyorum. Yani kullanıcı sürekli input’ta bulunuyor, business kodunuz (JS) çalışarak ekranda render edilmesi için main thread’e gerekli mesajları iletiyor sürekli olarak. Yoksa RN ile yazılmış büyük ölçekli mobil uygulamarı görüyoruz. Oyun da yazmayıverelim arkadaş, değil mi?

Bir de benim de karşılaştığım ve RN kullanıcılarının da sıkça müzdarip olduğu bir problem var:

# Üçüncü parti komponentler (3rd party components)

Open source’un en güzel yanı, bir ürün ortaya çıktıktan sonra, tüm developer’larca geliştirilmeye devam etmesidir belki de. RN’de de durumlar böyle ilerliyor genel olarak. Ama sorun şu ki, FB’nin genel olarak developer’lardan gelen taleplere karşılık vermemesinden kaynaklı, component’ler dışarda geliştirilmeye devam ediyor. Doğal olarak bir RN ile geliştirme yapacak bir developer, FB’nin sunduğu component’leri mi kullanması gerekiyor, yoksa kullanacağı komponent sorunlu mu bilemiyor. E FB’nin sunduklarına muadil olarak yapılanlara da herzaman güvenemiyorsun. Çok hızlı versiyon değiştirebiliyorlar, deprecated olabiliyorlar.

Bunun bir üst level’ı da, FB’nin “arkadaşlar bizdeki komponent’e destek vermiyoruz, gidip şurdan kullanın” diye sizi iyice güvensiz hissettirmesi. Burada bahsettiğim component, map (harita) component’i. Bir mobil uygulama için gayet temel component’lerden biri olan bu map component’i için, Airbnb’nin geliştirdiği react-native-maps’i kullanmanız gerekiyor. Çünkü RN ile gelen map’te Android desteği yok. Şimdi burada, “ee ne var bunda” diyebilirsiniz. Ben olsam ben de derdim. Ama react-native-maps component’inin literatüre “BLANK MAP” olarak geçen bir issue’su var ki… Dillere destan. Hikayeyi okumak ve insanların çaresizlikten kendi aralarında neler yapmaya çalıştığını görmek isterseniz <a href="https://github.com/airbnb/react-native-maps/issues/118" data-href="https://github.com/airbnb/react-native-maps/issues/118" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">şuradan buyurun.</a>


<a href="https://medium.com/codefiction/bir-backend-geli%C5%9Ftiricinin-mobil-geli%C5%9Ftirme-d%C3%BCnyas%C4%B1na-olan-yolculu%C4%9Fu-1-105db01da3d1">***Yazının Kaynağı : Medium - Onur Aykaç***</a>