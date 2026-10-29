# Derin Öğrenme Yöntemleri Kullanılarak X-Ray Kemik Görüntülerinde Normallik ve Anormallik Tespiti

[![Canva Sunumu](https://img.shields.io/badge/Canva-Poster_Sunumu-00C4CC?style=for-the-badge&logo=canva)](https://www.canva.com/design/DAGH0u1qobc/DzwSXA0mAcz9H_-Nu55kmg/edit)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)](https://www.tensorflow.org/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)

## 📌 Proje Özeti

Bu proje, X-ray kemik görüntülerinde (radyografilerde) anormallik olup olmadığını otomatik olarak tahmin edebilen derin öğrenme modellerinin geliştirilmesini ve karşılaştırılmasını içermektedir.

Çalışmanın temel amacı; radyologların ve doktorların tanı süreçlerindeki iş yükünü hafifletmek, yapay zeka destekli bir araç ile daha hızlı ve doğru hastalık teşhisi yapmalarına yardımcı olmaktır. Sağlıkta ortopedi ve yapay zekayı birleştiren bu çalışma, tıbbi görüntüleme alanındaki gelecekteki araştırmalar için önemli bir referans niteliği taşımaktadır.

---

## 📊 Veri Seti: MURA-v1.1

Çalışmada Stanford Üniversitesi Makine Öğrenmesi Grubu tarafından hazırlanan **MURA-v1.1 (Musculoskeletal Radiographs)** veri seti kullanılmıştır.

* **İçerik:** Toplamda 40.327'den fazla üst ekstremite kemik röntgeni içermektedir.
* **İncelenen Bölgeler:** Dirsek (Elbow), Parmak (Finger), Önkol (Forearm), El (Hand), Kazı Kemiği (Humerus), Omuz (Shoulder) ve Bilek (Wrist).
* **Dağılım:** Veri setinin yapısını anlamak ve sınıflar (eğitim, test, normal, anormal) arası dengesizlikleri gözlemlemek için veri dağılım grafikleri ile Keşifsel Veri Analizi (EDA) uygulanmıştır.

---

## ⚙️ Ön İşleme ve Görüntü İyileştirme (Preprocessing)

Tıbbi görüntülerin kalitesini artırmak ve modellerin öğrenme kapasitesini maksimize etmek için **CLAHE (Contrast Limited Adaptive Histogram Equalization)** yöntemi kullanılmıştır.

* **Neden CLAHE?** Bu yöntem, görüntünün çeşitli karo bölgeleri üzerinde histogramlara dayalı hesaplamalar yaparak yerel detayları belirginleştirir.
* **Etkisi:** Genel görüntüye göre çok karanlık veya çok aydınlık olan bölgelerde bile tıbbi anomalilerin (çatlak, kırık vb.) daha açık bir şekilde görünmesini sağlar. Histogramdaki artışın sınırlandırılması, homojen bölgelerde oluşabilecek gürültüleri engeller.

---

## 🛠 Kullanılan Modeller ve Metodoloji

Projede klasik yaklaşımlar ve modern mimariler bir arada kullanılarak üç temel strateji izlenmiştir:

1. **Sıfırdan Eğitim:** Klasik bir Evrişimsel Sinir Ağının (CNN) sıfırdan eğitilmesi.
2. **Ön İşlemeli Eğitim:** Görüntülere CLAHE ön işlemesi uygulandıktan sonra model eğitimi.
3. **Transfer Öğrenme (Transfer Learning):** ImageNet üzerinde önceden eğitilmiş ağırlıkların kullanılması (İnce ayar / Fine-tuning yapılarak).

### Eğitilen Derin Öğrenme Mimarileri:
* `DenseNet169` & `DenseNet201`
* `ResNet50`
* `VGG16` & `VGG19`
* `EfficientNetV2 B0`
* `Özel CNN (Custom CNN)`

### 🔄 Akış Şeması (Pipeline)
Sistem mimarisi aşağıdaki adımlarla ilerlemektedir:
1. **Başla:** Veri setinin sisteme yüklenmesi.
2. **Ön İşleme:** Keşifsel Veri Analizi (EDA) ve CLAHE histogram eşitleme işlemlerinin uygulanması.
3. **Model Eğitimi:** Hazırlanan verilerin VGG19, ResNet50, DenseNet, CNN gibi derin öğrenme mimarilerine beslenmesi.
4. **Sonuç & Değerlendirme:** Modellerin performans metriklerine göre karşılaştırılması ve en iyi sonucun kaydedilmesi.
5. **Bitir**.

---

## 📈 Model Değerlendirme Metrikleri

TensorFlow kütüphanesi kullanılarak eğitilen modellerin başarısı çeşitli metrikler üzerinden test edilmiştir. Elde edilen sonuçlar karşılaştırmalı olarak tablolaştırılmış olup değerlendirmede şu metrikler baz alınmıştır:

* **Loss** (Kayıp Fonksiyonu)
* **Binary Accuracy** (İkili Sınıflandırma Doğruluğu)
* **Precision** (Kesinlik)
* **Recall** (Duyarlılık)
* **F1-Score**
* **ROC AUC** (Alıcı İşletim Karakteristiği Eğrisi Altındaki Alan)

*Detaylı model sonuçları (Tablo 1) değerlendirme notebook dosyasında (değerlendirme.ipynb) incelenebilir.*

---

## 🚀 Kurulum ve Çalıştırma

Projeyi kendi ortamınızda çalıştırmak için aşağıdaki adımları izleyebilirsiniz:

1. Depoyu bilgisayarınıza klonlayın:
   ```bash
   git clone https://github.com/akdenur/-Normality-and-Abnormality-Detection-in-X-Ray-Bone-Images-Using-Deep-Learning-Methods.git
   ```
2. Proje dizinine gidin ve `değerlendirme.ipynb` dosyasını **Jupyter Notebook** veya **Google Colab** üzerinden açın.
3. Gerekli kütüphaneleri yükleyin:
   ```bash
   pip install tensorflow pandas numpy matplotlib opencv-python
   ```
4. Veri setini bağlayarak hücreleri sırasıyla çalıştırın.

---

## 📚 Kaynakça

1. Abunasser, B. S., et al., "Breast Cancer Detection and Classification using Deep Learning Xception Algorithm", *International Journal of Advanced Computer Science and Applications (IJACSA)*, vol. 13, no. 7, pp. 223-228, 2022.
2. Karel Zuiderveld, "Graphics gems iv," chapter *Contrast Limited Adaptive Histogram Equalization*, pp. 474–485. Academic Press Professional, Inc., San Diego, CA, USA, 1994.

---

## 👥 Ekip ve Kurum

* **Geliştiriciler:** Berre Zehra TOP, Akdenur YEĞİN
* **Akademik Danışman:** Dr. Öğr. Üyesi Seda ŞAHİN
* **Kurum:** Çankırı Karatekin Üniversitesi, Mühendislik Fakültesi, Bilgisayar Mühendisliği Bölümü, Çankırı, Türkiye
* **İletişim:** sedasahin@karatekin.edu.tr
* **GitHub Deposu:** [Proje Bağlantısı](https://github.com/akdenur/-Normality-and-Abnormality-Detection-in-X-Ray-Bone-Images-Using-Deep-Learning-Methods/tree/main)