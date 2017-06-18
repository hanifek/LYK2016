## RUNLEVELS 
Linux sistemlerde sistem açılışında runlevel dediğimiz sistemin sunacağı hizmetlere göre yapılandırıldığı çalışma seviyeleri mevcuttur. 
Basitce windows sistemlerde Safe mode ile girdiğimiz ve sistemlerin tekli kullanıcı moda’ta sorunları çözebileceğimz şekilde de 
Linux sisteminde RunLevel ‘lar günlük hayatımızda karşımıza çıkar. Linux sistemlerde birden fazla açılış modu bulunmaktadır. Her bir modun 
çalıştırdığı servisler farklıdır. Bu servislere müdahele edilebilir.

- Run Level 0 (Halt) - Sistemin kapalı olduğu durumdur.
- Run Level 1 (Single user mode) - Sistemi kurtarmak için kullanılan network ayarlarının aktif olmadığı tek kullanıcılı mod.
- Run Level 2 (Multiuser, without NFS) - Bu düzeyde ağ servisleri çalışmaz.
- Run Level 3 (Full Multiuser Mode) - Tüm ağ servisleri çalışır, CLI ( Komut Arayüzü ) olarak sisteme erişilir.
- Run Level 4 - Kullanılmamaktadır.
- Run Level 5 - KDE, Gnome, X Window System gibi grafiksel arayüzler kullanılabilir.
- Run Level 6 (Reboot) - Açık olan sistemi yeniden başlatır.

~~~bash
telinit 6
~~~
Telinit komutu girilen run leveli uygular.

~~~bash
runlevel
~~~
Bulunduğumuz run leveli gösterir.

## SYSTEMD ARAÇLARI - SYSTEMCTL
Systemd olarak adlandırılan program, Linux sistemleri için geliştirilmiştir. Amacı; bilgisayardaki sistem ve servislerin çalışmasını 
organize etmektir. Bu yönetimi, systemctl, journalctl, notify, analyze, cgls, cgtop, loginctl ve nspawn olarak adlandırılan araçlar 
sayesinde gerçekleştirir.Systemctl komutları ile Linux tabanlı işletim sistemlerinde servisleri yönetilebiliriz. En basit tanımıyla 
systemd linux kerneli için sistem ve servis yöneticisidir. Systemd linux tabanlı işletim sistemleri için geliştirilmiştir.

~~~bash
systemctl stop httpd.service
~~~
Httpd servisini durdurur.

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
Sistemi yeniden başlatır.

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

## SYSTEMCTL ARAÇLARI - JOURNALCTL
Journald daemon’u çekirdek, initrd, servislerinden gelen tüm mesajları kayıt eder, saklar ve journalctl komutu ile bu journald 
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

~~~bash
timedatectl
~~~
Sistemin bulunduğu zaman, saat farkı, P(internet üzerinden saat ayarları) gösterilir.

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
Bilgisayar açıldığında otomatik olarak saati ayarlar.

~~~bash
tzselect
~~~
Zaman dilimini değiştirir. 



