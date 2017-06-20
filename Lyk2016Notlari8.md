## RUNLEVELS 
Linux sistemlerde sistem açılışında runlevel dediğimiz sistemin sunacağı hizmetlere göre yapılandırıldığı çalışma seviyeleri mevcuttur. 
Her runlevel, kullanıcıya makinenin davranışını kontrol edebilmesi için durdurulan veya başlatılan belirli sayıda hizmete sahiptir. Sıfırdan altıya kadar numaralanan yedi çalışma seviyesi mevcuttur.Her bir modun çalıştırdığı servisler farklıdır. Bu servislere müdahele edilebilir. Linux çekirdeği önyüklendikten sonra, init programı her çalışma seviyesinin davranışını belirlemek için /etc/inittab dosyasını okur. Kullanıcı başka bir değeri bir çekirdek önyükleme parametresi olarak belirtmedikçe, sistem varsayılan runlevelde başlayacaktır.

- Run Level 0 (Halt) - Sistemin kapalı olduğu durumdur.
- Run Level 1 (Single user mode) - Sistemi kurtarmak için kullanılan network ayarlarının aktif olmadığı tek kullanıcılı mod.
- Run Level 2 (Multiuser, without NFS) - Bu düzeyde ağ servisleri çalışmaz.
- Run Level 3 (Full Multiuser Mode) - Tüm ağ servisleri çalışır, CLI ( Komut Arayüzü ) olarak sisteme erişilir.
- Run Level 4 - Kullanılmamaktadır.
- Run Level 5 - KDE, Gnome, X Window System gibi grafiksel arayüzler kullanılabilir.
- Run Level 6 (Reboot) - Açık olan sistemi yeniden başlatır.

~~~bash
runlevel
~~~
Bulunduğumuz run leveli gösterir.

~~~bash
telinit 6
~~~
Runlevel değiştirmek için bu komut kullanılır.

## SYSTEMD

Systemd Linux için bir sistem ve servis yöneticisidir. Bir systemd , daemon çevresindeki tüm paketleri, araçları ve kütüphaneleri ifade edebilir. Init'in eksikliklerinin üstesinden gelmek için tasarlanmıştır. Bir init işlemi seri olarak başlar, yani bir görev yalnızca son görev başlatma başarılı olduktan sonra başlar ve bellekte yüklenir. Bu, genellikle gecikmeli ve uzun önyükleme süresine neden olmuştur. Systemd, süreçleri paralel olarak başlatmak için tasarlanmıştır. Böylece önyükleme süresini ve hesaplama yükünü azaltılmıştır. 

## Systemctl 

Systemctl, "systemd" sisteminin ve servis yöneticisinin durumunu incelemek ve kontrol etmek için kullanılan en temel araçtır.

~~~bash
systemctl
~~~
Çalışan servislerin tamamını görmemizi sağlar.

~~~bash
systemctl start httpd.service
~~~
Girilen servisi başlatır. Yazdığımız komut httpd.service'i aktif eder.

~~~bash
systemctl stop httpd.service
~~~
Girilen servisi durdurur.

~~~bash
systemctl status
~~~
Aktif ve çalışabilirlik durumunu söyler. Çalışma süresini gösterir.

Systemctlyi durdurup statusune baktığımızda son 10 logu kaydettiğinden sistemde bir problemle karşılaştığımızda nedenini öğrenebiliriz.

~~~bash
systemctl enable sshd.service
~~~
Bilgisayar açıldığında hangi servisin otomatik açılacağını belirtir. 

~~~bash
systemctl reload sshd.service
~~~
Servisi minimum derecede kesintiye uğratarak ayarları yükler. Girmek isteyen kullanıcıyı bekletir.

~~~bash
systemctl restart sshd.service
~~~
Servisi yeniden başlatır.

~~~bash
systemctl list-units
~~~
Yüklü olan servisleri gösterir.

~~~bash
systemctl list-dependencies
~~~
Bağımlılıkları ve çalışıp çalışmayan servisleri gösterir.

~~~bash
 systemctl isolate multi-user.target 
~~~
Runlevel değiştirir.

~~~bash
systemd-analyze
~~~
Sistem yavaşladığında (kernel,userspace) hangisinin yavaşladığını görebiliriz.

~~~bash
systemd-analyze blame
~~~
Servislerin bağlanma sürelerini gösterir.

~~~bash
systemd-analyze critical-chain
~~~
Web sunucusunun açılmasının ne kadar sürdüğümü görebiliriz.

## Journalctl
Journald daemon’u çekirdek, initd, servislerinden gelen tüm mesajları kayıt eder, saklar ve journalctl komutu ile bu journald 
üzerindeki kayıtların sorgulanmasını sağlayıp, işlem yapılabilir. Journald daemon, tüm uygun kaynaklardan verileri kolay ve dinamik 
bir şekilde işlemek için binary yapıda toplayıp saklamaktadır.

~~~bash
journalctl
~~~
Sistemin tüm loglarını gösterir.

~~~bash
journalctl --unit
~~~
Hangi servisin loglarını istiyorsak bu komutla bulabiliriz.

~~~bash
journalctl --since=today
~~~
Bugün tutulan logları gösterir.

~~~bash
journalctl -p debug
~~~ 
Debug loglarını gösterir. Debug en detaylı log levelidir.

~~~bash
journalctl --disk-usage
~~~
Maximum disk kullanımı gösterir.

## Localectl 

Localectl , sistem yerel ayarı ve klavye düzen ayarlarını sorgulamak veya değiştirmek için kullanılabilir.

~~~bash
localectl
~~~
Sistemin dilini ve klavyesini gösterir.

~~~bash
localectl list-keymaps
~~~
Klavye dillerini gösterir.

~~~bash
localectl set-keymap
~~~
Klavye dilini değiştirir.

## Timedatectl

Sistem saatini ve ayarlarını sorgulamak ve değiştirmek için timedatectl kullanılabilir.

~~~bash
timedatectl
~~~
Sistemin bulunduğu zaman, saat farkı gösterilir.

~~~bash
timedatectl set-time
~~~
Şuanki zamanı değiştirir.

~~~bash
timedatectl list-timezones
~~~
Zaman dilimi listesini gösterir.

~~~bash
timedatectl set-timezone
~~~
Zaman dilimini değiştirir.

~~~bash
date --set
~~~
Zamanı değiştirir.

~~~bash
systemctl enable ntpd.service
~~~
Ağ üzerinden zaman eşitlemesi yaparak saati ayarlar.

~~~bash
tzselect
~~~
Zaman dilimini değiştirir. 



