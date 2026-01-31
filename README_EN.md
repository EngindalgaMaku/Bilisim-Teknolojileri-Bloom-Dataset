# Information Technologies RAG Dataset

[Türkçe](README.md) | **English**

## Overview

This dataset consists of Turkish question-answer pairs classified according to Bloom's Taxonomy, specifically designed for evaluating Retrieval-Augmented Generation (RAG) systems. The dataset is derived from educational materials in the field of information technologies and is designed to measure RAG system performance in multiple dimensions.

## Dataset Characteristics

### Statistics
- **Total Questions**: 100
- **Bloom Level Distribution**:
  - Remembering: 50 questions (50%)
  - Understanding / Applying: 30 questions (30%)
  - Analyzing / Evaluating: 20 questions (20%)
- **Language**: Turkish
- **Domain**: Information Technologies
- **Format**: JSON, CSV, XLSX

### Data Structure

Each data sample contains the following fields:

| Field | Description |
|-------|-------------|
| `ID` | Unique question identifier |
| `Soru` | User question |
| `İdeal Cevap (GT)` | Ground Truth - Reference answer |
| `Bağlam (Context)` | Source document context |
| `Bloom Seviyesi` | Bloom's Taxonomy classification |
| `Konu` | Question topic/category |
| `Chunk_ID` | Source chunk identifier |

## Bloom's Taxonomy Classification

The dataset is classified according to Bloom's Revised Taxonomy into three main cognitive levels:

1. **Remembering**: Recalling basic information and concepts, retrieving definitions and facts
2. **Understanding / Applying**: Making sense of concepts, explaining them, and applying knowledge in new situations
3. **Analyzing / Evaluating**: Breaking down information into parts, examining relationships, and making criterion-based judgments

This classification enables evaluation of RAG system performance across different cognitive levels, particularly allowing comparison between basic knowledge recall and higher-order cognitive skills.

### Rationale for Bloom Level Distribution

The Bloom level distribution in the dataset (50% Remembering, 30% Understanding/Applying, 20% Analyzing/Evaluating) is intentionally designed in a pyramid structure:

**1. Pedagogical Foundation**: The original structure of Bloom's Taxonomy is a pyramid where higher-level cognitive skills build upon lower-level skills. Students are expected to first recall basic information, then understand it, and finally perform analysis/evaluation. This distribution reflects this fundamental principle in educational sciences.

**2. Real-World Scenario**: By preserving the natural question distribution in the source educational material (Turkish Ministry of Education Information Technologies Textbook), we aim to more accurately measure RAG system performance in real educational environments. The question distribution students encounter in actual classroom settings reflects these proportions.

**3. Statistical Reliability**: Sufficient number of questions is provided for meaningful evaluation at each level. While 50 remembering questions enable comprehensive evaluation of basic retrieval capabilities, 20 analysis/evaluation questions have sufficient statistical power to test higher-order cognitive skills.

**4. Retrieval-Focused Evaluation**: More remembering questions are needed to comprehensively test the basic retrieval capabilities of RAG systems (finding the correct chunk, retrieving relevant context). This level best measures the system's fundamental functionality.

**5. Benchmark Compatibility**: Similar distributions are observed in RAG and question-answering benchmarks in the literature (SQuAD, Natural Questions, TriviaQA). This approach ensures our results are comparable with other studies.

## Use Cases

### 1. RAG System Evaluation
- Measuring retrieval quality
- Evaluating generation performance
- Comparing different embedding models
- Testing reranking strategies

### 2. Cognitive Level Analysis
- Analyzing RAG system success rates at different Bloom levels
- Identifying system strengths and weaknesses
- Measuring effectiveness of educational materials

### 3. Turkish NLP Research
- Evaluating Turkish language models
- Developing question-answering systems
- Semantic similarity studies

## Evaluation Metrics

The dataset enables evaluation with the following metrics:

### Retrieval Metrics
- **Precision@K**: Ratio of correct chunks in top K results
- **Recall@K**: Rate of finding relevant chunks
- **MRR (Mean Reciprocal Rank)**: Ranking of first correct result

### Generation Metrics
- **ROUGE-1, ROUGE-2, ROUGE-L**: N-gram and longest common subsequence overlap
- **BERTScore**: Semantic similarity measurement
- **Semantic Similarity**: Embedding-based similarity

### RAG-Specific Metrics
- **Context Relevance**: Context relevance
- **Answer Relevance**: Answer relevance
- **Faithfulness**: Faithfulness to context
- **Context Recall**: Context recall rate

## Dataset Formats

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

### Files
- `Bilisim_Teknolojileri_Bloom_Sirali_FINAL.json`: Dataset in JSON format
- `Bilisim_Teknolojileri_Bloom_Sirali_FINAL.csv`: Dataset in CSV format
- `Bilisim_Teknolojileri_Bloom_Sirali_FINAL.xlsx`: Dataset in Excel format

## Usage Examples

### Loading Data with Python

```python
import json
import pandas as pd

# Loading in JSON format
with open('Bilisim_Teknolojileri_Bloom_Sirali_FINAL.json', 'r', encoding='utf-8') as f:
    dataset = json.load(f)

# Loading CSV with Pandas
df = pd.read_csv('Bilisim_Teknolojileri_Bloom_Sirali_FINAL.csv', encoding='utf-8')

# Filtering by Bloom level
remembering_questions = [item for item in dataset if item['Bloom Seviyesi'] == 'Remembering']
understanding_applying = [item for item in dataset if item['Bloom Seviyesi'] == 'Understanding / Applying']
analyzing_evaluating = [item for item in dataset if item['Bloom Seviyesi'] == 'Analyzing / Evaluating']

print(f"Remembering: {len(remembering_questions)} questions")
print(f"Understanding/Applying: {len(understanding_applying)} questions")
print(f"Analyzing/Evaluating: {len(analyzing_evaluating)} questions")
```

### RAG Evaluation Example

```python
from sklearn.metrics.pairwise import cosine_similarity
import numpy as np

def evaluate_rag_response(ground_truth, generated_answer, embedding_model):
    """
    Compare RAG system generated answer with ground truth
    """
    gt_embedding = embedding_model.encode(ground_truth)
    gen_embedding = embedding_model.encode(generated_answer)
    
    similarity = cosine_similarity(
        gt_embedding.reshape(1, -1), 
        gen_embedding.reshape(1, -1)
    )[0][0]
    
    return similarity

# Performance analysis by Bloom level
def analyze_by_bloom_level(results, dataset):
    bloom_levels = {}
    for item, result in zip(dataset, results):
        level = item['Bloom Seviyesi']
        if level not in bloom_levels:
            bloom_levels[level] = []
        bloom_levels[level].append(result['score'])
    
    for level, scores in bloom_levels.items():
        print(f"{level}: Average Score = {np.mean(scores):.3f}")
```

## Methodology

### Data Collection
The dataset is compiled from the official information technologies textbook published by the Turkish Ministry of National Education:

**Source Document**: [Information Technologies Textbook (BT2025BTT920)](https://meslek.meb.gov.tr/upload/dersmateryali/pdf/BT2025BTT920.pdf)

Questions are designed to reflect real educational scenarios and matched with context information by dividing the source document into chunks.

### Quality Control
- Bloom level validation through expert evaluation
- Consistency check of ground truth answers with source context
- Meaningfulness and clarity evaluation of question-answer pairs
- Elimination of repetitive or ambiguous questions

### Ethical Considerations
- Dataset is designed for educational and research purposes
- Contains no personal information
- Source material is publicly published by the Ministry of National Education
- Copyrights belong to the relevant educational materials

## License and Citation

This dataset is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](LICENSE).

### Terms of Use
- ✅ You can use it for commercial and academic purposes
- ✅ You can modify and distribute the dataset
- ⚠️ You must provide attribution when using

### Citation Format

Please cite as follows when using:

```bibtex
@dataset{bilisim_rag_dataset_2026,
  title={Information Technologies RAG Dataset: Turkish Question-Answer Pairs Classified with Bloom's Taxonomy},
  author={Engin Dalga},
  year={2026},
  publisher={GitHub},
  url={https://github.com/EngindalgaMaku/Bilisim-Teknolojileri-Bloom-Dataset}
}
```

## Contributing

To contribute to the development of the dataset:
1. Open an issue for bug reports
2. Submit pull requests for new question suggestions
3. Share Bloom level classification suggestions

## Contact

For questions and suggestions:
- **GitHub**: [Engin Dalga](https://github.com/EngindalgaMaku)
- **GitHub Issues**: [Repository Issues](https://github.com/EngindalgaMaku/Bilisim-Teknolojileri-Bloom-Dataset/issues)
- **Email**: 2430131010@ogr.mehmetakif.edu.tr

## Version History

### v1.0.0 (January 2026)
- Initial release
- 100 question-answer pairs added
- Bloom's Taxonomy classification applied
- JSON, CSV, and XLSX formats provided

---

**Note**: This dataset is continuously being developed. Follow the repository for updates.
