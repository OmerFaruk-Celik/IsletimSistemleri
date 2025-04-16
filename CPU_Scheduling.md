# **🧠 CPU Scheduling – Algoritmalar ve Kriterler**

Bu notlar, CPU Scheduling algoritmalarını ve değerlendirme kriterlerini detaylı ve örneklerle desteklenmiş bir şekilde açıklar.

---

## **📄 CPU Scheduling Algoritmaları**

### **1. FCFS (First Come First Serve)**
- **Mantık:** İşlemler, sıraya göre yürütülür. İlk gelen işlem önce çalışır.
- **Avantaj:** Basit ve adil bir yöntem.
- **Dezavantaj:** Uzun işlemler, diğerlerini bekletir (**Convoy Effect**).

#### **📌 Örnek:**
| Proses | Süre (ms) |
|--------|-----------|
| **P1** | 24        |
| **P2** | 3         |
| **P3** | 3         |

**Sıra:** P1 → P2 → P3  
**Bekleme Süreleri:**
- **P1:** 0 ms.
- **P2:** 24 ms.
- **P3:** 27 ms.  
**Ortalama Bekleme Süresi:** (0 + 24 + 27) / 3 = **17 ms**

---

### **2. SJF (Shortest Job First)**
- **Mantık:** Süresi en kısa olan işlem önce çalışır.
- **Avantaj:** Ortalama bekleme süresini düşürür.
- **Dezavantaj:** İşlem sürelerini tahmin etmek zordur.

#### **📌 Örnek:**
| Proses | Süre (ms) |
|--------|-----------|
| **P1** | 6         |
| **P2** | 8         |
| **P3** | 7         |
| **P4** | 3         |

**Sıra:** P4 → P1 → P3 → P2  
**Bekleme Süreleri:**
- **P4:** 0 ms.
- **P1:** 3 ms.
- **P3:** 9 ms.
- **P2:** 16 ms.  
**Ortalama Bekleme Süresi:** (0 + 3 + 9 + 16) / 4 = **7 ms**

---

### **3. Priority Scheduling**
- **Mantık:** Önceliği yüksek olan işlem önce çalışır. (Öncelik: Küçük sayı = Yüksek öncelik)
- **Avantaj:** Kritik işlemler hızlı tamamlanır.
- **Dezavantaj:** Düşük öncelikli işlemler bekleyebilir (**Starvation**).

#### **📌 Örnek:**
| Proses | Süre (ms) | Öncelik |
|--------|-----------|---------|
| **P1** | 10        | 3       |
| **P2** | 1         | 1       |
| **P3** | 2         | 4       |
| **P4** | 1         | 5       |

**Sıra:** P2 → P1 → P3 → P4

**Not:** Starvation problemini çözmek için **Yaşlandırma (Aging)** kullanılabilir.

---

### **4. Round Robin**
- **Mantık:** Her işleme sırayla sabit bir zaman dilimi (**Quantum**) verilir. Quantum süresi bitince işlem kuyruğun sonuna atılır.
- **Avantaj:** Kullanıcı dostudur, hızlı yanıt verir.
- **Dezavantaj:** Quantum küçükse fazla **context switch** olur.

#### **📌 Örnek:**
| Proses | Süre (ms) |
|--------|-----------|
| **P1** | 24        |
| **P2** | 3         |
| **P3** | 3         |

**Quantum:** 4 ms.  
**Çalışma Sırası:**  
P1 (4) → P2 (3) → P3 (3) → P1 (4) → P1 (4) → P1 (4) → P1 (4)

---

### **5. SRTF (Shortest Remaining Time First)**
- **Mantık:** En kısa kalan süreye sahip işlem önce çalışır. **SJF**’nin preemptive versiyonudur.
- **Avantaj:** Ortalama bekleme süresi çok düşüktür.
- **Dezavantaj:** İşlem yarıda kesilebilir.

#### **📌 Örnek:**
- P1 başlar (10 ms).  
- 2 ms sonra **P2 gelir (kalan 5 ms).**  
- **P2**, kalan süresi daha kısa olduğu için öncelik alır.

---

### **6. Multilevel Queue**
- **Mantık:** İşlemler, türlerine göre farklı kuyruklara ayrılır. Her kuyruğun kendi algoritması vardır.
- **Avantaj:** İş türüne göre özelleştirme sağlar.
- **Dezavantaj:** Kuyruklar arasında geçiş yoktur.

#### **📌 Örnek:**
| Kuyruk Türü          | Algoritma    |
|----------------------|--------------|
| Etkileşimli işlemler | Round Robin  |
| Arka plan işlemleri  | FCFS         |

---

### **7. Multilevel Feedback Queue (MLFQ)**
- **Mantık:** İşlem performansına göre kuyruklar arasında geçiş yapılır. Dinamik bir yapıdır.
- **Avantaj:** Hem adil hem de verimlidir.
- **Dezavantaj:** Karmaşıktır.

#### **📌 Örnek:**
- **CPU’yu çok kullanan işlem:** Alt seviyeye alınır.
- **Kısa işlem:** Üst seviyeye çıkarılır.

---

## **📄 CPU Scheduling Kriterleri**

### **1. CPU Kullanımı (CPU Utilization)**
- **Tanım:** CPU'nun aktif olarak kullanıldığı zamanın toplam çalışma süresine oranı.
- **Amaç:** CPU’nun her zaman çalışır durumda olması.

---

### **2. Throughput**
- **Tanım:** Belirli bir zaman diliminde tamamlanan işlem sayısı.
- **Amaç:** İşlem sayısını artırmak.

---

### **3. Turnaround Time**
- **Tanım:** Bir işlemin gönderilmesi ile tamamlanması arasında geçen süre.
- **Hesaplama:** `Turnaround Time = Çıkış Zamanı - Giriş Zamanı`

---

### **4. Waiting Time**
- **Tanım:** İşlemin Ready kuyruğunda beklediği toplam süre.
- **Hesaplama:** `Waiting Time = Turnaround Time - İşlem Süresi`

---

### **5. Response Time**
- **Tanım:** Bir işlem tarafından verilen ilk yanıtın alınma süresi.
- **Amaç:** Kullanıcıların hızlı yanıt almasını sağlamak.

---

## **📄 Algoritmaların Karşılaştırması**

| **Algoritma**         | **Preemptive?** | **Açlık Riski** | **Ortalama Bekleme Süresi** | **Kullanıcı Dostu** |
|------------------------|-----------------|-----------------|-----------------------------|---------------------|
| **FCFS**              | Hayır           | Az              | Orta                        | Düşük               |
| **SJF**               | Hayır           | Yüksek          | En düşük                    | Düşük               |
| **SRTF**              | Evet            | Yüksek          | Çok düşük                   | Orta                |
| **Priority**          | Her ikisi       | Yüksek          | Orta                        | Değişken            |
| **Round Robin**       | Evet            | Düşük           | Orta                        | Yüksek              |
| **Multilevel Queue**  | Hayır           | Orta            | Orta                        | Orta                |
| **MLFQ**              | Evet            | Düşük           | Düşük                       | Yüksek              |

---

Bu notlar, CPU Scheduling algoritmalarını ve kriterlerini detaylı bir şekilde anlamak için kapsamlı bir rehber niteliğindedir. Daha fazla açıklama veya başka bir konuda yardım istersen, memnuniyetle destek olurum! 😊
