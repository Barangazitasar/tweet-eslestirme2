# 📌 Sosyal Medya Projesi: Tweet - İçerik Politikası Eşleşmesi
**Baran Gazi Taşar - 2311081051**

Bu proje, Doğal Dil İşleme (NLP) dersi kapsamında gerçekleştirdiğim bir ödevdir. Amacım, sosyal medya üzerinden alınan tweet verileriyle içerik politikası benzerliklerini analiz eden bir sistem geliştirmekti.

---

## 🧠 Proje Amacı

Proje boyunca belirli bir örnek giriş cümlesi verildiğinde, bu cümleye en çok benzeyen 5 tweet'in bulunması hedeflenmiştir. Bu benzerlik analizleri hem **TF-IDF** hem de **Word2Vec** temelli yöntemlerle yapılmıştır.

---

## 📁 Kullanılan Veri Setleri

Proje boyunca aşağıdaki veri dosyalarını kullandım:

- `twitter.csv`: Ham tweet verisi
- `lemmatized_tweets.csv`: Lemmatizasyon uygulanmış temiz tweetler
- `stemmed_tweets.csv`: Stem uygulanmış temiz tweetler

Tüm veri dosyaları CSV formatında ve her biri 10.000 satırdan oluşmaktadır.

---

## ⚙️ Kullanılan Yöntemler

### 1. TF-IDF Tabanlı Benzerlik

- Giriş cümlesi temizlendi ve aynı işlemler tweetler için de uygulandı.
- `TfidfVectorizer` ile hem lemmatized hem de stemmed veri vektörlendirildi.
- Cosine Similarity kullanılarak giriş cümlesine en benzer 5 tweet bulundu.

### 2. Word2Vec Tabanlı Benzerlik

- Giriş cümlesi temizlendikten sonra her kelime vektöre dönüştürüldü.
- Hazırladığım Word2Vec modelleri:
  - CBOW tabanlı, `dim=100`, `window=2`
- Her tweet için ortalama vektör alındı.
- Cosine Similarity ile giriş cümlesine en yakın 5 tweet bulundu.

---

## 📊 Anlam Puanlaması ve Yorumlama

Her model için önerilen 5 tweet’e **1–5 arası** anlam puanı verdim:

| Model Adı                        | Anlam Skorları     | Ortalama |
|----------------------------------|--------------------|----------|
| tfidf_lemmatized                 | 4, 4, 3, 4, 4      | 3.8      |
| tfidf_stemmed                    | 3, 3, 3, 3, 3      | 3.0      |
| word2vec_lemmatized_cbow_win2   | 2, 2, 2, 3, 2      | 2.2      |

- En başarılı model: **TF-IDF (lemmatized)**, çünkü önerdiği cümleler girişle daha tematik olarak örtüşüyordu.
- Word2Vec biraz daha genel benzerlikler önerdi, ama anlam bazlı çok güçlü değildi.

---

## 🧮 Jaccard Benzerlik Matrisi

Farklı modellerin sıraladığı ilk 5 tweet arasındaki **ortak ID sayıları** ile Jaccard benzerlikleri hesapladım.

|                              | tfidf_lemmatized | tfidf_stemmed | word2vec_lemmatized_cbow |
|------------------------------|------------------|----------------|---------------------------|
| **tfidf_lemmatized**         | 1.00             | 0.25           | 0.11                      |
| **tfidf_stemmed**            | 0.25             | 1.00           | 0.25                      |
| **word2vec_lemmatized_cbow** | 0.11             | 0.25           | 1.00                      |

> Bu tablo, en tutarlı sonuçları **TF-IDF tabanlı modellerin** verdiğini göstermektedir.

---

## 🔧 Çalıştırma Talimatları

Projeyi çalıştırmak için:

1. Gerekli kütüphaneleri yükleyin:
```bash
pip install pandas numpy sklearn gensim matplotlib seaborn
Jupyter Notebook üzerinden tweet_veri_toplama.ipynb dosyasını açın.
📂 Proje Klasörü
├── twitter.csv                        # Ham tweet verisi
├── lemmatized_tweets.csv             # Lemmatize edilmiş temiz veri
├── stemmed_tweets.csv                # Stem uygulanmış temiz veri
├── tweet_veri_toplama.ipynb          # Tüm işlemleri içeren notebook

