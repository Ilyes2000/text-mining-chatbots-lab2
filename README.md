# Text Mining and Chatbots  Lab 2  
## Lemmatization and Byte Pair Encoding (BPE)

This repository contains the complete implementation and report for **Lab 2** of the course **Text Mining and Chatbots** (Université Paris-Saclay).

The objective of this laboratory is twofold:
1. To design and evaluate **custom lemmatizers for French**
2. To implement the **Byte Pair Encoding (BPE)** algorithm for subword tokenization

All experiments, evaluations, and analyses strictly follow the instructions provided by the course instructor.

---

## Authors

- **Ilyes SAIS** – ilyes.sais@universite-paris-saclay.fr  
- **Wenchong PAN** – wenchong.pan@universite-paris-saclay.fr  
- **Quaisar Muhammad** – muhammad.qaisar@universite-paris-saclay.fr  

---

## Lab Objectives

### Part 1 – Lemmatization
- Implement multiple French lemmatization approaches:
  - Dictionary-based lemmatizer
  - Machine learning lemmatizer (character-level)
  - spaCy lemmatizer (baseline)
- Compare performance:
  - With and without Part-of-Speech (PoS) information
- Evaluate models on:
  - In-domain test set
  - Out-of-domain historical **Gallica** dataset
- Analyze robustness and domain generalization

### Part 2 – Byte Pair Encoding (BPE)
- Implement the BPE algorithm from scratch
- Learn subword merge rules from a corpus
- Apply learned merges to tokenize new text
- Analyze vocabulary growth and tokenization behavior

---

---

## Lemmatization Approaches

### 1. Dictionary-Based Lemmatizer
- Builds a lookup table from the training set
- Two configurations:
  - Token → Lemma
  - (Token, PoS) → Lemma
- Fast and highly accurate on in-domain data
- Produces `UNK` for unseen tokens

### 2. Machine Learning Lemmatizer
- Character-level n-gram representation
- Multinomial Logistic Regression classifier
- Two configurations:
  - Without PoS
  - With PoS concatenated to the token
- Learns morphological regularities
- Limited by lemma vocabulary seen during training

### 3. spaCy Lemmatizer (Baseline)
- Uses `fr_core_news_sm`
- Rule-based + statistical lemmatization
- No task-specific training required

---

## 📊 Evaluation Results

| Method                | PoS Used | Test Accuracy | Gallica Accuracy |
|----------------------|----------|---------------|------------------|
| Dictionary-based     | No       | 0.94          | 0.00             |
| Dictionary-based     | Yes      | **0.95**      | 0.00             |
| ML (char n-grams)    | No       | 0.50          | 0.00             |
| ML (char n-grams)    | Yes      | 0.85          | 0.00             |
| spaCy baseline       | No       | 0.82          | 0.00             |

---

## Why is Gallica Accuracy 0?

The **Gallica dataset** contains historical French text with:
- Archaic spelling variants
- Obsolete morphological forms
- Latin tokens and mixed-language content
- Strong orthographic divergence from modern French

None of the lemmatizers were trained on historical French.
As a result:
- Most tokens are unseen during training
- Dictionary-based methods return `UNK`
- ML models cannot generalize to archaic forms
- Exact-match evaluation yields an accuracy of 0

This highlights the importance of **domain adaptation** in lemmatization.

---

## Byte Pair Encoding (BPE)

- Character-level vocabulary initialization
- Iterative merging of most frequent adjacent pairs
- Merge rules learned from corpus statistics
- Applied consistently to tokenize unseen words
- Fully implemented following Sennrich et al. (2016)



