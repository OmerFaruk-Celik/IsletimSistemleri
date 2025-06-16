📖 İşletim Sistemleri - Kapsamlı Çalışma Rehberi

Bu rehber, İşletim Sistemleri (Operating Systems) dersinin temel konularını, kavramsal açıklamaları ve sınav odaklı soru çözümlerini içermektedir. Amacı, konuları mantıksal bir sırayla sunarak kalıcı öğrenmeyi sağlamaktır.
🗂️ İçindekiler

    Bölüm 1: İşletim Sistemine Giriş ve Temel Kavramlar

        İşletim Sistemi Nedir?

        Sistem Çağrıları (System Calls) ve API

        İşletim Sistemi Yapıları (Monolitik, Mikroçekirdek)

    Bölüm 2: Süreç (Process) Yönetimi

        Program ve Proses Arasındaki Fark

        Prosesin Bellek Yapısı ve Proses Kontrol Bloğu (PCB)

        Bağlam Değiştirme (Context Switch)

        Proses Oluşturma ve Sonlandırma

    Bölüm 3: İş Parçacıkları (Threads)

        Thread Nedir?

        Proses vs. Thread Karşılaştırması

        Multithreading Modelleri

    Bölüm 4: CPU Zamanlaması (Scheduling)

        Zamanlayıcı Tipleri ve Kriterleri

        Zamanlama Algoritmaları (FCFS, SJF, SRTF, RR)

    Bölüm 5: Süreç Senkronizasyonu

        Yarış Durumu (Race Condition) ve Kritik Bölge

        Kritik Bölge Çözüm Koşulları

        Semaforlar ve Mutex Kilitleri

    Bölüm 6: Kilitlenmeler (Deadlocks)

        Deadlock Şartları

        Kaynak Ayırma Grafiği

        Deadlock Yönetimi

    Bölüm 7: Bellek Yönetimi

        Adres Uzayları ve MMU

        Bölünme (Fragmentation)

        Sayfalama (Paging) ve Segmentasyon

    Bölüm 8: Sanal Bellek (Virtual Memory)

        Talep Üzerine Sayfalama (Demand Paging)

        Sayfa Değiştirme Algoritmaları (FIFO, LRU, Optimal)

Bölüm 1: İşletim Sistemine Giriş ve Temel Kavramlar
1.1. İşletim Sistemi Nedir?

İşletim sistemi (OS), bilgisayar donanımı ile kullanıcı/uygulamalar arasında bir arayüz görevi gören, kaynakları (CPU, bellek, disk vb.) yöneten ve kontrol eden temel sistem yazılımıdır.
1.2. Sistem Çağrıları (System Calls) ve API

Bir uygulama, işletim sisteminin sunduğu bir hizmete (örneğin dosya okuma) ihtiyaç duyduğunda, bunu doğrudan yapamaz. Bunun yerine işletim sistemi çekirdeğine (kernel) bir istek gönderir.

    Sistem Çağrısı (System Call): Uygulamanın çekirdekten hizmet isteme mekanizmasıdır. Bu, programın kullanıcı modu'ndan çekirdek modu'na kontrollü geçiş yapmasını sağlar.

    API (Application Programming Interface): Programcıların sistem çağrılarını daha kolay kullanabilmesi için sağlanan üst seviye kütüphane fonksiyonlarıdır.

    🎯 Sınav Sorusu (Görsel 14, Soru 2):
    Program geliştiriciler genellikle ihtiyaç duydukları işletim sistemi servislerine sistem çağrıları ile ulaşmak yerine daha üst seviye ve kullanımı daha kolay olan _______'ler kullanırlar.

    Cevap: a. Uygulama programlama arayüzü (API)
    Açıklama: Programcı, sistem çağrısının karmaşık detayları yerine printf() gibi basit bir API fonksiyonu kullanır. API, bu karmaşıklığı gizler.

1.3. İşletim Sistemi Yapıları

    Monolitik Çekirdek (Monolithic Kernel): İşletim sisteminin tüm bileşenleri (dosya sistemi, zamanlayıcı, sürücüler) tek ve büyük bir çekirdek programı içinde çalışır.

        Avantaj: Bileşenler arası iletişim hızlıdır (fonksiyon çağrısı).

        Dezavantaj: Bir sürücüdeki hata tüm sistemi çökertebilir. Hantal ve bakımı zordur.

    Mikroçekirdek (Microkernel): Çekirdekte sadece en temel hizmetler (IPC, bellek yönetimi, temel zamanlama) bulunur. Dosya sistemi, sürücüler gibi diğer servisler kullanıcı modunda ayrı prosesler olarak çalışır.

        Avantaj: Güvenli ve modülerdir. Bir servis çökerse sistem etkilenmez.

        Dezavantaj: Servisler arası iletişim (mesajlaşma) yavaştır.

    🎯 Sınav Sorusu (Görsel 29, Soru 20):
    Aşağıdaki işletim sistemi yapısından hangisi Mach OS için olanıdır?

    Cevap: b. Microkernel
    Açıklama: Mach, mikroçekirdek tasarımının en bilinen ve etkili örneğidir.

Bölüm 2: Süreç (Process) Yönetimi
2.1. Program ve Proses Arasındaki Fark
Özellik	Program	Proses (Süreç)
Durum	Pasif Varlık	Aktif Varlık
Konum	Disk	Bellek (RAM)
Ömür	Kalıcı	Geçici
Analoji	Yemek Tarifi	Yemeği Yapan Aşçı
2.2. Prosesin Bellek Yapısı ve Proses Kontrol Bloğu (PCB)

Bir prosesin bellekteki düzeni ve işletim sisteminin onu yönetmek için kullandığı veri yapısı aşağıda gösterilmiştir:

      
+------------------+
|      Stack       |  <-- Fonksiyon çağrıları, lokal değişkenler
|       ↓          |
|                  |
|       ↑          |
|      Heap        |  <-- Dinamik bellek (malloc, new)
+------------------+
|       Data       |  <-- Global/Statik değişkenler
+------------------+
|       Text       |  <-- Program kodu (salt okunur)
+------------------+

    

IGNORE_WHEN_COPYING_START
Use code with caution.
IGNORE_WHEN_COPYING_END

    Proses Kontrol Bloğu (PCB): İşletim sisteminin her proses için tuttuğu "kimlik kartı"dır.

        İçeriği: Proses ID (PID), Proses Durumu (New, Ready, Running, Waiting), Program Sayacı (PC), CPU Yazmaçları, Bellek Limitleri, Açık Dosyalar Listesi.

    🎯 Sınav Sorusu (Görsel 16, Soru 5):
    Bir prosesin çağıracağı fonksiyonlar için fonksiyon parametreleri, fonksiyon geri dönüş adresleri, lokal değişkenleri aşağıdakilerin hangisinde tutulur?

    Cevap: a. Stack
    Açıklama: Bu, Stack'in tanımı ve temel görevidir.

2.3. Bağlam Değiştirme (Context Switch)

CPU'nun bir prosesten diğerine geçirilmesi işlemidir. Bu sırada işletim sistemi:

    Kaydet: Mevcut prosesin durumunu (PC, yazmaçlar vb.) PCB'sine kaydeder.

    Yükle: Yeni prosesin durumunu PCB'sinden CPU'ya yükler.

    🎯 Sınav Sorusu (Görsel 5, Soru 5):
    ...mevcut prosesin durum bilgilerinin kaydedilip CPU'dan çıkarılması ve sonraki prosesin durum bilgilerinin yüklenip CPU'ya geçmesi işlemine _______ denir.

    Cevap: d. Context switching
    Açıklama: Bu, bağlam değiştirmenin birebir tanımıdır.

2.4. Proses Oluşturma ve Sonlandırma (UNIX Örneği)

    fork(): Kendisinin kopyası olan bir alt proses (child) yaratır.

    exec(): Bir prosesin bellek alanını yeni bir programla doldurur.

    wait(): Ebeveyn prosesin, alt prosesin bitmesini beklemesini sağlar. Alt prosesin çıkış durumunu ve PID'sini döndürür.

    🎯 Sınav Sorusu (Görsel 2, Soru 3):
    Aşağıdaki sistem çağrılarından hangisi UNIX için sonlandırılan child prosesin durum bilgisini ve PID değerini geri döndürür?

    Cevap: b. wait
    Açıklama: wait(), "zombi prosesleri" (işi bitmiş ama sonucu alınmamış prosesler) önlemek için kullanılır ve alt prosesin bitiş bilgilerini ebeveyne iletir.

Bölüm 3: İş Parçacıkları (Threads)
3.1. Thread Nedir?

Bir proses içinde çalışabilen en küçük yürütme birimidir. Thread'ler, ait oldukları prosesin kaynaklarını paylaşır, bu da onları "hafif siklet prosesler" yapar.
3.2. Proses vs. Thread Karşılaştırması
Özellik	Her Thread'e Özel (Paylaşılmaz)	Tüm Thread'ler Tarafından Paylaşılır
Bileşenler	Stack (Yığın) <br> Program Sayacı (PC) <br> Yazmaç Kümesi	Kod (Text) Bölümü <br> Veri (Data) Bölümü <br> Heap <br> Açık Dosyalar
Oluşturma	Hızlı ve ucuz	Yavaş ve maliyetli (proses için)
İletişim	Kolay (Paylaşılan bellek üzerinden)	Zor (IPC mekanizmaları gerekir)

    🎯 Sınav Sorusu (Görsel 6, Soru 7):
    Bir prosese ait threadler yukarıdakilerden hangilerini aralarında paylaşırlar?
    I. Yığın (Stack), II. Program sayıcı (PC), III. Yazmaç kümesi, IV. Veri bölümü, V. Kod bölümü

    Cevap: d. IV-V
    Açıklama: Thread'ler, kendi bağımsız çalışmalarını sağlayan Stack, PC ve Yazmaçları paylaşmazlar. Ait oldukları prosesin ortak kaynakları olan Veri ve Kod bölümlerini paylaşırlar.

3.3. Multithreading Modelleri

    Many-to-One: Birçok kullanıcı thread'i tek bir çekirdek thread'ine eşlenir. Bir thread bloke olursa, hepsi bloke olur. Verimsizdir.

    One-to-One: Her kullanıcı thread'i ayrı bir çekirdek thread'ine eşlenir. Gerçek paralellik sağlar. (Windows, Linux)

    Many-to-Many: Kullanıcı thread'leri, daha az veya eşit sayıda çekirdek thread'ine esnek bir şekilde eşlenir.

    🎯 Sınav Sorusu (Görsel 6, Soru 8):
    Aşağıdaki Multithreading modellerinden hangisinde bir thread bloke olduğunda tüm process bloke olur?

    Cevap: Many-to-One (Not: Sınavdaki şıklar hatalı olabilir.)
    Açıklama: Tüm kullanıcı thread'leri tek bir çekirdek thread'ine bağlı olduğu için, o çekirdek thread'i bloke olursa (örneğin bir G/Ç işlemi beklerse), diğer tüm kullanıcı thread'leri de çalışamaz ve proses bloke olur.

Bölüm 4: CPU Zamanlaması (Scheduling)

Hangi hazır prosesin CPU'ya atanacağına karar verme işlemidir.
4.1. Zamanlama Algoritmaları
Algoritma	Açıklama	Avantaj / Dezavantaj	Tür
FCFS	İlk gelen ilk hizmet alır.	Basit. / Konvoy Etkisi (uzun iş kısayı bekletir).	Non-Preemptive
SJF	En kısa iş önce.	Ortalama bekleme süresi en iyi. / Sonraki iş süresini bilmek zor.	Non-Preemptive
SRTF	Kalan süresi en kısa olan önce.	SJF'nin preemptive versiyonu. Daha optimal. / Sık context switch.	Preemptive
Round Robin (RR)	Her prosese quantum kadar zaman verilir.	Etkileşimli sistemler için adil. / Performans quantum'a bağlı.	Preemptive

    🎯 Sınav Sorusu (Görsel 4, Soru 4):
    Zaman paylaşımlı (time-sharing) işletim sistemlerde bir proses kendisi için belirlenen zaman aralığında CPU'da çalıştıktan sonra, proses running durumundan hangi duruma geçer?

    Cevap: a. Ready
    Açıklama: Zaman paylaşımlı sistemler RR kullanır. Zaman dilimi (quantum) dolduğunda, prosesin işi bitmemişse zorla durdurulur (preempted) ve tekrar çalıştırılmak üzere Ready (Hazır) kuyruğunun sonuna gönderilir.

Bölüm 5: Süreç Senkronizasyonu
5.1. Yarış Durumu (Race Condition) ve Kritik Bölge

    Yarış Durumu: Birden fazla prosesin paylaşılan bir veriye aynı anda erişip, sonucun erişim sırasına göre değiştiği durum.

    Kritik Bölge (Critical Section): Bir programın, paylaşılan kaynaklara eriştiği kod parçası.

5.2. Kritik Bölge Çözüm Koşulları

    Karşılıklı Dışlama (Mutual Exclusion): Bir proses kritik bölgesindeyken, başka hiçbir proses kendi kritik bölgesine giremez.

    İlerleme (Progress): Kritik bölge boşsa ve girmek isteyenler varsa, seçim süresiz ertelenmemeli.

    Sınırlı Bekleme (Bounded Waiting): Bir prosesin kritik bölgeye girmek için sonsuza kadar beklemesi engellenmeli.

    🎯 Sınav Sorusu (Görsel 11, Soru 15):
    Hiçbir proses kritik bölgede (KB) değilken... KB'ye girecek prosesin seçimi süresiz ertelenmemeli... Bu özelliğe _______ denir.

    Cevap: c. İlerleme (Progress)
    Açıklama: Bu tanım, bir karar verilmesi ve sistemin ilerlemesi gerektiğini vurguladığı için İlerleme'yi ifade eder.

5.3. Semaforlar ve Mutex Kilitleri

    Mutex (Mutual Exclusion) Kilit: Basit bir kilit mekanizmasıdır. Sadece iki durumu vardır: locked (kilitli) ve unlocked (kilitsiz). Kritik bölgeye girmeden önce lock() yapılır, çıkarken unlock() yapılır.

    Semafor (Semaphore): Belirli sayıda prosesin bir kaynağa erişimine izin veren genelleştirilmiş bir kilit mekanizmasıdır. wait() ve signal() atomik operasyonlarını kullanır.

    🎯 Sınav Sorusu (Görsel 11, Soru 16):
    Şekilde verilen semafor veri yapısında process list hangi problemin önüne geçmek için kullanılır?

    Cevap: b. Meşgul Bekleme (Busy Waiting)
    Açıklama: Semaforun wait işlemi içinde beklemesi gereken prosesi bir listeye alıp block() (uyutma) komutu çalıştırması, CPU'yu sürekli while döngüsüyle meşgul eden Meşgul Bekleme'yi önlemek içindir.

Bölüm 6: Kilitlenmeler (Deadlocks)
6.1. Deadlock Şartları

Bir deadlock'un oluşması için aşağıdaki 4 şartın aynı anda sağlanması gerekir:

    Karşılıklı Dışlama (Mutual Exclusion)

    Tut ve Bekle (Hold and Wait)

    Geri Alınamazlık (No Preemption)

    Döngüsel Bekleme (Circular Wait)

6.2. Kaynak Ayırma Grafiği (Resource Allocation Graph)

Deadlock'ları görselleştirmek için kullanılır.

    Daireler prosesleri, kareler kaynakları temsil eder.

    Proses -> Kaynak: Proses kaynağı istiyor (istek kenarı).

    Kaynak -> Proses: Kaynak prosese atanmış (atama kenarı).

    Grafikte bir döngü (cycle) varsa, deadlock olabilir (eğer her kaynak türünden tek bir örnek varsa kesinlikle deadlock vardır).

    🎯 Sınav Sorusu (Görsel 10, Soru 12):
    (Görselde Proses1 -> Kaynak2 ve Kaynak1 -> Proses1; Proses2 -> Kaynak1 ve Kaynak2 -> Proses2 şeklinde bir döngü var.) Bu problem hangisine bir örnektir?

    Cevap: c. Ölümcül Kilitlenme (Deadlock)
    Açıklama: Görsel, iki prosesin birbirlerinin tuttuğu kaynakları beklediği klasik bir döngüsel bekleme durumunu gösterir. Bu da deadlock'a yol açar.

Bölüm 7: Bellek Yönetimi
7.1. Adres Uzayları ve MMU

    Mantıksal Adres: CPU tarafından üretilir (sanal).

    Fiziksel Adres: RAM tarafından kullanılan gerçek adrestir.

    MMU (Memory Management Unit): Mantıksal adresi fiziksel adrese çeviren donanımdır.

7.2. Bölünme (Fragmentation)

    Dışsal Bölünme (External): Bellekte yeterli toplam boş alan olmasına rağmen, bu alanların bitişik olmaması nedeniyle prosesin yerleştirilememesi.

    İçsel Bölünme (Internal): Belleğin sabit boyutlu bloklara (sayfa) ayrılmasıyla, bir prosese tahsis edilen bloğun son kısmının boş kalması.

    🎯 Sınav Sorusu (Görsel 26, Soru 17):
    Devamlı Tahsis yaklaşımında, hafıza üzerinde çok sayıda küçük boşluk olduğu halde proseslerin yerleşebileceği büyüklükte tek parça boşluk kalmaması durumuna ne denir?

    Cevap: b. Dışsal parçalanma (External Fragmentation)
    Açıklama: Bu, dışsal parçalanmanın tanımıdır. Çözümü genellikle sayfalama (paging) veya sıkıştırma (compaction)'dır.

7.3. Sayfalama (Paging)

    Fiziksel belleği sabit boyutlu çerçevelere (frames), mantıksal belleği aynı boyutlu sayfalara (pages) böler.

    Bir prosesin sayfaları, bellekteki herhangi bir boş çerçeveye yerleştirilebilir.

    Sayfa Tablosu (Page Table): Her proses için, sayfa numarasını çerçeve numarasına eşleyen bir tablo tutulur.

Bölüm 8: Sanal Bellek (Virtual Memory)

Bir prosesin tamamının fiziksel bellekte olmasına gerek kalmadan çalışabilmesini sağlayan tekniktir. Prosesin sadece o an ihtiyaç duyulan kısımları (sayfaları) belleğe yüklenir.
8.1. Talep Üzerine Sayfalama (Demand Paging)

Bir sayfaya, o bellekte değilken erişilmeye çalışıldığında bir sayfa hatası (page fault) oluşur. İşletim sistemi bu hatayı yakalar:

    İstenen sayfanın diskte nerede olduğunu bulur.

    Bellekte boş bir çerçeve bulur.

    Sayfayı diskten o çerçeveye yükler.

    Prosesin sayfa tablosunu günceller.

    Prosesi kaldığı yerden devam ettirir.

8.2. Sayfa Değiştirme Algoritmaları

Bellekte boş çerçeve kalmadığında, yeni bir sayfa getirmek için hangi eski sayfanın diskle takas edileceğine (swap out) karar verirler.

    FIFO (First-In, First-Out): Belleğe ilk giren sayfa ilk çıkar. Basittir ama performansı kötü olabilir.

    LRU (Least Recently Used): En uzun süredir kullanılmayan sayfa çıkarılır. Genellikle iyi performans gösterir ama donanım desteği gerektirir.

    Optimal (OPT): Gelecekte en uzun süre boyunca kullanılmayacak olan sayfa çıkarılır. Mümkün olan en iyi performansı verir ama geleceği bilmek imkansız olduğu için sadece teoriktir ve diğer algoritmaları ölçmek için kullanılır
