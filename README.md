# Bilişim Teknolojileri RAG Veri Seti

**Türkçe** | [English](README_EN.md)

## Genel Bakış

Bu veri seti, Retrieval-Augmented Generation (RAG) sistemlerinin değerlendirilmesi için özel olarak hazırlanmış, Bloom Taksonomisi ile sınıflandırılmış Türkçe soru-cevap çiftlerinden oluşmaktadır. Veri seti, bilişim teknolojileri alanında eğitim materyallerinden türetilmiş ve RAG sistemlerinin performansını çok boyutlu olarak ölçmek üzere tasarlanmıştır.

## Veri Seti Özellikleri

### İstatistiksel Bilgiler
- **Toplam Soru Sayısı**: 100
- **Bloom Seviyesi Dağılımı**:
  - Remembering: 50 soru (%50)
  - Understanding / Applying: 30 soru (%30)
  - Analyzing / Evaluating: 20 soru (%20)
- **Dil**: Türkçe
- **Alan**: Bilişim Teknolojileri
- **Format**: JSON, CSV, XLSX

### Veri Yapısı

Her veri örneği aşağıdaki alanları içermektedir:

| Alan | Açıklama |
|------|----------|
| `ID` | Benzersiz soru tanımlayıcısı |
| `Soru` | Kullanıcı sorusu |
| `İdeal Cevap (GT)` | Ground Truth - Referans cevap |
| `Bağlam (Context)` | Kaynak doküman bağlamı |
| `Bloom Seviyesi` | Bloom Taksonomisi sınıflandırması |
| `Konu` | Soru konusu/kategorisi |
| `Chunk_ID` | Kaynak chunk tanımlayıcısı |

## Bloom Taksonomisi Sınıflandırması

Veri seti, Bloom'un Revize Edilmiş Taksonomisi'ne göre üç ana bilişsel düzeyde sınıflandırılmıştır:

1. **Remembering (Hatırlama)**: Temel bilgi ve kavramların hatırlanması, tanımların ve olguların geri çağrılması
2. **Understanding / Applying (Anlama / Uygulama)**: Kavramların anlamlandırılması, açıklanması ve bilginin yeni durumlarda uygulanması
3. **Analyzing / Evaluating (Analiz / Değerlendirme)**: Bilginin parçalara ayrılması, ilişkilerin incelenmesi ve kriterlere dayalı yargılama

Bu sınıflandırma, RAG sistemlerinin farklı bilişsel seviyelerdeki performansını değerlendirmeyi mümkün kılar ve özellikle temel bilgi hatırlama ile üst düzey bilişsel becerilerin karşılaştırılmasına olanak tanır.

### Bloom Seviyesi Dağılımının Gerekçesi

Veri setindeki Bloom seviyesi dağılımı (%50 Remembering, %30 Understanding/Applying, %20 Analyzing/Evaluating) kasıtlı olarak piramit yapısında tasarlanmıştır:

**1. Pedagojik Temel**: Bloom Taksonomisi'nin orijinal yapısı, üst seviye bilişsel becerilerin alt seviye becerilere dayandığı bir piramittir. Öğrencilerin önce temel bilgileri hatırlaması, sonra anlaması ve en son analiz/değerlendirme yapabilmesi beklenir. Bu dağılım, eğitim bilimlerindeki bu temel prensibi yansıtır.

**2. Gerçek Dünya Senaryosu**: Kaynak eğitim materyalindeki (MEB Bilişim Teknolojileri Ders Kitabı) doğal soru dağılımını koruyarak, RAG sistemlerinin gerçek eğitim ortamlarındaki performansını daha doğru ölçmeyi hedefledik. Gerçek sınıf ortamlarında öğrencilerin karşılaştığı soru dağılımı bu oranları yansıtmaktadır.

**3. İstatistiksel Güvenilirlik**: Her seviyede anlamlı değerlendirme yapabilmek için yeterli soru sayısı sağlanmıştır. 50 hatırlama sorusu, temel retrieval yeteneklerinin kapsamlı değerlendirilmesini sağlarken, 20 analiz/değerlendirme sorusu üst seviye bilişsel becerileri test etmek için yeterli istatistiksel güce sahiptir.

**4. Retrieval Odaklı Değerlendirme**: RAG sistemlerinin temel retrieval yeteneklerini (doğru chunk'ı bulma, ilgili bağlamı getirme) kapsamlı şekilde test etmek için daha fazla hatırlama sorusu gereklidir. Bu seviye, sistemin temel işlevselliğini en iyi şekilde ölçer.

**5. Benchmark Uyumluluğu**: Literatürdeki RAG ve soru-cevap benchmark'larında (SQuAD, Natural Questions, TriviaQA) benzer dağılımlar görülür. Bu yaklaşım, sonuçlarımızın diğer çalışmalarla karşılaştırılabilir olmasını sağlar.

## Kullanım Alanları

### 1. RAG Sistem Değerlendirmesi
- Retrieval kalitesinin ölçülmesi
- Generation performansının değerlendirilmesi
- Farklı embedding modellerinin karşılaştırılması
- Reranking stratejilerinin test edilmesi

### 2. Bilişsel Seviye Analizi
- RAG sistemlerinin farklı Bloom seviyelerindeki başarı oranlarının analizi
- Sistem güçlü ve zayıf yönlerinin belirlenmesi
- Eğitim materyallerinin etkinliğinin ölçülmesi

### 3. Türkçe NLP Araştırmaları
- Türkçe dil modellerinin değerlendirilmesi
- Soru-cevap sistemlerinin geliştirilmesi
- Semantik benzerlik çalışmaları

## Değerlendirme Metrikleri

Veri seti, aşağıdaki metriklerle değerlendirme yapılmasına olanak tanır:

### Retrieval Metrikleri
- **Precision@K**: İlk K sonuçtaki doğru chunk oranı
- **Recall@K**: İlgili chunk'ların bulunma oranı
- **MRR (Mean Reciprocal Rank)**: İlk doğru sonucun sıralaması

### Generation Metrikleri
- **ROUGE-1, ROUGE-2, ROUGE-L**: N-gram ve en uzun ortak alt dizi örtüşmesi
- **BERTScore**: Semantik benzerlik ölçümü
- **Semantic Similarity**: Embedding tabanlı benzerlik

### RAG-Specific Metrikleri
- **Context Relevance**: Bağlam ilgililiği
- **Answer Relevance**: Cevap ilgililiği
- **Faithfulness**: Bağlama sadakat
- **Context Recall**: Bağlam hatırlama oranı

## Veri Seti Formatları

### JSON Format
```json
{
  "ID": 1,
  "Soru": "...",
  "İdeal Cevap (GT)": "...",
  "Bağlam (Context)": "...",
  "Bloom Seviyesi": "Remembering",
  "Konu": "...",
  "Chunk_ID": 3039
}
```

### Dosyalar
- `Bilisim_Teknolojileri_Bloom_Sirali_FINAL.json`: JSON formatında veri seti
- `Bilisim_Teknolojileri_Bloom_Sirali_FINAL.csv`: CSV formatında veri seti
- `Bilisim_Teknolojileri_Bloom_Sirali_FINAL.xlsx`: Excel formatında veri seti

## Kullanım Örnekleri

### Python ile Veri Yükleme

```python
import json
import pandas as pd

# JSON formatında yükleme
with open('Bilisim_Teknolojileri_Bloom_Sirali_FINAL.json', 'r', encoding='utf-8') as f:
    dataset = json.load(f)

# Pandas ile CSV yükleme
df = pd.read_csv('Bilisim_Teknolojileri_Bloom_Sirali_FINAL.csv', encoding='utf-8')

# Bloom seviyesine göre filtreleme
remembering_questions = [item for item in dataset if item['Bloom Seviyesi'] == 'Remembering']
understanding_applying = [item for item in dataset if item['Bloom Seviyesi'] == 'Understanding / Applying']
analyzing_evaluating = [item for item in dataset if item['Bloom Seviyesi'] == 'Analyzing / Evaluating']

print(f"Remembering: {len(remembering_questions)} soru")
print(f"Understanding/Applying: {len(understanding_applying)} soru")
print(f"Analyzing/Evaluating: {len(analyzing_evaluating)} soru")
```

### RAG Değerlendirme Örneği

```python
from sklearn.metrics.pairwise import cosine_similarity
import numpy as np

def evaluate_rag_response(ground_truth, generated_answer, embedding_model):
    """
    RAG sisteminin ürettiği cevabı ground truth ile karşılaştır
    """
    gt_embedding = embedding_model.encode(ground_truth)
    gen_embedding = embedding_model.encode(generated_answer)
    
    similarity = cosine_similarity(
        gt_embedding.reshape(1, -1), 
        gen_embedding.reshape(1, -1)
    )[0][0]
    
    return similarity

# Bloom seviyesine göre performans analizi
def analyze_by_bloom_level(results, dataset):
    bloom_levels = {}
    for item, result in zip(dataset, results):
        level = item['Bloom Seviyesi']
        if level not in bloom_levels:
            bloom_levels[level] = []
        bloom_levels[level].append(result['score'])
    
    for level, scores in bloom_levels.items():
        print(f"{level}: Ortalama Skor = {np.mean(scores):.3f}")
```

## Metodoloji

### Veri Toplama
Veri seti, Milli Eğitim Bakanlığı tarafından yayınlanan resmi bilişim teknolojileri ders kitabından derlenmiştir:

**Kaynak Doküman**: [Bilişim Teknolojileri Ders Kitabı (BT2025BTT920)](https://meslek.meb.gov.tr/upload/dersmateryali/pdf/BT2025BTT920.pdf)

Sorular, gerçek eğitim senaryolarını yansıtacak şekilde tasarlanmış ve kaynak dokümandan chunk'lara ayrılarak bağlam bilgisi ile eşleştirilmiştir.

### Kalite Kontrol
- Uzman değerlendirmesi ile Bloom seviyesi doğrulaması
- Ground truth cevapların kaynak bağlamla tutarlılık kontrolü
- Soru-cevap çiftlerinin anlamlılık ve netlik değerlendirmesi
- Tekrarlayan veya belirsiz soruların elenmesi

### Etik Hususlar
- Veri seti eğitim ve araştırma amaçlı kullanım için tasarlanmıştır
- Kişisel bilgi içermemektedir
- Kaynak materyal Milli Eğitim Bakanlığı tarafından kamuya açık olarak yayınlanmıştır
- Telif hakları ilgili eğitim materyallerine aittir

## Lisans ve Atıf

Bu veri seti akademik ve araştırma amaçlı kullanım için sunulmaktadır. Kullanımda aşağıdaki atıf yapılması rica olunur:

```bibtex
@dataset{bilisim_rag_dataset_2026,
  title={Bilişim Teknolojileri RAG Veri Seti: Bloom Taksonomisi ile Sınıflandırılmış Türkçe Soru-Cevap Çiftleri},
  author={Engin Dalga},
  year={2026},
  publisher={GitHub},
  url={https://github.com/EngindalgaMaku/Bilisim-Teknolojileri-Bloom-Dataset}
}
```

## Katkıda Bulunma

Veri setinin geliştirilmesine katkıda bulunmak için:
1. Hata bildirimleri için issue açın
2. Yeni soru önerileri için pull request gönderin
3. Bloom seviyesi sınıflandırma önerileri paylaşın

## İletişim

Sorularınız ve önerileriniz için:
- **GitHub**: [Engin Dalga](https://github.com/EngindalgaMaku)
- **GitHub Issues**: [Repository Issues](https://github.com/EngindalgaMaku/Bilisim-Teknolojileri-Bloom-Dataset/issues)
- **Email**: 2430131010@ogr.mehmetakif.edu.tr

## Sürüm Geçmişi

### v1.0.0 (Ocak 2026)
- İlk sürüm yayınlandı
- 100 soru-cevap çifti eklendi
- Bloom Taksonomisi sınıflandırması uygulandı
- JSON, CSV ve XLSX formatları sağlandı

---

**Not**: Bu veri seti sürekli geliştirilmektedir. Güncellemeler için repository'yi takip ediniz.
