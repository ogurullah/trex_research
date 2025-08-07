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
    ```  eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxZGZlZThkOC05OGE1LTQzMTQtYjRhZS1mYjU1YzRiMTg4NDUiLCJlbWFpbCI6ImFyaWVsQGNvZGluZ2x5LmlvIiwibmFtZSI6IkFyaWVsIFdlaW5iZXJnZXIiLCJyb2xlIjoiVVNFUiIsImlhdCI6MTU5ODYwODg0OCwiZXhwIjoxNTk4NjA5MTQ4fQ.oa3ziIZAoVFdn-97rweJAjjFn6a4ZSw7ogIHA74mGq0
    ```
</details>









