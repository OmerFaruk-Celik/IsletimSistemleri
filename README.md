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

Bu notlar, işletim sistemleri konusunu kapsamlı bir şekilde anlamak ve sınavlara hazırlanmak için rehber niteliğindedir. Konular, öğrenmeyi kolaylaştıracak şekilde yapılandırılmış ve eksik olan bilgilerle zenginleştirilmiştir.
