# Cicek Siniflandirma CNN Modeli
CNN tabanlı bir model kullanarak Kaggle platformunda yer alan flowers-dataset veri setindeki çiçek türlerini tahmin eden model geliştirildi.

## Projenin Amacı
* Akbank Derin Öğrenmeye Giriş Bootcamp'i eğitimi gereği CNN tabanlı bir proje geliştirmek. Projeyi Kaggle'dan da görüntüleyebilirsiniz: [https://www.kaggle.com/code/tugbakaratas/cnnproject]
* Kaggle platformunda yer alan flowers-dataset kapsamında yer alan çiçek resimlerini daisy, dandelon, rose, sunflower, tulip olmak üzere 5 kategoriye sınıflandırma yapabilen bir derin öğrenme modeli geliştirmek.

## Veri Seti
* Bu proje kapsamında kullandığım veri seti Kaggle platformunda yer almaktadır. Veri setine bu linkten ulaşabilirsiniz: [https://www.kaggle.com/datasets/imsparsh/flowers-dataset]
* Bu veri setinde iki adet klasör bulunmaktadır. Bu klasörlerden biri train veri seti diğeri ise test veri seti olarak adlandırılmıştır. test klasöründeki .jpg uzantılı resimler etiketli değildir ancak train klasörü içinde 5 adet farklı adlarda klasör daha bulunmaktadır. Bu klasörün isimleri aynı zamanda bizim etiket isimlerimiz olmakla birlikte şöyledir: daisy, dandelon, rose, sunflower, tulip. Bu alt klasörler içinde de klasör isimleri ile aynı kategoride yer alan .jpg uzantılı resimler bulunmaktadır.
* Oluşturduğum CNN modeli kapsamında test veri seti için test klasörünü, train ve valisyon için de train klasöründeki etiketli verileri %20 validasyon, %80 train olmak üzere ayırdım ve kullandım.
* Bu resim verilerini numpy kütüphanesini kullanarak numpy arrayine çevirdim daha sonra her piksel 0-255 arasında değere sahip olduğunda modeli daha iyi eğitmek için normalizayon yapıp bu değerleri 0-1 arasına indirgedim. Resim boylarını da sabit bir boyut belirleyip (160,160) yaptım.

## Kullanılan Yöntemler
* CNN modeli kurmada 3 tane **Convolutional Layers (Conv2D)** katmanı kullandım ve aktivasyon fonksiyonu olarak da *ReLu* kullandım. Katmanlardaki Conv2D adedi ve filtre boyutları değişmektedir. Bu katman sayesinde feature (özellik) çıkarımı yapıldı.
* Daha sonra **Pooling Layers (MaxPooling2D)** ile boyut küçültme (downsampling) ve özellikleri özetleme yapar. Böylece modelin daha genelleştirilmiş olmasını sağlar.
* Ara katmanlarda ise aktivasyon öncesinde **Batch Normalization** işlemi yapılmaktadır. Böylece eğitim daha da hızlanır ve overfitting olma ihtimali azalır.
* Overfitting model oluşturuken en istemediğimiz durumlardan biridir onun önüne geçmek için de ara ara **Dropout** katmanı kullaandım. Dropout Overfitting’i önlemek için rastgele nöronları kapatma yöntemidir.
* **Aktivasyon fonksiyonu** olarak da hidden layerlarda **'ReLu'**, output layerında ise **'Softmax'** kullandım.
* Convolution ve pooling çıktılarını 1 boyutlu vektöre çevirmek için de **Flatten** katmanı kullandım.
* **One-Hot Encoding**: to_categorical ile etiketleri vektör haline getirdim.
* Eğitim sırasında veri çeşitliliği oluşturması için **ImageDataGenerator** kullandım.
* Callbacks için de **EarlyStopping**: *Val_loss artarsa eğitim durur, en iyi ağırlıkları geri yükler.* ve **ReduceLROnPlateau**: *Val_loss iyileşmezse learning rate’i düşürür.* kullandım.
* Modeli eğitirken Google Colab ortamından yardım aldım güçlü GPU ve TPU desteği ile bu süreci daha iyi yönettim.

## Sonuçlar
* Modeli eğitirken farklı epoch ve batch size değerleri denedim ancak sistemle ilgili sorunlar nedeni ile her denememi görsel olarak gösteremedim.
* Modelimizin başarısına gelecek olursak %55 - %60 civarı başarı oranı yakaladığım hiperparametre değerleri oldu ancak zaman kısıtından dolayı daha faazla deneyimleyemedim. Modelde kullandığım hiperparametre ayarlarını değiştirerek hatta gerek olursa yeni katmanlar ekleyerek bu başarı oranını arttırmayı hedefliyorum. Projeyi githuba yükledim ancak **proje üzerinde çalışmalarım devam edecektir.**

## Modelde Geliştirilebilecek Yönler
* Farklı hipermatre ayarlamaları yapılabilir. (learning rate düşürme gibi, daha fazla conv2d katmanı ekleme gibi, batch & epoch değeri arttırma gibi)
* Veriler daha farklı yöntemler kullanılarak çoğaltılabilir.
