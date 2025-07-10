# *KAYITLI MODELLER VE NPY DATALARI İÇİN ZİP DOSYASINI PROJE DOSYALARININ İÇİNE ÇIKARILMASI GEREKMEKTEDİR*
(gitHub'ın 100mb max dosya boyutu kısıtından kaynaklı ziplenmiştir)
Erişilememesi durumunda Tüm proje indirme linki: https://drive.google.com/file/d/15L5Vr9idbO4InSY4eP5_o4GuHCheXglS/view?usp=sharing

Ali Emre Çaylak
211301007 TOBB ETU
acaylak@etu.edu.tr

YAP 470 Dersi

Bu proje Kuruyemiş Dükkanı Gelecek Satış Tahmini makine öğrenmesi projesi için yapılmaktadır.

Dosyalar:

01_data_preperation:
Kayıtların çekilir, hatalı kayıtlar, iade ve stok girişi verileri silinir. Tarih ve saat bilgileri "datatime" cinsine çevrilir. Veriler 5er dakikalık zaman dilimlerine ayrılır ve her ürün için o zaman dilimindeki satışlar çıkarılır. Öznitelik mühendisliği basamakları burada gerçekleşir, saat, gün, haftanın günü, haftasonu olma bilgisi, 1 zaman dilimi önceki değer (lag) ve önceki 5 zaman dilimindeki ortalama satış bilgiler her ürün için eklenir. pivot_final_with_features_ALL.xlsx olarak kaydedilir


02_data_transformation:
pivot_final_with_features_ALL.xlsx dosyası okunur. Veriler z-score yöntemi ile standartlaştırılır. Zamansal değişkenler uygun şekilde sayısallaştırılır ve uygun şekilde kaydedilir. İlk 2 yıl verisi train, son yıl verisi test olacak şekilde veriler ayrılır. öznitelikler gruplandırılır. X (tüm öznitelikler), X1 (fiyat, lag, Rolling mean), X2 (gün, saat, haftanın günü, hafta sonu alma durumu), X3 (diğer ürünlerin satış, lag, rolling mean, fiyat durumları), X12 (X1 ve X2 öznitelikleri) olarak öznitelikler gruplandırılmıştır. Bunlarla birlikte tek ürün ve tüm ürünler için gruplandırma yapılmıştır. Bu eğitilmiş tüm modeller, denenen tüm kombinasyonlar ve üretilmiş 2 veri seti için de ortak bir hazırlık aşaması olmuştur.


101_train_my_mlp_multi_output_one_layer & 101_test_my_mlp_multi_output_one_layer:
Eğitmen tarafından konulan önceden optimize edilmiş algoritmaların kullanılmayacağına yönelik kısıtın yanlış anlaşılması üzerine giriş seviye bir perceptron mantığı baştan üretilmiştir. İlk olarak perceptronlar, tek katmanlı olarak paralel çalışan çalışmıştır. W1, b1, W2, b2 sonuç parametreleridir. Cross-validation geliştirilmediği için test verisi ile grid search yaparak verilen hiperparametre değerleri denenmektedir. Ağırlık ayarlaması için backpropagation methodu kullanılmaktadır. Aktivasyon fonksiyonu için relu kullanılmıştır, overfitting önlemek için early stopping (patient) bulunmaktadır. Bununla birlikte kullanıcı tarafından tespiti için train MSE ve test MSE sonuçları plot alınmaktadır. Train dosyasında eğitilen model dışa aktarılır ve test dosyasında test edilebilir.

102_train_my_mlp_multi_output_multi_layer & 102_test_my_mlp_multi_output_multi_layer:
101'den farklı olarak 3 katmanlı bir yapı üretilmiştir. 1. katmanda X1 verisi, 2. katmanda X2 verisi alınmıştır. 3. katmanda X3 verisi boş olarak verilmiştir. Bunun nedeni tüm ürünler tahmin edileceği için X3 kısmına veri kalmamıştır.

103_train_my_mlp_multi_output_one_layer_onlyPriceLagiRollingMean & 103_test_my_mlp_multi_output_one_layer_onlyPriceLagiRollingMean:
101'den farklı olarak tüm veriler yerine sadece X1 verileri kullanılır.

104_train_my_mlp_multi_output_one_layer_onlyDateTime & 104_test_my_mlp_multi_output_one_layer_onlyDateTime
103'ten farklı olarak X1 yerine X2 verileri kullanılır.


111_train_XGBoost & 111_test_XGBoost:
XGBoost modeli tüm featurelar ile (X) eğitilmiştir. Hiperparametre denemeleri gridSearchCV methoduyla yapılmıştır. Cross validation 3 parçada yapılmıştır. Estimator sayısı, max depth, learning rate, subsample parametreleri optimize edilmiştir. Train dosyasında eğitilen model dışa aktarılır ve test dosyasında test edilebilir.

112_train_XGBoost_X1 & 112_test_XGBoost_X1:
111'den farklı olarak X1 feature grubu ile eğitilmiştir.

113_train_XGBoost_X2 & 113_test_XGBoost_X2:
112'den farklı olarak X1 verileri yerine X2 kullanılmıştır.


121_train_RF & 121_test_RF:
RF modeli tüm featurelar ile (X) eğitilmiştir. Hiperparametre denemeleri gridSearchCV metoduyla yapılmıştır. Cross validation 3 parçada gerçekleştirilmiştir. Estimator sayısı, max depth, min samples split, min samples leaf parametreleri optimize edilmiştir. Train dosyasında eğitilen model dışa aktarılır ve test dosyasında test edilebilir.

122_train_RF_X1 & 122_test_RF_X1:
121'den farklı olarak X1 feature grubu ile eğitilmiştir.

123_train_RF_X2 & 123_test_RF_X2:
112'den farklı olarak X1 verileri yerine X2 verileri kullanılmıştır.


131_train_KNN & 131_test_KNN:
KNN modeli tüm featurelar ile (X) eğitilmiştir. Hiperparametre denemeleri gridSearchCV methoduyla yapılmıştır. Cross validation 3 parçada gerçekleştirilmiştir. Neighbor sayısı, weight bilgisi, ölçüm çeşidi (Manhattan, Öklid) optimize edilmiştir. Hem genelde tercih olması hem de literatürdeki yerinden kaynaklı distance seçeneği ve öklid mesafe ölçümü kullanılmıştır. Train dosyasında eğitilen model dışa aktarılır ve test dosyasında test edilebilir.
! Eğitilmiş model boyutu yüksek olduğu için gitHub'a eklenmemiştir. !

132_train_KNN_X1 & 132_test_KNN_X1:
131'den farklı olarak X1 feature grubu ile eğitilmiştir.
! Eğitilmiş model boyutu yüksek olduğu için gitHub'a eklenmemiştir. !

133_train_KNN_X2 & 133_test_KNN_X2:
132'den farklı olarak X2 feature grubu ile eğitilmiştir.


--- 2. Veri seti (tek ürün (Ekmek) tahmini, X12 (X1 ve X2 verileri) kullanarak tahmin:

201_train_my_mlp_single_output_multi_layer & 201_test_my_mlp_single_output_multi_layer:
Eğitmen tarafından konulan önceden optimize edilmiş algoritmaların kullanılmayacağına yönelik kısıtın yanlış anlaşılması üzerine giriş seviye bir perceptron mantığı baştan üretilmiştir. 1. katmanda X1 verisi, 2. katmanda X2 verisi alınmıştır. 3. katmanda yeni öznitelik input'u bulunmamaktadır. İlk olarak perceptronlar, 3 katmanlı üretilmiştir. W1, b1, W2, b2, W3, b3, W4, b4 sonuç parametreleridir. Cross-validation geliştirilmediği için test verisi ile grid search yaparak verilen hiperparametre değerleri denenmektedir. Ağırlık ayarlaması için backpropagation methodu kullanılmaktadır. Aktivasyon fonksiyonu için relu kullanılmıştır, overfitting önlemek için early stopping (patient) bulunmaktadır. Bununla birlikte kullanıcı tarafından tespiti için train MSE ve test MSE sonuçları plot alınmaktadır. Train dosyasında eğitilen model dışa aktarılır ve test dosyasında test edilebilir.

202_train_my_mlp_single_output_one_layer & 202_test_my_mlp_single_output_one_layer
201'den farklı olarak tek katmanlı paralel çalışan perceptron bir yapısı üretilmiştir. input olarak X12 (X1 ve X2 öznitelikleri) kullanılmıştır. W1, b1, W2, b2 çıktılardır.


211_train_XGBoost_SingleOutput_X12 & 211_test_XGBoost_SingleOutput_X12
XGBoost modeli X12 feature'ları ile eğitilmiştir. Hiperparametre denemeleri gridSearchCV methoduyla yapılmıştır. Cross validation 3 parçada yapılmıştır. Estimator sayısı, max depth, learning rate, subsample parametreleri optimize edilmiştir. Train dosyasında eğitilen model dışa aktarılır ve test dosyasında test edilebilir.


221_train_RF_SingleOutput_X12 & 221_test_RF_SingleOutput_X12:
RF modeli X12 feature'ları ile eğitilmiştir. Hiperparametre denemeleri gridSearchCV metoduyla yapılmıştır. Cross validation 3 parçada gerçekleştirilmiştir. Estimator sayısı, max depth, min samples split, min samples leaf parametreleri optimize edilmiştir. Train dosyasında eğitilen model dışa aktarılır ve test dosyasında test edilebilir.


231_train_KNN_SingleOutput_X12 & 231_test_KNN_SingleOutput_X12:
KNN modeli X12 feature'ları ile eğitilmiştir. Hiperparametre denemeleri gridSearchCV methoduyla yapılmıştır. Cross validation 3 parçada gerçekleştirilmiştir. Neighbor sayısı, weight bilgisi, ölçüm çeşidi (Manhattan, Öklid) optimize edilmiştir. Hem genelde tercih olması hem de literatürdeki yerinden kaynaklı distance seçeneği ve öklid mesafe ölçümü kullanılmıştır. Train dosyasında eğitilen model dışa aktarılır ve test dosyasında test edilebilir.