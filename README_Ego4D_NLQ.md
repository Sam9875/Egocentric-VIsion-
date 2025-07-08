# 🎩 Natural Language Queries in Egocentric Videos (Ego4D NLQ)

This project explores **natural language query (NLQ) grounding in egocentric videos** using the **Ego4D dataset** and the **VSLNet architecture**. It supports both baseline models and extended approaches leveraging **LLMs/VLMs** for enhanced performance.

---

## 📁 Project Structure

| File | Description |
|------|-------------|
| `main.py` | Core pipeline for training and evaluation |
| `VSLNet.py` | Definitions for VSLBase and VSLNet models |
| `data_loader.py` | Data loading and preprocessing routines |
| `data_gen.py` | Converts datasets and creates vocab/embeddings |
| `layers.py` | Core model components (encoders, attention, prediction layers) |

✅ **Note:** This implementation uses **BERT embeddings** for improved contextual understanding (replacing GloVe).

---

## 🎯 Project Objective

Given a **natural language query** and a **video from the Ego4D dataset**, the goal is to **localize the segment** of the video that best answers the query.

### Example Queries:
- 🗣️ *“Where was the phone last seen?”*
- 🗣️ *“How many frying pans can I see on the shelf?”*

The project follows the **Ego4D NLQ benchmark** and implements:
- Baselines using **VSLBase/VSLNet**
- Feature extractors: **Omnivore** and **EgoVLP**
- **Extension**: Generating **textual answers** from localized segments using **Video-LLaVA**

---

## ⚙️ Installation

Install the required dependencies:

```bash
pip install torch transformers submitit nltk tqdm
```

Add any additional packages as needed (especially if using Jupyter notebooks).

---

## 📦 Dataset Setup

1. **Request access** and agree to the [Ego4D license](https://ego4d-data.org).
2. **Download** annotations and video features:

```bash
ego4d --download-annotations nlq
ego4d --download-features omnivore_video_swinl_fp16
```

3. **Organize your files** as follows:

```
data/
├── features/
│   └── <task>/<feature_version>/
└── dataset/
    └── <task>/
        ├── train.json
        ├── val.json
        └── test.json
```

💡 *You can skip downloading if you already have the preprocessed features.*

---

## 🚀 Running the Model

### 🏋️ Training

```bash
python main.py     --mode train     --task ego4d     --fv omnivore     --max_pos_len 128     --predictor rnn     --epochs 10     --batch_size 32
```

Adjust `--batch_size` based on your hardware.

### 🧪 Evaluation

```bash
python main.py     --mode test     --task ego4d     --fv omnivore     --predictor rnn
```

📌 *Default text embedding uses BERT. Use `--predictor glove` if you'd prefer GloVe.*

Use **TensorBoard** to monitor loss curves:

```bash
tensorboard --logdir=runs
```

---

## 🔁 Extension: From Segment to Answer

After retrieving the relevant **video clip via NLQ**, we pass the **query + segment** into **Video-LLaVA** to generate a **natural language answer**.

This bridges **temporal localization** and **video question answering (VideoQA)** in a unified pipeline.

---

## 📊 Results

Performance is evaluated via:

- 🧭 **Recall@K** at various tIoU thresholds (for localization)
- 📝 **ROUGE / BLEU** scores (for textual answer generation)

---

## 📓 Jupyter Notebooks

Notebooks are included for:
- Exploratory data analysis
- Feature visualization
- Query-based qualitative results
- Training and evaluation walkthroughs

---

## 📚 References

- Ego4D Dataset — *Grauman et al., 2022*
- VSLNet — *Zhang et al., 2020*
- Omnivore — *Girdhar et al., 2022*
- EgoVLP — *Lin et al., 2022*
- Video-LLaVA — *Lin et al., 2023*

> ⚠️ Some implementation insights were inspired by community codebases, research papers, and large language models.

---

## 🙏 Acknowledgements

Developed as part of the **Egocentric Video Understanding** course under the guidance of:

- **Simone Alberto Peirone**
- **Gaetano Salvatore Falco**
