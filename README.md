# 🌐 Bilgisayar Ağları ve Veri İletişimi (Computer Networks & Datacom)

> ### 📌 Dokümantasyon Hakkında
> Bu çalışma; **Huawei ICT Academy – Computer Networks Bootcamp** kapsamında edindiğim temel üzerine inşa edilmiştir. 
> 
> Eğitimi yalnızca üreticiye (Huawei) özgü komut ve senaryolarla sınırlı bırakmayıp; üniversite bilgisayar mühendisliği müfredatındaki standart akademik kaynakları (*James F. Kurose & Keith W. Ross - Computer Networking: A Top-Down Approach*, *Andrew S. Tanenbaum - Computer Networks*) ve sektör standardı diğer üretici pratiklerini (Cisco vb.) kapsayacak şekilde derinleştirdim. 
> 
> **Amaç:** Hem kurumsal sertifikasyon süreçlerine hem de akademik ders/mülakat hazırlıklarına zemin oluşturacak, Türkçe ve uçtan uca kapsamlı bir ağ referans dokümantasyonu oluşturmaktır.
>
> [![PDF Dokümanı](https://img.shields.io/badge/PDF-Notları_İndir-blue?style=for-the-badge&logo=adobe-acrobat-reader)](Computer-Networks-and-Datacom-Notes.pdf)
---

## 📑 İçindekiler
- [1. Ağ Kavramları ve Türleri](#1-ağ-kavramları-ve-türleri)
- [2. Ağ Performansı ve Temel Metrikler](#2-ağ-performansı-ve-temel-metrikler)
- [3. Protokoller ve Referans Modelleri](#3-protokoller-ve-referans-modelleri)
- [4. Fiziksel Katman](#4-fiziksel-katman)
- [5. Veri Bağlantı Katmanı (Data Link Layer)](#5-veri-bağlantı-katmanı-data-link-layer)
- [6. Switch Temelleri](#6-switch-temelleri)
- [7. VLAN ve Trunk](#7-vlan-ve-trunk)
- [8. STP (Spanning Tree Protocol) Ailesi](#8-stp-spanning-tree-protocol-ailesi)
- [9. Link Aggregation (Bağlantı Birleştirme / LAG)](#9-link-aggregation-bağlantı-birleştirme--lag)
- [10. Ağ Katmanına Giriş: Devre/Paket Anahtarlama ve Router Mimarisi](#10-ağ-katmanına-giriş-devrepaket-anahtarlama-ve-router-mimarisi)
- [11. IPv4 Adresleme ve Subnetting](#11-ipv4-adresleme-ve-subnetting)
- [12. Yönlendirme (Routing) Temelleri](#12-yönlendirme-routing-temelleri)
- [13. Dinamik Yönlendirme Protokolleri](#13-dinamik-yönlendirme-protokolleri)
- [14. Inter-VLAN Routing (VLAN'lar Arası Yönlendirme)](#14-inter-vlan-routing-vlanlar-arası-yönlendirme)
- [15. IPv6](#15-ipv6)
- [16. Taşıma Katmanı: TCP ve UDP](#16-taşıma-katmanı-tcp-ve-udp)
- [17. Uygulama Katmanı Protokolleri](#17-uygulama-katmanı-protokolleri)
- [18. Socket Programlama Temelleri](#18-socket-programlama-temelleri)
- [19. Ağ Güvenliği](#19-ağ-güvenliği)
- [20. WAN Teknolojileri](#20-wan-teknolojileri)
- [21. Kablosuz Yerel Ağ (WLAN)](#21-kablosuz-yerel-ağ-wlan)
- [22. Ağ Yönetimi ve Modern Teknolojiler](#22-ağ-yönetimi-ve-modern-teknolojiler)
- [23. Kampüs Ağı Mimarileri](#23-kampüs-ağı-mimarileri)
- [24. Laboratuvar Araçları: Wireshark ve Cisco Packet Tracer](#24-laboratuvar-araçları-wireshark-ve-cisco-packet-tracer)
- [25. Cihaz Yönetimine Genel Bakış (CLI Kavramları)](#25-cihaz-yönetimine-genel-bakış-cli-kavramları)
- [26. Sınava / Tekrara Hazırlık — Kritik Noktalar](#26-sınava--tekrara-hazırlık--kritik-noktalar)

---

## 1. Ağ Kavramları ve Türleri
Bir ağ (network), düğümler (node — bilgisayar, switch, router, AP vb.) ile bunları birbirine bağlayan bağlantılardan (link) oluşan; kaynakların ve bilginin paylaşılmasını sağlayan bir sistemdir.  
İnternet, dünyanın en büyük ve en yaygın ağıdır; kökeni 1969'da ABD Savunma Bakanlığı projesi olan ARPANET'e dayanır. 1980'lerde TCP/IP'nin standart protokol olarak benimsenmesiyle bugünkü İnternet'in temelleri atılmıştır.

### Kapsama Alanına Göre Ağ Türleri
| Tür | Kapsama Alanı | Tipik Kullanım |
| :--- | :--- | :--- |
| **PAN** (Personal Area Network) | Birkaç metre | Bluetooth, kulaklık-telefon bağlantısı |
| **LAN** (Local Area Network) | Bina/ofis/kampüs | Yüksek hız, düşük maliyet, özel sahiplik |
| **MAN** (Metropolitan Area Network) | Şehir çapında | Kampüsler arası bağlantı |
| **WAN** (Wide Area Network) | Ülke/kıta çapında | İSS hatları, kiralık hatlar, MPLS |

### Ağ Bileşenleri (Donanım)
* **Host (uç cihaz):** PC, sunucu, telefon, IoT cihazı — ağın kullanıcı tarafı.
* **Switch:** Aynı yerel ağdaki (LAN) cihazları MAC adresine göre birbirine bağlar; OSI Katman 2'de çalışır.
* **Router:** Farklı ağlar (subnet) arasında IP adresine göre yönlendirme yapar; OSI Katman 3'te çalışır.
* **Firewall:** Güvenlik politikalarına göre trafiği filtreler; günümüzde çoğu Katman 3-7 arası (Next-Gen Firewall) işlev görebilir.
* **Access Point (AP):** Kablosuz istemcilerin ağa bağlanmasını sağlayan cihaz.

> [!NOTE]
> Bu ayrım (switch = L2, router = L3) en sık sorulan kavramlardan biridir; iyice pekiştirilmelidir.

### Ağ Topolojileri
| Topoloji | Açıklama | Avantaj / Dezavantaj |
| :--- | :--- | :--- |
| **Yıldız (Star)** | Tüm uçlar merkezi bir switch/hub'a bağlanır | Yönetimi kolay / merkez arızalanırsa tüm ağ etkilenir |
| **Veri Yolu (Bus)** | Tüm cihazlar tek bir omurga kabloya bağlanır | Ucuz / arıza tespiti zor, günümüzde kullanılmıyor |
| **Halka (Ring)** | Cihazlar dairesel bağlıdır, veri tek yönde dolaşır | Öngörülebilir gecikme / bir bağlantı kopunca tüm halka etkilenir |
| **Ağaç (Tree)** | Hiyerarşik yıldız birleşimi | Ölçeklenebilir / kök noktaya bağımlı |
| **Tam Örgü (Full-Mesh)** | Her düğüm diğer tüm düğümlere doğrudan bağlı | Çok yüksek güvenilirlik / n(n-1)/2 bağlantı, maliyetli |
| **Kısmi Örgü (Partial-Mesh)** | Bazı düğümler doğrudan, bazıları dolaylı bağlı | Maliyet/güvenilirlik dengesi |

Gerçek kurumsal ağlarda genelde hibrit (birleşik) topoloji kullanılır: çekirdek katmanda mesh, kenarda yıldız gibi.

---

## 2. Ağ Performansı ve Temel Metrikler
Bir ağın 'ne kadar iyi' çalıştığını ölçmek için kullanılan temel nicel kavramlardır; Türkiye'deki mühendislik derslerinde (Kurose & Ross kitabına dayalı müfredatlarda) giriş bölümünde işlenir.

### Gecikme (Delay) Türleri — Bir Paketin Uçtan Uca Toplam Gecikmesi
| Gecikme Türü | Tanım | Bağlı Olduğu Faktör |
| :--- | :--- | :--- |
| **İşlem gecikmesi** (*Processing delay*) | Router'ın paket başlığını inceleyip hangi çıkış arayüzüne yönlendireceğine karar verme süresi | Router işlemci hızı, genelde mikrosaniyeler |
| **Kuyruklama gecikmesi** (*Queuing delay*) | Paketin, çıkış arayüzünde gönderilmeyi beklerken kuyrukta geçirdiği süre | Trafik yoğunluğu — değişkendir, tıkanıklıkta artar |
| **İletim gecikmesi** (*Transmission delay*) | Paketin tüm bitlerinin bağlantıya 'itilmesi' için geçen süre = Paket boyutu / Bağlantı hızı | Paket boyutu ve link bant genişliği |
| **Yayılım gecikmesi** (*Propagation delay*) | Bir bitin, göndericiden alıcıya fiziksel ortamda yol alma süresi = Mesafe / Yayılım hızı | Fiziksel mesafe ve ortamın yayılım hızı |

Toplam uçtan uca gecikme (tek link için) = İşlem + Kuyruklama + İletim + Yayılım gecikmeleri toplamıdır. Çok hop'lu bir yolda bu toplam her router'da tekrarlanır.

### Diğer Temel Metrikler
* **Bant genişliği (Bandwidth):** bir bağlantının saniyede taşıyabileceği maksimum bit sayısı (bps, Mbps, Gbps).
* **Throughput (verim):** bir bağlantı üzerinden gerçekte başarıyla iletilen veri hızı; bant genişliğinden küçük veya eşittir, ağdaki en dar boğaz (bottleneck) tarafından belirlenir.
* **Jitter:** ardışık paketler arasındaki gecikme farkının değişkenliği; özellikle ses/video (VoIP) uygulamalarında kritik bir kalite göstergesidir.
* **Bandwidth-Delay Product (BDP):** Bant genişliği × RTT (Round-Trip Time) — bir bağlantı üzerinde 'aynı anda havada olabilecek' maksimum bit miktarını verir; TCP pencere boyutu optimizasyonunda kullanılır.
* **Paket kaybı oranı (Packet loss rate):** kuyruklar dolduğunda router'ların paketleri atması (drop) sonucu oluşan kayıp yüzdesidir.

---

## 3. Protokoller ve Referans Modelleri
Protokol: cihazlar arası iletişimin kurallarını (sözdizimi/syntax, anlam/semantics, zamanlama/timing) tanımlayan standarttır. Standart kuruluşları: ISO, IEEE, IETF, ITU-T, IANA.

### OSI Referans Modeli vs TCP/IP Modeli
| OSI (7 Katman) | No | TCP/IP (4 Katman) | PDU Adı | Örnek Protokol |
| :--- | :---: | :--- | :--- | :--- |
| **Uygulama** (*Application*) | 7 | Uygulama | Data | HTTP, FTP, DNS, SMTP |
| **Sunum** (*Presentation*) | 6 | Uygulama | Data | SSL/TLS, JPEG, ASCII |
| **Oturum** (*Session*) | 5 | Uygulama | Data | NetBIOS, RPC |
| **Taşıma** (*Transport*) | 4 | Taşıma | Segment | TCP, UDP |
| **Ağ** (*Network*) | 3 | İnternet | Packet | IP, ICMP, OSPF |
| **Veri Bağlantı** (*Data Link*) | 2 | Ağ Erişimi | Frame | Ethernet, PPP, ARP |
| **Fiziksel** (*Physical*) | 1 | Ağ Erişimi | Bit | Kablo, konnektör, sinyal |

> [!NOTE]
> ARP genelde 'Data Link' ile ilişkilendirilir ama teknik olarak Katman 2 ile Katman 3 arasında köprü kuran bir protokoldür (bazı kaynaklar L2.5 der). Sınav sorularında dikkat edilmesi gereken bir ayrıntıdır.

### Veri Kapsülleme (Encapsulation)
Gönderen tarafta veri, her katmanda bir üst katmandan gelen veriye kendi başlığını (header) ekleyerek alt katmana iletir: Data → Segment (L4 header) → Packet (L3/IP header) → Frame (L2 header + trailer) → Bit (fiziksel sinyal). Alıcıda ters işlem (decapsulation) uygulanır. Ara ağ cihazları yalnızca kendi çalıştıkları katmana kadar başlıkları okur (switch → L2, router → L3).

---

## 4. Fiziksel Katman
Görevi: bitleri elektriksel, optik veya radyo sinyallerine çevirip fiziksel ortamda iletmek.
* **Baseband transmission:** sinyal doğrudan sayısal (dijital) olarak iletilir — Ethernet kablolarında kullanılır.
* **Passband transmission:** sinyal modülasyonla bir taşıyıcı frekansa bindirilir — analog/radyo hatlarında kullanılır.
* **Kodlama (Encoding):** bit dizilerini sinyale çevirme teknikleri — Manchester, NRZ, 4B/5B vb.
* **Modülasyon/Demodülasyon:** dijital sinyalin analog taşıyıcıya bindirilmesi/çözülmesi (modem işlevi: AM, FM, PM türleri).
* **Çoklama (Multiplexing):** FDM (frekans bölmeli), TDM (zaman bölmeli), WDM (dalga boyu bölmeli — fiber optikte), CDM (kod bölmeli).

### Kablolama Standartları
* **Bükümlü çift kablo (Twisted Pair):** UTP (kalkansız, ucuz/esnek) ve STP (kalkanlı, parazite dayanıklı); kategoriler Cat5e (1 Gbps), Cat6/6a (10 Gbps), Cat7/8.
* **RJ45 konnektör;** T568A/T568B pin dizilimi — aynı standart iki uçta kullanılırsa 'düz kablo' (straight-through), farklı standartlar kullanılırsa 'çapraz kablo' (crossover); günümüzde Auto-MDIX ile çoğu cihaz otomatik algılar.
* **Fiber optik:** Multi-mode (kısa mesafe ~550m'ye kadar, LED kaynaklı, ucuz), Single-mode (uzun mesafe, 10-100km, lazer kaynaklı, pahalı).
* **Seri kablolar (Serial):** WAN bağlantılarında router-router arası kullanılır.
* **Kablosuz ortamlar:** radyo dalgaları (Wi-Fi, Bluetooth), mikrodalga (uydu, nokta-nokta link), kızılötesi (IR) — mesafe, hız ve engel geçirgenliği farklıdır.

### Kanal Kapasitesi Teoremleri
Bir iletişim kanalının teorik maksimum veri hızını (kapasitesini) belirleyen iki temel teorem, mühendislik müfredatının standart parçasıdır:
* **Nyquist Teoremi (gürültüsüz kanal için):** $C = 2 \times H \times \log_2(V)$ — burada $H$ kanal bant genişliği (Hz), $V$ kullanılan sinyal seviyesi sayısıdır. Gürültüsüz, ideal bir kanalın maksimum bit hızını verir.
* **Shannon Teoremi (gürültülü kanal için):** $C = H \times \log_2(1 + S/N)$ — burada $H$ bant genişliği (Hz), $S/N$ sinyal-gürültü oranıdır (genelde dB cinsinden verilip ondalığa çevrilir). Gerçek dünyadaki (gürültülü) kanalların ulaşabileceği teorik üst sınırı verir; hiçbir kodlama tekniği bu sınırı aşamaz.

#### Çözümlü Sayısal Örnek
Soru: $H = 3000 \text{ Hz}$ bant genişliğine ve $S/N = 30 \text{ dB}$ sinyal-gürültü oranına sahip bir telefon hattının (klasik ses bandı örneği) Shannon kapasitesini hesaplayın.

| Adım | İşlem | Sonuç |
| :---: | :--- | :--- |
| **1** | dB → oran (ondalık S/N) dönüşümü: $\text{dB} = 10 \times \log_{10}(S/N)$ formülü TERSİNE çevrilir → $S/N = 10^{(\text{dB}/10)}$ | $S/N = 10^{(30/10)} = 10^3 = 1000$ |
| **2** | Shannon formülüne yerleştir: $C = H \times \log_2(1 + S/N)$ | $C = 3000 \times \log_2(1 + 1000) = 3000 \times \log_2(1001)$ |
| **3** | $\log_2(1001) \approx 9.97$ (çünkü $2^{10}=1024$, 1001 buna çok yakın) | $C \approx 3000 \times 9.97 \approx 29.910 \text{ bps} \approx \sim 30 \text{ kbps}$ |

**Yorum:** bu, klasik bir telefon hattının (3000 Hz bant genişliği, tipik 30 dB S/N) teorik maksimum veri hızının neden ~33.6-56 kbps'lik eski dial-up modemlerin fiziksel sınırına yakın çıktığını açıklar — Shannon limiti, mühendislerin 'daha hızlı modem' arayışının neden belirli bir noktada fiziksel olarak imkansız hale geldiğini gösteren gerçek bir örnektir.

> [!NOTE]
> $\text{dB} \leftrightarrow \text{oran}$ dönüşüm formülünü ezbere bilmek şart: $\text{dB} = 10 \log_{10}(S/N) \iff S/N = 10^{(\text{dB}/10)}$. Bu iki formül birbirinin tersidir, sınavda hangi yönde soru geldiğine (dB verilip oran mı isteniyor, yoksa tam tersi mi) dikkat edin.  
> Bu iki formül sınavlarda sıkça sayısal soru olarak çıkar (örn. H=3000 Hz, S/N=30dB olan bir kanalın kapasitesini hesaplayın). Pratik ağ kurulumunda doğrudan kullanılmasa da, iletişim teorisinin temelini oluşturduğu için mühendislik müfredatının vazgeçilmez bir parçasıdır.

---

## 5. Veri Bağlantı Katmanı (Data Link Layer)
Görevleri: çerçeveleme (framing), hata tespiti/düzeltme, ortam erişim kontrolü (MAC), fiziksel adresleme.

### Çerçeveleme (Framing) Teknikleri
Veri bağlantı katmanı, fiziksel katmandan gelen ham bit akışını nereden nereye kadar bir çerçeve olduğunu anlayacak şekilde bölmelidir (framing). Bunun için kullanılan klasik yöntemler:
* **Karakter Sayımı (Character Count):** çerçevenin başına, çerçevenin toplam uzunluğunu belirten bir sayı eklenir. Basit ama kırılgandır — bu sayı alanı iletim sırasında bozulursa (bit hatası), alıcı çerçeve sınırını tamamen kaybeder ve senkronizasyon bozulur; bu yüzden günümüzde tek başına pek kullanılmaz.
* **Byte Stuffing (Byte Doldurma):** çerçevenin başına ve sonuna özel bir FLAG byte'ı (ör. 0x7E) konur. Veri içinde tesadüfen FLAG ile aynı byte geçerse, alıcının bunu çerçeve sonu sanmaması için önüne bir ESC (kaçış) byte'ı eklenir (stuffing); alıcı ESC gördüğünde bir sonraki byte'ı 'veri' olarak okur ve ESC'yi kendisi çıkarır (destuffing).
  * *Not:* PPP protokolü, iletim ortamına göre İKİ FARKLI yöntem kullanır: asenkron hatlarda (ör. eski modem bağlantıları) 0x7D kaçış (escape) byte'ı ile klasik byte stuffing uygulanır; senkron hatlarda (ör. router-router seri bağlantılar) ise HDLC'ye benzer BIT stuffing kullanılır. Yani 'PPP = byte stuffing' demek eksik bir genelleme olur — hangi iletim modunda çalıştığına bağlıdır.
* **Bit Stuffing (Bit Doldurma):** FLAG deseni bit dizisi olarak tanımlanır (ör. HDLC'de 01111110 — altı ardışık 1). Veri içinde art arda 5 tane '1' biti geldiğinde, gönderici otomatik olarak aradan bir '0' biti ekler (stuff); alıcı, art arda 5 '1' gördükten sonra gelen '0'ı otomatik siler. Böylece veri içinde FLAG deseninin kazara oluşması engellenir. HDLC ve Ethernet'in bazı alt katmanlarında kullanılır.
* **Fiziksel Katman Kodlama İhlali (Physical Layer Coding Violations):** bazı hat kodlama şemalarında (ör. Manchester encoding), her bit belirli bir sinyal geçişiyle temsil edilir; çerçeve sınırını belirtmek için normalde 'geçersiz/kullanılmayan' bir sinyal deseni kasıtlı olarak kullanılır. Ethernet'in bazı eski fiziksel katman varyantlarında görülür.

### Hata Tespiti ve Hata Düzeltme — Ayrım ve Hamming Kodu
Tanenbaum'un net ayrımı: Hata Tespiti (Error Detection), hatanın VARLIĞINI anlamayı sağlar (ne olduğunu değil); Hata Düzeltme (Error Correction), hatanın YERİNİ bulup veriyi yeniden gönderime gerek kalmadan düzeltmeyi sağlar.
* **Parity Check (Eşlik Biti):** veriye, toplam '1' bit sayısını çift (even parity) veya tek (odd parity) yapacak şekilde tek bir bit eklenir. Yalnızca TEK bit hatasını tespit edebilir (çift sayıda hata gözden kaçar); hatayı DÜZELTEMEZ, yalnızca 'bir hata var' der.
* **CRC (Cyclic Redundancy Check):** veri, sabit bir 'jeneratör polinomuna' bölünür, kalan (remainder) çerçeveye eklenir; alıcı aynı işlemi tekrarlayıp kalan sıfır çıkmazsa hatayı tespit eder. Çok daha güçlü bir tespit yöntemidir (ardışık/burst hataları da yakalar) ama YİNE DE yalnızca tespit eder, düzeltmez — hata bulunursa çerçeve atılır ve yeniden gönderim (retransmission, ör. ARQ mekanizmalarıyla) istenir.
* **Hamming Kodu (Hamming Code) — Hata DÜZELTME:** veri bitleri arasına belirli konumlara (2'nin kuvveti olan pozisyonlara: 1, 2, 4, 8...) eşlik (parity) bitleri yerleştirilir; her parity biti, verinin belirli bir alt kümesini kontrol eder. Alıcı tarafında bu parity bitleri tekrar hesaplanıp bir 'sendrom' (syndrome) oluşturulur — sendromun ikili değeri, DOĞRUDAN hatalı bitin POZİSYONUNU verir, böylece tek bitlik hatalar yeniden gönderime gerek kalmadan düzeltilebilir.
* **Hamming Mesafesi (Hamming Distance):** iki geçerli kod kelimesi arasındaki farklı bit sayısıdır. $d$ hamming mesafesine sahip bir kodlama şeması, $d-1$ bitlik hataları tespit edebilir ve $\lfloor (d-1)/2 \rfloor$ bitlik hataları düzeltebilir — bu formül, kaç bitlik hataya karşı ne kadar koruma sağlandığını hesaplamak için kullanılır.
* **Ne zaman hangisi kullanılır:** Kablolu ağlarda (Ethernet, TCP/IP) genelde yalnızca TESPİT (CRC) yeterlidir çünkü yeniden gönderim (retransmission) ucuz ve hızlıdır. Hata düzeltme (Hamming, veya daha gelişmiş Reed-Solomon/Turbo kodları) genelde yeniden göndermenin pahalı/yavaş olduğu ortamlarda tercih edilir: uydu iletişimi, derin uzay haberleşmesi, bellek (RAM/ECC), CD/DVD gibi depolama ortamları.

> [!TIP]
> Sınavda sık sorulan tip soru: 'Hamming mesafesi 4 olan bir kod, kaç bitlik hatayı tespit/düzeltebilir?'  
> $\rightarrow$ Tespit: $d-1 = 3 \text{ bit}$; Düzeltme: $\lfloor (d-1)/2 \rfloor = 1 \text{ bit}$. Bu formülü ezbere bilmek gerekir.

### Ortam Erişimi ve Adresleme
* **MAC Adresi:** 48 bit (6 byte), donanıma gömülü, dünya çapında (teorik olarak) tekildir. İlk 24 bit üretici kodu (OUI), son 24 bit seri numarasıdır. IP adresinden farkı: MAC fiziksel/sabittir (Katman 2), IP mantıksaldır ve değişebilir (Katman 3).
* **Çerçeve türleri:** Unicast (tek alıcı), Broadcast (FF:FF:FF:FF:FF:FF), Multicast (belirli bir gruba, 01:00:5E ile başlar).
* **CSMA/CD:** klasik yarı-çift-yönlü (half-duplex) Ethernet'te çarpışma tespiti için kullanılırdı; tam-çift-yönlü (full-duplex) switch bağlantılarında artık gerekli değildir. Kablosuz ağlarda benzer amaçla CSMA/CA (Collision Avoidance) kullanılır.

### Ethernet Çerçeve Formatı
`Preamble (8 byte)` | `Hedef MAC (6 byte)` | `Kaynak MAC (6 byte)` | `Tip/Uzunluk-EtherType (2 byte)` | `Data (46–1500 byte, MTU)` | `FCS/CRC (4 byte)`

---

## 6. Switch Temelleri
* **Çarpışma Alanı (Collision Domain):** aynı anda yalnızca bir cihazın gönderim yapabildiği segment; her switch portu ayrı bir çarpışma alanıdır.
* **Yayın Alanı (Broadcast Domain):** broadcast trafiğinin ulaştığı sınır; switch broadcast domain'i bölmez (VLAN ile bölünebilir), router her arayüzünde ayrı bir broadcast domain oluşturarak böler.
* **MAC Adres Tablosu:** switch, port $\leftrightarrow$ MAC eşleşmelerini tutar; kayıtlar belirli bir süre (aging time, genelde ~300 sn) kullanılmazsa silinir.
* **Switch'in 3 temel davranışı:** Flooding (hedef MAC bilinmiyorsa tüm portlara gönderme), Forwarding (hedef MAC biliniyorsa ilgili porta iletme), Discarding (gerekmeyen trafiği atma).
* **MAC öğrenme (self-learning):** switch, gelen çerçevenin kaynak MAC adresini geldiği portla ilişkilendirip tabloya kaydeder.

---

## 7. VLAN ve Trunk
* **VLAN (Virtual LAN):** fiziksel ağı mantıksal olarak alt ağlara bölerek broadcast domain'i küçültür, güvenliği ve yönetilebilirliği artırır.
* **VLAN Tag (IEEE 802.1Q):** Ethernet çerçevesine eklenen 4 byte'lık etiket; TPID (2 byte, 0x8100) + TCI (2 byte — Priority/3 bit, CFI/1 bit, VLAN ID/12 bit). VLAN ID teorik olarak 0–4095, ama 0 ve 4095 rezerve; kullanılabilir aralık 1–4094'tür.
* **VLAN atama modları:** Interface (port) tabanlı — en yaygın — ve MAC adresi tabanlı.

### Arayüz (Port) Türleri
* **Access:** tek bir VLAN'a ait, genelde son kullanıcı cihazına bağlanır; çerçeveler tag'siz (untagged) gönderilir.
* **Trunk:** birden fazla VLAN trafiğini taşır (switch-switch bağlantısı); çerçeveler tag'li (tagged) gönderilir. 'Native VLAN' — trunk üzerinde tag'siz gönderilen tek VLAN'dır, genelde yönetim VLAN'ı için kullanılır.
* **Hybrid:** hem tag'li hem tag'siz çerçeve gönderebilen esnek port tipi (bazı üreticilerin CLI'sinde ayrı mod olarak, bazılarında farklı komutlarla sağlanır).

---

## 8. STP (Spanning Tree Protocol) Ailesi
Amaç: switch'ler arası yedekli (redundant) fiziksel bağlantılardan doğabilecek Katman 2 döngülerini (loop) önlemek. Döngüler; broadcast storm, çerçevenin birden çok kopyasının alınması ve MAC tablosu kararsızlığı gibi ciddi sorunlara yol açar.

### Temel Kavramlar
* **BID (Bridge ID):** köprü önceliği (priority) + MAC adresinden oluşur; en düşük BID'e sahip switch Root Bridge seçilir.
* **Cost:** bağlantı hızına göre hesaplanan maliyet (yüksek hız = düşük cost); RPC (Root Path Cost) kök köprüye olan toplam maliyettir.
* **BPDU (Bridge Protocol Data Unit):** switch'lerin topoloji bilgisini birbirine göndermek için kullandığı özel paket.
* **Port rolleri:** Root Port (en düşük maliyetle köke giden port), Designated Port (bir segmentte iletim yapan port), Blocking/Alternate Port (döngüyü önlemek için trafiği durduran port).

### STP Sürüm Karşılaştırması
| Sürüm | Standart | Yakınsama | Ayırt Edici Özellik |
| :--- | :--- | :--- | :--- |
| **STP (klasik)** | IEEE 802.1D | ~30–50 sn (yavaş) | Port durumları: Blocking → Listening → Learning → Forwarding |
| **RSTP** | IEEE 802.1w | Saniyeler (hızlı) | Edge Port; Alternate/Backup port rolleri; durumlar Discarding/Learning/Forwarding olarak sadeleşir |
| **MSTP** | IEEE 802.1s | RSTP kadar hızlı | VLAN'ları örneklere (instance) gruplayarak yük dengeleme sağlar |

---

## 9. Link Aggregation (Bağlantı Birleştirme / LAG)
Amaç: bant genişliğini artırmak ve yedeklilik sağlamak — birden fazla fiziksel bağlantıyı tek mantıksal bağlantı gibi kullanmak. IEEE standardı: 802.3ad / LACP (Link Aggregation Control Protocol).
* **Manuel (statik) mod:** yük dengeleme yapılır ama otomatik negotiation/yedeklilik yoktur.
* **LACP modu:** dinamik ve otomatik; sistem/arayüz önceliğine göre aktif-pasif bağlantı seçimi yapılır.
* **Load Balancing:** trafiği kaynak/hedef MAC, IP gibi kriterlere (hash algoritması) göre bağlantılar arasında dağıtır.

> [!NOTE]
> Üreticiye göre isimlendirme değişir: IEEE/genel terim **'LAG (Link Aggregation Group)'**, Cisco'da **'EtherChannel/Port-Channel'**, Huawei'de **'Eth-Trunk'** olarak geçer — kavram aynıdır.

---

## 10. Ağ Katmanına Giriş: Devre/Paket Anahtarlama ve Router Mimarisi

### Devre Anahtarlama vs Paket Anahtarlama (Circuit vs Packet Switching)
* **Devre Anahtarlama (Circuit Switching):** iletişim öncesi uçtan uca sabit bir kaynak (bant genişliği, zaman dilimi) ayrılır ve bağlantı boyunca yalnızca bu iki taraf kullanır — klasik telefon şebekesi mantığı. Kaynak rezervasyonu FDM (frekans bölmeli) veya TDM (zaman bölmeli) ile yapılabilir. Avantajı: garantili, sabit performans. Dezavantajı: kaynak kullanılmasa bile (sessizlik anlarında bile) ayrılmış durumda kalır — verimsizdir.
* **Paket Anahtarlama (Packet Switching):** veri küçük paketlere bölünür, her paket ağ üzerinde bağımsız olarak, o an müsait olan yoldan iletilir (store-and-forward — her router paketi tamamen alıp sonra iletir); kaynaklar paylaşılır (statistical multiplexing). İnternet bu mantıkla çalışır. Avantajı: kaynak kullanımı verimlidir. Dezavantajı: değişken gecikme (jitter) ve tıkanıklık riski vardır.

### Ağ Katmanında İki Hizmet Modeli
* **Sanal Devre Ağları (Virtual Circuit / VC Networks):** paket anahtarlamalı olmasına rağmen, iletişim öncesi mantıksal bir 'yol' (VC) kurulur ve tüm paketler bu VC kimliğini taşıyarak aynı yoldan gider — ATM ve Frame Relay gibi eski WAN teknolojilerinde kullanılırdı; router'lar her VC için durum (state) bilgisi tutar.
* **Veri Paketi (Datagram) Ağları — İnternet'in modeli:** her paket (datagram) bağımsız olarak, kendi hedef IP adresine göre yönlendirilir; router'lar bağlantı durumu tutmaz, her paketi 'bağlamsız' (connectionless) olarak, o anki routing tablosuna göre iletir. Bu yüzden aynı iki nokta arasındaki farklı paketler farklı yollardan gidebilir.

### Router İç Mimarisi
Bir router, kavramsal olarak 4 temel bileşenden oluşur:
1. **Giriş portları (Input ports):** gelen fiziksel sinyali alır, veri bağlantı katmanı işlemlerini (çerçeve çözme) yapar, paket başlığını inceleyip hangi çıkış portuna gideceğine karar vermek için forwarding tablosuna bakar (lookup).
2. **Switching fabric (anahtarlama yapısı):** giriş portlarından gelen paketleri doğru çıkış portlarına 'içeride' taşıyan donanımdır; farklı mimarileri olabilir (paylaşımlı bellek, paylaşımlı veri yolu/bus, crossbar).
3. **Çıkış portları (Output ports):** paketi bekletir (kuyruklama — burada queuing delay oluşur), sıra kendine geldiğinde veri bağlantı katmanı işlemlerini yapıp fiziksel katmana iletir.
4. **Yönlendirme işlemcisi (Routing processor):** kontrol düzlemi (control plane) işlerini yürütür — routing protokollerini (OSPF, BGP vb.) çalıştırır, forwarding tablosunu hesaplayıp günceller. Bu, her paket için değil, topoloji değiştiğinde çalışır (paket başına giriş portlarındaki hızlı 'forwarding' işleminden farklıdır).

> [!NOTE]
> Forwarding (yönlendirme/iletme) ile Routing (rota belirleme) kavramları sıkça karıştırılır: Forwarding, bir paketi router'ın giriş portundan doğru çıkış portuna taşıma işidir (hızlı, donanım destekli, her paket için); Routing ise routing tablosunun nasıl oluşturulacağına karar verme sürecidir (protokoller aracılığıyla, arka planda çalışır).

---

## 11. IPv4 Adresleme ve Subnetting
IPv4 adresi 32 bit uzunluğundadır, 4 oktet halinde noktalarla ayrılmış ondalık gösterimle yazılır (ör. 192.168.1.1).

| Sınıf | İlk Bit(ler) | Aralık | Varsayılan Maske | Kullanım |
| :---: | :---: | :--- | :--- | :--- |
| **A** | 0 | 1–126 | /8 (255.0.0.0) | Çok büyük ağlar |
| **B** | 10 | 128–191 | /16 (255.255.0.0) | Orta ölçekli ağlar |
| **C** | 110 | 192–223 | /24 (255.255.255.0) | Küçük ağlar |
| **D** | 1110 | 224–239 | — | Multicast |
| **E** | 1111 | 240–255 | — | Deneysel/rezerve |

127.0.0.0/8 loopback için, 169.254.0.0/16 APIPA (otomatik özel IP, DHCP alınamadığında) için ayrılmıştır.

### Subnetting
Subnetting: büyük bir ağı daha küçük alt ağlara bölme işlemidir. Ödünç alınan (borrowed) bitlerle subnet sayısı, kalan bitlerle host sayısı hesaplanır.  
Kullanılabilir host sayısı: $2^n − 2$ ($n$ = host bit sayısı). İki adres (network ve broadcast) çıkarılır.

> [!NOTE]
> İstisna: /31 subnet (2 adres), point-to-point WAN bağlantılarında RFC 3021 gereği network/broadcast adresi ayırmadan her iki adres de host olarak kullanılabilir. /32 tek bir host/loopback adresini belirtir.

#### Çözümlü VLSM Örneği
Senaryo: 192.168.10.0/24 bloğu elimizde var. Üç farklı bölüme şu host sayıları gerekiyor: Bölüm A = 60 host, Bölüm B = 25 host, Bölüm C = 2 host (ör. router-router point-to-point bağlantı). VLSM ile her bölüme TAM İHTİYACI KADAR (ne fazla ne eksik) blok ayıracağız — bu, sabit boyutlu subnetting'e göre adres israfını önler.

| Adım | İşlem | Sonuç |
| :---: | :--- | :--- |
| **1** | İhtiyaçları büyükten küçüğe sırala (VLSM'de her zaman en büyük ihtiyaçla başlanır) | A(60) > B(25) > C(2) |
| **2** | A için: 60 host'u karşılayacak en küçük host-bit sayısını bul → $2^6−2=62 \ge 60$ ($2^5−2=30$ yetersiz) → 6 host biti gerekir → $32−6=26$ → /26 kullan | A = 192.168.10.0/26 (adres aralığı: .0–.63, kullanılabilir host: .1–.62, broadcast: .63) |
| **3** | B için: bir sonraki müsait bloktan devam et (.64'ten). 25 host için $2^5−2=30 \ge 25$ ($2^4−2=14$ yetersiz) → 5 host biti → /27 kullan | B = 192.168.10.64/27 (adres aralığı: .64–.95, kullanılabilir host: .65–.94, broadcast: .95) |
| **4** | C için: bir sonraki müsait bloktan devam et (.96'dan). Point-to-point bağlantı = 2 host → $2^2−2=2$ tam yeterli → 2 host biti → /30 kullan | C = 192.168.10.96/30 (adres aralığı: .96–.99, kullanılabilir host: .97–.98, broadcast: .99) |
| **5** | Kalan adresler (192.168.10.100 – .255) ileride kullanılmak üzere ayrılmış/boşta kalır | İleride yeni bir bölüm eklenirse buradan devam edilir |

> [!NOTE]
> VLSM'in temel mantığı: HER ZAMAN en büyük ihtiyaçtan başlayıp, bir önceki bloğun bittiği adresten devam ederek küçük ihtiyaçlara doğru ilerlemektir. Sabit boyutlu (ör. hepsine /26) subnetting yapılsaydı, C bölümü (2 host) için de 62 adreslik bir blok harcanır, adres israfı olurdu — VLSM tam da bunu önler.

### Özel Adres Blokları (RFC 1918)
* `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16` — private (özel) adresler, internete doğrudan yönlendirilmez.
* `127.0.0.0/8` — loopback; `169.254.0.0/16` — APIPA/link-local; `255.255.255.255` — sınırlı broadcast.

### IPv4 Paket Başlığı (Header) Alanları
| Alan | Boyut | İşlevi |
| :--- | :---: | :--- |
| **Version** | 4 bit | IP sürümü (IPv4 için değeri 4) |
| **Header Length (IHL)** | 4 bit | Başlığın uzunluğu (options alanı değişken olduğu için gereklidir) |
| **Type of Service (ToS/DSCP)** | 8 bit | QoS önceliklendirmesi için kullanılır |
| **Total Length** | 16 bit | Başlık + veri toplam uzunluğu (byte) |
| **Identification** | 16 bit | Aynı orijinal pakete ait parçaları (fragment) birbirine bağlamak için ortak kimlik |
| **Flags** | 3 bit | DF (Don't Fragment) ve MF (More Fragments) bitlerini içerir |
| **Fragment Offset** | 13 bit | Bu parçanın, orijinal paket içindeki konumu |
| **TTL (Time To Live)** | 8 bit | Her router'da 1 azalır; 0 olunca paket atılır — sonsuz döngüleri önler |
| **Protocol** | 8 bit | Üst katman protokolünü belirtir (TCP=6, UDP=17, ICMP=1 gibi) |
| **Header Checksum** | 16 bit | Yalnızca başlığın hata kontrolü (veri kısmı dahil değildir) |
| **Source / Destination Address**| 32+32 bit | Kaynak ve hedef IP adresleri |

### IP Fragmentation (Paket Parçalanması)
Bir paket, geçtiği bir bağlantının MTU (Maximum Transmission Unit) değerinden büyükse, router tarafından daha küçük parçalara bölünür (fragmentation); Identification alanı aynı kalır, Fragment Offset ile parçaların sırası belirlenir. Parçalar genellikle yeniden birleştirme (reassembly) işlemini ancak hedef host yapar (ara router'lar yapmaz) — bu da IPv4'te fragmentation'ın performans maliyetlerinden biridir. IPv6'da router'lar fragmentation yapmaz; bu iş kaynağa bırakılmıştır (Path MTU Discovery ile önceden öğrenilir).

### CIDR (Classless Inter-Domain Routing) — Detay
CIDR, IP adreslerinin A/B/C sınıf sınırlarına bağlı kalmadan, herhangi bir bit uzunluğunda (prefix) bloklara ayrılmasını sağlayan gösterimdir; 'a.b.c.d/n' notasyonu kullanılır (n = ağ kısmının bit sayısı).
* **Amaç 1 — Adres israfını önleme:** Sınıflı (classful) sistemde bir şirkete 500 host için ya /24 (254 host, yetersiz) ya da /16 (65534 host, çoğu boşa gider) verilebilirdi; CIDR ile tam ihtiyaca göre (/23 = 510 host gibi) blok ayrılabilir.
* **Amaç 2 — Route Aggregation (Route Summarization/Süpernetting):** birden fazla ardışık küçük ağ, tek bir büyük CIDR bloğunda özetlenerek routing tablolarındaki satır sayısı azaltılır (ör. 192.168.0.0/24 ve 192.168.1.0/24 → 192.168.0.0/23 olarak tek satırda özetlenebilir). Bu, İnternet'in routing tablolarının patlamasını (routing table explosion) önleyen temel mekanizmalardan biridir.
* **VLSM (Variable Length Subnet Masking):** CIDR mantığının subnetting'e uygulanmış hali — aynı büyük ağ bloğu içinde, ihtiyaca göre FARKLI boyutlarda alt ağlar (ör. bir bölüme /26, başka bir bölüme /29) oluşturulabilmesidir; sabit boyutlu subnetting'e göre çok daha verimlidir.

---

## 12. Yönlendirme (Routing) Temelleri
Router, farklı ağlar (subnet) arasında IP paketlerini en uygun yol üzerinden ileten Katman 3 cihazıdır.
* **Routing table:** hedef ağ, next-hop, çıkış arayüzü, metrik ve öncelik (preference/administrative distance) bilgilerini tutar.
* **Longest match (en uzun eşleşme) kuralı:** bir paket için birden fazla rota eşleşiyorsa, en spesifik (en uzun prefix) rota tercih edilir.
* **ARP (Address Resolution Protocol):** bilinen bir IP adresine karşılık gelen MAC adresini bulmak için kullanılır (broadcast ARP request → unicast ARP reply); sonuç ARP tablosunda (cache) önbelleğe alınır.
* **ICMP (Internet Control Message Protocol):** hata bildirimi ve tanılama için kullanılır — ping (Echo Request/Reply), tracert/traceroute (TTL azaltılarak yol izleme).

### Statik ve Dinamik Rota Karşılaştırması
| Özellik | Statik Rota | Dinamik Rota |
| :--- | :--- | :--- |
| **Yapılandırma** | Yönetici tarafından elle girilir | Protokol otomatik öğrenir |
| **CPU/Bant genişliği yükü** | Yok/çok az | Var (protokol mesajları) |
| **Topoloji değişikliğine uyum** | Manuel müdahale gerekir | Otomatik (yeniden yakınsama) |
| **Uygun ağ boyutu** | Küçük/basit ağlar | Orta-büyük, karmaşık ağlar |

Default route: 0.0.0.0/0 — routing tablosunda başka bir rota eşleşmediğinde kullanılan 'her şeyi kapsayan' rotadır.

### Administrative Distance / Route Preference
Aynı hedef ağa birden fazla protokolden rota öğrenildiğinde hangisinin tabloya gireceğini belirleyen değerdir; düşük değer = daha güvenilir. Bu değerler ÜRETİCİYE ÖZGÜDÜR, standart değildir — örnek genel sıralama: doğrudan bağlı (direct) < statik < link-state protokoller (OSPF, IS-IS) < distance-vector protokoller (RIP). Kullandığınız platformun (Cisco/Huawei/Juniper) belgelerinden tam sayısal değerleri ayrıca öğrenmeniz gerekir.

---

## 13. Dinamik Yönlendirme Protokolleri

### Yönlendirme Algoritmalarının Matematiksel Temeli
RIP ve OSPF'in arkasındaki iki klasik graf algoritması, mühendislik müfredatının standart konusudur:
* **Bellman-Ford Algoritması (Distance-Vector protokollerin temeli, ör. RIP):** her düğüm yalnızca doğrudan komşularıyla bilgi paylaşır ('komşuma göre dünya nasıl görünüyor'); her düğüm kendi mesafe tablosunu komşularından aldığı bilgiyle güncelleyerek zamanla (iteratif olarak) en kısa yola yakınsar. Dağıtık (distributed) ve asenkron çalışabilir, ama yakınsama yavaş olabilir ve 'count-to-infinity' gibi döngü problemlerine açıktır (bu yüzden split horizon/poison reverse gerekir).
* **Dijkstra Algoritması / SPF (Link-State protokollerin temeli, ör. OSPF):** her düğüm önce TÜM ağın topolojisini öğrenir (LSA'lar aracılığıyla, her düğüm kendi bağlantılarını tüm ağa duyurur — flooding), sonra kendi başına, merkezi bir hesaplama gibi, kendisinden tüm diğer düğümlere en kısa yolu hesaplar. Çalışma mantığı: başlangıç düğümünden başlanır, her adımda ziyaret edilmemiş düğümler arasından en düşük maliyetli olan seçilip 'kesinleşmiş' kümeye eklenir, komşularının maliyetleri güncellenir — bu N adım (N=düğüm sayısı) tekrarlanır. Daha hızlı yakınsar ama her düğümün tüm topolojiyi bilmesi ve hesaplaması gerektiğinden CPU/bellek yükü daha fazladır.

| Özellik | Bellman-Ford (Distance-Vector) | Dijkstra (Link-State) |
| :--- | :--- | :--- |
| **Kullanan protokol** | RIP | OSPF, IS-IS |
| **Bilgi paylaşımı** | Sadece komşularla, periyodik | Tüm ağa flooding, değişiklikte |
| **Her düğüm ağın tamamını bilir mi?** | Hayır, yalnızca 'komşuma göre mesafe' | Evet, tam topoloji (LSDB) |
| **Yakınsama hızı** | Yavaş | Hızlı |
| **Döngü riski** | Var (count-to-infinity) | Yok (tam topoloji bilindiği için) |

### RIP (Routing Information Protocol)
* Distance-vector (mesafe-vektör) tabanlı; metrik hop count, maksimum 15 hop — 16 = ulaşılamaz (infinity).
* RIPv1: classful, broadcast ile güncelleme, VLSM/CIDR desteklemez. RIPv2: classless (VLSM/CIDR destekler), multicast (224.0.0.9), authentication destekler.
* Döngü önleme: split horizon, poison reverse, triggered updates.
* Küçük/orta ölçekli ağlar için uygundur; büyük ağlarda yavaş yakınsama nedeniyle önerilmez.

### OSPF (Open Shortest Path First)
* Link-state tabanlı; Dijkstra/SPF algoritması ile en kısa yol hesaplanır. Metrik: cost (varsayılan olarak referans bant genişliği / arayüz bant genişliği ile hesaplanır).
* Temel kavramlar: Router ID, Hello/Dead interval, LSA (Link State Advertisement), LSDB (Link State Database), komşuluk durumları (Down → Init → 2-Way → ExStart → Exchange → Loading → Full).
* DR/BDR: broadcast/NBMA ortamlarda (ör. Ethernet) LSA trafiğini azaltmak için seçilir.
* Multi-Area OSPF: büyük ağları alanlara (Area) bölerek LSDB boyutu ve hesaplama yükünü azaltır; Area 0 (backbone) zorunludur. ABR alanlar arasında, ASBR OSPF dışından öğrenilen rotaları taşır.
* OSPFv3: OSPF'in IPv6 üzerinde çalışan versiyonu; temel mantık aynıdır.

> [!NOTE]
> Yapılandırma mantığı (genel, platformdan bağımsız akış): OSPF process başlat → ilgili alanı (area) tanımla → dahil edilecek ağları wildcard mask (subnet mask'in bit-tersi, ör. /24 → 0.0.0.255) ile belirt. Tam komut sözdizimi kullandığınız cihaza göre değişir.

### BGP (Border Gateway Protocol)
RIP ve OSPF birer IGP'dir (Interior Gateway Protocol — bir Otonom Sistem/AS içinde çalışır). BGP ise İnternet'in omurgasını oluşturan tek EGP'dir (Exterior Gateway Protocol — AS'lar/farklı organizasyonlar ARASINDA çalışır).
* **AS (Autonomous System):** tek bir yönetim otoritesi altındaki (ör. bir İSS, bir üniversite, bir büyük şirket) IP ağları topluluğu; her AS'a küresel olarak tekil bir AS numarası (ASN) atanır.
* **Neden IGP yeterli değil:** OSPF gibi link-state protokoller, tüm ağın topolojisini her düğümde tutar — bu, İnternet ölçeğinde (milyonlarca rota) hesaplama açısından imkansız hale gelir. BGP bunun yerine 'path vector' yaklaşımı kullanır: her AS, bir hedefe giden yolu, üzerinden geçtiği AS'ların listesi (AS-PATH) olarak komşularına duyurur.
* **eBGP (external BGP):** farklı AS'lar arasında çalışır — İSS'ler birbirleriyle bu şekilde konuşur. **iBGP (internal BGP):** aynı AS içindeki router'lar arasında BGP bilgisini tutarlı tutmak için kullanılır.
* **Rota seçimi metrik değil POLİTİKA tabanlıdır:** BGP, OSPF gibi 'en kısa/en düşük maliyetli' yolu seçmez; ticari anlaşmalara dayalı politikalarla (ör. 'müşteri AS'lerimin rotalarını herkese duyur, ama bir rakip İSS'den öğrendiğimi başka bir rakibe duyurma') rota seçer. Bu, BGP'yi diğer routing protokollerinden temelden ayıran en önemli özelliktir.
* BGP, TCP üzerinde çalışır (port 179) — bu da onu diğer routing protokollerinden (genelde doğrudan IP veya UDP üzerinde çalışırlar) ayıran bir başka özelliktir.

> [!NOTE]
> Sınavda sık sorulan ayrım: IGP (RIP, OSPF, IS-IS) = AS İÇİNDE, teknik metriğe göre; EGP (BGP) = AS'LAR ARASINDA, iş/politika kurallarına göre çalışır. 'İnternet neden tek bir dev OSPF ağı değil de binlerce AS'a bölünmüş' sorusunun cevabı da bu ölçeklenebilirlik sorunudur.

---

## 14. Inter-VLAN Routing (VLAN'lar Arası Yönlendirme)
VLAN'lar birbirinden izole olduğu için (ayrı broadcast domain), aralarında iletişim ancak bir Katman 3 cihaz üzerinden mümkündür.
* **Router-on-a-Stick (one-armed routing):** router üzerinde tek fiziksel arayüz kullanılır, alt arayüzler (sub-interface) ile her VLAN için ayrı IP/gateway tanımlanır. Basit ama tüm trafiği tek fiziksel bağlantıdan geçirdiği için darboğaz oluşturabilir.
* **Layer 3 Switching (sanal VLAN arayüzü):** L3 switch üzerinde her VLAN için sanal bir arayüz (Cisco'da SVI, bazı üreticilerde VLAN Interface olarak adlandırılır) tanımlanarak yönlendirme yapılır — daha performanslı, günümüzde en yaygın yöntemdir.

---

## 15. IPv6
IPv6 adresi 128 bit uzunluğundadır, 8 grup halinde 16'lık (hexadecimal) sayılarla gösterilir. Ardışık sıfır grupları çift nokta (::) ile bir kez kısaltılabilir; baştaki sıfırlar tek grup içinde atlanabilir.
* **Adres türleri:** Unicast, Multicast, Anycast — IPv6'da broadcast yoktur, yerine multicast kullanılır.
* **NDP (Neighbor Discovery Protocol):** IPv6'da ARP'ın yerini alan; komşu/adres çözümleme ve otomatik adresleme (SLAAC — Stateless Address Autoconfiguration) sağlar.
* **IPv4'e göre avantajlar:** çok daha büyük adres uzayı ($2^{128}$), basitleştirilmiş sabit uzunluklu başlık, yerleşik güvenlik desteği (IPSec), NAT'a ihtiyacın azalması.

---

## 16. Taşıma Katmanı: TCP ve UDP
Görevi: uçtan uca (end-to-end) iletişim sağlamak, port numaraları ile uygulamaları ayırt etmek (0–1023 well-known, 1024–49151 registered, 49152–65535 dynamic/private). Ayrıca 'multiplexing/demultiplexing' işlevini görür: gönderen tarafta farklı uygulamalardan gelen veriler tek bir ağ katmanı akışında birleştirilir (multiplex), alıcı tarafta port numarasına bakılarak doğru uygulamaya dağıtılır (demultiplex).

### Güvenilir Veri Transferi Prensipleri
TCP'nin 'güvenilir' olmasının ardında, bilgisayar ağları teorisinin klasik bir konusu olan güvenilir veri transferi (reliable data transfer) algoritmaları yatar:
* **Stop-and-Wait:** gönderici bir paket gönderir, ACK (onay) gelene kadar bekler, sonra bir sonrakini gönderir. Basit ama çok verimsizdir (bağlantı çoğu zaman boşta bekler).
* **Sliding Window (Kayan Pencere):** gönderici, ACK beklemeden art arda birden fazla paket gönderebilir ('pencere' büyüklüğü kadar); bu, bağlantıyı çok daha verimli kullanır ve TCP'nin temel mekanizmasıdır.
* **Go-Back-N (GBN):** pencere içinde bir paket kaybolursa, alıcı o paketten sonraki TÜM paketleri reddeder; gönderici kaybolan paketten itibaren her şeyi yeniden gönderir. Basit ama verimsiz olabilir.
* **Selective Repeat (SR):** alıcı, sırası bozuk gelen ama doğru alınan paketleri saklar (buffer); yalnızca gerçekten kaybolan/hatalı paket yeniden gönderilir. Daha verimli ama alıcı tarafında daha karmaşık buffer yönetimi gerektirir.

> [!NOTE]
> TCP, kavramsal olarak Sliding Window + Selective Repeat'e yakın bir hibrit mekanizma kullanır (kümülatif ACK + Selective ACK/SACK seçeneği ile).

### TCP (Transmission Control Protocol)
Bağlantı odaklı, güvenilir, sıralı teslimat; akış kontrolü (flow control) ve tıkanıklık kontrolü (congestion control) içerir.
* **3-way handshake:** SYN → SYN-ACK → ACK.
* **Bağlantı sonlandırma TEORİK olarak** 4 bağımsız segmentle anlatılır: FIN → ACK → FIN → ACK (her taraf kendi yönünü ayrı ayrı kapatır, TCP'nin 'half-close' özelliği). **PRATİKTE ise** pasif kapatan taraf genelde kendi ACK'i ile kendi FIN'ini TEK bir pakette birleştirir (FIN+ACK), bu durumda sonlandırma 3 segmentte tamamlanır: FIN → (ACK+FIN birleşik) → ACK. Sınav sorularında '4 adım' teorik/maksimum durumu, '3 adım' ise pratikte sıkça görülen optimize edilmiş durumu ifade eder — ikisi de doğrudur, hangisinin sorulduğuna dikkat edin.

### TCP ve UDP Başlık (Header) Formatları
IPv4 header'ı zaten detaylı verildi (bkz. Ağ Katmanı bölümü); TCP ve UDP header'ları da aynı titizlikte bilinmelidir, özellikle TCP flag bitleri sınavlarda sık sorulur.

| TCP Alanı | Boyut | İşlevi |
| :--- | :---: | :--- |
| **Source / Destination Port** | 16+16 bit | Kaynak ve hedef port numaraları |
| **Sequence Number** | 32 bit | Bu segmentteki ilk byte'ın sıra numarası |
| **Acknowledgment Number** | 32 bit | Bir sonraki beklenen byte'ın numarası (kümülatif ACK) |
| **Header Length (Data Offset)** | 4 bit | Header uzunluğu (options nedeniyle değişken olabilir) |
| **Flags (Kontrol Bitleri)** | 9 bit | SYN, ACK, FIN, RST, PSH, URG (+ ECE, CWR, NS) |
| **Window Size** | 16 bit | Akış kontrolü için alıcının o an kabul edebileceği byte miktarı (rwnd) |
| **Checksum** | 16 bit | Header + veri hata kontrolü |
| **Urgent Pointer** | 16 bit | URG biti set ise, acil verinin bittiği yeri gösterir |

#### TCP Flag (Bayrak) Bitleri — Sınavda Sık Sorulur
| Flag | Açık İsim | Anlamı |
| :--- | :--- | :--- |
| **SYN** | Synchronize | Bağlantı kurma isteği; sıra numaralarını senkronize eder (3-way handshake'in ilk/ikinci adımı) |
| **ACK** | Acknowledgment | Acknowledgment Number alanının geçerli olduğunu belirtir; bağlantı kurulduktan sonra hemen her segmentte 1'dir |
| **FIN** | Finish | Gönderenin veri göndermeyi bitirdiğini, bağlantıyı kapatmak istediğini belirtir |
| **RST** | Reset | Bağlantıyı anında ve anormal şekilde sonlandırır (ör. kapalı bir porta istek geldiğinde) |
| **PSH** | Push | Alıcıya, veriyi buffer'da bekletmeden hemen üst katmana iletmesini söyler (ör. interaktif oturumlarda) |
| **URG** | Urgent | Segmentte 'acil' veri olduğunu belirtir; Urgent Pointer alanıyla birlikte kullanılır (günümüzde nadiren kullanılır) |

#### UDP Header — Çok Daha Basit
UDP header'ı sabit ve yalnızca 8 byte'tır (TCP'nin aksine, options/flags yoktur — bu da UDP'nin düşük overhead'inin nedenidir):
`Source Port (16 bit)` | `Destination Port (16 bit)` | `Length (16 bit, header+veri toplam uzunluğu)` | `Checksum (16 bit, opsiyoneldir IPv4'te ama IPv6'da zorunludur)`

> [!NOTE]
> TCP header'ı en az 20 byte (options yoksa), UDP header'ı sabit 8 byte'tır. Bu fark, TCP'nin neden UDP'ye göre daha fazla overhead taşıdığının somut kanıtıdır.

* Sequence/Acknowledgment numaraları ile veri sırası korunur, kayıp/tekrar kontrolü yapılır.
* **Akış kontrolü (Flow Control):** alıcının işleyebileceğinden hızlı veri gönderilmesini önler; alıcı, kendi buffer'ındaki boş alanı 'receive window (rwnd)' değeriyle göndericiye bildirir — amaç ALICIYI korumaktır.

### Tıkanıklık Kontrolü (Congestion Control)
Flow control alıcıyı korurken, congestion control AĞI (routerları/bağlantıları) aşırı yüklenmekten korur. TCP'nin klasik congestion control algoritması şu aşamalardan oluşur:
* **Slow Start:** bağlantı başında congestion window (cwnd) küçük başlar (genelde 1 MSS) ve her RTT'de İKİYE KATLANIR (üstel artış) — ta ki bir eşik değere (ssthresh) ulaşana veya paket kaybı olana kadar.
* **Congestion Avoidance:** ssthresh'e ulaşıldıktan sonra artış doğrusal hale gelir (her RTT'de cwnd yalnızca 1 MSS artar) — bu, AIMD (Additive Increase, Multiplicative Decrease) prensibinin 'artış' kısmıdır.
* **Paket kaybı algılandığında (timeout veya 3 tekrarlı ACK):** cwnd büyük ölçüde küçültülür (AIMD'nin 'çarpımsal azalma' kısmı) — timeout'ta cwnd 1 MSS'e sıfırlanıp Slow Start'a dönülür (TCP Tahoe mantığı); 3 tekrarlı ACK'te cwnd yarıya indirilip doğrudan Congestion Avoidance'a geçilir (Fast Recovery — TCP Reno mantığı).
* **Modern varyantlar:** TCP Reno (klasik), TCP CUBIC (Linux'ta günümüzün varsayılanı, yüksek bant genişliğinde daha agresif), TCP BBR (Google, gecikme tabanlı, kuyruklanmayı azaltmayı hedefler).

> [!NOTE]
> Bu konu mühendislik sınavlarında sıkça 'cwnd zaman grafiği çizin' tarzında sorulur (testere dişi/sawtooth şeklinde bir grafik oluşur) — grafiği anlamak formülü ezberlemekten daha önemlidir.

### UDP (User Datagram Protocol)
Bağlantısız, güvenilirlik garantisi yok, düşük gecikme — DNS, DHCP, video/ses akışı, VoIP gibi hız öncelikli uygulamalarda kullanılır.  
UDP'de flow/congestion control YOKTUR — bu hem avantaj (overhead az, hız yüksek) hem dezavantajdır (ağı tıkanıklığa sürükleyebilir, bu yüzden gerçek zamanlı uygulamalar kendi uygulama-seviyesi mekanizmalarını kullanır, ör. RTP/RTCP).

---

## 17. Uygulama Katmanı Protokolleri

| Protokol | Port(lar) | Taşıma | İşlevi |
| :--- | :--- | :--- | :--- |
| **DNS** | 53 | UDP/TCP | Alan adını IP'ye çevirir; hiyerarşik yapı (Root → TLD → Authoritative); A/AAAA/CNAME/MX/NS kayıt türleri |
| **DHCP** | 67/68 | UDP | İstemcilere otomatik IP atar; süreç DORA: Discover → Offer → Request → Ack |
| **HTTP / HTTPS** | 80 / 443 | TCP | Web trafiği; HTTPS SSL/TLS ile şifrelidir |
| **FTP** | 20/21 | TCP | Güvenilir/bağlantı odaklı dosya transferi (20=veri, 21=kontrol) |
| **TFTP** | 69 | UDP | Basit, bağlantısız, kimlik doğrulamasız dosya transferi |
| **Telnet** | 23 | TCP | Uzaktan yönetim, şifresiz — güvenli değil |
| **SSH** | 22 | TCP | Uzaktan yönetim, şifreli — günümüzde tercih edilir |
| **SMTP** | 25 | TCP | E-posta gönderme |
| **POP3 / IMAP** | 110 / 143 | TCP | E-posta alma (POP3 indirir/siler, IMAP sunucuda senkronize tutar) |
| **NTP** | 123 | UDP | Ağ cihazları arasında saat senkronizasyonu |

### HTTP Detayları
* **Non-persistent HTTP:** her istek/cevap için ayrı bir TCP bağlantısı açılıp kapatılır — eski HTTP/1.0 davranışı, yavaştır (her bağlantı için 3-way handshake overhead'i).
* **Persistent HTTP (HTTP/1.1 varsayılanı):** aynı TCP bağlantısı üzerinden birden fazla istek/cevap gönderilir — bağlantı açma maliyeti azalır.
* **HTTP metotları:** GET (veri al), POST (veri gönder/oluştur), PUT (güncelle), DELETE (sil), HEAD (yalnızca başlık).
* **Durum kodları:** 2xx (başarılı, ör. 200 OK), 3xx (yönlendirme, ör. 301 Moved Permanently), 4xx (istemci hatası, ör. 404 Not Found), 5xx (sunucu hatası, ör. 500 Internal Server Error).
* **Cookie:** sunucunun istemcide sakladığı küçük veri parçası; HTTP'nin durumsuz (stateless) doğasına rağmen oturum (session) takibi yapılmasını sağlar.

### FTP ve SMTP Detayları
* **FTP:** iki ayrı TCP bağlantısı kullanır — kontrol bağlantısı (port 21, komutlar için, oturum boyunca açık kalır) ve veri bağlantısı (port 20, her dosya transferinde ayrı açılır). Bu, HTTP'nin tek bağlantıda hem kontrol hem veri taşımasından farklıdır.
* **SMTP:** e-posta gönderiminde kullanılır, yalnızca ASCII metin tabanlıdır (7-bit); ikili (binary) dosyalar/ekler gönderilmeden önce MIME standardıyla ASCII'ye kodlanır. Gönderen SMTP sunucusundan alıcı SMTP sunucusuna doğrudan itilerek (push) gönderilir — bu yüzden e-posta ALMAK için POP3/IMAP gibi ayrı bir protokol gerekir (SMTP yalnızca gönderim/aktarım içindir).

### DNS Hiyerarşisi (Detay)
DNS, tek bir merkezi sunucu yerine dağıtık ve hiyerarşik bir yapı kullanır — bu tasarım tek nokta arızasını (single point of failure) önler ve ölçeklenebilirlik sağlar:
* **Root (kök) sunucular:** hiyerarşinin en tepesinde, dünya genelinde birkaç yüz fiziksel/anycast sunucu; TLD sunucularının adreslerini bilir.
* **TLD (Top-Level Domain) sunucular:** .com, .org, .edu.tr gibi üst düzey alan adlarını yönetir; ilgili authoritative sunucuların adresini verir.
* **Authoritative (yetkili) sunucular:** bir alan adının (ör. example.com) gerçek kayıtlarını (A, MX, NS vb.) tutan sunucudur.
* **Local DNS Server (ISS/kurum sunucusu):** istemcinin ilk sorduğu sunucu; sonucu bir süre önbelleğe alır (caching) — her sorgu kök sunucudan başlamak zorunda kalmaz.
* **Sorgu türleri:** Recursive (yinelemeli — sunucu, kullanıcı adına tüm zinciri kendisi takip edip sonucu döner) ve Iterative (yinelemesiz — sunucu 'bir sonraki sorman gereken sunucu budur' diye yönlendirir, istemci kendisi devam eder).

### P2P (Peer-to-Peer) Uygulamalar
Geleneksel client-server modelinin aksine, P2P mimarisinde her düğüm (peer) hem istemci hem sunucu gibi davranabilir; merkezi bir sunucuya bağımlılık azalır veya tamamen ortadan kalkar.
* **Client-Server vs P2P:** Client-Server'da sunucu her zaman açık olmalı ve tüm istemcilere hizmet verir (ölçeklenmesi maliyetlidir); P2P'de her peer katkıda bulunduğu için sistem kendiliğinden ölçeklenir (self-scalability) — daha çok kullanıcı, daha çok kapasite demektir.
* **BitTorrent mantığı:** paylaşılan dosya küçük parçalara (chunk) bölünür; bir 'tracker' (veya DHT) hangi peer'ların hangi parçalara sahip olduğunu takip eder; istemciler parçaları birbirinden paralel indirir ve aynı anda başkalarına yükler ('tit-for-tat' teşvik mekanizmasıyla en çok paylaşana öncelik verilir).
* **DHT (Distributed Hash Table):** merkezi bir sunucu olmadan, peer'lar arasında 'hangi anahtar hangi peer'da' bilgisini dağıtık şekilde tutan yapı — tam merkezi olmayan (decentralized) P2P sistemlerin temelidir.
* **Örnekler:** BitTorrent (dosya paylaşımı), P2P VoIP (eski Skype mimarisi), blockchain ağları (kavramsal olarak P2P mimarisine dayanır).

---

## 18. Socket Programlama Temelleri
Socket, uygulama katmanındaki bir programın, işletim sistemi aracılığıyla taşıma katmanına (TCP/UDP) eriştiği 'kapı'dır. Türkiye'deki mühendislik derslerinde genelde Python ile pratik uygulama olarak öğretilir (ör. İKÜ ders çıktılarında 'ağ soket uygulamaları gerçekleştirme' açıkça hedeflenir).

### TCP Socket — Temel Akış (Python, kavramsal)
| Sunucu (Server) | İstemci (Client) |
| :--- | :--- |
| `socket()` — soket oluştur | `socket()` — soket oluştur |
| `bind()` — IP/port'a bağla | |
| `listen()` — bağlantı bekle | |
| `accept()` — bağlantıyı kabul et (bloklar) | `connect()` — sunucuya bağlan |
| `recv()` / `send()` — veri al/gönder | `send()` / `recv()` — veri gönder/al |
| `close()` | `close()` |

Basit bir örnek (Python, kavramsal — TCP echo sunucu):
```python
import socket

sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.bind(("0.0.0.0", 5000))
sock.listen(1)
conn, addr = sock.accept()
data = conn.recv(1024)
conn.send(data)  # echo
conn.close()
```

### UDP Socket — Temel Fark
UDP'de `connect()`/`accept()` aşaması yoktur — bağlantısız olduğu için doğrudan `sendto()`/`recvfrom()` ile veri alışverişi yapılır. Her paket, hedef IP/port bilgisini kendi içinde taşır.  
Socket türü seçimi: `socket.SOCK_STREAM` → TCP, `socket.SOCK_DGRAM` → UDP (Python'da socket modülü örneği).

> [!NOTE]
> Socket programlama, teorik olarak öğrendiğiniz TCP 3-way handshake, port numaraları ve client-server modelinin pratikte nasıl çalıştığını gözle görmenizi sağlar — bu yüzden akademik derslerde laboratuvar/ödev konusu olarak sıkça karşınıza çıkar.

---

## 19. Ağ Güvenliği

### 19.1 ACL (Access Control List)
* Trafiği kaynak/hedef IP, port, protokol gibi kriterlere göre izin ver/reddet (permit/deny) kurallarıyla filtreler.
* **Basic ACL:** sadece kaynak IP'ye göre filtreler.
* **Advanced/Extended ACL:** kaynak/hedef IP, port, protokol gibi çoklu kritere göre filtreler.
* Kurallar sırayla (yukarıdan aşağı) işlenir, ilk eşleşen kural uygulanır; listenin sonunda örtük (implicit) 'deny all' vardır.

### 19.2 AAA (Authentication, Authorization, Accounting)
* **Authentication:** kullanıcının kimliğinin doğrulanması ('kim olduğu').
* **Authorization:** doğrulanan kullanıcıya hangi yetkilerin verileceği.
* **Accounting:** kullanıcı işlemlerinin kayıt altına alınması (loglama, faturalama).
* Yerel (local) veya merkezi sunucu (RADIUS — UDP tabanlı, veya TACACS+ — TCP tabanlı, komut bazlı yetkilendirmeye izin verir) üzerinden uygulanabilir.

### 19.3 NAT (Network Address Translation)
Amaç: kamu (public) IPv4 adres kıtlığını çözmek — özel (private) IP adreslerini kamu IP'ye çevirerek internete çıkışı sağlamak; ayrıca iç ağ yapısını gizleyerek dolaylı bir güvenlik faydası sağlar.
* **Static NAT:** 1-e-1 sabit eşleme.
* **Dynamic NAT:** bir kamu IP havuzundan dinamik eşleme.
* **NAPT/PAT (Port Address Translation):** tek bir kamu IP'yi port numaralarıyla ayırt ederek birden fazla iç host'un paylaşması — ev/ofis router'larında en yaygın kullanılan yöntemdir.
* **Easy IP:** router'ın kendi WAN arayüz IP'sini kullanarak NAPT yapması.

### 19.4 VPN ve Şifreleme Temelleri
* **VPN (Virtual Private Network):** güvensiz bir ağ (İnternet) üzerinden şifreli bir 'tünel' oluşturarak iki nokta arasında güvenli bağlantı sağlar.
* **IPSec:** IP katmanında çalışan, veri bütünlüğü + gizlilik + kimlik doğrulama sağlayan protokol ailesi; site-to-site VPN'lerde yaygındır.
* **SSL/TLS VPN:** web tarayıcısı üzerinden uzaktan erişim VPN'i için kullanılır.
* **Simetrik şifreleme** (AES — aynı anahtar hem şifreleme hem çözme için) vs **asimetrik şifreleme** (RSA — açık/özel anahtar çifti): simetrik hızlıdır ama anahtar dağıtımı sorunludur; asimetrik anahtar dağıtımını çözer ama yavaştır — pratikte ikisi birlikte kullanılır (ör. TLS handshake).

### 19.5 Yaygın Saldırı Türleri
* **DoS/DDoS (Denial of Service):** bir hedefi aşırı trafikle meşgul ederek hizmet dışı bırakma.
* **MITM (Man-in-the-Middle):** iki taraf arasındaki iletişimi gizlice dinleme/değiştirme.
* **ARP Spoofing/Poisoning:** sahte ARP cevaplarıyla ağdaki cihazların ARP tablolarını yanıltarak trafiği kendi üzerinden geçirme (bir tür MITM).
* **MAC Flooding:** switch'in MAC tablosunu sahte adreslerle doldurarak switch'i hub gibi davranmaya zorlama.

---

## 20. WAN Teknolojileri
* **PPP (Point-to-Point Protocol):** iki nokta arası seri hatlarda kullanılan veri bağlantı katmanı protokolü.
* **PPP Authentication — PAP:** düz metin, iki yönlü el sıkışma (daha az güvenli). **CHAP:** şifreli, challenge-response mantığıyla üç yönlü el sıkışma (daha güvenli).
* **PPPoE (PPP over Ethernet):** PPP'nin Ethernet üzerinden taşınması; ADSL/fiber ev-ofis internet erişiminde kullanılır.

---

## 21. Kablosuz Yerel Ağ (WLAN)

### 802.11 (Wi-Fi) Mimarisi
* **BSS (Basic Service Set):** bir Access Point (AP) ve ona bağlı istemcilerden oluşan temel hücre; her BSS'in bir BSSID'si (genelde AP'nin MAC adresi) vardır.
* **SSID (Service Set Identifier):** kullanıcıların gördüğü, insan tarafından okunabilir ağ adı (ör. 'EvWifi').
* **ESS (Extended Service Set):** birden fazla BSS'in (AP'nin), aynı SSID ile ve kablolu bir omurga (distribution system) üzerinden birbirine bağlanarak tek bir mantıksal ağ gibi davranmasıdır — kullanıcı bir AP'den diğerine (roaming) fark etmeden geçebilir.
* **Ad-hoc (IBSS) mod:** AP olmadan, cihazların doğrudan birbirine bağlandığı mod (nadiren kullanılır, günümüzde Wi-Fi Direct benzeri kullanım alanları var).
* **İlişkilendirme (Association) süreci:** istemci önce AP'leri tarar (Scanning — Passive: beacon çerçevelerini dinleme, veya Active: Probe Request gönderme), sonra kimlik doğrulama (Authentication) yapar, son olarak AP ile ilişkilendirilir (Association) — bu adımdan sonra veri iletişimi başlayabilir.

### Hidden/Exposed Terminal Problemi ve RTS/CTS
* **Hidden Terminal (Gizli Terminal) Problemi:** A ve C istemcileri birbirini 'duyamıyor' (aralarında engel/mesafe var) ama ikisi de B (AP)'yi duyabiliyorsa, A ve C aynı anda gönderim yapıp B'de çarpışmaya (collision) neden olabilir — çünkü CSMA/CA'nın taşıyıcı dinleme (carrier sense) mekanizması bu çarpışmayı önleyemez, taraflar birbirini duymadığı için.
* **Exposed Terminal (Açıkta Kalan Terminal) Problemi:** bir istemci, aslında çarpışmaya neden olmayacak bir gönderimi, yanlışlıkla 'kanal meşgul' sanıp erteleyebilir — gereksiz bekleme, verim kaybı yaratır.
* **RTS/CTS (Request to Send / Clear to Send) mekanizması:** gönderici önce kısa bir RTS çerçevesi yollar; AP buna CTS ile cevap verip 'kanalı bu istemciye ayırdığını' tüm BSS'e duyurur — bu sayede gizli terminal problemi büyük ölçüde azaltılır (ek overhead pahasına, bu yüzden yalnızca büyük veri çerçevelerinde tercih edilir).

### Ağ Bileşenleri ve Mimariler
* **AP (Access Point):** kablosuz istemcilerin ağa bağlandığı erişim noktası.
* **AC (Access Controller):** birden çok AP'yi merkezi olarak yöneten denetleyici (kurumsal ağlarda).
* **CAPWAP:** AC ile AP arasındaki kontrol ve yönetim tünel protokolü.
* **Mimariler:** Layer 2 In-Path (AC trafik yolunun üzerinde) ve Layer 3 Off-Path (AC trafik yolunun dışında, farklı bir L3 ağda — daha esnek, büyük ağlarda tercih edilir).

### Kablosuz Güvenlik Standartları
| Standart | Durum | Not |
| :--- | :--- | :--- |
| **WEP** | Kırılmış, kullanılmamalı | Zayıf şifreleme (RC4) |
| **WPA** | Eski, önerilmez | WEP'in geçici düzeltmesi (TKIP) |
| **WPA2** | Yaygın, kabul edilebilir | AES-CCMP şifreleme |
| **WPA3** | Güncel standart | SAE, forward secrecy |

---

## 22. Ağ Yönetimi ve Modern Teknolojiler
* **SNMP (Simple Network Management Protocol):** ağ cihazlarını merkezi olarak izlemek/yönetmek için kullanılan protokol; NMS (yönetim istasyonu), Agent (cihaz üzerinde), MIB (yönetim bilgi tabanı) bileşenlerinden oluşur.
* **Syslog:** cihaz olaylarının merkezi loglanması; log seviyeleri (0-7: Emergency'den Debug'a) önem sırasına göre filtrelenebilir.
* **QoS (Quality of Service):** sınırlı bant genişliğini öncelik sırasına göre paylaştırma mekanizması; ses/video gibi gecikmeye duyarlı trafiğe öncelik tanınır (ör. DSCP, CoS işaretleme).
* **VRRP (Virtual Router Redundancy Protocol):** birden fazla router'ın tek bir sanal gateway IP'si paylaşarak gateway yedekliliği sağlamasıdır — büyük ağlarda kritik bir teknolojidir.

### SDN ve NFV
* **SDN (Software-Defined Networking):** kontrol düzlemi (control plane) ile veri düzlemini (data plane) birbirinden ayırır; ağ, merkezi bir controller üzerinden programatik (API ile) yönetilir. OpenFlow, controller-switch iletişimini tanımlayan öncü protokoldür.
* **NFV (Network Functions Virtualization):** ağ fonksiyonlarının (router, firewall, load balancer) özel donanım yerine genel amaçlı sunucularda sanal makine/konteyner olarak çalıştırılmasıdır. Bileşenler: NFVI (altyapı), VNF (sanallaştırılmış fonksiyonlar), MANO (yönetim ve orkestrasyon).

| Karşılaştırma | SDN | NFV |
| :--- | :--- | :--- |
| **Odak** | Ağın 'nasıl yönetileceği' | Ağ fonksiyonlarının 'nerede/nasıl çalıştığı' |
| **Mekanizma** | Control/data plane ayrımı + merkezi controller | Donanımdan bağımsız sanallaştırma |

### Ağ Otomasyonu
Geleneksel manuel (CLI ile tek tek) yönetimin zorlukları (yavaş, hataya açık, ölçeklenemez), ağ otomasyonu ihtiyacını doğurmuştur.  
Python ile otomasyon: `telnetlib` (eski, şifresiz — artık önerilmiyor), `Netmiko`/`Paramiko` (SSH tabanlı), `NETCONF`/`RESTCONF` (yapılandırılmış, API tabanlı — YANG modelleriyle birlikte modern tercih).

---

## 23. Kampüs Ağı Mimarileri
Kampüs ağı: bir kurumun/binanın/kampüsün içindeki yerel ağ altyapısıdır.

| Ölçek | Mimari | Özellikler |
| :--- | :--- | :--- |
| **Küçük kampüs ağı** | 2 katmanlı (erişim + çekirdek birleşik) | Basit yapı, düşük maliyet |
| **Orta ölçekli kampüs ağı** | Erişim + dağıtım (aggregation) + çekirdek — 3 katmana geçiş başlar | Büyüme için hazırlık |
| **Büyük kampüs ağı** | Tam 3 katmanlı hiyerarşik mimari (Access – Aggregation/Distribution – Core) | Yüksek yedeklilik (stacking/clustering, VRRP, çoklu link aggregation) gerektirir |

Kampüs ağlarında kullanılan ana teknolojiler: VLAN, STP/RSTP/MSTP, Link Aggregation, yönlendirme protokolleri, ACL/AAA, NAT, DHCP, WLAN.  
**Ağ Proje Yaşam Döngüsü:** İhtiyaç toplama ve analiz → Planlama ve tasarım → Uygulama (deployment) → İşletim/Bakım (O&M) → Optimizasyon.

---

## 24. Laboratuvar Araçları: Wireshark ve Cisco Packet Tracer
Teorik konuları pekiştirmek için ders kapsamında genellikle iki araç kullanılır; ikisinin amacı farklıdır ve birbirini tamamlar.

### Wireshark — Paket Analizi
Wireshark, bir ağ arayüzünden geçen gerçek paketleri yakalayıp (capture) katman katman inceleyen bir 'protokol analizörü'dür (sniffer). Teoride öğrenilen header alanlarını gerçek trafikte görmeyi sağlar.
* Capture filtresi (yakalama öncesi, ör. 'tcp port 80') ile display filtresi (yakalanan trafiği ekranda filtreleme, ör. 'http' veya 'dns') arasındaki fark önemlidir — capture filtresi performans için, display filtresi analiz için kullanılır.
* Tipik laboratuvar egzersizleri: bir web sayfası açılırken DNS sorgusunu, ardından TCP 3-way handshake'i (SYN/SYN-ACK/ACK), ardından HTTP GET isteğini ve son olarak TCP bağlantı sonlandırmasını (FIN/ACK) paket paket izlemek.
* 'Follow TCP Stream' özelliği, tek bir TCP bağlantısına ait tüm paketleri birleştirip okunabilir formatta gösterir — HTTP isteği/cevabını düz metin olarak görmeyi sağlar (HTTPS'te şifreli olduğu için bu doğrudan çalışmaz).
* ARP, ICMP (ping), DHCP (DORA süreci) gibi protokolleri de canlı gözlemlemek yaygın bir lab konusudur.

### Cisco Packet Tracer — Ağ Simülasyonu
Packet Tracer, gerçek donanım olmadan router, switch, PC, AP gibi cihazları sürükle-bırak ile yerleştirip birbirine bağlayarak sanal bir ağ topolojisi kurmayı ve bu cihazları gerçek CLI komutlarıyla (Cisco IOS sözdizimi) yapılandırmayı sağlayan bir simülatördür.
* Tipik lab senaryoları: birkaç PC ve bir switch ile basit bir LAN kurup PC'ler arası ping testi yapmak; VLAN oluşturup trunk/access port yapılandırması yapmak; iki veya daha fazla router arasında statik rota veya RIP/OSPF yapılandırıp uçtan uca erişilebilirliği test etmek.
* **Simulation Mode:** paketlerin ağ üzerinde adım adım (katman katman, cihazdan cihaza) nasıl ilerlediğini görsel olarak izlemeye imkân tanır — bu, encapsulation/decapsulation kavramını somutlaştırmak için özellikle faydalıdır.
* Packet Tracer, Cisco IOS komut sözdizimini simüle eder (ör. enable, configure terminal, interface, ip address, router ospf gibi) — genel CLI kavramları (running-config/startup-config, show komutları vb.) bu ortamda da geçerlidir, bkz. bir sonraki bölüm.

> [!NOTE]
> Bu iki araç birbirini tamamlar: Packet Tracer ile bir ağ KURULUR, Wireshark ile o ağdaki (veya gerçek bir ağdaki) trafik ANALİZ EDİLİR. Sınav/lab sorularında genelde önce bir topoloji kurmanız, sonra üzerinde belirli bir senaryoyu (ör. 'PC1'den PC2'ye ping atılamıyor, sorunu bulun') çözmeniz istenir.

---

## 25. Cihaz Yönetimine Genel Bakış (CLI Kavramları)
Farklı üreticilerin (Cisco, Huawei, Juniper vb.) komut satırları birbirinden farklıdır, ama temel mantık ortaktır — bu yüzden burada yalnızca genel kavramlar verilmiştir.
* **Yönetim arayüzleri:** Console (yerel, seri kablo ile), Telnet/SSH (uzaktan, komut satırı — SSH şifreli olduğu için tercih edilir), Web (grafik arayüz).
* **Komut satırı görünümleri (modes):** kullanıcı modu (temel izleme komutları), yapılandırma/global modu (genel ayarlar), arayüz modu (port bazlı ayarlar), protokol modu (ör. routing protokolüne özel ayarlar).
* `Tab` ile otomatik tamamlama, `?` ile bağlamsal yardım çoğu CLI'de ortak özelliklerdir.
* **Çalışan konfigürasyon (running-config) ile kalıcı kayıtlı konfigürasyon (startup-config) ayrımı kritiktir:** değişiklikler önce yalnızca running-config'te aktif olur; açıkça kaydedilmezse (ör. save, write, copy run start gibi komutlarla) cihaz yeniden başlatıldığında (reboot) TÜM değişiklikler kaybolur. Bu, gerçek cihaz yönetiminde en sık düşülen hatalardan biridir.
* Temel izleme komutları genelde 'display' veya 'show' önekiyle başlar (ör. arayüz durumu, routing tablosu, MAC adres tablosu, çalışan konfigürasyon görüntüleme) — üreticiye göre kelime değişir ama amaç aynıdır.

---

## 26. Sınava / Tekrara Hazırlık — Kritik Noktalar
* OSI 7 katman ↔ TCP/IP 4 katman eşleşmesini ve her katmanın PDU adını ezbere bilmek gerekir.
* Switch = Katman 2 (MAC ile çalışır), Router = Katman 3 (IP ile çalışır); switch broadcast domain'i bölmez, router böler.
* STP döngü (loop) problemini çözer; Link Aggregation ise bant genişliği/yedeklilik sağlar — birbirine karıştırılmamalıdır.
* RIP = distance-vector/hop count; OSPF = link-state/cost — OSPF'in yakınsama hızı RIP'ten çok daha iyidir.
* TCP = güvenilir/bağlantı odaklı; UDP = hızlı/bağlantısız.
* NAT (adres tasarrufu), ACL (trafik filtreleme), AAA (kimlik doğrulama/yetkilendirme) — üçü de güvenlikle ilişkilidir ama farklı amaçlara hizmet eder.
* PAP düz metin, CHAP şifreli — PPP kimlik doğrulamasında CHAP tercih edilir.
* Administrative distance/route preference değerleri üreticiye özgüdür — genel kavramı bilin, sınavda hangi platform sorulduğuna dikkat edin.
* SDN = control/data plane ayrımı + merkezi controller; NFV = ağ fonksiyonlarının donanımdan bağımsız sanal çalışması — sıkça karıştırılır, ayrımı net tutun.
* running-config kaydedilmeden reboot edilirse yapılan tüm değişiklikler kaybolur — gerçek laboratuvar/simülasyon sorularında dikkat edilmesi gereken en kritik pratik nokta.
* Akademik/teorik: uçtan uca gecikme = işlem + kuyruklama + iletim + yayılım gecikmesi toplamıdır — formülleri ve birimleri karıştırmayın (iletim gecikmesi = L/R, yayılım gecikmesi = d/s).
* Sliding Window > Go-Back-N > Selective Repeat verimlilik sıralamasını ve aralarındaki farkı (alıcı buffer'ı tutuyor mu, tüm pencereyi mi yoksa sadece kayıp paketi mi tekrar gönderiyor) net ayırt edin.
* TCP congestion control grafiği (cwnd vs zaman) testere dişi şeklindedir: Slow Start'ta üstel artış, Congestion Avoidance'ta doğrusal artış, kayıpta ani düşüş — bu grafiği çizebilmek sık sorulan bir beceridir.
* Dijkstra (link-state/OSPF) tüm topolojiyi bilerek merkezi hesap yapar; Bellman-Ford (distance-vector/RIP) yalnızca komşu bilgisiyle dağıtık hesap yapar — bu ayrım hem algoritma hem de gerçek protokol davranışı (yakınsama hızı, döngü riski) açısından sınavda sık sorulur.
* Nyquist (gürültüsüz kanal, $C=2H\log_2 V$) ve Shannon (gürültülü kanal, $C=H\log_2(1+S/N)$) formüllerini birbirine karıştırmayın — hangisinin gürültüyü hesaba kattığını hatırlamak yeterlidir.
* Datagram (İnternet/IP) ağları bağlantısızdır, her paket bağımsız yönlendirilir; Sanal Devre ağları iletişim öncesi sabit bir yol kurar — İnternet'in datagram tabanlı olması, esneklik/dayanıklılık sağlar ama garantili performans sağlamaz.
* Forwarding (hızlı, donanım destekli, her pakette) ile Routing (yavaş, kontrol düzleminde, topoloji değiştiğinde) ayrımını net tutun.
* CIDR'nin iki temel amacı: (1) adres israfını önlemek, (2) route aggregation ile routing tablolarını küçültmek — sadece 'sınıfsız adresleme' demek yetersiz bir cevaptır, NEDEN kullanıldığını da açıklayabilmelisiniz.
* BGP ile OSPF/RIP arasındaki temel fark: IGP'ler (OSPF/RIP) bir AS içinde METRİĞE göre çalışır; BGP (EGP) AS'lar arasında POLİTİKAYA göre çalışır — bu, sınavda en çok karıştırılan noktalardan biridir.
* Hidden terminal problemi kablosuz ağlara özgüdür (kablolu Ethernet'te yoktur, çünkü kablolu ortamda tüm istasyonlar aynı fiziksel ortamı paylaşır ve birbirini duyar) — RTS/CTS bu problemi azaltmak içindir, tamamen ortadan kaldırmaz.
* Hata TESPİTİ (parity, CRC) ile hata DÜZELTME (Hamming) birbirine karıştırılmamalı: tespit yöntemleri yalnızca 'hata var mı yok mu' söyler ve yeniden gönderim gerektirir; Hamming kodu hatalı bitin POZİSYONUNU bulup yeniden göndermeden düzeltir. Hamming mesafesi $d$ ise: $d-1$ bit tespit edilir, $\lfloor (d-1)/2 \rfloor$ bit düzeltilir.
* Byte stuffing (FLAG+ESC byte'ları ile, ör. PPP) ile bit stuffing (art arda 5 '1'den sonra '0' ekleme, ör. HDLC) farklı katmanlarda/protokollerde kullanılan iki ayrı çerçeveleme yöntemidir — hangi protokolün hangisini kullandığını karıştırmayın. Not: PPP'nin kendisi de iletim moduna göre (asenkron→byte stuffing, senkron→bit stuffing) ikisini de kullanabilir.
* TCP sonlandırma '4 adım mı 3 adım mı' sorusuna: teorik/maksimum durum 4 bağımsız segmenttir (FIN, ACK, FIN, ACK); pratikte pasif taraf FIN+ACK'i birleştirirse 3 segmentte biter — ikisi de doğru cevaptır, sorunun 'teorik' mi 'pratik' mi sorduğuna bakın.
* TCP header en az 20 byte (options hariç), UDP header sabit 8 byte'tır — bu fark, ikisinin overhead farkının somut kanıtıdır. TCP flag bitlerini (SYN/ACK/FIN/RST/PSH/URG) ezbere bilmek gerekir.
* $\text{dB} \rightarrow \text{oran}$ dönüşümü sınavda sık çıkar: $S/N \text{ (oran)} = 10^{(\text{dB}/10)}$. Bu formülü ezbere bilmeden Shannon formülünü sayısal olarak çözemezsiniz.
* VLSM'de her zaman EN BÜYÜK host ihtiyacından başlayıp küçüğe doğru, bir önceki bloğun bittiği adresten devam ederek ilerleyin — sıralamayı yanlış yaparsanız bloklar çakışır veya adres israfı oluşur.
