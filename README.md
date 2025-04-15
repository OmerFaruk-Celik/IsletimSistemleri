# **İşletim Sistemleri Kapsamlı ve Geliştirilmiş Çalışma Notları**

Bu notlar, işletim sistemleriyle ilgili temel kavramlardan başlayarak proses yönetimi, bellek yönetimi, thread ve multithreading, senkronizasyon, CPU zamanlaması ve sanal bellek gibi konuları detaylı bir şekilde ele alır. Ayrıca, boşluk doldurma sorularında yer alan eksik bilgiler de tamamlanmıştır.

---

## **1. İşletim Sistemi Temel Kavramları**

### **İşletim Sistemi Nedir?**
İşletim sistemi, bilgisayar donanımını yöneten ve kullanıcı programlarının çalışması için bir ortam sağlayan temel yazılım bileşenidir. İşletim sistemi:
- Donanım kaynaklarını adil ve etkin bir şekilde tahsis eder.
- Kullanıcı ve uygulama programlarının gereksinimlerini karşılar.
- Bellek, CPU, giriş/çıkış cihazları gibi donanım bileşenlerini yönetir.

### **İşletim Sisteminin Temel İşlevleri**
1. **Kaynak Yönetimi:**
   - CPU, bellek, I/O cihazları gibi kaynakların yönetimi.
2. **Kullanıcı ve Program Arayüzü Sağlama:**
   - Komut satırı (CLI) veya grafiksel kullanıcı arabirimi (GUI) sunar.
3. **Program Yürütme:**
   - Çalışan programların sırasını ve kaynak kullanımını düzenler.
4. **Veri Yönetimi:**
   - Dosya sistemlerini, depolama cihazlarını ve veri aktarımını yönetir.
5. **Hata Tespiti ve Güvenlik:**
   - Sistem hatalarını tespit eder ve kullanıcıların verilerini korur.

---

## **2. Process Kavramı**

### **Process Nedir?**
Process, bellekte yüklü olan ve çalışmakta olan bir programdır. Processler, işletim sisteminin kaynaklarını ve CPU’yu kullanarak görevlerini yerine getirir.

### **Process Bileşenleri**
1. **Text Section:** Program kodu.
2. **Data Section:** Global değişkenler.
3. **Heap:** Çalışma zamanında dinamik olarak ayrılan bellek.
4. **Stack:** Fonksiyon parametreleri, geri dönüş adresleri ve lokal değişkenler.

### **Process Durumları**
1. **New:** Process oluşturuluyor.
2. **Ready:** Process CPU’da çalışmak için hazır.
3. **Running:** Process CPU üzerinde yürütülüyor.
4. **Waiting:** Process bir olayın gerçekleşmesini bekliyor (ör. I/O işlemi).
5. **Terminated:** Process tamamlandı.

### **Process Scheduling**
- **Long-term Scheduler:** Diskteki işleri belleğe yükler.
- **Short-term Scheduler:** Hazır kuyruğundaki processlerden hangisinin CPU kullanacağını belirler.
- **Medium-term Scheduler:** Bellekten diske geçici olarak taşınan processleri (swapping) yönetir.

---

## **3. Thread ve Multithreading**

### **Thread Nedir?**
Thread, bir process içinde bağımsız olarak çalışabilen en küçük yürütme birimidir.

### **Multithreading Modelleri**
1. **Many-to-One:** Birden fazla kullanıcı thread’i bir kernel thread’i ile eşleştirilir.
2. **One-to-One:** Her kullanıcı thread’i bir kernel thread’i ile eşleştirilir.
3. **Many-to-Many:** Birden fazla kullanıcı thread’i birden fazla kernel thread’i ile eşleştirilir.

### **Multithreading Avantajları**
- **Cevap Verebilirlik:** Uzun süren işlemler sırasında uygulama çalışmaya devam eder.
- **Kaynak Paylaşımı:** Aynı process içindeki thread’ler bellek ve kaynakları paylaşır.
- **Ekonomi:** Thread oluşturmak, process oluşturmaktan daha az maliyetlidir.
- **Ölçeklenebilirlik:** Çok çekirdekli sistemlerde paralel çalışma avantajı sağlar.

---

## **4. Bellek Yönetimi**

### **Bellek Yönetim Teknikleri**
1. **Swapping:** Processlerin bellekteki yerini değiştirme.
2. **Paging:** Belleği sabit boyutlu bloklara (frame) ayırma.
3. **Segmentation:** Belleği mantıksal bölümlere ayırma.

### **Parçalanma (Fragmentation) Sorunları**
1. **İç Parçalanma:** Ayrılan bellek bloğunun kullanılmayan kısmı.
2. **Dış Parçalanma:** Ayrılmış bloklar arasında kullanılmayan alanlar.

### **Sanal Bellek**
- Fiziksel belleğin sınırlarını aşan bir çalışma alanı sağlar.
- **Demand Paging:** Sadece ihtiyaç duyulan sayfalar belleğe yüklenir.

---

## **5. Process Senkronizasyonu**

### **Senkronizasyon Kavramı**
Process senkronizasyonu, birden fazla process'in aynı kaynaklara erişimini düzenler.

### **Critical Section Problemi**
- Paylaşılan kaynaklara eşzamanlı erişimi kontrol eden bir problemdir.
- Çözüm için üç temel koşul:
  1. **Mutual Exclusion:** Aynı anda yalnızca bir process kaynaklara erişebilir.
  2. **Progress:** Processler arasında adil seçim yapılmalıdır.
  3. **Bounded Waiting:** Bir process’in bekleme süresi sınırlı olmalıdır.

### **Senkronizasyon Mekanizmaları**
1. **Mutex:** Kaynaklara erişimi kilitleme.
2. **Semaphore:** Sayısal sayaçlarla kaynak yönetimi.
3. **Monitor:** Yüksek seviyeli senkronizasyon aracı.

---

## **6. Deadlock (Ölümcül Kilitlenme)**

### **Deadlock Nedir?**
- Processlerin birbirlerinden kaynak beklerken sonsuza kadar bekleme durumuna girmesidir.

### **Deadlock Koşulları**
1. **Mutual Exclusion:** Kaynaklar paylaşılamaz.
2. **Hold and Wait:** Kaynak tutup başka kaynak bekleme.
3. **No Preemption:** Kaynaklar zorla alınamaz.
4. **Circular Wait:** Processler döngüsel olarak birbirlerini bekler.

### **Deadlock Yönetimi**
1. **Önleme:** Deadlock koşullarından birini engelleme.
2. **Kaçınma:** Banker's Algorithm gibi yöntemlerle kaynak tahsisi.
3. **Algılama ve Kurtarma:** Deadlock oluştuğunda tespit ve çözüm.

---

## **7. CPU Zamanlaması**

### **Zamanlama Algoritmaları**
1. **First-Come, First-Served (FCFS):** İlk gelen ilk yürütülür.
2. **Shortest-Job-First (SJF):** İşlem süresi en kısa olan yürütülür.
3. **Priority Scheduling:** Öncelik sırasına göre yürütülür.
4. **Round-Robin (RR):** Sabit zaman dilimiyle işlemler sırayla çalıştırılır.

### **Zamanlama Kriterleri**
- **CPU Kullanımı:** CPU’nun aktif kullanım oranı.
- **Bekleme Süresi:** Process'in ilgili kuyrukta bekleme süresi.
- **Yanıt Süresi:** İlk yanıtın verilme süresi.
- **Throughput:** Belirli bir zaman diliminde tamamlanan process sayısı.

---

## **8. Sanal Bellek**

### **Sanal Bellek Nedir?**
- Fiziksel belleğin sınırlarını aşan mantıksal bir bellek alanıdır.
- Programların tamamı bellekte olmadan çalıştırılabilir.

### **Sanal Bellek Teknikleri**
1. **Demand Paging:** Sadece ihtiyaç duyulan sayfalar belleğe yüklenir.
2. **Copy-on-Write:** Sayfa paylaşımını optimize eder.
3. **Thrashing:** Aşırı sayfa değiştirme nedeniyle sistem performansının düşmesi.

### **Page Replacement Algoritmaları**
1. **FIFO (First-In, First-Out):** İlk yüklenen sayfa ilk çıkarılır.
2. **Optimal:** Gelecekte en uzun süre kullanılmayacak sayfa çıkarılır.
3. **LRU (Least Recently Used):** En uzun süredir kullanılmayan sayfa çıkarılır.

---





# **Bellek Yönetimi - Detaylı ve Geliştirilmiş Notlar**

Bellek yönetimi, bilgisayar sistemlerinde RAM'in ve diğer depolama kaynaklarının etkin, adil ve verimli bir şekilde kullanılması için geliştirilen teknik ve algoritmaları kapsar. Bu notlar, bellek yönetimi konusunu derinlemesine anlamanıza yardımcı olacak şekilde düzenlenmiştir.

---

## **1. Bellek Yönetiminin Amacı**

Bellek yönetimi, bilgisayar kaynaklarının verimli kullanımını sağlamak için işletim sistemi tarafından uygulanan tekniklerin bütünüdür. Başlıca amaçları:
- **İşlemcinin etkinliğini artırmak:** CPU'nun sürekli çalışmasını sağlamak.
- **Belleği verimli kullanmak:** Bellek israfını önlemek.
- **Çoklu program çalışmasını desteklemek:** Birden fazla programın aynı anda çalışmasına olanak tanımak.
- **Güvenlik sağlamak:** Programların birbirinin belleğine erişmesini engellemek.

---

## **2. Temel Kavramlar**

### **2.1 Fiziksel Bellek**
- Gerçek RAM. Bilgisayarın anakartında bulunan donanımdır.
- Örn: 8 GB RAM’iniz varsa, fiziksel belleğiniz budur.

### **2.2 Sanal Bellek**
- Diskin bir kısmını RAM olarak kullanma yöntemidir.
- RAM yetmediğinde devreye girer ve programların çalışmaya devam etmesini sağlar.
- **Örnek:** Bilgisayarınızda 4 GB RAM var, ancak 6 GB'lık bir program çalıştırıyorsunuz. Eksik 2 GB disk alanından (swap) karşılanır.

### **2.3 Adres Alanı**
- Her programın kendi sanal adres alanı vardır.
- İşlemci, fiziksel bellek yerine sanal adreslerle çalışır.
- Bellek Yönetim Birimi (**MMU**) bu sanal adresleri fiziksel adreslere çevirir.

---

## **3. Bellek Yönetim Teknikleri**

### **3.1 Sabit Bölmeli Bellek (Fixed Partitioning)**

- Bellek, sabit boyutlu bölümlere ayrılır.
- Her bir program, bu bölümlerden birine yerleştirilir.
- **Sorun:** Programın boyutu küçükse, artan alan boşa gider (**iç parçalanma**).

#### **Örnek:**
- RAM: 400 KB, 4 eşit bölüme ayrılmış (100 KB + 100 KB + 100 KB + 100 KB).
- 70 KB’lik bir program bir bölüme yerleştirilir.
- **Kalan 30 KB boşa gider.**

---

### **3.2 Değişken Bölmeli Bellek (Variable Partitioning)**

- Bellek, programların ihtiyaç duyduğu kadar bölümlere ayrılır.
- Daha esnek bir yöntemdir ancak **dış parçalanma** oluşabilir.

#### **Örnek:**
- RAM: 400 KB.
  1. 70 KB program geldi → 70 KB verildi.
  2. 150 KB program geldi → 150 KB verildi.
  3. İlk 70 KB’lik program çıktı.
  4. Yeni gelen 100 KB’lik program, çıkan yere sığmaz (70 KB) → **Dış Parçalanma.**

---

### **3.3 Sayfalama (Paging)**

- Bellek, sabit boyutlu bloklara (**sayfa/page**) ayrılır.
- Programlar, bu sayfalara bölünerek fiziksel belleğe dağınık şekilde yerleştirilir.
- **Sayfa Tablosu:** Hangi sayfa fiziksel belleğin hangi kısmında tutuluyor, bunu takip eder.

#### **Örnek:**
- Program: 12 KB.
- Sayfa Boyutu: 4 KB.
  - Program → 3 sayfa olur (P0, P1, P2).
  - Fiziksel Bellek: P0 → 2. blok, P1 → 5. blok, P2 → 8. blok.
- **Avantaj:** Dış parçalanmayı önler.

---

### **3.4 Segmentasyon**

- Programlar, mantıksal parçalara (**segment**) ayrılır:
  - Kod Segmenti
  - Veri Segmenti
  - Yığın (**Stack**) Segmenti.
- Her segmentin başlangıç adresi ve uzunluğu saklanır.

#### **Örnek:**
- Kod Segmenti: 0x0000–0x1FFF.
- Veri Segmenti: 0x2000–0x3FFF.
- Stack: 0x4000’den başlar.

**Not:** Segmentasyon, mantıksal bir düzen sağlar.

---

### **3.5 Sayfalı Segmentasyon (Segmented Paging)**

- **Sayfalama** ve **Segmentasyon** yöntemlerinin birleşimidir.
- Segmentler, sayfalara bölünür ve bu sayfalar fiziksel belleğe yerleştirilir.

#### **Örnek:**
- Kod Segmenti → 3 sayfa.
- Veri Segmenti → 2 sayfa.
- **Avantaj:** Hem düzen sağlar, hem de dış parçalanmayı önler.

---

## **4. Parçalanma Türleri**

### **4.1 İç Parçalanma**
- Bellek bloğu büyük, program küçük → Artan alan boşa gider.
- **Örnek:** 100 KB’lik bölüme 60 KB’lik program → 40 KB boşa gider.

### **4.2 Dış Parçalanma**
- RAM’de boşluklar var ama kesintisiz değil → Yeni program sığmaz.
- **Örnek:** 3 tane 30 KB boşluk var ama 70 KB’lik program gelirse, sığamaz.

---

## **5. Bellek Yerleştirme Algoritmaları**

### **5.1 First Fit**
- İlk uygun boşluğa yerleştirir.
- **Avantaj:** En hızlıdır.
- **Dezavantaj:** Zamanla parçalanma oluşabilir.

### **5.2 Best Fit**
- En küçük uygun boşluğu seçer.
- **Avantaj:** İç parçalanmayı azaltır.
- **Dezavantaj:** Daha yavaş çalışır.

### **5.3 Worst Fit**
- En büyük boşluğu kullanır.
- **Avantaj:** Büyük parçaları korur.
- **Dezavantaj:** Verimsiz olabilir.

---

## **6. Sanal Bellek (Virtual Memory)**

### **Amaç:**
- Fiziksel belleğin yetersiz olduğu durumlarda, diski kullanarak programların çalışmasını sağlamak.
- Programların tamamı belleğe yüklenmeden çalışabilir.

### **Nasıl Çalışır?**
- **Swap Alanı:** Diskte ayrılmış bir bölge, sanal bellek olarak kullanılır.
- **Sayfalama ve Segmentasyon:** Sanal belleğin temelini oluşturur.

#### **Örnek:**
- Photoshop 6 GB RAM kullanıyor.
- Bilgisayarınızda 4 GB RAM var.
- Eksik 2 GB, diskte sanal bellek olarak karşılanır.

---

## **7. Bellek Koruma**

- Bellek koruma, programların birbirinin belleğine erişmesini engeller.
- Donanım desteğiyle sağlanır (**MMU: Memory Management Unit**).

#### **Örnek:**
- Chrome çalışırken, Word’ün belleğine erişemez.
- **Aksi takdirde:** Virüsler her yere ulaşabilir.

---

## **8. Özet**

Bellek yönetimi, bilgisayar sistemlerinde RAM’in etkin bir şekilde kullanılması için geliştirilmiş bir dizi teknik ve algoritmayı içerir. Başlıca hedefleri:
- Bellek israfını önlemek.
- Programların güvenli ve verimli çalışmasını sağlamak.
- Fiziksel belleğin sınırlarını aşarak sanal bellek desteği sunmak.

---

Bu geliştirilmiş ve detaylı notlar, bellek yönetimi konusunu daha derinlemesine anlamanıza yardımcı olacaktır. Her bir konu, gerçek dünyadan örneklerle desteklenmiş ve daha öğretici hale getirilmiştir. 😊
