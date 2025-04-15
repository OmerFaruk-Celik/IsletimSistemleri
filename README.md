# **İşletim Sistemleri Çalışma Notları**

Bu notlar, işletim sistemleri derslerinde sıkça karşılaşılan konuları kapsamlı bir şekilde ele alır. İçerik, işletim sistemlerinin temel kavramlarından başlayarak, process yönetimi, bellek yönetimi, senkronizasyon ve CPU zamanlaması gibi ileri düzey konulara kadar geniş bir kapsam sunar.

---

## **1. İşletim Sistemi Temel Kavramları**

### **İşletim Sistemi Nedir?**
İşletim sistemi, bilgisayar donanımını yöneten ve kullanıcı programlarının çalışması için bir ortam sağlayan temel yazılım bileşenidir. İşletim sisteminin başlıca görevleri:
- Donanım kaynaklarını adil ve verimli bir şekilde kullanmak.
- Kullanıcı ve programların gereksinimlerini karşılamak.
- Bellek, CPU, giriş/çıkış cihazları gibi donanım bileşenlerini yönetmek.

### **İşletim Sisteminin Temel İşlevleri**
1. **Kullanıcı programlarının uygun çalışmasını sağlamak.**
2. **Donanım kaynaklarını yönetmek ve tahsis etmek.**
3. **Bilgisayar sistemini kontrol altında tutmak.**

### **Temel Kavramlar**
- **Kesme (Interrupt):** Donanım veya yazılımın CPU’nun dikkatini çekmek için kullandığı bir mekanizmadır.
- **Çoklu Programlama (Multiprogramming):** Birden fazla programın aynı anda bellekte saklanması ve yürütülmesi.
- **Çoklu Görev (Multitasking):** CPU'nun birden fazla işlemi kısa aralıklarla çalıştırarak eşzamanlılık sağlaması.

---

## **2. Process Kavramı**

### **Process Nedir?**
Process, bellekte yüklü olan ve çalışmakta olan bir programdır. Bir process, programın aktif bir örneğidir ve işletim sistemi tarafından yönetilir.

### **Process Bileşenleri**
1. **Text Section:** Program kodu.
2. **Data Section:** Global değişkenler.
3. **Heap:** Dinamik bellek tahsisi için ayrılmış alan.
4. **Stack:** Fonksiyon parametreleri, lokal değişkenler ve geri dönüş adreslerini saklar.

### **Process Durumları**
1. **New:** Process oluşturuluyor.
2. **Ready:** Process CPU’da çalışmak için hazır.
3. **Running:** Process CPU üzerinde yürütülüyor.
4. **Waiting:** Process bir olayın gerçekleşmesini bekliyor (ör. I/O işlemi).
5. **Terminated:** Process tamamlandı.

### **Process Scheduling**
Processlerin CPU’da çalıştırılma sırasını belirler. Üç tür scheduler vardır:
1. **Long-term Scheduler:** Disk üzerindeki işleri hafızaya yükler.
2. **Short-term Scheduler:** Hazır kuyruğundaki processlerden hangisinin CPU kullanacağını belirler.
3. **Medium-term Scheduler:** Bellekteki processlerin disk ile değişimini yönetir (swapping).

### **Context Switch**
Bir process CPU’dan çıkarılırken durum bilgilerinin kaydedilmesi ve başka bir process'e geçilmesi işlemidir. Bu işlem, zaman kaybına neden olabilir.

---

## **3. Thread ve Multithreading**

### **Thread Nedir?**
Thread, bir process içindeki en küçük yürütme birimidir. Bir process, birden fazla thread içerebilir.

### **Thread Çeşitleri**
1. **User-level Threads:** İşletim sistemi tarafından fark edilmez.
2. **Kernel-level Threads:** İşletim sistemi tarafından yönetilir.

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

### **Parçalanma Problemleri**
1. **İç Parçalanma:** Blok içindeki kullanılmayan alanlar.
2. **Dış Parçalanma:** Ayrılmış bloklar arasında kullanılmayan alanlar.

### **Sanal Bellek**
Fiziksel belleğin sınırlarını aşan bir çalışma alanı sağlar. **Demand Paging** yöntemiyle sadece ihtiyaç duyulan sayfalar belleğe yüklenir.

---

## **5. Process Senkronizasyonu**

### **Senkronizasyon Kavramı**
Birden fazla process'in aynı kaynaklara erişimini koordine etmek için kullanılan mekanizmalardır.

### **Critical Section Problemi**
Paylaşılan kaynaklara eşzamanlı erişimi kontrol etmek için geliştirilmiş bir problem. Çözüm için üç koşul:
1. **Mutual Exclusion:** Bir kaynak aynı anda sadece bir process tarafından kullanılabilir.
2. **Progress:** Processler arasında adil bir seçim yapılmalıdır.
3. **Bounded Waiting:** Bir process’in bekleme süresi sınırlı olmalıdır.

### **Senkronizasyon Mekanizmaları**
- **Mutex:** Kaynaklara erişimi kilitleme.
- **Semaphore:** Sayısal sayaçlarla kaynak yönetimi.
- **Monitor:** Yüksek seviyeli senkronizasyon aracı.

---

## **6. Deadlock (Ölümcül Kilitlenme)**

### **Deadlock Nedir?**
Processlerin birbirlerinden kaynak beklerken sonsuza kadar bekleme durumuna girmesidir.

### **Deadlock Koşulları**
1. **Mutual Exclusion:** Kaynaklar paylaşılamaz.
2. **Hold and Wait:** Kaynak tutup başka kaynak bekleme.
3. **No Preemption:** Kaynaklar zorla alınamaz.
4. **Circular Wait:** Processler döngüsel olarak birbirlerini bekler.

### **Deadlock Yönetimi**
1. **Önleme:** Deadlock koşullarından birini engelleme.
2. **Kaçınma:** Kaynak tahsis algoritmalarıyla deadlock’tan kaçınma.
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

## **8. Örnek Problemler ve Çözümler**

### **Producer-Consumer Problemi**
Paylaşılan bir tampon kullanılarak üretilen ve tüketilen ürünlerin senkronize edilmesi.

#### **Çözüm:**
- **Semaphore:** Üretici ve tüketiciyi kontrol etmek için kullanılır.
- **Paylaşılan Bellek:** Tüm processler aynı tamponu paylaşır.

---

Bu notlar, işletim sistemleri konusunu kapsamlı bir şekilde anlamak ve sınavlara hazırlanmak için bir rehber niteliğindedir. Konuların her biri, örnekler ve açıklamalarla desteklenerek öğrenmeyi kolaylaştırır.
