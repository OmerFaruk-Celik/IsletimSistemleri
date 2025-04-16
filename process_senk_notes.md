# **🧠 Process Senkronizasyonu – Detaylı ve Örnekli Çalışma Notları**

Process senkronizasyonu, birden fazla işlem veya thread'in aynı kaynaklara eşzamanlı erişim sırasında veri tutarsızlıklarını önlemek için kullanılan mekanizmalar bütünüdür. Bu mekanizmalar, işlemlerin güvenli ve düzenli bir şekilde çalışmasını sağlar.

---

## **📄 Sayfa 1: Process Senkronizasyonunun Amacı**

### **Neden Gerekli?**
- Paylaşılan kaynaklara (örneğin: bellek, dosyalar, veri tabanları) aynı anda erişildiğinde veri bozulmaları ve tutarsızlıklar oluşabilir.
- **Process senkronizasyonu**, bu tür sorunları önlemek ve işlemler arasında uyum sağlamak için kullanılır.

#### **🎯 Hedefler:**
1. **Veri tutarlılığı:** Paylaşılan veriler doğru kalmalı.
2. **Adil erişim:** Hiçbir işlem kaynaklara erişimde "aç bırakılmamalıdır" (Starvation önlenmeli).
3. **Ölümlü kilitlenme (Deadlock) önleme:** Prosesler birbirlerini bekleyerek sonsuza kadar kilitlenmemeli.

---

## **📄 Sayfa 2: Kritik Bölge (Critical Section) Problemi**

### **Kritik Bölge Nedir?**
Kritik bölge, birden fazla işlem veya thread'in aynı anda erişmeye çalıştığı paylaşılan kaynakların bulunduğu kod bloğudur.

#### **🎯 Amaç:**  
Kritik bölgeye aynı anda yalnızca **bir işlem** girebilmelidir.

### **Kritik Bölge Probleminin Çözümünde Sağlanması Gereken Koşullar:**
1. **Mutual Exclusion (Karşılıklı Dışlama):**
   - Bir işlem kritik bölgedeyken, başka hiçbir işlem aynı anda bu bölgeye giremez.
2. **Progress (İlerlemenin Sağlanması):**
   - Kritik bölgede işlem yoksa, kaynaklara erişim için bekleyen işlemler arasında adil bir seçim yapılmalıdır.
3. **Bounded Waiting (Sınırlı Bekleme):**
   - Bir işlem kritik bölgeye girmek için istekte bulunduğunda, bekleme süresi sınırlı olmalıdır. Yani bir işlem sonsuza kadar bekletilemez.

#### **📌 Örnek:**  
- **Durum:** Banka hesabından iki işlem aynı anda para çekmeye çalışıyor.
- **Sonuç:**
  - Eğer senkronizasyon uygulanmazsa, iki işlem de aynı bakiye üzerinden işlem yapabilir ve hatalı sonuçlar oluşabilir.
  - Senkronizasyon mekanizmalarıyla bu işlemler sırayla gerçekleştirilir.

---

## **📄 Sayfa 3: Senkronizasyon Mekanizmaları**

### **1. Mutex (Mutual Exclusion Lock)**
- **Tanım:** Bir kaynak üzerinde aynı anda yalnızca bir işlem çalışabilsin diye kullanılan bir kilit mekanizmasıdır.
- **Nasıl Çalışır?**
  - **Kritik bölgeye girmek:** `lock()` çağrılır.
  - **Kritik bölgeden çıkmak:** `unlock()` çağrılır.
- **Örnek:**
  ```c
  mutex.lock(); // Kaynağı kilitle
  // Kritik Bölge
  mutex.unlock(); // Kaynağı serbest bırak
  ```
- **Avantaj:** Basit ve etkilidir.
- **Dezavantaj:** Meşgul bekleme (**Busy Waiting**) oluşabilir. Kritik bölge doluyken, diğer işlemler CPU’yu boşa kullanabilir.

---

### **2. Semaphore**
- **Tanım:** Kaynaklara erişimi bir sayaç aracılığıyla kontrol eden mekanizmadır.
- **Türleri:**
  1. **Binary Semaphore:** 0 veya 1 değerini alır (Mutex gibi çalışır).
  2. **Counting Semaphore:** Birden fazla kaynağı aynı anda kontrol edebilir.
- **Nasıl Çalışır?**
  - **Kaynağı almak:** `wait()` (veya `P()`).
  - **Kaynağı bırakmak:** `signal()` (veya `V()`).
- **Örnek:**
  ```c
  semaphore.wait(); // Kaynak müsaitse eriş
  // Kritik Bölge
  semaphore.signal(); // Kaynağı serbest bırak
  ```
- **Avantaj:** Aynı anda birden fazla işlem için kullanılabilir.
- **Dezavantaj:** Yanlış kullanıldığında deadlock veya starvation oluşabilir.

---

### **3. Monitor**
- **Tanım:** Yüksek seviyeli bir senkronizasyon aracıdır. Paylaşılan kaynaklara erişim için gerekli kilitleri otomatik olarak yönetir.
- **Nasıl Çalışır?**
  - **Koşul Değişkenleri:** `wait()` ve `signal()` ile işlemlerin sırasını belirler.
- **Örnek (Java’da synchronized):**
  ```java
  synchronized void criticalSection() {
      // Kritik Bölge
  }
  ```
- **Avantaj:** Programcı, kilitleme ve serbest bırakma işlemlerini manuel olarak yapmak zorunda kalmaz.
- **Dezavantaj:** Bazı programlama dillerinde desteklenmez.

---

## **📄 Sayfa 4: Kritik Bölge Problemi Çözümüne Örnek**

### **Örnek Problem: Producer-Consumer (Üretici-Tüketici) Problemi**

#### **Tanım:**
- Bir **üretici** veri üretir ve bir tamponda saklar.
- Bir **tüketici**, bu tampondan veri tüketir.
- **Sorun:** Üretici ve tüketici aynı tampon alanına erişmeye çalışırsa veri tutarsızlığı oluşabilir.

#### **Çözüm (Semaphore ile):**
```c
semaphore full = 0;    // Tüketici için dolu tampon sayacı
semaphore empty = N;   // Üretici için boş tampon sayacı
semaphore mutex = 1;   // Kritik bölgeyi kontrol eder

// Üretici
wait(empty);
wait(mutex);
// Veriyi üret ve tampona koy
signal(mutex);
signal(full);

// Tüketici
wait(full);
wait(mutex);
// Tampondan veriyi al ve işle
signal(mutex);
signal(empty);
```

#### **Sonuç:**
- **Mutual Exclusion:** `mutex` ile sağlanır.
- **Progress:** `full` ve `empty` semaforları üretim ve tüketim sırasını düzenler.

---

## **📄 Sayfa 5: Önemli Sorunlar ve Çözümler**

### **1. Deadlock (Ölümcül Kilitlenme)**
- **Tanım:** İşlemler birbirlerinden kaynak beklerken sonsuz döngüye girer.
- **Çözüm:**
  - Kaynakları belirli bir sırada talep etmek.
  - Timeout mekanizması kullanmak.

---

### **2. Starvation (Açlık)**
- **Tanım:** Düşük öncelikli işlemler, kaynaklara erişim hakkı elde edemeyebilir.
-
