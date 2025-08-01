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
<summary>Temel Git komutları: init, clone, add, commit, push, pull, branch, merge</summary>

* **init**: Boş bir Git repository'si oluşturur. Repository, Git'in üzerinde versiyon kontrolü yapacağı klasörlere verilen addır.
    * `cd Desktop` Masaüstüne gittim.
    * `mkdir trex_research` 'trex_research' adlı bir klasör oluşturdum.
    * `git init` 'trex_research' adında bir Git repository'si oluşturdum.
    * `ls` Şu anda klasör boş.
* README.md dosyasını manuel bir şekilde oluşturdum. Markdown dosyasını JupyterLab kullanarak düzenledim.
* **add**: Modified stage'de olan bir dosyayı, staged olmak üzere, gelecek commit'e ekler.
    * `git add README.md` 'README.md' Markdown dosyamı bir sonraki commit'e eklemek için işaretledim.
* *Git sisteminde modified, staged ve committed olmak üzere üç dosya türü vardır. Modified, Git'in local veritabanından farklı olan, üzerinde değişiklik yapılmış dosyalardır. Staged, bir sonraki commit'e eklenmek üzere add komutu ile işaretlenmiş dosyalardır. Committed, commit komutu ile yerel veritabanına eklenmiş dosyalardır.*
* **commit**: 'add' komutu ile eklenmiş, staged duruma gelmiş, bütün dosyaları committed duruma getirir yani yerel veritabanına ekler. Dosyaları 'push' komutu ile sunucuya yüklenmek üzere adeta paketler ve etiketler.
    * `git commit -m "paket mesajı"` Staged duruma getirdiğim bütün dosyalarımı (yalnızca 'README.md') bir sonraki 'push'ta GitHub'a yüklemek için paketledim, yerel veritabanına kaydettim.
    * Eğer '-m' ve beraberinde bir paket mesajı kullanmazsak Git bizi Vim veya Nano gibi bir text editor'e yönlendirir. Ben bunun yerine mesajımı '-m' kullanarak tek komutta eklemeyi tercih ediyorum.
* **push**: Sunucuya yüklenmek üzere paketlenmiş yerel veritabanındaki bütün değişiklikleri sunucuya gönderir.
    * `git push` 'README.md' dosyasını GitHub'a yükledim.
* **fetch**: Sunucudaki versiyon ile yerel veritabanındaki versiyonu kıyaslar, sunucudaki güncelse değişiklikleri alır.
    * `git fetch` Sunucudaki 'README.md' ile yerel aynı.
* **merge**: 'fetch' ile aldığı değişiklikleri yerel dosyalarla birleştirir. Branch'ları birleştirmek için de kullanılır.
    * `git merge` Already up to date.
* **pull**: 'fetch' ve sonrasında 'merge' uygular.
    * `git pull` Already up to date.
* **branch**: Var olan versiyonun ikisi birbiriyle çakışmayan bir klonunu üretir. Bir nevi paralel evren gibi çalışır. Başka branch'taki değişiklikler ana branch'i etkilemez.
    * `git branch test` 'test' adında bir branch oluşturur.
    * `git branch` '* main' ve 'test' olmak üzere iki branch görünüyor. '* main' şu anda main branch'teyiz demek.
* **checkout**: branch'lar arası geçiş yapmayı sağlar.
    * `git checkout test` main branch'tan çıkar ve test adındaki branch'a girer.
    * `git branch` 'main' ve '* test' olmak üzere iki branch görünüyor. Şu anda test'teyiz.
    * Burada yapacağımız bütün 'add', 'commit', 'push' işlemleri test branch'ın içerisinde olacak.
</details>

<details>
<summary>Merge conflict nedir, nasıl çözülür?</summary>

* Merge conflict, iki branch'ın 'merge'lenirken bir dosyanın aynı yerinde farklı değişiklikler yapılmış olmasından kaynaklanan 'merge'lenememe durumudur. Git, aynı yerde birbirinden farklı iki değişikliği nasıl ele alması gerektiğini bilemez ve hata verir. Dosyada çakışan bölge(ler),
    * `<<<<<<<HEAD` ve `=======`
* arasında gösterilir. Bu kısımda hangi versiyonun kabul edileceği yazılımcı tarafından manuel şekilde belirlenir ve ancak böyle 'merge' işlemi gerçekleşebilir.
</details>

<details>
<summary>CI/CD nedir? Azure DevOps, GitHub Actions ile pipeline örnekleri</summary>

* CI (Continuous Integration): CI basitçe kodunuzu sıklıkla ortak branch'e yüklemek, kendi kodunuzu da ortak kodu da güncel tutmak demektir. Yazılımcılar kodlarını kendi local branch'lerinde tutma eğilimi gösterebilirler. Bu prensip, bu duruma karşı olarak yazılımcıların kodlarını sıklıkla paylaşmaları gerektiğini söyler.
* CD (Continuous Delivery): CD, otomatik testler vb. kullanarak değişiklik yaptığınız kodunuzu da daima 'deployable' yani yayımlanabilir bir durumda tutma prensibidir.
* CI/CD pipeline dediğimiz şey basitçe bir yazılımcı ortak branch'e bir kod yüklediği zaman kodun otomatik şekilde yayımlanana kadar geçtiği adımlardır. Ortak branch'e bir kod yüklendiğinde, bu kodu önceden belirlenmiş testlere otomatik bir şekilde sokup, daha sonra projeyi otomatik bir şekilde build'leyip, süreç içerisinde herhangi bir sorun çıkmazsa da otomatik bir şekilde yayımlanmasına yarar. Çıkan bir sorunda da işlem durur ve ilgili yazılımcıya bildirim gider.
* Ortak branch'e her güncelleme geldiği zaman manuel bir şekilde kodları birleştirip test etmek ve yayımlamak insan hatalarına izin veren, yavaş ve verimsiz bir yöntem olduğu için pipeline çok kullanışlıdır.
* Basit bir GitHub Actions pipeline örneği: `.github/workflows/hello-world.yml`
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
* *.NET Framework, .NET Core ve .NET 7/8+ farkları*:

| .NET Framework   | .NET Core | .NET 7/8+  |
|:-----------------|:---------:|-----------:|
| A                | B         | C          |
| D                | E         | F          |

</details>

