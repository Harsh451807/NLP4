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


## 📋 Pipeline Flow

```mermaid
graph TD
    A[📁 Raw CSV Data - Kaggle IMDB 50K] --> B[🧹 Data Preprocessing]
    B --> C[✂️ Data Splitting]
    C --> D[🔤 Tokenization]
    D --> E[🧠 Model Training]
    E --> F[📊 Evaluation]
    F --> G[📈 Comparison & Analysis]

    B --> |HTML removal, cleaning, lowercase| B
    C --> |70% Train / 15% Val / 15% Test| C
    D --> |bert-base-uncased, MAX_LEN=256| D
    E --> |4 Experiments| E
    F --> |Accuracy, Precision, Recall, F1, Confusion Matrix| F
Step	Process	Details
1️⃣	Raw Data	Kaggle IMDB CSV (50K reviews)
2️⃣	Preprocessing	HTML removal, URL removal, lowercase, clean special characters
3️⃣	Data Splitting	70% Train / 15% Validation / 15% Test (Stratified)
4️⃣	Tokenization	bert-base-uncased tokenizer, MAX_LEN=256
5️⃣	Model Training	4 Experiments (Full, Frozen, Last 2 Layers, DistilBERT)
6️⃣	Evaluation	Accuracy, Precision, Recall, F1 Score, Confusion Matrix
7️⃣	Comparison	Side-by-side analysis of all experiments
🔍 Sample Predictions
Predictions made using the best model (Experiment 1: Full Fine-Tuning)

#	Review	Prediction	Confidence	Note
1	"This movie was absolutely wonderful! The acting was superb."	✅ POSITIVE	99.7%	Clear positive sentiment
2	"Terrible film. Waste of time. Awful plot and bad acting."	❌ NEGATIVE	99.8%	Clear negative sentiment
3	"An okay movie, nothing special but watchable."	✅ POSITIVE	57.5%	⚠️ Model correctly shows uncertainty on mixed review
4	"A masterpiece! Best film I have ever seen in my life."	✅ POSITIVE	99.7%	Strong positive sentiment
5	"Extremely boring. I fell asleep halfway through."	❌ NEGATIVE	99.6%	Clear negative sentiment
