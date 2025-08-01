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
* **merge**: 'fetch' ile aldığı değişiklikleri yerel dosyalarla birleştirir.
    * `git merge` Already up to date.
* **pull**: 'fetch' ve sonrasında 'merge' uygular.
    * `git pull` Already up to date.
* **branch**: Var olan versiyonun birbiriyle çakışmayan bir klonunu üretir. Bir nevi paralel evren gibi çalışır. Başka branch'taki değişiklikler ana branch'i etkilemez.
    * `git branch test` 'test' adında bir branch oluşturur.
    * `git branch` '* main' ve 'test' olmak üzere iki branch görünüyor. '* main' şu anda main branch'teyiz demek.
* **checkout**: branch'lar arası geçiş yapmayı sağlar.
    * `git checkout test` main branch'tan çıkar ve test adındaki branch'a girer.
    * `git branch` 'main' ve '* test' olmak üzere iki branch görünüyor. Şu anda test'teyiz.
    * Burada yapacağımız bütün 'add', 'commit', 'push' işlemleri test branch'ı içerisinde olacak.
</details>



