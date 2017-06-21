# Linux Dosya Sistemi Yapısı
Hangi dizinde olduğumuzu **pwd** komutuyla öğreniyorduk. Peki bu dizinler tam olarak ne işe yarıyor, bunu öğrenelim.
Bu yapıda her dosya **/** simgesiyle ifade edilen **kök dizin**in altındadır.
Kök dizinin altındaki dizinler;
- **/bin**
Temel ve gerekli kullanıcı komutlarının saklandığı dizindir.
- **/boot**
Linux çekirdeği burada bulunur. Bilgisayarın açılmasında yardımcı olur.
- **/lib**
Kütüphane dosyaları burada bulunur.
- **/lost+found**
Sistem çökmesi veya çalışır durumdaki sürücü/bölüm bağlantısı kopması gibi durumlarda kurtarılabilen dosyaların saklandığı dizindir.
- **/home**
Bir kullanıcının giriş yapabilmesi için gereken dizindir. Kullanıcıların masaüstü bilgilerini içerir. 
- **/media & /mount** 
Flash Bellek, CD gibi cihazların dosyaları bu klasörde bulunur.
- **/proc** 
Sistem ile ilgili bilgiler bu dizinde tutulur.
- **/run**
Programların çalışma id'leri bulunur.
- **/sys** 
Çalışan sisteme müdahale edebilmemiz için vardır.
- **/sbin**
Root kullanıcısının çalıştırabileceği programlar burada bulunur.
- **/srv**
Web Sunucu dosyaları burada bulunur.
- **/tmp**
Bu dizinde geçiçi olarak dosya yazıp silebiliriz. Sistemin bütün kullanıcıları dosya yazabilir fakat bir başka kullanıcının dosyalarına müdahale edilemez.
- **/var** 
Sistemimizin kayıtları burada tutulur.
- **/dev**
Donanım aygıtlarını dosya olarak bulunur.
- **/etc**
Sistemin yapılandırma dosyalarını içerir.
- **/usr**
Yüklediğimiz her program dosyaları /usr dizininde tutulur.
- **/opt** 
Dağıtımdan bağımsız ekstra yüklenen paketler için kullanılır.

## Root: 
Sistemdeki en yetkili kullanıcı yani yöneticidir.
Her kullanıcının kendisine ait bir **/home/** dizini bulunur. Normal bir kullanıcının home dizini **/home/kullaniciadi** olur.
Fakat Root'un /home dizini **/root**tur. 

## Dosya Yetkileri-Türleri
Bir dizinin içerisinde **ls -l** komutunu kullandığımızda en solda 
**drwxr-xr-x.**
şeklinde harfler görürüz.Bunları inceleyelim.
En solda bulunan d harfi **directory(dizin)** anlamına gelir. Dosyamızın türünü belirtir. **-** normal dosya (txt,jpg,png gibi) anlamına gelir. 
- b : block (/dev dizininde görülür) 
- c : character (/dev dizininde görülür)
- l : link
- d : directory 
Peki rwx nedir bunu inceleyelim. 
- r : read(dosyayı okuma izni)
- w : write(dosyaya yazma izni)
- x : execute(dosyayı çalıştırma izni)

**(Type) | (user) | (group) | (other)**

-| – - – | – - – | – - -

**drwxr-xr-x.**

Dosyanın türünden sonraki ilk üç tanesi dosyanın sahibinin (user) yetkilerini belirtir. Burdan anlayacağımız dosya sahibi 
full yetkiye **(rwx)** sahiptir. Dosya sahibinden sonra üç tanesi grubun yetkilerini belirtir. 
Daha sonraki üçlü de diğer kullanıcıların (others) yetkileridir.
Örneğimizdeki diğer kullanıcıların yazma yetkisi yoktur.
Bunlar dışında s ve t vardır.
- s : suid(secure user id) 
Dosyanın sahibinin yetkilerine sahip olur. 
- t : sticky
Temp dosyalarında bulunur. Her kullanıcının dosya oluşturma, yazma, kendi dosyalarını silme yetkileri vardır. 
Fakat başka bir kullanıcının dosyasını silemezler. 

*/dev dizinindeki bazı dosyaları inceleyelim.*
- sda : harddisk 
- sda1 : harddisk üzerinde bölümlendirme yaptıysak görünür
- random : rastgele sayı oluşturur
- zero : harddiski 0 ile doldurur

*/etc dizinindeki bazı dosyaları inceleyelim.*
- group : sistemde hangi grupların olduğunu gösterir
- passwd : kullanıcıların id numaraları , home dizinlerini gösterir. 
- shadow : kullanıcıların parola bilgileri tutulur. (şifrelenmiş biçimde)
Shadow dosyasında parolalar **SHA512** hash algoritması ile özetlenir.


*Shadow dosyasının içerisinden örnek bir satır inceleyelim.*
kullaniciadi:$6$7gNvdbpz$c6fb024a22c4db9101ea1d20596034../:15758:0:99999:7:::
- $6 = Sha-512 hash algoritması.   
- $7gNvdbpz = Salt değeri.  
- $6fb024a22c4db9101ea1d20596034.. = Parola
- :15758= Son parola değişikliği tarihi(gün sayısı)
- :0 = Parola değişiklikleri arasındaki minimum süre.
- :99999 = Parolanın maksimum geçerlilik süresi (gün sayısı)
- :7 = Hesap kapatıldıktan sonra parolanın dolma süresi
