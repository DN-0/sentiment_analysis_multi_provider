# sentiment_analysis_multi_provider

# Multi-Backend Sentiment Analysis (HuggingFace • OpenAI • Ollama)

This project compares three different approaches for **5-class sentiment analysis** on the Kaggle dataset  
**“Sentiment Analysis on Movie Reviews”**:

- **Hugging Face Transformers** (DistilBERT SST-5 model)
- **OpenAI LLMs** (via few-shot prompting)
- **Ollama Local LLMs** (e.g., Llama3/Mistral)

All backends output labels in the Kaggle format:

```
0 = negative  
1 = somewhat negative  
2 = neutral  
3 = somewhat positive  
4 = positive
```

---

## 📂 Project Structure

```
.
├── README.md
├── requirements.txt
├── main.py
├── data/
│   └── train.tsv
├── adapters/
│   ├── hf_adapter.py
│   ├── openai_adapter.py
│   └── ollama_adapter.py
├── notebooks/
│   └── Sentiment_Comparison.ipynb
├── utils/
│   └── evaluation.py
└── outputs/
    └── results.csv
```

---

## 🚀 Installation

Clone the repository:

```bash
git clone <your-repo-url>
cd sentiment-multi-backend
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## 📦 Dataset Setup

Download the competition dataset:

**Sentiment Analysis on Movie Reviews**  
https://www.kaggle.com/competitions/sentiment-analysis-on-movie-reviews/data

Place the file here:

```
data/train.tsv
```

---

## 🔌 Backend Setup

### Hugging Face  
No additional setup needed.

### OpenAI  
Set your API key:

```bash
export OPENAI_API_KEY="your-key"
```

### Ollama  
Install from: https://ollama.com

Run the server:

```bash
ollama serve
```

Pull a model:

```bash
ollama pull llama3
```

---

## 🧠 How Backends Work

All backends expose the same function:

```python
predict_label_id(text: str) -> int
```

This makes the pipeline interchangeable.

**Hugging Face:**  
- Uses a real 5-class DistilBERT SST-5 classifier  
- Predicts via logits → argmax → label  

**OpenAI and Ollama:**  
- Use the same few-shot prompt  
- Output text (e.g. “2”) which is parsed into labels  

---

## 🧪 Running Experiments

### Run the main script

```bash
python main.py --provider all
```

Options:

```
--provider hf
--provider openai
--provider ollama
--provider all
```

### Run the notebook

```bash
jupyter notebook notebooks/Sentiment_Comparison.ipynb
```

Set inside the notebook:

```python
PROVIDER = "hf"  # or "openai", "ollama", "all"
```

---

## 📊 Outputs

You will get:

- Accuracy  
- Confusion matrix  
- Seconds per sample  
- Cache hit rates (for LLMs)  
- Comparison table (saved in `outputs/`)  

PDF summaries can also be generated using ReportLab.

---

## 📌 Backend Comparison (Quick Summary)

| Aspect | Hugging Face | OpenAI | Ollama |
|-------|--------------|--------|--------|
| Runs locally | ✔️ | ❌ | ✔️ |
| Uses 5-class classifier | ✔️ | ❌ | ❌ |
| Accuracy | Good | ⭐ Best | Medium-Good |
| Internet needed | No | Yes | No |
| Cost | Free | Token-based | Free |
| Speed | Fast | Medium | Slower |
| Best for | Reliable, local inference | Highest reasoning | Offline workflows |

---

## 🙋 Improvements & Ideas

Planned enhancements:

- Error analysis notebook  
- Optional model fine-tuning  
- Confusion matrix heatmaps  
- GitHub Actions workflow for automated testing



---
