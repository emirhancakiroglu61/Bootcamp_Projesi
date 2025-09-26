 CNN Temelli CIFAR-10 Görüntü Sınıflandırma Projesi
Bu proje, görüntü işleme alanındaki akademik beklentilere uygun olarak, CIFAR-10 veri seti üzerinde geliştirilmiş detaylı bir Evrişimli Sinir Ağı (CNN) çözümünü sunmaktadır. 
Projenin ana hedefi, sağlam bir mimari ve ileri düzey düzenlileştirme teknikleri kullanarak aşırı öğrenmeye (overfitting) karşı dayanıklı, yüksek performanslı bir model ortaya koymaktır.

1. Metodoloji ve Veri Ön İşleme
Proje, titiz bir veri hazırlığı ile başladı.
 Görüntü piksel değerleri 0 ile 1 arasına normalize edildi ve etiketler One-Hot Encoding formatına dönüştürülerek çok sınıflı sınıflandırmaya uygun hale getirildi.

1.1 Veri Çoğaltma (Data Augmentation) Uygulaması
Proje kriterlerine uygun olarak, Veri Çoğaltma tekniğini aktif olarak kullandım. Bu yöntem, modelin genelleme yeteneğini artırmak ve eğitim verisinin sınırlılığından kaynaklanan overfitting riskini ortadan kaldırmak amacıyla hayati bir rol oynamıştır.
ImageDataGenerator kullanarak rastgele döndürme, kaydırma ve yatay çevirme gibi dönüşümler uygulayarak modelin her epoch'ta yeni varyasyonlarla karşılaşmasını sağladım.
<img width="983" height="440" alt="image" src="https://github.com/user-attachments/assets/3c29c3f8-f17c-4ff3-81df-97858837d0eb" />


2. CNN Model Mimarisi ve Regularizasyon Stratejileri
Modelim, proje gerekliliklerini karşılayan sığ ancak optimize edilmiş bir CNN yapısına sahiptir.

2.1 Mimarideki Temel Unsurlar
Model; Evrişim (Conv2D), Havuzlama (MaxPooling2D), Flatten ve Yoğun (Dense) katmanlardan oluşmaktadır.
Bu hiyerarşik yapı, görüntülerdeki yerel ve karmaşık özellikleri etkili bir şekilde çıkarmayı amaçlamıştır.

2.2 Dropout ile Aşırı Öğrenme Kontrolü
Aşırı öğrenmeyi engelleme stratejimin merkezinde Dropout katmanları yer almaktadır. 
Bu katmanları stratejik olarak modelin birden fazla noktasına (özellikle tam bağlantılı katmanlardan önce %50 oranında) uyguladım. 
Dropout, nöronlar arasındaki ortak adaptasyonu kesintiye uğratarak modelin eğitim verisindeki rastgele gürültüyü ezberlemesi yerine, daha soyut ve genelleştirilebilir özellikler öğrenmeye zorlar.

3. Eğitim Sonuçları ve Kapsamlı Değerlendirme
Model, Data Augmentation uygulanmış veri akışı üzerinde [10] epoch boyunca eğitilmiştir.
<img width="1073" height="699" alt="image" src="https://github.com/user-attachments/assets/2cfb0f62-9b77-4ee0-94a2-a5d75dabc1e0" />

3.1 Model Performans Skoru
Test Doğruluğu (Accuracy): % 62.86

Test Kaybı (Loss): 1.0650

3.2 Grafik Analizi ve Overfitting Yorumu
Eğitimden elde edilen Accuracy ve Loss Grafikleri dikkatle analiz edilmiştir:



Yorum: Grafikler incelendiğinde, eğitim doğruluk eğrisinin doğrulama doğruluk eğrisi ile çok yakın seyrettiği gözlemlenmiştir. 
Bu durum, uygulanan Dropout ve Data Augmentation tekniklerinin overfitting'i başarılı bir şekilde kontrol altına aldığını ve modelin yeni verilere iyi bir genelleme yeteneği sergilediğini kanıtlamaktadır.

3.3 Hata Analizi ve Sınıflandırma Raporu
Confusion Matrix analizi, modelin en çok [Örn: Kedi ve Köpek] gibi görsel olarak benzeyen sınıfları karıştırdığını gösterirken, [ uçak ] sınıfında ise en yüksek doğrulukla sınıflandırma yapmıştır.
Classification Report çıktısı, her bir sınıf için detaylı Precision, Recall ve F1-Score metriklerini sağlayarak modelin sınıf bazlı dengesini ortaya koymuştur.
<img width="889" height="411" alt="image" src="https://github.com/user-attachments/assets/6995de6a-44bd-400d-b974-01d5052d701f" />

<img width="786" height="700" alt="image" src="https://github.com/user-attachments/assets/8836fda9-ea81-4337-be0a-c0b214b6ce6d" />

<img width="677" height="482" alt="image" src="https://github.com/user-attachments/assets/9bba4436-a49c-4a94-a7ca-82f4e21e7600" />

4. İleri Seviye Görselleştirme ve Optimizasyon
4.1 Grad-CAM Şeffaflık Analizi (Gereklilik)
Proje yönergesinde istenen Grad-CAM (Heatmap) görselleştirmesi, modelin tahmin yaparken görüntünün hangi bölgelerine odaklandığını kanıtlayarak karar verme sürecini şeffaflaştırmaktadır. Bu, modelin yalnızca doğru sonucu vermekle kalmayıp, mantıksal olarak doğru nesne özelliklerine baktığını gösterir.

Sonuç ve Gelecek Çalışmalar
Bu proje, temel bir CNN modelinin görüntü sınıflandırma zorluklarını aşmak için Data Augmentation ve Dropout gibi modern tekniklerle nasıl güçlendirileceğini başarıyla göstermiştir. Elde edilen %48 doğruluk, mimarinin potansiyelini göstermekle birlikte, projenin gelecekteki gelişim için güçlü bir temel oluşturmaktadır.

Bu çalışma benim için bir son değil, Derin Öğrenme yolculuğumdaki sağlam bir başlangıç noktasıdır. Projeyi bir portföy değeri olarak görüyor ve kariyerimdeki ilgi alanlarım doğrultusunda şu vizyon ile geliştirmeyi planlıyorum:

Transfer Öğrenme (Transfer Learning) Entegrasyonu: Modelin sığ yapısını aşarak doğruluğu önemli ölçüde artırmak için, VGG16 veya ResNet50 gibi ImageNet üzerinde önceden eğitilmiş (pre-trained) modellerin kullanılması hedeflenmektedir. Bu, özellikle Kedi/Geyik gibi karıştırılan sınıflarda özellik çıkarım kalitesini yükseltecektir.

Arayüz Geliştirme (Deployment): Modelin Jupyter/Kaggle not defterinde kalmasını istemiyorum. Projemin gerçek zamanlı kullanılabilirliğini göstermek için bir web arayüzü (UI) geliştireceğim. Bu arayüzü Streamlit/Flask gibi Python tabanlı bir framework ile oluşturarak, kullanıcıların kendi görüntülerini yükleyip anında model tahmini alabilmelerini sağlayacağım. Bu, projeyi interaktif ve pazarlanabilir bir ürüne dönüştürecektir.

Dinamik Veri Akışı: Şu anki çalışma statik bir veri setine dayanmaktadır. Gelecekte, projeyi dinamik bir veri toplama aşaması ile birleştirerek, belirli bir alandan (örneğin trafik kameralarından) gerçek zamanlı görüntü akışı alıp sınıflandırma yapabilen bir yapıya dönüştürmeyi hedefliyorum. Bu, Edge Computing ve Gerçek Zamanlı Analiz gibi alanlara olan ilgimi somutlaştıracaktır.

LİNKLER
https://www.kaggle.com/code/emirhanakrolu/notebook10d6eacd11


