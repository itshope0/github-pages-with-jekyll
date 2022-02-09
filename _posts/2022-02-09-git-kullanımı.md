- Gitin yüklü olup olmadığının ya da versiyonunun kontrolü `git --version`
- Yüklü değilse Download git https://git-scm.com/downloads

## Ön ayarlar:

-   `git config --global user.name "your-name"` -> github.com'da oluşturduğunuz web reponuza local yani bilgisayarınızda bulunan repoyu push ederken kimin ismi ile görünmesini istersiniz 
-   (--global ile her oluşturduğunuz repo için bu ayar geçerli olur eklemezseniz sadece bulunduğunuz projede geçerli olur)
-   -   `git config --global user.email "your-email"`
-   Burada local reponuzda yaptığınız commitleri github.com reponuza gönderirken görülen email. Burada güvenlik için kendi emailimizin görünmesini istemiyorsak github.com profilimizde sağ üst taraftan `Settings` e tıklayarak sol tarafta `Access` adı altında `Emails` gelip oradan `"Keep my email address private"` seçiyoruz böylece artık orada bulunan `id+username@users.noreply.github.com` şeklinde bulunan githubın bize vermiş olduğu email adresimizi kopyalayıp yukarıda kullanarak `your-email` kendi emailimizi gizlemiş oluruz. Ayrıca hesabımızla olan bağlantıyı sağlamış github ana sayfamızda bulunan contributions bağlantısı da sağlanmış oluyor. (Yaptığımız aktiviteler)
-   Ayrıca `"Keep my email address private"` ın bir altında bulunan `Block command line pushes that expose my email` ide seçerek yanlışlıkla local repomuzu command line dan github.com web repomuza push ederken ayarlarımızda bir değişiklik yaptıysak ve githuba kayıt olduğumuz email görünüyorsa o commiti bloklar ve sizi uyarır.
- `git config --list` -> yukarıda yapılan ayarların doğruluğunun kontrolü

Daha sonra Github CLI ı indiriyoruz. "[About GitHub CLI](https://docs.github.com/en/github-cli/github-cli/about-github-cli)."
windows10 da kolayca `winget install --id GitHub.cli` yazarak indirebiliriz.

Github CLI ile `github.com` giriş yaparak local `git` imizi yetkilendiriyoruz.
Browser ı seçerek oradan yetkilendirme işlemini gerçekleştirebilirsiniz. HTTPS ile şifrelemiş biçimde credentialları gönderebilirsiniz. Github ın Credential Managerı nda tutulacaktır bunlar.
[`gh auth login`](https://cli.github.com/manual/gh_auth_login)


## Repo Oluşturma
Burada webte(github.com) ve localde(host bilgisayarımızda) repo oluşturup daha sonra ikisi arasındaki bağlantıyı gerçekleştirerek. Localdeki değişikliklerimizi webte depolayacağız. Böylece hem insanlar projemize katkı sağlayabilir hem kodlarımızı depolamış, ayrıca herhangi birinin projesini clone ladıysak ya da forkladıysak o değişiklikleri tekrar web forkuna (klonladıysak klon için yeni bir web reposu oluşturmamız gerek) push ederek ve github.com üzerinden projede pull kısmına gelip pull request atabiliriz. Böylece kendi branchimizde yapılan değişiklik kabul görürse ilgili kişiler kendi projenin kendi main branchine eklerler. 

`github.com` da sign up diyerek account açıp ilk web repomuzu oluşturuyoruz. Yine sağ üstte + ya tıklayarak `New repository` diyebilirsiniz. Daha sonra proje ismi yazıp `Create repository` diyebilirsiniz. 

Şimdi web te bir repomuz var. Windowsta `cmd` ye girerek.(Sol alt başlatın orda aramaya `cmd` yazın çıkar). Bilgisayarımızda projemizin olduğu yere gidiyoruz. Masaüstündeyse `cd C:\Users\BilgisayarKullanıcıAdınız\Desktop\ProjeAdı` veya `D` ya da başka bir sürücüdeyse `cd /d D:\ProjeYolu`  şeklinde klasöre gidiyoruz. Projemiz yoksa bir klasör açıyoruz `mkdir klasörAdı`. İçerisine basit bir dosya oluşturuyoruz. Daha sonra artık repo komutlarımıza başlayabiliriz. `type nul > test.txt` ile basit bir dosya oluşturabilirsiniz cmd de.

`git init` -> Projemizde git etkileşimini başlatıyoruz. .git adı altında gizli bir klasör oluşuyor. `Windows gizli dosyaları göster` kapalıysa bu dosyayı göremezsiniz.
`git add .` ile tüm dosyaları staginge tracinge (toplanma ya da izlenme alanı olarak aklınızda kalabilir) ekliyoruz.
ya da 
`git add dosyaAdı` ile hangi dosyayı istiyorsak sadece onu izlemesini, toplanma alanına eklemesini istiyoruz. Daha sonra bu alandaki dosyalardaki değişikliklerin kalıcı olması için commit işlemi gerçekleştireceğiz.
Yani burdaki `git rm --cached dosyaAdı`  ile istediğimiz dosyaların sürüm izlemesini kaldırabiliriz 
Tüm değişiklikler tamam artık kalıcı kayıt etmek istiyoruz 
`git commit -m "değişikliğimiz neyle ilgiliyse mesajımızı yazıyoruz"`
Mesaj önemli daha sonra neden bu değişikliği yaptığımıza dönüp bakabiliriz.
````shell
git remote add upstream  <REMOTE_URL> 
````
yani `git remote add origin https://github.com/username/repoadı.git` yazarak localdeki `main` adı altındaki yani şu anda bulunduğumuz branchin adının main olduğunu varsayıyoruz. Origin burda bizim remote adresimizin Takma adı oluyor. Yani kısacası `url` in yerini tutuyor. Repo adı burada yazının en başında github.com da web reposu oluşturduğumuz oluyor.
Kısacası local git imiz ile web github.com ın bağlantısını bu proje için yaptık. Artık `origin` bizim github.com daki remote proje repomuzun adresi.
- Orada eğer `readme.md` ekle seçtiysek kendisi main branchini oluşturuyor. 
- Local git imizde ise biz `git init` den sonra `git commit` işlemini gerçekleştirdiğimizde kendisi `master` isminde branch oluşturuyor.
- Unutmadan branchler bir commit işlemi olduğunda oluşuyor ilk olarak. Webte github.com da repoyu oluştururken `readme.md` yi vs oluşturarak commit işlemi yapıyor hatta `git init` işlemini de en başta yapıyor. Contributionsınızın artığını farkedebilirsiniz webte repo oluşturunca aynı şekilde.
- ```shell
git push  <REMOTENAME> <BRANCHNAME> ```
`git push -u origin main` dediğimizde localimizdeki `main` isimli branchi `origin` e yani uzak web repomuza göndermek istediğimizde hata alacağız.
Daha sonra localimizde bulunan `master` branchimizden webte github.com da bulunan `main` branchine `commit` ile yaptığımız yaptığımız kalıcı değişiklikleri depolamak istersek hata alacağız.
```
error: src refspec main does not match any
error: failed to push some refs to 'github.com:xxxxxx/xxx-project.git'
```
Burada localde source(src)(kaynak) olarak `main` isminde branch bulamadığını web github.com repomuza(origin) bunu gönderemediğini söylüyor.
Evet bu doğru çünkü github webte repo oluşturunce ve commit işleminden sonra `main` branchi oluşurken localimizde bulunan `git` bize commit işleminden sonra `master` isimli branch oluşturdu. Bunu `git branch` yazarak kontrol edebiliriz.


`git branch` yazarak kontrol edebiliriz. Yeşil olarak hangisi yanıyorsa.
`git checkout brachIsmi` ile o branche geçiş yapabiliriz.

Hatayı çözmek için:

`git branch -m master main` -> master ismindeki local branchimizn ismini main yapıyoruz. Böylece web github.com da bulunan repomuzun branchiyle aynı isimli oldu. Artık local branch `main` deki değişiklikleri web repomuza push etmek istediğimizde bu sefer de 
```
! [rejected]        main -> main (non-fast-forward)
```
şeklinde başlayan local main branchinin uzak main branchine push edilemeyeceği çünkü web github.com daki repomuz ilk oluşturulken `readme.md` dosyası oluşurken `commit` işlemi gerçekleşmiş ve `main` branchi oluşmuştu. Bu değişiklik `readme.md` oluşmadan da varoluyor burada. Bu yüzden ilk önce uzak repomuzdaki değişikliği locale çekmeliyiz ki çünkü orasının birden fazla insanın katkı yaptığı bir yer olarak düşünüyorsek ki github.com un amacı bu. Birden fazla insan bir proje üstünde çalışabilir. Herhangi bir insan değişiklik yaptıysa `main` yani production branchinde bu değişikliği önce kendi localimize almalıyız çünkü bu kabul görmüş bir değişiklik. Bunu fetch ile bilgileri çekiyor daha sonra merge ile şu andaki projemize dahil ediyoruz. Conflict olmaması için dua ederek yazımızı burada sonlandırıyoruz.
`git fetch origin`
`git merge --allow-unrelated-histories origin/main` 

Kaynaklar

https://docs.github.com/en/get-started/quickstart/set-up-git

https://stackoverflow.com/questions/65173291/git-push-error-src-refspec-main-does-not-match-any-on-linux

https://docs.github.com/en/get-started/using-git/pushing-commits-to-a-remote-repository

https://github.com/microsoft/Web-Dev-For-Beginners/tree/main/1-getting-started-lessons/2-github-basics


https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-user-account/managing-email-preferences/setting-your-commit-email-address

https://docs.github.com/en/articles/setting-your-commit-email-address

https://gitbetter.substack.com/p/how-to-clean-up-the-git-repo-and

https://training.github.com/downloads/tr/github-git-cheat-sheet/
