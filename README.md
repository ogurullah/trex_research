# trex_research
***
#### *Programlama hakkında öğretici ve temel bir araştırma raporu.*
***

## 1. Modern Yazılım Geliştirme Pratikleri

<details>
<summary>Git nedir? GitHub nedir?</summary>
    
* Kısaca açıklamak gerekirse, Git bir versiyon kontrol sistemidir. Ancak Git'i bu şekilde açıklamak tabiri caizse hakkını yemek olur. Git, diğer versiyon kontrol sistemlerine kıyasla (CVS, Subversion, Perforce vb.) dosyaları çok farklı bir şekilde ele alır. Bu vizyoner tavrı sayesinde Git, günümüzde yazılımcıların vazgeçilmezi olmuştur.
* Git'in dosyaları ele alma sisteminden bahsetmek gerekirse, diğer versiyon kontrol sistemleri dosyaları bir bütün olarak ele alırken, Git dosyaların adeta neye benzediğini kaydeder , bir nevi fotoğrafını çeker, ve böylelikle her işlemde dosyaları oradan oraya taşımak yerine yalnızca son değişiklikleri birbiriyle kıyaslayarak veri tabanına alır. Yalnız bu 'fotoğraflar' şüphelenebileceği gibi veri kayıpları olabilecek bir şekilde çalışmazlar. Git, kullandığı bir algoritma sayesinde dosyaların içeriklerinden 40 karakterlik bir string oluşturur. Bu sisteme SHA-1 hash adı verilir. Git, dosyaları bu hash string'leri kullanarak kıyaslar. Bu sayede Git hem her versiyonda bütün dosya değişiklikleri yapmayarak depolama alanından ve veri aktarımından tasarruf etmiş olur, hem de bu akıllı mekanizması sayesinde kendisinin haberi olmayan herhangi bir dosya değişikliği, silinmesi vb., yapılmasına izin vermez. Kısaca Git, dosyaların her versiyonunu kaydetmez ancak dosyaların her versiyonuna erişim sağlayabilir çünkü dosyalarda yapılan değişiklikleri kaydeder.
* Örnek bir SHA-1 hash string'i:
    * `24b9da6552252987aa493b52f8696cd6d3b00373`
* GitHub bir Git sunucusudur. Git ile depolanmış kodların host'lanabildiği bir uzak bilgisayar, bir nevi buluttur. GitLab, Gitea, Bitbucket, Gogs gibi farklı Git sunucuları da mevcuttur. Şu anda yazılımcılar arasında en popüler olanı GitHub'dır.

</details>

<details>
<summary`>Temel Git komutları: init, clone, add, commit, push, pull, branch, merge</summary>

* **`init`**: Boş bir Git repository'si oluşturur. Repository, Git'in üzerinde versiyon kontrolü yapacağı klasörlere verilen addır.
    * `cd Desktop` Masaüstüne gittim.
    * `mkdir trex_research` 'trex_research' adlı bir klasör oluşturdum.
    * `git init` 'trex_research' adında bir Git repository'si oluşturdum.
    * `ls` Şu anda klasör boş.
* README.md dosyasını manuel bir şekilde oluşturdum. Markdown dosyasını JupyterLab kullanarak düzenledim.
* **`add`**: Modified stage'de olan bir dosyayı, staged olmak üzere, gelecek commit'e ekler.
    * `git add README.md` 'README.md' Markdown dosyamı bir sonraki commit'e eklemek için işaretledim.
* *Git sisteminde modified, staged ve committed olmak üzere üç dosya türü vardır. Modified, Git'in local veritabanından farklı olan, üzerinde değişiklik yapılmış dosyalardır. Staged, bir sonraki commit'e eklenmek üzere add komutu ile işaretlenmiş dosyalardır. Committed, commit komutu ile yerel veritabanına eklenmiş dosyalardır.*
* **`commit`**: 'add' komutu ile eklenmiş, staged duruma gelmiş, bütün dosyaları committed duruma getirir yani yerel veritabanına ekler. Dosyaları 'push' komutu ile sunucuya yüklenmek üzere adeta paketler ve etiketler.
    * `git commit -m "paket mesajı"` Staged duruma getirdiğim bütün dosyalarımı (yalnızca 'README.md') bir sonraki 'push'ta GitHub'a yüklemek için paketledim, yerel veritabanına kaydettim.
    * Eğer '-m' ve beraberinde bir paket mesajı kullanmazsak Git bizi Vim veya Nano gibi bir text editor'e yönlendirir. Ben bunun yerine mesajımı '-m' kullanarak tek komutta eklemeyi tercih ediyorum.
* **`push`**: Sunucuya yüklenmek üzere paketlenmiş yerel veritabanındaki bütün değişiklikleri sunucuya gönderir.
    * `git push` 'README.md' dosyasını GitHub'a yükledim.
* **`fetch`**: Sunucudaki versiyon ile yerel veritabanındaki versiyonu kıyaslar, sunucudaki güncelse değişiklikleri alır.
    * `git fetch` Sunucudaki 'README.md' ile yerel aynı.
* **`merge`**: 'fetch' ile aldığı değişiklikleri yerel dosyalarla birleştirir. Branch'ları birleştirmek için de kullanılır.
    * `git merge` Already up to date.
* **`pull`**: 'fetch' ve sonrasında 'merge' uygular.
    * `git pull` Already up to date.
* **`branch`**: Var olan versiyonun ikisi birbiriyle çakışmayan bir klonunu üretir. Bir nevi paralel evren gibi çalışır. Başka branch'taki değişiklikler ana branch'i etkilemez.
    * `git branch test` 'test' adında bir branch oluşturur.
    * `git branch` '* main' ve 'test' olmak üzere iki branch görünüyor. '* main' şu anda main branch'teyiz demek.
* **`checkout`**: branch'lar arası geçiş yapmayı sağlar.
    * `git checkout test` main branch'tan çıkar ve test adındaki branch'a girer.
    * `git branch` 'main' ve '* test' olmak üzere iki branch görünüyor. Şu anda test'teyiz.
    * Burada yapacağımız bütün 'add', 'commit', 'push' işlemleri test branch'ın içerisinde olacak.
* **`stash`**: Değişiklik yapılmış dosyaları daha sonra geri dönebilmek üzere kenara atar. 'pull' yapıp yine de lokal değişiklikleri yitirmemeye yarar.
    * `git stash`: Henüz commit'lenmemiş ama 'add'lenmiş değişiklikleri kenara attım.
    * `git pull`: Sunucudaki güncel değişiklikleri çektim.
    * `git add README.md`: Dosyada değişiklik yaptım ve commit yapmak üzere paketledim.
    * `git commit -m "stash test"`: Paketim göndermeye hazır.
    * `git push`: Değişiklikleri sunucuya gönderdim.
    * `git stash pop`: Kenara atmış olduğum değişiklikleri elimdeki dosyalara uyguladım.
</details>

<details>
<summary>Merge conflict nedir, nasıl çözülür?</summary>

* Merge conflict, iki branch'ın 'merge'lenirken bir dosyanın aynı yerinde farklı değişiklikler yapılmış olmasından kaynaklanan 'merge'lenememe durumudur. Git, aynı yerde birbirinden farklı iki değişikliği nasıl ele alması gerektiğini bilemez ve hata verir. Dosyada çakışan bölge(ler),
    * `<<<<<<<HEAD` ve `=======`
* arasında gösterilir. Bu kısımda hangi versiyonun kabul edileceği yazılımcı tarafından manuel şekilde belirlenir ve ancak böyle 'merge' işlemi gerçekleşebilir.
</details>

<details>
<summary>CI/CD nedir? Azure DevOps, GitHub Actions ile pipeline örnekleri</summary>

* **CI (Continuous Integration)**: CI basitçe kodunuzu sıklıkla ortak branch'e yüklemek, kendi kodunuzu da ortak kodu da güncel tutmak demektir. Yazılımcılar kodlarını kendi local branch'lerinde tutma eğilimi gösterebilirler. Bu prensip, bu duruma karşı olarak yazılımcıların kodlarını sıklıkla paylaşmaları gerektiğini söyler.
* **CD (Continuous Delivery)**: CD, otomatik testler vb. kullanarak değişiklik yaptığınız kodunuzu da daima 'deployable' yani yayımlanabilir bir durumda tutma prensibidir.
* CI/CD pipeline dediğimiz şey basitçe bir yazılımcı ortak branch'e bir kod yüklediği zaman kodun otomatik şekilde yayımlanana kadar geçtiği adımlardır. Ortak branch'e bir kod yüklendiğinde, bu kodu önceden belirlenmiş testlere otomatik bir şekilde sokup, daha sonra projeyi otomatik bir şekilde build'leyip, süreç içerisinde herhangi bir sorun çıkmazsa da otomatik bir şekilde yayımlanmasına yarar. Çıkan bir sorunda da işlem durur ve ilgili yazılımcıya bildirim gider.
* Ortak branch'e her güncelleme geldiği zaman manuel bir şekilde kodları birleştirip test etmek ve yayımlamak insan hatalarına izin veren, yavaş ve verimsiz bir yöntem olduğu için pipeline çok kullanışlıdır.
* Basit bir GitHub Actions pipeline örneği: `trex_research/.github/workflows/hello-world.yml`
    * <pre> name: Basit Pipeline
        on: [push]
        jobs:
          hello-job:
            runs-on: ubuntu-latest
            steps:
              - name: Merhaba Dünya Yaz
                run: echo "Merhaba, dünya!"</pre>
    * Bu oldukça basit bir pipeline örneğidir. Tanımda anlatıldığı gibi otomatik test uygulama ve program deploy'lama işlevi yok ancak yeni kod geldiğinde GitHub'da repository'nin içindeki Actions terminalinde "Merhaba dünya!" yazıyor.
    * CI/CD kavramı bir .NET projesinde tıpkı diğer alanlarda kullanıldığı gibi kullanılabilir. Projeye yapılan katkılar otomatik testlerden geçip otomatik build'lenerek yine otomatik bir şekilde deploy'lanabilir.
</details>

<details>
<summary>Software Development Life Cycle (SDLC)</summary>

* Yazılım geliştirme sürecinin aşamaları, kaynaktan kaynağa değişmekle birlikte 6-7 adımdan oluşur.
    * **1.) Adım: Planlama**: Projenin büyüklüğü, kapsamlılığı, karmaşıklığı, içeriği, gereksinimleri, hedefleri ve özellikle neye ihtiyacının *olmadığı* bu aşamada belirlenir.
        * İlerleyen zamanlarda 'feature-creep' yaşamamak için projenin çapı daha ilk aşamadan belirlenmelidir.
    * **2.) Adım: Analiz ve Gereksinim Oluşturma**: Bu aşamada projenin özellikleri belirlenir. Bir yazılım projesinde yazılım gereksinimlerini (SR - Software Requirements) doğru oluşturmak çok önemlidir. Projenin geliştirilme sürecinin neredeyse tamamına yön verecek kritik bir aşamadır. Eğer proje çapı birinci aşamada tutarlı belirlendiyse ve bu aşamada çapa yönelik gereksinimler isabetli ve verimli şekilde oluşturulduysa bu projenin programlama süreci görece rahat geçecektir.
    * **3.) Adım: Mimari Dizaynı**: Bu aşamada projenin kodlarının mimarisi belirlenir. Arayüz tasarımları yapılır. Amaca en uygun yöntemler kullanılmak üzere seçilir. Aynı zamanda bu aşamada projenin siber güvenliği de düşünülebilir.
    * **4.) Adım: Kodlama**: Bu aşamada önceki adımlarda oluşturulmuş özellikler, fonksiyonlar, planlar ve kurallar uygulanarak proje kodlanır. Kullanılacak uygun yazılım dilleri seçilir, kodlar oluşturulur.
    * **5.) Adım: Testler**: Bu aşamada yazılmış olan kodların ekstrem noktaları, güvenlik açıkları, entegrasyonları, fonksiyonları, hepsi tek tek test edilir. Bu aşamadan önce hiç test uygulanmadığı düşünülmesin, bu aşamaya kadar küçük testler hep uygulanır ancak bu aşamada her şeyin kapsamlı testleri yazılır ve olabildiğince bug'sız bir program oluşturulmaya çalışılır.
    * **6.) Adım: Yayımlama**: Bu aşamada program adım adım yayımlanmaya başlar. Önce 'beta' diye adlandırılan, programın sınırla sayıda kullanıcıya ulaştırıldığı bir aşamaya girilir ve programın genel kullanıcı kullandığında nasıl bir deneyim sunduğu gözlemlenir. Gözden kaçmış pürüzler bu aşamada toparlanır ve ardından program yayımlanır.
    * **7.) Adım: Bakım**: Artık programın zaman içerisinde tespit edilememiş, mümkün olduğunca az, bug'ları ortaya çıkmaya başlar. Onları düzeltmek, programı değişen ihtiyaçlara göre güncellemek, destek vermek, bu aşamanın işidir. DevOps (development-IT operation) takımları bu aşamada CI/CD kullanarak programı günceller ve düzeltir.
* Bir yazılımcının sadece kod yazmaktan çok daha fazlasını bilmesi gerektiği bu anlatılan adımlardan aşikardır. Bir yazılımcı bu süreçte proje maliyeti hesaplama, kullanıcı isteklerini öğrenme, dil hakimiyeti ve hangi durumda hangi dilin kullanılması gerektiği hakkında tecrübe vb. çeşitli kabiliyetlere ihtiyaç duyar. Yazılım geliştirme sürecinde her aşamada yazılımcının rolü çok büyüktür.
</details>

## 2. .NET Ekosistemi

<details>
<summary>.NET Nedir? Tarihçesi, amacı, neden kullanılır?</summary>

* *.NET Tarihçesi*:
    * 90'ların sonunda Microsoft .NET platformunun ilk adımlarını attı. 2000 yılında C# yazılım dili duyuruldu. .NET Framework ve C#, .NET platformunu oluşturdu. 2014 yılında Microsoft, .NET Core'u duyurdu. .NET Framework'ün aksine açık kaynak kodlu, platformlar arası çalışabilen .NET Core ile beraber Microsoft, geçmiş kütüphaneleri de açık kaynak kodluya çevirdi. Bu platformun gelecekteki bütün .NET platformlarının temeli olacağı öne sürüldü. 2016'da .NET Core 1.0 ve Visual Studio Update 3 çıktı ve .NET Core'da yazılım geliştirme başladı. 2017'de .NET Core 2.0, Visual Studio 2017 15.3, ASP.NET Core 2.0 ve Entity Framework Core 2.0 çıktı. 2018'de önce .NET Core 2.1 ve Aralık ayında .NET Core 2.2 çıktı. 2019'da .NET Core 3 çıktı. .NET Core 3, Windows masaüstü uygulaması geliştirmeye olanak sağlıyordu ayrıca olağanüstü performans geliştirmeleri ve ek kütüphanelerle geliyordu. 2020'de .NET 5.0 çıktı. İsimden 'core' ibaresi kaldırıldı ve 4.0 versiyon sayısı atlandı. 2021'de .NET 6.0, 2022'de .NET 7.0, 2023'te .NET 8.0 ve 2024'te son versiyon olan .NET 9.0 çıktı.
    * Büyük versiyon geçişleri geçmiş API'ları bozuyorken küçük güncellemeler hata düzeltmeleri, ek kütüphaneler ve performans geliştirmelerinden oluşuyordu.
</details>

<details>
<summary>.NET Framework, .NET Core ve .NET 7/8+ farkları:</summary>
    
|Özellik| .NET Framework   | .NET Core | .NET 7/8+  |
|:-----------------:|:-----------------:|:-----------------:|:-----------------:|
|Platform desteği|Yalnızca Windows'ta çalışır|Platformlar arası çalışır(Linux,Windows,Mac vb.)|Platformlar arası çalışır|
|Güncellemeler|Güncelleme almaz|Güncelleme almaz|Güncelleme almaya devam eder|
|Kaynak kodu|Açık kaynak kodlu değil|Açık kaynak kodlu|Açık kaynak kodlu|
|Desteklediği araçlar|Visual Studio|Visual Studio, VS Code, CLI araçları|Visual Studio, VS Code, CLI araçları|
|Kullanım alanları|Eski Windows uygulamaları|Çoklu platform uygulamaları, Web, API, Mikroservis|Modern çoklu platform uygulamaları, Bulut, Web API ve dahası|
|Performans|Kıyasla düşük|Ortalama|En iyi performans|
</details>

<details>
<summary>Senkron ve Asenkron Programlama</summary>

* async, await, Task, Configureawait gibi anahtar kavramlar:
    * **async**: Kendinden sonraki kodun çalışması için işini bitirmesi gerekmeyen kod bloklarında kullanılır. *Aynı anda* birden fazla iş yapmak için kullanılır. Örneğin, programda kullanıcı ile alakasız ama yapılması gereken bir iş varsa, bu işi kullanıcı deneyimini hiç etkilemeden, arkaplanda, halletmek için **async** kullanılabilir.
    * **await**: Bitmesi uzun sürmesi beklenen kodlardan önce kullanılır. Yazılım diline bu işin bitmesini beklerken diğer satırlarla ilgilenmesi gerektiğini ama bu iş bittiğinde buraya geri döneceğini söyler.
    * **Task**: **await** ile birlikte çağırılacak **async** işi belirtir.
    * **Configureawait**: Varsayılan olarak açık gelir. *.Configureawait(false)* diyerek kapatılabilir. Bir görev bittiğinde başladığı akışa (thread) geri dönmesi anlamına gelir. Kullanıcı arayüzü uygulamalarında kapatılmamasına özen gösterilmelidir zira kullanıcı arayüzleri akış değiştirerek çalışamazlar. Kütüphane kodlarında kapatılması mantıklı olabilir.
 
* Senkron, Asenkron örnek senaryo açıklamaları:
    * HTTP çağrıları, Web API çağrıları vb. bekleme gerektirebilen işlemlerdir. Geleneksel senkron programlama ile bu işlemleri yapmaya çalışmak, lokal bilgisayarın elinde olmayan bir bekleme oluşturacağı için, kullanıcı deneyimi ve zaman verimliliği bakımlarından epey mantıksızdır. Kullanıcı, arkaplanda veri çağrıları yapılmışken başka işlerle ilgilenebilmek ister. Neticede, hiçbirimiz evde bulaşık makinesi çalışıyor diye donup kalmıyoruz, makinenin işini bitirmesini beklerken başka işlerle uğraşıyoruz. Bu şekilde bekleme gerektirebilen işlemleri senkron programlama ile çağırmak aynı bulaşık makinesinin işini bitirmesini oturup beklemek kadar mantıksızdır. Asenkron programlama sayesinde kullanıcı, çağırdığı bir verinin gelmesini beklerken, programın başka bir yerinde başka bir işlem yaparak kendisine epey zaman kazandırabilir.
</details>

<details>
<summary> dotnet --info çıktısı ve yorumlama:</summary>
    
    ```
    .NET SDK:
     Version:           8.0.412
     Commit:            819e1a9566
     Workload version:  8.0.400-manifests.9cf71931
     MSBuild version:   17.11.31+933b72e36
    
    Runtime Environment:
     OS Name:     Mac OS X
     OS Version:  15.6
     OS Platform: Darwin
     RID:         osx-arm64
     Base Path:   /usr/local/share/dotnet/sdk/8.0.412/
    
    .NET workloads installed:
    Configured to use loose manifests when installing new manifests.
    There are no installed workloads to display.
    
    Host:
      Version:      8.0.18
      Architecture: arm64
      Commit:       ef853a7105
    
    .NET SDKs installed:
      8.0.412 [/usr/local/share/dotnet/sdk]
    
    .NET runtimes installed:
      Microsoft.AspNetCore.App 8.0.18 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
      Microsoft.NETCore.App 8.0.18 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
    
    Other architectures found:
      None
    
    Environment variables:
      Not set
    
    global.json file:
      Not found
    
    Learn more:
      https://aka.ms/dotnet/info
    
    Download .NET:
      https://aka.ms/dotnet/download
    ```
    
* .NET 8.0.412 versiyonu kurulu. arm64 mimarili işlemcide Mac OS işletim sistemi üzerinde çalışıyor. Henüz workload yüklenmemiş.
</details>

<details>
<summary>arrow function (=>) ifadesinin C#'taki yeri:</summary>

* Tek satırda fonksiyon tanımlama:
      ```
      static int Multiply(int x, int y) => x * y;
      ```
* Lambda ifadesi:
      ```
      Func<int, int> square = n => n * n;
      ```
</details>

## 3. Backend Geliştirme Temelleri

<details>
<summary>Backend nedir? Frontend ile farkları</summary>

* **Backend**, bir yazılım programının, sunucu tarafında çalışan, mantık ve veri işlemlerinin halledildiği katmandır. Çeşitli sebeplerden dolayı, çalışması beklenen servisin işlem ve veri depolama kısımları kullanıcı ile paylaşılmaz. Güvenlik ve verimlilik, bu sebeplere örnektir. Kullanıcının eline geçmemesi gereken veriler, örneğin diğer kullanıcıların şifreleri vb., Backend'de yer alır. Kullanıcının bilgisayarıyla sürekli iletişim halinde olmak verimsiz olacağı için de bütün işlemler Backend'de görülüp Frontend'e genellikle sadece ham sonuç verileri gönderilir.

* **Frontend** ise aynı programın kullanıcı ile etkileşime geçen kısmıdır. Kullanıcı arayüzü, sunucuya veri gönderecek ve sunucudan gelen verileri düzenleyip gösterecek fonksiyonlar Frontend'de yer alır. Frontend yazılım işi olduğu kadar tasarım işidir de. Kullanıcıların bugüne dek alışmış olduğu belirli kurallara, estetik oranlarına, görsel iletişime uygun kurallı bir site tasarımı yapmak o siteyi kodlamak kadar zordur. Frontend'in ve Backend'in ikisinin de başarılı olmadığı bir senaryoda projenin kalitesi kullanıcı tarafından hissedilemez. Örneğin, güzel görünen ama çok yavaş çalışan bir site ya da hızlı çalışan ama butonları bulmakta zorlanılan bir site kullanıcı için hiç iyi bir deneyim sunmaz. İki katmanın da eş kalifiye elemanlar tarafından hazırlanması oldukça önemlidir.
</details>

<details>
<summary>Web sunucusu nedir? API nedir? API türleri</summary>

* **Web sunucusu**: Web sunucusu kısaca internete bağlı bir bilgisayardır. İçerisinde ilgili web sitesinin gerektirdiği yazılımlar bulunur. Birçok kullanıcının kullandığı tarayıcı HTTP protokolü kullanır ve bu tarayıcılara hitap etmesi için birçok web sunucusu HTTP yazılımı bulundurur. Sunucu, ilgili web sitesinin medya içeriklerini ve kodlarını depolar. Bu içerikleri kullanıcıya iki farklı şekilde gönderir, statik web sunucusu ve dinamik web sunucusu.
    * **Statik Web Sunucusu**: Statik web sunucusu, ilgili dosyaları kullanıcının tarayıcısına olduğu haliyle gönderir.
    * **Dinamik Web Sunucusu**: Dinamik web sunucusu, ilgili dosyalar ve HTTP yazılımının yanında ek yazılımlar da bulundurur. Kullanıcıya göndereceği dosyaları seçen yazılımlar, veri tabanları bunlara örnektir. Kullanıcıya göndereceği dosyaları göndermeden önce günceller ve ondan sonra gönderir.
 
* **API**: API (Application Programming Interface), farklı yazılımların iletişim kurmasını sağlayan bir arayüzdür. Çoğu zaman başkasının yazdığı bir programa erişim sağlar ve eğer kaynak kodları kapalıysa kontrolü elimizde değildir ama önceden belirlenmiş kurallara göre ona veri gönderebilir ve yanıt alabiliriz. Açık kaynak kodlu ya da bizim geliştirdiğimiz bir API'ın her detayını değiştirmek de elimizdedir. Herhangi bir yazılım API sağlayabilir. Bir işletim sistemi de, bir internet sitesi de, bir veritabanı da API sağlayabilir. Basitçe anlatmak gerekirse API, yazdığımız kodla başka bir kodun arasında veri akışı sağlayan bir köprü görevi görür.

* **API Örnekleri**:
    * **Evrensel Kayıt Ekranları**: Üyelik gerektiren bir uygulamaya giriş yaparken Google, Facebook vb. platformlarda zaten var olan bir hesabı bağlama yoluyla hesap açma yöntemi API'lara oldukça iyi bir örnektir. Uygulamalar, ilgili platformun sunduğu API sayesinde oraya hesap bilgisi gönderebilir ve alabilir.
    * **Sitelere Gömülü Youtube Videoları**: Bazı web sitelerinde otomatik oynatılabilen videolar olduğunu görmüşsünüzdür. Bunlardan bazıları gerçekten büyük boyutlu videolar olabiliyorlar, buna rağmen site açıldığı gibi direkt oynamaya başlayabiliyorlar. Bunun olmasına olanak sağlayan şey Youtube'un sağladığı API'dır. Youtube'da zaten yüklü olan videoların web sitelerinde oynatılabilmesini sağlar.
</details>

<details>
<summary>HTTP nedir? HTTP metodları: GET, POST, PUT, DELETE</summary>

* **HTTP**: HTTP (Hypertext Transfer Protocol), istemciler ve web sunucular arasında bilgi aktarmak için kullanılır. İnternetin temel yapıtaşlarından birisidir. Birçok tarayıcı ve internet sitesi HTTP protokolünü kullanır. Genelde kullanıcı bilgisayarından gelen talepler (request) ve onlara sunucudan gönderilen cevaplar (response) yoluyla çalışır.
* **GET, POST, PUT, DELETE** gibi yapılmak istenen işlemi belirten çeşitli metodlarla çalışır.
* Verilerin şifreli bir biçimde gönderildiği bir versiyonu (HTTPS) de mevcuttur.

* **HTTP Metodları**: Sunucuya yapılmak istenen işlem hakkında bilgi verir.
    * **`GET`**: Sunucudan ham veri talebinde bulunur. Fotoğraf indirme işlemleri buna örnektir.
    * **`POST`**: Sunucuya ham veri gönderme talebinde bulunur. Dosya yükleme işlemleri buna örnektir.
    * **`PUT`**: Var olan bir veriyi düzenleme, yoksa oluşturma talebinde bulunur. Profil düzenleme buna örnektir.
    * **`DELETE`**: Var olan bir veriyi silme talebi gönderir. Profil resmi kaldırmak buna örnektir.

</details>

<details>
<summary>RESTful servislerin çalışma mantığı</summary>
    
* **REST**: Sunucu ile istemciyi birbirinden modüler olarak ayıran genel kodlama prensiplerine denir. REST prensipleri dikkate alınarak kodlanmış web servislerinde istemcide sunucu etkilenmeden sunucuda da istemci etkilenmek değişiklik yapmak mümkündür, birbirlerine iletecekleri verilerin formatları değişmesin yeter.
    * REST prensipleriyle yazılmış web servislerinde ve istemcilerinde 'state' sistemi yoktur. İstemciler ve sunucular birbirlerinin hangi durumda oldukları hakkında haberdar değillerdir. Birbirlerine gönderdikleri bütün verileri her durumda her şekilde anlayabilirler. Bu kısıtlamanın sebebi kaynakları olabildiğince verimli kullanmaktır çünkü web'te iletişim hızı bir bilgisayarın kendi içindeki iletişim hızına kıyasla çok yavaştır.
    * REST mimarisinde istemci sunucuya çeşitli talepler gönderir ve sunucu bu taleplere yönelik cevaplar verir.
        * *HTTP metodları buna örnektir*.
</details>

<details>
<summary>JSON veri formatı ve kullanım amacı</summary>

* **JSON nedir?**: JSON (JavaScript Object Notation), JavaScript'ten türemiş, anahtar-değer eşleşmesi kaydeden bir metin depolama formatıdır. İç içe kategorizasyonu destekler. Okunabilir ve ayrıştırılabilir bir formattadır. Bu sayede yazılımlar ve bilgisayarlar arasında veri aktarımı için kullanılabilir.
* JSON'un tek işlevi veri tutmaktır, içerisinde kod bulundurmaz. Uygun veri formatları şunlardır:
    * `string, number, boolean, null, array, object`
* Formatı örnekte görüldüğü gibidir:
    ```
    {
      "name": "Oguz",
      "age": 19,
      "skills": ["Python", "C"],
      "isStudent": true
    }
    ```
</details>

<details>
<summary>SOAP ve GraphQL nedir, REST’ten farkları</summary>

* **SOAP**: SOAP (Simple Object Access Protocol), yalnızca XML formatında çalışan bir iletişim protokolüdür. Web servisleri ve API'ları arasında kullanılır. HTTP ve SMTP protokolleri üzerinde çalışır. Kendine has sıkı bir formatı vardır ve değiştirilemez.
    * SOAP servisleri, WSDL (Web Services Description Language) ile tanımlanır. Bu sayede istemci ile sunucu arasında nasıl iletişim kurulacağı detaylı bir şekilde anlatılır. SOAP'ın uzmanlık alanı hız, verimlilik vb. değil, güvenlik ve güvenilirliktir.

* **GraphQL**: GraphQL, JSON formatında çıktı veren, veriyi tanımlı kaynaklardan esnek bir şekilde toplayıp istemcinin beklediği mimaride gönderebilen bir sorgu dilidir. İstemciye sadece istediği verileri verebilir ve gereksiz veri akışını önlemeye yarar. HTTP protokolü üzerinde çalışır. Veri, istemcinin beklediği yapıda döner.

|Özellik| REST   | SOAP | GraphQL |
|:-----------------:|:-----------------:|:-----------------:|:-----------------:|
|Nedir?|Mimari stili|İletişim protokolü|Sorgu dili |
|Format|JSON,XML|XML|JSON|
|Esneklik|Belli başlı kuralları var|Oldukça sıkı kuralları var|İstemciye göre|
|Özellik|Pratik ve yaygın|Güvenilir|Esnek, istemciye göre|
</details>

## 4. ASP.NET

<details>
<summary>ASP.NET ve ASP.NET Core nedir? Avantajları, farkları</summary>

* **ASP.NET**: ASP.NET, .NET çatısı altında yer alan bir web geliştirme platformdur. Web uygulamaları, web siteleri ve web servisleri geliştirmeye yarar. Dinamik web sayfaları üretmeye olanak sağlar. Sunucu tarafı (backend) C# ile yazılabilir. Bu sayede işlemler hızlı ve güvenli şekilde çalışır. Kullanıcı yüzü ise (frontend) HTML, CSS, Javascript ile yazılır. Güncel frontend yazılımları da, -Blazor, React, Angular vb.- kullanılabilir.
* **ASP.NET Core**: ASP.NET'in çok daha gelişmiş ve performanslı bir versiyonudur. Açık kaynak kodlu ve çoklu platform desteklidir. REST API'lar yazmaya olanak sağlar. OpenAI ve Azure ile yapay zeka destekli web uygulamaları üretmeye olanak sağlar. ASP.NET artık güncelleme almıyor fakat ASP.NET onun devamı olarak güncelleme almaya ve geliştirilmeye devam ediyor.
* Artık ASP.NET kullanmanın geçerli bir avantajı kalmamış durumda. Çeşitli sebeplerden dolayı ASP.NET Core'a geçemeyen bir projeniz yoksa geçmemek için bir mazeretiniz yok gibi, çünkü ASP.NET Core, ASP.NET'in yaptığı her şeyi daha iyi yapıyor.
</details>

<details>
<summary>MVC nedir, ne için kullanılır?</summary>
    
* **MVC**: MVC (Model View Controller), bir uygulamada mantık, kullanıcı arayüzü ve veri arasındaki ilişkiyi birbirinden ayrı tutan ve optimize eden bir mimari modeldir. Başlarda masaüstü uygulamalarında GUI'lar (Graphical User Interface) için kullanılırken şimdi daha çok web uygulamalarında kullanılmaktadır. Üç ana parçadan oluşur: Controller, Model, View
    * **Controller**: Diğer iki bileşen ve kullanıcı arasında bir köprü görevi görür. Gelen verilere ve kullanıcı girdilerine göre karar verip çağrılarda bulunur. Diğer bileşenleri yöneten bileşendir.
    * **View**: Kullanıcı arayüzünü temsil eder. Controller'dan yeni veri geldiğinde, bir veri değiştiğinde, arayüz burada güncellenir. Programın kullanıcı ile etkileşime geçtiği yer burasıdır.
    * **Model**: Programın veritabanı ile iletişime geçen kısmıdır. Controller'dan gelen talepleri yerine getirir. Veritabanı üzerinde yazma, okuma, silme vb. işlemler yapar. Verilerle ilgili işlemler ve hesaplamalar bu bileşende yer alır.
</details>

<details>
<summary>Middleware nedir, nasıl çalışır?</summary>

* **Middleware**: Middleware, bir web geliştirme mimarisinde, kullanıcı isteği ile sunucu arasında bir ara katman olarak görev yapar. Gelen istekler (request) ile sunucudan gelen cevaplar (response) arasında çeşitli görevler üstlenebilir. Bu görevler, kayıt (log) tutma, doğrulama (authentication), sık istenen verileri önbellekten gönderme (cache) vb. olabilir.
    * **Nasıl çalışır?**: İstek gelir, Middleware'a uğrar. Middleware bu istekle ne yapacağına karar verir ve eğer varsa kendisinden sonraki Middleware'a, yoksa Controller'a bu isteği gönderir. Ardından Controller'dan çıkan yanıt (response) aynı Middleware'lardan ters yönde geçerek kullanıcıya ulaşır.
</details>

<details>
<summary>Dependency Injection (DI) nedir, neden önemlidir?</summary>

* **Dependency Injection**: Dependency Injection (DI), bir class'ın bağlı olduğu alt class'ları kendi içinde oluşturmadan var olabilmesini sağlar. Normalde bağlı olduğu alt class'ları kendisi oluşturan class'lar, DI sayesinde bu class'ları dışarıdan alabilme özelliğine sahip olur. Bunu bir örnekle açıklamak çok daha kolay olacaktır.
    * Bir araba class'ınız olduğunu düşünelim. Motor, far vb. alt class'lara sahip olsun. Bu sayede araba.hareket() gibi metodlarınız çalışabilecektir. Lakin, bu sadece tek bir motor class'ı olduğu durumda geçerli olur. Daha farklı bir motor ile aynı araba class'ını oluşturmak istediğinizde bunu geleneksel yollarla başaramazsınız.
        * Bu noktada DI devreye girer. class'ları, alt class bağlantılarını direkt bir şekilde yazmak yerine, yerine herhangi bir class gelebilecek bir tanımlamayla bırakarak oluşturur. Bu sayede siz gidip sonradan istediğiniz özellikteki alt class'ı oluşturup arabaya verebilirsiniz.
    * DI kullanmadan yazılmış bir araba class'ı şu şekilde görünür:
        ```
            class Araba:
                def __init__(self):
                    self.motor = V6_motor()

            araba = Araba() # Bu araba her zaman V6 motor ile çalışacak.
        ```
        * bu arabanın motorunu V8 yapmak istediğim senaryoda bütün class'ı baştan yazmam gerekecek. DI bizi bu durumdan bu şekilde kurtarıyor:
        ```
            class Araba:
                def __init__(self, motor):
                    self.motor = motor

            araba1 = Araba( V6_motor() )
            araba2 = Araba( V8_motor() )
        ```
    * Aynı zamanda DI ile yazılmış class'ların test kodlarını yazmak da kıyasla çok kolaydır çünkü DI class'ları modülerleştirir. Araba ve motor class'larını birbirinden ayrı şekilde test edebiliyor olmak işi epey basitleştirir. Bu sayede kodu yazarken hata ayıklama süreçleri de kolaylaşır.
</details>

<details>
<summary>Katmanlı Mimari (Layered Architecture)</summary>

* **Presentation, Business, Data Access katmanları**:
    * **Data Access**: Data Access (veri erişim) katmanı, sistemin kullandığı verilere erişilen katmandır. Bu katman kompleks bir veritabanı da, basit bir JSON dosyası ve fonksiyonları da olabilir. API bağlantıları vb. gelişmiş veri sistemleri bulundurabilir. Business'tan gelen kararları uygulayarak **CRUD** (Create, Read, Update, Delete) işlemleri burada uygulanır.
    * **Business**: Programın bütün mantıksal işlerinin yapıldığı katmandır. Hesaplamalar, veri işlemeler, doğrulamalar vb. hep bu katmanda yapılır. Verilerle ilgili kararlar bu katmandan Data Access'e gönderilir, kullanıcıya gösterilecek veriler de bu katmandan Presentation'a gönderilir.
    * **Presentation**: Programın kullanıcı ile iletişimde olan katmanı bu katmandır. Kullanıcı arayüzü, girdi kutuları vb. hep bu katmanda yer alır. Kullanıcının girdilerini Business katmanına gönderir ve Business katmanından gelen verileri kullanıcıya gösterir. Yalnız bu katman kullanıcı sadece kullanıcı ile iletişime geçmek zorunda değil. Yapılan program bir API olsaydı bu katman onun erişim noktası da olabilirdi.
        * Katman bağımlılığı tek yönlüdür: *`Presentation -> Business -> Data Access`*
 
* **Service and Repository pattern**: Service and Repository pattern, önceden gördüğümüz MVC (Model View Controller) modelinin biraz daha basit haline benzer. View katmanı yoktur ve maksatı üst seviye kodun alt seviye kodların nasıl çalıştığıyla ilgilenmemesidir.
    * **Service Katmanı**: Service katmanı bütün mantık, karar ve işlemlerin yapıldığı katmandır. Veri üzerinde yapılacak işlemlere bu katmanda karar verilir ve gerekli emirler Repository katmanına gönderilir.
    * **Repository Katmanı**: Repository, veritabanı (ya da JSON gibi bir depolama) katmanıdır. Service katmanından veri ile ilgili gelen CRUD taleplerini (bazen de daha karmaşık ve büyük talepleri) yerine getirir.
    * Bu katman sistemi sayesinde Controller gibi üst seviye katman kodları iyice alt seviye kodlardan uzaklaşır. Bu sayede üst seviye kod yazmak daha temiz, kolay ve test edilebilir hale gelir.
</details>

<details>
<summary>Clean Architecture</summary>
    
* **Clean Architecture**: Clean Architecture, Uncle Bob tarafından önerilen, business (iş) kodlarını veritabanından, frameworklerden ve arayüzden tamamen bağımsız hale getirmeyi öneren yazılım mimarisidir. Temel fikir, yazılım katmanlarında bağımlılığın her zaman dıştan içe olması gerektiği ve iç katmanların dış katmanlara bağlı olmaması gerektiğidir. Örneğin, ham kod framework'e bağlı olmamalıdır. Bu sayede kod daha kolay test edilebilir ve daha temiz olur.

* **Domain, Application, Infrastructure, API katmanları**:
    * **Domain**: En iç katman. Başka bir katmana bağlılığı yok. Temel iş modelleri (class'lar, fonksiyonlar vb.) içerir. Dış katmanlar hakkında bilgisi yoktur.
    * **Application**: Domain'i kullanarak iş akışını yönetir. Gelen isteğin hangi adımlardan geçeceğini belirler. Repository ve servis arayüzleri sayesinde Infrastructure ile haberleşir.
    * **Infrastructure**: Dış dünya ile iletişim sağlanır. Application'dan gelen talimatlar dahilinde veritabanında değişiklik yapma, log tutma vb. işlemlerle ilgilenir. Örneğin domain'deki nesneyi alır ve veritabanına kaydeder.
    * **API**: Presentation katmanıdır. Kullanıcı ve arkaplan arasında düzenli veri akışına olanak sağlar.

* **Bağımlılıkların dışa akması ilkesi (Dependency Inversion Principle)**:
    * DIP, karmaşık işleri üstlenen üst düzey modüllerin alt düzey modüllerdeki değişikliklerden direkt olarak etkilenmemesi gerektiğini savunur. DIP'e göre üst düzey modüller alt düzey modüllere direkt olarak bağımlı olamaz. Ancak ikisi de ortak soyutlamalara (arayüz vb.) bağlı olabilir. Bu sayede detaylar birbirine değil soyutlamalara bağlanmış olur. Bu prensip sürdürülebilir ve temiz kod yazımını destekler.

* **Startup.cs Middleware**:
    * Middleware, istek (request) ve yanıt (response) arasına girip belirli bir iş yapan yazılım parçasına denir. Birden fazla Middleware uç uca eklenerek bir middleware pipeline oluşturulabilir. Middleware'ların sırası önemlidir. İstekler her zaman bir yönde, yanıtlar da o yönün tersinde hareket edecektir. İlk middleware, isteği ilk karşılayıp yanıtı son gönderen olur.
        * Bir middleware pipeline örneği:
          ```
            ExceptionHandler # hata ayıklama
            HttpsRedirection # güvenli kanala yönlenme
            StaticFiles      # dosya çağrıları vb. controller'a gitmeden cevaplanabilsin
            Routing          # endpoint'i bulur
            Authentication   # gidilecek endpoint'e göre doğrulama&yetkilendirme
            Controller       # hedef
          ```
</details>

## 5. Veritabanı ve ORM

<details>
<summary>SQL nedir?</summary>

* **SQL**: SQL (Structured Query Language), bir veritabanı yönetim dilidir. Veritabanları ile etkileşime geçmesi için özellikle yazılmıştır. Ancak, geleneksel yazılım dillerinde görmeyi bekleyeceğimiz bütün özellikleri taşımaz. Bu yüzden genelde diğer yazılım dilleriyle yazılan projelere (Python, C vb.) gömülerek kullanılır.
    * Diğer dillerle birleştirilmiş ve farklı şekillerde kullanılan birçok varyasyonu mevcuttur (MySQL, Oracle SQL vb.).
    * Basit CRUD işlemlerinden çok daha kompleks tablo tasarlama ve düzenleme işlemlerine kadar birçok veri düzenleme özelliği vardır.
    * Filtreleme, sıralama vb. güçlü sorgulama özellikleri vardır.
    * *Deklaratif* bir dildir, yani ne istediğini yazdığında sana onu verir, nasıl yapılacağı ile arkaplanda kendisi ilgilenir.
    * 4 ayrı komut türü vardır:
        * **DDL (Data Definition Language)**: Yapı ile ilgili komutlar:
        * *İşlemler commit edilene kadar transaction olarak kalır.*
            * `CREATE` Yeni bir veritabanı nesnesi (tablo vb.) oluşturur.
            * `ALTER` Var olan bir veritabanı nesnesi üzerinde şekil değişikliği (sütün ekleme, silme vb.) yapar.
            *  `DROP` Var olan bir veritabanını nesnesini siler.
        * **DML (Data Manipulation Language)**: Veri ile ilgili komutlar:
            * `SELECT` Var olan bir veritabanı nesnesinin içeriklerini okur.
                * `SELECT * FROM Users` Bütün kullanıcıları listeler.
            * `INSERT` Var olan bir veritabanı nesnesine yeni veri ekler.
                ```
                    INSERT INTO Users(Name, Age)
                    VALUES('Oguz', 19)
                ```
                * İsmi 'Oguz' yaşı 19 olan yeni bir kullanıcı ekler.
            * `UPDATE` Var olan bir veritabanı nesnesinin içindeki bir veriyi değiştirir.
                ```
                    UPDATE Users
                    SET Age = 26
                    WHERE UserID = 1;
                ```
                * Kullanıcı no 1 olan kullanıcının yaşını 26 yapar.
            * `DELETE` Var olan bir veritabanı nesnesinin içindeki bir veriyi siler.
                ```
                    DELETE FROM Users
                    WHERE UserID = 3;
                ```
                * Kullanıcı no 3 olan kullanıcıyı veritabanından siler.
                * WHERE yazılmazsa bütün tablo silinir.
        * **DCL (Data Control Language)**: Yetkilendirme ile ilgili komutlar:
            * `GRANT` Kullanıcıya yeni bir yetki verir.
            * `REVOKE` Kullanıcıye verilmiş bir yetkiyi geri alır.
        * **TCL (Transaction Control Language)**: İşlemlerle ilgili komutlar:
        * *Transactionlar üzerinde değişiklik yapar.*
            * `COMMIT` Yapılan tüm işlemleri kalıcı hale getirir.
            * `ROLLBACK` Commit edilmemiş işlemleri geri alır.
</details>

<details>
<summary>İlişkisel ve ilişkisel olmayan veritabanları arasındaki farklar</summary>

* **İlişkisel Veritabanı (Relational Database)**:
    * Verileri bir tablo içerisinde depolar. Şemalıdır.
    * ACID işlemlerini destekler (atomity, consistency, isolation, durability)
        * *ACID özellikleri, verilerin veritabanından bir sorun olsa dahi uygun bir biçimde ayrıldığını garantiler.*
    * Karmaşık sorgu işlemlerini destekler.
    * MySQL, Oracle vb. örnektir.
* **İlişkisel Olmayan Veritabanı (Nonrelational Database)**:
    * Verileri birçok şekilde depolayabilir (key value pair, grafik vb.)
    * Şemasızdır. Esnektir ve biçimi sürekli değiştirilebilir.
    * ACID işlemlerini desteklemez.
    * Büyük miktarda veriyi hızlı şekilde işlemek için uygundur ancak karmaşık sorguları desteklemez.
    * MondoDB örnektir.
</details>

<details>
<summary>ORM nedir? Entity Framework Core nedir?</summary>

* **ORM (Object Relational Mapping)**: Nesne ilişkisel eşleme, obje tabanlı programlama ile (object oriented programming - OOP) ilişkisel veritabanları (Relational Database) arasında kolay bağlantı sağlar.
    * OOP dillerde veriler class ve object türlerinde tutulur. ORM'nin görevi, ilişkisel veritabanındaki satır ve sütunları gerekli class ve object'lere eşlemektir.
    * Hiç SQL komutu yazmadan veritabanı kullanmaya yarar.
        ```
            var users = context.Users.Where(u => u.Age > 18).ToList();
            // SELECT * FROM Users WHERE Age > 18
        ```
    * Farklı veritabanları arasında geçiş yapmayı kolaylaştırır.
    * Yazması ve okuması çok kolay bir koda olanak sağlar.
    * Ancak bazı karmaşık sorguları (çok tablo join'leri vb.) desteklemeyebilir, performansı da ham SQL komutu yazmaktan daha yavaştır.
* **Entity Framework Core**: EF Core, Microsoft tarafından geliştirilmiş, C# entity'lerini veritabanı tablolarına geçirebilmeye yarayan bir yazılım çatısıdır (framework). Çoklu platformu destekler. LINQ destekler. Veri değişikliklerini otomatik takip eder. DbContext kullanır.
    * Migration özelliği sayesinde otomatik veritabanı eşitleme desteği sunar. Sürüm kontrolü sağlar.
</details>

<details>
<summary>DbContext nedir, nasıl kullanılır?</summary>

* **DbContext**: Veritabanı ile C# arasındaki köprüdür. Veritabanıyla tek bir oturum açarak etkileşime geçer. C# class'ları, entity'ler, veritabanı tablolarına geçirilir ve özellikleri tabloların sütunlarına yazılır.
</details>

<details>
<summary>LINQ nedir? En çok kullanılan LINQ ifadeler</summary>

* **LINQ (Language Integrated Query)**: C# ve .NET'in SQL tarzında veri sorgulama ve manipülasyonu yapmaya yarayan aracıdır. (Dil Entegrasyonlu Sorgulama)
    * LINQ direkt C# içinde sorgu yazmamıza olanak sağlar.

        ```
        // Veri kaynağı
        int[] scores = [97, 92, 81, 60];
        
        // Sorgu ifadesi
        IEnumerable<int> scoreQuery =
            from score in scores
            where score > 80
            select score;
        
        // Sorguyu çalıştırma
        foreach (var i in scoreQuery)
        {
            Console.Write(i + " ");
        }
        ```
    * Bu kodun çıktısı "97 92 81" olacaktır.

    * LINQ kodları ve SQL karşılıkları:
        * `var result = users.Select(u => u);`
        * `SELECT * FROM Users`
            * Bu iki kod da aynı işi yapar, bütün kullanıcıları seçer.
         
        * `INSERT` LINQ'te doğrudan yoktur. Bu yüzden `add` metodu ile ekleme yapılır.
          ```
          users.Add(new User { Name = "Oguz", Age = 19 });
          context.SaveChanges();
          ```
          ```
          INSERT INTO Users(Name, Age)
          VALUES('Oguz', 19);
          ```
            * Bu iki kod da ismi 'Oguz' yaşı 19 olan yeni bir kullanıcı ekler.
        * `UPDATE` de LINQ'te doğrudan yoktur. Bu yüzden güncelleme yapıp `SaveChanges()` kullanılır.
          ```
          var user = users.First(u => u.UserID == 1);
          user.Age = 26;
          context.SaveChanges();
          ```
          ```
          UPDATE Users
          SET Age = 26
          WHERE UserID = 1;
          ```
            * Bu iki kod da kullanıcı no 1 olan kullanıcının yaşını 26 yapar.
        * `DELETE` de LINQ'te doğrudan yoktur. Entity Framework Core'dan `Remove` kullanılır.
          ```
          var user = users.First(u => u.UserID == 3);
          users.Remove(user);
          context.SaveChanges();
          ```
          ```
          DELETE FROM Users
          WHERE UserID = 3;
          ```
            * Bu iki kod da kullanıcı no 3 olan kullanıcıyı veritabanından siler.
</details>

<details>
<summary>Code-First ve Database-First yaklaşımı nedir?</summary>

* **Code-First**: Öncelikle kodun yazıldığı, veritabanının koda göre otomatik oluştuğu yaklaşımdır. .NET class'ları oluşturulur, Entity Framework Core ona göre veritabanı oluşturur. Esnektir, veri yapısı zaman içerisinde değiştirilebilir. 

```
    public class BloggingContext : DbContext
    {
        public DbSet<Blog> Blogs { get; set; } # blogs için tablo
        public DbSet<Post> Posts { get; set; } # posts için tablo
    }
    
    public class Blog
    {
        public int BlogId { get; set; }
        public string Name { get; set; }
    
        public virtual List<Post> Posts { get; set; }
    }
    
    public class Post
    {
        public int PostId { get; set; }
        public string Title { get; set; }
        public string Content { get; set; }
    
        public int BlogId { get; set; }
        public virtual Blog Blog { get; set; }
    }
```

* **Database-First**: Var olan bir veritabanı üzerine program oluşturulan yaklaşımdır. Tek tip bir veritabanı üzerinden ilerler. Gelecekte veritabanı değişirse ona yönelik olan kodlar da değişmek durumunda kalır.

| Özellik | Code-First | Database-First |
|:-------:|:----------:|:--------------:|
|Başlangıç|Class'lar üzerinden veritabanı oluşur.|Var olan veritabanına göre class'lar yazılır.|
|Veritabanı Oluşumu|EF migration ile otomatik oluşturur.|EF mevcurt veritabanından class'ları üretir.|
|Güncelleme|Kod değişince migration ile veritabanı güncellenir.|Veritabanı değişince kod scaffold edilir.|

* **Scaffold**: Bir komutla kodu otomatik şekilde yeni veritabanına uygun hale getirmek demektir.
    * `Scaffold-DbContext "Server=.;Database=MyDB;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer`
</details>

## 6. Güvenlik ve Performans

<details>
<summary>Authentication vs Authorization nedir?</summary>

* **Authentication**: Bir kullanıcının kim olduğunu doğrulama işlemine denir.
* **Authorization**: Kim olduğu doğrulanmış kullanıcının hangi özelliklere erişimi olduğunun izinlendirilmesi aşamasıdır.

| Authentication | Authorization |
|:--------------:|:-------------:|
|Şifre, güvenlik soruları, biyometrik tarama vb. yöntemler kullanılır.|Kurallara bakarak kullanıcının hangi izinlere sahip olduğunu belirlenir.|
|Genelde Authorization'dan önce yapılır.|Genelde Authentication'dan sonra yapılır.|
|Genelde ID Token kullanılır.|Genelde Access Token kullanılır.|
</details>

<details>
<summary>JWT (JSON Web Token) nedir, nasıl çalışır?</summary>

* JSON Web Token, JSON tabanlı, kullanıcı doğrulaması (authentication) ve yetkilendirmesi (authorization) yapmak için kullanılan bir standarttır.
* Header, payload ve signature olmak üzere 3 parçadan oluşur.
* Örnek bir JWT:
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9                          #header
.eyJ1c2VySWQiOjEyMywicm9sZSI6ImFkbWluIiwiaWF0IjoxNjg4MDAwMDB9 #payload
.RQ9lL7w-KaB6P3c5lyWrbQ1X0r7fDeDN4uX2uY6K6rE                  #signature
```
* **Header**: Header kısmı, JWT'nin sign'lanırken kullandığı algoritmayı ve token türünü içerir.
    * **`alg`**: HS256, RS256 vb. algoritmalar kullanılır.
    * **`typ`**: Token türünü belirtir. JSON Web Token'lerde bu her zaman JWt olacaktır.

    ```
    {
        "alg": "HS256",
        "typ": "JWT"
    }
    ```
* **Payload**: Token'in içerikleri, taşıdığı bilgi bu kısımda bulunur. Bazı önerilen standart başlıkları vardır.
    * **`sub`**: Subject, token'in ilgili olduğu kullanıcı ya da oturumu belirtir.
    * **`aud`**: Audience, token'in hedef kitlesini belirtir. Örneğin programın beta kullanıcı kitlesini belirtebilir.
    * **`iat`**: Token'in ne zaman üretildiğini belirtir.
    * **`nbf`**: Not before, token'in ne zamandan sonra kullanılabileceğini belirtir.
    * **`exp`**: Expiration, token'in ömrünün ne zaman biteceğini belirtir.
    ```
    {
      "sub": "1dfee8d8-98a5-4314-b4ae-fb55c4b18845",
      "aud": "https://ogurullah.com",
      "email": "oguzkagancelik16@gmail.com",
      "name": "Oguz Kagan Celik",
      "role": "ADMIN",
      "iat": 1598607423,
      "nbf": 1598607423,
      "exp": 1598607723
    }
    ```
* **Signature**: Token'in header ve payload bölgelerinden ve bir gizli anahtardan kriptografik bir algoritmayla oluşturulan imzadır. Token'ler kontrol edilirken bu imza da doğrulandığı için bir token'in içeriği ile oynanırsa imzalar sayesinde bu fark edilir ve token reddedilebilir.

* JWT'ler **stateless** çalışır. Doğrulama işlemlerini sunucuda ek herhangi bir veri tutmaya gerek kalmadan gerçekleştirebilir. Bu veri trafiğini büyük ölçüde azaltır ve kodun mimarisini basitleştirir. JWT bütün bunları yaparken güvenlikten de ödün vermediği için iyi bir standart seçeneğidir. 
</details>

<details>
<summary>OAuth, OAuth2.0, OpenIddict, OpenID nedir? Aralarındaki ilişki</summary>

* **OAuth**: OAuth (Open Authorization), birçok platformda kullanılan bir yetkilendirme çatısıdır (authorization framework). Bir aplikasyonun başka bir aplikasyonda var olan hesabınızla şifrenize erişmeden belirli yetki taleplerine izin vermenize yarar. Bunu kullanıcı bilgilerini açık etmeden üçüncü parti servislere erişim token'leri göndererek yapar.
    * Dikkat edilmesi gerekir ki, OAuth bir authentication (doğrulama) protokolü değil, bir authorization (yetkilendirme) protokolüdür, yani hesap-kullanıcı eşleşmesi hakkında bir fikir sahibi değildir, yalnızca zaten doğrulanmış ve giriş yapılmış hesaplardaki yetki düzenlemesinden sorumludur.
 
* **OAuth 2.0**: OAuth 1.0'ın 2012 yılında yerini alan, daha kolay ve kullanıcı dostu olan versiyonu OAuth 2.0'dır. OAuth 1.0'a kıyasla farklı yetkilendirme yöntemi seçenekleriyle gelir.
    * **Authorization Code**: Genelde web uygulamalarında kullanılır. İstemci yetkilendirme sunucusundan bir yetkilendirme kodu alır ve bir erişim tokeni ile bu kodu takas eder.
    * **Implicit**: İstemci tarafının güvenli bir şekilde client secret tutamadığı durumlarda kullanılır.
    * **Client credentials**: Kullanıcının değil direkt istemcinin kaynağa ihtiyaç duyduğu durumlarda kullanılır. Sunucu-sunucu arası etkileşimlerde yaygındır.
    * **Refresh token**: Önceki token'in süresi bittiğinde kullanıcının tekrar yetkilendirme yapmasına gerek kalmadan erişim token'i göndermek için kullanılır.
    * **Resource owner password credentials**: Kaynak sahibinin istemciye çok güven duyduğu durumlar dışında kullanılması önerilmez. Kullanıcı bilgilerinin doğrudan aktarılması ile çalıştığı için güvenlik sorunu oluşturması olasıdır.
 
    * **Token türleri**:
        * **Access Token**: Kaynaklara erişim sağlar.
        * **Refresh Token**: Erişim token'inin süresi geçtiğinde yenisini istemek için kullanılır.

| Özellik | OAuth 1.0 | OAuth 2.0 |
|:-------:|:---------:|:---------:|
|Doğrulama Metodu|Kriptografik imza|Tokenler|
|Güvenlik ve karmaşıklık|Güvenli ama karmaşık|Daha basit ama potansiyel güvenlik açıkları var|
|Özel anahtar (client secret) zorunluluğu|Her durumda kullanılır|Opsiyonel|
|Yetkilendirme yöntemleri|Sınırlıdır|Esnek (authorization code, implicit vb.)|

* **OpenID**: OpenID merkezi olmayan ve açık bir kimlik doğrulama protokolüdür. Kullanıcıların üçüncü parti kimlik sağlayıcı (IDP) hizmetlerini kullanarak bu hizmetle çalışan siteler (RP - Relying Parties) tarafından onaylanmalarını sağlar. Amacı, kullanıcının internetteki kimliğini tek bir kimlik sağlayıcı ile kanıtlamasını sağlamaktır (SSO - Single Sign On). Tek bir OpenID girişi ile OpenID desteği veren bütün sitelere girmeye olanak sağlar. Kullanıcı deneyimini kolaylaştırır.

* **OpenID Connect**: OAuth 2.0'ın bir uzantısıdır. Amacı doğrulama ve yetkilendirme süreçlerini standartlaştırmaktır. OAuth 2.0 sadece yetkilendirme ile ilgilenirken OpenID Connect işin içine authentication'ı da dahil eder, kimlik doğrulama yapabilir, bunun için JWT kullanabilir.
    * OAuth 2.0 uzantısı olduğu için, yetkilendirme yöntemleri ve erişim token'lerini kullanabilir.
    * Modern uygulamalarda sıklıkla kullanılır.

| Özellik |OAuth 2.0 | OpenID | OpenID Connect |
|:-------:|:--------:|:------:|:--------------:|
|Protokol|Yetkilendirme|Doğrulama|Doğrulama + Yetkilendirme|
|Amaç|Uygulamanın kullanıcı adına verilere erişmesi (yetkilendirme)|Kimlik doğrulaması|Evrensel kimlik doğrulama ve yetkilendirme|
|Tokenler|Erişim ve yenileme tokenleri|Token yok, bilgi taşımaz|Erişim ve kimlik tokenleri|
|SSO|Yok|Var|Var|
</details>

<details>
<summary>Performans artımı için ne yapılabilir? (AsNoTracking, IAsyncEnumerable, caching, profiling, redis)</summary>

* **`AsNoTracking`**: AsNoTracking, Entity Framework'te C# ile sorgu yaparken kullanılabilen bir fonksiyondur. Normalde yapılan bütün sorgu satırlarında Entity Framework 'tracking' yapar yani olası bütün değişiklikleri önbellekte kaydeder (caching). Yanına `.AsNoTracking()` eklenen sorgularda ise bu kayıt işlemi yapılmaz. Değişiklik kayıtı tutmayı kapatmanın durumdan duruma değişen iyi ve kötü etkileri olabilir.
    * Yalnızca okuma yapılacak, bir değişiklik yapılmayacak sorgularda değişiklik kaydı tutmak anlamsızdır. Boşuna hem önbellekte yer tutacak hem de işlem hızını, performansını, büyük ölçüde düşürecektir. Bu yüzden bu tür sorgularda `AsNoTracking()` kullanmak oldukça yararlıdır.
    * Veritabanında bir değişiklik yapacak bir sorgu işleminde `AsNoTracking()` kullanmak bazen sorun yaratabilir. Geri dönülmesi gereken yanlış bir değişiklik olduğu tespit edilirse, özellikle eski verileri akılda tutmanın olanaksız olduğu senaryolarda (eğer veri çok büyükse vb.), değişiklikleri görüntülemek gerekecektir. Bunun için de 'tracking'e ihtiyaç duyulacaktır. Bu yüzden veritabanında önemli değişiklikler yapan sorgu işlemlerinde *performans kaybı pahasına* 'tracking'i açık bırakmak önemlidir.
 
* **`IEnumerable`**: `IEnumerable` üzerinde döngüyle gezilebilen bir veri setini (liste, dictionary vb.) temsil eder. Senkronize bir şekilde çalışır, yani bir veriye ulaşmadan diğerini talep etmez, dolayısıyla büyük veri setlerinde ya da verilere gecikmeli bir şekilde ulaşılabilen senaryolarda çalışırken oldukça dezavantajlıdır, performans kayıplarına sebep olur.
* **`IAsyncEnumerable`**: `IEnumerable`'dan farklı olarak asenkron şekilde çalışır. Yani bir verinin çağırılması için önceki veriye ulaşılabilmesi önemli değildir. Özellikle büyük veri setlerinde ya da verilere gecikmeli bir şekilde ulaşılabilen senaryolarda oldukça başarılıdır ve performansı artırır.

* **Caching**: İstenilen verilerin yüksek hızlı belleklerde depolanabilmesi ve istenildiğinde yüksek hızlarla erişilebilmesi anlamına gelir. Bunun için genellikle RAM (Random Access Memory), işlemcilerin içindeki L1/L2 cache bellekleri veya SSD'ler (Solid State Drive) kullanılır.
    * RAM'ler, işlemcilerin içindeki cache belleklerinden sonra var olmuş en hızlı depolama cihazlarından biridir ama görece pahalıdır. Bu yüzden `caching` RAM miktarı düşük sistemlerde yalnızca çok sık erişilen küçük veriler için kullanılabilir. Sistemdeki RAM miktarı arttıkça `cache` alınacak veri miktarı esneyebilir.
    * İşlemcilerin içinde L1/L2 cache bellekleri en hızlı ama en pahalı seçenektir.
    * Genelde çok büyük veriler içinse disk tabanlı cache ve SSD'ler kullanılır. Bu cache türü diğer cache türlerinden farklıdır.

* **Profiling**: Programın sistem kapasitesinin ne kadarını kullandığını gözlemlemeye yarayan araçtır. Sistemin hangi senaryolarda ne kadar bellek veya işlemci kapasitesi kullandığını gözlemlemeye yarar ve optimizasyona ihtiyaç duyan bölgelerine odaklanabilmeyi sağlar. Kodun hangi bölgelerde darboğaza uğradığını gösterir. 

* **Redis**: Redis (Remote Dictionary Server), genelde büyük ve yüksek hızlı erişimi istenen verilerin tutulduğu uzak sunucu bilgisayarlarına denir. Büyük verileri yerel bir cihazda tutmak depolama alanı açısından verimsiz olacağından ve bazı senaryolarda birden çok yazılımcının aynı veriye erişmesi istenilebileceği için ortaya çıkmış bir yöntemdir. Büyük veri taleplerinde çeşitli optimizasyon yöntemleri kullanarak (caching vb. )performansı yüksek tutar.
</details>

<details>
<summary>OWASP Top 10</summary>

* **OWASP Top 10**: OWASP Top 10, web uygulamaları güvenliği ve yazılımcılar için standart bir farkındalık belgesidir. Web uygulamaları için var olan en kritik güvenlik açıklarını ele alır. Yeni versiyonunun çıkış tarihi 2025 yaz sonu/sonbahar başı olmak üzere belirlenmiştir. En güncel versiyonu 2021 yılında çıkmıştır. Bir öncekisi de 2017 yılında çıkmıştı.

* 2021 yılındaki en kritik 10 web uygulaması güvenlik sorunu:
    * **A01:2021 – Bozuk Erişim Kontrolü (Broken Access Control)**
        * Erişim kontrolünde hatalar sebebiyle kullanıcılar erişememeleri gereken verilere erişme şansı yakalayabilirler. Örneğin sadece kullanıcı olarak giriş yapabilmesi gereken bir kişi programa admin olarak giriş yapıp veritabanına erişebilir. Önceki versiyondan bu yana erişim kontrolü açıkları beşinci sıradan birinci sıraya yükseldi. Test edilen uygulamaların %94'ünde bozuk erişim kontrolü tespit edildi. Şu an web uygulamalarında olan en yaygın güvenlik açığı bu.
        * **CSRF**:
            * Kullanıcıyı link'e tıklaması için Sosyal Mühendislik yoluyla kullanıcıyı kandırmayla sunucuya kullanıcı için zararlı bir işlem talebi gönderir. Link'te kullanıcının bilgilerini çalmak, değiştirmek vb. etkinlikler için bütün HTTP talepleri hazırdır, hepsinin aktifleşip çalışması için yalnızca kullanıcının link'e tıklaması yeterlidir.
        * **Broken Auth**:
            * Otomatik kullanıcı girişi saldırılarından tek bir kişiyi hedef alan saldırılara kadar geniş bir yelpazeye hitap eder. Kullanıcının hesabına giriş yaptıktan sonra uygulama ile etkileşime girerken kullandığı oturum ID'sine erişmek vb. yöntemler de kullanırlar. Şifre püskürtme, kimlik bilgisi doldurma gibi önceden farklı platformların veritabanlarından çalınmış kullanıcı adı ve şifresi verilerini otomatik bir şekilde deneyerek hesaplara girmeye çalışırlar.
    * **A02:2021 - Kriptografik Hatalar (Cryptographic Failures)**
        * Modüller arasında iletilen verilerin transfer sırasında okunmaması için şifrelenmesini sağlayan kriptografi sistemleri, bazen düzgün çalışmayarak iletimdeki hassas verilerin okunabilmesine olanak verebilir. Bu sorun üçüncü sıradan ikinci sıraya yükseldi. Önceki ismi hassas veri sızması idi, lakin bu ana sebepten çok bir semptomdu. Artık yeni hedef kriptografi hatalarına odaklanmak çünkü hassas verilere ulaşabilmeye genelde bu sebep olur.
    * **A03:2021 - Enjeksiyon (Injection)**
        * Kullanıcıdan gelen verilerin doğru tespit edilmediği, filtrelenmediği, temizlenmediği durumlarda kullanıcının web uygulaması için zararlı (veritabanına erişebilen vb.) komutlar girebilmesi demektir. SQL Injection, XSS bu duruma iyi örneklerdir.
        * **SQL Injection**:
            * Bir noktada SQL sorgularında kullanılacağı bilinen *string*'lere sistem için zararlı kodlar ekleme yoluyla yapılan saldırıdır.
        * **XSS**:
            * Cross Site Scripting Attack (XSS), siteler arası komut çalıştırma saldırıları, iyi huylu görünen bir web sayfasının içeriğine istemci taraflı komut olarak zararlı bir yazılım atması yoluyla gerçekleşen saldırılardır.
    * **A04:2021 - Güvensiz Dizayn (Insecure Design)**
        * Bu kategori 2021 versiyonunda yeni açıldı. Web uygulamanın dizaynında güvenlik açıkları bulunması demektir. Genelde uygulamaların gereksinimlerinin (SR - Software Requirements) belirlenmesi aşamasında güvenlik açıkları ile ilgili yeterince beklenti olmamasından ve uygulamanın üretim aşamasında güvenlik testlerinin ve denetimlerinin yeterince yapılmamasından kaynaklanır. Kullanıcı girdileri uygulamanın frontend'den backend'e neredeyse her aşamasında filtrelenmeli ve doğrulanmalıdır.
    * **A05:2021 - Güvenliği Yanlış Yapılandırma (Security Misconfiguration)**
        * Sunucunun ve web uygulamanın izinlerinin, güvenlik protokollerinin ayarlanmamasından, test aşamalarında kullanılan default hesapların girili kalmasından, gereksiz açık port ve kapı bırakılmasından vb. gözden kaçan detaylardan ve sistemin belirli parçalarının güncellenmemesinden kaynaklanabilir.
    * **A06:2021 – Zafiyet İçeren ve Güncel Olmayan Bileşenler (Vulnerable and Outdated Components)**
        * Güncellemeler genelde ek özellikler eklemenin yanında güvenlik açıklarını kapatan değişiklikler de yapar. Bu yüzden programları, framework'leri, kütüphaneleri vb. güncel tutmak güvenlik açısından önemlidir. Eski versiyonlar güvenlik açıkları bulundurabilirler. Yazılım parçalarını güncellemek, güncel versiyonların açıklarını yakalamak için testler yazmak, kullanılmayan parçaları kaldırmak vb. yöntemlerle bu güvenlik açığının önüne geçilebilir.
    * **A07:2021 - Kimlik Tanımlama ve Doğrulama Hataları (Identification and Authentication Failures)**
        * Bu güvenlik problemi ikinci sıradan yedinci sıraya kadar geriledi. Halen ilk onun içinde olmasına rağmen güncel standartlar bu güvenlik sorununu ortadan kaldırmaya oldukça yardımcı oluyor gibi görünüyor.
        * Brute force saldırıları, otomatik saldırılar vb. saldırıları engelleyememekte, çok basit şifreleri kabul etmekte, kırması basit kriptografi algoritmaları kullanmakta, oturum ID'lerini saklayamamakta vb. olan bir sistem varsa bu güvenlik sorununun yaşanması oldukça olasıdır. Çok aşamalı doğrulama vb. ek sistemler kullanılarak bu güvenlik sorununun önüne geçilebilir.
    * **A08:2021 – Yazılım ve Veri Bütünlüğü Hataları (Software and Data Integrity Failures)**
        * Bu kategori de 2021 yılında ilk defa oluşturuldu. Yazılımların güncellenmelerinde, CI/CD pipeline'larında, dosya bütünlüğünün kontrol edilmemesine odaklanır. Güncellemelerin imzalı olması ve kontrol edilmesi gerekir. Bunu yapmayan sistemler güncelleme gibi görünen zararlı yazılımlara karşı savunmasızdır.
    * **A09:2021 – Güvenlik Kayıtı ve Gözlemleme Hataları (Security Logging and Monitoring Failures)**
        * Hatalı giriş yapma etkinliklikleri vb. gözlemlenmesi gereken hareketlerin log'larının tutulmaması, log'lara kullanıcının ulaşabilmesi ve hangi durumlarda log tutulmadığını keşfedebilmesi, log'ların enkripte edilmemesi vb. durumlar güvenlik açığı oluşturur. Giriş etkinlikleri, doğrulamalar, erişim izinleri vb. etkinliklerin yeterli kullanıcı verisi dahil ederek ve kullanıcıya göstermeden enkripte edilerek kaydedilmesi ile olası saldırılar tespit edilebilir.
    * **A10:2021 – Sunucu Taraflı Taleplerde Sahtecilik (Server-Side Request Forgery – SSRF)**
        * Bu önemli olduğu bilinen ama çok vakası görülmeyen bir güvenlik açığı problemidir. Kullanıcıdan gelen URL'lerin kontrol edilmeden veri çekmek için kullanılması durumunda sistemin içine zararlı yazılım göndermekle çalışır. Kullanıcı verilerini harici ağlara göndererek etkisi azaltılabilir. Filtreleme, temizleme yaparak tehlikesi azaltılabilir.
     
    * **ASP.NET Core ile alınabilecek önlemler**:
        * **Model Validation**: Kullanıcıdan gelecek verilerin kurallandırılması ve belirlenen kurallara göre filtrelenmesi anlamına gelir. String uzunluklarını kısıtlama, girdi formatını kısıtlama vb. yöntemlerle injection saldırılarını engellemek için kullanılır.
        * **Input Sanitization**: XSS saldırıları vb. yöntemlere karşı gelen HTTP isteklerini ve verilerini istenmeyen karakterlere karşı taramak için kullanılır. "<, >, &" gibi kullanıcıdan gelmesi beklenmeyen kod karakterleri tespit edilir.
        * Bunlar dışında HTTPS zorunluluğu, anlık ileti limiti gibi yöntemler kullanılabilir. Log tutma ve gözlemleme, injection saldırılarına karşı string filtreleme, CSRF korumaları, doğru authentication ve authorization yapma gibi yöntemlerle de güvenlik iyice artırılabilir.
</details>

## 7. Logging ve Hata Yönetimi

<details>
<summary>Neden loglama yapılır? Log seviyesi nedir?</summary>

* **Neden loglama yapılır?**: Log tutmak, loglama yapmak, programda gerçekleşen adımların gerekli bilgilerle birlikte metin olarak kayıtlarının tutulması demektir. Giriş yapma işlemleri, kullanıcı girdileri, if else zincirleri vb. başarılı çalışması gereken mantık kodlarının kayıtlarının tutulması bu kritik noktalarda oluşabilecek hataların tespitini kolaylaştırır. Log tutmaktaki amaç, programda oluşan sorunların nerede, ne zaman ve nasıl gerçekleştiğini hakkında bilgi sahibi olmaktır. Log tutulan bir programa kıyasla log tutulmayan bir programdaki bir hatayı ve sebebini tespit etmek oldukça zordur.

* **Log seviyesi nedir?**: Log seviyesi, programın sorunlarıyla ilgilenecek kişiler için ikaz niteliği taşıyan durumlarla sıradan durumlar arasında bir hiyerarşi oluşturur. Bir güvenlik açığı, bir saldırı vb. halinde dikkat çekici uyarılar gönderecek, lakin, sıradan bir başarısız giriş durumunda yalnızca kayıt tutmakla kalacak bir sistemdir.
    * **Log Seviyeleri**:
        * **TRACE**: Olabilecek en detaylı log seviyesidir. Bir algoritmanın bütün adımları, üçüncü parti kütüphanelerin bütün hareketleri vb. kodla ilgili yaşanan her şeyin izinin sürülebildiği log seviyesidir. Sık kullanılmaz ama ihtiyaç duyulduğu durumlar olabilir.
        * **DEBUG**: Trace kadar detaylı olmasa da günlük ihtiyaçlardan daha detaylıdır. Daha çok kodlardaki sorunları gidermek için kullanılır. Her detayı değil, yalnızca sorun yapma olanağı yüksek olan kısımların log'larını tutar.
        * **INFORMATION**: Programın tutacağı standart log seviyesidir. Bir kullanıcının giriş yapması, bir çıktının alınması vb. işlemlerin kayıtlarını tutar. Bakmayınca önemli bir detay kaçırılmayacak işlemlerin log'larını tutar.
        * **WARNING**: Programın devamlılığını tehdit edecek kadar ciddi olmayan ancak başarısız olmuş işlemlerin kayıtları için kullanılır. Beklenmeyen davranışları bildirir.
        * **ERROR**: Bir fonksiyonun, programın bir kısmının çalışmaya devam etmemesi gereken durumlarda kullanılır. Örneğin bir ödeme sistemindeki hata için kullanılabilir, programın ilgili modülünün geçici olarak çalışmasını durdurmak için kullanılabilir.
        * **CRITICAL**: Program için hayati değer taşıyan kısımlardan birisinin çalışmaya devam edemeyeceği durumlarda kullanılır. Örneğin bir veritabanına erişilememesi ya da ödeme işlemlerinin alınamaması gibi durumlar buna örnek olabilir.
</details>

<details>
<summary>ASP.NET Core'da logging altyapısı</summary>

* ASP.NET Core'da üç adet logging systemi vardır. Bunlar EventSource, ILogger ve DiagnosticSource'tur.
    * **EventSource**: .NET Framework 4.5'ten beri vardır. Framework'un kendini izlemesi için kullanılır. Veri önceden belirlenmiş bir formatta kaydedilir ve serileştirilebilir. Kullanılan işletim sistemiyle entegre çalışacak şekilde tasarlanmıştır.
        * **Serileştirme**: Verinin RAM'de durduğu halinin bir veri formatına dönüştürülebilmesi demektir. 
    * **ILogger**: ASP.NET Core'da en sık kullanılan logging altyapısıdır. Class'lara bir ILogger oturumu enjekte edip `ILogger.Information()` çağırarak çalıştırılır. Yalnızca string kaydeder.
    * **DiagnosticSource**: EventSource'a benzer ancak tek farkı verinin belleği terk etmiyor olmasıdır yani serileştirilmesi gerekmez. Ayrıca verilerini ETW (Event Tracking for Windows) formatına çevirecek bir adaptör de bulundurur.
</details>

<details>
<summary>Global exception handling nasıl yapılır?</summary>

* **Global Exception Handling**: Sistemde bir yürütme hatası yaşandığında programın davranışlarını belirleyen iş akışına denir. Zaten programın yönelimi belli olmayan hatalar için bir üst çatıdır.

* **Nasıl yapılır?**: ASP.NET Core'da programın başlangıç yapılandırmasına Global Exception Handler Middleware'ı aşağıdaki gibi girilir:
```
app.UseExceptionHandler(
    options =>
    {
        options.Run(async context =>
            {
                context.Response.StatusCode = (int)HttpStatusCode.BadRequest;
                context.Response.ContentType = "text/html";
                var exceptionObject = context.Features.Get<IExceptionHandlerFeature>();
                if (null != exceptionObject)
                {
                    var errorMessage = $"{exceptionObject.Error.Message}";
                    await context.Response.WriteAsync(errorMessage).ConfigureAwait(false);
            }});
    }
);
```
* Uygulamanın pipeline'ına herhangi bir hata oluştuğunda tespit edecek bir modül olan Global Exception Handler'ı eklediğimizde olası bütün hatalar orada işlenecektir.
</details>

<details>
<summary>UseExceptionHandler vs ILogger nasıl kullanılır?</summary>

* **UseExceptionHandler**: Özel bir hata ele alma sayfası oluşturmak için UseExceptionHandler çağırılabilir. UseExceptionHandler ele alınmamış istisnai durumları yakalar ve log'unu tutar. İstisnai duruma sebep olmuş HTTP request'i değiştirip tekrar yollayarak özel hata ekranı oluşturur. Bu sayede bir hatada programı kapanmaktan kurtarır.

    * `Program.cs`'te diğer middleware modüllerden önce yerleştirilir.
    ```
    if (!app.Environment.IsDevelopment())
    {
        app.UseExceptionHandler("/Home/Error"); // /Home/Error aksiyonuna yönlendirir
        app.UseHsts();
    }
    ```
    * Talepin gideceği yer bu durumda `/Home/Error` olarak değiştirildi.

* **ILogger**: ASP.NET Core uygulamalarında kullanılan bir log tutma sistemidir. Program çalışırken olanların kaydını bir log'lama framework'üne bağlı kalmadan tutmaya yarar. Log seviyelerini destekler. Seviyelere göre log'lar içinde filtreleme yapabilir. DI (Dependency Injection) yoluyla çalışır.
```
public class MyService
{
    private readonly ILogger<MyService> _logger;

    public MyService(ILogger<MyService> logger)
    {
        _logger = logger;
    }

    public void Process()
    {
        _logger.LogInformation("İşlem {time} tarihinde başladı", DateTime.UtcNow);
        _logger.LogWarning("Düşük disk alanı tespit edildi");
        _logger.LogError("Veritabanına bağlanılamadı");
    }
}
```
</details>









