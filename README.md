# 📚 Öğrenci Etüt Programı Optimizasyonu: Genetik Algoritma (GA)

Bu proje, bir öğrencinin **matematik (x₁) ve fen (x₂) etüt sürelerini** en verimli şekilde planlayarak **başarı skorunu maksimize etmeyi** amaçlamaktadır. Problem, **Genetik Algoritma (GA)** kullanılarak çözülmüş bir **kısıtlı optimizasyon problemi** olarak ele alınmıştır.

---

## 1. 📝 Problem Tanımı ve Matematiksel Model

Amaç, öğrencinin haftalık etüt sürelerini temsil eden karar değişkenlerini kullanarak başarı skorunu en üst düzeye çıkarmaktır.

### Amaç Fonksiyonu (Maksimizasyon)

Başarı skorunu hesaplamak için kullanılan fonksiyon:

\[
y = 4x_1 + 5x_2 - 0.5x_1^2 - 0.2x_2^2
\]

- **x₁:** Matematik etüt süresi (saat)  
- **x₂:** Fen etüt süresi (saat)

Doğrusal terimler etüt sürelerinin başarıya katkısını, karesel terimler ise aşırı çalışmanın verimi düşürücü etkisini modellemektedir.

---

### Kısıtlamalar

Değişkenler hem fiziksel sınırlar hem de problem tanımına özgü kısıtlarla sınırlandırılmıştır:

| Kısıt Tipi | Değişken | Aralık / Kural |
| :--- | :--- | :--- |
| **Fiziksel Aralık** | x₁ (Matematik) | \( 0 \leq x_1 \leq 10 \) |
| **Fiziksel Aralık** | x₂ (Fen) | \( 0 \leq x_2 \leq 10 \) |
| **Problem Kısıtı** | x₁ + x₂ | \( x_1 + x_2 \leq 12 \) |
| **Problem Kısıtı** | x₂ | \( x_2 \geq 2 \) |

Kısıt ihlalleri, genetik algoritma içerisinde **ceza (penalty) yöntemi** kullanılarak ele alınmıştır.

---

## 2. ⚙️ Genetik Algoritma (GA) Yapısı

Optimizasyon probleminin çözümü için kullanılan Genetik Algoritma’nın temel parametreleri ve mekanizmaları aşağıda sunulmuştur.

### GA Parametreleri

| Parametre | Değer | Açıklama |
| :--- | :--- | :--- |
| Popülasyon Büyüklüğü (`POPULASYON_BOYUTU`) | 30 | Her nesildeki birey sayısı |
| Nesil Sayısı (`NESIL_SAYISI`) | 50 | Algoritmanın çalışacağı toplam nesil sayısı |
| Mutasyon Oranı (`MUTASYON_ORANI`) | 0.2 | Genlerin mutasyona uğrama olasılığı |
| Mutasyon Büyüklüğü | 1.0 | Mutasyon sırasında eklenecek rastgele değişim miktarı |

---

### GA Operatörleri ve Stratejileri

- **Başlangıç Popülasyonu:** x₁ ve x₂ değişkenleri, tanımlanan sınırlar içerisinde **rastgele** oluşturulmuştur.
- **Seçilim (Selection):** Ebeveyn seçimi için **Rulet Tekerleği Seçimi** yöntemi kullanılmıştır.
- **Çaprazlama (Crossover):** **Tek Noktalı Çaprazlama** uygulanarak ebeveynlerin genleri birleştirilmiştir.
- **Mutasyon (Mutation):** Belirlenen olasılık ile genlere küçük rastgele değişimler uygulanmış ve sınır kontrolleri yapılmıştır.
- **Kısıt Yönetimi (Ceza Fonksiyonu):** Kısıt ihlali yapan bireylerin fitness değeri düşürülerek seçilme olasılıkları azaltılmıştır.
- **Elitizm:** Her neslin en iyi bireyi doğrudan bir sonraki nesle aktarılmıştır.

---

## 3. 📈 Görselleştirme ve Analiz

Algoritmanın performansını değerlendirmek amacıyla:

- Nesillere göre **en iyi x₁ ve x₂ değerlerinin değişimi**
- Nesillere göre **en iyi fitness değerinin değişimi**

grafikler aracılığıyla görselleştirilmiştir. Bu sayede algoritmanın yakınsama davranışı ve çözümün kararlılığı analiz edilmiştir.

---

## 4. ✅ Sonuçlar

Genetik algoritma sonucunda:

- Başarı skorunun nesiller boyunca arttığı,
- Belirli bir noktadan sonra kararlı bir çözüme ulaşıldığı,
- Elde edilen en iyi çözümün tüm kısıtları sağladığı

gözlemlenmiştir.

Bu çalışma, genetik algoritmaların **kısıtlı optimizasyon problemlerinde etkili ve uygulanabilir** bir yöntem olduğunu göstermektedir.

---

## 5. 🚀 Çalıştırma ve Kurulum

Proje tek bir Jupyter Notebook dosyası (`burak.ipynb`) üzerinden çalıştırılmaktadır.

### Gerekli Kütüphaneler

Aşağıdaki kütüphanelerin yüklü olması gerekmektedir:

```bash
pip install numpy matplotlib
