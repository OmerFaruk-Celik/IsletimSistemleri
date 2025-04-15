# ⚙️ İŞletim Sistemleri Kapsamlı ve Geliştirilmiş Çalışma Notları

Bu notlar, işletim sistemleriyle ilgili temel kavramlardan başlayarak proses yönetimi, bellek yönetimi, thread ve multithreading, senkronizasyon, CPU zamanlaması ve sanal bellek gibi konuları detaylı bir şekilde ele alır. Ayrıca, sınavlar için faydalı olabilecek örnekler, tablolar ve karşılaştırmalarla zenginleştirilmiştir.

## 1. İŞletim Sistemi Temel Kavramları

### İŞletim Sistemi Nedir?
İşletim sistemi, bilgisayar donanımını yöneten ve kullanıcı programlarının çalışması için bir ortam sağlayan temel yazılım bileşenidir.

#### İşlevleri:
- Donanım kaynaklarını adil ve etkin şekilde tahsis eder.
- Bellek, CPU, giriş/çıkış cihazlarını yönetir.
- Kullanıcıya CLI veya GUI ile arabirim sunar.
- Program yürütme, hata kontrolü ve veri yönetimi sağlar.

---

## 2. Process (Proses) Kavramı

### Process Nedir?
Bellekte yüklü olan ve çalışan bir program.

### Bileşenleri:
- **Text:** Program kodu
- **Data:** Global değişenler
- **Heap:** Dinamik bellek
- **Stack:** Lokal değişenler ve fonksiyon bilgileri

### Durumlar:
- New, Ready, Running, Waiting, Terminated

### Scheduling:
- **Long-term:** Diskten belleğe alır.
- **Short-term:** CPU için seçim yapar.
- **Medium-term:** Swap işlemleri

---

## 3. Thread ve Multithreading

### Thread Nedir?
Bir process içinde bağımsız çalışabilen en küçük birim.

### Modeller:
- Many-to-One
- One-to-One
- Many-to-Many

### Avantajlar:
- Daha az kaynak kullanımı
- Daha hızlı tepki
- Paralel çalışma imkanı

---

## 4. Bellek Yönetimi

### Teknikler:
- **Swapping:** Bellekten diske, diskten belleğe
- **Paging:** Sabit boyutlu sayfalar
- **Segmentation:** Mantıksal bölümleme

### Parçalanma:
- **Iç Parçalanma:** Ayrılan blokların boş kalan kısmı
- **Dış Parçalanma:** Bloklar arasındaki boşluklar

### Sanal Bellek:
- RAM yetmediğinde disk kullanılır.
- Demand Paging, Thrashing, COW desteklidir.

---

## 5. Process Senkronizasyonu

### Kritik Bölge Problemi:
- **Mutual Exclusion:** Aynı anda birden fazla erişime izin verilmez.
- **Progress & Bounded Waiting** 

### Mekanizmalar:
- Mutex, Semaphore, Monitor

---

## 6. Deadlock (Kilitleme)

### Koşullar:
- Mutual Exclusion
- Hold & Wait
- No Preemption
- Circular Wait

### Çözümler:
- Önleme, Kaçınma (Banker’s Algorithm), Algılama & Kurtarma

---

## 7. CPU Scheduling

### Algoritmalar:
- **FCFS:** Sıra ile
- **SJF:** Kısa işlem önce
- **Priority:** Önceliklere göre
- **Round Robin:** Quantum time ile döngüsel
- **SRTF, MLFQ, Multilevel Queue**

### Kriterler:
- CPU kullanımı, throughput, bekleme, yanıt, turnaround

---

## 8. Sanal Bellek

### Teknikler:
- Demand Paging
- Copy-on-Write
- Thrashing

### Sayfa Değişim Algoritmaları:
- FIFO, LRU, Optimal

---

## 9. Bellek Yerleştirme Algoritmaları

- **First Fit:** İlk uygun yere
- **Best Fit:** En küçük uygun yere
- **Worst Fit:** En büyük boşluğa

---

## 10. Gantt Diyagramı

Zamanlama algoritmalarını görselleştirir.

---

## 11. Zamanlama Karşılaştırması

| Algoritma        | Preemptive | Bekleme Süresi | Kullanıcı Dostu |
|------------------|------------|------------------|------------------|
| FCFS             | Hayır      | Orta             | Düşük           |
| SJF              | Hayır      | Düşük           | Düşük           |
| SRTF             | Evet       | En Düşük        | Orta             |
| Priority         | Evet/Hayır| Orta             | Değişken         |
| Round Robin      | Evet       | Orta             | Yüksek            |
| MLFQ             | Evet       | Düşük           | Yüksek            |

---

## 12. Kaynaklar

- Tanenbaum - Modern Operating Systems
- Silberschatz - Operating System Concepts
- Lecture slides and university notes

---

> Hazırlayan: [Ömer Faruk Çelik](https://github.com/kullaniciadi)

Bu repo, işletim sistemleri dersine çalışan öğrenciler için kapsamılı bir kaynak sunmayı amaçlamaktadır. Geri bildirim ve katkılarınızı beklerim! ✨

