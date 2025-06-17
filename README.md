# Egocentric-VIsion-Natural Language Queries in Egocentric Videos (Ego4D NLQ)
This project focuses on answering natural language queries from egocentric videos, leveraging the Ego4D dataset and the VSLNet architecture. It supports both baseline training and extended methods such as using LLMs or VLMs for improved performance.

📁 Project Structure
main.py — Core training and evaluation pipeline.

VSLNet.py — VSLNet and VSLBase model definitions.

data_loader.py — Data loading and preprocessing routines.

data_gen.py — Dataset conversion and vocabulary/embedding creation.

layers.py — Model architecture components (encoders, attention, predictors, etc.).

✅ All models were trained on different sets of video features (Omnivore and EgoVLP).

🎯 Project Objective
Given a natural language query and a video from the Ego4D dataset, the task is to localize the segment of the video that answers the query.

Examples:

"Where was the phone last seen?"

"How many frying pans can I see on the shelf?"

The project follows the Ego4D NLQ benchmark and implements VSLBase and VSLNet, trained on pre-extracted features using Omnivore and EgoVLP.

⚙️ Installation
Install the necessary libraries:

bash
Copy
Edit
pip install torch transformers submitit nltk tqdm
Add any additional dependencies used in your Jupyter notebooks as needed.

📦 Dataset Setup
Request access to the Ego4D dataset and sign the data agreement here.

Download annotations and features via Ego4D CLI (optional if already available):

bash
Copy
Edit
ego4d --download-annotations nlq
ego4d --download-features omnivore_video_swinl_fp16
Organize the files in this structure:

php-template
Copy
Edit
data/
├── features/
│   └── <task>/<feature_version>/
└── dataset/
    └── <task>/
        ├── train.json
        ├── val.json
        └── test.json
🔑 We used pre-downloaded features; you may skip downloading if you have access.

🚀 Running the Model
🔧 Training
bash
Copy
Edit
python main.py \
    --mode train \
    --task ego4d \
    --fv omnivore \
    --max_pos_len 128 \
    --predictor rnn \
    --epochs 10 \
    --batch_size 32
Adjust --batch_size according to your system and the feature type.

🧪 Evaluation
bash
Copy
Edit
python main.py \
    --mode test \
    --task ego4d \
    --fv omnivore \
    --predictor rnn
📈 Optionally, enable TensorBoard to visualize training loss over time.

🧩 Extension
We implemented Proposal 2: From video interval to a textual answer.

After retrieving the correct video segment with NLQ, we used Video-LLaVA to generate direct textual answers based on the localized clip and the query.

📊 Results
Performance is evaluated using:

Recall@k at multiple tIoU thresholds (baseline)

ROUGE / BLEU metrics (for textual answers in the extension)

📓 Notebooks
Jupyter notebooks are provided for:

Exploratory data analysis

Feature visualization

Query-based qualitative result inspection

Training/evaluation workflows

📚 References
Ego4D Dataset — Grauman et al., 2022

VSLNet — Zhang et al., 2020

Omnivore — Girdhar et al., 2022

EgoVLP — Lin et al., 2022

Video-LLaVA — Lin et al., 2023

🙏 Acknowledgements
This project was developed for the Egocentric Video Understanding course, with guidance from:

Simone Alberto Peirone

Gaetano Salvatore Falco
