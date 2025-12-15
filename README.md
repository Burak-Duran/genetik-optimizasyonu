# Genetik Algoritma ile Öğrenci Etüt Programı Optimizasyonu

Bu proje, BLG-307 Yapay Zeka Sistemleri dersi kapsamında,
bir öğrencinin matematik (x₁) ve fen (x₂) derslerine ayırdığı etüt sürelerini,
sınav başarısını maksimize edecek şekilde planlamayı amaçlamaktadır.

Problem, hem doğrusal olmayan bir amaç fonksiyonu
hem de birden fazla kısıt içerdiği için
kısıtlı bir optimizasyon problemi olarak ele alınmış
ve çözüm sürecinde *Genetik Algoritma* yöntemi kullanılmıştır.

---

## 1. Problem Tanımı

Öğrencilerin çalışma süreleri sınırlıdır ve bu süre,
farklı dersler arasında dengeli bir biçimde paylaştırılmalıdır.
Matematik ve fen derslerine ayrılan süreler,
öğrencinin akademik başarısını doğrudan etkilemektedir.

Ancak çalışma süresi ile başarı arasındaki ilişki doğrusal değildir:
- Yetersiz çalışma başarının düşmesine neden olurken,
- Aşırı çalışma belirli bir noktadan sonra verim kaybına yol açabilmektedir.
- Ayrıca bazı dersler için minimum çalışma süresi gibi
akademik gereklilikler bulunmaktadır.

Bu nedenle problem, yalnızca başarıyı artırmayı değil,
aynı zamanda gerçekçi ve uygulanabilir çalışma kısıtlarını
dikkate alan bir optimizasyon problemi hâline gelmektedir.

---

## 2. Matematiksel Model

### 2.1 Amaç Fonksiyonu

Öğrencinin başarı skorunu temsil eden amaç fonksiyonu aşağıdaki şekilde tanımlanmıştır:

\[
y = 4x_1 + 5x_2 - 0.5x_1^2 - 0.2x_2^2
\]

Burada:
- *x₁:* Matematik dersi için ayrılan etüt süresi (saat)
- *x₂:* Fen dersi için ayrılan etüt süresi (saat)

Fonksiyondaki doğrusal terimler,
çalışma süresinin başarı üzerindeki olumlu etkisini temsil ederken;
ikinci dereceden terimler,
aşırı çalışmanın verimi düşürücü etkisini modele dahil etmektedir.
Bu sayede daha dengeli ve gerçekçi çözümler tercih edilmektedir.

---

### 2.2 Değişken Aralıkları ve Kısıtlar

Optimizasyon probleminde kullanılan kısıtlar aşağıda özetlenmiştir:

| Kısıt | Açıklama |
|-----|----------|
| 0 ≤ x₁ ≤ 10 | Matematik etüt süresi sınırları |
| 0 ≤ x₂ ≤ 10 | Fen etüt süresi sınırları |
| x₁ + x₂ ≤ 12 | Toplam etüt süresi |
| x₂ ≥ 2 | Fen dersi için minimum süre |

Bu kısıtlar, Genetik Algoritma sürecinde
ceza yöntemi kullanılarak fitness fonksiyonuna entegre edilmiştir.

---

## 3. Kullanılan Yöntem: Genetik Algoritma

Bu çalışmada çözüm yöntemi olarak
Genetik Algoritma tercih edilmiştir.

Genetik Algoritma, rastgelelik ve seçilim temelli yapısı sayesinde
karmaşık ve doğrusal olmayan problemlerin çözümünde
etkili sonuçlar üretebilmektedir.

---

### 3.1 Başlangıç Popülasyonu

Başlangıç popülasyonu, her biri iki genli (x₁, x₂) bireylerden oluşacak şekilde,
önceden tanımlanan değişken aralıkları içinde
rastgele üretilmiştir.
Bu yaklaşım, çözüm uzayının farklı bölgelerinin
başlangıç aşamasında keşfedilmesini sağlar.

---

### 3.2 Fitness Hesaplaması

Her birey için:
1. Amaç fonksiyonu değeri hesaplanır.
2. Kısıt ihlalleri ceza fonksiyonu ile belirlenir.
3. Nihai fitness değeri, amaç fonksiyonundan cezanın çıkarılmasıyla elde edilir.

Bu yapı sayesinde hem yüksek başarı üreten
hem de kısıtlara uygun çözümler
daha avantajlı hâle gelmektedir.

---

### 3.3 Seçilim: Rulet Tekerleği Yöntemi

Ebeveyn seçimi için rulet tekerleği seçimi kullanılmıştır.
Bu yöntemde fitness değeri yüksek bireylerin seçilme olasılığı artarken,
düşük fitnesslı bireylerin de küçük bir ihtimalle seçilmesi sağlanarak
popülasyon çeşitliliği korunmuştur.

---

### 3.4 Çaprazlama 

Yeni bireylerin üretilmesi amacıyla
tek noktalı çaprazlama yöntemi uygulanmıştır.
İki ebeveyn bireyin genetik bilgileri farklı kombinasyonlarla birleştirilerek
yeni çözüm adayları oluşturulmuştur.

---

### 3.5 Mutasyon 

Mutasyon işlemi, genetik çeşitliliği artırmak ve
algoritmanın yerel optimumlara erken sıkışmasını önlemek amacıyla kullanılmıştır.
Belirli bir olasılıkla gen değerlerine küçük rastgele değişiklikler eklenmiş
ve mutasyon sonrası değerlerin tanımlı sınırlar içinde kalması sağlanmıştır.

---

### 3.6 Elitizm

Her nesilde en yüksek fitness değerine sahip birey,
bilgi kaybını önlemek amacıyla
doğrudan bir sonraki nesle aktarılmıştır.
Bu yaklaşım, algoritmanın kararlılığını artırmaktadır.

---

## 4. Deneysel Sonuçlar ve Analiz

Genetik Algoritma çalıştırıldığında,
nesiller ilerledikçe en iyi fitness değerinin arttığı
ve algoritmanın kısıtları sağlayan
kararlı bir çözüme yakınsadığı gözlemlenmiştir.

Algoritmanın davranışı;
- En iyi x₁ ve x₂ değerlerinin nesillere göre değişimi,
- En iyi fitness değerinin zaman içindeki gelişimi

grafikler aracılığıyla analiz edilmiştir.
Fitness eğrisinin belirli bir noktadan sonra yataylaşması,
çözümün kararlı hâle geldiğini göstermektedir.

---

## 5. Çalıştırma ve Kullanım

Proje tek bir Google Colab (.ipynb) dosyasından oluşmaktadır.

### Gerekli Kütüphaneler
- numpy
- random
- matplotlib

Notebook dosyası,
Google Colab ortamında
hücreler sırasıyla çalıştırılarak kullanılabilir.

---

## 6. Proje Bilgileri

- *Ders:* BLG-307 Yapay Zeka Sistemleri  
- *Senaryo:* 9  
- *Konu:* Genetik Algoritma ile Öğrenci Etüt Programı Optimizasyonu  
- *Hazırlayan:* Burak Duran
