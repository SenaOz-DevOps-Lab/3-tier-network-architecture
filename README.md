# 3-Tier Network Troubleshooting & Architecture Lab

Bu proje, DevOps pratiklerinde hayati bir rol oynayan ağ yönetimi (networking), güvenlik duvarı (firewall) yapılandırması ve hata ayıklama (troubleshooting) süreçlerini simüle etmek amacıyla hazırlanmış 3 katmanlı (Proxy-Web-DB) bir altyapı laboratuvarıdır.

## 🏗️ Proje Mimarisi

Altyapı **Vagrant** kullanılarak 3 adet CentOS Stream 9 sanal makinesi ile oluşturulmuştur:

- **proxy01 (192.168.50.10):** Nginx Reverse Proxy. Dış dünyadan gelen HTTP (Port 80) isteklerini karşılar ve Web sunucusuna iletir.
- **web01 (192.168.50.11):** Apache Web Server. Özel olarak 8080 portunda çalışacak şekilde yapılandırılmıştır.
- **db01 (192.168.50.12):** MariaDB Database Server. Sadece iç ağdan (3306 portu) erişime açıktır.

## 🚀 Kullanılan Teknolojiler & Araçlar

- **Provisioning:** Vagrant, VirtualBox
- **OS:** CentOS Stream 9
- **Web & Proxy:** Nginx, Apache (httpd)
- **Database:** MariaDB
- **Güvenlik:** firewalld, SELinux
- **Ağ Analizi Araçları:** `ping`, `ss`, `nc` (Netcat), `curl`, `ip route`, `nmap`

## 🛠️ Öğrenim Kazanımları (Troubleshooting Senaryoları)

Bu projede sadece kurulum yapılmamış, aynı zamanda gerçek dünya kriz senaryoları yaratılıp çözülmüştür:

1. **Servis Çökmesi (Connection Refused):** Veritabanı servisi durdurulup, sorunun ağda (Ping) değil Uygulama Katmanında (Netcat) olduğu teşhis edilmiştir.
2. **Güvenlik Duvarı Engeli (No Route to Host / 502 Bad Gateway):** `firewalld` kuralları nedeniyle Nginx'in Apache'ye ulaşamaması simüle edilmiş ve sadece belirli portlar (`80` ve `8080`) dışarıya açılarak sorun giderilmiştir.
3. **Yönlendirme (Routing) Hatası (Network Unreachable):** Yönlendirme tablosuna kasıtlı olarak "Blackhole" (Kara Delik) kuralı eklenmiş ve ağ paketlerinin kernel seviyesinde nasıl düştüğü `ip route` üzerinden analiz edilmiştir.

## 💻 Kurulum ve Çalıştırma

Projeyi kendi bilgisayarınızda çalıştırmak için:

1. Depoyu klonlayın ve klasöre girin:
   ```bash
   git clone <REPO_URL>
   cd 3tier-network-lab
   ```

2. Vagrant ile tüm altyapıyı ayağa kaldırın:
   ```bash
   vagrant up
   ```

3. Kurulum tamamlandıktan sonra test etmek için ana makineden (veya proxy sunucusundan) şu komutu çalıştırın:
   ```bash
   curl http://192.168.50.10
   ```
   *Beklenen Çıktı: "Merhaba, ben Web01! DevOps Lab basariyla calisiyor."*

4. İşiniz bittiğinde kaynakları serbest bırakmak için:
   ```bash
   vagrant destroy -f
   ```

## 📸 Uygulama Görselleri & Test Çıktıları

Projenin kurulumu ve sorun giderme (troubleshooting) aşamalarında alınan bazı canlı terminal çıktıları:

![Test 1](<images/Ekran görüntüsü 2026-08-28 185538.png>)
![Test 2](<images/Ekran görüntüsü 2026-08-28 185644.png>)
![Test 3](<images/Ekran görüntüsü 2026-08-28 190042.png>)
![Test 4](<images/Ekran görüntüsü 2026-08-28 190936.png>)
![Test 5](<images/Ekran görüntüsü 2026-08-28 191118.png>)
![Test 6](<images/Ekran görüntüsü 2026-08-28 191328.png>)
![Test 7](<images/Ekran görüntüsü 2026-08-28 191515.png>)
![Test 8](<images/Ekran görüntüsü 2026-08-28 191742.png>)
![Test 9](<images/Ekran görüntüsü 2026-08-28 191937.png>)
![Test 10](<images/Ekran görüntüsü 2026-08-28 192558.png>)
![Test 11](<images/Ekran görüntüsü 2026-08-28 192947.png>)

---
*Bu proje, DevOps ağ iletişimi ve Linux sunucu yönetimi becerilerini geliştirmek için uygulamalı bir pratik olarak hazırlanmıştır.*
