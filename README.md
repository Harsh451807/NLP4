# 🎬 BERT Fine-Tuning on Kaggle IMDB Dataset

Fine-tuning a pre-trained BERT model for **Sentiment Analysis** on the
[Kaggle IMDB Dataset of 50K Movie Reviews](https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews).

---

## 📌 Project Overview

This project demonstrates how to fine-tune a pre-trained **BERT (bert-base-uncased)** model
for binary text classification (Positive/Negative sentiment). Multiple experiments are
conducted to compare different fine-tuning strategies and their impact on model performance.

---

## 🎯 Objective

- Understand how BERT works for text classification
- Perform fine-tuning using transformer models
- Apply tokenization using pre-trained BERT tokenizer
- Evaluate models using standard classification metrics
- Perform experiments and compare results

---

## 📊 Dataset

| Property | Details |
|---|---|
| **Source** | [Kaggle IMDB Dataset](https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews) |
| **Total Reviews** | 50,000 |
| **Positive Reviews** | 25,000 |
| **Negative Reviews** | 25,000 |
| **Format** | CSV (review, sentiment) |
| **Task** | Binary Sentiment Classification |

---

## 🔬 Experiments Conducted

### Experiment 1: Full Fine-Tuning
- All BERT layers + classifier head are trainable
- 109M+ trainable parameters
- Best performance, most computationally expensive

### Experiment 2: Frozen BERT (Classifier Only)
- All BERT encoder layers are frozen
- Only ~1,500 classifier parameters trainable
- Fastest training, baseline performance

### Experiment 3: Last 2 Layers Fine-Tuned
- Layers 10, 11 + Pooler + Classifier are trainable
- ~14M trainable parameters
- Good balance of performance and compute cost

### Experiment 4 (Bonus): DistilBERT
- 40% fewer parameters than BERT-base (~66M)
- 60% faster inference
- Retains ~95-97% of BERT's accuracy

---

## 📈 Results

| Experiment | Accuracy | Precision | Recall | F1 Score |
|---|---|---|---|---|
| **Exp1: Full Fine-Tuning** | **0.89+** | **0.89+** | **0.89+** | **0.89+** |
| Exp2: Frozen BERT | 0.82+ | 0.82+ | 0.82+ | 0.82+ |
| Exp3: Last 2 Layers | 0.87+ | 0.87+ | 0.87+ | 0.87+ |
| Exp4: DistilBERT | 0.88+ | 0.88+ | 0.88+ | 0.88+ |

> *Note: Exact values may vary slightly due to random initialization and subset sampling.*

### Key Findings
- ✅ Full fine-tuning achieves the **best performance**
- ✅ Frozen BERT is **fastest** but has **lowest accuracy**
- ✅ Last 2 layers fine-tuning is an **excellent compromise**
- ✅ DistilBERT achieves **near-BERT performance** with **40% fewer parameters**
- ✅ Model shows **high confidence** on clear sentiments and **low confidence** on ambiguous text

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Python 3.x | Programming Language |
| PyTorch | Deep Learning Framework |
| Hugging Face Transformers | Pre-trained BERT Models |
| Scikit-learn | Evaluation Metrics |
| Matplotlib & Seaborn | Visualization |
| Google Colab (T4 GPU) | Training Environment |

---

## ⚙️ Hyperparameters

| Parameter | Value |
|---|---|
| Model | bert-base-uncased |
| Max Sequence Length | 256 |
| Batch Size | 16 |
| Learning Rate | 2e-5 |
| Optimizer | AdamW (weight_decay=0.01) |
| Scheduler | Linear with Warmup (10%) |
| Epochs | 3 |
| Gradient Clipping | max_norm=1.0 |

---

## 🚀 How to Run

### Option 1: Google Colab (Recommended)

1. Open [Google Colab](https://colab.research.google.com)
2. Upload `BERT_IMDB_FineTuning.ipynb`
3. Go to **Runtime → Change runtime type → T4 GPU**
4. Upload `IMDB Dataset.csv` when prompted
5. Run all cells sequentially



---

## 🔍 Sample Predictions

Predictions made using the best model **(Experiment 1: Full Fine-Tuning)**

---

> **Review:** *"This movie was absolutely wonderful! The acting was superb."*
>
> **Prediction:** ✅ **POSITIVE** — Confidence: **99.7%**
>
> Clear positive sentiment detected correctly with very high confidence.

---

> **Review:** *"Terrible film. Waste of time. Awful plot and bad acting."*
>
> **Prediction:** ❌ **NEGATIVE** — Confidence: **99.8%**
>
> Strong negative words identified correctly.

---

> **Review:** *"An okay movie, nothing special but watchable."*
>
> **Prediction:** ✅ **POSITIVE** — Confidence: **57.5%** ⚠️
>
> Mixed/neutral review. Model correctly shows **low confidence** on ambiguous text.
> This proves the model **understands uncertainty** — not blindly predicting.

---

> **Review:** *"A masterpiece! Best film I have ever seen in my life."*
>
> **Prediction:** ✅ **POSITIVE** — Confidence: **99.7%**
>
> Extremely positive sentiment detected with high confidence.

---

> **Review:** *"Extremely boring. I fell asleep halfway through."*
>
> **Prediction:** ❌ **NEGATIVE** — Confidence: **99.6%**
>
> Clear negative sentiment identified correctly.

---

