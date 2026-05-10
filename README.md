# Dry Bean Veri Bilimi Projesi

Bu proje, Dry Bean veri seti üzerinde çok sınıflı fasulye türü sınıflandırması yapmak amacıyla hazırlanmıştır. Projede veri temizleme, eğitim-test ayrımı, ölçekleme, farklı makine öğrenmesi algoritmalarının eğitilmesi ve sonuçların karşılaştırılması adımları bulunmaktadır.

## Kullanılan Algoritmalar

Projede toplam 6 sınıflandırma algoritması kullanılmıştır:

- K-En Yakın Komşu (KNN)
- Karar Ağacı (Decision Tree)
- Gaussian Naive Bayes
- Destek Vektör Makineleri (SVM)
- Rastgele Orman (Random Forest)
- Yapay Sinir Ağı (YSA / MLP Classifier)

## Proje Klasör Yapısı

```text
Veri_Bilimi_Proje/
├── data/
│   ├── Dry_Bean_Dataset.xlsx
│   ├── dry_bean_clean.csv
│   ├── X_train.csv
│   ├── X_test.csv
│   ├── y_train.csv
│   ├── y_test.csv
│   ├── X_train_scaled.csv
│   └── X_test_scaled.csv
│
├── readable_data/
│   ├── dry_bean_clean_okunabilir.xlsx
│   ├── X_train_okunabilir.xlsx
│   ├── X_test_okunabilir.xlsx
│   ├── y_train_okunabilir.xlsx
│   ├── y_test_okunabilir.xlsx
│   ├── X_train_scaled_okunabilir.xlsx
│   └── X_test_scaled_okunabilir.xlsx
│
├── notebooks/
│   ├── 00_veri_hazirlama_ortak.ipynb
│   ├── 01_kisi1_modeller.ipynb
│   ├── 02_kisi2_modeller.ipynb
│   ├── 03_sonuclari_birlestirme.ipynb
│   └── 04_ozellik_muhendisligi_ve_dermason_sira_analizi.ipynb
│
├── reports/
│   ├── figures/
│   ├── results/
│   └── references/
│
├── requirements.txt
└── README.md
```

## Kurulum

Projeyi çalıştırmak için bilgisayarda Python kurulu olmalıdır.

Gerekli Python paketlerini yüklemek için proje ana klasöründe terminal açıp aşağıdaki komutu çalıştırın:

```bash
python -m pip install -r requirements.txt
```

Alternatif olarak:

```bash
pip install -r requirements.txt
```

## Çalıştırma Sırası

Notebook dosyaları aşağıdaki sırayla çalıştırılmalıdır:

### 1. Ortak Veri Hazırlama

İlk olarak şu notebook çalıştırılır:

```text
notebooks/00_veri_hazirlama_ortak.ipynb
```

Bu dosyada:

- Veri seti okunur.
- Eksik değer kontrolü yapılır.
- 68 tekrarlı kayıt temizlenir.
- Temiz veri kaydedilir.
- Eğitim/test ayrımı yapılır.
- Ölçeklenmiş veri dosyaları oluşturulur.
- Ortak CSV dosyaları `data/` klasörüne kaydedilir.
- Okunabilir Excel dosyaları `readable_data/` klasörüne kaydedilir.

Bu notebook çalışmadan diğer model notebookları çalıştırılmamalıdır.

### 2. Kişi 1 Modelleri

Sonra şu notebook çalıştırılır:

```text
notebooks/01_kisi1_modeller.ipynb
```

Bu dosyada şu modeller çalıştırılır:

- KNN
- Decision Tree
- Gaussian Naive Bayes

Sonuçlar şu dosyaya kaydedilir:

```text
reports/results/kisi1_model_sonuclari.csv
```

Confusion matrix görselleri şu klasöre kaydedilir:

```text
reports/figures/
```

### 3. Kişi 2 Modelleri

Sonra şu notebook çalıştırılır:

```text
notebooks/02_kisi2_modeller.ipynb
```

Bu dosyada şu modeller çalıştırılır:

- SVM
- Random Forest
- YSA / MLP Classifier

Sonuçlar şu dosyaya kaydedilir:

```text
reports/results/kisi2_model_sonuclari.csv
```

Confusion matrix görselleri şu klasöre kaydedilir:

```text
reports/figures/
```

### 4. Sonuçları Birleştirme

Ardından şu notebook çalıştırılır:

```text
notebooks/03_sonuclari_birlestirme.ipynb
```

Bu dosyada:

- Kişi 1 ve Kişi 2 sonuçları okunur.
- Toplam 6 model tek tabloda birleştirilir.
- Modeller Weighted F1-score değerine göre sıralanır.
- En iyi model belirlenir.
- Final sonuç tablosu kaydedilir.

Final sonuç dosyası:

```text
reports/results/tum_model_sonuclari.csv
```

### 5. Özellik Mühendisliği ve Dermason-Sıra Analizi

Son olarak şu notebook incelenir:

```text
notebooks/04_ozellik_muhendisligi_ve_dermason_sira_analizi.ipynb
```

Bu notebookta özellikle Dermason ve Sıra sınıflarının karıştırılma durumu incelenmiştir. Permutation importance, korelasyon analizi, türetilmiş özellikler ve threshold tuning denemeleri yapılmıştır. Sonuç olarak türetilen özelliklerin mevcut özelliklerle yüksek korelasyon gösterdiği ve güvenilir/kalıcı bir performans artışı sağlamadığı görülmüştür.

## Önemli Notlar

- Notebook dosyaları `notebooks/` klasörü içinden çalıştırılmalıdır.
- Notebooklar tek başına başka klasöre taşınıp çalıştırılmamalıdır.
- `00_veri_hazirlama_ortak.ipynb` çalıştırılmadan model notebookları çalıştırılırsa veri dosyaları eksik olabilir.
- Model notebooklarında tekrar `train_test_split` yapılmamaktadır.
- Tüm modeller ortak veri bölünmesi üzerinde karşılaştırılır.
- KNN, SVM ve YSA modelleri ölçeklenmiş veriyle çalışır.
- Decision Tree, Random Forest ve Gaussian Naive Bayes modelleri ham veriyle çalışır.

## Beklenen Çıktılar

Çalıştırma sonunda aşağıdaki dosyaların oluşması beklenir:

```text
reports/results/kisi1_model_sonuclari.csv
reports/results/kisi2_model_sonuclari.csv
reports/results/tum_model_sonuclari.csv
```

Ayrıca confusion matrix görselleri:

```text
reports/figures/kisi1_knn_confusion_matrix.png
reports/figures/kisi1_decision_tree_confusion_matrix.png
reports/figures/kisi1_gaussian_nb_confusion_matrix.png
reports/figures/kisi2_svm_confusion_matrix.png
reports/figures/kisi2_random_forest_confusion_matrix.png
reports/figures/kisi2_ysa_confusion_matrix.png
```

## Sonuç

Birleşik sonuç tablosuna göre modeller karşılaştırılır ve en iyi model `reports/results/tum_model_sonuclari.csv` dosyasından incelenir.
