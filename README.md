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

* init: Boş bir Git repository'si oluşturur.
    * `cd Desktop`
    * `mkdir trex_research`
    * `git init`
  
</details>



