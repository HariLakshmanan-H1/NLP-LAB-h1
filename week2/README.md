# 📘 Bigram Association Analysis using t-test and Chi-square (NLP)

This project demonstrates how **statistical hypothesis tests** can be applied to **Natural Language Processing (NLP)** for discovering **meaningful word associations (collocations)**.

It compares:

- **Manual statistical implementations**
- **NLTK’s out-of-the-box association measures**

and visualizes both **t-test** and **χ²-test** intuitively.

---

## 🎯 Objective

To answer the question:

> _Do two words occur together more often than expected by chance?_

Using:

- **Student’s t-test** → consistency against noise
- **Chi-square test (χ²)** → incompatibility with independence

---

## 🧠 Conceptual Intuition

| Test    | What it Measures            | Intuition |
| ------- | --------------------------- | --------- |
| t-test  | Signal vs noise             | 🎯 vs ☁️  |
| χ²-test | Surprise under independence | 😬² ÷ 📏  |

Both tests answer **different statistical questions**, so both are useful in NLP collocation discovery.

---

## 📂 Input Data

- Input file: **Excel (.xlsx)**
- Each row contains **one sentence**
- Example:

  ```
  Sastra University main campus
  Nuclear fission laboratory
  ```

---

## 🔄 Processing Pipeline

### 1️⃣ Data Loading

- Reads sentences from an Excel file
- Ignores empty or invalid rows

### 2️⃣ Text Preprocessing

- Lowercasing
- Punctuation removal
- Whitespace normalization
- Tokenization (NLTK `word_tokenize`)
- Sentence-level token preservation

### 3️⃣ Token Aggregation

- Flattens tokens into a single corpus
- Computes:
  - Word frequencies
  - Bigram frequencies
  - Trigram frequencies

---

## 📐 Statistical Measures Implemented

### ✅ Manual t-test (Bigram)

Based on **Bernoulli variance**:

[
t = \frac{\bar{x} - \mu}{\sqrt{\frac{s^2}{N}}}
]

Where:

- (\bar{x}) = observed bigram probability
- (\mu) = expected probability under independence
- (s^2 = \bar{x}(1-\bar{x}))
- (N) = total bigram positions

This version explicitly models **sampling variability**.

---

### ✅ Manual χ²-test (Bigram)

Uses a **2×2 contingency table**:

|     | w₂  | ¬w₂ |
| --- | --- | --- |
| w₁  | O₁₁ | O₁₂ |
| ¬w₁ | O₂₁ | O₂₂ |

[
\chi^2 = \sum \frac{(O - E)^2}{E}
]

Measures **how incompatible the observation is with independence**.

---

### 🧰 NLTK Out-of-the-Box Measures

The project also uses:

- `BigramCollocationFinder`
- `BigramAssocMeasures.student_t`
- `BigramAssocMeasures.chi_sq`

This allows **direct comparison** between:

- Hand-derived statistics
- Library implementations

---

## 📊 Output Report

A comparison table like:

| Bigram            | Frequency | Manual t | NLTK t | Manual χ² | NLTK χ² |
| ----------------- | --------- | -------- | ------ | --------- | ------- |
| sastra university | 32        | 5.25     | 5.09   | 303.13    | 303.13  |
| main campus       | 1         | 0.99     | 0.99   | 104.60    | 104.60  |

This confirms:

- Correctness of manual implementations
- Expected numerical agreement with NLTK

---

## 📈 Visualization

### 🔹 t-test Visualization

- Student’s t-distribution
- Observed bigram t-values plotted as vertical markers
- Critical value (α = 0.01) marked
- Acceptance and rejection regions shaded

Interpretation:

- Right tail → strong association
- Near zero → noise-level co-occurrence

---

### 🔹 χ²-test Visualization

- Chi-square distribution (df = 1)
- Observed χ² values overlaid
- Critical χ² threshold (3.84 for α = 0.05)
- Rejection region shaded

Interpretation:

- Large χ² → independence assumption collapses
- Small χ² → nothing surprising

---

## 🧪 Example Bigram Cases

| Bigram            | Interpretation              |
| ----------------- | --------------------------- |
| sastra university | Strong semantic collocation |
| main campus       | Moderate association        |
| nuclear fission   | Absent or unrelated         |

---

## 📦 Dependencies

Install the required libraries:

```bash
pip install pandas numpy nltk scipy matplotlib
```

Additionally, download NLTK resources:

```python
import nltk
nltk.download('punkt')
nltk.download('stopwords')
```

---

## 🧠 Who This Is For

- NLP students learning **statistical collocations**
- Anyone transitioning from **formulae → intuition**
- Researchers wanting **transparent implementations**
- Teaching demonstrations for hypothesis testing in NLP

---

## ✨ Key Takeaway

> **t-test asks:**
> “Is this co-occurrence consistently stronger than noise?”

> **χ²-test asks:**
> “How shocked should I be if independence were true?”

Using both gives a **complete statistical picture** of word association.

---

_Optional next steps:_

- PMI vs t vs χ² comparison
- Entropy-based association
- Collocation ranking dashboard
- Paper-ready methodology section
